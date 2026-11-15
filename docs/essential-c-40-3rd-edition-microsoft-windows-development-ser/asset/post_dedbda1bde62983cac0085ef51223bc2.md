
- IsBackground: Another thread configuration option is the thread.IsBackground property. By default, a thread is a foreground thread, meaning the process will not terminate until the thread completes. In contrast, setting the IsBackground property to true will allow process execution to terminate prior to a thread's completion.

- Priority: When using the Join() method, you can increase or decrease the thread's priority by setting the Priority to a new ThreadPriority enum value (Lowest, BelowNormal, Normal, AboveNormal, or Highest).

- ThreadState: A thread's state is accessible through the ThreadState property, a more precise reflection of the Boolean IsAlive property. The ThreadState enum flag values are Aborted, AbortRequested, Background, Running, Stopped, SleepRequested, SuspendRequested, Unstarted, and WaitSleepJoin. The flag names indicate activities that may occur on a thread. Two noteworthy methods are Thread.Sleep() and Abort().

- Thread.Sleep(): Thread.Sleep() is a static method that pauses the current thread for a period. A single parameter (in milliseconds, or a TimeSpan) specifies how long the active thread waits before continuing execution. This enables switching to a different thread for a specific period. This method is not for accurate timing. Returns can occur hundreds of milliseconds before or after the specified time.

- Abort(): A thread's Abort() method causes a ThreadAbortException to be thrown within the target thread at whatever location the thread is executing when Abort() is invoked. As already detailed, aborting a thread introduces uncertainty into the thread's behavior and could cause data integrity and resource cleanup problems. Developers should consider the Abort() method to be a last resort. Instead, they should rely on threads running to completion and/or signaling them to escape out of whatever code is running via shared state.

From this list of Thread members, only Join() and ThreadState have Task equivalents. For the most part, this is because there are generally preferable equivalents or the behavior of the member is undesirable as a best practice. For example, aborting a thread may threaten data integrity or inadequate resource de-allocation, as mentioned earlier in the chapter. Therefore, given the .NET Framework 4, developers should generally avoid these members in favor of their task equivalents or alternative patterns entirely.

In summary, the general priority for selecting from the asynchronous class options is Task, ThreadPool, and Thread. In other words, use TPL, but if that doesn't fit, use ThreadPool; if that still doesn't suffice, use Thread.

One particular Thread member that is likely to crop up more frequently because there is no Task or ThreadPool equivalent is Thread.Sleep(). Although, if it doesn't introduce too much unnecessary complexity, consider using a timer in place of Sleep().

## Thread Pooling

Regardless of the number of processors, an excess of threads negatively affects performance. To efficiently manage thread creation, TPL makes extensive use of CLR's thread pool, System.Threading.ThreadPool. Most importantly, the thread pool dynamically determines when to use existing threads rather than creating new ones. Fortunately, the .NET 3.5 Framework includes a version of the System.Threading.ThreadPool, so it is available even without TPL.

Accessing threads in ThreadPool is similar to explicit use of the Thread class except that the invocation is via a static method, QueueUserWorkItem() (see Listing 18.19).

### LISTING 18.19: Using ThreadPool Instead of Instantiating Threads Explicitly

```
using System;
using System.Threading;

public class Program
{
    public const int Repetitions = 1000;
    public static void Main()
    {
        ThreadPool.QueueUserWorkItem(DoWork, '.');

        for (int count = 0; count < Repetitions; count++)
        {
            Console.Write("-");
        }
    // Pause until the thread completes
    Thread.Sleep(1000);
}
public static void DoWork(object state)
{
    for (int count = 0; count < Repetitions; count++)
    {
        Console.Write(state);
    }
}
```

The output is similar to Output 18.9, an intermingling of . and -. This provides more-efficient execution on single- and multiprocessor computers. The efficiency is achieved by reusing threads over and over, rather than reconstructing them for every asynchronous call.

Unfortunately, thread pool usage is not without its pitfalls. Activities such as I/O operations and other framework methods that internally use the thread pool can consume threads as well. Consuming all threads within the pool can delay execution and, in extreme cases, cause a deadlock. Similarly, if the asynchronous code will take a long time to execute, then it is inappropriate to consume a shared thread from the thread pool and instead favor explicit Thread instantiation (use TaskCreationOptions.LongRunning given TPL as mentioned earlier).

Unfortunately, another disadvantage with the thread pool is that, unlike either Thread or Task, the ThreadPool API does not return a handle to the thread or task itself. This prevents the calling thread from controlling it with the thread management functions described earlier in the chapter. Just monitoring state is not available without explicitly adding a custom implementation. Assuming these deficiencies are not critical, developers should consider using the thread pool over explicit thread creation because of its increased efficiency—at least prior to .NET Framework 4 and TPL; the fact that TPL uses the thread pool internally indicates the significance of using it for the majority of multithreading scenarios.

## Unhandled Exceptions on the AppDomain

To catch all exceptions from a thread (for which appropriate handling is known), you surround the root code block with a try/catch/finally block, just as you would for all code within Main(). However, what happens if a third-party component creates an alternate thread and throws an unhandled exception from that thread? Similarly, what if queued work on the thread pool throws an exception? A try/catch block in Main() will not catch an exception on an alternate thread. Furthermore, without access to any “handle” that invoked the thread (such as a Task) there is no way to catch any exceptions that it might throw. Even if there was, the code could never appropriately recover from all possible exceptions and continue executing (in fact, this is why in .NET 4.0 exceptions such as System.StackOverflowException, for example, will not be caught and instead will tear down the application. The general unhandled-exceptions guideline is for the program to shut down and restart in a clean state instead of behaving erratically or hanging because of an invalid state.

However, instead of crashing suddenly or ignoring an unhandled exception entirely if it occurs on an alternate thread, it is often desirable to save any working data and/or log the exception for error reporting and future debugging. This requires a mechanism to register for notifications of unhandled exceptions.

Registering for unhandled exceptions on the main application domain occurs via an application domain’s UnhandledException event. Listing 18.20 demonstrates that process, and Output 18.10 shows the results.

### LISTING 18.20: Registering for Unhandled Exceptions

```
using System;
using System.Threading;
public class Program
{
    public static void Main()
    {
        try
        {
            // Register a callback to
            // receive notifications
            // of any unhandled exception.
            AppDomain.CurrentDomain.UnhandledException
            += OnUnhandledException;
            ThreadPool.QueueUserWorkItem(
                state =>
                {
                    throw new Exception(
                        "Arbitrary Exception");
                });

            // ...
            // Wait for the unhandled exception to fire
            // ADVANCED: Use ManualResetEvent to avoid
            // timing dependent code.
            Thread.Sleep(100000);

            Console.WriteLine("Still running...");
        }
        finally
        {
            Console.WriteLine("Exiting...");
        }
    }
}
```

```
static void OnUnhandledException(
    object sender,
    UnhandledExceptionEventArgs eventArgs)
{
    Exception exception =
        (Exception)eventArgs.ExceptionObject;
    Console.WriteLine("ERROR ({0}): ---> {1}",
        exception.GetType().Name,
        exception.Message,
        exception.InnerException.Message);
}
```

```
public static void ThrowException()
{
    throw new ApplicationException(
        "Arbitrary exception");
}
```

OUTPUT 18.10:

```
Still running...
Exiting...
ERROR (AggregateException):One or more errors occurred. ---> Arbitrary
Exception
```
