# Chapter 5 while Loops 235

statement following the expression is executed repeatedly as long as the expression evaluates to a non-zero value. Considering just the expression and the statement following the parentheses, the computer uses this process in evaluating a statement:

+   1. Test the expression
2. If the expression has a non-zero (true) value
   a. execute the statement following the execute
   b. go back to Step 1
   else
   exit the while statement and execute the execute statement following the statement

Notice that Step 2b forces program control to be transferred back to Step 1. This back to the start of a while statement to evaluate the expression is what forms the loop program. The while statement literally loops back on itself to re the expression until it evaluates to zero (becomes false). Naturally, this rechecking means that somewhere in the loop must be a provision that alters the value of the tested expression. As you will see, this process is instead needed.

5.3 The looping process a while statement produces. A diamond shape is shown to use the two entry and two exit points required in the decision part of the while statement.

To make this looping process more tangible, the relational expression count <= 10 and the statement count << count; Using these elements, you can write the valid while statement:

```
while (count <= 10)
count << count;
```

Although this is valid, the alert reader will realize that it creates a situation in which the count statement is executed forever (or until you stop the program) or not at all. Here if your count has a value less than or equal to 10 then the expression is evaluated, and the count statement is executed. The while statement automatically loops on itself until the expression becomes false. Because we haven't changed the value in count, every execution of the count statement is still true, and this continues forever, or until the program containing this statement is stopped by the user. However, if count starts with a value greater than 10, the expression is false to begin, and the count statement is never executed.

How do you set an initial value in count to control what the while statement does the first time it is evaluated? The answer, of course, is to assign values to each variable in the test expression before the while statement is encountered. For example, the following sequence of instructions is valid:

```
count = 1;
while (count <= 10)
count << count;
```

Using this sequence of instructions ensures that count starts with a value of 1. You could assign any value to count in the assignment statement. What's important is to assign some value. In practice, the assigned value depends on the application.

You must change the value of count so that you can finally exit the while statement. Doing this requires an expression such as count = count + 1 to increment the value of count each time the while statement is executed. The fact that a while