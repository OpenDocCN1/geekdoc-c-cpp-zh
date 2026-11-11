

```text
Before jobs
    Job prepared
        MySuspendAlways::await_ready
        MySuspendAlways::await_suspend
        MySuspendAlways::await_resume
    Job finished
    Job prepared
        MySuspendAlways::await_ready
        MySuspendAlways::await_resume
    Job finished
    Job prepared
        MySuspendAlways::await_ready
        MySuspendAlways::await_resume
    Job finished
    Job prepared
        MySuspendAlways::await_ready
        MySuspendAlways::await_resume
    Job finished
After jobs
```

自动恢复等待器

### 6.8.3 在独立线程上自动恢复等待器

让我进一步改进所展示的程序，并在独立线程上恢复等待器。

下面的程序基于前一个程序。

**在独立线程上自动恢复等待器**

```cpp
// startJobWithAutomaticResumptionOnThread.cpp

#include <coroutine>
#include <functional>
#include <iostream>
#include <random>
#include <thread>
#include <vector>

std::random_device seed;
auto gen = std::bind_front(std::uniform_int_distribution<>{0,1},
                          std::default_random_engine(seed()));

struct MyAwaitable {
    std::jthread outerThread;
    bool await_ready() const noexcept {
        auto res = gen();
        if (res) std::cout << " (executed)" << '\n';
        else std::cout << " (suspended)" << '\n';
        return res;
    }
    void await_suspend(std::coroutine_handle<> h) {
        outerThread = std::jthread([h] { h.resume(); });
    }
    void await_resume() { }
};

struct Job{
    static inline int JobCounter{1};
    Job() {
        ++JobCounter;
    }

    struct promise_type {
        int JobNumber {JobCounter};
        Job get_return_object() { return {}; }
        std::suspend_never initial_suspend() {
            std::cout << " Job " << JobNumber << " prepared on thread "
                      << std::this_thread::get_id();
            return {};
        }
        std::suspend_never final_suspend() noexcept {
            std::cout << " Job " << JobNumber << " finished on thread "
                      << std::this_thread::get_id() << '\n';
            return {};
        }
        void return_void() { }
        void unhandled_exception() { }
    };
};

Job performJob(std::jthread& out) {
    co_await MyAwaitable{out};
}

int main() {
    std::vector<std::thread> threads(8);
    for (auto& thr: threads) performJob(thr);
}
```

与上一个程序的主要区别是新的可等待对象 `MyAwaitable`，它在协程 `performJob`（第 54 行）中使用。相反，从协程 `performJob` 返回的协程对象则很直接。本质上，其成员函数 `initial_suspend`（第 38 行）和 `final_suspend`（第 43 行）返回预定义的可等待对象 `std::suspend_never`。此外，这两个函数都会显示所执行作业的 `JobNumber` 以及它运行所在的线程 ID。截图显示了哪些协程立即运行，哪些协程被挂起。借助线程 ID，你可以观察到被挂起的协程会在不同的线程上恢复。

