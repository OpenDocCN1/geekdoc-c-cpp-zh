```
switch-sections:
  switch-section
  switch-sections switch-section

switch-section:
  switch-labels statement-list

switch-labels:
  switch-label
  switch-labels switch-label

switch-label:
  case constant-expression :
  default :
```

A switch-statement consists of the keyword switch, followed by a parenthesized expression (called the switch expression), followed by a switch-block. The switch-block consists of zero or more switch-sections, enclosed in braces. Each switch-section consists of one or more switch-labels followed by a statement-list (§8.2.1).

The governing type of a switch statement is established by the switch expression.

+   - If the type of the switch expression is sbyte, byte, short, ushort, int, uint, long, ulong, bool, char, string, or an enum-type, or if it is the nullable type corresponding to one of these types, then that is the governing type of the switch statement.
+   - Otherwise, exactly one user-defined implicit conversion (§6.4) must exist from the type of the switch expression to one of the following possible governing types: sbyte, byte, short, ushort, int, uint, long, ulong, char, string, or a nullable type corresponding to one of those types.
+   - Otherwise, if no such implicit conversion exists, or if more than one such implicit conversion exists, a compile-time error occurs.

The constant expression of each case label must denote a value that is implicitly convertible (§6.1) to the governing type of the switch statement. A compile-time error occurs if two or more case labels in the same switch statement specify the same constant value.

There can be at most one default label in a switch statement.

A switch statement is executed as follows:

+   - The switch expression is evaluated and converted to the governing type.
+   - If one of the constants specified in a case label in the same switch statement is equal to the value of the switch expression, control is transferred to the statement list following the matched case label.