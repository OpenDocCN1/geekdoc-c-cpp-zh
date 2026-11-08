
## 一个贪婪的生成器函数

```cpp
// greedyGenerator.cpp

#include <iostream>
#include <vector>

std::vector<int> getNumbers(int begin, int end, int inc = 1) {

    std::vector<int> numbers;
    for (int i = begin; i < end; i += inc) {
        numbers.push_back(i);
    }

    return numbers;

}

int main() {

    std::cout << '\n';

    const auto numbers = getNumbers(-10, 11);

    for (auto n: numbers) std::cout << n << " ";

    std::cout << "\n\n";

    for (auto n: getNumbers(0, 101, 5)) std::cout << n << " ";

    std::cout << "\n\n";

}
```

当然，我用 getNumbers 重新发明了轮子，因为这项任务可以用 std::iota³ 完成。为了完整起见，这里是输出。

³http://en.cppreference.com/w/cpp/algorithm/iota

![](img/c60a87adb7f61e2e82071d081bbb389a_440_0.png)

## 一个生成器函数

对 greedyGenerator.cpp 程序的两点观察至关重要。一方面，第 8 行的 vector numbers 总是获取所有值。即使我只关心一个有 1000 个元素的 vector 的前 5 个元素，情况也是如此。另一方面，很容易将函数 getNumbers 转换为惰性生成器。以下程序故意不完整。生成器的定义仍然缺失。

## 一个惰性生成器函数

```cpp
// lazyGenerator.cpp

#include <iostream>

generator<int> generatorForNumbers(int begin, int inc = 1) {

    for (int i = begin; i += inc) {
        co_yield i;
    }

}

int main() {

    std::cout << '\n';

    const auto numbers = generatorForNumbers(-10);

    for (int i = 1; i <= 20; ++i) std::cout << numbers() << " ";

    std::cout << "\n\n";

    for (auto n: generatorForNumbers(0, 5)) std::cout << n << " ";

    std::cout << "\n\n";

}
```

虽然 greedyGenerator.cpp 文件中的函数 getNumbers 返回 std::vector<int>，但 `lazyGenerator.cpp` 中的协程 `generatorForNumbers` 返回一个生成器。第 17 行的生成器 `numbers` 或第 23 行的 `generatorForNumbers(0, 5)` 在请求时返回一个新数字。基于范围的 for 循环触发查询。准确地说，协程的查询通过 `co_yield` 返回值 i 并立即暂停其执行。如果请求新值，协程将恰好在该位置恢复执行。

第 23 行的表达式 `generatorForNumbers(0, 5)` 是生成器的就地使用。

我想明确强调一点。协程 `generatorForNumbers` 创建一个无限数据流，因为第 8 行的 for 循环没有结束条件。如果我只需要有限数量的值，例如第 20 行，这没问题。第 23 行则不然，因为没有结束条件。因此，该表达式会 *永远* 运行。

### 6.1.2 特性

协程有一些独特的特性。

#### 6.1.2.1 典型用例

协程是编写事件驱动应用程序¹的常用方式，这些应用程序可以是模拟、游戏、服务器、用户界面，甚至算法。协程通常也用于协作式多任务²。协作式多任务的关键在于每个任务按需花费时间，但避免睡眠或等待，而是允许其他任务运行。协作式多任务与抢占式多任务形成对比，后者有一个调度器决定每个任务获得 CPU 的时间。

协程有不同类型。

#### 6.1.2.2 底层概念

C++20 中的协程是**非对称的**、**一等公民的**和**无栈的**。

**非对称**协程的工作流返回给调用者。**对称**协程则不然。**对称**协程可以将其工作流委托给另一个协程。

**一等公民**协程类似于一等函数，因为协程的行为像数据。行为像数据意味着你可以将它们用作函数参数或返回值，或将它们存储在变量中。

**无栈**协程可以暂停和恢复顶层协程。协程的执行和从协程的让出会返回给调用者。协程将其状态存储在栈之外以便恢复。**无栈**协程通常被称为可恢复函数。

