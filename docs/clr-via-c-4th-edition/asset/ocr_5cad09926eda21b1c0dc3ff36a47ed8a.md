```
```csharp
private readonly Queue<TaskCompletionSource<Object>> m_qWaitingWriters =
    new Queue<TaskCompletionSource<Object>>();

// All waiting readers wake up by signaling a single TaskCompletionSource
private TaskCompletionSource<Object> m_waitingReadersSignal =
    new TaskCompletionSource<Object>();
private Int32 m_numWaitingReaders = 0;

public AsyncOneManyLock() {
    m_noContentionAccessGranter = Task.FromResult<Object>(null);
}

public Task WaitAsync(OneManyMode mode) {
    Task accessGranter = m_noContentionAccessGranter; // Assume no contention

    Lock();
    switch (mode) {
        case OneManyMode.Exclusive:
            if (IsFree) {
                MakeWriter(); // No contention
            } else {
                // Contention: Queue new writer task & return it so writer waits
                var tcs = new TaskCompletionSource<Object>();
                m_qWaitingWriters.Enqueue(tcs);
                accessGranter = tcs.Task;
            }
            break;

        case OneManyMode.Shared:
            if (IsFree || (IsOwnedByReaders && m_qWaitingWriters.Count == 0)) {
                AddReaders(1); // No contention
            } else { // Contention
                // Contention: Increment waiting readers & return reader task so reader waits
                m_numWaitingReaders++;
                accessGranter = m_waitingReadersSignal.Task.ContinueWith(t => t.Result);
            }
            break;
    }
    Unlock();

    return accessGranter;
}

public void Release() {
    TaskCompletionSource<Object> accessGranter = null; // Assume no code is released

    Lock();
    if (IsOwnedByWriter) MakeFree(); // The writer left
    else SubtractReader(); // A reader left

    if (IsFree) {
        // If free, wake 1 waiting writer or all waiting readers
```
```