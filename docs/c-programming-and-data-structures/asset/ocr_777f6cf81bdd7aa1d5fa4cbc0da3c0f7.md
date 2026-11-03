| Operator | Description | Associativity | Precedence |
|---|---|---|---|
| / | Division |  |  |
| % | Modulus |  |  |
| + | Addition | Left to right | 4 |
| - | Subtraction |  |  |
| << | Left shift | Left to right | 5 |
| >> | Right shift |  |  |
| < | Less than | Left to right | 6 |
| <= | Less than or equal to |  |  |
| > | Greater than |  |  |
| >= | Greater than or equal to |  |  |
| == | Equality | Left to right | 7 |
| != | Inequality |  |  |
| & | Bitwise AND | Left to right | 8 |
| ^ | Bitwise XOR | Left to right | 9 |
| | | Bitwise OR | Left to right | 10 |
| && | Logical AND | Left to right | 11 |
| || | Logical OR | Left to right | 12 |
| ?: | Conditional expression | Right to left | 13 |
| = | Assignment operators | Right to left | 14 |
| *= /= %= += -= &= ^= |= <<= >>= |  |  |  |
| , | Comma operator | Left to right | 15 |

# Rules of Precedence and Associativity

+   - Precedence rules decides the order in which different operators are applied
+   - Associativity rule decides the order in which multiple occurrences of the same level operator are applied

# 1.59 MATHEMATICAL FUNCTIONS

Mathematical functions such as cos, sqrt, log, etc. are frequently used in analysis of real-life problems. Most of the C compilers support these basic math functions. However, there are systems that have a more comprehensive math library and one should consult the reference manual to find out which functions are available. Table 1.26 lists some standard math functions.

Table 1.26 Math functions

| Function | Meaning |
|---|---|
| *Trigonometric* |  |
| acos(x) | Arc cosine of x |
| asin(x) | Arc sine of x |
| atan(x) | Arc tangent of x |
| atan2(x,y) | Arc tangent of x/y |