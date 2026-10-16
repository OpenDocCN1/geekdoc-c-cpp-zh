When a Java application program begins execution, a new thread is created (in which the main method will run) and main is called. Therefore, all Java application programs run in threads.

When a program has multiple threads, a scheduler must determine which thread or threads will run at any given time. In many cases, there is only a single processor available, so only one thread actually runs at a time. It is difficult to give a precise description of how the Java scheduler works, because the different implementations (Solaris, Windows, and so on) do not necessarily schedule threads in exactly the same way. Typically, however, the scheduler gives equal-size time slices to each ready thread in round-robin fashion, assuming all of these threads have the same priority. Section 13.7.2 describes how different priorities can be given to different threads.

The Thread class provides several methods for controlling the execution of threads. The yield method, which takes no parameters, is a request from the running thread to surrender the processor voluntarily.⁶ The thread is put immediately in the task-ready queue, making it ready to run. The scheduler then chooses the highest-priority thread from the task-ready queue. If there are no other ready threads with priority higher than the one that just yielded the processor, it may also be the next thread to get the processor.

The sleep method has a single parameter, which is the integer number of milliseconds that the caller of sleep wants the thread to be blocked. After the specified number of milliseconds has passed, the thread will be put in the task-ready queue. Because there is no way to know how long a thread will be in the task-ready queue before it runs, the parameter to sleep is the minimum amount of time the thread will not be in execution. The sleep method can throw an InterruptedException, which must be handled in the method that calls sleep. Exceptions are described in detail in Chapter 14.

The join method is used to force a method to delay its execution until the run method of another thread has completed its execution. join is used when the processing of a method cannot continue until the work of the other thread is complete. For example, we might have the following run method:

```
public void run() {
...
Thread myTh = new Thread();
myTh.start();
// do part of the computation of this thread
myTh.join();  // Wait for myTh to complete
// do the rest of the computation of this thread
}
```

The join method puts the thread that calls it in the blocked state, which can be ended only by the completion of the thread on which join was called. If that thread happens to be blocked, there is the possibility of deadlock. To prevent