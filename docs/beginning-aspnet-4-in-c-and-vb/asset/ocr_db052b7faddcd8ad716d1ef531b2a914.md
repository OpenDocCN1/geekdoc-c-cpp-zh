# Events

Events are the next of the system-wide synchronization resources. For using system events from managed code, the .NET Framework offers the classes ManualResetEvent, AutoResetEvent, ManualResetEventSlim, and CountdownEvent in the namespace System.Threading. ManualResetEventSlim and CountdownEvent are new with .NET 4.

![](bbox=[0.1, 0.3, 0.9, 0.42])

You can use events to inform other tasks that some data is present, something is completed, and so on. An event can be signaled or not signaled. A task can wait for the event to be in a signaled state with the help of the WaitHandle class, which was already discussed.

A ManualResetEvent is signaled by invoking the Set() method and turned back to a nonsignaled state with the Reset() method. If multiple threads are waiting for an event to be signaled, and the Set() method is invoked, then all threads waiting are released. Also, if a thread just invokes the WaitOne() method, but the event is already signaled, the waiting thread can continue immediately.

An AutoResetEvent is also signaled by invoking the Set() method. It is also possible to set it back to a nonsignaled state with the Reset() method. However, if a thread is waiting for an auto-reset event to be signaled, the event is automatically changed into a nonsignaled state when the wait state of the first thread is finished. This way, if multiple threads are waiting for the event to be set, only one thread is released from its wait state. It is not the thread that has been waiting the longest for the event to be signaled, but the thread waiting with the highest priority.

To demonstrate events with the ManualResetEventSlim class, the class Calculator defines the method Calculation(), which is the entry point for a task. With this method, the task receives input data for calculation and writes the result to the variable result that can be accessed from the Result property. As soon as the result is completed (after a random amount of time), the event is signaled by invoking the Set() method of the ManualResetEventSlim.

```
```csharp
public class Calculator
{
    private ManualResetEventSlim mEvent;
    public int Result { get; private set; }
    public Calculator(ManualResetEventSlim ev)
    {
        this.mEvent = ev;
    }
    public void Calculation(object obj)
    {
        Tuple<int, int> data = (Tuple<int, int>)obj;
        Console.WriteLine("Task {0} starts calculation", Task.Current.Id);
        Thread.Sleep(new Random().Next(3000));
        Result = data.Item1 + data.Item2;
        // signal the event-completed!
        Console.WriteLine("Task {0} is ready", Task.Current.Id);
        mEvent.Set();
    }
}
```
```