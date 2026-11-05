# 15.6.5 Semaphore

A Semaphore is similar to mutex, except that the Semaphore has no "owner"-it is thread-agnostic. Any thread can call Release on a Semaphore, whereas with Mutex and lock, only the thread that obtained the lock can release it. Semaphores can be useful in limiting concurrency-preventing too many threads from executing a particular piece of code at once.

# 15.6.6 Nonblocking Synchronization

For locking, always a thread must be blocked, suffering the overhead and latency of being temporarily descheduled.

The .NET Framework's nonblocking synchronization constructs can perform simple operations without ever blocking, pausing, or waiting. These involve using instructions that are strictly atomic or instructing the compiler to use "volatile" read and write semantics.

**Two Marks Questions with Answers**

**Q.1 Define thread. Explain about Multithreading.**

**Ans.:** Thread is a set of instructions that when executed enables the program to perform concurrent processing. Concurrent processing helps in doing more than one process at a time. By default, C# consists of only thread. Other threads can be created to execute the code in parallel with original thread.

Thread follows a life cycle where it starts whenever a thread is created and gets terminated immediately after the execution. The namespace it follows is System.Threading which has to be included to create threads and use its members.

Threads are created by extending the thread class. Start() method marks the beginning of the thread execution.

1. //callThread is our target method//
2. ThreadStart methodThread = new ThreadStart(CallThread);
3. Thread childThread = new Thread(methodThread);
4. childThread.start();

C# can also execute more than processes/task at a time which is done by handling different processes at different time labeled as "multithreading".

Several operations of the same are listed below:
- Start
- Sleep
- Abort