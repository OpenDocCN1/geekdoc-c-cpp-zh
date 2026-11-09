
In the beginning of this section, I mentioned that the double-check locking technique is not that interesting. In my opinion, developers think it is cool, and they use it far more often than they should. In most scenarios, this technique actually hurts efficiency. Here is a much simpler version of the Singleton class that behaves the same as the previous version. This version does not use the double-check locking technique:

```csharp
internal sealed class Singleton {
    private static Singleton s_value = new Singleton();

    // Private constructor prevents any code outside this class from creating an instance
    private Singleton() {
        // Code to initialize the one Singleton object goes here...
    }

    // Public, static method that returns the Singleton object (creating it if necessary)
    public static Singleton GetSingleton() { return s_value; }
}
```

Since the CLR automatically calls a type’s class constructor the first time code attempts to access a member of the class, the first time a thread queries Singleton’s GetSingleton method, the CLR will automatically call the class constructor, which creates an instance of the object. Furthermore, the CLR already ensures that calls to a class constructor are thread safe. I explained all of this in Chapter 8. The one downside of this approach is that the type constructor is called when any member of a class is first accessed. If the Singleton type defined some other static members, then the Singleton object would be created when any one of them was accessed. Some people work around this problem by defining nested classes.

Let me show you a third way of producing a single Singleton object:

```csharp
internal sealed class Singleton {
    private static Singleton s_value = null;

    // Private constructor prevents any code outside this class from creating an instance
    private Singleton() {
        // Code to initialize the one Singleton object goes here...
    }

    // Public, static method that returns the Singleton object (creating it if necessary)
    public static Singleton GetSingleton() {
        if (s_value != null) return s_value;

        // Create a new Singleton and root it if another thread didn’t do it first
        Singleton temp = new Singleton();
        Interlocked.CompareExchange(ref s_value, temp, null);

        // If this thread lost, then the second Singleton object gets GC’d

        return s_value; // Return reference to the single object
    }
}
```

If multiple threads call **GetSingleton** simultaneously, then this version might create two (or more) **Singleton** objects. However, the call to **Interlocked.CompareExchange** ensures that only one of the references is ever published into the **s_value** field. Any object not rooted by this field will be garbage collected later on. Since, in most applications, it is unlikely that multiple threads will call **GetSingleton** at the same time, it is unlikely that more than one **Singleton** object will ever be created.

Now it might upset you that multiple **Singleton** objects could be created, but there are many benefits to this code. First, it is very fast. Second, it never blocks a thread; if a thread pool thread is blocked on a **Monitor** or any other kernel-mode thread synchronization construct, then the thread pool creates another thread to keep the CPUs saturated with work. So now, another megabyte or more of memory is allocated and initialized and all the DLLs get a thread attach notification. With **CompareExchange**, this can never happen. Of course, you can use this technique only when the constructor has no side effects.

The FCL offers two types that encapsulate the patterns described in this section. The generic **System.Lazy** class looks like this (some methods are not shown):

```csharp
public class Lazy<T> {
    public Lazy(Func<T> valueFactory, LazyThreadSafetyMode mode);
    public Boolean IsValueCreated { get; }
    public T Value { get; }
}
```

This code demonstrates how it works:

```csharp
public static void Main() {
    // Create a lazy-initialization wrapper around getting the DateTime
    Lazy<String> s = new Lazy<String>(
        () => DateTime.Now.ToLongTimeString(),
        LazyThreadSafetyMode.PublicationOnly);

    Console.WriteLine(s.IsValueCreated);      // Returns false since Value not queried yet
    Console.WriteLine(s.Value);               // The delegate is invoked now
    Console.WriteLine(s.IsValueCreated);      // Returns true since Value was queried
    Thread.Sleep(10000);                      // Wait 10 seconds and display the time again
    Console.WriteLine(s.Value);               // The delegate is NOT invoked now; same result
}
```

When I run this, I get the following output:

```text
False
2:40:42 PM
True
2:40:42 PM    ← Notice that the time did not change 10 seconds later
```

The code above constructed an instance of the **Lazy** class and passed one of the **LazyThreadSafetyMode** flags into it. Here is what these flags look like and what they mean:

```csharp
public enum LazyThreadSafetyMode {
    None,                          // No thread-safety support at all (good for GUI apps)
    ExecutionAndPublication,       // Uses the double-check locking technique
    PublicationOnly,               // Uses the Interlocked.CompareExchange technique
}
```

In some memory-constrained scenarios, you might not even want to create an instance of the **Lazy** class. Instead, you can call static methods of the **System.Threading.LazyInitializer** class. The class looks like this:

```csharp
public static class LazyInitializer {
    // These two methods use Interlocked.CompareExchange internally:
    public static T EnsureInitialized<T>(ref T target) where T : class;
    public static T EnsureInitialized<T>(ref T target, Func<T> valueFactory) where T : class;

    // These two methods pass the syncLock to Monitor's Enter and Exit methods internally
    public static T EnsureInitialized<T>(ref T target, ref Boolean initialized,
        ref Object syncLock);
    public static T EnsureInitialized<T>(ref T target, ref Boolean initialized,
        ref Object syncLock, Func<T> valueFactory);
}
```

Also, being able to explicitly specify a synchronization object to the **EnsureInitialized** method's **syncLock** parameter allows multiple initialization functions and fields to be protected by the same lock.

Here is an example using a method from this class:

```csharp
public static void Main() {
    String name = null;
    // Since name is null, the delegate runs and initializes name
    LazyInitializer.EnsureInitialized(ref name, () => "Jeffrey");
    Console.WriteLine(name);   // Displays "Jeffrey"

    // Since name is not null, the delegate does not run; name doesn't change
    LazyInitializer.EnsureInitialized(ref name, () => "Richter");
    Console.WriteLine(name);   // Also displays "Jeffrey"
}
```

## The Condition Variable Pattern

Let's say that a thread wants to execute some code when a complex condition is true. One option would be to let the thread spin continuously, repeatedly testing the condition. But this wastes CPU time, and it is also not possible to atomically test multiple variables that are making up the complex condition. Fortunately, there is a pattern that allows threads to efficiently synchronize their operations based on a complex condition. This pattern is called the **condition variable pattern**, and we use it via the following methods defined inside the **Monitor** class:

```csharp
public static class Monitor {
    public static Boolean Wait(Object obj);
    public static Boolean Wait(Object obj, Int32 millisecondsTimeout);

    public static void Pulse(Object obj);
    public static void PulseAll(Object obj);
}
```

Here is what the pattern looks like:

```csharp
internal sealed class ConditionVariablePattern {
    private readonly Object m_lock = new Object();
    private Boolean m_condition = false;

    public void Thread1() {
        Monitor.Enter(m_lock);        // Acquire a mutual-exclusive lock

        // While under the lock, test the complex condition "atomically"
        while (!m_condition) {
            // If condition is not met, wait for another thread to change the condition
            Monitor.Wait(m_lock);      // Temporarily release lock so other threads can get it
        }

        // The condition was met, process the data...
        Monitor.Exit(m_lock);          // Permanently release lock
    }

    public void Thread2() {
        Monitor.Enter(m_lock);        // Acquire a mutual-exclusive lock

        // Process data and modify the condition...
        m_condition = true;

        // Monitor.Pulse(m_lock);        // Wakes one waiter AFTER lock is released
        Monitor.PulseAll(m_lock);      // Wakes all waiters AFTER lock is released

        Monitor.Exit(m_lock);          // Release lock
    }
}
```

In this code, the thread executing the `Thread1` method enters a mutual-exclusive lock and then tests a condition. Here, I am just checking a `Boolean` field, but this condition can be arbitrarily complex. For example, you could check to see if it is a Tuesday in March and if a certain collection object has 10 elements in it. If the condition is false, then you want the thread to spin on the condition, but spinning wastes CPU time, so instead, the thread calls `Wait`. `Wait` releases the lock so that another thread can get it and blocks the calling thread.

The `Thread2` method shows code that the second thread executes. It calls `Enter` to take ownership of the lock, processes some data, which results in changing the state of the condition, and then calls `PulseAll`, which will unblock a thread from its `Wait` call. `Pulse` unblocks the longest waiting thread (if any), while `PulseAll` unblocks all waiting threads.
