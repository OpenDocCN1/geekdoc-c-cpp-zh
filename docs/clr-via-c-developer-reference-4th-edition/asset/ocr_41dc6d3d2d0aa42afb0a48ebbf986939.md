The constructor's state parameter allows you to pass state data to the callback method each time it is invoked; you can pass null if you have no state data to pass. You use the dueDate parameter to tell the CLR how many milliseconds to wait before calling your callback method for the first time. You can specify the number of milliseconds by using a signed or unsigned 32-bit value, or a TimeSpan value. If the callback method is called immediately, specify 0 for the dueDate parameter. The last parameter, period, allows you to specify how long, in milliseconds, to wait before each successive call to the callback method. If you set Timeout.Infinite (-1) for this parameter, a thread pool will call the callback method just once.

Internally, the thread pool has one thread that for all Timer objects. This thread knows when the next Timer object's time is due. When the Timer object is due, the thread wakes up, and internally calls ThreadPool.QueueWorkItem to enter an entry into the thread pool's queue, causing your callback method to get called. If your callback method takes a long time to execute, this could cause multiple thread pools to execute simultaneously. To avoid this problem, I recommend the following: construct the Timer specifying Timeout.Infinite for the period parameter. Now, the timer will fire only once. Then, in your callback method, call the Change method and again specify Timeout.Infinite for the period parameter. Here is what the Change method overloads like.

```
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Change(Int32, Int32 period);
    public Boolean Change(UInt32, UInt32 period);
    public Boolean Change(Int64, Int32 period);
    public Boolean Change(TimeSpan dueDate, TimeSpan period);
}
```

The Timer class also offers a Dispose method that allows you to cancel the timer and optionally signal the kernel object identified by the notifyObject parameter when all callbacks for the time have completed. Here is what the Dispose method overloads look like.

```
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Dispose();
    public Boolean Dispose(WaitHandle notifyObject);
}
```

> Important When a Timer object is garbage collected, its finalization code calls the thread pool to cancel the timer so that it no longer goes off. When using a Timer object, make sure that a variable is keeping the Timer object alive or your callback method will stop getting called. This is discussed and demonstrated in the "Garbage Collections and Debugging" section in Chapter 21, "The Managed Heap and Garbage Collection."