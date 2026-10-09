# **LISTING 19.5: Calling Task.ContinueWith()**

```
```
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Before");
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task taskA =
            Task.Run( ( ) =>
                Console.WriteLine("Starting..."))
                .ContinueWith(antecedent =>
                    Console.WriteLine("Continuing A..."));
        Task taskB = taskA.ContinueWith( antecedent =>
            Console.WriteLine("Continuing B..."));
        Task taskC = taskA.ContinueWith( antecedent =>
            Console.WriteLine("Continuing C..."));
        Task.WaitAll(taskB, taskC);
        Console.WriteLine("Finished!");
    }
}
```
```

# **OUTPUT 19.2**

![](bbox=[0.15, 0.55, 0.85, 0.65])

The `ContinueWith()` method enables "chaining" two tasks together, such that when the predecessor task—the **antecedent task**—completes, the second task—the **continuation task**—is automatically started asynchronously. In Listing 19.5, for example, `Console.WriteLine("Starting...")` is the antecedent task body and `Console.WriteLine("Continuing A...")` is its continuation task body. The continuation task takes a `Task` as its argument (antecedent), thereby allowing the continuation task's code to access the antecedent task's completion state. When the antecedent task is completed, the continuation task starts automatically, asynchronously executing the second delegate and passing the just-completed antecedent task as an argument to that delegate. Furthermore, since the `ContinueWith()`