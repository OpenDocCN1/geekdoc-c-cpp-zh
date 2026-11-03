```
Output
a = 16 b = 10 c = 6
a = 16 b = 11 d = 26
a/b = 1
a%b = 5
a * b = 176
0
1
```

Fig. 4.3 Further illustration of arithmetic operators

# 4.10 ARITHMETIC EXPRESSIONS

An arithmetic expression is a combination of variables, constants, and operators arranged as per the syntax of the language. We have used a number of simple expressions in the examples discussed so far. C can handle any complex mathematical expressions. Some of the examples of C expressions are shown in Table 3.6. Remember that C does not have an operator for exponentiation.

# 4.11 EVALUATION OF EXPRESSIONS

Expressions are evaluated using an assignment statement of the form

```
variable = expression;
```

Table 4.6 Expressions

| Algebraic expression | C expression |
|---|---|
| a x b - c | a * b - c |
| (m + n)(x + y) | (m + n)*(x + y) |
| ab/c | a * b/c |
| 3x² + 2x + 1 | 3 * x * x + 2 * x + 1 |
| x/y + c | x/y + c |

Variable is any valid C variable name. When the statement is encountered, the expression is evaluated first and the result then replaces the previous value of the variable on the left-hand side. All variables used in the expression must be assigned values before evaluation is attempted. Examples of evaluation statements are

```
x = a *b - c;
y = b / c * a;
z = a - b / c + d;
```

The blank space around an operator is optional and adds only to improve readability. When these statements are used in a program, the variables a, b, c, and d must be defined before they are used in the expressions.