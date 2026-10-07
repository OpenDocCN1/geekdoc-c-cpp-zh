

## 7.5 原子操作与内存模型 第 07 章 并行与并发

4. **最终一致性 (Final Consistency)**：这是最弱的一致性要求。它只保证操作会在未来的某个点被观察到，但并不要求观测到的时间。因此我们甚至可以稍微加强这一条件，例如指定操作的观测时间始终是有界的。当然，这就不属于我们的讨论范围了。

```
x.store(3)   x.store(4)
T1--------------------------------------------------------------------->
T2--------------------------------------------------------------------->
x.read()      x.read()      x.read()      x.read()
```

在上述情况下，如果我们假设 x 的初始值为 0，那么 T2 中的四个 'x.read()' 可能不限于以下结果：

```
3 4 4 4 // x 的写入操作被迅速观察到
0 3 3 4 // x 写入操作的观测时间存在延迟
0 0 0 4 // 最后一次读取了 x 的最终值，但之前的更改没有被观察到。
0 0 0 0 // 当前时间内没有观察到 x 的写入操作，但情况
```

## 内存顺序 (Memory Orders)

为了实现极致性能并满足不同强度的一致性要求，C++11 为原子操作定义了六种不同的内存序列。std::memory_order 指定了多个线程之间的同步模型：

1. **宽松模型 (Relaxed model)**：在此模型下，单线程内的原子操作按顺序执行的，不允许指令排序，但线程之间的原子操作顺序是任意的。该类型由 `std::memory_order_relaxed` 指定。让我们来看一个例子：

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

2. **释放/消费模型 (Release/consumption model)**：在此模型中，我们开始限制进程之间的操作顺序。如果一个线程需要修改一个值，但另一个线程对该值的操作有依赖，即后者依赖于前者。具体来说，A 对 x 完成了三次写入，而 B 仅在第三次写入操作时释放，无论 x 的前两次写入如何，当 A 调用 `x.release()`（即使用 `std::memory_order_release`）时，`std::memory_order_consume` 选项确保 B 在调用 `x.load()` 时观察到对 x 的三次写入。让我们来看一个例子：

```cpp
// 初始化为 nullptr 以防止消费者加载悬空指针
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

3. **释放/获取模型 (Release/Acquire model)**：在此模型下，我们可以进一步收紧不同线程之间原子操作的顺序，特别是指定释放 `std::memory_order_acquire` 和获取 `std::memory_order_acquire` 之间的时机。释放操作之前的所有写入对任何其他线程可见，即发生于（happens-before）。

如你所见，`std::memory_order_release` 确保写入行为发生在释放操作之前，这是一个前向屏障；`std::memory_order_acquire` 确保之前的写入发生在获取操作之后，这是一个后向屏障。对于 `std::memory_order_acq_rel` 选项，它结合了二者的特征定义了一个内存屏障，使得当前线程的读写在该操作前后不会重排。让我们来看一个例子：

```cpp
std::vector<int> v;
std::atomic<int> flag = {0};
std::thread release([&]() {
    v.push_back(42);
    flag.store(1, std::memory_order_release);
});

std::thread acquire([&]() {
    int expected = 1; // 必须使用 compare_exchange_strong
    while (!flag.compare_exchange_strong(expected, 2, std::memory_order_acq_rel)) {
        expected = 1; // 必须使用 compare_exchange_strong
    }
    // flag 已经变为 2
    while (flag.load(std::memory_order_acquire) == 2) {
        std::cout << v[0] << std::endl; // 必须是 42
    }
});
release.join();
acquire.join();
```

在这种情况下使用 `compare_exchange_strong`，它是一种比较交换原语；较弱的版本 `compare_exchange_weak` 允许在失败时返回失败，是因为在某些平台上当 CPU 执行上下文切换时会产生不一致。此外，`compare_exchange_strong` 的性能可能略低于 `compare_exchange_weak`，但在大多数情况下应该使用 `compare_exchange_strong`。

4. **顺序一致性模型 (Sequential Consistent Model)**：在此模型下，原子操作满足一致性，可以通过 `std::memory_order_seq_cst` 显式指定。让我们来看一个简单的示例：

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

这个示例与第一个相同，只需将原子操作的内存顺序改为 `memory_order_seq_cst`。感兴趣的读者可以编写自己的程序来测量这些内存序列带来的性能差异。

## 总结

C++11 语言为并发提供了支持。本节介绍了 `std::thread`/`std::mutex`/`std::future` 等并发编程中不可避免的工具。此外，我们还引入了内存模型，作为 C++11 最重要的特性之一。它们为 C++ 的高性能计算提供了关键基础。

## 练习

- 1. 编写一个简单的线程池，提供以下功能：

```cpp
ThreadPool p(4); // 指定工作线程

// 提交任务并返回一个 std::future
auto f = pool.enqueue([](int life) {
    return life;
}, 42);

// 从 future 获取结果
std::cout << f.get() << std::endl;
```

- 2. 使用 `std::atomic<bool>` 实现互斥锁。

## 扩展阅读

- C++
- Thread document
- Herlihy, M. P., & Wing, J. M. (1990). Linearizability: a correctness condition for concurrent objects. ACM Transactions on Programming Languages and Systems, 12(3), 463–492. https://doi.org/10.1145/78969.78972

## 第08 章 文件系统

文件系统库提供了与文件系统、路径、文件、目录操作相关的函数。与正则表达式库类似，它是 boost 发布并最终合并到 C++ 标准的库之一。

### 8.1 文档与链接

TODO

### 8.2 std::filesystem

TODO

## 第 09 章次要特性

### 9.1 新类型

**long long int**

`long long int` 并不是 C++11 引入的。事实上，早在 C99，`long long int` 就已经包含在 C 标准中了，因此大多数编译器已经支持了它。C++11 正式将其纳入标准库，规定 `long long int` 类型至少为 64 位。

### 9.2 noexcept 及其操作

C++ 相比 C 的一个大优势是 C++ 自身定义了一套完整的异常处理机制。但在 C++11 之前，几乎没有人会在函数名后编写异常声明。从 C++11 开始，这种机制被弃用了，因此我们不会讨论或介绍以前的机制。关于它如何工作以及如何使用，你不必主动去理解它。

C++11 将异常声明简化为两种情况：

- 1. 函数可能会抛出任何异常
- 2. 函数不能抛出任何异常

并使用 `noexcept` 来限制这两种行为，例如：

```cpp
void may_throw();      // 可能抛出任何异常
void no_throw() noexcept; // 不能抛出任何异常
```

如果函数被修改为 `noexcept`，编译器将使用 `std::terminate()` 立即终止程序。

`noexcept` 也可以作为运算符来操作表达式。当表达式没有异常抛出时，它返回 true，否则返回 false。

```cpp
#include <iostream>
void may_throw() {
    throw;
}
```

