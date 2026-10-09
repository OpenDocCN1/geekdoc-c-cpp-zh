```
// if-else statement
if (condition)
{
	then-statement;
}
else
{
	else-statement;
}
// Next statement in the program.

// if statement without an else
if (condition)
{
	then-statement;
}
// Next statement in the program.
```

In an if-else statement, if condition evaluates to true, the then-statement runs. If condition is false, the else-statement runs. Because condition can’t be simultaneously true and false, the then-statement and the else-statement of an if-else statement can never both run. After the then-statement or the else-statement runs, control is transferred to the next statement after the if statement.

In an if statement that doesn’t include an else statement, if condition is true, the then-statement runs. If condition is false, control is transferred to the next statement after the if statement.

Both the then-statement and the else-statement can consist of a single statement or multiple statements that are enclosed in braces ({}). For a single statement, the braces are optional but recommended.

The statement or statements in the then-statement and the else-statement can be of any kind, including another if statement nested inside the original if statement. In nested if statements, each else clause belongs to the last if that