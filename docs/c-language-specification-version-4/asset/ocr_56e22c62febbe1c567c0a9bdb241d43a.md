# C# LANGUAGE SPECIFICATION

```
```csharp
if (x) {
    if (y) {
        F();
    }
    else {
        G();
    }
}
```
```

An if statement is executed as follows:

+   - The boolean-expression (§7.20) is evaluated.
+   - If the boolean expression yields true, control is transferred to the first embedded statement. When and if control reaches the end point of that statement, control is transferred to the end point of the if statement.
+   - If the boolean expression yields false and if an else part is present, control is transferred to the second embedded statement. When and if control reaches the end point of that statement, control is transferred to the end point of the if statement.
+   - If the boolean expression yields false and if an else part is not present, control is transferred to the end point of the if statement.

The first embedded statement of an if statement is reachable if the if statement is reachable and the boolean expression does not have the constant value false.

The second embedded statement of an if statement, if present, is reachable if the if statement is reachable and the boolean expression does not have the constant value true.

The end point of an if statement is reachable if the end point of at least one of its embedded statements is reachable. In addition, the end point of an if statement with no else part is reachable if the if statement is reachable and the boolean expression does not have the constant value true.

# 8.7.2 The switch statement

The switch statement selects for execution a statement list having an associated switch label that corresponds to the value of the switch expression.

```
switch-statement:
    switch ( expression ) switch-block
switch-block:
    { switch-sections_opt }
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