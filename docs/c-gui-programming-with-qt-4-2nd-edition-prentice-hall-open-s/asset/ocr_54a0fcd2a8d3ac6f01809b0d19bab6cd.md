# 4. Multithreading

![](bbox=[0.012, 0.046, 0.178, 0.126])

+   - Creating Threads
- Synchronizing Threads
- Communicating with the Main Thread
- Using Qt's Classes in Secondary Threads

Conventional GUI applications have one thread of execution and perform one operation at a time. If the user invokes a time-consuming operation from the user interface, the interface typically freezes while the operation is in progress. Chapter 7 presents some solutions to this problem. Multithreading is another solution.

In a multithreaded application, the GUI runs in its own thread and additional processing takes place in one or more other threads. This results in applications that have responsive GUIs even during intensive processing. When running on a single processor, multithreaded applications may run slower than a single-threaded equivalent due to the overhead of having multiple threads. But on multiprocessor systems, which are becoming increasingly common, multithreaded applications can execute several threads simultaneously on different processors, resulting in better overall performance.

In this chapter, we will start by showing how to subclass QThread and how to use QMutex, QSemaphore, and QWaitCondition to synchronize threads.[[*] Then we will see how to communicate with the main thread from secondary threads while the event loop is running. Finally, we round off with a review of which classes can be used in secondary threads and which cannot.

> [* Qt 4.4 is expected to provide a higher-level threading API, supplementing the threading classes described here, to make writing multithreaded applications less error-prone.

Multithreading is a large topic with many books devoted to the subject—for example, Threads Primer: A Guide to Multithreaded Programming by Bill Lewis and Daniel J. Berg (Prentice Hall, 1995) and Multithreaded, Parallel, and Distributed Programming by Gregory Andrews (Addison-Wesley, 2000). Here it is assumed that you already understand the fundamentals of multithreaded programming, so the focus is on explaining how to develop multithreaded Qt applications rather than the subject of itself.

# Creating Threads