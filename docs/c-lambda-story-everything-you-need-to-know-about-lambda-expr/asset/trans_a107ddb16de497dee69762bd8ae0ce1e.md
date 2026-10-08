
我们可以通过使用互斥锁并在每次调用 `push_back` 之前对其加锁来解决同步问题。但这种代码仍然高效吗？如果过滤条件非常简单且执行速度快，那么你的性能可能比串行版本 (seq) 还要慢。

更不用说，通过并行运行它，你无法确定输出向量中被复制元素的顺序。

本节仅展示了并行算法的基本概览，如果你想了解更多内容，请参阅以下文章：Bartek 的编程博客：C++17 并行算法的惊人性能，可能吗？

## Lambda 与 Async - 封装（Wrap Upon）

总结一下：当你想启动线程、通过 `std::async` 调用异步代码或与并行算法一起使用时，Lambda 表达式非常方便。然而，务必记住，闭包对象在并发方面并不是唯一的，所有的挑战在这里同样适用。

## 总结

在本章中，你已经看到 C++17 结合了 C++ 的两个核心元素：`constexpr` 与 Lambda。这是向改进语言中元编程支持的必要一步。我们将在下一个关于 C++20 的章节中看到更多内容。此外，C++17 标准还解决了捕获 `this` 的问题。在新标准中，你可以通过值捕获它，使得代码变得安全得多。

我们还查看了 Lambda 的一些用例：IIFE（立即调用函数表达式）技术、折叠表达式和变长通用 Lambda，以及 Lambda 表达式和异步代码执行。得益于 C++17 提供的各种特性，我们现在有了更优雅的语法和更直接的方法编写高效代码。

## 5. C++20 中的 Lambda

在 2020 年 2 月于拉格的会议上，ISO 委员会最终批准了 C++20 标准并将其推正式发布（可能在 2020 年底）。新规范为语言和标准库带来了许多实质改进！Lambda 表达式也得到了几次升级。

在本章中，你将看到：

- C++20 中的哪些变化。
- 捕获 `this` 指针的新选项。
- 模板 Lambda。
- 如何使用概念（concepts）改进通用 Lambda。
- 如何将 Lambda 与 `constexpr` 算法结合。
- 如何让重载模式更短。

你可以在 N4861（当前的 C++20 草案，拉格版本之后）以及 lambda 章节：`[expr.prim.lambda]` 中查看与 lambda 规范。

## Lambda 语法更新

在 C++20 中，我们关于 Lambda 表达式的语法有了更多变化：

- 你现在可以在参数列表后添加 `consteval`。
- 有一个指定模板尾部（template tail）的选项。
- 在尾部返回之后你可以放置 `requires` 声明。

```
<params> () specifiers exception attr - -> requires { /code; /* */
  ^       ^       ^
  |       | |
  |       optional: 尾部返回类型
  | optional: mutable, constexpr, consteval, noexcept, attributes
  | 参数列表（当未添加修饰符时可选）
  |
optional: 模板参数列表
|
带有可选捕获列表的 lambda 引导符
```

你可以在后续章节中阅读新的修改内容。

## 变更快速概述

通过 C++20，我们将获得以下与 Lambda 表达式相关的特性：

- 允许使用 `[=, this]` 作为 Lambda 捕获 - P049R2，并弃用通过 `[]` 隐式捕获 `this` - P0806。
- Lambda 初始化捕获中的包展开：`...args = std::move(args) {}` - P0780。
- 用于结构化绑定的 `static`、`thread_local` 和 Lambda 捕获 - P1091。
- 模板 Lambda（带概念） - P0428R2。
- 简化隐式 Lambda 捕获 - P0588R1。
- 可默认构造和赋值的静态 Lambda - P0624R2。
- 未求值上下文中的 Lambda - P0315R4。
- `constexpr` 算法 - 最重要的是 P2022、P0879 和 P1645。

如果你想了解更多关于 C++20 的信息，可以查看总结所有变化的论文：C++17 与 C++20 差异 DIS - P2131。

你也可以查看我的参考卡，其中列了所有语言和库特性：Bartek 的编程博客：C++20 参考卡。

现在让我们快速查看一些变化。

在大多数情况下，新添加的特性“清理”了 Lambda 语法。此外，C++20 增加了允许我们在高级场景中使用 Lambda 的增强功能。

例如，通过 P1091，你可以捕获结构化绑定：

> 某些编译器即使在 C++17 中也支持结构化绑定（针对 GCC），但当时标准并未强制规定。

C++20 还带来了与 *`this` 捕获*相关的澄清。如果你在方法中捕获 `[=]`，将得到一个警告：

关于隐式 *this 捕获*。实时代码 @Wandbox

```cpp
struct Baz {
    auto foo() {
        return [=]() { cout << s << '\n'; };
    }
    std::string s;
};
```

使用 GCC 9 编译会产生以下警告：

warning: implicit capture of 'this' ['=] is deprecated in C++20

警告的出现是因为，即使使用 `[=]`，你也会将 `this` 作为指针捕获。最好显式地写出你想要的：`[=, this]` 或 `[=, *this]`。

在快速回顾后，让我们看看 C++20 中与 Lambda 相关的更显著特性。

## consteval Lambda

虽然 C++11 的 `constexpr` 允许在编译阶段执行函数，但在运行时运行这些函数也是可能的。似乎在某些情况下，将功能仅限制在编译时是最好的。这就是为什么在 C++20 中，我们有一个新的关键字，它可以创建符合 `constexpr` 函数规则但只能在编译时评估的函数。这类函数也称为“立即函数”（immediate functions）。

这个新关键字也可以应用于 Lambda。让我们查看一个简单的示例：

立即 Lambda。实时代码 @Wandbox

```cpp
int main() {
    const int x = 10;
    auto lam = [int x] consteval { return x; };
    return lam(x);
}
```

在，你在参数列表后应用了 `consteval`。这与 `constexpr` 非常相似。区别在于，如果你去掉 `x` 的 `const`，Lambda 可以工作（运行时），而立即 Lambda 则不能。

默认情况下，如果 Lambda 遵循 `constexpr` 函数规则，编译器会将其标记为隐式。对于 `consteval` 则并非如此。你可以在提案中找到该特性的完整规范：P1073R3。

## 捕获参数包

C++20 获得的一个改进是捕获中的包展开：

```cpp
template <typename...Args> void call(Args&&... args) {
    auto ret = [...capturedArgs] = std::move(args)]();
}
```

以前在 C++20，代码无法编译（参见该问题的 C11 章节），为了解决这个问题，你必须将参数封装进独立的元组。你可以在 P0780 中阅读。

总之，捕获变长包，我们可以从 C11 章节获取示例进行实验，并添加最新的特性。例如，我们可以利用折叠表达式对每个捕获的对象进行打印：

捕获变长包。实时代码 @Wandbox

```cpp
#include <iostream>
#include <memory>

template < class First, class... Args>
void captureTest(First& first, Args&... args) {
    const auto printer = [first = std::move(first),
        ...capturedArgs = std::move(args)]() {
        ((std::cout << ", ") << capturedArgs, ...));
        std::cout << '\n';
    };
    printer();
}

int main() {
    auto ptr = std::make_unique<int>(10);
    captureTest(std::move(ptr), 2, 3, 4);
    captureTest(std::move(ptr), 'a', 'b');
}
```

输出：

0xf06cb20, 2, 3, 4
a, b

在示例中，我们使用了一个打印对象，与我们在 C11 章节中编写的代码相似，但这次我们捕获变量而不是而不是作为 Lambda 参数传递它们。
