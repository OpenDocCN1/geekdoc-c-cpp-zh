| Type | Storage | Smallest Magnitude | Largest Magnitude | Minimum Precision |
| :--- | :--- | :--- | :--- | :--- |
| float | 4 bytes | 1.17549 x 10^-38 | 3.40282 x 10^+38 | 6 digits |
| double | 8 bytes | 2.22507 x 10^-308 | 1.79769 x 10^+308 | 15 digits |
| long double | 8 bytes | 2.22507 x 10^-308 | 1.79769 x 10^+308 | 15 digits |

Table 3.3: Characteristics of Floating-point Numbers on 32-bit Computer Systems

# Listing 3.8: pi-print.cpp

```
#include <iostream>
int main() {
    double pi = 3.14159;
    std::cout << "pi = " << pi << '\n';
    std::cout << "or " << 3.14 << " for short" << '\n';
}
```

The first line in Listing 3.8 (pi-print.cpp) declares a variable named pi and assigns it a value. The second line in Listing 3.8 (pi-print.cpp) prints the value of the variable pi, and the third line prints a literal value. Any literal numeric value with a decimal point in a C++ program automatically has the type double, so

3.14
has type double. To make a literal floating-point value a float, you must append an f or F to the number, as in
3.14f

(The f or F suffix is used with literal values only; you cannot change a double variable into a float variable by appending an f. Attempting to do so would change the name of the variable!)

> All floating-point literals are double values unless an f or F is appended to the end of the number, for example, 2.0 is a double literal, while 2.0f is a float literal.

Floating-point numbers are an approximation of mathematical real numbers. As in the case of the int data type, the range of floating-point numbers is limited, since each value requires a fixed amount of memory. In some ways, though, ints are very different from doubles. Any integer within the range of the int data type can be represented exactly. This is not true for the floating-point types. Consider the real number π. Since π contains an infinite number of digits, a floating-point number with finite precision can only approximate its value. Since the number of digits available is limited, even numbers with a finite number of digits have no exact representation; for example, the number 23.123400654033989 contains too many digits for the double type and must be approximated as 23.3023498654034. Section 4.8.2 contains more information about the consequences of the inexact nature of floating-point numbers.

We can express floating-point numbers in scientific notation. Since most programming editors do not provide superscripting and special symbols like ×, C++ slightly alters the normal scientific notation. The number 6.022 × 10²³ is written 6.022e23. The number to the left of the e (we can use capital E as well) is