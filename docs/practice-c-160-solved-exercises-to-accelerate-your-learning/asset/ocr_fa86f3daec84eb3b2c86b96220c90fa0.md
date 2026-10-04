# 18. Create a program that calculates and displays the perimeter of a circle, prompting the user for the radius, using the formula P = 2πr

```
#include <iostream>
#include <cmath> // Required for the M_PI constant

int main() {
    double radius;

    // Prompt the user for the radius
    std::cout << "Enter the radius of the circle: ";
    std::cin >> radius;

    // Calculate the perimeter/circumference
    double perimeter = 2 * M_PI * radius;

    // Display the result
    std::cout << "The perimeter (circumference) of the circle with radius " << radius << " is: " <<
```