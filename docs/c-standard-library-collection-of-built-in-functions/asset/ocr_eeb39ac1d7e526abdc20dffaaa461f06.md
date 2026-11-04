| # | Description |
|---|---|
|15| **double modf(double x, double *integer)**
The returned value is the fraction component (part after the decimal), and sets integer to the integer component. |
|16| **double pow(double x, double y)**
Returns **x** raised to the power of **y**. |
|17| **double sqrt(double x)**
Returns the square root of **x**. |
|18| **double ceil(double x)**
Returns the smallest integer value greater than or equal to **x**. |
|19| **double fabs(double x)**
Returns the absolute value of **x**. |
|20| **double floor(double x)**
Returns the largest integer value less than or equal to **x**. |
|21| **double fmod(double x, double y)**
Returns the remainder of **x** divided by **y**. |

# double acos(double x)

# Description

The C library function **double acos(double x)** returns the arc cosine of **x** in radians.

# Declaration

Following is the declaration for acos() function.

```
double acos(double x)
```

# Parameters

+   - **x** -- This is the floating point value in the interval [-1, +1].

# Return Value

This function returns principal arc cosine of x, in the interval [0, pi] radians.