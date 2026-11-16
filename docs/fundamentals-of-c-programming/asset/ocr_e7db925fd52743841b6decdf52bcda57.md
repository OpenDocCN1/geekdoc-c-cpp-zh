```
break;
default:
    std::cout << " *** Error: illegal die value ***\n";
    break;
}
std::cout << "+-------\n";
}
/* roll
 * Returns a pseudorandom number in the range 1...6
 */
int roll() {
    return rand() % 6 + 1;
}
/* main
 * Simulates the roll of a die three times
 */
int main() {
    // Initialize the die
    initialize_die();

    // Roll the die three times
    for (int i = 0; i < 3; i++)
        show_die(roll());
}
```

In Listing 9.13 (betterdie.cpp), main is no longer concerned with the details of pseudorandom number generation, nor is it responsible for drawing the die. These important components of the program are now in functions, so their details can be perfected independently from main.

Note how the result of the call to roll is passed directly as an argument to show_die.

# 9.4.5 Tree Drawing Function

# Listing 9.14: treefunc.cpp

```
#include <iostream>
/* tree(height)
 * Draws a tree of a given height
 * height is the height of the displayed tree
 */
void tree(int height) {
    int row = 0; // First row, from the top, to draw
    while (row < height) { // Draw one row for every unit of height
        // Print leading spaces
        int count = 0;
        while (count < height - row) {
            std::cout << " ";
```