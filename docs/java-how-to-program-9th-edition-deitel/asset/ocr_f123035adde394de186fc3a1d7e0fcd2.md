+   - Executor method execute (p. 1051) receives a Runnable and assigns it to an available thread in a thread pool. If there are none, the Executor creates a new thread or waits for one to become available.
+   - Interface ExecutorService (of package java.util.concurrent; p. 1051) extends interface Executor and declares other methods for managing the life cycle of an Executor.
+   - An object that implements the ExecutorService interface can be created using static methods declared in class Executors (of package java.util.concurrent).
+   - Executors method newCachedThreadPool (p. 1052) returns an ExecutorService that creates new threads as they’re needed by the application.
+   - ExecutorService method execute executes its Runnable sometime in the future. The method returns immediately from each invocation—the program does not wait for each task to finish.
+   - ExecutorService method shutdown (p. 1054) notifies the ExecutorService to stop accepting new tasks, but continues executing existing tasks and terminates when those tasks complete execution.

# Section 26.4 Thread Synchronization

+   - Thread synchronization (p. 1054) coordinates access to shared data by multiple concurrent threads.
+   - By synchronizing threads, you can ensure that each thread accessing a shared object excludes all other threads from doing so simultaneously—this is called mutual exclusion (p. 1054).
+   - A common way to perform synchronization is to use Java’s built-in monitors. Every object has a monitor and a monitor lock (p. 1055). The monitor ensures that its object’s monitor lock is held by a maximum of only one thread at any time, and thus can be used to enforce mutual exclusion.
+   - If an operation requires the executing thread to hold a lock while the operation is performed, a thread must acquire the lock (p. 1055) before it can proceed with the operation. Any other threads attempting to perform an operation that requires the same lock will be blocked until the first thread releases the lock, at which point the blocked threads may attempt to acquire the lock.
+   - To specify that a thread must hold a monitor lock to execute a block of code, the code should be placed in a synchronized statement (p. 1055). Such code is said to be guarded by the monitor lock (p. 1055).
+   - The synchronized statements are declared using the synchronized keyword:

```
synchronized ( object )
{
    statements
} // end synchronized statement
```

where object is the object whose monitor lock will be acquired; object is normally this if it’s the object in which the synchronized statement appears.

+   - Java also allows synchronized methods (p. 1055). Before executing, a non-static synchronized method must acquire the lock on the object that’s used to call the method. Similary, a static synchronized method must acquire the lock on the class that’s used to call the method.
+   - ExecutorService method awaitTermination (p. 1058) forces a program to wait for threads to terminate. It returns control to its caller either when all tasks executing in the ExecutorService complete or when the specified timeout elapses. If all tasks complete before the timeout elapses, the method returns true; otherwise, it returns false.
+   - You can simulate atomicity (p. 1060) by ensuring that only one thread performs a set of operations at a time. Atomicity can be achieved with synchronized statements or synchronized methods.
+   - When you share immutable data across threads, you should declare the corresponding data fields final to indicate that variables’ values will not change after they’re initialized.