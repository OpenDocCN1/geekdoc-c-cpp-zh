count starts with a value greater than 10, the expression is false to begin with, and the call to cout is never made.

![](bbox=[0.22, 0.26, 0.85, 0.77])

# Figure 5.1 Anatomy of a while loop

How do you set an initial value in count to control what the while statement does the first time the expression is evaluated? The answer, of course, is to assign values to each variable in the tested expression before the while statement is encountered. For example, the following sequence of instructions is valid:

```
count = 1;
while (count <= 10)
    cout << count << " ";
```

Using this sequence of instructions ensures that count starts with a value of 1. You could assign any value to count in the assignment statement. What's important is to assign some value. In practice, the assigned value depends on the application.

You must still change the value of count so that you can finally exit the while statement. Doing so requires an expression such as count = count + 1 to increment the value of count each time the while statement is executed. The fact that a while statement provides