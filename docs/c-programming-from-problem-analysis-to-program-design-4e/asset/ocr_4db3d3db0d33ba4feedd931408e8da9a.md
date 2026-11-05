Figure 6–12 illustrates the flow of execution in a posttest loop.

![](bbox=[0.25, 0.18, 0.78, 0.7])

# FIGURE 6-12 Do...while loop

A do...while loop is used in Example 6-14 to display numbers and their squares. The first value printed is 10. Each iteration through the loop decreases the counter by one until the counter reaches zero.

# EXAMPLE 6.14

```
int counter = 10;
do    // No semicolon on this line
{
    Console.WriteLine(counter + "\t" + Math.Pow(counter, 2));
    counter--;
}
while (counter > 0);
```