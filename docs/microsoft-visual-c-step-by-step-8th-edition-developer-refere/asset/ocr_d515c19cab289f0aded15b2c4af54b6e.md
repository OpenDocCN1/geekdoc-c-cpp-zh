|  |  |
|---|---|---|
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