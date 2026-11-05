![](bbox=[0.24, 0.09, 0.7, 0.58])

Figure 6-1 Pretest loop

# Counter-Controlled Loop

Many programs you develop require that you write one or more statements that must be performed more than once. When you know the number of times the statements must be executed, you can create a counter-controlled loop. With a counter-controlled loop, a variable simulating a counter is used as the loop control variable to keep track of the number of iterations. Example 6-1 adds values to an accumulator. The variable, sum, is initialized to zero and the positive integers 1 through 10 are added to the sum memory location, one value at a time.

# Example 6-1

```
```csharp
/* SummedValues.cs      Author: Doyle
 * Demonstrates use of a loop to add 10
 * integers. Displays the total after
 * the loop body is completed.
 */
using System;
namespace SummedValues
{
    class SummedValues
    {
        static void Main( )
```
```