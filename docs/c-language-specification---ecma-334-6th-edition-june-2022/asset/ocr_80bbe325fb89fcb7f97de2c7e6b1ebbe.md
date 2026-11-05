```
```text
if (x)
{
    if (y)
    {
        F();
    }
    else
    {
        G();
    }
}
```
```

*end example*

An `if` statement is executed as follows:

+   - The *Boolean_expression* (§11.21) is evaluated.
+   - If the Boolean expression yields **true**, control is transferred to the first embedded statement. When and if control reaches the **end point** of that statement, control is transferred to the **end point** of the `if` statement.
+   - If the Boolean expression yields **false** and if an `else` part is present, control is transferred to the second embedded statement. When and if control reaches the **end point** of that statement, control is transferred to the **end point** of the `if` statement.
+   - If the Boolean expression yields **false** and if an `else` part is not present, control is transferred to the **end point** of the `if` statement.

The first embedded statement of an `if` statement is reachable if the `if` statement is **reachable** and the Boolean expression does not have the constant value **false**.

The second embedded statement of an `if` statement, if present, is **reachable** if the `if` statement is **reachable** and the Boolean expression does not have the constant value **true**.

The **end point** of an `if` statement is reachable if the end point of at least one of its embedded statements is reachable. In addition, the **end point** of an `if` statement with no `else` part is reachable if the `if` statement is reachable and the Boolean expression does not have the constant value **true**.

# 12.8.3 The switch statement

The `switch` statement selects for execution a statement list having an associated switch label that corresponds to the value of the switch expression.

```
```text
switch_statement
    : 'switch' '(' expression ')' switch_block
    ;

switch_block
    : '{' switch_section* '}'
    ;

switch_section
    : switch_label+ statement_list
    ;

switch_label
    : 'case' constant_expression ':'
```
```