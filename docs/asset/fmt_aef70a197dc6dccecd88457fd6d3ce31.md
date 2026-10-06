
```cpp
template <C1 Type> // 约束
requires C2<Type> void fun();
```

```cpp
template <typename> // 相同的，使用'and'
requires C1<Type> and C2<Type> void fun();
```

```cpp
template <typename> // 相同的，尾随'requires'
void fun() requires C1<Type> and C2<Type>;
```

```cpp
template <typename>
struct Multi;
```

```cpp
template <C1 Type> // 约束
requires C2<Type> struct Multi<Type>; // 类模板
```

## 23.13. CEPTS

```cpp
template <Subtractable Type>
struct Data<Type>
{};
```

但这可能不是你想要的：当定义 `Data<vector<int>>()` 时，由于 `template<typename Type> Data` 仅被声明，编译器会报错说 `Data<std::vector<int>>` 是一个不完整的结构体，因为它无法使用针对 `Addable` 或 `Subtractable` 的特化。它会回退到通用模板，但该模板没有可用实现，而在这里它是不完整的。

定义一个需要两个类型的模板（第一个类型是 `Addable`，第二个参数无限制的），同时又定义了一个需要 `Subtractable` 类型和 `int` 的特化版本，这同样无法按意图工作。在这种情况下，模板可能是：

```cpp
template <typename t1, typename t2> requires Addable<t1>
struct Data
{};
template <Subtractable Type>
struct Data<Type, int>
{};
```

它会回退到第一个（通用的）模板定义。然而，那一个也不行，因为第一个参数不是可加的，你会收到关于 `(lh + rh)` 格式不错误的报错。

现在，正如你所预期的，模板的第二个参数本该让你收到关于 `(lh - rh)` 格式错误的报错，但并没有发生。换句话说：使用概念（Concepts）仍然需要你理解发生了什么。概念帮助编译器定位编译失败的原因，但归根结底需要你理解自己在做什么，以便明白编译器正试图告诉你的什么。

### 23.13.7.2 绑定的自由运算符

早些在第 22.10.2 节中，涵盖了模板类中嵌套类的自由运算符的构造。其中定义的嵌套类通常通过定义由嵌套类定义的类型的模板参数，来选择合适的自由运算符。

概念提供了另一种定义自由运算符的方法，将其绑定到嵌套类模板类型的类型上。使用概念时，类模板及其嵌套类可以以最基础的形式定义，如下：

```cpp
template <typename Data>
struct String
{
    struct iterator
    {
        using value_type = Data;
        std::string::iterator d_iter;
        // 注意这里的 <>：operator== 是一个函数模板特化
        // 因为 'iterator' 是一个类模板
        friend bool operator==(iterator const &lhs, iterator const &rhs);
        iterator begin() {
            return iterator();
        }
    };
};
```

一旦指定了类接口（`struct String`），就可以构化出概念 `StringIterator`。它要求自由运算符匹配 `String<Data>::iterator`：

```cpp
template<typename Type>
concept StringIterator = std::same_as<Type, typename String<Data>::iterator_type>;
```

现在可以使用简写规范将自由（运算符）定义为函数模板：

```cpp
inline bool operator==(StringIterator auto const &lhs, StringIterator auto const &rhs)
{
    return lhs.d_iter == rhs.d_iter;
}
```

通过概念定义嵌套类的自由运算符，我们实现了这些运算符的完美匹配。此外，在设计类模板时，软件工程师可以集中在类的本质特征上，而不必考虑第 22.10.2 节中涵盖的特殊定义。

## 24. 协程

考虑以下任务：设计一个程序，在后续调用时提供一个返回下一个斐波那契数字的函数。这是一个关于程序如何设计的示例：它定义了一个类 `Fibo`，并在 `main` 中调用 `Fibo::next` 来计算下一个斐波那契数字（为了简洁起见，程序使用单个文件）：

```cpp
#include <iostream>
#include <string>
using namespace std;
class Fibo {
    size_t d_return = 0;
    size_t d_next = 1;
public:
    size_t next();
};
size_t Fibo::next() {
    size_t ret = d_return;
    d_return = d_next;
    d_next += ret;
    return ret;
}
int main(int argc, char *argv) {
    Fibo fibo;
}
```

> ¹ 斐波那契数从 0 和 1 开始。下一个斐波那契数是最后两个斐波那契数之和。从此开始，序列为 0, 1, 2, 3, 5...

```cpp
size_t sum = 0;
Fibo fibo;
for (size_t begin = 0, end = argc == 1 : stoul(argv[1]); begin < end; ++begin) {
    sum += fibo.next();
}
cout << sum << '\n';
```

显然，`next` 成员并不复杂。但当它被调用时，会执行一些操作，这些操作本身与计算斐波那契数字无关：

