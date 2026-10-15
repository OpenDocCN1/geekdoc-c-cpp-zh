# Preparing the Code for Concurrency and Parallelism

Parallel and concurrent programming applied to certain complex algorithms is not as simple as shown in the previously explained examples. Sometimes, the differences between a reliable and bug-free parallelized version and its sequential counterpart could reveal an initially unexpected complexity. The code can become too complex, even when taking advantage of the new features offered by TPL. In fact, a complex sequential algorithm is probably going to be a more complex parallel algorithm. Therefore, TPL offers many new data structures for parallel programming that simplify many complex synchronization problems:

+   - Concurrent collection classes
+   - Lightweight synchronization primitives
+   - Types for lazy initialization

The aforementioned data structures were designed to avoid locks wherever possible, and use fine-grained locking when they are necessary on their different shared resources. Locks generate many potential bugs and can significantly reduce scalability. However, sometimes they are necessary because writing lock-free code isn’t always possible.

These new data structures enable you to forget about complex lock mechanisms in certain situations, because they already include all the necessary lightweight synchronization under the hood. Therefore, it is a good idea to use these data structures whenever possible.

# Synchronization Primitives

Furthermore, .NET Framework 4 offers synchronization primitives for managing and controlling the interactions between different tasks and their underlying threads, including the following operations:

+   - **Locking** — As with relational databases, sometimes you need to ensure that only one piece of code is working with a variable at that time. Unfortunately, the same problems that appear when working with concurrent access in a relational database are also present in concurrent and parallel code.
+   - **Signaling** — It provides a waiting and signaling mechanism to simplify the communication between different tasks and their underlying threads. The previously explained cancellation token is a clear example of signaling among many tasks. The mechanisms to wait for certain tasks to complete and the continuations are also examples of signaling implementations.
+   - **Lock constructors (interlocked operations)** — These provide a mechanism to perform atomic operations, such as addition, increment, decrement, exchange, or conditional exchange, depending on the results of a comparison and read operations.

# Synchronization Problems

The aforementioned synchronization primitives are advanced topics that require an in-depth analysis in order to determine the most convenient primitive to apply in a given situation. Nowadays, it is important to use the right synchronization primitive in order to avoid potential pitfalls, explained in the following list, while still keeping the code scalable.

Many techniques and new debugging tools can simplify the most complex problems, such as the following:

+   - **Deadlock** — At least two tasks are waiting for each other, but the wait never ends because they won’t continue with other instructions until the other task releases the protection held over certain resources. The other task is also waiting for resources held by its counterpart to resume its execution. As no task is willing to release its protection, none of them make any progress, and the tasks continue to wait for each other forever. Consider the following situation, task t1 holds a protection over resource A and is waiting to gain exclusive access over resource B. However, at the same time, task t2 holds a protection over resource B and is waiting to gain exclusive access over resource A. This is one of the most horrible bugs.