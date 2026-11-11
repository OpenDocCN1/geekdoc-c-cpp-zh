
### 2.3.2.1.1 Spinlock versus Mutex

What happens to the CPU load if the function workOnResource locks the spinlock for 2 seconds (lines 23 - 25)?

### Waiting with a spinlock

```cpp
// spinlockSleep.cpp

#include <atomic>
#include <thread>

class Spinlock{
  std::atomic_flag flag = ATOMIC_FLAG_INIT;
public:

  void lock(){
    while( flag.test_and_set() );
  }

  void unlock(){
    flag.clear();
  }

};

Spinlock spin;

void workOnResource(){
  spin.lock();
  std::this_thread::sleep_for(std::chrono::milliseconds(2000));
  spin.unlock();
}


int main(){

  std::thread t(workOnResource);
  std::thread t2(workOnResource);

  t.join();
  t2.join();

}
```

If the theory is correct, one of the four cores of my PC is fully utilized. This is precisely what happens.

Take a look at the screenshot.

![](img/d61a6c83410484053b8892275d2fcc4f_49_0.png)

A spinlock that sleeps for two seconds

The screenshot shows nicely that the load of one core reaches 100% on my PC. Each time a different core performs busy waiting.

Now I use a mutex instead of a spinlock. Let’s see what happens.

### Waiting with a mutex

```cpp
// mutex.cpp

#include <mutex>
#include <thread>

std::mutex mut;

void workOnResource(){
  mut.lock();
  std::this_thread::sleep_for(std::chrono::milliseconds(5000));
  mut.unlock();
}

14 int main(){
15 
16     std::thread t(workOnResource);
17     std::thread t2(workOnResource);
18 
19     t.join();
20     t2.join();
21 
22 }
```

Although I executed the program several times, I did not observe a significant load on any of the cores.

![](img/d61a6c83410484053b8892275d2fcc4f_50_0.png)

A mutex that sleeps for two seconds

Thanks to std::atomic_flag, thread synchronization is straightforward and fast.

### 2.3.2.2 Thread Synchronization

for pointers `std::atomic<T>*`, and with C++20 for smart pointers `std::atomic<smart T*>`, full specialisations for integral types `std::atomic<integral type>`, and with C++20 for floating-point types `std::atomic<floating-point>`.

The atomic booleans, the atomic user-defined types, and the atomic smart pointer support the same interface. I call it the fundamental atomic interface. The atomic pointer extends the fundamental atomic interface. The same applies to the atomic arithmetic types: the atomic floating-point types extend the interface of the atomic pointers, and the atomic integral types extend the interface of the atomic floating-point types.

The downside of the various variations of `std::atomic` is that you do not have the guarantee that they are lock-free. In the next subsection, I present the various atomic types based on their interface. Roughly speaking, there are four subsections. Let me start with atomic booleans, atomic user-defined types, and atomic smart pointers (C++20).

### 2.3.3.1 Fundamental Atomic Interface

The three partial specializations `std::atomic<bool>`, `std::atomic<user-defined type>`, and `std::atomic<smart T*>` support the fundamental atomic interface.

| Member functions | Description |
| :--- | :--- |
| is_lock_free | Checks if the atomic object is lock-free. |
| atomic_ref<T>::is_always_lock_free | Checks at compile time if the atomic type is always lock-free. |
| load | Atomically returns the value of the atomic. |
| operator T | Atomically returns the value of the atomic. Equivalent to atom.load(). |
| store | Atomically replaces the value of the atomic with the non-atomic. |
| exchange | Atomically replaces the value with the new value. Returns the old value. |
| compare_exchange_strong | Atomically compares and eventually exchanges the value. Details are here. |
| compare_exchange_weak | |
| notify_one (C++20) | Notifies one atomic wait operation. |
| notify_all (C++20) | Notifies all atomic wait operations. |
| wait (C++20) | Blocks until it is notified. Compares itself with the old value to protect against spurious wakeups and lost wakeups. If the old value compares to unequal, returns. |

### 2.3.3.1.1 std::atomic<bool>

std::atomic<bool> has a lot more to offer than std::atomic_flag. It can explicitly be set to true or false.

