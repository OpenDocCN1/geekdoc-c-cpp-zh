never evaluate to false. Careful thought must focus on how the loop will end with a normal termination. Without incrementing the counter used in the conditional expression, the loop would go on indefinitely.

Why not put the following statement, which began on Line 8, inside the loop body?
Console.WriteLine("Sum of values 1 through 10 is " + sum);

The final value of sum would be printed if the WriteLine() method is placed in the body of the loop. However, you would also have nine additional printed lines. Every time sum changes, a line would be printed showing its new value. Thus, it is better to print the result after all the calculations have been performed.

You could modify Example 6-1 to allow the user to input the first and last values to be summed. Both operands in the conditional expression could be variables. Example 6-2 prompts the user for the boundaries.

# EXAMPLE 6.2

```
/* InputEndPointsWithWhile.cs    Author: Doyle
 * Demonstrates use of a loop to add any range
 * of values. User inputs start and stop values.
 * Displays the result after the loop is
 * completed.
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace InputEndPointsWithWhile
{
    class InputEndPointsWithWhile
    {
        static void Main()
        {
            int sum = 0;
            int startValue,
                endValue;
            string inValue;
            Console.Write("Enter the beginning value: ");
            inValue = Console.ReadLine();
            if (int.TryParse(inValue, out startValue) == false)
                Console.WriteLine("Invalid input - 0 recorded for start value");
            Console.Write("Enter the last value: ");
            inValue = Console.ReadLine();
            if (int.TryParse(inValue, out endValue) == false)
                Console.WriteLine("Invalid input - 0 recorded for end value");
            Console.Write("Sum of values {0} through {1} ",
                startValue, endValue);
```