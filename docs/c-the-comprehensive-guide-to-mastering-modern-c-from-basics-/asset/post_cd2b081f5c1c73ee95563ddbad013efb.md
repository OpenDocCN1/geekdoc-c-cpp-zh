
```
// https://godbolt.org/z/Tvx4qcrE6
#include <iostream>
#include <cmath>
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

The header defines macros or constants for the special values. HUGE, VALF, and HUGEVAL contain large values, INFINITY the positive infinity, and NAN not a number.

In addition to fpclassify, other functions are available in <cmath> to determine the properties of floating-point numbers. isfinite (not NAN or INFINITY), isinf (INFINITY), isnan (NAN), isnnormal (not INFINITY, NAN, Zero, or subnormal), and signbit (sign) have the obvious meanings. isnordered checks whether at least one of two numbers is NAN.

# Tips for Almost Calculation

When adding, it is better to add large numbers to large numbers and small numbers to small numbers rather than large to small numbers.

Multiplication is a little trickier. Due to the scaling in the exponent, calculations between -1.0 and +1.0 are more accurate than those further away from 0.0. It is advisable to bring calculations as close to this range as possible. This means, if you can influence it, arrange the multiplications in such a way that you follow this rule: “Large to small, small to large.”

This means that (0.1 * 10.0) * (10.0 * 0.1) is better than (0.1 * 0.1) * (10.0 * 10.0), mainly for extreme values. This means that the intermediate results do not move further away from 1 than necessary.

I think a detailed example will help you to see what can happen if the calculation elements are arranged unfavorably. For example, there is Heron’s formula to calculate the area of a triangle given three side lengths (a, b, c):

Rewritten slightly, Heron's formula in C++ looks like this:

```cpp
float heron(float a, float b, float c) {
    auto s = (a+b+c) / 2;
    return sqrt(s*(s-a)*(s-b)*(s-c));
}
```

For comparison, the Kahan method, {11} which first sorts the side lengths of the triangles according to a b ≥ c and looks for a better grouping. {12} After sorting, the formula results:

$A = \frac{1}{4} \sqrt{(a+b+c)(c-a+b)(c-a-b)(a+b-c)}$

However, only c ≤ a-b, because otherwise the sides do not form a triangle. In C++, it looks like:

```cpp
float kahan(float a, float b, float c) {
    auto x = max(a,max(b,c));
    auto y = max(min(a,b), min(max(a,b),c));
    auto z = 2 * min(a,b,c);
    return sqrt((x+y)*(z-x))*(x+y)*(x+(y-z))/4;
}
```

For a right-angled triangle with the side lengths 3, 4, and 5, the area 6 can be calculated in the head using the Pythagorean theorem. The following program is the same for both methods. I have used the template variable T instead of double as the type in order to be able to execute the same code with double and float (see Chapter 23):

```cpp
https://godbolt.org/z/We3oprcrcW
#include <iostream>
#include <cmath> // sqrt
#include <concepts> // floating_point
```

```cpp
using std::min; using std::max; using std::floating_point;

template<floating_point T> T heron(T a, T b, T c) {
    auto s = (a+b+c) / 2;
    return sqrt((s-a)*(s-b)*(s-c));
}
```

```cpp
template<floating_point T> T kahan(T a, T b, T c) {
    auto x = max(a,max(b,c));
    auto y = max(min(a,b), min(max(a,b),c));
    auto z = 2 * min(a,b,c);
    return sqrt((x+y)*(z-x))*(x+y)*(x+(y-z)) / 4;
}
```

```cpp
template<floating_point T> void triangle(T a, T b, T c) {
    std::cout << "heron: " << heron(a,b,c) << "\n";
    std::cout << "kahan: " << kahan(a,b,c) << "\n";
}
```

```cpp
int main() {
    triangle(3.0f, 4.0f, 5.0f);
}
```

The output is then 6 for both. Funny things when you insert the side lengths (100000.0, 99999.99979, 0.00029) and let the computer calculate the area. I run both calculations for float and double more digits:

```cpp
// godbolt.org/z/863b1z
int main() {
    std::cout << std::precision(15) << std::fixed;
    triangle(100000.0, 99999.99979f, 0.00029f);
    triangle(100000.0, 99999.99979, 0.00029);
}
```

The exact result would be 10. The example was carefully chosen so that float has the calculation: while the classic formula gives 0, the Kahan formula calculates 14.5. And 14.5 would look like a nice result if you didn't know that 10 is correct. Even though both methods give a better result with double—I told you that 10 should come out—such an example could also have been found for double. The actual outputs as follows:

```
heron: 0.0000000000000
kahan: 14.5000000000000
heron: 9.99999900063829
kahan: 10.00000007702138
```

However, it is even more important that you have to perform as few calculations as possible. Let's assume you work in video editing and want to calculate the length of a movie. Videos often have one frame per 1/25 of a second. Then you can calculate the current movie time in a loop in two ways. First, try it accumulated, and second, try it with multiplication, as the following listings demonstrate.

```cpp
// https://godbolt.org/z/SEEp9Hb
#include <iostream> // setprecision, fixed
constexpr int framesPerSec = 25;
constexpr int runtimeInSec = 3600;
constexpr int framesTotal = runtimeInSec * framesPerSec;
constexpr float frametime = 1.0 / framesPerSec;

int main() {
    float filetime = 0.0f;
    for(int n=0; n < framesTotal; ++n) {
        filetime += frametime; // accumulate
    }
    std::cout << std::precision(10) << std::fixed
              << filetime << "\n"; // output: 3602.260531250
}
```

**Listing 4.36** Accumulated time measurement.

You shouldn't be surprised that more than two seconds of errors have accumulated in one hour of film.

# Labeling Constants

For constexpr, refer to Chapter 13, Section 13.10.6. It is advantageous for the compiler and for you if you mark unchanging values (i.e., constants) as such. You can use (static) const or constexpr for this purpose. The latter ensures that the compiler can calculate the constant in advance. If it cannot do this, it will inform you accordingly.

Let the loop run from 1 to <= framesTotal to be able to compare it better with the next example.

However, you can also approach this differently. So long as the frametime remains constant over the course of the movie, you can calculate it in one step. So you are scaling as in the following listing.

```cpp
// https://godbolt.org/z/dKPo7andE
#include <iostream> // setprecision, fixed
constexpr int framesPerSec = 25;
constexpr int runtimeInSec = 3600;
constexpr int framesTotal = runtimeInSec * framesPerSec;
constexpr float frametime = 1.0f / framesPerSec;
int main() {
    float filtime = 0.0f;
    for(int n=0; n <= framesTotal; ++n) { // 1 ... framesTotal, because of formula
        filtime = frametime * n; // scale
        // ... code for this frame
    }
    std::cout << std::precision(10) << std::fixed // output: 3600.0000000000
              << filtime << '\n';
}
```

Listing 4.37 Closed time animation.
