
co_yield 直到——在这种情况下——交付了 10 个值。协程终止并被清理（因为 promise_type 是这样决定的）。

## 29.8.3 使用 "promise_type" 的协程

带有 `promise_type` 的返回类型相当复杂。你需要自己编写该类并实现你需要的属性。

你的返回类型必须是一个包含或命名为 `promise_type` 的类。这个 `promise_type` 必须具备以下方法：

- get_return_object()
  此方法在协程启动时被调用。它返回一个合适的 `std::coroutine_handle`。通过它，调用者与协程进行通信。

- initial_suspend()
  如果协程不立即启动，则返回 `suspend_always`，否则返回 `suspend_never`。

- final_suspend()
  包含协程的最终清理操作。返回 `suspend_always` 或 `suspend_never`。

- unhandled_exception()
  当协程中发生异常时调用。它可以处理该异常或将其重新抛出。

最简单的实现之一如下所示：

```cpp
// https://godbolt.org/z/8enx43Ksb
#include <coroutine>
#include <iostream>
struct Routine { // 协程返回类型
    struct promise_type: // 先定义的返回类型
        Routine(auto h) : hdl(h) {} // 构造函数
        ~Routine() { if (hdl_) hdl_.destroy(); } // 析构函数
        Routine(const Routine&) = delete; // 禁止拷贝
        Routine(const Routine&) = delete; // 禁止移动
        // 给调用者的接口：
        bool more() {
            if(hdl_ || hdl_.done()) return false; // 没有更多事要做了
            hdl_.resume(); // 阻塞调用
            return !hdl_.done(); // 信号完成或未完成
        }
    private:
        using handle_type = std::coroutine_handle<promise_type>;
        handle_type hdl_; // 控制协程
    };
    struct promise_type { // 必要的 promise 类型
        auto get_return_object() { // 初始化句柄
            return Routine{handle_type::from_promise(*this)};
        }
        auto initial_suspend() { return std::suspend_never{}; } // 立即启动
        auto final_suspend() noexcept { return std::suspend_always{}; } // 协程没有恢复操作；
        正常情况
        void unhandled_exception() {} // 无异常处理
        void return_void() {} // 无返回
    };
    Routine counter() { // 返回类型是我们的包装类，带有
        promise_type promise;
        for (unsigned i = 0; i; ++i) {
            co_await std::suspend_always{}; // 挂起协程
            std::cout << "counter: " << i << std::endl;
        }
    }

int main() {
    Routine routine = counter(); // 创建并启动协程
    for (int i = 0; i < 3; ++i) {
        std::cout << "Hello main!\n";
        routine.more(); // 继续协程
    }
}
```

**列表 24.43** 一个带有其 "promise-type" 的协程返回类型的简单示例。

`Routine` 类是 `coroutine_handle` 的包装器。它还包含了 `promise_type`，它描述了协程的行为。在 `get_return_object()` 中，句柄被初始化并返回给调用者。其他方法都是平凡的。

调用者在启动时接收来自 `get_return_object()` 的返回值。这本质上是返回类型的工厂方法。`Routine` 的构造函数接收句柄并将其存储，以便稍后与协程通信。析构函数在句柄仍然存在时对句柄调用 `destroy()`。在这里，情况总是如此，但有了移动语义，这可能会变得重要，因为句柄也可以为空。

通过对句柄调用 `resume()` 并调用 `more()` 来恢复协程。顺便说，`hdl_` 达到相同的效果。在此之前，我们通过 `!hdl_` 检查是否存在句柄。通过 `hdl_.done()` 检查协程是否已经完成。在我们特定的协程中，这种情况从未发生，但一般情况下它可能会发生。返回值直接从 `hdl_.done()` 传递，并向调用者信号协程是否可以继续运行。

通过 `initial_suspend()` 的返回值，你决定协程是在创建时立即开始运行还是否。使用 `suspend_never`，它不会立即启动（懒性）；使用 `suspend_always`，它将立即启动（激进）。

`final_suspend()` 的返回值决定协程寿命结束时发生什么。在这里，`suspend_always` 是正常情况。

真正有趣的定义是协程 `counter()`。它的返回类型是 `Routine`，即包装器。它通过调用 `co_await suspend_always{}` 挂起三次。这样，程序控制权返回给调用者。调用者随后继续循环并调用 `more()`。这导致协程恢复直到下一次 `co_await`。

### Awaiter 和 Awaitable
挂起和类型是所谓的 awaitables（可等待对象）。它们是最简单的 awaitables，并由库提供。这些类是编译器期望你实现 `await_ready()`、`await_suspend()` 和 `await_resume()` 方法的类。

挂起和类型是所谓的 awaitables。它们是最简单的 awaitables，并由库提供。这些类是编译器期望你实现 `await_ready()`、`await_suspend()` 和 `await_resume()` 方法的类。

挂起和类型是所谓的 awaitables。它们是最简单的 awaitables，并由库提供。这些类是编译器期望你实现 `await_ready()`、`await_suspend()` 和 `await_resume()` 方法的类。

挂起和类型是所谓的 awaitables。它们是最简单的 awaitables，并由库提供。这些类是编译器期望你实现 `await_ready()`、`await_suspend()` 和 `await_resume()` 方法的类。

挂起和类型是所谓的 awaitables。它们是最简单的 awaitables，并由库提供。这些类是编译器期望你实现 `await_ready()`、`await_suspend()` 和 `await_resume()` 方法的类。

（注：原文中存在大量重复段落，已根据要求保留逻辑并进行翻译）
