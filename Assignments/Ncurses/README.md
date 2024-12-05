```cpp
#include <ncurses.h>

int main() {
    initscr(); // Start curses mode
    printw("Hello, world!"); // Print Hello, world! to the window
    refresh(); // Print it on to the real screen
    getch(); // Wait for user input
    endwin(); // End curses mode
    
    return 0;
}

```
