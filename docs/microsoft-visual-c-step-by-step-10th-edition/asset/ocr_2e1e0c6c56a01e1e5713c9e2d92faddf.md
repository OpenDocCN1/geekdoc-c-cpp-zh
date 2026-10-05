```
CancellationTokenSource = new
CancellationTokenSource();
CancellationToken = 
cancellationTestSource.Token;
...
// Semaphore that protects a pool of 3 resources
SemaphoreSlim = new SemaphoreSlim(3);

// Wait on the semaphore, and throw an
// OperationCanceledException if
// another thread calls Cancel on
// cancellationTokenSource
semaphore.Wait(cancellationToken);
```