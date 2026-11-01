You call up these methods like this:

```
```csharp
using System;

namespace Wrox.ProCSharp.Delegates
{
    delegate double DoubleOp(double x);

    class Program
    {
        static void Main()
        {
            DoubleOp[] operations =
            {
                MathOperations.MultiplyByTwo,
                MathOperations.Square
            };

            for (int i=0; i < operations.Length; i++)
            {
                Console.WriteLine("Using operations[{0}]: ", i);
                ProcessAndDisplayNumber(operations[i], 2.0);
                ProcessAndDisplayNumber(operations[i], 7.94);
                ProcessAndDisplayNumber(operations[i], 1.414);
                Console.WriteLine();
            }

            static void ProcessAndDisplayNumber(DoubleOp action, double value)
            {
                double result = action(value);
                Console.WriteLine(
                    "Value is {0}, result of operation is {1}", value, result);
            }
        }
    }
}
```
```

code snippet SimpleDelegate/Program.cs

In this code, you instantiate an array of DoubleOp delegates (remember that after you have defined a delegate class, you can basically instantiate instances just as you can with normal classes, so putting some into an array is no problem). Each element of the array gets initialized to refer to a different operation implemented by the MathOperations class. Then, you loop through the array, applying each operation to three different values. This illustrates one way of using delegates — that you can group methods together into an array using them, so that you can call several different methods in a loop.

The key lines in this code are the ones in which you actually pass each delegate to the ProcessAndDisplayNumber() method, for example:

```
ProcessAndDisplayNumber(operations[i], 2.0);
```

Here, you are passing in the name of a delegate but without any parameters. Given that operations[i] is a delegate, syntactically:

+   - operations[i] means the delegate (that is, the method represented by the delegate).
+   - operations[i] (2.0) means actually call this method, passing in the value in parentheses.