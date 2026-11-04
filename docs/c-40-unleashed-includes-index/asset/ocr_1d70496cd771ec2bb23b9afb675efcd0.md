# The ThreadLocal<T> Class

![](bbox=[0.07, 0.16, 0.13, 0.26])

Closely related to the Lazy<T> class, the ThreadLocal<T> class was introduced in .NET 4. Essentially, this type addresses the shortcomings of the ThreadStatic attribute when initialization code is required for the per-thread state. The ThreadLocal<T> class acts as a factory for per-thread state, using a Func<T> delegate that's invoked once per thread upon calling the Value property. This pattern should be familiar; after all, the same pattern is used for Lazy<T>.

For instance, consider the code example from the previous section. Rewriting this example using the ThreadLocal<T> type (with T substituted for TextWriter) results in the following code:

```
```csharp
class Program
{
    static void Main()
    {
        new Thread(() =>
        {
            // Some thread that's responsible for some I/O operation.
            // At various times, it writes to the log, as shown here:
            s_log.Value.WriteLine("{0} - Performed some action", DateTime.Now);

            // Much more code is executed on this thread...
        }) { Name = "Lazy writer" }
            .Start();

        // Others threads could be created
        Console.ReadLine();
    }

    static ThreadLocal<TextWriter> s_log = new ThreadLocal<TextWriter>(() =>
    {
        string name = Thread.CurrentThread.Name
            ?? Thread.CurrentThread.ManagedThreadId.ToString();

        // More complicated initialization logic could be dreamed up.
        // What matters is the fact this method will run multiple times
        // on different threads, initializing that thread's logger.
        return File.CreateText(name + ".log");
    });
}
```
```

Two key differences are the absence of the ThreadStatic attribute on the s_log field and the use of the Value property to retrieve the thread-local state. In addition, an IsValueCreated property exists to check whether the initialization delegate (or factory, if