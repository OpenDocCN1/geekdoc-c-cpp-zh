

```cpp
        std::cout << gen2.getNextValue() << " ";
    }

    std::cout << "\n\n";

    std::vector myVec{1, 2, 3, 4, 5};
    auto gen3 = getNext(myVec);
    for (int i = 0; i < myVec.size(); ++i) {
        std::cout << gen3.getNextValue() << " ";
    }

    std::cout << '\n';

}
```

在这个示例中，生成器被实例化并使用了三次。前两种情况下，`gen`（第 76 行）和 `gen2`（第 83 行）用 `std::string helloWorld` 初始化，而 `gen3` 使用 `std::vector<int>`（第 91 行）。程序的输出应该不会令人意外。第 78 行依次返回字符串 `helloWorld` 的所有字符，第 85 行只返回前五个字符，第 93 行返回 `std::vector<int>` 的元素。

你可以在 Compiler Explorer³ 上试用该程序。

![](img/c60a87adb7f61e2e82071d081bbb389a_575_0.png)

一个依次返回每个元素的生成器

简而言之，`Generator<T>` 的实现与上一个几乎相同。与上一个程序的关键区别在于协程 `getNext`。

## getNext

```cpp
template <typename Cont>
Generator<typename Cont::value_type> getNext(Cont cont) {
    for (auto c: cont) co_yield c;
}
```

`getNext` 是一个函数模板，它接受一个容器作为参数，并在基于范围的 for 循环中遍历所有容器元素。每次迭代后，该函数模板会暂停。返回类型 `Generator<typename Cont::value_type>` 可能会让你感到意外。`Cont::value_type` 是一个依赖模板参数，解析器需要提示。默认情况下，如果某个名称可以被解释为类型或非类型，编译器会假定它是非类型。因此，我必须在 `Cont::value_type` 前面加上 `typename`。

³https://godbolt.org/z/jozmva

这个通用协程仍然有一些缺陷。在最后的迭代中，我修复了这些缺陷，并扩展了它的接口，使其可用于基于范围的 for 循环。

## 7.3.3 迭代器协议

### 支持迭代器协议的生成器

```cpp
// coroutineRange.cpp

#include <concepts>
#include <coroutine>
#include <exception>
#include <iostream>
#include <string>
#include <vector>


template<typename T>
struct Generator {

    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;


    Generator(handle_type h) : coro(h) { }
    handle_type coro;
    ~Generator() { if (coro) coro.destroy(); }

    Generator(const Generator&) = delete;
    Generator& operator=(const Generator&) = delete;
    Generator(Generator&& oth) : coro(oth.coro) {
        oth.coro = nullptr;
    }
    Generator& operator= (Generator&& oth) {
        coro = oth.coro;
        oth.coro = nullptr;
        return *this;
    }

    struct promise_type {
        T coroValue;

        std::suspend_always yield_value(const T val) {
            coroValue = val;
            return {};
        }

        auto get_return_object() {
            return std::coroutine_handle<promise_type>::from_promise(*this);
        }
        std::suspend_always initial_suspend() { return {}; }
        void return_void() { }
        void unhandled_exception() { std::terminate(); }
        std::suspend_always final_suspend() noexcept { return {}; }
    };

    struct Iterator {
        handle_type coro;
        Iterator(auto p) : coro(p) { }
        void getNext() {
            if (coro) {
                coro.resume();
                if (coro.done()) {
                    coro = nullptr;
                }
            }
        }
        T operator*() const {
            return coro.promise().coroValue;
        }
        Iterator operator++() {
            getNext();
            return *this;
        }
        bool operator==(const Iterator& i) const = default;
    };

    Iterator begin() const {
        if (!coro || coro.done()) {
            return Iterator(nullptr);
        }
        Iterator itor{coro};
        itor.getNext();
        return itor;
    }

    Iterator end() const {
        return Iterator(nullptr);
    }
};

template <std::ranges::forward_range Cont>
Generator<typename Cont::value_type> getCoroutine(Cont cont) {

    for (const auto& c : cont) {
        co_yield c;
    }
}

int main() {

    std::string helloWorld = "Hello world";
    auto genChar = getCoroutine(helloWorld);
    for (const auto& val : genChar) {
        std::cout << val << " ";
    }

    std::cout << "\n\n";

    std::vector myVec{1, 2, 3, 4, 5};
    auto genNumbers = getCoroutine(myVec);
    for (const auto& val : genNumbers) {
        std::cout << val << " ";
    }

    std::cout << "\n\n";
}
```

