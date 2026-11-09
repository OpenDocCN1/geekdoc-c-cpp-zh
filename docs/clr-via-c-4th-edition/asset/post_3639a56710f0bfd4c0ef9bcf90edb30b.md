
Of course, if you do write code that holds a lock, your code should not hold the lock for a long time, because this increases the likelihood of threads blocking. In the "Asynchronous Synchronization" section later in this chapter, I will show a technique that uses collection classes as a way to avoid holding a lock for a long time.

Finally, for compute-bound work, you can use tasks (discussed in Chapter 27) to avoid a lot of the thread synchronization constructs. In particular, I love that each task can have one or more continuations tasks associated with it that execute via some thread pool thread when some operation completes. This is much better than having a thread block waiting for some operation to complete. For I/O-bound work, call the various XxxAsync methods that cause your code to continue running after the I/O operation completes; this is similar to a task's continue-with task.

### The Famous Double-Check Locking Technique

There is a famous technique called double-check locking, which is used by developers who want to defer constructing a singleton object until an application requests it (sometimes called lazy initialization). If the application never requests the object, it never gets constructed, saving time and memory. A potential problem occurs when multiple threads request the singleton object simultaneously. In this case, some form of thread synchronization must be used to ensure that the singleton object gets constructed just once.

This technique is not famous because it is particularly interesting or useful. It is famous because there has been much written about it. This technique was used heavily in Java, and later it was discovered that Java couldn't guarantee that it would work everywhere. The famous document that describes the problem can be found on this webpage: www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html.

Anyway, you'll be happy to know that the CLR supports the double-check locking technique just fine because of its memory model and volatile field access (described in Chapter 29). Here is code that demonstrates how to implement the double-check locking technique in C#.

```csharp
internal sealed class Singleton {
   // s_lock is required for thread safety and having this object assumes that creating
   // the singleton object is more expensive than creating a System.Object object and that
   // creating the singleton object may not be necessary at all. Otherwise, it is more
   // efficient and easier to just create the singleton object in a class constructor
   private static readonly Object s_lock = new Object();

   // This field will refer to the one Singleton object
   private static Singleton s_value = null;

   // Private constructor prevents any code outside this class from creating an instance
   private Singleton() {
      // Code to initialize the one Singleton object goes here...
   }

   // Public, static method that returns the Singleton object (creating it if necessary)
   public static Singleton GetSingleton() {
        // If the Singleton was already created, just return it (this is fast)
        if (s_value != null) return s_value;

        Monitor.Enter(s_lock);   // Not created, let 1 thread create it
        if (s_value == null) {
            // Still not created, create it
            Singleton temp = new Singleton();

            // Save the reference in s_value (see discussion for details)
            Volatile.Write(ref s_value, temp);
        }
        Monitor.Exit(s_lock);

        // Return a reference to the one Singleton object
        return s_value;
    }
}
```

The idea behind the double-check locking technique is that a call to the GetSingleton method quickly checks the s_value field to see if the object has already been created, and if it has, the method returns a reference to it. The beautiful thing here is that no thread synchronization is required after the object has been constructed; the application will run very fast. On the other hand, if the first thread that calls the GetSingleton method sees that the object hasn't been created, it takes a thread synchronization lock to ensure that only one thread constructs the single object. This means that a performance hit occurs only the first time a thread queries the singleton object.

Now, let me explain why this pattern didn't work in Java. The Java Virtual Machine read the value of s_value into a CPU register at the beginning of the GetSingleton method and then just queried the register when evaluating the second if statement, causing the second if statement to always evaluate to true, and multiple threads ended up creating Singleton objects. Of course, this happened only if multiple threads called GetSingleton at exactly the same time, which in most applications is very unlikely. This is why it went undetected in Java for so long.

In the CLR, calling any lock method is a full memory fence, and any variable writes you have before the fence must complete before the fence and any variable reads after the fence must start after it. For the GetSingleton method, this means that the s_value field must be reread after the call to Monitor.Enter; it cannot be cached in a register across this method call.

Inside GetSingleton, you see the call to Volatile.Write. Here's the problem that this is solving. Let's say that what you had inside the second if statement was the following line of code.

```csharp
        s_value = new Singleton();   // This is what you'd ideally like to write
```

You would expect the compiler to produce code that allocates the memory for a Singleton, calls the constructor to initialize the fields, and then assigns the reference into the s_value field. Making a value visible to other threads is called publishing. But the compiler could do this instead: allocate memory for the Singleton, publish (assign) the reference into s_value, and then call the constructor. From a single thread's perspective, changing the order like this has no impact. But what if, after publishing the reference into s_value and before calling the constructor, another thread calls the GetSingleton method? This thread will see that s_value is not null and start to use the Singleton object, but its constructor has not finished executing yet! This can be a very hard bug to track down, especially because it is all due to timing.

The call to Volatile.Write fixes this problem. It ensures that the reference in temp can be published into s_value only after the constructor has finished executing. Another way to solve this problem would be to mark the s_value field with C#'s volatile keyword. This makes the write to s_value volatile, and again, the constructor has to finish running before the write can happen. Unfortunately, this makes all reads volatile, too, and because there is no need for this, you are hurting your performance with no benefit.

In the beginning of this section, I mentioned that the double-check locking technique is not that interesting. In my opinion, developers think it is cool, and they use it far more often than they should. In most scenarios, this technique actually hurts efficiency. Here is a much simpler version of the Singleton class that behaves the same as the previous version. This version does not use the double-check locking technique.

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

Because the CLR automatically calls a type's class constructor the first time code attempts to access a member of the class, the first time a thread queries Singleton's GetSingleton method, the CLR will automatically call the class constructor, which creates an instance of the object. Furthermore, the CLR already ensures that calls to a class constructor are thread safe. I explained all of this in Chapter 8. The one downside of this approach is that the type constructor is called when any member of a class is first accessed. If the Singleton type defined some other static members, then the Singleton object would be created when any one of them was accessed. Some people work around this problem by defining nested classes.

Let me show you a third way of producing a single Singleton object.

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
```
