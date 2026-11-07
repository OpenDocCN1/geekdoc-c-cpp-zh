+   b) The C++ standard says, “________ is a single flow of control within a program, including the initial invocation of a specific top-level function, and recursively including every function invocation subsequently executed by the thread.”

+   c) One approach to thread safety is using only ________ data.

+   d) You can use the timing features from the ________ header to demonstrate the performance improvement of one algorithm over another.

+   e) Each parallel algorithm overload requires as its first parameter a(n) ________ indicating whether to parallelize a task and, if so, how to do it.

+   f) The ________ execution policy indicates that the algorithm should try to execute portions of its work simultaneously on multiple cores.

+   g) The parallel algorithm ________ produces a single value from a range of values.

+   h) Operating systems can employ a technique called ________ to prevent starvation—as a thread waits in the ready state, the operating system gradually increases the thread’s priority to ensure that it will eventually run.

+   i) A thread is ________ if it is waiting for a particular event that will not occur.

+   j) The four necessary conditions that Coffman, Elphick and Shoshani proved are necessary for deadlock to exist are mutual exclusion, wait for, no preemption and ________.

+   k) Deadlock and indefinite postponement each involve some form of ________.

+   l) All operations on shared mutable data accessed by concurrent threads must be guarded with a(n) ________ to prevent corruption.

+   m) When a multithreaded application needs to terminate, it’s good practice to shut down threads that are still performing tasks, so they can release resources they’re using. C++20 added ________ to enable programs to notify threads when it’s time for them to terminate. A task executing in a thread can watch for such notifications, then complete critical work, release resources and terminate.

+   n) The ________ header contains features that enable you to execute asynchronous tasks and receive the results of those tasks when they finish executing.

+   o) If multiple threads need access to an asynchronous task’s result, you can use ________ objects.

+   p) Typically, a barrier is used for repetitive tasks in a loop: Each thread works, then reaches a barrier and waits for it to open. When the specified number of threads reaches the barrier, an optional ________ executes. The barrier resets its count, which unblocks the threads so they may continue executing and repeat this process.

+   q) In Dijkstra’s seminal paper on cooperating sequential processes, the P operation is also called the ________ operation, and the V operation is also called the ________ operation.

+   r) A std::binary_semaphore is simply a counting_semaphore with a count of ________ and can be used like a std::mutex.

17.2 State whether each of the following is true or false. If false, explain why.

+   a) Concurrency is a subset of parallelism.

+   b) Programs can have multiple threads of execution, each with its own function-call stack and program counter, allowing it to execute concurrently with other threads.

+   c) Parallel algorithms always improve performance over sequential algorithms.