Altogether our loop is

```
Loop
    Read next value.
    If value is higher than the highest temperature, set highest temperature to that value,
        highest month to current month.
    Increment current month.
```

# Step 2

Specify the loop condition.

What goal do you want to reach in your loop? Typical examples are:

+   - Has the counter reached the final value?
+   - Have you read the last input value?
+   - Has a value reached a given threshold?

In our example, we simply want the current month to reach 12.

# Step 3

Determine the loop type.

We distinguish between two major loop types. A definite or count-controlled loop is executed a definite number of times. In an indefinite or event-controlled loop, the number of iterations is not known in advance—the loop is executed until some event happens. A typical example of the latter is a loop that reads data until a sentinel is encountered.
If you know in advance how many times a loop is repeated, use a for statement. For other loops, consider the loop condition. Do you need to complete one iteration of the loop body before you can tell when to terminate the loop? In that case, you should choose a do loop. Otherwise, use a while loop.
In our example, we read 12 temperature values. Therefore, we choose a for loop.

# Step 4

Set up variables for entering the loop for the first time.

List all variables that are used and updated in the loop, and determine how to initialize them. Commonly, counters are initialized with 0 or 1, totals with 0.
In our example, the variables are

```
current month
highest value
highest month
```

We need to be careful how we set up the highest temperature value. We can’t simply set it to 0. After all, our program needs to work with temperature values from Antarctica, all of which may be negative.
A good option is to set the highest temperature value to the first input value. Of course, then we need to remember to only read in another 11 values, with the current month starting at 2.
We also need to initialize the highest month with 1. After all, in an Australian city, we may never find a month that is warmer than January.

# Step 5

Process the result after the loop has finished.

In many cases, the desired result is simply a variable that was updated in the loop body. For example, in our temperature program, the result is the highest month. Sometimes, the loop computes values that contribute to the final result. For example, suppose you are asked to average the temperatures. Then the loop should compute the sum, not the average. After the loop has completed, you are ready to compute the average: divide the sum by the number of inputs.