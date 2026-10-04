ensures that any data stored in the initiating thread's logical call context is available to the helper thread.

By default, the CLR automatically causes the initiating thread's execution context to flow to any helper threads. This transfers context information to the helper thread, but it comes at a performance cost, because there is a lot of information in an execution context, and accumulating all of information and copying it for the helper thread takes a fair amount of time. If the helper thread employs additional helper threads, more execution context data structures have to be created and initialized as well.

In the System. Threading namespace, there is an ExecutionContext class that allows you to control how a thread's execution context flows from one to another. Here is what the class looks like:

```
public sealed class ExecutionContext : IDisposable, ISerializable {
    [SecurityCritical] public static AsyncControl SuppressFlow();
    public static void RestoreFlow();
    public static bool IsFlowSuppressed();
```

```
// Less used methods are not
```

You can use this to suppress the flowing of an execution context, improving your application's performance. The performance gains can be quite substantial for a server application. There is not much performance benefit for a client application, and the SuppressFlow method is marked with the [SecurityCritical] attribute, making it impossible to call in some client applications (like Microsoft Silverlight). Of course, you should suppress the flowing of execution context only if the helper thread does not need to access the context information. If the initiating execution context does not flow to a helper thread, the helper thread will use whatever execution context it last with. Therefore, the helper thread shouldn't execute any code that relies on the execution context state (such as a user's identity).

Here is an example of how suppressing the flow of execution context affects data in a thread's logical call context when queuing a work item to the CLR's thread pool.

```
public static void Main() {
    // Put some data into the Main thread's logical call context
    CallContext.LogicalGetData("Name", "Jeffrey");

    // Initiate some work to be done by a thread pool thread
    // The thread pool can access the logical call context data
    ThreadPool.QueueUserWorkItem(state => {
        state = "0";Console.WriteLine("Name={0}", CallContext.LogicalGetData("Name"));));
```

```
// Now, suppress the flowing of the Main thread's execution context
ExecutionContext.SuppressFlow();
```

The items that you add to the logical call context must be serializable, as discussed in Chapter 24, Runtime Serialization." Flowing an execution context that contains logical call data items can hurt performance dramatically, because capturing the execution context requires serializing and deserializing the data items.