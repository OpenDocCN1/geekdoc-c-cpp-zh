
#include <thread>

#include <latch>

#include <iostream>

int count = 0; // 同时被修改

void run() {

    for(int i=0; i<1000; ++i) { // 修正此处示例逻辑以匹配

        count += 1; // 未受保护

    }

}
```
```cpp

int main() {

    std::latch la(3); // 我们期望 3 个线程

    std::thread th1 [&la]{ fib(39); la.count(); };

    std::thread th2 [&la]{ fib(38); la.count(); };

    std::thread th3 [&la]{ fib(40); la.count(); };

    std::cout << "Main thread: done\n";

    la.wait(); // 等待 la == 0

    std::cout << "Rest done\n"

}
```

```
// https://gdbbolt.org/z/515dMo9Kx
#include <thread>
#include <barrier>
#include <iostream>
#include <vector>
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); };
constexpr int anz = 8;           // 8 个线程
constexpr int max = 32;         // 计算到 32
std::vector<long> results(anz); // 缓冲区：8个结果的空间

void output() {
    // 信号函数指向缓冲区
    for (auto &n : results) std::cout << n << ' ';
    std::cout << '\n';
}

std::barrier ba(anz, output); // 在 8 个线程后总是输出

void worker(std::stop_token st, int idx) {
    // n = 0, 9, 17, 25, ... 1, 10, 18, 26, ...
    for(int n=idx; n<max; n+=anz) {
        if(st.stop_requested()) return;
        results[idx] = fib(n); // 将结果写入缓冲区
        ba.arrive_and_wait(); // 等待 8 个线程都到达
    }
}

int main() {
    std::vector<std::thread> threads; // 8 个线程
    for (int idx=0; idx<anz; ++idx) {
        threads.emplace_back(worker, idx); // 创建带索引的线程
    }
    for (auto &t : threads) t.join(); // 等待所有线程完成
}
```

**Listing 29.16** 屏障（barrier）等待特定数量的线程。

每个工作线程函数以 8 为步长计算斐波那契数，并将结果写入其对应的位置——因此线程之间不会互相互干扰。`output` 函数输出所有结果。这恰好发生在 worker 中的八个线程到达 `arrive_and_wait()` 调用时。

输出为：

0 1 2 3 5 8 13

21 34 55 89 144 233 377 610

987 1597 2584 4181 6765 10946 17711 28657

因此， 斐波那契数是并行计算的。输出总在八个线程完成时发生。

其他可能有用的方法如下：

- `arrive()`：为另一个线程提供令牌 `t`，该线程可以调用 `wait(t)`。

- `wait()`：等待由 `arrive()` 生成的令牌。

- `arrive_and_wait()`：等同于 `ba.wait(ba.arrive())`。

- `arrive_drop()`：永久减少计数器但不等待。

>

在考虑互斥锁（mutex）之前，你应该首先考虑使用未来（futures），因为它们是配合 `async` 或 `jthread` 的轻量级替代方案。

### 29.2. 互斥锁（Mutex）代表互斥

你对想要防止并发访问的资源使用互斥锁：无论有多少个线程，资源都拥有一个互斥锁。

在每个线程中，使用资源之前会锁定该互斥锁。如果另一个线程想要使用同一个互斥锁，它尝试锁定时会失败，第二个线程可以等待或放弃使用资源。

一旦第一个线程完成它的事务，它会解锁互斥锁。通过这种方式，线程通过互斥锁协调工作，互斥地访问关键资源。

# 信号量（Semaphore）是互斥锁的特殊情况

信号量允许固定数量的线程同时使用资源。互斥锁是限制为一的信号量：最多有一个线程可以使用资源。

在 C++20 中，新增了 `counting_semaphore` 和 `binary_semaphore` 类。从某种意义上说，它们是互斥锁的替代替代方案。你不使用锁（即不使用 RAII），而是手动调用 `acquire` 和 `release`。另一个区别是，信号量不取决于由哪个线程释放，而互斥锁必须由原始线程释放。

这在 C++ 实践中是什么样的？你使用属于资源的互斥锁实例，并在线程中对其锁定和解锁。

使用 `lock_guard` 类，你无法忘记解锁互斥锁，因为析构函数处理了这一点，遵循 RAII 原则。因此，`lock_guard` 实例初始化后的作用范围是被保护的。

对于特殊任务，有互斥锁和 `lock_guard` 的合适替代，我稍后会讨论。

下面的列表显示了基础工具的典型且简单的用法。

```cpp
// https://godbolt.org/z/3fz5a4v
#include <mutex> // mut斥锁
#include <list>
#include <algorithm>
using std::mutex;
using std::lock_guard;

