
your application needs to perform many tasks and CPUs are available, the thread pool creates more threads. If your application's workload decreases, the thread pool threads kill themselves.

## Performing a Simple Compute-Bound Operation

To queue an asynchronous compute-bound operation to the thread pool, you typically call one of the following methods defined by the ThreadPool class.

```csharp
static Boolean QueueUserWorkItem(WaitCallback callBack);
static Boolean QueueUserWorkItem(WaitCallback callBack, Object state);
```

These methods queue a "work item" and optional state data to the thread pool's queue, and then all of these methods return immediately. A work item is simply a method identified by the callBack parameter that will be called by a thread pool thread. The method can be passed a single parameter specified via the state (the state data) argument. The version of QueueUserWorkItem without the state parameter passes null to the callback method. Eventually, some thread in the pool will process the work item, causing your method to be called. The callback method you write must match the System.Threading.WaitCallback delegate type, which is defined as follows.

```csharp
delegate void WaitCallback(Object state);
```

> **Note** The signatures of the WaitCallback delegate, the TimerCallback delegate (discussed in this chapter's "Performing a Periodic Compute-Bound Operation" section), and the ParameterizedThreadStart delegate (discussed in Chapter 26, "Thread Basics") are all identical. If you define a method matching this signature, the method can be invoked by using ThreadPool.QueueUserWorkItem, by using a System.Threading.Timer object, or by using a System.Threading.Thread object.

The following code demonstrates how to have a thread pool thread call a method asynchronously.

```csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        Console.WriteLine("Main thread: queuing an asynchronous operation");
        ThreadPool.QueueUserWorkItem(ComputeBoundOp, 5);
        Console.WriteLine("Main thread: Doing other work here...");
        Thread.Sleep(10000);   // Simulating other work (10 seconds)
        Console.WriteLine("Hit <Enter> to end this program...");
        Console.ReadLine();
    }

    // This method's signature must match the WaitCallback delegate
    private static void ComputeBoundOp(Object state) {
        // This method is executed by a thread pool thread
        Console.WriteLine("In ComputeBoundOp: state={0}", state);
        Thread.Sleep(1000);  // Simulates other work (1 second)

        // When this method returns, the thread goes back
        // to the pool and waits for another task
    }
}
```

When I compile and run this code, I get the following output.

```text
Main thread: queuing an asynchronous operation
Main thread: Doing other work here...
In ComputeBoundOp: state=5
```

And, sometimes when I run this code, I get this output.

```text
Main thread: queuing an asynchronous operation
In ComputeBoundOp: state=5
Main thread: Doing other work here...
```

The difference in the order of the lines in the output is attributed to the fact that the two methods are running asynchronously with respect to one another. The Windows scheduler determines which thread to schedule first, or it may schedule them both simultaneously if the application is running on a multi-CPU machine.

> **Note** If the callback method throws an exception that is unhandled, the CLR terminates the process (unless the host imposes its own policy). Unhandled exceptions are discussed in Chapter 20, “Exceptions and State Management.”

> **Note** For Windows Store apps, the System.Threading.ThreadPool class is not publicly exposed. However, it is used indirectly when you use types in the System.Threading.Tasks namespace (see the “Tasks” Section later in this chapter).

## Execution Contexts

Every thread has an execution context data structure associated with it. The execution context includes things such as security settings (compressed stack, Thread's Principal property, and Windows identity), host settings (see System.Threading.HostExecutionContextManager), and logical call context data (see System.Runtime.Remoting.Messaging.CallContext's LogicalSetData and LogicalGetData methods). When a thread executes code, some operations are affected by the values of the thread's execution context settings. This is certainly true for the security settings. Ideally, whenever a thread uses another (helper) thread to perform tasks, the issuing thread's execution context should flow (be copied) to the helper thread. This ensures that any operations performed by helper thread(s) are executing with the same security settings and host settings. It also ensures that any data stored in the initiating thread's logical call context is available to the helper thread.

By default, the CLR automatically causes the initiating thread's execution context to flow to any helper threads. This transfers context information to the helper thread, but it comes at a performance cost, because there is a lot of information in an execution context, and accumulating all of this information and then copying it for the helper thread takes a fair amount of time. If the helper thread then employs additional helper threads, then more execution context data structures have to be created and initialized as well.

In the System.Threading namespace, there is an ExecutionContext class that allows you to control how a thread's execution context flows from one thread to another. Here is what the class looks like.

```csharp
public sealed class ExecutionContext : IDisposable, ISerializable {
   [SecurityCritical] public static AsyncFlowControl SuppressFlow();
   public static void RestoreFlow();
   public static Boolean IsFlowSuppressed();

   // Less commonly used methods are not shown
}
```

You can use this class to suppress the flowing of an execution context, thereby improving your application's performance. The performance gains can be quite substantial for a server application. There is not much performance benefit for a client application, and the SuppressFlow method is marked with the [SecurityCritical] attribute, making it impossible to call in some client applications (like Microsoft Silverlight). Of course, you should suppress the flowing of execution context only if the helper thread does not need to access the context information. If the initiating thread's execution context does not flow to a helper thread, the helper thread will use whatever execution context it last associated with it. Therefore, the helper thread really shouldn't execute any code that relies on the execution context state (such as a user's Windows identity).

