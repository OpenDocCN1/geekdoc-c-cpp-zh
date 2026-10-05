

# 从协程返回

`co_return` 语句有两种形式。`co_return` 语句可以返回一个值，也可以返回任意类型的值。在两种情况下，`co_return` 语句的指定如下：

```cpp
co_return;
```

然而，必须定义相应的特殊函数来处理每种 `co_return` 情况。对于 `co_return` 语句不返回值的情况，该特殊函数在 `promise_type` 结构体中声明为：

```cpp
void return_void();
```

函数的体可以是空的，也可以实现一些清理代码。

在下例示例中，我们实现了一个简单地打印 hello world 然后退出的协程：

```cpp
#include <coroutine>
#include <iostream>

struct ReturnObject {
    struct promise_type = default;
    ReturnObject get_return_object() { return {}; };
    std::suspend_never initial_suspend() { return {}; };
    std::suspend_never final_suspend() noexcept { return {}; };
    void unhandled_exception() { };

    void return_void() {}
};
```

```cpp
// 协程 foo 的声明
struct ReturnObject foo() {
    std::cout << "hello world" << std::endl;
    co_return;
}

int main(void) {
    foo();
}

// 输出
hello world
```

# 从协程返回一个值

如果 `co_return` 返回一个值，那么协程除了声明 `return_void()` 之外，还必须在 `ReturnObject` 中声明一个名为 `return_value` 的函数以返回值。

在接下来的示例中，协程在返回时会返回字符串 "hello, I am returning"：

```cpp
#include <coroutine>
#include <iostream>

using namespace std;

struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return ReturnObject();
        }

        std::suspend_never initial_suspend() {
            return {};
        }

        std::suspend_never final_suspend() noexcept {
            return {};
        }
    };
    void return_void() {}
    void unhandled_exception() { };

    string return_value() const { return "hello, I am returning\n"; };
};

// 协程 foo 的声明
struct ReturnObject foo() {
    co_return;
}

int main(void) {
    ReturnObject ret = foo();
    cout << ret.return_value();
    cout << "exiting main";
}

// 输出
hello, I am returning
exiting main
```

# 挂起协程

协程可以挂起执行。它不能被调用者挂起。当协程自身挂起时，它会将状态保存在堆上并返回一个指向 `ReturnObject` 的句柄（给调用协程的函数）。调用函数可以使用该句柄来恢复或销毁协程。

协程挂起点通过 `co_await` 和 `co_yield` 关键字标识。协程可以有多个挂起点。

`co_await` 运算符接受一个 awaiter 对象作为其唯一参数。例如：

```cpp
co_await std::suspend_always {};
或
co_await std::suspend_never {};
```

在下例示例中，我们的 `foo` 协程挂起了它自己：

```cpp
#include <coroutine>
#include <iostream>

struct ReturnObject {
    struct promise_type = default;
    ReturnObject get_return_object() { return {}; };
    std::suspend_never initial_suspend() { return {}; };
    std::suspend_never final_suspend() noexcept { return {}; };
    void unhandled_exception() { };
    void return_void() {}
};
```

```cpp
// 协程 foo 的声明
struct ReturnObject foo() {
    std::cout << "hello world" << std::endl;

    co_await std::suspend_always {};

    std::cout << "good-bye" << std::endl;
}

int main(void) {
    foo();
}
```

```cpp
// 输出
hello world
```

文本 good-bye 没有输出，因为我们已经挂起了协程。

注意 `co_await` 只是一个一元运算符，所以我们可以将其写成：

```cpp
co_await(std::suspend_always {});
```

运算符函数的体可以提供在挂起之前执行的代码。

# 恢复已挂起的协程

调用函数通过 `coroutine_handle` 对象控制协程。

参阅：https://en.cppreference.com/w/cpp/coroutine/handle

`coroutine_handle` 是一个带有如下声明的模板对象：

```cpp
template<typename promise_type = void> struct coroutine_handle;
```

它有两个感兴趣的特化版本。一个基于 `promise_type` 的主特化，以及 `<void>` 特化。后者的特化版本等同于 `template<> struct coroutine_handle`，一个没有参数的模板。

`coroutine_handle` 持有一个指向堆上协程数据的指针，并实现了若干控制协程的函数。编译器可以根据基于主特化的 `coroutine_handle` 隐式转换为 `void` 特化版本。这执行了类型擦除（移除了 `coroutine_handle` 中的 `promise_type`）。

我们现在将分两步展示 `coroutine_handle` 的规范。

首先，`coroutine_handle` 对象必须是 `ReturnObject` 的成员：

```cpp
struct ReturnObject {
    struct promise_type {
        promise_type() = default;
        ReturnObject get_return_object() { return {}; };
        std::suspend_never initial_suspend() { return {}; };
        std::suspend_never final_suspend() noexcept { return {}; };
        void unhandled_exception() { };
        void return_void() { };
    };
    coroutine_handle<promise_type> handle;
    ReturnObject(coroutine_handle<promise_type> _handle) : handle(_handle) {}
};
```

这里 `get_return_object` 创建了来自 `promise_type` 对象的句柄。

第二步使用 `coroutine_handle::from_promise` 静态成员函数从 `promise_type` 对象来实例化句柄。`from_promise` 接收 `promise_type` 对象并返回句柄。

因此 `ReturnObject` 的声明如下：

```cpp
struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return coroutine_handle<promise_type>::from_promise(*this);
        }

        std::suspend_never initial_suspend() {
            cout << "ready to execute coroutine" << endl;
            return {};
        }

        std::suspend_never final_suspend() noexcept {
            cout << "exiting coroutine" << endl;
            return {};
        }
    };
    void return_void() {cout << "returning no value to caller" << endl; }
    void unhandled_exception() { };

    coroutine_handle<promise_type> handle;
    ReturnObject(coroutine_handle<promise_type> _handle) : handle(_handle) {}
};
```

`ReturnObject` 的构造函数使用了句柄。`coroutine_handle` 提供了 `resume()` 方法来恢复协程。`done()` 方法是一个检查协程是否完成的谓词函数。如果协程处于挂起状态，则返回 true，否则返回 false。

在接下来的示例中，协程挂起了它两次，调用函数恢复了协程两次：

```cpp
#include <coroutine>
#include <iostream>

using namespace std;

struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return coroutine_handle<promise_type>::from_promise(*this);
        }

        std::suspend_never initial_suspend() {
            cout << "ready to execute coroutine" << endl;
            return {};
        }

        std::suspend_never final_suspend() noexcept {
            cout << "exiting coroutine" << endl;
            return {};
        }
    };
    void return_void() {cout << "returning no value to caller" << endl; }
    void unhandled_exception() { };

    coroutine_handle<promise_type> handle;
    ReturnObject(coroutine_handle<promise_type> _handle) : handle(_handle) {}
};

// 协程 foo 的声明
struct ReturnObject foo() {
    cout << "coroutine is executing\n";
    co_await std::suspend_always {};
    cout << "coroutine has resumed\n";
    co_await std::suspend_always {};
    cout << "coroutine has resumed\n";
    co_return;
}

int main(void) {
    ReturnObject ret = foo();

    if (ret.handle.done() == false) {
        cout << "resuming coroutine\n";
        ret.handle.resume();
    }

    if (ret.handle.done() == false) {
        cout << "resuming coroutine again\n";
        ret.handle.resume();
    }

    if (ret.handle.done()) {
        cout << "coroutine has finished";
    }
}
```

