| To | Do this |
| Access a single array element | Write the name of the array variable, followed by the integer index of the element enclosed in square brackets. Remember, array indexing starts at 0, not 1. For example:

Click here to view code image
```csharp
bool initialElement = flags[0];n``` |
| Iterate through the elements of an array | Use a for statement or a foreach statement. For example:
Click here to view code image
```csharp
bool[] flags = { true, false, true, false };
for (int i = 0; i < flags.Length; i++)
{
    Console.WriteLine(flags[i]);
    foreach (bool flag in flags)
    {
        Console.WriteLine(flag);
    }
}
``` |
| Declare a multidimensional array variable | Write the name of the element type, followed by a set of square brackets, with a comma separator indicating the number of dimensions, followed by the name of the variable, followed by a semicolon. For example, use the following to create a two-dimensional array called table and initialize it to hold four rows of six columns:

```csharp
int[,] table;
table = new int[4,6];
```