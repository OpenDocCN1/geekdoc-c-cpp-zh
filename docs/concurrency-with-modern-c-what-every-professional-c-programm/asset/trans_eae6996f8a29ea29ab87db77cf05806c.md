
![](img/d61a6c83410484053b8892275d2fcc4f_475_0.png)

## 涉及引用的数据竞争

我在示例 `copiedValueDataRace.cpp` 中做了一个假设：对于布尔值这是简单的，但对于更复杂的类型则并非如此。如果参数是所谓的值对象，那么按拷贝传递参数就是无数据竞争的。

![](img/d61a6c83410484053b8892275d2fcc4f_475_1.png)

### 值对象

值对象是一种相等性不基于标识、而基于其状态的对象。值对象应是不可变的，这样如果创建时相等，它们在其生命周期内就保持相等。如果按拷贝将值对象传递给线程，则无需同步其访问。根据 Martin Fowler 的文章 ValueObject<sup>2</sup>，你可以想到两类对象：值对象和引用对象。

### 9.1.1.1.1 当引用实际上是拷贝

你可能认为，前面示例 `copiedValueDataRace.cpp` 中的线程 `t3` 可以直接替换为 `std::thread t3(byConstReference, shared)`。程序可以编译并运行，但看起来像引用的东西实际上是拷贝。原因是 `std::decay` 被应用于线程的每个参数。<sup>3</sup> `std::decay` 对其类型 T 执行左值到右值、数组到指针和函数到指针的隐式转换。特别地，在这种情况下，它对类型 T 调用 `std::remove_reference`^1。程序 `perConstReference.cpp` 使用不可拷贝类型 `NonCopyableClass`。

<sup>2</sup>https://martinfowler.com/bliki/ValueObject.html
<sup>3</sup>https://en.cppreference.com/w/cpp/types/decay

### 按引用传递线程参数的隐式拷贝

```cpp
// perConstReference.cpp

#include <thread>

class NonCopyableClass{
  public:

    // the compiler generated default constructor
    NonCopyableClass() = default;

    // disallow copying
    NonCopyableClass& operator = (const NonCopyableClass&) = delete;
    NonCopyableClass (const NonCopyableClass&) = delete;
};

void perConstReference(const NonCopyableClass& nonCopy){}

int main(){

    NonCopyableClass nonCopy;

    perConstReference(nonCopy);

    std::thread t(perConstReference, nonCopy);
    t.join();

}
```

对象 `nonCopy`（第21行）不可拷贝。如果我用参数 `nonCopy` 调用函数 `perConstReference`，这没问题，因为该函数按常量引用接受参数。在线程 t（第25行）中使用同一函数会导致 GCC 6 生成超过300行的冗长编译器错误：

^1 https://en.cppreference.com/w/cpp/types/remove_reference

![](img/d61a6c83410484053b8892275d2fcc4f_477_0.png)

错误消息的关键部分位于截图中间红色圆角矩形内：“error: use of deleted function”。类 NonCopyableClass 的拷贝构造函数不可用。

![](img/d61a6c83410484053b8892275d2fcc4f_477_1.png)

### 9.1.1.2 引用的生命周期问题

如果你的线程按引用使用其参数，并且你分离了线程，就必须极其小心。小程序 copiedValueLifetimeIssues.cpp 具有未定义行为。

### 引用的生命周期问题

```cpp
// copiedValueLifetimeIssues.cpp

#include <iostream>
#include <string>
#include <thread>

void executeTwoThreads(){

    const std::string localString("local string");

    std::thread t1([localString]{
        std::cout << "Per Copy: " << localString << '\n';
    });

    std::thread t2([&localString]{
        std::cout << "Per Reference: " << localString << '\n';
    });

    t1.detach();
    t2.detach();
}

using namespace std::chrono_literals;

int main(){

    std::cout << '\n';

    executeTwoThreads();

    std::this_thread::sleep_for(1s);

    std::cout << '\n';

}
```

executeTwoThreads（第7 - 21行）启动两个线程。两个线程都被分离（第19和20行）并打印局部变量 localString（第9行）。第一个线程按拷贝捕获局部变量，第二个线程按引用捕获局部变量。为简单起见，在两种情况下，我都使用 lambda 表达式绑定参数。

因为 executeTwoThreads 函数不会等到两个线程完成，线程 t2 引用了局部字符串，而该字符串绑定到调用函数的生命周期。这会导致