- 调用函数会为了忽略拷贝和销毁值参数以及局部对象的复杂性：
    - 将其参数推入栈中；
    - 将这些参数所需的字节数推入栈中；
    - 将下一条执行指令的位置推入栈中以完成函数；
    - 将当前函数的栈帧位置推入栈中；
    - 将当前栈指针的值拷贝到寄存器；
    - 在函数的第一个指令处继续执行；
    - 这首先为栈上所有的局部变量留出了空间。
- 一旦执行了返回语句：
    - 栈指针被重置为存储在基寄存器中的值，移除局部变量；
    - 弹出基寄存器；恢复调用者的帧；
    - 从栈中弹出调用者的下一条执行指令的值；
    - 通过栈顶的值缩小栈。

C++ 协程允许我们避免调用普通函数所需的步骤。后续章节将深入探讨协程，但这里是协程版的 `Fibo::next` 作为入门示例：

```cpp
#include "main.h"
FiboCoro() {
    size_t returnFibo = 0;
    size_t next = 1;
    while (true) {
        size_t ret = returnFibo;
        returnFibo = next;
        next += ret;
        co_yield;
    }
}
```

现在我们已经观察到 `fiboCoro` 协程的一些特征：它是一个自由函数，因此没有指向调用协程的对象的（隐藏）指针。

1012

第 24 章 协程 (COROUTINES)

在第 5 行调用了 `fiboCoro`，它返回一个（尚未介绍的）纤对象。这个纤对象被称为协程处理器，调用 `fibo.next()`，这会恢复 `fiboCoro`，随后它在 `co_yield` 语句处挂起，通过处理器的 `next` 函数返回下一个可用值。

协程的核心特性是它们可以暂停挂起执行，同时保留当前状态。通常情况下，一旦挂起，协程的调用者将从返回协程值的指令之后恢复其工作。因此，协程也被称为**协作例程**，不应将其与并发例程混淆。

## 24.1 定义协程

在定义协程时，必须包含 `<coroutine>` 头文件。

如果一个函数使用了 `co_yield`、`co_await` 或 `co_return` 关键字，则该函数是一个协程。协程不能使用 `return` 关键字，不能定义变量参数，且它们的返回类型必须是一个现有类型，该类型定义了协程处理器。

```cpp
int main(int argc, char **argv)
{
    auto fibo = Fibo();
    sum += fibo.next();
}
```

`Fibo` 类本身定义了相关特性，允许编译器生成代码，将协程的局部变量、协程返回或挂起时下一条执行指令的位置以及其所谓的 `promise_type` 对象存储在堆上。这只发生一次，当协程被激活时，通常会在调用函数时采取这些步骤并立即执行协程，使用其可用的局部变量和参数。协程的处理器类被称为 `Future`，它们的嵌套状态类必须是处理器的 `promise_type`。

## 24.1 定义协程

现在通常使用 **Handler** 和 **State** 这两个术语。

定义一个协程很容易，但在使用协程时，必须定义其处理器类。此外，处理器类必须定义一个嵌套类，该嵌套类的名称必须作为 `promise_type` 公开可用。

```cpp
#include <coroutine>
class Fibo {
    class State
    {
    };
    std::coroutine_handle<State> d_handle;
    public:
        using promise_type = State;
        explicit Fibo(std::coroutine_handle<State> handle);
        ~Fibo();
        size_t next();
};
```

协程的处理器类具有以下特征：

- 它有一个嵌套类，用于跟踪协程的状态；
- 它通常定义一个类型为 `std::coroutine_handle<State>` 的私有数据成员；
- 除非处理器的嵌套类通过声明自动调用为 `promise_type`，否则必须指定以使该嵌套类名称也称为 `promise_type`；
- 其他成员是公共的，尽管通常至少有一个成员返回协程状态中可用的值，例如示例 `main` 函数中使用的 `next` 成员：

```cpp
sum += fibo.next();
```

`next` 成员的当前实现会恢复协程。

```cpp
size_t Fibo::next()
{
  if (d_handle)
    d_handle.resume();
  return d_handle.promise().value;
}
```

### 24.1.1 协程的状态 (promise_type)

`State` 类跟踪协程的状态。

```cpp
class State {
    size_t d_value;
    public:
        Fibo get_return_object();
        std::suspend_always yield_value(size_t value);
        std::suspend_always initial_suspend();
        std::suspend_always final_suspend() noexcept;
        void unhandled_exception();
};
```

`State` 类没有声明构造函数，因此使用了默认构造函数。也可以声明并定义默认构造函数。

通过返回空的 `suspend_always`，协程的操作将被挂起直到恢复。

```cpp
inline std::suspend_always Fiber::State::initial_suspend()
{
  return {};
}
inline std::suspend_always Fiber::State::final_suspend() noexcept
{
  return {};
}
```

```cpp
inline void Fiber::State::unhandled_exception()
std::rethrow_exception(std::current_exception());
```

成员 `Fiber::State::get_return_object()` 返回协程处理器类的对象。

以下是 `Fibo::State::get_return_object` 的实现：
