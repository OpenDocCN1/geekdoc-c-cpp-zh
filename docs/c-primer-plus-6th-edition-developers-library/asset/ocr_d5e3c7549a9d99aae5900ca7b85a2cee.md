| Prototype | Description |
|---|---|
| double log(double x) | Returns the natural logarithm of x |
| double log10(double x) | Returns the base 10 logarithm of x |
| double pow(double x, double y) | Returns x to the y power |
| double sqrt(double x) | Returns the square root of x |
| double cbrt(double x) | Returns the cube root of x |
| double ceil(double x) | Returns the smallest integral value not less than x |
| double fabs(double x) | Returns the absolute value of x |
| double floor(double x) | Returns the largest integral value not greater than x |

# A Little Trigonometry

Let’s use the math library to solve a common problem: converting from x/y coordinates to magnitudes and angles. For example, suppose you draw, on a grid work, a line that transverses 4 units horizontally (the x value) and 3 units vertically (the y value). What is the length (magnitude) of the line and what is its direction? Trigonometry tells us the following:

```
magnitude = square root (x² + y²)
```

and

```
angle = arctangent (y/x)
```

The math library provides a square root function and a couple arctangent functions, so you can express this solution in a C program. The square root function, called sqrt(), takes a double argument and returns the argument’s square root, also as a type double value.

The atan() function takes a double argument—the tangent—and returns the angle having that value as its tangent. Unfortunately, the atan() function is confused by, say, a line with x and y values of −5 and −5. Because (−5)/(−5) is 1, atan() would report 45°, the same as it does for a line with x and y values of 5 and 5. In other words, atan() doesn’t distinguish between a line of a given angle and one 180° in the opposite direction. (Actually, atan() reports in radians, not degrees; we’ll discuss that conversion soon.)

Fortunately, the C library also provides the atan2() function. It takes two arguments: the x value and the y value. That way, the function can examine the signs of x and y and figure out the correct angle. Like atan(), atan2() returns the angle in radians. To convert to degrees, multiply the resulting angle by 180 and divide by pi. You can have the computer calculate pi by using the expression 4 * atan(1). Listing 16.14 illustrates these steps. It also gives you a chance to review structures and the typedef facility.