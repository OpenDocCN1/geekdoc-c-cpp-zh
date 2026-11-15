This code validates the text entered to ensure that it is a valid tic-tac-toe move. If the value of input were 9, for example, the program would have to perform nine different evaluations. It would be preferable to jump to the correct code after only one evaluation. To enable this, you use a switch statement.

# The switch Statement

Given a variable to compare and a list of constant values to compare against, the switch statement is simpler to read and code than the if statement. The switch statement looks like this:

```
switch(test-expression)
{
    [case option-constant:
        statement
    [default:
        statement]
}
```

Here is a breakdown of the switch statement.

+   - test-expression returns a value that is compatible with the governing types. Allowable governing data types are sbyte, byte, short, ushort, int, uint, long, ulong, char, string, and an enum type (covered in Chapter 8).
+   - constant is any constant expression compatible with the data type of the governing type.
+   - statement is one or more statements to be executed when the governing type expression equals the constant value. The statement or statements must have no reachable endpoint. In other words, the statement, or last of the statements if there are more than one, must be a jump statement such as a break, return, or goto statement. If the switch statement appears within a loop, then continue is also allowed.

A switch statement should have at least one case statement or a default statement. In other words, switch(x) {} will generate a warning.

Listing 3.47, with a switch statement, is semantically equivalent to the series of if statements in Listing 3.46.