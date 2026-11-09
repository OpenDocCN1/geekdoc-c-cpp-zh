```
```csharp
Monitor.PulseAll(m_lock);

Monitor.Exit(m_lock);
}

public T Dequeue() {
    Monitor.Enter(m_lock);

    // Loop while the queue is empty (the condition)
    while (m_queue.Count == 0)
        Monitor.Wait(m_lock);

    // Dequeue an item from the queue and return it for processing
    T item = m_queue.Dequeue();
    Monitor.Exit(m_lock);
    return item;
}
```
```

# # Asynchronous Synchronization

I’m not terribly fond of any of the thread synchronization constructs that use kernel-mode primitives, because all of these primitives exist to block a thread from running, and threads are just too expensive to create and not have them run. Here is an example that hopefully clarifies the problem.

Imagine a website into which clients make requests. When a client request arrives, a thread pool thread starts processing the client’s request. Let’s say that this client wants to modify some data in the server in a thread-safe way, so it acquires a reader-writer lock for writing. Let’s pretend that this lock is held for a long time. As the lock is held, another client request comes in, so that thread pool creates a new thread for the client request, and then the thread blocks trying to acquire the reader-writer lock for reading. In fact, as more and more client requests come in, the thread pool creates more and more threads. Thus, all these threads are just blocking themselves on the lock. The server is spending all its time creating threads so that they can stop running! This server does not scale well at all.

Then, to make matters worse, when the writer thread releases the lock, all the reader threads unblock simultaneously and get to run, but now there may be lots of threads trying to run on relatively few CPUs, so Windows is context switching between the threads constantly. The result is that the workload is not being processed as quickly as it could because of all the overhead associated with the context switches.

If you look over all the constructs shown in this chapter, many of the problems that these constructs are trying to solve can be much better accomplished using the Task class discussed in Chapter 27. Take the Barrier class, for example: You could spawn several Task objects to work on a phase and then, when all these tasks complete, you could continue with one or more other Task objects. Compared to many of the constructs shown in this chapter, tasks have many advantages:

+   - Tasks use much less memory than threads and they take much less time to create and destroy.