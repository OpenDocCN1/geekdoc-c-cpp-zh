Although all delegate data types derive indirectly from System.Delegate, the C# compiler does not allow you to declare a class that derives directly or indirectly from System.Delegate or System.MulticastDelegate. As a consequence, the code shown in Listing 12.9 is not valid.

# LISTING 12.9: System.Delegate Cannot Explicitly Be a Base Class

```
// ERROR: 'ComparisonHandler' cannot
// inherit from special class 'System.Delegate'
public class ComparisonHandler: System.Delegate
{
    // ...
}
```

Passing the delegate to specify the sort order is a significantly more flexible strategy than using the approach described at the beginning of this chapter. By passing a delegate you can change the sort order to be alphabetical simply by adding an alternative delegate to convert integers to strings as part of the comparison. Listing 12.10 shows a full listing that demonstrates alphabetical sorting, and Output 12.1 shows the results.

# LISTING 12.10: Using a Different ComparisonHandler-Compatible Method

```
using System;
class DelegateSample
{
    public delegate bool ComparisonHandler(int first, int second);
    public static void BubbleSort(
        int[] items, ComparisonHandler comparisonMethod)
    {
        int i;
        int j;
        int temp;
        for (i = items.Length - 1; i >= 0; i--)
        {
            for (j = 1; j <= i; j++)
            {
                if (comparisonMethod(items[j - 1], items[j]))
                {
                    temp = items[j - 1];
                    items[j - 1] = items[j];
                    items[j] = temp;
                }
            }
        }
    }
```