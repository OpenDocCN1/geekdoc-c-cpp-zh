
method that you want called back by a thread pool thread. Of course, the callback method that you write must match the `System.Threading.TimerCallback` delegate type, which is defined as follows:

```csharp
delegate void TimerCallback(Object state);
```

The constructor’s state parameter allows you to pass state data to the callback method each time it is invoked; you can pass null if you have no state data to pass. You use the dueTime parameter to tell the CLR how many milliseconds to wait before calling your callback method for the very first time. You can specify the number of milliseconds by using a signed or unsigned 32-bit value, a signed 64-bit value, or a TimeSpan value. If you want the callback method called immediately, specify 0 for the dueTime parameter. The last parameter, period, allows you to specify how long, in milliseconds, to wait before each successive call to the callback method. If you specify Timeout.Infinite (-1) for this parameter, a thread pool thread will call the callback method just once.

Internally, the thread pool has just one thread that it uses for all Timer objects. This thread knows when the next Timer object’s time is due. When the next Timer object is due, the thread wakes up, and internally calls ThreadPool’s QueueUserWorkItem to enter an entry into the thread pool’s queue, causing your callback method to get called. If your callback method takes a long time to execute, the timer could go off again. This could cause multiple thread pool threads to be executing your callback method simultaneously. To work around this problem, I recommend the following: Construct the Timer specifying Timeout.Infinite for the period parameter. Now, the timer will fire only once. Then, in your callback method, call the Change method specifying a new due time and again specify Timeout.Infinite for the period parameter. Here is what the Change method overloads look like:

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Change(Int32 dueTime, Int32 period);
    public Boolean Change(UInt32 dueTime, UInt32 period);
    public Boolean Change(Int64 dueTime, Int64 period);
    public Boolean Change(TimeSpan dueTime, TimeSpan period);
}
```

The Timer class also offers a Dispose method which allows you to cancel the timer altogether and optionally signal the kernel object identified by the notifyObject parameter when all pending callbacks for the timer have completed. Here is what the Dispose method overloads look like:

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Dispose();
    public Boolean Dispose(WaitHandle notifyObject);
}
```

**Important** When a Timer object is garbage collected, its finalization code tells the thread pool to cancel the timer so that it no longer goes off. So when using a Timer object, make sure that a variable is keeping the Timer object alive or else your callback method will stop getting called. This is discussed and demonstrated in the “Garbage Collections and Debugging” section in Chapter 21, “Automatic Memory Management Garbage Collection.”

The following code demonstrates how to have a thread pool thread call a method starting immediately and then every 2 seconds thereafter:

```csharp
internal static class TimerDemo {
    private static Timer s_timer;

    public static void Main() {
        Console.WriteLine("Checking status every 2 seconds");

        // Create the timer ensuring that it never fires. This ensures that
        // s_timer refers to it BEFORE Status is invoked by a thread pool thread
        s_timer = new Timer(Status, null, Timeout.Infinite, Timeout.Infinite);

        // Now that s_timer is assigned to, we can let the timer fire knowing
        // that calling Change in Status will not throw a NullReferenceException
        s_timer.Change(0, Timeout.Infinite);

        Console.ReadLine();   // Prevent the process from terminating
    }

    // This method's signature must match the TimerCallback delegate
    private static void Status(Object state) {
        // This method is executed by a thread pool thread
        Console.WriteLine("In Status at {0}", DateTime.Now);
        Thread.Sleep(1000);   // Simulates other work (1 second)

        // Just before returning, have the Timer fire again in 2 seconds
        s_timer.Change(2000, Timeout.Infinite);

        // When this method returns, the thread goes back
        // to the pool and waits for another work item
    }
}
```

If you have an operation you want performed periodically, there is another way you can structure your code by taking advantage of Task's static Delay method along with C#'s async and await keywords (discussed extensively in Chapter 28). Here is a rewrite of the above code demonstrating this:

```csharp
internal static class DelayDemo {
    public static void Main() {
        Console.WriteLine("Checking status every 2 seconds");
        Status();
        Console.ReadLine();   // Prevent the process from terminating
    }

    // This method can take whatever parameters you desire
    private static async void Status() {
        while (true) {
            Console.WriteLine("Checking status at {0}", DateTime.Now);
            // Put code to check status here...

            // At end of loop, delay 2 seconds without blocking a thread
            await Task.Delay(2000); // await allows thread to return
            // After 2 seconds, some thread will continue after await to loop around
        }
    }
}
```

purpose thread-scheduling technology designed to work with a large myriad of applications; it will work better for some applications than for others. It works very well today, and I highly recommend that you trust it, because it would be very hard for you to produce a thread pool that works better than the one shipping in the CLR. And, over time, most applications should improve as the thread pool code internally changes how it manages threads.

## Setting Thread Pool Limits

The CLR allows developers to set a maximum number of threads that the thread pool will create. However, it turns out that thread pools should never place an upper limit on the number of threads in the pool because starvation or deadlock might occur. Imagine queueing 1,000 work items that all block on an event that is signaled by the 1,001st item. If you’ve set a maximum of 1,000 threads, the 1,001st work item won’t be executed, and all 1,000 threads will be blocked forever, forcing end users to terminate the application and lose all their work. Also, it is very unusual for developers to artificially limit the resources that they have available to their application. For example, would you ever start your application and tell the system you’d like to restrict the amount of memory that the application can use or limit the amount of network bandwidth that your application can use? Yet, for some reason, developers feel compelled to limit the number of threads that the thread pool can have.

Because customers have had starvation and deadlock issues, the CLR team has steadily increased the default maximum number of threads that the thread pool can have. The default maximum is now about 1,000 threads, which is effectively limitless since a 32-bit process has at most 2 GB of usable address space within it. After a bunch of Win32 DLLs load, the CLR DLLs load, the native heap and the managed heap is allocated, there is approximately 1.5 GB of address space left over. Since each thread requires more than 1 MB of memory for its user-mode stack and thread environment block (TEB), the most threads that can get in a 32-bit process is about 1,360. Attempting to create more threads than this will result in an OutOfMemoryException being thrown. Of course, a 64-bit process offers 8 terabytes of address space, so you could theoretically create hundreds of thousands of threads. But allocating anywhere near this number of threads is really just a waste of resources, especially when the ideal number of threads to have is equal to the number of CPUs in the machine. What the CLR team should do is remove the limits entirely, but they can’t do this now because doing so might break some applications that expect thread pool limits to exist.

The System.Threading.ThreadPool class offers several static methods that you can call to manipulate the number of threads in the thread pool: GetMaxThreads, SetMaxThreads, GetMinThreads, SetMinThreads, and GetAvailableThreads. I highly recommend that you do not call any of these methods. Playing with thread pool limits usually results in making an application perform worse, not better. If you think that your application needs hundreds or thousands of threads, there is something seriously wrong with the architecture of your application and the way that it’s using threads. This chapter and Chapter 28 demonstrate the proper way to use threads.
