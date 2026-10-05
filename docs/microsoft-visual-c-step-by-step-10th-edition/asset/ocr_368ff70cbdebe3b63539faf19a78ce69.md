Both while and for statements test their Boolean expression at the beginning of the loop. This means that if the expression evaluates to false on the first test, the body of the loop does not run (not even once). The do statement is different: its Boolean expression is evaluated after each iteration, so the body always executes at least once.

The syntax of the do statement is as follows (don't forget the final semicolon):

```
do
  statement
while (booleanExpression);
```

You must use a statement block if the body of the loop contains more than one statement. (The compiler will report a syntax error if you don't.) Here's a version of the example that writes the values 0 through 9 to the console, this time constructed using a do statement:

```
int i = 0;
do
{
  Console.WriteLine(i);
  i++;
} while (i < 10);
```

# The break and continue statements

In Chapter 4, you saw how to use the break statement to jump out of a switch statement. You can also use a break statement to jump out of the body of an iteration statement. When you break out of a loop, the loop exits immediately, and execution continues at the first statement that follows the loop. Neither the update nor the continuation condition of the loop is rerun.

In contrast, the continue statement causes the program to perform the next iteration of the loop immediately (after reevaluating the Boolean expression). Here's another version that writes the values 0 through 9 to the console, this time using break and continue statements:

```
int i = 0;
while (true)
{
  Console.WriteLine(i);
```