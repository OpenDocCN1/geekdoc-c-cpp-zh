# Implementing a Simple Spin Lock

The Interlocked methods are great, but they mostly operate on Int32 values. If you need to manipulate a bunch of fields in a class object atomically? In this case, we need a way to stop all threads but not one entering the region of code that manipulates the fields. Using Interlocked methods, we can build a thread synchronization lock.

```
internal struct SimpleSpinLock {
    private Int32 m_ResourceInUse; // 0=false (default), 1=true

    public void Enter() {
        while (true) {
            // Always set resource to in-use
            // When this thread changes it from not in-use
            if (Interlocked.Exchange(ref m_ResourceInUse, 1) == 0) return;
            // Black magic goes here...
        }
    }

    public void Leave() {
        // Set resource to not in-use
        Volatile.Write(ref m_ResourceInUse, 0);
    }
```

Here is a class that shows how to use the SimpleSpinLock.

```
public sealed SomeResource {
    private SimpleSpinLock m_sl = new SimpleSpinLock();

    public void AccessResource() {
        m_sl.Enter();
        // Only one thread at a time can get here to access the resource...
        m_sl.Leave();
    }
```

The SimpleSpinLock implementation is very simple. If two threads call Enter at the same time, Interlocked.Exchange ensures one thread changes m_resourceInUse from 0 to 1 and sees m_resourceInUse was 0. This thread returns from Enter so that can continue executing the code in the AccessResource method. The other thread will change m_resourceInUse from 1 to 1. This thread will see that did not change m_resourceInUse from a 0, and this thread will start spinning continuously, calling Exchange until the first thread calls Leave.

When the first thread is done manipulating the fields of the SomeResource object, it calls Leave, the spinning thread then Volatile.Write and changes m_resourceInUse back to 0. This causes the spinning thread to then change m_resourceInUse from 0 to 1, and this thread now gets to return from Enter so it can access SomeResource object's fields.

You have it. This is a simple implementation of a thread synchronization lock. The big potential problem with this lock is that it spins when there is contention for the lock.