class MxList {
    std::list<int> data;
    mutable mutex mx;
public:
    void add(int value) {
        lock_guard<mutex> lock(mx);
        data.push_back(value);
    }
    bool contains(int searchVal) const {
        lock_guard<mutex> lock(mx);
        return std::find(data.begin(), data.end(), searchVal) != data.end();
    }
};
```

**Listing 29.17** 用于保护列表的互斥锁。

由于资源在线程之间共享，它必须被保护。在上面的示例中，`lock_guard` 确保一次时间只有一个线程可以访问 `data` 列表。

# 关键区域（Critical Section）

关键区域是访问被多个线程使用的共享资源的代码部分。为了防止竞态条件，这些区域必须由互斥锁保护。

```cpp
// 关键区域示例
{
    lock_guard<mutex> lock(mtx);
    // 访问共享资源
}
```

被互斥锁保护的代码块被称为关键区域。它确保一次只有一个线程可以执行该块，从而防止数据损坏。

# 可变互斥锁？

标记为 `const` 的方法不应该修改对象的状态。然而，互斥锁在锁定时必须被。为了在 `const` 方法中允许这一点，互斥锁被声明为 `mutable`。

```cpp
class MyClass {
    int data;
    mutable mutex mx;
public:
    int getValue() const {
        lock_guard<mutex> lock(mx);
        return data;
    }
};
```

在这里我向你展示 `mutable` 的罕见的有意义用法之一。

# 多线程简单的接口设计

这里的栈（stack）意味着我想从顶部添加和删除元素，并知道栈是否包含元素。在列表 29.18 中，我向你展示了公共部分和方法声明，而不是定义。你应该注意到该类在并行使用时会遇到困难，并且它并不是本质上安全的。这里的问题是你无法在并行操作中依赖 `isEmpty()` 的结果。虽然函数在调用时安全地返回了正确的结果，但一旦它退出，其他线程就可以调用 `push()` 或 `pop()` 了。

考虑以下列表。

```cpp
// https://godbolt.org/z/4j7njd763
#include <vector>

