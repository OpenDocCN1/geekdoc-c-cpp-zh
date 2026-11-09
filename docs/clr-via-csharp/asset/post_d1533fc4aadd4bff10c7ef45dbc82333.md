
These options basically give you some control over speed versus memory consumption. **NotBuffered** saves memory but processes items slower. **FullyBuffered** consumes more memory while running fastest. **AutoBuffered** is the compromise in between **NotBuffered** and **FullyBuffered**. Really, the best way to know which of these to pick for any given query is to try them all and compare their performance results, or just accept the default, which tends to work pretty well for many queries. See the following blog posts for more information about how Parallel LINQ partitions work across CPU cores:

- http://blogs.msdn.com/pfxteam/archive/2009/05/28/9648672.aspx
- http://blogs.msdn.com/pfxteam/archive/2009/06/13/9741072.aspx

## Performing a Periodic Compute-Bound Operation

The **System.Threading** namespace defines a **Timer** class, which you can use to have a thread pool thread call a method periodically. When you construct an instance of the **Timer** class, you are telling the thread pool that you want a method of yours called back at a future time that you specify. The **Timer** class offers several constructors, all quite similar to each other:

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Timer(TimerCallback callback, Object state, Int32 dueTime, Int32 period);
    public Timer(TimerCallback callback, Object state, UInt32 dueTime, UInt32 period);
    public Timer(TimerCallback callback, Object state, Int64 dueTime, Int64 period);
    public Timer(TimerCallback callback, Object state, TimeSpan dueTime, TimeSpan period);
}
```

All four constructors construct a **Timer** object identically. The **callback** parameter identifies the method that you want called back by a thread pool thread. Of course, the callback method that you write must match the **System.Threading.TimerCallback** delegate type, which is defined as follows:

```csharp
delegate void TimerCallback(Object state);
```

The constructor’s **state** parameter allows you to pass state data to the callback method each time it is invoked; you can pass **null** if you have no state data to pass. You use the **dueTime** parameter to tell the CLR how many milliseconds to wait before calling your callback method for the very first time. You can specify the number of milliseconds by using a signed or unsigned 32-bit value, a signed 64-bit value, or a **TimeSpan** value. If you want the callback method called immediately, specify 0 for the **dueTime** parameter. The last parameter, **period**, allows you to specify how long, in milliseconds, to wait before each successive call to the callback method. If you pass **Timeout.Infinite** (-1) for this parameter, a thread pool thread will call the callback method just once.

Internally, the thread pool has just one thread that it uses for all **Timer** objects. This thread knows when the next **Timer** object's time is due. When the next **Timer** object is due, the thread wakes up, and internally calls **ThreadPool's QueueUserWorkItem** to enter an entry into the thread pool's queue, causing your callback method to get called. If your callback method takes a long time to execute, the timer could go off again. This could cause multiple thread pool threads to be executing your callback method simultaneously. To work around this problem, I recommend the following: Construct the **Timer** specifying **Timeout.Infinite** for the **period** parameter. Now, the timer will fire only once. Then, in your callback method, call the **Change** method specifying a new due time and again specify **Timeout.Infinite** for the **period** parameter. Here is what the **Change** method overloads look like:

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Change(Int32 dueTime, Int32 period);
    public Boolean Change(UInt32 dueTime, UInt32 period);
    public Boolean Change(Int64 dueTime, Int64 period);
    public Boolean Change(TimeSpan dueTime, TimeSpan period);
}
```

The **Timer** class also offers a **Dispose** method which allows you to cancel the timer altogether and optionally signal the kernel object identified by the **notifyObject** parameter when all pending callbacks for the timer have completed. Here is what the **Dispose** method overloads look like:

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Dispose();
    public Boolean Dispose(WaitHandle notifyObject);
}
```

> **Important** When a **Timer** object is garbage collected, its finalization code tells the thread pool to cancel the timer so that it no longer goes off. So when using a **Timer** object, make sure that a variable is keeping the **Timer** object alive or else your callback method will stop getting called. This is discussed and demonstrated in the "Garbage Collections and Debugging" section in Chapter 21, "Automatic Memory Management (Garbage Collection)."

The following code demonstrates how to have a thread pool thread call a method starting immediately and then every 2 seconds thereafter:

```csharp
internal static class TimerDemo {
    private static Timer s_timer;

    public static void Go() {
        Console.WriteLine("Main thread: starting a timer");
        using (s_timer = new Timer(ComputeBoundOp, 5, 0, Timeout.Infinite)) {
            Console.WriteLine("Main thread: Doing other work here...");
            Thread.Sleep(10000);  // Simulating other work (10 seconds)
        } // Calls Dispose to cancel the timer now
    }

    // This method's signature must match the TimerCallback delegate
    private static void ComputeBoundOp(Object state) {
        // This method is executed by a thread pool thread
        Console.WriteLine("In ComputeBoundOp: state={0}", state);
        Thread.Sleep(1000);  // Simulates other work (1 second)

        // Have the Timer call this method again in 2 seconds
        s_timer.Change(2000, Timeout.Infinite);

        // When this method returns, the thread goes back
        // to the pool and waits for another work item
    }
}
```

### So Many Timers, So Little Time

Unfortunately, the FCL actually ships with several timers, and it is not clear to most programmers what makes each timer unique. Let me attempt to explain:

- **System.Threading's Timer class**  This is the timer discussed in the previous section, and it is the best timer to use when you want to perform periodic background tasks on a thread pool thread.
- **System.Windows.Forms's Timer class**  Constructing an instance of this class tells Windows to associate a timer with the calling thread (see the Win32 SetTimer function). When this timer goes off, Windows injects a timer message (WM_TIMER) into the thread's message queue. The thread must execute a message pump that extracts these messages and dispatches them to the desired callback method. Notice that all of the work is done by just one thread—the thread that sets the timer is guaranteed to be the thread that executes the callback method. This also means that your timer method will not be executed by multiple threads concurrently.
- **System.Windows.Threading's DispatcherTimer class**  This class is the equivalent of the System.Windows.Forms's Timer class for Silverlight and WPF applications.
- **System.Timers's Timer class**  This timer is basically a wrapper around System.Threading's Timer class that causes the CLR to queue events into the thread pool when the timer comes due. The System.Timers.Timer class is derived from System.ComponentModel's Component class, which allows these timer objects to be placed on a design surface in Visual Studio. Also, it exposes properties and events, allowing it to be used more easily from Visual Studio's designer. This class was added to the FCL years ago while Microsoft was still sorting out the threading and timer stuff. This class probably should have been removed so that everyone would be using the System.Threading.Timer class instead. In fact, I never use the System.Timers.Timer class, and I'd discourage you from using it, too, unless you really want a timer on a design surface.
