
## Strategized Locking via Compile-Time Polymorphism using the concept BasicLockable

```cpp
// strategizedLockingCompileTimeWithConcepts.cpp

#include <iostream>
#include <mutex>
#include <shared_mutex>

template <typename T>
concept BasicLockable = requires(T lo) {
    lo.lock();
    lo.unlock();
};

template <BasicLockable Lock>
class StrategizedLocking {
    Lock& lock;
public:
    StrategizedLocking(Lock& l): lock(l) {
        lock.lock();
    }
    ~StrategizedLocking() {
        lock.unlock();
    }
};

struct NullObjectMutex {
    void lock(){}
    void unlock(){}
};

class NoLock {
public:
    void lock() const {
        std::cout << "NoLock::lock: " << '\n';
        nullObjectMutex.lock();
    }
    void unlock() const {
        std::cout << "NoLock::unlock: " << '\n';
        nullObjectMutex.unlock();
    }
    mutable NullObjectMutex nullObjectMutex;
};

class ExclusiveLock {
public:
    void lock() const {
        std::cout << "    ExclusiveLock::lock: " << '\n';
        mutex.lock();
    }
    void unlock() const {
        std::cout << "    ExclusiveLock::unlock: " << '\n';
        mutex.unlock();
    }
    mutable std::mutex mutex;
};

class SharedLock {
public:
    void lock() const {
        std::cout << "    SharedLock::lock_shared: " << '\n';
        sharedMutex.lock_shared();
    }
    void unlock() const {
        std::cout << "    SharedLock::unlock_shared: " << '\n';
        sharedMutex.unlock_shared();
    }
    mutable std::shared_mutex sharedMutex;
};

int main() {

    std::cout << '\n';

    NoLock noLock;
    StrategizedLocking<NoLock> stratLock1{noLock};

    {
        ExclusiveLock exLock;
        StrategizedLocking<ExclusiveLock> stratLock2{exLock};
        {
            SharedLock sharLock;
            StrategizedLocking<SharedLock> stratLock3{sharLock};
        }
83      }
84
85      std::cout << '\n';
86
87    }
```

^18 https://en.cppreference.com/w/cpp/concepts  
^19 https://en.cppreference.com/w/cpp/named_req

### 9.2.2.3 Further Information

- Design Patterns: Elements of Reusable Object-Oriented Software²²
- Strategy Pattern²³
- Null Object Pattern²⁴
- Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects²⁵

### 9.2.3 Thread-Safe Interface

The thread-safe interface fits very well when the critical sections are just objects. The naïve idea to protect all member functions with a lock causes, in the best case, a performance issue and, in the worst case, a deadlock. The small pseudocode makes my point clear.

```cpp
struct Critical{
    void memberFunction1(){
        lock(mut);
        memberFunction2();
        ...
    }
    void memberFunction2(){
        lock(mut);
        ...
    }
    mutex mut;
};

Critical crit;
crit.memberFunction1();
```

Calling `crit.memberFunction1` causes the mutex `mut` being locked twice. For simplicity reasons the `lock` is a scoped lock. Here are the two issues:

- 1. when `lock` is a recursive lock, the second `lock(mut)` in `memberFunction2` is redundant.
- 2. when `lock` is a non-recursive lock, the second `lock(mut)` in `memberFunction2` leads to undefined behavior. Most of the time, you get a `deadlock`.

The thread-safe interface overcomes both issues. Here is the straightforward idea:

- All interface member functions (`public`) should use a lock.
- All implementation member functions (`protected` and `private`) must not use a lock.
- The interface member functions call only `protected` or `private` member functions but no `public` member functions.

The `ThreadSafeInterface.cpp` program shows its usage.

## The ThreadSafe Interface

```cpp
1  // ThreadSafeInterface.cpp
2
3  #include <iostream>
4  #include <mutex>
5  #include <thread>
6
7  class Critical{
8
9  public:
10     void interface1() const {
11         std::lock_guard<std::mutex> lockGuard(mut);
12         implementation1();
13     }
14     void interface2(){
15         std::lock_guard<std::mutex> lockGuard(mut);
16         implementation2();
17         implementation3();
18         implementation1();
19     }
20 private:
21     void implementation1() const {
22         std::cout << "implementation1: "
23                   << std::this_thread::get_id() << '\n';
24     }
25     void implementation2(){
26         std::cout << "  implementation2: "
27                   << std::this_thread::get_id() << '\n';
28     }
29     void implementation3(){
30         std::cout << "    implementation3: "
31                   << std::this_thread::get_id() << '\n';
32     }
33 
34     mutable std::mutex mut;
35 
36 
37 };
38 
39 int main(){
40 
41     std::cout << '\n';
42 
43     std::thread t1([&]{
44         const Critical crit;
45         crit.interface1();
46     });
47 
48     std::thread t2([&]{
49         Critical crit;
50         crit.interface2();
51         crit.interface1();
52     });
53 
54     Critical crit;
55     crit.interface1();
56     crit.interface2();
57
58    t1.join();
59    t2.join();
60
61    std::cout << '\n';
62
63 }
```

Three threads, including the main thread, use instances of `Critical`. Thanks to the thread-safe interface, all calls to the public API are synchronized. The mutex `mut` in line 35 is mutable and can be used in the constant member function `interface1`.

The advantages of the thread-safe interface are threefold.

- 1. A recursive call of a mutex is not possible. Recursive calls on a non-recursive mutex are undefined behavior in C++ and usually end in a deadlock.
- 2. The program uses minimal locking and, therefore, minimal synchronization. Using just a `std::recursive_mutex` in each public or private member function of the class `Critical` would end in more expensive synchronizations.
- 3. From the user perspective, `Critical` is straightforward to use because synchronization is only an implementation detail.

Each interface member function delegates its work to the corresponding implementation member function. The indirection overhead is a typical disadvantage of the thread-safe interface pattern.

The output of the program shows the interleaving of the three threads.

![](img/d61a6c83410484053b8892275d2fcc4f_499_0.png)

Thread Safe Interface

Although the thread-safe interface seems easy to implement, there are two grave perils you have to keep in mind.

#### 9.2.3.1 Perils

Using a static member in your class or having virtual interfaces requires special care.

##### 9.2.3.1.1 Static members

When your class has a static member that is not constant, you have to synchronize all member function calls on the class instances.

**The Thread Safe Interface with a static member**

```cpp
class Critical{

public:
    void interface1() const {
        std::lock_guard<std::mutex> lockGuard(mut);
        implementation1();
    }
    void interface2(){
        std::lock_guard<std::mutex> lockGuard(mut);
        implementation2();
```
