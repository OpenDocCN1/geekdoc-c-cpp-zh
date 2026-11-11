

### yield_value 从不挂起

```cpp
std::suspend_never yield_value(int value) {
    std::cout << "        promise_type::yield_value" << '\n';
    current_value = value;
    return {};
}
```

正如你可能猜到的，while 循环（第 77 - 82 行）会永远运行下去，协程不会返回任何内容。

```
promise_type::promise_type
promise_type::get_return_object
Generator::Generator
promise_type::initial_suspend
Generator::getNextValue
getNext: start
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
```

*yield_value 从不挂起*

重构生成器 infiniteDataStreamComments.cpp，使其产生有限数量的值，是件很简单的事。

### 6.7.2 泛化

你可能想知道为什么我从未使用 Generator 的全部泛型潜力。让我调整它的实现，以生成标准模板库中任意容器的连续元素。

## 生成器依次返回每个元素

```cpp
// coroutineGetElements.cpp

#include <coroutine>
#include <memory>
#include <iostream>
#include <string>
#include <vector>

template <typename T>
struct Generator {

    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    Generator(handle_type h): coro(h) {}

    handle_type coro;

    ~Generator() {
        if ( coro ) coro.destroy();
    }
    Generator(const Generator&) = delete;
    Generator& operator = (const Generator&) = delete;
    Generator(Generator&& oth): coro(oth.coro) {
        oth.coro = nullptr;
    }
    Generator& operator = (Generator&& oth) {
        coro = oth.coro;
        oth.coro = nullptr;
        return *this;
    }
    T getNextValue() {
        coro.resume();
        return coro.promise().current_value;
    }
    struct promise_type {
        promise_type() {}

        ~promise_type() {}

        std::suspend_always initial_suspend() {
            return {};
        }
        std::suspend_always final_suspend() noexcept {
```

## 6.8 各种任务工作流

在修改 co_await 一节中的工作流之前，我想让 awaiter 工作流更加透明。

### 6.8.1 透明的 Awaiter 工作流

我为程序 startJob.cpp 添加了一些注释。

按需启动任务（包含注释）

```cpp
// startJobWithComments.cpp

#include <coroutine>
#include <iostream>

struct MySuspendAlways {
  bool await_ready() const noexcept {
    std::cout << "      MySuspendAlways::await_ready" << '\n';
    return false;
  }
  void await_suspend(std::coroutine_handle<>) const noexcept {
    std::cout << "      MySuspendAlways::await_suspend" << '\n';
  }

  void await_resume() const noexcept {
    std::cout << "      MySuspendAlways::await_resume" << '\n';
  }
};

struct MySuspendNever {
  bool await_ready() const noexcept {
    std::cout << "      MySuspendNever::await_ready" << '\n';
    return true;
  }
  void await_suspend(std::coroutine_handle<>) const noexcept {
    std::cout << "      MySuspendNever::await_suspend" << '\n';
  }

  void await_resume() const noexcept {
    std::cout << "      MySuspendNever::await_resume" << '\n';
  }
};

struct Job {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;
    handle_type coro;
    Job(handle_type h) : coro(h) {}
    ~Job() {
        if ( coro ) coro.destroy();
    }
    void start() {
        coro.resume();
    }


    struct promise_type {
        auto get_return_object() {
            return Job{handle_type::from_promise(*this)};
        }
        MySuspendAlways initial_suspend() {
            std::cout << "  Job prepared" << '\n';
            return {};
        }
        MySuspendAlways final_suspend() noexcept {
            std::cout << "  Job finished" << '\n';
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}

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

### 显式启动任务

```cpp
int main() {

    std::cout << "Before job" << '\n';

    auto job = prepareJob();
    job.start();

    std::cout << "After job" << '\n';

}
```

此处显式调用 job.start() 是必要的，因为 Awaitable MySuspendAlways 中的 await_ready 总是返回 false。现在假设 await_ready 可以返回 true 或 false，并且任务没有被显式启动。简短提醒：当 await_ready 返回 true 时，会直接调用 await_resume 函数，而不会调用 await_suspend。

### 自动恢复 Awaiter

```cpp
// startJobWithAutomaticResumption.cpp

#include <coroutine>
#include <functional>
#include <iostream>
#include <random>

std::random_device seed;
auto gen = std::bind_front(std::uniform_int_distribution<>{0,1},
                           std::default_random_engine(seed()));

struct MySuspendAlways {
    bool await_ready() const noexcept {
        std::cout << "    MySuspendAlways::await_ready" << '\n';
        return gen();
    }
    bool await_suspend(std::coroutine_handle<> handle) const noexcept {
        std::cout << "    MySuspendAlways::await_suspend" << '\n';
        handle.resume();
        return true;
    }
    void await_resume() const noexcept {
        std::cout << "    MySuspendAlways::await_resume" << '\n';
    }
};

struct Job {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;
    handle_type coro;
    Job(handle_type h): coro(h) {}
    ~Job() {
        if ( coro ) coro.destroy();
    }

    struct promise_type {
        auto get_return_object() {
            return Job(handle_type::from_promise(*this));
        }
        MySuspendAlways initial_suspend() {
            std::cout << "  Job prepared" << '\n';
            return {};
        }
        std::suspend_always final_suspend() noexcept {
            std::cout << "  Job finished" << '\n';
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}

    };
};

Job performJob() {
    co_await std::suspend_never;
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

首先，这个协程现在叫作 `performJob`，并且会自动运行。`gen`（第 9 行）是一个生成 0 或 1 的随机数生成器。它使用以该种子初始化的默认随机引擎来完成任务。借助 `std::bind_front`^24，我可以把它和 `std::uniform_int_distribution` 绑定在一起，得到一个可调用对象；调用后，它会给出随机数 0 或 1。

在这个例子中，我移除了 C++ 标准中预定义的 Awaitable，只保留作为成员函数 `initial_suspend`（第 41 行）返回类型的 Awaitable `MySuspendAlways`。`await_ready`（第 13 行）返回一个布尔值。当布尔值为 true 时，控制流直接跳转到成员函数 `await_resume`（第 23 行）；当为 false 时，协程会立即挂起，因此会运行 `await_suspend` 函数（第 17 行）。`await_suspend` 函数获取协程的句柄，并用它来恢复协程（第 19 行）。除了返回值 `true` 之外，`await_suspend` 也可以返回 `void`。

下面的截图展示了：当 `await_ready` 返回 `true` 时，会调用 `await_resume` 函数；当 `await_ready` 返回 `false` 时，也会调用 `await_suspend` 函数。

你可以在 Compiler Explorer^27 上尝试运行这个程序。

- 24 https://en.cppreference.com/w/cpp/utility/functional/bind_front
- 27 https://godbolt.org/z/8b1Y14

