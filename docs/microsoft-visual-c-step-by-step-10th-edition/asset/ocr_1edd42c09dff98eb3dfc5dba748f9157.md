statement, it’s much harder to accidentally leave out the code that initializes or updates the control variable, so you are less likely to write code loops forever. Here’s the syntax of a for statement:

Click here to view code image

```
for (initialization; Boolean expression; update control variable)
statement
```

The statement that forms the body of the for construct can be a single line of code or a block enclosed in braces.

You can rephrase the while loop show earlier that displays the integers from 0 through 9 as the following for loop:

```
for (int i = 0; i < 10; i++)
{
  Console.WriteLine(i);
```

The initialization occurs just once, at the very beginning of the loop. Then, if the Boolean expression evaluates to true, the statement runs. The control variable update occurs, and then the Boolean expression is reevaluated. If the condition still evaluates to true, the statement is executed again, the control variable is updated, the Boolean expression is reevaluated again, and so on.

Notice that the initialization occurs only once, the statement in the body of the loop always executes before the update occurs, and that the update occurs before the Boolean expression reevaluates.

> Tip
As with the while statement, it’s considered a good practice to always use a code block even if the body of the for loop contains just a single statement. If you add more statements to the body of the for loop later, this approach will help to ensure that your code is always executed as part of each iteration.