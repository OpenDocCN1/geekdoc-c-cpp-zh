# Logical Operations

+   a > b && c > d = true
+   a < b && c > d = false
+   a < b || c > d = true
+   !(a-b) == c = true

# MATHEMATICAL FUNCTIONS

Often, we may need to use trigonometric functions and logarithms. The System namespace defines a class known as Math class with a rich set of static methods that makes math-oriented programming easy and efficient. It also contains two static members, E and PI, representing the values of mathematical constants e and p. Table 5.11 lists some of the mathematical methods contained in the Math class.

# Table 5.11 Main mathematical methods

| Method | Description |
|---|---|
| Sin () | sine of an angle in radians |
| Cos () | cosine of an angle in radians |
| Tan () | tangent of an angle in radians |
| Asin () | inverse of sine |
| Acos () | inverse of cosine |
| Atan () | inverse of tangent |
| Atan2 () | inverse tangent, with x and y co-ordinates specified |
| Sinh () | hyperbolic sine |
| Cosh () | hyperbolic cosine |
| Tanh () | hyperbolic tangent |
| Sqrt () | square root |
| Pow () | number raised to a given power |
| Exp () | exponential |
| Log () | natural logarithm (base e) |
| Log10 () | base 10 logarithm |
| Abs () | absolute value of a number |
| Min () | lower of two numbers |
| Max () | higher of two numbers |
| Sign () | sign of the number |

Note that all the methods take double type parameters and return a double type value. However, the parameters of Abs (), Min (), Max (), and Sign () may of any numeric type.

Program 5.8 demonstrates the use of Math class with a simple application.