¹ https://en.wikipedia.org/wiki/Event-driven_programming
² https://en.wikipedia.org/wiki/Computer_multitasking

#### 6.1.2.3 设计目标

Gor Nishanov 在提案 N4402^4 中描述了协程的设计目标。

协程应该

- 具有高可扩展性（可扩展到数十亿个并发协程）
- 具有高效的恢复和暂停操作，其成本与函数开销相当
- 与现有设施无缝交互且无额外开销
- 具有开放的协程机制，允许库设计者开发暴露各种高级语义的协程库，例如生成器、协程^5、任务等
- 可用于禁止或不可用异常的环境

由于可扩展性和与现有设施无缝交互的设计目标，协程是无栈的。相比之下，有栈协程在 Windows 上保留 1MB 的默认栈，在 Linux 上保留 2MB 的默认栈。

函数成为协程有四种方式。

#### 6.1.2.4 成为协程

函数使用以下内容时成为协程

- `co_return`，或
- `co_await`，或
- `co_yield`，或
- 基于范围的 for 循环中的 `co_await` 表达式。

^4 https://isocpp.org/files/papers/N4402.pdf
^5 https://tour.golang.org/concurrency/1

## 区分协程和协程句柄

术语“协程”通常用于两个不同的事物：调用 `co_return`、`co_await` 或 `co_yield` 的函数，以及协程句柄。对两个不同实体使用同一个术语可能会让你困惑（就像我一样）。让我澄清这两个术语。

**一个产生 2021 的简单协程**

```cpp
MyFuture<int> createFuture() {
    co_return 2021;
}

int main() {

    auto fut = createFuture();
    std::cout << "fut.get(): " << fut.get() << '\n';

}
```

这个简单的示例有一个函数 `createFuture`，并返回一个 `MyFuture<int>` 类型的对象。两者都被称为协程。具体来说，函数 `createFuture` 是返回协程句柄 `MyFuture<int>` 的协程。协程句柄是指向一个对象的句柄，该对象实现了框架以对特定行为建模。我在 `co_return` 一节中介绍了这个简单协程的实现和使用。

##### 6.1.2.4.1 限制

协程不能有 `return` 语句或占位符返回类型。这适用于无约束占位符（`auto`）和受约束占位符（概念）。

此外，具有可变参数^8 的函数、`constexpr` 函数、`consteval` 函数、构造函数、析构函数和 `main` 函数不能是协程。

### 6.1.3 框架

用于实现协程的框架包含 20 多个函数，其中一些必须实现，一些可以覆盖。因此，你可以根据需要定制协程。

一个协程与三个部分相关联：承诺对象、协程句柄和协程帧。客户端获取协程句柄以与承诺对象交互，承诺对象将其状态保存在协程帧中。

#### 6.1.3.1 承诺对象

承诺对象在协程内部被操作，并通过承诺对象传递其结果或异常。

承诺对象支持以下接口。其中一些函数必须实现，一些是可选的。

**承诺对象**

| 成员函数 | 描述 |
|---|---|
| `Constructor` | 承诺需要一个构造函数。 |
| `initial_suspend()` | 确定协程在运行前是否暂停。 |
| `final_suspend() noexcept` | 确定协程在结束前是否暂停。 |
| `unhandled_exception()` | 当发生未处理异常时调用。 |
| `get_return_object()` | 初始化返回给调用者的协程句柄。 |
| `get_return_object_on_allocation_failure()` | 定义内存分配失败时的行为。 |
| `return_value(val)` | 由 `co_return val` 调用。 |
| `return_void()` | 由 `co_return` 或协程结束调用。 |
| `yield_value(val)` | 由 `co_yield val` 调用。 |
| `await_transform(val)` | 返回一个可等待对象。 |
| `operator new(size)` | 定义协程如何分配内存。 |
| `operator delete(ptr, size)` | 定义协程如何释放内存。 |

编译器在执行协程期间自动调用这些函数。工作流一节详细介绍了此工作流。

函数 get_return_object 初始化客户端用于与协程交互的协程句柄。

