# Introduction to File Input

One point that you should note when using the continue statement in a loop is that the continue statement transfers control to the update expression. So, any loop variable will be updated immediately after the continue statement is executed.

Note that a break statement completes the loop. In contrast, a continue statement merely ends one iteration (if any) continues the loop. You will find it instructive to compare the details of the programs in Displays 2.8 and 2.9. Pay particular attention to the change in controlling the Boolean expression.
Note that you never absolutely need a break or continue statement. The programs in Displays 2.8 and 2.9 can be rewritten so that neither uses a break or continue statement. The continue statement can be particularly tricky and can make your code hard to read. It may be best to use the continue statement completely or at least only on rare occasions.

![](bbox=[0.048, 0.355, 0.168, 0.431])

# Nested Loops

It is perfectly legal to nest one loop statement inside another loop statement. When doing so, make sure that any break or continue statement is the innermost loop (switch) statement containing the break or continue statement. It is best to avoid nested loops by placing the inner loop inside a function definition and placing the outer loop. We describe how to write your own functions in Chapter 3.

![](bbox=[0.048, 0.52, 0.178, 0.538])

# Self-Test Exercises

+   36. What does a break statement do? Where is it legal to put a break statement?
37. Predict the output of the following loops:

```
int n, m;
for (n = 1; n <= 10; n++)
    for (m = 10; m >= 1; m--)
        cout << n << " " << times << " " << m
            cout << " = " << n << " * " << m << endl;
```

# 2.4 Introduction to File Input

> You shall see them on a beautiful quarto page, where a neat rivulet of text shall meander through a margin of margin.

RICHARD BRINSLEY SHERIDAN, *The School for Scandal*

Now you should be familiar with using cin to read data from the keyboard. cin is an example of something called an input stream. We can also connect an input stream to a file on the disk. This once up we can read the file in almost exactly the same way we read from cin. Details about reading and writing to files are not discussed until Chapter 12 and require an understanding of programming concepts we have not

![](bbox=[0.048, 0.878, 0.152, 0.89])