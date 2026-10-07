
## 7.5 Atomic Operation and Memory Model CHAPTER 07 PARALLELISM AND CONCURRENCY

4. Final Consistency: It is the weakest consistency requirement. It only guarantees that an operation will be observed at a certain point in the future, but does not require the observed time. So we can even strengthen this condition a bit, for example, to specify that the time observed for an operation is always bounded. Of course this is no longer within our discussion.

```
x.store(3)   x.store(4)
T1--------------------------------------------------------------------->
T2--------------------------------------------------------------------->
x.read()      x.read()      x.read()      x.read()
```

In the case above, if we assume the initial value of x is 0, then the four 'x.read()' in T2 may not be limited to the following:

```
3 4 4 4 // The write operation of x was quickly observed
0 3 3 4 // There is a delay in the observed time of the x write operation
0 0 0 4 // The last read read the final value of x, but the previous changes were not observed.
0 0 0 0 // The write operation of x is not observed in the current time, but the situation
```

## Memory Orders

To achieve the ultimate performance and achieve consistency of various strength requirements, C++11 defines six different memory sequences for atomic operations. The option std::memory_order specifies synchronization models between multiple threads:

1. Relaxed model: Under this model, atomic operations within a single thread are executed sequentially, and instruction ordering is not allowed, but the order of atomic operations between threads is arbitrary. The type is specified by std::memory_order_relaxed. Let's look at an example:

```cpp
std::atomic<int> counter = {0};
std::vector<std::thread> vt;
for (int i = 0; i < 100; ++i) {
    vt.emplace_back([&]{
        counter.fetch_add(i, std::memory_order_relaxed);
    });
}
for (auto& t : vt) {
    t.join();
}
std::cout << "current counter: " << counter << std::endl;
```

2. Release/consumption model: In this model, we begin to limit the order of operations between processes. If a thread needs to modify a value, but another thread has a dependency on that operation of the value, that is, the latter depends. Specifically, A has completed three writes to x, and B releases only on the third write operation, regardless of the first two writes of x, A when calling x.release() (ie use std::memory_order_release), the option std::memory_order_consume ensures that B observes when calling x.load()) Three writes to x. Let's look at an example:

```cpp
// initialize as nullptr to prevent consumer load a dangling pointer
std::atomic<int*> ptr(nullptr);
int v;
std::thread producer([&]() {
    int* p = new int(42);
    ptr.store(p, std::memory_order_release);
});

std::thread consumer([&]() {
    int* p;
    while (!(p = ptr.load(std::memory_order_consume))) {
        std::cout << "x: " << *p << std::endl;
        std::cout << "y: " << v << std::endl;
    }
});

producer.join();
consumer.join();
```

3. Release/Acquire model: Under this model, we can further tighten the order of atomic operations between different threads, specifically specifying the timing between releasing std::memory_order_acquire and getting std::memory_order_acquire. All writes before the release operation are visible to any other thread, ie, happens-before.

As you can see, std::memory_order_release ensures that the write behavior does not occur before the release operation, which is a forward barrier, std::memory_order_acquire ensures that its previous write behavior does not occur after this acquisition operation, which is a backward barrier. For the std::memory_order_acq_rel option, it combines the characteristics of two and defines a memory barrier, so that the current thread's reading and writing of memory will not be rearranged before and after this operation.

Let's check out an example:

```cpp
std::vector<int> v;
std::atomic<int> flag = {0};
std::thread release([&]() {
    v.push_back(42);
    flag.store(1, std::memory_order_release);
});

std::thread acquire([&]() {
    int expected = 1; // must before compare_exchange_strong
    while (!flag.compare_exchange_strong(expected, 2, std::memory_order_acq_rel)) {
        expected = 1; // must after compare_exchange_strong
    }
    // flag has changed to 2
    while (flag.load(std::memory_order_acquire) < 2) {
        std::cout << v[0] << std::endl; // must be 42
    }
});
release.join();
acq.join();
acquire.join();
```

In this case use compare_exchange_strong, which is the Compare-and-swap primitive, which has a weaker version, compare_exchange_weak, which allows a failure to be returned if unsuccessful. The reason is due to false failure on some platforms, specifically, when the CPU performs context switch, another thread loads the address to produce inconsistency. In addition, the performance of compare_exchange_strong may be slightly worse than compare_exchange_weak, but in most cases, compare_exchange_strong should be used.

4. Sequential Consistent Model: Under this model, atomic operations satisfy consistency, which can be specified explicitly by std::memory_order_seq_cst. Let's look at a simple example:

```cpp
std::atomic<int> counter{0};
std::vector<std::thread> vt;
for (int i = 0; i < 100; ++i) {
    vt.emplace_back([&](){
        counter.fetch_add(1, std::memory_order_seq_cst);
    });
}

for (auto & t : vt) {
    t.join();
}
std::cout << "current counter: " << counter << std::endl;
```

This example is essentially the same as the first. Just change the memory order of the atomic operation to memory_order_seq_cst. Interested readers can write their own programs to measure performance difference caused by these memory sequences.

## Conclusion

The C++11 language provides support for concurrent programming. This section introduces `std::thread/mutex/std::future`, important tools that can't be avoided in concurrent programming. In addition, we also introduced the `memory model` as one of the most important features of C++11. They provide a critical foundation for high performance computing of C++.

## Exercises

- 1. Write a simple thread pool that provides the following features:

```cpp
ThreadPool p(4); // specify work thread

// enqueue a task, and return a std::future
auto f = pool.enqueue([](int life) {
    return life;
}, 42);

// fetch result from future
std::cout << f.get() << std::endl;
```

- 2. Use std::atomic<bool> to implement a mutex.

## Further Readings

- C++
- Thread document
- Herlihy, M. P., & Wing, J. M. (1990). Linearizability: a correctness condition for concurrent objects. ACM Transactions on Programming Languages and Systems, 12(3), 463–492. https://doi.org/10.1145/78969.78972

## Chapter 08 File System

The file system library provides functions related to the operation of the file system, path, files, directories, and so on. Similar to the regular expression library, it was one of the first libraries launched by boost and eventually merged into the C++ standard.

### 8.1 Document and Link

TODO:

### 8.2 std::filesystem

TODO:

## Chapter 09 Minor Features

### 9.1 New Type

**long long int**

long long int is not the first to be introduced in C++11. In fact, as early as C99, long long int has been included in the C standard, so most compilers already support it. C++11 formally incorporate it into the standard library, specifying a long long int type with at least 64 bits.

### 9.2 noexcept and Its Operations

One of the big advantages of C++ over C is that C++ itself defines a complete set of exception handling mechanisms. However, before C++11, almost no one used to write an exception declaration after the function name. Starting from C++11, this mechanism was deprecated, so we will not discuss or introduce the previous mechanism. How to work and how to use it, you should not take the initiative to understand it.

C++11 simplifies exception declarations into two cases:

- 1. The function may throw any exceptions
- 2. The function can't throw any exceptions

And use noexcept to limit these two behaviors, for example:

```cpp
void may_throw();      // May throw any exception
void no_throw() noexcept; // Cannot throw any exception
```

If a function is modified with noexcept, the compiler will use std::terminate() to immediately terminate the program.

noexcept can also be used as an operator to manipulate an expression. When the expression has no exception, it returns true, otherwise it returns false.

```cpp
#include <iostream>
void may_throw() {
    throw;
}
```
