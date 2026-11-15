characteristics are suboptimal given other approaches—namely Thread, ThreadPool, and TPL. Therefore, developers should tend to favor one of these alternatives rather than implementing new development using the asynchronous delegate invocation API. Further discussion of the pattern is included in the Advanced Topic text so that developers who encounter it will understand how it works.

# ADVANCED TOPIC

# Asynchronous Delegate Invocation in Detail

With asynchronous delegate invocation, you do not code using an explicit reference to Task or Thread. Instead, you use delegate instances and the compiler-generated BeginInvoke() and EndInvoke() methods—whose implementation requests threads from the ThreadPool. Consider the code in Listing 1919.

# LISTING 19.19: Asynchronous Delegate Invocation

```
using System;

public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Application started...");

        Console.WriteLine("Starting thread...");
        Func<int, string> workerMethod =
            PicCalculator.Calculate;
        IAsyncResult asyncResult =
            workerMethod.BeginInvoke(500, null, null);

        // Display progress as progress bar.
        while (!asyncResult.AsyncWaitHandle.WaitOne(
            100, false))
        {
            Console.Write('.');
        }
        Console.WriteLine();

        Console.WriteLine("Thread ending...");
        Console.WriteLine(
            workerMethod.EndInvoke(asyncResult));
    }
}
```