The final value of sum would be printed if the WriteLine( ) method is placed in the body of the loop. However, you would also have nine additional printed lines. Every time sum changes, a line would be printed showing its new value. Thus, it is better to print the result after all the calculations have been performed.

You could modify Example 6-1 to allow the user to input the first and last values to be summed. Both operands in the conditional expression could be variables. Example 6-2 prompts the user for the boundaries.

# Example 6-2

```
```csharp
/* InputEndPointsWithWhile.cs        Author: Doyle
 * Demonstrates use of a loop to add any range
 * of values. User inputs start and stop values.
 * Displays the result after the loop is
 * completed.
 */
using System;
namespace InputEndPointsWithWhile
{
    class InputEndPointsWithWhile
    {
        static void Main( )
        {
            int sum = 0;
            int startValue,
                endValue;
            string inValue;
            Console.Write("Enter the beginning value. ");
            inValue = Console.ReadLine();
            startValue = Convert.ToInt32(inValue);
            Console.Write("Enter the last value. ");
            inValue = Console.ReadLine();
            endValue = Convert.ToInt32(inValue);
            Console.Write("Sum of values {0} through {1} ",
                startValue, endValue);
            while (startValue < endValue + 1)
            {
                sum = sum + startValue;
                startValue++;
            }
            Console.WriteLine("is {0}", sum);
        }
    }
}
```
```

There are a couple of interesting issues to consider with Example 6-2. The conditional expression now reads:

```
while (startValue < endValue + 1)
```