
task.Start();
faultedTask.Wait();
Trace.Assert(parentTaskFaulted);
if (task.IsFaulted)
{
    task.Wait();
}
else
{
    Console.WriteLine(
        "ERROR: {0}", task.Exception.Message);
}
}
}

### Output 18.4:

```
ERROR: in the application.
```

Rather than calling task.Wait() and throwing an exception, Listing 18.5 uses a ContinueWith() task and calls continueWithTask.Wait() on this task to determine that the original task completed. In addition, the call to task.ContinueWith() passes a TaskContinuationOptions.OnlyOnFaulted parameter causing this continuation task to execute only if the antecedent task throws an exception. Without the additional parameter, the code execution would have been the same as Listing 18.5 because it would have executed regardless. By specifying the TaskContinuationOptions.OnlyOnFaulted flag, we are able to “register” for the fault “notification.”

Notice that to retrieve the unhandled exception on the original task we use the Exception property. The result is an output identical to Output 18.3.

## Canceling a Task

One particular functional difference between the .NET 3.5 and earlier APIs versus the .NET Framework 4 APIs is support for cancellation requests on threads. The threading API in .NET 3.5 and earlier has little support for cancellation requests and instead relies on a “rude” interruption approach. In this approach, the cancellation of a thread is forced and the target thread has little or no choice about the matter. Calling thread-abort, unloading the AppDomain, or killing the process are all examples of “rude” interruption. Such unexpected interruptions as aborting a thread can potentially occur during execution of a vital code block, threatening data integrity caused by partial data updates or inadequate resource de-allocation. Aborting a thread causes a ThreadAbortException exception to occur anywhere within the target thread’s execution. This introduces uncertainty into the thread’s behavior. (To complicate matters, the target thread’s abort call could be rejected by handling the ThreadAbortException exception and issuing a reset abort method call inside the abort-targeted thread—rendering uncertainty in the abort-issuing thread.) Similarly, if the abort-targeted thread is running unmanaged code, the ThreadAbortException exception will not throw until the code returns to managed execution. As a result, except in rare circumstances, developers should consider the rude interruption approach a last resort at best.

Of course, the earlier APIs are still fully available in the .NET Framework 4, but the additional PLINQ- and TPL-based APIs support only a cancellation request approach in which the target Task opts in to the cancellation request—a process known as cooperative cancellation. Instead of one “thread” aborting another, the cancellation API “requests” a Task to cancel. By checking the cancellation flag—a System.Threading.CancellationToken—the task targeted for cancellation can respond appropriately to the cancellation request.

Listing 18.6 demonstrates both the request and the response to the request. Note that this sample uses a PiCalculator.Calculate() method that we will delve into further in the Executing Iterations in Parallel section.

### Listing 18.6: Canceling a Task Using CancellationToken

```
using System;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        string stars = "*".PadRight(Console.WindowWidth-1, '*');
        Console.WriteLine("Push ENTER to exit.");

        CancellationTokenSource cancellationTokenSource =
            new CancellationTokenSource();
        Task task = Task.Factory.StartNew(
            () =>
            {
                WritePi(cancellationTokenSource.Token);
            },
            cancellationTokenSource.Token);

        // Wait for the user's input
        Console.ReadLine();

        cancellationTokenSource.Cancel();
        Console.WriteLine(stars);
        task.Wait();
        Console.WriteLine();
    }

    private static void WritePi(
        CancellationToken cancellationToken)
    {
        const int batchSize = 1;
        string piSection = string.Empty;
        int i = 0;

        while (!cancellationToken.IsCancellationRequested
            || i == int.MaxValue)
        {
            piSection = PiCalculator.Calculate(
                batchSize, (i++) * batchSize);
            Console.Write(piSection);
        }
    }
}
```

After starting the Task, a Console.ReadLine() blocks the main thread. At the same time, the task continues to execute, calculating the next digit of pi and printing it out. Once the user presses Enter, the execution encounters a call to CancellationTokenSource.Cancel(). In Listing 18.6, we split the call to cancellationTokenSource.Cancel() from the call to task.Wait() and print out * in between. The purpose of this is to show that quite possibly an additional iteration will occur before the cancellation token is observed—hence the additional 2 in Output 18.5 following the stars. The 2 appears because the CancellationTokenSource.Cancel() doesn't rudely stop the Task from executing.

### Output 18.5:

```
Push ENTER to exit.
31.415926535897932384626433832795028841971693993751058209749445923078164
0A62B4B6796E810B3D5295291770879B2140B06513282D06A470938446095505822317253
97402062A1B17F0
*****************************************************************
2
```

Rather, the Cancel() call sets the IsCancellationRequested property on all cancellation tokens copied from CancellationTokenSource.Token. There are a couple things to note from the previous sentence.

- Cancellation token: A CancellationToken, not a CancellationTokenSource, is evaluated in the asynchronous task. A CancellationToken is seemingly similar to the CancellationTokenSource except that the CancellationToken is for monitoring and responding to a cancellation request while the CancellationTokenSource is for canceling the task itself (see Figure 18.2).
- Copied: A CancellationToken is a struct, so calling CancellationTokenSource.Token will create a copy of the token. As a result, all instances of the cancellation token will be thread-safe.

![](img/ef1bd88b5fdf5fb56f8510479607fe66_769_0.png)

### FIGURE 18.2: CancellationTokenSource and CancellationToken Class Diagrams

To monitor the IsCancellationRequested property an instance of the CancellationToken (retrieved from CancellationTokenSource.Token) is passed to the parallel task. In Listing 18.6, we then check the IsCancellationRequested property on the CancellationToken parameter after each digit calculation. If IsCancellationRequested returns true, the while loop exits.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes a listener on the corresponding CancellationTokenSource’s Cancel() (see Listing 18.7 later in the chapter).

Since canceling before completing is expected behavior in this program, Listing 18.6 does not throw a System.Threading.Tasks.TaskCanceledException. Because of this, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in fact cancelled. In this example, there is no need for such an indication; however, TPL does include the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be the TPL pattern for reporting it. Instead of throwing the exception explicitly, CancellationToken includes a ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

Throwing the TaskCanceledException on the executing Task results in an AggregateException thrown on Task completion members: task.Wait(), Task.WaitAny(), or task.Result.

This example demonstrates how a long-running operation (calculating pi almost indefinitely) can monitor for a cancellation request and respond if one occurs. There are some cases, however, when cancellation can occur without explicitly coding for it within the target task. (For example, the Parallel class discussed later in the chapter offers such a behavior by default.)

## Long-Running Tasks

As noted earlier in the chapter, Tasks provide an abstraction over the operating system threads so that the thread pool can efficiently manage
