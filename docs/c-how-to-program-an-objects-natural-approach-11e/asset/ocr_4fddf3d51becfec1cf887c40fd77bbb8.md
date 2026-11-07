# ### 5.3 Math Library Functions

In the Objects-Natural case study sections, you’ve created objects of existing classes, then called their member functions to perform useful tasks. Some reusable code is provided simply as standalone functions, known as global functions.

The `<cmath>` header provides many global functions (in the std namespace) for common mathematical calculations. For example,

```
sqrt(900.0)
```

calculates the square root of 900.0 and returns the result, 30.0. Function sqrt takes a double argument and returns a double result. Some popular math library functions are summarized in the following table. The variables x and y are of type double.

| Function | Description | Example |
|---|---|---|
| `ceil(x)` | rounds x to the smallest integer not less than x | `ceil(9.2)` is 10.0<br>`ceil(-9.8)` is -9.0 |
| `cos(x)` | trigonometric cosine of x (x in radians) | `cos(0.0)` is 1.0 |
| `exp(x)` | exponential function of x | `exp(1.0)` is 2.718282<br>`exp(2.0)` is 7.389056 |
| `fabs(x)` | absolute value of x | `fabs(5.1)` is 5.1<br>`fabs(0.0)` is 0<br>`fabs(-8.76)` is 8.76 |
| `floor(x)` | rounds x to the largest integer not greater than x | `floor(9.2)` is 9.0<br>`floor(-9.8)` is -10.0 |
| `fmod(x, y)` | remainder of x/y as a floating-point number | `fmod(2.6, 1.2)` is 0.2 |
| `log(x)` | natural logarithm of x (base e) | `log(2.718282)` is 1.0<br>`log(7.389056)` is 2.0 |
| `log10(x)` | logarithm of x (base 10) | `log10(10.0)` is 1.0<br>`log10(100.0)` is 2.0 |
| `pow(x, y)` | x raised to power y (x^y) | `pow(2, 7)` is 128<br>`pow(9, .5)` is 3 |
| `sin(x)` | trigonometric sine of x (x in radians) | `sin(0.0)` is 0 |
| `sqrt(x)` | square root of x (where x is a non-negative value) | `sqrt(9.0)` is 3.0 |
| `tan(x)` | trigonometric tangent of x (x in radians) | `tan(0.0)` is 0 |

# ### Additional Math Functions

Recent C++ versions added dozens of new math functions to the `<cmath>` header. Some were entirely new, and some were other versions of existing functions but for arguments of type float or long double rather than double. The two-argument hypot function, for example, calculates a right triangle’s hypotenuse. There is also a three-argument version of hypot to calculate the hypotenuse in three-dimensional space. See the complete list

```
https://en.cppreference.com/w/cpp/numeric/math
```

and the C++ standard section, “Mathematical functions for floating-point types”:

```
https://timsong-cpp.github.io/cppwp/n4861/c.math
```