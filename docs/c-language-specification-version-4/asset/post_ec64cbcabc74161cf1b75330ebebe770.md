
The type and constant-expression of a local constant declaration must follow the same rules as those of a constant member declaration (§10.4). The value of a local constant is obtained in an expression using a simple-name (§7.6.2). The scope of a local constant is the block in which the declaration occurs. It is an error to refer to a local constant in a textual position that precedes its constant-declarator. Within the scope of a local constant, it is a compile-time error to declare another local variable or constant with the same name. A local constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same type.

## 8.6 Expression statements

An expression-statement evaluates a given expression. The value computed by the expression, if any, is discarded.

```
expression-statement:
    statement-expression ;
statement-expression:
    invocation-expression
    object-creation-expression
    assignment
    post-increment-expression
    post-decrement-expression
    pre-increment-expression
    pre-decrement-expression
```

Not all expressions are permitted as statements. In particular, expressions such as x + y and x == 1 that merely compute a value (which will be discarded), are not permitted as statements.

Execution of an expression-statement evaluates the contained expression and then transfers control to the end point of the expression-statement. The end point of an expression-statement is reachable if that expression-statement is reachable.

## 8.7 Selection statements

Selection statements select one of a number of possible statements for execution based on the value of some expression.

```
selection-statement:
    if-statement
    switch-statement
```

### 8.7.1 The if statement

The if statement selects a statement for execution based on the value of a boolean expression.

```
if-statement:
    if ( boolean-expression ) embedded-statement
    if ( boolean-expression ) embedded-statement else embedded-statement
```

An else part is associated with the lexically nearest preceding if that is allowed by the syntax. Thus, an if statement of the form if (x) if (y) F(); else G(); is equivalent to

C# LANGUAGE SPECIFICATION

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

An if statement is executed as follows:

- The boolean-expression (§7.20) is evaluated.
- If the boolean expression yields true, control is transferred to the first embedded statement. When and if control reaches the end point of that statement, control is transferred to the end point of the if statement.
- If the boolean expression yields false and if an else part is present, control is transferred to the second embedded statement. When and if control reaches the end point of that statement, control is transferred to the end point of the if statement.
- If the boolean expression yields false and if an else part is not present, control is transferred to the end point of the if statement.

The first embedded statement of an if statement is reachable if the if statement is reachable and the boolean expression does not have the constant value false.

The second embedded statement of an if statement, if present, is reachable if the if statement is reachable and the boolean expression does not have the constant value true.

The end point of an if statement is reachable if the end point of at least one of its embedded statements is reachable. In addition, the end point of an if statement with no else part is reachable if the if statement is reachable and the boolean expression does not have the constant value true.

### 8.7.2 The switch statement

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

A switch-statement consists of the keyword switch, followed by a parenthesized expression (called the switch expression), followed by a switch-block. The switch-block consists of zero or more switch-sections, enclosed in braces. Each switch-section consists of one or more switch-labels followed by a statement-list (§8.2.1).

The governing type of a switch statement is established by the switch expression.

- If the type of the switch expression is sbyte, byte, short, ushort, int, uint, long, ulong, bool, char, string, or an enum-type, or if it is the nullable type corresponding to one of these types, then that is the governing type of the switch statement.
- Otherwise, exactly one user-defined implicit conversion (§6.4) must exist from the type of the switch expression to one of the following possible governing types: sbyte, byte, short, ushort, int, uint, long, ulong, char, string, or a nullable type corresponding to one of those types.
- Otherwise, if no such implicit conversion exists, or if more than one such implicit conversion exists, a compile-time error occurs.

The constant expression of each case label must denote a value that is implicitly convertible (§6.1) to the governing type of the switch statement. A compile-time error occurs if two or more case labels in the same switch statement specify the same constant value.

There can be at most one default label in a switch statement.

A switch statement is executed as follows:

- The switch expression is evaluated and converted to the governing type.
- If one of the constants specified in a case label in the same switch statement is equal to the value of the switch expression, control is transferred to the statement list following the matched case label.
- If none of the constants specified in case labels in the same switch statement is equal to the value of the switch expression, and if a default label is present, control is transferred to the statement list following the default label.
- If none of the constants specified in case labels in the same switch statement is equal to the value of the switch expression, and if no default label is present, control is transferred to the end point of the switch statement.

If the end point of the statement list of a switch section is reachable, a compile-time error occurs. This is known as the “no fall through” rule. The example

```
switch (i) {
    case 0:
        caseZero();
        break;
    case 1:
        caseOne();
        break;
    default:
        caseOthers();
        break;
}
```

is valid because no switch section has a reachable end point. Unlike C and C++, execution of a switch section is not permitted to “fall through” to the next switch section, and the example

```
switch (i) {
  case 0:
    CaseZero();
  case 1:
    CaseZeroOrOne();
  default:
    CaseAny();
}
```

results in a compile-time error. When execution of a switch section is to be followed by execution of another switch section, an explicit goto case or goto default statement must be used:

```
switch (i) {
  case 0:
    CaseZero();
    goto case 1;
  case 1:
    CaseZeroOrOne();
    goto default;
  default:
    CaseAny();
    break;
}
```

Multiple labels are permitted in a switch-section. The example

```
switch (i) {
  case 0:
    CaseZero();
    break;
  case 1:
    CaseOne();
    break;
  case 2:
  default:
    CaseTwo();
    break;
}
```

is valid. The example does not violate the "no fall through" rule because the labels case 2: and default: are part of the same switch-section.

The "no fall through" rule prevents a common class of bugs that occur in C and C++ when break statements are accidentally omitted. In addition, because of this rule, the switch sections of a switch statement can be arbitrarily rearranged without affecting the behavior of the statement. For example, the sections of the switch statement above can be reversed without affecting the behavior of the statement:

```
switch (i) {
  default:
    CaseAny();
    break;
  case 1:
    CaseZeroOrOne();
    goto default;
  case 0:
    CaseZero();
    goto case 1;
}
```

The statement list of a switch section typically ends in a break, goto case, or goto default statement, but any construct that renders the end point of the statement list unreachable is permitted. For example, a while statement controlled by the boolean expression true is known to never reach its end point. Likewise, a throw or return statement always transfers control elsewhere and never reaches its end point. Thus, the following example is valid:
