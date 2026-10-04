# 16. Write a program that calculates the geometric mean of three numbers entered by the user -> GeoMean = $\sqrt[3]{n_1 	imes n_2 	imes n_3}$

```
#include <iostream>
#include <cmath> // Required for the cbrt() and pow() functions

int main() {
    double num1, num2, num3;

    // Prompt the user for three numbers
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    std::cout << "Enter the third number: ";
    std::cin >> num3;
```