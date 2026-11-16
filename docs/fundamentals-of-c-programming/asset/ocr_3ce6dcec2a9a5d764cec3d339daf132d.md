# 9.4.2 Command Interpreter

Some functions are useful even if they accept no information from the caller and return no result. Listing 9.11 (calculator.cpp) uses such a function.

```
Listing 9.11: calculator.cpp
#include <iostream>
#include <cmath>

/*
 * help_screen
 * Displays information about how the program works
 * Accepts no parameters
 * Returns nothing
 */
void help_screen() {
    std::cout << "Add: Adds two numbers\n";
    std::cout << "Example: a 2.5 8.0\n";
    std::cout << "Subtract: Subtracts two numbers\n";
    std::cout << "Example: s 10.5 8.0\n";
    std::cout << "Print: Displays the result of the latest operation\n";
    std::cout << "Example: p\n";
    std::cout << "Help: Displays this help screen\n";
    std::cout << "Example: h\n";
    std::cout << "Quit: Exits the program\n";
    std::cout << "Example: q\n";
}

/*
 * menu
 * Display a menu
 * Accepts no parameters
 * Returns the character entered by the user.
 */
char menu() {
    // Display a menu
    std::cout << "=== A)dd S)ubtract P)rint H)elp Q)uit ===\n";
    // Return the char entered by user
    char ch;
    std::cin >> ch;
    return ch;
}

/*
 * main
 * Runs a command loop that allows users to
 * perform simple arithmetic.
 */
int main() {
    double result = 0.0, arg1, arg2;
    bool done = false; // Initially not done
    do {
        switch (menu()) {
        case 'A': // Addition
```