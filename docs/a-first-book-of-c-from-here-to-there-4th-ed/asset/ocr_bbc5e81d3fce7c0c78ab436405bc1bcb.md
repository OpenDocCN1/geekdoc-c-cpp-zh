This form is a two-way selection statement. If the expression has a non-zero value, it's considered true and statement1 is executed; otherwise, statement2 is executed.

+   4. An if-else statement can contain other if-else statements. In the absence of braces, each else is associated with the closest preceding unpaired if.

+   5. The if-else chain is a multiway selection statement with this general form:

```
if (expression_1)
    statement_1;
else if (expression_2)
    statement_2;
else if (expression_3)
    statement_3;
    .
    .
    .
else if (expression_m)
    statement_m;
else
    statement_n;
```

Each expression is evaluated in the order in which it appears in the chain. If an expression is true (has a non-zero value), only the statement between this expression and the next else if or else is executed, and no further expressions are tested. The final else is optional, and the statement corresponding to the final else is executed only if no previous expressions are true.

+   6. A compound statement consists of any number of single statements enclosed by the brace pair { and }. Compound statements are treated as a single unit and can be used anywhere a single statement is used.

+   7. Variables have meaning only in the block in which they're declared, which includes any inner block contained in the declaring block.

+   8. The switch statement is a multiway selection statement with this general form:

```
switch (integer_expression)
{   // start of compound statement
case value_1:  // terminated with a colon
    statement1;
    statement2;
    .
    .
    break;
case value_2:  // terminated with a colon
    statementm;
    statementn;
```