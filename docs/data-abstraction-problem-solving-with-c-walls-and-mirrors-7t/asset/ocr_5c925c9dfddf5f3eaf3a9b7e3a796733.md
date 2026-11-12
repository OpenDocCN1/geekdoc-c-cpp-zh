If no case label matches the current value of the switch expression, the statements that follow the default label, if one exists, are executed. If no default exists, the switch statement exits.

# A.5 Iteration Statements

C++ has three statements—the while, for, and do statements—that provide for repetition by iteration, that is, loops. Each statement controls the number of times that another C++ statement—the body—is executed. The body cannot be a declaration and is often a compound statement.

# A.5.1 The while Statement

A while statement executes as long as the expression is true

The general form of the while statement is

```
while (expression)
statement
```

As long as the value of expression is true, statement is executed. Because expression is evaluated before statement is executed, it is possible that statement will not execute at all. Note that the parentheses around expression are required.

Suppose that you wanted to compute the sum of positive integers that you enter at the keyboard.

Since the integers are positive, you can use a negative value or zero to indicate the end of the list of integers. The following while statement accomplishes this task:

```
int nextValue = 0;
int sum = 0;

cin >> nextValue;
while (nextValue > 0)
{
    sum += nextValue;
    cin >> nextValue;
} // end while
```

If 0 was the first value read, the body of the while statement would not execute.

Recall that the expression cin >> nextValue has the value true if the input operation was successful and false otherwise. Thus, you could revise the previous statements as

```
int nextValue = 0;
int sum = 0;
while ( (cin >> nextValue) && (nextValue > 0) )
    sum += nextValue;
```

# A.5.2 The for Statement

A for statement lists the initialization, testing, and updating steps in one location

The for statement provides for counted loops and has the general form

```
for (initialize; test; update)
statement
```

where initialize, test, and update are expressions. Typically, initialize is an assignment expression that initializes a counter to control the loop. This initialization occurs only once. Then if test, which is usually a logical expression, is true, statement executes. The expression update executes next, usually incrementing or decrementing the counter. This sequence of events repeats, beginning with the evaluation of test, until the value of test is false.