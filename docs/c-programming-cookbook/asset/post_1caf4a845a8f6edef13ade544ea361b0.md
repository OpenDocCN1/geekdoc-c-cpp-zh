
## Chapter 7: Concurrency and Multithreading

## Introduction

Exploring parallel computing in C++ apps is something we need to master so that we can improve speed, responsiveness, and scalability. The intricacies of concurrent programming are broken down into manageable chunks in this chapter, which offers helpful hints and solutions for making the most of C++'s threading features. Beginning with the std::thread foundations, we will go into the ins and outs of threading to learn how to generate, manage, and synchronize threads to do tasks simultaneously, making our application far more efficient to execute.

To keep data intact and avoid race circumstances when numerous threads access shared resources, the concurrency trip continues with a thorough examination of synchronization methods, including atomics, locks, and mutexes. In concurrent programs, thread safety is of the utmost importance. This chapter provides solutions and best practices to avoid common errors in multithreaded programming. Further streamlining the process of optimizing our application for concurrent operations, we will also explore the parallel algorithms included in C++20. These algorithms permit the easy construction of parallel execution patterns.

A complete toolbox for developing strong multithreaded programs is provided, including coverage of managing the thread lifecycle and state, understanding and using futures and promises for asynchronous task execution, and implementing task-based concurrency. Particular emphasis is placed on avoiding deadlocks, which are prevalent in concurrent programming, by providing examples of strategies that do just that. This chapter teaches you how to use C++'s concurrency and multithreading features to their fullest potential through examples and explanations. This will allow them to build efficient, scalable, and high-performance apps that can handle today's software problems.

## Recipe 1: Perform Basic Threading with std::thread

### Situation

Making use of the host system's numerous cores becomes crucial when our application starts to process more user requests at once and increasingly complicated background operations. The std::thread module in C++ is useful in this situation. A simple yet powerful method to construct and manage threads, std::thread was introduced in C++11 and allows tasks to be completed simultaneously. Software engineers may make our application faster, more efficient, more scalable by learning how to use std::thread correctly.

### Practical Solution

### Creating and Using Threads

The first step in utilizing multithreading with std::thread involves spawning new threads and assigning them tasks to execute. Each std::thread instance manages a separate thread of execution. The thread starts executing immediately upon its creation, given a function (or a callable object) to run.

Following is the example of basic threading:

```cpp
#include <iostream>
#include <thread>
#include <string>

// A simple function that will be executed by a thread
void printMessage(const std::string& message) {
    std::cout << "Thread message: " << message << std::endl;
}

int main() {
    // Creating a thread to execute the printMessage function
    std::thread threadObj(printMessage, "Hello from std::thread!");

    // Ensure the main thread waits for the new thread to finish
    if (threadObj.joinable()) {
        threadObj.join(); // Blocks the current thread until threadObj finishes
    }

    return 0;
}
```

In the above given sample program, printMessage is executed in a separate thread from the main program thread. After creating the thread, the main thread waits for threadObj to complete its execution using join(). The joinable() check ensures that the program doesn't attempt to join a thread that's already been joined or not joinable, which would lead to a runtime error.

### Managing Thread Lifecycle

It's crucial to manage the lifecycle of threads properly to avoid undefined behavior. The join() function is used to wait for a thread to finish its execution, ensuring that the program doesn't exit prematurely. Alternatively, detach() can be used to allow a thread to execute independently of the main thread, but care must be taken to ensure that detached threads do not access any resources that may be cleaned up by the main thread or become unreachable. Proper thread lifecycle management, including the use of join() or detach(), is essential to ensure that applications remain stable and resources are correctly managed.

## Recipe 2: Implement Synchronization Mechanisms: Mutex, Locks, and Atomics

### Situation

The importance of checking data for consistency and integrity grows as more threads run in parallel. Race conditions, ill-defined behavior, or corrupted data can result from concurrent changes to shared resources that are not properly synchronized. C++ has a number of synchronization methods, such as locks, mutexes, and atomic operations, to control who has access to what shared resources. In order to create dependable programs that are thread-safe, it is essential to understand and effectively implement these principles.

### Practical Solution

### Mutexes and Locks

Mutexes (mutual exclusions) are used to protect shared data by only allowing one thread to access the data at a time. The std::mutex class offers a straightforward interface for locking and unlocking, but C++ also provides RAII-style lock management classes like std::lock_guard and std::unique_lock to simplify mutex usage and prevent common pitfalls.

Following is the example of using a mutex with std::lock_guard:

```cpp
#include <iostream>
#include <mutex>
#include <thread>
#include <vector>

std::mutex mu;
int sharedData = 0;

void incrementSharedData() {
    std::lock_guard<std::mutex> lock(mu); // Locks mu upon construction
                                           // and unlocks on destruction
    ++sharedData;
    std::cout << "Data incremented to " << sharedData << std::endl;
}

int main() {
    std::vector<std::thread> threads;

    for (int i = 0; i < 5; ++i) {
        threads.emplace_back(incrementSharedData);
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

### Atomic Operations

For simple data types, atomic operations offer a lock-free mechanism to ensure thread safety. C++ provides the std::atomic template class for types that can be read, written, or modified atomically.

Following is the example of using std::atomic:

```cpp
#include <atomic>
#include <iostream>
#include <thread>
#include <vector>

std::atomic<int> atomicData(0);

void atomicIncrement() {
    int oldValue = atomicData.fetch_add(1); // Atomically increments atomicData and returns the old value
    std::cout << "Data incremented from " << oldValue << std::endl;
}

int main() {
    std::vector<std::thread> threads;

    for (int i = 0; i < 5; ++i) {
        threads.emplace_back(atomicIncrement);
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

Mutexes, combined with RAII-style locks, provide a robust way to protect complex data structures or sections of code that require exclusive access. For operations on simple data types, atomic operations offer a performant, lock-free alternative to ensure thread safety.

## Recipe 3: Achieve Thread Safety

### Situation

Thread safety is becoming increasingly important as our application adds functionality that needs concurrent execution. When developing code, it is important to keep thread safety in mind. This is particularly true when dealing with shared data and numerous threads executing at the same time. Making our application thread safe will keep it efficient and dependable in all kinds of situations where there is a lot of concurrency, including when there is a race condition, a deadlock, or data corruption.

### Practical Solution

### Strategies for Thread Safety

Achieving thread safety in a multithreaded application like our application requires employing specific coding practices and utilizing C++ concurrency features effectively. Following are some fundamental strategies:

- Minimize Shared State: Reduce the amount of shared data accessible by multiple threads. This can involve limiting the scope of shared variables or using thread-local storage for data that does not need to be shared across threads.
- Immutable Data: Whenever possible, use immutable data structures that cannot be modified after their creation. Immutable objects are inherently thread-safe since their state cannot change, eliminating the need for synchronization.
- Synchronization Mechanisms: For data that must be shared and modified by multiple threads, use appropriate synchronization mechanisms to manage access. Mutexes, locks, and atomic operations are key tools provided by C++ for safeguarding shared resources.
- Higher-level Constructs: Leverage higher-level concurrency constructs like thread pools, futures, promises, and task-based parallelism which abstract away many low-level threading details, including some aspects of thread safety.

Following is the sample program of using Mutex for thread safety:

```cpp
#include <iostream>
#include <mutex>
#include <thread>
```
