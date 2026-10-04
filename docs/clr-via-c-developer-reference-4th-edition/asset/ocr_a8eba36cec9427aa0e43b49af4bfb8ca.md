+   When calling a type's constructor (discussed in Chapter 8, "Methods"), the CLR takes a lock on the type's object to ensure that only one thread initializes the type object and its static fields. Again, this could be loaded domain neutral, causing a problem. For example, if the type constructor's code enters an infinite loop, the type is unusable by all Domains in the process. The recommendation here is to avoid type constructors as much as possible or keep them short and simple.

Unfortunately, the story gets worse. Because it is so common for developers to take a lock, do some work, and release the lock within a single method, the C# language offers simplified syntax via its lock keyword. Suppose that you wrote a method like this:

```
private void SomeMethod() {
  lock(this) {
    // This has exclusive access to the data...
  }
```

It is equivalent to writing the method like this:

```
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
```

The first problem is that the C# team felt they were doing you a favor by calling Monitor.Exit in a finally block. Their thinking was that this ensures the lock is always released no matter what happens inside the try block. However, this is not a good idea. If an exception occurs inside the try block while changing state, then the state is corrupted. When the lock is exited in the finally block, another thread will now start manipulating the state. It is better to have your application hang than to continue running with a corrupted state and security holes. The second problem is entering and leaving a try block decreases the performance of the method. And JIT compilers inline a method that contains a try block in it, which decreases performance even more. Now so we have slower code that threads access corrupted state.3 recommendation is not to use C#'s lock statement.

Now we get to the Boolean lockTaken variable. The problem that this variable is trying to solve. Let's say a thread enters the try block and before calling Monitor.Enter, the thread is aborted (as discussed in Chapter 22). Now the finally block is called, but its code would not exit the lock. The lockTaken variable solves this. It is initialized to false, which assumes that the lock has not been entered. Then, if Monitor.Enter and successfully takes the

> 3 By the way, while a performance hit, it is safe to release a lock in a finally block if the code in the try block reads the state without attempting to modify it.