# 30. Make a program that reads a value of a product and the tax (in percentage), and calculates the final value of it.

```
#include <iostream>
```

```
int main() {
    double productValue, taxRate;

    // Prompt the user for the product value
    std::cout << "Enter the value of the product: ";
    std::cin >> productValue;

    // Prompt the user for the tax rate (in percentage)
    std::cout << "Enter the tax rate (in percentage): ";
    std::cin >> taxRate;

    // Calculate the tax amount
    double taxAmount = (taxRate / 100) * productValue;

    // Calculate the final product value including
```