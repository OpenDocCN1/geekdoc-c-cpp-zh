![](bbox=[0.52, 0.12, 0.68, 0.3])

# FIGURE 6.1 The logic of a do loop

The following code prints the numbers from 1 to 5 using a do loop. Compare this code with the similar example in Chapter 5 that uses a while loop to accomplish the same task.

```
int count = 0;
do
{
    count++;
    System.out.println (count);
}
while (count < 5);
```

# KEY CONCEPT

A do statement executes its loop body at least once.

Note that the do loop begins simply with the reserved word do. The body of the do loop continues until the while clause that contains the boolean condition that determines whether the loop body will be executed again. Sometimes it is difficult to determine whether a line of code that begins with the reserved word while is the beginning of a while loop or the end of a do loop.

Let’s look at another example of the do loop. The program called ReverseNumber, shown in Listing 6.2, reads an integer from the user and reverses its digits mathematically.

# Do Statement

![](bbox=[0.3, 0.82, 0.78, 0.87])

The do loop repeatedly executes the specified Statement as long as the boolean Expression is true. The Statement is executed at least once, then the Expression is evaluated to determine whether the Statement should be executed again.