Here is an example showing how suppressing the flow of execution context affects data in a thread's logical call context when queuing a work item to the CLR's thread pool.^1

```csharp
public static void Main() {
   // Put some data into the Main thread's logical call context
   CallContext.LogicalSetData("Name", "Jeffrey");

   // Initiate some work to be done by a thread pool thread
   // The thread pool thread can access the logical call context data
   ThreadPool.QueueUserWorkItem(
      state => Console.WriteLine("Name={0}", CallContext.LogicalGetData("Name")));

   // Now, suppress the flowing of the Main thread's execution context
   ExecutionContext.SuppressFlow();
```

1 The items that you add to the logical call context must be serializable, as discussed in Chapter 24, "Runtime Serialization." Flowing an execution context that contains logical call context data items can hurt performance dramatically, because capturing the execution context requires serializing and deserializing all the data items.

allow themselves to be canceled. Here are the most useful members of the CancellationToken value type.

```csharp
public struct CancellationToken {  // A value type
    public static CancellationToken None { get; }  // Very convenient

    public Boolean    IsCancellationRequested { get; } // Called by non-Task invoked operations
    public void       ThrowIfCancellationRequested();  // Called by Task-invoked operations

    // WaitHandle is signaled when the CancellationTokenSource is canceled
    public WaitHandle WaitHandle { get; }
    // GetHashCode, Equals, operator== and operator!= members are not shown

    public Boolean CanBeCanceled { get; }   // Rarely used

    public CancellationTokenRegistration Register(Action<Object> callback, Object state,
                                                 Boolean useSynchronizationContext);  // Simpler overloads not shown
}
```

A CancellationToken instance is a lightweight value type because it contains a single private field: a reference to its CancellationTokenSource object. A compute-bound operation's loop can periodically call CancellationToken's IsCancellationRequested property to know if the loop should terminate early, thereby ending the compute-bound operation. Of course, the benefit here is that CPU time is no longer being wasted on an operation whose result you know you're not interested in. Now, let me put all this together with some sample code.

```csharp
internal static class CancellationDemo {
    public static void Main() {
        CancellationTokenSource cts = new CancellationTokenSource();

        // Pass the CancellationToken and the number-to-count-to into the operation
        ThreadPool.QueueUserWorkItem(o => Count(cts.Token, 1000));

        Console.WriteLine("Press <Enter> to cancel the operation.");
        Console.ReadLine();
        cts.Cancel(); // If Count returned already, Cancel has no effect on it
        // Cancel returns immediately, and the method continues running here...

        Console.ReadLine();
    }

    private static void Count(CancellationToken token, Int32 countTo) {
        for (Int32 count = 0; count < countTo; count++) {
            if (token.IsCancellationRequested) {
                Console.WriteLine("Count is canceled");
                break; // Exit the loop to stop the operation
            }

            Console.WriteLine(count);
            Thread.Sleep(200);  // For demo, waste some time
        }
        Console.WriteLine("Count is done");
    }
}
```
