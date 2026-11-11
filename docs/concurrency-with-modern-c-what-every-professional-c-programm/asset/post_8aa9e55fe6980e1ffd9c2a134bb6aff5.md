
Now, let us look once more at the spinlock in the subsection `std::atomic_flag`. We can write it more efficiently because the synchronization is done with the `atomic_flag` flag. Therefore the acquire-release semantic applies.

**A Spinlock with acquire-release semantic**

```cpp
// spinlockAcquireRelease.cpp

#include <atomic>
#include <thread>

class Spinlock{
    std::atomic_flag flag;
    public:
    Spinlock(): flag(ATOMIC_FLAG_INIT) {}

    void lock(){
        while(flag.test_and_set(std::memory_order_acquire));
    }

    void unlock(){
        flag.clear(std::memory_order_release);
    }
};

Spinlock spin;

void workOnResource(){
    spin.lock();
    // shared resource
    spin.unlock();
}

int main(){

    std::thread t(workOnResource);
    std::thread t2(workOnResource);

    t.join();
    t2.join();

}
```

The flag.clear call in line 16 is a release, the flag.test_and_set call in line 12 an acquire operation, and the acquire synchronizes with the release operation. The heavyweight synchronization of two threads with sequential consistency (std::memory_order_seq_cst) is replaced by the more lightweight and performant acquire-release semantic (std::memory_order_acquire and std::memory_order_release). The behavior is not affected.

Although the flag.test_and_set(std::memory_order_acquire) call is a read-modify-write operation, the acquire semantic is sufficient. In summary, flag is an atomic and guarantees, therefore, modification order. This means all modifications to flag occur in some particular total order.

The acquire-release semantic is transitive. That means if you have an acquire-release semantic between two threads (a, b) and an acquire-release semantic between (b, c), you get an acquire-release semantic between (a, c).

### 2.4.3.1 Transitivity

A release operation synchronizes with an acquire operation on the same atomic variable and establishes ordering constraint. These are the components to synchronize threads in a performant way if they act on the same atomic. How can that work if two threads share no atomic variable? We do not want any sequential consistency because that is too expensive, but we want the light-weight acquire-release semantic.

The answer to this question is straightforward. Applying the transitivity of the acquire-release semantic, we can synchronize independent threads.

In the following example, thread t2 with its work package deliveryBoy is the connection between two independent threads t1 and t3.

**Transitivity of the acquire-release semantics**

```cpp
// transitivity.cpp

#include <atomic>
#include <iostream>
#include <thread>
#include <vector>

std::vector<int> mySharedWork;
std::atomic<bool> dataProduced(false);
std::atomic<bool> dataConsumed(false);

void dataProducer(){
    mySharedWork = {1,0,3};
    dataProduced.store(true, std::memory_order_release);
}

void deliveryBoy(){
    while(!dataProduced.load(std::memory_order_acquire));
    dataConsumed.store(true, std::memory_order_release);
}

void dataConsumer(){
    while(!dataConsumed.load(std::memory_order_acquire));
    mySharedWork[1] = 2;
}

int main(){

    std::cout << '\n';

    std::thread t1(dataConsumer);
    std::thread t2(deliveryBoy);
    std::thread t3(dataProducer);

    t1.join();
    t2.join();
    t3.join();

    for (auto v: mySharedWork){
        std::cout << v << " ";
    }

    std::cout << "\n\n";

}
```

The output of the program is deterministic. mySharedWork has the values 1, 2, and 3.

![](img/d61a6c83410484053b8892275d2fcc4f_92_0.png)

Output of the program transitivity.cpp

There are two critical observations:

1. Thread t2 waits in line 18, until thread t3 sets dataProduced to true (line 14).
2. Thread t1 waits in line 23, until thread t2 sets dataConsumed to true (line 19).

Let me explain the rest with a graphic.

```cpp
void dataProducer() {
    mySharedWork[1, , ,];
    dataProduced.store(true, std::memory_order_release);
}

void deliveryBoy() {
    while(!dataProduced.load(std::memory_order_acquire)) ;
    dataConsumed.store(true, std::memory_order_release);
}

void dataConsumer() {
    while(!dataConsumed.load(std::memory_order_acquire)) ;
    mySharedWork[1] == 2;
}
```

Transitivity of the acquire-release semantic

- The **blue** arrows are the *sequenced-before* relations. This means that all operations in one thread are executed in source code order.
- The **red** arrows are the *synchronizes-with* relations. The reason is the acquire-release semantic of the atomic operations on the same atomic. The synchronization between the atomics, and therefore between the threads happen at specific points.
- *sequenced-before* establishes a *happens-before* and *synchronizes-with* an *inter-thread happens-before* relation.

The rest is pretty simple. The *happens-before* and *inter-thread happens-before* order of the instructions correspond to the arrows' direction from top to bottom. Finally, we guarantee that `mySharedWork[1] == 2` is executed last.

A release operation *synchronizes-with* an acquire operation on the same atomic variable, so we can easily synchronize threads, if ... . The typical misunderstanding is about the if.

### 2.4.3.2 The Typical Misunderstanding

What is my motivation for writing about the typical misunderstanding of the acquire-release semantic? Many of my readers and students have already fallen into this trap. Let's look at the straightforward case.

### 2.4.3.2.1 Waiting Included

**Acquire-release with waiting**

```cpp
// acquireReleaseWithWaiting.cpp

#include <atomic>
#include <iostream>
#include <thread>
#include <vector>

std::vector<int> mySharedWork;
std::atomic<bool> dataProduced(false);

void dataProducer(){
    mySharedWork = {1, 0, 3};
    dataProduced.store(true, std::memory_order_release);
}

void dataConsumer(){
    while( !dataProduced.load(std::memory_order_acquire) );
    mySharedWork[1] = 2;
}

int main(){

    std::cout << '\n';

    std::thread t1(dataConsumer);
    std::thread t2(dataProducer);

    t1.join();
    t2.join();

    for (auto v: mySharedWork){
        std::cout << v << "  ";
    }

    std::cout << "\n\n";

}
```

The consumer thread t1 in line 17 waits until the producer thread t2 in line 13 sets dataProduced to true. dataProduced is the guard, and it guarantees that access to the non-atomic variable mySharedWork is synchronized. Synchronized means that the producer thread t2 initializes mySharedWork, then the consumer thread t1 finishes the work by setting mySharedWork[1] to 2. The program is well-defined.

![](img/d61a6c83410484053b8892275d2fcc4f_98_0.png)

### 2.4.3.2.3 The Solution

*synchronizes-with* means: if `dataProduced.store(true, std::memory_order_release)` happens before `dataProduced.load(std::memory_order_acquire)`, then all visible effects of the operations before `dataProduced.store(true, std::memory_order_release)` are visible after `dataProduced.load(std::memory_order_acquire)`. The key is the word *if*. That *if* is guaranteed in the first program with the predicate (`while(!dataProduced.load(std::memory_order_acquire))`).

Here it comes once again, but more formally.

All operations before `dataProduced.store(true, std::memory_order_release)` *happens-before* all operations after `dataProduced.load(std::memory_order_acquire)`, if the following holds: `dataProduced.store(true, std::memory_order_release)` *happens-before* `dataProduced.load(std::memory_order_acquire)`.

### 2.4.3.3 Release Sequence

A release sequence is quite an advanced concept when dealing with acquire-release semantic. So let first start with the acquire-release semantic in the following example.
