
We now generalise and improve this code by encapsulating the above functionality with lambda functions which will be used in parallel code:

```
auto fn1 = [&]()
{
    LatticeMechanisms::ForwardInduction<double>
        (euroPut, algo, rootVal);
    std::cout << "Euro put: " << BackwardInduction<double>
        (asset, euroPut, algo, PutPayoff, EmptyAdjuster) << '\n';
};
```

```
auto fn2 = [&]()
{
    LatticeMechanisms::ForwardInduction<double>
        (euroCall, algo, rootVal);
    std::cout << "Euro call: " << BackwardInduction<double>
        (asset, euroCall, algo, CallPayoff, EmptyAdjuster) << '\n';
};
```

```
auto fn3 = [&]()
{
    LatticeMechanisms::ForwardInduction<double>
        (earlyPut, algo, rootVal);
    std::cout << "Early put: " << BackwardInduction<double>
        (asset, earlyPut, algo, PutPayoff, AmericanPutAdjuster);
};
```

```
auto fn4 = [&]()
{
    LatticeMechanisms::ForwardInduction<double>
        (earlyCall, algo, rootVal);
    std::cout << "Early call: " << BackwardInduction<double>
        (asset, earlyCall, algo, CallPayoff, AmericanCallAdjuster);
};
```

We now discuss a number of ways to parallelise the above code. Each solution is based on the fork-and-join model in which a master thread creates a team of child threads, gives them work to do and waits for them to finish:

+   S1: Using C++ threads.
+   S2: Using an array of C++ threads.
+   S3: Using Boost thread group.
+   S4: Using OpenMP parallel loops.
+   S5: Using C++ futures (asynchronous tasks) (to be discussed in Chapter 29).

The solutions in this case are easy to program because the shared data is read-only and each thread operates on its own thread-local data. Thus, in this case we do not have to employ locking mechanisms in order to avoid data races which will have an adverse impact on run-time performance. We do not need to lock shared data in the current case.

```
boost::thread_group threads;
for (std::size_t i = 0; i < tGroupFunctions.size(); ++i)
{
    threads.create_thread(tGroupFunctions[i]);
}
std::cout << "Thread group size: " << threads.size() << '\n';

threads.join_all();

sw.Stop();
std::cout <<"Elapsed time BOOST thread groups in seconds:"
          << sw.GetTime() << '\n';
```

Solution S4 has the same form as solution S2 but in this case we do not have to explicitly create threads. In this case we use a pragma to announce that a group of threads should be created. Each thread performs a subset of the work. There is a default barrier after the loop body where each thread waits for all the other threads to arrive. Only when all threads have arrived at this barrier does the code continue execution (the barrier directive). In other words, a barrier synchronises all the threads executing within the parallel region:

```
sw.Start();
std::cout << '\n';
#pragma omp parallel for
for (long i = 0; i < tGroupFunctions.size(); ++i)
{
    tGroupFunctions[i]();
}
sw.Stop();
std::cout << "Elapsed time OpenMP thread groups in seconds: "
          << sw.GetTime() << '\n';
```

Again, race conditions will not occur because each loop iteration is executed by a single thread and furthermore, each thread operates on its own thread-local data.

Finally, we give a preview of how C++ supports multitasking and allows developers to create parallel code using higher-level syntax (solution S5). In particular, we run asynchronous tasks and we wait for them to finish:

```
sw.Start();
std::cout << '\n';
// Start future by running the functions asynchronously
std::future<void> fut1(std::async(fn1));
std::future<void> fut2(std::async(fn2));
std::future<void> fut3(std::async(fn3));
std::future<void> fut4(std::async(fn4));

// Wait for results to become available
fut1.wait();
fut2.wait();
fut3.wait();
fut4.wait();
```

```
// No shared data so we define 1 barrier/rendezvous point
fut1.get();
fut2.get();
fut3.get();
fut4.get();

sw.Stop();
std::cout << "Elapsed time C++11 futures in seconds: " << sw.GetTime();
```

Finally, the output from the above code is:

```
Stress test, number of time steps: 7000
Interest: 0.08
Vol: 0.3
Strike: 65
Expiration: 0.25
Dividend: 0
4 processors/cores detected.

Euro put: 5.8464
Euro call: 2.13349
Early put: 6.12361
Early call: 2.13349
Elapsed time (seconds) sequential code: 1.68254

Euro call: 2.13349
Early call: 2.13349
Euro put: 5.8464
Early put: 6.12361
Elapsed time C++11 threads in seconds: 0.714551

Euro call: 2.13349
Early call: 2.13349
Euro put: 5.8464
Early put: 6.12361
Elapsed time C++ thread array in seconds: 0.714546

Thread group size: 4
Euro call: 2.13349
Early call: 2.13349
Euro put: 5.8464
Early put: 6.12361
Elapsed time BOOST thread groups in seconds: 0.719553

Euro call: 2.13349
Early call: 2.13349
Euro put: 5.8464
Early put: 6.12361
Elapsed time OpenMP thread groups in seconds: 0.702057
```

