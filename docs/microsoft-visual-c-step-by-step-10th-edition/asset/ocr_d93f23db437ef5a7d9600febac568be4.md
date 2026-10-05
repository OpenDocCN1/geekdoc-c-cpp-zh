# Canceling synchronization

The ManualResetEventSlim, SemaphoreSlim, CountdownEvent, and Barrier classes all support cancellation by following the cancellation model described in Chapter 23. The wait operations for each of these classes take an optional CancellationToken parameter, retrieved from a CancellationSource object. If you call the Cancel method of the CancellationSource object, each wait operation referencing a CancellationToken generated from this is aborted with an OperationCanceledException exception (possibly wrapped in an AggregateException exception, depending on the context of the wait operation).

The following code shows how to invoke the Wait method of a SemaphoreSlim object and specify a cancellation token. If the wait operation is canceled, the OperationCanceledException catch handler runs.

Click here to view code image

```
CancellationSource = new CancellationSource();
cancellationToken = cancellationSource.Token;
...
// Semaphore that protects a pool of 3 resources
SemaphoreSlim semaphoreSlim = new SemaphoreSlim(3);
...
// Wait on the semaphore, and catch the OperationCanceledException
if
// another thread calls Cancel on cancellationToken
try{
    semaphoreSlim.Wait(cancellationToken);
}
catch (OperationCanceledException e)
{
    ...
}
```

# The concurrent collection classes

A common requirement of multithreaded applications is to store and retrieve data in a collection. The standard collection classes provided with .NET are not thread-safe by default, although you can use the synchronization