newsletter once, and then use a loop that sends the newsletter to each subscriber the code finds in a database.

Loops come as a few different types, each with their own usage and advantages.

# The For Loop

The For Loop simply repeats its code a predefined number of times. You define the exact number of iterations when you set up the loop. The For Loop takes the following format:

```
VB.NET
For counter [ As datatype ] = start To end [ StepSize ]
' Code that must be executed for each iteration
Next [ counter ]
```

```
C#
for (startCondition; endregion; step definition)
{
  // Code must be executed for each iteration
}
```

This looks a little odd, but a concrete example makes this a lot easier to understand:

```
VB.NET
For loopCount As Integer = 1 To 10
Label.Text &= loopCount.ToString() & "<br />"
Next
```

```
C#
for (int loopCount = 1; loopCount <= 10)
{
  Label.Text += loopCount.ToString() + "<br />";
}
```

Although the syntax in both languages is quite different, both code examples perform the same action: they loop is started by the assignment of 1 to the variable loopCount. The value is converted to a String and assigned to the Label control. Then loopCount is increased by 1, and the loop continues. Since we used numbers from 1 to 10 followed by a break the loop runs until loopCount is 10, and then the loop ends. In this example, hard-coded numbers are used. However, you can replace the start and end conditions with dynamic values from variables or other objects. For example, if you're working with the roles you array earlier, you can write out each role in the array like this:

```
VB.NET
For loopCount As Integer = 0 To roles.Length
Label.Text &= roles(loopCount) & "<br />"
Next
```

```
C#
for (int loopCount = 0; loopCount < roles.Length; loopCount++)
{
  Label.Text += roles[loopCount] + "<br />";
}
```