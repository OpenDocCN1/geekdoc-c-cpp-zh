# Mathematical Functions

# 24 Mathematical Functions

Class Math provides static methods to compute mathematical functions. Floating-point numbers (double and float) conform to IEEE754 include positive and negative infinities as non-numbers, called NaNs. There is also a distinction between positive zero and negative zero, ignored here.

These methods return non-numbers (NaNs) when applied to illegal arguments, called NaNs, and return infinities in case of overflow; do not throw exceptions. They behave sensibly when applied to positive or negative infinities; they return the limit if it exists, or else NaN. The methods round to the nearest even integer in case of a tie. The methods Abs and Sign are overloaded on arguments of type float, int, long, byte, and short; the methods Min and Max are overloaded on the unsigned types.

+   * static double E is the e ≈2.71828, the base of the natural logarithm.
* static double PI is the constant π≈3.14159, the circumference of a circle with diameter 1.
* static double Abs(double x) is the absolute value: if x<0, and -x if x<0.
* static double Acos(double x) is the arc cosine of x, in the range [0,π], for -1<=x<=1.
* static double Asin(double x) is the arc sine of x, in the range [-π/2,π/2], for -1<=x<=1.
* static double Atan(double y, double x) is the arc tangent of y/x in the quadrant of (x, y), in the range [-π,π]. When x is 0, the result is π/2 with the same sign as y.
* static double Ceil(double x) is the smallest integral value >=x.
* static double Cos(double x) is the cosine of x, in the range [-1,1].
* static double Exp(double x) is the exponential of x, that is, e to the power of x.
* static double Floor(double x) is the largest integral value<=x.
* static double IEEERemainder(double x, double y) is the remainder of x/y, that is, x-y*, where n is the integer closest to x/y. May be negative when x is negative and y is positive.
* static double Log(double x) is the base e logarithm or natural logarithm of x, for x>=0.
* static double Log10(double x) is the base 10 logarithm of x, for x>0.
* static double Min(double x, double y) is the smallest of x and y.
* static double Pow(double x, double y) is x to the power of y, that is, x^y. If y is 1, the result is x. If y is 0, then the result is 1.0. If x<0 and y is not integral, then the result is a NaN.
* static double Round(double x) is the whole number that is closest to x.
* static double Round(double x, int d) is the number closest to x, rounded to d<=15.
* static double Sin(double x) is the sine of x.
* static int Sign(double x) returns +1 or 0 or -1 as x>0 or x=0 or x<0.
* static double Sqrt(double x) is the square root of x, for x>=0.
* static double Tan(double x) is the tangent of x.