classified as the entry-controlled loop or as the exit-controlled loop. In the entry-controlled loop, first the conditions are tried out and if satisfied then only body of loop is executed. In the exit-controlled, the test is made at the end of the body, so the body is executed unconditionally first time.

executed. After execution of instruction of the body, the test-condition is once again evaluated and if it is true, the body is executed once again. This process of repeated execution of the body continues until the test-condition finally becomes false and the control is transferred out of the loop. On exit, the program extends with the statement immediately after the body of the loop. The body contains only one statement it is not necessary to put the braces, but placing them is a good programming practice.

A looping process, in general, would involve the following four steps:

+   1. Setting and initialization of a counter.
+   2. Executing of the statements in the loop.
+   3. Test for a defined condition for execution of the loop.
+   4. Incrementing the counter.

The C language supplies three loop constructs for performing loop operations. They are:

+   1. The while statement.
+   2. The do statement.
+   3. The for statement.

# Nested Loops

+   - The while loop keeps repeating an action until an action condition returns **false**. This is useful where the programmer does not acknowledge in advance how many times the loop will be traversed.
+   - The do while loop is similar, but the condition is checked after the loop body is executed. This ensures that the loop body is run at least once.
+   - The for loop is often used, usually where the loop will be traversed a fixed number of times.

# The While Loop

When in a program a single statement or a certain group of statements are to be executed repeatedly depending upon certain test condition, then *while statement* is used. The general syntax of while loop is as follows:

```
while (test condition)
{
    body of the loop
}
```

The while is an entry-controlled loop statement. The test condition is measured and only if the condition is true the body is

The flow chart of while loop is as follows:

# Example

```
.......
.......
x = 10; -------- Initialization
while (x < 16) -------- Test condition
{
printf("%d",x); -------- body of the loop
x = x+1;
}
.......
```

![](bbox=[0.537, 0.504, 0.892, 0.827])

The above example shows a simple position where the test condition is measured first and since the test is satisfied the body is executed. This will proceed exactly six times printing out 10 to 15. Finally when x becomes 16 then