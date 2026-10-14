will add up. The general rule is to use *Parallel.Invoke* only when it is worthwhile. You should reserve *Parallel.Invoke* for operations that are computationally intensive; otherwise, the overhead of creating and managing tasks can actually slow down an application.

The other key consideration for using the *Parallel* class is that parallel operations should be independent. For example, if you attempt to use *Parallel.For* to parallelize a loop in which iterations have a dependency on each other, the results will be unpredictable.

To see what I mean, look at the following code (you can find this example in the ParallelLoop solution, which is located in the \Microsoft Press\VCSBS\Chapter 23\ParallelLoop folder in your Documents folder):

Click here to view code image

```
using System;
using System.Threading;
using System.Threading.Tasks;

namespace ParallelLoop
{
    class Program
    {
        private static int accumulator = 0;

        static void Main(string[] args)
        {
            for (int i = 0; i < 100; i++)
            {
                AddToAccumulator(i);
            }
            Console.WriteLine($"Accumulator is {accumulator}");
        }

        private static void AddToAccumulator(int data)
        {
            if ((accumulator % 2) == 0)
            {
                accumulator += data;
            }
            else
            {
                accumulator -= data;
            }
        }
    }
}
```

This program iterates through the values from 0 to 99 and calls the *AddToAccumulator* method with each value in turn. The *AddToAccumulator* method examines the current value of the *accumulator* variable and, if it is even, adds the value of the parameter to the *accumulator* variable; otherwise, it subtracts the value of the parameter. At the end of the program, the result is