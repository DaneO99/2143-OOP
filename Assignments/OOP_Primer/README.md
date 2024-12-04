#### OOP Terminology

## Abstract Classes:
These are classes that cannot be instantiated on their own and are typically used as base classes. They contain at least one pure virtual function, which forces derived classes to provide an implementation for these functions, thus implementing specific behaviors.
```cpp
class AbstractAnimal {
public:
    virtual void Speak() = 0; // Pure virtual function
};
```
## Interfaces:
In C++, an interface can be simulated using a class where all methods are pure virtual. Interfaces define a set of methods that derived classes must implement, ensuring a consistent API regardless of the specific object's type.
```cpp
class Interface {
public:
    virtual void method() = 0;
};
```
## Abstraction:
Abstraction involves hiding the complex reality while exposing only the necessary parts of an object. It helps in reducing programming complexity and increasing efficiency.
```cpp
class Car {
public:
    void startEngine() {
        igniteSparkPlug();
        injectFuel();
    }
private:
    void igniteSparkPlug() {}
    void injectFuel() {}
};
```
## Access Modifiers:
These keywords control how members (variables, methods) of a class can be accessed.
# Public: 
Members are accessible from any part of the program.
# Private: 
Members cannot be accessed (or viewed) from outside the class.
# Protected: 
Members cannot be accessed from outside the class, except by inherited classes.
## Attributes/Properties:
These are data members of a class that hold data specific to an object and define its state. Properties can have public, protected, or private visibility.
```cpp
class Rectangle {
private:
    double width;
    double height;
public:
    Rectangle(double w, double h) : width(w), height(h) {}
};
```
## Class Variables:
These are static members of a class, shared among all instances of the class. They represent global properties of a class.
```cpp
class Account {
public:
    static int TotalAccounts;
};
int Account::TotalAccounts = 0;
```
## Classes and Objects:
A class is a blueprint for creating objects (a particular data structure), providing initial values for state (member variables) and implementations of behavior (member functions or methods). An object is an instance of a class.
```cpp
class Dog {
public:
    void bark() {}
};

Dog myDog;  // Creating an object
myDog.bark();
```
## Collections and Iterators:
Collections are data structures that hold objects. Iterators are used to navigate through collections.
```cpp
#include <vector>

std::vector<int> vec = {1, 2, 3, 4};
for(auto it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << std::endl;
}
```
## Compostion:
A design principle where a class includes instances of other classes inside itself to provide enhanced functionality. This differs from inheritance and is often used to express a "has-a" relationship.
```cpp
class Engine {
};

class Car {
private:
    Engine engine; // Car contains an Engine
};
```
## Constructors and Destructors:
Constructors are special class functions which are executed whenever a new object of that class is created. They generally initialize the attributes of the new object. Destructors are special functions executed when an object is destroyed or deleted. They are used to perform cleanup before the object is deallocated.
```cpp
class Example {
public:
    Example() { std::cout << "Created\n"; }
    ~Example() { std::cout << "Destroyed\n"; }
};
```
## Encapsulation:
The act of restricting access to some of the object's components, which means that the internal representation of an object is generally hidden from view outside of the object’s definition. Access to the data and methods is tightly controlled by an interface.
```cpp
class EncapsulatedObject {
private:
    int x;
public:
    void setX(int i) { x = i; }
    int getX() { return x; }
};
```
## Exception Handiling:
Mechanism to handle runtime errors, providing a way to react to exceptional circumstances (like runtime errors) in programs by transferring control to special functions called handlers.
```cpp
try {
    throw std::runtime_error("Something went wrong");
} catch (const std::exception& e) {
    std::cout << e.what() << std::endl;
}
```
## Generics and Templates:
Templates in C++ are a powerful feature that allows you to write generic programs that work with any data type. It enables the creation of functions and classes that can work with any data type without being rewritten for each type.
```cpp
template <typename T>
class Box {
private:
    T content;
public:
    void setContent(T newContent) { content = newContent; }
    T getContent() { return content; }
};
```
## Inheritance:
It is a mechanism wherein a new class is derived from an existing class. The derived class inherits all the features from the base class, adding new features or modifying existing ones.
```cpp
class Animal {
public:
    void eat() {}
};

class Dog : public Animal {
public:
    void bark() {}
};
```
## Method Overloading:
This involves having multiple methods in the same scope, with the same name but different parameters.
```cpp
class Print {
public:
    void show(int i) { std::cout << i << std::endl; }
    void show(double f) { std::cout << f << std::endl; }
};
```
## Polymorphism:
The ability of a message to be displayed in more than one form. A person at the same time can have different characteristics. Similarly, a method in a child class can have a different implementation than a method in the parent class, which it overrides.
```cpp
class Animal {
public:
    virtual void makeSound() { std::cout << "Some sound\n"; }
};

class Cat : public Animal {
public:
    void makeSound() override { std::cout << "Meow\n"; }
};
```
## Static(Methods and Variables):
Static variables are used to store common data across all class instances, and static methods are accessed without creating an instance of the class.
```cpp
class Math {
public:
    static int add(int x, int y) { return x + y; }
};

int result = Math::add(5, 3); // No instance of Math needed
```
## UML Diagrams and Modeling:
UML (Unified Modeling Language) is a standardized modeling language enabling developers to specify, visualize, construct, and document artifacts of software systems, as well as for business modeling. UML diagrams represent classes, objects, interfaces, and their relationships.