```cpp
// threadLocalSummation.cpp

...

thread_local unsigned long long tmpSum = 0;

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end) {
  for (auto i = beg; i < end; ++i) {
    tmpSum += val[i];
  }
  sum.fetch_add(tmpSum, std::memory_order_relaxed);
}

...

std::atomic<unsigned long long> sum{};

std::thread t1(sumUp, std::ref(sum), std::ref(randValues), 0, fir);
std::thread t2(sumUp, std::ref(sum), std::ref(randValues), fir, sec);
std::thread t3(sumUp, std::ref(sum), std::ref(randValues), sec, thi);
std::thread t4(sumUp, std::ref(sum), std::ref(randValues), thi, fou);
```

你将基于范围的 for 循环放入函数中，让每个线程在线程局部变量 tmpSum 中计算总和的四分之一。代码行 sum.fetch_add(tmpSum, std::memory_order_relaxed) 最终将原子 sum 中的所有值相加。

我已经在“计算向量元素之和”一章中讨论了汇总所有向量元素的各种方法。你可以在那里研究整个程序。

![](img/d61a6c83410484053b8892275d2fcc4f_480_0.png)

### 使用标准模板库的算法

如果标准模板库的算法可以完成这项工作，就不应编写循环。在这种情况下，std::accumulate 的工作是汇总向量的所有元素：sum = std::accumulate(randValues.begin(), randValues.end(), 0)。自 C++17 起，可以使用 std::reduce 算法，它是 std::accumulate 的可并行化版本：sum = std::reduce(std::execution::par, randValues.begin(), randValues.end(), 0)。

### 9.1.2.1 更多信息

- 面向模式的软件架构：并发与联网对象模式

> ¹https://en.cppreference.com/w/cpp/algorithm/accumulate
> ²https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/

首先，通过锁（例如作用域锁或策略化锁定）保护临界区。在面向对象设计中，临界区通常是一个包含其接口的对象。线程安全接口保护整个对象。如果变量从未被修改，则不需要通过昂贵的锁或原子来进行同步。在这种情况下，只需确保变量以线程安全的方式初始化。我已在上一节线程安全初始化以及关于单例线程安全初始化的案例研究中讨论了几种可能性，包括臭名昭著的双重检查锁定模式。

其次，修改线程只需在其完成工作时发出信号。这是守卫挂起策略。

### 9.2.1 作用域锁定

作用域锁定是将 RAII 应用于互斥量的思想。作用域锁定也称为同步块和守卫。该惯用法的关键思想是将资源获取和释放绑定到对象的生命周期。顾名思义，对象的生命周期是有作用域的。作用域意味着 C++ 运行时负责对象销毁，因此负责释放资源。

类 `ScopedLock` 实现了作用域锁定。

**作用域锁定**

```cpp
// scoped_lock.cpp

#include <iostream>
#include <mutex>
#include <new>
#include <string>

class ScopedLock{
private:
    std::mutex& mut;
public:
    explicit ScopedLock(std::mutex& m): mut(m){
        mut.lock();
        std::cout << "Lock the mutex: " << &mut << '\n';
    }
    ~ScopedLock(){
        std::cout << "Release the mutex: " << &mut << '\n';
        mut.unlock();
    }
};

int main(){

    std::cout << '\n';

    std::mutex mutex1;
    ScopedLock scopedLock1{mutex1};

    std::cout << "\nBefore local scope" << '\n';
    {
        std::mutex mutex2;
        ScopedLock scopedLock2{mutex2};
    }
    std::cout << "After local scope" << '\n';

    std::cout << "\nBefore try-catch block" << '\n';
    try{
        std::mutex mutex3;
        ScopedLock scopedLock3{mutex3};
        throw std::bad_alloc();
    }
    catch (std::bad_alloc& e){
        std::cout << e.what();
    }
    std::cout << "\nAfter try-catch block" << '\n';

    std::cout << '\n';
}
```

ScopedLock 通过引用获取其互斥量（第12行）。互斥量在构造函数中锁定（第13行），并在析构函数中解锁（第18行）。得益于 RAII 惯用法，对象的销毁以及因此互斥量的解锁是自动完成的。

作用域锁定具有以下优缺点。

- 优点：
  - 健壮性，因为锁会自动获取和释放
- 缺点：
  - 对 `std::mutex` 的递归锁定是未定义行为，并且通常可能导致死锁
  - 如果使用 C 函数 `longjmp`^13，锁不会自动释放；`longjmp` 不会调用作用域对象的 C++ 析构函数

^13https://en.cppreference.com/w/cpp/utility/program/longjmp
