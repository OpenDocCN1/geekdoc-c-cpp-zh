
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
    CaseZero();
    break;
case 1:
    CaseOne();
    break;
default:
    CaseOthers();
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

Multiple labels are permitted in a switch section. The example

```
switch (i) {
case 0:
    caseZero();
    break;
case 1:
    caseOne();
    break;
case 2:
default:
    caseTwo();
    break;
}
```

is valid. The example does not violate the “no fall through” rule because the labels case 2: and default: are part of the same switch section.

The “no fall through” rule prevents a common class of bugs that occur in C and C++ when break statements are accidentally omitted. In addition, because of this rule, the switch sections of a switch statement can be arbitrarily rearranged without affecting the behavior of the statement. For example, the sections of the switch statement above can be reversed without affecting the behavior of the statement:

```
switch (i) {
    default:
        caseAny();
        break;
    case 1:
        caseZeroOrOne();
        goto default;
    case 0:
        caseZero();
        goto case 1;
}
```

The statement list of a switch section typically ends in a break, goto case, or goto default statement, but any construct that renders the end point of the statement list unreachable is permitted. For example, a while statement controlled by a boolean expression true is known to never reach its end point. Likewise, a throw or return statement always transfers control elsewhere and never reaches its end point. Thus the following example is valid:

```
switch (i) {
    case 0:
        while (true) F();
    case 1:
        throw new ArgumentException();
    case 2:
        return;
}
```

> > **JON SKEET** I wonder whether it might have been wise for the C# designers to have redesigned switch/case from scratch. The scoping rules for variables introduced in cases are somewhat surprising, and the break statement feels wrong, too. I believe developers think of cases as blocks—so why not enforce that?
> >
> > ~~~csharp
> >     case 0:
> >     {
> >         // Code for case 0 goes here, with no need for a break
> >     }
> > ~~~
> >
> > Likewise, it would probably have been more readable to allow a comma-separated list of expressions for multiple cases to match a single block, rather than repeating whole case labels.

The governing type of a switch statement may be the type string. For example:

```
~~~csharp
void DoCommand(string command) {
    switch (command.ToLower()) {
    case "run":
        DoRun();
        break;
    case "save":
        DoSave();
        break;
    case "quit":
        DoQuit();
        break;
    default:
        InvalidCommand(command);
        break;
    }
}
~~~
```

Like the string equality operators (§7.10.7), the switch statement is case sensitive and will execute a given switch section only if the switch expression string exactly matches a case label constant.

When the governing type of a switch statement is string, the value null is permitted as a case label constant.

The statement-lists of a switch-block may contain declaration statements (§8.5). The scope of a local variable or constant declared in a switch block is the switch block.

> > **BILL WAGNER** This idea suggests that implicit braces surround each switch block.

Within a switch block, the meaning of a name used in an expression context must always be the same (§7.6.2.1).

The statement list of a given switch section is reachable if the switch statement is reachable and at least one of the following is true:

- The switch expression is a nonconstant value.
- The switch expression is a constant value that matches a case label in the switch section.
- The switch expression is a constant value that doesn't match any case label, and the switch section contains the default label.
- A switch label of the switch section is referenced by a reachable goto case or goto default statement.

> VLADIMIR RESHETNIKOV This rule is not applied when the goto case or goto default statement is inside a try or catch block of a try statement that includes a finally block, and the switch label is outside the try statement, and the end point of the finally block is unreachable.

The end point of a switch statement is reachable if at least one of the following is true:

- The switch statement contains a reachable break statement that exits the switch statement.

> VLADIMIR RESHETNIKOV This rule is not applied when the break statement is inside a try or catch block of a try statement that includes a finally block, and the target of the break statement is outside the try statement, and the end point of the finally block is unreachable.

- The switch statement is reachable, the switch expression is a nonconstant value, and no default label is present.
- The switch statement is reachable, the switch expression is a constant value that doesn't match any case label, and no default label is present.
