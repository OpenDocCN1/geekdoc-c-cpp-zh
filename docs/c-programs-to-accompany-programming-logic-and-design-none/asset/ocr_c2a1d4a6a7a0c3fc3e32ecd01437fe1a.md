The following code samples illustrate how relational operators are used in expressions:

+   - » number1 < number2 evaluates to `true` because 10 is less than 15.
+   - » number1 <= number2 evaluates to `true` because 10 is less than or equal to 15.
+   - » number1 > number2 evaluates to `false` because 10 is not greater than 15.
+   - » number1 >= number2 evaluates to `false` because 10 is not greater than or equal to 15.
+   - » number1 == number2 evaluates to `false` because 10 is not equal to 15.
+   - » number1 != number2 evaluates to `true` because 10 is not equal to 15.

# ### LOGICAL OPERATORS

You can use another type of Boolean operator, **logical operators**, when you need to ask more than one question but you want to receive only one answer. For example, in a program, you may want to ask if a number is between the values 1 and 10. This actually involves two questions. You need to ask if the number is greater than 1 AND if the number is less than 10. Here, you are asking two questions but you want only one answer—either yes (`true`) or no (`false`).

Like statements that contain relational expressions, statements that contain logical operators evaluate to `true` or `false`, thereby permitting decision-making in your programs.

Table 4-2 lists the logical operators used in C++.

| Operator | Name | Description |
|---|---|---|
| `&&` | AND | All expressions must evaluate to `true` for the entire expression to be `true`; this operator is written as two `&` symbols with no space between them. |
| `\|\|` | OR | Only one expression must evaluate to `true` for the entire expression to be `true`; this operator is written as two `\|` symbols with no space between them. |
| `!` | NOT | This operator reverses the value of the expression; for example, if the expression evaluates to `false`, then reverse it so that the expression evaluates to `true`. |

**Table 4-2** Logical operators

To see how to use the logical operators, suppose you declare two variables: an `int` named `number1` that you initialize with the value 10; and another `int` variable named `number2` that you initialize with the value 15. The declaration statements for these variables are shown in the following code:

```
```cpp
int number1 = 10;
int number2 = 15;
```
```

![](bbox=[0.94, 0.32, 0.99, 0.38])