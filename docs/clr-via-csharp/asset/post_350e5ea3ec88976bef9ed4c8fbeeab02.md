
Worry about the system running out of sync blocks if many objects are being synchronized simultaneously.

![](img/3c46ff5b170881db4209d365b1f7a808_849_0.png)

FIGURE 29-1 Objects in the heap (including type objects) can have their sync block indexes refer to an entry in the CLR's sync block array

Here is some code that demonstrates how the Monitor class was originally intended to be used:

```csharp
internal sealed class Transaction {
    private DateTime m_timeOfLastTrans;

    public void PerformTransaction() {
        Monitor.Enter(this);
        // This code has exclusive access to the data...
        m_timeOfLastTrans = DateTime.Now;
        Monitor.Exit(this);
    }

    public DateTime LastTransaction {
        get {
            Monitor.Enter(this);
            // This code has shared access to the data...
            DateTime temp = m_timeOfLastTrans;
            Monitor.Exit(this);
            return temp;
        }
    }
}
```

这是一段示例文本。

If Transaction's members were static, then simply make the m_lock field static, too, and now the static members are thread safe.

It should be clear from this discussion that Monitor should not have been implemented as a static class; it should have been implemented like all the other constructs: a class you instantiate and call instance methods on. In fact, Monitor has many other problems associated with it that are all because it is a static class. Here is a list of additional problems:

- A variable can refer to a proxy object if the type of object it refers to is derived from the `System.MarshalByRefObject` class (discussed in Chapter 22, “CLR Hosting and AppDomains”). When you call Monitor's methods, passing a reference to a proxy object, you are locking the proxy object, not the actual object that the proxy refers to.
- If a thread calls `Monitor.Enter`, passing it a reference to a type object that has been loaded domain neutral (discussed in Chapter 22), the thread is taking a lock on that type across all AppDomains in the process. This is a known bug in the CLR that violates the isolation that AppDomains are supposed to provide. The bug is difficult to fix in a high-performance way, so it never gets fixed. The recommendation is to never pass a reference to a type object into Monitor's methods.
- Because strings can be interned (as discussed in Chapter 14, “Chars, Strings, and Working with Text”), two completely separate pieces of code could unknowingly get references to a single `String` object in memory. If they pass the reference to the `String` object into Monitor's methods, then the two separate pieces of code are now synchronizing their execution with each other unknowingly.
- When passing a string across an AppDomain boundary, the CLR does not make a copy of the string; instead, it simply passes a reference to the string into the other AppDomain. This improves performance, and in theory, it should be OK since `String` objects are immutable. However, like all objects, `String` objects have a sync block index associated with them, which is mutable, and this allows threads in different AppDomains to synchronize with each other unknowingly. This is another bug in CLR's AppDomain isolation story. The recommendation is to never pass `String` references to Monitor's methods.
- Since Monitor's methods take an `Object`, passing a value type causes the value type to get boxed, resulting in the thread taking a lock on the boxed object. Each time `Monitor.Enter` is called, a lock is taken on a completely different object and you get no thread synchronization at all.
- Applying the `[MethodImpl(MethodImplOptions.Synchronized)]` attribute to a method causes the JIT compiler to surround the method's native code with calls to `Monitor.Enter` and `Monitor.Exit`. If the method is an instance method, then this is passed to these methods, locking the implicitly public lock. If the method is static, then a reference to the type's type object is passed to these methods, potentially locking a domain-neutral type. The recommendation is to never use this attribute.
- When calling a type's type constructor (discussed in Chapter 8, "Methods"), the CLR takes a lock on the type's type object to ensure that only one thread initializes the type object and its static fields. Again, this type could be loaded domain neutral, causing a problem. For example, if the type constructor's code enters an infinite loop, then the type is unusable by all AppDomains in the process. The recommendation here is to avoid type constructors as much as possible or at least keep them short and simple.

Unfortunately, the story gets worse. Since it is so common for developers to take a lock, do some work, and then release the lock within a single method, the C# language offers simplified syntax via its **lock** keyword. Suppose that you write a method like this:

```csharp
private void SomeMethod() {
    lock (this) {
        // This code has exclusive access to the data...
    }
}
```

It is equivalent to having written the method like this:

```csharp
private void SomeMethod() {
    Boolean lockTaken = false;
    try {
        //
        Monitor.Enter(this, ref lockTaken);
        // This code has exclusive access to the data...
    }
    finally {
        if (lockTaken) Monitor.Exit(this);
    }
}
```

The first problem here is that the C# team felt that they were doing you a favor by calling **Monitor.Exit** in a **finally** block. Their thinking was that this ensures that the lock is always released no matter what happens inside the **try** block. However, this is not a good thing. If an exception occurs inside the **try** block while changing state, then the state is now corrupted. When the lock is exited in the **finally** block, another thread will now start manipulating the corrupted state. It is better to have your application hang than it is to continue running with a corrupted state and potential security holes. The second problem is that entering and leaving a **try** block decreases the performance of the method. And some JIT compilers won't inline a method that contains a **try** block in it, decreasing performance even more. So now we have slower code that lets threads access corrupted state.³ The recommendation is not to use C#'s **lock** statement.

³ By the way, while still a performance hit, it is safe to release a lock in a **finally** block if the code in the **try** block reads the state without attempting to modify it.

Now we get to the **Boolean lockTaken** variable. Here is the problem that this variable is trying to solve. Let's say that a thread enters the **try** block and before calling **Monitor.Enter**, the thread is aborted (as discussed in Chapter 22). Now the `finally` block is called, but its code should not exit the lock. The `lockTaken` variable solves this problem. It is initialized to `false`, which assumes that the lock has not been entered into. Then, if `Monitor.Enter` is called and successfully takes the lock, it sets `lockTaken` to `true`. The `finally` block examines `lockTaken` to know whether to call `Monitor.Exit` or not.⁴ By the way, the `SpinLock` structure also supports this `lockTaken` pattern.

## The ReaderWriterLockSlim Class

It is common to have threads simply read the contents of some data. If this data is protected by a mutually exclusive lock (like the `SimpleSpinLock`, `SimpleWaitLock`, `SimpleHybridLock`, `AnotherHybridLock`, `Mutex`, or `Monitor`), then if multiple threads attempt this access concurrently, only one thread gets to run and all the other threads are blocked, which can reduce scalability and throughput in your application substantially. However, if all the threads want to access the data in a read-only fashion, then there is no need to block them at all; they should all be able to access the data concurrently. On the other hand, if a thread wants to modify the data, then this thread needs exclusive access to the data. The `ReaderWriterLockSlim` construct encapsulates the logic to solve this problem. Specifically, the construct controls threads like this:

- When one thread is writing to the data, all other threads requesting access are blocked.
- When one thread is reading from the data, other threads requesting read access are allowed to continue executing, but threads requesting write access are blocked.
- When a thread writing to the data has completed, either a single writer thread is unblocked so it can access the data or all the reader threads are unblocked so that all of them can access the data concurrently. If no threads are blocked, then the lock is free and available for the next reader or writer thread that wants it.
- When all threads reading from the data have completed, a single writer thread is unblocked so it can access the data. If no threads are blocked, then the lock is free and available for the next reader or writer thread that wants it.

Here is what this class looks like (some method overloads are not shown):

```csharp
public class ReaderWriterLockSlim : IDisposable {
    public ReaderWriterLockSlim(LockRecursionPolicy recursionPolicy);
    public void Dispose();

    public void   EnterReadLock();
    public Boolean TryEnterReadLock(Int32 millisecondsTimeout);
    public void   ExitReadLock();
}
```