template<class T>
class MxStack {
public:
    bool isEmpty() const;
    void push(const T&);
    void pop();
    const T& top() const;
};
```

**Listing 29.18** 多线程栈的接口。

```
// ...
if( mxs.isEmpty()) { // 不安全
    const auto value = mxs.top(); // 不安全
    mxs.pop(); // 不安全
    // ...
    // 更多代码
    // ...
}
```

# 列表 29.19 “MxStack”的有问题的代码。

这里有两种可能的数据竞态，第一个发生在 `isEmpty()` 和 `mx.top()` 的调用之间。假设栈 `mxs` 持有一个元素 `{3}`，且一个线程到达 `!isEmpty()`。由于 `!isEmpty` 为真，进入了 then 分支。但此时，另一个线程正在执行前面的代码并执行了 `mx.pop()`——最后一个元素被删除了！继续执行第一个线程，它现在在 `if` 语句中的空栈上执行 `top()`。这突然无法工作了，尽管 `!isEmpty()` 刚刚确保容器容器为空。这是一个棘手的陷阱。

第二个数据竞态检测起来稍微复杂一点；它发生在 `top()` 和 `pop` 之间。[ 84 ] 我将让之前代码中两个线程的执行过程更清晰一些。时间线从上到下运行，线程并排显示。

```
/* Thread 1 */                /* Thread 2 */
if(! mxs.isEmpty()) {
    if(! mxs.isEmpty()) {
        const auto value = mxs.top();
        const auto value = mxs.top();
    mxs.pop();
    // ... 更多代码
```

# 列表 29.20 线程执行之前代码的一种可能。

假设我们从栈 `mxs={1,2,3}` 开始。那么在前两行中，两个线程都正确地判断栈不为空。然而，使用 `top()` 从栈中获取顶部元素 3。随后两个栈都执行了 `pop()`，不仅删除了 3，还删除了 2。结果是 3 被处理了两次，而 2 完全没有被考虑。

即使我已经在内部使用互斥锁很好地保护了 `MxStack` 以防止不一致的操作，但 `MxStack` 接口的整体使用对于并行操作仍然是不够的。

解决方案在于改变接口：它必须确保典型操作是一致的。这意味着在很大程度上取决于应用程序。如果不确定，你应该提供一个精简的接口，不要被不必要的方法过度负载。这使得用户更容易从接口规范中识别正确的操作。

一个解决我们问题的示例包含接口的更改：

- `top()` 和 `pop()` 必须合并为单个调用。

- 单独的 `isEmpty()` 是安全的，必须由 `pop()` 可能抛出的异常来进行补充。

# 一个带有实现的简单接口可能如下所示。

```
// https://cppgodbolt.org/vcb9gPBjK
#include<vector>
#include<thread>
#include<mutex>
#include<iostream>
#include<numeric> // iota
#include<concepts> // copyable

/* T: noexcept copyable and assignable */
template<std::copyable T>
class MxStack {
    std::vector<T> data_;
    std::mutex mx_;
public:
    MxStack() : data_() {}

    bool isEmpty() const { return data_.empty(); }

    void push(const T& val) {
        std::lock_guard<std::mutex> g(mx_);
        data_.push_back(val);
    }

    T pop() {
        std::lock_guard g(mx_);
        if(data_.empty()) {
            throw std::length_error("empty stack");
        }
        T tmp(std::move(data_.back()));
        data_.pop_back();
        return tmp;
    }
};

int main() {
    // 准备栈
    MxStack<int> mx;
    for(int i=1; i<=1000000; ++i) mx.push(i);
    // 定义计算
    auto sumIt = [&mx](long &sum) {
        int val();
        try {
            while (! mx.isEmpty()) {
                sum += mx.pop(); // 可能仍抛出异常
            }
        } catch(std::length_error &ex) {
    }
}
```

```
// 计算
// 用于部分结果
long sum1 = 0;
std::jthread th1(sumIt, std::ref(sum1));
long sum2 = 0; // 用于部分结果
std::thread th2(sumIt, std::ref(sum2));
th1.join(); th2.join();
long Sum = sum1 + sum2; // 结果结果
// 结果
std::cout << "Expected result:
  << (1'0000'001L*1'0000'001)/2 << '\n'; // 输出: 500000500000
std::cout << "Actual:
  // 输出: 500000500000
  << sum << '\n';
```

# 列表 29.21 一个非常简单的线程安全栈。

关于并发性，可以这样说：

- `push` 和 `pop` 都分别由同一个互斥锁的 `lock_guard` 保护，因此它们之间互不干扰。

- `isEmpty` 不需要保护。

- 如果容器为空，`pop` 可能会抛出异常。

## 29.2.6 锁可能导致死锁

在互斥锁上使用多个锁可能会导致死锁。例如，如果一个方法调用另一个方法并尝试锁定，那么第二个调用将永远等待下去。在伪代码中，它看起来像：

```
class MxStack {
  bool isEmpty() const {
    std::lock_guard<std::mutex> g(mx);
    return data_.empty();
  }
  void top() {
    std::lock_guard<std::mutex> g(mx);
    if(!data_.isEmpty()) // 在  锁定
  }
};
```

当不同线程中的两个操作 `a` 和 `b` 需要锁定两个互斥锁 `mx` 和 `my` 时，也会出现类似的情况。再次使用伪代码：

```
Thread 1:
  operation a():
    mx.lock();
    my.lock();
    /* 执行 a... */

Thread 2:
  operation b():
    my.lock();
    mx.lock();
    /* 执行 b... */
```

在这种情况下，线程 1 等待 `my` 释放，线程 2 等待 `mx` 释放。两者都不会发生，因为每个线程都在等待——死锁。

## 始终以相同的顺序锁定多个互斥锁

如果多个操作都都需要锁定多个互斥锁，应该以相同的顺序进行。至少对于简单场景，可以排除死锁的可能性。

标准库提供了一种同时锁定多个互斥锁的方法，这消除了这些场景下死锁的风险。一个典型的示例是大数据结构的 `swap` 方法，每个实例都由它自己的互斥锁保护，例如列表 29.21 中的 `MxStack`。在下一个列表中，你将看到一个详细交换实现的示例。

```
// https://github.com/z/9PMzc1qP
friend void swap(MxStack& re, MxStack& li) {
    if(&re==li) return; // 同地址？自交换没有必要
    std::lock(re.mx_, li.mx_); // 同时锁定多个
    std::lock_guard lk1(re.mx_, std::adopt_lock); // 已锁定
    std::lock_guard lk2(li.mx_, std::adopt_lock); // 已锁定
    std::swap(li.data_, re.data_); // 执行交换
}
```
