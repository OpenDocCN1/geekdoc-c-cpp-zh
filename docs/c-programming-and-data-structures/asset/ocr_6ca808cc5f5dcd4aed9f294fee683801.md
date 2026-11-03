60 – 69  6
50 – 59  5
40 – 49  4
.  .
0  0

This segment of the program illustrates two important features. First, it uses empty cases. The first three cases will execute the same statements

```
grade = "Honours";
break;
```

Same is the case with case 7 and case 6. Second, default condition is used for all other cases where marks is less than 40.

The switch statement is often used for menu selection. For example:

```
-----
printf(" TRAVEL GUIDE\n\n");
printf(" A Air Timings\n");
printf(" T Train Timings\n");
printf(" B Bus Service\n");
printf(" X To skip\n");
printf("\n Enter your choice\n");
character = getchar();
switch (character)
{
case 'A' :
    air-display();
    break;
case 'B' :
    bus-display();
    break;
case 'T' :
    train-display();
    break;
default :
    printf(" No choice\n");
}
-----
```

It is possible to nest the switch statements. That is, a switch may be part of a case statement. ANSI C permits 15 levels of nesting.

# Rules for Switch Statement

+   - The switch expression must be an integral type.
+   - Case labels must be constants or constant expressions.
+   - Case labels must be unique. No two labels can have the same value.
+   - Case labels must end with semicolon.
+   - The break statement transfers the control out of the switch statement.
+   - The break statement is optional. That is, two or more case labels may belong to the same statements.
+   - The default label is optional. If present, it will be executed when the expression does not find a matching case label.
+   - There can be at most one default label.
+   - The default may be placed anywhere but usually placed at the end.
+   - It is permitted to nest switch statements.