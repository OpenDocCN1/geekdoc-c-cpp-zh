# #### 1.1.1.1 Atomics

C++ has a set of simple atomic data types. These are booleans, characters, numbers, and pointers in many variants. You can define your atomic data type with the class template `std::atomic`. Atomics establishes synchronization and ordering constraints that can also hold for non-atomic types.

The standardized threading interface is the core of concurrency in C++.

# ### 1.1.2 Multithreading

![](bbox=[0.09, 0.285, 0.93, 0.558])

Multithreading in C++ consists of threads, synchronization primitives for shared data, thread-local data, and tasks.

# #### 1.1.2.1 Threads

C++ supports two kind of threads: the basic thread `std::thread` (C++11) and the improved thread `std::jthread` (C++20).

# ##### 1.1.2.1.1 std::thread

A `std::thread` represents an independent unit of program execution. The executable unit, which is started immediately, receives its work package as a callable unit. A callable unit can be a named function, a function object, or a lambda function.

The creator of a thread is responsible for its lifecycle. The executable unit of the new thread ends with the end of the callable. Either the creator waits until the created thread is done (`t.join()`) or the creator detaches itself from the created thread: `t.detach()`. A thread `t` is joinable if no operation `t.join()` or `t.detach()` was performed on it. A joinable thread calls `std::terminate` in its destructor, and the program terminates.