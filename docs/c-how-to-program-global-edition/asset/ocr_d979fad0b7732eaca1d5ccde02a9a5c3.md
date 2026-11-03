```
unsigned int counter = 1; // initialize counter

do {
    printf("%u ", counter);
} while (++counter <= 10);
```

1 2 3 4 5 6 7 8 9 10

Fig. 4.9 | Using the do...while iteration statement. (Part 2 of 2.)

# do...while Statement Flowchart

Figure 4.10 shows the do...while statement flowchart, which makes it clear that the loop-continuation condition does not execute until after the action is performed at least once.

![](bbox=[0.35, 0.58, 0.75, 0.84])

Fig. 4.10 | Flowcharting the do...while iteration statement.

# 4.9 break and continue Statements

The break and continue statements are used to alter the flow of control. Section 4.7 showed how break can be used to terminate a switch statement's execution. This section discusses how to use break in an iteration statement.

# break Statement

The break statement, when executed in a while, for, do...while or switch statement, causes an immediate exit from that statement. Program execution continues with the next statement after that while, for, do...while or switch. Common uses of break are to escape early from a loop or to skip the remainder of a switch (as in Fig. 4.7). Figure 4.11 demonstrates the break statement (line 14) in a for iteration statement. When the if statement detects that x has become 5, break is executed. This terminates the for statement, and the program continues with the printf after the for. The loop fully executes only four times. We declared x before the loop in this example, so that we could use its final value after the loop terminates. Recall that when you declare the control variable in a for loop's initialization expression, the variable no longer exists after the loop terminates.