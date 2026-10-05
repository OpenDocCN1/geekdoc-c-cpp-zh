```
// https://godbolt.org/z/Tvx4qcrE6
#include <iostream>
#include <cclassify>
#include <limits> // numeric_limits
#include <string>

std::string fpclassify(double x) {
    switch(x) {
        case FP_INFINITE:   return "infinite";
        case FP_NAN:        return "NaN";
        case FP_NORMAL:     return "normal";
        case FP_SUBNORMAL:  return "subnormal";
        case FP_ZERO:       return "zero";
        default:             return "unknown";
    }
}

int main() {
    const auto dmin = std::limits<double>::min();
    std::cout
      << "1.0 is " << fpclassify(1.0) << "\n" // Output: 1.0/0.0 is infinite
      << "0.0 is " << fpclassify(0.0/0.0) << "\n" // Output: 0.0/0.0 is NaN
      << "dmin/2 is " << fpclassify(dmin/2) << "\n" // Output: dmin/2 is subnormal
      << "-0.0 is " << fpclassify(-0.0) << "\n" // Output: -0.0 is zero
      << "1.5 is " << fpclassify(1.5) << "\n"; // Output: 1.5 is normal
}
```

**Listing 4.35** Among other things, you can discover special values with "fpclassify."

The header defines macros or constants for the special values. HUGE, VALF, and HUGE VALL contain large values, INFINITY the positive infinity, and NAN not a number.

In addition to fpclassify, other functions are available in <cmath> to determine the properties of floating-point numbers. isfinite (not NAN or INFINITY), isinf (INFINITY), isnan (NAN), isnnormal (not INFINITY, NAN, Zero, or subnormal), and signbit (sign) have the obvious meanings. isnorderd checks whether at least one of two numbers is NAN.

# Tips for Almost Calculation

When adding, it is better to add large numbers to large numbers and small numbers to small numbers rather than large to small numbers.

Multiplication is a little trickier. Due to the scaling in the exponent, calculations between -1.0 and +1.0 are more accurate than those further away from 0.0. It is advisable to bring calculations as close to this range as possible. This means, if you can influence it, arrange the