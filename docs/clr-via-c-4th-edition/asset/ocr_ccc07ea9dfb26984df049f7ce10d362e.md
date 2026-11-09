+   - When calling a type's type constructor (discussed in Chapter 8, "Methods"), the CLR takes a lock on the type's type object to ensure that only one thread initializes the type object and its static fields. Again, this type could be loaded domain neutral, causing a problem. For example, if the type constructor's code enters an infinite loop, then the type is unusable by all AppDomains in the process. The recommendation here is to avoid type constructors as much as possible or least keep them short and simple.

Unfortunately, the story gets worse. Because it is so common for developers to take a lock, do some work, and then release the lock within a single method, the C# language offers simplified syntax via its lock keyword. Suppose that you write a method like this.

```
```csharp
private void SomeMethod() {
    lock (this) {
        // This code has exclusive access to the data...
    }
}
```
```

It is equivalent to having written the method like this.

```
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
```

The first problem here is that the C# team felt that they were doing you a favor by calling Monitor.Exit in a finally block. Their thinking was that this ensures that the lock is always released no matter what happens inside the try block. However, this is not a good thing. If an exception occurs inside the try block while changing state, then the state is now corrupted. When the lock is exited in the finally block, another thread will now start manipulating the corrupted state. It is better to have your application hang than it is to continue running with a corrupted state and potential security holes. The second problem is that entering and leaving a try block decreases the performance of the method. And some JIT compilers won't inline a method that contains a try block in it, which decreases performance even more. So now we have slower code that lets threads access corrupted state.³ The recommendation is not to use C#'s lock statement.

Now we get to the Boolean lockTaken variable. Here is the problem that this variable is trying to solve. Let's say that a thread enters the try block and before calling Monitor.Enter, the thread is aborted (as discussed in Chapter 22). Now the finally block is called, but its code should not exit the lock. The lockTaken variable solves this problem. It is initialized to false, which assumes that the lock has not been entered into. Then, if Monitor.Enter is called and successfully takes the

³ By the way, while still a performance hit, it is safe to release a lock in a finally block if the code in the try block reads the state without attempting to modify it.