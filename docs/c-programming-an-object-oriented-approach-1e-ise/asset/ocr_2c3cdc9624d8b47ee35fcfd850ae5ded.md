# **Program 3.23**  Testing floating-point manipulators

```
```cpp
/**************************************************************
 * A program to test some manipulators for floating-point types *
 **************************************************************/
#include <iostream>
using namespace std;

int main( )
{
    // Declarations
    double x = 1237;
    double y = 12376745.5623;
    // Using fixed (default) and showpoint manipulator
    cout << "x in fixed_point format: " << x << endl;
    cout << "x in fixed_point format: " << showpoint << x << endl;
    // Using scientific manipulator
    cout << "y in scientific format: " << y << scientific;
    return 0;
}
```
```

```
```text
Run:
x in fixed_point format: 1237          // We have not used showpoint
x in fixed_point format: 1237.00        // We have used showpoint
y in scientific format: 1.23767e+007
```
```

# **EXAMPLE 3.19**

Program 3.23 shows how we use manipulators for the floating-point types.

**Manipulators for Showing the Positive Sign** C++ does not show a positive sign (+) if the number is positive (the negative sign is always shown). To force a positive number to be printed with the positive sign, we can use the `showpos` manipulator.

**Manipulators for Showing Letters in Uppercase** We have seen that the integer and floating-point values sometimes include alphabetic characters (a, b, c, d, e, f) for values in hexadecimal notation, x for hexadecimal notation, and e for scientific notation. These characters are printed in lowercase by default. If we want them to be printed in uppercase, we use the manipulator **uppercase**.

**Manipulator for Adjusting Numbers in a Field** Later we see how we can define the size of a field (number of characters occupied) to print a value using manipulators with arguments. After the size is determined, we need to decide how we want to adjust the value and the sign (if any) in the field. C++ uses three formats for this as shown in Figure 3.12.

![](bbox=[0.331, 0.869, 0.832, 0.928])