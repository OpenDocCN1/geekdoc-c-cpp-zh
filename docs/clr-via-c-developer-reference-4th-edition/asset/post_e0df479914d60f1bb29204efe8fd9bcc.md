
On the surface, this seems enough, but there is something wrong with this code. The problem is that each object's sync block index is implicitly public. The following code demonstrates the impact of this.

```csharp
public static void SomeMethod() {
    var t = new Transaction();
    Monitor.Enter(t); // This thread takes the object's public lock
```

```cs
// Have a thread pool display the LastTransaction time
// NOTE: The thread pool thread blocks until SomeMethod calls Monitor.Exit!
ThreadPool.QueueWorkItem(o => Console.WriteLine(t.LastTransaction));
```

```cs
// Execute some other code here...
Monitor.Exit(t);
```

In this code, the thread executing SomeMethod calls Monitor.Enter, entering the Transaction object's publicly exposed lock. When the thread pool queries the LastTransaction property, this property also calls Monitor.Enter to acquire the same lock, causing the thread pool to block until the thread executing SomeMethod calls Monitor.Exit. Using a debugger, you can determine that the thread pool is blocked inside the LastTransaction property, but it is very hard to determine which thread has the lock. If you figure out which thread has the lock, then you have to figure out what code caused it to take the lock. This is very difficult, and even worse, if you figure out that, the code might not be that you fix the problem. Therefore, my suggestion is to you might not always use a private lock instead. Here's how I'd fix the Transaction class.

```csharp
internal sealed class Transaction {
    private readonly Object m_lock = new Object(); // Each transaction has a PRIVATE lock now
    private DateTime m_timeOfLastTrans;

    public void PerformTransaction() {
        Monitor.Enter(m_lock); // Enter the private lock
        // This code has exclusive access to the data...
        m_timeOfLastTrans = DateTime.Now;
        Monitor.Exit(m_lock); // Exit the private lock
    }

    public DateTime LastTransaction() {
        Monitor.Enter(m_lock); // Enter the private lock
        // This code has exclusive access to the data...
        DateTime temp = m_timeOfLastTrans;
        Monitor.Exit(m_lock); // Exit the private lock
        return temp;
    }
}
```

If Transaction::members were static, simply make the m_lock field static, too, and now the static members are thread safe.

It should be clear from this discussion that Monitor should not have been implemented as a static class; it should have been implemented like all the others: a class you instantiate and call methods on. In fact, Monitor has many other problems associated with it that are all because it is a static class. Here is a list of problems:

- A variable can be a proxy object if the type of object it refers to is derived from the System.MarshalByRef object (discussed in Chapter 22, "CLR Hosting and AppDomains"). When you call Monitor's methods, passing a reference to a proxy object, you are locking the proxy object, not the actual object that proxy refers to.

- If a thread calls Monitor, passing a reference to a type object that has been loaded domain neutral (discussed in Chapter 22), the thread is taking a lock on that across all AppDomains in the process. This is a known bug in the CLR that violates the isolation that AppDomains are supposed to provide. The bug is difficult to fix in a high-performance way, so it never gets fixed. The recommendation is to never pass a reference to a type object into Monitor's methods.

- Because strings can be interned (discussed in Chapter 14, "Chars, Strings and Working with Text"), two separate pieces of code could unknowingly get references to a single String object. If they pass the reference to the String object into Monitor's methods, then the two separate pieces of code are now synchronizing their execution with each other unknowingly.

- When passing a string across an AppDomain boundary, the CLR does not make a copy of the string; instead, it simply passes a reference to the string into the other AppDomain. This improves performance, and in theory, it should be OK because String objects are immutable. However, like objects, String objects have a sync block index associated with them, which is mutable, and this allows threads in different AppDomains to synchronize with each other unknowingly. This is another bug in CLR's AppDomain isolation story. The recommendation is to never pass String references to Monitor's methods.

- Because Monitor's methods take an Object, passing a value type causes the value type to get boxed, resulting in the thread taking a lock on the boxed object. Each time Monitor::Enter is called, a lock is taken on a completely different object and no thread synchronization at all.

- Applying the [MethodImpl(MethodOptions.Synchronized)] to a method causes the JIT compiler to surround the method's native code with calls to Monitor::Exit. If the method is an instance method, then this is passed to these methods, locking the implicitly public lock. If the method is static, then a reference to the type's object is passed to these methods, potentially locking a domain-neutral type. The recommendation is to never use this attribute.

- When calling a type's constructor (discussed in Chapter 8, "Methods"), the CLR takes a lock on the type's object to ensure that only one thread initializes the type object and its static fields. Again, this could be loaded domain neutral, causing a problem. For example, if the type constructor's code enters an infinite loop, the type is unusable by all Domains in the process. The recommendation here is to avoid type constructors as much as possible or keep them short and simple.

Unfortunately, the story gets worse. Because it is so common for developers to take a lock, do some work, and release the lock within a single method, the C# language offers simplified syntax via its lock keyword. Suppose that you wrote a method like this:

```csharp
private void SomeMethod() {
  lock(this) {
    // This has exclusive access to the data...
  }
}
```

It is equivalent to writing the method like this:

```csharp
private void SomeMethod() {
  Boolean lockTaken = false;
  try {
    // An exception (such as ThreadAbortException) could occur here...
    Monitor.Enter(this, ref lockTaken);
    // This code has exclusive access to the data...
  }
  finally {
    if (lockTaken) Monitor.Exit(this);
  }
}
```

The first problem is that the C# team felt they were doing you a favor by calling Monitor.Exit in a finally block. Their thinking was that this ensures the lock is always released no matter what happens inside the try block. However, this is not a good idea. If an exception occurs inside the try block while changing state, then the state is corrupted. When the lock is exited in the finally block, another thread will now start manipulating the state. It is better to have your application hang than to continue. The second problem is that the C# team felt they were doing you a favor by calling Monitor.Exit in a finally block. Their thinking was that this ensures the lock is always released no matter what happens inside the try block. However, this is not a good idea. If an exception occurs inside the try block while changing state, then the state is corrupted. When the lock is exited in the finally block, another thread will now start manipulating the state. It is better to have your application hang than to continue.
