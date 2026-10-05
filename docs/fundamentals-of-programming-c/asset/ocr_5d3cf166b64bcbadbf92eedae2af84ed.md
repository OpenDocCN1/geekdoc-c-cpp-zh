# D.2. THE FLOATING-POINT TYPES

![](bbox=[0.219, 0.13, 0.781, 0.237])

The scheme duplicates some numbers; for example, three different bit patterns represent the decimal value 0.5:

$0.100 \times 2^{00} = 0.010 \times 2^{01} = 0.001 \times 2^{10} = 0.510$

This duplication limits the number of different values that can be represented by a given number of bits.

+   3. They are not uniformly dense. There are more values near zero, and the integers become sparse farther away from zero.

The integer types discussed in Section D.1 exhibit one of these weaknesses. All integers in a range are present, no two bitstrings represent the same value, and the integers are uniformly distributed across their specified range. The standard floating-point types provided by C++ use many more bits than this simplified example, but the problems shown here still exist to a much smaller size. This is solely a problem of C++'s implementation of floating-point numbers: all languages and hardware that adhere to the IEEE 754 standard exhibit these problems. Mathematical real numbers require an infinite amount of storage to be represented exactly, but any computer's memory is finite.

Listing D.1 (imprecisedifference.cpp) demonstrates the inexactness of floating-point arithmetic.

# Listing D.1: imprecisedifference.cpp

```
#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    double d1 = 2000.5;
    double d2 = 2000.0;
    cout << setprecision(16) << (d1 - d2) << endl;
    double d3 = 2000.58;
    double d4 = 2000.0;
    cout << setprecision(16) << (d3 - d4) << endl;
}
```

The output of Listing D.1 (imprecisedifference.cpp) is:

| 0.5 |
| 0.5799999999999922 |