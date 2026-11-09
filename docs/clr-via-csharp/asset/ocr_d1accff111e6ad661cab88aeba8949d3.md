Most people do not like this additional logic. The problem is that these “features” have a cost associated with them. The `Mutex` object needs more memory to hold the additional thread ID and recursion count information. And, more importantly, the `Mutex` code has to maintain this information, which makes the lock slower. If an application needs or wants these additional features, then the application code could have done this itself; the code doesn't have to be built into the `Mutex` object. For this reason, a lot of people avoid using `Mutex` objects.

Usually a recursive lock is needed when a method takes a lock and then calls another method that also requires the lock, as the following code demonstrates:

```
```csharp
internal class SomeClass : IDisposable {
    private readonly Mutex m_lock = new Mutex();

    public void Method1() {
        m_lock.WaitOne();
        // Do whatever...
        Method2(); // Method2 recursively acquires the lock
        m_lock.ReleaseMutex();
    }

    public void Method2() {
        m_lock.WaitOne();
        // Do whatever...
        m_lock.ReleaseMutex();
    }

    public void Dispose() { m_lock.Dispose(); }
}
```
```

In the code above, code that uses a `SomeClass` object could call `Method1`, which acquires the `Mutex`, performs some thread-safe operation, and then calls `Method2`, which also performs some thread-safe operation. Since `Mutex` objects support recursion, the thread will acquire the lock twice and then release it twice before another thread can own the `Mutex`. If `SomeClass` has used an `AutoResetEvent` instead of a `Mutex`, then the thread would block when it called `Method2`’s `WaitOne` method.

If you need a recursive lock, then you could create one easily by using an `AutoResetEvent`:

```
```csharp
internal sealed class RecursiveAutoResetEvent : IDisposable {
    private AutoResetEvent m_lock = new AutoResetEvent(true);
    private Int32 m_owningThreadId = 0;
    private Int32 m_recursionCount = 0;

    public void Enter() {
        // Obtain the calling thread's unique Int32 ID
        Int32 currentThreadId = Thread.CurrentThread.ManagedThreadId;

        // If the calling thread owns the lock, increment the recursion count
        if (m_owningThreadId == currentThreadId) {
            m_recursionCount++;
            return;
        }
    }
```
```