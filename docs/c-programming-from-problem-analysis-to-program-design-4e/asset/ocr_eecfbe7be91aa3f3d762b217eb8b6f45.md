```
```csharp
public static int DetermineLargest(int value1, int value2)
{
    int largestOne;        //Local variable declared to
                           //facilitate single exit from method
    if (value1 > value2)
    {
        largestOne = value1;
    }
    else
    {
        largestOne = value2;
    }
    return largestOne;
}

public static void PrintResults(int largestOne)
{
    Console.WriteLine( );
    Console.WriteLine("The largest value entered was "
                      + largestOne);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(largestOne));
    Console.ReadLine( );
}
}
}
```
```

When you are writing selection statements, try to avoid repeating code. Instead of duplicating statements for both the true and false statements, pull out common statements and place them before or after the selection statement. You might have been tempted to solve the problem presented for Example 5-13 with the following two-way if statement:

```
```csharp
if (value1 > value2)
{
    Console.WriteLine("The largest value entered was "
                      + value1);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value1));
}
else
{
    Console.WriteLine("The largest value entered was "
                      + value2);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value2));
}
```
```