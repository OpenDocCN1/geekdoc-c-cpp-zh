# Chapter 18

# Library Functions

# 18.1 Mathematical Functions

The header file math.h contains declarations for several exponential, logarithmic, trigonometric, hyperbolic, and other mathematical functions. In all trigonometric functions, angles are taken in radians.

# 18.1.1 abs()

```
int abs(int x);
```

It returns the absolute value of the argument. If the argument is positive then it returns the positive value, if the argument is negative then it negates the value and returns the positive value.

# 18.1.2 acos()

```
double acos(double x);
```

This function returns the arc cosine of x i.e. cos⁻¹x. The argument should be in the range -1 to 1 and the return value lies in the range 0 to π.

# 18.1.3 asin()

```
double asin(double x);
```

This function returns the arc sine of x i.e. sin⁻¹x. The argument should be in the range -1 to 1 and the return value lies in the range -π/2 to π/2.

# 18.1.4 atan()

```
double atan(double x);
```

This function returns the arc tangent of x i.e. tan⁻¹x. The argument should be in the range -1 to 1 and the return value lies in the range -π/2 to π/2.

# 18.1.5 atan2()

```
double atan2(double y, double x);
```

This function is used for computing the arc tangent of y/x i.e. tan⁻¹(y/x). The return value lies in the range -π to π.

# 18.1.6 cabs()

```
double cabs(struct complex x);
```

This function returns the absolute value of complex number.