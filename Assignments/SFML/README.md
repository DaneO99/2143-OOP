## SFML KnuckleBones Project
# main.cpp
```cpp
#include <SFML/Graphics.hpp>
#include "Game.h"
#include <iostream>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "KnuckleBones Game");
    Game game;

    // Initialize players with names
    std::string name1, name2;
    std::cout << "Enter name for Player 1: ";
    std::cin >> name1;
    std::cout << "Enter name for Player 2: ";
    std::cin >> name2;

    game.initialize(name1, name2);

    while (window.isOpen()) {
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
            game.handleEvent(event, window);
        }

        window.clear(sf::Color::Black); // Clear the screen with black color
        game.draw(window);              // Draw the game state
        window.display();               // Display what was drawn to the screen
    }

    return 0;
}

```
# Dice.h
```cpp
#pragma once
#include <SFML/Graphics.hpp>
#include <cstdlib>  // For std::rand()

class Dice {
    sf::Texture textures[6];  // Textures for dice faces 1-6
    sf::Sprite sprite;        // Sprite to display the current dice face
    int currentFace = 0;      // Current dice face index

public:
    Dice();
    void loadTextures();              // Load textures for dice faces
    void roll();                      // Start rolling the dice
    void draw(sf::RenderWindow& window); // Draw the dice
    int getValue() const;             // Get the current value of the dice
    void setPosition(float x, float y); // Set position of the dice sprite
};

```
# Dice.cpp
```cpp
#include "Dice.h"
#include <ctime>    // For std::time()

Dice::Dice() {
    std::srand(std::time(nullptr));  // Seed the random number generator
    loadTextures();
    sprite.setTexture(textures[0]);  // Set the first texture
    sprite.setPosition(400, 50);  // Set initial position
}

void Dice::loadTextures() {
    for (int i = 0; i < 6; i++) {
        if (!textures[i].loadFromFile("resources/dice_" + std::to_string(i + 1) + ".png")) {
            throw std::runtime_error("Failed to load dice texture");
        }
    }
}

void Dice::roll() {
    currentFace = std::rand() % 6;  // Generate a new face index
    sprite.setTexture(textures[currentFace]);
}

void Dice::draw(sf::RenderWindow& window) {
    window.draw(sprite);
}

int Dice::getValue() const {
    return currentFace + 1;  // Return the actual dice value (1-6)
}

void Dice::setPosition(float x, float y) {
    sprite.setPosition(x, y);
}

```
# Grid.h
```cpp
#pragma once
#include <SFML/Graphics.hpp>
#include <array>
#include <vector>

class Grid {
    std::array<std::vector<int>, 3> columns;  // Each column can hold up to 3 dice
    sf::Font font;
    sf::Vector2f position;
    float cellSize = 100.0f;  // Size of each grid cell

public:
    Grid(const sf::Vector2f& pos);
    bool placeDice(int col, int value);
    void draw(sf::RenderWindow& window);
    int calculateScore() const;  // Calculate total score for the grid
};

```
# Grid.cpp
```cpp
#include "Grid.h"
#include <sstream>

Grid::Grid(const sf::Vector2f& pos) : position(pos) {
    if (!font.loadFromFile("resources/Arial.ttf")) {
        throw std::runtime_error("Failed to load font");
    }
}

bool Grid::placeDice(int col, int value) {
    if (columns[col].size() < 3) {
        columns[col].push_back(value);
        return true;
    }
    return false;
}

void Grid::draw(sf::RenderWindow& window) {
    for (int col = 0; col < 3; ++col) {
        for (size_t row = 0; row < columns[col].size(); ++row) {
            sf::RectangleShape cell(sf::Vector2f(cellSize, cellSize));
            cell.setPosition(position.x + col * cellSize, position.y + row * cellSize);
            cell.setFillColor(sf::Color::White);
            cell.setOutlineColor(sf::Color::Black);
            cell.setOutlineThickness(1);

            sf::Text text(std::to_string(columns[col][row]), font, 24);
            text.setFillColor(sf::Color::Black);
            text.setPosition(cell.getPosition().x + 10, cell.getPosition().y + 10);
            window.draw(cell);
            window.draw(text);
        }
    }
}

int Grid::calculateScore() const {
    int totalScore = 0;
    for (const auto& col : columns) {
        std::map<int, int> counts;  // Count occurrences of each dice value (1-6)
        for (int num : col) {
            counts[num]++;
        }
        for (auto& pair : counts) {
            totalScore += pair.first * pair.second * pair.second; // Value * count^2
        }
    }
    return totalScore;
}

```
# Player.h
```cpp
#pragma once
#include "Grid.h"
#include <string>

class Player {
    std::string name;
    Grid grid;

public:
    Player(const std::string& n, const sf::Vector2f& gridPos);
    void placeDice(int col, int diceValue);
    void draw(sf::RenderWindow& window);
    int getScore() const;
    std::string getName() const;
};

```
# Player.cpp
```cpp
#include "Player.h"

Player::Player(const std::string& n, const sf::Vector2f& gridPos) : name(n), grid(gridPos) {}

void Player::placeDice(int col, int diceValue) {
    grid.placeDice(col, diceValue);
}

void Player::draw(sf::RenderWindow& window) {
    grid.draw(window);
}

int Player::getScore() const {
    return grid.calculateScore();
}

std::string Player::getName() const {
    return name;
}

```
# Game.h
```cpp
#pragma once
#include "Player.h"
#include "Dice.h"
#include <SFML/Graphics.hpp>

class Game {
    Player player1, player2;
    Dice dice;
    Player* currentPlayer;

public:
    Game();
    void initialize(const std::string& name1, const std::string& name2);
    void handleEvent(sf::Event& event, sf::RenderWindow& window);
    void draw(sf::RenderWindow& window);
    void switchPlayer();
    bool checkGameOver() const;
};

```
# Game.cpp
```cpp
#include "Game.h"

Game::Game() : currentPlayer(&player1) {}

void Game::initialize(const std::string& name1, const std::string& name2) {
    player1 = Player(name1, sf::Vector2f(50, 150));
    player2 = Player(name2, sf::Vector2f(450, 150));
    dice.setPosition(350, 50);  // Central position for the dice
}

void Game::handleEvent(sf::Event& event, sf::RenderWindow& window) {
    if (event.type == sf::Event::KeyPressed) {
        // Allow user to roll dice and select column using the number keys
        if (event.key.code >= sf::Keyboard::Num1 && event.key.code <= sf::Keyboard::Num3) {
            int col = event.key.code - sf::Keyboard::Num1;  // Convert key code to column index
            dice.roll();
            bool success = currentPlayer->placeDice(col, dice.getValue());
            if (success) {
                switchPlayer();  // Change turn after successful placement
            }
        }
    }
}

void Game::draw(sf::RenderWindow& window) {
    player1.draw(window);
    player2.draw(window);
    dice.draw(window);
}

void Game::switchPlayer() {
    currentPlayer = (currentPlayer == &player1) ? &player2 : &player1;
}

bool Game::checkGameOver() const {
    // Implement the logic to check if all columns are filled
    return false;
}

```
