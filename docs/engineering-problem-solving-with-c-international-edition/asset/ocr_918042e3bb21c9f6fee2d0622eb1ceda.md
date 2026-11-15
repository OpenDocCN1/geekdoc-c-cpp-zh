Remember that the logarithm of a negative value or zero does not exist, and thus an execution error occurs if you use a logarithm function with a negative value for its argument.

An additional mathematical function that you may find useful is the abs function. This function computes the absolute value of an integer, and returns an integer value. The header file containing information relative to this function is stdlib.h, and it should be included in programs referencing this function.

# PRACTICE!

+   Evaluate the following expressions:
+   1. floor(-2.6)
+   2. ceil(-2.6)
+   3. pow(2, -3)
+   4. sqrt(floor(10.7))
+   5. fabs(-10.2 * 5)
+   6. floor(ceil(10.8))
+   7. log10(100) + log10(0.001)
+   8. fabs(pow(-2, 5))

# Trigonometric Functions

Trigonometric functions

The trigonometric functions assume that all arguments are of type double and that they return values of type double. In addition, as previously stated, the trigonometric functions also assume that angles are represented in radians. To convert radians to degrees, or degrees to radians, use the following statements:

```
#define PI 3.141593
...
angle_deg = angle_rad * (180 / PI);
angle_rad = angle_deg * (PI / 180);
```

The trigonometric functions are included in the Standard C library, and a preprocessor directive including the information in math.h should be used with these functions. Following is a brief summary of these functions:

| sin(x) | This function computes the sine of x, where x is in radians. |
| cos(x) | This function computes the cosine of x, where x is in radians. |
| tan(x) | This function computes the tangent of x, where x is in radians. |
| asin(x) | This function computes the arcsine or inverse sine of x, where x must be in the range [-1, 1]. The function returns an angle in radians in the range [-π/2, π/2]. |
| acos(x) | This function computes the arccosine or inverse cosine of x, where x must be in the range [-1, 1]. The function returns an angle in radians in the range [0, π]. |
| atan(x) | This function computes the arctangent or inverse tangent of x. The function returns an angle in radians in the range [-π/2, π/2]. |
| atan2(y, x) | This function computes the arctangent or inverse tangent of the value y/x. The function returns an angle in radians in the range [-π, π]. |