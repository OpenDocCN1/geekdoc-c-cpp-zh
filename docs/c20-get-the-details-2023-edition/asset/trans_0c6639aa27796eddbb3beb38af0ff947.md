

```cpp
void return_void() { }
void unhandled_exception() { }

};
};

Job prepareJob() {
    co_await MySuspendNever();
}

int main() {

    std::cout << "Before job" << '\n';

    auto job = prepareJob();
    job.start();

    std::cout << "After job" << '\n';
}
```

首先，我将预定义的 awaitable `std::suspend_always` 和 `std::suspend_never` 替换为 awaitable MySuspendAlways（第 6 行）和 MySuspendNever（第 20 行）。我在第 51、55 和 66 行使用它们。这些 awaitable 模仿预定义 awaitable 的行为，但额外写入一条注释。由于使用了 `std::cout`，成员函数 await_ready、await_suspend 和 await_resume 不能声明为 constexpr。

程序执行的截图很好地展示了控制流，你可以直接在 [Compiler Explorer] 上观察。

⁷https://godbolt.org/z/T5rcE4

```text
Before job
    Job prepared
        MySuspendAlways::await_ready
        MySuspendAlways::await_suspend
        MySuspendAlways::await_resume
        MySuspendNever::await_ready
        MySuspendNever::await_resume
    Job finished
        MySuspendAlways::await_ready
        MySuspendAlways::await_suspend
After job
```

按请求启动任务（包括注释）

函数 `initial_suspend`（第 51 行）在协程开始时执行，函数 `final_suspend` 在其结束时执行（第 55 行）。调用 `prepareJob()`（第 73 行）会触发协程对象的创建，而函数调用 `job.start()` 是恢复，因此也是完成（第 74 行）。于是，MySuspendAlways 的成员 await_ready、await_suspend 和 await_resume 会执行。当你没有恢复 awaitable（例如由成员函数 final_suspend 返回的协程对象）时，函数 await_resume 不会被处理。相反，awaitable 的 MySuspendNever 函数会立即就绪，因为 await_ready 返回 true，因此不会挂起。

