```
Displayed in default format:
0.00123457        1.946e+009

Displayed in scientific format:
1.234567e-003    1.946000e+009

Displayed in fixed format:
0.001235        1946000000.000000
```

**Fig. 15.18** | Floating-point values displayed in default, scientific and fixed formats. (Part 2 of 2.)

# ### 15.7.6 Uppercase/Lowercase Control (uppercase)

Stream manipulator **uppercase** outputs an uppercase X or E with hexadecimal-integer values or with scientific notation floating-point values, respectively (Fig. 15.19). Using stream manipulator uppercase also causes all letters in a hexadecimal value to be uppercase. By default, the letters for hexadecimal values and the exponents in scientific notation floating-point values appear in lowercase. To reset the uppercase setting, output the stream manipulator **nouppercase**.

```
```cpp
// Fig. 15.19: Fig15_19.cpp
// Stream manipulator uppercase.
#include <iostream>
using namespace std;

int main()
{
   cout << "Printing uppercase letters in scientific" << endl
        << "notation exponents and hexadecimal values:" << endl;

   // use std::uppercase to display uppercase letters; use std::hex and
   // std::showbase to display hexadecimal value and its base
   cout << uppercase << 4.345e10 << endl
        << hex << showbase << 123456789 << endl;
} // end main
```
```

```
Printing uppercase letters in scientific
notation exponents and hexadecimal values:
4.345E+010
0X75BCD15
```

**Fig. 15.19** | Stream manipulator uppercase.

# ### 15.7.7 Specifying Boolean Format (boolalpha)

C++ provides data type bool, whose values may be false or true, as a preferred alternative to the old style of using 0 to indicate false and nonzero to indicate true. A bool variable outputs as 0 or 1 by default. However, we can use stream manipulator **boolalpha** to set the output stream to display bool values as the strings "true" and "false". Use stream manipulator **noboolalpha** to set the output stream to display bool values as integers (i.e., the default setting). The program of Fig. 15.20 demonstrates these stream manipulators.