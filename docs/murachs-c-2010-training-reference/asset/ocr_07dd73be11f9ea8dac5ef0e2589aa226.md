# Logical operators

| Operator | Name | Description |
|---|---|---|
| && | Conditional-And | Returns a true value if both expressions are true. This operator only evaluates the second expression if necessary. |
| || | Conditional-Or | Returns a true value if either expression is true. This operator only evaluates the second expression if necessary. |
| & | And | Returns a true value if both expressions are true. This operator always evaluates both expressions. |
| | | Or | Returns a true value if either expression is true. This operator always evaluates both expressions. |
| ! | Not | Reverses the value of the expression. |

# Examples

```
subtotal >= 250 && subtotal < 500
timeService <= 4 || timeService >= 12
```

```
isValid = true && counter++ < years
isValid = true || counter++ < years
```

```
date > startDate && date < expirationDate || isValid = true
((thisYTD > lastYTD) && empType="Part time") && startYear < currentYear
```

```
(counter++ >= years)
```

# Description

+   * You can use the logical operators to create a Boolean expression that combines two or more Boolean expressions.
* Since the && and || operators only evaluate the second expression if necessary, they're sometimes referred to as *short-circuit operators*. These operators are slightly more efficient than the && and || operators.
* By default, Not operations are performed first, followed by And operations, and then Or operations. These operations are performed after arithmetic operations and relational operations.
* You can use parentheses to change the sequence in which the operations will be performed or to clarify the sequence of operations.