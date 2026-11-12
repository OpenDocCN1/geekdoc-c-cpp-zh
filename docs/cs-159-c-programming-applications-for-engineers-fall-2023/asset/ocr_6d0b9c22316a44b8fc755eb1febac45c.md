# Conditional Expressions

The conditional expression has three operands and two operators. Each operand is itself an expression.

+   - The first operator is a question mark that separates the first two expressions.
+   - The second operator is a colon and separates the last two expressions.

To evaluate a conditional expression, we first must evaluate the leftmost expression. When this expression is true, then the value of the second expression (the first expression after the ?) is evaluated. However, if the logical expression (before the ?) is false, then the third expression is evaluated.

Below, when the sum of the two variables is greater than zero the variable a is incremented. When the sum is less than or equal to zero then the variable b is incremented.

```
a + b > 0 ? a++ : b++;
```

# More Conditional Expression Examples:

| Code | Output Generated: |
| :--- | :--- |
| int a = 1;<br>int b = -1;<br>int c;<br><br>a + b > 0 ? a++ : b++;<br><br>c = a > b ? 5 : 3;<br><br>printf("c = %d\n", c);<br><br>a == b ? printf("a == b\n") : printf("a != b\n"); | |

Must there be an expression for both the second and third expressions?

+   - Yes.
+   - error: expected expression before ';' token

Is it possible for each option, true and false to have more than one expression?

+   - No.