# Mathematical Functions

The C standard library contains a variety of functions that perform mathematical operations in the header file math.h. Prototypes for the mathematical functions are. The math functions all return a type double. For the trigonometric functions, angles are expressed in radians rather than degrees, which you may be more used to. One radian equals 57.296 degrees, and a full circle (360 degrees) contains 2π radians.

# Trigonometric Functions

The trigonometric functions perform calculations that are used in some graphical and engineering applications:

| Function | Description |
| --- | --- |
| acos() | double acos(double x) | Returns the arcosine of its argument. The argument must be in the range -1 <= x <= 1, and the return value is in the range 0 <= acos <= [pi]. |
| asin() | double asin(double x) | Returns the arcsine of its argument. The argument must be in the range -1 <= x <= 1, and the return value is in the range [-pi/2] <= asin <= [pi/2]. |
| atan() | double atan(double x) | Returns the arctangent of its argument. The return value is in the range [-pi/2] <= atan <= [pi/2]. |
| atan2() | double atan2(double x, double y) | Returns the arctangent of x/y. The value returned is in the range [-pi] <= atan2 <= [pi]. |
| cos() | double cos(double x) | Returns the cosine of its argument. |
| sin() | double sin(double x) | Returns the sine of its argument. |
| tan() | double tan(double x) | Returns the tangent of its argument |

# Exponential and Logarithmic Functions

The exponential and logarithmic functions are needed for certain types of mathematical calculations: