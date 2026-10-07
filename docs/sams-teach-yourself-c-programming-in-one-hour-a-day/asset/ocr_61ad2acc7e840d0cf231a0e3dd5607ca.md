The structure of the do...while loop is as follows:

do
  statement
  while (condition);

condition is any C expression, and statement is a single or compound C statement.
When program execution reaches a do...while statement, the following events occur:

+   1. The statements in statement are executed.
2. condition is evaluated. If it's true, execution returns to step 1. If it's false, the loop terminates.

The operation of a do...while loop is shown in Figure 6.4.

# FIGURE 6.4
Theoperation of a do...while loop.

![](bbox=[0.281, 0.406, 0.713, 0.758])

The statements associated with a do...while loop are always executed at least once. This is because the test condition is evaluated at the end, instead of the beginning of the loop. In contrast, for loops and while loops evaluate the test condition at the start of the loop, so the associated statements are not executed at all if the test condition is initially false.

The do...while loop is used less frequently than while and for loops. It is most appropriate when the statement(s) associated with the loop must be executed at least once. You could, of course, accomplish the same thing with a while loop by making sure