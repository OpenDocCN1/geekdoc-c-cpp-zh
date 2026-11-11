The program executes this part after running the loop’s body. Keep in mind that this statement updates the counter’s value.

# *The Loop’s Body*

This part consists of C# statements. It can utilize the variables you declared in the loop’s initializing fragment. Check the example below:

```
```csharp
for (double sample = 10; sample > 1; sample--)
{
        System.Console.WriteLine(sample);
}
```
```

# *The Continue Operator*

In some cases, you need to stop the active iteration without ending the loop itself. You can accomplish this task using the C# operator called “continue”. The example given below will illustrate how this operator works: