data could get corrupted if it is manipulated by multiple threads simultaneously. Normally, you would fix this by adding thread synchronization locks around the data access, but if you do this, then one thread at a time can access the data and you would lose the benefit of processing multiple items in parallel.

In addition, there is overhead associated with the **Parallel** methods; delegate objects have to be allocated, and these delegates are invoked once for each work item. If you have lots of work items that can be processed by multiple threads, then you might gain a performance increase. Also, if you have lots of work to do for each item, then the performance hit of calling through the delegate is negligible. You will actually hurt your performance if you use the **Parallel** methods for just a few work items or for work items that are processed very quickly.

I should mention that **Parallel's** **For**, **ForEach**, and **Invoke** methods all have overloads that accept a **ParallelOptions** object, which looks like this:

```
```csharp
public class ParallelOptions{
   public ParallelOptions();

   // Allows cancellation of the operation
   public CancellationToken CancellationToken { get; set; } // Default=CancellationToken.None

   // Allows you to specify the maximum number of work items
   // that can be operated on concurrently
   public Int32 MaxDegreeOfParallelism { get; set; }    // Default=-1 (# of available CPUs)

   // Allows you to specify which TaskScheduler to use
   public TaskScheduler TaskScheduler { get; set; }    // Default=TaskScheduler.Default
}
```
```

In addition, there are overloads of the **For** and **ForEach** methods that let you pass three delegates:

+   - The task local initialization delegate (**localInit**) is invoked once for each task participating in the work. This delegate is invoked before the task is asked to process a work item.
+   - The body delegate (**body**) is invoked once for each item being processed by the various threads participating in the work.
+   - The task local finally delegate (**localFinally**) is invoked once for each task participating in the work. This delegate is invoked after the task has processed all the work items that will be dispatched to it. It is even invoked if the body delegate code experiences an unhandled exception.

Here is some sample code that demonstrates the use of the three delegates by adding up the bytes for all files contained within a directory: