
# Chapter 22: Thread Synchronization

```cs
{
    get { return Program._Count; }
    set { Program._Count = value; }
}

public static void Main()
{
    Thread thread = new(Decrement);
    thread.Start();

    // Increment
    for(int i = 0; i < short.MaxValue; i++)
    {
        Count++;
    }

    thread.Join();
    Console.WriteLine("Main Count = {0}", Count);
}

public static void Decrement()
{
    for(int i = 0; i < short.MaxValue; i++)
    {
        Count--;
    }
    Console.WriteLine("Decrement Count = {0}", Count);
}
```

OUTPUT 22.8
Decrement Count = -32767
Main Count = 32767.01134

As in Listing 22.11, the value of Count for the thread executing Main() is never decremented by the thread executing Decrement(). For Main()'s thread, the initial value is a negative _Total and the final value is 0. In other words, with ThreadStaticAttribute the value of Count for each thread is specific to the thread and not accessible across threads.

Notice that unlike Listing 22.11, the value displayed for the decrement count does not have decimal digits, indicating it was never initialized to 0.01134. Although the value of _Count is assigned during declaration—private double _Count = 0.01134 in this example—only the static instance associated with the thread running the static constructor will be initialized. In Listing 22.12, only the thread executing Main() will have a thread local storage variable initialized to 0.01134. The value of _Count in Decrement() decrements always be initialized to 0 (default(double)) since _Count is a double.

Similarly, if a constructor initializes the thread local storage instance, only the constructor calling that thread will. For this reason, it is good practice to initialize a thread local storage field within the method that each thread initially calls. However, this is not always reasonable, especially in connection with async: Different pieces of computation might run on different threads, resulting in unexpectedly differing thread local storage values on each piece.

The decision to use thread local storage requires some degree of cost-benefit analysis. For example, consider using local storage for a database connection. Depending on the database management system, database connections are relatively expensive, so creating a connection for every thread could be costly. Similarly, locking a connection so that all database calls are synchronized significantly lower the ceiling on scalability. Each pattern has its costs and benefits, and the best choice depends largely on the individual implementation.

Another reason to use thread local storage is to commonly needed context information available to other methods without explicitly passing the data via parameters. For example, if multiple methods in the call stack require user security information, you can pass the data using thread local storage fields instead of parameters. This technique keeps APIs cleaner while still making the information available to methods in a thread-safe manner. Such an approach requires that the thread local data is always set—a step that is especially important on Tasks or other thread pool threads because the underlying threads are reused.

# Timers

On occasion, it is necessary to delay code execution for a specific period of time or to register for a notification after a specific period of time. Examples include refreshing the screen at specific time intervals, rather than immediately, when frequent data changes occur. One approach to implementing timers is to leverage the async/await pattern and the Task.Delay() method added in .NET 4.5. As we pointed out in Chapter 19, the key feature of TAP is that the code executing after an async call will continue in a supported thread context, avoiding any UI cross-threading issues. Listing 22.13 provides an example of how to use the Task.Delay() method.

LISTING 22.13: Using Task.Delay() as a Timer

```cs
using System;
using System.Threading.Tasks;

public class Pomodoro
{
    // ...

    private static async Task AsyncTask(System.Threading.CancellationToken token)
    {
        for(int minute = 0; minute < 25; minute++)
        {
            DisplayMinuteTicker(minute);
            for(int second = 0; second < 60; second++)
            {
                await Task.Delay(1000, token);
                if (token.IsCancellationRequested)
                {
                    break;
                }
                DisplaySecondTicker();
            }
        }
    }
    // ...
}
```

The call to Task.Delay(1000) will set a continuation that appears after it. Frankly, TAP's use of synchronization specifically addressed UI-related issues. Prior to that, it was necessary to use specific timer classes that were UI-thread safe. Others such as System.Windows.Forms.Timer, System.Threading.DispatcherTimer (if configured appropriately) are UI-thread friendly. Others, such as System.Threading.Timer, are optimized for performance.

# Controlling the COM Threading Model with STAThreadAttribute

With COM, different apartment-threading models determine the threading rules relating to COM objects. Fortunately, these rules—and the complexity that accompanied them—have disappeared from .NET as the program invokes COM components. Furthermore, apartment initialization does not occur unless a COM call is made. The caveat to this approach is that all threads (including those of Task) default to multithreaded apartment (MTA). In turn, care needs to be taken when invoking COM from other threads besides the main one.

COM interop is not necessarily an explicit action by the developer. Microsoft implemented many of the components within the .NET Framework by creating a runtime callable wrapper (RCW) rather than rewriting all of the functionality within managed code. As a result, COM calls are often made unknowingly. To ensure that these calls are always made from a single-threaded apartment, it is generally a good practice to decorate the main method of all Windows Forms executables with the System.STAThreadAttribute.

# Summary

In this chapter, we looked at various synchronization mechanisms and saw how a variety of classes are available to protect against race conditions. Coverage included the lock keyword, which leverages System.Threading.Monitor under the covers. Other synchronization classes include System.Threading.Interlocked, System.Threading.Mutex, System.Threading.WaitHandle, reset events, semaphores, and the concurrent collection classes.

In spite of all the progress made in improving multithreaded programming between early versions of .NET and today, synchronization of multithreaded programming remains complicated, with numerous pitfalls awaiting the unwary developer. To avoid these traps, several best practices have been identified, including consistently acquiring synchronization targets in the same order and wrapping static members with synchronization logic.

Before closing the chapter, we considered the Task.Delay() method, a .NET 4.5–introduced API for implementing a timer based on TAP.

The next chapter investigates another complex .NET technology: that of marshaling calls out of .NET and into unmanaged code using P/Invoke. In addition, it introduces a concept known as unsafe code, which C# uses to access memory pointers directly, as unmanaged code does (e.g., C++).
