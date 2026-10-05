unlock() and functions.

A lock_guard automatically releases a mutex when it goes out of scope even if an exception is thrown. The following example shows how to use a std::lock_guard<mutex> object:

```
#include <iostream>
#include <thread>
#include <mutex>

size_t sum = 0;
std::mutex m1;

void adder(std::string id, size_t loop_limit) {
    // create a lock_guard object with parameter m1
    std::lock_guard<std::mutex> lock(m1);
    // critical section
    for (size_t i = 0; i < loop_limit; i++) {
        sum += i;
    }
    std::cout << id << ":" << sum << std::endl;
}

int main() {
    std::thread t1(adder, "t1", 20);
    std::thread t2(adder, "t2", 30);
    t1.join();
    t2.join();
    return 0;
}

// output
t1:190
t2:625
```

We create a lock_guard object lock for mutex m1. A thread entering the adder function will wait until a lock is acquired. The lock will be automatically released once the lock_guard object goes out of scope or if an exception is thrown.

Ownership of a lock_guard object cannot be given by a copy constructor or assignment.