| To | Do this |
| Synchronize one or more tasks to implement thread-safe exclusive access to shared data | Use the lock statement to guarantee exclusive access to the data. For example:

Click here to view code image
```csharp
object myLockObject = new object();
...
lock (myLockObject)
{
    // Code that requires exclusive access
    // to a shared resource
...
}\ | Synchronize threads and make them wait for an event | Use a ManualResetEventSlim object to synchronize an indeterminate number of threads. Use a CountdownEvent object to wait for an event to be signaled a specified number of times. Use a Barrier object to coordinate a specified number of threads and synchronize them at a particular point in an operation. | Synchronize access to a shared pool of resources | Use a SemaphoreSlim object. Specify the number of items in the pool in the constructor. Call the Wait method prior to accessing a resource in the shared pool. Call the Release method when you've finished with the resource. For example:

Click here to view code image
```csharp
SemaphoreSlim semaphore = new SemaphoreSlim(3);
...
semaphore.Wait();
// Access a resource from the pool
...
semaphore.Release();
``` |