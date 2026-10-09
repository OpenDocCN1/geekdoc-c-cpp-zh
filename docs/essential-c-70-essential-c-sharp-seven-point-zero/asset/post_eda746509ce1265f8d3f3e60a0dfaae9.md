
As a result, there is no need for synchronization, as there is no point in synchronizing data that occurs within only a single thread's context. Two examples of thread local storage implementations are `ThreadLocal<T>` and `ThreadStaticAttribute`.

## ThreadLocal<T>

Use of thread local storage with Microsoft .NET Framework 4 or later involves declaring a field (or variable, in the case of closure by the compiler) of type `ThreadLocal<T>`. The result is a different instance of the field for each thread, as demonstrated in Listing 20.11 and Output 20.7. Note that a different instance exists even if the field is static.

### LISTING 20.11: Using `ThreadLocal<T>` for Thread Local Storage

```csharp
using System;
using System.Threading;

public class Program
{
    static ThreadLocal<double> _Count = 
        new ThreadLocal<double>(() => 0.01134);

    public static double Count
    {
        get { return _Count.Value; }
        set { _Count.Value = value; }
    }

    public static void Main()
    {
        Thread thread = new Thread(Decrement);
        thread.Start();

        // Increment
        for(double i = 0; i < short.MaxValue; i++)
        {
            Count++;
        }

        thread.Join();
        Console.WriteLine("Main Count = {0}", Count);
    }

    static void Decrement()
    {
        Count = -Count;
    }
}
```

### OUTPUT 20.7

```text
Decrement Count = -32767.01134
Main Count = 32767.01134
```

As Output 20.7 demonstrates, the value of Count for the thread executing Main() is never decremented by the thread executing Decrement(). For Main()'s thread, the initial value is 0.01134 and the final value is 32767.01134. Decrement() has similar values, except that they are negative. As Count is based on the static field of type ThreadLocal<T>, the thread running Main() and the thread running Decrement() have independent values stored in _Count.Value.

## Thread Local Storage with ThreadStaticAttribute

Decorating a static field with ThreadStaticAttribute, as in Listing 20.12, is a second way to designate a static variable as an instance per thread. This technique has a few caveats relative to ThreadLocal<T>, but it also has the advantage of being available prior to Microsoft .NET Framework 4. (Also, since ThreadLocal<T> is based on the ThreadStaticAttribute, it would consume less memory and give a slight performance advantage given frequently enough repeated small iterations.)

### LISTING 20.12: Using ThreadStaticAttribute for Thread Local Storage

```csharp
using System;
using System.Threading;

public class Program
{
    [ThreadStatic]
    static double _Count = 0.01134;
    public static double Count
    {
        get { return Program._Count; }
        set { Program._Count = value; }
    }

    public static void Main()
    {
        Thread thread = new Thread(Decrement);
        thread.Start();

        // Increment
        for(int i = 0; i < short.MaxValue; i++)
        {
            Count++;
        }

        thread.Join();
        Console.WriteLine("Main Count = {0}", Count);
    }

    static void Decrement()
    {
        for(int i = 0; i < short.MaxValue; i++)
        {
            Count--;
        }
        Console.WriteLine("Decrement Count = {0}", Count);
    }
}
```

The results of Listing 20.12 appear in Output 20.8.

### OUTPUT 20.8

```text
Decrement Count = -32767
Main Count = 32767.01134
```

As in Listing 20.11, the value of Count for the thread executing Main() is never decremented by the thread executing Decrement(). For Main()'s thread, the initial value is a negative _Total and the final value is 0. In other words, with ThreadStaticAttribute the value of Count for each thread is specific to the thread and not accessible across threads.

Notice that unlike with Listing 20.11, the value displayed for the decrement count does not have any decimal digits, indicating it was never initialized to 0.01134. Although the value of _Count is assigned during declaration—private double _Count = 0.01134 in this example—only the thread static instance associated with the thread running the static constructor will be initialized. In Listing 20.12, only the thread executing Main() will have a thread local storage variable initialized to 0.01134. The value of _Count that Decrement() decrements will always be initialized to 0 (default(double) since _Count is an double). Similarly, if a constructor initializes a thread local storage field, only the constructor calling that thread will initialize the thread local storage instance. For this reason, it is a good practice to initialize a thread local storage field within the method that each thread initially calls. However, this is not always reasonable, especially in connection with async, in which different pieces of computation might run on different threads, resulting in unexpectedly differing thread local storage values on each piece.

The decision to use thread local storage requires some degree of cost– benefit analysis. For example, consider using thread local storage for a data- base connection. Depending on the database management system, database connections are relatively expensive, so creating a connection for every thread could be costly. Similarly, locking a connection so that all database calls are synchronized places a significantly lower ceiling on scalability. Each pattern has its costs and benefits, and the best choice depends largely on the individual implementation.

Another reason to use thread local storage is to make commonly needed context information available to other methods without explicitly passing the data via parameters. For example, if multiple methods in the call stack require user security information, you can pass the data using thread local storage fields instead of as parameters. This technique keeps APIs cleaner while still making the information available to methods in a thread-safe manner. Such an approach requires that you ensure the thread local data is always set— a step that is especially important on Tasks or other thread pool threads because the underlying threads are reused.

## Timers

On occasion, it is necessary to delay code execution for a specific period of time or to register for a notification after a specific period of time. Examples include refreshing the screen at a specific period rather than immediately when frequent data changes occur. One approach to implementing timers is to leverage the async/await pattern of C# 5.0 and the Task.Delay() method added in .NET 4.5. As we pointed out in Chapter 19, one key feature of TAP is that the code executing after an async call will continue in a supported thread context, thereby avoiding any UI cross-threading issues. Listing 20.13 provides an example of how to use the Task.Delay() method.

### LISTING 20.13: Using Task.Delay() as a Timer

```csharp
using System;
using System.Threading.Tasks;

public class Pomodoro
{
    // ...
    private static async Task TickAsync(
        System.Threading.CancellationToken token)
    {
        for(int minute = 0; minute < 25; minute++)
        {
            DisplayMinuteTicker(minute);
            for(int second = 0; second < 60; second++)
            {
                await Task.Delay(1000);
                if(token.IsCancellationRequested) break;
                DisplaySecondTicker();
            }
            if(token.IsCancellationRequested) break;
        }
    }
}
```

The call to `Task.Delay(1000)` will set a countdown timer that triggers after 1 second and executes the continuation code that appears after it.

Fortunately, in C# 5.0, TAP’s use of the synchronization context specifically addressed executing UI-related code exclusively on the UI thread. Prior to that, it was necessary to use specific timer classes that were UI-thread-safe—or could be configured as such. Timers such as `System.Windows.Forms.Timer`, `System.Windows.Threading.DispatcherTimer`, and `System.Timers.Timer` (if configured appropriately) are UI-thread-friendly. Others, such as `System.Threading.Timer`, are optimized for performance.

## ADVANCED TOPIC

## Controlling the COM Threading Model with the STA[hread]Attribute

With COM, four different apartment-threading models determine the threading rules relating to calls between COM objects. Fortunately, these rules—and the complexity that accompanied them—have disappeared