你可以在 [Wandbox](https://wandbox.org/permlink/skHgWKF0SYAwp8Dm) 上试用该程序。

![](img/d61a6c83410484053b8892275d2fcc4f_426_0.png)

让我讨论一下这个程序有趣的控制流。第 59 行创建了八个默认构造的线程，协程 `performJob`（第 53 行）以引用方式接收它们。此外，该引用成为创建 `MyAwaitable{out}`（第 54 行）的参数。根据 `res`（第 17 行）的值，也就是函数 `await_ready` 的返回值，可等待对象会继续运行（res 为 true）或被挂起（res 为 false）。如果 `MyAwaitable` 被挂起，就会执行函数 `await_suspend`（第 22 行）。由于对 `outerThread` 的赋值（第 23 行），它成为一个正在运行的线程。正在运行的线程必须比协程的生命周期更长。因此，这些线程具有主函数的作用域。

² https://wandbox.org/permlink/skHgWKF0SYAwp8Dm

![](img/d61a6c83410484053b8892275d2fcc4f_427_0.png)

## 提炼信息

- 计算向量之和可以通过多种方式完成。你可以顺序执行，也可以并发执行，并在最大程度和最小程度上共享数据。性能数值差异巨大。
- 单例的线程安全初始化是共享变量线程安全初始化的经典用例。实现方式有很多，性能特征各不相同。
- 我从小程序开始，通过弱化内存序逐步改进它。我用 CppMem 验证持续优化过程中的每一步。CppMem 是一个交互式工具，用于探索使用 C++ 内存模型的小代码片段的行为。
- 在 C++20 中有很多同步线程的方法。你可以使用条件变量、`std::atomic_flag`、`std::atomic<bool>` 或信号量。我讨论了各种乒乓游戏的性能数值。
- 借助新关键字 `co_return`，我可以在 futures 的变体一节中实现急切 future、惰性 future，或在独立线程中运行的 future。大量使用的注释使其工作流程清晰透明。
- `co_yield` 使其能够创建无限数据流。在生成器的修改与泛化案例研究中，无限数据流变得有限且通用。
- 各种作业工作流的案例研究展示了几个在必要时自动恢复的协程。`co_await` 使之成为可能。

## 7. 未来：C++23

![](img/d61a6c83410484053b8892275d2fcc4f_428_0.png)

Cippi 预测未来

本章讨论 C++ 的未来：C++23。在本章中，我不打算像本书其他章节那样精确。原因有两个。首先，并非所有介绍的特性都会进入 C++23 标准。其次，如果某个特性进入 C++23 标准，该特性的接口很可能会发生变化。这对执行器尤其如此。我会定期更新本书，因此本章会反映修订后的提案和新提案。

本章的目标很简单：让你了解 C++23 中即将到来的并发特性。

![](img/d61a6c83410484053b8892275d2fcc4f_429_0.png)

- 内存模型
- 原子操作
- 线程
- 互斥量与锁
- 线程局部数据
- 条件变量
- 任务
- 读写锁
- 并行 STL
- 原子智能指针
- std::jthread
- 闩锁与屏障
- 信号量
- 协程
- 执行器
- 有栈协程扩展
- 事务内存
- 任务块
- 数据并行向量库

C++23 中的并发

### 7.1 执行器

执行器是 C++ 中执行的基本构建块，并且为执行扮演着类似的角色，就像分配器之于 C++ 容器。诸如 `async`、标准模板库的并行算法、future 的 `then` 续接、任务块的 `run` 成员函数，或 Networking TS 的 `post`、`dispatch` 或 `defer` 调用等函数都会使用它们。此外，执行是编程的一个基本关注点。目前还没有标准化的执行方式。

下面是提案 P0761² 的入门示例。

**各种 `parallel_for` 实现**

```cpp
void parallel_for(int facility, int n, function<void(int)> f) {
  if(facility == OPENMP) {
    #pragma omp parallel for
    for(int i = 0; i < n; ++i) {
      f(i);
    }
  }
  else if(facility == GPU) {
    parallel_for_gpu_kernel<<<n>>>(f);
  }
  else if(facility == THREAD_POOL) {
    global_thread_pool_variable.submit(n, f);
  }
}
```

这个 `parallel_for` 函数有几个问题。

- 像 `parallel_for` 这样简单的函数维护起来却很**复杂**。如果要支持新算法或新的并行范式，复杂性会变得越来越糟。
- 函数的每个分支都有不同的**同步**属性。OpenMP¹ 可能会阻塞，直到所有派生线程完成；GPU 通常异步运行；线程池可能会阻塞，也可能不会。同步不足可能导致数据竞争或死锁。最好的情况下，你会遇到竞态条件。
- `parallel_for` 循环过于**受限**。例如，无法在该函数中使用你自己的线程池来代替全局线程池：`global_thread_pool_variable.submit(n, f);`。

¹ https://en.cppreference.com/w/cpp/experimental
² https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0761r2.pdf
³ https://en.wikipedia.org/wiki/OpenMP

