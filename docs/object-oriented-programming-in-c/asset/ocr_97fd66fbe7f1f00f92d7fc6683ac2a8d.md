# 4.11 Math Library Functions

The standard C++ supports many math functions that can be used for performing certain commonly used calculations. Most frequently used math library functions are summarized in Table 4.1.

# Table 4.1 Commonly used math library functions

| Function | Purposes |
|---|---|
| ceil(x) | Rounds x to the smallest integer not less than x ceil(8.1) = 9.0 and ceil(-8.8) = -8.0 |
| cos(x) | Trigonometric cosine of x (x in radians) |
| exp(x) | Exponential function e^x. |
| fabs(x) | Absolute value of x.
If x>0 then abs(x) is x
If x=0 then abs(x) is 0.0
If x<0 then abs(x) is -x |
| floor(x) | Rounds x to the largest integer not greater than x
floor(8.2) = 8.0 and floor(-8.8 = -9.0 |
| log(x) | Natural logarithm of x(base e) |
| log10(x) | Logarithm of x(base 10) |
| pow(x,y) | x raised to power y(x^y) |
| sin(x) | Trigonometric sine of x (x in radians) |
| sqrt(x) | Square root of x |
| tan(x) | Trigonometric tangent of x (x in radians) |

> note
> The argument variables x and y are of type double and all the functions return the data type double.

To use the math library functions, we must include the header file math.h in conventional C++ and cmath in ANSI C++.

# SUMMARY

+   It is possible to reduce the size of program by calling and using functions at different places in the program.

+   In C++ the main() returns a value of type int to the operating system. Since the return type of functions is int by default, the keyword int in the main() header is optional. Most C++ compilers issue a warning, if there is no return statement.