```
```cpp
int main() {
    const double dmin = std::numeric_limits<double>::min();
    std::cout
        << "1.0/0.0 is " << fpclassify(1/0.0) << '\n'  // Output: 1.0/0.0 is infinite
        << "0.0/0.0 is " << fpclassify(0.0/0.0) << '\n' // Output: 0.0/0.0 is NaN
        << "dmin/2 is " << fpclassify(dmin/2) << '\n'   // Output: dmin/2 is subnormal
        << "-0.0 is " << fpclassify(-0.0) << '\n'       // Output: -0.0 is zero
        << "1.0 is " << fpclassify(1.0) << '\n';       // Output: 1.0 is normal
}
```
```

**Listing 4.35** Among other things, you can discover special values with “fpclassify.”

The header defines macros or constants for the special values. HUGE_VAL, HUGE_VALF, and HUGE_VALL contain very large values, INFINITY the positive infinity, and NAN not a number.

In addition to fpclassify, other functions are available in <cmath> to determine the properties of floating-point numbers. isfinite (not NAN or INFINITY), isinf (INFINITY), isnan (NAN), isnormal (not INFINITY, NAN, zero, or subnormal), and signbit (sign) have the obvious meanings. isunordered checks whether at least one of two numbers is NAN.

# Tips for Almost Exact Calculation

When adding, it is better to add large numbers to large numbers and small numbers to small numbers rather than large numbers to small numbers.

Multiplication is a little trickier. Due to the scaling in the exponent, calculations between −1.0 and +1.0 are more accurate than those further away from 0.0. It is advisable to bring calculations as close to this range as possible. This means, if you can influence it, arrange the multiplications in such a way that you follow this rule: “Large to small, small to large.”

This means that (0.1*10.0) * (10.0*0.1) is better than (0.1*0.1) * (10.0*10.0), but mainly for extreme values. This means that the intermediate results do not move further away from 1 than necessary.

I think a detailed example will help you to see what can happen if the calculation elements are arranged unfavorably. For example, there is Heron’s formula to calculate the area of a triangle given three side lengths (a, b, c):

Rewritten slightly, Heron’s formula in C++ looks like this:

```
```cpp
float heron(float a, float b, float c) {
    auto s = (a+b+c) / 2;
    return sqrt(s*(s-a)*(s-b)*(s-c));
}
```
```