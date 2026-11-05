# EXAMPLE 6.19

```
int total = 0;
for (int nValue = 0; nValue < 10; nValue++)
{
    if (nValue % 2 == 0)
    {
        continue;
    }
    total += nValue;
    Console.Write(nValue + "\t");
}
Console.WriteLine("\nTotal is equal to {0}.", total);
```

The output for this code is:

1      3      5      7      9
Total is equal to 25.

Note that the difference between the break and continue statements is that the continue statement does not stop the execution of the loop body, but rather, halts that iteration and transfers control to the next iteration of the loop.

The other jump statements in C# are goto, throw, and return. You will learn about the throw statement with exception handling in Chapter 12. You have used the return statement in your value-returning methods. The goto statement transfers control to a statement that is marked by a label. The goto statement has a bad reputation. It is associated with poorly designed spaghetti code that is difficult to debug and maintain. You should not use a goto jump statement in your programs.

The break and continue statements should also be used sparingly. It is appropriate and a requirement that you use a break statement with a switch statement. However, when you use break and continue statements with a loop, you are violating the single entry and single exit guideline for developing a loop. What this means is that there should be only one way to enter a loop and one way to exit. When you exit a loop from multiple locations, it becomes more difficult to debug. The loop might end because the condition evaluates to false or it might end prematurely because of the break. This adds complications when you are trying to walk through the logic.

# Deciding Which Loop to Use

The decision regarding which type of loop to use is sometimes a personal choice; however, there are some considerations you might want to acknowledge and allow to overrule your personal biases. Remember that the body of the do...while is always executed at least once. Thus, you should avoid using this form if there is the possibility that the loop body should not be executed when certain types of data are input into your program. Conversely, if you know your loop will always be executed at least once, the do...while is a good option.