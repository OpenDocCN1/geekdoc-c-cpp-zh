Fortunately, the FCL defines a base class, called **System.Threading.SynchronizationContext**, which solves all these problems. Simply stated, a **SynchronizationContext**-derived object connects an application model to its threading model. The FCL defines several classes derived from **SynchronizationContext**, but usually you will not deal directly with these classes; in fact, many of them are not publicly exposed or documented. Here is what the **SynchronizationContext** class looks like (I show only the members relevant to this discussion):

```
```csharp
public class SynchronizationContext {
    public static SynchronizationContext Current { get; }
    public virtual void Post(SendOrPostCallback d, object state); // Call asynchronously
    public virtual void Send(SendOrPostCallback d, object state); // Call synchronously
}

// SendOrPostCallback is a delegate defined like this:
public delegate void SendOrPostCallback(Object state);
```
```

For Windows Forms applications, WPF applications, and Silverlight applications, the GUI thread will have a **SynchronizationContext**-derived class associated with it. You can get a reference to this object by having the GUI thread query **SynchronizationContext**'s static **Current** property. You would then save a reference to this object in some shared variable (like a **static** field of your own class). Then, whenever a thread pool thread needs to have the GUI thread update the UI, you would have the thread pool thread reference the saved **SynchronizationContext**-derived object and call its **Post** method, passing in the method (matching the **SendOrPostCallback** delegate's signature) that should be invoked by the GUI thread and an argument that should be passed to this method.

I recommend calling the **Post** method, as it queues up the callback to the GUI thread and allows the thread pool thread to return immediately. **Send**, on the other hand, queues up the callback to the GUI thread and then blocks the thread pool thread until the GUI thread has completed calling the callback. Blocking the thread pool thread will most likely cause the thread pool to create a new thread, increasing resource consumption while decreasing performance. This is why I always avoid calling the **Send** method.

> > **Note** For the curious, here is how the various **SynchronizationContext**-derived classes get the GUI thread to invoke the **SendOrPostCallback** method. For Windows Forms, the **System.Windows.Forms.WindowsFormsSynchronizationContext** class's **Post** method internally calls **System.Windows.Forms.Control**'s **BeginInvoke** method, and its **Send** method internally calls **Control**'s **Invoke** method. For WPF and Silverlight, the **System.Windows.Threading.DispatcherSynchronizationContext** class's **Post** method internally calls **System.Windows.Threading.Dispatcher**'s **BeginInvoke** method, and its **Send** method internally calls **Dispatcher**'s **Invoke** method.