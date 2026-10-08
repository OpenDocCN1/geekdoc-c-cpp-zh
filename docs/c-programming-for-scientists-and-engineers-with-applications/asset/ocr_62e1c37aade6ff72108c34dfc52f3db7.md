Notice that a and b are variables.

```
a = 5;
b = 6;
c = 3;
d = 8;
a * b > c + d evaluates to 1, true
b / c > a evaluates to 0, false
```

Notice that a *, b, c + d, and b/c are arithmetic expressions. When arithmetic expressions are used in a relational expression, the arithmetic expressions are evaluated first, and then the relational expression is avoided. The comparison for equality of arithmetic expressions producing real numbers because real numbers may not be stored accurately in the computer.

Programming Hint: When real numbers are compared, it is better to compare for approximate equality of the two operands.

The following example shows the comparison of two floating-point numbers:

```
float a;
a = 1.0 / 3.0;
a = 3 * a;
if(fabs(a - 1.0) < 0.0001) /* is approximately equal */
```

rather than

```
if(a == 1.0)
```

Relational expressions may be used in arithmetic. The following example determines which is the largest of two numbers:

```
big = a * ( a > b) + b * (b > a) + a * ( a == b);
```

The relational operations evaluate to true or false, which are represented by 1 or 0, respectively, and can be used in arithmetic.