

constructor does not take a parameter.
You do not need to change any other code in this method; you add an item to a ConcurrentBag<T> collection by using the Add method, which is the same mechanism that you use to add an item to a List<T> collection.

- 4. On the Debug menu, click Start Without Debugging.

The program runs and displays its approximation of pi by using the SerialPI and ParallelPI methods. The following image shows the typical output.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_697_0.png)

This time, the pointsList collection in the ParallelPI method contains the correct number of points, but the number of points within the circle still appears to be very high; it should be the same as that reported by the SerialPI method.

You should also note that the time taken by the ParallelPI method has increased compared with the previous exercise. This is because the methods in the ConcurrentBag<T> class have to lock and unlock data to guarantee thread safety, and this process adds to the overhead of calling these methods. Keep this point in mind when you’re considering whether it is appropriate to parallelize an operation.

- 5. Close the console window, and return to Visual Studio.

You currently have the correct number of points in the pointsList collection, but the value recorded for each of these points is now questionable. The code in the Parallel.For construct calls the Next method of a Random object, but like the methods in the generic List<T> class, this method is not thread safe. Sadly, there is no concurrent version of the Random class, so you must resort to using an alternative technique to serialize calls to the Next method. Because each invocation is relatively brief, it makes sense to use a simple lock to guard calls to this method.

## Use a lock to serialize method calls

- 1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text Editor window if it is not already open.

- 2. Locate the ParallelPI method. Modify the code in the lambda expression in the Parallel.For statement to protect the calls to random.Next by using a lock statement. Specify the pointsList collection as the subject of the lock, as shown here in bold:

Click here to view code image

```
static double ParallelPI()
{
    ...
    Parallel.For(0, NUMPOINTS, (x) =>
    {
        int xCoord;
        int yCoord;

        lock(pointsList)
        {
            xCoord = random.Next(RADIUS);
            yCoord = random.Next(RADIUS);
        }

        double distanceFromOrigin = Math.Sqrt(xCoord * xCoord + yCoord * yCoord);
        pointsList.Add(distanceFromOrigin);
        doAdditionalProcessing();
    });
    ...
}
```

Notice that the xCoord and yCoord variables are declared outside the lock statement. You do this because the lock statement defines its own scope, and any variables defined within the block specifying the scope of the lock statement disappear when the construct exits.

3. On the Debug menu, click Start Without Debugging.

This time, the values of pi calculated by the SerialPI and ParallelPI methods are the same. The only difference is that the ParallelPI method runs more quickly.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_698_0.png)

4. Close the console window, and return to Visual Studio.

## Summary

In this chapter, you saw how to define asynchronous methods by using the async modifier and the await operator. Asynchronous methods are based on tasks, and the await operator specifies the points at which a task can be used to perform asynchronous processing.

You also learned a little about PLINQ and how you can use the AsParallel

extension method to parallelize some LINQ queries. However, PLINQ is a big subject in its own right, and this chapter has only shown you how to get started. For more information, see the topic “Parallel LINQ (PLINQ)” in the documentation provided with Visual Studio.

This chapter also showed you how to synchronize data access in concurrent tasks by using the synchronization primitives provided for use with tasks. You saw how to use the concurrent collection classes to maintain collections of data in a thread-safe manner.

- If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 25, “Implementing the user interface for a Universal Windows Platform app.”

- If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Implement an asynchronous method | Define the method with the async modifier and change the type of the method to return a Task (or a void). In the body of the method, use the await operator to specify points at which asynchronous processing can be performed. For example:
private async Task<int> calculateValueAsync(...)
{
    // Invoke calculateValue using a Task
    Task<int> generateResultTask = Task.Run(() => calculateValue(...));
    await generateResultTask;
    return generateResultTask.Result;
} |
| Parallelize a LINQ query | Specify the AsParallel extension method with the data source in the query. For example:
var over100 = from n in numbers.AsParallel()
              where ...
              select n; |
| Enable cancellation in a PLINQ query | Use the WithCancellation method of the ParallelQuery class in the PLINQ query and specify a cancellation token. For example:
CancellationToken tok = ...;
...
var orderInfoQuery = from c in CustomersInMemory.Customers.AsParallel().WithCancellation(tok)
                     join o in OrdersInMemory.Orders.AsParallel()
                     on ... |
| Synchronize one or more tasks to implement thread-safe exclusive access to shared data | Use the lock statement to guarantee exclusive access to the data. For example:
object myLockObject = new object();
...
lock (myLockObject)
{
    // Code that requires exclusive access to a shared resource
    ...
} |

|  |  |
|---|---|
| Synchronize threads and make them wait for an event | Use a *ManualResetEventSlim* object to synchronize an indeterminate number of threads.
Use a *CountdownEvent* object to wait for an event to be signaled a specified number of times.
Use a *Barrier* object to coordinate a specified number of threads and synchronize them at a particular point in an operation. |
| Synchronize access to a shared pool of resources | Use a *SemaphoreSlim* object. Specify the number of items in the pool in the constructor. Call the *Wait* method prior to accessing a resource in the shared pool. Call the *Release* method when you have finished with the resource. For example:
```
SemaphoreSlim semaphore = new SemaphoreSlim(3);
...
semaphore.Wait();
// Access a resource from the pool
...
semaphore.Release();
``` |
| Provide exclusive write access to a resource but shared read access | Use a *ReaderWriterLockSlim* object. Prior to reading the shared resource, call the *EnterReadLock* method. Call the *ExitReadLock* method when you have finished. Before writing to the shared resource, call the *EnterWriteLock* method. Call the *ExitWriteLock* method when you have completed the write operation. For example:
```
ReaderWriterLockSlim readerWriterLock = new ReaderWriterLockSlim();

Task readerTask = Task.Factory.StartNew() =>
{
    readerWriterLock.EnterReadLock();
    // Read shared resource
    readerWriterLock.ExitReadLock();
});

Task writerTask = Task.Factory.StartNew() =>
{
    readerWriterLock.EnterWriteLock();
    // Write to shared resource
    readerWriterLock.ExitWriteLock();
});
``` |
| Cancel a blocking wait operation | Create a cancellation token from a *CancellationTokenSource* object, and specify this token as a parameter to the wait operation. To cancel the wait operation, call the *Cancel* method of the *CancellationTokenSource* object. For example:
```
CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();
CancellationToken cancellationToken = cancellationTokenSource.Token;
...
// Semaphore that protects a pool of 3 resources
SemaphoreSlim semaphoreSlim = new SemaphoreSlim(3);
...
// Wait on the semaphore, and throw an OperationCanceledException if
// another thread calls Cancel on cancellationTokenSource
semaphore.Wait(cancellationToken);
``` |