得益于成员函数 begin（第 72 行）和 end（第 81 行），Generator 支持迭代器协议。这两个成员函数都返回迭代器对象。begin 返回容器中的第一个元素，而结束迭代器为 Iterator{nullptr}。为了获取第一个值，begin 通过调用 getNext()（第 77 行）恢复协程一次。Iterator 是一个最小迭代器，支持三个基本成员函数：operator*（第 61 行）、operator++（第 64 行）和 operator==（第 68 行）。

- operator* 返回当前值
- operator++ 递增当前值
- operator!= 将当前值与结束迭代器进行比较。编译器根据 operator== 生成 operator!=。

程序 coroutineRange.cpp 中的 Generator 明显比程序 coroutineGetElements.cpp 中的上一个更健壮。这种健壮性主要归功于迭代器。成员函数 getNext（第 53 行）会检查句柄 coro 是否表示一个协程（第 54 行）。此外，成员函数 begin（第 72 行）保证只有在协程未完成时才恢复它：coro.done()（第 73 行）。恢复一个已经完成的协程是未定义行为。

### 恢复已完成的协程

```cpp
std::string helloWorld = "Hello world";
auto genChar = getCoroutine(helloWorld);
for (const auto& val : genChar) {
    std::cout << val << " ";
}

for (const auto& val : genChar) {
    std::cout << val << " ";
}
```

如果没有程序 coroutineRange.cpp 中的 coro.done()（第 73 行）检查，那么第二个基于范围的 for 循环（第 7 行）将触发协程恢复，因此会导致未定义行为。

泛型函数 getCoroutine（第 86 行）使用了概念 std::ranges::forward_range。

最后，以下是程序的输出：

![](img/c60a87adb7f61e2e82071d081bbb389a_579_0.png)

一个支持迭代器协议的生成器

## 7.4 各种任务工作流

![](img/c60a87adb7f61e2e82071d081bbb389a_580_0.png)

Cippi 在挖花园

在修改 `co_await` 一节中的工作流之前，我想让 `awaiter` 工作流更加透明。

### 7.4.1 透明的 Awaiter 工作流

我在程序 startJob.cpp 中添加了一些输出消息。

按请求启动任务（包括注释）

```cpp
// startJobWithComments.cpp

#include <coroutine>
#include <iostream>

struct MySuspendAlways {
    bool await_ready() const noexcept {
        std::cout << "        MySuspendAlways::await_ready" << '\n';
        return false;
    }

    void await_suspend(std::coroutine_handle<>) const noexcept {
        std::cout << "        MySuspendAlways::await_suspend" << '\n';
    }
    void await_resume() const noexcept {
        std::cout << " MySuspendAlways::await_resume" << '\n';
    }
};

struct MySuspendNever {
    bool await_ready() const noexcept {
        std::cout << " MySuspendNever::await_ready" << '\n';
        return true;
    }
    void await_suspend(std::coroutine_handle<>) const noexcept {
        std::cout << " MySuspendNever::await_suspend" << '\n';
    }
    void await_resume() const noexcept {
        std::cout << " MySuspendNever::await_resume" << '\n';
    }
};

struct Job {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;
    handle_type coro;
    Job(handle_type h): coro(h){}
    ~Job() {
        if (coro) coro.destroy();
    }
    void start() {
        coro.resume();
    }
};

struct Job::promise_type {
    auto get_return_object() {
        return Job{handle_type::from_promise(*this)};
    }
    MySuspendAlways initial_suspend() {
        std::cout << " Job prepared" << '\n';
        return {};
    }
    MySuspendAlways final_suspend() noexcept {
        std::cout << " Job finished" << '\n';
        return {};
    }
};
```

