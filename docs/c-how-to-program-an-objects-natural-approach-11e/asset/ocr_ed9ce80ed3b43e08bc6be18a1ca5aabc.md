integer value representing the maximum number of concurrent threads that can access a shared resource, such as **shared mutable data**. Once initialized, that integer can be accessed and altered by only two operations, $P$ and $V$. These are short for the Dutch words *proberen*, meaning “to test,” and *verhogen*, meaning “to increase.”¹⁰⁸ A thread calls the $P$ operation (also called the **wait operation**) when it wants to enter a **critical section** and calls the $V$ operation (also called the **signal operation**) when it wants to exit a critical section. Once the maximum number of threads are operating in the critical section, other threads trying to enter must wait. $P$ and $V$ are abstractions that encapsulate the details of mutual exclusion implementations. They can support any number of cooperating threads. C++’s semaphore classes call these operations **acquire** and **release**. For a nice discussion of semaphore fundamentals, check out Allen B. Downey’s *The Little Book of Semaphores*.¹⁰⁹

C++20’s `<semaphore>` header contains features for implementing **counting semaphores** and **binary semaphores**:

+   - A `std::counting_semaphore` implements the semaphore concept, which is lower level than `std::latch` and `std::barrier`, but still higher level than mutexes, locks, condition variables and atomics.¹¹⁰,¹¹¹ A **counting_semaphore** can allow multiple threads to access a shared resource. Its constructor initializes its internal integer counter. When a thread **acquires the semaphore**, the internal counter decrements by one. If the counter reaches zero, a thread attempting to **acquire the semaphore** will block until the count increases to indicate that the shared resource is available. When a thread releases the semaphore, the internal counter increments by one (by default) and threads waiting to **acquire the semaphore** unblock.
+   - A `std::binary_semaphore` is simply a **counting_semaphore** with a count of 1 and can be used like a `std::mutex`.¹¹²

# Producer–Consumer Using C++20 `std::binary_semaphore`

The C++ standard says semaphores “are widely used to implement other synchronization primitives and, whenever both are applicable, can be more efficient than condition variables.”¹¹³ Figure 17.16 reimplements class Synchron in `zeidbuf` from Section 17.6 using `binary_semaphores` for mutual exclusion. This gives you a neat, simple, higher-level way to replace lower-level mutex code. We reuse Fig. 17.8’s main function, so we do not repeat it here.

108. “Semaphore (Programming)—Operation Names.” Accessed April 18, 2023. https://en.wikipedia.org/wiki/Semaphore_(programming)#Operation_names

109. Allen B. Downey, *The Little Book of Semaphores* (Version 2.2.1), Section “3.6.4 Barrier Solution,” 2016. Green Tea Press. https://greenteapress.com/semaphores/littlebookofsemaphores.pdf. License: http://creativecommons.org/licenses/by-nc-sa/4.0. Thanks to one of our reviewers, Anthony Williams, for pointing us to Downey’s work.

110. C++ Standard, “Thread Support Library—Semaphore.” Accessed April 18, 2023. https://tim-song-cpp.github.io/cppwp/n4861/thread.sema.

111. `std::counting_semaphore`, `std::binary_semaphore.` Accessed April 18, 2023. https://en.cppreference.com/w/cpp/thread/counting_semaphore.

112. `std::counting_semaphore`, `std::binary_semaphore.` Accessed April 18, 2023. https://en.cppreference.com/w/cpp/thread/counting_semaphore.

113. C++ Standard, “32.7 Semaphore.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/thread.sema.