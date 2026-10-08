When a double-precision value is used in a mixed-mode operation with an integer or single-precision value, the integer or single-precision value is converted to double-precision before the operation is performed. The result is a double-precision value that has no more accuracy than the less accurate of the two operands.

# 2.3.2 Arithmetic Expressions

In engineering and scientific applications it is very common to use arithmetic expressions that include constants as well as variables. An expression can be used in a C program wherever a value of the same type can be used. The examples show arithmetic expressions and the results for the following variable declarations:

int a, b, c, d;
float x, y, z, w;

| Expression | Result |
|---|---|
| 5 + 6 * 8 / 2 | integer constant |
| 3.0 + 5 * 2.5 + 6.0 / 2 | floating-point constant |
| a + b * c - d / c | integer value |
| x - y * z + w / 2 | floating-point value |
| a * x - b / y + w / c | floating-point value |

# 2.3.3 Assignment Statement

The assignment statement is the fundamental statement in most programming languages, including C. In C the equal sign (=) is used in the assignment statement. This symbol does not have the same meaning that it does in algebraic expressions. The meaning of this symbol in C is like its meaning in mathematical formulas. It indicates that the value computed from the expression on the right of the equal sign is to be assigned to the variable on the left (or stored in the memory location allocated to the variable on the left side of the equal sign). The following examples show the assignment statement:

area = (3.141593 * d * d) / 4.0;

means calculate $\pi^2/4$ and assign the result to area.

That is, the area of a circle by multiplying $\pi$ times the diameter squared and dividing by 4. $\pi$ has seven digits because values of data type float are stored with seven digits.