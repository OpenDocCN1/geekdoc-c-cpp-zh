```
```csharp
if (overallScore > 8.0)
{
    tasks.Add("Work with leadership to reward staff");
}
else
{
    tasks.Add("Work with employees for improvement ideas.");
}

if (responseRate < .33)
{
    tasks.Add("Research options to improve response rate.");
}
else if (responseRate > .33 && responseRate < .66)
{
{
```
```

Let's rewrite this block of code as a ternary to see them side by side. So above that statement, let's define a variable to hold the result of our ternary operation. So, I'll type out var newTask =, and then let's say overallScore > 8, which will still act as our conditional, just like below. And then we could use our ternary operator for the true scenario, which will result in a value of Work with leadership to reward staff.

```
```csharp
tasks.Add(overallScore > 8.0 ? "Work with leadership" : "Work with employees for ideas.");
```
```

Then we can add another half of our operator with a colon for the else condition and provide a value of Work with employees for improvement ideas. Now after this expression is evaluated, it will assign a task to our variable. On the next line, we can then say tasks.Add(newTask), and add that to our list. This code now produces the same result as the eight lines below it using only two lines. However, we can actually simplify this further by just passing the entire ternary expression into the tasks.Add method, similar to