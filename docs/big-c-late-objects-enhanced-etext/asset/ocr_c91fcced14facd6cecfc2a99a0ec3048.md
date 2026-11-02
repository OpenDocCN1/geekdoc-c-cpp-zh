# Table 6 Arithmetic Expressions

| Mathematical Expression | C++ Expression | Comments |
|---|---|---|
| (x + y)/2 | (x + y) / 2 | The parentheses are required; x + y / 2 computes x + y/2. |
| xy/2 | x * y / 2 | Parentheses are not required; operators with the same precedence are evaluated left to right. |
| (1 + r/100)^n | pow(1 + r / 100, n) | Remember to add #include <cmath> to the top of your program. |
| sqrt(a^2 + b^2) | sqrt(a * a + b * b) | a * a is simpler than pow(a, 2). |
| (i + j + k)/3 | (i + j + k) / 3.0 | If i, j, and k are integers, using a denominator of 3.0 forces floating-point division. |

Table 7 shows additional functions that are declared in the <cmath> header. Inputs and outputs are floating-point numbers.

# Table 7 Other Mathematical Functions

| Function | Description |
|---|---|
| sin(x) | sine of x (x in radians) |
| cos(x) | cosine of x |
| tan(x) | tangent of x |
| log(x) | (natural log) ln(x), x > 0 |
| log10(x) | (decimal log) log10(x), x > 0 |
| abs(x) | absolute value |x| |

# EXAMPLE CODE

See sec02 of your companion code for a program that gives examples of working with numbers in C++.

![](bbox=[0.15, 0.88, 0.2, 0.98])

# Common Error 2.3

# Unintended Integer Division

It is unfortunate that C++ uses the same symbol, namely /, for both integer and floating-point division. These are really quite different operations. It is a common error to use integer division by accident. Consider this segment that computes the average of three integers:

```
cout << "Please enter your last three test scores: ";
int s1;
int s2;
int s3;
cin >> s1 >> s2 >> s3;
```