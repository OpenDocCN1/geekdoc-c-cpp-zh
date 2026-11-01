# Monitor

The C# compiler resolves the lock statement to use the Monitor class. The following lock statement:

```
lock (obj)
{
    // synchronized region for obj
}
```

is resolved to invoking the Enter() method, which waits until the thread gets the lock of the object. Only one thread at a time may be the owner of the object lock. As soon as the lock is resolved, the thread can enter the synchronized section. The Exit() method of the Monitor class releases the lock. The compiler puts the Exit() method into a finally handler of a try block so that the lock is also released if an exception is thrown.

> try/finally is covered in Chapter 15, "Errors and Exceptions."

```
Monitor.Enter(obj);
try
{
    // synchronized region for obj
}
finally
{
    Monitor.Exit(obj);
}
```

code snippet SynchronizationSamples/Program.cs

The Monitor class has a big advantage compared to the lock statement of C#: you can add a timeout value for waiting to get the lock. So instead of endlessly waiting to get the lock, you can use the TryEnter() method, where you can pass a timeout value that defines the maximum amount of time to wait to get the lock. If the lock for obj is acquired, TryEnter() sets the Boolean ref parameter to true and performs synchronized access to the state guarded by the object obj. If obj is locked for more than 500 milliseconds by another thread, TryEnter() sets the variable lockTaken to false, and the thread does not wait any longer but is used to do something else. Maybe at a later time, the thread can try to acquire the lock once more.

```
bool lockTaken = false;
Monitor.TryEnter(obj, 500, ref lockTaken);
if (lockTaken)
{
    try
    {
        // acquired the lock
        // synchronized region for obj
    }
    finally
    {
        Monitor.Exit(obj);
    }
}
else
{
    // didn't get the lock, do something else
}
```