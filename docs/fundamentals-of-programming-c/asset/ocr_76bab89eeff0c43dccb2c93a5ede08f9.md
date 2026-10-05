# 8.2. STANDARD MATH FUNCTIONS

| mathfunctions Module |
| double sqrt(double x) |
| Computes the square root of a number: $sqrt(x) = \sqrt{x}$ |
| double exp(double x) |
| Computes e raised to: $exp(x) = e^x$ |
| double log(double x) |
| Computes the natural logarithm of a number: $log(x) = \ln x$ |
| double log10(double x) |
| Computes the common logarithm of a number: $log(x) = \log_{10} x$ |
| double cos(double x) |
| Computes the cosine of a value in radians: $cos(x) = cos x$; other trigonometric functions include sine, tangent, arcsine, arccos, hyperbolic cosine, hyperbolic tangent |
| double pow(double x, double y) |
| Raises one number to a power of: $pow(x,y) = x^y$ |
| double fabs(double x) |
| Computes the absolute value of a number: $fabs(x) = |x|$ |

Table 8.1: A view of the functions from the *cmath* library

The *cmath* the *cmath* library also defines a constant HUGE\_VAL. Programmers can use this to represent infinity or an undefined value like the slope of a vertical line or a fraction with a zero denominator. A list of the numeric functions available to C++ can be found at http://www.cplusplus.com/reference/library/cmath/.

> Be careful to put the function's arguments in the proper order when calling a function; for example, the call `pow(10,2)` computes $10^2 = 100$, but the call `pow(2,10)` computes $2^{10} = 1024$.

A C++ program that uses any of the functions from the *cmath* library must use the following preprocessor `#include` directive:

```
#include <cmath>
```

Functions in the *cmath* library are ideal for solving problems like the one shown in Figure 8.4. Suppose a spacecraft is at a fixed location in space relative to some planet. The spacecraft' distance to the planet, therefore, is fixed. A satellite orbiting the planet in a circular orbit. We wish to compute how much away the satellite will be from the spacecraft when it has progressed 10 degrees along its orbital path.

We will let the origin of our coordinate system (0,0) be located at the center of the planet which corresponds to the point $(x_1,y_1)$. The satellite is stationary at point $(x_2,y_2)$. The spacecraft is located in the same plane as the satellite's orbit. We need to compute the difference in the distances between the new point (satellite) and the fixed point (spacecraft) at two different times during the satellite's orbit.

Facts from mathematics provide solutions to the following problems: