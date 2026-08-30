
# C++23 最佳实践：提升 C++ 的简单规则与具体行动项

本书可在`http://leanpub.com/cpp23_best_practices`购买。此版本出版于 2024-01-01。

![出版商标志](https://leanpub.com/)

这是一本`Leanpub`书。`Leanpub`通过精益出版（Lean Publishing）流程为作者和出版商赋能。精益出版是指使用轻量级工具和多次迭代来发布正在进行中的电子书，并不断获取反馈，直到拥有正确的书籍。

©2024 Jason Turner 献给我的妻子 Jen。

## 指南

1. 封面

# 第一部分：优秀 C++ 的介绍与哲学

## C++23 版本简介

距离我最初发布第一版《最佳实践》已经过去大约 3 年了。在发布时，这本书的内容并不多。我选择向任何购买了`Leanpub`电子书的用户免费提供`C++20`更新（即“第二版”）。

我曾考虑过将`C++23`更新作为免费的“第三版”发布。然而，当我考虑到需要进行的更新时，我决定是时候对这本书进行完全全新的发布了。之所以需要这本书，主要是因为`C++23`改变了我们使用语言的许多基础方式（例如标准库模块）。与之前版本的区别也允许我重新组织主题以获得更好的流程。在之前的任何更新中，我都避免了重新组织（以便同事引用相关内容并避免混淆）。

我已经更新了书中所有的相关章节，以展示代码在`C++23`中应有的样子，并重新组织了许多主题。放心，这是对原《最佳实践》的一次重大更新！

## 原版简介

作为一名培训师和承包商，我的目标是让自己不再需要。我希望每个人都能：

1. 学会如何进行实验。
2. 不要仅仅相信我，而是去进行测试。
3. 学习语言是如何运作的。
4. 不要再犯上一代人同样的错误。

我正在考虑将我的头衔从“C++ 培训师”改为“C++ 指南”。我总是根据目前的课程来调整我的课程和材料。我们可能对一门关于`X`的课程达成一致，但在第一天途中我会将其改为`Y`以满足组织的需求。

在此过程中，我们作为一个小组进行实验和学习。我经常在教学中学习。每个小组都是独特的；每个班都有新问题。我在课程中收到的很多问题都是重复的，以至于我看起来像个读心者，因为我能预判下一个被提出的问题。

因此，有了这本书，以及它所源的 Twitter 推文，以帮助传播长期以来的最佳实践。

# 关于最佳实践

简单来说，最佳实践关乎于：

1. 减少常见错误。
2. 快速发现错误。
3. 在不牺牲（且通常会提升）性能的情况下。

## 为什么要用最佳实践？

### 你的项目并不特殊

如果你在用`C++`编程，那么你或你公司的某人就很在乎性能。否则，他们可能会使用其他编程语言。我去过很多公司，他们都告诉我他们很特殊，因为他们需要运行得飞快！

剧透一下：他们都在出于相同的原因做出相同的决定。极少数例外。那些做出不同决定的离群者，是那些已经在遵循书中建议的组织。

## 最坏会发生什么？

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

### 游戏

严重的缺陷会导致远程安全漏洞或攻击向量。

### 金融

严重的缺陷会导致[巨额资金损失、交易加速、市场崩溃](https://en.wikipedia.org/wiki/2010_flash_crash)。

### 航空航天

严重的缺陷会导致航天器丢失或[人类生命损失](https://spectrum.ieee.org/aerospace/aviation/how-the-boeing-737-max-disaster-looks-to-a-software-developer)。

### 你的行业

严重的缺陷会导致……金钱损失？丢工作？远程黑客攻击？

## 示例

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

我不想让气氛太沉闷，但让我们花时间思考一下，如果你的项目存在致命缺陷，最坏的情况会怎样。

```cpp
import std;

struct S {
  S(){ std::println("S()"); }
  S(const S &){ std::println("S(const S &)"); }
  S(S &&){ std::println("S(S &&)"); }
  S &operator=(const S &){
    std::println("operator=(const S &)");
    return *this;
  }
  S &operator=(S &&){
    std::println("operator=(S &&)");
    return *this;
  }
  ~S() { std::println("~S()"); }
};
```

图 1. 对象生命周期工具

| ![](img/leanpub_pencil.png) |
|---|

## 练习：构建你的第一个 C++ 实验

你是否有一个困扰你已久的 C++ 问题？你能设计一个实验来测试它吗？记住，Compiler Explorer 现在已经允许你运行代码了。

| ![](img/leanpub_pencil.png) |
|---|

## 练习：开始收集你的实验

一旦你创建了实验和测试，请务必保存它。考虑使用 GitHub gists 作为一种简单的方法来保存并与他人共享你的测试。

### 6.1：资源

- [Compiler Explorer 的快速上手示例。](https://godbolt.org/z/3eGP56)

# 7：记住：C++ 并不是面向对象的

我不是第一个指出这一点的人，也不会是最后一个。我认为这个概念现在已经被广泛接受了，但我仍然看到 C++ 学习者专注于“OOP”。

Bjarne Stroustrup 在*C++ 程序语言（第 3 版）*中写道：

> C++ 是一种通用的编程语言，偏向于系统编程，它：
>
> - 是一种更好的 C 语言；
> - 支持数据抽象；
> - 支持面向对象编程；
> - 支持泛型编程。

你必须理解 C++ 是一门多学科编程语言，才能充分发挥该语言的作用。C++ 有效地支持今天所有的编程范式。

- 过程式（Procedural）
- 函数式（Functional）
- 面向对象（Object-Oriented）
- 泛型（Generic）
- 编译时（`constexpr`和模板元编程）

知道在何时使用这些工具中的每一个是编写良好 C++ 的关键。僵化地坚持一种范式的项目会错过该语言最强大的特性。

| ![](img/leanpub_warning.png) |
|---|

不要试图一直尝试使用所有可能的技术。你最终将得到一堆难以维护和阅读的杂乱代码。在适当的时间使用适当的技术需要自律和练习。

| ![](img/leanpub_pencil.png) |
|---|

## 练习：质疑你当前的设计

如果你能跳出你项目正在使用的设计，你会做什么不同的改变？

### 7.1：资源

- [C++ 中的函数式编程](https://www.manning.com/books/functional-programming-in-c-plus-plus?a_aid=FPinCXX&a_bid=441f12cc)
- [C++ Weekly 第 137 集：C++ 不是面向对象的语言](https://youtu.be/AUT201AXeJg)

# 8：学习另一种语言

考虑到 C++ 不是面向对象的语言，你必须了解许多不同的技术才能充分利用 C++。

以下练习将帮助你接触到其他语言。但事实是，目前很少有语言是纯单范式语言。

每种语言都有其偏好的解决方法，这些方法在语言偏好的范式内有效。

Ben Deane [推荐这组程序员都应该学习的语言](http://www.elbeno.com/blog/?p=420)：

- ALGOL 家族（C 及其后代）
- Forth
- Lisp 及其变言
- Haskell
- Smalltalk
- Erlang

| ![](img/leanpub_pencil.png) |
|---|

## 练习：选择一种函数式语言学习

你能找到一种纯函数式语言吗？

| ![](img/leanpub_pencil.png) |
|---|

## 练习：选择一种面向对象的语言学习

找到一种纯面向对象的语言甚至更难！如今 Java 也有 lambda 函数了。

| ![](img/leanpub_pencil.png) |
|---|

## 练习：选择一种具有不同语法的语言

看起来像 C 家族语言的语言可能会让你感到更自在。尝试寻找一种看起来不同的语言并挑战你的思维。

### 8.1：资源

- [在名词王国中执行](https://steve-yegge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html)——让你思考不同的编程范式。

# 9：了解你的标准库

C++ 标准库正在不断增长。在 C++23 标准中，该库约为 1403 页，占标准的 66%。在 C++17 中，它只有 965 页。

意识到标准中发生的变化是关重要的。我们只触及部分内容，但 C++20 和 C++23 的一些亮点包括：

- 极大地扩展的时间处理（with calendar）
- 并发的许多变化
- `std::format`
- ranges
- concepts
- `<stacktrace>`

| ![](img/leanpub_pencil.png) |
|---|

## 练习：浏览 C++23，看看哪些吸引了你

https://en.cppreference.com/w/cpp

# 10：使用工具

在本书中你会看到关于工具的引用，以及一个专门关于“使用工具”的章节。C++ 默认有很多陷阱和边缘情况。我们使用各种工具来缓解这些问题。这是 C++ 的核心原则：开启所有工具！

# 11：不要触发未定义行为

好的，有很多未定义行为（UB），很难追踪，所以我们将在给出一些示例。你需要理解的关键是，UB 的存在意味着你的整个程序。[抽象说明](http://eel.is/c++draft/intro.abstract-5)

> 符合标准的实现执行良好的程序时，应产生与相同输入的一种可能的执行结果相同的观测行为。
>
> 然而，如果任何此类执行包含未定义操作，本文档对执行该输入的实现不作任何要求（即使是第一个操作之前的操作）。

注意这句话：“本文档对执行该输入的实现不作任何要求（即使是第一个操作之前的操作）”。

如果你有 UB，整个程序都是可疑的。

| ![](img/leanpub_info-circle.png) |
|---|

接下来的几项讨论了减少项目中未定义行为的方法。

| ![](img/leanpub_pencil.png) |
|---|

## 练习：使用 UBSan、ASan 和警告

理解所有的未定义行为是不可能的。幸运的是，我们有工具帮助。希望你已经为代码开启了 UBSan、ASan 并开启了警告。现在是回去评估你的情况并看看是否有新发现的好机会。

### 11.1：资源

- [C++Now 2018：John Regehr 闭场演讲：未定义行为与编译器优化](https://youtu.be/AeEwxtEOgH0)
- [CppCon 2018：Barbara Geller & Ansel Sermersheim 未定义行为不是错误](https://youtu.be/XEXpwis_deQ)

# 12：永远不要测试`this`是否为`nullptr`，那是 UB

```cpp
int Class::member() {
  if (this == nullptr) {
    // 会被编译器删除，如果这真的为空的话
    // 将是 UB
    return 42;
  } else {
    return 0;
  }
}
```

图 2. 检查`this`是否为`nullptr`是无效的。

从技术上讲，导致未定义行为（UB）的并不是这个检查。但是这个检查永远是不可能失败的。如果`this`是`nullptr`，你就会处于未定义行为状态。人们以前经常这样做，但它一直一直是 UB。你不能在对象的生命周期之外访问它。现在的编译器总是会移除这个检查。

理论上，`this`可能为`null`的唯一方法是当你直接在一个空指针对象上调用成员函数时。

| ![](img/leanpub_warning.png) |
|---|

后面是反面示例，请不要重复。

```cpp
Type *obj = nullptr;
obj->do_thing(); // 永远不要这样做
```

图 3. 在`nullptr`上调用成员的错误示例。

即使在（技术上可行，但永远不要这样做）的调用`delete this`场景下，也是如此。

```cpp
struct S {
  std::string data;

  void delete_yourself() {
    // 执行一些操作
    delete this; // 技术上可行

    if (this) {
      // 这个块将始终被执行，没有任何变化
      // 我们对 `this` 的视图
    }

    // 永远不要这样做
    data.size(); // UB，data 的生命周期已经结束
  }
};
```

图 4. `delete this`的错误示例。

在现代编译器上，不存在任何一种情况下对`if (this)`的检查会返回`false`。

| ![](img/leanpub_pencil.png) |
|---|

## 练习：你会检查`this`是否为`nullptr`吗？

对`nullptr`的检查可能伪装成对`NULL`的检查或对`0`的检查。对`this`是否为`NULL`的检查可能只存在非常旧的代码库中。确保你开启了警告，然后寻找这些情况。

在你的代码库中搜索`this ==`可能是很有趣的，看看那里存在什么奇怪的事情。

### 12.1：资源

- [迁移到 GCC-6 优化移除了对`this`的空指针检查](https://www.gnu.org/software/gcc/gcc-6/porting_to.html#this-cannot-be-null)

# 13：永远不要测试引用是否为`nullptr`，那是 UB

```cpp
int get_value(int &thing) {
  if (&thing == nullptr) {
    // 被编译器移除
    return 42;
  } else {
    return thing;
  }
}
```

图 5. 对`null`引用的测试被移除了。

创建一个空引用是 UB，不要尝试。始终假设引用指向一个有效的对象。在设计 API 时，利用这一事实来让自己占优势（（`#all_chapter_contents.xhtml_make-interfaces-hard-to-use-wrong`）。

| ![](img/leanpub_pencil.png) |
|---|

## 练习：检查对象地址的检查

使用`&thing ==`检查对象的特定地址有很多有效的用例，但也有许多方法可以让这种检查是错误的。

搜索你的代码中检查对象内存地址的语句，并理解它们在做什么以及是如何工作的（或者是否工作）。

| ![](img/leanpub_question-circle.png) |
|---|

除了`==`之外，还可以通过其他方法检查对象的地址？

这个练习让你在使用各种搜索/grep 工具以及玩正则表达式方面获得很棒的经验。

### 13.1：资源



* [-Wtautological-undefined-compare](https://clang.llvm.org/docs/Diagnostics.html#tautological-undefined-compare)（注：此处原文链接可能不完整，已根据语境补全）

# Part II：使用工具

## 14：使用工具：自动化测试

你需要一个命令来运行测试。如果你没有自动化测试，那么维护质量是不可能的。

以下是常用的测试框架：

- [Catch2](https://github.com/catchorg/catch2)：流行的框架，源自 [Martin Hoenestrup](https://github.com/hoenestrup) 和 [Petr Horenovský]。
- [doctest](https://github.com/doctest/doctest)：与 Catch2 类似，但更轻量。
- [Google Test](https://github.com/google/googletest)：谷歌出品。
- [Boost.Test](https://www.boost.org/doc/libs/1_84_0/libs/test_framework/index.html)：Boost 标准。

`ctest`（https://cmake.org/ctest.html）是 CMake 的测试运行器，可以与上述任何框架配合使用。理想的 CMake 构建流程看起来像这样：

```text
1 cmake -S src -B builddir -G <Generator>
2 cmake --build builddir --config <Configuration>
3 cd builddir
4 ctest -C <Configuration>
```

图 6. 可能的构建测试步骤。

没有自动化测试，你无法维护项目质量。

在我职业生涯处理过的 C++ 项目中，我不得不支持某些组合：

- x86
- x64
- SPARC
- ARM
- MIPS
- Windows
- Solaris
- MacOS
- Linux

当你开始在多个平台组合多个编译器时，某个平台上的重大更改可能会破坏一个或多个平台。

为了解决这个问题，为你的项目开启带有测试的持续构建：

- 测试你支持的所有平台。
- 分别测试 Debug 和 Release。
- 测试所有配置选项。
- 针对比你支持的新版本的编译器进行测试。

> Sanitizers 只能对未被优化器移除的代码注入，但优化器有时会利用 UB，因此你至少需要 Debug、Debug + Sanitizers、Release、Release + Sanitizers，至少在一个平台上！

> 如果你不要求 100% 的测试通过，你永远不知道代码的状态。

## 练习：开启持续构建

了解你组织目前的持续构建环境。如果不存在，建立它的障碍是什么？为你的项目设置类似 GitLab、GitHub Actions、Appveyor 或 Travis 有多困难？

## 16：使用工具：编译器警告

你有许多没有使用的警告，其中绝大多数是有益的。`-Wall` 并不是 GCC 和 Clang 上的所有警告。`-Wextra` 仅仅是触及表面！

> `/Wall` 在 MSVC 上是所有的警告。我们的编译器编写者建议在 MSVC 上使用 `/Wall` 或在 Clang 上使用 `-Weverything`，因为其中许多是不可操作的诊断性警告。GCC 没有提供等效方案。

强烈建议使用 `-Wpedantic`（GCC/Clang）。此命令行选项会禁用语言扩展，并让代码更接近 C++ 标准。你今天开启的警告越多，未来迁移到其他平台时就越越容易。

> 在 MSVC 的 C++20 模式下，`/permissive-` 不再是必要的，它现在是 `cl.exe` 的默认设置。

## 练习：启用更多警告

1. 探索你的编译器提供的可用警告集。尽可能开启所有警告。
2. 修复新生成的警告。
3. 回到第 1。

> MSVC 拥有一套非常出色的警告，可以通过警告级别启用。你可以从 `/W1` 开始，并在修复每组警告的过程中，逐步提升到 `/W4`。

这个过程会让你觉得枯燥且毫无意义，但这些警告会捕捉真实的 Bug。

## 练习：讨论在 CI 上启用 `-Werror` 或 `-WX` 以确保警告不累积

> 我观察到，你需要在开发者机器和 CI 上都开启“警告视为错误”，否则开发者会将 CI 视为敌人，并会禁用越来多的警告！

### 16.1：资源

- [C++ 最佳实践网站整理的警告列表](https://github.com/lefticus/cppbestpractices/blob/master/02-Use_the_Tools_Available.md#compilers)
- [GCC 完整警告列表](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)
- [Clang 完整警告列表](https://clang.llvm.org/docs/DiagnosticsReference.html)
- [MSVC 默认关闭的编译器警告](https://docs.microsoft.com/en-us/cpp/preprocessor/compiler-warnings-that-are-off-by-default?view=vs-2019)
- [C++ Weekly 第 168 期——发现你应该使用的警告](https://youtu.be/IOo8gTDMFkM)

## 17：使用工具：静态分析

静态分析工具是在不编译或执行代码的情况下分析代码的工具。你的编译器就是此类工具之一，也是你的第一道防线。

许多工具都是免费的，有些对开源项目免费。

`cppcheck` 和 `clang-tidy` 是两个流行且免费的工具，与主流 IDE 和编辑器有深度集成。

## 练习：启用更多静态分析

Visual Studio：查看随附的 Microsoft 静态分析器。考虑使用 `Clang Power Tools`。下载 Visual Studio 的 `cppcheck` 插件。

CMake：启用 `cppcheck` 和 `clang-tidy` 集成。

## 练习：在你的 IDE 中启用静态分析

大多数现代 IDE 都内置支持 `clang-tidy` 和静态分析工具。研究如何启用这些支持，并配置你的 `.clang-tidy` 文件，以开启适用于你项目的分析。

### 17.1：资源

- [cppbestpractices.com 静态分析器列表](https://github.com/lefticus/cppbestpractices/blob/master/02-Use_the_Tools_Available.md#static-analyzers)

## 18：使用工具：考虑自定义静态分析

记住专注于让你的接口难以误用。然后，作为第二道防线，考虑编写自己的静态分析。

这些可能以以下形式存在：

- [自定义 clang-tidy 分析](https://clang.llvm.org/extra/clang-tidy/Contributing.html)
- 使用 `clang-query` 查询项目的 [AST](https://clang.llvm.org/docs/LibASTMatchersReference.html) 以查找常见错误。
- 为 `cppcheck` 编写[自定义规则](https://sourceforge.net/projects/cppcheck/files/Articles/)。
- [CodeQL](https://codeql.github.com/) 自定义检查。

## 练习：寻找常见的编码错误

只需与团队其他成员讨论你在代码库中看到的常见问题。看看是否能隔离出一两个自定义分析检查就能发现的常见问题。使用上述工具之一实现一个检查。

### 18.1：资源

- [快速演讲：使用 Clang Query 隔离 AST 元素——Kristen Shaker——C++ on Sea 2022](https://youtu.be/2LOxsfpCCyI)
- [供学习的自定义 cppcheck 规则数据库](https://github.com/embeddedartistry/cppcheck-rules)
- [CodeQL 教程](https://codeql.github.com/docs/writing-codeql-queries/ql-tutorials/)

## 19：使用工具：Sanitizers（消毒器）

Sanitizers 是 C++ 的运行时分析工具，内置于 GCC、Clang 和 MSVC 中。

如果你熟悉 Valgrind，Sanitizers 提供了类似的功能，但速度比 Valgrind 快几个数量级。

可用的 Sanitizers 包括：

- Address（ASan）
- Undefined Behavior（UBSan）（更多信息见后文）
- Thread
- DataFlow
- Fuzzer

Address Sanitizer、Undefined Behavior Sanitizer 和 Thread Sanitizer 可以发现很多问题。

当发生内存越界等错误时，Sanitizer 会给出报告并提供修复建议。

你可以通过以下命令启用 Address 和 Undefined Behavior sanitizers：

```bash
gcc -fsanitize=address,undefined <file>
```

Sanitizers 在链接阶段也必须启用。

> 使用 sanitizers 的示例可见 [C++ Template](https://github.com/cpp-best-practices/cmake_template)。

> 结合 Debug、Release、开启 sanitizer 和关闭 sanitizer 的构建，每种组合都能暴露不同的问题。

## 练习：启用 Sanitizers

- 研究如何为你的项目添加 sanitizer 支持。
- 先启用 ASan。
- 运行测试套件并调查发现的问题。
- 后启用 UBSan。
- 再次运行测试套件。

目标：在你的环境下运行所有 ASan 和 UBSan。

## 练习：回到 Valgrind 或 Dr Memory

如果你无法在环境中运行 ASan 和 UBSan，请研究使用 Dr Memory（Windows/Linux/MacOS）或 Valgrind（Linux/MacOS）运行测试套件。

### 19.1：资源

- [MSVC 版 AddressSanitizer（ASan）](https://devblogs.microsoft.com/cppblog/addresssanitizer-asan-for-windows-with-msvc/)
- [GitHub 上的 Sanitizers 与文档](https://github.com/google/sanitizers)
- [Clang AddressSanitizer 文档](https://clang.llvm.org/docs/AddressSanitizer.html)
- [Clang UndefinedBehaviorSanitizer 文档](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html)

## 20：使用工具：加固

安全对于许多行业和产品都很重要。如果安全是你关注的，你应该考虑在发布二进制时进行加固。

待填充。

## 练习：考虑 UBSan 最小运行时

UBSan 的“最小运行时”版本是为二进制加固设计的。

## 21：使用工具：多个编译器

在你的平台上支持*至少* 2 个编译器。每个编译器进行不同的分析，并且对标准的实现也略有不同。

如果你使用 Visual Studio，你应该相对容易地在 `clang` 和 `cl.exe` 之间切换。你可以使用 WSL 并启用远程 Linux 构建。

如果你使用 Linux，你应该轻松地在 GCC 和 Clang 之间切换。

> 在 MacOS 上，请确保你使用的编译器确实是你所认为的那一个。`gcc` 命令很可能是 Apple 安装的 clang 的软链接。

> `apple-clang` 与主线 clang 不是一回事，它们的版本号也不匹配。通常很难知道 `apple-clang` 支持哪些功能。cppreference 的[编译器支持参考文档](https://en.cppreference.com/w/cpp/compiler_support)可能会有所帮助。

要在你的平台上安装较新版本或不同的编译器，可以参考以下方法：

### Ubuntu / Debian

- `GCC`：[工具链 PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/ppa)
- `Clang`：[apt 软件包](https://apt.llvm.org/)

### Windows

- [GCC MinGW](http://mingw.org/)
- [Clang 官方下载](https://releases.llvm.org/download.html)

### MacOS

- Homebrew / MacPorts

## 练习：添加另一个编译器

既然你已经开启了系统的持续构建，现在是添加另一个编译器的时候了。

你当前需要的编译器的新版本总是个好主意。但如果你只支持 `GCC`，考虑添加 `Clang`。如果你只支持 `Clang`，请添加 `GCC`。如果你在 Windows 上，除了 `MSVC` 之外，添加 `MinGW` 或 `Clang`。

## 练习：添加另一个操作系统

希望你的项目至少部分可以移植到另一个操作系统。让项目部分在另一个操作系统和工具链上编译的练习将让你深入了解你代码的本质。

### 21.1：资源

- [C++Now 2015：Jason Turner“思考移植性：如何以及为什么让你的 C++ 跨平台”](https://youtu.be/cb3WIL96N-o)

## 22：使用工具：模糊测试与变异

你的想象力限制了你所创建的测试。在调用 API 时你会尝试进行恶意调用吗？你会故意向输入传递格式错误的数据吗？你会处理来自未知或不可信源的输入吗？

为所有可能的组合中的所有函数调用生成所有可能的输入是不可能的。幸运的是，有工具可以解决这个问题。

### 22.1：模糊测试（Fuzzing）

模糊测试器生成各种长度的随机数据字符串。你编写的测试框架消耗这些数据字符串，并以适用于你的应用程序的方式进行处理。模糊测试器分析由测试执行生成的覆盖率数据，并利用这些信息移除冗余测试，生成新的新颖且独特的测试。

从理论上讲，如果运行足够的时间，模糊测试最终将达到被测试代码 100% 的覆盖率。结合 `AddressSanitizer`，这成为了一个发现代码中 bug 的强大工具。[来自 2015 年的一篇有趣文章](https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html)描述了模糊测试器与 `AddressSanitizer` 的结合如何在不到 6 小时内发现 OpenSSL 中的“heartbleed”漏洞。

这 6 小时现在已经完全过时了。使用现代的模糊测试工具和更新的计算机，像 heartbleed 这样的漏洞可以在几分钟内被发现。

> 模糊测试主要发现内存和安全漏洞。

存在许多不同的模糊测试工具。为了本节内容，我将关注 [LLVM 的 libFuzzer](https://www.llvm.org/docs/LibFuzzer.html)。大多数模糊测试器都在相同的前提下运行。

你必须提供某种入口。入口的形式通常如下函数：

```cpp
extern "C" int LLVMFuzzerTestOneInput(const uint8_t *Data,
                                     size_t Size);
```

图 8. `libFuzzer` 入口。`Data` 指针总是有效的，`Size` 参数 >= 0。



如果你的库主要解析文件（例如 `libpng`），那么你的工作非常简单：

```cpp
extern "C" int LLVMFuzzerTestOneInput(const uint8_t *Data,
                                     size_t Size)
{
  parseInput(Data, Size);
}
```

图 9. `libFuzzer` 的数据使用。

如果你的函数接收的是数据结构而非输入字符串，你的工作会复杂一些，但可行：

```cpp
template<typename Type>
std::tuple<const uint8_t *, size_t, Type>
    createStruct(const uint8_t *Data, size_t Size)
{
  // 仅允许简单类型 (trivial types) 执行此操作
  static_assert(std::is_trivial_v<Type>);
  Type result{}; // 初始化
  const auto bytesToRead = std::min(sizeof(Type), Size);
  std::memcpy(&result, Data, bytesToRead);
  return {std::next(Data, bytesToRead), Size - bytesToRead, result};
}
```

（注：上述代码基于提供的文本逻辑的表示。）

- [CppCon 2020: Barnabás Bágyi “Fuzzing Class Interfaces for Generating and Running Tests with `libFuzzer`”](https://cppcon2020.sched.com/event/e7An/fuzzing-class-interfaces-for-generating-and-running-tests-with-libfuzzer?iframe=no) - 关于以新方式使用模糊测试的启发性演讲。视频尚未上线 YouTube，但请在本书出版后尝试查找。
- [Autotest](https://gitlab.com/wilzegers/autotest/) - 与“Fuzzing Class Interfaces for Generating and Running Tests with `libFuzzer`”演讲相关的库。
- [FuzzTest](https://github.com/google/fuzztest) - Google 提供的模糊测试库。
- [DeepState](https://github.com/trailofbits/deepstate) - TrailOfBits 提供的模糊测试工具。
- [oss-fuzz](https://github.com/google/oss-fuzz) - 开源项目的持续模糊测试。
- [Mutate++](https://github.com/nlohmann/mutate_cpp) - 变异测试工具。

# 23：使用工具：构建生成器

- [CMake](https://cmake.org)
- [Meson](https://mesonbuild.com/)
- [Bazel](https://bazel.build/)
- [其他](https://github.com/lefticus/cppbestpractices/blob/master/02-Use_the_Tools_Available.md)

原始 `Makefile` 或 Visual Studio 项目文件会让实现上述任何一项都变得过于复杂。使用构建工具来帮助维护跨平台和编译器的可移植性。

像对待其他代码一样对待你的构建脚本。它们有自己的最佳实践，编写不可维护的构建脚本和编写不可维护的 C++ 一样容易。

构建生成器还可以通过 `cmake --build` 等工具抽象并简化你的持续构建环境，无论使用什么平台，它都能执行正确的操作。

| ![](img/leanpub_pencil.png) |

## 练习：调查你的构建系统

- 你的项目目前使用构建生成器吗？
- 你的构建脚本有多久了？

查看是否有你需要应用的当前最佳实践。是否有可以在你的构建脚本上运行的 tidy 或格式化工具？

回本书书中之前的最佳实践，看看它们如何应用于你的构建脚本。

- 你是否在重复造轮？
- 是否存在更高级的抽象？

| ![](img/leanpub_info-circle.png) |

最新版本的 CMake 添加了如 `--profiling-output` 等工具，帮助你查看生成器花费时间在哪里。

## 23.1：资源

- [Professional CMake: A Practical Guide](https://crascit.com/professional-cmake/)
- [cmake-tidy](https://github.com/MaciejPatro/cmake-tidy)
- [C++Now 2017: Daniel Pfeiffer “Effective CMake”](https://youtu.be/bsXLMQ6WgIk)
- [CppCon 2017: Mathieu Ropert “Using Modern CMake Patterns to Enforce a Good Modular Design”](https://youtu.be/eC9-iRN2b04)
- [CppCon 2018: Jussi Pakkanen “Compiling Multi-Million Line C++ Code Bases Effortlessly with the Meson Build System”](https://youtu.be/SCZLnopmYBM)
- [BazelCon 2019](https://www.youtube.com/playlist?list=PLxNYxgaZ8Rsf-7g43Z8LyXct9ax6egdSj)
- [CppCon 2019: Mathieu Ropert “Cato the Elder”](https://youtu.be/D07iF4Lp4kM) - 关于构建脚本质量的简短吐槽。
- [C++ Weekly Ep 218 - The Ultimate CMake / C++ Quick Start](https://youtu.be/YbgH7yat-Jo)
- [Twitter 关于 CMake 资源的讨论](https://twitter.com/Cor3ntin/status/1310990444915032067)

# 24：使用工具：包管理器

近年来，人们对 C++ 包管理器的兴趣爆发式增长。以下这两个变得最受欢迎：

- [Vcpkg](https://github.com/Microsoft/vcpkg)
- [Conan](https://conan.io/)

使用包管理器有明确的优势。包管理器有助于可移植性并减轻开发者的维护负担。

| ![](img/leanpub_info-circle.png) |

我还想引起你关注 [CPM](https://github.com/cpm-cmake/CPM.cmake)。

CPM 提供了一种简单直接的 CMake 集成方法，用于构建和链接到可以通过 `fetch_content` 获取的 CMake 项目。

| ![](img/leanpub_pencil.png) |

## 练习：你的依赖有哪些？

花时间清理你项目的依赖项。将你的依赖项与上述包管理器提供的包进行比较。是否有某个包管理器包含了你所有的依赖项？你现在的软件包过时多久？你目前缺少哪些安全修复？

# 第三部分：API 和代码设计

# 25：让接口变得难以使用

接口是你的第一道防线。如果你提供一个易于使用的接口，用户就会使用它。如果你提供一个难以使用的接口，用户就会误用它。

## 25.1：资源

- [The Little Manual of API Design](https://people.mpi.de/~blanche/api-design.pdf)

# 26：考虑错误地使用 API

考虑 POSIX `socket` 的 API：

```text
1 socket(int, int, int);
```

图 13. POSIX `socket` API。参数（以某种顺序）表示：

- 类型 (`type`)
- 协议 (`protocol`)
- 域 (`domain`)

这种设计是有问题的，但我们的代码中潜伏着不那么明显的问题。你是否接受原始指针？是否有方法保证内部用户不会误用 API？

| ![](img/circle.png) |

是否有方法保证外部用户不会误用 API？

| ![](img/circle.png) |

## 练习：检查类型

C++ 指南支持库 (GSL) 有 `not_null` 指针类型，可以保证传递的指针永远为 `nullptr`。对于目前传递原始指针的 API，这种方法可行吗？

`std::string_view` (C++17) 和 `std::span` (C++20) 是指针/长度对的极佳替代方案。

## 26.1：资源

- [boost::safe_numerics](https://github.com/boostorg/safe_numerics)

# 27：害怕全局状态

推理全局状态很困难。任何非 `const` 的 `static` 值或 `shared_ptr` 都可能是全局状态。永远不知道谁会更新该值，以及这样做是否线程安全。

全局状态会导致微妙且难以追踪的错误：一个函数更改了全局状态，而另一个函数依赖该更改或受到其影响。

| ![](img/leanpub_pencil.png) |

## 练习：全局状态，剩下什么？

如果你完成了之前的练习，你已经将所有的 `static` 变量变成了 `const`。这很好！你可能还将其中一些变为 `constexpr`，那更好！

但你可能仍有全局状态潜伏。你有一个全局单例日志记录吗？日志是否会在系统的模块之间意外共享状态？其他单例呢？可以消除吗？它们是否存在线程初始化问题（如果两个线程尝试首次访问其中一个对象会发生什么）？

## 27.1：资源

- [Retiring the Singleton Pattern - Peter Muldoon - Meeting C++ 2019](https://youtu.be/f46jmm7r8Yg)

# 28：使用更强的类型

考虑 `Rectangle` 的 API：

```text
1 Rectangle(int, int, int, int);
```

定义不当。

这种设计是有问题的，但我们的代码中潜伏着不那么明显的问题。

```text
1 Rectangle(int, int, int, int);
```

图 14. 定义不当的构造函数。

该函数的参数可能是 `(x, y, width, height)`，也可能是 `(x1, y1, x2, y2)`。另一种较小但仍可能的可能是 `(width, height, x, y)`。

你对像 `true` 这样的 API 怎么看？

```text
1 Rectangle(Position, Size);
```

图 15. 强类型构造函数。

在许多情况下，只需花一点精力就能编写出更强类型的 API。

```cpp
 1 struct Position {
 2   int x;
 3   int y;
 4 };
 5 
 6 struct Size {
 7   int width;
 8   int height;
 9 };
10 
11 struct Rectangle {
12   Position position;
13   Size size;
14 };
```

图 16. 更强类型的类型定义。

这可以导致其他在逻辑上可组合的语句，并带有运算符重载，例如：

```cpp
1 // 返回一个通过传入的偏移量
2 // 移动的新矩形
3 Rectangle operator+(Rectangle, Position);
```

图 17. 耦合类型的运算符重载。

| ![](img/leanpub_info-circle.png) |

在某些情况下，使用结构体可能会提高性能 [C++ Weekly Ep 119, Negative Cost Structs](https://youtu.be/FwsO12x8nyM)。

## 28.1：避免布尔参数

本章的预发布读者指出，Steve Maguire 在他的书籍《Writing Solid Code》的第 5 章中提到：“在调用处使代码易于读懂。避免使用布尔参数。”

在 C++11 中，`enum class` 为你提供了一种简单的方法来增加强类型、避免布尔参数并让你的 API 更难被误用。

考虑：

```cpp
1 struct Widget {
2   // 这个构造函数很容易用错，我们
3   // 很容易交换参数
4   Widget(bool visible, bool resizable);
5 }
```

图 18. 不直观的参数顺序。

相比之下：

```cpp
1 struct Widget {
2   enum struct Visible { True, False };
3   enum struct Resizable { True, False };
4 
5   // 仍然可能用错，但困难得多
6   Widget(Visible visible, Resizable resizable);
7 }
```

图 19. 使用作用域枚举的强类型。

| ![](img/leanpub_pencil.png) |

识别你现有代码中存在问题的 API。

你经常以错误的顺序调用哪个函数？该如何修复它？

| ![](img/leanpub_pencil.png) |

## 练习：研究 C++ 的强类型 typedef 库

现有的某些库可以在你创建强类型 `int` 时为你简化一些样板代码。Jonathan Muller、Bjorn Fahller 和 Peter Sommerlad 每人都写了一个，还有其他库供选择。

| ![](img/leanpub_pencil.png) |

## 练习：考虑使用 `=delete` 消除问题的转换

```cpp
1 double high_precision_thing(double);
```

图 20. 简单的函数声明。

如果用 `float` 调用上述函数可能是一个 bug 呢？

```cpp
1 double high_precision_thing(double);
2 double high_precision_thing(float) = delete;
```

图 21. 消除从 `float` 到 `double` 的意外类型提升。

在 C++11 中，任何函数或重载都可以被 `=delete`。

| ![](img/leanpub_pencil.png) |

启用 clang-tidy 的 [Easily Swappable Parameters](https://clang.llvm.org/extra/clang-tidy/checks/bugprone-easily-swappable-parameters.html) 检查。

## 28.2：资源

- [C++ Weekly Ep 107: “The Power of `=delete`”](https://youtu.be/aAvjUU0m6AU)
- [Adi Shavit and Björn Fahller “The Curiously Recurring Pattern of Coupled Types”](https://youtu.be/msi4WNQZyWs)
- 研究“Affine space types”（Affine 空间类型）。
- [C++Now 2017: Jonathan Müller “Type-safe Programming”](https://youtu.be/iihlo9A2Ezw)

# 29：广泛使用 `[[nodiscard]]`

`[[nodiscard]]` 是一个 C++ 属性，它告诉编译器如果在忽略返回值时发出警告。它可以用于函数：

```cpp
1 [[nodiscard]] int get_value();
2 
3 int main()
4 {
5   // 警告，忽略了 [[nodiscard]] 值
6   get_value();
7 }
```

图 22. `[[nodiscard]]` 的示例用法。

以及在类型上：

```cpp
1 struct [[nodiscard]] ErrorCode{};
2 
3 ErrorCode get_value();
4 
5 int main()
6 {
7   // 警告，忽略了 [[nodiscard]] 值
8   get_value();
9 }
```

图 23. 类型上的 `[[nodiscard]]`。

C++20 增加了提供描述的能力。

```cpp
1 [[nodiscard("Ignoring this result leaks resources")]]
```

图 24. 带有描述的 C++20 `[[nodiscard]]`。

```cpp
1 [[nodiscard("Ignoring this result leaks resources")]]
2 Rectangle(Position, Size);
3 size(int size) {
4   if (size < 0) {
5     throw std::invalid_argument("size must be positive");
6   }
7 }
```

- [模块入门指南 - Daniela Engert - Meeting C++ 2019](https://youtu.be/Kqo-jIq4V3I)



- [实战现代 C++ - Daniela Engert - CppCon 2022](https://youtu.be/yUIFdL3D0Vk)
- [所以，你想用 C++ 模块……跨平台吗？ - Daniela Engert - C++ on Sea 2023](https://youtu.be/DJTEUFRslbI)

# 31：一致地导出模块重载

应该使用 C++23 模块（记住忘记头文件的存在这件事），但它们确实为确保你的库能被正确使用引入了新的挑战。

如果你熟悉如何使用 `DLLs` 和显式库导出（通常在 `MSVC` 中需要，但如果你选择在任何操作系统上都不从动态库中导出所有符号，这也是必要的），那么你可能见过像这样的代码：

```cpp
1 EXTERN_DLL_EXPORT int calculate(int input) {
2   return input * 10;
3 }
```

图 32. 简单的库导出示例

如果你导出时不一致，你将得到链接错误：

```cpp
1 // library.hpp
2 [[nodiscard]] constexpr int calculate(int input) {
3   return input * 10;
4 }
5 
6 EXTERN_DLL_EXPORT [[nodiscard]] constexpr int calculate(float input) {
7   return input * 10.1;
8 }
```

图 33. 简单的库错误示例

```cpp
 1 #include "library.hpp"
 2 import std;
 3 
 4 int main()
 5 {
 6   // 这可以通过编译但会产生链接时错误
 7   //（在静态链接阶段或运行时链接阶段）
 8   // 因为 float 重载在编译时找到了
 9   // 但没有为了库的使用而导出
10   std::println("{}", calculate(3));
11 }
```

图 34. 简单的库错误用法示例

C++20 模块为我们带来了一个相似但不同，且可能更隐蔽的问题。

```cpp
 1 // library.ixx
 2 export module library;
 3 
 4 // 我只导出了 float 重载
 5 export [[nodiscard]] constexpr float calculate(float val) noexcept
 6 {
 7   return val * 10.1f;
 8 }
 9 
10 [[nodiscard]] constexpr int calculate(int val) noexcept
11 {
12   return val * 10;
13 }
```

图 35. 部分导出的重载集

```cpp
1 import library;
2 import std;
 3 
 4 int main()
 5 {
 6   // 这可以通过编译和链接且没有警告，但
 7   // 输出 float "30.3" 而不是可能预期的 int "30"
 8   std::println("{}", calculate(3));
 9 }
```

图 36. 部分导出的重载用法

# 32：优先使用栈而非堆

栈对象（局部作用域且未动态分配的对象）对优化器更友好，对缓存更友好，并且可能被优化器完全消除。正如 Björn Fahller 所说过的：“假设任何指针间接都是缓存缺失。”

用最简单的话来说：

```cpp
1 std::string make_string() { return "Hello World"; }
```

图 37. 可以接受主意，使用了栈且可以被优化。

```cpp
1 std::unique_ptr<std::string> make_string() {
2   return std::make_unique<std::string>("Hello World");
3 }
```

图 38. 糟糕的主意，使用了堆。

```cpp
1 void use_string() {
2   // 这个字符串存在栈上
3   std::string value("Hello World");
4 }
```

图 39. 可以接受主意。

```cpp
1 void use_string() {
2   // 字符串存在堆上
3   std::string *value = new std::string("Hello World");
4 }
```

图 40. 极其糟糕的主意，使用了堆并内存泄漏。

记住，`std::string` 本身可能会进行内部分配并使用堆。如果你的目标是完全不使用堆，那么你需要采取其他措施。目标是不产生**不必要的**堆分配。

通常情况下，用 `new` 表达式创建的对象（或通过 `make_unique` 或 `make_shared`）是堆对象，具有**动态存储期**。在局部作用域内创建的对象是栈对象，具有**自动存储期**。

> 对于编译器和工具来说，查找未初始化栈值的读取操作比查找堆值要容易得多。

## 练习：寻找堆的使用

有时具有 C 和 Java 背景的开发者会对此感到困难。对于 Java 来说，是因为创建对象需要 `new`。对于 C 来说，是因为由于语言差异，C 编译器无法执行与 C++ 编译器相同种类的优化。

所以，你的代码中最终出现了一些 `vectors`。

## 练习：运行堆使用检测

有几种工具可以找到潜在的堆使用。

# 33：不要返回原始指针

返回原始指针会让读者思考所有权。是否由我来 `delete` 它？

```cpp
1 int *get_value();
```

图 41. 返回原始指针。

如果你需要所有权，返回 `std::unique_ptr` 或 `std::shared_ptr`。

# 34：了解容器

按以下顺序优先选择容器：

- `std::array`
- `std::vector`

## `std::array`

固定大小栈容器。大小必须在编译时已知，并且你有足够的栈空间来存放数据。这种容器帮助我们优先使用栈而非堆。连续的内存使得 `std::array` 成为“零成本抽象”。

## `std::vector`

动态大小堆容器。虽然编译器不知道数据最终驻留在哪里，但它知道元素在内存中是相邻排列的。连续性为编译器提供了更多优化机会并且缓存友好。

几乎任何其他容器都需要注释和理由。对于小型容器，使用线性搜索的扁平 map 可能比 `std::map` 更好。

但不要对此过于疯狂。如果你需要键查找，使用 `std::map` 并评估它是否具有你需要的性能特性。

## 练习：将 `vector` 替换为 `array`

寻找固定大小的 `vectors` 并尽可能将它们替换为 `array`。有了 C++17 的类模板参数推导，这可以变得更容易。

```cpp
const std::vector<int> data{n+1, n+2, n+3, n+4};
```

图 42. 固定大小数据的 `const std::vector`。

可以变为：

```cpp
1 const std::array<int, 4> data{n+1, n+2, n+3, n+4}; // C++11
2 const std::array data{n+1, n+2, n+3, n+4};         // C++17
```

图 43. 固定大小数据的 `const std::array`。

你已经让这些变成了 `const`，现在如果可能，回去将它们设为 `constexpr`。

## 34.1：资源

- [Bjarne Stroustrup “列表是邪恶的？”](https://www.stroustrup.com/bs_faq.html#list)

# 35：注意自定义分配和 PMR

C++17 添加了多态内存资源（`PMR`），这使得向标准容器添加你自己的自定义分配策略变得异常而而容易。

（遗憾的是，在本书出版时，只有 `GCC` 和 `MSVC` 实现了这一 C++17 特性。）

我**不**建议在代码的任何地方使用 `PMR` 或其他自定义分配策略。如果你遵循了书中的其他规则，这些策略大部分情况下是不需要的。

然而，我认为了解这些策略的存在并是一项最佳实践，它们可以作为工具来限制你对堆的使用，并获得你可能需要的“最后一公里”性能。

一个简单的示例是：

```cpp
 1 import std;
 2 
3 int main() {
 4   //为数据创建栈空间
 5   std::array<std::byte, 2048> stackBuf;
 6 
 7   // 创建 monotonic_buffer_resource
 8   //   * 在所有缓冲区被销毁之前，没有数据会被释放
 9   std::pmr::monotonic_buffer_resource
10     rsrc(stackBuf.data(), stackBuf.size());
11 
12   // 所有的列表节点都在 stackBuf 存储中创建
13   // 不使用任何动态分配
14   std::pmr::list<int> listOfThings{
15     {1,2,3,4,5,6,7,8,9,10,1,2,3,4,5,6,7,8,9,10},
16     &rsrc};
17 }
```

图 44. 简单的 PMR 示例。

C++ 标准提供了几种不同的分配策略，可以与回退机制结合分层，并且很容易创建你自己的。查看关于此主题的 C++ Weekly 播放列表资源。

## 练习：PMR 在你的项目应该处于什么位置？

- 运行堆分析器并寻找多余的堆分配。消除那些你可以消除的。
- 在剩余的热点区域尝试使用 `PMR`，看看它在何处提供帮助。

## 练习：理解数据的“消逝”

- 这是一个高级主题，不适合心脏粗细的人。
- 实际上在 `pmr` 资源内部创建被包含的对象本身是可能的。
- 当你这样做时，如果所有数据都由一个缓冲区资源所有，则可能安全地避免调用所有析构函数。
- 花些时间[欣赏这个概念](https://github.com/lefticus/cpp_weekly/blob/master/PMR/performance_tests.cpp#L259-L274)。

## 35.1：资源

- [C++ Weekly PMR 播放列表](https://www.youtube.com/playlist?list=PLs3KjaCtOwSYXK0avDSF)
- [编译器支持矩阵 cppreference](https://en.cppreference.com/w/cpp/support/17)

# 36：约束你的模板参数

概念（Concepts）相比 `SFINAE`，将带来更好的错误信息（最终）和更好的编译时间。而且代码远比 `SFINAE` 可读性得多。

如果我们继续构建我们的 `divide` 示例，可以从优先使用 `if constexpr` 优替 `SFINAE` 章节获取这个 `if constexpr` 版本。

```cpp
 1 import std;
 2
3 template <typename Numerator, typename Denominator>
 4 [[nodiscard]] constexpr auto divide(Numerator, Denominator)
 5 nominator) {
 6   if constexpr (std::integral_v<Numerator> &&
 7                 std::integral_v<Denominator>) {
 8     // 是整数除法
 9     if (denominator == 0) {
10     throw std::runtime_error("divide by 0!");
11     }
12   }
13   return numerator / denominator;
14 }
```

图 45. `divide` 函数的 `if constexpr` 版本。

我们可以使用概念将其重新拆分为两个函数。概念可以在不同的上下文中使用。这个版本使用了简单的 `requires` 子句。

```cpp
 1 import std;
 2
3 template <typename Numerator, typename Denominator>
 4 [[nodiscard]] constexpr auto divide(Numerator, Denominator)
 5 nominator) requires
 6        (std::integral_v<Numerator>
 7         && std::integral_v<Denominator>) {
 8   // 是整数除法
 9   if (denominator == 0) {
10     throw std::runtime_error("divide by 0!");
11   }
12   return numerator / denominator;
13 }
14
15 template <typename Numerator, typename Denominator>
16 [[nodiscard]] constexpr auto divide(Numerator, Denominator)
17 nominator) {
18   return numerator / denominator;
19 }
```

图 46. `requires` 子句中的概念。

这个版本将概念作为函数参数。C++20 甚至有一个“`auto` 概念”，它是一个隐式模板函数。

```cpp
1 import std;
 2
3 [[nodiscard]] constexpr auto divide(std::integral auto numerator,
 4             std::integral auto denominator) {
 5   // 是整数除法
 6   if (denominator == 0) {
 7     throw std::runtime_error("divide by 0!");
 8   }
 9   return numerator / denominator;
10 }
11
12 [[nodiscard]] constexpr auto divide(auto numerator, auto denominator) {
13   // 是浮点除法
14   return numerator / denominator;
15 }
```

图 47. 简洁的概念语法。

概念可以定义复杂的需求，包括预期的成员。本节几乎没有触及这些可能性。

## 练习：理解 C++20 提供了哪些概念

像往常，`cppreference` 通过[提供概念列表](https://en.cppreference.com/w/cpp/concepts)来帮助。

## 练习：创建你自己的概念

这个示例是否给了你一些想要但 `<concepts>` 未提供的概念想法？

查看 [cppreference 上非常简单的 `integral` 概念](https://en.cppreference.com/w/cpp/concepts/integral)，看看它是否激发了你的灵感。

## 36.1：资源

- [C++ Weekly Ep 194：从 SFINAE 到 C++20 概念](https://youtu.be/dR64GQb4AGo)
- [C++ Weekly Ep 196：什么是 requires](https://youtu.be/tc0hVIOJk_U)

# 37：理解 `consteval` 和 `constinit`

我已经鼓励你使用 `constexpr`。C++20 添加了 `consteval` 和 `constinit`，理解它们的作用很重要。

## 变量声明

- `consteval int x = /**/` 无效，`consteval` 适用于函数。
- `constexpr int x = /**/` 声明一个在编译期可用的常量，并在需要时在编译期进行评估。
- `static constexpr int x = /**/` 声明一个在编译期可用的常量，并在编译期进行评估。
- `constinit int x = /**/` 无效。
- `static constinit int x = /**/` 声明一个非常量值（即可变的），该值在编译期不可用，但在编译期会被评估。

## 函数声明

- `consteval int func(int)`：声明一个**必须**在编译期进行评估的函数。
- `constexpr int func(int)`：声明一个**可以在**编译期调用的函数。
- `constinit int func(int)` 无效，`constinit` 适用于变量。

## 练习：讨论用户定义字面量是否应该是 `consteval`

讨论是否存在某些时刻用户定义字面量**不应该**是 `consteval`？

用户定义字面量提供了将字面量转换为另一种类型的快捷方法。



标准库提供了许多不同的用户定义字面量。两个显著但不同的是针对[`std::string`](https://en.cppreference.com/w/cpp/string/basic_string/operator%22%22s)和[`std::string_view`](https://en.cppreference.com/w/cpp/string/basic_string_view/operator%22%22sv)的。

```cpp
import std;

int main(const int argc, const char *[]) {
  using std::literals::string_literals;
  using std::literals::string_view_literals;

  // 目前标准库提供的 s 字面量
  // 不是 consteval。它应该是这样的吗？
  const auto my_string
    = "Hello World"s; // 创建了一个字符串

  // 目前标准库提供的 sv 字面量
  // 不是 consteval。它应该是这样的吗？
  const auto my_string_view
    = "Hello World"sv; // 创建了一个 string_view
}
```

图 48：`consteval` UDL

![图片](img/image)

## 练习：如果函数必须在编译时调用意味着什么？

```cpp
consteval int get_value(const int input) {
  return input * 42;
}

int main(const int argc, const char *[]) {
  // 这段代码能编译吗？
  const auto value = get_value(argc);
}
```

图 49：`consteval` 练习

## 37.1：资源

- [Andreas Fertig 的博客：“consteval 的一个小妙用”](https://andreasfertig.blog/2021/07/cpp20-a-neat-trick-with-consteval/)
- [C++ Weekly 第 304 期：“C++23 的 `if consteval` 对比 C++20 的 `is_constant_evaluated` 对比 C++17 的 `if constexpr`”](https://youtu.be/AtdlMB_n2pI)
- [C++ Weekly 第 308 期：“`if consteval` - 还有更多故事”](https://youtu.be/y3r9l3LZi)

# 38：优先使用飞船运算符（Spaceships）

C++20 可以为你生成任何比较运算符（因其形状，口俗被称为“飞船运算符”）。

- 如果你定义了`==`，编译器会自动生成`!=`。
- 如果你定义了`<=>`，编译器将生成所有其他比较（`==`和`!=`除外）。
- 你可以显式地对任何比较操作使用默认。

```cpp
struct MyData {
  int i;
  int j;

  // 提供所有比较运算符
  friend auto operator<=>(const MyData &, const MyData &) = default;
};
```

图 50：基础飞船运算符示例

C++ 标准已经开始弃用显式的比较操作，请参考标准中的示例。

注意，为了性能考虑，`std::string`实现了自定义的`operator==`（提供`==`和`!=`）和`operator<=>`（提供剩余比较）。

<https://en.cppreference.com/w/cpp/string/basic_string/operator_cmp>

![图片](img/image)

如果你为你的类型提供了自定义的`operator<=>`，编译器将不会为你提供`operator==`或`operator!=`！这类似于针对特殊成员函数的“零之规则”和“五之规则”。

- 如果你提供了自定义的`operator<=>`，你必须提供自己的`operator==`。
- 如果你需要自定义的`operator<=>`，那么显式默认的`operator==`可能无法完成正确的工作。

![图片](img/image)

## 练习：实现飞船运算符

```cpp
import std;

struct Container {
  // 固定容量的容器
  std::array<int, 10> data;

  // size 是当前使用的元素数量
  std::size_t size;

  // 比较运算符应该什么样子的？
  // 默认的有效吗？
  // 我们需要自定义的 operator== 吗？
};
```

图 51：飞船运算符练习

## 38.1：资源

- [cppreference.com 文档](https://en.cppreference.com/w/cpp/language/default_comparisons)

# 39：遵循零之规则（Rule of 0）

在正确的情况下，没有析构函数总是更好的。空析构函数会破坏性能：

- 它们使类型不再是平凡的（trivial）。
- 没有功能性用途。
- 可能会影响析构的联动。
- 隐式禁用移动操作。

![图片](img/image)

如果你因为进行资源管理或定义带有虚函数的基类而需要析构函数，那么你需要遵循五之规则。

如果你提供了自定义的删除器，`std::unique_ptr`可以帮助你应用零之规则。

![图片](img/image)

## 练习：在你的代码中寻找违反零之规则的行为

寻找类似这样的代码（我保证你能找到）：

```cpp
struct S {
  // 一堆
  ~S();
};
```

图 52：空析构函数。

```cpp
struct S {
  ~S();
};
```

图 53：空析构函数。

![图片](img/image)

存在析构函数吗？如果有，请删除它们。

![图片](img/image)

## 练习：使用零之规则

```cpp
struct S {
  // 一些
  ~S();
};
```

图 54：零之规则

```cpp
struct S {
  // 没有影响
  ~S() = default;
};

void some_func(std::vector<S>);
```

## 练习：在代码中寻找违反“五规则”的区域

当你在定义特殊成员函数时，现有的代码中可能没有提供一致的生命周期语义。为了评估其影响，你可以快速对任何缺失的特殊成员函数使用`= delete;`并查看哪些部分会报错。

## 40.1：资源

- [C++ 参考文档：三规则/五规则/零规则](https://en.cppreference.com/w/cpp/language/rule_of_three)

# 第四部分：代码实现指南

# 41：不要复制粘贴代码

如果你发现自己正准备选择一段代码并复制它：停下！

后退一步，重新审视这段代码。

- 你为什么要复制它？
- 源代码和目标代码有多相似？
- 将其封装成函数有意义吗？
- 记住，不要害怕模板。

我发现，这个简单的规则对我的代码质量产生了最直接的影响。

如果粘贴操作的结果是进入当前函数，请考虑使用 lambda。

C++14 风格的 lambda 带有泛型（即`auto`）参数，为你提供了一种简单易用的创建复用代码的方法，可以与不同的数据类型共享，而无需处理`template`语法。

## 练习：尝试 CPD（重复代码检测）

有几种不同的复制粘贴检测工具可以查找代码库中的重复代码。

对于此练习，请下载 [PMD CPD 工具](https://pmd.github.io/latest/pmd_userdocs_cpd.html) 并在你的代码库上运行。

如果你使用 Arch Linux，可以通过 AUR 安装此工具。包名是`pmd`；工具名是`pmd-cpd`。

你能识别出代码中被复制粘贴的关键部分吗？如果你在其中一个版本中发现了 bug 会发生什么？你能确定会看到所有同样需要更新的地方吗？

## 41.1：资源

- [复制粘贴编程](https://www.viva64.com/en/t/0068/)
- [最后一行效应](https://www.viva64.com/en/b/0260/)
- [我不会复制粘贴代码](https://twitter.com/bjorn_fahller/status/1072432257799987200)

# 42：优先使用`format`而非`iostream`或 C 格式化函数

C++20 添加了`<format>`头文件，提供了`std::format`函数。

`std::format`接收字符串、参数并返回一个`std::string`对象。

`format`的优点是：

- 编译比 iostreams 快。
- 执行比 iostreams 快。
- 比 iostreams 更具可读性。
- 比`printf`系列函数更类型安全。

```cpp
1 import std;
2 
3 int main()
4 {
5   const auto result = std::format("Hello {}!", "Jason");
6 }
```

图 57：简单的 format 使用

遗憾的是，C++20 的用例非常有限，以格式化为字符串为主机制，我们往往会写出这样的代码：

```cpp
1 // 使用 include 是因为这是 C++20
2 #include <format>
3 
4 int main()
5 {
6   std::cout << std::format("Hello {}!\n", "Jason");
7 }
```

图 58：format 使用

为了解决这个问题，C++23 添加了`<print>`头文件，我们可以通过模块使用它。

```cpp
1 import std;
2 
3 int main()
4 {
5   std::println("Hello {}!", "Jason");
6 }
```

图 59：使用`std::println`

`std::print`有多个重载版本，辅助函数`std::println`会在消息末尾自动添加换行符。

这个例子过于复杂了！

```cpp
1 import std;
2 
3 int main()
4 {
5   std::print(std::cout, "Hello");
6   std::println(stdout, " World");
7 }
```

图 60：使用`std::print`的重载

## 练习：学习`std::print`的语法并开始将`std::cout`转换为`print`

## 练习：使用`clang-tidy`的`modernize-use-print`升级你拥有的任何`printf`系列函数

# 43：`constexpr`掌控一切！

在定义特殊成员函数时，你可能没有提供一致的生命周期语义。为了评估其影响，你可以快速对任何缺失的特殊成员函数使用`= delete;`并查看哪些部分会报错。

`static`变量比我以前任何时候更有理由使用`constexpr`。

C++23 和模块的结合消除了几乎所有使用`static`的理由。

在模块头文件中，`constexpr`应该成为默认值。

- 在模块中，尽可能多地在编译时计算（`constexpr`）。
- `constexpr`开启了我们尚未考虑的用例。
- 只要是`static`，尽可能在编译时计算。
- 标准库技术需要`constexpr`开启。

当你看到类似这样的内容时（我在真实代码中看到的）：

```cpp
1 static const std::vector<int> angles{-90,-45,0,45,90};
```

图 61：`static const`在编译时已知

这真的应该是：

```cpp
1 static constexpr std::array angles{-90,-45,0,45,90};
```

图 62：将`static const`转换为`static constexpr`

`static constexpr`在这里是必要的，确保对象不会在每次调用时重新初始化。使用`static`变量在整个程序生命周期内存在，且我们知道它会被初始化一次。

这种差异体现在：

- 数组的大小现在在编译时已知。
- 我们消除了动态分配。
- 我们不再需要访问静态的对象。

对于头文件中的全局变量，优先使用`inline constexpr`而非`static constexpr`，这样链接器可以合并数据结构并减少代码膨胀。

主要的收益来自前两者，但我们需要`constexpr`思维来寻找这种机会。我们还需要`constexpr`知识来了解如何在更复杂的情况下应用它。

有时，非静态`constexpr`局部变量是最有效的选项，因为数据存储在栈上而不是二进制文件的其他部分。在你的优化阶段检查这是否重要。

技术上，非静态`constexpr`变量并不非要在编译时计算。然而，它们几乎确定是在编译时计算的，将它们认为是在编译时计算是有用的。

## 练习：`constexpr`你的`const`值

阅读代码时，查看所有的`const`值。问：“这个值在编译时已知吗？”如果是，需要什么才能让值变为`constexpr`？

## 练习：`static constexpr`你的`static const`

遍历你当前的代码库，寻找目前为`static const`的代码。你可能在某处有一些。

- 如果目前是`static const`，可能大小和数据在编译时已知。
- 这段代码可以变成`constexpr`吗？
- 什么阻止了它变成`constexpr`？
- 修改填充`static const`数据的函数需要多少工作量，以便它们也成为`constexpr`？
- 请记住，如果它是头文件中的全局变量，你应该优先使用`inline constexpr`。

## 练习：让头文件代码转为`constexpr`

如果你已经在头文件中定义了函数和类型，尝试让这些函数和类型完全启用`constexpr`属性。

## 练习：将头文件中定义的`constexpr`函数移动到模块接口文件中

我们希望避免继续重复解析`constexpr`函数，而模块接口文件为我们提供了这种方法。

## 练习：寻找额外的非 IO 函数并转为`constexpr`

在学习旅程的这个阶段，基本上任何非 IO 函数都可以转变为`constexpr`函数。

- 将这些函数移动到你的模块接口文件中。
- 将函数标记为`constexpr`。

## 43.1：资源

- [C++Now 2017：Ben Deane & Jason Turner “`constexpr`全面体”](https://youtu.be/HMB9oXFobJc)（与现代`constexpr`技术相比稍显过时）
- [C++ Weekly Ep 233：`constexpr` map vs `std::map`](https://youtu.be/INn3xa4pMfg)
- [Meeting C++ 2017：Jason Turner “实用的`constexpr`”](https://youtu.be/xtf9qkDTrZE)
- [C++ Russia 2019：Hana Dusíková “编译期正则表达式的状态”](https://youtu.be/r_ZASJFQGQI)




# C++ 核心准则：现代 C++ 实践深度指南

## 44: 让头文件中的全局变量变为 `inline constexpr`

1. 畏惧全局状态！
2. 忘记头文件的存在吧！

所有全局数据都应该是 `constexpr` 的。

但全局 `constexpr` 值是完全安全的。它们不会变化，也不会影响“远处的神秘作用”。

如果你还没有完全迁移到模块（modules），仍然在使用头文件……

所有的全局 `constexpr` 值都应该是 `inline constexpr`。

在模块接口内部，`constexpr` 全局变量和 `inline constexpr` 全局变量都具有“外部链接”（external linkage），所以我们不需要担心这个问题。

```
1 // my_library.hpp
2 
3 // 对象 `dataset` 将在包含该 .hpp 文件的每个 .cpp
4 文件中重复
5 static constexpr auto dataset = make_data();
```

图 63. static constexpr 示例

```
1 // my_library.hpp
2 
3 // 对象 `dataset` 在整个二进制文件中存在一次
4 inline constexpr auto dataset = make_data();
```

图 64. inline constexpr 示例

## 45: 对所有非 `constexpr` 的内容使用 `const`

许多人（如 Kate Gregory 和 James McNellis）已经多次说过这一点。将对象标记为 `const` 可以起到两个作用：

1. 它强制我们思考对象的初始化和生命周期，这会影响性能。
2. 向代码的阅读者传达语义。

顺便提一下，如果是静态对象，编译器现在可以自由将其移动到二进制文件的常量部分，这会影响优化器。

### 练习：寻找 `const` 机会

在阅读代码时，你应该寻找不是 `const` 的变量并将它们设为 `const`。

* 如果一个变量不是 `const`，问问为什么不是？
* 使用 lambda 或添加命名函数是否可以让你让该值变为 `const`？

```
1 const auto data = [](){ // 无参数
2   std::vector<int> result;
3   // 用某些内容填充 result。
4   return result;
5 }(); // 立即调用
```

图 65. 使用 lambda 初始化 `const` 值

使用 lambda 或添加命名函数是否可以让你让该值变为 `const`？

由于 RVO（返回值优化），使用 lambda 可能会提高性能。

然而，需要注意的是，值的 `constexpr` 可能是脆弱的。

```
1 ReturnType some_function(int value)
2 {
3   // 如果结果的类型不同
4   // 且存在隐式转换，你会得到
5   // 隐式移动。
6   // 如果它们相同，则保证
7   // 应用去 constexpr 化
8   const auto result = get_value(42);
9   return result;
10 }
```

图 66

```
1 ReturnType some_function(int value)
2 {
3   // 如果结果的类型不同
4   // 且存在隐式转换，你会得到
5   // 隐式移动。
6   // 如果它们相同，则保证
7   // 应用去 constexpr 化
8   return get_value(42);
9 }
```

图 67. 优先不要为临时变量命名

clang-tidy 的 [No Move](https://clang.llvm.org/extra/clang-tidy/checks/performance-automatic-move.html) 分析在很大程度上是失效的。它在 `constexpr` 适用时也会警告，而在需要的地方却不警告。参见此分析：[`compiler-explorer.com/z/a476nb`](https://compiler-explorer.com/z/a476nb)。

你可能不想让 `class` 成员成为 `const`；这会破坏移动语义等基本功能。

## 46: 始终初始化你的非 const、非 auto 值

理想情况是将所有内容 `const`，这会强制你进行初始化。然而，并非总是可行。同样，如果你使用 `auto`，你会被强制初始化对象。

* 编译器将“丢弃”对未初始化值的操作
* 确保启用了 `-Wunitialized` 类的警告

请注意，在某些情况下，默认初始化与看似空的初始化之间存在差异。

编译器并不总是能完美捕捉未初始化值的使用。例如，GCC（截至 2023-12-30）需要开启优化才能捕捉这种未初始化变量的访问，这是未定义行为（UB）。

```
#include <span>

float sum(std::span<float> values)
{
  float result;

  for (const auto f : values) {
    result += f;
  }

  return result;
}
```

图 68. 在未开启优化时 GCC 无法捕捉的未初始化变量读取

### 练习：理解你正在调用哪个构造函数

获取此示例代码并在 compiler-explorer.com 中以不同的优化级别进行调试，以理解每次构造函数调用可能执行的差异。

```
import std;

int main()
{
  // std::string is not trivially constructible, so this calls
  // the default constructor and it is initialized to ""
  std::string str;

  // explicitly call the default constructor
  std::string str2{};

  // call the constructor that takes a `const char *`
  // try commenting this out as you play with various
  // optimization levels
  std::string str3 = "";
}
```

图 69. 调用了哪个构造函数？

### 练习：确保 `-Wuninitialized` 未禁用，并认真对待它

#### 46.1: 工具

* [Valgrind 的 Memcheck](https://www.valgrind.org/info/tools.html#memcheck)
* [Dr Memory](https://dynamorio.org/drmemory_docs/page-uninit.html)

#### 46.2: 资源

* [C++ Weekly - Ep 257 - 垃圾进，垃圾出 - 为什么初始化很重要](https://youtu.be/uYN6-YQPsGo)
* [COVID-19 研究与未初始化变量](https://www.viva64.com/en/b/0796/)
* [Windows 中的图像解析模糊测试，第二部分：未初始化内存](https://www.fireeye.com/blog/threat-research/2021/03/fuzzing-image-parsing-in-windows-uninitialized-memory.html)

## 47: 在许多情况下优先使用 `auto`

我不是一个几乎总是自动（AAA）支持者，但让我问你这个问题：`std::count` 的结果类型是什么？

我的答案是，“我不在乎。”

```
const auto result = std::count( /* stuff */ );
```

图 70. `const auto`

或者，如果你喜欢的话：

```
auto const result = std::count( /* stuff */ );
```

图 71. `auto const`

使用 `auto` 可以避免不必要的转换和数据丢失。与范围循环（ranged-for loops）一样。`auto` 需要初始化，与 `const` 一样，其理由也是相同的。

```
auto i; // 无法编译
auto i = int; // 无法编译
```

图 72. auto 需要初始化

示例：

```
const std::string value = get_string_value();
```

图 73. 可能的昂贵转换

`get_string_value()` 的返回类型是什么？如果它是 `std::string_view` 或 `const char *`，我们将在所有编译器上获得一个潜在的昂贵转换，且没有任何诊断提示。

```
// 避免转换
const auto value = get_string_value();
```

图 74. 没有可能性的昂贵转换

此外，`auto` 返回类型实际上可以显著简化泛型代码。

```
// 我们来自“不要害怕模板”的示例
template<typename Arithmetic>
Arithmetic divide(Arithmetic numerator, Arithmetic denominator) {
  return numerator / denominator;
}
```

图 75. C++ 98 模板用法

这段代码迫使我们对分子和分母使用相同的类型（尝试这样操作并看看你会得到的奇怪的编译错误）。

```
template<typename Numerator, typename Denominator>
/* 返回类型是什么？ */
divide(Numerator numerator, Denominator denominator) {
  return numerator / denominator;
}
```

图 76. 让 C++ 98 模板更具通用性？

C++98 没有为这个问题提供解决方案，但 C++11 有。

```
// 使用尾随返回类型
template<typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator)
  -> decltype(numerator / denominator)
{
  return numerator / denominator;
}
```

图 77. C++11 尾随返回类型

但在 C++14 中，我们可以完全省略返回类型（记得跳过 C++11）。

```
template<typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator)
{
  return numerator / denominator;
}
```

图 78. C++14 `auto` 返回类型

在 C++20 中，我们可以通过 `auto` 函数参数进一步简化这段代码（它为我们创建了隐式模板）。

```
auto divide(auto numerator, auto denominator)
{
  return numerator / denominator;
}
```

图 79. C++20 `auto` 参数

如果这对你的应用程序有意义，考虑对这些参数进行约束。

```cpp
// 这应该是 constexpr 且带有 [[nodiscard]]
std::floating_point auto divide(
    std::floating_point auto numerator, std::floating_point auto denominator)
{
  return numerator / denominator;
}
```

图 80. 约束参数

### 练习：熟悉 `auto`

```
const int();

main() {
  auto val = get();
}
```

## 48: 使用范围（Ranges）和视图（Views）提高正确性和可读性

在最好情况下，C++20 范围和视图可以在不影响性能或编译时间的情况下极大提高代码的可读性。

在最坏的情况下，C++20 范围和视图可能会增加编译时间并影响代码的可读性。

由于某些缺点，有些人建议永远不要使用。本书没有那样建议。相反，我们应该学习它们的优缺点。

作者认为“遍历第一个元素之外的所有元素”这一简单用例是范围和视图的“杀手级特性”。

```
void print_all_but_first(const std::vector<int> &values) {
  // 忘记这个在 0 个元素时会产生未定义行为（UB）
  if (values.empty()) { return; }

  for (auto itr = next(begin(values)); itr != end(values); ++itr) {
    std::println("{}", *itr);
  }
}
```

图 87. 不使用范围

```cpp
void print_all_but_first(const std::vector<int> &values) {
  for (const auto val : values | std::views::drop(1)) {
    std::println("{}", val);
  }
}
```

图 88. 使用范围

除了范围库更复杂且可组合的功能外，请注意这些非常简单但强大的用例。

### 练习：阅读 [`en.cppreference.com/w/cpp/ranges`](https://en.cppreference.com/w/cpp/ranges) 可用的视图集

### 练习：使用 [compiler explorer](https://compiler-explorer.com) 在不同的优化级别对比上述两个函数

* [C++ Weekly - Ep 399 - C++23 的 slide_view vs adjacent_view](https://youtu.be/czmGjH16Hb0)
* [C++ Weekly - Ep 401 - C++23 的 chunk view and stride view](https://youtu.be/3ZeV-F1Rbaw)
* [Effective Ranges: 使用 C++2x Ranges 的教程 - Jeff Garland - CppCon 2023](https://youtu.be/QoaVRQvA6hI)

## 49: 不要复用视图（Views）

范围视图（Range views）可能会以意想不到的方式持有状态，从而导致意料之外的代码评估。

```cpp
import std;

int main()
{
    std::list<int> values{1,2,3,4,5,6,7,8,9};

    auto drop_2 = values | std::views::drop(2);

    std::println("{}", drop_2);

    values.erase(values.begin());

    std::println("{}", drop_2);
}
```

图 89. `drop` 的复用，带有缓存效应

你可能会惊讶地发现上述代码打印了：

```
> 3, 4, 5, 6, 7, 8, 9
> 3, 4, 5, 6, 7, 8, 9
```

图 90. 使用 `list` 的 `drop` 输出复用

然而，如果我们将代码更改为使用 `std::vector`，就会得到预期的输出。




```cpp
 1 import std;
 2 
 3 int main()
 4 {
 5     std::vector<int> values{1,2,3,4,5,6,7,8,9};
 6 
 7     auto drop_2 = values | std::views::drop(2);
 8 
 9     std::println("{}", drop_2);
10 
11     values.erase(values.begin());
12 
13     std::println("{}", drop_2);
14 }
```

图 91. `drop` 的复用，没有缓存效应。

```
1 > 3, 4, 5, 6, 7, 8, 9
2 > 4, 5, 6, 7, 8, 9
```

图 92. 使用 `vector` 的 `drop` 输出复用。

有些人会告诉你，由于这类问题的存在，应该完全避免使用视图。

我们将采取一种更审慎的方法。

不要复用视图！

解决这个问题的相对简单的方案：

```cpp
 1 import std;
 2 
 3 int main()
 4 {
 5     std::list<int> values{1,2,3,4,5,6,7,8,9};
 6 
 7     auto drop_2 = []{ return values | std::views::drop(2); };
 8 
 9     std::println("{}", drop_2());
10 
11     values.erase(values.begin());
12 
13     std::println("{}", drop_2());
14 }
```

图 93. 使用 `lambda` 创建视图。

## 49.1：资源

- [Denver C++ Meetup: 2023-04 - Tyler Weaver - 阅读 Ranges（不要听我的）](https://youtu.be/H-CMApmuBoQ)
- [关于 C++ Ranges 的 Belle Views、其细节与魔鬼 - Nico Josuttis - Keynote Meeting C++ 2022](https://youtu.be/O8HndvYNvQ4)

# 50：优先使用算法而非循环

算法传达含义并帮助我们应用“万物皆 `const`”规则。在 C++20 中，我们获得了范围（ranges），这使得算法使用起来更加舒适。

通过函数式方法并使用算法，我们写出读起来像句子一样的 C++ 代码。

```cpp
1 const auto has_value 
2   = std::any_of(container, greater_than(12));
```

图 94. 带有范围的算法。

```cpp
1 const auto has_value 
2   = std::any_of(begin(container), end(container), 
3                 greater_than(12));
```

图 95. 带有显式迭代器的算法。

注意，在某些[少数情况](https://sourceforge.net/p/cppcheck/wiki/ListOfChecks/)下，你的静态分析工具可能会建议使用某种算法。

## 练习：研究现有循环

下次当你阅读代码库中的循环时，请对照 [C++ `<algorithm>` 头文件](https://en.cppreference.com/w/cpp/algorithm) 进行交叉引用，并尝试寻找可以应用的算法。

本书仅提到了 C++20 范围。截至本书出版时，编译器才开始支持范围。范围可以组合，并且对 `constexpr` 有完全支持。

## 50.1：资源

- [GoingNative 2013: Sean “C++ Seasoning”](https://channel.msdn.com/Events/GoingNative/2013/Seasoning)
- [CppCon 2018: Jonathan Boccara “一小时内的 105 种算法”](https://youtu.be/olsf6IkU)
- [C++ Now 2019: Conor Hoekstra “算法直觉”](https://youtu.be/48gV1SNmWA)
- [MeetingC++ 2019: Conor Hoekstra “更好的直觉”](https://youtu.be/TSZzvohtTQ)
- [Conor Hoekstra “双胞算法”](https://www.youtube.com/live/iferBv3s)
- [C++ Weekly Ep 187 “C++20 的 `constexpr` 算法”](https://youtu.be/9YWzSronY)
- [C++ Weekly Ep 105 “现代”C++ 5：循环与算法](https://youtu.be/A0-xDjeyQ)
- [算法选择](https://codereport.github.io/Algorithm-Selection/)

# 51：当视图和算法无法帮助时使用范围循环

（谨慎地）优先使用范围、视图和算法，但在此处使用范围循环。

```cpp
1 for (int i = 0; i < container.size(); ++i) {
```

图 96. 类型不匹配。

```cpp
1 for (auto itr = container.begin();
2      itr != container.end();
3      ++itr) { 
```

图 97. 循环时的类型不匹配。

```cpp
1 for (const autoelement) {
2   // 示例
 }
```

图 98. 范围循环示例。

## 练习：现代化你的循环

你的代码中可能存在旧式循环。

1. 应用 `clang-tidy` 的 `modernize-loop-convert` 检查。
2. 寻找可以转换的循环。
   - 可以转换的循环可能有 bug。
   - 可以转换但没有 bug 的循环是良好的候选。

## 51.1：资源

- [clang-tidy modernize-loop-convert](https://clang.llvm.org/extra/clang-tidy/checks/modernize-loop-convert.html)

# 52：在范围为循环中使用 `auto`

不使用 `auto` 可能会让代码更容易出现意外错误。

```cpp
1 for (const int value : container_of_double) {
2   // 意外转换，可能的警告
 }
```

图 99. 意外转换。

```cpp
1 for (const base value : container_of_derived) { 
2   // 意外切割
 }
```

图 100. 意外切割。

```cpp
1 for (const auto &value : container) {
2   // 没有问题
```

图 101. 没有问题。

优先：

- `const &` 用于非修改性循环。
- `auto &` 用于修改性循环。
- `auto &&` 仅当你需要处理 `std::vector<bool>` 等特殊类型，或从容器中移动元素时。

## 练习：理解 `std::map` 和范围为循环

理解这段代码在做什么。它在拷贝吗？为什么？如何？

```cpp
1 std::map<std::string, int> get_map();
2 
3 using element_type = std::pair<std::string, int>;
4 
5 for (const element_type & : get_map())
6 {
7 }
```

图 102. 意外拷贝？现代编译器可以直接捕捉上述问题，但你必须开启警告才能看到它！

# 53：在 `switch` 语句中避免 `default`

这个问题最好通过一系列示例来描述。从这一个开始：

```cpp
 1 enum class Values {
 2   val1,
 3   val2
 4 };
 5 
6 [[nodiscard]] constexpr std::string_view get_name(Values value) {
 7   switch (value) {
 8   case Values::val1: return "val1";
 9   case Values::val2: return "val2";
10   }
11 }
```

图 103. 带有警告的 `switch`。

如果你开启了所有的警告，那么你可能会在这里得到一个“并非所有代码路径都返回返回值”的警告。这在技术上是正确的。我们可以调用 `get_name(static_cast<Values>(15))` 且不会违反 C++ `[dcl.enum/5]` 的任何部分，除了函数未返回值导致的未定义行为（Undefined Behavior）之外。

你可能会忍不住想像这样修复这段代码：

```cpp
 1 enum class Values {
 2   val1,
 3   val2
 4 };
 5 
 6 [[nodiscard]] constexpr std::string_view get_name(Values value) {
 7   switch (value) {
 8   case Values::val1: return "val1";
 9   case Values::val2: return "val2";
10   default: return "unknown";
11   }
12 }
```

图 104. 使用 `default` 的 `switch` 以避免警告。

但这引入了一个新问题：

```cpp
 1 enum class Values {
 2   val1,
 3   val2,
 4   val3 // 添加了一个新值
 5 };
 6 
 7 [[nodiscard]] constexpr std::string_view get_name(Values value) {
 8   switch (value) {
 9   case Values::val1: return "val1";
10   case Values::val2: return "val2";
11   default: return "unknown";
12   }
13   // 编译器没有对 `val3` 未被处理进行诊断
14 }
```

图 105. 未处理的情况。

相反，优于如下代码：

```cpp
 1 enum class Values {
 2   val1,
 3   val2,
 4   val3 // 添加了一个新值
 5 };
 6 
 7 [[nodiscard]] constexpr std::string_view get_name(Values value) {
 8   switch (value) {
 9   case Values::val1: return "val1";
10   case Values::val2: return "val2";
11   } // 现在会产生枚举值未处理的警告
12 
13   return "unknown";
14 }
```

图 106. 优选版本。

在上面的示例中，你不应该得到“不可达代码”的警告，因为`有效值范围`几乎总是大于你定义的值。

一些现代工具可以为你检测出这些对 `default` 的使用。

## 练习：寻找 `default:`

你在代码库中发现了什么？在之前的练习中开启警告是否已经为你发现了对 `default:` 的使用？

## 练习：考虑 `std::unreachable`

`std::unreachable`（在 C++23 中添加）在被执行时会显式地触发未定义行为。它可以被用于 `switch` 语句的“不可达”情况，以确保编译器执行最优操作。

这可能是令人生畏的。你真的想要因为代码“不可能”被到达而使用未定义行为吗？与你的同事讨论这一点，并考虑你在何处、何时以及是否使用这个工具。更多信息请参见资源中的 C++ Weekly 剧集。

## 53.1：资源

- [CppCon 2018: Jason Turner “Applied Best Practices”](https://youtu.be/DHOlsEd0eDE)
- [C++ Weekly - Ep 393 - C++23’s `std::unreachable`](https://youtu.be/ohMyb4jPIAQ) [`-Wswitch-enum`](https://clang.llvm.org/docs/DiagnosticsReference.html#wswitch-enum)
- [`-Wswitch`](https://clang.llvm.org/docs/DiagnosticsReference.html#wswitch)

# 54：优选作用域枚举

C++11 引入了作用域枚举，旨在解决从 C 继承的 `enum` 的许多问题。

```cpp
 1 enum Choices {
 2   option1 // 在全局作用域
 3 };
 4 
 5 enum OtherChoices {
 6   option2
 7 };
 8 
 9 int main() {
10   int val = option1; //
12 }
```

图 107. C98 的 `enum`。

- `enum Choices;`
- `enum OtherChoices;`

这两个很容易混淆，因为它们位于全局命名空间。

- `enum Choices;`
- `enum OtherChoices;`

作用域枚举的值是有作用域的且强类型的。

```cpp
 1 enum class Choices {
 2   option1
 3 };
 4 
 5 enum class OtherChoices {
 6   option2
 7 };
 8 
 9 int main() {
10   int val = Choices::option1;
11   int val2 = OtherChoices::option2;
12 }
```

图 108. C++11 的作用域。

枚举的标识符现在是有作用域的。

## 练习：`enum` 或 `class`

决定使用 `enum` 还是 `class`，迁移到作用域枚举可能会发现 bug！

## 54.1：资源

- [CppCon 2018: Victor Ciura “Better Tools”](https://youtu.be/4X_0)
- [Enumeration](https://en.cppreference.com/w/enum)

# 55：优选 `if constexpr` 比 SFINAE

SFINAE 意味着如果函数编译失败，它将从重载解析中移除。

如果我们要在除法上添加不同的行为，在 C++17 之前，我们会使用 SFINAE：

```cpp
 1 #include <stdexcept>
 2 #include <type_traits>
 3 #include <utility>
 4 
 5 template <typename Numerator, typename Denominator>
 6           std::enable_if_t<std::is_integral_v<Numerator> &&
 7                            std::is_integral_v<Denominator>,
 8                            int = 0>
 9 auto divide(Numerator, Denominator) {
10   // 整数除法
11   if (denominator == 0) {
12     throw std::runtime_error("divide by 0!");
13   }
14   return numerator / denominator;
15 }
16 
17 template <typename Numerator, typename Denominator>
18           std::enable_if_t<std::is_floating_point_v<Numerator> ||
19                            std::is_floating_point_v<Denominator>,
20                            int = 0>
21 auto divide(Numerator, Denominator) {
22   // 浮点除法
23   return numerator / denominator;
24 }
```

图 110. SFINAE `divide` 函数。

C++17 的 `if constexpr` 结构可以简化这段代码：



```cpp
import std;

// 注意我们可以对 numerator 和 denominator 使用 auto
// 但会使 if constexpr 代码复杂化
// 因为我们需要使用 decltype 来获取类型信息。
template <typename Numerator, typename Denominator>
[[nodiscard]] constexpr auto divide(Numerator numerator, Denominator denominator) {
  if constexpr (std::is_integral_v<Numerator> &&
                std::is_integral_v<Denominator>) {
    // 整数除法
    if (denominator == 0) {
      throw std::runtime_error("divide by 0!");
    }
  }

  return numerator / denominator;
}
```

图 111. `if constexpr` 用于编译时行为。

在许多情况下，使用概念（concepts）代替 `if constexpr` 以提高可读性。

```cpp
import std;

// 默认重载
[[nodiscard]] constexpr auto divide(auto numerator, auto denominator) {
  return numerator / denominator;
}

// 只有当两个参数都是整数时才调用的版本
[[nodiscard]] constexpr auto divide(
  std::integral auto numerator, std::integral auto denominator) {

  // 整数除法
  if (denominator == 0) {
    throw std::runtime_error("divide by 0!");
  }

  return numerator / denominator;
}
```

图 112. 使用约束代替 `if constexpr`。

| ![](img/leanpub_info-circle.png) |
| --- |

`if constexpr` 块内部的代码在语法上必须是正确的。`if constexpr` 并不等同于 `#define`。

| ![](img/leanpub_key.png) |
| --- |

某些你通常会选择放在 `if` 块之外的代码，现在可能需要放在 `else` 块内部，以确保它们不会用无效类型进行实例化。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：深入研究“内省设计（design by introspection）”

`if constexpr`、概念（concepts）和 `requires` 的结合产生了一种非常强大、几乎类似于反射的能力。

```cpp
constexpr void add_values(auto &container, auto first, auto second)
{
  // 我们在编译时询问这个容器
  // 是否有 reserve 和 size 成员。
  if constexpr(requires {container.reserve(container.size() + 2); }) {
    // 如果这是一个有效操作，则在运行时执行
    container.reserve(container.size() + 2);
  }

  // 无论如何，添加值
  container.push_back(first);
  container.push_back(second);
}
```

图 113. “内省设计”示例。

## 55.1: 资源

- [C++ Weekly 特别版：使用 C++17 的 constexpr if](https://youtu.be/_Ny6Qbm_uMI)
- [C++ Weekly - Ep 122 - 配合 optional 和 variant 使用 constexpr](https://youtu.be/2eCV_udkP_o)
- [CppCon 2017: Jason Turner “实战 C++17”](https://youtu.be/nnY4e4faNp0)
- [C++ Weekly - Ep 242 - C++20 中的内省设计](https://youtu.be/sy32kAtsIKg)
- [Tony Tables 中的 C++17：constexpr if](https://github.com/tvaneerd/cpp17_in_TTs/blob/master/if_constexpr.md)

# 56: 去模板化你的泛型代码（De-template-ize）

尽可能将内容移出模板之外。使用其他函数。使用基类。编译器仍然可以对它们进行内联处理或保持不内联。

去模板化将缩短编译时间并减少二进制文件体积。这两者都有帮助。它还消除了人们认为的“模板代码膨胀”（在我看来，这[并不存在](https://articles.emptycrate.com/2008/05/06/nobody_understands_c_part_5_template_code_bloat.html)）。

```cpp
template<typename T>
constexpr void do_things()
{
  // 这个 lambda 必须为每个
  // 模板实例化生成
  auto lambda = [](){ /* 一个不捕获变量的 lambda */ };
  auto value = lambda();
}
```

图 114. 为每个函数模板实例化生成了一个新的 lambda。

相比之下：

```cpp
constexpr auto some_function() { /* 执行操作*/ }

template<typename T>
constexpr void do_things()
{
  auto value = some_function();
}
```

图 115. 模板实例化之间共享的逻辑。

现在内部逻辑只有一个版本被编译，并且由编译器决定是否应该对其进行内联。

类似的技巧也适用于基类和模板化的派生类。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：Bloaty McBloatface 和 -ftime-trace

我们有越来越多的工具可以用来查找二进制文件中的膨胀问题并分析编译时间。研究这些工具以及你平台上其他工具。

在你的二进制文件上运行这些工具，看看你会发现什么。

使用 Clang 的 `-ftime-trace` 时，也要查看 ClangBuildAnalyzer。

## 56.1: 资源

- [Templight](https://github.com/mikael-s-persson/templight)
- [C++ Weekly Ep 89: “过度使用 Lambda”](https://youtu.be/OmKMNQFx_8Y)
- [C++ Weekly Christmas Class 2019 - 第 3 章](https://www.youtube.com/watch?v=VEqOOKU8RjQ&list=PLs3KjaCtOwSY_Awyliwm-fRjEOa-SRbs-&index=16)（这是第 3 章的第一集，它引入了为什么以及两个不同的[选项会有差异](https://godbolt.org/z/b4znvK)的问题。该列表中接下来的几集提供了背景，第 4 章的开头给出了答案。与模板膨胀问题非常相关。）
- Effective C++（第 3 版）Item 44 - 从模板中提取与参数无关的代码

# 57: 使用 Lippincott 函数

参数与去模板化相同。这是一个用于对你的代码进行去模板化的 Lippincott 函数。

如果你有许多不同的异常类型，你可能会有这样的代码：

```cpp
void some_function() {
  try {
    do_something();
  } catch (const exception_type1&) {
    // ...
  } catch (const exception_type2&) {
    // ...
  }
}
```

图 116. 异常处理。

这种技术并不是新的——从 C++98 起就有了。

```cpp
void some_function() {
  try {
    do_something();
  } catch (const exception_type1&) {
    // ...
  } catch (const exception_type2&) {
    // ...
  }
}
```

图 117. 异常处理。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：你使用异常吗？

如果你的项目使用异常，那么就有某些地方需要集中处理。如果不使用异常，那么你可能有其他重复的类型。

## 57.1: 资源

- [C++ Secrets：使用 Lippincott 函数](https://cppsecrets.blogspot.com/2013/12/using-lippincott-function-for.html)
- [C++ Weekly Ep 91: Lippincott 函数](https://youtu.be/-amJL3Ay)

# 58: 不再需要 new！

你已经在避免堆内存并使用智能指针进行资源管理了，对吧？！

更进一步，在需要堆内存的极少数情况下使用 [`std::make_unique<>`](https://en.cppreference.com/w/memory/unique_ptr/make_unique)（C++14）。

在需要共享权的极少数情况下，使用 [`std::make_shared<>`](https://en.cppreference.com/w/memory/shared_ptr/make_shared)（C++11）。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：你使用 Qt 或其他组件库吗？

你考虑过编写自己的 `make_qobject` 辅助函数吗？赋予它需要的 `[[nodiscard]]`。

在任何情况下，你都可以将 `new` 的使用限制在少数核心库函数上。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：使用 clang-tidy 现代化修复

通过 clang-tidy，你可以自动将 `new` 语句转换为 `make_unique<>` 和 `make_shared<>` 调用。在发现后，务必使用 `-fix` 应用更改。

## 58.1: 资源

- [clang-tidy modernize-make-shared](https://clang.llvm.org/extra/clang-tidy/checks/modernize-make-shared.html)
- [clang-tidy modernize-make-unique](https://clang.llvm.org/extra/clang-tidy/checks/modernize-make-unique.html)

# 59: 避免 std::bind 和 std::function

虽然编译器不断改进，且优化器在绕过这些类型的复杂性，但其中任何一种仍然可能增加显著的编译时间和运行时开销。

C++14 的 lambda 配合泛化捕获表达式，可以实现 `std::bind` 所能的功能。

| ![](img/leanpub_key.png) |
| --- |

`std::function` 不支持 `constexpr`，这是你可能在代码中避免使用它的另一个原因。

```cpp
import std;

[[nodiscard]] constexpr double divide(double numerator, double denominator) {
  return numerator / denominator;
}

auto inverted_divide = std::bind(
  divide,
  std::placeholders::_2,
  std::placeholders::_1);
```

图 118. 使用 `std::bind` 更改参数顺序。

```cpp
import std;

[[nodiscard]] constexpr double divide(double numerator, double denominator) {
  return numerator / denominator;
}

auto inverted_divide = [](const auto numerator,
                          const auto denominator) {
  return divide(denominator, numerator);
};
```

图 119. 使用 Lambda 更改参数顺序。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：比较各种可能性

在 Compiler Explorer 中尝试这些选项。编译时间和生成的汇编代码看起来是一样的吗？

```cpp
import std;

// std::function 没有开启 constexpr 支持，所以这个
// 不能是 constexpr
[[nodiscard]] std::function<int(int)> bind_3(auto func)
{
  return std::bind(func, std::placeholders::_1, 3);
}

int main(int argc, const char *[])
{
  return bind_3(std::plus<>{})(argc);
}
```

图 120. `std::function` 和 `std::bind`。

```cpp
#include <functional>

// std::bind 开启了 constexpr 支持
[[nodiscard]] constexpr auto bind_3(auto func)
{
  return std::bind(func, std::placeholders::_1, 3);
}

int main(int argc, const char *[])
{
  return bind_3(std::plus<>{})(argc);
}
```

图 121. 仅使用 `std::bind`。作为加分项，函数 `bind_3` 返回什么类型？

```cpp
#include <functional>

[[nodiscard]] constexpr auto bind_3(auto func)
{
  return [func](auto value) { return func(value, 3); };
}

int main(int argc, const char *[])
{
  return bind_3(std::plus<>{})(argc);
}
```

图 122. 仅使用 lambda，没有标准库封装器。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：观察 `std::bind_front`、`std::bind_back`

```cpp
#include <functional>

[[nodiscard]] constexpr auto bind_3(auto func)
{
  return std::bind_back(func, 3);
}

int main(int argc, const char *[])
{
  return bind_3(std::plus<>{})(argc);
}
```

图 123. C++23 的 `bind_back`。

## 59.1: 资源

- [CppCon 2015: Stephan T. Lavavej “：新特性与正确用法”](https://youtu.be/zt7ThwVfap0)
- [C++ Weekly Ep 16: “避免 `std::bind`”](https://youtu.be/ZlHi8txU4aQ)

# 60: 不要对非平凡类型使用 initializer_list

“初始化列表（Initializer List）”是 C++ 中的一个重载术语。“初始化列表（Initializer Lists）”用于直接初始化值。`initializer_list` 用于将一个值列表传递给函数或构造函数。

| ![](img/leanpub_pencil.png) |
| --- |

## 练习：理解 initializer_list 可能会带来的开销

使用 Andreas Fertig 开发出的非常棒的 [cppinsights.io](http://cppinsights.io) 来理解这两个示例的作用。



```cpp
#include <vector>
#include <memory>

std::vector<std::shared_ptr<int>> vec{
   std::make_shared<int>(40), std::make_shared<int>(2)
};
```

图 124. 使用 `shared_ptr` 的 `initializer_list` 构造函数。

```cpp
#include <array>
#include <memory>

std::array<std::shared_ptr<int>, 2> data{
   std::make_shared<int>(40), std::make_shared<int>(2)
};
```

图 125. 使用 `shared_ptr` 的 `std::array` 构建。

并解释它们的区别。如果你能做到，说明你比大多数 C++ 开发者都懂得多。

> ![](img/leanpub_pencil.png)

## 练习：理解为什么这无法编译

```cpp
#include <vector>
#include <memory>

std::vector<std::unique_ptr<int>> data{
   std::make_unique<int>(40), std::make_unique<int>(2)
};
```

图 126. 使用 `unique_ptr` 的 `initializer_list` 构造。

### 60.1 资源

- [C++Now 2018: Jason Turner “初始化列表坏了，让我们修复它们”](https://youtu.be/sSlmmMFsXQ)（深入探讨问题）
- [C++ Insights](https://cppinsights.io/)

# 61. 考虑指定初始化（C++20）

直接初始化（Direct-Initialization）提供了一种初始化公共成员的高效方式。

```cpp
#include <string>

struct Data {
  std::string first;
  std::string second;
};

int main() {
  // 直接初始化 `first` 和 `second`
  // 这没有拷贝或移动开销
  Data d{"Hello", "World"};
}
```

这种方式是 C++20 添加了“指定初始化（designated initializers）”，允许你指定对象的名称。

- 必须按顺序初始化。
- 名称必须是唯一的。

```cpp
#include <string>

struct Data {
  std::string first;
  std::string second;
};

int main() {
  Data d{.first = "Hello", .second = "World"};
}
```

图 127. 直接初始化示例。

> ![](img/info-circle.png)

重要的是：编译器对指定初始化的支持是不一致的。确保在你的指定初始化时开启警告。

> ![](img/leanpub_pencil.png)

## 练习：与你的团队讨论你的偏好

- 跳过参数是优势还是劣势？
- 参数的名称重要吗？
- 在你的系统中强类型重要吗？

> ![](img/leanpub_pencil.png)

## 练习：比较具有公共成员的简单 `struct` 和带有构造函数的 `class`

```cpp
#include <string>

class Data {
 public:
  // 添加构造函数、getter 和 setter
  // 这更好吗？
  // 它增加了多少编译时间和运行时开销？
 private:
  std::string first;
  std::string second;
};
```

图 128. 实现构造函数和 getter。

图 129.

# 第 V 部分：附录章节

# 62. 优化编译时间

让编译时间不那么痛苦的一些实用考虑因素：

- 尽可能对代码去模板化。
- 在适当使用前置声明。
- 在你的构建系统中启用 PCH（预编译头文件）。
- 使用 `ccache` 或类似的工具（有很多经常更新的选项，请自行搜索）。
- 注意统一编译（unity builds）。
- 了解 `extern template` 的可能性和局限性。
- 使用构建分析工具查看编译时间花在哪里。

## 62.1 使用 IDE

这是我观察到的使用现代 IDE 最令人意外的副作用：IDE 会对代码进行实时分析。实时分析意味着你在输入代码时就知道代码是否可以编译。因此，你减少了等待构建的时间。

> ![](img/leanpub_pencil.png)

## 练习：编译时间让你付出了什么代价？

尝试计算一下构建时间在开发者时间上消耗了多少成本，并看看如果缩短构建时间可以节省多少成本。

## 62.2 资源

- [Unity 构建指南](https://onqtam.com/programming/2018-07-07-unity-builds/)
- [使用 Meson 进行 Unity 构建](https://mesonbuild.com/Unity-builds.html)
- [使用 CMake 进行 Unity 构建](https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD.html)
- [使用 Meson 使用 PCH（预编译头文件）](https://mesonbuild.com/Precompiled-headers.html)
- [使用 CMake 使用 PCH（预编译头文件）](https://cmake.org/cmake/help/latest/command/target_precompile_headers.html)
- [`ccache`](https://ccache.dev/)
- [CMake 启动器](https://cmake.org/cmake/help/latest/prop_tgt/LANG_COMPILER_LAUNCHER.html?highlight=ccache)
- [Clang 构建分析器](https://github.com/aras-p/ClangBuildAnalyzer)
- [开始使用 C++ Build Insights](https://docs.microsoft.com/en-us/cpp/build-insights/get-started-with-cpp-build-insights?view=vs-2019)
- [介绍用于 C++ 构建时间分析的 `vcperf /timetrace`](https://devblogs.microsoft.com/cppblog/introducing-vcperf-timetrace-for-cpp-build-time-analysis/)

# 63. 继续你的 C++ 教育

如果你想在领域内做得更好，就必须不断学习，而且有很多资源可以供你继续 C++ 教育。

## 63.1 知道如何提问

Kate Gregory 发表了一篇[关于如何提问题的优秀文章](http://www.gregcons.com/KateBlog/HowToAskForCCodingHelp.aspx)。

一些关键点是：

- 不要使用截图。
- 使用良好的变量名。
- 添加一些测试。
- 听别人告诉你的什么。

## 63.2 会议与本地用户小组

你附近几乎肯定有一个。这是建立人脉和学习新事物的极佳方法。查看[全球 ISO C++ 会议列表](https://isocpp.org/wiki/faq/conferences-worldwide) 和 [Meeting C++ 用户小组列表](https://meetingcpp.com/usergroups/)。

我在全球 COVID-19 大疫情期间完成这本书。因此，目前会议和用户小组大多处于暂停状态。但这为许多人提供了一个极具吸引力的新机会。

许多会议和用户小组现在都在在线举行。我们现在完全可以参加彼此的用户小组。例如，[北丹佛罗地铁 C++ Meetup](https://www.meetup.com/North-Denver-Metro-C-Meetup/) 每月经常有一个来自泰国的参加者。

> ![](img/leanpub_key.png)

作者注：在与 C++ 社区互动时，请记住尊重他人并维护他人；保持耐心；花时间理解你所交互特定社区的规则和规范。

## 63.3 C++ Weekly

本书处处引用 C++ Weekly 作为资源，以便查阅更多信息和可以与同事分享的示例。目前，该节目已经连续播放了 235 周，包含了许多特别节目、额外内容和直播。

## 63.4 cppreference.com

这个网站非常棒，但你可能不知道你可以创建一个账户并根据你正在使用的 C++ 版本自定义内容。此外，还可以执行示例并[下载离线版本](https://en.cppreference.com/w/Cppreference)!

## 63.5 雇佣培训师到公司上门

团队培训能让你的团队向新方向思考，提高士气并增加员工留存。既然你已经到了这里，我将给你一个优惠券。

如果你提到这本书，我将为你公司的上门培训费用为你提供 9 折优惠（差旅费不参与）。希望旅行限制不会持续太久。

## 63.6 YouTube

- [C++ Weekly（作者频道）](https://www.youtube.com/@cppweekly)
- [Andreas Fertig 频道](https://www.youtube.com/@andreas_fertig)
- [C++ on Sea](https://www.youtube.com/@cpponsea2834)
- [C++Now](https://www.youtube.com/@BoostCon)
- [code_report](https://www.youtube.com/@code_report)
- [code::dive](https://www.youtube.com/@codediveconference)
- [CopperSpice](https://www.youtube.com/copperspice)
- [Core C++](https://www.youtube.com/@corecpp)
- [CppCon](https://www.youtube.com/@CppCon)
- [CppNorth](https://www.youtube.com/@cppnorth)

## 63.7 播客

- [CppCast](https://cppcast.com/)

## 63.8 博客与有用网站

- [The Pasture](https://thephd.dev/)
- [eel.is / 当前 C++ 草案](http://eel.is/c++draft)
- [wg21 / 当前标准](https://wg21.link)
- [C++ Stories](https://cppstories.com/)
- [Fluent C++](https://www.fluentcpp.com/)

# 64. 感谢

## 64.1 赞助

如果你想在领域内做得更好，就必须不断学习，而且有很多资源可以供你继续 C++ 教育。

## 64.2 评审者

如果你提到这本书，我将为你公司的上门培训费用为你提供 9 折优惠（差旅费不参与）。

# 65. 进阶：理解 Lambda

简单的背后隐藏着惊人的复杂性。随着每个 C++ 版本的更新，Lambda 变得灵活而强大。

如果你能[阅读标准](http://eel.is/c++draft)，就可以自己研究 C++20 lambda 的所有功能。

```cpp
1 // 有效的空 lambda，什么都不做
2 []{};

// 参数列表可选
4 [](){

// C++17 显式 constexpr 和 void 返回
6 []() constexpr -> void {};

// 立即调用 lambda
8 auto i = [](){ return 42; }();

// C++17 之前不允许，因为 constexpr
10 constexpr auto j = []{ return 42; }();
```

图 130. Lambda 语法。

```cpp
1 // 泛型 lambda, C++14
2 [](auto x){ return x + 42; };

// 变长参数 lambda, C++14
4 [](auto ... x){ return std::vector<int>(x...); };

// 按值捕获, C++11
6 [i](){ return i + 42; };

// 泛化捕获, C++14（i 的类型是什么?）
8 [i = 42]{ return i + 42; };

// 有状态的 lambda, C++11
10 [i]() mutable { return ++i; };

// 显式模板, C++20
12 []<typename T>(T x){ return x + 42; };

// C++14 泛型 lambda 返回一个 C++20 lambda，该 lambda 使用变长
14 // 捕获表达式并返回一个折叠表达式
15 // 捕获值的求和。
16 [](auto ... val){ return [...val = val]{ return (val + ...); }; };
```

图 131. C++20 中允许的 lambda。

如果你理解 C++ lambda 的每一个方面，以及编译器是如何实现它们的，那么你已经掌握了关于 C++ 的所有重要内容。

这就是为什么我在 [YouTube 上整理了我的关于 lambda 的 C++ 课程](https://www.youtube.com/playlist?list=PLs3KjaCtOwSY_Awyliwm-fRjEOa-SRbs-)。

2018 年当编译器首次开始支持 C++20 的新 lambda 时，我使用 lambda 实现了这个基本符合标准的 `std::bind` 版本。

（续自下一页。）

```cpp
 1 template <std::size_t Idx>
 2 struct Placeholder {};
 3 
 4 template <typename T>
 5 struct Bound {
 6   constexpr decltype(auto) operator()(auto &&...param) const {
 7     return t(std::forward<decltype(param)>(param)...);
 8   }
 9 
10   T t;
11 };
12 
13 template <typename T>
14 Bound(T) -> Bound<T>;
15 
16 template <std::size_t Idx, typename T>
17 constexpr decltype(auto) get_param(const Placeholder<Idx> &,
18                                    T &&t) {
19   return std::get<Idx>(t);
20 }
21 
22 template <typename Param, typename T>
23 constexpr decltype(auto) get_param(Param &&param, T &&) {
24   return std::forward<Param>(param);
25 }
26 
27 template <typename Param, typename T>
28 constexpr decltype(auto) get_param(const Bound<Param> &b,
29                                    T &&t) {
30   return std::apply(b, std::forward<T>(t));
31 }
32 
33 constexpr decltype(auto) bind(auto &&callable, auto &&...param) {
34   return Bound{
35       [callable = std::forward<decltype(callable)>(callable),
36        ... xs = std::forward<decltype(param)>(param)]
37       (auto &&...values) {
38         auto passed_params =
39             std::forward_as_tuple(
40                std::forward<decltype(values)>(values)...);
41         return std::invoke(callable,
42                            get_param(xs, passed_params)...);
43       }
44   };
45 }
```

图 132. 使用 C++20 lambda 实现的 `std::bind`。

我已经两年没看过这段代码了，但这里有一个 Compiler Explorer 链接供你玩一玩。

[`godbolt.org/z/hhde3P`](https://godbolt.org/z/hhde3P)

> ![](img/leanpub_pencil.png)

## 练习：理解给定的示例并对其进行批判。



针对上面的示例，我应该做哪些不同的改进？可以使用概念（`concepts`）对其进行约束吗？它需要更好的命名吗？会有什么不同的做法？