```
Euro call: 2.13349
Early call: 2.13349
Euro put: 5.8464
Early put: 6.12361
Elapsed time C++11 futures in seconds: 0.707558
```

We formally discuss multitasking in Chapters 29 and 30. The code in this section can be used as a template (or *cook y cutter*) for other similar kinds of applications that we would like to parallelise, as we shall see in Section 32.2 when we compute option prices using the Monte Carlo method.

## 28.5 ATOMICS

One of the most far-reaching features in C++11 is that it supports a new *multithreading-aware memory model* (see Williams, 2012 for a detailed discussion). We do not go into details just yet but instead introduce a number of related concepts. An *atomic operation* is an indivisible operation. It cannot be half-done; it must be executed with success or not done at all. In database applications it is similar to a *transaction* that executes completely or not at all. In the current chapter we wish to ensure that only one thread can access an object, resource or piece of memory at any moment in time. Not all operations are atomic. For example, an assignment statement of 64-bit variables may not be atomic because one thread may be updating the high-order 32-bit part while another thread can be simultaneously updating the low-order 32-bit part. In general, an atomic operation at the hardware level is uninterruptible and it must be guaranteed to terminate, for example it can never get stuck in an infinite loop.

An *atomic type* is one for which all atomic operations are atomic and only operations on these types are atomic in the sense of the language. Atomic types are supported in C++ by the template struct `std::atomic`. It has support for standard types such as char, int, long (both signed and unsigned versions) as well as *fast integer types* for better performance. The member functions are:

+   - Constructors: default constructor and constructor taking a value (latter is not atomic).
+   - Is the atomic object *lock-free* (can more than one thread access the object concurrently)? This allows the developer to determine whether operations on a given type are executed directly with atomic instructions or executed by using a lock internal to the compiler and library.
+   - Store: atomically replace the value of the atomic object with a non-atomic argument.
+   - Load: atomically obtain the value of the atomic object.
+   - Load a value from an atomic object.
+   - Exchange: atomically replace the values of the atomic objects and obtain the value held previously.

Furthermore, there are specialised member functions for atomic addition and subtraction as well as for bitwise AND, OR and XOR. Finally, there are operators for atomic increment and decrement.

We now give some examples of using `std::atomic` based on the above discussion:

```
#include <atomic>
#include <iostream>

int main()
{
    // Full specification std::atomic<long long>
    std::atomic_llong v1(std::numeric_limits<long long>::max());
    std::atomic_llong v2;

    // Lock-free ADT more than 1 thread can access it concurrently
    std::cout << "Lock-free? " << std::boolalpha
              << v1.is_lock_free();

    std::cout << "Value v1, v2: "<<v1 << ", " <<v2; // max, random value

    // Atomically replace the value of v2 by the value of v1
    v2.store(v1);
    std::cout << "Value v1, v2: "<<v1<<", " << v2; // max, max

    // Automatically load and return current value
    std::cout << "Current values v1, v2: " << v1.load() << ", "
              << v2.load() << std::endl; // max, max

    v2.store(0);
    std::cout << "Exchanged: " << v1.exchange(v2)
              << ", " << v2 << std::endl; // max, 0
    std::cout << "Current values v1, v2: " << v1.load() << ", "
              << v2.load() << std::endl; // 0, 0

    // Increment/decrement
    std::atomic_int_fast16_t v3(1);
    //std::atomic_int_fast16_t v4(v3); NO

    std::atomic_int_fast16_t v4;
    v4.store(10);

    std::cout << "Current values v3, v4: " << v3.load() << ", "
              << v4.load() << std::endl; // 1, 10

    v3++; v4--;
    std::cout << "Current values v3, v4: " << v3.load() << ", "
              << v4.load() << std::endl; // 2, 9

    // Addition and substraction
    std::atomic<long long> v5(0);
    std::atomic<int> v6(10);

    v5.fetch_add(10); v6.fetch_sub(20);
    std::cout << "Current values v5, v6: " << v5.load() << ", "
              << v6.load() << std::endl; // 10, -10
```
