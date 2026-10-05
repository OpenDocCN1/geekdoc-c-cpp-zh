

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

29.2. 互斥锁（Mutex）代表互斥。你对想要防止并发访问的资源使用互斥锁：无论有多少个线程，资源都拥有一个互斥锁。

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

