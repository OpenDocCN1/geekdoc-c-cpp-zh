| Precedence | Operator | Associativity |
| :--- | :--- | :--- |
| 1 | Parentheses: ( ) | Innermost first |
| 2 | Unary operators:
-- ++ + - (type) | Right to left |
| 3 | Binary operators:
* / % | Left to right |
| 4 | Binary operators:
+ - | Left to right |
| 5 | Assignment operators:
= += -= *= /= %= | Right to left |

To evaluate this properly, we use Table 2.5, which indicates that the assignment operators are evaluated last, and their associativity is right to left. Thus, the statement is equivalent to the following:

```
a = (b += (c + d));
```

If we replace the abbreviated forms with the longer forms of the operations, we have

```
a = (b = b + (c + d));
```

or

```
b = b + (c + d);
a = b;
```

Evaluating this statement was good practice with the precedence and associativity table, but, in general, statements used in a program should be more readable. Therefore, using abbreviated assignment statements in a multiple-assignment statement is not recommended. Also, note that the spacing convention that we use inserts spaces around abbreviated operators and multiple-assignment operators because these operators are evaluated after the arithmetic operators.

![](bbox=[0.135, 0.665, 0.225, 0.725])

# Practice 2.6

Give a memory snapshot after each statement is executed, assuming that x is equal to 2 and that y is equal to 4 before the statement is executed. Also, assume that all the objects are integers.

+   1. z = x++ * y;
+   2. z = ++x * y;
+   3. x += y;
+   4. y %= x;