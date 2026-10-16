Because counting loops are used so often, nearly all programming languages provide a special statement to implement them. In C++ this is the for statement or for loop. The four components of a counting for loop were introduced in Section 5.5:

![](bbox=[0.11, 0.22, 0.85, 0.39])

As noted in Chapter 5, a trace table is a useful tool to trace the action of a loop (especially in debugging). For example, in the first sample run of Example 9.1 where the value 5 is entered for n, the loop counts through the values 1 through 5, so that the body of the for loop is executed five times. The following table shows the value of the various variables and loop condition as the function sum() executes:

| count | n | count <= n | Action | runningTotal |
|---|---|---|---|---|
| 1 | 5 | true | Execute loop body | 1 |
| 2 | 5 | true | Execute loop body | 3 |
| 3 | 5 | true | Execute loop body | 6 |
| 4 | 5 | true | Execute loop body | 10 |
| 5 | 5 | true | Execute loop body | 15 |
| 6 | 5 | false | Terminate repetition | 15 |

A similar trace table for the second sample run where n has the value 100 would show that the loop counts through the values 1 through 100, so that the loop body is executed 100 times.

There are two forms of the for statement that are commonly used to implement counting loops: an ascending form, in which the loop control variable is incremented,

```
for (int control_variable = initial_value;
    control_variable <= limit_value;
    increment_expression)
statement
```

and a descending form, in which the loop control variable is decremented:

```
for (int control_variable = initial_value;
    control_variable >= limit_value;
    decrement_expression)
statement
```