![](img/d61a6c83410484053b8892275d2fcc4f_55_0.png)

**atomic is not volatile**

What does the keyword volatile in C# and Java have in common with the keyword volatile in C++? Nothing! That's the difference between volatile and std::atomic.

- volatile: is for special objects on which optimized read or write operations are not allowed.
- std::atomic: defines atomic variables, which are meant for a thread-safe reading and writing.

The confusion starts here. The keyword volatile in Java and C# has the meaning of std::atomic in C++. Alternatively, volatile has no multithreading semantics in C++. volatile is typically used in embedded programming to denote objects which can change independently of the regular program flow. One example is an object which represents an external device (memory-mapped I/O). Because these objects can change independently of the regular program flow and their value is directly written into main memory, no optimized storage in caches occurs.

std::atomic<bool> is already sufficient to synchronise two threads and I can, therefore, implement a kind of a condition variable with a std::atomic<bool>.

### 2.3.3.1.2 Simulating a Condition Variable

Let's first use a condition variable to synchronize two threads.

**Usage of a condition variable**

```cpp
// conditionVariable.cpp

#include <condition_variable>
#include <iostream>
#include <thread>
#include <vector>

std::vector<int> mySharedWork;
std::mutex mutex_;
std::condition_variable condVar;

bool dataReady{false};

void waitingForWork(){
15    std::cout << "Waiting " << '\n';
16    std::unique_lock<std::mutex> lck(mutex_);
17    condVar.wait(lck, []{ return dataReady; });
18    mySharedWork[1] = 2;
19    std::cout << "Work done " << '\n';
20  }
21
22  void setDataReady(){
23    mySharedWork = {1, 0, 3};
24    {
25      std::lock_guard<std::mutex> lck(mutex_);
26      dataReady = true;
27    }
28    std::cout << "Data prepared" << '\n';
29    condVar.notify_one();
30  }
31
32  int main(){
33
34    std::cout << '\n';
35
36    std::thread t1(waitingForWork);
37    std::thread t2(setDataReady);
38
39    t1.join();
40    t2.join();
41
42    for (auto v: mySharedWork){
43      std::cout << v << " ";
44    }
45
46
47    std::cout << "\n\n";
48
49  }
```

Let me say a few words about the program. For an in-depth discussion of condition variables, read the chapter condition variables in this book.

Thread t1 waits in line 17 for the notification of thread t2. Both threads use the same condition variable `condVar` and synchronize on the same mutex `mutex_`. How does the workflow run?

- Thread t2
  - prepares the work package mySharedWork = {1, 0, 3}

![](img/d61a6c83410484053b8892275d2fcc4f_59_0.png)

Synchronizations of two threads with an atomic and a condition variable

## Push versus Pull Principle

I cheated a little. There is one key difference between synchronizing threads with a condition variable and `std::atomic<bool>`. The condition variable notifies the waiting thread (`condVar.notify()`) that it should proceed with its work. The waiting thread with `std::atomic<bool>` checks if the sender is done with its work (`dataReady == true`).

The condition variable notifies the waiting thread (push principle) while the atomic boolean repeatedly asks for the value (pull principle).

`std::atomic<bool>` and the other full or partial specializations of `std::atomic` support the bread and butter of all atomic operations: `compare_exchange_strong` and `compare_exchange_weak`.

### 2.3.3.1.3 `compare_exchange_strong` and `compare_exchange_weak`

`compare_exchange_strong` has the syntax: `bool compare_exchange_strong(T& expected, T& desired)`. Because this operation compares and exchanges its values in one atomic operation, it is often called compare and swap (CAS). This kind of operation is available in many programming languages and is the foundation of non-blocking algorithms. Of course, the behavior may vary a little. `atomicValue.compare_exchange_strong(expected, desired)` has the following behavior.

- If the atomic comparison of `atomicValue` with `expected` returns true, `atomicValue` is set in the same atomic operation to `desired`.
- If the comparison returns false, `expected` is set to `atomicValue`.

The reason the operation `compare_exchange_strong` is called strong is apparent. There is also a member function `compare_exchange_weak`. The weak version can fail spuriously. That means, although `atomicValue == expected` holds, `atomicValue` was not set to `desired` and the function call returns
