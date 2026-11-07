```
```cpp
int main() {
    // use tab and bell manipulators
    std::cout << "Testing the tab manipulator:\n"
        << 'a' << tab << 'b' << tab << 'c' << '\n';
    std::cout << "Testing the bell manipulator\n" << bell;
}
```
```

> ```text
> Testing the tab manipulator:
> a   b   c
> Testing the bell manipulator
> ```

**Fig. 19.9** | Creating and testing user-defined, nonparameterized stream manipulators. (Part 2 of 2.)

# 19.6.5 Trailing Zeros and Decimal Points (showpoint)

Stream manipulator showpoint (Fig. 19.10) is a sticky setting that forces a floating-point number to display a decimal point and trailing zeros. For example, the floating-point value 79.0 prints as 79 without using showpoint and prints as 79.0000 using showpoint. The number of trailing zeros is determined by the current precision. To reset the showpoint setting, output the stream manipulator noshowpoint. The default precision of floating-point numbers is 6, which you can see in the output produced by lines 13–17. When neither the fixed nor the scientific stream manipulator is used, the precision represents the number of significant digits to display (i.e., the total number of digits to display), not the number of digits to display after the decimal point.

```
```cpp
// fig19_10.cpp
// Displaying trailing zeros and decimal points in floating-point values.
#include <iostream>

int main() {
    // display double values with default stream format
    std::cout << "Before using showpoint"
        << "\n9.9900 prints as: " << 9.9900
        << "\n9.9000 prints as: " << 9.9000
        << "\n9.0000 prints as: " << 9.0000;

    // display double value after showpoint
    std::cout << std::showpoint
        << "\nAfter using showpoint"
        << "\n9.9900 prints as: " << 9.9900
        << "\n9.9000 prints as: " << 9.9000
        << "\n9.0000 prints as: " << 9.0000 << '\n';
}
```
```

> ```text
> Before using showpoint
> 9.9900 prints as: 9.99
> 9.9000 prints as: 9.9
> 9.0000 prints as: 9
> ```

**Fig. 19.10** | Controlling the printing of trailing zeros and decimal points in floating-point values. (Part 1 of 2.)