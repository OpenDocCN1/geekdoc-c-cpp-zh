# The syntax of the switch statement

```
switch (switchExpression) {
  case constantExpression:
    statements
    break;
  [case constantExpression:
    statements
    break];...
  default:
    statements
    break;
}
```

# A switch statement with a default label

```
switch (customerType) {
  case "R":
    discountPercent = .1m;
    break;
  case "C":
    discountPercent = .2m;
    break;
  default:
    discountPercent = .0m;
    break;
}
```

# A switch statement that falls through the first case label

```
switch (customerType) {
  case "R":
  case "C":
    discountPercent = .2m;
    break;
  case "T":
    discountPercent = .4m;
    break;
}
```

# Description

+   - A switch statement begins evaluating its switch expression. This expression must evaluate to a string, char, byte, sbyte, short, ushort, int, uint, long, long, or bool type.
- After evaluating the switch expression, the switch statement transfers control to the appropriate case label. If control isn't transferred to one of the case labels, the optional default label is executed.
- The break statement exits the switch statement. If a label contains one or more statements, the label must end with a break statement.
- If a label doesn't contain any statements, code execution will fall through to the next label. That means the statements contained by the next label will be executed.

![](bbox=[0.056, 0.938, 0.456, 0.953])