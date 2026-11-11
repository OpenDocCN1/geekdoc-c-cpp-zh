
## 基于 BasicLockable 概念通过编译期多态实现策略化锁定

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

### 9.2.2.3 更多信息

- 《设计模式：可复用面向对象软件的基础》²²
- 策略模式²³
- 空对象模式²⁴
- 《面向模式的软件架构：并发和网络对象模式》²⁵

### 9.2.3 线程安全接口

当临界区只是对象时，线程安全接口非常适用。用锁保护所有成员函数的朴素想法，最好的情况会导致性能问题，最坏的情况会导致死锁。下面这段小型伪代码清楚地说明了我的观点。

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

调用 `crit.memberFunction1` 会导致互斥量 `mut` 被锁定两次。为简单起见，这里的 `lock` 是作用域锁。这里有两个问题：

- 1. 当 `lock` 是递归锁时，`memberFunction2` 中的第二个 `lock(mut)` 是多余的。
- 2. 当 `lock` 是非递归锁时，`memberFunction2` 中的第二个 `lock(mut)` 会导致未定义行为。大多数情况下，你会遇到 `deadlock`。

线程安全接口克服了这两个问题。下面是直观的思路：

- 所有接口成员函数（`public`）都应使用锁。
- 所有实现成员函数（`protected` 和 `private`）不得使用锁。
- 接口成员函数只调用 `protected` 或 `private` 成员函数，而不调用 `public` 成员函数。

`ThreadSafeInterface.cpp` 程序展示了它的用法。

## 线程安全接口

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

三个线程（包括主线程）使用 `Critical` 的实例。得益于线程安全接口，对公共 API 的所有调用都是同步的。第 35 行的互斥量 `mut` 是 mutable 的，因此可以在常量成员函数 `interface1` 中使用。

线程安全接口的优势有三点。

- 1. 不可能对互斥量进行递归调用。在 C++ 中，对非递归互斥量进行递归调用属于未定义行为，通常会导致死锁。
- 2. 程序使用最少的锁定，因此也使用最少的同步。如果在 `Critical` 类的每个公共或私有成员函数中仅使用一个 `std::recursive_mutex`，最终会导致更昂贵的同步。
- 3. 从用户角度看，`Critical` 使用起来很直观，因为同步只是一个实现细节。

每个接口成员函数都将自己的工作委托给相应的实现成员函数。这种间接层开销是线程安全接口模式的一个典型缺点。

程序的输出展示了三个线程的交错执行。

![](img/d61a6c83410484053b8892275d2fcc4f_499_0.png)

线程安全接口

尽管线程安全接口看起来容易实现，但你必须牢记两个严重的隐患。

#### 9.2.3.1 隐患

在类中使用静态成员或拥有虚接口时需要特别小心。

##### 9.2.3.1.1 静态成员

当你的类有一个非常量静态成员时，你必须同步对类实例的所有成员函数调用。

**带静态成员的线程安全接口**

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
