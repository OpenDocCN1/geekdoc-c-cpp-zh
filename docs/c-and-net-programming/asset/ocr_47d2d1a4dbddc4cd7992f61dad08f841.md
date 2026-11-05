# 4. **Synchronization using Nonblocking**

By this method, access to a common field is protected by calling upon processor primitives. The Interlocked class and the volatile keyword are the two constructs for achieving nonblocking methodology.

# 15.6.2 Blocking

# Concept

+   - A thread is said to be blocked when its execution is paused for some reason, such as when waiting for another to end via Join or EndInvoke.

# Explanation

+   - A blocked thread consumes almost no processor time.
+   - The CLR and operating system know about blocked threads, and provide appropriate support to keep them in a non-working state, waking them up when their blocking conditions are satisfied.

# 15.6.3 Locking

# Concept

+   - Exclusive locking is used to ensure that only one thread can enter particular sections of code at a time. The .NET Framework provides two exclusive locking constructs namely lock and Mutex.

# Explanation

+   - Only one thread can lock the synchronizing object (in this case, locker) at a time, and any contending threads are blocked until the lock is released. If more than one thread contends the lock, they are queued on a "ready queue" and granted the lock on a first-come, first-served basis. Exclusive locks are sometimes said to enforce serialized access to whatever's protected by the lock, because one thread's access cannot overlap with that of another thread.
+   - A thread is blocked while awaiting a contended lock has a **ThreadState** of **WaitSleepJoin**.
+   - Locking should be done before accessing any field comprising writable shared state.

# 15.6.4 Mutex

A Mutex is like a C# lock, but it can work across multiple processes. In other words, Mutex can be computer-wide as well as application-wide.