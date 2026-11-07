easily handles selecting a choice from an extended list. Here’s the general form for a switch statement:

```
```c
switch (integer-expression)
{
        case label1 : statement(s)
        case label2 : statement(s)
        ...
        default     : statement(s)
}
```
```

A C++ switch statement acts as a routing device that tells the computer which line of code to execute next. On reaching a switch statement, a program jumps to the line labeled with the value corresponding to the value of `integer-expression`. For example, if `integer-expression` has the value 4, the program goes to the line that has a `case 4:` label. The value `integer-expression`, as the name suggests, must be an expression that reduces to an integer value. Also each label must be an integer constant expression. Most often, labels are simple int or char constants, such as 1 or 'q', or enumerators. If `integer-expression` doesn’t match any of the labels, the program jumps to the line labeled `default`. The default label is optional. If you omit it and there is no match, the program jumps to the next statement following the switch (see Figure 6.3).

The switch statement is different from similar statements in languages such as Pascal in a very important way. Each C++ case label functions only as a line label, not as a boundary between choices. That is, after a program jumps to a particular line in a switch, it then essentially executes all the statements following that line in the switch unless you explicitly direct it otherwise. Execution does not automatically stop at the next case. To make execution stop at the end of a particular group of statements, you must use the `break` statement. This causes execution to jump to the statement following the switch.

Listing 6.10 shows how to use switch and break together to implement a simple menu for executives. The program uses a `showmenu()` function to display a set of choices. A switch statement then selects an action based on the user’s response.

![](bbox=[0.163, 0.678, 0.859, 0.867])

Figure 6.3  The structure of switch statements.