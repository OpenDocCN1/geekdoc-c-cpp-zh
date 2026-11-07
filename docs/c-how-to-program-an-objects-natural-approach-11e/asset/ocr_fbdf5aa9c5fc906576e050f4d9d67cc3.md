+   d) We cannot predict the order in which tasks will start executing, even if we know the order in which they were created and started. This is one of the challenges of multithreaded programming.

+   e) Print spooling is a common example of a producer–consumer relationship. A printer is an exclusive resource. Although a printer might not be available when you want to print from an application (the producer), you can still “complete” the print task. The data is temporarily stored (called spooling) until the printer becomes available.

+   f) A thread should never sleep while holding a lock in a real application.

+   g) A circular buffer never becomes full.

+   h) Before using the ++ operator on an atomic object, you must synchronize access to the object.

**17.3** *(Mutual Exclusion)* Discuss how mutually exclusive access to shared mutable data may be performed with critical sections and mutexes.

# ## Answers to Self-Review Exercises

**17.1** a) concurrently. b) a thread of execution. c) immutable. d) `<chrono>`. e) execution policy. f) `std::execution::par`. g) reduce. h) aging. i) deadlocked. j) circular wait. k) waiting. l) lock. m) cooperative cancellation. n) `<future>`. o) `std::shared_future`. p) completion function. q) wait, signal. r) 1.

**17.2** a) False. Actually, parallelism is a subset of concurrency. b) True. c) False. Actually, you cannot simply assume that using parallel algorithms will improve performance. Sometimes parallel algorithms actually perform worse than the corresponding sequential algorithms. This is especially true when processing small numbers of elements and when using non-random-access iterators. In these cases, the overhead of parallelization may outweigh the benefits of parallel performance. d) True. e) True. f) True. g) False. Actually, even with a circular buffer, a producer thread could fill the buffer, forcing the producer to wait until a consumer consumed a value to free an element in the buffer. h) False. Actually, operator ++ is one of a limited number of operations you can perform on atomic objects. When one thread is executing ++ on an atomic object, the increment is guaranteed to complete before another thread can modify or view that atomic object’s value.

**17.3** A common way to implement mutually exclusive access to shared mutable resources is by creating critical sections. These synchronized blocks of code execute atomically using features from the `<mutex>` header. A `std::mutex` can be owned by only one thread at a time. A thread that requires exclusive access to a resource must first acquire a lock on a mutex—typically at the beginning of a block of code. Other threads attempting to perform operations that require the same mutex will be blocked until the first thread releases the lock—typically at the end of a block of code. At that point, the blocked threads may attempt to acquire the lock and proceed with the operation.

# ## Exercises

**17.4** Fill in the blanks in each of the following statements:

+   a) Two tasks that are operating ________ are truly executing simultaneously.