借助这些注释，你应该对 [awaiter 工作流](#) 有了初步理解。现在，是时候对它做些变化了。

## 7.4.2 自动恢复 Awaiter

在前面的工作流中，我显式启动了任务。

显式启动任务

```cpp
int main() {

    std::cout << "Before job" << '\n';

    auto job = prepareJob();
    job.start();

    std::cout << "After job" << '\n';

}
```

显式调用 `job.start()` 是必要的，因为 awaitable MySuspendAlways 中的 `await_ready` 总是返回 false。现在假设 `await_ready` 可以返回 true 或 false，并且任务不会被显式启动。简短提醒：当 `await_ready` 返回 true 时，会直接调用函数 `await_resume`，而不会调用 `await_suspend`。

### 自动恢复 Awaiter

```cpp
// startJobWithAutomaticResumption.cpp

#include <coroutine>
#include <functional>
#include <iostream>
#include <random>

std::random_device seed;
auto gen = std::bind_front(std::uniform_int_distribution<>(0,1),
                           std::default_random_engine(seed()));

struct MySuspendAlways {
    bool await_ready() const noexcept {
        std::cout << "MySuspendAlways::await_ready" << '\n';
        return gen();
    }
    bool await_suspend(std::coroutine_handle<> handle) const noexcept {
        std::cout << "MySuspendAlways::await_suspend" << '\n';
        handle.resume();
        return true;
    }

    void await_resume() const noexcept {
        std::cout << "MySuspendAlways::await_resume" << '\n';
    }
};

struct Job {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;
    handle_type coro;
    Job(handle_type h): coro(h){}
    ~Job() {
        if ( coro ) coro.destroy();
    }

    struct promise_type {
        auto get_return_object() {
            return Job{handle_type::from_promise(*this)};
        }
        MySuspendAlways initial_suspend() {
            std::cout << "Job prepared" << '\n';
            return {};
        }

        std::suspend_always final_suspend() noexcept {
            std::cout << "Job finished" << '\n';
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}

    };
};

Job performJob() {
    co_await std::suspend_never();
}

int main() {
    std::cout << "Before jobs" << '\n';

    performJob();
    performJob();
    performJob();
    performJob();

    std::cout << "After jobs" << '\n';
}
```

首先，协程现在名为 performJob 并自动运行。gen（第 9 行）是一个生成数字 0 或 1 的随机数生成器。它使用默认随机引擎来完成工作，该引擎用 seed 初始化。借助 `std::bind_front`，我可以将它和 `std::uniform_int_distribution` 绑定在一起，得到一个可调用对象，使用时给我一个 0 或 1 的随机数。

在这个示例中，我移除了 C++ 标准中预定义的 awaitable，只保留了 awaitable mySuspendAlways 作为成员函数 initial_suspend 的返回类型（第 41 行）。`await_ready`（第 13 行）返回一个布尔值。如果该布尔值为 true，控制流直接跳到 `await_resume` 成员函数（第 23 行）；如果为 false，协程立即挂起，并执行函数 `await_suspend`（第 17 行）。函数 `await_suspend` 获得协程的句柄，并用它恢复协程（第 19 行）。`await_suspend` 也可以返回 void，而不是返回值 true。

下面的截图显示：当 `await_ready` 返回 true 时，会调用函数 `await_resume`；当 `await_ready` 返回 false 时，也会调用函数 `await_suspend`。

你可以在 Compiler Explorer<sup>8</sup> 上试用该程序。

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

**自动恢复 Awaiter**

让我进一步改进所展示的程序，并在单独的线程上恢复 awaiter。

## 7.4.3 在单独线程上自动恢复 Awaiter

下面的程序基于前一个程序。

### 在单独线程上自动恢复 Awaiter

```cpp
// startJobWithAutomaticResumptionOnThread.cpp

#include <coroutine>
#include <functional>
#include <iostream>
#include <random>
#include <thread>
#include <vector>

std::random_device seed;
auto gen = std::bind_front(std::uniform_int_distribution<>(0,1),
                        std::default_random_engine(seed()));

struct MyAwaiter {
    std::jthread& outerThread;
    bool await_ready() const noexcept {
        auto res = gen();
        if (res) std::cout << " (executed)" << '\n';
        else std::cout << " (suspended)" << '\n';
        return res;
    }
    void await_suspend(std::coroutine_handle<> h) {
        outerThread = std::jthread([h] { h.resume(); });
    }
    void await_resume() {}
};


struct Job{
    static inline int JobCounter{};
    Job() {
        ++JobCounter;
    }

    struct promise_type {
        int JobNumber{JobCounter};
        Job get_return_object() { return {}; }
        std::suspend_never initial_suspend() {
            std::cout << "   Job " << JobNumber << " prepared on thread "
                      << std::this_thread::get_id();
            return {};
        }
        std::suspend_never final_suspend() noexcept {
            std::cout << "   Job " << JobNumber << " finished on thread "
                      << std::this_thread::get_id() << '\n';
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}
    };
};

Job performJob(std::jthread& out) {
    co_await MyAwaiter{out};
}

int main() {

    std::vector<std::jthread> threads(8);
    for (auto& thr : threads) performJob(thr);

}
```

与上一个程序的主要区别是新的 awaitable MyAwaiter，它在协程 performJob 中使用（第 54 行）。相反，从协程 performJob 返回的协程对象很直接。本质上，它的成员函数 initial_suspend（第 38 行）和 final_suspend（第 43 行）返回预定义的 awaitable std::suspend_never。此外，这两个函数都会显示所执行任务的 JobNumber 及其运行的线程 ID。截图显示了哪些协程立即运行、哪些被挂起。借助线程 ID，你可以观察到被挂起的协程会在不同的线程上恢复。

你可以在 Wandbox^a 上试用该程序。

^a <https://wandbox.org/permalink/kkHgWKF0SYAwp8Dm>

