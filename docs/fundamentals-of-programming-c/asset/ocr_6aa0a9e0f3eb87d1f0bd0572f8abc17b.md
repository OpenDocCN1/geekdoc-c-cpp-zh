# 3.4. FLOATING-POINT TYPES

# 3.14

has type **double**. To make a literal floating-point value a **float**, you must append an **f** or **F** to
number, as in

# 3.14f

(The **f** or **F** suffix is used with literal values only; you cannot change a **double** variable into a **float**
variable by appending an f. Attempting to do so would change the name of the variable!)

> All floating-point literals are **double** unless an **f** or **F** is appended to
end of the number; for example, 2. **0** is a **double** literal, 2.**0f** is a **float**
literal.

As in the case of the
**int** type, the range of floating-point numbers is limited, each value requires a fixed amount of
memory. In some ways, **ints** are very different from **doubles**. Any integer within the range of
t**int** type can be represented exactly. This is not true for the floating-point types. The
real $\pi$ contains an infinite number of digits, its value can only be approximated.
The number of digits is limited, so a finite number of digits can only be approximated;
for example, the number 3.141592653589793 contains too many digits for the **double** type and must be
approximated as 3.230249863404. This can occur due to the inexact nature of
floating-point numbers stored in later in Listing 4.2 (precision.cpp).

We can express floating-point numbers in scientific notation. Most programming editors do not
use superscript and special symbols like $	imes$, C+ shifts the normal scientific notation. The
number $6.022 	imes 10^{23}$ is written as **6.022e23**. The number to the left of the **e** to the right is the exponent of 10. Another example, $-5.1 	imes 10^4$
is expressed in C++ as **-5.1e-4**. Listing 3.9 (scientificnotation.cpp) prints some scientific constants using
scientific notation.

Listing 3.9:scientificnotation.cpp
```cpp
#include <iostream>
using namespace std;
int main() {
    double avogadro_number = 6.022e23, c = 2.998e8;
    cout << "Avogadro's number = " << avogadro_number << endl;
    cout << "Speed of light = " << c << endl;
}
```

Appendix 2.2 shows some insight into the implementation of C++ floating-point values and explains how
internally all floating-point numbers are stored in exponential notation with a mantissa and exponent.

©2014 Richard L. Halterman Last date: January 26, 2014