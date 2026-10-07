
## ADVANCED TOPIC

## Dealing with Unhandled Exceptions on a Thread

As we discussed earlier, an unhandled exception on any thread by default causes the application to shut down. An unhandled exception is a fatal, unexpected bug, and the exception may have occurred because a crucial data structure is corrupt. Since you have no idea what the program could possibly be doing, the safest thing to do is to shut down the whole thing immediately.

Ideally, no programs would throw unhandled exceptions on any thread; programs that do have bugs, and the best course of action is to find and fix the bug before the software is shipped to customers. However, rather than shutting down an application as soon as possible when an unhandled exception occurs, it is often desirable to save any working data and log the exception for error reporting and future debugging. This requires a mechanism to register notifications of unhandled exceptions.

With both the Microsoft .NET Framework and .NET Core 2.0 (or later), every AppDomain provides such a mechanism, and to observe the unhandled exceptions that occur in an AppDomain, you must add a handler to the UnhandledException event. The UnhandledException event will fire for all unhandled exceptions on threads within the application domain, whether it is the main thread or a worker thread. Note that the purpose of this mechanism is notification; it does not permit the application to recover from the unhandled exception and continue executing. After the event handlers run, the application will display the operating system's error reporting dialog, and then the application will exit. (For console applications, the exception details will also appear on the console).

In Listing 19.7, we show how to create a second thread that throws an exception, which is then handled by the application domain's unhandled exception handler. For demonstration purposes, to ensure that threading issues do not come into play, we insert some artificial delays using Thread.Sleep. Output 19.4 shows the results.

## LISTING 19.7: Registering for Unhandled Exceptions

```
using System;
using System.Diagnostics;
using System.Threading;
```

```
public class Program {
    private static Stopwatch Clock { get; } = new Stopwatch();

    public static void Main() {
        try {
            Clock.Start();
            // Register a callback to receive notifications
            // of any unhandled exception

            AppDomain.CurrentDomain.UnhandledException += (s, e) => {
                Message("Event handler starting");
                Delay(4000);
            };
            Thread thread = new(() => {
                Message("Throwing exception.");
                throw new Exception();
            });
            thread.Start();

            Delay(2000);
        } finally {
            Message("Finally block running.");
        }
    }

    static void Delay(int i) {
        Message($"Sleeping for {i} ms");
        Thread.Sleep(i);
        Message("Awake");
    }

    static void Message(string text) {
        Console.WriteLine("{0}:{1:0000}:{2}", Thread.CurrentThread.ManagedThreadId, Clock.ElapsedMilliseconds, text);
    }
}
```

## Chapter 19: Introducing Multithreading

OUTPUT 19.4

```
3:0047:Throwing exception.
3:0052:Unhandled exception handler starting.
3:0055:Sleeping for 4000 ms
1:0056:Sleeping for 2000 ms
1:2059:Awake
1:2060:Finally block running.
3:4059:Awake
Unhandled Exception: System.Exception: Exception of type 'System.
Exception' was thrown.
```

As you see in Output 19.4, the new thread is assigned thread ID 3 and the main thread is assigned thread ID 1. The operating system schedules thread 3 to run for a while; it throws an unhandled exception, the event handler is invoked, and it goes to sleep. Soon thereafter, the operating system realizes that thread 1 can be scheduled, its code immediately puts it to sleep. Thread 1 wakes up and first runs the finally block, and then 2 seconds later thread 3 wakes up, and the unhandled exception finally crashes the process.

This sequence of events—the event handler executing, and the process crashing after it is finished—is typical but not guaranteed. The moment there is an unhandled exception in your program, all bets are off; the program is now in an unknown and potentially unstable state, so its behavior is unpredictable. In this case, you can see, the CLR allows the main thread to continue running and executing its finally block, even though it knows that by the time control gets to the finally block, another thread is in the AppDomain's unhandled exception event handler.

To emphasize this point, try changing the delays so that the main thread sleeps longer than the exception thread. In that scenario, the finally block will never execute! The process will be destroyed by the unhandled exception before thread 1 wakes up. You can also get different results depending on whether the exception-throwing thread is or not created by the thread pool. The best practice, therefore, is to avoid all possible unhandled exceptions, whether they occur in worker threads or in the main thread.

How does this pertain to tasks? What if there are unfinished tasks hanging around the system when you want to shut it down? We look at task cancellation in the next section.

## Guidelines

- **AVOID** writing programs that produce unhandled exceptions on any thread.
- **CONSIDER** registering an unhandled exception event handler for debugging, logging, and emergency shutdown purposes.
- **DO** cancel unfinished tasks rather than allowing them to run during application shutdown.

## Canceling a Task

Earlier in this chapter, we described why it's a bad idea to rudely abort a thread so as to cancel a task being performed by that thread. The TPL uses *cooperative cancellation*, a far more polite, robust, and reliable technique for safely canceling a task that is no longer needed. A task that supports cancellation monitors a CancellationToken (found in the System.Threading namespace) by periodically polling it to see if a cancellation request has been issued. Listing 19.8 demonstrates both the cancellation request and the response to the request. Output 19.5 shows the results.

Listing 19.8: Canceling a Task Using CancellationToken

```
using System;
using System.Threading;
using System.Threading.Tasks;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;

public class Program
{
    public static void Main()
    {
        string stars =
CancellationToken cancellationSource = new();
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task task = Task.Run(
            () =>
                WritePi(cancellationSource.Token,
                       cancellationSource.Token);

        // Wait for the user's
        Console.ReadLine();

```
```
        cancellationSource.Cancel();
        Console.WriteLine(stars);
        task.Wait();
        Console.WriteLine();
    }
}

```
    private static void WritePi(CancellationToken cancellation)
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

OUTPUT 19.5

```
Push ENTER to exit.
3.1415926535089793238462643382795028841...
************************************************
2
```

After starting the task, Console.Read() blocks the main thread. At the same time, the task continues to execute, calculating the next digit of pi and printing it out. Once the user presses Enter, the execution encounters a call to CancellationToken.Cancel(). In Listing 19.2, we split the call to task.Wait() and print out a line of asterisks in between. The 2 appears in Output 19.5 because CancellationTokenSource.Cancel() doesn’t rudely stop the task. The task keeps on running until it checks the token, and politely shuts down when it sees the owner of the task is requesting cancellation.

To monitor the IsCancellationRequested property, a copy of the CancellationToken (retrieved from CancellationTokenSource.Token) is passed to the task. In Listing 19.7, we then occasionally check the CancellationToken property on IsCancellationRequested property; in this case, we check after each digit calculation. If IsCancellationRequested returns true, the loop exits. Unlike a thread abort, which would throw an exception at essentially a random point, we exit the loop using normal control flow.

- A CancellationToken, not a CancellationTokenSource, is given to the asynchronous task. A CancellationToken enables polling for a cancellation request; the CancellationTokenSource provides the token and signals when it is canceled (see Figure 19.3). By passing the CancellationToken rather than the CancellationTokenSource, we don’t have to worry about thread synchronization issues on the CancellationTokenSource because the latter remains accessible to only the original thread.

- A CancellationToken is a struct, so it is copied by value. The value returned by CancellationTokenSource.Token produces a copy of the token. The fact that CancellationToken is a value type and a copy is created in thread-safe access to CancellationTokenSource.Token—it is available only from within the WritePi() method.
