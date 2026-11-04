Applications of Floating-Point Numbers
Floating-point numbers have numerous applications, especially for measured values. For example, when we speak of a "normal" body temperature of 98.6 degrees Fahrenheit, we need not be precise to a large number of digits. When we read the temperature on a thermometer as 98.6, it may actually be 98.5999473210643. Calling this number simply 98.6 is fine for most applications involving body temperatures. Similarly, we used type double to perform class-average calculations in Chapter 5. Due to the imprecise nature of floating-point numbers, type double is preferred over type float, because double variables can represent floating-point numbers more precisely. For this reason, we use type double throughout the book, unless we're manipulating monetary amounts, in which case we use decimal.

# 6.6 do...while Iteration Statement

The do...while iteration statement is similar to the while statement. In the while, the app tests the loop-continuation condition at the beginning of the loop, before executing the loop's body. If the condition is false, the body never executes. The do...while statement tests the loop-continuation condition after executing the loop's body; therefore, the body always executes at least once. When a do...while statement terminates, execution continues with the next statement in sequence. Figure 6.7 uses a do...while (lines 11–15) to output the numbers 1–10.

```
```csharp
// Fig. 6.7: DoWhileTest.cs
// do...while iteration statement.
using System;

class DoWhileTest
{
   static void Main()
   {
      int counter = 1; // initialize counter

      do
      {
         Console.Write( "{counter} " );
         ++counter;
      } while ( counter <= 10 ); // required semicolon

      Console.WriteLine();
   }
}
```
```

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|

Fig. 6.7 | do...while iteration statement.

Line 9 declares and initializes control variable counter. Upon entering the do...while statement, line 13 outputs counter's value, and line 14 increments counter. Then the app evaluates the loop-continuation test at the bottom of the loop (line 15). If the condition is true, the loop continues from the first body statement (line 13). If the condition is false, the loop terminates, and the app continues with the next statement after the loop (line 17).