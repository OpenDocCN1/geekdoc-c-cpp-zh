```
Console.WriteLine("Max value is : {0}", ret);
Console.ReadLine();
}
}

```

The result given below is produced by the above example.

Max value is : 200

# Understanding Recursive Method Call

It is possible for a method to call itself. Such a process is called recursion. The following example illustrates the use of a recursive method call. Here, factorial is calculated for a given number with the help of a recursive method call.

```
using System;
namespace CalculatorApplication
{
    class NumberManipulator
    {
        public int factorial(int num)
        {
            /* local variable declaration */
            int result;
            if (num == 1)
            {
```