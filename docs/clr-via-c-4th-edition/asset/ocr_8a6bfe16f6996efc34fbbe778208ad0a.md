# # Implementing a Simple Spin Lock

The Interlocked methods are great, but they mostly operate on Int32 values. What if you need to manipulate a bunch of fields in a class object atomically? In this case, we need a way to stop all threads but one from entering the region of code that manipulates the fields. Using Interlocked methods, we can build a thread synchronization lock.

```
```csharp
internal struct SimpleSpinLock {
    private Int32 m_ResourceInUse;  // 0=false (default), 1=true

    public void Enter() {
        while (true) {
            // Always set resource to in-use
            // When this thread changes it from not in-use, return
            if (Interlocked.Exchange(ref m_ResourceInUse, 1) == 0) return;
            // Black magic goes here...
        }
    }

    public void Leave() {
        // Set resource to not in-use
        Volatile.Write(ref m_ResourceInUse, 0);
    }
}
```
```

And here is a class that shows how to use the SimpleSpinLock.

```
```csharp
public sealed class SomeResource {
    private SimpleSpinLock m_sl = new SimpleSpinLock();

    public void AccessResource() {
        m_sl.Enter();
        // Only one thread at a time can get in here to access the resource...
        m_sl.Leave();
    }
}
```
```

The SimpleSpinLock implementation is very simple. If two threads call Enter at the same time, Interlocked.Exchange ensures that one thread changes m_resourceInUse from 0 to 1 and sees that m_resourceInUse was 0. This thread then returns from Enter so that it can continue executing the code in the AccessResource method. The other thread will change m_resourceInUse from a 1 to a 1. This thread will see that it did not change m_resourceInUse from a 0, and this thread will now start spinning continuously, calling Exchange until the first thread calls Leave.

When the first thread is done manipulating the fields of the SomeResource object, it calls Leave, which internally calls Volatile.Write and changes m_resourceInUse back to a 0. This causes the spinning thread to then change m_resourceInUse from a 0 to a 1, and this thread now gets to return from Enter so that it can access SomeResource object's fields.

There you have it. This is a simple implementation of a thread synchronization lock. The big potential problem with this lock is that it causes threads to spin when there is contention for the lock.