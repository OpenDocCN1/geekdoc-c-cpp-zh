However, if that expression is false, then we know that score is less than 250 and the statement associated with the final else clause is executed and the message, “You scored less than 250. Nothing to brag about.” is displayed.

> Hint
> While the final else clause in an if else-if suite isn’t required, you can use it as a way to execute code if none of the expressions in the sequence are true.

# USING THE SWITCH STATEMENT

You can use a switch statement to create multiple branching points in your code. Here’s a generic form of the switch statement:

```
switch (choice)
{
case value1:    statement1;
                break;
case value2:    statement2;
                break;
case value3:    statement3;
                break;
                .
                .
                .
case valueN:    statementN;
                break;
default:        statementN + 1;
}
```

The statement tests choice against the possible values—value1, value2, and value3—in order. If choice is equal to a value, then the program executes the corresponding statement. When the program hits a break statement, it exits the switch structure. If choice doesn’t match any value, then the statement associated with the optional default is executed.

The use of break and default are optional. If you leave out a break, however, the program will continue through the remaining statements until it hits a break or a default or until the switch statement ends. Usually you want one break statement to end each case.