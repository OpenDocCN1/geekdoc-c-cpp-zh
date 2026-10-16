```
// The results are processed as each of the threads completes
// and they are added to a
System.Collections.Concurrent.ConcurrentBag(Of Int)
// because this can take concurrent add operations in safety
query.ForAll(e => concurrentBag.Add(Compute(e)));
```

# Cancellation

PLINQ has full integration with .NET Framework 4 cancellation types. Because of that, we can cancel a PLINQ query, unlike the sequential LINQ to Object query. If you want to create a PLINQ that can be canceled, the WithCancellation operator should be used on the query and a CancellationToken instance used as the argument. When the IsCancellationRequested token property is set as true, it will be noticed by PLINQ which will then cease processing on the threads and an OperationCancelledException will be thrown.

# Exceptions

When a PLINQ query is executed, exceptions might be thrown from different threads all at the same time. Plus, the code needed to handle the exception may be on a separate thread than the code that caused the exception to be thrown. The AggregateException type is used by PLINQ for encapsulating every exception a query throws and sends the exceptions right back to the calling thread. On this thread, we only need a single try-catch block, but it is possible to iterate through every encapsulated exception in AggregateException; any that can be recovered from safely will be caught. There are rare cases where exceptions can be thrown that aren’t wrapped up in the AggregateException; ThreadAbortExceptions will also not be wrapped.

When an exception is allowed back up to the joining thread, the query may continue processing a few items after the exception is raised.

# Custom Partitioners