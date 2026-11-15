# Table 2.5 Precedence of Arithmetic and Assignment Operators

| Precedence | Operator | Associativity |
| :--- | :--- | :--- |
| 1 | Parentheses: ( ) | Innermost first |
| 2 | Unary operators:
+ - ++ -- (type) | Right to left |
| 3 | Binary operators:
* / % | Left to right |
| 4 | Binary operators:
+ - | Left to right |
| 5 | Assignment operators:
= += -= *= /= %= | Right to left |

If we replace the abbreviated forms with the longer forms of the operations, we have

```
a = (b = b + (c + d));
or
b = b + (c + d);
a = b;
```

Evaluating this statement was good practice with the precedence/associativity table, but statements used in a program should be more readable. Therefore, using abbreviated assignment statements in a multiple-assignment statement is not recommended. Also, note that the spacing convention that we use inserts spaces around abbreviated operators and multiple-assignment operators because these operators are evaluated after the arithmetic operators.

![](bbox=[0.14, 0.48, 0.2, 0.53])

# PRACTICE!

Give a memory snapshot after each statement is executed, assuming that x is equal to 2 and that y is equal to 4 before the statement is executed. Also, assume that all the variables are integers.

+   1. z = x++*y;
+   2. z = ++x*y;
+   3. x += y;
+   4. y %= x;

# 2.4 Standard Input and Output

We have discussed statements for declaring variables and then using the variables to compute new values. We now present a statement that allows us to print these new values. In addition, we also discuss a statement that allows us to enter values from the keyboard when the program is executed. To use either of these statements in a program, we must include the following preprocessor directive:

```
#include <stdio.h>
```