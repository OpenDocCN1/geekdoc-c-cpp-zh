tions. For an extensive discussion of atomics’ performance vs. that of related technologies, see the blog post, “A Concurrency Cost Hierarchy.”

# Incrementing an `int`, a `std::atomic<int>` and a `std::atomic_ref<int>` from Two Concurrent Threads

Figure 17.13 presents a simple demonstration of two concurrent threads incrementing

+   - an unprotected `int`,
+   - an object of type `std::atomic<int>` and
+   - an object of the class template `std::atomic_ref<int>`.

Class template `std::atomic_ref` was introduced in C++20 to enable atomic operations on a referenced variable (an `int` in this program). First, we’ll show `std::atomic<int>` and `std::atomic_ref<int>` in action, then we’ll say a bit more about atomics.

```
```cpp
// Fig. 17.13: atomic.cpp
// Incrementing integers from concurrent threads
// with and without atomics.
#include <atomic>
#include <format>
#include <iostream>
#include <thread>

int main() {
    int count{0};
    std::atomic<int> atomicCount{0};
    int count2{0};
    std::atomic_ref<int> atomicRefCount{count2};

    {
        std::cout << "Two concurrent threads incrementing int count1, "
                  << "atomicCount and atomicRefCount\n\n";

        // lambda to increment counters
        auto incrementer{
            [&]() {
                for (int i{0}; i < 1000; ++i) {
                    ++count1; // no synchronization
                    ++atomicCount; // ++ is an atomic operation
                    ++atomicRefCount; // ++ is an atomic operation
                    std::this_thread::yield(); // force thread to give up CPU
                }
            }
        };

        std::jthread t1{incrementer};
        std::jthread t2{incrementer};
    }
}
```
```

**Fig. 17.13**  Incrementing integers from concurrent threads with and without atomics. (Part 1 of 2.)