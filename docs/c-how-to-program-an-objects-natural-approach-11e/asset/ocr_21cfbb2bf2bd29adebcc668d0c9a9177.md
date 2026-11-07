# **std::atomic_ref Class Template**

Like `std::atomic`, the `std::atomic_ref` class template can be specialized for any primitive type, pointer type or trivially copyable type. However, a `std::atomic_ref` object is initialized with a reference rather than a value. You use the `atomic_ref` to perform atomic operations on the referenced object. Multiple `atomic_refs` can refer to the same object. The referenced object must outlive the `std::atomic_ref`; otherwise, a dangling reference or pointer will result.

# 17.1.3 **Coordinating Threads with C++20 Latches and Barriers**

So far, we’ve coordinated threads using `std::mutex`, `std::condition_variable` and locks. C++20 provides higher-level thread-coordination types `std::latch` and `std::barrier`, which do not require explicit use of mutexes, condition variables and locks.

# 17.1.3.1 C++20 `std::latch`

A `std::latch` (from the `<latch>` header) is a single-use gateway in your code that remains closed until a specified number of threads reach the latch. At that point, the gateway remains open permanently. The gateway serves as a one-time synchronization point, allowing threads to wait until a specified number of threads reach that point. Latches are simpler to use than mutexes and condition variables for coordinating threads.

Consider a parallel sorting algorithm that

+   - launches several worker threads to sort portions of a large array,
+   - waits for the worker threads to complete, then
+   - merges the sorted sub-arrays into the final sorted array.

Assume the algorithm uses two worker threads, each sorting half the array. The algorithm can use a `std::latch` object to wait until the workers are done:

+   - First, the algorithm creates a `std::latch` with a **non-zero count**. In this case, it needs two worker threads to complete, so we initialize the `latch` to 2.
+   - Each worker has a reference to the same `latch`.
+   - After launching the workers, the algorithm **waits on that latch**, which blocks the **algorithm from continuing**.
+   - When a thread reaches the `latch`, the thread reduces the `latch`’s count by 1 (known as signaling the latch) to indicate that it finished sorting a sub-array.

99. C++ Standard, “31.7 Class Template atomic_ref.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/atomics.ref.generic
100. “std::atomic_ref.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/atomic/atomic_ref
101. C++ Standard, “Thread Support Library—Coordination Types,” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/thread.coord
102. Bryce Adelstein Lelbach, “The C++20 Synchronization Library,” October 24, 2019. November 30, 2021. https://www.youtube.com/watch?v=Zcqw3CBWqS4.
103. C++ Standard, “Thread Support Library—Coordination Types—Latches.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/thread.latch.