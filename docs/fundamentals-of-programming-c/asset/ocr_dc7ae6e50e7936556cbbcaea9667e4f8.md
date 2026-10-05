# 9.4. FUNCTION EXAMPLES

```
}
```

Observe that the name height is being used as a local variable in main and as a formal parameter name in tree. There is no conflict here, and the two heights represent two different locations in memory. Furthermore, that the statement

```
tree(height);
```

uses main's height as an actual parameter and height happens to be the name as the formal parameter is simply a coincidence. During the call, the value of main's height variable is copied into the parameter in tree also named height. The compiler can keep track of which height is based on where each is declared.

# 9.4.6 Floating-Point Equality

Recall from Listing 4.2 (imprecision.cpp) that floating-numbers are not mathematical real numbers; a floating-point number is finite and represented internally as a quantity with a binary mantissa and exponent. Just as 1/3 cannot be represented finely in the decimal (base 10) system, 1/10 cannot be represented exactly in the binary (base 2) system with a fixed number of digits. Often, problems arise from this imprecision, and in many software applications have been written using floating-point numbers calculations such as directing a spacecraft to a distant. In such small errors can result in complete failures. Floating-point numbers can be used safely and effectively, but without appropriate care.

To build our confidence with floating-point numbers, consider Listing 9.14 (simplefloataddition.cpp), which adds two double-precision floating-point numbers and checks for a given value.

> Listing 9.14: simplefloataddition.cpp

```
#include <iostream>

using namespace std;

int main() {
    double x = 0.9;
    x += 0.1;
    if (x == 1.0)
        cout << "OK" << endl;
    else
        cout << "NOT OK" << endl;
}
```

All seems well judging Listing 9.14 (simplefloataddition.cpp). Next, consider Listing 9.15 (badfloatcheck.cpp) which attempts to control a loop with a double-precision floating-point number.

> Listing 9.15: badfloatcheck.cpp

```
#include <iostream>

using namespace std;

int main() {
    // Count to ten by tenths
```