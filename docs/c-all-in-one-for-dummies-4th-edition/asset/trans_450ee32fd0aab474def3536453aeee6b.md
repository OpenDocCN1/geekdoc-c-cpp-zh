
该示例首先创建一个待排序项的 vector。然后创建两条排序规则。SortRule1 和 SortRule2 都会执行比较，并返回一个 bool 值，表示该比较（第一项小于第二项）是否为 true。区别在于，SortRule2 针对列表的两列执行任务，因此需要两级比较。随后代码调用 sort() 执行列表排序，并依靠 foreach 循环显示结果，结果如下：

```
One Column Sort
Mirror 54   1st Floor
Statue 33   1st Floor
Chair 44    1st Floor
Mirror 33   2nd Floor
Chair 36    2nd Floor
Statue 40   Basement
Statue 30   Basement

Two Column Sort
Chair 44    1st Floor
Mirror 54   1st Floor
Statue 33   1st Floor
Chair 36    2nd Floor
Mirror 33   2nd Floor
Statue 40   Basement
Statue 30   Basement
```

### 指定 lambda 表达式抛出异常

异常可能是代码中很难正确实现的一部分，因为异常表示发生了意外情况，调用方需要采取行动。早期版本的 lambda 表达式在声明中包含 throw() 说明，作为声明的一部分，但该说明被证明难以实现，许多程序员认为它是一种笨拙的编程方式。因此，尽管 throw() 仍是规范中的可选部分，但通常看不到它被使用。事实上，在 C++20 中不能使用它，因为它已被弃用并移除。

![](img/128ab511de4e7360e167e3b15cdd5dd0_432_0.png)

MultiTask 示例（参见清单 2-5）在调用方未提供可接受的正确类型输入时抛出异常。抛出异常仍然完全可以接受，而且当从 lambda 表达式调用外部函数时，这些函数也可能抛出异常。然而，有时你确实不希望异常发生，因为这种意外情况是预期内的。为解决这个问题，可以使用 `noexcept()` 忽略异常，如下所示：

```cpp
cout << noexcept(ChangeNum(5,5)) << endl;
```

代码不会输出异常，而是输出捕获的 `Total` 值，即 0。这是 `noexcept()` 的运算符形式。你还可以使用 `noexcept()` 的说明符形式，但它不保证能在较旧版本的 C++ 中工作。它看起来像这样：

```cpp
auto ChangeNum = [Total](auto Type, int Value) mutable
    noexcept { ... }
```

在这种情况下，无法抛出异常会影响整个 lambda 表达式，以及它调用的任何函数。当然，现在你不知道异常条件何时真的发生——当出现未预见的情况时，代码只是尽可能输出某个答案，而这个答案很可能是错误的。

**本章内容**

-   理解 C++ lambda 表达式
-   在新的位置放置 lambda 表达式
-   创建可赋值的 lambda 表达式
-   展开参数包

## 第 3 章：高级 lambda 表达式

上一章演示了在大多数 C++11 及更高版本中可以使用 lambda 表达式执行的任务。本章进一步讨论使用更新版本 C++ 可以执行的高级任务。事实上，第一节是 C++20 特有的。其余部分章节中也有一些适用于 C++17。重点在于，如果你使用的是较旧版本的 C++，本章看到的大部分内容都无法工作。请记住，如果你的 C++ 编译器不提供所需的 C++20 功能，你可以使用 Wandbox（https://wandbox.org/）测试本章示例。

本章还会介绍在 C++20 中使用 lambda 表达式的新方式。在 C++20 之前，不能在需要未求值表达式的上下文中使用 lambda 表达式，包括 `decltype()` 运算符，而这是本章的具体主题。不过，你学到的技术可以应用于其他未求值上下文。如果你现在还不理解这些术语，不用担心；本章后文会介绍它们。

较旧版本的 C++ 不允许你赋值 lambda 表达式，也不允许使其可构造。因此，当源 map 对象包含 lambda 表达式时，你无法做类似让两个 map 对象相等的事情（有关 map 的详细信息，参见第 5 册第 6 章的“映射你的数据”一节）。此外，很难让 lambda 表达式成为 map 声明中可构造的一部分，因此最终每次都要重新创建它。本章将探讨 C++20 如何修复这两个问题。

上一章探讨了各种类型的捕获。不过，可以将其概括为按副本、按引用或按 `std::tuple` 捕获。要发送任意打包的数据列表，且参数数量可变，需要使用可变参数模板。本章最后一节讨论包的使用，并演示 C++ 如何展开包以允许访问。你会在此类功能中使用参数数量直到运行时才已知的场合。例如，你可能需要处理带有可变数量约束的数据。

![](img/128ab511de4e7360e167e3b15cdd5dd0_435_0.png)

你不必手动输入本章的源代码。事实上，使用可下载的源代码要容易得多。你可以在可下载源代码的 `\CPP_AIO4\BookIII\Chapter03` 文件夹中找到本章的源代码。有关如何找到这些源文件的详细信息，请参见引言。

### 考虑 C++20 lambda 扩展

C++20 增加了许多 lambda 扩展。其中一些扩展会在本章后续内容中出现。其余扩展将在以下各节中介绍。

### 定义立即函数

立即函数与 `consteval` 相关联，它通常如下所示：

```cpp
#include <iostream>

using namespace std;

consteval double sqr(float x) {
  return x * x;
}

int main()
{
    constexpr double MySquare = sqr(4.2);
    cout << MySquare << endl;
    return 0;
}
```

MySquare 的值在编译时而非运行时计算。MySquare 从应用程序开始到结束时占用静态内存空间，并且其值从不改变。

lambda 表达式的 consteval 说明符具有相同效果，但通常更灵活、更简洁。下面是同一代码的 lambda 表达式版本：

```cpp
#include <iostream>

using namespace std;

int main()
{
    auto sqr = [](auto x) consteval {return x*x;};
    constexpr double MySquare = sqr(4.2);
    constexpr auto MySquare2 = sqr(20);

    cout << MySquare << endl;
    cout << MySquare2 << endl;
    return 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_436_0.png)

与函数版本一样，MySquare 和 MySquare2 的值都在编译时计算。因此，如果你尝试使用编译时未知的值，编译器会生成错误消息。

### 在捕获中使用 = 和 this

本迷你书第 2 章的“在类和结构中使用 lambda 表达式”和“使用捕获子句”两节中展示的示例演示了如何使用捕获。有些捕获目前不太易读。例如，下面两个捕获都隐含 this，即指向当前对象的指针，但只有一个捕获显式写出了 this：

```cpp
[=]
[=, *this]
```

`=` 运算符表示按副本捕获所有变量。`this` 运算符也按副本捕获当前对象。使用 `*this` 按引用捕获当前对象，这意味着你可以对其进行更改。在 C++20 中，现在可以使用 `[=, this]` 明确表示你按副本捕获变量和当前对象，而不是按引用捕获。你还可以使用 `[&, this]`，它表示按引用捕获所有变量，但按副本捕获对象。

### 查找其他更改

有时，尽管你对 lambda 表达式有尽可能最好的理解，但在编写代码时事情就是不工作，而看起来它们本应工作。通常，你会发现规范中的细微变化，这些变化告诉你某些东西为什么不再工作。例如，你可以在论文“P1091R2 Extending structured bindings to be more like variable declarations”（将结构化绑定扩展得更像变量声明）中看到其中一些变化，网址为 http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1091r2.html。

### 在未求值上下文中工作

未求值表达式是一种完整表达式；它不需要在运行时求值。例如，`typeof`、`sizeof`、`noexcept` 和 `decltype` 运算符不会被求值。此外，C++20 的 requires 表达式（参见 https://en.cppreference.com/w/cpp/language/constraints）也不会被求值。未求值上下文是 C++ 在其中寻找某种类型的未求值表达式的上下文。C++20 允许在未求值表达式、模板实参、别名声明和 `typedef` 声明中使用 lambda 表达式。

要了解未求值上下文如何工作，清单 3-1 中所示的 `PriorityQueue` 示例演示了如何在 `decltype()` 中添加 lambda 表达式比较器，以自动对优先队列排序。

**清单 3-1：** 定义优先队列比较器

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
```
