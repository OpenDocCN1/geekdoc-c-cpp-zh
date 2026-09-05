
# Boost C++ 库

![](img/cover.jpeg)

Copyright © 2008-2014 Boris Schäling

在下述例外情况下，本作品根据知识共享 署名-非商业性-禁止衍生性 4.0 国际许可协议进行许可。访问 [`creativecommons.org/licenses/by-nc-nd/4.0/deed.en`](http://creativecommons.org/licenses/by-nc-nd/4.0/deed.en) 查看完整许可协议副本。

例外：Boost C++ 标志是 Boost C++ 开发者的财产，在此处经其许可使用。除 Boost C++ 标志外，封面版权所有所有 © 2014 XML Press，保留所有权利。

# 前言

## 你将学到

本书是 Boost C++ 库的介绍。Boost C++ 库是对标准库的补充。由于 Boost C++ 库基于标准库，因此它们使用最先进的 C++ 实现。它们是平台无关的，并由大型开发者社区支持包括 Windows 和 Linux 在内的许多操作系统。

Boost C++ 库能够帮助你提升作为 C++ 开发者的生产力。例如，你可以从智能指针中受益，它们能帮助你编写更可靠的代码；或者使用许多库之一开发平台无关的网络应用程序。由于 Boost 库部分预判了标准库的发展，你可以更早从这些工具中受益，而无需等待它们在标准库中可用。

## 你应该了解

由于 Boost 库基于标准并扩展了标准，你应该熟悉标准库。你应该理解并能够使用容器、迭代器和算法，理想情况下，你应该听过如 `RAII`、函数对象和谓词等概念。你对标准的了解越深，从 Boost 库中获得的益处就越多。

通常情况下，使用本书中介绍的库不需要任何模板元编程的知识。本书的重点是那些可以快速、易地学习，并且能立即对你的 C++ 开发工作产生巨大益益的库。

许多示例使用了随 C++11 添加到标准中的特性。例如，使用 `auto` 关键字来避免显式指定类型。构造函数通过统一初始化调用：变量在可能的情况下使用一对大括号而不是括号进行初始化。许多示例使用 Lambda 函数使代码更短、更紧凑。虽然你可以在没有详细了解 C++11 的情况下理解许多示例，但本书是基于当前标准编写的。

## 排版规范

本书使用了以下文本样式：

`等宽字体`

等宽字体用于类名、函数名和关键字——基本上用于任何 C++ 代码。它也用于代码示例、命令行选项和程序输出。例如：`int i = 0;`

`等宽加粗字体`

等宽加粗字体用于变量名、对象和用户输入。例如：变量 `i` 被初始化为 0。

**粗体**

命令用粗体标记。例如：Boost 库使用一个名为 `bjam` 的程序进行编译。

*斜体*

当引入新概念并首次提到它时使用斜体字体。例如：`RAII` 是资源获取初始化（Resource Acquisition Is Initialization）的缩写——这是智能指针所基于的概念。

## 示例

本书包含了 430 多个示例。每个示例都是完整的，可以编译并运行。你可以从 [`theboostcpplibraries.com/examples/`](http://theboostcpplibraries.com/examples/) 下载所有示例以快速上手。

所有示例都已通过以下编译器测试：Microsoft Visual Studio Professional 2013 Update 1 (64-bit Windows 7 Professional with Service Pack 1)、`GCC 4.8.3` (64-bit Cygwin 1.7.30)、`GCC 4.6.3` (32-bit Ubuntu 12.04.4) 以及 `Clang 3.3` (32-bit Ubuntu 12.04.4)。

本书中的所有示例都基于 C++11 标准。在测试期间，所有编译器均配置为启用 C++11 支持。大多数示例可以在 Windows、Linux 和 OS X 上运行，但少数示例取决于平台。例外情况已在示例说明中注明。

示例不提供任何明示或暗示的保证。与本书一样，它们根据知识共享 署名-非商业性-禁止衍生性 4.0 国际许可协议进行许可。

# 简介

[Boost C++ 库](http://www.boost.org/doc/libs/) 是基于 C++ 标准的现代库集合。源代码根据 [Boost 软件许可，](http://www.boost.org/LICENSE_1_0.txt) 发布，允许任何人免费使用、修改和分发这些库。这些库是平台无关的，并支持大多数流行的编译器，以及许多较不为人知的编译器。

Boost 社区负责开发和发布 Boost 库。该社区由全球范围内的一群规模较大的 C++ 开发者组成，通过 [www.boost.org](http://www.boost.org/) 网站以及若干邮件列表进行协调。[GitHub](http://github.com/boostorg) 被用作代码仓库。社区的使命宣言是开发和收集补充标准库的高质量库。证明具有价值并对 C++ 开发至关重要的库，有很大机会在某时被纳入标准库。

Boost 社区出现于 1998 年左右，当时第一个版本的标准刚刚发布。从那时起，它不断成长，现在在 C++ 的标准化中发挥着重要作用。尽管 Boost 社区与标准化委员会之间没有正式关系，但一些开发者活跃在两个群体中。2011 年批准的当前 C++ 标准版本包含了源自 Boost 社区的库。

当你的需求超出了标准库提供的范围时，Boost 库是提高 C++ 项目生产力的良好选择。由于 Boost 库的演进比标准库快，你可以更早地获得开发，而无需等待它们被添加到标准库中。因此，感谢 Boost 库，你可以更快地从 C++ 的进化进展中受益。

得于 Boost 库的良好声，精通它们对工程师来说是一项价值技能。面试中问及 Boost 库并不罕见，因为熟悉这些库的开发者通常也熟悉 C++ 的最新创新，并且编写和理解现代 C++ 代码。

## 开发流程

Boost 库的开发之所以可能，是因为个人开发者和组织的支持。由于 Boost 只接受解决现有问题、设计精良、使用现代 C++ 开发并以易懂方式记录的库，每个 Boost 库背后都有大量的工作。

C++ 开发者可以参与 Boost 社区并提议新库。然而，将一个想法转换为 Boost 库需要大量的时间和精力。因此，在 Boost 邮件列表中与其他开发者和潜在用户讨论需求和解决方案至关重要。

一个库是否被接受入 Boost 取决于评审结果。库的开发者可以申请评审，评审通常持续 10 天。在评审期间，会要求其他开发者对该库进行评分。根据正面和负面评价的数量，评审经理将决定是否将该库纳入 Boost。由于某些评审者可能是第一次看到提议的新库，因此要求其进行修改的情况并不罕见。

如果一个库因为技术原因被拒绝，仍然可以修改该库并针对更新后的版本请求新的评审。然而，如果库被拒绝的原因是它没有解决任何实际问题，或者它对现有问题提供了一个缺乏说服力的解决方案，那么它在另一次评审中极很有可能再次被拒绝。

由于新库可以随时被接受，Boost 库每三个月发布一个新版本。这确保了开发者能够定期且及时地从 Boost 库的改进中受益。

### 注意事项

本书基于 Boost 库 `1.55.0` 和 `1.56.0`。`1.55.0` 版本于 2013 年 11 月发布。由于 Boost 社区在 2013 年底从 Subversion 切换到 Git，并且需要时间适应发布流程，下一个版本 `1.56.0` 直到 2014 年 8 月才发布。这发生在本书出版前的两周。由于 `1.55.0` 在九个月的时间里都是最新版本，本书基于 Boost `1.55.0`。然而，所有示例都已通过 Boost `1.56.0` 进行了测试，且所有示例都可以在 Boost `1.55.0` 或 `1.56.0` 下编译。

## 安装

Boost 库以源代码的形式提供。虽然大多数库仅由可以可以直接使用的头文件组成，但某些库需要进行编译。为了让安装变得尽可能简单，我们提供了一个基于 `Boost.Build` 的自动化安装过程。`Boost.Build` 不需要单独地验证和编译每个库，而是自动安装整套库。`Boost.Build` 可用于许多操作系统和编译器，并能够根据适当的文件编译每个库。

要使用 `Boost.Build` 自动安装 Boost 库，可以使用命令行程序 `bjam`。Boost 库以源代码形式提供该程序，而不是可执行文件。因此，构建和安装 Boost 库需要两个步骤。下载 Boost 库后，切换到 Boost 目录并输入以下命令：

1. 在 Windows 上输入 `bootstrap`，在 Linux 等其他平台上输入 `./bootstrap.sh` 进行编译。该脚本会自动搜索 C++ 编译器。

2. 然后，在 Windows 上输入 `bjam`，在其他平台上输入 `./bjam` 开始安装 Boost 库。

你只需要使用一次 `bootstrap` 来构建。但是，你可能需要频繁使用 `bjam`，因为 `bjam` 支持通过命令行选项以不同的方式构建 Boost 库。如果你在不带任何命令行选项的情况下启动 `bjam`，将使用默认配置。由于默认配置并不总是适用，你应该了解最常用的命令行选项：

- 命令行选项 `stage` 和 `install` 指定 Boost 库是安装在名为 `stage` 的子目录中，还是系统级安装。系统的范围取决于操作系统。在 Windows 上，目标目录是 `C:\Boost`；在 Linux 上是 `/usr/local`。也可以通过 `--prefix` 选项指定目标目录。

- 如果在不带任何命令行选项的情况下调用 `bjam`，它将搜索合适的 C++ 编译器。要在 Windows 上选择 C++ 2013，请使用 `--toolset=msvc-12.0` 调用 `bjam`。要在 Linux 上选择 GCC 编译器，使用 `--toolset=gcc`。

- 命令行选项 `--build-type` 决定创建哪些构建类型的库。默认情况下，此选项设置为 `minimal`，这意味着只创建发布（release）版本。对于想要使用 C++ 或 GCC 创建项目调试（debug）版本的开发者来说这可能会是一个问题。因为这些编译器会自动尝试链接 Boost 库的调试版本，会导致显示错误信息。在这种情况下，应将选项 `--build-type` 设置 `complete` 以生成 Boost 库的调试和发布版本。这可能花费相当的时间，这就是为什么 `complete` 不是默认设置。

- 必须编译的 Boost 库在 Windows 上以包含版本号和各种标记的文件名提供。这使得我们能够判断某个库是作为调试变体还是发布变体构建的。`libboost_atomic-vc120-mt-gd-1_56` 就是这样一个文件名。该库是用 C++ 2013 构建的。它属于 Boost 库 `1.56.0`。它是一个调试变体，可以用于多线程程序。通过命令行选项 `--layout`，可以告诉 `bjam` 生成其他文件名。例如，如果你将其设置为 `system`，则相同的文件将被命名为 `libboost_atomic`。在 Linux 上，`system` 是默认设置。如果你想让 Linux 上的文件名与 Windows 上默认生成的相同相同，请将 `--layout` 设置为 `versioned`。要使用 C++ 2013 创建 Boost 库的调试和发布版本并将它们安装到目录 `D:\Boost` 中，请输入以下命令：

```
bjam --toolset=msvc-12.0 --build-type=complete --prefix=D:\Boost install
```

要在 Linux 上构建它们并安装到默认目录，命令应为：

```
bjam --toolset=gcc --build-type=complete install
```

还有许多其他命令行选项可以详细指定如何编译 Boost 库。请看以下命令：

```
bjam --toolset=msvc-12.0 debug release link=static runtime-link=shared install
```

`debug` 和 `release` 选项会导致生成调试和发布版本。`link=static` 只创建静态库。`runtime-link=shared` 指定动态链接 C++ 运行时库，这是 C++ 2013 项目的默认设置。

## 概述

有多个 Boost 库。本书将详细讨论以下库：

表 1. 涵盖的库

| Boost 库 | 标准 | 简述 |
| --- | --- | --- |
| Boost.Accumulators | | Boost.Accumulators 累加器，向其中添加数字可以获取平均值或标准差。 |
| Boost.Algorithm | | Boost.Algorithm 提供了补充标准库算法的各种算法。 |
| Boost.Any | | Boost.Any 提供了一种名为 `boost::any` 类型，它可以存储任意类型的对象。 |
| Boost.Array | TR1, C++11 | Boost.Array 使 C++ 数组像标准库容器一样使用。 |
| Boost.Asio | | Boost.Asio 允许开发异步处理数据的应用程序（如网络应用程序）。 |
| Boost.Assign | | Boost.Assign 提供了辅助函数，用于向容器添加多个值，而无需多次调用 `push_back()` 等成员函数。 |

### Boost.Atomic

C++11 `Boost.Atomic` 定义了 `boost::atomic` 类，用于对整数值执行原子操作。该库用于需要在线程间共享整数值的多线程应用程序中。

### Boost.Bimap

`Boost.Bimap` 提供了一个名为 `boost::bimap` 的类，它类似于 `std::map`。关键区别在于 `boost::bimap` 允许你同时对键和值进行搜索。

### Boost.Bind

TR1, C++11 `Boost.Bind` 是一种将函数作为模板参数的适配器，即使函数签名与预期的模板参数不兼容。

### Boost.Chrono

C++11 `Boost.Chrono` 定义了许多时钟，用于获取当前时间或 CPU 时间等值。

### Boost.CircularBuffer

`Boost.CircularBuffer` 提供了一个具有固定内存的循环容器。

### Boost.CompressedPair

`Boost.CompressedPair` 提供了数据结构 `boost::compressed_pair`，它类似于 `std::pair`，当模板参数为空类时，它需要的内存更少。

### Boost.Container

`Boost.Container` 定义了标准库中的所有容器，以及诸如 `boost::container::slist` 等额外的容器。

### Boost.Conversion

`Boost.Conversion` 提供两个转换运算符，用于执行向下转换（downcasts）和交叉转换（cross casts）。

### Boost.Coroutine

`Boost.Coroutine` 在 C++ 中使用协程成为可能。协程通常在其他编程语言中使用关键字 `yield`。

### Boost.DateTime

`Boost.DateTime` 可用于处理、读取和写入日期和时间值。

### Boost.DynamicBitset

`Boost.DynamicBitset` 提供了一个类似于 `std::bitset` 的结构，不同之处是在运行时进行配置。

### Boost.EnableIf

C++11 `Boost.EnableIf` 允许根据类型属性重载函数。

### Boost.Exception

`Boost.Exception` 允许你向抛出的异常添加额外数据，以便为 `catch` 处理器提供更多信息。

### Boost.Filesystem

`Boost.Filesystem` 提供了一个处理路径的类以及几个访问文件和目录的函数。

### Boost.Flyweight

`Boost.Flyweight` 使得使用同名的设计模式变得简单。

### Boost.Foreach

`Boost.Foreach` 提供了一个类似于 C++11 引入的基于范围的 `for` 循环的宏。

### Boost.Format

`Boost.Format` 用类型安全且可扩展的类 `boost::format` 取替函数 `std::printf()`。

### Boost.Function

TR1, C++11 `Boost.Function` 简化了函数指针的定义。

### Boost.Fusion

`Boost.Fusion` 允许你创建异构容器——即可以存储不同类型元素的容器。

### Boost.Graph

`Boost.Graph` 提供了用于寻找两点间最短路径等操作的算法。

### Boost.Heap

`Boost.Heap` 提供了标准库 `std::priority_queue`类的许多变体。

### Boost.Integer

C++11 `Boost.Integer` 定义了特殊整数类型，自 1999 年标准 C99 发布以来一直供 C 开发者使用。

### Boost.Interprocess

`Boost.Interprocess` 使用共享内存帮助应用程序快速、高效地通信。

## Boost.Intrusive

`Boost.Intrusive` 定义了性能比标准库更高的容器，但对其所包含的对象有特殊要求。

### Boost.IOStreams

`Boost.IOStreams` 提供流和过滤器。过滤器可以与流连接，例如写入压缩后的数据。

### Boost.Lambda

`Boost.Lambda` 允许你在没有 C++11 的情况下定义匿名函数。

### Boost.LexicalCast

`Boost.LexicalCast` 提供了一个转换运算符，用于将数字转换为字符串反之亦然。



# Boost.Lockfree

`Boost.Lockfree` 定义了多个线程并发访问的线程安全容器。

# Boost.Log

`Boost.Log` 是 Boost 中的日志库。

# Boost.MetaStateMachine

`Boost.MetaStateMachine` 使得按照 UML 定义状态机成为可能。

# Boost.MinMax

C++11 `Boost.MinMax` 提供了一种算法，可以在不调用 `std::min()` 和 `std::max()` 的情况下找到容器中的最小最大值。

# Boost.MPI

`Boost.MPI` 为 MPI 标准提供了 C++ 接口。

# Boost.MultiArray

`Boost.MultiArray` 简化了多维数组的操作。

# Boost.MultiIndex

`Boost.MultiIndex` 允许你定义支持多种接口的新容器，例如来自 `std::vector` 和 `std::map` 的接口。

# Boost.NumericConversion

`Boost.NumericConversion` 提供了一个转换运算符，用于在不同数值类型的值之间安全转换，而不产生溢出条件。

# Boost.Operators

`Boost.Operators` 允许在已定义运算符的帮助下自动重载许多运算符。

# Boost.Optional

`Boost.Optional` 提供了一个用于表示可选返回值的类。无法总是返回结果的函数不再需要使用 `-1` 或空指针等特殊值。

# Boost.Parameter

`Boost.Parameter` 允许你像使用 Python 等编程语言那样，以键值对的形式将参数传递给函数。

# Boost.Phoenix

`Boost.Phoenix` 可以在没有 C++11 的情况下创建 lambda 函数。与 C++11 lambda 函数不同，该库的 lambda 函数是通用的。

# Boost.PointerContainer

`Boost.PointerContainer` 提供了针对动态分配对象管理优化的容器。

# Boost.Pool

`Boost.Pool` 是一个内存管理库。例如，`Boost.Pool` 定义了一个分配器，针对需要创建和销毁许多相同大小的情况进行了优化。

# Boost.ProgramOptions

`Boost.ProgramOptions` 允许应用程序定义和评估命令行选项。

# Boost.PropertyTree

`Boost.PropertyTree` 提供了一个以树形结构存储键值对的容器。这使得管理许多应用程序使用的配置数据变得更加容易。

# Boost.Random

`Boost.Random` 提供了随机数生成器。（TR1, C++11）

# Boost.Range

`Boost.Range` 引入了“范围”（range）的概念，取代了通常从容器中通过 `begin()` 和 `end()` 获取的迭代器。范围使得你不需要向算法传递迭代迭代器对。

# Boost.Ref

`Boost.Ref` 提供了适配器，允许你将不可拷贝对象的引用传递给通过拷贝传递参数的函数。（TR1, C++11）

# Boost.Regex

`Boost.Regex` 提供了使用正则表达式搜索字符串的函数。（TR1, C++11）

# Boost.ScopeExit

`Boost.ScopeExit` 提供了宏，用于定义在当前作用域结束时执行的代码块。这样可以在当前作用域结束时释放资源，而无需使用智能指针或其他类。

# Boost.Serialization

`Boost.Serialization` 允许你序列化对象并将其存储在文件中以便以后加载。

# Boost.Signals2

`Boost.Signals2` 是一个基于信号/槽（signal/slot）概念的事件处理框架，它将函数与信号关联，并在信号触发时自动调用相应的函数。

# Boost.SmartPointers

`Boost.SmartPointers` 提供了一组智能指针，简化了动态分配对象的管理。（TR1, C++11）

# Boost.Spirit

`Boost.Spirit` 允许你使用类似于 EBNF（扩展巴科斯诺尔式）的语法生成解析器。

# Boost.StringAlgorithms

`Boost.StringAlgorithms` 提供了许多独立函数方便字符串处理。

# Boost.Swap

`Boost.Swap` 定义了 `boost::swap()`，其功能与 `std::swap()` 相同，但针对许多 Boost 库进行了优化。

# Boost.System

`Boost.System` 提供了一个处理系统和应用程序特定错误代码的框架。（C++11）

# Boost.Thread

`Boost.Thread` 允许你开发多线程应用程序。（C++11）

# Boost.Timer

`Boost.Timer` 定义了可以测量代码性能的时钟。

# Boost.Tokenizer

`Boost.Tokenizer` 允许你遍历字符串中的标记（tokens）。

# Boost.Tribool

`Boost.Tribool` 提供了一种类型，与 `bool` 不同，它区分三种状态而非两种。

# Boost.Tuple

`Boost.Tuple` 提供了 `std::pair` 的通用版本，可以存储任意数量的值，而不只是两个。（TR1, C++11）

# Boost.TypeTraits

`Boost.TypeTraits` 提供了检查类型属性的函数。（TR1, C++11）

# Boost.Unordered

`Boost.Unordered` 提供了哈希容器：`boost::unordered_set` 和 `boost::unordered_map`。（TR1, C++11）

# Boost.Utility

`Boost.Utility` 是各种工具集合，这些工具小到无法独立成库，也不适合其他库。

# Boost.Uuid

`Boost.Uuid` 定义了 `boost::uuids::uuid` 类以及创建 UUID 的生成器。

# Boost.Variant

`Boost.Variant` 允许定义像 `union` 一样组合多个类型的类型。

# Boost.Xpressive

`Boost.Xpressive` 使得可以使用正则表达式搜索字符串。正则表达式被编码为 C++ 代码而非字符串。

# 第一部分. RAII 与内存管理

RAII 代表“资源获取即初始化”。这种模式背后的思想是：对于获取的任何资源，都应该初始化一个对象来拥有该资源，并在析构函数中关闭它。智能指针是 RAII 的显著示例。以下库提供了智能指针和其他工具，帮助你更轻松地管理内存。

- `Boost.PointerContainer` 定义了存储动态分配对象的容器——即通过 `new` 创建的对象。由于该库的容器在析构函数中使用 `delete` 释放对象，因此不需要使用智能指针。

- `Boost.ScopeExit` 使对任何资源使用 RAII 模式成为可能。虽然 `Boost.SmartPointers` 和 `Boost.PointerContainer` 只能与动态分配对象的指针配合，但使用 `Boost.ScopeExit` 不需要使用任何特定资源的类。

- `Boost.Pool` 与 RAII 无关，但与内存管理有关。该库定义了许多类以为你的程序提供更快的内存分配。

# 1. Boost.SmartPointers

[Boost.SmartPointers](http://www.boost.org/libs/smart_ptr) 提供了各种智能指针。它们帮助你管理动态分配的对象，这些对象锚位于智能指针中，智能指针在析构函数中释放动态分配的对象。由于析构函数在智能指针的作用域结束时执行，因此保证释放动态分配的对象。例如，如果你忘记调用 `delete`，就不可能发生内存泄漏。

标准库自 C++98 起就包含了智能指针 `std::auto_ptr`，但从 C++11 起，`std::auto_ptr` 已被弃用。C++11 在标准库中引入了新的更好的智能指针。`std::shared_ptr` 和 `std::weak_ptr` 源自 `Boost.SmartPointers`，在本库中被称为 `boost::shared_ptr` 和 `boost::weak_ptr`。这里没有 `std::unique_ptr` 的对应项。然而，`Boost.SmartPointers` 提供了四个额外的智能指针——`boost::scoped_ptr`、`boost::scoped_array`、`boost::shared_array` 和 `boost::intrusive_ptr`，它们在标准库中是不存在的。

## 独占所有

`boost::scoped_ptr` 是一种对动态分配对象拥有唯一所有权的智能指针。`boost::scoped_ptr` 不能被复制或移动。该智能指针定义在头文件 `boost/scoped_ptr.hpp` 中。

类型为 `boost::scoped_ptr` 的智能指针不能转移对象的所有权。一旦用地址初始化，当执行析构函数或调用成员函数 `reset()` 时，动态分配的对象就会被释放。

示例 1.1，“使用 `boost::scoped_ptr`” 使用了类型为 `boost::scoped_ptr<int>` 的智能指针 `p`。`p` 用一个指向存储数字 1 的动态分配对象的指针初始化。通过 `operator*`，`p` 被解引用并将 `1` 写入标准输出。

示例 1.1. 使用 `boost::scoped_ptr`

```
#include <boost/scoped_ptr.hpp>
#include <iostream>

int main()
{
  boost::scoped_ptr<int> p{new int{1}};
  std::cout << *p << '\n';
  p.reset(new int{2});
  std::cout << *p.get() << '\n';
  p.reset();
  std::cout << std::boolalpha << static_cast<bool>(p) << '\n';
}
```

通过 `reset()` 可以在智能指针中存储一个新的地址。这样，示例将一个包含数字 2 的新分配 `int` 对象的地址传递给 `p`。调用 `reset()` 后，`p` 中当前引用的对象会被销毁。

`get()` 返回锚在智能指针中的对象地址。示例对 `get()` 返回的地址进行解引用，将 `2` 写入标准输出。

`boost::scoped_ptr` 重载了运算符 `operator bool`。如果智能指针包含对对象的引用——即它不为空，`operator bool` 返回 `true`。示例向标准输出写入了 `false`，因为 `p` 已通过调用 `reset()` 被重置。

`boost::scoped_ptr` 的析构函数使用 `delete` 释放引用的对象。这就是为什么 `boost::scoped_ptr` 不得用动态分配数组的地址初始化，因为数组必须用 `delete[]` 释放。对于数组，`Boost.SmartPointers` 提供了 `boost::scoped_array` 类。

示例 1.2. 使用 `boost::scoped_array`

```
#include <boost/scoped_array.hpp>

int main()
{
  boost::scoped_array<int> p{new int[2]};
  *p.get() = 1;
  p[1] = 2;
  p.reset(new int[3]);
}
```

智能指针 `boost::scoped_array` 的用法类似于 `boost::scoped_ptr`。关键区别在于 `boost::scoped_array` 的析构函数使用运算符 `delete[]` 来释放包含的对象。由于该运算符仅适用于数组，`boost::scoped_array` 必须用动态分配数组的地址初始化。

`boost::scoped_array` 定义在 `boost/scoped_array.hpp` 中。

`boost::scoped_array` 为 `operator[]` 和 `operator bool` 提供了重载。使用 `operator[]` 可以访问数组的特定元素。因此，类型为 `boost::scoped_array` 的对象的行为就像它拥有的数组。示例 1.2，“使用 `boost::scoped_array`” 类似于 `boost::scoped_ptr`。

## 共享所有

智能指针 `boost::shared_ptr` 类似于 `scoped_ptr`。关键区别在于 `boost::shared_ptr` 并不是对象的唯一所有者。所有权可以与其他智能指针共享。直到最后一个智能指针销毁时，对象才会释放。`boost::shared_ptr` 可以复制，这在 `scoped_ptr` 中是不可能的。`boost::shared_ptr` 定义在头文件 `boost/shared_ptr.hpp` 中。

示例 1.3. 使用 `boost::shared_ptr`

```
#include <boost/shared_ptr.hpp>
#include <iostream>

int main()
{
  boost::shared_ptr<int> p1{new int{1}};
  std::cout << *p1 << '\n';
  boost::shared_ptr<int> p2{p1};
  p1.reset(new int{2});
  std::cout << *p1.get() << '\n';
  p1.reset();
  std::cout << std::boolalpha << static_cast<bool>(p2) << '\n';
}
```

示例 1.3，“使用 `boost::shared_ptr`” 使用了类型为 `boost::shared_ptr` 的两个智能指针 `p1` 和 `p2`。`p2` 用 `p1` 初始化，这意味着两个智能指针共享同一个 `int` 对象的所有权。当对 `p1` 调用 `reset()` 时，一个新的 `int` 对象被锚在 `p1` 中。这并不意味着现有 `int` 对象被销毁。因为它也被锚在 `p2` 中，所以继续存在。调用 `reset()` 后，`p1` 是数字 2 `int` 对象的唯一所有者，而 `p2` 是数字 1 `int` 对象的唯一所有者。

`boost::shared_ptr` 内部使用引用计数器。只有当 `boost::shared_ptr` 检测到最后一个拷贝被销毁时，才会通过 `delete` 释放包含的对象。

与 `boost::scoped_ptr` 一样，`boost::shared_ptr` 重载了 `operator bool()`、`operator*()` 和 `operator->()`。提供了成员函数 `get()` 和 `reset()` 用于获取当前存储的地址或存储新地址。

作为第二个参数，可以将删除器传递给 `boost::shared_ptr` 构造函数。删除器必须是一个函数或函数对象，其唯一参数类型为 `boost::shared_ptr` 实例化时的指针类型。删除器会在析构函数中调用而不是 `delete`。这使得在 `boost::shared_ptr` 管理动态分配对象以外的资源成为可能。

示例 1.4. 使用自定义删除器的 `boost::shared_ptr`

```cpp
#include <boost/shared_ptr.hpp>
#include <Windows.h>

int main()
{
  boost::shared_ptr<void> handle(OpenProcess(PROCESS_SET_INFORMATION, FALSE,
    GetCurrentProcessId()), CloseHandle);
}
```

在示例 1.4，“带有自定义删除器的 `boost::shared_ptr`” 中，`boost::shared_ptr` 使用 `void` 实例化。传递给构造函数的第一个参数是 `OpenProcess()` 的返回值。`OpenProcess()` 是一个获取进程句柄的 Windows 函数。在示例中，`OpenProcess()` 返回当前进程的句柄——即示例本身的句柄。

Windows 使用句柄（handles）来引用资源。一旦资源不再被使用，必须使用 `CloseHandle()` 关闭句柄。`CloseHandle()` 期望唯一参数是要关闭的句柄。在示例中，`CloseHandle()` 作为第二个参数传递给 `boost::shared_ptr` 的构造函数。`CloseHandle()` 是 `handle` 的删除器。当 `handle` 在 `main()` 结束时被销毁，析构函数会调用 `CloseHandle()` 来关闭作为第一个参数传递给构造函数的句柄。

### 注意



示例 1.4，“带有自定义删除器的 `boost::shared_ptr`” 之所以能够工作是因为 Windows 句柄被定义为 `void*`。如果 `OpenProcess()` 返回的不是 `void*` 类型，且 `CloseHandle()` 不期望 `void*` 类型的参数，那么在该示例中就无法使用 `boost::shared_ptr`。删除器并让 `boost::shared_ptr` 成为管理任意资源的“万灵药”。

## 示例 1.5. 使用 `boost::make_shared`

```
#include <boost/make_shared.hpp>
#include <typeinfo>
#include <iostream>

int main()
{
  auto p1 = boost::make_shared<int>(1);
  std::cout << typeid(p1).name() << '\n';
  auto p2 = boost::make_shared<int[]>(10);
  std::cout << typeid(p2).name() << '\n';
}
```

Boost.SmartPointers 在 `boost/make_shared.hpp` 中提供了一个辅助函数 `boost::make_shared()`。通过 `boost::make_shared()`，你可以创建一个类型为 `boost::shared_ptr` 的智能指针，而无需亲自调用 `boost::shared_ptr` 的构造函数。

`boost::make_shared()` 的优势在于，动态分配的对象内存和智能指针内部使用的引用计数器内存可以在同一块内存中预留。使用 `boost::make_shared()` 比调用 `new` 创建动态分配对象，然后在 `boost::shared_ptr` 构造函数中再次调用 `new` 为引用计数器分配内存更高效。

你也可以将 `boost::make_shared()` 用于数组。在示例 1.5，“使用 `boost::make_shared`” 的第二次调用 `boost::make_shared()` 中，一个包含十个元素的 `int` 数组被锚定在 `p2` 中。

`boost::shared_ptr` 从 Boost 1.53.0 版本开始才支持数组。`boost::shared_array` 提供了一个类似于 `boost::shared_ptr` 的智能指针，就像 `boost::scoped_array` 类似于 `boost::scoped_ptr` 一样。当使用 Visual C++ 2013 和 Boost 1.53.0 或更高版本编译时，示例 1.5，“使用 `boost::make_shared`” 为 `p2` 打印 `class boost::shared_ptr<int [0]>`。

从 Boost 1.53.0 开始，`boost::shared_ptr` 支持单对象和数组，并能检测需要使用 `delete` 还是 `delete[]` 释放资源。由于 `boost::shared_ptr` 也重载了 `operator[]`（自 Boost 1.53.0 起），该智能指针可以 `boost::shared_array` 的替代方案。

`boost::shared_array` 补充了 `boost::shared_ptr`：由于 `boost::shared_array` 在析构函数中调用 `delete[]`，因此该智能指针可用于数组。对于 Boost 1.53.0 之前的版本，必须使用 `boost::shared_array` 处理数组，因为 `boost::shared_ptr` 不支持数组。

`boost::shared_array` 定义在 `boost/shared_array.hpp` 中。

## 示例 1.6. 使用 `boost::shared_array`

```
#include <boost/shared_array.hpp>
#include <iostream>

int main()
{
  boost::shared_array<int> p1{new int[1]};
  {
    boost::shared_array<int> p2{p1};
    p2[0] = 1;
  }
  std::cout << p1[0] << '\n';
}
```

在示例 1.6，“使用 `boost::shared_array`” 中，智能指针 `p1` 和 `p2` 共享数组的所有权。`boost::shared_array` 在析构函数中调用 `delete[]`，智能指针 `p1` 和 `p2` 共享数组的所有权。`boost::shared_array` 提供了 `get()` 和 `reset()` 方法。此外，它重载了 `operator[]`。

### 示例 1.7. 带有自定义删除器的 `boost::shared_ptr`

```cpp
#define BOOST_SP_USE_ALLOCATOR
#include <boost/shared_ptr.hpp>
#include <iostream>
#include <ctime>

int main()
{
  boost::shared_ptr<int> p;
  std::time_t then = std::time(nullptr);
  for (int i = 0; i < 1000000; ++i)
    p.reset(new int{i});
  std::time_t now = std::time(nullptr);
  std::cout << now - then << '\n';
}
```

可以使用标准库中类似于 `boost::shared_ptr` 的智能指针。Boost.SmartP 支持 `BOOST_SP_DEBUG_HOOKS` 宏。这些宏的名称以 `BOOST_SP` 开头，便于在头文件中查找。

### 提示

除了 `BOOST_SP_USE_ALLOCATOR` 之外，Boost.SmartP 支持 `BOOST_SP_DEBUG_HOOKS` 宏。这些宏的名称以 `BOOST_SP` 开头，便于在头文件中查找。

## 特殊智能指针

目前为止引入的智能指针都可以单独使用。然而，`boost::weak_ptr` 只有在与 `boost::shared_ptr` 配合使用才有意义。`boost::weak_ptr` 定义在 `boost/weak_ptr.hpp` 中。

## 示例 1.8. 使用 `boost::weak_ptr`

```cpp
#include <boost/shared_ptr.hpp>
#include <boost/weak_ptr.hpp>
#include <thread>
#include <functional>
#include <iostream>

void reset(boost::shared_ptr<int> &sh)
{
  sh.reset();
}

void print(boost::weak_ptr<int> &w)
{
  boost::shared_ptr<int> sh = w.lock();
  if (sh)
    std::cout << *sh << '\n';
}

int main()
{
  boost::shared_ptr<int> sh{new int{99}};
  boost::weak_ptr<int> w{sh};
  std::thread t1{reset, std::ref(sh)};
  std::thread t2{print, std::ref(w)};
  t1.join();
  t2.join();
}
```

`boost::weak_ptr` 必须用 `boost::shared_ptr` 初始化。它最重要的成员函数是 `lock()`。`lock()` 返回一个与初始化弱指针的共享指针共享所有权的 `boost::shared_ptr`。如果该共享指针为空，则返回的指针也将为空。

当一个函数预期处理一个由 `shared pointer` 管理的对象，但该对象的生命周期并不依赖于函数本身时，`boost::weak_ptr` 就很有意义了。只要程序中某处至少有一个 `shared pointer` 拥有该对象，函数就可以使用该对象。如果 `shared pointer` 被 `reset`，则无法因为相应函数内部额外的 `shared pointer` 而保持对象存活。

Example 1.8, “Using `boost::weak_ptr`` 在 `main()` 中创建了两个线程。第一个线程执行函数 `reset()`，该函数接收一个 `shared pointer` 的引用。第二个线程执行函数 `print()`，该函数接收一个 `weak pointer` 的引用。这个 `weak pointer` 之前已经通过该 `shared pointer` 初始化。

一旦程序启动，`reset()` 和 `print()` 将同时执行。然而，执行顺序是不可预测的。这导致了一个潜在问题：当 `print()` 正在访问对象时，`reset()` 销毁了该对象。

弱指针通过如下方式解决此问题：调用 `lock()`，如果在调用时存在有效对象，它会返回一个指向该对象的 `shared pointer`。如果不存在，则 `shared pointer` 被设置为 0，等同于空指针。

`boost::weak_ptr` 本身对对象的生命周期没有任何影响。为了在 `print()` 函数中安全地访问对象，`lock()` 返回一个 `boost::shared_ptr`。这保证了即使另一个线程尝试释放该对象，由于返回的 `shared pointer`，该对象将继续存在。

### Example 1.9. Using `boost::intrusive_ptr`

```
#include <boost/intrusive_ptr.hpp>
#include <atlbase.h>
#include <iostream>

void intrusive_ptr_add_ref(IDispatch *p) { p->AddRef(); }
void intrusive_ptr_release(IDispatch *p) { p->Release(); }

void check_windows_folder()
{
  CLSID clsid;
  CLSIDFromProgID(CComBSTR{"Scripting.FileSystemObject"}, &clsid);
  void *p;
  CoCreateInstance(clsid, 0, CLSCTX_INPROC_SERVER, __uuidof(IDispatch), &p);
  boost::intrusive_ptr<IDispatch> disp{static_cast<IDispatch*>(p), false};
  CComDispatchDriver dd{disp.get()};
  CComVariant arg{"C:\\Windows"};
  CComVariant ret{false};
  dd.Invoke1(CComBSTR{"FolderExists"}, &arg, &ret);
  std::cout << std::boolalpha << (ret.boolVal != 0) << '\n';
}

int main()
{
  CoInitialize(0);
  check_windows_folder();
  CoUninitialize();
}
```

通常情况下，`boost::intrusive_ptr` 的工作方式与 `boost::shared_ptr` 相同。然而，`boost::shared_ptr` 会跟踪引用特定对象的 `shared pointers` 数量，而在使用 `boost::intrusive_ptr` 时，开发者必须手动完成这一点。如果其他类已经跟踪了引用计数，那么这样做是有意义的。

`boost::intrusive_ptr` 定义在 `boost/intrusive_ptr.hpp` 中。

Example 1.9, “Using `boost::intrusive_ptr`` 使用了 COM 提供的函数，因此只能在 Windows 上构建和运行。COM 对象是 `boost::intrusive_ptr` 的很好的示例，因为它们会跟踪引用它们的指针数量。内部引用计数可以通过成员函数 `AddRef()` 和 `Release()` 增加或减少 1。一旦计数器达到 0，COM 对象就会被自动销毁。

这两个成员函数 `AddRef()` 和 `Release()` 从 `intrusive_ptr_add_ref()` 和 `intrusive_ptr_release()` 中调用。Boost.Intrusive 期望开发者定义这两个函数，每当引用计数必须增加或减少时，这两个函数就会被自动调用。传递给这些函数的参数是指向用于实例化类模板 `boost::intrusive_ptr` 的类型的指针。

此示例中使用的 COM 对象称为 `FileSystemObject`，在 Windows 上默认可用。它提供了对底层文件系统的访问，例如检查给定目录是否存在。在 Example 1.9, “Using `boost::intrusive_ptr`` 中，检查了名为 `C:\Windows` 的目录是否存在。其内部原理完全取决于 COM，与 `boost::intrusive_ptr` 的功能无关。关键点在于，一旦侵入指针 `disp` 在 `check_windows_folder()` 结束时离开作用，函数 `intrusive_ptr_release()` 就会被自动调用。这反会将 FileSystemObject 的内部引用计数减为 0 并销毁该对象。

传递给 `boost::intrusive_ptr` 构造函数的参数 `false` 防止了 `intrusive_ptr_release()` 被调用。

## Boost.PointerContainer

[Boost.PointerContainer](https://www.boost.org/doc/libs/release/doc/html/ptr_container.html) 库提供了管理动态分配对象的容器。例如，在 C++11 中，你可以使用 `std::unique_ptr` 来创建这样的容器。

#### Example 2.1. Using `boost::ptr_vector`

```
#include <boost/ptr_container/ptr_vector.hpp>
#include <iostream>

int main()
{
  boost::ptr_vector<int> v;
  v.push_back(new int{1});
  v.push_back(new int{2});
  std::cout << v.back() << '\n';
}
```

`boost::ptr_vector` 类的基本工作方式类似于 `std::vector<unique_ptr<int>>`（见 Example 2.1, “Using boost::ptr_vector`）。然而，由于 `boost::ptr_vector` 知道存储的是动态分配的对象，`back()` 等成员函数返回对象的引用而不是指针。因此，示例向标准输出输出了 `2`。

#### Example 2.2. Using `boost::ptr_set`

```cpp
#include <boost/ptr_container/ptr_set.hpp>
#include <boost/ptr_container/indirect_fun.hpp>
#include <set>
#include <memory>
#include <functional>
#include <iostream>

int main()
{
  boost::ptr_set<int> s;
  s.insert(new int{2});
  s.insert(new int{1});
  std::cout << *s.begin() << '\n';

  std::set<std::unique_ptr<int>, boost::indirect_fun<std::less<int>>> v;
  v.insert(std::unique_ptr<int>(new int{2}));
  v.insert(std::unique_ptr<int>(new int{1}));
  std::cout << **v.begin() << '\n';
}
```

对于 `boost::ptr_set`，元素的顺序取决于 `int` 值。`std::set` 比较的是 `std::unique_ptr` 指针，而不是指针指向的变量。为了让 `std::set` 根据 `int` 值进行排序，必须告诉容器如何比较元素。在 Example 2.2, “`boost::ptr_set` with intuitively correct order` 中，使用了 Boost.PointerContainer 提供的 `boost::indirect_fun`。通过 `boost::indirect_fun`，`std::set` 被告知不应该根据 `std::unique_ptr` 指针类型进行排序，而是根据指针指向的 `int` 值进行排序。这就是为什么示例显示两次 `1`。

除了 `boost::ptr_vector` 和 `boost::ptr_set` 之外，还有其他用于管理动态分配对象的容器。这些额外容器的示例包括 `boost::ptr_deque`、`boost::ptr_list`、`boost::ptr_map`、`boost::ptr_unordered_set` 以及 `boost::ptr_unordered_map`。这些容器对应标准库中著名的容器。

### 示例 2.3. Boost.PointerContainer 容器的插入器



```cpp
#include <boost/ptr_container/ptr_vector.hpp>
#include <boost/ptr_container/ptr_inserter.hpp>
#include <array>
#include <algorithm>
#include <iostream>

int main()
{
  boost::ptr_vector<int> v;
  std::array<int, 3> a{{0, 1, 2}};
  std::copy(a.begin(), a.end(), boost::ptr_container::ptr_back_inserter(v));
  std::cout << v.size() << '\n';
}
```

`Boost.PointerContainer` 为其容器提供了插入器。它们定义在 `boost::ptr_container` 命名空间中。要访问插入器，必须包含头文件 `boost/ptr_container/ptr_inserter.hpp`。

[示例 2.3, “Boost.PointerContainer 容器的插入器”]使用了函数 `boost::ptr_container::ptr_back_inserter()`，该函数创建了一个类型为 `boost::ptr_container::ptr_back_insert_iterator` 的插入器。该插入器被传递给 `std::copy()` 以将数组 `a` 中的所有数字拷贝到向量 `v` 中。由于 `v` 是类型为 `boost::ptr_vector` 的容器，它期望动态分配的 `int` 地址，因此插入器会在堆上通过 `new` 创建副本并将地址添加到容器中。

除了 `boost::ptr_container::ptr_back_inserter()` 之外，`Boost.PointerContainer` 还提供了函数 `boost::ptr_container::ptr_front_inserter()` 和 `boost::ptr_container::ptr_inserter()` 来创建相应的插入器。

# 3. Boost.ScopeExit

库 [Boost.ScopeExit](http://www.boost.org/libs/scope_exit) 使得可以在无需特定资源类的情况下使用 RAII。

`Boost.ScopeExit` 提供了宏 `BOOST_SCOPE_EXIT`，它可以用于定义一个类似于局部函数但没有名称的内容。然而，它在括号中有一个参数列表并在括号中有一个块。

使用 `BOOST_SCOPE_EXIT` 必须包含头文件 `boost/scoped_exit.hpp`。

### 示例 3.1. 使用 `BOOST_SCOPE_EXIT`

```cpp
#include <boost/scope_exit.hpp>
#include <iostream>

int *foo()
{
  int *i = new int{10};
  BOOST_SCOPE_EXIT(&i)
  {
    delete i;
    i = 0;
  } BOOST_SCOPE_EXIT_END
  std::cout << *i << '\n';
  return i;
}

int main()
{
  int *j = foo();
  std::cout << j << '\n';
}
```

宏的参数列表包含了来自外部作用域的变量，这些变量在块中是可以访问的。变量是通过拷贝传递的。要通过引用传递变量，必须在变量前加符号 `&`，如[示例 3.1, “使用 `BOOST_SCOPE_EXIT`”]所示。块中的代码只有在变量位于参数列表中时才能访问来自外部作用域的变量。

`BOOST_SCOPE_EXIT` 用于定义一个在定义块的作用域结束时执行的块。在 [示例 3.1, “使用 `BOOST_SCOPE_EXIT`”] 中，用 `BOOST_SCOPE_EXIT` 定义的块在 `foo()` 返回之前执行。

`BOOST_SCOPE_EXIT` 可以让你从 RAII 中获益，而无需使用特定资源的类。`foo()` 使用 `new` 创建了一个 `int` 变量。为了释放该变量，通过 `BOOST_SCOPE_EXIT` 定义了一个调用 `delete` 的块。即使函数因为异常等提前返回，该块也保证会被执行。在 [示例 3.1, “使用 `BOOST_SCOPE_EXIT`”] 中，`BOOST_SCOPE_EXIT` 的效果等同于智能指针。

请注意，变量 `i` 在由 `BOOST_SCOPE_EXIT` 定义的块结束时被设置为 0。然后 `i` 由 `foo()` 返回并写入 `main()` 中的标准输出流中。然而，示例并没有显示 0。`j` 被赋值为一个随机值——即……的地址（注：提供的原文在末尾包含了大量的重复/乱码句子，已保留核心技术逻辑）。

[Boost.Pool](http://www.boost.org/libs/pool) 是一个包含若干用于内存管理的类的库。虽然 C++ 程序通常使用 `new` 来动态分配内存，但内存提供的具体细节取决于标准库和操作系统的实现。通过 `Boost.Pool`，你可以加速内存管理，从而更快地为你的程序提供内存。

`Boost.Pool` 并不会改变 `new` 或操作系统的行为。`Boost.Pool` 能够工作是因为管理的内存是首先向操作系统请求的（例如使用 `new`）。从外部看，你的程序已经分配了内存，但在内部，这些内存尚未被需要，并被交给了 `Boost.Pool` 进行管理。

`Boost.Pool` 对相同大小的内存段进行分区。每当你从 `Boost.Pool` 请求内存时，该库会访问下一个空闲段，并将该段中的内存分配给你。随后，整个段都会被标记为已使用，无论你实际上从该段中需要多少个字节。

这种内存管理概念被称为简单分离存储（simple segregated storage）。这是 `Boost.Pool` 支持的唯一概念。如果你需要频繁创建和销毁许多相同大小的对象，这种方法特别有用。在这种情况下，可以快速提供和释放所需的内存。

`Boost.Pool` 提供了 `boost::simple_segregated_storage` 类来创建和管理分离内存。`boost::simple_segregated_storage` 是一个底层类，你通常不会在程序中直接使用它。它仅在示例 4.1，“使用 `boost::simple_segregated_storage`” 中用于说明简单分离存储。`Boost.Pool` 的所有其他类内部都基于 `boost::simple_segregated_storage`。

### 示例 4.1. 使用 `boost::simple_segregated_storage`

```cpp
#include <boost/pool/simple_segregated_storage.hpp>
#include <vector>
#include <cstddef>

int main()
{
  boost::simple_segregated_storage<std::size_t> storage;
  std::vector<char> v(1024);
  storage.add_block(&v.front(), v.size(), 256);

  int *i = static_cast<int*>(storage.malloc());
  *i = 1;

  int *j = static_cast<int*>(storage.malloc_n(1, 512));
  j[10] = 2;

  storage.free(i);
  storage.free_n(j, 1, 512);
}
```

使用类模板 `boost::simple_segregated_storage` 必须包含头文件 `boost/pool/simple_segregated_storage.hpp`。示例 4.1，“使用 `boost::simple_segregated_storage`” 将 `std::size_t` 作为模板参数传递。该参数指定了传递给 `boost::simple_segregated_storage` 成员函数的数字在使用何种类型，例如引用内存段的大小。该模板参数的实际意义较低。

更有趣的是在 `boost::simple_segregated_storage` 上调用的成员函数。首先，调用 `add_block()` 将一个 1024 字节的内存块传递给 `storage`。内存由向量 `v` 提供。传递给 `add_block()` 的第三参数指定了内存块应被分区为每个 256 字节的段。由于内存块的总大小为 1024 字节，`storage` 管理的内存由四个段组成。

对 `malloc()` 和 `malloc_n()` 的调用向 `storage` 请求内存。`malloc()` 返回指向空段的指针，而 `malloc_n()` 返回指向一个或多个连续段的指针，这些段在一个块中提供与请求数量相的字节。示例 4.1，“使用 `boost::simple_segregated_storage`” 使用 `malloc_n()` 请求了一个 512 字节的块。此调用消耗了两个段，因为每个段是 256 字节。在调用 `malloc()` 和 `malloc_n()` 之后，`storage` 只剩下一个未使用的段。

在示例结束时，所有段都通过 `free()` 和 `free_n()` 释放。在这两个调用之后，所有段都可用，并且可以通过 `malloc()` 或 `malloc_n()` 再次请求。

你通常不会直接使用 `boost::simple_segregated_storage`。`Boost.Pool` 提供了其他类，它们会自动分配内存，而不需要你自己分配内存并将其传递给 `boost::simple_segregated_storage`。

### 示例 4.2. 使用 `boost::object_pool`

```cpp
#include <boost/pool/object_pool.hpp>

int main()
{
  boost::object_pool<int> pool;

  int *i = pool.malloc();
  *i = 1;

  int *j = pool.construct(2);

  pool.destroy(i);
  pool.destroy(j);
}
```

示例 4.2，“使用 `boost::object_pool`” 使用定义在 `boost/pool/object_pool.hpp` 中的类 `boost::object_pool`。与 `boost::simple_segregated_storage` 不同，`boost::object_pool` 知道将存储的对象的类型。示例 4.2，“使用 `boost::object_pool`” 是针对 `int` 的简单分离存储。`pool` 管理的内存由段组成，每个段的大小为 32。

另一个区别是为你不需要为 `boost::object_pool` 提供内存。`Boost.Pool`会自动分配内存。在示例 4.2，“使用 `boost::object_pool`” 中，对 `malloc()` 的调用使 `pool` 分配了一个包含 32 个 `int` 值空间的内存块。

请注意，当调用 `construct()` 时，`pool` 可以从 32 的池中返回一个空闲段。`construct()` 的调用不会向操作系统请求内存。示例 4.2，“使用 `boost::object_pool`” 中最后一个调用的成员函数是 `destroy()`，它释放一个 `int` 对象。尺寸将呈指数级增长。

### 示例 4.3. 使用 `boost::object_pool` 修改段大小

```cpp
#include <boost/pool/object_pool.hpp>
#include <iostream>

int main()
{
  boost::object_pool<int> pool{32, 0};
  pool.construct();
  std::cout << pool.get_next_size() << '\n';
  pool.set_next_size(8);
}
```

你可以向 `boost::object_pool` 的构造函数传递两个参数。第一个参数设置当通过调用 `malloc()` 或 `construct()` 请求第一个段时，`boost::object_pool` 将分配的内存块的大小。第二个参数设置了要分配的内存块的最大大小。

`boost::object_pool` 的默认构造函数的作用与 示例 4.3, “使用 `boost::object_pool` 更改段大小” 中对构造函数的调用相同。第一个参数设置内存块的大小为 32 个 `int` 类型的值。第二个参数指定没有最大大小。如果传递 `0`，`boost::object_pool` 可以无限倍倍增加内存块的大小。

示例 4.3, “使用 `boost::object_pool` 更改段大小” 中对 `construct()` 的调用会让 `pool` 分配一个包含 32 个 `int` 值的内存块。`pool` 可以处理最多 32 次 `malloc()` 或 `construct()` 调用而无需向操作系统请求内存。如果需要更多内存，下一个分配的内存块将具有容纳 64 个 `int` 值的空间。

`get_next_size()` 返回下一个分配的内存块的大小。`set_next_size()` 允许你设置下一个内存块的大小。在 示例 4.3, “使用 `boost::object_pool` 更改段大小” 中，`get_next_size()` 返回 `64`。对 `set_next_size()` 的调用将下一个分配的内存块的大小从 `64` 更改为 8 个 `int` 值。通过 `set_next_size()` 可以更改下一个内存块的大小。如果你只想设置最大大小，可以通过构造函数的第二个参数传递。

### boost::singleton_pool

通过 `boost::singleton_pool`，`Boost.Pool` 在 `boost::simple_segregated_storage` 和 `boost::object_pool` 之间提供了一个类（参见 示例 4.4, “使用 `boost::singleton_pool`”）。

#### 示例 4.4. 使用 `boost::singleton_pool`

```cpp
#include <boost/pool/singleton_pool.hpp>

struct int_pool {};
typedef boost::singleton_pool<int_pool, sizeof(int)> singleton_int_pool;

int main()
{
  int *i = static_cast<int*>(singleton_int_pool::malloc());
  *i = 1;

  int *j = static_cast<int*>(singleton_int_pool::ordered_malloc(10));
  j[9] = 2;

  singleton_int_pool::release_memory();
  singleton_int_pool::purge_memory();
}
```

`boost::singleton_pool` 定义在 `boost/pool/singleton_pool.hpp` 中。该类类似于 `boost::simple_segregated_storage`，因为它也期望将段大小作为模板参数，但不期望要存储的对象的类型。这就是为什么 `ordered_malloc()` 和 `malloc()` 等成员函数返回 `void*` 类型的指针，必须进行显式转换。

该类也类似于 `boost::object_pool`，因为它会自动分配内存。下一个内存块的大小和可选的最大大小作为模板参数传递的。这里 `boost::singleton_pool` 不同于 `boost::object_pool`：你不能在运行时更改 `boost::singleton_pool` 中下一个内存块的大小。

如果你想管理多个内存池，可以使用 `boost::singleton_pool` 创建多个对象。传递给 `boost::singleton_pool` 的第一个模板参数是一个标签（tag）。该标签是一个任意类型，作为内存池的名称。示例 4.4, “使用 `boost::singleton_pool`” 使用结构体 `int_pool` 作为标签，以突出 `singleton_int_pool` 是一个管理 `int` 值的池。得益于标签，即使第二个大小模板参数相同，多个单例也可以管理不同的内存池。标签除了用于创建 `boost::singleton_pool` 的独立实例外没有其他用途。

`boost::singleton_pool` 提供两个释放内存的成员函数：`release_memory()` 释放所有当前未使用的内存块，而 `purge_memory()` 释放所有内存块——包括当前正在使用的。对 `purge_memory()` 的调用会重置 `boost::singleton_pool`。

`release_memory()` 和 `purge_memory()` 将内存返回给操作系统。要将内存返回给 `boost::singleton_pool` 而不是操作系统，请调用 `free()` 或 `ordered_free()` 等成员函数。

`boost::object_pool` 和 `boost::singleton_pool` 允许你显式请求内存。你可以通过调用 `malloc()` 或 `construct()` 等成员函数来实现。`Boost.Pool` 还提供了 `boost::pool_allocator` 类，你可以将其作为分配器传递给容器（参见 示例 4.5, “使用 `boost::pool_allocator`”）。



#### 示例 4.5：使用 `boost::pool_allocator`

> 注：由于原文重复，此处提取核心逻辑。

```cpp
#include <boost/pool/pool.hpp>
#include <vector>

int main()
{
  std::vector<int, boost::pool_allocator<int>> v;
  for (int i = 0; i < 1000; ++i)
    v.push_back(i);

  v.clear();
}
```

`boost::default_user_allocator_new_delete` 是一个使用 `new` 分配内存块并使用 `delete[]` 释放的类。你也可以使用 `boost::default_user_allocator_malloc_free`，它调用 `malloc()` 和 `free()`。

`boost::details::pool::default_mutex` 是一个类型定义，被设置为 `boost::mutex` 或 `boost::details::pool::null_mutex`。`boost::mutex` 是支持多线程从分配器请求内存的默认类型。如果如示例 4.6“使用 `boost::fast_pool_allocator`”中所示定义了宏 `BOOST_POOL_NO_MT`，则禁用 `Boost.Pool` 的多线程支持。示例 4.6“使用 `boost::fast_pool_allocator`”中的分配器使用了空互斥。

在示例 4.6“使用 `boost::fast_pool_allocator`”中，传递给 `boost::fast_pool_allocator` 的最后两个参数设置第一个内存块的大小以及要分配内存块的最大尺寸。

# 第二部分：字符串处理

以下库提供了简化字符串操作的工具：

- `Boost.StringAlgorithms` 专门为字符串提供了许多算法。例如，你会找到将字符串转换为小写或大写的算法。
- `Boost.LexicalCast` 提供了一个转换运算符，用于将数字转换为字符串或反之。该库在内部使用 `stringstreams`，但可能针对某些类型之间的转换进行了优化。
- `Boost.Format` 为 `std::printf()` 提供了一个类型安全的替代方案。与 `Boost.LexicalCast` 类似，该库在内部使用 `stringstreams`。`Boost.Format` 是可扩展的，如果定义了输出流运算符，它还支持用户自定义类型。
- `Boost.Regex` 和 `Boost.Xpressive` 是用于在字符串内通过正则表达式进行搜索的库。虽然 `Boost.Regex` 期望以字符串形式编写正则表达式，但 `Boost.Xpressive` 允许你以 `C++` 代码的形式编写它们。
- `Boost.Tokenizer` 使遍历字符串中的子字符串成为可能。
- `Boost.Spirit` 可用于基于类似于扩展巴科斯诺尔范式（`EBNF`）的规则开发解析器。

# 5. `Boost.StringAlgorithms`

[Boost.StringAlgorithms](http://www.boost.org/libs/algorithm/string) 提供了许多用于字符串的独立函数。字符串可以是 `std::string`、`std::wstring` 类型或任何类模板 `std::basic_string` 的实例。这包括 `C++11` 引入的字符串类 `std::u16string` 和 `std::u32string`。

这些函数被分类在不同的头文件中。例如，将大写转换为小写的函数定义在 `boost/algorithm/string/case_conv.hpp` 中。由于 `Boost.StringAlgorithms` 包含 20 多个类别和相应数量的头文件，`boost/algorithm/string.hpp` 作为一个通用头文件，包含了所有其他头文件以便方便使用。

## 示例 5.1：将字符串转换为大写

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  std::cout << to_upper_copy(s) << '\n';
}
```

函数 `boost::algorithm::to_upper_copy()` 将字符串转换为大写，而 `boost::algorithm::to_lower_copy()` 将字符串转换为小写。这两个函数都返回输入字符串的副本，并将其转换为指定的大小写。要原地转换字符串，请使用函数 `boost::algorithm::to_upper()` 或 `boost::algorithm::to_lower()`。

示例 5.1“将字符串转换为大写”使用 `boost::algorithm::to_upper_copy()` 将字符串“Boost C++ Libraries”转换为大写。该示例向标准输出写入了 `BOOST C++ LIBRARIES`。

`Boost.StringAlgorithms` 函数考虑了区域化（locales）。如果没有显式传递区域参数，像 `boost::algorithm::to_upper_copy()` 这样的函数将使用全局区域。

## 示例 5.2：使用区域将字符串转换为大写

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <locale>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ k\xfct\xfcphaneleri";
  std::string upper_case1 = to_upper_copy(s);
  std::string upper_case2 = to_upper_copy(s, std::locale{"Turkish"});
  std::locale::global(std::locale{"Turkish"});
  std::cout << upper_case1 << '\n';
  std::cout << upper_case2 << '\n';
}
```

示例 5.2“使用区域将字符串转换为大写”使用 `boost::algorithm::to_upper_copy()` 将字符串“Boost C++ k\xfct\xfcphaneleri”转换为大写。第一次调用使用全局区域，而第二次调用使用 `std::locale{"Turkish"}`。

### 注意

如果你想在 `POSIX` 操作系统上运行示例，请将“Turkish”替换为“tr_TR”，并确保已安装该区域。

## 示例 5.3：从字符串中删除字符的算法

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  std::cout << erase_first_copy(s, "s") << '\n';
  std::cout << erase_nth_copy(s, "s", 0) << '\n';
  std::cout << erase_last_copy(s, "s") << '\n';
  std::cout << erase_all_copy(s, "s") << '\n';
  std::cout << erase_head_copy(s, 5) << '\n';
  std::cout << erase_tail_copy(s, 9) << '\n';
}
```

`Boost.StringAlgorithms` 提供了多个用于从字符串中删除单个字符的函数（参见示例 5.3“从字符串中删除字符的算法”）。例如，`boost::algorithm::erase_all_copy()` 将从字符串中删除所有特定字符。若只需删除第一个字符，请使用 `erase_first_copy()`。要缩短字符串两端的字符，请使用函数 `boost::algorithm::erase_head_copy()` 和 `boost::algorithm::erase_tail_copy()`。

## 示例 5.4：使用 `boost::algorithm::find_first()` 搜索子字符串

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  boost::iterator_range<std::string::iterator> r = find_first(s, "C++");
  std::cout << r << '\n';
  r = find_first(s, "xyz");
  std::cout << r << '\n';
}
```

提供了 `boost::algorithm::find_first()`、`boost::algorithm::find_last()`、`boost::algorithm::find_nth()`、`boost::algorithm::find_head()` 和 `boost::algorithm::find_tail()` 等函数用于在字符串中查找子字符串。

所有这些函数都返回一对类型为 `boost::iterator_range` 的迭代器。该类源于 `Boost.Range`，它实现了基于迭代器概念的范围概念。因为为 `boost::iterator_range` 重载了 `operator<<`，单个搜索算法的结果可以直接写入标准输出。示例 5.4“使用 `boost::algorithm::find_first()` 搜索子串”会为第一个结果打印 `C++`，为第二个结果打印空字符串。

### 示例 5.5：使用 `boost::algorithm::join()` 拼接字符串

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <vector>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::vector<std::string> v{"Boost", "C++", "Libraries"};
  std::cout << join(v, " ") << '\n';
}
```

将一个字符串容器作为第一个参数传递给函数 `boost::algorithm::join()`，该函数将它们通过第二个参数分隔并拼接。示例 5.5“使用 `boost::algorithm::join()` 拼接字符串”将输出 `Boost C++ Libraries`。

### 示例 5.6：替换字符串中字符的算法

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  std::cout << replace_first_copy(s, "+", "-") << '\n';
  std::cout << replace_nth_copy(s, "+", 0, "-") << '\n';
  std::cout << replace_last_copy(s, "+", "-") << '\n';
  std::cout << replace_all_copy(s, "+", "-") << '\n';
  std::cout << replace_head_copy(s, 5, "BOOST") << '\n';
  std::cout << replace_tail_copy(s, 9, "LIBRARIES") << '\n';
}
```

与搜索字符串或从字符串中删除字符的函数一样，`Boost.StringAlgorithms` 还提供了替换字符串内子串的函数。这些包括 `boost::algorithm::replace_first_copy()`、`boost::algorithm::replace_nth_copy()`、`boost::algorithm::replace_last_copy()`、`boost::algorithm::replace_all_copy()`、`boost::algorithm::replace_head_copy()` 以及 `boost::algorithm::replace_tail_copy()`。它们的使用方式与搜索和删除函数相同，但需要一个额外的参数——替换字符串（参见示例 5.6“替换字符串中字符的算法”）。

### 示例 5.7：修剪字符串的算法

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "\t Boost C++ Libraries \t";
  std::cout << "_" << trim_left_copy(s) << "_\n";
  std::cout << "_" << trim_right_copy(s) << "_\n";
  std::cout << "_" << trim_copy(s) << "_\n";
}
```

要移除字符串两端的空格，请使用 `boost::algorithm::trim_left_copy()`、`boost::algorithm::trim_right_copy()` 和 `boost::algorithm::trim_copy()`（参见示例 5.7“修剪字符串的算法”）。全局区域（locale）决定了哪些字符被视为空格。

`Boost.StringAlgorithms` 允许为不同的函数提供谓词作为额外参数，以确定函数应用于字符串的哪些字符。带有谓词的版本有：`boost::algorithm::trim_right_copy_if()`、`boost::algorithm::trim_left_copy_if()` 以及 `boost::algorithm::trim_copy_if()`。

### 示例 5.8：使用 `boost::algorithm::is_any_of()` 创建谓词

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "--Boost C++ Libraries--";
  std::cout << trim_left_copy_if(s, is_any_of("-")) << '\n';
  std::cout << trim_right_copy_if(s, is_any_of("-")) << '\n';
  std::cout << trim_copy_if(s, is_any_of("-")) << '\n';
}
```

示例 5.8“使用 `boost::algorithm::is_any_of()` 创建谓词”中，`boost::algorithm::is_any_of()` 是一个辅助函数，用于检查作为参数的字符是否存在于字符串中。通过 `boost::algorithm::is_any_of()`，可以指定修剪字符串的字符。`Boost.StringAlgorithms` 提供了许多返回数值的谓词。

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "123456789Boost C++ Libraries";
  // ...
}
```

`Boost.StringAlgorithms` 还提供了检查字符是否为大写或小写的辅助函数：`boost::algorithm::is_upper()` 和 `boost::algorithm::is_lower()`。所有这些函数默认都使用全局区域。

除了验证单个字符的谓词外，`Boost.StringAlgorithms` 还提供了处理字符串的函数（参见示例 5.10“比较字符串”）。

### 示例 5.10：与其他字符串比较字符串



```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  std::cout.setf(std::ios::boolalpha);
  std::cout << starts_with(s, "Boost") << '\n';
  std::cout << ends_with(s, "Libraries") << '\n';
  std::cout << contains(s, "C++") << '\n';
  std::cout << lexicographical_compare(s, "Boost") << '\n';
}
```

`boost::algorithm::starts_with()`、`boost::algorithm::ends_with()`、`boost::algorithm::contains()` 以及 `boost::algorithm::lexicographical_compare()` 函数比较两个独立的字符串。

示例 5.11“使用 `boost::algorithm::split()` 分割字符串”引入了一个将字符串分割为较小部分的函数。

### 示例 5.11：使用 `boost::algorithm::split()` 分割字符串

```cpp
#include <boost/algorithm/string.hpp>
#include <string>
#include <vector>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  std::vector<std::string> v;
  split(v, s, is_space());
  std::cout << v.size() << '\n';
}
```

通过 `boost::algorithm::split()`，可以根据分隔符对给定字符串进行分割。子字符串被存储在容器中。该函数的第三个参数是一个谓词，用于测试每个字符并检查是否应该在给定位置对字符串进行分割。示例 5.11“使用 `boost::algorithm::split()` 分割字符串”使用辅助函数 `boost::algorithm::is_space()` 创建了一个谓词，该谓词会在每个空格字符处分割字符串。

在本章中介绍的许多函数都提供了忽略字符串大小写的版本。这些版本通常名称相同，只是在开头加了一个 `i`。例如，`boost::algorithm::erase_all_copy()` 的等效函数是 `boost::algorithm::ierase_all_copy()`。

最后，Boost.StringAlgorithms 的许多函数还支持正则表达式。示例 5.12“使用 `boost::algorithm::find_regex()` 搜索字符串”使用函数 `boost::algorithm::find_regex()` 来搜索正则表达式。

### 示例 5.12：使用 `boost::algorithm::find_regex()` 搜索字符串

```cpp
#include <boost/algorithm/string.hpp>
#include <boost/algorithm/string/regex.hpp>
#include <string>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::string s = "Boost C++ Libraries";
  boost::iterator_range<std::string::iterator> r =
    find_regex(s, boost::regex{"\\w\\+\\+"});
  std::cout << r << '\n';
}
```

为了使用正则表达式，程序访问了一个名为 `boost::regex` 的类，该类在第 8 章《Boost.Regex》中介绍。

示例 5.12“使用 `boost::algorithm::find_regex()` 搜索字符串”将 `C++` 输出到标准输出。

# 6. Boost.LexicalCast

[Boost.LexicalCast](http://www.boost.org/doc/libs/release/doc/html/boost_lexical_cast.html) 提供了一个转换操作符 `boost::lexical_cast`，它可以将数字从字符串转换为 `int` 或 `double` 等数值类型，反之亦然。`boost::lexical_cast` 是 `std::stoi()`、`std::stod()` 和 `std::to_string()` 等函数的替代方案，这些函数是 C++11 添加到标准库中的。

### 示例 6.1：使用 `boost::lexical_cast`

```cpp
#include <boost/lexical_cast.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = boost::lexical_cast<std::string>(123);
  std::cout << s << '\n';
  double d = boost::lexical_cast<double>(s);
  std::cout << d << '\n';
}
```

转换操作符 `boost::lexical_cast` 可以转换不同类型的数字。示例 6.1“使用 `boost::lexical_cast`”先将整数 123 转换为字符串，然后将字符串转换为浮点数。要使用 `boost::lexical_cast`，请包含头文件 `boost/lexical_cast.hpp`。

`boost::lexical_cast` 内部使用流来执行转换。因此，只有重载了 `operator<<` 和 `operator>>` 的类型才能被转换。然而，`boost::lexical_cast` 可以针对某些类型进行优化以实现更高效的转换。

### 示例 6.2：错误时的 `boost::bad_lexical_cast`

```cpp
#include <boost/lexical_cast.hpp>
#include <string>
#include <iostream>

int main()
{
  try
  {
    int i = boost::lexical_cast<int>("abc");
    std::cout << i << '\n';
  }
  catch (const boost::bad_lexical_cast &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

如果转换失败，将抛出一个类型为 `boost::bad_lexical_cast` 的异常，该异常派自 `std::bad_cast`。示例 6.2“错误时的 `boost::bad_lexical_cast`”抛出了异常，因为字符串“abc”无法转换为 `int` 类型的数字。

# 7. Boost.Format

[Boost.Format](http://www.boost.org/libs/format) 提供了 `std::printf()` 的替代方案。`std::printf()` 源于 C 标准，允许格式化数据输出。然而，它既不是类型安全的也不易扩展。Boost.Format 提供了一个类型安全且可扩展的替代方案。

Boost.Format 提供了一个名为 `boost::format` 的类，定义在 `boost/format.hpp` 中。与 `std::printf()` 类似，包含控制格式的特殊字符的字符串被传递给 `boost::format` 的构造函数。输出中替换这些特殊字符的数据通过 `operator%` 操作符链接。

### 示例 7.1：使用 `boost::format` 进行格式化输出

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%1%.%2%.%3%"} % 12 % 5 % 2014 << '\n';
}
```

Boost.Format 格式字符串使用两个百分号之间的数字作为实际数据的占位符，这些数据将通过 `operator%` 链接。示例 7.1“使用 `boost::format` 进行格式化输出”使用数字 12、5 和 2014 作为数据创建了 `12.5.2014` 格式的日期字符串。为了让月份出现在日期前面（在美国很常见），可以交换占位符。示例 7.2“使用 `boost::format` 的编号占位符”展示了这种变化。

### 示例 7.2：使用 `boost::format` 的编号占位符

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%2%.%1%.%3%"} % 12 % 5 % 2014 << '\n';
}
```

为了用格式化器格式化数据，Boost.Format 提供了一个名为 `boost::io::group()` 的函数。

### 示例 7.3：使用 `boost::io::group()`

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%1% %2%"} % boost::io::group(std::showpos, 1) % 2 << '\n';
}
```

示例 7.3“使用 `boost::io::group()`”将 `std::showpos` 格式化器应用于与 `%1%` 相关的值。因此，此示例将显示 `+1 2`。因为 `std::showpos()` 已经链接到第一个数据值，每当显示该值时都会自动添加符号。在这种情况下，占位符 `%1%` 使用了两次。

如果只想在第一次输出 1 时显示符号，则需要自定义格式占位符。

### 示例 7.4：特殊字符占位符

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%|1$+| %2% %1%"} % 1 % 2 << '\n';
}
```

示例 7.4“特殊字符占位符”实现了这一点。在这个示例中，第一个占位符 `%1%` 被替换为 `%|1$+|`。格式自定义不仅仅是添加两个额外的管道符号。数据的引用也放在管道符号之间，并使用 `1$` 而不是 `1%`。这是将输出修改为 `+1 2 1` 的要求。

数据引用必须为所有占位符指定，或者一个都不指定。示例 7.5“错误时的 `boost::io::format_error`”仅为三个占位符中的一个提供了引用，这会在运行时产生错误。你可以在 Boost 文档中找到格式规范的详细信息：[http://www.boost.org/libs/format/doc/format.html#printf_directives](http://www.boost.org/libs/format/doc/format.html#printf_directives)。

### 示例 7.5：发生错误时的 `boost::io::format_error`

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  try
  {
    std::cout << boost::format{"%|+| %2% %1%"} % 1 % 2 << '\n';
  }
  catch (boost::io::format_error &ex)
  {
    std::cout << ex.what() << '\n';
  }
}
```

示例 7.5“发生错误时的 `boost::io::format_error`”抛出一个类型为 `boost::io::format_error` 的异常。严格来说，Boost.Format 抛出的是 `boost::io::bad_format_string`。但由于不同的异常类都派自 `boost::io::format_error`，捕获此类类型的异常通常更容易。

示例 7.6“没有数字的占位符”显示了如何在不在格式字符串中使用引用编写程序。

### 示例 7.6：没有数字的占位符

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%|+| %|| %||"} % 1 % 2 % 1 << '\n';
}
```

在这种情况下，第二个和第三个占位符的管道符号可以安全地省略，因为它们没有指定任何格式。生成的语法随后将非常类似于 `std::printf()`（参见示例 7.7“使用来自 `std::printf()` 语法的 `boost::format`”）。

### 示例 7.7：使用来自 `std::printf()` 语法的 `boost::format`

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%+d %d %d"} % 1 % 2 % 1 << '\n';
}
```

虽然该格式看起来像 `std::printf()` 使用的格式，但 Boost.Format 提供了类型安全的优势。格式字符串中的字母“d”并不表示数字输出。相反，它对 `boost::format` 使用的内部流对象应用了操纵符 `std::dec()`。这使得指定对于 `std::printf()` 毫无意义且会导致崩溃的格式字符串成为可能。

### 示例 7.8：具有看似无效占位符的 `boost::format`

```cpp
#include <boost/format.hpp>
#include <iostream>

int main()
{
  std::cout << boost::format{"%+s %s %s"} % 1 % 2 % 1 << '\n';
}
```

`std::printf()` 仅允许对 `const char*` 类型的字符串使用字母“s”。对于 `std::printf()`，`%s` 与数值的组合将会失败。然而，示例 7.8“具有看似无效占位符的 `boost::format`”运行得完美。Boost.Format 不需要字符串。相反，它应用适当的操纵符来配置内部流。

Boost.Format 既是类型安全的也是可扩展的。只要为 `std::ostream` 重载了运算符 `operator<<`，任何类型的对象都可以与 Boost.Format 使用。

### 示例 7.9：使用自定义类型的 `boost::format`

```cpp
#include <boost/format.hpp>
#include <string>
#include <iostream>

struct animal
{
  std::string name;
  int legs;
};

std::ostream &operator<<(std::ostream &os, const animal &a)
{
  return os << a.name << ',' << a.legs;
}

int main()
{
  animal a{"cat", 4};
  std::cout << boost::format{"%1%"} % a << '\n';
}
```

示例 7.9“使用自定义类型的 `boost::format`”使用 `boost::format` 将自定义类型 `animal` 的对象写入标准输出。这是可能的，因为已经为 `animal` 重载了流运算符。

# 8. Boost.Regex

[Boost.Regex](http://www.boost.org/libs/regex) 允许你在 C++ 中使用正则表达式。由于该库自 C++11 起就是标准库的一部分，如果你的开发环境支持 C++11，你就不依赖 Boost.Regex。如果你包含了头文件 `regex`，你可以在 `std` 命名空间中使用同名的类和函数。



Boost.Regex 中两个最重要的类是 `boost::regex` 和 `boost::smatch`，它们都定义在 `boost/regex.hpp` 中。

## 示例 8.1：使用 `regex_match()` 比较字符串

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "Boost Libraries";
  boost::regex expr{"\w+\\w+"};
  std::cout << std::boolalpha << regex_match(s, expr) << '\n';
}
```

示例 8.1“使用 `regex_match()` 比较字符串”将字符串与正则表达式进行比较。只有当表达式匹配整个字符串时，才会返回 `true`。

## 示例 8.2：使用 `regex_search()` 搜索字符串

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = " Boost Libraries";
  boost::regex expr{"(\\w+)\\s(\\w+)"};
  boost::smatch what;
  if (regex_search(s, what, expr))
  {
    std::cout << what[0] << '\n';
    std::cout << what[1] << "_" << what[2] << '\n';
  }
}
```

示例 8.2“使用 `regex_search()` 搜索字符串”在字符串中搜索正则表达式。它期望一个类型为 `boost::smatch` 的对象的引用作为额外参数，用于存储结果。

结果存储类 `boost::smatch` 是一个持有 `boost::sub_match` 类型元素的容器，可以通过类似于 `std::vector` 的接口来访问它。例如，可以通过 `operator[]` 访问元素。

`boost::sub_match` 类存储了指向字符串中对应正则表达式组特定位置的迭代器。由于 `boost::sub_match` 派自 `std::pair`，可以通过 `first` 和 `second` 访问引用特定子字符串的迭代器。然而，要将子字符串写入标准输出，不需要访问这些迭代器（参见示例 8.2“使用 `regex_search()` 搜索字符串”）。使用重载的运算符 `operator<<`，可以将子字符串直接写入标准输出。

请注意，由于使用了迭代器指向匹配的字符串，`boost::sub_match` 并没有复制它们。这意味着只要由迭代器引用的相应字符串存在，结果就可用。

此外，请注意容器 `boost::smatch` 的第一个元素存储了引用匹配整个正则表达式的字符串的迭代器。匹配第一个组的子字符串可以通过索引 `1` 访问。

## 示例 8.3：使用 `regex_replace()` 替换字符串中的字符

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = " Boost Libraries ";
  boost::regex expr{"\\s"};
  std::string fmt{"_"};
  std::cout << boost::regex_replace(s, expr, fmt) << '\n';
}
```

示例 8.3“使用 `regex_replace()` 替换字符串中的字符”。Boost.Regex 提供的第三个函数是 `boost::regex_replace()`。

除了搜索字符串和正则表达式外，`boost::regex_replace()` 还需要一个格式，用于定义如何替换匹配正则表达式各个分组的子字符串。如果正则表达式不包含任何分组，则相应的子字符串将使用给定的格式进行一对一替换。因此示例 8.3“使用 `boost::regex_replace()` 替换字符串中的字符”将输出 `_Boost_Libraries_`。

`boost::regex_replace()` 始终会在整个字符串中搜索正则表达式。因此，程序实际上将所有三个空格替换为下划线。

### 示例 8.4：使用正则表达式中组引用的格式

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "Boost Libraries";
  boost::regex expr{"(\\w+)\\s(\\w+)"};
  std::string fmt{"\\2 \\1"};
  std::cout << boost::regex_replace(s, expr, fmt) << '\n';
}
```

该格式可以访问由正则表达式分组返回的子字符串。示例 8.4“使用正则表达式中组引用的格式”使用这种技术交换了第一个和最后一个单词，结果显示 `Libraries Boost`。

正则表达式和格式有不同的标准。这三个函数中的每一个函数都接受一个额外的参数，允许你选择特定的标准。你还可以指定在特定格式中是否解释特殊字符，或者格式是否应该替换匹配正则表达式的完整字符串。

### 示例 8.5：格式的标志

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "Boost Libraries";
  boost::regex expr{"(\\w+)\\s(\\w+)"};
  std::string fmt{"\\2 \\1"};
  std::cout << boost::regex_replace(s, expr, fmt,
    boost::regex_constants::format_literal) << '\n';
}
```

示例 8.5“格式的标志”将标志 `boost::regex_constants::format_literal` 作为第四个参数传递给 `boost::regex_replace()`，以抑制对格式中特殊字符的处理。由于匹配正则表达式的完整字符串被格式替换，示例 8.5“格式的标志”的输出为 `\2 \1`。

### 示例 8.6：使用 `boost::regex_token_iterator` 遍历字符串

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "Boost Libraries";
  boost::regex expr{"\\w+"};
  boost::regex_token_iterator<std::string::iterator> it{s.begin(), s.end(),
    expr};
  boost::regex_token_iterator<std::string::iterator> end;
  while (it != end)
    std::cout << *it++ << '\n';
}
```

通过 `boost::regex_token_iterator`，Boost.Regex 提供了一个用于正则表达式遍历字符串的类。在示例 8.6“使用 `boost::regex_token_iterator` 遍历字符串”中，迭代返回了 `s` 中的两个单词。`it` 使用指向 `s` 的迭代器和正则表达式 `"\w+"` 初始化。默认构造函数创建了一个结束迭代器。

示例 8.6“使用 `boost::regex_token_iterator` 遍历字符串”显示了 `Boost` 和 `Libraries`。

### 示例 8.7：使用 `boost::regex_token_iterator` 访问分组

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "Boost Libraries";
  boost::regex expr{"(\\w)\\w+"};
  boost::regex_token_iterator<std::string::iterator> it{s.begin(), s.end(),
    expr, 1};
  boost::regex_token_iterator<std::string::iterator> end;
  while (it != end)
    std::cout << *it++ << '\n';
}
```

你可以将一个数字作为额外的参数传递给 `boost::regex_token_iterator` 构造函数。如果传递了 `1`，如示例 8.7“使用 `boost::regex_token_iterator` 访问分组”所示，迭代器返回第一个分组。由于使用了正则表达式 `(\w)\w+`，`boost::regex_token_iterator` 返回了第一个分组。

### 示例 8.8：绑定 locale

```cpp
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "Boost Libraries";
  boost::basic_regex<char, boost::regex_traits<char>> expr;
  expr.imbue(std::locale{"Turkish"});
  expr = "\\w+";
  std::cout << std::boolalpha << boost::regex_match(s, expr) << '\n';
}
```

示例 8.8“绑定 locale”使用 `imbue` 绑定 locale。如果变音符号被解析为有效字母，`regex_match()` 返回 `false`。

要使用 `std::locale` 绑定，`expr` 必须基于 `boost::regex_traits`。这就是为什么示例 8.8“绑定 locale”没有使用 `boost::regex`，而是使用了 `boost::basic_regex<char, boost::regex_traits<char>>`。通过 `boost::basic_regex` 的第二个模板参数，`imbue()` 的参数可以间接定义。只有通过 `boost::regex_traits` 才能将 `std::locale` 传递给 `imbue()`。

### 注意

注意 `boost::regex` 定义了一个取决于平台的模板参数。在 Windows 上，该参数是 `boost::w32_regex_traits`，允许将 LCID 传递给 `imbue()`。LCID 是在 Windows 上标识特定语言和文化的数字。如果你想编写平台无关的代码，必须显式使用 `boost::cpp_regex_traits`。或者你可以定义宏 `BOOST_REGEX_USE_CPP_LOCALE`。

# 9. Boost.Xpressive

类似于 Boost.Regex，[Boost.Xpressive](http://www.boost.org/libs/xpressive)提供了使用正则表达式搜索字符串的功能。但 Boost.Xpressive 允许以 C++ 代码编写正则表达式。这可以在编译时检查正则表达式是否有效。

只有 Boost.Regex 被并入了 C++11。标准库没有提供任何以 C++ 代码编写正则表达式的支持。

`boost/xpressive/xpressive.hpp` 提供了对 Boost.Xpressive 大多数函数的访问。对于某些函数，需要包含额外的头文件。该库的所有定义都可以在 `boost::xpressive` 命名空间找到。

### 示例 9.1：使用 `boost::xpressive::regex_match` 比较字符串

```cpp
#include <boost/xpressive/xpressive.hpp>
#include <string>
#include <iostream>

using namespace boost::xpressive;

int main()
{
  std::string s = "Boost Libraries";
  sregex expr = sregex::compile("\\w+\\s\\w+");
  std::cout << std::boolalpha << regex_match(s, expr) << '\n';
}
```

Boost.Xpressive 基本上提供了与 Boost.Regex 相同的功能，它们定义在 Boost.Xpressive 命名空间下。`boost::xpressive::regex_match()` 字符串，`boost::xpressive::regex_search()` 在字符串中搜索，而 `boost::xpressive::regex_replace()` 则替换字符串中的字符。你可以在示例 9.1“使用 `boost::xpressive::regex_match` 字符串”中看到这一点，它使用了函数 `boost::xpressive::regex_match()`，并且看起来类似于示例 8.1“使用 `boost::regex_match()` 比较字符串”。

然而，Boost.Xpressive 和 Boost.Regex 之间存在根本的区别。Boost.Xpressive 中正则表达式的类型取决于被搜索字符串的类型。由于在示例 9.1“使用 `boost::xpressive::regex_match` 字符串”中 `s` 基于 `std::string`，因此正则表达式的类型必须是 `boost::xpressive::sregex`。将此与示例 9.2“带有 `const char*` 类型字符串的 `boost::xpressive::cregex`”进行比较，在后者正则表达式被应用于类型为 `const char*` 的字符串。

### 示例 9.2：带有 `const char*` 类型字符串的 `boost::xpressive::cregex`

```cpp
#include <boost/xpressive/xpressive.hpp>
#include <iostream>

using namespace boost::xpressive;

int main()
{
  const char *c = "Boost Libraries";
  cregex expr = cregex::compile("\\w+\\s\\w+");
  std::cout << std::boolalpha << regex_match(c, expr) << '\n';
}
```

对于 `const char*` 类型字符串，请使用类 `boost::xpressive::cregex`。如果你使用其他字符串类型，例如 `std::wstring` 或 `const wchar_t*`，请使用 `boost::xpressive::wsregex` 或 `boost::xpressive::wcregex`。

对于以字符串形式的正则表达式，必须调用静态成员函数 `compile()`。该成员函数必须在用于正则表达式的类型上调用。

Boost.Xpressive 支持直接初始化以 C++ 代码编写的正则表达式。正则表达式必须用 Boost.Xpressive 支持的表示法表示（见示例 9.3“带有 C++ 代码的正则表达式”）。

### 示例 9.3：带有 C++ 代码的正则表达式

```cpp
#include <boost/xpressive/xpressive.hpp>
#include <string>
#include <iostream>

using namespace boost::xpressive;

int main()
{
  std::string s = "Boost Libraries";
  sregex expr = +_w >> _s >> +_w;
  std::cout << std::boolalpha << regex_match(s, expr) << '\n';
}
```



在示例 9.2“带有 `const char*` 类型字符串的 `boost::xpressive::cregex`”中，以字符串 `"\w+\s\w+"` 编写的正则表达式，现在在示例 9.3“带有 C++ 代码的正则表达式”中表示为 `+_w >> _s >> +_w`。它们是完全相同的正则表达式。两个示例都搜索至少一个字母数字字符，后面跟着一个空格，然后是至少一个字母数字字符。

Boost.Xpressive 使使用 C++ 代码编写正则表达式成为可能。该库为字符组提供了对象。例如，对象 `_w` 类似于 `"\w"`。`_s` 的含义与 `"\s"` 相同。

虽然 `"\w"` 和 `"\s"` 可以在字符串中连续书写，但像 `_w` 和 `_s` 这样的对象必须用操作符连接。否则，结果将不是有效的 C++ 代码。Boost.Xpressive 提供了运算符 `operator>>`，它被用于示例 9.3“带有 C++ 代码的正则表达式”。

对于以字符串形式编写的正则表达式，必须调用静态成员函数 `compile()`。该成员函数必须在用于正则表达式的类型上调用。

Boost.Xpressive 支持直接初始化以 C++ 代码编写的正则表达式。正则表达式必须用 Boost.Xpressive 支持的表示法表示（见示例 9.3“带有 C++ 代码的正则表达式”）。

> 注：原始文本中存在重复段落，重复内容已合并。

[Boost.Tokenizer](http://www.boost.org/libs/tokenizer) 允许你通过将某些字符解释为分隔符来遍历字符串中的部分表达式。

### 示例 10.1：使用 `boost::tokenizer` 遍历字符串中的部分表达式

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::char_separator<char>> tokenizer;
  std::string s = "Boost C++ Libraries";
  tokenizer tok{s};
  for (tokenizer::iterator it = tok.begin(); it != tok.end(); ++it)
    std::cout << *it << '\n';
}
```

`Boost.Tokenizer` 在 `boost/tokenizer.hpp` 中定义了一个名为 `boost::tokenizer` 的类模板。它期望一个模板参数，是一个能够识别连贯表达式的类。示例 10.1“使用 `boost::tokenizer` 遍历字符串中的部分表达式”使用了 `boost::char_separator` 类，该类将空格和标点符号解释为分隔符。

分词器必须用 `std::string` 类型的字符串初始化。通过使用成员函数 `begin()` 和 `end()`，可以像容器一样访问分词器。用于初始化分词器的字符串部分表达式可以通过迭代器获取。部分表达式如何求值取决于作为模板参数传递的类类型。

由于 `boost::char_separator` 默认将空格和标点符号解释为分隔符，示例 10.1“使用 `boost::tokenizer` 遍历字符串中的部分表达式”显示了 `Boost`、`C`、`+`、`+` 和 `Libraries`。`boost::char_separator` 使用 `std::isspace()` 和 `std::ispunct()` 来识别分隔符字符。它区分应该显示的分隔符和应该被抑制的分隔符。默认情况下，空格会被抑制而标点符号会被显示。

### 示例 10.2：初始化 `boost::char_separator` 以适应迭代

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::char_separator<char>> tokenizer;
  std::string s = "Boost C++ Libraries";
  boost::char_separator<char> sep{" "};
  tokenizer tok{s};
  for (const auto &t : tok)
    std::cout << t << '\n';
}
```

为了防止标点符号被解释为分隔符，请在将其传递给分词器之前初始化 `boost::char_separator` 对象。`boost::char_separator` 的构造函数接受共三个参数，但只需要第一个。第一个参数描述被抑制的分隔符。示例 10.2“初始化 `boost::char_separator` 以适应迭代”就像示例 10.1“使用 `boost::tokenizer` 遍历字符串中的部分表达式”那样将空格视为分隔符。第二个参数指定应该显示的分隔符。如果省略此参数，则没有分隔符被显示，程序将显示 `Boost`、`C++` 和 `Libraries`。

### 示例 10.3：使用 `boost::char_separator` 模拟默认行为

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::char_separator<char>> tokenizer;
  std::string s = "Boost C++ Libraries";
  boost::char_separator<char> sep{"+"};
  tokenizer tok{s, sep};
  for (const auto &t : tok)
    std::cout << t << '\n';
}
```

如果将加号作为第二个参数，示例 10.3“使用 `boost::char_separator` 模拟默认行为”就像示例 10.1“使用 `boost::tokenizer` 遍历字符串中的部分表达式”那样将加号视为分隔符。第三个参数决定是否显示空部分表达式。如果连续发现两个分隔符，对应的部分表达式为空。默认情况下，这些空表达式是不显示的。使用第三个参数可以更改默认行为。

### 示例 10.4：初始化 `boost::char_separator` 显示空部分表达式

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::char_separator<char>> tokenizer;
  std::string s = "Boost C++ Libraries";
  boost::char_separator<char> sep{" ";
  // ...
}
```

示例 10.4“初始化 `boost::char_separator` 显示空部分表达式”显示了两个部分表达式。

### 示例 10.5：Boost.Tokenizer 处理宽字符串

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::char_separator<wchar_t>,
    std::wstring::const_iterator, std::wstring> tokenizer;
  std::wstring s = L"Boost C++ Libraries";
  boost::char_separator<wchar_t> sep{L" "};
  tokenizer tok{s, sep};
  for (const auto &t : tok)
    std::wcout << t << '\n';
}
```

示例 10.5“Boost.Tokenizer 处理宽字符串”遍历类型为 `std::wstring` 的字符串。为了支持这种字符串类型，分词器必须用额外的模板参数初始化。`boost::char_separator` 类也必须用 `wchar_t` 初始化。

### 示例 10.6：使用 `boost::escaped_list_separator` 解析 CSV 文件

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::escaped_list_separator<char>> tokenizer;
  std::string s = "Boost,\"C++ Libraries";
  tokenizer tok{s};
  for (const auto &t : tok)
    std::cout << t << '\n';
}
```

`boost::escaped_list_separator` 用于读取逗号分隔的多个值。这种格式被称为 CSV（逗号分隔值）。`boost_list_separator` 还能处理双引号和转义序列。因此，示例 10.6“使用 `boost::escaped_list_separator` 解析 CSV 文件”的输出是 `Boost` 和 `C++ Libraries`。

### 示例 10.7：使用 `boost::offset_separator` 遍历部分表达式

```cpp
#include <boost/tokenizer.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tokenizer<boost::offset_separator> tokenizer;
  std::string s = "Boost C++ Libraries";
  int offsets[] = {5, 5, 9};
  boost::offset_separator sep{offsets, offsets + 3};
  tokenizer tok{s, sep};
  for (const auto &t : tok)
    std::cout << t << '\n';
}
```

`boost::offset_separator` 指定了字符串中各个部分表达式结束的位置。示例 10.7“使用 `boost::offset_separator` 迭代部分表达式”规定第一个部分表达式在 5 个字符后结束，第二个在额外的 5 个字符后结束，第三个在随后的 9 个字符后结束。输出将恰别为 `Boost`、`C++` 和 `Libraries`。

# 11. Boost.Spirit

本章介绍了 [Boost.Spirit](http://www.boost.org/libs/spirit) 库。Boost.Spirit 用于开发用于文本格式的解析器。例如，你可以使用 Boost.Spirit 开发一个用于加载配置文件的解析器。Boost.Spirit 也可以用于二进制格式，尽管它在这方面的用处非常有限。

Boost.Spirit 简化了解析器的开发，因为格式是用规则描述的。规则定义了格式的外观——Boost.Spirit 完成其余的工作。你可以将 Boost.Spirit 与正则表达式进行类比，从某种意义上说，它让你能够处理复杂的逻辑——正则表达式中是模式搜索，而在 Boost.Spirit 中是解析——而无需编写代码来实现这些处理过程。

Boost.Spirit 期望使用解析表达式语法（PEG）来描述规则。PEG 与扩展巴科斯-诺尔范式（EBNF）有关。即使你不熟悉这些语言，本章中的示例也足够让你上手。

Boost.Spirit 有两个版本。第一个版本被称为 Spirit.Classic。该版本已不应再使用。当前版本是 `2.5.2`。这是本章中引入的版本。

从 `2.x` 版本开始，Boost.Spirit 既可以用于生成器（generators），也可以用于解析器（parsers）。解析器读取文本格式，而生成器写入这些格式。用于开发解析器的 Boost.Spirit 组件称为 `Spirit.Qi`。`Spirit.Karma` 是用于开发生成器的组件。命名空间相应划分：用于开发解析器的类和函数可以在 `boost::spirit::qi` 中找到，用于开发生成器的类和函数可以在 `boost::spirit::karma` 中找到。

除了 `Spirit.Qi` 和 `Spirit.Karma` 之外，该库还包含一个名为 `Spirit.Lex` 的组件，它可以用于开发词法分析器（lexers）。

本章重点关注开发解析器。示例主要使用了 `boost::spirit` 和 `boost::spirit::qi` 中的类和函数。对于这些类和函数，只需包含头文件 `boost/spirit/include/qi.hpp` 即可。

如果你不想包含像 `boost/spirit/include/qi.hpp` 这样的主文件，可以单独包含 `boost/spirit/include/` 中的头文件。仅包含该目录下的头文件是重要的。`boost/spirit/include/` 是面向用户的接口。其他目录中的头文件在新库版本中可能会发生变化。

## API

Boost.Spirit 提供 `boost::spirit::qi::parse()` 和 `boost::spirit::qi::phrase_parse()` 来解析格式。

### 示例 11.1：使用 `boost::spirit::qi::parse()`

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  bool match = qi::parse(it, s.end(), ascii::digit);
  std::cout << std::boolalpha << match << '\n';
  if (it != s.end())
    std::cout << std::string{it, s.end()} << '\n';
}
```



示例 11.1：“使用`boost::spirit::qi::parse()`”引入了`boost::spirit::qi::parse()`。该函数期望两个指向待解析字符串的迭代器和一个解析器。示例使用了由 Boost.Spirit 提供的解析器`boost::spirit::ascii::digit`。这是几种字符分类解析器之一。这些解析器测试字符是否属于某个特定类。`boost::spirit::ascii::digit`测试字符是否为 0 到 9 之间的数字。

示例传递了从`std::cin`读取的字符串迭代器。请注意，起始迭代器并没有直接传递给`boost::spirit::qi::parse()`。它存储在变量`it`中，然后被传递给`boost::spirit::qi::parse()`。这样做是因为`boost::spirit::qi::parse()`可能会修改迭代器。

如果你输入一个数字并按回车，示例将显示`true`。如果你输入两个数字并按回车，输出将是`true`，随后跟随第二个数字。如果你输入一个字母并按回车，输出将是`false`，随后跟随该字母。

解析器`boost::spirit::ascii::digit`（如示例 11.1：“使用`boost::spirit::qi::parse()`”）恰好测试一个字符以判断它是否为数字。如果第一个字符是数字，`boost::spirit::qi::parse()`返回`true`；否则返回`false`。`boost::spirit::qi::parse()`的返回值指示解析器是否成功。

如果你输入多个数字，`boost::spirit::qi::parse()`也会返回`true`。因为解析器`boost::spirit::ascii::digit`只测试第一个字符，所以它会在这种字符串上成功。第一个字符之后的所有数字都被忽略。

为了让你确定字符串有多少部分被成功解析，`boost::spirit::qi::parse()`会改变迭代器`it`。在调用`boost::spirit::qi::parse()`后，`it`指向最后一个成功解析字符之后的字符。如果你输入多个数字，`it`指向第二个数字。如果你只输入一个数字，`it`等于`s`的结束迭代器。如果你输入一个字母，`it`指向该字母。

`boost::spirit::qi::parse()`不忽略空格。如果你运行示例 11.1：“使用`boost::spirit::qi::parse()`”并输入空格，将显示`false`。`boost::spirit::qi::parse()`测试第一个字符，即使该字符是空格。如果你想忽略空格，请使用`boost::spirit::qi::phrase_parse()`代替`boost::spirit::qi::parse()`。

### 示例 11.2：使用`boost::spirit::qi::phrase_parse()`

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  bool match = qi::phrase_parse(it, s.end(), ascii::digit, ascii::space);
  std::cout << std::boolalpha << match << '\n';
  if (it != s.end())
    std::cout << std::string{it, s.end()} << '\n';
}
```

`boost::spirit::qi::phrase_parse()`的工作类似于`boost::spirit::qi::parse()`，但它期望另一个名为 skipper（跳过符）的参数。skipper 是用于被忽略字符的解析器。示例 11.2：“使用`boost::spirit::qi::phrase_parse()`”使用`boost::spirit::ascii::space`（用于检测空格的字符分类解析器）作为 skipper。

skipper`boost::spirit::ascii::space`将空格作为分隔符丢弃。如果你启动示例并输入空格加数字，它将显示`true`。与上一个示例不同，解析器`boost::spirit::ascii::digit`不应用于空格，而是应用于第一个非空格字符。

请注意，此示例忽略任意数量的空格。因此，如果你输入多个空格后跟一个数字，`boost::spirit::qi::phrase_parse()`将返回`true`。

与`boost::spirit::qi::parse()`类似，`boost::spirit::qi::phrase_parse()`会修改作为第一个参数传递的迭代器。这样，你就知道解析器成功处理了字符串中的多远位置。示例 11.2：“使用`boost::spirit::qi::phrase_parse()`”会跳过在成功解析字符之后出现的空格。如果你输入一个数字，后跟一个空格，然后是一个字母，迭代器将指向该字母，而不是它前面的空格。如果你想让迭代器指向该空格，请将`boost::spirit::qi::skip_flag::dont_postskip`作为另一个参数传递给`boost::spirit::qi::phrase_parse()`。

### 示例 11.3：使用`boost::spirit::qi::skip_flag::dont_postskip`的`phrase_parse()`

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  bool match = qi::phrase_parse(it, s.end(), ascii::digit, ascii::space,
    qi::skip_flag::dont_postskip);
  std::cout << std::boolalpha << match << '\n';
  if (it != s.end())
    std::cout << std::string{it, s.end()} << '\n';
}
```

示例 11.3：“使用`boost::spirit::qi::skip_flag::dont_postskip`的`phrase_parse()`”将`boost::spirit::qi::skip_flag::dont_postskip`传递给`boost::spirit::qi::phrase_parse()`，告诉解析器不要跳过在成功解析的数字之后、第一个解析失败的字符之前出现的空格。如果你输入一个数字，后跟一个空格，然后是一个字母，`it`在调用`boost::spirit::qi::phrase_parse()`后将指向该空格。

标志`boost::spirit::qi::skip_flag::postskip`是默认值，当既未指定`boost::spirit::qi::skip_flag::dont_postskip`也未指定`boost::spirit::qi::skip_flag::postskip`时，将使用该值。

### 示例 11.4：使用宽字符串的`boost::spirit::qi::phrase_parse()`

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::wstring s;
  std::getline(std::wcin, s);
  auto it = s.begin();
  bool match = qi::phrase_parse(it, s.end(), ascii::digit, ascii::space,
    qi::skip_flag::dont_postskip);
  std::wcout << std::boolalpha << match << '\n';
  if (it != s.end())
    std::wcout << std::wstring{it, s.end()} << '\n';
}
```

`boost::spirit::qi::parse()`和`boost::spirit::qi::phrase_parse()`接受宽字符串的迭代器。示例 11.4：“使用宽字符串的`boost::spirit::qi::phrase_parse()`”的工作方式与之前的示例相同，只是使用了宽字符串。

Boost.Spirit 还支持 C++11 标准库中的字符串类型`std::u16string`和`std::u32string`。

## 解析器

本节解释了如何定义解析器。你通常从 Boost.Spirit 访问现有的解析器——例如`boost::spirit::ascii::digit`或`boost::spirit::ascii::space`。通过组合解析器，你可以解析更复杂的格式。这个过程与定义正则表达式相似，正则表达式也是由基本构建块构建的。

示例 11.5：“两个连续数字的解析器”测试是否输入了两个数字。`boost::spirit::qi::phrase_parse()`仅在两个数字连续出现时才返回`true`。空格会被忽略。

与之前的示例一样，使用`boost::spirit::ascii::digit`来识别数字。由于`boost::spirit::ascii::digit`恰好测试一个字符，因此使用了两次解析器来测试输入是否为两个数字。要连续使用两次`boost::spirit::ascii::digit`，必须使用运算符。Boost.Spirit 为解析器重载了`operator>>`。通过`ascii::digit >> ascii::digit`创建了一个用于测试字符串是否包含两个数字的解析器。

如果你运行示例并输入两个数字，将显示`true`。如果你只输入一个数字，则将显示`false`。

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  bool match = qi::phrase_parse(it, s.end(), ascii::digit, ascii::space,
    qi::skip_flag::dont_postskip);
  std::cout << std::boolalpha << match << '\n';
  if (it != s.end())
    std::cout << std::string{it, s.end()} << '\n';
}
```

示例 11.8：“数值解析器”期望一个整数。`boost::spirit::qi::int_`是一个识别正负整数的数值解析器。与`boost::spirit::ascii::digit`不同，`boost::spirit::qi::int_`能够将多个字符识别为整数，例如`+1`或`-23`。

Boost.Spirit 提供了额外的逻辑解析器。`boost::spirit::qi::float_`、`boost::spirit::qi::double_`和`boost::spirit::qi::bool_`是可以读取浮点数和布尔值的数值解析器。通过`boost::spirit::qi::eol`，你可以测试行尾字符。`boost::spirit::qi::byte_`和`boost::spirit::qi::word`可用于读取一个或两个字节。`boost::spirit::qi::word`和其他二进制解析器会识别平台的字节序并相应进行解析。如果你想不分平台根据特定的字节序进行解析，可以使用如`boost::spirit::qi::little_word`和`boost::spirit::qi::big_word`等解析器。

## Actions（动作）

到目前为止，本章中的示例仅检测了两个内容：解析器是否成功以及解析何时结束。然而，解析器通常会以某种方式处理数据，正如你将在后续示例中所看到的。

### 示例 11.9：将动作与解析器链接

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  bool match = qi::phrase_parse(it, s.end(),
    qi::int_([{ std::cout << i << '\n'; })], ascii::space);
  std::cout << std::boolalpha << match << '\n';
  if (it != s.end())
    std::cout << std::string{it, s.end()} << '\n';
}
```

示例 11.9：“将动作与解析器链接”使用`boost::spirit::qi::int_`解析一个整数，然后将该整数写入标准输出。这就是为什么为`boost::spirit::qi::int_`链接了一个动作（action）。动作是在应用解析器时调用的函数或函数对象。链接是通过运算符`operator[]`完成的，该运算符被`boost::spirit::qi::int_`和其他解析器进行了重载。示例 11.9：“将动作与解析器链接”使用了一个 lambda 函数作为动作，该函数接收一个类型为`int`的唯一参数并将其写入标准输出。

如果你启动示例 11.9：“将动作与解析器链接”并输入一个数字，该数字将被显示出来。

传递给动作的参数类型取决于解析器。例如，`boost::spirit::qi::int_`转发一个`int`值，而`boost::spirit::qi::float_`传递一个`float`值。

### 示例 11.10：结合 Boost.Phoenix 的 Boost.Spirit

```cpp
#define BOOST_SPIRIT_USE_PHOENIX_V3
#include <boost/spirit/include/qi.hpp>
#include <boost/phoenix/phoenix.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;
using boost::phoenix::ref;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  int i;
  bool match = qi::phrase_parse(it, s.end(), qi::int_[ref(i) = qi::_1],
    ascii::space);
  std::cout << std::boolalpha << match << '\n';
  if (match)
    std::cout << i << '\n';
  if (it != s.end())
    std::cout << std::string{it, s.end()} << '\n';
}
```

示例 11.10：“结合 Boost.Phoenix 的 Boost.Spirit”使用 Boost.Phoenix 将通过`boost::spirit::qi::int_`解析出的`int`值存储在`i`中。如果`boost::spirit::qi::phrase_parse()`返回`true`，则将`i`写入标准输出。

此示例在包含 Boost.Spirit 头文件之前定义了宏`BOOST_SPIRIT_USE_PHOENIX_V3`。该宏选择了 Boost.Phoenix 的第三个也是当前的版本。这很重要，因为 Boost.Phoenix 是从 Boost.Spirit 分支出来的，而 Boost.Spirit 包含了 Boost.Phoenix 的第二个版本。

## Attributes（属性）

动作处理解析值的方法之一。另一种方法是将对象传递给`boost::spirit::parse()`。每个解析器都有一个属性（attribute）。例如，`boost::spirit::qi::int_`有一个类型为`int`的属性。在以下示例中，属性并不是作为参数传递的。相反，解析后的值存储在属性中。

### 示例 11.11：在属性中存储`int`值



```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  int i;
  if (qi::phrase_parse(it, s.end(), qi::int_, ascii::space, i))
    std::cout << i << '\n';
}
```

示例 11.11，“在属性中存储 `int` 值”使用解析器 `boost::spirit::qi::int_`。解析出的 `int` 值存储在变量 `i` 中。`i` 作为另一个参数传递给 `boost::spirit::phrase_parse()`，因此成为解析器 `boost::spirit::qi::int_` 的属性。

如果你启动示例 11.11，“在属性中存储 `int` 值”并输入一个数字，该数字将被写入标准输出。

### 示例 11.12：在属性中存储多个 `int` 值

示例 11.12，“在属性中存储多个 `int` 值”使用由 `qi::int_ % ','` 定义的解析器。该解析器接受由逗号分隔的任意数量的整数。像往常一样，空格会被忽略。

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <vector>
#include <iterator>
#include <algorithm>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  std::vector<int> v;
  if (qi::phrase_parse(it, s.end(), qi::int_ % ',', ascii::space, v))
  {
    std::ostream_iterator<int> out{std::cout, ";"};
    std::copy(v.begin(), v.end(), out);
  }
}
```

除了 `vector` 之外，你也可以传递其他类型的容器，例如 `std::list`。

Boost.Spirit 文档描述了[哪些属性类型与哪些运算符配合使用](http://www.boost.org/libs/spirit/doc/html/spirit/qi/quick_reference/qi_parsers/operator.html)。

## 规则

在 Boost.Spirit 中，解析器由规则（rules）组成。由于规则通常基于 Boost.Spirit 提供的解析器，因此两者之间没有明确的区别。例如，`boost::spirit::ascii::digit` 既可以是解析器，也可以是规则。通常，规则指的是像 `qi::int_ % ','` 这样复杂的表达式。

在之前所有的示例中，规则都是直接传递给 `boost::spirit::qi::parse()` 或 `boost::spirit::qi::phrase_parse()`。通过 `boost::spirit::qi::rule`，Boost.Spirit 提供了一个用于定义规则变量的类。例如，如果规则需要存储在类的成员变量中，则需要使用 `boost::spirit::qi::rule`。

### 示例 11.13：使用 `boost::spirit::qi::rule` 定义规则

```cpp
#include <boost/spirit/include/qi.hpp>
#include <string>
#include <vector>
#include <iterator>
#include <algorithm>
#include <iostream>

using namespace boost::spirit;

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  qi::rule<std::string::iterator, std::vector<int>(),
    ascii::space_type> values = qi::int_ % ',';
  std::vector<int> v;
  if (qi::phrase_parse(it, s.end(), values, ascii::space, v))
  {
    std::ostream_iterator<int> out{std::cout, ";"};
    std::copy(v.begin(), v.end(), out);
  }
}
```

示例 11.13，“使用 `boost::spirit::qi::rule` 定义规则”的工作方式与示例 11.12，“在属性中存储多个 `int` 值”相同。如果你输入以逗号分隔的多个整数，它们将用分号显示。与上一个示例不同，解析器没有直接传递给 `boost::spirit::qi::phrase_parse()`，而是定义在 `boost::spirit::qi::rule` 变量中。

`boost::spirit::qi::rule` 是一个类模板。唯一的强制参数是正在解析的字符串迭代器类型。在示例中，还传递了两个可选的模板参数。

第二个模板参数是 `std::vector<int>()`，它是一个返回 `std::vector<int>` 类型向量且不接受参数的函数签名。该模板参数表示所解析属性的类型是 `int` 向量。

第三个模板参数是 `boost::spirit::qi::phrase_parse()` 使用的跳符（skipper）类型。在示例中，使用了跳符 `boost::spirit::ascii::space`。该跳符的类型可以通过 `boost::spirit::ascii::space_type` 获取，并作为模板参数传递给 `boost::spirit::qi::rule`。

### 注意事项

如果你希望代码具有平台无关性，并且可以在 C++11 开发环境中运行，你应该优先使用 `boost::spirit::qi::rule` 而不是 `auto` 关键字。如果使用 `auto` 定义 `values`，该示例在 GCC 和 Clang 中按预期工作。但在 Visual C++ 2013 中，只有第一个数字会被解析并写入标准输出。

### 示例 11.14：规则的嵌套

```cpp
#include <boost/spirit/include/qi.hpp>
#include <boost/variant.hpp>
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace boost::spirit;

struct print : public boost::static_visitor<>
{
  template <typename T>
  void operator()(T t) const
  {
    std::cout << std::boolalpha << t << ';';
  }
};

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  qi::rule<std::string::iterator, boost::variant<int, bool>(),
    ascii::space_type> value = qi::int_ | qi::bool_;
  qi::rule<std::string::iterator, std::vector<boost::variant<int, bool>>(),
    ascii::space_type> values = value % ',';
  std::vector<boost::variant<int, bool>> v;
  if (qi::phrase_parse(it, s.end(), values, ascii::space, v))
  {
    for (const auto &elem : v)
      boost::apply_visitor(print{}, elem);
  }
}
```

示例 11.14，“规则的嵌套”定义了规则，其中一个引用另一个：`values` 定义为 `value % ','`，而 `value` 设置为 `qi::int_ | qi::bool_`。`values` 表示逗号分隔的多个值。`value` 定义了一个值为整数或布尔值。这些规则共同表示可以解析整数和布尔值。

## 语法（Grammar）

如果你想解析复杂的格式并需要定义相互引用的规则，可以使用 `boost::spirit::grammar` 将它们分组。

示例 11.15，“在语法中分组规则”的工作方式与示例 11.14，“规则的嵌套”相同：你可以输入逗号分隔的整数和布尔值。示例使用了与上一个示例相同的规则——`value` 和 `values`。然而，这次语法定义在类 `my_grammar` 中，该类派生自 `boost::spirit::grammar`。`my_grammar` 和 `boost::spirit::grammar` 都是类模板。`boost::spirit::grammar` 的模板参数与 `boost::spirit::qi::rule` 相同。要解析字符串的迭代器类型必须传递给 `boost::spirit::grammar`。你还可以传递定义属性类型和跳符类型的函数签名。

在 `my_grammar` 中，使用 `boost::spirit::qi::rule` 来定义规则 `value` 和 `values`。这些规则作为成员变量定义，并在构造函数中初始化。

请注意，外层规则必须通过 `base_type` 传递给基类的构造函数。通过这种方式，Boost.Spirit 知道哪个规则是语法的入口。

一旦定义了语法，就可以像解析器一样使用它。在示例 11.15，“在语法中分组规则”中，`main()` 实例化 `my_grammar` 以创建 `g`。然后将 `g` 传递给 `boost::spirit::qi::phrase_parse()`。

```cpp
#include <boost/spirit/include/qi.hpp>
#include <boost/variant.hpp>
#include <string>
#include <vector>
#include <iostream>

using namespace boost::spirit;

template <typename Iterator, typename Skipper>
struct my_grammar : qi::grammar<Iterator,
  std::vector<boost::variant<int, bool>>(), Skipper>
{
  my_grammar() : my_grammar::base_type{values}
  {
    value = qi::int_ | qi::bool_;
    values = value % ',';
  }

  qi::rule<Iterator, boost::variant<int, bool>(), Skipper> value;
  qi::rule<Iterator, std::vector<boost::variant<int, bool>>(), Skipper>
    values;
};

struct print : public boost::static_visitor<>
{
  template <typename T>
  void operator()(T t) const
  {
    std::cout << std::boolalpha << t << ';';
  }
};

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  my_grammar<std::string::iterator, ascii::space_type> g;
  std::vector<boost::variant<int, bool>> v;
  if (qi::phrase_parse(it, s.end(), g, ascii::space, v))
  {
    for (const auto &elem : v)
      boost::apply_visitor(print{}, elem);
  }
}
```

### 示例 11.16：将解析后的值存储在结构体

```cpp
#include <boost/spirit/include/qi.hpp>
#include <boost/variant.hpp>
#include <boost/fusion/include/adapt_struct.hpp>
#include <string>
#include <vector>
#include <iostream>

using namespace boost::spirit;

typedef boost::variant<int, bool> int_or_bool;

struct int_or_bool_values
{
  int_or_bool first;
  std::vector<int_or_bool> others;
};

BOOST_FUSION_ADAPT_STRUCT(
  int_or_bool_values,
  (int_or_bool, first)
  (std::vector<int_or_bool>, others)
)

template <typename Iterator, typename Skipper>
struct my_grammar : qi::grammar<Iterator, int_or_bool_values(), Skipper>
{
  my_grammar() : my_grammar::base_type{values}
  {
    value = qi::int_ | qi::bool_;
    values = value >> ',' >> value % ',';
  }

  qi::rule<Iterator, int_or_bool(), Skipper> value;
  qi::rule<Iterator, int_or_bool_values(), Skipper> values;
};

struct print : public boost::static_visitor<>
{
  template <typename T>
  void operator()(T t) const
  {
    std::cout << std::boolalpha << t << ';';
  }
};

int main()
{
  std::string s;
  std::getline(std::cin, s);
  auto it = s.begin();
  my_grammar<std::string::iterator, ascii::space_type> g;
  int_or_bool_values v;
  if (qi::phrase_parse(it, s.end(), g, ascii::space, v))
  {
    print p;
    boost::apply_visitor(p, v.first);
    for (const auto &elem : v.others)
      boost::apply_visitor(p, elem);
  }
}
```

示例 11.16，“将解析后的值存储在结构体”基于之前的示例，但它期望至少有两个值。规则 `values` 被定义为 `value >> ',' >> value % ','`。

`values` 中的第一个部分是 `value`，第二个部分是 `value % ','`。第一个部分解析出的值必须存储在类型为 `boost::variant` 的对象中。第二个部分解析出的值必须存储在容器中。通过 `int_or_bool_values`，示例提供了一个结构体来存储由规则 `values` 的两个部分解析出的值。

要在 Boost.Spirit 中使用 `int_or_bool_values`，必须使用 `BOOST_FUSION_ADAPT_STRUCT` 宏。该宏由 Boost.Fusion 提供。此宏使得可以将 `int_or_bool_values` 视为一个包含两个类型为 `int_or_bool` 和 `std::vector<int_or_bool>` 值的元组（tuple）。因为这个元组具有正确数量和正确类型的值，因此可以使用签名 `int_or_bool_values()` 来定义 `values`。`values` 将第一个解析出的值存储在 `first` 中，并将所有其他解析出的值存储在 `others` 中。

一个类型为 `int_or_bool_values` 的对象作为属性传递给 `boost::spirit::qi::phrase_parse()`。如果你启动示例并输入至少两个用逗号分隔的整数或布尔值，它们都将存储在属性中并写入标准输出流。

### 注意事项



该解析器已与上一个示例中使用的有所不同。如果`values`是用`value % ','`定义的，那么`int_or_bool_values`将只有一个成员变量，并且所有解析出的值都可以存储在 vector 中，正如上一个示例所示。因此，`int_or_bool_values`将像一个只有一个值的元组——而 Boost.Spirit 并不支持这种。只有一个成员变量的结构体会导致编译错误。针对该问题有多种[解决方法](http://stackoverflow.com/questions/19823413/spirit-qi-attribute-propagation-issue-with-single-member-struct)。

# 第 III 部分：容器

容器是 C++ 中最有用的数据结构之一。标准库提供了许多容器，而 Boost 库提供了更多。

- Boost.MultiIndex 更进了一步：该库的容器可以同时支持来自其他容器的多个接口。Boost.MultiIndex 的容器类似于合并后的容器，并提供了它们所合并的所有容器的优点。
- Boost.Bimap 基于 Boost.MultiIndex。它提供了一个与`std::unordered_map`类似的容器，不同之处在于元素可以从两边进行查找。因此，取决于访问容器的方式，任何一侧都可以作为键（key）。
- Boost.Array 和 Boost.Unordered 定义了`boost::array`、`boost::unordered_set`和`boost::unordered_map`，这些在 C++11 中被添加到标准库。
- Boost.CircularBuffer 提供了一个容器，其最重要的属性是当添加值时，它会覆盖缓冲区中的第一个元素。
- Boost.Heap 提供了优先级队列的变体——类似于`std::priority_queue`的类。
- Boost.Intrusive 允许你创建容器，它与标准库容器不同，不复制也不移动对象。然而，要将对象添加到侵入式列表（intrusive list），对象的类型必须满足某些要求。
- Boost.MultiArray 试图简化多数组的使用。例如，可以将二维数组的一部分作为一个独立的数组。
- Boost.Container 是一个定义了与标准库相同容器的库。如果平台支持该库，并希望避免由标准库实现差异引起的问题，那么使用 Boost.Container 就很有意义。

# 12. Boost.MultiIndex

[Boost.MultiIndex](http://www.boost.org/libs/multi_index)使得支持任意数量接口的容器成为可能。虽然`std::vector`提供了一个通过索引直接访问元素的接口，而`std::set`提供了一个排序元素的接口，但 Boost.MultiIndex 允许你定义支持这些接口的容器。这种容器可以用于通过索引和排序访问元素。

如果元素需要以不同的方式访问并且通常需要存储在多个容器中，则 Boost.MultiIndex 很有用。与其不断将元素存储在 vector 和 set 中并同步容器，不如使用 Boost.MultiIndex 定义一个提供 vector 接口和 set 接口的容器。

在示例 12.1“使用`boost::multi_index::multi_index_container`”中，动物可以通过名称和数量查找。当你使用 Boost.MultiIndex 时，第一步是定义新容器。你必须决定新容器支持哪些接口以及它访问哪些元素属性。

类`boost::multi_index::multi_index_container`定义在`boost/multi_index_container.hpp`中，用于每个容器定义。这是一个至少需要两个参数的类模板。第一个参数是容器应该存储的元素类型——在示例 12.1 中，这是一个名为`animal`的用户定义类。第二个参数用于指定容器应该提供的不同索引。

### 示例 12.1：使用`boost::multi_index::multi_index_container`

```cpp
#include <boost/multi_index_container.hpp>
#include <boost/multi_index/hashed_index.hpp>
#include <boost/multi_index/member.hpp>
#include <string>
#include <iostream>

using namespace boost::multi_index;

struct animal
{
  std::string name;
  int legs;
};

typedef multi_index_container<
  animal,
  indexed_by<
    hashed_non_unique<
      member<
        animal, std::string, &animal::name
      >
    >,
    hashed_non_unique<
      member<
        animal, int, &animal::legs
      >
    >
  >
> animal_multi;

int main()
{
  animal_multi animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"spider", 8});

  std::cout << animals.count("cat") << '\n';

  const animal_multi::nth_index<1>::type &legs_index = animals.get<1>();
  std::cout << legs_index.count(8) << '\n';
}
```

基于 Boost.MultiIndex 的容器的主要优势在于你可以通过不同的接口访问元素。当你定义一个新容器时，可以指定接口的数量和类型。示例 12.1 中的容器需要支持通过名称或腿数搜索动物，因此定义了两个接口。Boost.MultiIndex 将这些接口称为索引（indexes）——这就是该库名称的由来。

接口是通过类`boost::multi_index::indexed_by`定义的。每个接口都作为模板参数传递。示例 12.1 使用了两个类型为`boost::multi_index::hashed_non_unique`的接口，该类型定义在`boost/multi_index/hashed_index.hpp`中。使用这些接口使得容器的行为类似于`std::unordered_set`，并使用哈希值查找值。

`boost::multi_index::hashed_non_unique`类也是一个模板，它期望唯一的参数是一个计算哈希值的类。由于容器的两个接口都需要查找动物，因此一个接口为名称计算哈希值，而另一个接口为腿数计算哈希值。

Boost.MultiIndex 提供了辅助类模板`boost::multi_index::member`（定义在`boost/multi_index/member.hpp`中），用于访问成员变量。如示例 12.1 所示，指定了多个参数让`boost::multi_index::member`知道应该访问`animal`的哪个成员变量以及该成员变量的类型。

尽管`animal_multi`的定义初看起来很复杂，但该类的工作方式像一个 map。动物的名称和腿数可以被视为键值对。`animal_multi`容器相比于`std::unordered_map`等 map 的优势在于，可以通过名称或腿数查找动物。`animal_multi`支持两个接口，一个基于名称，一个基于腿数。接口决定了哪个成员变量是键，哪个成员变量是值。

要访问 MultiIndex 容器，你需要选择一个接口。如果你直接使用`insert()`或`count()`访问对象`animals`，将使用第一个接口。在示例 12.1 中，这是成员变量`name`的哈希容器。如果你需要不同的接口，必须显式地选择它。

接口是连续编号的，第一个接口索引从 0 开始。要访问第二个接口——如示例 12.1 所示——调用成员函数`get()`并将接口的索引作为模板参数传递。

`get()`的返回值看起来很复杂。它访问了 MultiIndex 容器中的一个名为`nth_index`的类，该类同样是一个模板。要使用的接口索引必须作为模板参数指定。此索引必须与传递给`get()`的索引相同。最后一步是访问`nth_index`中名为`type`的类型定义。`type`的值代表对应接口的类型。以下示例使用`auto`关键字来简化代码。

虽然你不需要了解接口的具体细节，因为它们是从`nth_index`和`type`自动推导出来的，但你应该理解访问的是什么样的接口。由于接口在容器定义中是连续编号的，这很容易回答，因为索引同时传递给了`get()`和`nth_index`。因此，`legs_index`是通过腿数查找动物的哈希接口。

### 示例 12.2：使用`modify()`修改 MultiIndex 容器中的元素

```cpp
#include <boost/multi_index_container.hpp>
#include <boost/multi_index/hashed_index.hpp>
#include <boost/multi_index/member.hpp>
#include <string>
#include <iostream>

using namespace boost::multi_index;

struct animal
{
  std::string name;
  int legs;
};

typedef multi_index_container<
  animal,
  indexed_by<
    hashed_non_unique<
      member<
        animal, std::string, &animal::name
      >
    >,
    hashed_non_unique<
      member<
        animal, int, &animal::legs
      >
    >
  >
> animal_multi;

int main()
{
  animal_multi animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"spider", 8});

  auto &legs_index = animals.get<1>();
  auto it = legs_index.find(4);
  legs_index.modify(it, [](animal &a){ a.name = "dog"; });

  std::cout << animals.count("dog") << '\n';
}
```

就像`std::unordered_map`类型容器中的键不能修改一样，MultiIndex 容器内部存储的数据也无法修改。严格来说，存储在 MultiIndex 容器中的所有数据都是常量。这包括未被任何接口使用的成员变量。即使没有接口访问`legs`，`legs`也无法被更改。

为了避免从 MultiIndex 容器中删除元素并插入新元素，Boost.MultiIndex 提供了直接更改值的成员函数。因为这些成员函数作用于 MultiIndex 容器本身，并且由于容器中的元素没有被直接修改，所有接口将收到通知并重新计算哈希值。

`Boost.MultiIndex`提供的每个接口都提供了成员函数`modify()`，该函数直接在容器上操作。要修改的对象通过传递给`modify()`第一个参数的迭代器来标识。第二个参数是一个函数或函数对象，它期望的唯一参数是一个与容器中存储类型相同的对象。该函数或函数对象可以根据需要任意地更改元素。示例 12.2“使用`modify()`更改 MultiIndex 容器中的元素”演示了如何使用成员函数`modify()`来更改元素。

到为止，仅引入了一个接口：`boost::multi_index::hashed_non_unique`，它计算出一个不必须是唯一的哈希值。为了保证某个值不会被存储两次，请使用`boost::multi_index::hashed_unique`。请注意，如果值不满足特定容器所有接口的要求，则无法存储。如果一个接口不允许你多次存储某个值，那么另一个接口是否允许并不重要。

### 示例 12.3：使用`boost::multi_index::hashed_unique`的 MultiIndex 容器

```cpp
#include <boost/multi_index_container.hpp>
#include <boost/multi_index/hashed_index.hpp>
#include <boost/multi_index/member.hpp>
#include <string>
#include <iostream>

using namespace boost::multi_index;

struct animal
{
  std::string name;
  int legs;
};

typedef multi_index_container<
  animal,
  indexed_by<
    hashed_non_unique<
      member<
        animal, std::string, &animal::name
      >
    >,
    hashed_unique<
      member<
        animal, int, &animal::legs
      >
    >
  >
> animal_multi;

int main()
{
  animal_multi animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"dog", 4});

  auto &legs_index = animals.get<1>();
  std::cout << legs_index.count(4) << '\n';
}
```

示例 12.3“使用`boost::multi_index::hashed_unique`的 MultiIndex 容器”容器使用了`boost::multi_index::hashed_unique`作为第二个接口。这意味着容器中不能存储两个具有相同腿数量的动物，因为它们的哈希值将是相同的。

该示例尝试存储一条狗，它的腿数与已经存储的猫相同。因为这违反了第二个接口需要唯一哈希值的要求，所以这条狗不会被存储在容器中。因此，当搜索四条腿的动物时，程序显示`1`，因为只有猫被存储并计数。

示例 12.4“`sequenced`、`ordered_non_unique`和`random_access`接口”引入了 Boost.MultiIndex 的最后三个接口：`boost::multi_index::sequenced`、`boost::multi_index::ordered_non_unique`和`boost::multi_index::random_access`。

`boost::multi_index::sequenced`接口允许你将 MultiIndex 容器视为类型为`std::list`的列表。元素按照给定的顺序存储。

使用`boost::multi_index::ordered_non_unique`接口时，对象会自动排序。该接口要求你在定义容器时指定排序准则。示例 12.4“`sequenced`、`ordered_non_unique`和`random_access`接口”使用辅助类`boost::multi_index::member`按腿数对`animal`类型的对象进行排序。

`boost::multi_index::ordered_non_unique`提供了特殊的成员函数来在排序值中查找特定范围。使用`lower_bound()`和`upper_bound()`，程序搜索至少有四条且不超过八条腿的动物。因为它们要求元素经过排序，其他接口并不提供这些成员函数。

最后引入的接口是`boost::multi_index::random_access`，它允许你将 MultiIndex 容器视为类型为`std::vector`的向量。两个最显著成员函数是`operator[]`和`at()`。

`boost::multi_index::random_access`包含了`boost::multi_index::sequenced`。通过`boost::multi_index::random_access`，`boost::multi_index::sequenced`的所有成员函数也可用。

### 示例 12.4：`sequenced`、`ordered_non_unique`和`random_access`接口



```cpp
#include <boost/multi_index_container.hpp>
#include <boost/multi_index/sequenced.hpp>
#include <boost/multi_index/ordered_index.hpp>
#include <boost/multi_index/random_access.hpp>
#include <boost/multi_index/member.hpp>
#include <string>
#include <iostream>

struct animal
{
  std::string name;
  int legs;
};

typedef multi_index_container<
  animal,
  indexed_by<
    sequenced<
    ordered_non_unique<
      member<
        animal, int, &animal::legs
      >
    >,
    random_access<>
  >
> animal_multi;

int main()
{
  animal_multi animals;

  animals.push_back({"cat", 4});
  animals.push_back({"shark", 0});
  animals.push_back({"dog", 4});

  auto &legs_index = animals.get<1>();
  auto it = legs_index.lower_bound(4);
  auto end = legs_index.upper_bound(8);
  for (; it != end; ++it)
    std::cout << it->name << '\n';

  const auto &rand_index = animals.get<2>();
  std::cout << rand_index[0].name << '\n';
}
```

### 示例 12.5. `identity` 和 `const_mem_fun` 提取器

```cpp
#include <boost/multi_index_container.hpp>
#include <boost/multi_index/ordered_index.hpp>
#include <boost/multi_index/hashed_index.hpp>
#include <boost/multi_index/mem_fun.hpp>
#include <boost/multi_index/identity.hpp>
#include <string>
#include <utility>
#include <iostream>

using namespace boost::multi_index;

class animal
{
public:
  animal(std::string name, int legs) : name_{std::move(name)},
    legs_(legs) {}
  bool operator<(const animal &a) const { return legs_ < a.legs_; }
  const std::string &name() const { return name_; }
private:
  std::string name_;
  int legs_;
};

typedef multi_index_container<
  animal,
  indexed_by<
    ordered_unique<
      identity<animal>
    >,
    hashed_unique<
      const_mem_fun<
        animal, const std::string&, &animal::name
      >
    >
  >
> animal_multi;

int main()
{
  animal_multi animals;

  animals.emplace("cat", 4);
  animals.emplace("shark", 0);
  animals.emplace("spider", 8);

  std::cout << animals.begin()->name() << '\n';

  const auto &name_index = animals.get(1);
  std::cout << name_index.count("shark") << '\n';
}
```

现在我们已经涵盖了 Boost.MultiIndex 的四个接口，本章剩余部分将关注键提取器（key extractors）。已经引入了一个键提取器：`boost::multi_index::member`，它定义在`boost/multi_index/member.hpp`。这个辅助类被称为键提取器，因为它允许你指定类的哪个成员变量作为接口的键。

示例 12.5，“`identity` 和 `const_mem_fun` 提取器”引入了另外两个键提取器。

`boost::multi_index::identity` 提取器定义在`boost/multi_index/identity.hpp`，它使用存储在容器中的元素本身作为键。这要求类是可排序的，因为元素对象将作为`ordered_unique`接口的键。在示例 12.5，“`identity` 和 `const_mem_fun` 提取器”中，这是通过重载`operator<`实现的。

头文件`boost/multi_index/mem_fun.hpp`定义了两个键提取器——`boost::multi_index::const_mem_fun`和`boost::multi_index::mem_fun`——它们使用成员函数的返回值作为键。在示例 12.5，“键提取器 `identity` 和 `const_mem_fun`”中，`name()`的返回值就是这样被使用的。`boost::multi_index::const_mem_fun`用于常成员函数，而`boost::multi_index::mem_fun`用于非常成员函数。

Boost.MultiIndex 提供了另外两个键提取器：`boost::multi_index::global_fun`和`boost::multi_index::composite_key`。前者可用于自由函数或静态成员函数，后者允许你设计一个由多个其他键提取器组成的键提取器。

# 13. Boost.Bimap

库 [Boost.Bimap](http://www.boost.org/libs/bimap) 基于 Boost.MultiIndex，并提供了一个无需定义即可直接使用的容器。该容器类似于`std::map`，但支持从任一侧查找值。Boost.Bimap 允许你创建映射，根据你访问映射的方式，任何侧都可以作为键。当你将左侧作为键时，右侧是值，反之亦然。

## 示例 13.1. 使用 `boost::bimap`

```cpp
#include <boost/bimap.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::bimap<std::string, int> bimap;
  bimap animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"spider", 8});

  std::cout << animals.left.count("cat") << '\n';
  std::cout << animals.right.count(8) << '\n';
}
```

`boost::bimap`定义在`boost/bimap.hpp`中，并提供了两个成员变量`left`和`right`，可以用于访问由`boost::bimap`统一的两个`std::map`类型的容器。在示例 13.1，“使用 `boost::bimap`”中，`left`使用`std::string`类型的键访问容器，而`right`使用`int`类型的键。

除了支持使用左或右容器访问单个记录外，`boost::bimap`还允许你将记录视为关系（参见示例 13.2，“访问关系”）。

## 示例 13.2. 访问关系

```cpp
#include <boost/bimap.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::bimap<std::string, int> bimap;
  bimap animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"spider", 8});

  for (auto it = animals.begin(); it != animals.end(); ++it)
    std::cout << it->left << " has " << it->right << " legs\n";
}
```

没有必要使用`left`或`right`来访问记录。通过遍历记录，单个记录的左部分和右部分可以通过迭代器获取。

## 示例 13.3. 显式使用 `boost::bimaps::set_of`

```cpp
#include <boost/bimap.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::bimap<boost::bimaps::set_of<std::string>,
    boost::bimaps::set_of<int>> bimap;
  bimap animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"spider", 8});

  std::cout << animals.left.count("spider") << '\n';
  std::cout << animals.right.count(8) << '\n';
}
```

虽然`std::map`有一个名为`std::multimap`的容器，可以使用相同的键存储多条记录，但`boost::bimap`没有类似的对等物。然而，这并不意味着在`boost::bimap`类型的容器内部存储相同键的多个记录是不可能的。严格来说，两个所需的模板参数指定了`left`和`right`的容器类型，而不是要存储的元素类型。如果没有指定容器类型，则默认使用容器类型`boost::bimaps::set_of`。这种容器像`std::map`一样，只接受具有唯一键的记录。

示例 13.3，“显式使用 `boost::bimaps::set_of`”指定了`boost::bimaps::set_of`。

除了`boost::bimaps::set_of`之外，其他容器类型也可用于`boost::bimap`。

## 示例 13.4. 使用 `boost::bimaps::set_of` 允许重复

```cpp
#include <boost/bimap.hpp>
#include <boost/bimap/set_of.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::bimap<boost::bimaps::set_of<std::string>,
    boost::bimaps::set_of<int>> bimap;
  bimap animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});

  std::cout << animals.left.count("spider") << '\n';
  std::cout << animals.right.count(8) << '\n';
}
```

示例 13.4，“使用 `boost::bimaps::set_of` 允许重复”使用`boost::bimaps::multiset_of`，它类似于`boost::bimaps::set_of`，只是键不需要是唯一的。因为`boost::bimaps::set_of`是默认用于`boost::bimap`的，所以不需要包含`boost/bimap/set_of.hpp`。对于其他容器类型，必须包含相应的头文件。

除了上述的`boost::bimaps::set_of`，Boost.Bimap 还提供了：`boost::bimaps::unordered_set_of`、`boost::bimaps::unordered_multiset_of`、`boost::bimaps::list_of`、`boost::bimaps::vector_of`以及`boost::bimaps::unconstrained_set_of`。除了`boost::bimaps::unconstrained_set_of`之外，所有的容器类型都与标准库中的对应项相似。

## 示例 13.5. 使用 `unconstrained_set_of` 禁用一侧

```cpp
#include <boost/bimap.hpp>
#include <boost/bimap/unconstrained_set_of.hpp>
#include <boost/bimap/support/lambda.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::bimap<std::string,
    boost::bimaps::unconstrained_set_of<int>> bimap;
  bimap animals;

  animals.insert({"cat", 4});
  animals.insert({"shark", 0});
  animals.insert({"spider", 8});

  auto it = animals.left.find("cat");
  animals.left.modify_key(it, boost::bimaps::_key = "dog");

  std::cout << it->first << '\n';
}
```

`boost::bimaps::unconstrained_set_of`可用于禁用`boost::bimap`的一侧。在示例 13.5，“使用 `unconstrained_set_of` 禁用一侧”中，`boost::bimap`的行为类似于`std::map`。你无法访问`right`来通过腿数搜索动物。

示例 13.5，“使用 `unconstrained_set_of` 禁用一侧”说明了另一个为什么倾向于使用`boost::bimap`而不是`std::map`的理由。由于 Boost.Bimap 基于 Boost.MultiIndex，因此 Boost.MultiIndex 的成员函数是可用的。示例 13.5，“使用 `unconstrained_set_of` 禁用一侧”使用`modify_key()`修改键——这在`std::map`中是不可能的。

注意键是如何修改的。通过`boost::bimaps::_key`给当前键赋一个新值，它是定义在`boost/bimap/support/lambda.hpp`中的一个占位符。

`boost/bimap/support/lambda.hpp`也定义了`boost::bimaps::_data`。当调用成员函数`modify_data()`时，可以使用`boost::bimaps::_data`修改类型为`boost::bimap`的容器中的值。

# 14. Boost.Array

[Boost.Array](http://www.boost.org/libs/array/)库在`boost/array.hpp`中定义了类模板`boost::array`。`boost::array`与`std::array`类似，后者是 C++11 添加到标准库的。如果你在 C++11 开发环境下工作，可以忽略`boost::array`。

### 示例 14.1. `boost::array` 的各种成员函数

```cpp
#include <boost/array.hpp>
#include <string>
#include <algorithm>
#include <iostream>

int main()
{
  typedef boost::array<std::string, 3> array;
  array a;

  a[0] = "cat";
  a.at(1) = "shark";
  *a.rbegin() = "spider";

  std::sort(a.begin(), a.end());

  for (const std::string &s : a)
    std::cout << s << '\n';

  std::cout << a.size() << '\n';
  std::cout << a.max_size() << '\n';
}
```



使用 `boost::array` 可以创建一个具有与 C 数组相同属性的数组。此外，`boost::array` 符合 C++ 容器的要求，这使得处理此类数组就像处理任何其他容器一样简单。从原则上，可以将 `boost::array` 视为容器 `std::vector`，区别是 `boost::array` 中的元素数量是常数。

如示例 14.1，“`boost::array` 的各种成员函数”所示，使用 `boost::array` 相当简单，不需要额外的解释，因为调用的成员函数与其在 `std::vector` 中的对应函数具有相同的含义。

# 15. Boost.Unordered

[Boost.Unordered](http://www.boost.org/libs/unordered) 提供了类 `boost::unordered_set`、`boost::unordered_multiset`、`boost::unordered_map` 和 `boost::unordered_multimap`。这些类与 C++11 添加到标准库的哈容器相同。因此，如果你在支持 C++11 的开发环境下工作，可以忽略 Boost.Unordered 中的容器。

## 示例 15.1. 使用 `boost::unordered_set`

```cpp
#include <boost/unordered_set.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::unordered_set<std::string> unordered_set;
  unordered_set set;

  set.emplace("cat");
  set.emplace("shark");
  set.emplace("spider");

  for (const std::string &s : set)
    std::cout << s << '\n';

  std::cout << set.size() << '\n';
  std::cout << set.max_size() << '\n';

  std::cout << std::boolalpha << (set.find("cat") != set.end()) << '\n';
  std::cout << set.count("shark") << '\n';
}
```

`boost::unordered_set` 可以在示例 15.1，“使用 `boost::unordered_set`”中被 `std::unordered_set` 替换。`boost::unordered_set` 与 `std::unordered_set` 没有区别。

## 示例 15.2. 使用 `boost::unordered_map`

```cpp
#include <boost/unordered_map.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::unordered_map<std::string, int> unordered_map;
  unordered_map map;

  map.emplace("cat", 4);
  map.emplace("shark", 0);
  map.emplace("spider", 8);

  for (const auto &p : map)
    std::cout << p.first << ";" << p.second << '\n';

  std::cout << map.size() << '\n';
  std::cout << map.max_size() << '\n';

  std::cout << std::boolalpha << (map.find("cat") != map.end()) << '\n';
  std::cout << map.count("shark") << '\n';
}
```

示例 15.2，“使用 `boost::unordered_map`”使用 `boost::unordered_map` 来存储几种动物的名称和腿数。再次，`boost::unordered_map` 可以被 `std::unordered_map` 替换。

在示例 15.3，“使用 Boost.Unordered 的自定义类型”中，`animal` 类型的元素存储在类型为 `boost::unordered_set` 的容器中。由于 `boost::unordered_set` 哈希函数不知道 `animal` 类，因此无法自动计算该类型的哈希值。这就是必须定义哈希函数的原因——否则示例无法编译。

需要定义的哈希函数名称为 `hash_value()`。它必须接收要计算哈希值的对象作为唯一参数。`hash_value()` 的返回值类型必须是 `std::size_t`。

当需要计算对象的哈希值时，会自动调用 `hash_value()`。该函数在 Boost 库中已为多种类型定义，包括 `std::string`。对于自定义类型，它必须由开发者定义。

通常，`hash_value()` 的定义非常简单：哈希值通过访问对象的成员变量创建。这是通过 `hash_value()` 函数完成的。

## 示例 15.3. 使用 Boost.Unordered 的自定义类型

```cpp
#include <boost/unordered_set.hpp>
#include <string>
#include <iostream>
#include <functional/hash.hpp>

struct animal {
    std::string name;
    int legs;
};

bool operator==(const animal &lhs, const animal &rhs) {
    return lhs.name == rhs.name && lhs.legs == rhs.legs;
}

std::size_t hash_value(const animal &a) {
    std::size_t seed = 0;
    boost::hash_combine(seed, a.name);
    boost::hash_combine(seed, a.legs);
    return seed;
}

int main() {
    typedef boost::unordered_set<animal> unordered_set;
    unordered_set set;

    set.insert({"cat", 4});
    set.insert({"shark", 0});
    set.insert({"spider", 8});

    for (const auto &a : set) {
        std::cout << a.name << ": " << a.legs << '\n';
    }

    return 0;
}
```

要使用 `Boost.CircularBuffer` 中的循环缓冲区，请包含头文件 `boost/circular_buffer.hpp`。该头文件定义了 `boost::circular_buffer` 类。

`boost::circular_buffer` 是一个模板，必须用类型进行实例化。例如，在示例 16.1，“使用 `boost::circular_buffer`”中，循环缓冲区 `cb` 存储了 `int` 类型数字。

循环缓冲区的容量是在实例化类时指定的，而不是通过模板参数。`boost::circular_buffer` 的默认构造函数创建一个容量为零个元素的缓冲区。提供了另一个构造函数来设置容量。在示例 16.1，“使用 `boost::circular_buffer`”中，缓冲区 `cb` 的容量为三个元素。

## 示例 16.1. 使用 `boost::circular_buffer`

```cpp
#include <boost/circular_buffer.hpp>
#include <iostream>

int main()
{
  typedef boost::circular_buffer<int> circular_buffer;
  circular_buffer cb{3};

  std::cout << cb.capacity() << '\n';
  std::cout << cb.size() << '\n';

  cb.push_back(0);
  cb.push_back(1);
  cb.push_back(2);

  std::cout << cb.size() << '\n';

  cb.push_back(3);
  cb.push_back(4);
  cb.push_back(5);

  std::cout << cb.size() << '\n';

  for (int i : cb)
    std::cout << i << '\n';
}
```

可以通过调用 `capacity()` 来查询循环缓冲区的容量。在示例 16.1，“使用 `boost::circular_buffer`”中，`capacity()` 将返回 3。

容量并不等于所存储元素的数量。虽然 `capacity()` 的返回值是常数，但 `size()` 返回缓冲区中的元素数量，两者可能不同。`size()` 的返回值始终在 0 和循环缓冲区的容量之间。

示例 16.1，“使用 `boost::circular_buffer`”在第一次调用 `size()` 时返回 0，因为缓冲区不包含任何数据。在调用三次 `push_back()` 之后，缓冲区包含了三个元素，第二次调用 `size()` 将返回 3。再次调用 `push_back()` 不会导致缓冲区增长。新的三个数字将覆盖之前的三个数字。因此，当第三次调用 `size()` 时，它将返回 3。

作为一种验证，存储的数字会在示例 16.1，“使用 `boost::circular_buffer`”结束时写入标准输出。输出包含数字 3、4 和 5，因为之前存储的数字已经被覆盖了。

## 示例 16.2. `boost::circular_buffer` 的各种成员函数

```cpp
#include <boost/circular_buffer.hpp>
#include <iostream>

int main()
{
  typedef boost::circular_buffer<int> circular_buffer;
  circular_buffer cb{3};

  cb.push_back(0);
  cb.push_back(1);
  cb.push_back(2);
  cb.push_back(3);

  std::cout << std::boolalpha << cb.is_linearized() << '\n';

  circular_buffer::array_range ar1, ar2;

  ar1 = cb.array_one();
  ar2 = cb.array_two();
  std::cout << ar1.second << ";" << ar2.second << '\n';

  for (int i : cb)
    std::cout << i << '\n';

  cb.linearize();

  ar1 = cb.array_one();
  ar2 = cb.array_two();
  std::cout << ar1.second << ";" << ar2.second << '\n';
}
```

示例 16.2，“`boost::circular_buffer` 的各种成员函数”使用了成员函数 `is_linearized()`、`array_one()`、`array_two()` 和 `linearize()`，这些函数在其他容器中不存在。这些成员函数明确了循环缓冲区的内部结构。

循环缓冲区本质上可以与 `std::vector` 比较。由于起始和结束是有明确定义的，`vector` 可以被视为传统的 C 数组。也就是说，内存是连续的，第一个和最后一个元素始终位于最低和最高的内存地址。然而，循环缓冲区并不提供这种保证。

尽管谈论循环缓冲区的起始和结束听起来很奇怪，但它们确实存在。可以通过迭代器访问元素，`boost::circular_buffer` 提供了 `begin()` 和 `end()` 等成员函数。在使用迭代器时，你不需要担心起始和结束的位置，但使用普通指针访问元素时，情况会变得复杂一些，除非你使用 `is_linearized()`、`array_one()`、`array_two()` 和 `linearize()`。

成员函数 `is_linearized()` 在循环缓冲区的起始位置位于最低内存地址时返回 `true`。在这种情况下，缓冲区中的所有元素都从起始到结束以递增的内存地址连续存储，可以像传统的 C 数组一样访问元素。

如果 `is_linearized()` 返回 `false`，则循环缓冲区的起始不在最低内存地址，这在示例 16.2，“`boost::circular_buffer` 的各种成员函数”中所示。虽然前三个元素 0、1 和 2 是完全按照这个顺序存储的，但第四次调用 `push_back()` 将用 3 覆盖 0。由于 3 是 `push_back()` 添加的最后一个元素，它现在是循环缓冲区的结束。起始现在是元素 1，它存储在下一个内存地址。这意味着元素不再以递增的内存地址存储。

为了避免计算每个数组的位置和大小，`boost::circular_buffer` 提供了成员函数 `array_one()` 和 `array_two()`。`array_one()` 和 `array_two()` 都返回一个 `std::pair`，其第一个元素是对应数组的指针，第二个元素是大小。`array_one()` 访问循环缓冲区起始数组，而 `array_two()` 访问结束处的数组。

如果循环缓冲区是线性的且 `is_linearized()` 返回 `true`，也可以调用 `array_two()`。但由于缓冲区只有一个数组，第二个数组不包含元素。

为了简化问题并将循环缓冲区视为传统的 C 数组，可以通过调用 `linearize()` 强制元素进行重新排列。完成后，可以使用 `array_one()` 访问所有存储的元素。

Boost.CircularBuffer 提供了另一个名为 `boost::circular_buffer_space_optimized` 的类。该类也定义在 `boost/circular_buffer.hpp` 中。虽然该类的用法与 `boost::circular_buffer` 相同，但它在实例化时并不预留内存。相反，在添加元素时动态分配内存，直到达到容量。移除元素会释放内存。`boost::circular_buffer_space_optimized` 内存内存更高效，因此在某些场景下可能是更好的选择。例如，如果你需要一个容量很大的循环缓冲区，但程序并不总是使用整个缓冲区，它可能是一个很好的选择。

# 17. Boost.Heap

[Boost.Heap](http://www.boost.org/libs/heap) 也可以称为 Boost.PriorityQueue，因为该库提供了多种优先级队列。然而，Boost.Heap 中的优先级队列与 `std::priority_queue` 的区别在于它支持更多函数。

## 示例 17.1. 使用 `boost::heap::priority_queue`

```cpp
#include <boost/heap/priority_queue.hpp>
#include <iostream>

using namespace boost::heap;

int main()
{
  priority_queue<int> pq;
  pq.push(2);
  pq.push(3);
  pq.push(1);

  for (int i : pq)
    std::cout << i << '\n';

  priority_queue<int> pq2;
  pq2.push(4);
  std::cout << std::boolalpha << (pq > pq2) << '\n';
}
```

示例 17.1，“使用 `boost::heap::priority_queue`”使用了类 `boost::heap::priority_queue`，该类定义在 `boost/heap/priority_queue.hpp` 中。通常，该类的行为类似于 `std::priority_queue`，它允许你对元素进行迭代。迭代返回的元素顺序是随机的。

`boost::heap::priority_queue` 类型的对象可以相互比较。示例 17.1，“使用 `boost::heap::priority_queue`”中的比较返回 `true` 是因为 `pq` 拥有的元素比 `pq2` 多。如果两个队列的元素数量相同，则将成对元素进行比较。

## 示例 17.2. 使用 `boost::heap::binomial_heap`



```cpp
#include <boost/heap/binomial_heap.hpp>
#include <iostream>

using namespace boost::heap;

int main()
{
  binomial_heap<int> bh;
  bh.push(2);
  bh.push(3);
  bh.push(1);

  binomial_heap<int> bh2;
  bh2.push(4);
  bh.merge(bh2);

  for (auto it = bh.ordered_begin(); it != bh.ordered_end(); ++it)
    std::cout << *it << '\n';
  std::cout << std::boolalpha << bh2.empty() << '\n';
}
```

示例 17.2，“使用 `boost::heap::binomial_heap`”引入了类 `boost::heap::binomial_heap`。除了允许你按优先级顺序迭代元素外，它还允许合并优先级队列。从一个队列的元素可以添加到另一个队列中。

该示例在队列 `bh` 上调用了 `merge()`。队列 `bh2` 作为参数传递。对 `merge()` 的调用将数字 4 从 `bh2` 移动到 `bh`。调用后，`bh` 包含四个数字，而 `bh2` 为空。

`for` 循环在 `bh` 上调用了 `ordered_begin()` 和 `ordered_end()`。`ordered_begin()` 返回一个从高优先级元素到低优先级元素的迭代器。因此，示例 17.2，“使用 `boost::heap::binomial_heap`”按顺序向标准输出写入数字 4、3、2 和 1。

`boost::heap::binomial_heap` 允许你在元素添加到队列后对其进行修改。示例 17.3，“在 `boost::heap::binomial_heap` 中更改元素”保存了 `push()` 返回的句柄，使得能够访问存储在 `bh` 中的数字 2。

`update()` 是 `boost::heap::binomial_heap` 的成员函数，可以通过调用它来更改元素。示例 17.3，“在 `boost::heap::binomial_heap` 中更改元素”调用该成员函数将 2 替换为 4。之后，使用 `top()` 获取当前优先级最高的元素（现在为 4）。

### 示例 17.3. 在 `boost::heap::binomial_heap` 中更改元素

```cpp
#include <boost/heap/binomial_heap.hpp>
#include <iostream>

using namespace boost::heap;

int main()
{
  binomial_heap<int> bh;
  auto handle = bh.push(2);
  bh.push(3);
  bh.push(1);

  bh.update(handle, 4);

  std::cout << bh.top() << '\n';
}
```

除了 `update()` 之外，`boost::heap::binomial_heap` 还提供了其他成员函数来更改元素。如果你预先知道更改会导致更高或更低的优先级，可以调用 `increase()` 或 `decrease()` 成员函数。在示例 17.3，“在 `boost::heap::binomial_heap` 中更改元素”中，调用该成员函数将 2 替换为 4。之后，优先级最高的元素（现在是 4）通过 `top()` 获取。

## Boost.Intrusive

[Boost.Intrusive](https://www.boost.org/doc/libs/1_84_0/doc/html/intrusive/index.html) 提供了要求元素提供链接所需指针的容器。这允许在不进行节点分配的情况下进行插入和删除操作。当你希望自己管理元素的内存或避免单独分配节点的开销时，侵入式容器非常有用。

### 使用 `intrusive::list`

示例 17.1，“使用 `intrusive::list`”使用继承自 `list_base_hook` 的 `animal` 类。

```cpp
#include <boost/intrusive/list.hpp>
#include <string>
#include <utility>
#include <iostream>

using namespace boost::intrusive;

struct animal : public list_base_hook<>
{
  std::string name;
  int legs;
  animal(std::string n, int l) : name{std::move(n)}, legs{l} {}
};

int main()
{
  animal a1{"cat", 4};
  animal a2{"shark", 0};
  animal a3{"spider", 8};

  typedef list<animal> animal_list;
  animal_list animals;

  animals.push_back(a1);
  animals.push_back(a2);
  animals.push_back(a3);

  a1.name = "dog";

  for (const animal &a : animals)
    std::cout << a.name << '\n';
}
```

`intrusive::list` 要求元素派自某个钩子（hook）。在这种情况下，`list_base_hook` 提供了双向链所需的指针。这允许 `list` 在不为节点分配额外内存的情况下管理 `animal` 对象。

重要的是理解，侵入式容器并不存储副本；它们存储的是原始对象。示例 18.1，“使用 `boost::intrusive::list`”会向标准输出写入 `dog`、`shark` 和 `spider`，而不是 `cat`。对象 `a1` 被链接到列表中。这就是为什么当程序遍历列表中的元素并显示名称时，名称的更改是可见的。

由于侵入式容器不存储副本，因此在销毁对象之前，必须将其从侵入式容器中移除。

### 示例 18.2. 移除并销毁动态分配的对象

```cpp
#include <boost/intrusive/list.hpp>
#include <string>
#include <utility>
#include <iostream>

using namespace boost::intrusive;

struct animal : public list_base_hook<>
{
  std::string name;
  int legs;
  animal(std::string n, int l) : name{std::move(n)}, legs{l} {}
};

int main()
{
  animal a1{"cat", 4};
  animal a2{"shark", 0};
  animal *a3 = new animal{"spider", 8};

  typedef list<animal> animal_list;
  animal_list animals;

  animals.push_back(a1);
  animals.push_back(a2);
  animals.push_back(*a3);

  animals.pop_back();
  delete a3;

  for (const animal &a : animals)
    std::cout << a.name << '\n';
}
```

示例 18.2，“移除并销毁动态分配的对象”使用 `new` 创建了一个类型为 `animal` 的对象并将其插入列表 `animals`。如果你不再需要该对象并想用 `delete` 销毁它时，必须先从列表中移除。确保在销毁对象之前将其从列表中移除——顺序是非常重要的。否则，侵入式容器元素中的指针可能会指向一个不再包含 `animal` 类型对象的内存位置。

由于侵入式容器既不分配也不释放内存，因此当侵入式容器被销毁时，存储其中的对象继续存在。

由于从侵入式容器中移除元素不会自动销毁它们，容器提供了非标准的扩展。`pop_back_and_dispose()` 就是其中一个成员函数。

### 示例 18.3. 使用 `pop_back_and_dispose()` 移除并销毁

```cpp
#include <boost/intrusive/list.hpp>
#include <string>
#include <utility>
#include <iostream>

using namespace boost::intrusive;

struct animal : public list_base_hook<>
{
  std::string name;
  int legs;
  animal(std::string n, int l) : name{std::move(n)}, legs{l} {}
};

int main()
{
  animal a1{"cat", 4};
  animal a2{"shark", 0};
  animal *a3 = new animal{"spider", 8};

  typedef list<animal> animal_list;
  animal_list animals;

  animals.push_back(a1);
  animals.push_back(a2);
  animals.push_back(*a3);

  animals.pop_back_and_dispose([](animal *a){ delete a; });

  for (const animal &a : animals)
    std::cout << a.name << '\n';
}
```

`pop_back_and_dispose()` 从列表中移除一个元素并销毁它。由于侵入式容器不知道应该如何销毁元素，因此你需要向 `pop_back_and_dispose()` 传递一个知道如何销毁元素的函数或函数对象。`pop_back_and_dispose()` 会从列表中移除该对象，然后调用该函数或函数对象，并传递指向待销毁对象的指针。示例 18.3，“使用 `pop_back_and_dispose()` 移除并销毁”传递了一个调用 `delete` 的 lambda 函数。

在示例 18.3，“使用 `pop_back_and_dispose()` 移除并销毁”中，只有 `animals` 中的第三个元素可以被 `pop_back_and_dispose()` 移除。列表中的其他元素不是用 `new` 创建的，因此不能用 `delete` 销毁。

Boost.Intrusive 支持另一种机制来将元素的移除和销毁结合起来。

### 示例 18.4. 使用自动解链模式移除并销毁

```cpp
#include <boost/intrusive/list.hpp>
#include <string>
#include <utility>
#include <iostream>

using namespace boost::intrusive;

typedef link_mode<...> mode;

struct animal : public list_base_hook<>
{
  std::string name;
  int legs;
  animal(std::string n, int l) : name{std::move(n)}, legs{l} {}
};

int main()
{
  animal a1{"cat", 4};
  animal a2{"shark", 0};
  animal *a3 = new animal{"spider", 8};

  typedef list<animal> animal_list;
  animal_list animals;

  animals.push_back(a1);
  animals.push_back(a2);
  animals.push_back(*a3);

  delete a3;

  for (const animal &a : animals)
    std::cout << a.name << '\n';
}
```

Hooks 支持 `link_mode` 的一个参数。自动解链模式（auto unlink mode）会在元素被销毁时从侵入式容器中移除它。示例 18.4，“使用自动解链模式移除并销毁”仅向标准输出写入了 `cat` 和 `shark`。自动解链模式意味着 `size()` 所花费的时间取决于容器中存储了多少元素。要更改 `size()` 的复杂度，请使用 `boost::intrusive::constant_time_size`，它接受 `true` 或 `false` 作为模板参数。`boost::intrusive::constant_time_size` 可以作为第二个模板参数传递给侵入式容器（如 `boost::intrusive::list`），以设置复杂度。

现在我们已经看到侵入式容器支持链接模式，并且有一个设置复杂度的选项，这似乎还有很多可以发现的，但实际上并没有。例如，只有三种链接模式，而自动解链模式是你唯一需要了解的。如果你不选择链接模式，使用的默认模式对于所有其他情况都是足够的。

此外，其他成员函数没有选项。除了 `boost::intrusive::constant_time_size` 之外，没有其他你需要学习的类了。

示例 18.5，“为 `boost::intrusive::set` 定义成员变量 hook”介绍了使用另一种侵入式容器 `boost::intrusive::set` 的 hook 机制。

### 示例 18.5. 为 `boost::intrusive::set` 定义成员变量

```cpp
#include <boost/intrusive/set.hpp>
#include <string>
#include <utility>
#include <iostream>

using namespace boost::intrusive;

struct animal
{
  std::string name;
  int legs;
  set_member_hook<> set_hook;
  animal(std::string n, int l) : name{std::move(n)}, legs{l} {}
  bool operator<(const animal &a) const { return legs < a.legs; }
};

int main()
{
  animal a1{"cat", 4};
  animal a2{"shark", 0};
  animal a3{"spider", 8};

  typedef member_hook<animal, set_member_hook<>, &animal::set_hook> hook;
  typedef set<animal, hook> animal_set;
  animal_set animals;

  animals.insert(a1);
  animals.insert(a2);
  animals.insert(a3);

  for (const animal &a : animals)
    std::cout << a.name << '\n';
}
```

向类添加钩子（hook）有两种方法：要么从 hook 派生类，要么将 hook 定义为成员变量。之前的示例是从类派生 `boost::intrusive::list_base_hook`，而示例 18.5，“将成员变量为 `boost::intrusive::set` 定义 hook”使用类 `boost::intrusive::set_member_hook` 来定义一个成员变量。

请注意，成员变量的名称并不重要。然而，你使用的 hook 类取决于侵入式容器（intrusive container）。例如，要为侵入式列表定义一个成员变量作为 hook，应该使用 `boost::intrusive::list_member_hook` 而不是 `boost::intrusive::set_member_hook`。

侵入式容器有不同的 hook，因为它们对元素有不同的要求。然而，你可以使用多个 hook 允许对象存储在多个侵入式容器中。`boost::intrusive::any_base_hook` 和 `boost::intrusive::any_member_hook` 让你可以将对象存储在任何侵入式容器中。得亏这些类，你不需要从多个 hook 派生，或定义多个成员变量作为 hook。

侵入式容器默认期望 hook 定义在基类中。如果使用成员变量作为 hook，如示例 18.5，“将成员变量为 `boost::intrusive::set` 定义 hook”所示，则必须告诉侵入式容器使用哪一个成员变量。这就是为什么 `animal` 和 `hook` 类型都被传递给 `boost::intrusive::set`。`hook` 是通过 `boost::intrusive::member_hook` 定义的，每当成员变量作为 hook 使用时，就会使用它。`boost::intrusive::member_hook` 期望元素类型、hook 类型以及指向成员变量的指针作为模板参数。

示例 18.5，“将成员变量为 `boost::intrusive::set` 定义 hook”按顺序将 `shark`、`cat` 和 `spider` 写入标准输出。



除了本章介绍的 `boost::intrusive::list` 和 `boost::intrusive::set` 类外，Boost.Intrusive 还提供了诸如用于单链链表的 `boost::intrusive::slist` 和用于哈希容器的 `boost::intrusive::unordered_set`。

# 19. Boost.MultiArray

[Boost.MultiArray](http://www.boost.org/libs/multi_array) 是一个简化多维数组使用的库。它最重要的优势是多维数组可以像标准库中的容器一样使用。例如，存在诸如 `begin()` 和 `end()` 等成员函数，让你能够迭代器访问多维数组中的元素。迭代器比通常用于 C 数组的指针更容易使用，特别是对于具有许多维度的数组。

## 示例 19.1. 使用 `boost::multi_array` 的一维数组

```cpp
#include <boost/multi_array.hpp>
#include <iostream>

int main()
{
  boost::multi_array<char, 1> a{boost::extents[6]};

  a[0] = 'B';
  a[1] = 'o';
  a[2] = 'o';
  a[3] = 's';
  a[4] = 't';
  a[5] = '\0';

  std::cout << a.origin() << '\n';
}
```

Boost.MultiArray 提供了 `boost::multi_array` 类来创建数组。这是最重要的类。它定义在 `boost/multi_array.hpp` 中。

`boost::multi_array` 是一个期望两个参数的模板：第一个参数是元素类型，第二个参数决定数组应该有多少维度。

在示例 19.1，“使用 `boost::multi_array` 的一维数组”中，维度由 `boost::extents` 设置。该对象被传递给构造函数。

`boost::multi_array` 可以像普通数组一样使用。通过 `operator[]` 访问元素。在示例 19.1，“使用 `boost::multi_array` 的一维数组”中，它在数组中存储五个元素。

`origin()` 返回指向第一个元素的指针。与标准库中的容器不同，`operator[]` 会检查索引是否有效。如果你不想检查索引的有效性，可以在包含 `boost/multi_array.hpp` 之前定义宏 `BOOST_DISABLE_ASTS`。

## 示例 19.2. 二维数组的视图和子数组

```cpp
#include <boost/multi_array.hpp>
#include <algorithm>
#include <iostream>
#include <cstring>

int main()
{
  boost::multi_array<char, 2> a{boost::extents[2][6]};

  typedef boost::multi_array<char, 2>::array_view<1>::type array_view;
  typedef boost::multi_array_types::index_range range;
  array_view view = a[boost::indices[0][range{0, 5}]];

  std::memcpy(view.origin(), "tsooB", 6);
  std::reverse(view.begin(), view.end());

  std::cout << view.origin() << '\n';

  boost::multi_array<char, 2>::reference subarray = a[1];
  std::memcpy(subarray.origin(), "C++", 4);

  std::cout << subarray.origin() << '\n';
}
```

示例 19.2，“二维数组的视图和子数组”创建了一个二维数组。第一维的元素数量设置为 2，第二个维度设置为 6。将该数组想象成一个 2 行 6 列的表格。

表格的第一行将包含单词 "Boost"。由于只需要存储该单词五个字母，因此创建了一个跨越数组五个元素的视图。

视图基于 `boost::multi_array::array_view`，让你访问数组的一部分并将该部分视为一个独立的数组。

`boost::multi_array::array_view` 是一个模板，期望视图的维度数量作为模板参数。在示例 19.2，“二维数组的视图和子数组”中，视图的维度为 1。因为数组 `a` 有两个维度，所以一个维度被忽略了。

在示例 19.2，“二维数组的视图和子数组”中，传递给 `boost::indices` 的第一个参数不是范围，而是数字 `0`。当传递数字时，你无法使用 `boost::multi_array_types::index_range`。在示例中，视图将获取 `a` 的第一维——即索引为 `0` 的那维。

对于第二个参数，使用 `boost::multi_array_types::index_range` 来定义一个范围。通过向构造函数传递 `0` 和 `5`，使得 `a` 第一维的前五个元素变得可用。该范围从索引 `0` 开始到索引 `5` 结束——不包含索引为 `5` 的元素。第一维的第六个元素被忽略。

因此，`view` 是一个包含五个元素的一维数组——即 `a` 第一行的前五个元素。当访问 `view` 并使用 `std::memcpy()` 拷贝字符串以及使用 `std::reverse()` 反转元素时，这种关系并不重要。一旦视图被创建，它表现就像一个包含五个元素的独立数组。

当在类型为 `boost::multi_array` 的数组上调用 `operator[]` 时，返回值取决于维度的数量。在示例 19.1，“使用 `boost::multi_array` 的一维数组”中，该操作符返回 `char` 元素，因为访问的数组是一维的。

在示例 19.2，“二维数组的视图和子数组”中，`a` 是一个二维数组。因此，`operator[]` 返回一个子数组而不是 `char` 元素。由于子数组的类型不是公开的，必须使用 `boost::multi_array::reference`。即使子数组的行为类似于视图，该类型也不等同于 `boost::multi_array::array_view`。视图必须显式定义并可以跨越数组的任意部分，而子数组是由 `operator[]` 自动返回的，并跨越维维所有元素。

### 示例 19.3. 使用 `boost::multi_array_ref` 封装 C 数组

```cpp
#include <boost/multi_array.hpp>
#include <algorithm>
#include <iostream>
#include <cstring>

int main()
{
  char c[12] =
  {
    't', 's', 'o', 'o', 'B', '\0',
    'C', '+', '+', '\0', '\0', '\0'
  };

  boost::multi_array_ref<char, 2> a{c, boost::extents[2][6]};

  typedef boost::multi_array<char, 2>::array_view<1>::type array_view;
  typedef boost::multi_array_types::index_range range;
  array_view view = a[boost::indices[0][range{0, 5}]];

  std::reverse(view.begin(), view.end());
  std::cout << view.origin() << '\n';

  boost::multi_array<char, 2>::reference subarray = a[1];
  std::cout << subarray.origin() << '\n';
}
```

类 `boost::multi_array_ref` 封装了一个现有的 C 数组。在示例 19.3，“使用 `boost::multi_array_ref` 封装 C 数组”中，`a` 提供了与 `boost::multi_array` 相同的接口，但不分配内存。通过 `boost::multi_array_ref`，C 数组——无论它有多少维——都可以被视为类型为 `boost::multi_array` 的多维数组。只需要将 C 数组作为额外的参数添加到构造函数即可。

Boost.MultiArray 还提供了 `boost::const_multi_array_ref` 类，它将 C 数组视为常量多维数组。

# 20. Boost.Container

[Boost.Container](http://www.boost.org/libs/container) 是一个 Boost 库，提供了与标准库相同的容器。Boost.Container 专注于额外的灵活性。例如，来自该库中的所有容器都可以在共享内存中配合 Boost.Interprocess 使用——这对于标准库中的容器来说并不总是可以实现的。

Boost.Container 提供了额外的优势：

- 容器的接口与 C++11 标准库中的容器相似。例如，它们提供了诸如 `emplace_back()` 等成员函数，尽管该函数直到 C++11 才被加入标准库，但你仍可以在 C++98 程序中使用它。

- 通过 `boost::container::slist` 或 `boost::container::stable_vector`，Boost.Container 提供了标准库未提供的容器。

- 其实现是平台无关的。容器在任何地方的行为都相同。你不需要担心标准库实现之间可能存在的差异。

- Boost.Container 的容器支持不完整类型，并可以用于定义递归容器。

示例 20.1，“使用 Boost.Container 的递归容器”演示了不完整类型。

### 注意

本章中的示例无法用 Visual C++ 2003 编译。此错误在 [ticket9332](https://svn.boost.org/trac/boost/9332) 中描述。它已在 Boost 1.56.0 中修复。

```cpp
#include <container/vector.hpp>

namespace boost::container;

struct animal
{
  vector<animal> children;
};

int main()
{
  animal parent, child1, child2;
  parent.children.push_back(child1);
  parent.children.push_back(child2);
}
```

类 `animal` 有一个类型为 `vector<animal>` 的成员变量 `children`。`vector` 定义在 `container/vector.hpp` 中。因此，成员变量 `children` 的类型基于类 `animal`。虽然标准没有要求标准库容器支持不完整类型，但 Boost 显式支持递归容器。

示例 20.2，“使用 `boost::container::stable_vector`”

### 示例 20.2. 使用 `stable_vector`

```cpp
#include <container/stable_vector.hpp>
#include <iostream>

using namespace boost::container;

int main()
{
  stable_vector<int> v(2, 1);
  int &i = v[1];
  v.erase(v.begin());
  std::cout << i << '\n';
}
```

Boost.Container 在标准库著名的容器之外提供了容器。示例 20.2，“使用 `boost::container::stable_vector`”引入了容器 `boost::container::stable_vector`，它的行为与 `std::vector` 相似，但当 `boost::container::stable_vector` 变化时，迭代器和引用仍然有效。这是因为元素在 `boost::container::stable_vector` 中并不是连续存储的。尽管元素不是相邻存储的，但仍然可以使用索引访问元素。

Boost.Container 保证在示例 20.2，“使用 `boost::container::stable_vector`”中，删除向量中的第一个元素时，引用 `i` 仍然有效。示例显示为 `1`。

请注意，`boost::container::stable_vector` 以及该库的其他容器都不支持 C++11 初始化列表。在示例 20.2，“使用 `boost::container::stable_vector`”中，`v` 被初始化为两个元素，值都设置为 1。

`boost::container::stable_vector` 定义在 `container/stable_vector.hpp` 中。

- `boost::container::flat_set` 和 `boost::container::flat_map` 类似于 `std::set` 和 `std::map`。然而，它们被实现为有序 vector，而不是树。这允许更快的查找和迭代，但插入和删除元素的开销更大。

  这两个容器定义在头文件 `boost/container/flat_set.hpp` 和 `boost/container/flat_map.hpp` 中。

- `boost::container::slist` 是一个单链表。它类似于 `std::forward_list`，后者是 C++11 添加到标准库的。`boost::container::slist` 提供了成员函数 `size()`，而 `std::forward_list` 缺少该函数。

  `boost::container::slist` 定义在 `boost/container/slist.hpp` 中。

- `boost::container::static_vector` 像 `std::array` 一样直接将元素存储在容器中。像 `std::array` 一样，容器具有固定容量，尽管容量并不代表元素的数量。可以使用成员函数 `push_back()`、`pop_back()`、`insert()` 和 `erase()` 来插入或删除元素。在这方面，`boost::container::static_vector` 类似于 `std::vector`。成员函数 `size()` 返回容器中当前存储的元素数量。

  容量是固定的，但可以通过 `resize()` 进行更改。`push_back()` 不改变容量。只有当容量大于当前存储的元素数量时，你才能通过 `push_back()` 添加元素。否则 `push_back()` 会抛出类型为 `std::bad_alloc` 的异常。

  `boost::container::static_vector` 定义在 `boost/container/static_vector.hpp` 中。

# 第四部分 数据结构

数据结构与容器相似，因为它们可以存储一个或多个元素。然而，它们与容器的区别在于，它们不支持容器通常支持的操作。例如，使用本部分引入的数据结构无法在单次迭代中访问所有元素。

- Boost.Optional 使得标记可选返回值变得简单。使用 Boost.Optional 创建的对象要么为空，要么包含单个元素。通过 Boost.Optional，你不需要诸如空指针或 -1 等特殊值来指示函数可能没有返回值。

- Boost.Tuple 提供了 `boost::tuple`，该类自 C++11 起一直是标准库的一部分。

- Boost.Any 和 Boost.Variant 允许你创建存储不同类型值的变量。Boost.Any 支持任意类型，而 Boost.Variant 允许你将需要支持的类型作为模板参数传递。

- Boost.PropertyTree 提供了一种类似树的数据结构。该库通常用于帮助管理配置数据。数据也可以以 JSON 等格式写入文件或从文件加载。

- Boost.DynamicBitset 提供了一个类似于 `std::bitset` 的类，但在运行时进行配置。

- Boost.Tribool 提供了一种类似于 `bool` 但支持三种状态的数据类型。

- Boost.CompressedPair 定义了类 `boost::compressed_pair`，它可以替换 `std::pair`。该类支持所谓的空基类优化。

# 21. Boost.Optional

该库 [Boost.Optional](http://www.boost.org/libs/optional) 提供了 `boost::optional` 类，可用于可选返回值。这些是可能不总是返回结果的函数的返回值。示例 21.1，“用于表示可选返回值的特殊值”展示了在没有 Boost.Optional 的情况下如何实现可选返回值。

## 示例 21.1. 用于表示可选返回值的特殊值



```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cmath>

int get_even_random_number()
{
  int i = std::rand();
  return (i % 2 == 0) ? i : -1;
}

int main()
{
  std::srand(static_cast<unsigned int>(std::time(0)));
  int i = get_even_random_number();
  if (i != -1)
    std::cout << std::sqrt(static_cast<float>(i)) << '\n';
}
```

示例 21.1，“用于表示可选返回值的特殊值”使用了函数 `get_even_random_number()`，该函数应该返回一个偶数随机数。它通过一种相当原始的方式调用标准库中的函数 `std::rand()` 来实现。如果 `std::rand()` 生成了偶数随机数，则由 `get_even_random_number()` 返回该数。如果生成的随机数是奇数，则返回 `-1`。

在这个示例中，`-1` 表示无法生成偶数随机数。因此，`get_even_random_number()` 无法保证返回偶数随机数。返回值是可选的。

许多函数使用像 `-1` 这样的特殊值来表示无法返回结果。例如，`std::string` 成员函数 `find()` 在找不到子字符串时会返回特殊值 `std::string::npos`。Boost.Optional 提供了 `boost::optional`，使得清晰地标记返回值成为可能。

### 示例 21.2. 使用 `boost::optional` 的可选值

```cpp
#include <boost/optional.hpp>
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cmath>

using boost::optional;

optional<int> get_even_random_number()
{
  int i = std::rand();
  return (i % 2 == 0) ? i : optional<int>{};
}

int main()
{
  std::srand(static_cast<unsigned int>(std::time(0)));
  optional<int> i = get_even_random_number();
  if (i)
    std::cout << std::sqrt(static_cast<float>(*i)) << '\n';
}
```

在示例 21.2，“使用 `boost::optional` 的可选值”中，`get_even_random_number()`的返回值有一个新类型 `boost::optional<int>`。`boost::optional` 是一个模板，必须使用实际类型进行实例化。使用 `boost::optional` 需要包含 `boost/optional.hpp`。

如果 `get_even_random_number()` 生成了偶数随机数，该值将被直接返回并包装在 `boost::optional<int>` 对象中，因为 `boost::optional` 提供了一个非排斥构造函数。如果 `get_even_random_number()` 没有生成偶数随机数，则返回一个空的 `boost::optional<int>` 对象。该返回值通过调用默认构造函数创建。

`main()` 检查 `i` 是否为空。如果不为空，则通过 `operator*` 访问 `i` 中的数字。`boost::optional` 看起来像指针。然而，你不应该将 `boost::optional` 视为指针，因为例如 `boost::optional` 中的值是通过拷贝构造函数拷贝的，而指针不会拷贝它指向的值。

### 示例 21.3. `boost::optional` 的其他有用成员函数

```cpp
#include <boost/optional.hpp>
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cmath>

using boost::optional;

optional<int> get_even_random_number()
{
  int i = std::rand();
  return optional<int>{i % 2 == 0, i};
}

int main()
{
  std::srand(static_cast<unsigned int>(std::time(0)));
  optional<int> i = get_even_random_number();
  if (i.is_initialized())
    std::cout << std::sqrt(static_cast<float>(i.get())) << '\n';
}
```

示例 21.3，“`boost::optional` 的其他有用成员函数”介绍了 `boost::optional` 的其他有用成员函数。该类提供了一个特殊的构造函数，接受一个条件作为第一个参数。如果条件为真，则用第二个参数初始化一个类型为 `boost::optional` 的对象。如果条件为假，则创建一个类型为 `boost::optional` 的空对象。示例 21.3，“`boost::optional` 的其他有用成员函数”在 `get_even_random_number()`函数中使用了此构造函数。

通过 `is_initialized()`，你可以检查类型为 `boost::optional` 的对象是否为空。Boost.Optional 讨论的是已初始化和未初始化的对象——因此，成员函数名为 `is_initialized()`。成员函数 `get()` 等同于 `operator*`。

Boost.Optional 提供了独立的辅助函数，如 `boost::make_optional()` 和 `boost::get_optional_value_or()`（请参见示例 21.4，“Boost.Optional 的各种辅助函数”）。可以调用 `boost::make_optional()` 来创建一个类型为 `boost::optional` 的对象。如果你想在 `boost::optional` 为空时返回默认值，可以调用 `boost::get_optional_value_or()`。

`boost::get_optional_value_or()`函数也作为 `boost::optional` 的成员函数提供。它被称为 `get_value_or()`。

结合 `boost/optional/optional_io.hpp`，Boost.Optional 提供了一个带有重载流操作符头文件，这让你可以将类型为 `boost::optional` 的对象写入标准输出等。

### 示例 21.4. Boost.Optional 的各种辅助函数

```cpp
#include <boost/optional.hpp>
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cmath>

using namespace boost;

optional<int> get_even_random_number()
{
  int i = std::rand();
  return make_optional(i % 2 == 0, i);
}

int main()
{
  std::srand(static_cast<unsigned int>(std::time(0)));
  optional<int> i = get_even_random_number();
  double d = get_optional_value_or(i, 0);
  std::cout << std::sqrt(d) << '\n';
}
```

# 22. Boost.Tuple

[Boost.Tuple](http://www.boost.org/libs/tuple)提供了一个名为 `boost::tuple` 的类，它是 `std::pair` 的通用版本。虽然 `std::pair` 只能存储两个值，但 `boost::tuple` 允许你选择存储多少个值。

标准库自 C++11 起就提供了 `std::tuple` 类。如果你使用的开发环境支持 C++11，那么可以忽略 Boost.Tuple，因为 `boost::tuple` 和 `std::tuple` 是相同的。

### 示例 22.1. `boost::tuple` 替换 `std::pair`

```cpp
#include <boost/tuple/tuple.hpp>
#include <boost/tuple/tuple_io.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tuple<std::string, int> animal;
  animal a{"cat", 4};
  std::cout << a << '\n';
}
```

要使用 `boost::tuple`，请包含头文件 `boost/tuple/tuple.hpp`。要在流中使用元组，请包含头文件 `boost/tuple/tuple_io.hpp`。Boost.Tuple 没有提供自动包含所有其他文件的主头文件。

`boost::tuple` 的用法与 `std::pair` 相同。在示例 22.1，“`boost::tuple` 替换 `std::pair`”中，创建了一个包含一个 `std::string` 类型值和一个 `int` 类型值的元组。该类型被称为 `animal`，它存储了动物的名字和腿数。

虽然类型 `animal` 的定义可以使用 `std::pair`，但类型为 `boost::tuple` 的对象可以写入流中。要做到这一点，必须包含头文件 `boost/tuple/tuple_io.hpp`，它提供了所需的操作符。示例 22.1，“`boost::tuple` 替换 `std::pair`”显示了 `(cat 4)`。

### 示例 22.2. `boost::tuple` 作为更好的 `std::pair`

```cpp
#include <boost/tuple/tuple.hpp>
#include <boost/tuple/tuple_io.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tuple<std::string, int, bool> animal;
  animal a{"cat", 4};
  std::cout << a << '\n';
}
```

示例 22.6，“写入元组元素”修改了动物名称，因此显示了 `(dog 4 true)`。

Boost.Tuple 还定义了比较运算符。要比较元组，请包含头文件 `boost/tuple/tuple_comparison.hpp`。

### 示例 22.7. 比较元组

```cpp
#include <boost/tuple/tuple.hpp>
#include <boost/tuple/tuple_comparison.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tuple<std::string, int, bool> animal;
  animal a1 = boost::make_tuple("cat", 4, true);
  animal a2 = boost::make_tuple("shark", 0, true);
  std::cout << std::boolalpha << (a1 != a2) << '\n';
}
```

示例 22.7，“比较元组”显示 `true`，因为元组 `a1` 和 `a2` 是不同的。

头文件 `boost/tuple/tuple_comparison.hpp` 还包含其他比较运算符的定义，例如大于运算符，它执行的是字典序比较。

Boost.Tuple 支持一种特殊形式的元组，称为 tier（层级）。tier 是所有元素均为引用类型的元组。它们可以使用函数 `boost::tie()` 来构造。

### 示例 22.8. 使用 `boost::tie()` 创建 tier

```cpp
#include <boost/tuple/tuple.hpp>
#include <boost/tuple/tuple_io.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tuple<std::string&, int&, bool&> animal;
  std::string name = "cat";
  int legs = 4;
  bool tail = true;
  animal a = boost::tie(name, legs, tail);
  name = "dog";
  std::cout << std::boolalpha << a << '\n';
}
```

示例 22.8，“使用 `boost::tie()` 创建 tier”创建了一个 tier `a`，它包含对变量 `name`、`legs` 和 `tail` 的引用。当变量 `name` 被修改时，该 tier 会同时被修改。

示例 22.8，“使用 `boost::tie()` 创建 tier”也可以使用 `boost::make_tuple()` 和 `boost::ref()` 来实现（参见示例 22.9，“不使用 `boost::tie()` 创建 tier”）。

### 示例 22.9. 不使用 `boost::tie()` 创建 tier

```cpp
#include <boost/tuple/tuple.hpp>
#include <boost/tuple/tuple_io.hpp>
#include <string>
#include <iostream>

int main()
{
  typedef boost::tuple<std::string&, int&, bool&> animal;
  std::string name = "cat";
  int legs = 4;
  bool tail = true;
  animal a = boost::make_tuple(boost::ref(name), boost::ref(legs),
    boost::ref(tail));
  name = "dog";
  std::cout << std::boolalpha << a << '\n';
}
```

`boost::tie()` 简化了语法。该函数也可以用于解包元组。在示例 22.10，“从元组中解包函数的返回值”中，函数返回的元组各个值会被立即存储在变量中。

### 示例 22.10. 从元组中解包函数的返回值

```cpp
#include <boost/tuple/tuple.hpp>
#include <string>
#include <iostream>

boost::tuple<std::string, int> new_cat()
{
  return boost::make_tuple("cat", 4);
}

int main()
{
  std::string name;
  int legs;
  boost::tie(name, legs) = new_cat();
  std::cout << name << ", " << legs << '\n';
}
```

`boost::tie()`将字符串“cat”和数字 4（它们都作为元组从 `new_cat()` 返回）存储在变量 `name` 和 `legs` 中。

# 23. Boost.Any

强类型语言（如 C++）要求每个变量都有特定的类型，以定义它能够存储什么种类的信息。其他语言（如 JavaScript）允许开发者在变量中存储任何类型的信息。例如，在 JavaScript 中，单个变量可以包含字符串，然后是数字，之后是另一个值。[Boost.Any](http://www.boost.org/libs/any)提供了 `boost::any` 类，它像 JavaScript 变量一样可以存储任意类型的信息。

### 示例 23.1. 使用 `boost::any`

```cpp
#include <boost/any.hpp>

int main()
{
  boost::any a = 1;
  a = 34;
  a = true;
}
```

要使用 `boost::any`，请包含头文件 `boost/any.hpp`。可以创建 `boost::any` 类型的对象来存储任意信息。在示例 23.1，“使用 `boost::any`”中，`a` 存储了 `int`，然后是 `double`，最后是 `bool`。

`boost::any` 类型存储的内容并不是无限的，有一些前提条件。存储在 `boost::any` 变量中的任何值必须是可拷贝的。因此，无法存储数组。

要存储字符串而不仅仅是字符串指针，请使用 `std::string`（参见示例 23.2，“在 `boost::any` 中存储字符串”）。

### 示例 23.2. 在 `boost::any` 中存储字符串



```cpp
#include <boost/any.hpp>
#include <string>

int main()
{
  boost::any a = std::string{"Boost"};
}
```

要访问 `boost::any` 变量的值，请使用转换运算符 `boost::any_cast`（参见 示例 23.3, “使用 `boost::any_cast` 获取值”）。

### 示例 23.3. 使用 `boost::any_cast` 获取值

```cpp
#include <boost/any.hpp>
#include <iostream>

int main()
{
  boost::any a = 1;
  std::cout << boost::any_cast<int>(a) << '\n';
  a = 34;
  std::cout << boost::any_cast<double>(a) << '\n';
  a = true;
  std::cout << std::boolalpha << boost::any_cast<bool>(a) << '\n';
}
```

通过向 `boost::any_cast` 传递适当类型来转换变量。如果指定了无效类型，将抛出 `boost::bad_any_cast` 异常。

### 示例 23.4. 错误情况下的 `boost::bad_any_cast`

```cpp
#include <boost/any.hpp>
#include <iostream>

int main()
{
  try
  {
    boost::any a = 1;
    std::cout << boost::any_cast<float>(a) << '\n';
  }
  catch (boost::bad_any_cast &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

示例 23.4, “错误情况下的 `boost::bad_any_cast`” 抛出了异常，因为 `float` 类型模板参数与存储在 `a` 中的 `int` 类型不匹配。如果使用 `short` 或 `long` 作为模板参数，程序也会抛出异常。

由于 `boost::bad_any_cast` 派自 `std::bad_cast`，`catch` 处理器也可以捕获这种异常。

要检查 `boost::any` 类型变量是否包含信息，请使用成员函数 `empty()`。要检查存储的信息类型，请使用成员函数 `type()`。

### 示例 23.5. 检查当前存储值的类型

```cpp
#include <boost/any.hpp>
#include <typeinfo>
#include <iostream>

int main()
{
  boost::any a = 1;
  if (!a.empty())
  {
    const std::type_info &ti = a.type();
    std::cout << ti.name() << '\n';
  }
}
```

示例 23.5, “检查当前存储值的类型” 同时使用了 `empty()` 和 `type()`。虽然 `empty()` 返回布尔值，但 `type()` 的返回值类型是 `std::type_info`，它定义在头文件 `typeinfo` 中。

示例 23.6, “通过指针访问值” 显示了如何使用 `boost::any_cast` 获取指向 `boost::any` 变量中存储值的指针。

### 示例 23.6. 通过指针访问值

```cpp
#include <boost/any.hpp>
#include <iostream>

int main()
{
  boost::any a = 1;
  int *i = boost::any_cast<int>(&a);
  std::cout << *i << '\n';
}
```

你只需将指向 `boost::any` 变量的指针传递给 `boost::any_cast`；模板参数保持不变。

# 24. Boost.Variant

[Boost.Variant](http://www.boost.org/libs/variant) 提供了一个名为 `boost::variant` 的类，它类似于 `union`。你可以在 `boost::variant` 变量中存储不同类型的值。在任何时候，都只能存储一个值。当赋予一个新值时，旧值会被覆盖。然而，新值的类型可能与旧值不同。唯一的要求是，这些类型必须作为模板参数传递给 `boost::variant`，以便它们对 `boost::variant` 变量是已知的。

`boost::variant` 支持任何类型。例如，可以在 `boost::variant` 变量中存储 `std::string` —— 这在 C++11 之前通过 `union` 是无法实现的。从 C++11 开始，`union` 的要求被放宽了。现在 `union` 可以包含一个 `std::string`。由于 `std::string` 必须通过放置 new（placement new）进行初始化，并且必须通过显式调用析构函数来销毁，因此即使在 C++11 开发环境中，使用 `boost::variant` 仍然有意义。

### 示例 24.1. 使用 `boost::variant`

```cpp
#include <boost/variant.hpp>
#include <string>

int main()
{
  boost::variant<double, char, std::string> v;
  v = 3.14;
  v = 'A';
  v = "Boost";
}
```

`boost::variant` 定义在 `boost/variant.hpp` 中。由于 `boost::variant` 是一个模板，至少必须指定一个参数。一个或多个模板参数指定了支持的类型。在 示例 24.1, “使用 `boost::variant`” 中，`v` 可以存储 `double`、`char` 或 `std::string` 类型的值。然而，如果你尝试给 `v` 赋值一个 `int` 类型的值，生成的代码将无法编译。

### 示例 24.2. 使用 `boost::get()` 访问 `boost::variant` 中的值

```cpp
#include <boost/variant.hpp>
#include <string>
#include <iostream>

int main()
{
  boost::variant<double, char, std::string> v;
  v = 3.14;
  std::cout << boost::get<double>(v) << '\n';
  v = 'A';
  std::cout << boost::get<char>(v) << '\n';
  v = "Boost";
  std::cout << boost::get<std::string>(v) << '\n';
}
```

要显示 `v` 存储的值，请使用自由函数 `boost::get()`（参见 示例 24.2, “使用 `boost::get()` 访问 `boost::variant` 中的值”）。

`boost::get()` 期望将对应变量有效类型之一作为模板参数。指定无效类型将导致运行时错误，因为类型验证不在编译时进行。

类型为 `boost::variant` 的变量可以写入流（如标准输出流），从而规避运行时错误的风险（参见 示例 24.3, “在流上直接输出 `boost::variant`”）。

### 示例 24.3. 在流上直接输出 `boost::variant`

```cpp
#include <boost/variant.hpp>
#include <string>
#include <iostream>

int main()
{
  boost::variant<double, char, std::string> v;
  v = 3.14;
  std::cout << v << '\n';
  v = 'A';
  std::cout << v << '\n';
  v = "Boost";
  std::cout << v << '\n';
}
```

### 示例 24.4. 为 `boost::variant` 使用访问者（visitor）

```cpp
#include <boost/variant.hpp>
#include <string>
#include <iostream>

struct output : public boost::static_visitor<>
{
  void operator()(double d) const { std::cout << d << '\n'; }
  void operator()(char c) const { std::cout << c << '\n'; }
  void operator()(std::string s) const { std::cout << s << '\n'; }
};

int main()
{
  boost::variant<double, char, std::string> v;
  v = 3.14;
  boost::apply_visitor(output{}, v);
  v = 'A';
  boost::apply_visitor(output{}, v);
  v = "Boost";
  boost::apply_visitor(output{}, v);
}
```

为了类型安全的访问，Boost.Variant 提供了一个名为 `boost::apply_visitor()` 的函数。

作为其第一个参数，`boost::apply_visitor()` 期望一个派自 `boost::static_visitor` 的类的对象。该类必须为 `boost::variant` 使用的每个类型重载 `operator()`。

### 示例 24.5. 为 `boost::variant` 使用函数模板

```cpp
#include <boost/variant.hpp>
#include <string>
#include <iostream>

struct output : public boost::static_visitor<>
{
  template <typename T>
  void operator()(T t) const { std::cout << t << '\n'; }
};

int main()
{
  boost::variant<double, char, std::string> v;
  v = 3.14;
  boost::apply_visitor(output{}, v);
  v = 'A';
  boost::apply_visitor(output{}, v);
  v = "Boost";
  boost::apply_visitor(output{}, v);
}
```

如果重载是等价的，可以通过模板来简化代码（参见 示例 24.5, “使用函数模板使用 `boost::variant`”）。

# 25. Boost.PropertyTree

通过 `boost::property_tree::ptree` 类，[Boost.PropertyTree](http://www.boost.org/libs/property_tree) 提供了一种树结构来存储键值对。树结构意味着存在一个树干，带有许多树枝。文件系统是树结构的一个很好的例子。文件系统有根目录，子目录本身也可以包含子目录，以此类推。

要使用 `boost::property_tree::ptree`，请包含头文件 `boost/property_tree/ptree.hpp`。这是一个主头文件，因此 Boost.PropertyTree 不需要其他头文件。

### 示例 25.1. 访问 `boost::property_tree::ptree` 中的数据

```cpp
#include <boost/property_tree/ptree.hpp>
#include <iostream>

using boost::property_tree::ptree;

int main()
{
  ptree pt;
  pt.put("C:.Windows.System", "20 files");

  ptree &c = pt.get_child("C:");
  ptree &windows = c.get_child("Windows");
  ptree &system = windows.get_child("System");
  std::cout << system.get_value<std::string>() << '\n';
}
```

示例 25.1, “在 `boost::property_tree::ptree` 中访问数据” 使用 `boost::property_tree::ptree` 来存储目录的路径。这是通过调用 `put()` 实现的。该成员函数期望两个参数，因为 `boost::property_tree::ptree` 是一个保存键值对的树形结构。树不仅仅由分支和叶子组成，每个分支和叶子都必须分配一个值。在示例 25.1, “在 `boost::property_tree::ptree` 中访问数据” 中，该值为“20 files”。

传递给 `put()` 的第一个参数更有趣。它是一个目录路径。然而，它没有使用反斜杠（Windows 上常用的路径分隔符），而是使用了点。

你需要使用点，因为点是 Boost.PropertyTree 期望用于键的分隔符。参数“C:.Windows.System”告诉 `pt` 创建一个名为 `C:` 的分支，其中包含一个名为 `Windows` 的分支，`Windows` 下还有一个名为 `System` 的分支。点创建了分支的嵌套结构。如果将“C:\Windows\System”作为参数传递，`pt` 将只有一个名为 `C:\Windows\System` 的分支。

调用 `put()` 之后，访问 `pt` 以读取存储的值“20 files”并将其写入标准输出。这是通过在分支与分支之间（或目录与目录之间）跳转完成的。

要访问子分支，可以调用 `get_child()`，它返回对调用 `get_child()` 的对象的相同类型的引用。在示例 25.1, “在 `boost::property_tree::ptree` 中访问数据” 中，这是对 `boost::property_tree::ptree` 的引用。因为每个分支都可以有子分支，而且高低层分支之间没有结构上的差异，所以使用了相同的类型。



第三次调用`get_child()`获取代表 System 目录的`boost::property_tree::ptree`。调用`get_value()`来读取在示例开始通过`put()`存储的值。

请注意，`get_value()`是一个函数模板。你将返回值的类型作为模板参数传递。这样`get_value()`就可以进行自动类型转换。

## 示例 25.2. 在`basic_ptree<std::string, int>`中访问数据

```cpp
#include <boost/property_tree/ptree.hpp>
#include <utility>
#include <iostream>

int main()
{
  typedef boost::property_tree::basic_ptree<std::string, int> ptree;
  ptree pt;
  pt.put(ptree::path_type{"C:\\Windows\\System", '\\'}, 20);
  pt.put(ptree::path_type{"C:\\Windows\\Cursors", '\\'}, 50);

  ptree &windows = pt.get_child(ptree::path_type{"C:\\Windows", '\\'});
  int files = 0;
  for (const std::pair<std::string, ptree> &p : windows)
    files += p.second.get_value<int>();
  std::cout << files << '\n';
}
```

与示例 25.1，“在`boost::property_tree::ptree`中访问数据”相比，示例 25.2，“在`basic_ptree<std::string, int>`中访问数据”中有两个变化。这些变化是为了更方便地存储目录路径和目录中的文件数量。首先，路径在传递给`put()`时使用反斜杠作为分隔符。其次，文件数量被存储为`int`。

默认情况下，Boost.PropertyTree 使用点作为键的分隔符。如果你需要使用另一个字符（如反斜杠）作为分隔符，则不要将键作为字符串传递给`put()`。相反，将其封装在`boost::property_tree::ptree::path_type`类型的对象中。该类的构造函数依赖于`boost::property_tree::ptree`，将键作为第一个参数，将分隔符作为第二个参数。这样你就可以使用像`C:\Windows\System`这样的路径，如示例 25.2，“在`basic_ptree<std::string, int>`中访问数据”所示。

```cpp
#include <boost/property_tree/ptree.hpp>
#include <boost/optional.hpp>
#include <iostream>
#include <cstdlib>

struct string_to_int_translator
{
  typedef std::string internal_type;
  typedef int external_type;

  boost::optional<int> get_value(const std::string &s)
  {
    char *c;
    long l = std::strtol(s.c_str(), &c, 10);
    return boost::make_optional(c != s.c_str(), static_cast<int>(l));
  }
};

int main()
{
  typedef boost::property_tree::iptree ptree;
  ptree pt;
  pt.put(ptree::path_type{"C:\\Windows\\System", '\\'}, "20 files");
  pt.put(ptree::path_type{"C:\\Windows\\Cursors", '\\'}, "50 files");

  string_to_int_translator tr;
  int files =
    pt.get<int>(ptree::path_type{"c:\\windows\\system", '\\'}, tr) +
    pt.get<int>(ptree::path_type{"c:\\windows\\cursors", '\\'}, tr);
  std::cout << files << '\n';
}
```

与示例 25.1，“访问`boost::property_tree::ptree`中的数据”不同，`get_child()`不需要多次调用来访问子分支。就像`put()`可以直接在子分支中存储值一样，可以使用`get()`从子分支读取值。键的定义方式相同——例如使用`boost::property_tree::iptree::path_type`。

与`get_value()`类似，`get()`是一个函数模板。你必须将返回值的类型作为模板参数传递。Boost.PropertyTree 会执行自动类型转换。

为了转换类型，Boost.PropertyTree 使用翻译器（translators）。该库提供了一些基于流（streams）的内置翻译器，可以自动转换类型。

示例 25.3，“使用翻译器访问数据”定义了翻译器`string_to_int_translator`，它将`std::string`类型的值转换为`int`。该翻译器被作为额外参数传递给`get()`。由于翻译器仅用于读取，因此它只定义了一个成员函数`get_value()`。如果你也想在写入时使用该翻译器，则需要定义一个成员函数`put_value()`，然后将翻译器作为额外参数传递给`put()`。

`get_value()`返回在`pt`中使用的类型的值。然而，由于类型转换并不总是成功，因此使用了`boost::optional`。如果示例 25.3，“使用翻译器访问数据”中存储的值无法通过`std::strtol()`转换为`int`，则将返回一个`boost::optional`类型的空对象。

请注意，翻译器还必须定义两个类型`internal_type`和`external_type`。如果你在存储数据时需要转换类型，请类似于`get_value()`定义`put_value()`。

如果你修改了示例 25.3，“使用翻译器访问数据”以存储值“20”而不是“20 files”，则可以在不传递翻译器的情况下调用`get_value()`。Boost.PropertyTree 提供的翻译器可以将`std::string`转换为`int`。然而，只有当整个字符串都可以转换时，类型转换才会成功。字符串不能包含任何字母。只要字符串以数字开头，`std::strtol()`就能进行类型转换，因此在示例 25.3 中使用了更宽松的翻译器`string_to_int_translator`。

## 示例 25.4. `boost::property_tree::ptree`的各种成员函数

```cpp
#include <boost/property_tree/ptree.hpp>
#include <utility>
#include <iostream>

using boost::property_tree::ptree;

int main()
{
  ptree pt;
  pt.put("C:.Windows.System", "20 files");

  boost::optional<std::string> c = pt.get_optional<std::string>("C:");
  std::cout << std::boolalpha << c.is_initialized() << '\n';

  pt.put_child("D:.Program Files", ptree{"50 files"});
  pt.add_child("D:.Program Files", ptree{"60 files"});

  ptree d = pt.get_child("D:");
  for (const std::pair<std::string, ptree> &p : d)
    std::cout << p.second.get<std::string>() << '\n';

  boost::optional<ptree> e = pt.get_optional("E:");
  std::cout << e.is_initialized() << '\n';
}
```

除了`boost::property_tree::json_parser::write_json()`和`boost::property_tree::json_parser::read_json()`函数外，Boost.PropertyTree 还提供了其他数据格式的函数。你可以使用来自`boost/property_tree/ini_parser.hpp`的`boost::property_tree::ini_parser::write_ini()`和`boost::property_tree::ini_parser::read_ini()`来支持 INI 文件。通过来自`boost/property_tree/xml_parser.hpp`的`boost::property_tree::xml_parser::write_xml()`和`boost::property_tree::xml_parser::read_xml()`，可以在 XML 格式加载并存储数据。通过来自`boost/property_tree/info_parser.hpp`的`boost::property_tree::info_parser::write_info()`和`boost::property_tree::info_parser::read_info()`，你可以访问另一种专门为序列化 Boost.PropertyTree 优化的格式。

所有支持的格式都不保证`boost::property_tree::ptree`在保存并重新加载后外观保持一致。例如，JSON 格式可能会丢失类型信息，因为`boost::property_tree::ptree`无法区分`true`和“true”。类型始终是相同的。即使各种函数可以方便地保存和加载`boost::property_tree::ptree`，也别忘记 Boost.PropertyTree 并不完全支持这些格式。该库的重点是`boost::property_tree::ptree`结构，而不是支持各种数据格式。

# 26. Boost.DynamicBitset

[Boost.DynamicBitset](http://www.boost.org/libs/dynamic_bitset) 库提供了`boost::dynamic_bitset`类，其用法类似于`std::bitset`。区别在于`std::bitset`的位数必须在编译时指定，而`boost::dynamic_bitset`的位数是在运行时指定的。

若要使用`boost::dynamic_bitset`，请包含头文件`boost/dynamic_bitset.hpp`。

## 示例 26.1. 使用`boost::dynamic_bitset`

```cpp
#include <boost/dynamic_bitset.hpp>
#include <iostream>

int main()
{
  boost::dynamic_bitset<> db{3, 4};

  db.push_back(true);

  std::cout.setf(std::ios::boolalpha);
  std::cout << db.size() << '\n';
  std::cout << db.count() << '\n';
  std::cout << db.any() << '\n';
  std::cout << db.none() << '\n';

  std::cout << db[0].flip() << '\n';
  std::cout << ~db[3] << '\n';
  std::cout << db << '\n';
}
```

`boost::dynamic_bitset`是一个模板，实例化时不需要任何模板参数；在这种情况下会使用默认类型。更重要的是传递给构造函数的参数。在示例 26.1，“使用`boost::dynamic_bitset`”中，构造函数创建了一个具有 3 位的`db`。第二个参数初始化位；在这种情况下，4 初始化了最高位——左侧的位。

`boost::dynamic_bitset`对象内部的位数可以随时更改。成员函数`push_back()`添加另一个位，该位将成为最高位。在示例 26.1，“使用`boost::dynamic_bitset`”中调用`push_back()`会导致`db`包含 4 位，其中最高位被设置。因此，`db`存储数字 1。

你可以通过调用成员函数`resize()`来减少位数。根据传递给`resize()`的参数，位将被添加或删除。

`boost::dynamic_bitset`提供了查询数据和访问单个位的成员函数。成员函数`size()`和`count()`分别返回位数和当前设置为 1 的个数。`any()`在至少有一个位被设置时返回`true`，而`none()`在没有位被设置时返回`true`。

若要访问单个位，请使用数组语法。它将返回一个对内部类的引用，该引用表示该位并提供了操作它的成员函数。例如，成员函数`flip()`可以翻转该位。同样可以使用位运算符，如`operator~`。总的来说，`boost::dynamic_bitset`类提供了与`std::bitset`相同的位功能。

像`std::bitset`一样，`boost::dynamic_bitset`不支持迭代器。

# 27. Boost.Tribool

[Boost.Tribool](http://boost.org/libs/logic) 库提供了`boost::logic::tribool`类，它类似于`bool`。然而，`bool`可以区分两种状态，而`boost::logic::tribool`处理三种状态。

若要使用`boost::logic::tribool`，请包含头文件`boost/logic/tribool.hpp`。

类型为`boost::logic::tribool`的变量可以设置为`true`、`false`或`indeterminate`（不确定）。

`boost::logic::tribool`类型的变量可以设置为`true`、`false`或`indeterminate`。默认构造函数将变量设置为`false`。在示例 27.1，“三状态逻辑`boost::logic::tribool`”中，这为什么是`false`。

## 示例 27.1. 三状态`boost::logic::tribool`

```cpp
#include <boost/logic/tribool.hpp>
#include <iostream>

using namespace boost::logic;

int main()
{
  boost::logic::tribool b;
  std::cout << boolalpha << b << '\n';

  b = true;
  b = false;
  b = indeterminate;
  if (b)
    ;
  else if (!b)
    ;
  else
    std::cout << "indeterminate\n";
}
```

示例 27.1，“三状态`boost::logic::tribool`”说明了如何正确评估`b`。你必须显式地检查`true`和`false`。如果变量设置为`indeterminate`，如示例所示，`else`块将执行。

Boost.Tribool 还提供了函数`boost::logic::indeterminate()`。如果你传递一个设置为`indeterminate`的`boost::logic::tribool`类型变量，该函数将返回`true`。如果变量设置为`true`或`false`，它将返回`false`。

## 示例 27.2. `boost::logic::tribool`的逻辑运算符



```cpp
#include <boost/logic/tribool.hpp>
#include <boost/logic/tribool_io.hpp>
#include <iostream>

using namespace boost::logic;

int main()
{
  std::cout.setf(std::ios::boolalpha);

  boost::logic::tribool b1 = true;
  std::cout << (b1 || indeterminate) << '\n';
  std::cout << (b1 && indeterminate) << '\n';

  boost::logic::tribool b2 = false;
  std::cout << (b2 || indeterminate) << '\n';
  std::cout << (b2 && indeterminate) << '\n';

  boost::logic::tribool b3 = indeterminate;
  std::cout << (b3 || b3) << '\n';
  std::cout << (b3 && b3) << '\n';
}
```

你可以对`boost::logic::tribool`变量使用逻辑运算符，就像对`bool`变量一样。实际上，这是处理`boost::logic::tribool`变量的唯一方法，因为该类没有提供任何成员函数。

示例 27.2, "`boost::logic::tribool`的逻辑运算符" 对于`b1 || indeterminate`返回`true`，对于`b2 && indeterminate`返回`false`，在所有其他情况下返回`indeterminate`。

# 28. Boost.CompressedPair

[Boost.CompressedPair](http://www.boost.org/libs/utility/compressed_pair.htm)提供了`boost::compressed_pair`，这是一个行为类似于`std::pair`的类。然而，如果一个或两个模板参数为空类，`boost::compressed_pair`消耗的内存更少。`boost::compressed_pair`使用了一种名为空基类优化的技术。

要使用`boost::compressed_pair`，请包含头文件`boost/compressed_pair.hpp`。

### 示例 28.1. 使用`boost::compressed_pair`减少内存需求

```cpp
#include <boost/compressed_pair.hpp>
#include <utility>
#include <iostream>

struct empty {};

int main()
{
  std::pair<int, empty> p;
  std::cout << sizeof(p) << '\n';

  boost::compressed_pair<int, empty> cp;
  std::cout << sizeof(cp) << '\n';
}
```

示例 28.1, "使用`boost::compressed_pair`减少内存需求" 通过对`cp`使用`boost::compressed_pair`并对`p`使用`std::pair`说明了这一点。当使用 Visual C++ 2013 编译并在 64 位 Windows 7 系统上运行时，示例的`sizeof(cp)`返回 4，`sizeof(p)`返回 8。

请注意，`boost::compressed_pair`与`std::pair`还有另一个区别：`boost::compressed_pair`中存储的值通过成员函数`first()`和`second()`访问。而`std::pair`使用两个同名的成员变量。

# 第 V 部分 算法

以下库提供了对标准库算法的补充算法。

* `Boost.Algorithm`收集并提供了实用的算法。
* `Boost.Range`也提供了算法，但更重要的是，它定义了一个名为`range`的新概念，这应该让使用算法变得更容易。
* `Boost.Graph`专门用于图，并提供了如寻找两点之间最短路径等算法。

书中包含算法的几个库将在书的其他部分介绍。例如，你将在`Boost.StringAlgorithms`库中找到字符串的算法，该库在第 II 部分, "字符串处理" 中介绍。

# 29. Boost.Algorithm

[Boost.Algorithm](http://www.boost.org/libs/algorithm)提供了对标准库算法的补充算法。与`Boost.Range`不同，`Boost.Algorithm`没有引入新概念。`Boost.Algorithm`定义的算法与标准库的算法相似。

请注意，其他 Boost 库也提供了许多算法。例如，你将在`Boost.StringAlgorithms`中找到处理字符串的算法。`Boost.Algorithm`提供的算法并不限于特定类（如`std::string`）。与标准库的算法一样，它们可以用于任何容器。

### 示例 29.1. 使用`boost::algorithm::one_of_equal()`测试恰好仅有一个值

```cpp
#include <boost/algorithm/cxx11/one_of.hpp>
#include <array>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::array<int, 6> a{{0, 5, 2, 1, 4, 3}};
  auto predicate = [](int i){ return i == 4; };
  std::cout.setf(std::ios::boolalpha);
  std::cout << one_of(a.begin(), a.end(), predicate) << '\n';
  std::cout << one_of_equal(a.begin(), a.end(), 4) << '\n';
}
```

`boost::algorithm::one_of()`测试某个条件是否恰好满足一次。要测试的条件以谓词的形式传递。在示例 29.1, "使用`boost::algorithm::one_of_equal()`测试恰好仅有一个值" 中，对`boost::algorithm::one_of()`的调用返回`true`，因为数字 4 在`a`中恰好存储了一次。

要测试容器中的元素是否相等，请调用`boost::algorithm::one_of_equal()`。你不需要传递谓词。相反，你传递一个值给`boost::algorithm::one_of_equal()`进行比较。在示例 29.1, "使用`boost::algorithm::one_of_equal()`测试恰好仅有一个值" 中，对`boost::algorithm::one_of_equal()`的调用也返回`true`。

`boost::algorithm::one_of()`补充了 C++11 添加到标准库的`std::all_of()`、`std::any_of()`和`std::none_of()`。然而，`Boost.Algorithm`提供了`boost::all_of()`、`boost::any_of()`和`boost::none_of()`。与标准库算法一样，它们可以用于任何容器。

### 示例 29.2. C++11 算法的变体

```cpp
#include <boost/algorithm/cxx11/iota.hpp>
#include <boost/algorithm/cxx11/is_sorted.hpp>
#include <boost/algorithm/cxx11/copy_if.hpp>
#include <vector>
#include <iterator>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::vector<int> v;
  iota_n(std::back_inserter(v), 10, 5);
  std::cout.setf(std::ios::boolalpha);
  std::cout << is_increasing(v) << '\n';
  std::ostream_iterator<int> out{std::cout, ","};
  copy_until(v, out, [](int i){ return i > 12; });
}
```

`Boost.Algorithm`在`iota_hpp`中提供了 C++11 算法`iota()`。该函数生成顺序递增的数字。它期望两个用于容器边界的迭代器。随后容器中的元素将被重写为顺序递增的数字。

与其使用`boost::iota()`，示例 29.2, "C++11 算法的变体" 使用`iota_n()`。该函数期望一个用于写入数字的迭代器。生成的数字数量作为第三个参数传递给`iota_n()`。

`Boost.Algorithm`还提供了以下内容：`one_equal()`、`any_equal()`和`none_equal()`。这些内容位于相应的头文件中。

示例 29.2, "C++11 算法的变体" 显示`boost::algorithm::is_increasing()`的结果为`true`，且`boost::algorithm::copy_until()`将数字`10`、`11`和`12`写入标准输出。

### 示例 29.3. 来自 Boost.Algorithm 的 C++14 算法

```cpp
#include <boost/algorithm/cxx14/equal.hpp>
#include <boost/algorithm/cxx14/mismatch.hpp>
#include <vector>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::vector<int> v{1, 2};
  std::vector<int> w{1, 2, 3};
  std::cout.setf(std::ios::boolalpha);
  std::cout << equal(v.begin(), v.end(), w.begin(), w.end()) << '\n';
  auto pair = mismatch(v.begin(), v.end(), w.begin(), w.end());
  if (pair.first != v.end())
    std::cout << *pair.first << '\n';
  if (pair.second != w.end())
    std::cout << *pair.second << '\n';
}
```

除了 C++11 标准库中的算法外，Boost.Algorithm 还定义了极有可能添加到 C++14 标准库中的算法。示例 29.3, "来自 Boost.Algorithm 的 C++14 算法" 使用了其中两个函数的变体：`boost::algorithm::equal()`和`boost::algorithm::mismatch()`。与自 C++98 以来就一直是标准库的同名函数不同，这些新函数接收的是四个迭代器而不是三个。示例 29.3, "来自 Boost.Algorithm 的 C++14 算法" 中的算法并不期望第二个序列包含与第一个序列一样多的元素。

虽然`boost::algorithm::equal()`返回一个`bool`，但`boost::algorithm::mismatch()`返回一个包含两个迭代器的`std::pair`。`first`和`second`分别指向第一个和第二个序列中第一个不匹配的元素。这些迭代器也可能指向序列的末尾。

示例 29.3, "来自 Boost.Algorithm 的 C++14 算法" 向标准输出写入了`false`和`3`。`false`是`boost::algorithm::equal()`的返回值，`3`是`w`中的第三个元素。由于`v`和`w`的前两个元素相等，`boost::algorithm::mismatch()`返回的`first`是一个指向`v`末尾的迭代器，而`second`是一个指向`w`第三个元素的迭代器。由于`first`指向`v`的末尾，该迭代器没有被解引用，因此没有输出。

### 示例 29.4. 使用`boost::algorithm::hex()`和`boost::algorithm::unhex()`

```cpp
#include <boost/algorithm/hex.hpp>
#include <vector>
#include <string>
#include <iterator>
#include <iostream>

using namespace boost::algorithm;

int main()
{
  std::vector<char> v{'C', '+', '+'};
  hex(v, std::ostream_iterator<char>{std::cout, ""});
  std::cout << '\n';

  std::string s = "C++";
  std::cout << hex(s) << '\n';

  std::vector<char> w{'4', '3', '2', 'b', '2', 'b'};
  unhex(w, std::ostream_iterator<char>{std::cout, ""});
  std::cout << '\n';

  std::string t = "432b2b";
  std::cout << unhex(t) << '\n';
}
```

示例 29.4, "使用`boost::algorithm::hex()`和`boost::algorithm::unhex()`" 使用了`boost::algorithm::hex()`和`boost::algorithm::unhex()`。这两个函数`boost::algorithm::hex()`和`boost::algorithm::unhex()`设计用于将字符串转换为十六进制。

`boost::random_shuffle()`的工作类似于`std::random_shuffle()`，它会随机改变范围内元素的顺序。示例 30.2, "与标准库算法相关的范围算法" 使用默认随机数生成器使用了`boost::random_shuffle()`。然而，你可以将一个随机数生成器作为第二个参数传递。该随机数生成器可以来自 C++11 的头文件`random`，也可以来自 Boost.Random。

`boost::copy()`的工作类似于`std::copy()`。`boost::max_element()`和`boost::accumulate()`的工作方式与标准库中同名的算法一致。与`std::max_element()`一样，`boost::max_element()`返回指向数值最大元素的迭代器。

使用`boost::accumulate()`必须包含头文件`boost/range/numeric.hpp`。正如`std::accumulate()`定义在`numeric`中一样，`boost::accumulate()`定义在`boost/range/numeric.hpp`中，而不是`boost/range/algorithm.hpp`。

Boost.Range 还提供了一些标准库中没有对应项的算法。

### 示例 30.3. 标准库中没有对应的范围算法

```cpp
#include <boost/range/algorithm_ext.hpp>
#include <array>
#include <deque>
#include <iterator>
#include <iostream>

int main()
{
  std::array<int, 6> a{{0, 1, 2, 3, 4, 5}};
  std::cout << std::boolalpha << boost::is_sorted(a) << '\n';
  std::deque<int> d;
  boost::push_back(d, a);
  boost::remove_erase(d, 2);
  boost::copy_n(d, 3, std::ostream_iterator<int>{std::cout, ","});
}
```

示例 30.3, "标准库中没有对应的范围算法" 中使用的算法需要头文件`boost/range/algorithm_ext.hpp`。该头文件提供了对标准库中没有对应项的算法的访问。

`boost::is_sorted()`测试范围内的元素是否排序。在示例 30.3, "标准库中没有对应的范围算法" 中，`boost::is_sorted()`返回`true`因为`a`是有序的。可以将一个谓词作为第二个参数传递给`boost::is_sorted()`，例如检查范围是否是按降序排序的。



`boost::push_back()` 期望的第一个参数是一个容器，第二个参数是一个范围。该容器必须定义了成员函数 `push_back()`。范围中的所有元素将按照范围指定的顺序通过该成员函数添加到容器中。由于 `d` 初始为空，在调用 `boost::push_back()` 之后，它将包含与 `a` 相同的数字。

`boost::remove_erase()` 从 `d` 中删除数字 2。该算法结合了对函数 `std::remove()` 的调用以及相应容器成员函数 `erase()` 的调用。得益于 `boost::remove_erase()`，你不需要先找到所需元素的迭代器，然后在第二步将其传递给 `erase()`。

`boost::copy_n()` 与 `std::copy()` 类似，但它只复制作为第二个参数传递的数量的元素。示例 30.3, “与标准库算法相关的范围算法” 仅将 `d` 中的前三个数字写入标准输出。因为在上一行中从 `d` 中删除了 2，所以显示了 `0,1,3,`。

## 适配器 (Adaptors)

标准库提供了几种可以传递谓词的算法。例如，传递给 `std::count_if()` 的谓词决定了哪些元素被计数。Boost.Range 提供了类似的函数 `boost::count_if()`。然而，提供该算法只是为了完整性，因为 Boost.Range 提供了适配器，使得带有谓词的算法变得多余。

你可以将适配器理解为过滤器。它们根据另一个范围返回一个新的范围。由于范围仅仅是一对迭代器，因此适配器返回一个新的点对。这对仍然可以用于迭代原始范围，但例如可能会跳过某些元素。如果配合这种适配器使用 `boost::count()`，则不再需要 `boost::count_if()` 了。算法与适配器的区别在于，算法在范围上进行迭代并处理数据，而适配器返回一个新范围——即新的迭代器——该范围决定了迭代返回哪些元素。然而，适配器本身并不执行迭代。必须通过调用算法。

### 示例 30.4. 使用 `boost::adaptors::filter()` 过滤范围

```cpp
#include <boost/range/algorithm.hpp>
#include <boost/range/adaptors.hpp>
#include <array>
#include <iterator>
#include <iostream>

int main()
{
  std::array<int, 6> a{{0, 5, 2, 1, 3, 4}};
  boost::copy(boost::adaptors::filter(a, [](int i){ return i > 2; }),
    std::ostream_iterator<int>{std::cout, ","});
}
```

示例 30.4, “与标准库算法相关的范围算法” 使用了一个可以过滤范围的适配器。正如你所见，适配器只是一个函数。`boost::filter()` 期望的第一个参数是一个待过滤的范围，第二个参数是一个谓词。示例 30.4, “与标准库算法相关的范围算法” 过滤除了范围中不大于 2 的数字。

`boost::filter()` 不改变范围 `a`，它返回一个新的范围。由于范围与迭代器对并不相似，新范围也指向 `a`。然而，新范围的迭代器跳过了所有小于或等于 2 的数字。示例 30.4, “与标准库算法相关的范围算法” 向标准输出写入了 `5,3,4`。

示例 30.5, “与标准库算法相关的范围算法” 使用两个适配器 `boost::adaptors::keys()` 和 `boost::adaptors::values()` 来访问 `std::map` 类型容器的键和值。它还展示了适配器如何嵌套。因为 `m` 存储的是值的指针而不是值本身，所以 `boost::adaptors::values()` 返回的范围被传递给了 `boost::adaptors::indirect()`。当范围由指针组成可以使用该适配器，但迭代应该返回指针所指向的值。这就是为什么示例 30.5, “与标准库算法相关的范围算法” 向标准输出写入了 `a,b,c,0,1,2,`。

### 示例 30.5. 使用 `keys()`, `values()` 和 `indirect()`

```cpp
#include <boost/range/algorithm.hpp>
#include <boost/range/adaptors.hpp>
#include <array>
#include <map>
#include <string>
#include <utility>
#include <iterator>
#include <iostream>

int main()
{
  std::array<int, 3> a{{0, 1, 2}};
  std::map<std::string, int*> m;
  m.insert(std::make_pair("a", &a[0]));
  m.insert(std::make_pair("b", &a[1]));
  m.insert(std::make_pair("c", &a[2]));

  boost::copy(boost::adaptors::keys(m),
    std::ostream_iterator<std::string>{std::cout, ","});
  boost::copy(boost::adaptors::indirect(boost::adaptors::values(m)),
    std::ostream_iterator<int>{std::cout, ","});
}
```

示例 30.6, “boost::adaptors::tokenize() – 字符串适配器” – an adaptor for strings") 介绍了一个用于字符串的适配器。你可以使用 `boost::adaptors::tokenize()` 配合正则表达式从字符串中获取一个范围（range）。你将一个字符串和一个类型为 `boost::regex` 的正则表达式传递给 `boost::adaptors::tokenize()`。此外，你还需要传递一个表示正则表达式中某个分组的数字和一个标志位。如果没有使用分组，可以传递 `0`。标志位 `boost::regex_constants::match_default` 选择正则表达式的默认设置。你也可以传递其他标志位。例如，如果你想让正则表达式按照 Perl 编程语言的规则进行应用，可以使用 `boost::regex_constants::match_perl`。

示例 30.6. `boost::adaptors::tokenize()` – 字符串适配器

```
#include <boost/range/algorithm.hpp>
#include <boost/range/adaptors.hpp>
#include <boost/regex.hpp>
#include <string>
#include <iostream>

int main()
{
  std::string s = "The Boost C++ Libraries";
  boost::regex expr{"[\\w+]+"};
  boost::copy(boost::adaptors::tokenize(s, expr, 0,
    boost::regex_constants::match_default),
    std::ostream_iterator<std::string>{std::cout, ","});
}
```

## 辅助类与函数

Boost.Range 提供的算法和适配器是基于模板的。你不需要将容器转换为范围才能传递给算法或适配器。然而，Boost.Range 定义了几个范围类，其中 `boost::iterator_range` 是最重要的。之所以需要 `boost::iterator_range` 是因为适配器和少数算法返回的范围必须具有类型。此外，还存在一些辅助函数，它们可以创建迭代器包含迭代所需所有数据的范围。这些范围的迭代器并不引用容器或其他数据结构。这里也使用了像 `boost::iterator_range` 这样的类。

示例 30.7. 使用 `boost::irange()` 为整数创建范围

```
#include <boost/range/algorithm.hpp>
#include <boost/range/irange.hpp>
#include <iostream>

int main()
{
  boost::integer_range<int> ir = boost::irange(0, 3);
  boost::copy(ir, std::ostream_iterator<int>{std::cout, ","});
}
```

示例 30.7, “使用 `boost::irange()` 为整数创建范围”}") 使用了函数 `boost::irange()`。该函数创建了一个整数范围，而无需使用容器或其他数据结构。你只需要向 `boost::irange()` 传递一个下界和一个上限，其中上限是开区间。

`boost::irange()` 返回一个类型为 `boost::integer_range` 的范围。该类派自 `boost::iterator_range`。`boost::iterator_range` 是一个模板，它期望迭代器类型作为其唯一的模板参数。`boost::irange()` 使用的迭代器与该函数紧密耦合，并且是一个实现细节。因此，迭代器类型是不可知的，不能作为模板参数传递给 `boost::iterator_range`。然而，`boost::integer_range` 只期望一种整数类型，这使得它比传递迭代器类型时更容易使用。

示例 30.7, “使用 `boost::irange()` 为整数创建范围”") 向标准输出写入了 `0,1,2`。

示例 30.8, “使用 `boost::istream_range()` 为输入流创建范围”") 引入了函数 `boost::istream_range()`，它为输入流创建一个范围。该函数返回一个 `boost::iterator_range` 类型的范围。这意味着必须作为模板参数传递迭代器类型。

当你开始 示例 30.8, “使用 `boost::istream_range()` 为输入流创建范围”")，输入一个数字并按 `Enter`，该数字将打印在下一行。如果你输入另一个数字并按 `Enter`，该数字会被打印。`boost::istream_range()` 返回的范围使得 `boost::copy()` 可以遍历所有输入的数字并将它们写入 `std::cout`。

你可以随时通过输入 `Ctrl`+`C` 终止程序。

示例 30.8. 使用 `boost::istream_range()` 为输入流创建范围

```
#include <boost/range/algorithm.hpp>
#include <boost/range/istream_range.hpp>
#include <iterator>
#include <iostream>

int main()
{
  boost::iterator_range<int> ir = boost::istream_range<int>(std::cin);
  boost::copy(ir, std::ostream_iterator<int>{std::cout, "\n"});
}
```

除了 `boost::iterator_range`，Boost.Range 还提供了 `boost::sub_range` 类，它派自 `boost::iterator_range`。`boost::sub_range` 是像 `boost::iterator_range` 一样的模板。然而，`boost::sub_range` 期望范围的类型而非迭代器类型。这可以简化用法。

示例 30.9. 使用 `boost::sub_range()` 更方便地创建范围

```
#include <boost/range/algorithm.hpp>
#include <boost/range/iterator_range.hpp>
#include <boost/range/sub_range.hpp>
#include <array>
#include <iterator>
#include <iostream>

int main()
{
  std::array<int, 6> a{0, 1, 2, 3, 4, 5};
  boost::iterator_range<std::array<int, 6>> r1 =
    boost::random_shuffle(a);
  boost::sub_range<std::array<int, 6>> r2 =
    boost::random_shuffle(r1);
  boost::copy(r2, std::ostream_iterator<int>{std::cout, ","});
}
```

Boost.Range 中的少数算法返回一个范围——例如 `boost::random_shuffle()`。该算法通过引用修改传递给它的范围并返回该范围。在 示例 30.9, “使用 `boost::sub_range()` 更方便地创建范围”") 中，`boost::random_shuffle()` 被调用两次，所以数组 `a` 被随机打乱了两次。

对于第一个返回值，示例使用了 `boost::iterator_range`；对于第二个返回值，它使用了 `boost::sub_range`。这两个类的用法区别仅在于模板参数。不仅 `boost::sub_range` 实例化更方便，它还提供了 `const_iterator` 类型定义。

# 31. Boost.Graph

[Boost.Graph](http://www.boost.org/libs/graph) 提供了处理图的工具。图是点之间具有任意数量线的二维点云。地铁地图是一个很好的例子。地铁站是点，地铁线连接它们。

## 顶点与边

图由顶点和边组成。为了创建一个图，你必须定义一组点以及它们之间的任意线。示例 31.1, “具有四个顶点的 `boost::adjacency_list` 类型图” 包含第一个由四个点且没有线的简单图。

Boost.Graph 提供了三种容器来定义图。最重要的容器是 `boost::adjacency_list`，它几乎用于本章中所有的示例。要使用此类类，请包含头文件 `boost/graph/adjacency_list.hpp`。如果你想使用其他容器，必须包含另一个头文件。没有一个主头文件可以访问 Boost.Graph 中的所有类和函数。

### 示例 31.1. 四个顶点的 `boost::adjacency_list` 图

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <iostream>

int main()
{
  boost::adjacency_list<> g;

  boost::adjacency_list<>::vertex_descriptor v1 = boost::add_vertex(g);
  boost::adjacency_list<>::vertex_descriptor v2 = boost::add_vertex(g);
  boost::adjacency_list<>::vertex_descriptor v3 = boost::add_vertex(g);
  boost::adjacency_list<>::vertex_descriptor v4 = boost::add_vertex(g);

  std::cout << v1 << ", " << v2 << ", " << v3 << ", " << v4 << '\n';
}
```

`boost::adjacency_list` 是一个模板，在示例 31.1, “四个顶点的 `boost::adjacency_list` 图” 中使用默认参数实例化。稍后你会看到可以传递哪些参数。该类定义在 `boost` 命名空间中。Boost.Graph 的所有类和函数都在这个命名空间中。

要向图中添加四个点，必须调用四次 `boost::add_vertex()` 函数。

`boost::add_vertex()` 是一个独立函数，而不是 `boost::adjacency_list` 的成员函数。你会发现 Boost.Graph 中有很多独立函数，这些函数本可以实现为成员函数。Boost.Graph 的设计更像是一个泛型库，而不是一个面向对象的库。

`boost::add_vertex()` 向图中添加一个点。在图论中，点被称为顶点（vertex），这解释了该函数的命名。

`boost::add_vertex()` 返回类型为 `boost::adjacency_list::vertex_descriptor` 的对象。该对象代表图中新添加的点。你可以像示例 31.1, “四个顶点的 `boost::adjacency_list` 图”所示所示将对象写入标准输出。该示例显示了 `0, 1, 2, 3`。

示例 31.1, “四个顶点的 `boost::adjacency_list` 图”通过正整数识别点。这些数字是 `boost::adjacency_list` 内部使用的 vector 的索引。`boost::add_vertex()` 返回 0, 1, 2 和 3 并不意外，因为每次调用都会向 vector 中添加另一个点。

`std::vector` 是 `boost::adjacency_list` 默认用于存储点的容器。在这种情况下，`boost::adjacency_list::vertex_descriptor` 是 `std::size_t` 的类型定义。因为可以使用其他容器来存储点，所以 `boost::adjacency_list::vertex_descriptor` 并不总是 `std::size_t`。



### 示例 31.2. 使用 `boost::vertices()` 访问顶点

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <utility>
#include <algorithm>
#include <iterator>
#include <iostream>

int main()
{
  boost::adjacency_list<> g;

  boost::add_vertex(g);
  boost::add_vertex(g);
  boost::add_vertex(g);
  boost::add_vertex(g);

  std::pair<boost::adjacency_list<>::vertex_iterator,
    boost::adjacency_list<>::vertex_iterator> vs = boost::vertices(g);

  std::copy(vs.first, vs.second,
    std::ostream_iterator<boost::adjacency_list<>::vertex_descriptor>{
      std::cout, "\n"});
}
```

要获取图中所有的点，调用`boost::vertices()`。此函数返回两个类型为`boost::adjacency_list::vertex_iterator`的迭代器，分别指向起点和终点。迭代器以`std::pair`的形式返回。示例 31.2, “使用 `boost::vertices()` 访问顶点”") 使用迭代器将所有点写入标准输出。该示例显示了数字 0, 1, 2 和 3，与上一个示例一样。

### 示例 31.3. 使用 `boost::edges()` 访问边

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <utility>
#include <algorithm>
#include <iterator>
#include <iostream>

int main()
{
  typedef boost::adjacency_list<boost::setS, boost::vecS,
    boost::undirectedS> graph;
  graph g;

  boost::adjacency_list<>::vertex_descriptor v1 = boost::add_vertex(g);
  boost::adjacency_list<>::vertex_descriptor v2 = boost::add_vertex(g);
  boost::add_vertex(g);
  boost::add_vertex(g);

  std::pair<graph::edge_descriptor, bool> p =
    boost::add_edge(v1, v2, g);
  std::cout.setf(std::ios::boolalpha);
  std::cout << p.second << '\n';

  p = boost::add_edge(v1, v2, g);
  std::cout << p.second << '\n';

  p = boost::add_edge(v2, v1, g);
  std::cout << p.second << '\n';

  std::pair<graph::edge_iterator,
    graph::edge_iterator> es = boost::edges(g);

  std::copy(es.first, es.second,
    std::ostream_iterator<graph::edge_descriptor>{std::cout, "\n"});
}
```

默认情况下，`boost::adjacency_list`使用`std::vector`来处理点和线。通过在示例 31.4, “带有选择器的 `boost::adjacency_list`”中在第一个模板参数中传递`boost::setS`，`std::set`被选为用于线的容器。由于`std::set`不支持重复项，因此无法多次使用`boost::add_edge()`添加相同的线。因此，该示例仅显示了一次`(0,1)`。

第二个模板参数告诉`boost::adjacency_list`应该使用哪个类来处理点。在示例 31.4, “带有选择器的 `boost::adjacency_list`”中传递了`boost::vecS`。这是第二个模板参数的默认值。设置它的目的是为了你可以传递第三个模板参数。

第三个模板参数决定了线是有向的还是无向的。默认是`boost::directedS`，这意味着所有线都是有向的，并且可以画成箭头。线只能向一个方向跨越。

`boost::undirectedS`使用在示例 31.4, “带有选择器的 `boost::adjacency_list`”中。该选择器使所有线变为无向的，这意味着可以从任何方向跨越线。哪个点是起点，哪个点是终点并不重要。这也是为什么示例 31.4, “带有选择器的 `boost::adjacency_list`”中的图只包含一条线的另一个原因。第三次调用函数`boost::add_edge()`交换了起点和终点，但由于示例中的线是无向的，这条线与之前的相同，因此没有被添加。

Boost.Graph 提供了更多的选择器，包括`boost::listS`、`boost::mapS`和`boost::hash_setS`。可以使用`boost::bidirectionalS`使线变为双向的。该选择器类似于`boost::undirectedS`，但在这种情况下，起点和终点是重要的。如果你在示例 31.4, “带有选择器的 `boost::adjacency_list`”中使用`boost::bidirectionalS`，那么第三次调用`boost::add_edge()`将向图中添加一条线。

### 示例 31.5. 使用 `boost::add_edge()` 自动创建索引

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <tuple>
#include <algorithm>
#include <iterator>
#include <iostream>

int main()
{
  typedef boost::adjacency_list<boost::setS, boost::vecS,
    boost::undirectedS> graph;
  graph g;

  enum { topLeft, topRight, bottomRight, bottomLeft };

  boost::add_edge(topLeft, topRight, g);
  boost::add_edge(topRight, bottomRight, g);
  boost::add_edge(bottomRight, bottomLeft, g);
  boost::add_edge(bottomLeft, topLeft, g);

  graph::edge_iterator it, end;
  std::tie(it, end) = boost::edges(g);
  std::copy(it, end,
    std::ostream_iterator<graph::edge_descriptor>{std::cout, "\n"});
}
```

示例 31.5, “使用 `boost::add_edge()` 自动创建索引”) 定义了一个由四个点组成的图。你可以将该图可视化为包含四个字段的地图，每个字段由一个点表示。点被命名为`topLeft`、`topRight`、`bottomRight`和`bottomLeft`。由于名称是在枚举中分配的，每个名称将有一个作为索引使用的数值值。

可以在不调用`boost::add_vertex()`的情况下定义图。Boost.Graph 会向图中添加缺失的点。在示例 31.5, “使用 `boost::add_edge()` 自动创建索引”)中，`boost::add_edge()`调用不仅定义了线，还添加了点。`std::tie()`用于将`boost::edges()`返回的迭代器存储在`std::pair`中。`std::tie()`从 C++11 起就是标准库的一部分。示例 31.5, “使用 `boost::add_edge()` 自动创建索引”)中的图是一个带有四个字段的地图。要从左上角到右下角，可以跨越右上角的字段或左下角的字段。相反的字段之间没有线。因此，无法直接从左上角到右下角。

### 示例 31.6. `boost::adjacent_vertices()` 和 `boost::out_edges()`

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <tuple>
#include <algorithm>
#include <iterator>
#include <iostream>

int main()
{
  typedef boost::adjacency_list<boost::setS, boost::vecS,
    boost::undirectedS> graph;
  graph g;

  enum { topLeft, topRight, bottomRight, bottomLeft };

  boost::add_edge(topLeft, topRight, g);
  boost::add_edge(topRight, bottomRight, g);
  boost::add_edge(bottomRight, bottomLeft, g);
  boost::add_edge(bottomLeft, topLeft, g);

  graph::adjacency_iterator vit, vend;
  std::tie(vit, vend) = boost::adjacent_vertices(topLeft, g);
  std::copy(vit, vend,
    std::ostream_iterator<graph::vertex_descriptor>{std::cout, "\n"});

  graph::out_edge_iterator eit, eend;
  std::tie(eit, eend) = boost::out_edges(topLeft, g);
  std::for_each(eit, eend,
    &g
      { std::cout << boost::target(it, g) << '\n'; });
}
```

示例 31.6, “`boost::adjacent_vertices()` 和 `boost::out_edges()`” and boost::out_edges()) 介绍了获取点额外信息的函数。`boost::adjacent_vertices()`返回一对迭代器，指向与点连接的点。如果你想访问从点出发的所有出线，则调用`boost::out_edges()`。`boost::in_edges()`访问入线。对于无向线，调用哪一个函数都没有区别。

`boost::target()`返回线的终点。起点通过`boost::source()`返回。

Example 31.6, “`boost::adjacent_vertices()` 和 `boost::out_edges()`” and boost::out_edges()") 向标准输出输出了两次 1 和 3，分别是右上角和左下角字段的索引。调用`boost::adjacent_vertices()`并传入`topLeft`会返回并显示右上角和左下角字段的索引。`topLeft`也被传递给`boost::out_edges()`以获取出边。由于在`std::for_each()`中对每条出边都调用了`boost::target()`，因此右上角和左下角字段的索引显示了两次。

### 示例 31.7. 通过线条初始化 `boost::adjacency_list`

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <array>
#include <utility>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::adjacency_list<boost::setS, boost::vecS,
    boost::undirectedS> graph;
  graph g{edges.begin(), edges.end(), 4};

  std::cout << boost::num_vertices(g) << '\n';
  std::cout << boost::num_edges(g) << '\n';

  g.clear();
}
```

你可以将迭代器传递给`boost::adjacency_list`的构造函数，这些迭代器指向`std::pair<int, int>`类型的对象，代表线条。如果你传递了迭代器，还必须提供第三个参数来确定图中点的总数。图将包含线条所需的点。第三个参数允许你向图中添加未与其他点连接的点。

示例 31.7, “通过线条初始化 `boost::adjacency_list`” 使用了`boost::num_vertices()`和`boost::num_edges()`函数，它们分别返回点的数量和线条的数量。示例显示了两次`4`。

示例 31.7, “通过线条初始化 `boost::adjacency_list`” 调用了`boost::adjacency_list::clear()`。该成员函数移除所有点和线条。它是`boost::adjacency_list`的成员函数，而不是自由函数。

## 算法

Boost.Graph 的算法与标准库的算法相似——它们是通用的且非常灵活。然而，并不总是一眼看出如何使用它们。

### 示例 31.8. 使用 `breadth_first_search()` 从内向外访问点

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/breadth_first_search.hpp>
#include <boost/graph/named_function_params.hpp>
#include <boost/graph/visitors.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <iterator>
#include <algorithm>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::adjacency_list<boost::setS, boost::vecS,
    boost::undirectedS> graph;
  graph g{edges.begin(), edges.end(), 4};

  std::array<int, 4> distances{{0}};

  boost::breadth_first_search(g, topLeft,
    boost::visitor(
      boost::record_distances(distances.begin(),
          boost::on_tree_edge{})));

  std::copy(distances.begin(), distances.end(), std::ostream_iterator<int>(std::cout, "\n"));
}
```



# 示例 31.8：使用 `breadth_first_search()` 从内向外访问点

使用 `breadth_first_search()` 算法从内向外访问点。它从第二个参数传递的点开始，并访问从该点直接到达的所有点。`breadth_first_search()` 并不返回特定结果，它只是访问点。

通过向 `breadth_first_search()` 传递访问者（visitors），你可以决定访问点时发生什么。访问者是在访问点时会被调用的成员函数。

示例 31.8 使用了一个记录距离的访问者。距离是从一个点到另一个点需要跨越的线条数量。Boost.Graph 提供了辅助函数 `record_distances()` 来创建访问者。

属性映射（property maps）存储点或线条的属性。Boost.Graph 描述了属性映射的概念。由于属性映射接受指针或迭代器作为起始，因此不需要深入理解属性映射。在示例 31.8 中，通过 `distances.begin()` 将数组的起始传递给 `record_distances()`。这足够让 `distances` 用作属性映射。然而，数组的大小不能小于点的数量。

请注意，`distances` 是基于 `boost::array` 的，而不是 `std::array`。使用 `std::array` 将导致编译错误。

不同的算法对应不同的事件。传递给 `record_distances()` 的第二个参数指定了访问者应该通知哪些事件。Boost.Graph 定义了空类来命名事件。示例 31.8 中的 `boost::on_tree_edge` 标签指定在发现新点时记录距离。

事件取决于算法。你需要查看算法的文档以确定支持哪些事件以及可以使用哪些标签。

由 `boost::record_distances()` 创建的访问者（visitor）与算法无关，因此你可以将 `boost::record_distances()` 与其他算法配合使用。适配器（adapter）用于绑定算法和访问者。示例 31.8 调用了 `boost::make_bfs_visitor()` 来创建此适配器。该辅助函数返回 `boost::breadth_first_search()` 预期的访问者。该访问者定义了算法支持的成员函数。例如，`boost::make_bfs_visitor()` 返回的访问者定义了成员函数 `tree_edge()`。如果将带有 `boost::on_tree_edge` 标签的访问者传递给 `boost::make_bfs_visitor()`（当 `tree_edge()` 被调用时，访问者会被通知），这允许你在不同算法中使用访问者，而无需让这些访问者定义算法的所有成员函数。

`boost::make_bfs_visitor()` 返回的适配器不能直接传递给 `boost::breadth_first_search()`。它必须用 `boost::visitor()` 包裹并作为第三个参数传递。`boost::breadth_first_search()` 有变体。一种要求传递算法支持的所有参数。另一种支持类似于命名参数的形式。通常使用这种变体更简单，因为只需要传递你感兴趣的参数。许多参数不需要传递，因为算法使用了默认值。示例 31.8 使用了期望命名参数的 `boost::breadth_first_search()` 变体。前两个参数是图和起点，它们是必须的。然而，第三个参数可以是任何内容。在示例 31.8 中需要传递一个访问者。为了实现这一点，`boost::make_bfs_visitor()` 返回的适配器使用 `boost::visitor()` 进行命名。现在很清楚第三个参数是一个访问者。你将在下面的示例中看到如何通过名称将其他参数传递给 `boost::breadth_first_search()`。

示例 31.8 显示了 0、1、2。这些是从左上到所有点的距离。索引为 1 的右上字段只有一步之遥。索引为 2 的右下字段有两步遥。索引为 3 的左下字段同样只有一步之遥。首先打印的数字 0 指的是左上字段。由于它是传递给 `boost::breadth_first_search()` 的起点，因此到达它需要零步。`boost::breadth_first_search()` 不设置数组中的元素，它只是增加存储的值。因此，在开始之前必须初始化 `distances` 数组中的所有元素。

示例 31.9 说明了如何寻找最短路径。示例 31.9 显示了 0、1 和 2。这是从左上到右下的最短路径。它经过了右上字段，尽管经过左下字段的路径同样短。再次使用了 `boost::breadth_first_search()`——这次是为了寻找最短路径。如你所知，该算法只是访问点。要获取最短路径的描述，必须使用适当的访问者。示例 31.9 调用了 `boost::record_predecessors()` 来获取一个。`boost::record_predecessors()` 返回一个用于存储前驱的访问者。每当 `boost::breadth_first_search()` 访问新点时，上一个点就会存储在属性映射中。随着 `boost::breadth_first_search()` 从内向外访问点，找到了最短路径——从传递给 `boost::record_predecessors()` 的点开始。示例 31.9 找到了最短路径。

## 示例 31.9：使用 `breadth_first_search()` 查找路径

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/breadth_first_search.hpp>
#include <boost/graph/named_params.hpp>
#include <boost/graph/visitors.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <algorithm>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::adjacency_list<boost::setS, boost::vecS, boost::undirectedS> graph;
  graph g{edges.begin(), edges.end(), 4};

  boost::array<int, 4> predecessors;
  predecessors[bottomRight] = bottomRight;

  boost::breadth_first_search(g, bottomRight,
    boost::visitor(
      boost::make_bfs_visitor(
        boost::record_predecessors(predecessors.begin(),
          boost::on_tree_edge{}))));

  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = predecessors[p];
  }
  std::cout << p << '\n';
}
```

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/breadth_first_search.hpp>
#include <boost/graph/named_function_params.hpp>
#include <boost/graph/visitors.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <algorithm>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::adjacency_list<boost::setS, boost::vecS,
    boost::undirectedS> graph;
  graph g{edges.begin(), edges.end(), 4};

  boost::array<int, 4> distances{{0}};
  boost::array<int, 4> predecessors;
  predecessors[bottomRight] = bottomRight;

  boost::breadth_first_search(g, bottomRight,
    boost::visitor(
      boost::make_bfs_visitor(
        std::make_pair(
          boost::record_distances(distances.begin(),
            boost::on_tree_edge()),
          boost::record_predecessors(predecessors.begin(),
            boost::on_tree_edge{})))));

  std::for_each(distances.begin(), distances.end(),
    [](int d){ std::cout << d << '\n'; });

  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = predecessors[p];
  }
  std::cout << p << '\n';
}
```

# 示例 31.10：使用 `breadth_first_search()` 距离和路径

示例 31.10 展示了如何在使用两个访问者时使用 `boost::breadth_first_search()`。要使用两个访问者，你需要将它们放入 `std::make_pair()` 生成的配对中。如果需要两个以上的访问者，则必须对对进行嵌套。示例 31.10 所实现的功能与示例 31.8 和示例 31.9 结合的功能相同。

`boost::breadth_first_search()` 仅当每条边的权重相同时时才能使用。这意味着跨越点与点之间任何边所需的时间总是相同的。如果边是有权重的（意味着每条边可能需要不同的时间来通过），那么你需要使用不同的算法来寻找最短路径。

## 示例 31.11：使用 `dijkstra_shortest_paths()` 查找路径

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/dijkstra_shortest_paths.hpp>
#include <boost/graph/named_function_params.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::adjacency_list<boost::listS, boost::vecS,
    boost::undirectedS, boost::no_property,
    boost::property<boost::edge_weight_t, int>> graph;

  std::array<int, 4> weights{{2, 1, 1, 1}};

  graph g{edges.begin(), edges.end(), weights.begin(), 4};

  boost::array<int, 4> directions;
  boost::dijkstra_shortest_paths(g, bottomRight,
    boost::predecessor_map(directions.begin()));

  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = directions[p];
  }
  std::cout << p << '\n';
}
```

示例 31.11 使用 `dijkstra_shortest_paths()` 查找路径。`dijkstra_shortest_paths()` 只有在边有权重时才能使用。示例 31.11 使用了 `dijkstra_shortest_paths()` 来查找最短路径。`dijkstra_shortest_paths()` 是在边是有权重的情况下。示例 31.11 假设从左上角到右下角的时间是跨越其他边时间的两倍。

在使用 `dijkstra_shortest_paths()` 之前，必须为边分配权重。这是通过 `weights` 数组实现的。`dijkstra_shortest_paths()` 只有在属性已定义的情况下才有效。为了给边分配权重，使用了 `weights`。`dijkstra_shortest_paths()` 传递给 `adjacency_list` 的额外的参数。



默认情况下，`adjacency_list` 使用 `boost::no_property`，这意味着点和边都没有属性。示例 31.11，“使用 `dijkstra_shortest_paths()` 查找路径” 的第五个参数使用 `boost::property` 来定义打包属性。打包属性（bundled properties）是存储在图中的属性。由于可以定义多个属性，`boost::property` 需要一个标签来定义每个属性。Boost.Graph 提供了一些标签，如 `boost::edge_weight_t`，用于定义算法自动识别并使用的属性。传递给 `boost::property` 的第二个模板参数是属性的类型。示例 31.11，“使用 `dijkstra_shortest_paths()` 查找路径” 中权重是 `int` 类型。`dijkstra_shortest_paths()` 自动使用了类型为 `boost::edge_weight_t` 的打包属性。

注意没有向 `dijkstra_shortest_paths()` 传递访问者。该算法不仅仅是访问点。它是在寻找最短路径——这就是为什么它被称为 `dijkstra_shortest_paths()`。你不需要考虑事件或访问者。你只需要传递一个容器来存储每个前驱。如果你使用带有命名参数的 `dijkstra_shortest_paths()` 变体（参见示例 31.11，“使用 `dijkstra_shortest_paths()` 查找路径”），请通过 `boost::predecessor_map()` 传递容器。这是一个辅助函数，它期望指向数组开头的指针或迭代器。

示例 31.11，“使用 `dijkstra_shortest_paths()` 查找路径” 显示了 0, 3 和 2：从左上角到右下角的最短路径经过了左下角区域。经过右上角区域的路径权重大于其他可能性。

### 示例 31.12. 使用自定义属性的 `dijkstra_shortest_paths()`

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/dijkstra_shortest_paths.hpp>
#include <boost/graph/named_function_params.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  struct edge_properties
  {
    int weight;
  };

  typedef boost::adjacency_list<boost::listS, boost::vecS,
    boost::undirectedS, boost::no_property,
    edge_properties> graph;

  graph g{edges.begin(), edges.end(), 4};

  graph::edge_iterator it, end;
  boost::tie(it, end) = boost::edges(g);
  g[*it].weight = 2;
  g[*++it].weight = 1;
  g[*++it].weight = 1;
  g[*++it].weight = 1;

  boost::array<int, 4> directions;
  boost::dijkstra_shortest_paths(g, bottomRight,
    boost::predecessor_map(directions.begin()).
    weight_map(boost::get(&edge_properties::weight, g)));

  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = directions[p];
  }
  std::cout << p << '\n';
}
```

示例 31.12，“使用 `dijkstra_shortest_paths()` 的自定义属性” 工作方式与之前的一个相同，并显示相同的数字，但它使用用户定义的类 `edge_properties`，而不是预定义的属性。

`edge_properties` 定义了成员变量 `weight` 用来存储边的权重。如果需要其他属性，可以添加更多成员变量。

如果你使用边的描述符作为图的索引，就可以访问用户定义的属性。因此，图的行为就像一个数组。你可以从 `boost::edges()` 返回的边迭代器中获取描述符。这样，就可以为每条边分配权重。

为了让 `boost::dijkstra_shortest_paths()` 知道权重存储在 `edge_properties` 的 `weight` 中，必须传递另一个命名参数。这是通过 `weight_map()` 完成的。注意，`weight_map()` 是从 `boost::predecessor_map()` 返回的对象的成员函数。还有一个名为 `boost::weight_map()` 的非成员函数。如果你需要传递多个命名参数，必须在第一个命名参数（即由非成员函数返回的那个）上调用成员函数。这样，所有参数都会被封装到一个对象中，然后传递给算法。

为了告诉 `boost::dijkstra_shortest_paths()` `edge_properties` 中的 `weight` 包含权重，需要传递该属性的指针。它不是直接传递给 `weight_map()` 的，而是通过 `boost::get()` 创建的对象传递的。现在调用完成了，`boost::dijkstra_shortest_paths()` 知道应该访问哪个属性来获取权重。

### 示例 31.13. 在图定义时初始化自定义属性

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/dijkstra_shortest_paths.hpp>
#include <boost/graph/named_function_params.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  struct edge_properties
  {
    int weight;
  };

  typedef boost::adjacency_list<boost::listS, boost::vecS,
    boost::undirectedS, boost::no_property,
    edge_properties> graph;

  boost::array<edge_properties, 4> props{{2, 1, 1, 1}};

  graph g{edges.begin(), edges.end(), props.begin(), 4};

  std::array<int, 4> directions;
  boost::dijkstra_shortest_paths(g, bottomRight,
    boost::predecessor_map(directions.begin()).
    weight_map(boost::get(&edge_properties::weight, g)));

  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = directions[p];
  }
}
```

在定义图时可以初始化自定义属性。你只需要向 `boost::adjacency_list` 传递一个迭代器作为第三参数，指向属性。示例 31.13，“在图定义时初始化自定义属性” 工作方式与之前的一个相同，并显示相同的结果。

```cpp
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/dijkstra_shortest_paths.hpp>
#include <boost/graph/named_function_params.hpp>
#include <boost/array.hpp>
#include <array>
#include <utility>
#include <iostream>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  struct edge_properties
  {
    int weight;
  };

  typedef boost::adjacency_list<boost::listS, boost::vecS,
    boost::undirectedS, boost::no_property,
    edge_properties> graph;

  boost::array<edge_properties, 4> props{{2, 1, 1, 1}};

  graph g{edges.begin(), edges.end(), props.begin(), 4};

  std::array<int, 4> directions;
  boost::dijkstra_shortest_paths(g, bottomRight,
    boost::predecessor_map(directions.begin()).
    weight_map(boost::get(&edge_properties::weight, g)));

  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = directions[p];
  }
  std::cout << p << '\n';
}
```

示例 31.12，“使用 `dijkstra_shortest_paths()` 的自定义属性” 中算法返回传递给 `boost::predecessor_map` 的容器中的前驱。与 `dijkstra_shortest_paths()` 不同，起始点没有直接作为参数传递给 `random_shortest_tree()`。它必须作为命名参数传递。这就是为什么在 `predecessor_map` 类型的对象上调用了 `root_vertex()`。

```cpp
// ... 省略代码 ...
int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };
  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};
  struct edge_properties
  {
    int weight;
  };
  typedef boost::adjacency_list<boost::listS, boost::vecS,
    boost::undirectedS, boost::no_property,
    edge_properties> graph;
  graph g{edges.begin(), edges.end(), 4};
  boost::array<int, 4> directions;
  boost::dijkstra_shortest_paths(g, bottomRight,
    boost::predecessor_map(directions.begin()).
    weight_map(boost::get(&edge_properties::weight, g)));
  int p = topLeft;
  while (p != bottomRight)
  {
    std::cout << p << '\n';
    p = directions[p];
  }
  std::cout << p << '\n';
}
```

示例 31.14，“使用 `dijkstra_shortest_paths()` 的随机路径” 寻找随机路径。

因为 `dijkstra_shortest_paths()` 正在寻找随机路径，因此必须将随机数生成器作为第二个参数传递。示例 31.14，“使用 `dijkstra_shortest_paths()` 的随机路径” 使用 `std::mt19937`，从 C++11 起它是标准库的一部分。你也可以使用 Boost.Random 中的随机数生成器。

示例 31.14，“使用 `dijkstra_shortest_paths()` 的随机路径” 显示 1, 0 和 3，或者 1, 2 和 3。1 是右上角，3 是左下角。从右上角到左下角只有两条可能的路径：通过左上角或通过右下角。`dijkstra_shortest_paths()` 必须返回这两条路径之一。

## 容器

到目前为止本书中的所有示例都使用了 `boost::adjacency_list` 来定义图。本节介绍了 Boost.Graph 提供的另外两个图容器：`boost::adjacency_matrix` 和 `boost::compressed_sparse_row_graph`。

在 Boost 1.56.0 中，`boost/graph/adjacency_matrix.hpp` 缺少一个包含文件。要使用 Boost 1.56.0 编译示例 31.15，“使用 `boost::adjacency_matrix` 的图”，请在包含 `boost/graph/adjacency_matrix.hpp` 之前包含 `boost/functional/hash.hpp`。

### 示例 31.15. 使用 `boost::adjacency_matrix` 的图

```cpp
#include <boost/graph/adjacency_matrix.hpp>
#include <array>
#include <utility>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::adjacency_matrix<boost::undirectedS> graph;
  graph g{edges.begin(), edges.end(), 4};
}
```



`boost::adjacency_matrix` 的用法类似于 `boost::adjacency_list`（请参阅 示例 31.15，“使用 `boost::adjacency_matrix` 的图”）。然而，用于传递选择器的两个模板参数在 `boost::adjacency_matrix` 中并不存在。使用 `boost::adjacency_matrix` 时不需要使用如 `boost::vecS` 和 `boost::setS` 等选择器。`boost::adjacency_matrix` 将图存储在 `matrix` 中，其内部结构是硬编码的。你可以将 `matrix` 视为二维表格：该表格是一个正方形，其行数和列数等于图中点的数量。通过标记对应 `line` 两个端点的行和列相交的单元格，创建一个 `line`。

`boost::adjacency_matrix` 的内部结构使其能够快速地添加和删除 `lines`。然而，它的内存消耗更高。经验法是，当 `lines` 的数量相对于点较少时，使用 `boost::adjacency_list`。`lines` 越多，使用 `boost::adjacency_matrix` 就越有意义。

### 示例 31.16. 使用 `boost::compressed_sparse_row_graph` 的图

```cpp
#include <boost/graph/compressed_sparse_row_graph.hpp>
#include <array>
#include <utility>

int main()
{
  enum { topLeft, topRight, bottomRight, bottomLeft };

  std::array<std::pair<int, int>, 4> edges{{
    std::make_pair(topLeft, topRight),
    std::make_pair(topRight, bottomRight),
    std::make_pair(bottomRight, bottomLeft),
    std::make_pair(bottomLeft, topLeft)
  }};

  typedef boost::compressed_sparse_row_graph<boost::bidirectionalS> graph;
  graph g{boost::edges_are_unsorted_multi_pass, edges.begin(),
    edges.end(), 4};
}
```

`boost::compressed_sparse_row_graph` 的用法与 `boost::adjacency_list` 和 `boost::adjacency_matrix` 相同（请参阅 示例 31.16，“使用 `boost::compressed_sparse_row_graph` 的图”）。最重要的区别是图无法通过 `boost::compressed_sparse_row_graph` 进行更改。一旦创建，就不能添加或删除点和 `lines`。因此，`boost::compressed_sparse_row_graph` 仅在使用不可变图时才有意义。

`boost::compressed_sparse_row_graph` 只支持有向的 `lines`。你不能使用模板参数 `boost::undirectedS` 实例化 `boost::compressed_sparse_row_graph`。

`boost::compressed_sparse_row_graph` 主要优势是内存消耗低。如果你有一个巨大的图并且需要保持低内存消耗，`boost::compressed_sparse_row_graph` 特别有用。

# 第六部分. 通信

以下库有助于与其他程序进行通信。

* `Boost.Asio` 用于通过网络通信。`Boost.Asio` 不仅支持网络操作。Asio 代表异步输入/输出。你可以使用此库来异步处理数据，例如，当你的程序与设备（如网卡）通信时，这些设备可以与你程序中执行的代码并发处理任务。

* `Boost.Interprocess` 用于通过共享内存进行通信。

# 32. Boost.Asio

本章介绍 [Boost.Asio](http://www.boost.org/libs/asio) 库。Asio 代表异步输入/输出。该库使得异步处理数据成为可能。异步意味着当操作启动时，发起的程序不需要等待操作结束。相反，`Boost.Asio` 在操作结束时会通知程序。其优势是可以并发执行其他操作。

`Boost.Thread` 是另一个允许并发执行操作的库。`Boost.Thread` 与 `Boost.Asio` 的区别在于，`Boost.Thread` 访问程序内部资源，而 `Boost.Asio` 访问外部资源。例如，如果你开发一个需要耗时的函数，可以在线程中调用它并让其在核心上执行。对于程序而言，线程核心是内部资源。如果你想访问外部资源，可以使用 `Boost.Asio`。

网络连接是外部资源的示例。如果必须发送或接收数据，会让网卡执行操作。对于发送操作，网卡获取一个要发送数据的缓冲区；对于接收操作，网卡获取一个应该填充接收数据的缓冲区。由于网卡是程序的外部资源，它可以独立执行操作。Asio 允许你更有效地利用可用设备。

在网络上发送和接收数据在 `Boost.Asio` 中实现为异步操作。可以将异步操作理解为立即返回但不带结果的函数。结果稍后提供。在第一步中，启动异步操作；在第二步中，会通知程序。这种分离使得不需要阻塞函数。

## I/O 服务与 I/O 对象

基于 `Boost.Asio` 的异步数据处理基于 I/O 服务和 I/O 对象。I/O 服务抽象了操作系统接口。I/O 对象发起异步操作。这两个概念有助于清晰分离任务：I/O 服务面向操作系统 API，而 I/O 对象面向开发者需要完成的任务。

作为 `Boost.Asio` 的用户，你通常不会直接与 I/O 服务连接。I/O 服务由 I/O 对象管理。I/O 对象像一个注册表，列出了 I/O 服务。每个 I/O 对象知道自己的 I/O 服务，并通过 I/O 对象获取对 I/O 服务的访问。

`Boost.Asio` 定义了 `boost::asio::io_service`，这是 I/O 服务对象的单一类。每个 `Boost.Asio` 程序都使用 `boost::asio::io_service` 对象。也可以使用全局变量。

虽然 I/O 服务对象只有一个类，但 I/O 对象有多个类。因为 I/O 对象面向任务，所以实例化的类取决于任务。例如，如果要在 TCP/IP 连接上发送或接收数据，可以使用类型为 `boost::asio::ip::tcp::socket` 的 I/O 对象。

`boost::asio::steady_timer` 就像一个闹钟。当闹钟响起时，你的程序不需要等待一个阻塞函数返回，而是会收到通知。因为 `boost::asio::steady_timer` 只是在等待一段时间到期，看起来似乎没有访问任何外部资源。然而，在这种情况下，外部资源是操作系统在时间段到期时通知程序的能力。这使得程序从仅为了调用阻塞函数而创建新线程中解放出来。由于 `boost::asio::steady_timer` 是一个非常简单的 I/O 对象，它将被用于介绍 `Boost.Asio`。

### 注意

由于 `Boost.Asio` 中的一个错误，无法使用 Clang 编译以下某些示例。该错误已在 [ticket 8835](https://svn.boost.org/trac/boost/ticket/8835) 中报告。作为变通方法，如果你将 `std::chrono` 中的类型替换为 `boost::chrono` 中相应的类型，就可以用 Clang 编译这些示例。

示例 32.1，“使用 `boost::asio::steady_timer`”创建了一个 I/O 服务对象 `ioservice`，并用它初始化 I/O 对象 `timer`。与 `boost::asio::steady_timer` 一样，所有的 I/O 对象都期望将 I/O 服务对象作为构造函数的第一个参数。由于 `timer` 代表一个闹钟，可以向 `boost::asio::steady_timer` 的构造函数传递第二个参数，定义闹钟应该响的特定时间或时间段。在 示例 32.1，“使用 `boost::asio::steady_timer`”中，闹钟被设置为在 3 秒后响。时间从定义 `timer` 时开始。

#### 示例 32.1. 使用 `boost::asio::steady_timer`

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/steady_timer.hpp>
#include <chrono>
#include <iostream>

using namespace boost::asio;

int main()
{
  io_service ioservice;

  steady_timer timer{ioservice, std::chrono::seconds{3}};
  timer.async_wait([](const boost::system::error_code &ec)
    { std::cout << "3 sec\n"; });

  ioservice.run();
}
```

`Boost.Asio` 并不是调用一个在闹钟响起时返回的阻塞函数，而是允许你启动一个异步操作。要做到这一点，调用成员函数 `async_wait()`，它期望处理器（handler）作为唯一的参数。处理器是在异步操作结束时调用的函数或函数对象。在 示例 32.1，“使用 `boost::asio::steady_timer`”中，传递了一个 lambda 函数作为处理器。

`async_wait()` 会立即返回。它并不是等待三秒直到闹钟响起，而是在三秒后调用 lambda 函数。当 `async_wait()` 返回时，程序可以执行其他事情。

像 `async_wait()` 这样的成员函数是非阻塞调用的。I/O 对象通常还提供阻塞成员函数作为替代。例如，你可以调用 `boost::asio::steady_timer` 上的阻塞成员函数 `wait()`。因为这个成员函数是阻塞的，所以不需要传递处理器。`wait()` 在特定时间或时间段后返回。

在 示例 32.1，“使用 `boost::asio::steady_timer`”中，`main()` 中的最后一条语句是对 I/O 服务对象的 `run()` 调用。这个调用是必要的，因为必须让特定的函数接管控制权。

如果在类型为 `boost::asio::io_service` 的对象上调用成员函数 `run()`，关联的处理器将在同一线程内被调用。通过使用多个线程，程序可以多次调用 `run()`。一旦异步操作完成，I/O 服务对象将在这些线程之一中执行处理器。如果第二个操作在第一个操作完成后不久又完成，I/O 服务对象可以在不同的线程中执行处理器。现在，不仅进程之外的操作可以并发执行，进程内部的处理器也可以并发执行。

### 示例 32.3. I/O 服务对象使用两个线程并发执行处理器

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/steady_timer.hpp>
#include <chrono>
#include <thread>
#include <iostream>

using namespace boost::asio;

int main()
{
  io_service ioservice;

  steady_timer timer1{ioservice, std::chrono::seconds{3}};
  timer1.async_wait([](const boost::system::error_code &ec)
    { std::cout << "3 sec\n"; });

  steady_timer timer2{ioservice, std::chrono::seconds{3}};
  timer2.async_wait([](const boost::system::error_code &ec)
    { std::cout << "3 sec\n"; });

  std::thread thread1{[&ioservice](){ ioservice.run(); }};
  std::thread thread2{[&ioservice](){ ioservice.run(); }};
  thread1.join();
  thread2.join();
}
```

上一个示例已转换为多线程程序，参见示例 32.3，“I/O 服务对象使用两个线程并发执行处理器”。通过 `std::thread`，在 `main()` 中创建了两个线程。每个线程中都对唯一的 I/O 服务对象调用了 `run()`。这使得 I/O 服务对象在异步操作完成后可以使用两个线程来执行处理器。

在示例 32.3，“I/O 服务对象使用两个线程并发执行处理器”中，两个闹钟都会在三秒后响铃。因为有两个线程可用，两个 lambda 函数可以并发执行。如果第二个闹钟在第一个闹钟的处理器执行时响起，则处理器可以在第二个线程中执行。如果第一个闹钟的处理器已经返回，则执行第二个处理器。

当然，使用线程并不总是有意义的。示例 32.3，“I/O 服务对象使用两个线程并发执行处理器”可能不会按顺序将消息写入标准输出流。相反，它们可能会混杂。两个在两个线程中并发运行的处理器共享全局资源 `std::cout`。为了避免中断，对 `std::cout` 的访问需要同步处理。如果处理器不能并发执行，线程的优势就会消失。

### 示例 32.4. 两个 I/O 服务对象各使用一个线程并发执行处理器

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/steady_timer.hpp>
#include <chrono>
#include <thread>
#include <iostream>

using namespace boost::asio;

int main()
{
  io_service ioservice1;
  io_service ioservice2;

  steady_timer timer1{ioservice1, std::chrono::seconds{3}};
  timer1.async_wait([](const boost::system::error_code &ec)
    { std::cout << "3 sec\n"; });

  steady_timer timer2{ioservice2, std::chrono::seconds{3}};
  timer2.async_wait([](const boost::system::error_code &ec)
    { std::cout << "3 sec\n"; });

  std::thread thread1{[&ioservice1](){ ioservice1.run(); }};
  std::thread thread2{[&ioservice2](){ ioservice2.run(); }};
  thread1.join();
  thread2.join();
}
```

在单个 I/O 服务对象上反复调用 `run()` 是使基于 `Boost.Asio` 的程序更具扩展性的推荐方法。然而，与其为一个 I/O 服务对象提供多个线程，你也可以创建多个 I/O 服务对象。

在示例 32.4，“两个 I/O 服务对象各使用一个线程并发执行处理器”中，两个类型为 `boost::asio::steady_timer` 的闹钟旁边分别使用了两个 I/O 服务对象。程序基于两个线程，每个线程绑定到一个服务对象。`timer1` 和 `timer2` 没有绑定到同一个 I/O 服务上。

在示例 32.4，“两个 I/O 服务对象各使用一个线程并发执行处理器”中，其工作方式与之前相同。对于何时使用多个 I/O 服务对象合适，无法给出通用的建议。在 Windows 上，`boost::asio::io_service` 通常基于 IOCP；在 Linux 上，它代表特定的接口。

## 网络编程

尽管 `Boost.Asio` 可以异步处理任何类型的数据，但它主要用于网络编程。这是因为在 `Boost.Asio` 添加额外的 I/O 对象之前，就已经支持网络函数了。网络函数是异步操作的完美用例，因为通过网络传输数据可能需要很长时间，这意味着确认和错误返回可能没有发送或接收函数那么快。

`Boost.Asio` 提供了许多 I/O 对象来开发网络程序。示例 32.5，“使用 `boost::asio::tcp::socket` 的网络客户端”使用 `boost::asio::tcp::socket` 类与另一台计算机建立连接。该示例向 Web 服务器发送 HTTP 请求以下载首页。

在 `main()` 中，实例化了 `boost::asio::ip::tcp::resolver::query` 来创建一个对象 `q`。`q` 代表对名称解析器的查询，这是一个类型为 `boost::asio::ip::tcp::resolver` 的 I/O 对象。通过将 `q` 传递给 `async_resolve()`，启动了一个用于解析名称的异步操作。示例 32.5，“一个使用 `boost::asio::ip::tcp::socket` 的网络客户端”解析了名称 `theboostcpplibraries.com`。在异步操作启动后，在 I/O 服务对象上调用了 `run()`，将控制权交给操作系统。

### 示例 32.5. 使用 `boost::asio::ip::tcp::socket` 的网络客户端



以下是一个使用 Boost.Asio 库的 C++ 程序示例，它通过异步操作从 `theboostcpplibraries.com` 下载首页内容：

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/write.hpp>
#include <boost/asio/buffer.hpp>
#include <boost/asio/ip/tcp.hpp>
#include <array>
#include <string>
#include <iostream>

using namespace boost::asio;
using namespace boost::asio::ip;

io_service ioservice;
tcp::resolver resolv{ioservice};
tcp::socket tcp_socket{ioservice};
std::array<char, 4096> bytes;

void read_handler(const boost::system::error_code &ec,
  std::size_t bytes_transferred)
{
  if (!ec)
  {
    std::cout.write(bytes.data(), bytes_transferred);
    tcp_socket.async_read_some(buffer(bytes), read_handler);
  }
}

void connect_handler(const boost::system::error_code &ec)
{
  if (!ec)
  {
    std::string r =
      "GET / HTTP/1.1\r\nHost: theboostcpplibraries.com\r\n\r\n";
    write(tcp_socket, buffer(r));
    tcp_socket.async_read_some(buffer(bytes), read_handler);
  }
}

void resolve_handler(const boost::system::error_code &ec,
  tcp::resolver::iterator it)
{
  if (!ec)
    tcp_socket.async_connect(*it, connect_handler);
}

int main()
{
  tcp::resolver::query q{"theboostcpplibraries.com", "80"};
  resolv.async_resolve(q, resolve_handler);
  ioservice.run();
}
```

当名称解析完成后，会调用 `resolve_handler()`。该处理程序首先检查名称解析是否成功。在这种情况下，`ec` 为 0。只有此时，才会访问 socket 以建立连接。要连接的服务器地址由第二个参数提供，其类型为 `boost::asio::ip::tcp::resolver::iterator`。该参数是名称解析的结果。

对 `async_connect()` 的调用之后是调用了处理程序 `connect_handler()`。同样，首先检查 `ec` 以确定是否可以建立连接。如果是，则在 socket 上调用 `async_read_some()`。通过此调用，开始读取数据。接收到的数据存储在数组 `bytes` 中，并作为第一个参数传递给 `async_read_some()`。

当接收到一个或多个字节并复制到 `bytes` 时，会调用 `read_handler()`。类型为 `std::size_t` 的参数 `bytes_transferred` 包含了接收到的字节数。按照惯例，处理程序应首先检查 `ec` 异步操作是否成功完成。只有在这种情况下，数据才会写入标准输出。

请注意，`read_handler()` 在数据写入 `std::cout` 之后再次调用了 `async_read_some()`。这是因为你无法确定整个首页是否已经在单次异步操作中下载并复制到 `bytes` 中。重复调用 `async_read_some()` 后重复调用 `read_handler()` 直到连接关闭，而连接关闭发生在 Web 服务器发送了整个首页之后。此时，`read_handler()` 在 `ec` 中报告错误。此时，不再有进一步的数据写入 `std::cout`，且不再在 socket 上调用 `async_read()`。由于没有待挂的异步操作，程序退出。

示例 32.6，“一个使用 `boost::asio::ip::tcp::acceptor` 的时间服务器`是一个时间服务器。你可以使用 telnet 客户端连接以获取当前时间。之后时间服务器关闭。

时间服务器使用 I/O 对象 `boost::asio::ip::tcp::acceptor` 来接受来自另一个程序的传入连接。你必须初始化该对象，使其知道在哪个端口上使用什么协议。在示例中，使用了类型为 `boost::asio::ip::tcp::endpoint` 的变量 `tcp_endpoint` 来告诉 `tcp_acceptor` 接受端口 2014 上的互联网协议 4 版本的传入连接。

在 acceptor 初始化后，调用了 `listen()`。调用 `listen()` 是为了让 acceptor 开始工作。

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/spawn.hpp>
#include <boost/asio/write.hpp>
#include <boost/asio/buffer.hpp>
#include <boost/asio/ip/tcp.hpp>
#include <list>
#include <string>
#include <ctime>

using namespace boost::asio;
using namespace boost::asio::ip;

io_service ioservice;
tcp::endpoint tcp_endpoint{tcp::v4(), 2014};
tcp::acceptor tcp_acceptor{ioservice, tcp_endpoint};
std::list<tcp::socket> tcp_sockets;

void do_write(tcp::socket &tcp_socket, yield_context yield)
{
  std::time_t now = std::time(nullptr);
  std::string data = std::ctime(&now);
  async_write(tcp_socket, buffer(data), yield);
  tcp_socket.shutdown(tcp::socket::shutdown_send);
}

void do_accept(yield_context yield)
{
  for (int i = 0; i < 2; ++i)
  {
    tcp_sockets.emplace_back(ioservice);
    tcp_acceptor.async_accept(tcp_sockets.back(), yield);
    spawn(ioservice, [](yield_context yield)
      { do_write(tcp_sockets.back(), yield); });
  }
}

int main()
{
  tcp_acceptor.listen();
  spawn(ioservice, do_accept);
  ioservice.run();
}
```

协程允许你创建一种与实际程序逻辑镜像的结构。异步操作不会拆分函数，因为没有处理器（handlers）来定义异步操作完成时应该发生什么。程序不再需要处理器之间相互调用，而是可以使用顺序结构。

在 Boost.Asio 中使用协程调用的函数是 `boost::asio::spawn()`。传递的第一个参数必须是一个 I/O 服务对象。第二个参数是要作为协程的函数。该函数必须接受一个类型为 `boost::asio::yield_context` 的对象作为唯一参数。它不能有返回值。示例 32.7, “使用 Boost.Asio 的协程` 使用 `do_accept()` 和 `do_write()` 作为协程。如果函数签名不同（如 `do_write()` 的情况所示），你必须使用像 `std::bind` 或 lambda 表达式这样的适配器。

你可以不传递处理器，而是向异步函数传递一个类型为 `boost::asio::yield_context` 的对象。`do_accept()` 将参数 `yield` 传递给 `async_accept()`。在 `do_write()` 中，`yield` 被传递给 `async_write()`。这些函数调用仍然启动了异步操作，但在操作完成时不会调用处理器。相反，启动异步操作的上下文将被恢复。当这些异步操作完成时，程序将从上次停止的地方继续执行。

`do_accept()` 包含一个 `for` 循环。每次调用该函数时，都会向 `async_accept()` 传递一个新的套接字。一旦客户端建立连接，就会通过 `boost::asio::spawn()` 作为协程调用 `do_write()`，向客户端发送当前时间。

`for` 循环使得我们很容易看出程序在退出前可以服务两个客户端。由于示例是基于协程的，异步操作的重复执行可以在 `for` 循环中实现。这提高了程序的可读性，因为你不需要追踪对处理器的潜在调用，以确定最后一个异步操作何时完成。如果时间服务器需要支持两个两个客户端，只需调整 `for` 循环即可。

## 特定于平台的 I/O 对象

到为止，本章中的所有示例都是平台无关的。如 `boost::asio::steady_timer` 和 `boost::asio::ip::tcp::socket` 等 I/O 对象在所有平台上都受支持。然而，Boost.Asio 也提供了特定于平台的 I/O 对象，因为某些异步操作仅在某些平台上可用，例如 Windows 或 Linux。示例 32.8, “使用 boost::asio::windows::object_handle` 使用 `boost::asio::windows::object_handle`，这是仅在 Windows 上可用的 I/O 对象。`RegisterWaitForObject()` 函数允许你启动异步操作。所有由 `RegisterWaitForObject()` 接受的句柄都可以配合 `boost::asio::windows::object_handle` 使用。通过 `wait()`，可以异步等待句柄的变化。

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/windows/object_handle.hpp>
#include <boost/system/error_code.hpp>
#include <iostream>
#include <Windows.h>

using namespace boost::asio;
using namespace boost::system;

int main()
{
  io_service ioservice;

  HANDLE file_handle = CreateFile(".", FILE_DIRECTORY,
    FILE_SHARE_READ | FILE_SHARE_WRITE | FILE_SHARE_DELETE, NULL,
    OPEN_EXISTING, FILE_BACKUP_SEMANTICS | FILE_FLAG_OVERAPPED, NULL);

  char buffer[1024];
  DWORD transferred;
  OVERLAPPED overlapped;
  ZeroMemory(&overlapped, sizeof(overlapped));
  overlapped.hEvent = CreateEvent(NULL, FALSE, NULL);
  ReadDirectoryChangesW(file_handle, buffer, sizeof(buffer), FALSE,
    FILE_NOTIFY_CHANGE_FILE_NAME, &transferred, &overlapped, NULL);

  windows::object_handle obj_handle{ioservice, overlapped.hEvent};
  obj_handle.async_wait(&buffer, &overlapped {
    if (!ec)
    {
      DWORD transferred;
      GetOverlappedResult(overlapped.hEvent, &overlapped, &transferred, FALSE);
      auto notification = reinterpret_cast<FILE_NOTIFY_INFORMATION*>(buffer);
      std::wcout << notification->Action << '\n';
      std::streamsize size = notification->FileNameLength / sizeof(wchar_t);
      std::wcout.write(notification->FileName, size);
    }
  });

  ioservice.run();
}
```

示例 32.8, “使用 boost::asio::windows::object_handle` 使用 Windows 函数 `CreateEvent()` 创建句柄初始化 `boost::asio::windows::object_handle` 对象。该句柄是 `OVERLAPPED` 结构的一部分，其地址被传递给 `ReadDirectoryChangesW()`。Windows 使用 `OVERLAPPED` 结构来启动异步操作。为了通过 Boost.Asio 报告异步操作的完成，在调用 `ReadDirectoryChangesW()` 之前会将事件处理器存储在 `OVERLAPPED` 结构中。该事件处理器随后传递给 `obj_handle`。当在 `obj_handle` 上调用 `async_wait()` 时，当检测到目录变化时，处理器就会执行。

`boost::asio::windows::overlapped_ptr` 是一个没有启动异步操作成员成员的 I/O 对象。异步操作是通过将指向内部 `OVERLAPPED` 变量的指针传递给 Windows 函数来启动的。除了 I/O 服务对象外，`boost::asio::windows::overlapped_ptr` 的构造函数还期望一个在异步操作完成后被调用的处理器（handler）。

示例 32.9，“使用 `boost::asio::windows::overlapped_ptr`”](#part0057.html_ex.asio_09 "Example 32.9. Using boost::asio::windows::overlapped_ptr") 使用 `boost::asio::use_service()` 来获取 I/O 服务对象 `ioservice` 中服务的引用。`boost::asio::use_service()` 是一个函数模板。你想要获取的 I/O 服务类型必须作为模板参数传递。在示例中，传递了 `boost::asio::detail::io_service_impl`。这种类型的 I/O 服务最接近操作系统。在 Windows 上，`boost::asio::detail::io_service_impl` 使用 IOCP，而在 Linux 上它使用 `epoll()`。`boost::asio::detail::io_service_impl` 是一个类型定义，在 Windows 上被设置为 `boost::asio::detail::win_iocp_io_service`，在 Linux 上被设置为 `boost::asio::detail::task_io_service`。

`boost::asio::detail::win_iocp_io_service` 提供成员函数 `register_handle()` 将句柄链接到 IOCP 句柄。`register_handle()` 调用 Windows 函数 `CreateIoCompletionPort()`。该调用对于示例的正确运行是必要的。`CreateFileA()` 返回的句柄只有在链接到 IOCP 句柄后才能通过 `overlapped` 传递给 `ReadDirectoryChangesW()`。

示例 32.9，“使用 `boost::asio::windows::overlapped_ptr`”](#part0057.html_ex.asio_09 "Example 32.9. Using boost::asio::windows::overlapped_ptr")检查 `ReadDirectoryChangesW()` 是否失败。如果 `ReadDirectoryChangesW()` 失败，则在 `overlapped` 上调用 `complete()` 来完成 Boost.Asio 的异步操作。传递给 `complete()` 的参数会被转发给处理器。

如果 `ReadDirectoryChangesW()` 成功，则调用 `release()`。此时，异步操作处于挂起状态，只有在通过 Windows 函数 `ReadDirectoryChangesW()` 启动的操作完成后，才会完成。

### 示例 32.9. 使用 `boost::asio::windows::overlapped_ptr`



```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/windows/overlapped_ptr.hpp>
#include <boost/system/error_code.hpp>
#include <iostream>
#include <Windows.h>

using namespace boost::asio;
using namespace boost::system;

int main()
{
  io_service ioservice;

  HANDLE file_handle = CreateFileA(".", FILE_LIST_DIRECTORY,
    FILE_SHARE_READ | FILE_SHARE_WRITE | FILE_SHARE_DELETE, NULL,
    OPEN_EXISTING, FILE_FLAG_BACKUP_SEMANTICS | FILE_FLAG_OVERAPPED, NULL);

  error_code ec;
  auto &io_service_impl = use_service<detail::io_service_impl>(ioservice);
  io_service_impl.register_handle(file_handle, ec);

  char buffer[1024];
  auto handler = &buffer {
    if (!ec)
    {
      auto notification =
        reinterpret_cast<FILE_NOTIFY_INFORMATION*>(buffer);
      std::wcout << notification->Action << '\n';
      std::streamsize size = notification->FileNameLength / sizeof(wchar_t);
      std::wcout.write(notification->FileName, size);
    }
  };
  windows::overlapped_ptr overlapped{ioservice, handler};
  DWORD transferred;
  BOOL ok = ReadDirectoryChangesW(file_handle, buffer, sizeof(buffer),
    FALSE, FILE_NOTIFY_CHANGE_FILE_NAME, &transferred, overlapped.get(),
    NULL);
  int last_error = GetLastError();
  if (!ok && last_error != ERROR_IO_PENDING)
  {
    error_code ec{last_error, error::get_system_category()};
    overlapped.complete(ec, 0);
  }
  else
  {
    overlapped.release();
  }

  ioservice.run();
}
```

### 示例 32.10. 使用 `boost::asio::posix::stream_descriptor`

```cpp
#include <boost/asio/io_service.hpp>
#include <boost/asio/posix/stream_descriptor.hpp>
#include <boost/asio/write.hpp>
#include <boost/system/error_code.hpp>
#include <iostream>
#include <unistd.h>

using namespace boost::asio;

int main()
{
  io_service ioservice;

  posix::stream_descriptor stream{ioservice, STDOUT_FILENO};
  auto handler = [](const boost::system::error_code&, std::size_t) {
    std::cout << "Hello!\n";
  };
  async_write(stream, boost::buffer("Hello!"), handler);

  ioservice.run();
}
```

示例 32.10，“使用 `boost::asio::posix::stream_descriptor`” 为 POSIX 平台引入了一个 I/O 对象。`boost::asio::posix::stream_descriptor` 可以用文件描述符初始化。

# 33 Boost.Interprocess

进程间通信描述了运行在同一台计算机上的进程之间交换数据的机制。它不包括网络。虽然不同操作系统之间的进程间通信概念相似，但接口可能会有很大差异。本章介绍了该库，该库涵盖了 Boost.asio。

## 共享内存

共享内存通常是最快的进程间通信形式。它提供了一个进程间共享的内存区域。一个进程可以向该区域写入数据，另一个进程可以读取它。

在 Boost.Interprocess 中，使用 `boost::interprocess::shared_memory_object` 类来表示共享内存。使用该类需要包含头文件 `boost/interprocess/shared_memory_object.hpp`。

### 示例 33.1. 创建共享内存

```cpp
#include <boost/interprocess/shared_memory_object.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object shdmem{open_or_create, "Boost", read_write};
  shdmem.truncate(1024);
  std::cout << shdmem.get_name() << '\n';
  offset_t size;
  if (shdmem.get_size(size))
    std::cout << size << '\n';
}
```

`boost::interprocess::shared_memory_object` 的构造函数期望三个参数。第一个参数指定是创建共享内存还是仅打开。示例 33.1，“创建共享内存” 处理了这两种情况。`boost::interprocess::open_or_create` 如果共享内存已存在则打开它，如果不存在则创建它。

打开现有的共享内存假设它已经被创建过。为了唯一标识共享内存，分配了一个名称。该名称是由传递给 `boost::interprocess::shared_memory_object` 构造函数的第二个参数指定的。

第三个参数决定了进程如何访问共享内存。在示例 33.1，“创建共享内存” 中，`boost::interprocess::read_write` 表示具有读写权限。

在创建类型为 `boost::interprocess::shared_memory_object` 的对象后，操作系统中将创建一个对应的共享内存块。该内存区域的大小初始为 0。要使用该区域，调用 `truncate()` 并传入以字节为单位的共享内存大小。在示例 33.1，“创建共享内存” 中，共享内存为 1,024 字节提供了空间。只有当共享内存以 `boost::interprocess::read_write` 模式打开时，才能调用 `truncate()`。否则，将抛出类型为 `boost::interprocess::interprocess_exception` 的异常。可以多次调用 `truncate()` 来调整共享内存的大小。

在创建共享内存后，可以使用 `get_name()` 和 `get_size()` 等成员函数来查询共享内存的名称和大小。

由于共享内存用于在不同进程之间交换数据，每个进程都需要将共享内存映射到自己的地址空间中。`boost::interprocess::mapped_region` 类用于此操作。可能让你惊讶的是，访问共享内存需要两个类（`boost::interprocess::shared_memory_object` 和 `boost::interprocess::mapped_region`）。这样做是为了让 `boost::interprocess::mapped_region` 类也能用于将其他对象映射到进程的地址空间。

### 示例 33.2. 将共享内存映射到进程的地址空间

```cpp
#include <boost/interprocess/shared_memory_object.hpp>
#include <boost/interprocess/mapped_region.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object shdmem{open_or_create, "Boost", read_write};
  shdmem.truncate(1024);
  mapped_region region{shdmem, read_write};
  std::cout << std::hex << region.get_address() << '\n';
  std::cout << std::dec << region.get_size() << '\n';
  mapped_region region2{shdmem, read_only};
  std::cout << std::hex << region2.get_address() << '\n';
  std::cout << std::dec << region2.get_size() << '\n';
}
```

要使用 `boost::interprocess::mapped_region` 类，请包含头文件 `boost/interprocess/mapped_region.hpp`。必须将类型为 `boost::interprocess::shared_memory_object` 的对象作为第一个参数传递给 `boost::interprocess::mapped_region` 的构造函数。第二个参数决定了对内存区域的访问是只读还是读写。

示例 33.2，“将共享内存映射到进程的地址空间” 创建了两个类型为 `boost::interprocess::mapped_region` 的对象。名为 Boost 的共享内存被两次映射到进程的地址空间。使用成员函数 `get_address()` 和 `get_size()` 将映射内存区域的地址和大小写入标准输出。在两种情况下，`get_size()` 都返回 1024，但每个对象的 `get_address()` 返回值是不同的。

### 注意

示例 33.2，“将共享内存映射到进程的地址空间” 以及随后的某些示例会导致 Visual C++ 2013 和 Boost 1.55.0 出现编译错误。该错误在 ticket 9332 中描述。此错误在 Boost 1.56.0 中已修复。

### 示例 33.3. 在共享内存中写入和读取数字

```cpp
#include <boost/interprocess/shared_memory_object.hpp>
#include <boost/interprocess/mapped_region.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object shdmem{open_or_create, "Boost", read_write};
  shdmem.truncate(1024);
  mapped_region region{shdmem, read_write};
  int *i1 = static_cast<int*>(region.get_address());
  *i1 = 99;
  mapped_region region2{shdmem, read_only};
  int *i2 = static_cast<int*>(region2.get_address());
  std::cout << *i2 << '\n';
}
```

示例 33.3，“在共享内存中写入和读取数字” 使用映射的内存区域写入和读取数字。`region` 将 99 写入共享内存。`region2` 读取共享内存中的相同位置。

### 示例 33.4. 删除共享内存

```cpp
#include <boost/interprocess/shared_memory_object.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  bool removed = shared_memory_object::remove("Boost");
  std::cout << std::boolalpha << removed << '\n';
}
```

要删除共享内存，`boost::interprocess::shared_memory_object` 提供了静态成员函数 `remove()`，它接受要删除的共享内存名称作为参数（参见示例 33.4，“删除共享内存”）。

### 示例 33.5. 使用 Windows 特有的共享内存

```cpp
#include <boost/interprocess/windows_shared_memory.hpp>
#include <boost/interprocess/mapped_region.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  windows_shared_memory shdmem{open_or_create, "Boost", read_write, 1024};
  mapped_region region{shdmem, read_write};
  int *i1 = static_cast<int*>(region.get_address());
  *i1 = 99;
  mapped_region region2{shdmem, read_only};
  int *i2 = static_cast<int*>(region2.get_address());
  std::cout << *i2 << '\n';
}
```

`boost::interprocess::windows_shared_memory` 没有提供 `truncate()` 成员函数。相反，需要将共享内存的大小作为第四个参数传递给构造函数。

尽管 `boost::interprocess::windows_shared_memory` 类不可移植且只能在 Windows 上使用，但当需要与使用这种特殊共享内存的现有 Windows 程序交换数据时，它是非常有用的。

上一节引入了 `boost::interprocess::shared_memory_object` 类，它可以用于创建和管理共享内存。在实践中，该类很少被使用，因为它要求程序从共享内存中直接读写单个字节。C++ 风格倾向于创建类对象，并隐藏数据在内存中存储的位置和方式的细节。

Boost.Interprocess 提供了 `boost::interprocess::managed_shared_memory` 类（该类定义在 `boost/interprocess/managed_shared_memory.hpp` 中），用于支持托管共享内存。该类允许你实例化内存位于共享内存中的对象，使得这些对象对任何访问相同共享内存的程序自动可用。

### 示例 33.6. 使用托管共享内存



```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object::remove("Boost");
  managed_shared_memory managed_shm{open_or_create, "Boost", 1024};
  int *i = managed_shm.construct<int>("Integer")(99);
  std::cout << *i << '\n';
  std::pair<int*, std::size_t> p = managed_shm.find<int>("Integer");
  if (p.first)
    std::cout << *p.first << '\n';
}
```

示例 33.6, “使用托管共享内存” 打开了大小为 1024 字节、名为 `Boost` 的共享内存。如果共享内存不存在，它将被自动创建。

在普通共享内存中，直接访问单个字节来读写数据。托管共享内存使用如 `construct()` 等成员函数，它期望一个类型作为模板参数（在 示例 33.6, “使用托管共享内存” 中为 `int`）。该成员函数期望一个名称来表示在托管内存中创建的对象。示例 33.6, “使用托管共享内存” 使用了名称 `Integer`。

由于 `construct()` 返回一个代理对象，因此可以将参数传递给它以初始化创建的对象。该语法看起来类似于调用构造函数。这确保了对象可以在托管内存中被创建并初始化。

要访问托管内存中的特定对象，可以使用成员函数 `find()`。通过将对象的名称传递给 `find()`，`find()` 将返回对象的指针，或者在未找到给定名称的对象时返回 0。如 示例 33.6, “使用托管共享内存” 所示，`find()` 返回一个类型为 `std::pair` 对象。对象的指针作为成员变量 `first` 提供。示例 33.7, “在共享内存中创建数组” 显示了在 `second` 中接收到的内容。

### 示例 33.7. 在共享内存中创建数组

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object::remove("Boost");
  managed_shared_memory managed_shm{open_or_create, "Boost", 1024};
  int *i = managed_shm.construct<int>("Integer")10;
  std::cout << *i << '\n';
  std::pair<int*, std::size_t> p = managed_shm.find<int>("Integer");
  if (p.first)
  {
    std::cout << *p.first << '\n';
    std::cout << p.second << '\n';
  }
}
```

在 示例 33.7, "在共享内存中创建数组” 中，通过在调用 `construct()` 之后提供方括号括起来的值 `10`，创建了一个包含十个 `int` 类型元素的数组。该相同的 `10` 通过成员变量 `second` 写入标准输出。得益于此成员变量，你可以判断由 `find()` 返回的对象是单个对象还是数组。对于前者，`second` 被设置为 1；而对于后者，`second` 被设置为数组中元素的数量。

请注意，数组中的所有十个元素都用值 99 进行初始化。如果你想用不同的值初始化元素，请传递一个迭代器。如果托管内存中已经存在具有给定名称的对象，则 `construct()` 将失败。在这种情况下，`construct()` 返回 0 且不发生初始化。若要使用已存在的对象，请使用成员函数 `find_or_construct()`，它会返回指向现有对象的指针或创建一个新对象。

还有其他情况会导致 `construct()` 失败。示例 33.8, "异常类型为 `boost::interprocess::bad_alloc` 的异常` 尝试创建一个包含 4096 个元素的 `int` 数组。然而，托管内存只有 1024 字节。这导致抛出了 `boost::interprocess::bad_alloc` 异常。一旦在托管内存中创建了对象，可以使用成员函数 `destroy()` 删除它们。

### 示例 33.8. 异常类型为 `boost::interprocess::bad_alloc` 的异常

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  try
  {
    shared_memory_object::remove("Boost");
    managed_shared_memory managed_shm{open_or_create, "Boost", 1024};
    int *i = managed_shm.construct<int>("Integer")4096;
  }
  catch (boost::interprocess::bad_alloc &ex)
  {
    std::cerr << ex.what() << '\n';
  }
}
```

在 示例 33.9, “在共享内存中移除对象” 中，将删除对象的名称作为唯一参数传递给 `destroy()`。可以检查类型为 `bool` 的返回值来验证对象是否成功找到并删除。因为如果找到对象会被删除，因此返回 `false` 表示未找到给定名称的对象。

成员函数 `destroy_ptr()` 可用于传递托管内存中对象的指针。它也可以用于删除数组。

### 示例 33.9. 在共享内存中移除对象

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object::remove("Boost");
  managed_shared_memory managed_shm{open_or_create, "Boost", 1024};
  int *i = managed_shm.find_or_construct<int>("Integer")(99);
  std::cout << *i << '\n';
  managed_shm.destroy<int>("Integer");
  std::pair<int*, std::size_t> p = managed_shm.find<int>("Integer");
  std::cout << p.first << '\n';
}
```

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/allocators/allocator.hpp>
#include <boost/interprocess/containers/string.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  shared_memory_object::remove("Boost");
  managed_shared_memory managed_shm{open_or_create, "Boost", 1024};
  typedef allocator<char,
    managed_shared_memory::segment_manager> CharAllocator;
  typedef basic_string<char, std::char_traits<char>, CharAllocator> string;
  string *s = managed_shm.find_or_construct<string>("String")("Hello!",
    managed_shm.get_segment_manager());
  s->insert(5, ", world");
  std::cout << *s << '\n';
}
```

为了创建一个在与其所在的同一托管共享内存内存中分配内存的字符串，必须定义相应的类型。新的字符串类型必须使用由 Boost.Interprocess 提供的分配器，而不是标准库提供的默认分配器。

为此，Boost.Interprocess 提供了 `boost::interprocess::allocator` 类，它定义在 `boost/interprocess/allocators/allocator.hpp` 中。通过该类，可以创建一个内部使用托管共享内存的段管理器（segment manager）的分配器。段管理器负责管理托管共享内存块内的内存。使用新创建的分配器，可以定义相应的字符串类型。如上所示，使用 `boost::interprocess::basic_string` 代替 `std::basic_string`。新类型——在示例 33.10, “将字符串放入共享内存”）中被称为 `string`——基于 `boost::interprocess::basic_string`，并通过其分配器访问段管理器。为了让通过调用 `find_or_construct()` 创建的特定 `string` 实例知道它应该访问哪个段管理器，请将相应段管理器的指针作为第二个参数传递给构造函数。

Boost.Interprocess 提供了标准库中许多其他容器的实现。例如，`boost::interprocess::vector` 和 `boost::interprocess::map` 分别定义在 `boost/interprocess/containers/vector.hpp` 和 `boost/interprocess/containers/map.hpp` 中。

请注意，来自 Boost.Container 的容器支持 Boost.Interprocess 并可以放入共享内存。它们可以替代 `boost::interprocess` 中的容器。Boost.Container 引入自第 20 章，*Boost.Container]。当不同的进程访问同一个托管共享内存时，创建、查找和销毁对象等操作会自动同步。如果两个程序尝试在托管共享内存中创建不同名称的对象，访问将相应地进行序列化。要一次性执行多个操作而不被来自不同进程的操作中断，请使用成员函数 `atomic_func()`（参见示例 33.11, “托管共享内存上的原子访问`）。

## 示例 33.11. 托管共享内存上的原子访问

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <functional>
#include <iostream>

using namespace boost::interprocess;

void construct_objects(managed_shared_memory &managed_shm)
{
  managed_shm.construct<int>("Integer")(99);
  managed_shm.construct<float>("Float")(14);
}

int main()
{
  shared_memory_object::remove("Boost");
  managed_shared_memory managed_shm{open_or_create, "Boost", 1024};
  auto atomic_construct = std::bind(construct_objects, std::ref(managed_shm));
  managed_shm.atomic_func(atomic_construct);
  std::cout << *managed_shm.find<int>("Integer").first << '\n';
  std::cout << *managed_shm.find<float>("Float").first << '\n';
}
```

`atomic_func()` 期望的唯一参数是一个无参数且无返回值的函数。传递的函数调用的方式将确保对托管共享内存的排他访问。然而，只有当所有访问托管共享内存的其他进程也使用 `atomic_func()` 时，才能确保排他访问。如果另一个进程拥有托管共享内存内某个对象的指针，它可以使用该指针访问并修改该对象。

Boost.Interprocess 也可以用于同步对象访问。由于 Boost.Interprocess 并不知道在特定时间谁可以访问单个对象，因此需要显式地处理同步。本节将介绍为同步提供的类。

## 同步

Boost.Interprocess 允许多个进程使用共享内存。因为共享内存根据定义在进程之间是共享的，所以 Boost.Interprocess 需要支持某种同步机制。

考虑到同步时，会联想到 C++11 标准库或 Boost.Thread 中的类。但这些类只能用于同步同一进程内的线程；它们不支持不同进程之间的同步。然而，由于两种情况下的挑战是相同的，同步的概念也是相同的。

虽然互斥和条件变量等同步对象在多线程应用程序中位于相同的地址空间，因此对所有线程可见，但共享内存的挑战在于独立进程需要共享这些对象。例如，如果一个进程创建一个互斥锁，它需要某种方式被另一个进程访问。

Boost.Interprocess 提供了两种同步对象：匿名对象直接存储在共享内存中，使得对所有进程自动可用；命名对象由操作系统管理，不存储在共享内存中，可以通过名称引用。

### 示例 33.12. 使用 `boost::interprocess::named_mutex` 命名互斥锁

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/sync/named_mutex.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  managed_shared_memory managed_shm{open_or_create, "shm", 1024};
  int *i = managed_shm.find_or_construct<int>("Integer")();
  named_mutex named_mtx{open_or_create, "mtx"};
  named_mtx.lock();
  ++(*i);
  std::cout << *i << '\n';
  named_mtx.unlock();
}
```

示例 33.12, “使用 `boost::interprocess::named_mutex` 命名互斥锁` 使用 `boost::interprocess::named_mutex` 类创建并使用命名互斥锁，该类定义在 `boost/interprocess/sync/named_mutex.hpp` 中。

`boost::interprocess::named_mutex` 的构造函数期望一个参数来指定是创建还是打开互斥锁，以及互斥锁的名称。任何知道名称的进程都可以打开同一个互斥锁。为了访问共享内存中的数据，程序需要通过调用成员函数 `lock()` 获取互斥锁的所有权。由于互斥锁只能被一个进程拥有，另一个进程可能需要等待直到 `unlock()`()`。一旦进程获得了互斥锁的所有权，它就对互斥锁保护的资源具有排他访问权限。在示例 33.12, “使用 `boost::interprocess::named_mutex` 命名互斥锁`中，资源是一个类型为 `int` 的变量，会被递增并输出到标准输出流。

如果多次启动示例程序，每个实例打印的值都将比上一个值增加 1。得益于互斥锁，不同进程之间对共享内存以及变量本身的访问是同步的。

Example 33.13, “Using an anonymous mutex with `interprocess_mutex`` 使用类型为 `boost::interprocess::interprocess_mutex` 的匿名互斥量，该类型定义在 `boost/interprocess/sync/interprocess_mutex.hpp` 中。为了让所有进程都能访问该互斥量，将其存储在共享内存中。

### Example 33.13. Using an anonymous mutex with `interprocess_mutex`



```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/sync/interprocess_mutex.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  managed_shared_memory managed_shm{open_or_create, "shm", 1024};
  int *i = managed_shm.find_or_construct<int>("Integer")();
  interprocess_mutex *mtx =
    managed_shm.find_or_construct<interprocess_mutex>("mtx")();
  mtx->lock();
  ++(*i);
  std::cout << *i << '\n';
  mtx->unlock();
}
```

Example 33.13, “Using an anonymous mutex with `interprocess_mutex`” 的行为与上一个完全相同。唯一的区别是互斥量，它现在直接存储在共享内存中。这可以通过 `boost::interprocess::managed_shared_memory` 类的成员函数 `construct()` 或 `find_or_construct()` 实现。

除了 `lock()` 之外，`boost::interprocess::named_mutex` 和 `boost::interprocess::interprocess_mutex` 都提供了成员函数 `try_lock()` 和 `timed_lock()`。它们的行为与标准库和 Boost.Thread 中的对应完全一致。如果需要递归互斥量，Boost.Interprocess 提供了两个类：`boost::interprocess::named_recursive_mutex` 和 `boost::interprocess::interprocess_recursive_mutex`。

互斥量保证了对共享资源的独占访问，而条件变量则控制谁在何时拥有独占访问权限。通常，Boost.Interprocess 提供的条件变量工作方式与 C++11 标准库和 Boost.Thread 提供的类似。它们具有类似的接口，使得这些库的用户在 Boost.Interprocess 中使用这些变量时感到非常熟悉。

### Example 33.14. Using a named condition with `boost::interprocess::named_condition`

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/sync/named_mutex.hpp>
#include <boost/interprocess/sync/named_condition.hpp>
#include <boost/interprocess/sync/scoped_lock.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  managed_shared_memory managed_shm{open_or_create, "shm", 1024};
  int *i = managed_shm.find_or_construct<int>("Integer")(0);
  named_mutex named_mtx{open_or_create, "mtx"};
  named_condition named_cnd{open_or_create, "cnd"};
  scoped_lock<named_mutex> lock{named_mtx};
  while (*i < 10)
  {
    if (*i % 2 == 0)
    {
      ++(*i);
      named_cnd.notify_all();
      named_cnd.wait(lock);
    }
    else
    {
      std::cout << *i << std::endl;
      ++(*i);
      named_cnd.notify_all();
      named_cnd.wait(lock);
    }
  }
  named_cnd.notify_all();
  shared_memory_object::remove("shm");
  named_mutex::remove("mtx");
  named_condition::remove("cnd");
}
```

Example 33.14, “Using a named condition with `boost::interprocess::named_condition`” 使用类型为 `boost::interprocess::named_condition` 的条件变量，该类型定义在 `boost/interprocess/sync/named_condition.hpp` 中。由于它是命名变量，因此不需要存储在共享内存中。

应用程序使用 `while` 循环来增加 `int` 类型的变量，该变量存储在共享内存中。虽然变量在每次循环迭代中都会递增，但它每隔一次迭代才会写入标准输出流——即只写入奇数。

每当变量递增 1 时，就会调用条件变量 `named_cnd` 的成员函数 `wait()`。一个锁——在 Example 33.14, “Using a named condition with `boost::interprocess::named_condition`”——被传递给这个成员函数。这是基于在析构函数内部获取互斥量所有权的 RAII 模式。

正如存在两种类型的互斥量（必须存储在共享内存中的匿名类型和命名类型）一样，条件变量也有两种。Example 33.15, “Using an anonymous condition with `interprocess_condition`” 是使用匿名条件变量对上一个示例的重写。

### Example 33.15. Using an anonymous condition with `interprocess_condition`

```cpp
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/sync/interprocess_mutex.hpp>
#include <boost/interprocess/sync/interprocess_condition.hpp>
#include <boost/interprocess/sync/scoped_lock.hpp>
#include <iostream>

using namespace boost::interprocess;

int main()
{
  managed_shared_memory managed_shm{open_or_create, "shm", 1024};
  int *i = managed_shm.find_or_construct<int>("Integer")(0);
  interprocess_mutex *mtx =
    managed_shm.find_or_construct<interprocess_mutex>("mtx")();
  interprocess_condition *cnd =
    managed_shm.find_or_construct<interprocess_condition>("cnd")();
  scoped_lock<interprocess_mutex> lock{*mtx};
  while (*i < 10)
  {
    if (*i % 2 == 0)
    {
      ++(*i);
      cnd->notify_all();
      cnd->wait(lock);
    }
    else
    {
      std::cout << *i << std::endl;
      ++(*i);
      cnd->notify_all();
      cnd->wait(lock);
    }
  }
  cnd->notify_all();
  shared_memory_object::remove("shm");
}
```

示例 33.15, “使用 `interprocess_condition` 使用匿名条件” 的工作方式与上一个完全相同，并且也需要启动两次将 `int` 变量增加十次。

除了互斥锁和条件变量外，Boost.Interprocess 还支持信号量和文件锁。信号量与条件变量类似，区别在于它们不区分两种状态；相反，它们基于计数器。文件锁的行为类似于互斥锁，但它们被用于硬盘上的文件，而不是内存中的对象。

正如 C++11 标准库和 Boost.Thread 区分不同类型的互斥锁和锁一样，Boost.Interprocess 提供了多种互斥锁和锁。例如，互斥锁可以是独占的也可以是非独占的。如果多个进程需要同时读取数据，这将非常有帮助，因为只有在写入数据时才需要独占互斥锁。提供了不同的锁类来将 RAII 模式应用于单个互斥锁上。

除非使用匿名同步对象，否则名称应该是独一无二的。尽管互斥锁和条件变量是基于不同类的对象，但这对于 Boost.Interprocess 封装的依赖于操作系统的接口可能并不一定成立。在 Windows 上，互斥锁和条件变量使用相同的操作系统函数。如果两个对象（每个类型一个）使用相同的名称，程序在 Windows 上的行为将不正确。

# 第七部分：流与文件

以下库有助于处理流和文件的操作：

- `Boost.IOStreams` 提供了远超标准库所提供的流。Boost.IOStreams 允许你访问更多的流，以便从许多不同的源和汇点读写数据。此外，过滤器（filters）能够实现各种操作，例如在读取或写入时对数据进行压缩/解压缩。
- `Boost.Filesystem` 提供了对文件系统的访问。通过 Boost.Filesystem，你可以例如复制文件或遍历目录中的文件。

# 34. Boost.IOStreams

本章介绍了 [Boost.IOStreams](http://www.boost.org/libs/iostreams) 库。Boost.IOStreams 将标准库中著名的流拆分为更小的组件。该库定义了两个概念：`device`（设备），描述数据源和汇点；以及 `stream`（流），描述基于标准库接口的格式化输入/输出接口。由 Boost.IOStreams 定义的流不会自动连接到数据源或汇点。

Boost.IOStreams 提供了这两个概念的众多实现。例如，存在设备 `boost::iostreams::mapped_file`，它可以将文件部分或完全加载到内存中。流 `boost::iostreams::stream` 可以连接到像 `boost::iostreams::mapped_file` 的设备，使用熟悉的流操作符 `operator<<` 和 `operator>>` 来读写数据。

除了 `boost::iostreams::stream` 之外，Boost.IOStreams 还提供了流 `boost::iostreams::filtering_stream`，允许你添加数据过滤器。例如，你可以使用 `boost::iostreams::gzip_compressor` 写入 GZIP 格式压缩的数据。

Boost.IOStreams 还可以用于连接到特定平台的对象。该库提供了连接到 Windows 句柄或文件描述符的设备。通过这种方式，底层 API 的对象可以在平台无关的 C++ 代码中使用。

Boost.IOStreams 提供的类和函数定义在 `boost::iostreams` 命名空间中。没有主头文件。由于 Boost.IOStreams 包含非头文件内容，因此必须经过预编译。这可能很重要，因为取决于 Boost.IOStreams 预编译的方式，某些功能可能会缺失。

## 设备（Devices）

设备是提供对通常进程之外的对象（例如文件）的读写访问的类。然而，你也可以将内部对象（如数组）作为设备。

设备只是具有成员函数 `read()` 或 `write()` 的类。设备可以连接到流，以便你可以读取和写入数据，而不是使用 `read()` 和 `write()` 函数。

### 示例 34.1：使用 `boost::iostreams::array_sink` 使用数组

```cpp
#include <boost/iostreams/device/array.hpp>
#include <boost/iostreams/stream.hpp>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  char buffer[16];
  array_sink sink{buffer};
  stream<array_sink> os{sink};
  os << "Boost" << std::flush;
}
```

示例 34.1，“使用 `boost::iostreams::array_sink` 使用数组作为设备” 使用 `boost::iostreams::array_sink` 向数组写入数据。数组作为 `boost::iostreams::stream` 构造函数的参数。设备类型作为模板参数。示例使用 `operator<<` 将“Boost”写入流。流将数据传递给设备。由于设备连接到数组，“Boost”存储在数组中。由于数组的内容被写入标准输出，当你运行示例时，`Boost` 将显示。

### 示例 34.2：使用 `boost::iostreams::array_source` 使用数组作为设备

```cpp
#include <boost/iostreams/device/array.hpp>
#include <boost/iostreams/stream.hpp>
#include <string>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  char buffer[16];
  array_sink sink{buffer};
  stream<array_sink> os{sink};
  os << "Boost" << std::endl;

  array_source source{buffer};
  stream<array_source> is{source};
  std::string s;
  is >> s;
  std::cout << s << '\n';
}
```

示例 34.2，“使用 `boost::iostreams::array_source` 使用数组作为设备” 基于上一个示例。使用 `boost::iostreams::array_sink` 写入数组的字符串通过 `boost::iostreams::array_source` 读取。

`boost::iostreams::array_source` 的用法类似于 `boost::iostreams::array_sink`。虽然 `boost::iostreams::array_sink` 只支持写入操作，但 `boost::iostreams::array_source` 只支持读取。`boost::iostreams::array` 同时支持读写操作。

请注意，`boost::iostreams::array_source` 和 `boost::iostreams::array_sink` 接收数组的引用。在设备仍使用期间，数组不能被销毁。

### 示例 34.3：使用 `boost::iostreams::back_insert_device` 将 vector 作为设备

使用类型为 `boost::iostreams::back_insert_device` 的设备，而不是 `boost::iostreams::array_sink`。该设备可以将数据写入到任何提供成员函数 `insert()` 的容器中。设备通过调用此成员函数将数据转发到容器。

该示例使用 `boost::iostreams::back_insert_device` 向 `vector` 写入“Boost”。之后，从 `boost::iostreams::array_source` 读取“Boost”。`vector` 的起始地址和大小被作为参数传递给 `boost::iostreams::array_source` 的构造函数。

示例 34.3，“使用 `boost::iostreams::back_insert_device` 将 vector 作为设备” 显示了 `Boost`。



```cpp
#include <boost/iostreams/device/array.hpp>
#include <boost/iostreams/device/back_inserter.hpp>
#include <boost/iostreams/stream.hpp>
#include <vector>
#include <string>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  std::vector<char> v;
  back_insert_device<std::vector<char>> sink{v};
  stream<back_insert_device<std::vector<char>>> os{sink};
  os << "Boost" << std::endl;

  array_source source{v.data(), v.size()};
  stream<array_source> is{source};
  std::string s;
  is >> s;
  std::cout << s << '\n';
}
```

# 示例 34.4. 使用 `boost::iostreams::file_source` 将文件作为设备

使用设备 `boost::iostreams::file_source` 读取文件。虽然之前引入的设备不提供成员函数，但 `boost::iostreams::file_source` 提供了 `is_open()` 来测试文件是否成功打开。它还提供了成员函数 `close()` 来显式关闭文件。你不需要调用 `close()`，因为 `boost::iostreams::file_source` 的析构函数会自动关闭文件。

```cpp
#include <boost/iostreams/device/file.hpp>
#include <boost/iostreams/stream.hpp>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  file_source f{"main.cpp"};
  if (f.is_open())
  {
    stream<file_source> is{f};
    std::cout << is.rdbuf() << '\n';
    f.close();
  }
}
```

除了 `boost::iostreams::file_source`，Boost.IOStreams 还提供了设备 `boost::iostreams::mapped_file_source`，用于将文件部分或完全加载到内存中。`boost::iostreams::mapped_file_source` 定义了一个成员函数 `data()` 来接收相应内存区域的指针。这样，就可以对文件进行随机访问，而不需要顺序读取文件。

对于文件的写访问，Boost.IOStreams 提供了设备 `boost::iostreams::file_sink` 和 `boost::iostreams::mapped_file_sink`。

## 示例 34.5. 使用 `file_descriptor_source` 和 `file_descriptor_sink`

```cpp
#include <boost/iostreams/device/file_descriptor.hpp>
#include <boost/iostreams/stream.hpp>
#include <iostream>
#include <Windows.h>

using namespace boost::iostreams;

int main()
{
  HANDLE handles[2];
  if (CreatePipe(&handles[0], &handles[1], nullptr, 0))
  {
    file_descriptor_source src{handles[0], close_handle};
    stream<file_descriptor_source> is{src};

    file_descriptor_sink snk{handles[1], close_handle};
    stream<file_descriptor_sink> os{snk};

    os << "Boost" << std::endl;
    std::string s;
    std::getline(is, s);
    std::cout << s;
  }
}
```

`boost::iostreams::file_source` 和 `boost::iostreams::file_sink` 使用 `CreatePipe()` 函数创建一个管道。管道的读写端存储在 `handles` 中。`boost::iostreams::file_source` 和 `boost::iostreams::file_sink` 期望两个参数。第一个参数是 Windows 句柄（或者在 POSIX 系统上运行时是文件描述符）。第二个参数必须是 `boost::iostreams::close_handle` 或 `boost::iostreams::never_close`。该参数指定析构函数是否关闭 Windows 句柄。`boost::iostreams::file_source` 和 `boost::iostreams::file_sink` 将“Boost”通过管道发送到标准输出。

## 过滤器

除了设备，Boost.IOStreams 还提供了过滤器，它们在设备之前对读取或写入的数据进行过滤。以下示例使用了 `boost::iostreams::filtering_istream` 和 `boost::iostreams::filtering_ostream`。它们取代了不支持过滤器的 `boost::iostreams::stream`。

### 示例 34.6. 使用 `boost::iostreams::regex_filter`

```cpp
#include <boost/iostreams/device/array.hpp>
#include <boost/iostreams/filtering_stream.hpp>
#include <boost/iostreams/filter/regex.hpp>
#include <boost/regex.hpp>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  char buffer[16];
  array_sink sink{buffer};
  filtering_ostream os;
  os.push(regex_filter{boost::regex{"Bo+st"}, "C++"});
  os.push(sink);
  os << "Boost" << std::flush;
  os.pop();
  std::cout.write(buffer, 3);
}
```

使用设备 `boost::iostreams::array_sink` 向数组写入数据。数据通过类型为 `boost::iostreams::regex_filter` 的过滤器发送，该过滤器会替换字符。过滤器期望一个正则表达式和一个格式字符串。正则表达式描述要替换的内容。格式字符串指定了字符应替换为什么。该示例将“Boost”替换为“C++”。过滤器将匹配“Boost”中一个或多个连续的字母“o”，但不匹配零个。过滤器和设备通过 `boost::iostreams::filtering_ostream` 流连接。该类提供了一个成员函数 `push()`，将过滤器和设备传递给该函数。

过滤器必须在设备之前传递；顺序非常重要。一旦传递了设备，流就完整了，你不能再次调用 `push()`。

`boost::iostreams::regex_filter` 过滤器无法逐字符地处理数据，因为正则表达式需要查看字符组。这就是为什么 `boost::iostreams::regex_filter` 只有在写入操作完成且所有数据可用后才开始过滤。这发生在通过成员函数 `pop()` 将设备从流中移除时。示例 34.6，“使用 `boost::iostreams::regex_filter`”在向流写入“Boost”后调用了 `pop()`。如果没有调用 `pop()`，`boost::iostreams::regex_filter` 将不会处理任何数据，也不会将数据转发到设备。

请注意，你不能使用未连接到设备的流。但是，如果在调用 `pop()` 之后通过 `push()` 添加设备，就可以完成一个流。

示例 34.6，“使用 `boost::iostreams::regex_filter`”显示了 `C++`。

### 示例 34.7. 在 `boost::iostreams::filtering_ostream` 中访问过滤器

```cpp
#include <boost/iostreams/device/array.hpp>
#include <boost/iostreams/filtering_stream.hpp>
#include <boost/iostreams/filter/counter.hpp>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  char buffer[16];
  array_sink sink{buffer};
  filtering_ostream os;
  os.push(counter{});
  os.push(sink);
  os << "Boost" << std::flush;
  os.pop();
  counter *c = os.component<counter>(0);
  std::cout << c->characters() << '\n';
  std::cout << c->lines() << '\n';
}
```

示例 34.7，“在 `boost::iostreams::filtering_ostream` 中访问过滤器”使用了过滤器 `boost::iostreams::counter`，它可以计算字符和行。该类提供了成员函数 `characters()` 和 `lines()`。

`boost::iostreams::filtering_stream` 提供了成员函数 `component()` 来访问过滤器。必须将相应过滤器的索引作为参数传递。由于 `component()` 是模板，过滤器的类型必须作为模板参数传递。`component()` 返回指向过滤器的指针。如果作为模板参数传递了错误的过滤器类型，它将返回 0。

示例 34.7，“在 `boost::iostreams::filtering_ostream` 中访问过滤器”向流写入了五个字符。它没有写入换行符（“\n”）。因此，示例显示了 `5` 和 `0`。

### 示例 34.8. 使用 ZLIB 压缩写入和读取数据

```cpp
#include <boost/iostreams/device/array.hpp>
#include <boost/iostreams/device/back_inserter.hpp>
#include <boost/iostreams/filtering_stream.hpp>
#include <boost/iostreams/filter/zlib.hpp>
#include <vector>
#include <string>
#include <iostream>

using namespace boost::iostreams;

int main()
{
  std::vector<char> v;
  back_insert_device<std::vector<char>> snk{v};
  filtering_ostream os;
  os.push(zlib_compressor{});
  os.push(snk);
  os << "Boost" << std::flush;
  os.pop();

  array_source src{v.data(), v.size()};
  filtering_istream is;
  is.push(zlib_decompressor{});
  is.push(src);
  std::string s;
  is >> s;
  std::cout << s << '\n';
}
```

示例 34.8，“使用 ZLIB 压缩写入和读取数据”使用了过滤器 `boost::iostreams::counter`。

成员函数 `generic_string()` 和 `generic_wstring()` 均以通用格式返回路径。这些是可移植路径；字符串根据 POSIX 标准的规则进行规范化。因此，通用路径与在 Linux 上使用的路径相同。例如，斜杠被用作目录的分符。如果在 Windows 上运行示例 35.3，“从 `boost::filesystem::path` 获取字符串形式路径”，`generic_string()` 和 `generic_wstring()` 都会向标准输出流写入 `C:/Windows/System`。

### 示例 35.3. 从 `boost::filesystem::path` 获取字符串形式路径

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\Windows\\System"};

#ifdef BOOST_WINDOWS_API
  std::wcout << p.native() << '\n';
#else
  std::cout << p.native() << '\n';
#endif

  std::cout << p.string() << '\n';
  std::wcout << p.wstring() << '\n';

  std::cout << p.generic_string() << '\n';
  std::wcout << p.generic_wstring() << '\n';
}
```

返回原生路径的成员函数的返回值取决于程序运行的操作系统。返回通用路径的成员函数的返回值则独立于操作系统。通用路径能够独立于操作系统唯一地标识文件和目录，因此编写平台无关的代码变得简单。

由于 `boost::filesystem::path` 可以用不同的字符串类型初始化，因此提供了多个成员函数以不同的字符串类型检索路径。`string()` 和 `generic_string()` 返回 `std::string` 类型的字符串，而 `wstring()` 和 `generic_wstring()` 返回 `std::wstring` 类型的字符串。

`native()` 的返回类型取决于程序编译的目标操作系统。在 Windows 上，返回类型为 `std::wstring` 的字符串。在 Linux 上，它返回类型为 `std::string` 的字符串。

`boost::filesystem::path` 的构造函数支持通用路径和依赖于平台的路径。在示例 35.3，“从 `boost::filesystem::path` 获取字符串形式路径”中，路径“C:\Windows\System”是 Windows 特有的、不可移植的。请注意，因为反斜杠在 C++ 中是转义字符，所以它本身必须被转义。该路径只有在 Windows 上运行时才能被 Boost.Filesystem 正确识别。在 Linux 等符合 POSIX 标准的操作系统上运行时，此示例调用的所有成员函数将返回 `C:\Windows\System`。由于反斜杠不是 Linux 的通用格式或原生格式分隔符，Boost.Filesystem 不会将该字符识别为文件和目录的分符。

宏 `BOOST_WINDOWS_API` 来自 Boost.System，如果示例在 Windows 上编译会被定义。POSIX 操作系统的相应宏是 `BOOST_POSIX_API`。

### 示例 35.4. 使用可移植路径初始化 `boost::filesystem::path`



```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"/"};
  std::cout << p.string() << '\n';
  std::cout << p.generic_string() << '\n';
}
```

示例 35.4，“使用可移植路径初始化 `boost::filesystem::path`”使用可移植路径来初始化 `boost::filesystem::path`。

由于 `generic_string()` 返回的是可移植路径，其值为斜杠（“/”），与初始化 `boost::filesystem::path` 时使用的相同。然而，成员函数 `string()` 根据平台返回不同的值。在 Windows 和 Linux 上，它都返回 `"/"`。输出相同是因为 Windows 接受斜杠作为目录分隔符，尽管它更倾向于使用反斜杠。

### 示例 35.5. 访问路径的组件

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\Windows\\System"};
  std::cout << p.root_name() << '\n';
  std::cout << p.root_directory() << '\n';
  std::cout << p.root_path() << '\n';
  std::cout << p.relative_path() << '\n';
  std::cout << p.parent_path() << '\n';
  std::cout << p.filename() << '\n';
}
```

`boost::filesystem::path` 提供了多个成员函数来访问路径的某些组件。如果示例 35.5，“访问路径的组件”在 Windows 上执行，`root_name()` 返回 `C:`，`root_directory()` 返回 `\`，`root_path()` 返回 `C:\`，`relative_path()` 返回 `Windows\System`，`parent_path()` 返回 `Windows`，而 `filename()` 返回 `System`。

`boost::filesystem::path` 以依赖于平台的格式存储路径。要检索可移植格式的路径，需要调用 `generic_string()` 等成员函数。

如果示例 35.5，“访问路径的组件”在 Linux 上执行，大多数成员函数将返回空字符串，因为没有根目录或目录。

Boost.Filesystem 提供了额外的成员函数来验证路径是否包含子字符串。这些是：`has_root_name()`、`has_root_directory()`、`has_root_path()`、`has_relative_path()`、`has_parent_path()` 和 `has_filename()`。每个成员函数返回一个 `bool` 值。

还有两个成员函数可以将文件名拆分为组件。只有在 `has_filename()` 返回 `true` 时才调用它们。否则，它们将返回空字符串，因为没有文件名。

### 示例 35.6. 获取文件名和后缀名

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"photo.jpg"};
  std::cout << p.stem() << '\n';
  std::cout << p.extension() << '\n';
}
```

示例 35.6，“获取文件名和后缀名”为 `stem()` 返回 `photo`，为 `extension()` 返回 `.jpg`。

与其通过成员函数访问路径的组件，你还可以遍历组件。

### 示例 35.7. 遍历路径的组件

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\Windows\\System"};
  for (const path &pp : p)
    std::cout << pp << '\n';
}
```

如果在 Windows 上执行，示例 35.7，“遍历路径的组件”将依次输出 `C:`、`/`、`Windows` 和 `System`。在 Linux 上，输出将为 `C:\Windows\System`。

虽然之前的示例介绍了访问路径不同组件的各种成员函数，但示例 35.8，“使用 `operator/=` 拼接路径”使用成员函数来修改路径。

### 示例 35.8. 使用 `operator/=` 拼接路径

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\"};
  p /= "Windows\\System";
  std::cout << p.string() << '\n';
}
```

使用 `operator/=`，示例 35.8，“使用 `operator/=` 拼接路径”将一个路径追加到另一个路径之后。在 Windows 上，程序输出 `C:\Windows\System`。在 Linux 上，输出为 `C:\/Windows\System`，因为斜杠被用作文件和目录的分隔符。斜杠也是 `operator/=` 被重载的原因；毕竟，斜杠是运算符的一部分。

除了 `operator/=` 之外，Boost.Filesystem 还提供了成员函数 `remove_filename()`、`replace_extension()`、`make_absolute()` 和 `make_preferred()` 来修改路径。最后提到的那个成员函数是专门为 Windows 设计的。

### 示例 35.9. 使用 `make_preferred()` 的偏好表示法

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:/Windows/System"};
  std::cout << p.make_preferred() << '\n';
}
```

尽管反斜杠默认用作文件和目录的分隔符，但 Windows 仍然接受斜杠。因此，“C:/Windows/System”是一个合法的原生路径。通过 `make_preferred()`，此类路径可以转换为 Windows 上的偏好表示法。示例 35.9，“使用 `make_preferred()` 的偏好表示法”显示为 `"C:\Windows\System"`。

成员函数 `make_preferred()` 对 Linux 等符合 POSIX 标准的操作没有影响。

请注意，`make_preferred()` 不仅返回转换后的路径，还会修改它所调用的对象。调用后，`p` 包含 `"C:\Windows\System"`。

## 文件和目录

`boost::filesystem::path` 提供的成员函数简单地处理字符串。它们访问路径的各个组件，将路径相互追加等。

为了对硬盘上的物理文件和目录进行操作，还提供了若干独立函数。它们期望一个或多个 `boost::filesystem::path` 类型的参数，并在内部调用操作系统函数。

在引入各种函数之前，了解发生错误时会发生什么是非常重要的。所有函数都会调用可能失败的操作系统函数。因此，Boost.Filesystem 提供了两种变体，它们在发生错误时的行为不同：

- 第一种变体抛出类型为 `boost::filesystem::filesystem_error` 的异常。该类派生自 `boost::system::system_error`，因此符合 Boost.System 框架。
- 第二种变体期望一个类型为 `boost::system::error_code` 的对象作为额外参数。该对象通过引用传递，并在函数调用后进行检查。如果发生失败，该对象将存储相应的错误代码。

`boost::system::system_error` 和 `boost::system::error_code` 在第 55 章“Boost.System”中介绍。除了继承自 `boost::system::system_error` 的接口外，`boost::filesystem::filesystem_error` 还提供了两个名为 `path1()` 和 `path2()` 的成员函数，它们都返回类型为 `boost::filesystem::path` 的对象。由于存在期望两个 `boost::filesystem::path` 类型参数的函数，这两个成员函数为发生错误时获取相应路径提供了一种方法。

示例 35.10，“使用 `boost::filesystem::status()`”引入了 `boost::filesystem::status()`，它可以查询文件或目录的状态。该函数返回一个类型为 `boost::filesystem::file_status` 的对象，可以将其传递给额外的辅助函数进行评估。例如，如果查询的是目录状态，`boost::filesystem::is_directory()` 将返回 `true`。除了 `boost::filesystem::is_directory()` 之外，还有其他函数，包括 `boost::filesystem::is_regular_file()`、`boost::filesystem::is_symlink()` 和 `boost::filesystem::exists()`，它们都返回类型为 `bool` 的值。

### 示例 35.10. 使用 `boost::filesystem::status()`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\"};
  try
  {
    file_status s = status(p);
    std::cout << std::boolalpha << is_directory(s) << '\n';
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

函数 `boost::filesystem::symlink_status()` 查询链接的状态。通过 `boost::filesystem::status()` 查询文件状态。在 Windows 上，符号链接由文件识别。

### 示例 35.11. 使用 `boost::filesystem::file_size()`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\ini"};
  boost::system::error_code ec;
  boost::uintmax_t filesize = file_size(p, ec);
  if (!ec)
    std::cout << filesize << '\n';
  else
    std::cout << ec << '\n';
}
```

一组函数使得查询属性成为可能。`boost::filesystem::file_size()` 返回文件的大小。返回值类型为 `boost::uintmax_t`，即 `unsigned long long`。

示例 35.11，“使用 `boost::filesystem::file_size()`”使用 `boost::system::error_code` 对象，需要进行评估以判断 `boost::filesystem::file_size()` 是否成功。

### 示例 35.12. 使用 `boost::filesystem::last_write_time()`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>
#include <ctime>

using boost::filesystem;

int main()
{
  path p{"C:\\Windows"};
  try
  {
    std::time_t t = last_write_time(p);
    std::cout << std::ctime(&t) << '\n';
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

要确定文件最后修改的时间，可以使用 `boost::filesystem::last_write_time()`（参考示例 35.12，“使用 `boost::filesystem::last_write_time()`”）。

### 示例 35.13. 使用 `boost::filesystem::space()`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\"};
  try
  {
    space_info s = space(p);
    std::cout << s.capacity << '\n';
    std::cout << s.free << '\n';
    std::cout << s.available << '\n';
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

`boost::filesystem::space()` 获取总磁盘空间和剩余空间（参考示例 35.13，“使用 `boost::filesystem::space()`”）。它返回一个类型为 `boost::filesystem::space_info` 的对象，该对象提供了三个公共成员变量：`capacity`、`free` 和 `available`，类型均为 `boost::uintmax_t`。磁盘空间单位为字节。

### 示例 35.14. 创建、重命名和删除目录

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"C:\\Test"};
  try
  {
    if (create_directory(p))
    {
      rename(p, "C:\\Test2");
      boost::filesystem::remove("C:\\Test2");
    }
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

示例 35.14，“创建、重命名和删除目录”应该是不言自明的。仔细观察，可以发现，传递给函数的并不总是 `boost::filesystem::path` 类型的对象，而是一个简单的字符串。这是可能的，因为 `boost::filesystem::path` 有一个非显式的构造函数，它可以将字符串转换为 `boost::filesystem::path` 的对象。这使得使用 Boost.Filesystem 变得简单，因为不需要显式创建路径。

> **注意**
>
> 在示例 35.14，“创建、重命名和删除目录”中，使用命名空间显式调用了 `boost::filesystem::remove()`。否则，Visual C++ 2013 会将该函数与头文件 `stdio.h` 中的 `remove()` 混淆。

其他函数如用于创建符号链接的 `create_symlink()` 以及用于复制文件和目录的 `copy_file()` 和 `copy_directory()`。

### 示例 35.15. 使用 `boost::filesystem::absolute()`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  try
  {
    std::cout << absolute("photo.jpg") << '\n';
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

示例 35.15，“使用 `boost::filesystem::absolute()`”展示了一个根据文件名或路径部分创建绝对路径的函数。显示的路径取决于程序启动时所在的目录。例如，如果程序在 `C:\` 下启动，输出将是 `"C:\photo.jpg"`。



若要获取相对于另一个目录的绝对路径，可以向 `boost::filesystem::absolute()` 传递第二个参数。

### 示例 35.16：创建相对于另一个目录的绝对路径

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  try
  {
    std::cout << absolute("photo.jpg", "D:\\") << '\n';
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

示例 35.16“创建相对于另一个目录的绝对路径”显示了 `"D:\photo.jpg"`。

本节的最后一个示例，示例 35.17“使用 `boost::filesystem::current_path()`”，引入了一个实用的辅助函数来获取当前工作目录。

### 示例 35.17：使用 `boost::filesystem::current_path()`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  try
  {
    std::cout << current_path() << '\n';
    current_path("C:\\");
    std::cout << current_path() << '\n';
  }
  catch (filesystem_error &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

示例 35.17“使用 `boost::filesystem::current_path()`”多次调用了 `boost::filesystem::current_path()`。如果不带参数调用该函数，则返回当前工作目录。如果传递了 `boost::filesystem::path` 类型的对象，则设置当前工作目录。

## 目录迭代器

Boost.Filesystem 提供了迭代器 `boost::filesystem::directory_iterator` 来遍历目录中的文件（参见示例 35.18“遍历目录中的文件”）。

### 示例 35.18：遍历目录中的文件

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p = current_path();
  directory_iterator it(p);
  for (; it != directory_iterator(); ++it)
  {
    std::cout << *it << '\n';
  }
}
```

`directory_iterator` 使用路径初始化。为了获取目录的起始位置，可以使用默认构造函数实例化 `directory_iterator`。在迭代期间可以创建或删除项。为了确保所有项可见，若要递归遍历子目录，Boost.Filesystem 提供了 `boost::filesystem::recursive_directory_iterator`。

## 文件流

标准 `fstream` 中定义了各种文件流。它们接受 `path` 类型。如果你想打开文件，请包含 `filesystem.hpp`。

### 示例 35.19：使用 `boost::filesystem::ofstream`

```cpp
#include <boost/filesystem.hpp>
#include <iostream>

using namespace boost::filesystem;

int main()
{
  path p{"test.txt"};
  ofstream ofs{p};
  ofs << "Hello, world!\n";
}
```

示例 35.19“使用 `boost::filesystem::ofstream`”通过 `boost::filesystem::ofstream` 类打开文件。`boost::filesystem::path` 类型的对象可以传递给 `boost::filesystem::ofstream` 的构造函数。成员函数 `open()` 也接受 `path`。

## 时间

以下库处理时间值：

- Boost.DateTime 定义了时间点和周期（针对当天和日历），以及处理它们的函数。例如，可以对日期进行迭代。
- Boost.Chrono 和 Boost.Timer 提供了测量时间的计时。Boost.Timer 提供的计时用于测量执行时间，仅在优化代码时使用。

# 36. Boost.DateTime

[Boost.DateTime](http://www.boost.org/libs/date_time) 库可以处理日期和时间数据。此外，Boost.DateTime 提供了时区的扩展，并支持日期和时间的格式化输入输出。如果你正在寻找获取当前时间或测量时间的函数，请参见第 37 章 `Boost.Chrono`（[链接](#part0073.html_25JP22-4acad2cb18c04a1fb9fdf6a8cc19f92 "37. Boost.Chrono")）。

## 日期

Boost.DateTime 只支持基于格里祖历的日历日期，这通常不是问题，因为这是最广泛使用的历。如果你与某人约定在 2014 年 5 月 12 日见面，不需要说明该日期是基于格里祖历的。

格里祖历是由教格利利三世引入的。Boost.DateTime 支持 1400 年到 9999 年的日历日期，这意味着它的支持追溯到 1582 年以前。因此，只要将日期转换为格里祖历，你就可以使用 Boost.DateTime 处理 1400 年之后的任何日历日期。为了处理更早的日期，必须扩展 Boost.DateTime。

头文件 `boost/date_time/gregorian/gregorian.hpp` 包含了所有处理日历日期的类和函数的定义。这些函数和类可以在 `boost::gregorian` 命名空间中找到。要创建日期，请使用 `boost::gregorian::date` 类。

`boost::gregorian::date` 提供了几个构造函数来创建日期。最基础的构造函数接受年、月、日作为参数。如果给出无效值，将抛出类型为 `boost::gregorian::bad_day_of_month`、`boost::gregorian::bad_year` 或 `boost::gregorian::bad_month` 的异常。所有类都派生自 `std::out_of_range`。

### 示例 36.1：使用 `boost::gregorian::date` 创建日期

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

int main()
{
  boost::gregorian::date d{2014, 1, 31};
  std::cout << d.year() << '\n';
  std::cout << d.month() << '\n';
  std::cout << d.day() << '\n';
  std::cout << d.day_of_week() << '\n';
  std::cout << d.end_of_month() << '\n';
}
```

如示例 36.1“使用 `boost::gregorian::date` 创建日期”所示，有许多可用的成员函数。某些成员函数（如 `year()`、`month()` 和 `day()`）返回日期的相应部分，而另一些函数（如 `day_of_week()` 和 `end_of_month()`）则计算值。

`boost::gregorian::date` 的构造函数期望年、月、日的数值值来设置日期。然而，示例程序的输出中月份显示为 `Jan`，星期显示为 `Fri`。`month()` 和 `day_of_week()` 的返回值不是普通的数值，而是类型为 `boost::gregorian::date::month_type` 和 `boost::gregorian::date::day_of_week_type` 的值。Boost.DateTime 对格式化的输入输出提供了全面的支持，因此可以调整输出，例如将 `Jan` 调整为 `1`。

`boost::gregorian::date` 的默认构造函数会创建一个无效日期。也可以通过向构造函数传递 `boost::date_time::not_a_date_time` 作为唯一参数来显式创建一个无效日期。

除了直接调用构造函数外，还可以通过其他类的自由函数和成员函数创建 `boost::gregorian::date` 类型的对象。

### 示例 36.2：从时钟或字符串获取日期

示例 36.2“从时钟或字符串获取日期”使用 `boost::gregorian::day_clock` 类，它返回当前日期。成员函数 `universal_day()` 返回 UTC 日期，该日期独立于时区和夏令时。UTC 是世界标准时间的国际缩写。`boost::gregorian::day_clock` 还提供了一个名为 `local_day()` 的成员函数，它考虑了本地设置。要在本地时区内获取当前日期，请使用 `local_day()`。

`boost::gregorian` 命名空间包含一些自由函数，可以将存储为字符串的日期转换为 `boost::gregorian::date` 类型的对象。示例 36.2“从时钟或字符串获取日期”使用函数 `boost::gregorian::date_from_iso_string()` 将 ISO 8601 格式的日期转换。其他函数包括：`boost::gregorian::from_simple_string()` 和 `boost::gregorian::from_us_string()`。

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date d = day_clock::universal_day();
  std::cout << d.year() << '\n';
  std::cout << d.month() << '\n';
  std::cout << d.day() << '\n';

  d = date_from_iso_string("20140131");
  std::cout << d.year() << '\n';
  std::cout << d.month() << '\n';
  std::cout << d.day() << '\n';
}
```

虽然 `boost::gregorian::date` 标记了一个特定的时间，但 `boost::gregorian::date_duration` 表示一个时长。

### 示例 36.3：使用 `boost::gregorian::date_duration`

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date d1{2014, 1, 31};
  date d2{2014, 2, 28};
  date_duration dd = d2 - d1;
  std::cout << dd.days() << '\n';
}
```

由于 `boost::gregorian::date` 重载了 `-` 运算符，可以减去时间点（参见示例 36.3“使用 `boost::gregorian::date_duration`”）。`boost::gregorian::date_duration` 提供的最重要的成员函数是 `days()`。

### 示例 36.4：特殊时长

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date_duration dd{4};
  std::cout << dd.days() << '\n';
  weeks ws{4};
  std::cout << ws.days() << '\n';
  months ms{4};
  std::cout << ms.days() << '\n';
  years ys{4};
  std::cout << ys.days() << '\n';
}
```

`boost::gregorian::date_duration` 也可以通过向构造函数传递天数来创建。要创建涉及 `weeks`、`months` 或 `years` 的时长，请使用示例 36.4“特殊时长”。无论是 `boost::gregorian::date` 还是 `boost::gregorian::date_duration` 允许你确定天数，因为月份和年份的长度不同。尽管，使用这些类仍然意义，参见示例 36.5“处理特殊时长”。

### 示例 36.5：处理特殊时长

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date d{2014, 1, 31};
  months ms{1};
  date d2 = d + ms;
  std::cout << d2 << '\n';
  date d3 = d2 - ms;
  std::cout << d3 << '\n';
}
```

示例 36.5“处理特殊时长”向给定的 2014 年 1 月 31 日日期增加一个月，导致 `d2` 为 2014 年 2 月 28 日。在下一步中，减去一个月，`d3` 再次变为 2014 年 1 月 31 日。如所示，时间点和时长都可以使用。然而，某些细节需要考虑。例如，从一个月的最后一天开始，`boost::gregorian::months` 总是到达另一个月份的最后一天，这可能会导致意外。

### 示例 36.6：处理特殊时长时的意外

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date d{2014, 1, 30};
  months ms{1};
  date d2 = d + ms;
  std::cout << d2 << '\n';
  date d3 = d2 - ms;
  std::cout << d3 << '\n';
}
```

示例 36.6“处理特殊时长时的意外”与上一个相同，只是 `d` 初始化为 2014 年 1 月 30 日。尽管这不是 1 月的最后一天，向前移动一个月会导致 `d2` 变为 2014 年 2 月 28 日，因为没有 2 月 30 日。然而，再次向后移动一个月会导致 `d3` 变为 2014 年 1 月 31 日。由于 2014 年 2 月 28 日是 2 月的最后一天，向后移动返回到了 1 月的最后一天。

要更改此行为，请取消定义宏 `BOOST_DATE_TIME_OPTIONAL_GREGORIAN_TYPES`。在此宏被取消定义后，`boost::gregorian::weeks`、`boost::gregorian::months` 和 `boost::gregorian::years` 类将不再可用。唯一可用的类将是 `boost::gregorian::date_duration`，它简单地按指定的天数向前或后跳转，而不会对月份的第一天和最后一天进行特殊考虑。

### 示例 36.7：使用 `boost::gregorian::date_period`

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date d1{2014, 1, 1};
  date d2{2014, 2, 28};
  date_period dp{d1, d2};
  date_duration dd = dp.length();
  std::cout << dd.days() << '\n';
}
```

虽然 `boost::gregorian::date_duration` 仅适用于持续时间，但 `boost::gregorian::date_period` 支持两个日期之间的范围。



`boost::gregorian::date_period` 的构造函数可以接受两种输入。你可以传递两个类型为 `boost::gregorian::date` 的参数，一个作为起始日期，一个作为结束日期。或者你可以指定起始日期和一个类型为 `boost::gregorian::date_duration` 的持续时间。请注意，结束日期的前一天实际上是该周期的最后一天。这对于理解示例 36.8“测试周期是否包含日期”的输出非常重要。

### 示例 36.8 测试周期是否包含日期

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::gregorian;

int main()
{
  date d1{2014, 1, 1};
  date d2{2014, 2, 28};
  date_period dp{d1, d2};
  std::cout.setf(std::ios::boolalpha);
  std::cout << dp.contains(d1) << '\n';
  std::cout << dp.contains(d2) << '\n';
}
```

示例 36.8“测试周期是否包含日期”通过调用 `contains()` 来检查特定日期是否在周期内。注意，尽管 `d2` 定义了周期的结束，但它并不被视为周期的一部分。因此，成员函数 `contains()` 在调用 `d1` 时返回 `true`，在调用 `d2` 时返回 `false`。

`boost::gregorian::date_period` 提供了额外的成员函数用于操作，例如移动周期或计算两个重叠周期的交集。

Boost.DateTime 还提供了迭代器和其他实用的自由函数，如示例 36.9“遍历日期”所示。

使用迭代器 `boost::gregorian::day_iterator` 从特定日期向前或向后跳转一天。使用 `boost::gregorian::week_iterator`、`boost::gregorian::month_iterator` 和 `boost::gregorian::year_iterator` 分别按周、月或年跳转。

示例 36.9“遍历日期”还使用了函数 `boost::date_time::next_weekday()`，它根据给定的日期返回下一个工作日的日期。示例 36.9“遍历日期”显示了 `2014-May-16`，这是 2014 年 5 月 13 日之后的第一个周五。

### 示例 36.9 遍历日期

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost;

int main()
{
  gregorian::date d{2014, 5, 12};
  gregorian::day_iterator it{d};
  std::cout << *++it << '\n';
  std::cout << date_time::next_weekday(*it,
    gregorian::greg_weekday(date_time::Friday)) << '\n';
}
```

## 与位置无关的时间

`boost::posix_time::ptime` 类定义了一个与位置无关的时间。它使用了类型 `boost::gregorian::date`，但也存储了时间。要使用 `boost::posix_time::ptime`，请包含头文件 `boost/date_time/posix_time/posix_time.hpp`。

### 示例 36.10 使用 `boost::posix_time::ptime`

```cpp
#include <boost/date_time/posix_time/posix_time.hpp>
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  ptime pt{2014, 5, 12}, time_duration{12, 0, 0};
  date d = pt.date();
  std::cout << d << '\n';
  time_duration td = pt.time_day();
  std::cout << td << '\n';
}
```

要初始化 `boost::posix_time::ptime` 对象，传递一个类型为 `boost::gregorian::date` 的日期和一个类型为 `boost::posix_time::time_duration` 的持续时间。示例 36.10“使用 `boost::posix_time::ptime`”指定了 5 月 12 日 12 点。要查询日期和时间，使用成员函数 `date()` 和 `time_day()`。`boost::gregorian::date` 的构造函数创建了一个无效的日期，`boost::posix_time::time_duration` 也是。`boost::posix_time::ptime` 提供了创建日期的自由函数。

### 示例 36.11 使用时钟创建时间点

```cpp
#include <boost/date_time/posix_time/posix_time.hpp>
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>

using namespace boost::posix_time;

int main()
{
  ptime pt = second_clock::universal_time();
  std::cout << pt.date() << '\n';
  std::cout << pt.time_day() << '\n';

  pt = from_iso_string("20140512T120000");
  std::cout << pt.date() << '\n';
  std::cout << pt.time_day() << '\n';
}
```

`boost::posix_time::second_clock` 返回当前时间。成员函数 `universal_time()` 返回 UTC 时间（参见示例 36.11“使用时钟创建时间点”）。`local_time()` 返回本地时间。如果你需要更高的分辨率，`boost::posix_time::microsec_clock` 返回包含微秒的时间。

自由函数 `boost::posix_time::from_iso_string()` 将使用 ISO 8601 标准格式的字符串转换为 `boost::posix_time::ptime` 对象。

### 示例 36.12 使用 `boost::posix_time::time_duration`

```cpp
#include <boost/date_time/posix_time/posix_time.hpp>
#include <iostream>

using namespace boost::posix_time;

int main()
{
  time_duration td{16, 30, 0};
  std::cout << td.hours() << '\n';
  std::cout << td.minutes() << '\n';
  std::cout << td.seconds() << '\n';
  std::cout << td.total_seconds() << '\n';
}
```

Boost.DateTime 还提供了 `boost::posix_time::time_duration` 类，它指定了一个持续时间。这个类之前被提到过，因为 `boost::posix_time::ptime` 的构造函数的第二个参数期望一个类型为 `boost::posix_time::time_duration` 的对象。你也可以独立使用 `boost::posix_time::time_duration`。

`hours()`、`minutes()` 和 `seconds()` 返回持续时间的各个部分，而 `total_seconds()`（返回总秒数）等成员函数提供了额外信息（参见示例 36.12“使用 `boost::posix_time::time_duration`”）。传递 `boost::posix_time::time_duration` 的值没有上限限制（例如 24 小时）。

### 示例 36.13 处理时间点

```cpp
#include <boost/date_time/posix_time/posix_time.hpp>
#include <iostream>

using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  ptime pt1{date{2014, 5, 12}, time_duration{12, 0, 0}};
  ptime pt2{date{2014, 5, 12}, time_duration{18, 30, 0}};
  time_duration td = pt2 - pt1;
  std::cout << td.hours() << '\n';
  std::cout << td.minutes() << '\n';
  std::cout << td.seconds() << '\n';
}
```

与日历日期一样，时间点和持续时间也可以进行计算。如果两个类型为 `boost::posix_time::ptime` 的时间相互相减，如示例 36.13“处理时间点”所示，结果是一个 `boost::posix_time::time_duration` 类型的对象，指定了两个时间之间的持续时间。

### 示例 36.14 处理持续时间

```cpp
#include <boost/date_time/posix_time/posix_time.hpp>
#include <iostream>

using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  ptime pt1{date{2014, 5, 12}, time_duration{12, 0, 0}};
  time_duration td{6, 30, 0};
  ptime pt2 = pt1 + td;
  std::cout << pt2.time_of_day() << '\n';
}
```

如示例 36.14“处理持续时间”所示，可以将持续时间加到时间上，得到一个新的时间点。此示例向标准输出流写入 `18:30:00`。

Boost.DateTime 对日历日期和时间使用了相同的概念。就像存在用于时间和持续时间的类一样，也存在表示时间段（periods）的类。对于日历日期，是 `boost::gregorian::date_period`；对于时间，是 `boost::posix_time::time_period`。这两个类的构造函数都期望两个参数：`boost::gregorian::date_period` 期望两个日历日期作为参数，而 `boost::posix_time::time_period` 期望两个时间点。

### 示例 36.15 使用 `boost::posix_time::time_period`

```cpp
#include <boost/date_time/posix_time/posix_time.hpp>
#include <iostream>

using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  ptime pt1{date{2014, 5, 12}, time_duration{12, 0, 0}};
  ptime pt2{date{2014, 5, 12}, time_duration{18, 30, 0}};
  time_period tp{pt1, pt2};
  std::cout.setf(std::ios::boolalpha);
  std::cout << tp.contains(pt1) << '\n';
  std::cout << tp.contains(pt2) << '\n';
}
```

一般而言，`boost::posix_time::time_period` 的工作方式类似于 `boost::gregorian::date_period`。它提供了一个成员函数 `contains()`，对于时间段内的每个时间点都返回 `true`。由于传递给 `boost::posix_time::time_period` 构造函数的结束时间不属于时间段的一部分，因此在示例 36.15“使用 `boost::posix_time::time_period`”中第二次调用 `contains()` 返回 `false`。

`boost::posix_time::time_period` 还提供了额外的成员函数，如 `intersection()` 和 `merge()`，它们分别计算两个重叠时间段的交集并合并两个交叉的时间段。

最后，迭代器 `boost::posix_time::time_iterator` 用于遍历时间点。

示例 36.16“遍历时间点”使用迭代器 `it` 从时间 `pt` 向前跳转 6.5 小时。因为迭代器增加了两次，输出为 `2014-May-12 18:30:00` 和 `2014-May-13 01:00:00`。

### 示例 36.16 遍历时间点

```cpp
#include <boost/date_time/local_time/local_time.hpp>
#include <iostream>

using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  ptime pt1{date{2014, 5, 12}, time_duration{12, 0, 0}};
  ptime pt2{date{2014, 5, 12}, time_duration{18, 30, 0}};
  time_period tp{pt1, pt2};
  std::cout.setf(std::ios::boolalpha);
  std::cout << tp.contains(pt1) << '\n';
  std::cout << tp.contains(pt2) << '\n';
}
```

## 依赖位置的时间

与上一节介绍的与位置无关的时间不同，依赖位置的时间考虑了时区。Boost.DateTime 提供了 `boost::local_time::local_date_time`，它定义在 `boost/time/local_time.hpp` 中。

### 示例 36.17 使用 `boost::local_time::local_time`

时区为 Europe。

```cpp
#include <boost/date_time/local_time/local_time.hpp>
#include <iostream>

using namespace boost::local_time;
using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  time_zone_ptr tz{new posix_time_zone{"CET+1"}};
  ptime pt{date{2014, 5, 12}, time_duration{12, 0, 0}};
  local_date_time dt{pt, tz};
  std::cout << dt.local_time() << '\n';
  std::cout << dt << '\n';
  std::cout << dt.zone_name() << '\n';
}
```

`boost::local_time::local_date_time` 的构造函数期望第一个参数为 `boost::posix_time::ptime` 类型，第二个参数为 `boost::local_time::time_zone_ptr` 类型。

Boost.DateTime 提供了 `boost::local_time::local_date_time`，它定义在 `boost/date_time/local_time.hpp` 中。当 `boost::local_time::local_date_time` 对象被写入标准输出流或调用成员函数 `local_time()` 时，会使用小时偏移量来计算本地时间。由于 CET 比 UTC 早一小时，偏移量表示为 +1。Boost.DateTime 无法解释时区缩写，因此必须提供小时偏移量；如果没有偏移量，请使用值 +0。

示例 36.17“使用 `boost::local_time::local_time`”。



程序向标准输出流写入了字符串 `2014-May-12 12:00:00`、`2014-May-12 13:00:00 CET`、`2014-May-12 13:00:00` 和 `CET`。用于初始化 `boost::posix_time::ptime` 和 `boost::local_time::local_date_time` 对象的值始终与时区相关。

### 示例 36.18. 依赖位置的时间点和不同的时区

```cpp
#include <boost/date_time/local_time/local_time.hpp>
#include <iostream>

using namespace boost::local_time;
using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  time_zone_ptr tz{new posix_time_zone{"CET+1"}};

  ptime pt{date{2014, 5, 12}, time_duration{12, 0, 0}};
  local_date_time dt{pt, tz};
  std::cout << dt.local_time() << '\n';

  time_zone_ptr tz2{new posix_time_zone{"EET+2"}};
  std::cout << dt.local_time_in(tz2).local_time() << '\n';
}
```

使用 `local_time()` 时，会遵循时区的偏移。为了计算 CET（欧洲中部标准时间）时间，需要在存储在 `dt` 中的 UTC 时间 12 PM 基础上加一小时，因为 CET 比 UTC 早一小时。这就是为什么在示例 36.18“依赖位置的时间点和不同的时区”中，`local_time()` 向标准输出写入了 `2014-May-12 13:00:00`。

相比之下，成员函数 `local_time_in()` 将存储在 `dt` 中的时间解释为作为参数传递的时区中的时间。这意味着 UTC 12 PM 等于 EET 2 PM（EET 代表东欧时间，它比 UTC 早两小时）。

最后，Boost.DateTime 提供了 `boost::local_time::local_time_period` 类用于处理依赖位置的周期。

### 示例 36.19. 使用 `boost::local_time::local_time_period`

```cpp
#include <boost/date_time/local_time/local_time.hpp>
#include <iostream>

using namespace boost::local_time;
using namespace boost::posix_time;
using namespace boost::gregorian;

int main()
{
  time_zone_ptr tz{new posix_time_zone{"CET+0"}};

  ptime pt1{date{2014, 12, 5}, time_duration{12, 0, 0}};
  local_date_time dt1{pt1, tz};

  ptime pt2{date{2014, 12, 5}, time_duration{18, 0, 0}};
  local_date_time dt2{pt2, tz};

  local_time_period tp{dt1, dt2};

  std::cout.setf(std::ios::boolalpha);
  std::cout << tp.contains(dt1) << '\n';
  std::cout << tp.contains(dt2) << '\n';
}
```

示例 36.19“使用 `boost::local_time::local_time_period`”中的 `boost::local_time::local_time_period` 构造函数期望两个类型为 `boost::local_time::local_date_time` 的参数。与其他提供的用于周期的类型一样，代表结束时间的第二个参数并不属于该周期的一部分。通过 `contains()`、`intersection()`、`merge()` 等成员函数的帮助，你可以基于 `boost::local_time::local_time_period` 对周期进行处理。

## 格式化的输入和输出

本章在此为止描述的示例程序以 `2014-May-12` 的格式写入结果。Boost.DateTime 允许用不同的格式显示结果。可以使用 `boost::date_time::date_facet` 和 `boost::date_time::time_facet` 对日历日期和时间进行格式化。

Boost.DateTime 使用标准库中的区域（locales）概念。要格式化日历日期，必须创建一个类型为 `boost::date_time::date_facet` 的对象并将其安装到区域中。描述新格式的字符串传递给 `boost::date_time::date_facet` 的构造函数。示例 36.20“用户自定义的日期格式”传递了 “%A, %d %B %Y”，这指定了星期后面跟着全称月份日期：`Monday, 12 May 2014`。

### 示例 36.20. 用户自定义的日期格式

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>
#include <locale>

using namespace boost::gregorian;

int main()
{
  date d{2014, 5, 12};
  date_facet *df = new date_facet{"%A, %d %B %Y"};
  std::cout.imbue(std::locale{std::cout.getloc(), df});
  std::cout << d << '\n';
}
```

Boost.DateTime 提供了许多格式标志，每个标志由一个百分号后跟一个字符组成。Boost.DateTime 的文档包含了[所有支持标志的完整概述](http://www.boost.org/doc/html/date_time/date_time_io.html#date_time.format_flags)。

如果程序被德国或德语国家的人使用，那么使用德语而非英语来显示星期和月份会更好。

通过将包含所需名称的向量（vectors）传递给类 `boost::date_time::date_facet` 的成员函数 `long_month_names()` 和 `long_weekday_names()`，可以更改星期和月份名称。示例 36.21“更改星期和月份名称”现在写入了 `Montag, 12 May 2014`（注：原文为德语，此处意指德语格式）。在标准输出中写入 `Montag, 12 Mai 2014`。

### 注意

为了在标准输出中写入 `Montag, 12 Mai 2014`，请将示例 36.21 替换为“de_DE”，并确保安装了德语区域。

### 示例 36.21. 更改星期和月份名称

```cpp
#include <boost/date_time/gregorian/gregorian.hpp>
#include <iostream>
#include <locale>
#include <vector>
#include <string>

using namespace boost::gregorian;

int main()
{
  date d{2014, 5, 12};
  date_facet *df = new date_facet{"%A, %d %B %Y"};
  std::cout.imbue(std::locale{std::cout.getloc(), df});
  std::cout << d << '\n';
}
```

# 37. Boost.Chrono

[Boost.Chrono](http://www.boost.org/doc/libs/chrono/) 提供了多种时钟。例如，你可以获取当前时间或测量通过的时间。Boost.Chrono 的部分被添加到 C++11。如果你的开发环境支持 C++11，你可以使用某些时钟。

通过头文件 `boost/chrono.hpp` 可以访问 Boost.Chrono 时钟。唯一的扩展是自定义格式化，它需要头文件 `boost/chrono_io.hpp`。

示例 37.1“Boost.Chrono 的所有时钟”介绍了 Boost.Chrono 提供的所有时钟。所有时钟都有一个返回时间点的成员函数 `now()`。所有时间点都相对于一个通用时间点。这个参考点被称为 epoch。常用的 epoch 是 1970 年 1 月 1 日。示例 37.1“Boost.Chrono 的所有时钟”为显示的每个时间点写入了 epoch。

### 示例 37.1. Boost.Chrono 的所有时钟

```cpp
#include <boost/chrono.hpp>
#include <iostream>

using namespace boost::chrono;

int main()
{
  std::cout << system_clock::now() << '\n';
#ifdef BOOST_CHRONO_HAS_CLOCK_STEADY
  std::cout << steady_clock::now() << '\n';
#endif
  std::cout << high_resolution_clock::now() << '\n';

#ifdef BOOST_CHRONO_HAS_PROCESS_CLOCKS
  std::cout << process_real_cpu_clock::now() << '\n';
  std::cout << process_user_cpu_clock::now() << '\n';
  std::cout << process_system_cpu_clock::now() << '\n';
  std::cout << process_cpu_clock::now() << '\n';
#endif

#ifdef BOOST_CHRONO_HAS_THREAD_CLOCK
  std::cout << thread_clock::now() << '\n';
#endif
}
```

- `boost::chrono::system_clock` 返回系统时间。这通常是你电脑桌面上显示的时间。如果你更改了电脑时间，`boost::chrono::system_clock` 将返回新时间。示例 37.1“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`13919594042183544 [1/10000000]seconds since Jan 1, 1970`。

  `boost::chrono::system_clock` 的起始时间（epoch）并没有标准。这些示例中使用的 1970 年 1 月 1 日起始时间取决于实现。但是，如果你特别想获取自 1970 年 1 月 1 日以来的时间，请调用 `to_time_t()`。`to_time_t()` 是一个静态成员函数，它以 `std::time_t` 类型返回自 1970 年 1 月 1 日以来的秒数作为当前系统时间。

- `boost::chrono::steady_clock` 是一种在稍后访问时总是返回更晚时间的时钟。即使电脑上的时间被调回，`boost::chrono::steady_clock` 也会返回更晚的时间。这种时间被称为单调时间（monotonic time）。示例 37.1“来自 Boost.Chrono 的所有时”显示自系统启动以来的纳秒数。消息如下：`10594369282958 nanoseconds since boot`。`boost::chrono::steady_clock` 测量自上次启动以来的经过时间。然而，从上次启动开始测量是一个实现细节。参考点可能会随着不同的实现而改变。

  `boost::chrono::steady_clock` 并不是所有平台都支持。只有在定义了宏 `BOOST_CHRONO_HAS_CLOCK_STEADY` 时，该时钟可用。

- `boost::chrono::high_resolution_clock` 是 `boost::chrono::system_clock` 或 `boost::chrono::steady_clock` 的类型定义，取决于哪个时钟测量时间更精确。因此，其输出与 `boost::chrono::high_resolution_clock` 所基于的时钟的输出相同。

- `boost::chrono::process_real_cpu_clock` 返回进程运行运行的 CPU 时间。该时钟测量自程序开始以来的时间。示例 37.1“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`1000000 nanoseconds since process start-up`。

  你也可以使用 `ctime` 中的 `std::clock()` 获取此时间。事实上，`boost::chrono::process_real_cpu_clock` 的当前实现是基于 `std::clock()` 的。

  只有在定义了宏 `BOOST_CHRONO_HAS_PROCESS_CLOCKS` 时，才能使用 `boost::chrono::process_real_cpu_clock` 时钟和其他测量 CPU 时间的时钟。

- `boost::chrono::process_user_cpu_clock` 返回进程在用户空间花费的 CPU 时间。用户空间指的是独立于操作系统函数运行的代码。在程序调用的操作系统函数中执行代码所需的时间不计入用户空间时间。

  `boost::chrono::process_user_cpu_clock` 仅返回在用户空间运行花费的时间。如果程序暂停一段时间（例如通过 Windows 的 `Sleep()` 函数），在 `Sleep()` 中花费的时间不会被 `boost::chrono::process_user_cpu_clock` 测量。

  示例 37.1“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`15600100 nanoseconds since process start-up`。

- `boost::chrono::process_system_cpu_clock` 与 `boost::chrono::process_user_cpu_clock` 。然而，此时钟测量在内核空间花费的时间。`boost::chrono::process_system_cpu_clock` 返回进程执行操作系统函数花费的 CPU 时间。

  示例 37.1“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`0 nanoseconds since process start-up`。由于此示例没有直接调用操作系统函数，且 Boost.Chrono 只使用了少数操作系统函数，`boost::chrono::process_system_cpu_clock` 可能返回 0。

- `boost::chrono::process_cpu_clock` 返回一个元组，包含由 `boost::chrono::process_real_cpu_clock`、`boost::chrono::process_user_cpu_clock` 和 `boost::chrono::process_system_cpu_clock` 返回的 CPU 时间。示例 37.1“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`1000000 nanoseconds since process start-up`。

- `boost::chrono::steady_clock` 是一种在稍后访问时总是返回更晚时间的时钟。即使电脑上的时间被调回，`boost::chrono::steady_clock` 也会返回更晚的时间。这种时间被称为单调时间。示例 37.1“来自 Boost.Chrono 的所有时”显示自系统启动以来的纳秒数。消息如下：`10594369282958 nanoseconds since boot`。`boost::chrono::steady_clock` 测量自上次启动以来的时间。然而，从上次启动开始测量是一个实现细节。参考点可能会随着不同的实现而改变。

  `boost::chrono::steady_clock` 并不是所有平台都支持。只有在定义了宏 `BOOST_CHRONO_HAS_CLOCK_STEADY` 时，该时钟可用。

- `boost::chrono::high_resolution_clock` 是 `boost::chrono::system_clock` 或 `boost::chrono::steady_clock` 的类型定义，取决于哪个时钟测量时间更精确。因此，其输出与 `boost::chrono::high_resolution_clock` 所基于的时钟的输出相同。

- `boost::chrono::process_real_cpu_clock` 返回进程运行的 CPU 时间。该时钟测量自程序开始以来的时间。示例 37.1“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`1000000 nanoseconds since start-up`。



你也可以使用 `ctime` 中的 `std::clock()` 获取此时间。事实上，`boost::chrono::process_real_cpu_clock` 的当前实现是基于 `std::clock()` 的。

只有在定义了宏 `BOOST_CHRONO_HAS_PROCESS_CLOCKS` 时，才能使用 `boost::chrono::process_real_cpu_clock` 时钟和其他测量 CPU 时间的时钟。

- `boost::chrono::process_user_cpu_clock` 返回进程在用户空间花费的 CPU 时间。用户空间指的是独立于操作系统函数运行的代码。在程序调用的操作系统函数中执行代码所需的时间不计入用户空间时间。

  `boost::chrono::process_user_cpu_clock` 仅返回在用户空间运行花费的时间。如果程序暂停一段时间（例如通过 Windows 的 `Sleep()` 函数），在 `Sleep()` 中花费的时间不会被 `boost::chrono::process_user_cpu_clock` 测量。

  示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`15600100 nanoseconds since process start-up`。

- `boost::chrono::process_system_cpu_clock` 与 `boost::chrono::process_user_cpu_clock` 相似。然而，此时钟测量在内核空间花费的时间。`boost::chrono::process_system_cpu_clock` 返回进程执行操作系统函数花费的 CPU 时间。

  示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`0 nanoseconds since process start-up`。由于此示例没有直接调用操作系统函数，且 Boost.Chrono 只使用了少数操作系统函数，`boost::chrono::process_system_cpu_clock` 可能返回 0。

- `boost::chrono::process_cpu_clock` 返回一个元组，包含由 `boost::chrono::process_real_cpu_clock`、`boost::chrono::process_user_cpu_clock` 和 `boost::chrono::process_system_cpu_clock` 返回的 CPU 时间。示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`1000000 nanoseconds since process start-up`。

- `boost::chrono::system_clock` 返回系统时间。这通常是你电脑桌面上显示的时间。如果你更改了电脑时间，`boost::chrono::system_clock` 将返回新时间。示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`13919594042183544 [1/10000000]seconds since Jan 1, 1970`。

  `boost::chrono::system_clock` 的起始时间（epoch）并没有标准。这些示例中使用的 1970 年 1 月 1 日起始时间取决于实现。但是，如果你特别想获取自 1970 年 1 月 1 日以来的时间，请调用 `to_time_t()`。`to_time_t()` 是一个静态成员函数，它以 `std::time_t` 类型返回自 1970 年 1 月 1 日以来的秒数作为当前系统时间。

- `boost::chrono::steady_clock` 是一种在稍后访问时总是返回更晚时间的时钟。即使电脑上的时间被调回，`boost::chrono::steady_clock` 也会返回更晚的时间。这种时间被称为单调时间。示例 37.1，“来自 Boost.Chrono 的所有时”显示自系统启动以来的纳秒数。消息如下：`10594369282958 nanoseconds since boot`。`boost::chrono::steady_clock` 测量自上次启动以来的时间。然而，从上次启动开始测量是一个实现细节。参考点可能会随着不同的实现而改变。

  `boost::chrono::steady_clock` 并不是所有平台都支持。只有在定义了宏 `BOOST_CHRONO_HAS_CLOCK_STEADY` 时，该时钟可用。

- `boost::chrono::high_resolution_clock` 是 `boost::chrono::system_clock` 或 `boost::chrono::steady_clock` 的类型定义，取决于哪个时钟测量时间更精确。因此，其输出与 `boost::chrono::high_resolution_clock` 所基于的时钟的输出相同。

- `boost::chrono::process_real_cpu_clock` 返回进程运行的 CPU 时间。该时钟测量自程序开始以来的时间。示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`1000000 nanoseconds since process start-up`。

  你也可以使用 `ctime` 中的 `std::clock()` 获取此时间。事实上，`boost::chrono::process_real_cpu_clock` 的当前实现是基于 `std::clock()` 的。

  只有在定义了宏 `BOOST_CHRONO_HAS_PROCESS_CLOCKS` 时，才能使用 `boost::chrono::process_real_cpu_clock` 时钟和其他测量 CPU 时间的时钟。

- `boost::chrono::process_user_cpu_clock` 返回进程在用户空间花费的 CPU 时间。用户空间指的是独立于操作系统函数运行的代码。在程序调用的操作系统函数中执行代码所需的时间不计入用户空间时间。

  `boost::chrono::process_user_cpu_clock` 仅返回在用户空间运行花费的时间。如果程序暂停一段时间（例如通过 Windows 的 `Sleep()` 函数），在 `Sleep()` 中花费的时间不会被 `boost::chrono::process_user_cpu_clock` 测量。

  示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`15600100 nanoseconds since process start-up`。

- `boost::chrono::process_system_cpu_clock` 与 `boost::chrono::process_user_cpu_clock` 相似。然而，此时钟测量在内核空间花费的时间。`boost::chrono::process_system_cpu_clock` 返回进程执行操作系统函数花费的 CPU 时间。

  示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`0 nanoseconds since process start-up`。由于此示例没有直接调用操作系统函数，且 Boost.Chrono 只使用了少数操作系统函数，`boost::chrono::process_system_cpu_clock` 可能返回 0。

- `boost::chrono::process_cpu_clock` 返回一个元组，包含由 `boost::chrono::process_real_cpu_clock`、`boost::chrono::process_user_cpu_clock` 和 `boost::chrono::process_system_cpu_clock` 返回的 CPU 时间。示例 37.1，“来自 Boost.Chrono 的所有时”向标准输出写入如下所示字符串：`1000000 nanoseconds since process start-up`。

# 示例 37.3. 使用 `boost::chrono::time_point_cast()` 时间点

```cpp
#include <boost/chrono.hpp>
#include <iostream>

using namespace boost::chrono;

int main()
{
  process_real_cpu_clock::time_point p = process_real_cpu_clock::now();
  std::cout << p << '\n';
  std::cout << time_point_cast<minutes>(p) << '\n';
}
```

`boost::chrono::time_point_cast()` 函数的使用方式类似于强制转换符。示例 37.3，“使用 `boost::chrono::time_point_cast()` 时间点”使用 `boost::chrono::time_point_cast()` 将一个基于纳秒的时间点转换为分钟的时间点。在这种情况下，你必须使用 `boost::chrono::time_point_cast()`，因为时间点在可能丢失精度的情况下，无法用精度较低的单位（分钟）来表示。从低精度单位转换为高精度单位时，你不需要 `boost::chrono::time_point_cast()`。

Boost.Chrono 还为持续时长提供了强制转换符。

## 示例 37.4. 使用 `boost::chrono::duration_cast()` 转换时长

```cpp
#include <boost/chrono.hpp>
#include <iostream>

using namespace boost::chrono;

int main()
{
  minutes m{1};
  seconds s{35};

  std::cout << m + s << '\n';
  std::cout << duration_cast<minutes>(m + s) << '\n';
}
```

示例 37.4，“使用 `boost::chrono::duration_cast()` 转换时长”使用 `boost::chrono::duration_cast()` 函数将持续时长从秒转换为分钟。此示例向标准输出写入 `1 minute`。

## 示例 37.5. 持续时舍入

```cpp
#include <boost/chrono.hpp>
#include <iostream>

using namespace boost::chrono;

int main()
{
  std::cout << floor<minutes>(minutes{1} + seconds{45}) << '\n';
  std::cout << round<minutes>(minutes{1} + seconds{15}) << '\n';
  std::cout << ceil<minutes>(minutes{1} + seconds{15}) << '\n';
}
```

Boost.Chrono 还提供了在转换时对持续时长进行舍入的函数。`boost::chrono::round()` 向上或向下舍入，`boost::chrono::floor()` 向下取整，而 `boost::chrono::ceil()` 向上取整。`boost::chrono::floor()` 使用 `boost::chrono::duration_cast()`——这两个函数之间没有区别。

示例 37.5，“持续时长舍入”向标准输出写入 `1 minute`、`1 minute` 和 `2 minutes`。

## 示例 37.6. 用户定义输出的流操符

```cpp
#define BOOST_CHRONO_VERSION 2
#include <boost/chrono.hpp>
#include <boost/chrono/chrono_io.hpp>
#include <iostream>

using namespace boost::chrono;

int main()
{
  std::cout << symbol_format << minutes{10} << '\n';

  std::cout << time_fmt(boost::chrono::timezone::local, "%H:%M:%S") <<
    system_clock::now() << '\n';
}
```

Boost.Chrono 提供了各种流操符来格式化时间点和持续时长的输出。例如，使用操符 `boost::chrono::symbol_format()`，时间单位将以符号而非名称写入。因此示例 37.6，“用户定义输出的流操符”显示 `10 min`。

操符 `boost::chrono::time_fmt()` 可用于设置时区和格式字符串。时区必须设置为 `boost::chrono::timezone::local` 或 `boost::chrono::timezone::utc`。格式字符串可以使用标志来引用时间点的各种组件。例如，示例 37.6，“用户定义输出的流操符”向标准输出写入一个如下的字符串：`15:46:44`。

除了流操符外，Boost.Chrono 还为许多不同的定制提供了面幅（facets）。例如，有一个面幅能够以另一种语言输出时间点。

### 注意

自 Boost 1.52.0 以来，输入/输出函数有两个版本。从 Boost 1.55.0 开始，默认使用较新版本。如果你使用早于 1.55.0 的版本，必须定义 `BOOST_CHRONO_VERSION` 并将其设置为 `2`，以便示例 37.6，“用户定义输出的流操符”正常工作。

## Boost.Timer

[Boost.Timer](http://www.boost.org/libs/timer) 提供了测量性能的计时器。初看起来它似乎与 `boost::chrono` 竞争。然而，虽然 `boost::chrono` 用于测量任意周期，但你应该使用 `Boost.Timer` 来测量代码。

从 1.48 版本开始，有两个版本的 Boost.Timer。第一个版本只有一个头文件：`boost/timer/timer.hpp`。

Boost.Timer 提供的计时器通过 `boost::timer::cpu_timer` 和 `boost::timer::auto_timer` 类实现。`boost::timer::auto_timer` 派自 `boost::timer::cpu_timer` 并在析构函数中自动停止计时。

在实例化 `boost::timer::cpu_timer` 时开始测量。你可以在任何时候调用成员函数 `format()` 获取已时间。示例 38.1，“使用 `boost::timer::cpu_timer()` 测量时间”以以下格式显示输出：`0.099170s wall, 0.093601s user + 0.000000s system = 0.093601s CPU (94.4%)`。

### 示例 38.1. 使用 `boost::timer::cpu_timer` 测量时间

```cpp
#include <boost/timer/timer.hpp>
#include <iostream>
#include <cmath>

using namespace boost::timer;

int main()
{
  cpu_timer timer;

  for (int i = 0; i < 1000000; ++i)
    std::pow(1.234, i);
  std::cout << timer.format() << '\n';
}
```

Boost.Timer 测量墙上时间（wall time）和 CPU 时间。墙上时间是根据挂钟流逝的时间。你可以用秒表测量这段时间。CPU 时间表示程序执行代码所花费的时间。在当今的多任务系统中，处理器并不总是对程序可用。程序可能还需要停止并等待用户输入。在这些情况下，墙上时间继续移动，但 CPU 时间不会。

## 示例 38.2. 停止和恢复计时器

```cpp
#include <boost/timer/timer.hpp>
#include <iostream>
#include <cmath>

using namespace boost::timer;

int main()
{
  cpu_timer timer;

  for (int i = 0; i < 1000000; ++i)
    std::pow(1.234, i);
  std::cout << timer.format() << '\n';

  timer.stop();

  for (int i = 0; i < 1000000; ++i)
    std::pow(1.234, i);
  std::cout << timer.format() << '\n';

  timer.resume();

  for (int i = 0; i < 1000000; ++i)
    std::pow(1.234, i);
  std::cout << timer.format() << '\n';
}
```



`boost::timer::cpu_timer` 提供了成员函数 `stop()` 和 `resume()`，用于停止和恢复计时器。在示例 38.2“停止和恢复计时器”中，计时器在第二个 `for` 循环运行之前被停止，并在之后恢复。因此，第二个 `for` 循环没有被测量。这类似于一个停止后在一段时间后再次恢复的秒表。在示例 38.2“停止和恢复计时器”中，第二次调用 `format()` 返回的时间与不存在第二个 `for` 循环时的结果是一样的。

`boost::timer::cpu_timer` 还提供了一个成员函数 `start()`。如果你调用 `start()` 而不是 `resume()`，计时器将从零重新启动。`boost::timer::cpu_timer` 的构造函数会调用 `start()`，这也就是为什么计时器在实例化 `boost::timer::cpu_timer` 时会立即启动。

## 示例 38.3：获取元组形式的墙钟时间和 CPU 时间

```cpp
#include <boost/timer/timer.hpp>
#include <iostream>
#include <cmath>

using namespace boost::timer;

int main()
{
  cpu_timer timer;

  for (int i = 0; i < 1000000; ++i)
    std::pow(1.234, i);

  cpu_times times = timer.elapsed();
  std::cout << times.wall << '\n';
  std::cout << times.user << '\n';
  std::cout << times.system << '\n';
}
```

虽然 `format()` 以字符串的形式返回测量的墙钟时间和 CPU 时间，但也可以以元组的形式接收这些时间（参见示例 38.3“获取元组形式的墙钟时间和 CPU 时间”）。`boost::timer::cpu_timer` 提供了成员函数 `elapsed()` 来实现。`elapsed()` 返回一个类型为 `boost::timer::times` 的元组。该元组有三个成员变量：`wall`、`user` 和 `system`。这些成员变量包含纳秒单位的墙时间和 CPU 时间。它们的类型是 `boost::int_least64_t`。

`boost::timer::times` 提供了成员函数 `clear()` 来将 `wall`、`user` 和 `system` 设置为 0。

## 示例 38.4：使用 `boost::timer::auto_cpu_timer` 自动测量时间

```cpp
#include <boost/timer/timer.hpp>
#include <cmath>

using namespace boost::timer;

int main()
{
  auto_cpu_timer timer;

  for (int i = 0; i < 1000000; ++i)
    std::pow(1.234, i);
}
```

你可以使用 `boost::timer::auto_cpu_timer` 测量代码块的墙时间和 CPU 时间。由于该类的析构函数会停止计时并将时间写入标准输出流，因此示例 38.4“使用 `boost::timer::auto_cpu_timer` 自动测量时间”的操作与示例 38.1“使用 `boost::timer::cpu_timer` 测量时间”相同。

`boost::timer::auto_cpu_timer` 提供了几个构造函数。例如，你可以传递一个用于显示时间的输出流。默认情况下，输出流是 `std::cout`。

你可以为 `boost::timer::auto_cpu_timer` 和 `boost::timer::cpu_timer` 指定报告时间的格式。Boost.Timer 提供了类似于 Boost.Format 或 `std::printf()` 所支持的格式标志。文档包含了这些格式标志的概述。

# 第 IX 部分：函数式编程

在函数式编程模型中，函数是对象，与其他对象一样，它们可以作为参数传递给函数或存储在容器中。有许多 Boost 库支持函数式编程模型。

- `Boost.Phoenix` 是用于创建对象的强大库。
- `Boost.Function` 为任何可调用目标提供了通用接口。
- `Boost.Bind` 允许将参数绑定到函数。
- `Boost.Lambda` 提供定义匿名函数的方法。
- `Boost.Ref` 允许通过引用向对象传递参数。
- `Boost.Callable` 是检查类型是否可用的工具。

# 39. Boost.Phoenix

[Boost.Phoenix](https://www.boost.org/doc/libs/release/) 是一个创建对象的库。在函数式编程中，函数是可以到处传递的对象。Boost.Phoenix 提供了各种表达式来创建这些对象。每个表达式都可以通过 `operator()` 调用。

Boost.Phoenix 中常用的表达式有：

- `_1`、`_2` 等：代表函数的第一个、第二个参数的占位符。
- `_a`：代表传递给函数的任意占位符。
- `_val`：返回传递值的占位符。
- `bind`：创建一个将参数绑定到函数的函数。
- `lambda`：从 lambda 表达式创建函数。
- `ref`：创建一个通过引用传递参数的函数。
- `const`：创建一个通过常量传递参数的函数。

### 如何使用 Boost.Phoenix 表达式示例

```cpp
#include <boost/phoenix/phi.hpp>
#include <iostream>
#include <functional>

using namespace boost::phoenix;

int add(int a, int b) {
  return a + b;
}

int main() {
  // 使用占位符和运算符
  auto func = _1 + _2; 
  std::cout << func(5, 3) << std::endl; // 输出: 8

  // 使用 bind
  auto bound_func = bind(add, _1, _2);
  std::cout << bound_func(10, 20) << std::endl; // 输出: 30

  // 使用 lambda
  auto lambda_func = []((int x) { return x * 2; });
  std::cout << lambda_func(5) << std::endl; // 输出: 10

  // 使用 ref
  int x = 10;
  auto ref_func = bind(add, ref(x), _1);
  std::cout << ref_func(5) << std::endl; // 输出: 15
}
```

`arg1` 是调用 Phoenix 函数时传递的数值的占位符。由于这里只使用了 `arg1`，因此创建了一个一元函数。Boost.Phoenix 提供了额外的占位符，例如 `boost::phoenix::placeholders::arg2` 和 `boost::phoenix::placeholders::arg3`。Phoenix 函数期望的参数数量始终与编号最大的占位符一致。

示例 39.1“作为全局函数、lambda 函数和 Phoenix 函数的谓词”向标准输出输出了三次 `3`。

示例 39.2“Phoenix 函数对比 lambda 函数”强调了 Phoenix 和 lambda 函数之间的关键区别。除了不需要带有参数列表的函数头外，Phoenix 函数的参数没有类型。lambda 函数 `lambda` 期望一个 `int` 类型的参数，而 Phoenix 函数 `phoenix` 将接受取模运算符可以处理的任何类型。

将 Phoenix 函数视为函数模板。就像函数模板一样，Phoenix 函数可以接受任何类型。这使得在示例 39.2“Phoenix 函数对比 lambda 函数”中可以使用 `phoenix` 作为容器 `v` 和 `v2` 的谓词，尽管它们存储的是不同类型的数字。如果你尝试在 `v2` 上使用谓词 `lambda`，你将得到编译器错误。

## 示例 39.2：Phoenix 函数对比 lambda 函数

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  auto lambda = [](int i){ return i % 2 == 1; };
  std::cout << std::count_if(v.begin(), v.end(), lambda) << '\n';

  std::vector<long> v2;
  v2.insert(v2.begin(), v.begin(), v.end());

  using namespace boost::phoenix::placeholders;
  auto phoenix = arg1 % 2 == 1;
  std::cout << std::count_if(v.begin(), v.end(), phoenix) << '\n';
  std::cout << std::count_if(v2.begin(), v2.end(), phoenix) << '\n';
}
```

示例 39.3“作为延迟 C++ 代码的 Phoenix 函数”使用 Phoenix 函数作为 `std::count_if()` 的谓词，用于统计大于 2 的奇数。Phoenix 函数访问了 `arg1` 两次：一次用于测试占位符是否大于 2，另一次测试它是否为奇数。这些条件通过 `&&` 连接。

## 示例 39.3：作为延迟 C++ 代码的 Phoenix 函数

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  using namespace boost::phoenix::placeholders;
  auto phoenix = arg1 > 2 && arg1 % 2 == 1;
  std::cout << std::count_if(v.begin(), v.end(), phoenix) << '\n';
}
```

你可以将 Phoenix 函数视为不会立即执行的 C++ 代码。示例 39.3“作为延迟 C++ 代码的 Phoenix 函数”中的 Phoenix 函数看起来像是一个使用了多个逻辑和算术运算符的条件。然而，该条件并没有立即执行。它只有在从 `std::count_if()` 内部被访问时才会执行。`std::count_if()` 中的访问是一个普通的函数调用。

示例 39.3“作为延迟 C++ 代码的 Phoenix 函数”向标准输出输出了 `2`。

## 示例 39.4：显式 Phoenix 类型

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  using namespace boost::phoenix;
  using namespace boost::phoenix::placeholders;
  auto phoenix = arg1 > val(2) && arg1 % val(2) == val(1);
  std::cout << std::count_if(v.begin(), v.end(), phoenix) << '\n';
}
```

示例 39.4“显式 Phoenix 类型”使用 `boost::phoenix::placeholders::arg1` 和 `boost::phoenix::val()` 创建了一个函数。Phoenix 函数访问了 `arg1` 两次：一次用于测试占位符是否大于 2，另一次测试它是否为奇数。这些条件通过 `&&` 连接。

示例 39.5“显式 Phoenix 类型”展示了如何使用 `boost::phoenix::val()` 来指定参数类型。

示例 39.6“创建自己的函数”演示了如何定义自定义函数对象并使用 `boost::phoenix::function`。

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

struct is_odd_impl
{
    typedef bool result_type;

    template <typename T>
    bool operator()(T t) const { return t % 2 == 1; }
};

boost::phoenix::function<is_odd_impl> is_odd;

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  using namespace boost::phoenix::placeholders;
  std::cout << std::count_if(v.begin(), v.end(), is_odd(arg1)) << '\n';
}
```

你使用宏 `BOOST_PHOENIX_ADAPT_FUNCTION` 将一个独立函数转换为 Phoenix 函数。向该宏传递返回值的类型、要定义的 Phoenix 函数名称、独立函数的名称以及参数的个数。

### 示例 39.7：将独立函数转换为 Phoenix 函数

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

bool is_odd_function(int i) { return i % 2 == 1; }

BOOST_PHOENIX_ADAPT_FUNCTION(bool, is_odd, is_odd_function, 1)

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  using namespace boost::phoenix::placeholders;
  std::cout << std::count_if(v.begin(), v.end(), is_odd(arg1)) << '\n';
}
```

要将独立函数作为 Phoenix 函数使用，你也可以像示例 39.8“使用 `boost::phoenix::bind()` 的 Phoenix 函数”那样使用 `boost::phoenix::bind()`。其工作方式与 `std::bind()` 类似。独立函数的名称作为第一个参数传递。所有后续参数都会转发给该独立函数。

### 示例 39.8：使用 `boost::phoenix::bind()` 的 Phoenix 函数

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

bool is_odd(int i) { return i % 2 == 1; }

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  using namespace boost::phoenix;
  using namespace boost::phoenix::placeholders;
  std::cout << std::count_if(v.begin(), v.end(), bind(is_odd, arg1)) << '\n';
}
```

### 提示

避免使用 `boost::phoenix::bind()`。创建你自己的 Phoenix 函数。这会让代码更具可读性。特别是在处理复杂表达式时，处理 `boost::phoenix::bind()` 的额外细节将没有任何帮助。

### 示例 39.9：任意复杂的 Phoenix 函数

```cpp
#include <boost/phoenix/phoenix.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

int main()
{
  std::vector<int> v{1, 2, 3, 4, 5};

  using namespace boost::phoenix;
  using namespace boost::phoenix::placeholders;
  int count = 0;
  std::for_each(v.begin(), v.end(), if_(arg1 > 2 && arg1 % 2 == 1)
    [
      ++ref(count)
    ]);
  std::cout << count << '\n';
}
```



Boost.Phoenix 提供了一些用于模拟 C++ 关键字的函数对象。例如，你可以使用函数 `boost::phoenix::if_()`（参见示例 39.9，“任意复杂的 Phoenix 函数”）来创建一个像 `if` 一样测试条件的函数对象。如果条件为真，则将执行通过 `operator[]` 传递给函数对象的代码。当然，那些代码也必须基于函数对象。这样，你就可以创建复杂的 Phoenix 函数。

示例 39.9，“任意复杂的 Phoenix 函数”为每个大于 2 的奇数增加 `count` 的值。为了在 `count` 上使用自增运算符，使用 `boost::phoenix::ref()` 将 `count` 封装在函数对象中。与 `boost::phoenix::val()` 不同，没有值被拷贝到函数对象中。`boost::phoenix::ref()` 返回的函数对象存储了一个引用——在此处是对 `count` 的引用。

### 提示

不要使用 Boost.Phoenix 创建复杂函数。使用 C++11 的 lambda 函数会更好。虽然 Boost.Phoenix 的语法接近 C++，但使用像 `if_` 关键字或方括号之间的代码块并不一定能提高可读性。

# 40. Boost.Function

[Boost.Function](http://www.boost.org/libs/function) 提供名为 `boost::function` 的类来封装函数指针。它定义在 `boost/function.hpp` 中。

如果你在支持 C++11 的开发环境中工作，你可以访问头文件 `functional` 中的 `std::function` 类。在这种情况下，你可以忽略 Boost.Function，因为 `boost::function` 和 `std::function` 是等价的。

### 示例 40.1. 使用 `boost::function`

```cpp
#include <boost/function.hpp>
#include <iostream>
#include <cstdlib>
#include <cstring>

int main()
{
  boost::function<int(const char*)> f = atoi;
  std::cout << f("42") << '\n';
  f = nullptr;
  if (f.empty())
  {
    std::cout << "Function is empty\n";
  }
}
```

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

void print(int i)
{
  std::cout << i << '\n';
}

int main()
{
  std::vector<int> v{1, 3, 2};
  std::for_each(v.begin(), v.end(), print);
}
```

`std::for_each()` 的第三个参数是一个接受单个参数的函数或函数对象。在示例 41.1，“使用兼容函数的 `std::for_each()`”中，`std::for_each()` 将容器 `v` 中的数字作为单个参数一个接一个传递给 `print()`。

如果你需要传递一个签名不符合算法要求的函数，情况就会变得更加复杂。例如，如果你想让 `print()` 接受一个输出流作为额外参数，那么你不能再原样地在 `std::for_each()` 中使用它。

就像示例 41.1，“使用兼容函数的 `std::for_each()`”一样，示例 41.2，“使用 `std::bind1st()` 的 `std::for_each()`”将 `v` 中的所有数字写入标准输出。然而，这次输出流是作为参数传递给 `print()` 的。为了实现这一点，函数 `print()` 被定义为派自 `std::binary_function` 的函数对象。

### 示例 41.2. 使用 `std::bind1st()` 的 `std::for_each()`

```cpp
#include <vector>
#include <algorithm>
#include <functional>
#include <iostream>

class print : public std::binary_function<std::ostream*, int, void>
{
public:
  void operator()(std::ostream *os, int i) const
  {
    *os << i << '\n';
  }
};

int main()
{
  std::vector<int> v{1, 3, 2};
  std::for_each(v.begin(), v.end(), std::bind1st(print{}, &std::cout));
}
```

使用 Boost.Bind，你不需要将 `print()` 从函数转换为函数对象。相反，你使用的是定义在 `boost/bind.hpp` 中的函数模板 `boost::bind()`。

示例 41.3，“使用 `boost::bind()` 的 `std::for_each()`”使用 `print()` 作为函数，而不是作为函数对象。由于 `print()` 期望两个参数，因此该函数无法直接传递给 `std::for_each()`。相反，将 `boost::bind()` 传递给 `std::for_each()`，并将 `print()` 作为第一个参数传递给 `boost::bind()`。

由于 `print()` 期望两个参数，那么这两个参数也必须传递给 `boost::bind()`。它们是指向 `std::cout` 的指针和 `_1`。

`_1` 是一个占位符。Boost.Bind 定义了从 `_1` 到 `_9` 的占位符。这些占位符告诉 `boost::bind()` 返回一个函数对象，其期望的参数数量等于最大的占位符数量。如果如示例 41.3，“使用 `boost::bind()` 的 `std::for_each()`”所示，只使用了占位符 `_1`，`boost::bind()` 返回一个元函数对象——一个接受单个参数的函数对象。在这种情况下这是必要的，因为 `std::for_each()` 只传递了一个参数。

### 示例 41.3. 使用 `boost::bind()` 的 `std::for_each()`

```cpp
#include <boost/bind.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

void print(std::ostream *os, int i)
{
  *os << i << '\n';
}

int main()
{
  std::vector<int> v{1, 3, 2};
  std::for_each(v.begin(), v.end(), boost::bind(print, &std::cout, _1));
}
```

`std::for_each()` 调用一个一元函数对象。传递给函数对象的值——来自容器 `v` 的数字——占据了占位符 `_1` 的位置。`boost::bind()` 获取该数字和指向 `std::cout` 的指针并将它们转发给 `print()`。

请注意，`boost::bind()` 与 `std::bind1st()` 和 `std::bind2nd()` 一样，按值传递参数。为了防止调用程序尝试拷贝 `std::cout`，`print()` 期望一个指向 `std::cout` 的指针。

示例 41.1，“使用兼容函数的 `std::for_each()`”

示例 41.2，“使用 `std::bind1st()` 的 `std::for_each()`”

在 C++11 之前，你需要使用诸如 [Boost.Lambda](http://www.boost.org/libs/lambda) 的库来利用 lambda 函数。自 C++11 起，该库可以被视为过时，因为 lambda 函数现在已经是编程语言的一部分。如果你在一个不支持 C++11 的开发环境中工作，在转向 `Boost.Lambda` 之前，你应该考虑 `Boost.Phoenix`。`Boost.Phoenix` 是一个较新的库，如果你需要在没有 C++11 的情况下使用 lambda 函数，它可能是更好的选择。

lambda 函数的目的是让代码更加紧凑且易于理解（参见示例 43.1，“使用 lambda 函数的 `std::for_each()`”）。

## 示例 43.1. 使用 lambda 函数的 `std::for_each()`

```cpp
#include <boost/lambda/lambda.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

int main()
{
  std::vector<int> v{1, 3, 2};
  std::for_each(v.begin(), v.end(),
    std::cout << boost::lambda::_1 << "\n");
}
```

`Boost.Lambda` 提供了几个辅助工具来创建匿名函数。代码写在它应该执行的地方，不需要封装在函数中，也不需要显式调用函数。在示例 43.1，“使用 lambda 函数的 `std::for_each()`”中，`std::cout << boost::lambda::_1 << "\n"` 是一个期望一个参数的 lambda 函数，它将参数以及换行符写入标准输出。

`boost::lambda::_1` 是一个占位符，创建一个期望一个参数的 lambda 函数。占位符中的数字决定了预期参数的数量，因此 `boost::lambda::_2` 期望两个参数，而 `boost::lambda::_3` 期望三个参数。`Boost.Lambda` 只提供了这三个占位符。示例 43.1，“使用 lambda 函数的 `std::for_each()`”中的 lambda 函数使用 `boost::lambda::_1`，因为 `std::for_each()` 期望一个元函数。

包含 `boost/lambda/lambda.hpp` 以使用占位符。

请注意，示例 43.1，“使用 lambda 函数的 `std::for_each()`”中使用了 `\n` 而不是 `std::endl` 来输出换行。如果你使用 `std::endl`，示例将无法编译，因为 lambda 函数 `std::cout << boost::lambda::_1` 的类型与一元函数模板 `std::endl()` 期望的类型不同。因此，你不能使用 `std::endl`。

## 示例 43.2. 使用 `boost::lambda::if_then()` 的 lambda 函数

```cpp
#include <boost/lambda/lambda.hpp>
#include <boost/lambda/if.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

int main()
{
  std::vector<int> v{1, 3, 2};
  std::for_each(v.begin(), v.end(),
    boost::lambda::if_then(boost::lambda::_1 > 1,
    std::cout << boost::lambda::_1 << "\n"));
}
```

头文件 `boost/lambda/if.hpp` 定义了你可以用于在 lambda 函数中创建 `if` 控制结构的结构。最简单的结构是函数模板 `boost::lambda::if_then()`，它期望两个参数：第一个参数是条件。如果条件为真，则执行第二个参数。两个参数都可以是 lambda 函数，如示例 43.2，“使用 `boost::lambda::if_then()` 的 lambda 函数”所示。

除了 `boost::lambda::if_then()` 之外，`Boost.Lambda` 还提供了函数模板 `boost::lambda::if_then_else()` 和 `boost::lambda::if_then_else_return()`，它们都期望三个参数。此外还提供了用于在 lambda 函数中使用 `for` 循环、转换运算符以及抛出异常的函数模板。`Boost.Lambda` 定义的许多函数模板使得定义在任何方面都不低于普通 C++ 函数的 lambda 函数成为可能。

# 第 X 部分. 并行编程

以下库支持并行编程模型。

- `Boost.Thread` 允许你创建和管理自己的线程。
- `Boost.Atomic` 允许你从多个线程通过原子操作访问整数类型的变量。
- `Boost.Lockfree` 提供了线程安全的容器。
- `Boost.MPI` 源于超级计算机领域。通过 `Boost.MPI`，你的程序会被启动多次并在多个进程中执行。你专注于编写应该并发执行的实际任务，而 `Boost.MPI` 负责协调。

## Boost.Thread

[Boost.Thread](https://www.boost.org/libs/thread) 是允许你使用线程的库。标准库自 C11 起就支持线程。

## 创建和管理线程

该库中最重要的类是 `boost::thread`，它定义在 `boost/thread.hpp` 中。示例 44.1，“使用 `boost::thread`”是一个创建线程的简单示例。

新线程应该执行的函数名称被传递给 `boost::thread` 的构造函数。一旦创建，该函数就会在自己的线程中开始执行。此时，它会与 `main()` 函数并发执行。

为了防止程序终止，在新创建的线程上调用了 `join()`。`join()` 会阻塞当前线程，直到调用 `join()` 的线程结束为止。这导致 `main()` 等待直到线程返回。

### 示例 44.1. 使用 `boost::thread`

```cpp
#include <boost/thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

void thread()
{
  for (int i = 0; i < 5; ++i)
  {
    wait(1);
    std::cout << i << '\n';
  }
}

int main()
{
  boost::thread t{thread};
  t.join();
}
```

可以使用变量（此示例中的 `t`）访问特定线程以等待其终止。然而，即使 `t` 离开作用域并被销毁，线程仍继续执行。线程最初总是绑定到 `boost::thread` 类型的变量上的，但一旦创建，线程不再依赖于该变量。有一个名为 `detach()` 的成员函数，允许 `boost::thread` 类型的变量与其对应的线程分离。在调用 `detach()` 之后无法调用 `join()` 等成员函数，因为分离的变量不再代表有效的线程。

任何在函数内部可以执行的操作也可以在线程内部执行。归结底，线程与函数没有区别，只是它是与另一个函数并发执行的。在示例 44.1，“使用 `boost::thread`”中，通过循环向标准输出流写入了五个数字。为了减慢输出速度，循环的每次迭代都会调用 `wait()` 函数暂停一秒。`wait()` 使用了 `sleep_for()` 函数，该函数由 Boost.Thread 提供并存在 `boost::this_thread` 命名空间中。

`sleep_for()` 期望唯一的参数是一个时间段，表示当前线程应该暂停多久。通过传递一个类型为 `boost::chrono::seconds` 的对象可以设置这段时间。`boost::chrono::seconds` 来自于 Boost.Chrono，该库在第 37 章，*Boost.Chrono* 中引入。

`sleep_for()` 只接受来自 Boost.Chrono 的类型。尽管 Boost.Chrono 自 C++11 起已标准库的一部分，但 `std::chrono` 中的类型不能与 Boost.Thread 使用。这样做会导致编译器错误。

如果你不想在 `main()` 结束时调用 `join()`，可以使用 `boost::scoped_thread` 类。`boost::scoped_thread` 的构造函数期望一个类型为 `boost::thread` 的对象。在 `boost::scoped_thread` 的析构函数中，操作可以访问该对象。默认情况下，`boost::scoped_thread` 使用一个对线程调用 `join()` 的操作。因此，示例 44.2，“使用 `boost::scoped_thread` 等待线程”的工作类似于示例 44.1，“使用 `boost::thread`”。



### Example 44.2. Waiting for a thread with `boost::scoped_thread`

```cpp
#include <boost/thread.hpp>
#include <boost/thread/scoped_thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

void thread()
{
  for (int i = 0; i < 5; ++i)
  {
    wait(1);
    std::cout << i << '\n';
  }
}

int main()
{
  boost::scoped_thread<> t{boost::thread{thread}};
}
```

你可以将用户自定义的操作作为模板参数。该操作必须是一个带有 `operator()` 的类，且该操作符接受一个类型为 `boost::thread` 的对象。`boost::scoped_thread` 保证该操作符会在析构函数中被调用。

你只能在 Boost.Thread 中找到 `boost::scoped_thread` 类。标准库中没有对应的项。确保为 `boost::scoped_thread` 包含了头文件 `boost/thread/scoped_thread.hpp`。

示例 44.3，“带有 `boost::this_thread::sleep_for()` 的中断点” 引入了中断点，这使得中断线程成为可能。中断点仅由 Boost.Thread 支持，标准库并不支持。

在线程对象上调用 `interrupt()` 会中断相应的线程。在这种背景下，中断意味着在线程中抛出一个类型为 `boost::thread_interrupted` 的异常。然而，这只会在线程到达中断点时才会发生。

### Example 44.3. An interruption point with `boost::this_thread::sleep_for()`

```cpp
#include <boost/thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

void thread()
{
  try
  {
    for (int i = 0; i < 5; ++i)
    {
      wait(1);
      std::cout << i << '\n';
    }
  }
  catch (boost::thread_interrupted&) {}
}

int main()
{
  boost::thread t{thread};
  wait(3);
  t.interrupt();
  t.join();
}
```

如果给定的线程不包含中断点，简单调用 `interrupt()` 将没有任何影响。每当线程到达中断点时，它都会检查 `interrupt()` 是否已被调用。如果已被调用，则会抛出一个类型为 `boost::thread_interrupted` 的异常。

Boost.Thread 定义了诸如 `sleep_for()` 等中断点。示例 44.3，“带有 `boost::this_thread::sleep_for()` 的中断点” 中断点使得中断线程成为可能。中断点仅由 Boost.Thread 支持，标准库并不支持。

```cpp
#include <boost/thread.hpp>
#include <iostream>

int main()
{
  std::cout << boost::this_thread::get_id() << '\n';
  std::cout << boost::thread::hardware_concurrency() << '\n';
}
```

在 `boost::this_thread` 命名空间中，定义了一些适用于当前线程的非成员函数。其中一个函数是 `sleep_for()`，我们之前见过它。另一个函数是 `get_id()`，它返回一个数字来唯一地标识当前线程（参见 示例 44.6, “检测线程 ID 和可用处理器数量”）。`get_id()` 也作为 `boost::thread` 类的成员函数提供。

静态成员函数 `boost::thread::hardware_concurrency()` 根据底层的 CPU 或 CPU 核心数，返回可以同时物理执行的线程数。在双核处理器上调用此函数将返回值 2。该函数提供了一种简单的方法来识别应该使用的理论最大线程数。

Boost.Thread 还提供了 `boost::thread_group` 类来管理线程组。该类提供的一个函数是成员函数 `join_all()`，它会等待组中的所有线程终止。

## 线程同步

虽然使用多个线程可以提高应用程序的性能，但它通常也会增加复杂性。如果几个函数同时执行，必须对共享资源的访问进行同步。一旦应用程序达到一定规模，这就会涉及大量的编程工作。本节介绍了 Boost.Thread 提供的用于同步线程的类。

### 示例 44.7. 使用 `boost::mutex` 进行互斥访问

```cpp
#include <boost/thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

boost::mutex mutex;

void thread()
{
  using boost::this_thread::get_id;
  for (int i = 0; i < 5; ++i)
  {
    wait(1);
    mutex.lock();
    std::cout << "Thread " << get_id() << ": " << i << std::endl;
    mutex.unlock();
  }
}

int main()
{
  boost::thread t1{thread};
  boost::thread t2{thread};
  t1.join();
  t2.join();
}
```

多线程程序使用互斥锁（mutex）进行同步。Boost.Thread 提供了不同的互斥锁类，其中 `boost::mutex` 是简单的。互斥锁的基本原理是在特定线程拥有互斥锁时防止其他线程获取所有权。一旦释放，另一个线程就可以获取所有权。这导致线程等待，直到拥有互斥锁的线程完成处理并释放对互斥锁的所有权。

示例 44.7, “使用 `boost::mutex` 进行互斥访问” 使用了类型为 `boost::mutex` 的全局互斥锁 `mutex`。`thread()` 函数通过调用 `lock()` 获取该对象的所有权。这发生在函数向标准输出流写入消息之前。一旦写入消息，就会通过调用 `unlock()` 释放所有权。

`main()` 创建两个线程，它们都在执行 `thread()` 函数。每个线程在 `for` 循环的每次迭代中计数到五，并向标准输出流写入消息。由于 `std::cout` 是线程共享的全局对象，必须对访问进行同步。否则，消息可能会混乱。同步保证了在任何时刻，只有一个线程可以访问 `std::cout`。互斥锁保证了在范围内只有一个线程进入临界区。

### 示例 44.8. `boost::lock_guard` 保证释放

```cpp
#include <boost/thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

boost::mutex mutex;

void thread()
{
  using boost::this_thread::get_id;
  for (int i = 0; i < 5; ++i)
  {
    wait(1);
    boost::lock_guard<boost::mutex> lock(mutex);
    std::cout << "Thread " << get_id() << ": " << i << std::endl;
  }
}

int main()
{
  boost::thread t1{thread};
  boost::thread t2{thread};
  t1.join();
  t2.join();
}
```

获取和释放互斥锁是一种典型的模式，Boost.Thread 支持不同的类型。例如，与其手动调用 `lock()` 和 `unlock()`，可以使用 `boost::lock_guard`。`boost::lock_guard` 在构造函数中获取互斥锁，并在析构函数中自动释放。示例 44.8, “`boost::lock_guard` 保证释放” 这样做确保了资源在不再需要时被释放。`boost::lock_guard` 是 RAII 模式的一个示例，即使发生异常也能确保锁释放。

除了 `boost::mutex`，Boost.Thread 还提供了额外的类来支持同步。其中非常有用的类之一是 `boost::unique_lock`。示例 44.9, “灵活的 `boost::unique_lock`” 使用了 `thread()` 函数的变体。`thread1()` 将 `mutex` 传递给 `unique_lock` 的构造函数，这使得 `unique_lock` 尝试获取互斥锁。在这种情况下，`unique_lock` 的行为与 `lock_guard` 不同。`unique_lock` 的构造函数调用 `lock()`。

然而，`unique_lock` 的析构函数在 `thread1()` 中并不释放互斥锁。在 `thread1()` 中调用了 `release()`，将锁解耦。默认情况下，`unique_lock` 的析构函数会释放互斥锁，就像 `lock_guard` 一样——但如果已经解耦则不会。这就是为什么在 `thread1()` 中显式调用了 `unlock()`。

`thread2()` 将 `mutex` 和 `boost::try_to_lock` 传递给 `unique_lock` 的构造函数。这使得 `unique_lock` 的构造函数不调用 `lock()` 而是调用 `try_lock()`。因此，构造函数只尝试锁定互斥锁。如果互斥锁被另一个线程占用，尝试将失败。

`owns_lock()` 允许检测 `unique_lock` 是否成功锁定了互斥锁。如果 `owns_lock()` 返回 `true`，`thread2()` 可以立即访问 `std::cout`。如果 `owns_lock()` 返回 `false`，则会调用 `try_lock_for()`。该成员函数也尝试锁定互斥锁，但它会在指定的时间内等待。在 示例 44.9, “灵活的 `boost::unique_lock`” 中，锁尝试获取一秒的互斥锁。如果 `try_lock_for()` 返回 `true`，则可以访问 `std::cout`。否则，`thread2()` 将放弃并跳过一个数字。

请注意，在示例 44.9, “万能锁 `boost::unique_lock`” 中，`mutex` 的类型是 `boost::timed_mutex`，而不是 `boost::mutex`。示例使用了 `boost::timed_mutex` 是因为该互斥锁是唯一提供成员函数 `try_lock_for()` 的类型。当在锁上调用 `try_lock_for()` 时，就会调用该成员函数。`boost::mutex` 只提供了成员函数 `lock()` 和 `try_lock()`。

`boost::unique_lock` 是一个互斥锁。互斥锁始终是 `mutex` 的唯一所有者。只有在互斥锁释放它之后，另一个锁才能获得 `mutex` 的控制权。Boost.Thread 还通过 `boost::shared_lock` 类支持共享锁，该类配合 `shared_mutex` 使用。

### 示例 44.9. 万能锁 `boost::unique_lock`

```cpp
#include <boost/thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

boost::timed_mutex mutex;

void thread1()
{
  using boost::this_thread::get_id;
  for (int i = 0; i < 5; ++i)
  {
    wait(1);
    boost::unique_lock<boost::timed_mutex> lock{mutex};
    std::cout << "Thread " << get_id() << ": " << i << std::endl;
    boost::timed_mutex *m = lock.release();
    m->unlock();
  }
}

void thread2()
{
  using boost::this_thread::get_id;
  for (int i = 0; i < 5; ++i)
  {
    wait(1);
    boost::unique_lock<boost::timed_mutex> lock{mutex,
      boost::try_to_lock};
    if (lock.owns_lock() || lock.try_lock_for(boost::chrono::seconds{1}))
    {
      std::cout << "Thread " << get_id() << ": " << i << std::endl;
    }
  }
}

int main()
{
  boost::thread t1{thread1};
  boost::thread t2{thread2};
  t1.join();
  t2.join();
}
```

### 示例 44.10. 使用 `boost::shared_lock` 的共享锁

```cpp
#include <boost/thread.hpp>
#include <boost/chrono.hpp>
#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>

void wait(int seconds)
{
  boost::this_thread::sleep_for(boost::chrono::seconds{seconds});
}

boost::shared_mutex mutex;
std::vector<int> random_numbers;

void fill()
{
  std::srand(static_cast<unsigned int>(std::time(0)));
  for (int i = 0; i < 3; ++i)
  {
    boost::unique_lock<boost::shared_mutex> lock{mutex};
    random_numbers.push_back(std::rand());
    lock.unlock();
    wait(1);
  }
}

void print()
{
  for (int i = 0; i < 3; ++i)
  {
    wait(1);
    boost::shared_lock<boost::shared_mutex> lock{mutex};
    std::cout << random_numbers.back() << '\n';
  }
}

int sum = 0;

void count()
{
  for (int i = 0; i < 3; ++i)
  {
    wait(1);
    boost::shared_lock<boost::shared_mutex> lock{mutex};
    sum += random_numbers.back();
  }
}

int main()
{
  boost::thread t1{fill}, t2{print}, t3{count};
  t1.join();
  t2.join();
  t3.join();
  std::cout << "Sum: " << sum << '\n';
}
```

如果线程只需要对特定资源进行只读访问，可以使用类型为 `boost::shared_lock` 的非互斥锁。修改资源的线程需要写访问权限，因此需要互斥锁。由于具有只读访问权限的线程不受其他同时读取同一资源的线程的影响，因此它们可以使用非互斥锁并共享一个 `mutex`。



在示例 44.10《使用 `boost::shared_lock` 的共享锁》中，`print()` 和 `count()` 都只读取变量 `random_numbers`。`print()` 函数将 `random_numbers` 中的最后一个值写入标准输出流，而 `count()` 函数将其加到变量 `sum` 中。由于这两个函数都没有修改 `random_numbers`，因此它们都可以使用类型为 `boost::shared_lock` 的非互斥锁同时访问它。

示例 44.11《使用 `boost::condition_variable_any` 的条件变量》中，如果锁不是 `for` 循环中的局部变量，而是在外部作用范围内实例化的，同样有效。事实上，这样做更有意义，因为锁不需要在每次迭代中销毁并重建。由于互斥量通过 `wait()` 释放，因此不需要在迭代结束时销毁锁。

## 线程本地存储

线程本地存储（`TLS`）是一个只能被一个线程访问的专用存储区域。`TLS` 变量可以被视为仅对特定线程可见，而非整个程序可见的全局变量。

### 示例 44.12. 使用静态变量同步多个线程

```cpp
#include <boost/thread.hpp>
#include <iostream>

boost::mutex mutex;

void init()
{
  static bool done = false;
  boost::lock_guard<boost::mutex> lock{mutex};
  if (!done)
  {
    done = true;
    std::cout << "done" << '\n';
  }
}

void thread()
{
  init();
  init();
}

int main()
{
  boost::thread t[3];

  for (int i = 0; i < 3; ++i)
    t[i] = boost::thread{thread};

  for (int i = 0; i < 3; ++i)
    t[i].join();
}
```

示例 44.12《使用静态变量同步多个线程》在三个线程中执行函数 `thread()`。`thread()` 调用了另一个函数 `init()` 两次，而 `init()` 检查布尔变量 `done` 是否为 `false`。如果是，则将该变量设置为 `true` 并将 `done` 写入标准输出。

`done` 是一个所有线程共享的静态变量。如果第一个线程将 `done` 设置为 `true`，则第二个和第三个线程将不会将 `done` 写入标准输出。任何线程中的第二次调用 `init()` 也不会将 `done` 写入标准输出。该示例将打印一次 `done`。

像 `done` 这样的静态变量可以用于在进程中进行一次性初始化。为了每个线程进行一次性初始化，可以使用 `TLS`。

### 示例 44.13. 使用 TLS 同步多个线程

```cpp
#include <boost/thread.hpp>
#include <iostream>

boost::mutex mutex;

void init()
{
  static boost::thread_specific_ptr<bool> tls;
  if (!tls.get())
  {
    tls.reset(new bool{true});
    boost::lock_guard<boost::mutex> lock{mutex};
    std::cout << "done" << '\n';
  }
}

void thread()
{
  init();
  init();
}

int main()
{
  boost::thread t[3];

  for (int i = 0; i < 3; ++i)
    t[i] = boost::thread{thread};

  for (int i = 0; i < 3; ++i)
    t[i].join();
}
```

在示例 44.13《使用 TLS 同步多个线程》中，静态变量 `done` 被替换为 TLS 变量 `tls`。该变量基于类模板 `boost::thread_specific_ptr`，并使用 `bool` 类型实例化。原则上讲，`tls` 的工作方式与 `done` 类似：它作为一个指示某些操作是否已经完成的条件。然而，关键区别在于，`tls` 存储的值仅对相应的线程可见并可用。

一旦创建了 `boost::thread_specific_ptr` 变量，就可以对其进行设置。该变量期望一个 `bool` 类型变量的地址，而不是变量本身。使用成员函数 `reset()`，可以将地址存储在 `tls` 中。在示例 44.13《使用 TLS 同步多个线程》中，动态分配了一个 `bool` 类型变量，并将 `new` 返回的地址存储在 `tls` 中。为了避免每次调用 `init()` 时都设置 `tls`，使用了成员函数 `get()` 来检查是否已经存储了地址。

由于 `boost::thread_specific_ptr` 存储的是一个地址，因此该类的行为像一个指针。例如，它提供了成员函数 `operator*` 和 `operator->`，它们的工作方式正如你预期指针的工作方式一样。

示例 44.13《使用 TLS 同步多个线程》向标准输出打印了三次 `done`。每个线程在第一次调用 `init()` 时都会打印 `done`。由于使用了 TLS 变量，每个线程都使用自己的变量 `tls`。

## 未来（Futures）与承诺（Promises）

Future 和 Promise 是从一个线程传递数据到另一个线程的工具。可以使用全局变量来实现，但 Future 和 Promise 不需要它们。

### 示例 44.14. 使用 `future` 和 `promise`

```cpp
#define BOOST_THREAD_PROVIDES_FUTURE
#include <boost/thread.hpp>
#include <boost/thread/future.hpp>
#include <functional>
#include <iostream>

void accumulate(boost::promise<int> &p)
{
  int sum = 0;
  for (int i = 0; i < 5; ++i)
    sum += i;
  p.set_value(sum);
}

int main()
{
  boost::promise<int> p;
  boost::future<int> f = p.get_future();
  boost::thread t{std::ref(p)};
  std::cout << f.get() << '\n';
}
```

示例 44.14《使用 `future` 和 `promise`》显示了 `10`。

`accumulate()` 经过调整以在线程中执行。它必须接受一个 `boost::promise` 类型的参数并将结果存储其中。Future `f` 和 Promise `p` 是关联的。当在 future 上调用 `get()` 时，将返回通过 `set_value()` 存储在 promise 中的值。

### 示例 44.15. 使用 `boost::packaged_task`

`boost::packaged_task` 可以将从任何函数返回的值转发到 future，只要该函数通过 `return` 返回结果即可。

```cpp
#define BOOST_THREAD_PROVIDES_FUTURE
#include <boost/thread.hpp>
#include <boost/thread/future.hpp>
#include <utility>
#include <iostream>

int accumulate()
{
  int sum = 0;
  for (int i = 0; i < 5; ++i)
    sum += i;
  return sum;
}

int main()
{
  boost::packaged_task<int> task{accumulate};
  boost::future<int> f = task.get_future();
  boost::thread t{std::move(task)};
  std::cout << f.get() << '\n';
}
```

示例 44.15《使用 `boost::packaged_task`》与上一个示例类似，但这次没有使用 `boost::promise`。相反，这个示例使用了 `boost::packaged_task` 类，它和 `boost::promise` 一样，提供了一个返回 future 的成员函数 `get_future()`。

`boost::packaged_task` 的构造函数期望将一个将在线程中执行的函数作为参数，但 `boost::packaged_task` 本身不会启动线程。必须将类型为 `boost::packaged_task` 的对象传递给 `boost::thread` 的构造函数，才能在新线程中执行该函数。

`boost::packaged_task` 的优势在于可以将函数的返回值存储在 future 中。你不需要对函数进行适配来将其值存储在 future 中。`boost::packaged_task` 可以看作是一个适配器，可以将任何函数的返回值存储在 future 中。

虽然该示例去掉了 `boost::promise`，但下面的示例也没有使用 `boost::packaged_task` 和 `boost::thread`。

### 示例 44.16. 使用 `boost::async()`

```cpp
#define BOOST_THREAD_PROVIDES_FUTURE
#include <boost/thread.hpp>
#include <boost/thread/future.hpp>
#include <iostream>

int accumulate()
{
  int sum = 0;
  for (int i = 0; i < 5; ++i)
    sum += i;
  return sum;
}

int main()
{
  boost::future<int> f = boost::async(accumulate);
  std::cout << f.get() << '\n';
}
```

在示例 44.16《使用 `boost::async()`》中，`accumulate()` 被传递给函数 `boost::async()`。该函数统一了 `boost::packaged_task` 和 `boost::thread`。它在新线程中启动 `accumulate()` 并返回一个 future。

可以向 `boost::async()` 传递启动策略（launch policy）。这个额外参数决定了 `boost::async()` 是在新线程还是当前线程中执行函数。如果你传递 `boost::launch::async`，`boost::async()` 将启动新线程；这是默认行为。如果你传递 `boost::launch::deferred`，函数将在调用 `get()` 时在当前线程中执行。

尽管 Boost 1.56.0 允许向 `boost::async()` 传递 `boost::launch::async` 或 `boost::launch::deferred`，但在当前线程中执行函数的功能尚未实现。如果你传递 `boost::launch::deferred`，程序将终止。

# 45. Boost.Atomic

[Boost.Atomic](http://www.boost.org/libs/atomic) 提供了 `boost::atomic` 类，可用于创建原子变量。它们被称为原子变量，是因为所有访问都是原子的。在多线程程序中，Boost.Atomic 用于当一个线程对变量的访问不应被另一个访问相同变量的线程干扰时。如果没有 `boost::atomic`，从多个线程访问共享变量需要使用锁进行同步。

`boost::atomic` 取决于目标平台是否支持原子变量访问。否则，`boost::atomic` 使用锁。该库允许你检测目标平台是否支持原子变量访问。

如果你的开发环境支持 C++11，则不需要 Boost.Atomic。C++11 标准库提供了一个头文件 `atomic`，定义了与 Boost.Atomic 相同的功能。例如，你会发现一个名为 `std::atomic` 的类。

Boost.Atomic 支持与标准库大体相同的功能。虽然 Boost.Atomic 中的某些函数被重载了，但它们在标准库中可能有不同的名称。标准库还提供了一些函数，例如 `std::atomic_init()` 和 `std::kill_dependency()`，这些在 Boost.Atomic 中是缺失的。

## 示例 45.1. 使用 `boost::atomic`

```cpp
#include <boost/atomic.hpp>
#include <thread>
#include <iostream>

boost::atomic<int> a{0};

void thread()
{
  ++a;
}

int main()
{
  std::thread t1{thread};
  std::thread t2{thread};
  t1.join();
  t2.join();
  std::cout << a << '\n';
}
```

示例 45.1《使用 `boost::atomic`》使用两个线程递增 `int` 变量 `a`。示例没有使用锁，而是使用了 `boost::atomic` 进行原子访问。示例向标准输出写入 `2`。`boost::atomic` 之所以有效，是因为某些处理器支持变量的原子访问。如果在不支持将 `int` 作为原子操作的平台上运行此示例，`boost::atomic` 将使用锁。

## 示例 45.2. `boost::atomic` 有锁或无锁

```cpp
#include <boost/atomic.hpp>
#include <iostream>

int main()
{
  std::cout.setf(std::ios::boolalpha);

  boost::atomic<short> s;
  std::cout << s.is_lock_free() << '\n';

  boost::atomic<int> i;
  std::cout << i.is_lock_free() << '\n';

  boost::atomic<long> l;
  std::cout << l.is_lock_free() << '\n';
}
```

示例 45.2《`boost::atomic` 有锁或无锁》仅使用了整数类型。你不应对 `std::string` 或 `std::vector` 等类使用 `boost::atomic`。Boost.Atomic 提供了 `BOOST_ATOMIC_INT_LOCK_FREE` 和 `BOOST_ATOMIC_LONG_LOCK_FREE` 宏，用于在编译时检查哪些数据类型支持无锁访问。

## 示例 45.3. 使用 `boost::memory_order_seq_cst` 的 `boost::atomic`

```cpp
#include <boost/atomic.hpp>
#include <thread>
#include <iostream>

boost::atomic<int> a{0};

void thread()
{
  a.fetch_add(1, boost::memory_order_seq_cst);
}

int main()
{
  std::thread t1{thread};
  std::thread t2{thread};
  t1.join();
  t2.join();
  std::cout << a << '\n';
}
```

示例 45.3《使用 `boost::memory_order_seq_cst` 的 `boost::atomic`》递增了 `a` 两次——这次不是通过 `operator++`，而是通过调用 `fetch_add()`。

### 注意

指定内存序（memory order）可以优化性能，但增加了复杂性并使编写正确代码变得更加困难。因此，在实践中，你应该有一个真正充分的理由才使用内存序。

示例 45.3《带有 `boost::memory_order_seq_cst` 的 `boost::atomic`》使用内存顺序 `boost::memory_order_seq_cst` 将 `a` 增 1。该内存顺序代表顺序一致性（sequential consistency）。这是限制性最强的内存顺序。所有在 `fetch_add()` 调用之前出现的内存访问必须在该成员函数执行之前发生。所有在 `fetch_add()` 调用之后出现的内存访问都必须在该成员函数执行之后发生。编译器和处理器可能会重排 `fetch_add()` 调用前后的内存访问，但它们不能将内存访问从 `fetch_add()` 调用之前移动到之后，或者反之亦然。`boost::memory_order_seq_cst` 是两个方向内存访问的严格边界。

`boost::memory_order_seq_cst` 是限制性最强的内存顺序。当未设置内存顺序时，默认使用它。因此，在示例 45.1《使用 `boost::atomic`》中，当使用 `operator++` 增加 `a` 时，将使用 `boost::memory_order_seq_cst`。



`boost::memory_order_seq_cst` 并不总是必要的。例如，在示例 45.3“带有 `boost::memory_order_seq_cst` 的 `boost::atomic`”中，不需要同步其他变量的内存访问，因为 `a` 是线程使用的唯一变量。`a` 在 `main()` 中被写入标准输出，但在两个线程终止之后。对 `join()` 的调用保证了 `a` 只在两个线程完成后才被读取。

### 示例 45.4. 带有 `memory_order_relaxed` 的 `boost::atomic`

```cpp
#include <boost/atomic.hpp>
#include <thread>
#include <iostream>

boost::atomic<int> a{0};

void thread()
{
  a.fetch_add(1, boost::memory_order_relaxed);
}

int main()
{
  std::thread t1{thread};
  std::thread t2{thread};
  t1.join();
  t2.join();
  std::cout << a << '\n';
}
```

示例 45.4“带有 `memory_order_relaxed` 的 `boost::atomic`”将内存顺序设置为 `boost::memory_order_relaxed`。这是限制性最弱的内存顺序：它允许内存访问的任意重排。此示例在此顺序下有效，是因为线程没有访问 `a` 之外的任何变量。因此，不需要特定的顺序。

### 示例 45.5. 带有 `memory_order_release` 和 `memory_order_acquire` 的 `boost::atomic`

```cpp
#include <boost/atomic.hpp>
#include <thread>
#include <iostream>

boost::atomic<int> a{0};
int b = 0;

void thread1()
{
  b = 1;
  a.store(1, boost::memory_order_release);
}

void thread2()
{
  while (a.load(boost::memory_order_acquire) != 1)
    ;
  std::cout << b << '\n';
}

int main()
{
  std::thread t1{thread1};
  std::thread t2{thread2};
  t1.join();
  t2.join();
}
```

示例 45.5“带有 `memory_order_release` 和 `memory_order_acquire` 的 `boost::atomic`”引入了内存顺序 `boost::memory_order_release` 和 `boost::memory_order_acquire`。

在代码中出现在 `boost::memory_order_release` 语句之前的内存访问将在 `boost::memory_order_release` 语句之前执行。编译器和处理器不能将内存访问从 `boost::memory_order_release` 之前移动到之后。然而，它们可以将内存访问从 `boost::memory_order_release` 之后移动到之前。

`boost::memory_order_acquire` 的工作类似于 `boost::memory_order_release`，但它指的是 `boost::memory_order_acquire` 之后的内存访问。编译器和处理器不能将内存访问从 `boost::memory_order_acquire` 语句之后移动到之前。然而，它们可以将内存访问从之前移动到 `boost::memory_order_acquire` 之后。

示例 45.5“带有 `memory_order_release` 和 `memory_order_acquire` 的 `boost::atomic`”在第一个线程中使用 `boost::memory_order_release` 来确保 `b` 在被设置为 1 之前已经设置。

队列的大小传递给构造函数。由于 `boost::lockfree::spsc_queue` 是用循环缓冲区实现的，因此示例 46.1“使用 `boost::lockfree::spsc_queue`”中的队列容量为 100 个元素。如果因为队列满而无法添加值，`push()` 将返回 `false`。示例没有检查 `push()` 的返回值，因为队列中恰好添加了 100 个数字。因此，100 个元素是足够的。

示例 46.2“带有 `boost::lockfree::capacity` 的 `boost::lockfree::spsc_queue`”工作方式与之前的示例相同，但这次循环缓冲区的大小是在编译时设置的。这是通过模板 `boost::lockfree::capacity` 实现的，它期望将容量作为模板参数。`q` 使用默认构造函数实例化——容量无法在运行时设置。

函数 `consume()` 已更改为使用 `consume_one()` 而不是 `pop()` 来读取数字。一个 lambda 函数作为参数传递给 `consume_one()`。`consume_one()` 像 `pop()` 一样读取一个数字，但该数字不会通过引用返回给调用者，而是作为 lambda 函数的唯一参数传递。

当线程终止时，`main()` 调用成员函数 `consume_all()` 而不是 `consume()`。`consume_all()` 的工作方式类似于 `consume_one()`，但它能确保在调用后队列为空。只要队列中还有元素，`consume_all()` 就会调用 lambda 函数。

### 示例 46.2. 带有 `boost::lockfree::capacity` 的 `boost::lockfree::spsc_queue`

```cpp
#include <boost/lockfree/spsc_queue.hpp>
#include <boost/lockfree/policies.hpp>
#include <thread>
#include <iostream>

using namespace boost::lockfree;

spsc_queue<int, capacity<100>> q;
int sum = 0;

void produce()
{
  for (int i = 1; i <= 100; ++i)
    q.push(i);
}

void consume()
{
  while (q.consume_one([](int i){ sum += i; }))
    ;
}

int main()
{
  std::thread t1{produce};
  std::thread t2{consume};
  t1.join();
  t2.join();
  q.consume_all([](int i){ sum += i; });
  std::cout << sum << '\n';
}
```

再次，示例 46.2“带有 `boost::lockfree::capacity` 的 `boost::lockfree::spsc_queue`”向标准输出写入了 `5050`。

示例 46.3“变变容器大小的 `boost::lockfree::queue`”在两个线程中执行 `consume()`。因为有多个线程从队列中读取数据，因此不能使用 `boost::lockfree::spsc_queue` 类。此示例改用了 `boost::lockfree::queue`。

得益于 `std::atomic`，对变量 `sum` 的访问现在也是线程安全的。

队列的大小设置为 100——这是传递给构造函数的参数。然而，这只是初始大小。默认情况下，`boost::lockfree::queue` 不是用循环缓冲区实现的。如果向队列添加的项超过了设置的容量，它会自动增加。如果初始大小不足，`boost::lockfree::queue` 会动态分配额外的内存。

### 示例 46.3. 变变容器大小的 `boost::lockfree::queue`

```cpp
#include <boost/lockfree/queue.hpp>
#include <thread>
#include <atomic>
#include <iostream>

boost::lockfree::queue<int> q{100};
std::atomic<int> sum{0};

void produce()
{
  for (int i = 1; i <= 10000; ++i)
    q.push(i);
}

void consume()
{
  int i;
  while (q.pop(i))
    sum += i;
}

int main()
{
  std::thread t1{produce};
  std::thread t2{consume};
  std::thread t3{consume};
  t1.join();
  t2.join();
  t3.join();
  consume();
  std::cout << sum << '\n';
}
```

这意味着 `boost::lockfree::queue` 并不一定是无锁的。

如果你想使用 MPI，则需要该标准的实现版本。虽然 MPI 定义了许多函数，但操作系统通常不会默认就支持这些函数。例如，Windows 桌面版本并未附带 `MPI` 支持。

最重要的 `MPI` 实现有 [MPICH](http://www.mpich.org/) 和 [Open MPI](http://www.open-mpi.org/)。`MPICH` 是最早的 MPI 实现之一，自 20 世纪 90 年代中期一直存在。`MPICH` 是一个成熟且可移植的实现，一直在活跃维护和更新。`Open MPI` 的第一个版本发布于 2005 年。由于 `Open MPI` 是一个协作项目，包含了许多负责早期 MPI 实现的开发者，因此 `Open MPI` 被视为未来的标准。然而，这并不意味着可以忽略 `MPICH`。有几个基于 `MPICH` 的 MPI 实现。例如，微软提供了一个名为 `Microsoft HPC Pack` 的 MPI 实现，它是基于 `MPICH` 的。

`MPICH` 为各种操作系统（如 Windows、Linux 和 OS X）提供了安装文件。如果你需要一个 MPI 实现且不想从源代码编译，那么 `MPICH` 安装文件是开始使用 MPI 的快速路径。

`MPICH` 安装文件包含了开发 MPI 程序所需的头文件和库。此外，它们还包含一个 MPI 运行环境。由于 MPI 程序在多个处理器上并发执行任务，因此它们在多个进程中运行。一个 MPI 程序会被启动多次，而不仅仅一次。同一个 MPI 程序的多个实例运行在多个处理器上，并通过 MPI 标准定义的函数进行通信。

你不能通过双击来启动 MPI 程序。你需要使用一个辅助程序，通常称为 `mpiexec`。你将你的 MPI 程序传递给 `mpiexec`，由它在 MPI 运行环境中启动你的程序。命令行选项决定了启动多少进程以及它们如何通信——例如，通过套接或共享内存。由于 MPI 运行环境会处理这些细节，因此你可以专注于并行编程。

如果你决定使用来自 `MPICH` 的安装文件，请注意 `MPICH` 只提供 64 位版本。你必须使用 64 位编译器来使用 `MPICH` 开发 MPI 程序，并构建 64 位的 `Boost.MPI`。

## 简单数据交换

`Boost.MPI` 是 MPI 标准的 C++ 接口。该库使用命名空间 `boost::mpi`。只需包含头文件 `boost/mpi.hpp` 即可访问所有类和函数。

### 示例 47.1. MPI 环境和通信器

```cpp
#include <boost/mpi.hpp>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  std::cout << world.rank() << ", " << world.size() << '\n';
}
```

示例 47.1“MPI 环境和通信器”是一个简单的 MPI 程序。它使用了你将在接后的所有示例中找到的两个类。`boost::mpi::environment` 初始化 MPI。构造函数调用了 MPI 标准中的 `MPI_Init()` 函数。析构函数调用 `MPI_Finalize()`。`boost::mpi::communicator` 用于创建通信器。通信器是 MPI 的核心概念之一，支持进程之间的数据交换。

`boost::mpi::environment` 是一个非常简单的类，只提供了几个成员函数。你可以调用 `initialized()` 来检查 MPI 是否已成功初始化。该成员函数返回一个 `bool` 类型的值。`processor_name()` 返回当前进程的名称（`std::string`）。而 `abort()` 会停止整个 MPI 程序，而不只是当前进程。你向 `abort()` 传递一个 `int` 值。该值将作为 MPI 程序的返回值传递给 MPI 运行环境。对于大多数 MPI 程序，你不需要这些成员函数。你通常在程序开始实例化 `boost::mpi::environment`，之后不再使用该对象——正如示例 47.1“MPI 环境和通信器”以及本章后续示例所示。

`boost::mpi::communicator` 更有趣。这个类是一个通信器，连接了属于 MPI 程序的进程。每个进程都有一个秩（rank），这是一个整数——所有进程都是被枚举的。进程可以通过调用通信器上的 `rank()` 来发现自己的秩。如果进程想知道有多少个进程，它调用 `size()`。

要运行示例 47.1“MPI 环境和通信器”，你必须使用你所使用的 MPI 实现提供的辅助程序。对于 `MPICH`，该辅助程序称为 `mpiexec`。你可以使用以下命令通过该程序运行示例 47.1“MPI 环境和通信器”：

```bash
mpiexec -n 4 sample.exe
```

`mpiexec` 期望一个 MPI 程序的名称和一个告诉它要启动多少进程的选项。选项 `-n 4` 告诉 `mpiexec` 启动 4 个进程。由于 MPI 运行环境处理了这些细节，你可以专注于并行编程。

如果你决定使用来自 `MPICH` 的安装文件，请注意 `MPICH` 只提供 64 位版本。你必须使用 64 位编译器来使用 `MPICH` 开发 MPI 程序，并构建 64 位的 `Boost.MPI`。

### 示例 47.2. 用于发送和接收的阻塞函数

```cpp
#include <boost/mpi.hpp>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
{
    int i;
    world.recv(1, 16, i);
    std::cout << i << '\n';
  }
  else if (world.rank() == 1)
  {
    world.send(0, 16, 99);
  }
}
```

`boost::mpi::communicator` 提供了两个简单的成员函数 `send()` 和 `recv()`，用于在进程之间交换数据。它们是阻塞函数，只有在数据发送或接收后才会返回。这对于 `recv()` 尤为重要。如果调用 `recv()` 时没有另一个进程发送数据，该调用将阻塞，进程会在调用处停滞。

在示例 47.2“用于发送和接收的阻塞函数”中，秩为 0 的进程通过 `recv()` 接收数据。秩为 1 的进程通过 `send()` 发送数据。如果你启动程序时进程超过两个，其他进程将在不执行任何操作的情况下退出。

你向 `send()` 传递三个参数：第一个参数是要发送目标进程的秩；第二个参数是标识数据的标签（tag）；第三个参数是数据。

标签始终整数。在示例 47.2 中，标签是 `16`。标签使得识别 `send()` 调用变得可能。你会看到标签也被用于 `recv()`。

传递给 `send()` 的第三个参数是 99。这个数字从 rank 为 1 的进程发送到 rank 为 0 的进程。Boost. 支持 支持原始类型。像 99 这样的 `int` 值可以直接被发送。

`recv()` 期望类似的参数。第一个参数是应该从哪个进程接收数据的进程 rank。第二个参数是将 `recv()` 调用与 `send()` 调用关联的标签（tag）。第三个参数是用于存储接收到的数据的变量。

如果你使用至少两个进程运行示例 47.2“用于发送和接收数据的阻塞函数”，则会显示 `99`。

### 示例 47.3. 从任何进程接收数据



```cpp
#include <boost/mpi.hpp>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    int i;
    world.recv(boost::mpi::any_source, 16, i);
    std::cout << i << '\n';
  }
  else
  {
    world.send(0, 16, world.rank());
  }
}
```

示例 47.3“从任何进程接收数据”基于示例 47.2“用于发送和接收数据的阻塞函数”。该示例不是发送数字 99，而是发送调用`send()`的进程的 rank。这可以是任何 rank 大于 0 的进程。

rank 为 0 的进程的`recv()`调用也发生了变化。第一个参数是`boost::mpi::any_source`。这意味着`recv()`调用将接受来自任何发送标签为 16 数据的进程的数据。

如果你使用两个进程启动示例 47.3“从任何进程接收数据”，则会显示`1`。毕竟，只有一个进程可以调用`send()`——即 rank 为 1 的进程。如果你用两个以上的进程启动程序，则无法确定将显示哪个数字。在这种情况下，多个进程将调用`send()`并尝试发送它们的 rank。哪个进程先调用，因此显示哪个 rank，是随机的。

`recv()`的返回类型为`boost::mpi::status`。该类提供了一个成员函数`source()`，它返回接收数据的进程的 rank。示例 47.4“使用`boost::mpi::status`检测发送者”会告诉你数字 99 是从哪个进程接收到的。

### 示例 47.4. 使用`boost::mpi::status`检测发送者

```cpp
#include <boost/mpi.hpp>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    int i;
    boost::mpi::status s = world.recv(boost::mpi::any_source, 16, i);
    std::cout << s.source() << ": " << i << '\n';
  }
  else
  {
    world.send(0, 16, 99);
  }
}
```

到目前为止，所有示例都使用`send()`和`recv()`来传输`int`值。在示例 47.5“使用`send()`和`recv()`传输数组”中，传输的是字符串。

`send()`和`recv()`也可以传输数组而不仅仅是单个值。示例 47.5“使用`send()`和`recv()`传输数组”传输了一个`char`数组中的字符串。由于`send()`和`recv()`支持如`char`等原始类型，因此`char`数组可以无问题地传输。

### 示例 47.5. 使用`send()`和`recv()`传输数组

```cpp
#include <boost/mpi.hpp>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    char buffer[14];
    world.recv(boost::mpi::any_source, 16, buffer, 13);
    buffer[13] = '\0';
    std::cout << buffer << '\n';
  }
  else
  {
    const char *c = "Hello, world!";
    world.send(0, 16, c);
  }
}
```

`send()`接收字符串作为第三个参数，并将字符串的大小作为第四个参数。`recv()`的第三个参数是用于存储接收数据的指针。第四个参数告诉`recv()`应该接收多少个`char`。示例 47.5“使用`send()`和`recv()`传输数组”向标准输出写入了`Hello, world!`。

### 示例 47.6. 使用`send()`和`recv()`传输字符串

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization.hpp>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    std::string s;
    world.recv(boost::mpi::any_source, 16, s);
    std::cout << s << '\n';
  }
  else
  {
    std::string s = "Hello, world!";
    world.send(0, 16, s);
  }
}
```

尽管 Boost.MPI 只支持原始类型，但这并不意味着无法传输非原始类型。Boost.MPI 与 Boost.Serialization 协作。示例 47.6“使用`send()`和`recv()`传输字符串”这次传输的不是`char`数组而是`std::string`。Boost.Serialization 提供了头文件`boost/serialization.hpp`，包含它即可使`std::string`可序列化。

## 异步数据交换

除了阻塞函数`send()`和`recv()`，Boost.MPI 还通过成员函数`isend()`和`irecv()`支持异步数据交换。名称以`i`开头，表示这些函数会立即返回。

### 示例 47.7. 使用`irecv()`异步接收数据

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization.hpp>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    std::string s;
    boost::mpi::request r = world.irecv(boost::mpi::any_source, 16, s);
    if (r.test())
      std::cout << s << '\n';
    else
      r.cancel();
  }
  else
  {
    std::string s = "Hello, world!";
    world.send(0, 16, s);
  }
}
```

示例 47.7“使用`irecv()`异步接收数据”使用阻塞函数`send()`发送字符串“Hello, world!”。然而，数据使用异步函数`irecv()`接收。该成员函数期望与`recv()`相同的参数。区别在于当`irecv()`返回时，无法保证数据已经接收到`s`中。

`irecv()`返回一个类型为`boost::mpi::request`的对象。你可以调用`test()`来检查是否已接收。该成员函数返回一个`bool`值。你可以根据需要频繁调用`test()`。由于`irecv()`是异步成员函数，可能第一次调用返回`false`而第二次返回`true`。这意味着异步操作在两次调用之间完成了。

示例 47.7“使用`irecv()`异步接收数据”仅调用了一次`test()`。如果已在`s`中接收到数据，则该变量将被写入标准输出流。如果没有接收到数据，则通过`cancel()`取消该异步操作。

如果你多次运行示例 47.7“使用`irecv()`异步接收数据”，有时会显示`Hello, world!`，有时则没有输出。结果取决于在调用`test()`之前是否接收到了数据。

你可以多次对`boost::mpi::request`调用`test()`，以检测异步操作何时完成。然而，你也可以像示例 47.8“使用`wait_all()`等待多个异步操作”那样调用阻塞函数`boost::mpi::wait_all()`。`boost::mpi::wait_all()`是一个阻塞函数，但它的优势是可以等待多个异步操作完成。`boost::mpi::wait_all()`在它所等待的所有异步操作都完成后返回。

### 示例 47.8. 使用`wait_all()`等待多个异步操作

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    boost::mpi::request requests[2];
    std::string s[2];
    requests[0] = world.irecv(1, 16, s[0]);
    requests[1] = world.irecv(2, 16, s[1]);
    boost::mpi::wait_all(requests, requests + 2);
    std::cout << s[0] << "; " << s[1] << '\n';
  }
  else if (world.rank() == 1)
  {
    std::string s = "Hello, world!";
    world.send(0, 16, s);
  }
  else if (world.rank() == 2)
  {
    std::string s = "Hello, moon!";
    world.send(0, 16, s);
  }
}
```

在示例 47.8“使用`wait_all()`等待多个异步操作”中，rank 1 的进程发送了“Hello, world!”，rank 2 的进程发送了“Hello, moon!”。由于接收数据的顺序并不重要，rank 0 调用了`irecv()`。由于程序只有在所有异步操作完成且所有数据都接收后才会产生输出，因此类型为`boost::mpi::request`的返回值被传递给`boost::mpi::wait_all()`。因为`boost::mpi::wait_all()`期望两个迭代器，所以类型为`boost::mpi::request`的对象被存储在数组中。起始和结束迭代器被传递给`boost::mpi::wait_all()`。

Boost.MPI 提供了额外的函数供你等待异步操作的完成。`boost::mpi::wait_any()`在恰好有一个异步操作完成时返回，而`boost::mpi::wait_some()`在至少有一个异步操作完成时返回。这两个函数都返回一个`std::pair`，用于指示哪个操作或哪些操作已完成。

`boost::mpi::test_all()`、`boost::mpi::test_any()`和`boost::mpi::test_some()`通过单次调用测试多个异步操作的状态。这些函数是非阻塞的，会立即返回。

## 集合数据交换

到目前为止引入的函数共享一种一对一的关系：即一个进程发送，另一个进程接收。连接通过标签（tag）建立。本节介绍了在多个进程中以相同参数调用但执行不同操作的函数。对于一个进程，该函数可能是发送数据；而对于另一个进程，它可能是接收数据。这些函数被称为集合操作。

### 示例 47.9. 使用`gather()`从多个进程接收数据

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <vector>
#include <string>
#include <iterator>
#include <algorithm>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  if (world.rank() == 0)
  {
    std::vector<std::string> v;
    boost::mpi::gather<std::string>(world, "", v, 0);
    std::ostream_iterator<std::string> out{std::cout, "\n"};
    std::copy(v.begin(), v.end(), out);
  }
  else if (world.rank() == 1)
  {
    boost::mpi::gather(world, std::string("Hello, world!"), v, 0);
  }
  else if (world.rank() == 2)
  {
    boost::mpi::gather(world, std::string("Hello, moon!"), v, 0);
  }
}
```

在示例 47.9“使用`gather()`从多个进程接收数据”中，在多个进程中调用了`boost::mpi::gather()`函数。该函数是发送还是接收取决于 rank。rank 为 1 和 2 的进程使用`boost::mpi::gather()`发送数据——即字符串“Hello, world!”和“Hello, moon!”——取决于进程的 rank。由于`boost::mpi::gather()`不是成员函数，通信器`world`也必须传递。

rank 为 0 的进程调用`boost::mpi::gather()`进行接收。由于数据需要存储在某处，因此传递了类型为`std::vector<std::string>`的对象。请注意`boost::mpi::gather()`不支持其他容器。

rank 为 0 的进程必须向`boost::mpi::gather()`传递`world`、一个要的字符串以及 0。这就是为什么 rank 为 1 和 2 的进程传递相同的参数。如果你用三个进程启动示例 47.9“使用`gather()`从多个进程接收数据”，将显示`Hello, world!`和`Hello, moon!`。如果你仔细观察输出，你会发现首先写入了一个空行。第一行是 rank 0 传递`boost::mpi::gather()`的空字符串。`v`中有三个字符串，分别从 rank 0、1、2 进程接收。vector 中元素的索引对应进程的 rank。如果你多次运行该示例，你将总是得到第一个元素为空字符串，第二个元素为“Hello, world!”，第三个元素为“Hello, moon!”。

请注意，不能用超过三个进程运行示例 47.9“使用`gather()`从多个进程接收数据”。如果你用`-n 4`启动`mpieec`，将没有数据输出。程序将挂起并必须通过`CTRL+C`终止。

集合操作必须在所有进程中执行。如果你的程序调用了如`boost::mpi::gather()`的函数，你必须确保该函数在所有进程中调用。否则将违反 MPI 标准。因为像`boost::mpi::gather()`这样的函数必须由所有进程调用，所以通常调用方式没有区别，如示例 47.9“使用`gather()`从多个进程接收数据”所示。将之前的示例与示例 47.10“使用`gather()`收集所有进程的数据”进行对比，它们执行的是相同的功能。

### 示例 47.10. 使用`gather()`收集所有进程的数据



```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <vector>
#include <string>
#include <iterator>
#include <algorithm>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  std::string s;
  if (world.rank() == 1)
    s = "Hello, world!";
  else if (world.rank() == 2)
    s = "Hello, moon!";
  std::vector<std::string> v;
  boost::mpi::gather(world, s, v, 0);
  std::ostream_iterator<std::string> out{std::cout, "\n"};
  std::copy(v.begin(), v.end(), out);
}
```

你在所有进程中调用集合操作的函数。通常，这些函数的定义能够一眼看出需要执行哪种操作，即使所有进程传递了相同的参数。

### 示例 47.10：使用 `gather()` 从所有进程收集数据

示例 47.10 使用了 `boost::mpi::gather()`，该函数会收集数据。数据被收集在作为 `boost::mpi::gather()` 最后一个参数传递的 rank 对应的进程中。该进程收集从所有其他进程接收的数据。用于存储数据的 `vector` 仅供收集数据的进程专门使用。

`boost::mpi::gather()` 从所有进程收集数据。这包含了收集数据的进程本身。在示例 47.10 中，即 rank 为 `0` 的进程。该进程向它自己的 `s` 发送了一个空字符串。该空字符串被存储在 `v` 中。正如你在接下来的示例中看到的，集合操作始终包含所有进程。

你可以使用任意数量的进程运行示例 47.10，因为每个进程都调用了 `boost::mpi::gather()`。如果你用三个进程运行该示例，结果将与之前的示例相似。

### 示例 47.11：使用 `scatter()` 在所有进程间分发数据

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <vector>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  std::vector<std::string> v{"Hello, world!", "Hello, moon!",
    "Hello, sun!"};
  std::string s;
  boost::mpi::scatter(world, v, s, 0);
  std::cout << world.rank() << ": " << s << '\n';
}
```

示例 47.11 使用了函数 `boost::mpi::scatter()`。它的作用与 `boost::mpi::gather()` 相反。`boost::mpi::gather()` 将多个进程的数据收集到一个进程中，而 `boost::mpi::scatter()` 则将数据从一个进程分发到多个进程。

示例 47.11 将 rank 为 `0` 的进程中 `v` 的数据分发到所有进程（包括其自身）。rank 为 `0` 的进程在 `s` 中接收字符串“Hello, world!”，rank 为 `1` 的进程在 `s` 中接收“Hello, moon!”，rank 为 `2` 的进程在 `s` 中接收“Hello, sun!”。

### 示例 47.12：使用 `broadcast()` 向所有进程发送数据

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  std::string s;
  if (world.rank() == 0)
    s = "Hello, world!";
  boost::mpi::broadcast(world, s, 0);
  std::cout << s << '\n';
}
```

`boost::mpi::broadcast()` 将数据从一个进程发送到所有进程。该函数与 `boost::mpi::scatter()` 的区别在于向所有进程发送相同的数据。在示例 47.12 中，所有进程都在 `s` 中接收到字符串“Hello, world!”。

### 示例 47.13：使用 `reduce()` 收集并分析数据

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <string>
#include <iostream>

std::string min(const std::string &lhs, const std::string &rhs)
{
  return lhs.size() < rhs.size() ? lhs : rhs;
}

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  std::string s;
  if (world.rank() == 0)
    s = "Hello, world!";
  else if (world.rank() == 1)
    s = "Hello, moon!";
  else if (world.rank() == 2)
    s = "Hello, sun!";
  std::string result;
  boost::mpi::reduce(world, s, result, 0);
  if (world.rank() == 0)
    std::cout << result << '\n';
}
```

`boost::mpi::reduce()` 从多个进程收集数据，类似于 `boost::mpi::gather()`。然而，数据并没有存储在 `vector` 中。如果你运行示例 47.13 三个进程，rank 为 `0` 的进程会在 `result` 中接收到字符串“Hello, sun!”。它们使用作为 `boost::mpi::reduce()` 第四个参数的 `min` 函数进行分析。如果你运行示例 47.13 超过三个进程，则会显示空字符串，因为……

### 示例 47.14：使用 `all_reduce()` 收集并分析数据

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <string>
#include <iostream>

std::string min(const std::string &lhs, const std::string &rhs)
{
  return lhs.size() < rhs.size() ? lhs : rhs;
}

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  std::string s;
  if (world.rank() == 0)
    s = "Hello, world!";
  else if (world.rank() == 1)
    s = "Hello, moon!";
  else if (world.rank() == 2)
    s = "Hello, sun!";
  std::string result;
  boost::mpi::all_reduce(world, s, result, min);
  std::cout << world.rank() << ": " << result << '\n';
}
```

示例 47.14 使用了函数 `boost::mpi::all_reduce()`，它收集并分析数据的方式类似于 `boost::mpi::reduce()`。这两个函数的区别在于，`boost::mpi::all_reduce()` 将分析结果发送给所有进程，而 `boost::mpi::reduce()` 仅让结果对作为最后一个参数传递的 rank 进程可用。因此，没有向 `boost::mpi::all_reduce()` 传递 rank。如果你用三个进程运行该示例，每个进程都会向标准输出流写入 `Hello, sun!`。

本章中的所有示例仅使用一个通信器，该通信器连接了所有进程。然而，创建多个通信器来连接进程的子集。这对于不需要由所有进程执行的集合操作特别有用。

### 示例 47.15：使用多个通信器

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  boost::mpi::communicator local = world.split(world.rank() < 2 ? 99 : 100);
  std::string s;
  if (world.rank() == 0)
    s = "Hello, world!";
  boost::mpi::broadcast(local, s, 0);
  std::cout << world.rank() << ": " << s << '\n';
}
```

示例 47.15 使用了 `boost::mpi::broadcast()` 函数。该函数将秩为 0 的进程的字符串“Hello, world!”发送到所有连接到通信器 `local` 的进程。秩为 0 的进程也必须连接到该通信器。

通信器 `local` 是通过调用 `split()` 创建的。`split()` 是在全局通信器 `world` 上调用的成员函数。`split()` 期望一个整数将进程连接在一起。所有向 `split()` 传递相同整数的进程都会连接到同一个通信器。传递给 `split()` 的整数值并不重要。重要的是，所有进程应该通过传递相同的值由某个特定的通信器连接起来。

在示例 47.15 中，秩为 0 和 1 的两个进程向 `split()` 传递了 99。如果启动程序时进程数超过两个，额外的进程将传递 100。这意味着前两个进程拥有一个 `local` 通信器，而所有其他进程拥有另一个。每个进程都连接到由 `split()` 返回的通信器。其他进程是否也连接到同一个通信器上，取决于其他进程是否向 `split()` 传递了相同的整数。

请注意，秩（rank）始终是相对于通信器的。最低秩始终是 0。在示例 47.15 中，相对于全局通信器秩为 0 的进程，相对于其本地通信器的秩也为 0。相对于全局通信器秩为 2 的进程，相对于其本地通信器的秩为 0。

如果你用两个或多个进程启动示例 47.15，`Hello, world!` 将显示两次——分别由相对于全局通信器秩为 0 和 1 的进程显示一次。由于 `s` 仅在全局秩为 0 的进程中被设为“Hello, world!”，因此该字符串只通过通信器发送给那些连接到相同通信器的进程。这仅仅是全局秩为 1 的进程，即是另一个向 `split()` 传递了 99 的进程。

### 示例 47.16：使用 group 分组进程

```cpp
#include <boost/mpi.hpp>
#include <boost/serialization/string.hpp>
#include <boost/range/irange.hpp>
#include <boost/optional.hpp>
#include <string>
#include <iostream>

int main(int argc, char *argv[])
{
  boost::mpi::environment env{argc, argv};
  boost::mpi::communicator world;
  boost::mpi::group local = world.group();
  boost::integer_range<int> r = boost::irange(0, 1);
  boost::mpi::group subgroup = local.exclude(r.begin(), r.end());
  boost::mpi::communicator others{world, subgroup};
  std::string s;
  boost::optional<int> rank = subgroup.rank();
  if (rank)
  {
    if (rank == 0)
      s = "Hello, world!";
    boost::mpi::broadcast(others, s, 0);
  }
  std::cout << world.rank() << ": " << s << '\n';
}
```

MPI 支持进程分组。这是通过 `boost::mpi::group` 类辅助完成的。如果你在通信器上调用成员函数 `group()`，所有连接到该通信器的进程将以 `boost::mpi::group` 类型对象的形式返回。你不能使用此对象进行通信。它只能用于形成一个新的进程组，然后从该组中创建一个通信器。

`boost::mpi::group` 提供了如 `include()` 和 `exclude()` 类的成员函数。你传递迭代器来包含或排除进程。`include()` 和 `exclude()` 返回一个 `boost::mpi::group` 类型的新组。

示例 47.16 向 `exclude()` 传递了两个迭代器，它们指向一个 `boost::integer_range` 类型的对象。该对象表示一个整数范围。它是通过函数 `boost::irange()` 创建的，该函数期望一个下界和一个上限。上限是一个不属于该范围的整数。在这个示例中，这意味着 `r` 只包含整数 0。

对 `exclude()` 的调用导致创建了 `subgroup`，它包含了秩为 0 的进程以外的所有进程。该组随后被用于创建一个新的通信器 `others`。这是通过将全局通信器 `world` 和 `subgroup` 传递给 `boost::mpi::communicator` 的构造函数来实现。

请注意，`others` 在秩为 0 的进程中是一个空的通信器。秩为 0 的进程没有连接到该通信器，但变量 `others` 在该进程中存在。你必须小心在该进程中使用 `others`。示例 47.16 通过在 `subgroup` 上调用 `rank()` 避免了这种情况。该成员函数不在组内的进程中返回一个空的 `boost::optional` 对象。其他进程接收相对于组的秩。如果 `rank()` 返回一个秩且不是空的 `boost::optional` 对象，则调用 `boost::mpi::broadcast()`。

# XI. 泛型编程

以下库支持泛型编程。使用这些库不需要了解模板元编程。

- `Boost.TypeTraits` 提供了检查类型属性的功能。
- `Boost.EnableIf` 可以与 `Boost.TypeTraits` 一起使用，例如根据返回类型重载函数。
- `Boost.Fusion` 使得创建异构容器成为可能——元素具有不同类型的容器。

## 48. Boost.TypeTraits

类型具有泛型编程可以利用的属性。`Boost.TypeTraits` 库提供了确定和更改这些属性所需的工具。



```cpp
#include <boost/type_traits.hpp>
#include <iostream>

using namespace boost;

int main()
{
  std::cout.setf(std::ios::boolalpha);
  std::cout << is_integral<int>::value << '\n';
  std::cout << is_floating_point<int>::value << '\n';
  std::cout << is_arithmetic<int>::value << '\n';
  std::cout << is_reference<int>::value << '\n';
}
```

示例 48.1，“确定类型类别”调用了多个函数来确定类型类别。`boost::is_integral` 检查一个类型是否为整型——即是否可以存储整数。`boost::is_floating_point` 检查一个类型是否存储浮点数。`boost::is_arithmetic` 检查一个类型是否支持算术运算符。而 `boost::is_reference` 可用于确定一个类型是否为引用。

`boost::is_integral` 和 `boost::is_floating_point` 是互斥的。一个类型要么存储整数，要么存储浮点数。然而，`boost::is_arithmetic` 和 `boost::is_reference` 可以适用于多个类别。例如，整数类型和浮点类型都支持算术运算。

来自 Boost.TypeTraits 的所有函数都通过 `value` 提供结果，该结果为 `true` 或 `false`。示例 48.1，“确定类型类别”对 `is_integral<int>` 和 `is_arithmetic<int>` 输出 `true`，而对 `is_floating_point<int>` 和 `is_reference<int>` 输出 `false`。由于所有这些函数都是模板，因此在运行时不进行任何处理。该示例在运行时的行为就像在代码中直接使用了 `true` 和 `false` 值一样。

在示例 48.1，“确定类型类别”中，各种函数的结果是 `bool` 类型的值，可以直接写入标准输出。如果结果需要由函数模板处理，则应将其作为类型转发，而不是作为 `bool` 值。

## 示例 48.2. `boost::true_type` 和 `boost::false_type`

```cpp
#include <boost/type_traits.hpp>
#include <iostream>

using namespace boost;

int main()
{
  std::cout.setf(std::ios::boolalpha);
  std::cout << is_same<is_integral<int>::type, true_type>::value << '\n';
  std::cout << is_same<is_floating_point<int>::type, false_type>::value <<
    '\n';
  std::cout << is_same<is_arithmetic<int>::type, true_type>::value << '\n';
  std::cout << is_same<is_reference<int>::type, false_type>::value << '\n';
}
```

除了 `value` 之外，Boost.TypeTraits 的函数还通过 `type` 提供结果。虽然 `value` 是一个 `bool` 值，但 `type` 是一个类型。就像 `value` 只能被设置为 `true` 或 `false` 一样，`type` 只能设置为两种类型之一：`boost::true_type` 或 `boost::false_type`。`type` 允许你将函数的结果作为类型传递给另一个函数。

示例 48.2，“`boost::true_type` 和 `boost::false_type`”使用 Boost.TypeTraits 的另一个函数 `is_same`。`is_same` 接收两个类型并检查它们是否相同。通过 `is_integral`、`is_floating_point`、`is_arithmetic` 和 `is_reference` 传递给 `is_same` 的结果是 `true_type` 或 `false_type`。`type` 允许你将函数的结果作为类型传递给另一个函数。

`Boost.EnableIf` 提供了 `boost::enable_if` 类，它是一个期望两个参数的模板。第一个参数是条件。第二个参数是条件为真时 `boost::enable_if` 表达式的类型。其技巧在于，如果条件为假，该类型就不存在，在这种情况下 `boost::enable_if` 表达式是无效的 C++ 代码。然而，在处理模板时，编译器不会对无效代码报错。相反，它会忽略该模板并寻找另一个可能匹配的模板。这个概念被称为 `SFINAE`，全称为“替换失败不是错误”（Substitution Failure Is Not An Error）。

在示例 49.1，“通过返回值使用 `boost::enable_if` 来重载函数”中，`boost::enable_if` 表达式中的两个条件都使用了 `std::is_same` 类。该类定义在 C++11 标准库中，允许你比较两个类型。由于这种比较的结果非真即假，因此使用 `std::is_same` 来定义条件就足够了。

### 示例 49.1. 通过返回值使用 `boost::enable_if` 来重载函数

```cpp
#include <boost/utility/enable_if.hpp>
#include <type_traits>
#include <string>
#include <iostream>

template <typename T>
typename boost::enable_if<std::is_same<T, int>, T>::type create()
{
  return 1;
}

template <typename T>
typename boost::enable_if<std::is_same<T, std::string>, T>::type create()
{
  return "Boost";
}

int main()
{
  std::cout << create<std::string>() << '\n';
}
```

如果条件为真，相应的 `create()` 函数应该返回一个与模板参数传递给 `create()` 的类型相同的对象。这就是为什么 `T` 被作为第二个参数传递给 `boost::enable_if`。如果条件为真，整个 `boost::enable_if` 表达式将被替换为 `T`。在示例 49.1，“通过返回值使用 `boost::enable_if` 来重载函数”中，编译器看到的不是一个返回 `int` 的函数，就是一个返回 `std::string` 的函数。如果用 `int` 或 `std::string` 以外的任何类型调用 `create()`，编译器将报告错误。

示例 49.1，“通过返回值使用 `boost::enable_if` 来重载函数”显示了 `Boost`。

示例 49.2，“使用 `boost::enable_if` 为一组类型特化函数”使用 `boost::enable_if` 为一组类型特化函数。该函数名为 `print()`，并接收一个参数。它可以被重载，尽管重载要求你使用具体类型。为了对 `short`、`int` 或 `long` 等一组类型执行相同的操作，你可以使用 `boost::enable_if` 定义适当的条件。示例 49.2，“使用 `boost::enable_if` 为一组类型特化函数”使用 `std::is_integral` 来实现这一点。第二个 `print()` 函数通过 `std::is_floating_point` 针对所有浮点数进行了重载。

### 示例 49.2. 使用 `boost::enable_if` 为一组类型特化函数

```cpp
#include <boost/utility/enable_if.hpp>
#include <type_traits>
#include <iostream>

template <typename T>
void print(typename boost::enable_if<std::is_integral<T>, T>::type i)
{
  std::cout << "Integral: " << i << '\n';
}

template <typename T>
void print(typename boost::enable_if<std::is_floating_point<T>, T>::type f)
{
  std::cout << "Floating point: " << f << '\n';
}

int main()
{
  print<short>(1);
  print<long>(2);
  print<double>(3.14);
}
```

# 50. Boost.Fusion

标准库提供了许多容器，它们有一个共同点：它们是同质的。也就是说，来自标准库的容器只能存储一种类型的元素。`std::vector<int>` 类型的向量只能存储 `int` 值，而 `std::vector<std::string>` 类型的向量只能存储字符串。



`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`std::vector<int>` 类型的向量只能存储 `int` 值，而 `std::vector<std::string>` 类型的向量只能存储字符串。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。

`[Boost.Fusion](http://www.boost.org/doc/libs/release/)` 使得创建异构容器成为可能。例如，`Boost.Fusion` 提供了处理异构容器的算法。严格来说，自 `C++11` 以来，标准库已经提供了更多功能。然而，`Boost.Fusion` 提供的函数超出了标准库的范围。



[Boost.Fusion](http://www.boost.org/doc/libs/release/) 使得创建异构容器成为可能。例如，Boost.Fusion 提供了处理异构容器的算法。严格来说，自 C++11 以来，标准库已经提供了更多功能。然而，Boost.Fusion 提供的函数超出了标准库的范围。

在示例 49.1 中，`boost::enable_if` 表达式中的两个条件都使用了 `std::is_same` 类。该类定义在 C++11 标准库中，允许你比较两个类型。由于这种比较的结果非真即假，因此使用 `std::is_same` 来定义条件就足够了。

### 示例 49.1. 通过返回值使用 `boost::enable_if` 来重载函数

```cpp
#include <boost/utility/enable_if.hpp>
#include <type_traits>
#include <string>
#include <iostream>

template <typename T>
typename boost::enable_if<std::is_same<T, int>, T>::type create()
{
  return 1;
}

template <typename T>
typename boost::enable_if<std::is_same<T, std::string>, T>::type create()
{
  return "Boost";
}

int main()
{
  std::cout << create<std::string>() << '\n';
}
```

如果条件为真，相应的 `create()` 函数应该返回一个与模板参数传递给 `create()` 的类型相同的对象。这就是为什么 `T` 被第二个参数传递给 `boost::enable_if`。如果条件为真，整个 `boost::enable_if` 表达式将被替换为 `T`。在示例 49.1 中，编译器看到的不是一个返回 `int` 的函数，要么一个返回 `std::string` 的函数。如果用 `int` 或 `std::string` 以外的任何类型调用 `create()`，编译器将报告错误。

示例 49.1 显示了 `Boost`。

示例 49.2, “使用 `boost::enable_if` 为一组类型特化函数” 使用 `boost::enable_if` 为一组类型特化函数。该函数名为 `print()`，并接收一个参数。它可以被重载，尽管重载要求你使用具体类型。为了对 `short`、`int` 或 `long` 等一组类型执行相同的操作，你可以使用 `boost::enable_if` 定义适当的条件。示例 49.2, “使用 `boost::enable_if` 为一组类型特化函数” 使用 `std::is_integral` 来实现这一点。第二个 `print()` 函数通过 `std::is_floating_point` 针对所有浮点数进行了重载。

### 示例 49.2. 使用 `boost::enable_if` 为一组类型特化函数

```cpp
#include <boost/utility/enable_if.hpp>
#include <type_traits>
#include <iostream>

template <typename T>
void print(typename boost::enable_if<std::is_integral<T>, T>::type i)
{
  std::cout << "Integral: " << i << '\n';
}

template <typename T>
void print(typename boost::enable_if<std::is_floating_point<T>, T>::type f)
{
  std::cout << "Floating point: " << f << '\n';
}

int main()
{
  print<short>(1);
  print<long>(2);
  print<double>(3.14);
}
```

# 50. Boost.Fusion

标准库提供了许多容器，它们有一个共同点：它们是同质的。也就是说，来自标准库的容器只能存储一种类型的元素。`std::vector<int>` 类型的向量只能存储 `int` 值，而 `std::vector<std::string>` 类型的向量只能存储字符串。

[Boost.Fusion](http://www.boost.org/doc/libs/release/) 使得创建异构容器成为可能。例如，Boost.Fusion 提供了处理异构容器的算法。严格来说，自 C++11 以来，标准库已经提供了更多功能。然而，Boost.Fusion 提供的函数超出了标准库的范围。

`boost::fusion::for_each()` 被设计为像 `std::for_each()` 一样工作。`std::for_each()` 只能迭代同质容器，而 `boost::fusion::for_each()` 可以处理异构容器。你将容器而不是迭代器传递给 `boost::fusion::for_each()`。如果你不想迭代容器中的所有元素，可以使用视图（view）。

```cpp
#include <boost/fusion/tuple.hpp>
#include <boost/fusion/view.hpp>
#include <boost/fusion/algorithm.hpp>
#include <boost/type_traits.hpp>
#include <boost/mpl/arg.hpp>
#include <string>
#include <iostream>

using namespace boost::fusion;

struct print
{
  template <typename T>
  void operator()(const T &t) const
  {
    std::cout << std::boolalpha << t << '\n';
  }
};

int main()
{
  typedef tuple<int, std::string, bool, double> tuple_type;
  tuple_type t{10, "Boost", true, 3.14};
  filter_view<tuple_type, boost::is_integral<boost::mpl::arg<1>>> v{t};
  for_each(v, print{});
}
```

Boost.Fusion 提供了视图（views），它们的作用类似于容器但并不存储数据。通过视图，可以不同的方式访问容器中的数据。视图类似于 Boost.Range 中的适配器。然而，Boost.Range 的适配器只能应用于一个容器，而 Boost.Fusion 的视图可以跨越多个容器的数据。

示例 50.3 “使用 `boost::fusion::filter_view` 过滤 Fusion 容器” 使用 `boost::fusion::filter_view` 类来过滤元组 `t`。该过滤器引导 `boost::fusion::for_each()` 仅写入整型类型的元素。

`boost::fusion::filter_view` 期望第一个模板参数是待过滤容器的类型。第二个模板参数必须是一个用于过滤元素的谓词（predicate）。该谓词必须根据元素的类型对元素进行过滤。

该库之所以被称为 Boost.Fusion，因为它结合了两个世界：C++ 程序在运行时处理值，在编译时处理类型。对于开发者来说，运行的值通常更重要。标准库中的大多数工具都在运行时处理值。为了在编译时处理类型，则使用了模板元编程（template meta programming）。值的处理取决于运行时的其他值，而类型的处理取决于编译时的其他类型。Boost.Fusion 允许你根据类型处理值。

传递给 `boost::fusion::filter_view` 的第二个模板参数是一个谓词，它将应用于元组中的每个类型。谓词期望一个类型作为参数，如果该类型应该是视图的一部分，则返回 `true`。如果返回 `false`，则该类型被过滤掉。

示例 50.3 “使用 `boost::fusion::filter_view` 过滤 Fusion 容器”使用了 Boost.TypeTraits 中的 `boost::is_integral` 类。`boost::is_integral` 是一个检查类型是否为整数类型的模板。由于模板参数必须传递给 `boost::fusion::filter_view`，使用了来自 Boost.MPL 的占位符 `boost::mpl::arg<1>` 来创建一个 lambda 函数。`boost::mpl::arg<1>` 类似于 Boost.Phoenix 中的 `boost::phoenix::place_holders::arg1`。在示例 50.3 “使用 `boost::fusion::filter_view` 过滤 Fusion 容器”中，视图 `v` 将仅包含元组中的 `int` 和 `bool` 元素，因此示例将向标准输出写入 `10` 和 `true`。

### 示例 50.4. 使用迭代器访问 Fusion 容器中的元素

```cpp
#include <boost/fusion/tuple.hpp>
#include <boost/fusion/iterator.hpp>
#include <boost/mpl/int.hpp>
#include <string>
#include <iostream>

using namespace boost::fusion;

int main()
{
  typedef tuple<int, std::string, bool, double> tuple_type;
  tuple_type t{10, "Boost", true, 3.14};
  auto it = begin(t);
  std::cout << *it << '\n';
  auto it2 = advance<boost::mpl::int_<2>>(it);
  std::cout << std::boolalpha << *it2 << '\n';
}
```

在看到 `boost::fusion::tuple` 和 `boost::fusion::for_each()` 之后，在示例 50.4 “使用迭代器访问 Fusion 容器中的元素”中发现迭代器并不应该感到意外。Boost.Fusion 提供了几个独立函数，例如 `boost::fusion::begin()` 和 `boost::fusion::advance()`，它们的工作方式与标准库中同名的函数相同。

迭代器需要递增的步数作为模板参数传递给 `boost::fusion::advance()`。示例再次使用了 Boost.MPL 中的 `boost::mpl::int_`。

`boost::fusion::advance()` 返回一个与传入的类型不同的迭代器。在示例 50.4 “使用迭代器访问 Fusion 容器中的元素”中使用 `boost::fusion::advance()` 处理到第一个迭代器 `it`。程序向标准输出写入了 `10` 和 `true`。

除了示例中引入的函数，Boost.Fusion 还提供了其他与迭代器协作的函数。这些包括 `boost::fusion::end()`、`boost::fusion::distance()`、`boost::fusion::next()` 和 `boost::fusion::prior()`。

到为止，我们只看到一个容器 `boost::fusion::tuple`。示例 50.5 “带有 `boost::fusion::vector` 的异构向量”引入了另一个容器 `boost::fusion::vector`。

`boost::fusion::vector` 是一个向量：元素通过索引访问。相反，它是使用独立函数 `boost::fusion::at()` 实现的。索引被封装在 `boost::mpl::int_` 中并作为模板参数传递。

### 示例 50.5. 带有 `boost::fusion::vector` 的异构向量

```cpp
#include <boost/fusion/container.hpp>
#include <boost/fusion/sequence.hpp>
#include <boost/mpl/int.hpp>
#include <string>
#include <iostream>

using namespace boost::fusion;

int main()
{
  typedef vector<int, std::string, bool, double> vector_type;
  vector_type v{10, "Boost", true, 3.14};
  std::cout << at<boost::mpl::int_<0>>(v) << '\n';

  auto v2 = push_back(v, 'X');
  std::cout << size(v) << '\n';
  std::cout << size(v2) << '\n';
  std::cout << back(v2) << '\n';
}
```

此示例向向量添加了一个 `char` 类型的新元素。这是通过独立函数 `boost::fusion::push_back()` 完成的。传递给 `boost::fusion::push_back()` 的两个参数是要元素的向量以及要添加的值。

`boost::fusion::push_back()` 返回一个新的向量。向量 `v` 没有被改变。新向量是原始向量添加元素后的副本。

此示例使用 `boost::fusion::size()` 获取向量 `v` 和 `v2` 的元素数量，并将两个值写入标准输出。程序显示 `4` 和 `5`。然后它调用 `boost::fusion::back()` 获取并将 `v2` 的最后一个元素写入标准输出，在这种情况下，该值为 `X`。

Boost.Fusion 提供了额外的异构容器，包括：`boost::fusion::deque`、`boost::fusion::list` 和 `boost::fusion::set`。示例 50.6, “使用 `boost::fusion::map` 的异构 map” 引入了 `boost::fusion::map`，这是一种用于存储键值对的容器。

示例 50.6, “使用 `boost::fusion::map` 的异构 map” 使用 `boost::fusion::map()` 创建了一个异构的 map。该 map 的类型为 `boost::fusion::map`，由于使用了 `auto` 关键字，示例中并没有显式写出该类型。

### 示例 50.6. 使用 `boost::fusion::map` 的异构 map

```cpp
#include <boost/fusion/container.hpp>
#include <boost/fusion/sequence.hpp>
#include <boost/fusion/algorithm.hpp>
#include <string>
#include <iostream>

using namespace boost::fusion;

int main()
{
  auto m = make_map<int, std::string, bool, double>("Boost", 10, 3.14, true);
  if (has_key<std::string>(m))
    std::cout << at_key<std::string>(m) << '\n';
  auto m2 = erase_key<std::string>(m);
  auto m3 = push_back(m2, make_pair<float>('X'));
  std::cout << std::boolalpha << has_key<std::string>(m3) << '\n';
}
```



类型为`boost::fusion::map`的 map 像`std::map`一样存储键值对。然而，Fusion map 中的键是类型。一个键值对由一个类型和一个映射到该类型的值组成。值的类型可以与键的类型不同。在示例 50.6，“使用`boost::fusion::map`的异构 map”中，字符串“Boost”被映射到键`int`。

在创建 map 之后，调用`boost::fusion::has_key()`来检查是否存在键`std::string`类型。然后，调用`boost::fusion::at_key()`获取映射到该键的值。由于数字 10 被映射到`std::string`，因此它被写入标准输出。

随后使用`boost::fusion::erase_key()`删除了该键值对。这不会改变 map`m`。`boost::fusion::erase_key()`返回一个缺少了被删除键值对的新 map。

调用`boost::fusion::push_back()`向 map 添加了一个新的键值对。该键为`float`，值为“X”。调用`boost::fusion::make_pair()`来创建这个新的键值对。此函数类似于`std::make_pair()`。

最后，再次调用`boost::fusion::has_key()`检查 map 是否包含键`std::string`。由于它已被删除，因此返回`false`。

请注意，在调用`boost::fusion::at_key()`之前，你不需要调用`boost::fusion::has_key()`来检查键是否存在。如果传递给`boost::fusion::at_key()`的键在 map 中不存在，会导致编译错误。

Boost.Fusion 提供了几个宏，让你可以使用结构作为 Fusion 容器。这是可能的，因为结构可以作为异构容器。示例 50.7，“结构的 Fusion 适配器”得益于宏`BOOST_FUSION_ADAPT_STRUCT`定义了一个可以作为 Fusion 容器使用的结构。这使得结构能够配合`boost::fusion::at()`或`boost::fusion::back()`等函数使用。

### 示例 50.7. 结构的 Fusion 适配器

```cpp
#include <boost/fusion/adapted.hpp>
#include <boost/fusion/sequence.hpp>
#include <boost/mpl/int.hpp>
#include <iostream>

struct strct
{
  int i;
  double d;
};

BOOST_FUSION_ADAPT_STRUCT(strct,
  (int, i)
  (double, d)
)

using namespace boost::fusion;

int main()
{
  strct s = {10, 3.14};
  std::cout << at<boost::mpl::int_<0>>(s) << '\n';
  std::cout << back(s) << '\n';
}
```

Boost.Fusion 支持如`std::pair`和`boost::tuple`等结构，而无需使用宏。你只需要包含头文件`boost/fusion/adapted.hpp`（参见示例 50.8，“对`std::pair`的 Fusion 支持”）。

`cooperative()`向标准输出输出了`Hello`。随后，函数像调用函数一样访问了`sink`。这是因为`push_type`重载了`operator()`。当`main()`中的`source`代表协程`cooperative()`时，`cooperative()`中的`sink`则代表函数`main()`。调用`sink`会使`cooperative()`返回，`main()`从`cooperative()`被调用的地方继续执行，并向标准输出输出一个逗号。

然后，`main()`像调用函数一样调用了`source`。同样，这是通过重载的`operator()`实现的。这一次，`cooperative()`从上次停止的地方继续，向标准输出输出了`world`。由于`cooperative()`中没有其他代码，协程结束。它返回到`main()`，后者向标准输出输出一个感叹号。

结果是示例 51.1，“使用协程”显示了`Hello, world!`。

你可以将协程理解为协作线程。在某种程度上，函数`main()`和`cooperative()`并发运行。代码在`main()`和`cooperative()`之间切换执行。每个函数内部的指令是顺序执行的。得益于协程，函数在执行另一个函数之前不需要返回。

### 示例 51.2. 从协程返回值

```cpp
#include <boost/coroutine/all.hpp>
#include <functional>
#include <iostream>

using boost::coroutines::coroutine;

void cooperative(coroutine<int>::push_type &sink, int i)
{
  int j = i;
  sink(++j);
  sink(++j);
  std::cout << "end\n";
}

int main()
{
  using std::placeholders::_1;
  coroutine<int>::pull_type source{std::bind(cooperative, _1, 0)};
  std::cout << source.get() << '\n';
  source();
  std::cout << source.get() << '\n';
  source();
}
```

示例 51.2，“从协程返回值”与之前的示例类似。这一次，模板`boost::coroutines::coroutine`使用`int`实例化。这使得从协程向调用者返回`int`成为可能。

`int`值的传递方向取决于`pull_type`和`push_type`使用的位置。示例在`main()`中使用`pull_type`实例化。`cooperative()`访问`push_type`类型的对象。`push_type`发送值，而`pull_type`接收值；因此，数据传输的方向被设定了。

`cooperative()`调用带有`int`类型参数的`sink`。该参数是必要的，因为协程是用数据类型`int`实例化的。传递给`sink`的值是在`main()`中通过`pull_type`提供的成员函数`get()`接收到的。示例 51.2，“从协程返回值”也说明了带有多个参数的函数如何作为协程使用。`cooperative()`有一个额外的`int`类型参数，它不能直接传递给`pull_type`的构造函数。示例使用`std::bind()`将函数与`pull_type`链接。

示例向标准输出输出了`1`和`2`，然后是`end`。

### 示例 51.3. 向协程传递两个值

```cpp
#include <boost/coroutine/all.hpp>
#include <tuple>
#include <string>
#include <iostream>

using boost::coroutines::coroutine;

void cooperative(coroutine<std::tuple<int, std::string>>::pull_type &source)
{
  auto args = source.get();
  std::cout << std::get<0>(args) << " " << std::get<1>(args) << '\n';
  source();
  args = source.get();
  std::cout << std::get<0>(args) << " " << std::get<1>(args) << '\n';
}

int main()
{
  coroutine<std::tuple<int, std::string>>::push_type sink{cooperative};
  sink(std::make_tuple(0, "aaa"));
  sink(std::make_tuple(1, "bbb"));
  std::cout << "end\n";
}
```

示例 51.3，“向协程传递两个值”使用了`main()`中的`push_type`和`cooperative()`中的`pull_type`，这意味着数据从调用者传输到协程。

此示例说明了如何传递多个值。Boost.Coroutine 不支持多个值。但是，通过使用`std::tuple`，我们可以传递多个值。示例 51.3，“向协程传递两个值”使用了`main()`中的`push_type`和`cooperative()`中的`pull_type`，这意味着数据从调用者传输到协程。

[Boost.Parameter](http://www.boost.org/libs/parameter)使得以键值对的形式传递参数成为可能。该库除了支持函数参数外，还支持模板参数。如果你正在使用长参数列表，且参数的顺序和意义难以记忆，那么 Boost.Parameter 特别有用。键值对允许你以任何顺序传递参数。由于每个值都带有一个键传递的，因此各种值的含义也更加清晰。

示例 53.1，“作为键值对的函数参数”定义了一个函数`complicated()`，该函数期望五个参数。这些参数可以以任何顺序传递。Boost.Parameter 提供了宏`BOOST_PARAMETER_FUNCTION`来定义这样的函数。

在使用`BOOST_PARAMETER_FUNCTION`之前，必须先定义键值对的参数。这是通过宏`BOOST_PARAMETER_NAME`完成的，该宏只需传入一个参数名称。示例中使用了五次`BOOST_PARAMETER_NAME`来定义参数名称`a`、`b`、`c`、`d`和`e`。

请注意，参数名称自动定义在命名空间`tag`中。这可以避免与程序中同名的定义发生冲突。

在定义参数名称后，使用`BOOST_PARAMETER_FUNCTION`来定义函数`complicated()`。传递给`BOOST_PARAMETER_FUNCTION`的第一个参数是返回值类型。在示例中是`void`。请注意，类型必须封装在括号中——第一个参数是`(void)`。

第二个参数是正在定义的函数名称。第三个参数是包含参数名称的命名空间。在第四个参数中，通过访问参数名称来进行进一步指定。

### 示例 53.1. 作为键值对的函数参数

```cpp
#include <boost/parameter.hpp>
#include <string>
#include <iostream>
#include <ios>

BOOST_PARAMETER_NAME(a)
BOOST_PARAMETER_NAME(b)
BOOST_PARAMETER_NAME(c)
BOOST_PARAMETER_NAME(d)
BOOST_PARAMETER_NAME(e)

BOOST_PARAMETER_FUNCTION(
  (void),
  complicated,
  tag,
  (required
    (a, (int))
    (b, (char))
    (c, (double))
    (d, (std::string))
    (e, *)
  )
)
{
  std::cout.setf(std::ios::boolalpha);
  std::cout << a << '\n';
  std::cout << b << '\n';
  std::cout << c << '\n';
  std::cout << d << '\n';
  std::cout << e << '\n';
}

int main()
{
  complicated(_c = 3.14, _a = 1, _d = "Boost", _b = 'B', _e = true);
}
```

在示例 53.1，“作为键值对的函数参数”中，第四个参数以`required`开始，这是一个关键字，使得随后的参数是强制性的。`required`后面跟着一个或多个由参数名称和类型组成的对。将类型封装在括号中是非常重要的。

参数`a`、`b`、`c`和`d`使用了不同的类型。例如，`a`可用于向`complicated()`传递一个`int`值。`e`没有给出类型。相反，使用了星号，这表示所传递的值可以是任何类型。`e`是一个模板参数。

在将各种参数传递给`BOOST_PARAMETER_FUNCTION`之后，将定义函数体。这与常例一样在一对大括号之间完成。可以在函数体中访问参数。它们可以像变量一样使用，使用在`BOOST_PARAMETER_FUNCTION`中分配的类型。示例 53.1，“作为键值对的函数参数”将参数写入标准输出。

在`main()`中调用了`complicated()`。参数以任意顺序传递给`complicated()`。参数名称以下划线开头。Boost.Parameter 使用下划线来避免与其他变量发生名称冲突。

### 注意

在 C++ 中要键键值对的形式传递函数参数，你也可以使用[命名参数用法，](http://www.parashift.com/c++-faq/named-parameter-idiom.html)，它不需要像 Boost.Parameter 这样的库。

### 示例 53.2. 可选函数参数

```cpp
#include <boost/parameter.hpp>
#include <string>
#include <iostream>
#include <ios>

BOOST_PARAMETER_NAME(a)
BOOST_PARAMETER_NAME(b)
BOOST_PARAMETER_NAME(c)
BOOST_PARAMETER_NAME(d)
BOOST_PARAMETER_NAME(e)

BOOST_PARAMETER_FUNCTION(
  (void),
  complicated,
  tag,
  (required
    (a, (int))
    (b, (char))
    (c, (double))
    (d, (std::string))
    (e, *)
  )
)
{
  std::cout.setf(std::ios::boolalpha);
  std::cout << a << '\n';
  std::cout << b << '\n';
  std::cout << c << '\n';
  std::cout << d << '\n';
  std::cout << e << '\n';
}

int main()
{
  complicated(_c = 3.14, _a = 1, _d = "Boost", _b = 'B', _e = true);
}
```

`BOOST_PARAMETER_FUNCTION`也支持可选参数。在示例 53.2，“可选函数参数”中，参数`c`、`d`和`e`是可选的。它们在`BOOST_PARAMETER_FUNCTION`中使用`optional`关键字定义。

可选参数的定义与强制参数一样：参数名称后面跟着类型。和常一样，类型被封装在括号中。在调用`complicated()`时，只传递了`a`和`b`。这些是参数。

Boost.Parameter 除了`BOOST_PARAMETER_FUNCTION`之外还提供了宏。例如，你可以使用`BOOST_PARAMETER_MEMBER_FUNCTION`来定义成员函数，使用`BOOST_PARAMETER_CONST_MEMBER_FUNCTION`来定义常量成员函数。

你可以使用 Boost.Parameter 定义尝试自动为参数赋值的函数。在这种情况下，你不需要传递键值对——仅传递值就足够了。如果所有值的类型都不同，Boost.Parameter 可以检测哪个值属于哪个参数。这可能需要你对模板编程有更深入了解。

### 示例 53.3. 作为键值对的模板参数

示例 53.3，“作为键值对的模板参数”使用 Boost.Parameter 以键值对的形式传递模板参数。与函数一样，可以以任何顺序传递模板参数。

该示例定义了一个类`complicated`，它期望三个模板参数。由于参数顺序并不重要，因此被称为`A`、`B`和`C`。`A`、`B`和`C`并不是访问类模板时使用的参数名称。与函数一样，参数名称是使用宏定义的。对于模板参数，使用了`BOOST_PARAMETER_TEMPLATE_KEYWORD`。示例定义了三个参数名称`integral_type`、`floating_point_type`和`any_type`。

`boost::parameter::parameters`是描述参数的元组。强制参数用`boost::parameter::required`标记。



`boost::parameter::required` 需要两个参数。第一个是使用 `BOOST_PARAMETER_TEMPLATE_KEYWORD` 定义的参数名称。第二个是标识参数可能被设置的类型。例如，`integral_type` 可以被设置为整数类型。该要求通过 `std::is_integral<_>` 表达。`std::is_integral<_>` 是一个基于 Boost.MPL 的 lambda 函数。`boost::mpl::placeholders::_` 是该库提供的一个占位符。如果将 `integral_type` 设置的类型传递给 `std::is_integral` 而不是 `boost::mpl::placeholders::_`，并且结果为真，则使用该有效类型。其他参数 `floating_point_type` 和 `any_type` 的要求定义也类似。

### 示例 53.3. 作为键值对的模板参数

```cpp
#include <boost/parameter.hpp>
#include <boost/mpl/placeholders.hpp>
#include <type_traits>
#include <typeinfo>
#include <iostream>

BOOST_PARAMETER_TEMPLATE_KEYWORD(integral_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(floating_point_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(any_type)

using namespace boost::parameter;
using boost::mpl::placeholders::_;

typedef parameters<
  required<tag::integral_type, std::is_integral<_>>,
  required<tag::floating_point_type, std::is_floating_point<_>>,
  required<tag::any_type, std::is_object<_>>
> complicated_signature;

template <class A, class B, class C>
class complicated
{
public:
  typedef typename complicated_signature::bind<A, B, C>::type args;
  typedef typename value_type<args, tag::integral_type>::type integral_type;
  typedef typename value_type<args, tag::floating_point_type>::type
    floating_point_type;
  typedef typename value_type<args, tag::any_type>::type any_type;
};

int main()
{
  typedef complicated<floating_point_type<double>, integral_type<int>,
    any_type<bool>> c;
  std::cout << typeid(c::integral_type).name() << '\n';
  std::cout << typeid(c::floating_point_type).name() << '\n';
  std::cout << typeid(c::any_type).name() << '\n';
}
```

在创建并定义签名为 `complicated_signature` 后，它被类 `complicated` 使用。首先，该签名通过 `complicated_signature::bind` 绑定到模板参数 `A`、`B` 和 `C`。新类型 `args` 代表了所传递的模板参数与模板参数必须满足的要求之间的连接。接下来，访问 `args` 以获取参数值。这是通过 `boost::parameter::value_type` 实现的。`boost::parameter::value_type` 期望接收 `args` 和一个参数。该参数决定了创建的类型。在示例 53.3 中，`complicated` 类中的类型定义 `integral_type` 被用于获取传递给 `complicated` 的参数 `integral_type` 的类型。

`main()` 访问 `complicated` 以实例化该类。参数 `integral_type` 被设置为 `int`，`floating_point_type` 设置为 `double`，`any_type` 设置为 `bool`。传递参数的顺序并不重要。然后通过 `typeid` 访问类型定义 `integral_type`、`floating_point_type` 和 `any_type` 以获取它们的底层类型。使用 Visual C++ 2013 编译，示例向标准输出输出 `int`、`double` 和 `bool`。

### 示例 53.4. 可选模板参数

```cpp
#include <boost/parameter.hpp>
#include <boost/mpl/placeholders.hpp>
#include <type_traits>
#include <typeinfo>
#include <iostream>

BOOST_PARAMETER_TEMPLATE_KEYWORD(integral_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(floating_point_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(any_type)

using namespace boost::parameter;
using boost::mpl::placeholders::_;

typedef parameters<
  required<tag::integral_type, std::is_integral<_>>,
  optional<tag::floating_point_type, std::is_floating_point<_>>,
  optional<tag::any_type, std::is_object<_>>
> complicated_signature;

template <class A, class B = void_, class C = void_>
class complicated
{
public:
  typedef typename complicated_signature::bind<A, B, C>::type args;
  typedef typename value_type<args, tag::integral_type>::type integral_type;
  typedef typename value_type<args, tag::floating_point_type, float>::type
    floating_point_type;
  typedef typename value_type<args, tag::any_type, bool>::type any_type;
};

int main()
{
  typedef complicated<floating_point_type<double>, integral_type<int>,
    any_type<bool>> c;
  // 可选参数的实现细节
}
```

### Boost.Conversion

Boost.Conversion 在头文件 `boost/cast.hpp` 中定义了转换运算符 `polymorphic_cast` 和 `polymorphic_downcast`。它们设计用于更精确地处理类型转换——通常使用 `dynamic_cast` 完成。

#### 示例 54.1. 使用 `dynamic_cast` 进行向下转换和交叉转换

```cpp
#include <iostream>

struct base1 { virtual ~base1() = default; };
struct base2 { virtual ~base2() = default; };
struct derived : public base1, public base2 {};

void downcast(base1 *b1) {
  derived *d = dynamic_cast<derived*>(b1);
}

void crosscast(base1 *b1) {
  base2 *b2 = dynamic_cast<base2*>(b1);
}

int main() {
  derived *d = new derived;
  downcast(d);

  base1 *b1 = new derived;
  crosscast(b1);
}
```

#### 示例 54.2. 使用 `polymorphic_downcast` 和 `polymorphic_cast` 进行向下转换和交叉转换

```cpp
#include <boost/cast.hpp>
#include <iostream>

struct base1 { virtual ~base1() = default; };
struct base2 { virtual ~base2() = default; };
struct derived : public base1, public base2 {};

void downcast(base1 *b1) {
  derived *d = boost::polymorphic_downcast<derived*>(b1);
}

void crosscast(base1 *b1) {
  base2 *b2 = boost::polymorphic_cast<base2*>(b1);
}

int main() {
  derived *d = new derived;
  downcast(d);

  base1 *b1 = new derived;
  crosscast(b1);
}
```



`boost::parameter::required` 需要两个参数。第一个是使用 `BOOST_PARAMETER_TEMPLATE_KEYWORD` 定义的参数名称。第二个是标识参数可能被设置的类型。例如，`integral_type` 可以被设置为整数类型。该要求通过 `std::is_integral<_>` 表达。`std::is_integral<_>` 是一个基于 Boost.MPL 的 lambda 函数。`boost::mpl::placeholders::_` 是该库提供的一个占位符。如果将 `integral_type` 设置的类型传递给 `std::is_integral` 而不是 `boost::mpl::placeholders::_`，并且结果为真，则使用该有效类型。其他参数 `floating_point_type` 和 `any_type` 的要求定义也类似。

### 示例 53.3. 作为键值对的模板参数

```cpp
#include <boost/parameter.hpp>
#include <boost/mpl/placeholders.hpp>
#include <type_traits>
#include <typeinfo>
#include <iostream>

BOOST_PARAMETER_TEMPLATE_KEYWORD(integral_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(floating_point_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(any_type)

using namespace boost::parameter;
using boost::mpl::placeholders::_;

typedef parameters<
  required<tag::integral_type, std::is_integral<_>>,
  required<tag::floating_point_type, std::is_floating_point<_>>,
  required<tag::any_type, std::is_object<_>>
> complicated_signature;

template <class A, class B, class C>
class complicated
{
public:
  typedef typename complicated_signature::bind<A, B, C>::type args;
  typedef typename value_type<args, tag::integral_type>::type integral_type;
  typedef typename value_type<args, tag::floating_point_type>::type
    floating_point_type;
  typedef typename value_type<args, tag::any_type>::type any_type;
};

int main()
{
  typedef complicated<floating_point_type<double>, integral_type<int>,
    any_type<bool>> c;
  std::cout << typeid(c::integral_type).name() << '\n';
  std::cout << typeid(c::floating_point_type).name() << '\n';
  std::cout << typeid(c::any_type).name() << '\n';
}
```

在创建并定义签名为 `complicated_signature` 后，它被类 `complicated` 使用。首先，该签名通过 `complicated_signature::bind` 绑定到模板参数 `A`、`B` 和 `C`。新类型 `args` 代表了所传递的模板参数与模板参数必须满足的要求之间的连接。接下来，访问 `args` 以获取参数值。这是通过 `boost::parameter::value_type` 实现的。`boost::parameter::value_type` 期望接收 `args` 和一个参数。该参数决定了创建的类型。在示例 53.3 中，`complicated` 类中的类型定义 `integral_type` 被用于获取传递给 `complicated` 的参数 `integral_type` 的类型。

`main()` 访问 `complicated` 以实例化该类。参数 `integral_type` 被设置为 `int`，`floating_point_type` 设置为 `double`，`any_type` 设置为 `bool`。传递参数的顺序并不重要。然后通过 `typeid` 访问类型定义 `integral_type`、`floating_point_type` 和 `any_type` 以获取它们的底层类型。使用 Visual C++ 2013 编译，示例向标准输出输出 `int`、`double` 和 `bool`。

### 示例 53.4. 可选模板参数

```cpp
#include <boost/parameter.hpp>
#include <boost/mpl/placeholders.hpp>
#include <type_traits>
#include <typeinfo>
#include <iostream>

BOOST_PARAMETER_TEMPLATE_KEYWORD(integral_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(floating_point_type)
BOOST_PARAMETER_TEMPLATE_KEYWORD(any_type)

using namespace boost::parameter;
using boost::mpl::placeholders::_;

typedef parameters<
  required<tag::integral_type, std::is_integral<_>>,
  optional<tag::floating_point_type, std::is_floating_point<_>>,
  optional<tag::any_type, std::is_object<_>>
> complicated_signature;

template <class A, class B = void_, class C = void_>
class complicated
{
public:
  typedef typename complicated_signature::bind<A, B, C>::type args;
  typedef typename value_type<args, tag::integral_type>::type integral_type;
  typedef typename value_type<args, tag::floating_point_type, float>::type
    floating_point_type;
  typedef typename value_type<args, tag::any_type, bool>::type any_type;
};

int main()
{
  typedef complicated<floating_point_type<double>, integral_type<int>,
    any_type<bool>> c;
  // 可选参数的实现细节
}
```

### Boost.Conversion

Boost.Conversion 在头文件 `boost/cast.hpp` 中定义了转换运算符 `polymorphic_cast` 和 `polymorphic_downcast`。它们设计用于更精确地处理类型转换——通常使用 `dynamic_cast` 完成。

#### 示例 54.1. 使用 `dynamic_cast` 进行向下转换和交叉转换

```cpp
#include <iostream>

struct base1 { virtual ~base1() = default; };
struct base2 { virtual ~base2() = default; };
struct derived : public base1, public base2 {};

void downcast(base1 *b1) {
  derived *d = dynamic_cast<derived*>(b1);
}

void crosscast(base1 *b1) {
  base2 *b2 = dynamic_cast<base2*>(b1);
}

int main() {
  derived *d = new derived;
  downcast(d);

  base1 *b1 = new derived;
  crosscast(b1);
}
```

#### 示例 54.2. 使用 `polymorphic_downcast` 和 `polymorphic_cast` 进行向下转换和交叉转换

```cpp
#include <boost/cast.hpp>
#include <iostream>

struct base1 { virtual ~base1() = default; };
struct base2 { virtual ~base2() = default; };
struct derived : public base1, public base2 {};

void downcast(base1 *b1) {
  derived *d = boost::polymorphic_downcast<derived*>(b1);
}

void crosscast(base1 *b1) {
  base2 *b2 = boost::polymorphic_cast<base2*>(b1);
}

int main() {
  derived *d = new derived;
  downcast(d);

  base1 *b1 = new derived;
  crosscast(b1);
}
```

`boost::polymorphic_downcast`（参见示例 54.2，“使用 `polymorphic_downcast` 和 `polymorphic_cast` 进行向下转换和交叉转换”）只能用于向下类型转换（downcasts），因为它使用 `static_cast` 来执行转换。由于 `static_cast` 不会动态检查转换的有效性，因此 `boost::polymorphic_downcast` 必须仅在转换是安全时才使用。在调试构建版本中，`boost::polymorphic_downcast` 使用 `dynamic_cast` 和 `assert()` 来确保类型转换是有效的。此测试仅在未定义 `NDEBUG` 宏时执行，而这通常是调试构建的情况。

交叉类型转换（cross casts）需要 `boost::polymorphic_cast`。`boost::polymorphic_cast` 使用 `dynamic_cast`，这是唯一可以执行交叉转换的转换操作符。使用 `boost::polymorphic_cast` 替 `dynamic_cast` 更好，因为在发生错误时后者会抛出 `std::bad_cast` 类型的异常，而 `dynamic_cast` 在类型转换失败时会返回空指针。

仅使用 `boost::polymorphic_downcast` 和 `boost::polymorphic_cast` 来转换指针；否则请使用 `dynamic_cast`。由于 `boost::polymorphic_downcast` 基于 `static_cast`，它无法将基类对象转换为派生类对象。此外，使用 `boost::polymorphic_cast` 转换指针以外的类型也是没有意义的，因为如果转换失败，`dynamic_cast` 将抛出 `std::bad_cast` 类型的异常。

# 第 XIII 部分. 错误处理

以下库支持错误处理。

*   Boost.System 提供了描述和识别错误的类。从 C++11 开始，这些类已成为标准库的一部分。

*   Boost.Exception 允许在异常抛出后向其附带数据。

# 55. Boost.System



[Boost.System](http://www.boost.org/libs/system) 是一个库，它本质上定义了四个类来识别错误。这四个类都随着 C++11 添加到了标准库中。如果你的开发环境支持 C++11，你就不需要使用 Boost.System。然而，由于许多 Boost 库使用了 Boost.System，你可能会通过其他库遇到 Boost.System。

`boost::system::error_code` 是 Boost.System 中基础的类；它代表特定操作系统的错误。由于操作系统通常会枚举错误，`boost::system::error_code` 将错误代码保存在 `int` 类型的变量中。Example 55.1, “Using `boost::system::error_code`”说明了如何使用该类。

### 示例 55.1. 使用 `boost::system::error_code`

```cpp
#include <boost/system/error_code.hpp>
#include <iostream>

using namespace boost::system;

void fail(error_code &ec)
{
  ec = errc::make_error_code(errc::not_supported);
}

int main()
{
  error_code ec;
  fail(ec);
  std::cout << ec.value() << '\n';
}
```

Example 55.1, “Using `boost::system::error_code`”定义了函数 `fail()`，它用于返回错误。为了让调用者检测到 `fail()` 是否失败，通过引用传递了一个类型为 `boost::system::error_code` 的对象。Boost 库提供的许多函数都这样使用 `boost::system::error_code`。例如，Boost.Asio 提供了函数 `boost::asio::ip::host_name()`，你可以向其传递一个类型为 `boost::system::error_code` 的对象。

Boost.System 在 `boost::system::errc` 命名空间中定义了许多错误代码。Example 55.1, “Using `boost::system::error_code`”将错误代码 `boost::system::errc::not_supported` 赋值给 `ec`。由于 `boost::system::errc::not_supported` 是一个数字而 `ec` 是 `boost::system::error_code` 类型的对象，因此调用了函数 `boost::system::errc::make_error_code()`。该函数创建一个带有相应错误代码的 `boost::system::error_code` 类型的对象。

在 `main()` 中，对 `ec` 调用 `value()`。此成员函数返回存储在对象中的错误代码。

默认情况下，0 表示没有错误。其他任何数字都代表错误。错误代码的值取决于操作系统。请参考你操作系统的文档来获取错误代码的描述。

除了 `value()` 之外，`boost::system::error_code` 还提供了成员函数 `category()`，它返回一个类型为 `boost::system::error_category` 的对象。

错误代码仅仅是数值。虽然像微软这样的操作系统厂商能够保证系统的唯一性，但对于开发者来说，保证错误代码的唯一性几乎是不可能的，因此需要错误类别。错误类别是存在的。

### 示例 55.2. 使用 `boost::system::error_code`

```cpp
#include <boost/system/error_code.hpp>
#include <iostream>

using namespace boost::system;

void fail(error_code &ec)
{
  ec = errc::make_error_code(errc::not_supported);
}

int main()
{
  error_code ec;
  fail(ec);
  std::cout << ec.value() << '\n';
  std::cout << ec.category().name() << '\n';
}
```

`boost::system::error_code` 类型的错误可以通过 `category()` 成员函数获取其类别。使用 `errc::make_error_code()` 创建的错误属于通用类别。这是错误未显式分配类别时所属的类别。Example 55.1, “Using `boost::system::error_code`”中，`category()` 返回错误的类别。这是一个 `boost::system::error_category` 类型的对象。只有少数成员函数。例如，`name()` 获取类别的名称。Example 55.1, “Using `boost::system::error_code`”向标准输出写入 `generic`。

你也可以使用全局函数 `boost::system::generic_category()` 来访问通用类别。

Boost.System 提供了第二个类别。如果你调用全局函数 `boost::system::system_category()`，你会得到系统类的引用。如果你将类别名称写入标准输出，将显示 `system`。

错误由错误代码和错误类别唯一标识。由于错误代码只需要在类别内唯一，因此当你想要定义特定程序的错误代码时，应该创建一个新类别。这使得使用不与其他开发者冲突的代码成为可能。

### 示例 55.3. 创建错误类别

```cpp
#include <boost/system/error_code.hpp>
#include <string>
#include <iostream>

class application_category :
  public boost::system::error_category
{
public:
  const char *name() const noexcept { return "my app"; }
  std::string message(int ev) const { return "error message"; }
};

application_category cat;

int main()
{
  boost::system::error_code ec{129, cat};
  std::cout << ec.value() << '\n';
  std::cout << ec.category().name() << '\n';
}
```

一个新的错误类别是通过创建一个派生自 `boost::system::error_category` 的类定义的。这要求你定义各种成员函数。至少必须提供 `name()` 和 `message()` 成员函数，因为它们在 `boost::system::error_category` 中被定义为纯虚成员函数。对于额外的成员函数，如果需要可以覆盖默认行为。

当 `name()` 返回错误类别的名称时，`message()` 用于检索特定错误代码的错误描述。与示例 55.3, “创建错误类别”不同，参数 `ev` 通常会被求值以返回基于错误代码的描述。

新创建的错误类别类型的对象可以用于初始化错误代码。示例 55.3, “创建错误类别”使用新类别 `application_category` 定义了错误代码 `ec`。因此，错误代码 129 不再是一个通用错误；相反，它的含义由新错误类别的开发者定义。

### 注意事项

要使用 Visual C++ 2013 编译示例 55.3, “创建错误类别”，请移除 `noexcept` 关键字。此版本的 Microsoft 编译器不支持 `noexcept`。

`boost::system::error_code` 提供了一个名为 `default_error_condition()` 的成员函数，它返回一个类型为 `boost::system::error_condition` 的对象。`boost::system::error_condition` 的接口与 `boost::system::error_code` 的接口几乎相同。区别在于成员函数 `default_error_condition()`，它只由 `boost::system::error_code` 提供。

### 示例 55.4. 使用 `boost::system::error_condition`

```cpp
#include <boost/system/error_code.hpp>
#include <iostream>

using namespace boost::system;

void fail(error_code &ec)
{
  ec = errc::make_error_code(errc::not_supported);
}

int main()
{
  error_code ec;
  fail(ec);
  boost::system::error_condition ecnd = ec.default_error_condition();
  std::cout << ecnd.value() << '\n';
  std::cout << ecnd.category().name() << '\n';
}
```

`boost::system::error_condition` 的用法就像 `boost::system::error_code` 一样。这就是为什么如示例 55.4, “使用 `boost::system::error_condition`”所示，可以对类型为 `boost::system::error_condition` 的对象调用成员函数 `value()` 和 `category()`。

虽然类 `boost::system::error_code` 用于依赖平台的错误代码，但 `boost::system::error_condition` 用于访问与平台无关错误代码。成员函数 `default_error_condition()` 将依赖平台的错误代码转换为类型为 `boost::system::error_condition` 的与平台无关错误代码。

你可以使用 `boost::system::error_condition` 来识别与平台无关的错误。这种错误可以是，例如访问不存在的文件失败。虽然不同的操作系统可能提供不同的文件访问接口并返回不同的错误代码，但尝试访问不存在的文件在所有操作系统上都是一个错误。从特定操作系统接口返回的错误代码存储在 `boost::system::error_code` 中。描述访问不存在的文件失败的错误代码存储在 `boost::system::error_condition` 中。

Boost.System 提供的最后一个类是 `boost::system::system_error`，它派自 `std::runtime_error`。它可以用于异常中传输类型为 `boost::system::error_code` 的错误代码。

### 示例 55.5. 使用 `boost::system::system_error`

```cpp
#include <boost/system/error_code.hpp>
#include <boost/system/system_error.hpp>
#include <iostream>

using namespace boost::system;

void fail()
{
  throw system_error{errc::make_error_code(errc::not_supported)};
}

int main()
{
  try
  {
    fail();
  }
  catch (system_error &e)
  {
    error_code ec = e.code();
    std::cerr << ec.value() << '\n';
    std::cerr << ec.category().name() << '\n';
  }
}
```

在示例 55.5, “使用 `boost::system::system_error`”中，独立函数 `fail()` 已更改为在发生错误时抛出一个类型为 `boost::system::system_error` 的异常。该异常可以传输类型为 `boost::system::error_code` 的错误代码。异常在 `main()` 中被捕获，并将错误代码和错误类别写入标准错误输出。函数 `boost::asio::ip::host_name()` 的第二个变体也是这样工作的。

# 56. Boost.Exception

[Boost.Exception](http://www.boost.org/libs/exception) 库提供了新类型 `boost::exception`，允许你在异常抛出后为其添加数据。`boost::exception` 支持嵌套异常。`boost::exception` 类似于 `std::exception`。但是 `boost::exception` 缺少对 `noexcept` 的支持。

### 注意事项

要使用 Visual C++ 2013 编译示例 56.1, “使用 `boost::exception`”，请移除 `noexcept` 关键字。此版本的 Microsoft 编译器不支持 `noexcept`。

`boost::exception` 提供了一种向异常添加数据的机制。这是通过 `boost::error_info` 实现的。`boost::error_info` 是一个模板类，接受一个标签（tag）和一个值类型。标签通常是一个用于识别信息的结构体。

### 示例 56.1. 使用 `boost::exception`

```cpp
#include <boost/exception/all.hpp>
#include <exception>
#include <new>
#include <string>
#include <algorithm>
#include <limits>
#include <iostream>

typedef boost::error_info<struct tag_errmsg, std::string> errmsg_info;

struct allocation_failed : public boost::exception, public std::exception
{
  const char *what() const noexcept { return "allocation failed"; }
};

char *allocate_memory(std::size_t size)
{
  char *c = new (std::nothrow) char[size];
  if (!c)
    throw allocation_failed{};
  return c;
}

char *write_lots_of_zeros()
{
  try
  {
    char *c = allocate_memory(std::numeric_limits<std::size_t>::max());
    std::fill_n(c, std::numeric_limits<std::size_t>::max(), 0);
    return c;
  }
  catch (boost::exception &e)
  {
    e << errmsg_info{"writing lots of zeros failed"};
    throw;
  }
}

int main()
{
  try
  {
    char *c = write_lots_of_zeros();
    delete[] c;
  }
  catch (boost::exception &e)
  {
    std::cerr << boost::diagnostic_information(e);
  }
}
```

`allocation_failed` 派自 `boost::exception` 和 `std::exception`。将该类派自 `std::exception` 并不是必要的。`allocation_failed` 也可以派自另一个类层次结构中的类，以便将其嵌入现有的框架中。虽然示例 56.1, “使用 `boost::exception`”使用了标准定义的类层次结构，但仅将 `allocation_failed` 派自 `boost::exception` 就足够了。

如果捕获到类型为 `allocation_failed` 的异常，那么 `allocate_memory()` 必须是异常的来源，因为它是唯一抛出此类类型异常的函数。在有很多函数调用 `allocate_memory()` 的程序中，仅知道异常的类型不足以有效地调试程序。在这些情况下，如果知道是哪个函数尝试分配了 `allocate_memory()` 所能提供的内存，将大有帮助。

挑战在于，`allocate_memory()` 并没有包含任何额外信息（例如调用者名称）可以添加到异常中。`allocate_memory()` 无法富化异常。这只能在调用上下文中完成。

使用 Boost.Exception，可以在任何时间向异常中添加数据。你只需要为需要添加的每部分数据基于 `boost::error_info` 定义一个类型即可。



`boost::error_info` 是一个期望两个参数的模板。第一个参数是一个用于唯一标识新创建类型的标签（tag），这通常是一个具有唯一名称的结构体。第二个参数引用存储在异常内部的值的类型。Example 56.1, “Using `boost::exception`” 定义了一个新类型 `errmsg_info` —— 通过结构体 `tag_errmsg` 唯一标识 —— 它存储一个 `std::string` 类型的字符串。

在 `write_lots_of_zeros()` 的 `catch` 处理器中，`errmsg_info` 用于创建一个初始化为字符串“writing lots of zeros.”的对象。该对象随后通过 `operator<<` 添加到 `boost::exception` 类型异常中。然后异常被重新抛出。现在，异常不仅表示内存分配失败，还说明当程序尝试在 `write_lots_of_zeros()` 函数中写入零时内存分配失败。知道哪个函数调用了 `allocate_memory()` 会使调试变得更容易。

要从异常中检索所有可用数据，可以在 `main()` 的 `catch` 处理器中调用函数 `boost::diagnostic_information()`。`boost::diagnostic_information()` 为传递给它的异常调用成员函数 `what()` 并访问存储在异常内部的所有数据。`boost::diagnostic_information()` 返回一个 `std::string` 类型的字符串。

使用 Visual C++ 2013 编译时，Example 56.1, “Using `boost::exception`” 将显示如下：

```
Throw location unknown (consider BOOST_THROW_EXCEPTION)
Dynamic exception type: struct allocation_failed
std::exception::what: allocation failed
[struct tag_errmsg *] = writing lots of zeros
```

消息包含异常类型、从 `what()` 检索的描述。`boost::diagnostic_information()` 在运行时检查异常是否派自 `std::exception`。如果是这种情况，抛出 `allocation_failed` 类型异常的函数名称未知。

Boost.Exception 提供了一个宏来抛出异常，该异常不仅包含函数名，还包含文件名和行号等额外数据。使用 `BOOST_THROW_EXCEPTION` 替代 `throw`，函数名、文件名和行号数据会自动添加到异常中。但这仅在编译器支持额外数据的宏时才有效。

虽然像 `__FILE__` 和 `__LINE__` 宏自 C++98 起就已经标准化，但获取当前函数名称的宏 `__func__` 直到 C++11 才成为标准。由于许多编译器在 C++11 之前提供了此类宏，`BOOST_THROW_EXCEPTION` 会尝试识别编译器并使用相应的宏。

使用 Visual C++ 2013 编译，Example 56.2, “More data with `BOOST_THROW_EXCEPTION`” 显示如下消息：

```
main.cpp(20): Throw in function char *__cdecl allocate_memory(unsigned int)
Dynamic exception type: class boost::exception_detail::clone_impl<struct
  boost::exception_detail::error_info_injector<struct allocation_failed> >
std::exception::what: allocation failed
[struct tag_errmsg *] = writing lots zeros failed
```

在 Example 56.2, “More data with `BOOST_THROW_EXCEPTION`” 中，`allocation_failed` 不再派自 `boost::exception`。`BOOST_THROW_EXCEPTION` 访问函数 `boost::enable_error_info()` 来识别异常是否派自 `boost::exception`。如果不是，它创建一个派自指定类型和 `boost::exception` 的新异常类型。这就是为什么上面的消息包含与 `allocation_failed` 不同的异常类型。

## Example 56.2. More data with `BOOST_THROW_EXCEPTION`

```cpp
#include <boost/exception/all.hpp>
#include <exception>
#include <new>
#include <string>
#include <algorithm>
#include <limits>
#include <iostream>

typedef boost::error_info<struct tag_errmsg, std::string> errmsg_info;

struct allocation_failed : public std::exception
{
  const char *what() const noexcept { return "allocation failed"; }
};

char *allocate_memory(std::size_t size)
{
  char *c = new (std::nothrow) char[size];
  if (!c)
    BOOST_THROW_EXCEPTION(allocation_failed{});
  return c;
}

char *write_lots_of_zeros()
{
  try
  {
    char *c = allocate_memory(std::numeric_limits<std::size_t>::max());
    std::fill_n(c, std::numeric_limits<std::size_t>::max(), 0);
    return c;
  }
  catch (boost::exception &e)
  {
    e << errmsg_info{"writing lots of zeros failed"};
    throw;
  }
}

int main()
{
  try
  {
    char *c = write_lots_of_zeros();
    delete[] c;
  }
  catch (boost::exception &e)
  {
    std::cerr << boost::diagnostic_information(e);
  }
}
```

`boost::diagnostic_information()` 不使用 `diagnostic_information()`，它使用 `boost::error_info()` 直接访问类型为 `errmsg_info` 的错误消息。因为 `boost::error_info()` 返回类型为 `boost::shared_ptr` 的智能指针，所以使用 `operator*` 来获取错误消息。

如果传递给 `boost::error_info()` 的参数不是类型 `boost::exception`，则返回一个空指针。如果始终使用 `BOOST_THROW_EXCEPTION` 宏来抛出异常，则异常总是派自 `boost::exception` —— 无需检查返回的智能指针是否为空。

# 第 XIV 部分 数字处理

以下库都与数字处理有关：

- `Boost.Integer` 提供了整数类型，例如用于指定变量所占用的精确字节数。
- `Boost.Accumulators` 提供了累加器，当你计算平均值或标准差等数值时，可以把数字传递给累加器。
- `Boost.MinMax` 允许你通过一次函数调用获取容器中最小和最大的数字。
- `Boost.Random` 提供了随机数生成器。
- `Boost.NumericConversion` 提供了一种类型转换运算符，可以防止意外的溢出。

# 57. Boost.Integer

[Boost.Integer](http://www.boost.org/libs/integer) 提供了头文件 `boost/cstdint.hpp`，该文件为整数定义了特殊类型。这些定义源自 C99 标准。这是 1999 年发布的 C 语言标准的一个版本。由于第一个运行的 C++ 标准发布于 1998 年，因此它不包含 C99 中定义的特殊整数类型。

C99 在 `stdint.h` 头文件中定义了这些类型。该头文件被引入了 C++11。在 C++ 中，它被称为 `cstdint`。如果你的开发环境支持 C++11，你可以访问 `cstdint`，而无需使用 `boost/cstdint.hpp`。

来自 `boost/cstdint.hpp` 的类型定义在 `boost` 命名空间中。它们可以分为三类：

- 如 `boost::int8_t` 和 `boost::uint64_t` 等类型在其名称中带有精确的内存大小。因此，`boost::int8_t` 恰好包含 8 位，`boost::uint64_t` 恰好包含 64 位。
- 如 `boost::int_least8_t` 和 `boost::uint_least32_t` 等类型包含的位至少与其名称所示相同。`boost::int_least8_t` 的内存大小可能大于 8 位，`boost::uint_least32_t` 的内存大小可能大于 32 位。
- 如 `boost::int_fast8_t` 和 `boost::uint_fast16_t` 等类型也有最小尺寸。它们的实际尺寸被设置为一个能保证最佳性能的值。示例 57.1, “位数指定的整数类型” 使用 Visual C++ 2013 编译并运行在 64 位 Windows 7 系统上，`sizeof(uif16)` 显示为 `4`。

请注意，64 位类型并非在所有平台上都可用。你可以通过宏 `BOOST_NO_INT64_T` 检查是否存在 64 位类型。

## 示例 57.1. 位数指定的整数类型

```cpp
#include <boost/cstdint.hpp>
#include <iostream>

int main()
{
  boost::int8_t i8 = 1;
  std::cout << sizeof(i8) << '\n';

#ifndef BOOST_NO_INT64_T
  boost::uint64_t ui64 = 1;
  std::cout << sizeof(ui64) << '\n';
#endif

  boost::int_least8_t il8 = 1;
  std::cout << sizeof(il8) << '\n';

  boost::uint_least32_t uil32 = 1;
  std::cout << sizeof(uil32) << '\n';

  boost::int_fast8_t if8 = 1;
  std::cout << sizeof(if8) << '\n';

  boost::uint_fast16_t uif16 = 1;
  std::cout << sizeof(uif16) << '\n';
}
```

Boost.Integer 定义了 `boost::intmax_t` 和 `boost::uintmax_t` 类型，用于跨平台的整数。示例 57.2, “整数类型” 使用 Visual C++ 2013 编译并运行在 64 位系统上，`sizeof(imax)` 显示为 `8`。

## 示例 57.2. 整数类型

```cpp
#include <boost/cstdint.hpp>
#include <iostream>

int main()
{
  boost::intmax_t imax = 1;
  std::cout << sizeof(imax) << '\n';

#ifndef BOOST_NO_INT64_T
  boost::uintmax_t uiax = 1;
  std::cout << sizeof(umax) << '\n';
#endif
}
```

此外，Boost.Integer 提供了用于整数字面量的宏。在 C++ 代码中，默认情况下它们分配至少 4 字节。如 `BOOST_8` 和 `BOOST_64` 等宏，可以使用特定的类型。示例 57.3, “字面量” 使用 Visual C++ 2013 编译并运行在 64 位系统上，`sizeof(BOOST_8)` 显示为 `8`。

## 示例 57.3. 字面量

```cpp
#include <boost/cstdint.hpp>
#include <iostream>

int main()
{
  auto a = BOOST_8(1);
  std::cout << sizeof(a) << '\n';

  auto b = BOOST_64(1);
  std::cout << sizeof(b) << '\n';
}
```

# 58. Boost.Accumulators

[Boost.Accumulators](https://www.boost.org/libs/accumulators) 提供了处理样本的类。例如，你可以找到最大值或最小值，或者计算总和。你需要了解这一点，Boost.Accumulators 支持平均值和标准差。累加器是一个每次接收数据都会更新结果的容器。

Boost.Accumulators 包含三个部分：

- 框架提供了整体结构。它提供了 `boost::accumulators::accumulator_set`，始终与 `boost::accumulators` 使用。你需要了解这一点以及一些类，`boost/accumulators.hpp` 提供了访问。
- 框架提供了许多用于计算的累加器。`boost/accumulators/statistics.hpp` 提供了 `boost::accumators`。
- Boost.Accumulators 提供了运算符，例如将复数与 `int` 值相乘或相两个向量。头文件 `boost/accumulators/numeric.hpp` 为 `std::complex`、`std::valarray` 和 `std::vector` 定义了运算符。你不需要包含该头文件，但你必须定义宏 `BOOST_NUMERIC_FUNCTIONAL_COMPLEX_SUPPORT`、`BOOST_NUMERIC_FUNCTIONAL_VALARRAY_SUPPORT` 和 `BOOST_NUMERIC_FUNCTIONAL_VECTOR_SUPPORT` 以使运算符可用。

Boost.Accumulators 提供的所有类和函数都定义在 `boost::accumulators` 或嵌套命名空间中。例如，所有的累加器都定义在 `boost::accumulators::tag` 中。

## 示例 58.1. 使用 `boost::accumulators::tag::count` 计数

```cpp
#include <boost/accumulators/accumulators.hpp>
#include <boost/accumulators/statistics.hpp>
#include <iostream>

using namespace boost::accumulators;

int main()
{
  accumulator_set<int, features<tag::count>> acc;
  acc(4);
  acc(-6);
  acc(9);
  std::cout << count(acc) << '\n';
}
```

示例 58.1, “使用 `boost::accumulators::tag::count` 计数” 使用 `boost::accumulators::tag::count`，这是一个简单的计数传递它的值的累加器。因此，由于传递了三个值，此示例向标准输出写入 `3`。

要使用累加器，你需要访问 `boost::accumulators::accumulator_set` 类，它是一个模板，其第一个参数期望接收将处理的数值类型。

严格来说，你指定的是特征（features），而不是累加器（accumulators）。特征定义了应该计算的内容。你决定的是“是什么”，而不是“怎么做”。特征可以有不同的实现方式。这些实现方式就是累加器。

示例 58.1，“使用 `boost::accumulators::tag::count` 计数” 使用 `boost::accumulators::tag::count` 来选择一个计数的累加器。如果存在多个可以计数的累加器，Boost.Accumulators 会选择默认累加器。

请注意，你不能直接将特征传递给 `boost::accumulators::accumulator_set`。你需要使用 `boost::accumulators::features`。

类型为 `boost::accumulators::accumulator_set` 的对象可以像函数一样。可以通过调用 `operator()` 传递值。这些值会被立即处理。传递的值必须与作为 `boost::accumulators::accumulator_set` 第一个模板参数传递的类型相同。

对于每个特征，都有一个同名的提取器（extractor）。提取器接收累加器的当前结果。示例 58.1，“使用 `boost::accumulators::tag::count` 计数” 使用提取器 `boost::accumulators::count()`。传递的唯一参数是 `acc`。`boost::accumulators::count()` 返回 `3`。



### 示例 58.2：使用 `mean` 和 `variance`

```cpp
#include <boost/accumulators/accumulators.hpp>
#include <boost/accumulators/statistics.hpp>
#include <iostream>

using namespace boost::accumulators;

int main()
{
  accumulator_set<double, features<tag::mean, tag::variance>> acc;
  acc(8);
  acc(9);
  acc(10);
  acc(11);
  acc(12);
  std::cout << mean(acc) << '\n';
  std::cout << variance(acc) << '\n';
}
```

[示例 58.2，“使用 `mean` 和 `variance`”] 使用了两个特征 `boost::accumulators::tag::mean` 和 `boost::accumulators::tag::variance` 来计算五个值的平均值和方差。该示例向标准输出写入 `10` 和 `2`。

方差为 2 是因为 Boost.Accumulators 为这五个值中的每一个都分配了 0.2 的权重。使用 `boost::accumulators::tag::variance` 选择的累加器使用了权重。如果没有显式设置权重，则所有值将具有相同的权重。

### 示例 58.3：计算加权方差

```cpp
#include <boost/accumulators/accumulators.hpp>
#include <boost/accumulators/statistics.hpp>
#include <iostream>

using namespace boost::accumulators;

int main()
{
  accumulator_set<double, features<tag::mean, tag::variance>, int> acc;
  acc(8, weight = 1);
  acc(9, weight = 1);
  acc(10, weight = 4);
  acc(11, weight = 1);
  acc(12, weight = 1);
  std::cout << mean(acc) << '\n';
  std::cout << variance(acc) << '\n';
}
```

示例 58.3，“计算加权方差”将 `int` 作为第三个模板参数传递给 `boost::accumulators::accumulator_set`。该参数指定了权重的数据类型。在这个示例中，权重被分配给每个值。

Boost.Accumulators 使用 Boost.Parameter 以键/值对的形式传递额外参数（如权重）。权重的参数名称为 `weight`。你可以将该参数视为变量并对其赋值。该键/值对将作为额外参数在每个值之后传递给累加器。

在示例 58.3，“计算加权方差”中，值 10 的权重为 4，而所有其他值的权重均为 1。平均值仍然是 10，因为权重对平均值没有影响。然而，方差现在是 1.25。与之前的示例相比，它减少了，因为中间值的权重比其他值高。

Boost.Accumulators 提供了更多的累加器。它们的用法与本章介绍的累加器相同。该库的文档包含了所有可用累加器的概述。

# 59. Boost.MinMax

[Boost.MinMax](http://www.boost.org/libs/algorithm/minmax) 提供了一种算法，仅需一次函数调用即可找到两个值的最小值和最大值，这比调用 `std::min()` 和 `std::max()` 更高效。

Boost.MinMax 是 C++11 的一部分。如果你的开发环境支持 C++11，你可以在 `algorithm` 头文件中找到此 Boost 库中的算法。

### 示例 59.1：使用 `boost::minmax()`

```cpp
#include <boost/minmax.hpp>
#include <boost/tuple.hpp>
#include <iostream>

int main()
{
  int i = 2;
  int j = 1;

  boost::tuple<const int&, const int&> t = boost::minmax(i, j);

  std::cout << std::get<0>(t) << '\n';
  std::cout << std::get<1>(t) << '\n';
}
```

`boost::minmax()` 计算两个对象的最小值和最大值。虽然 `std::min()` 和 `std::max()` 只返回一个值，但 `boost::minmax()` 返回两个值的元组。示例 59.1，“使用 `boost::minmax()`”中，元组中的第一个元素指向最小值，第二个元素指向最大值。

`boost::minmax()` 定义在 `boost/algorithm.hpp` 中。

### 示例 59.2：使用 `minmax_element`

```cpp
#include <boost/minmax.hpp>
#include <array>
#include <utility>
#include <iostream>

int main()
{
  std::array<int, 4> a{{2, 3, 0, 1}};

  std::pair<std::array<int>::iterator, std::array<int>::iterator> p =
    boost::minmax_element(a.begin(), a.end());

  std::cout << *p.first << '\n';
  std::cout << *p.second << '\n';
}
```

正如标准库提供了查找容器中最小值和最大值的算法，Boost.MinMax 仅需调用一次 `minmax_element()` 即可实现相同的功能。与 `minmax()` 不同，`minmax_element()` 返回包含迭代器的 `std::pair`。第一个迭代器指向最小值，第二个指向最大值。示例 59.2，“使用 `minmax_element`”向标准输出写入 `0` 和 `3`。

这两个函数都可以带有第三个参数，指定如何比较对象。

# 60. Boost.Random

[Boost.Random](https://www.boost.org/libs/random) 提供了大量的随机数生成器，允许你决定如何生成随机数。在 C++ 中，始终可以使用 `cstdlib` 中的 `std::rand()` 生成随机数。然而，对于 `std::rand()`，随机数的生成方式取决于标准库的实现。

当你包含 `boost/random.hpp` 时，可以使用 Boost.Random 中的所有随机数生成器以及其他类和函数。

该库的大部分已在 C++11 中添加到标准库中。如果你的开发环境支持 C++11，你可以通过包含 `random` 头文件并访问 `std` 命名空间来重写本章的 Boost.Random 示例。

### 示例 60.1：使用 `boost::random::mt19937` 生成伪随机数

```cpp
#include <boost/random.hpp>
#include <iostream>
#include <ctime>
#include <cstdint>

int main()
{
  std::time_t now = std::time(0);
  boost::random::mt19937 gen{static_cast<std::uint32_t>(now)};
  std::cout << gen() << '\n';
}
```

示例 60.1，“使用 `boost::random::mt19937` 生成伪随机数”访问了随机数生成器 `boost::random::mt19937`。运算符 `operator()` 生成一个随机数并将其写入标准输出。

`boost::random::mt19937` 生成的随机数是整数。生成整数还是浮点数取决于你使用的特定生成器。所有随机数生成器都定义了类型 `result_type` 来确定随机数的类型。`boost::random::mt19937` 的 `result_type` 是 `boost::uint32_t`。

所有随机数生成器都提供了两个成员函数：`min()` 和 `max()`。这些函数返回该随机数生成器可以生成的最小值和最大值。

Boost.Random 几乎所有的随机数生成器都是伪随机数生成器。伪随机数生成器并不产生真正的随机数。它们基于生成看似随机数的算法。`boost::random::mt19937` 就是这些伪随机数生成器之一。

伪随机数生成器通常需要初始化。如果用相同的值进行初始化，它们将返回相同的随机数。这就是为什么在示例 60.1，“使用 `boost::random::mt19937` 生成伪随机数”中，`std::time()` 的返回值被传递给 `boost::random::mt19937` 的构造函数。这应该确保当程序在不同的时间运行时会生成不同的随机数。

伪随机数对于大多数用例已经足够了。`std::rand()` 也基于伪随机数生成器，必须使用 `std::srand()` 初始化。然而，Boost.Random 提供了一个可以生成真随机数的随机数生成器，只要操作系统拥有生成真随机数的源。

### 示例 60.2：使用 `boost::random::random_device` 生成真随机数

```cpp
#include <boost/random/random_device.hpp>
#include <iostream>

int main()
{
  boost::random::random_device gen;
  std::cout << gen() << '\n';
}
```

`boost::random::random_device` 是一个非确定随机数生成器，即一种可以生成真随机数的随机数生成器。它不需要初始化。因此，预测随机数是不可能的。非确定随机数生成器通常用于与安全相关的应用程序。

`boost::random::random_device` 调用操作系统函数生成随机数。如果像示例 60.2，“使用 `boost::random::random_device` 生成真随机数”那样调用默认构造函数，`boost::random::random_device` 在 Windows 上使用加密服务提供商 `MS_DEF_PROV`，在 Linux 上使用 `/dev/urandom` 作为源。

如果你想使用另一个源，请调用 `boost::random::random_device` 的构造函数，它期望一个 `std::string` 类型的参数。该参数如何被解释取决于操作系统。在 Windows 上，它必须是加密服务提供商的名字；在 Linux 上，它是设备路径。

请注意，如果你想使用 `boost::random::random_device` 类，必须包含 `boost/random/random_device.hpp`。该类没有通过 `boost/random.hpp` 提供。

### 示例 60.3：使用 `bernoulli_distribution` 生成随机 0 和 1

```cpp
#include <boost/random.hpp>
#include <iostream>
#include <ctime>
#include <cstdint>

int main()
{
  std::time_t now = std::time(0);
  boost::random::mt19937 gen{static_cast<std::uint32_t>(now)};
  boost::random::bernoulli_distribution<> dist;
  std::cout << dist(gen) << '\n';
}
```

示例 60.3，“使用 `bernoulli_distribution` 生成随机 0 和 1”使用了伪随机数生成器 `boost::random::mt19937`。此外，还使用了分布。分布是 Boost.Random 类，用于将随机数生成器的随机数范围映射到另一个范围。虽然像 `boost::random::mt19937` 这样的随机数生成器内置了可以通过 `min()` 和 `max()` 查看 的随机数上下限，但你可能需要不同范围内的随机数。

示例 60.3，“使用 `bernoulli_distribution` 生成随机 0 和 1”模拟了一个硬币。因为硬币只有两面，`boost::random::bernoulli_distribution` 是一个返回 0 或 1 的分布。分布像随机数生成器一样使用：你调用 `operator()` 来接收随机数。然而，你必须传递一个参数。在示例 60.3，“使用 `bernoulli_distribution` 生成随机 0 和 1”中，`dist` 使用伪随机数生成器 `gen` 返回 0 或 1。

### 示例 60.4：使用 `uniform_int_distribution` 生成 1 到 100 之间的随机数

```cpp
#include <boost/random.hpp>
#include <iostream>
#include <ctime>
#include <cstdint>

int main()
{
  std::time_t now = std::time(0);
  boost::random::mt19937 gen{static_cast<std::uint32_t>(now)};
  boost::random::uniform_int_distribution<> dist{1, 100};
  std::cout << dist(gen) << '\n';
}
```

Boost.Random 提供了大量的分布。示例 60.4，“使用 `uniform_int_distribution` 生成 1 到 100 之间的随机数”使用了一种经常需要的分布：`boost::random::uniform_int_distribution`。该分布允许你定义所需的随机数范围。在示例 60.4，“使用 `uniform_int_distribution` 生成 1 到 100 之间的随机数”中，`dist` 返回 1 到 100 之间的数。

请注意，`dist` 可以返回 1 和 100。分布的边界是包含在内的。

除了 `boost::random::bernoulli_distribution` 和 `boost::random::uniform_int_distribution`，Boost.Random 还有许多分布。例如，还有像 `boost::random::normal_distribution` 和 `boost::random::chi_squared_distribution` 这样的分布，它们用于统计学。

# 61. Boost.NumericConversion

[Boost.NumericConversion](http://www.boost.org/libs/numeric/conversion) 库可用于将一种数值类型的数字转换为另一种数值类型。在 C++ 中，这种转换也可以隐式发生，如示例 61.1，“从 `int` 到 `short` 的隐式转换”所示。

```cpp
#include <iostream>

int main()
{
  int i = 0x10000;
  short s = i;
  std::cout << s << '\n';
}
```

示例 61.1，“从 `int` 到 `short` 的隐式转换”将可以顺利编译，因为从 `int` 到 `short` 的类型转换是自动完成的。然而，尽管程序可以运行，转换结果取决于所使用的编译器。变量 `i` 中的数字 `0x10000` 太大，无法存储在 `short` 类型的变量中。根据标准，此操作的结果取决于具体实现。使用 Visual C++ 2013 编译时，程序显示为 `0`，这与 `i` 中的值明显不同。

为了避免这类问题，你可以使用强制转换运算符 `boost::numeric_cast`（请参见示例 61.2，“使用 `boost::numeric_cast` 进行溢出检测”）。`boost::numeric_cast` 的用法与现有的 C++ 转换运算符完全相同。必须包含正确的头文件；在这种情况下，头文件是 `boost/numeric/conversion/cast.hpp`。



`boost::numeric_cast` 执行与 C++ 相同的转换，但它会验证转换是否可以在不改变被转换值的情况下进行。在示例 61.2“使用 `boost::numeric_cast` 进行溢出检测”中，该验证会失败并抛出类型为 `boost::numeric::bad_numeric_cast` 的异常，因为 `0x10000` 太大，无法放入 `short` 类型的变量中。

## 示例 61.2. 使用 `boost::numeric_cast` 进行溢出检测

```cpp
#include <boost/numeric/conversion/cast.hpp>
#include <iostream>

int main()
{
  try
  {
    int i = 0x10000;
    short s = boost::numeric_cast<short>(i);
    std::cout << s << '\n';
  }
  catch (boost::numeric::bad_numeric_cast &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

严格来说，将抛出类型为 `boost::numeric::positive_overflow` 的异常。该类型指定了溢出——在本例中针对正数。还有 `boost::numeric::negative_overflow`，它指定了负数的溢出（参见示例 61.3“针对负数的溢出检测”）。

## 示例 61.3. 针对负数的溢出检测

```cpp
#include <boost/numeric/conversion/cast.hpp>
#include <iostream>

int main()
{
  try
  {
    int i = -0x10000;
    short s = boost::numeric_cast<short>(i);
    std::cout << s << '\n';
  }
  catch (boost::numeric::negative_overflow &e)
  {
    std::cerr << e.what() << '\n';
  }
}
```

Boost.NumericConversion 定义了额外的异常类型，它们都派自 `boost::numeric::bad_numeric_cast`。由于 `boost::numeric::bad_numeric_cast` 派自 `std::bad_cast`，`catch` 处理器也可以捕获此类类型的异常。

# 第 XV 部分 应用程序库

应用程序库是指通常专门用于独立应用程序开发，而不是用于库库的库。

- `Boost.Log` 是一个日志库。
- `Boost.ProgramOptions` 是用于定义和解析命令行选项的库。
- `Boost.Serialization` 允许你将对象序列化，例如将它们保存到文件并从文件中加载。
- `Boost.Uuid` 支持处理 UUID 操作。

# 62. Boost.Log

[Boost.Log](http://www.boost.org/libs/log) 是 Boost 中的日志库。它支持许多后端（back-ends），以各种格式记录日志数据。后端通过前端（front-ends）访问，前端封装了服务并以不同的方式转发日志目。例如，有一个前端使用线程来异步转发日志目。前端可以带有过滤器来忽略某些日志目。它们还定义了如何将日志目格式化为字符串。所有这些都是可扩展的，使得 Boost.Log 成为了一个强大的库。

示例 62.1“后端、前端、核心和记录器”介绍了 Boost.Log 的核心组件。Boost.Log 允许你访问后端、前端、核心和记录器：

- 后端决定数据写入哪里。`boost::log::sinks::text_ostream_backend` 使用类型为 `std::ostream` 的流初始化，并将日志目写入其中。
- 前端是核心与后端之间的连接。它们实现了各种功能，示例 62.1“后端、前端、核心和记录器”使用了 `boost::log::sinks::asynchronous_sink`。
- 核心是所有日志目路由通过的中心组件。要获取核心的指针，调用 `boost::log::core::get()`。
- 记录器是你在 Boost.Log 中最频繁使用的组件。

## 示例 62.1. 后端、前端、核心和记录器

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/logger.hpp>
#include <boost/utility/empty_deleter.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>

using namespace boost::log;

int main()
{
  typedef sinks::asynchronous_sink<sinks::text_ostream_backend> text_sink;
  boost::shared_ptr<text_sink> sink = boost::make_shared<text_sink>();

  boost::shared_ptr<std::ostream> stream{&std::clog,
    boost::empty_deleter{}};
  sink->locked_backend()->add_stream(stream);

  core::get()->add_sink(sink);

  sources::logger lg;

  BOOST_LOG(lg) << "note";
  sink->flush();
}
```

由于后端是前端的模板参数，因此它只能在前端实例化后才能进行配置。后端决定了这种实现方式。成员函数 `add_stream()` 由后端 `boost::log::sinks::text_ostream_backend` 提供，用于添加流。你可以为 `boost::log::sinks::text_ostream_backend` 添加多个流。其他后端提供了不同的成员函数用于配置。详细信息请参阅文档。

要访问后端，所有前端都提供了成员函数 `locked_backend()`。该成员函数之所以命名为 `locked_backend()`，是因为它返回一个指针，只要该指针存在，该指针就能提供对后端的同步访问。你可以从多个线程通过 `locked_backend()` 返回的指针访问后端，而无需自己手动进行访问同步。

你可以使用默认构造函数实例化如 `boost::log::sources::logger` 类的日志器。日志器会自动调用 `boost::log::core::get()` 将日志条目转发到核心。

你可以在不使用宏的情况下访问日志器。日志器是带有可以调用的成员函数的对象。然而，使用诸如 `BOOST_LOG` 这样的宏可以让编写日志条目变得更简单。如果没有宏，将无法在一行代码中完成日志条目的写入。

示例 62.1“后端、前端、核心和日志器”在 `main()` 结束处调用了 `boost::log::sinks::asynchronous_sink::flush()`。此调用是必要的，因为前端是异步的，并使用线程转发日志条目。该调用确保所有缓冲的日志条目都传递到后端并写入。如果没有调用 `flush()`，示例可能会在没有显示 `note` 的情况下终止。

示例 62.2“带有过滤器的 `boost::sources::severity_logger`”基于示例 62.1“后端、前端、核心和日志器”，但它将 `boost::sources::logger` 替换为日志器 `boost::sources::severity_logger`。该日志器为每个日志条目添加了一个日志级别属性。你可以使用宏 `BOOST_LOG_SEV` 来设置日志级别。

日志级别的类型取决于传递给 `boost::sources::severity_logger` 的模板参数。示例 62.2“带有过滤器的 `boost::sources::severity_logger`”使用 `int`。这就是为什么像 0 和 1 这样的数字会被传递给 `BOOST_LOG_SEV`。如果使用了 `BOOST_LOG`，日志级别将被设置为 0。

示例 62.2“带有过滤器的 `boost::sources::severity_logger`”还调用了 `set_filter()` 在前端注册了一个过滤器。每个日志条目都会调用该过滤器函数。如果函数返回 `true`，则日志条目被转发到后端。示例 62.2“带有过滤器的 `boost::sources::severity_logger`”定义了返回值为 `bool` 的函数 `only_warnings()`。

`only_warnings()` 期望一个类型为 `boost::log::attribute_value_set` 的参数。该类型代表日志条目在日志框架中传递的状态。`boost::log::record` 是另一种日志条目的类型，类似于 `boost::log::attribute_value_set` 的封装器。该类型提供了成员函数 `attribute_values()`，用于获取对 `boost::log::attribute_value_set` 的引用。过滤器函数直接接收 `boost::log::attribute_value_set` 而不接收 `boost::log::record`。`boost::log::attribute_value_set` 存储键值对。可以将其视为一个 `std::unordered_map`。

日志条目由属性组成。属性具有名称和值。你可以自己创建属性。它们也可以被自动创建——例如通过日志器。事实上，这就是为什么 Boost.Log 提供了多个日志器。`boost::log::sources::severity_logger` 为每个日志条目添加了一个名为 Severity 的属性。该属性存储了日志级别。这样，过滤器就可以检查日志条目的日志级别是否大于 0。

### 示例 62.2. 带有过滤器的 `boost::sources::severity_logger`

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/severity_logger.hpp>
#include <boost/utility/empty_deleter>
#include <boost/log/shared_ptr.hpp>
#include <boost/log/record_attributes.hpp>
#include <iostream>

using namespace boost::log;

bool only_warnings(const attribute_value_set &set)
{
  return set["Severity"].extract<int>() > 0;
}

int main()
{
  typedef sinks::asynchronous_sink<sinks::text_ostream_backend> text_sink;
  shared_ptr<text_sink> sink = boost::make_shared<text_sink>();

  shared_ptr<std::ostream> stream(&std::clog, empty_deleter{});
  sink->locked_backend()->add_stream(stream);
  sink->set_filter(&only_warnings);

  core::get()->add_sink(sink);

  sources::severity_logger<int> lg;

  BOOST_LOG(lg) << "note";
  BOOST_LOG_SEV(lg, 0) << "another note";
  BOOST_LOG_SEV(lg, 1) << "warning";
  sink->flush();
}
```

`boost::log::attribute_value_set` 提供了多个访问属性的成员函数。这些成员函数与 `std::unordered_map` 提供的相似。例如，`boost::log::attribute_value_set` 重载了 `operator[]`。该运算符返回作为参数传递的属性值。如果属性不存在，它将被创建。

属性名称的类型是 `boost::log::attribute_name`。该类提供一个接受字符串的构造函数，因此你可以直接向 `operator[]` 传递字符串，如示例 62.2“带有过滤器的 `boost::sources::severity_logger`”所示。

属性值的类型是 `boost::log::attribute_value`。该类提供了以属性原始类型接收值的成员函数。由于日志级别是一个 `int` 值，因此 `int` 被模板参数传递给 `extract()`。

`boost::log::attribute_value` 还定义了 `extract_or_default()` 和 `extract_or_throw()` 成员函数。如果类型转换失败，`extract()` 返回一个使用默认构造函数创建的值——例如在 `int` 的情况下返回 0。`extract_or_default()` 返回一个作为该成员函数另一个参数的默认值。`extract_or_throw()` 在发生错误时抛出一个 `boost::log::runtime_error` 异常。

对于类型转换，Boost.Log 提供了访问函数 `boost::log::visit()`，你可以用它代替 `extract()`。

示例 62.2“带有过滤器的 `boost::sources::severity_logger`”显示了 `warning`。该日志条目的日志级别大于 0，因此未被过滤。

### 示例 62.3. 使用 `set_formatter()` 更改日志条目的格式

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/severity_logger.hpp>
#include <boost/utility/empty_deleter.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>

using namespace boost::log;

void severity_and_message(const record_view &view, formatting_ostream &os)
{
  os << view.attribute_values()["Severity"].extract<int>() << ": " <<
    view.attribute_values()["Message"].extract<std::string>();
}

int main()
{
  typedef sinks::asynchronous_sink<sinks::text_ostream_backend> text_sink;
  boost::shared_ptr<text_sink> sink = boost::make_shared<text_sink>();

  boost::shared_ptr<std::ostream> stream{&std::clog,
    boost::empty_deleter{}};
  sink->locked_backend()->add_stream(stream);
  sink->set_formatter(&severity_and_message);

  core::get()->add_sink(sink);

  sources::severity_logger<int> lg;

  BOOST_LOG_SEV(lg, 0) << "note";
  BOOST_LOG_SEV(lg, 1) << "warning";
  sink->flush();
}
```

示例 62.3“使用 `set_formatter()` 更改日志条目的格式”是基于示例 62.2“带有过滤器的 `boost::sources::severity_logger`”。这次显示了日志级别。

前端提供了成员函数 `set_formatter()`，它可以向其传递一个格式化函数。如果日志条目没有被前端过滤，它将被转发到格式化函数。该函数将日志条目格式化为字符串，然后从前端传递到后端。如果你不调用 `set_formatter()`，默认情况下后端只会接收类似 `BOOST_LOG` 宏右侧的内容。

示例 62.3“使用 `set_formatter()` 更改日志条目的格式”将函数 `severity_and_message()` 传递给 `set_formatter()`。`severity_and_message()` 期望类型为 `boost::log::record_view` 和 `boost::log::formatting_ostream` 的参数。`boost::log::record_view` 是日志条目的视图。它类似于 `boost::log::record`。然而，`boost::log::record_view` 是一个不可变的日志条目。



`boost::log::record_view` 提供了成员函数 `attribute_values()`，它返回一个对 `boost::log::attribute_value_set` 的常量引用。`boost::log::formatting_ostream` 是用于创建传递到后端的字符串的流。

`severity_and_message()` 访问属性 `Severity` 和 `Message`。调用 `extract()` 获取属性值，然后将其写入流中。`Severity` 以 `int` 值返回日志级别。`Message` 提供了对类似 `BOOST_LOG` 宏右侧内容的访问。查阅文档可获得可用属性完整列表。

示例 62.3，“使用 `set_formatter()` 更改日志条目的格式”使用没有任何过滤器。示例写入了两个日志条目：`0: note` 和 `1: warning`。

示例 62.4，“使用 lambda 函数过滤并格式化日志条目”使用没有任何过滤器。示例写入了两个日志条目：`0: note` 和 `1: warning`。

前端提供了成员函数 `set_formatter()`，它可以向其传递一个格式化函数。如果日志条目没有被前端过滤，它将被转发到格式化函数。该函数将日志条目格式化为字符串，然后从前端传递到后端。如果你不调用 `set_formatter()`，默认情况下后端只会接收类似 `BOOST_LOG` 宏右侧的内容。

示例 62.3，“使用 `set_formatter()` 更改日志条目的格式”将函数 `severity_and_message()` 传递给 `set_formatter()`。`severity_and_message()` 期望类型为 `boost::log::record_view` 和 `boost::log::formatting_ostream` 的参数。`boost::log::record_view` 是日志条目的视图。它类似于 `boost::log::record`。然而，`boost::log::record_view` 是一个不可变的日志条目。

`boost::log::record_view` 提供了成员函数 `attribute_values()`，它返回一个对 `boost::log::attribute_value_set` 的常量引用。`boost::log::formatting_ostream` 是用于创建传递到后端的字符串的流。

`severity_and_message()` 访问属性 `Severity` 和 `Message`。调用 `extract()` 获取属性值，然后将其写入流中。`Severity` 以 `int` 值返回日志级别。`Message` 提供了对类似 `BOOST_LOG` 宏右侧内容的访问。查阅文档可获得可用属性完整列表。

示例 62.3，“使用 `set_formatter()` 更改日志条目的格式”使用没有任何过滤器。示例写入了两个日志条目：`0: note` 和 `1: warning`。

示例 62.4，“使用 lambda 函数过滤并格式化日志条目”使用没有任何过滤器。示例写入了两个日志条目：`0: note` 和 `1: warning`。

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/severity_logger.hpp>
#include <boost/utility/empty_deleter.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>

using namespace boost::log;

void severity_and_message(const record_view &view, formatting_ostream &os)
{
  os << view.attribute_values()["Severity"].extract<int>() << ": " <<
    view.attribute_values()["Message"].extract<std::string>();
}

int main()
{
  typedef sinks::asynchronous_sink<sinks::text_ostream_backend> text_sink;
  boost::shared_ptr<text_sink> sink = boost::make_shared<text_sink>();

  boost::shared_ptr<std::ostream> stream{&std::clog,
    boost::empty_deleter{}};
  sink->locked_backend()->add_stream(stream);
  sink->set_formatter(&severity_and_message);

  core::get()->add_sink(sink);

  sources::severity_logger<int> lg;

  BOOST_LOG_SEV(lg, 0) << "note";
  BOOST_LOG_SEV(lg, 1) << "warning";
  sink->flush();
}
```

前端 `boost::log::sinks::synchronous_sink` 提供了对后端的同步访问，这使得你即使后端不是线程安全的，也可以在多线程应用程序中使用该后端。

`boost::log::sinks::asynchronous_sink` 和 `boost::log::sinks::synchronous_sink` 这两个前端的区别在于，后者不是基于线程的。日志记录是在同一个线程中传递给后端的。

示例 62.8，“多个日志器、前端和后端”使用了前端 `boost::log::sinks::synchronous_sink` 配合后端 `boost::log::sinks::text_multifile_backend`。该后端将日志条目写入一个或多个文件。文件名是根据通过 `set_file_name_composer()` 传递给后端的规则创建的。如果你像示例那样使用独立函数 `boost::log::sinks::file::as_file_name_composer()`，则该规则可以作为一个 lambda 函数创建，其使用的构建块与格式化函数相同。然而，这些属性（attributes）并不会用于创建写入到后端的字符串。相反，该字符串将是日志条目要写入的文件名。

示例 62.8，“多个日志器、前端和后端”使用了 `channel` 和 `severity` 关键字，它们是通过宏 `BOOST_LOG_ATTRIBUTE_KEYWORD` 定义的。它们引用属性 `Channel` 和 `Severity`。在关键字上调用成员函数 `or_default()` 以在属性未设置时传递一个默认值。如果写入了一个日志条目且 `Channel` 和 `Severity` 未设置，该条目将被写入文件 `None-0.log`。如果写入日志级别为 1 的条目，它将存储在文件 `None-1.log` 中。如果日志级别为 1 且通道名为 `Main`，则日志条目保存在文件 `Main-1.log` 中。

属性 `Channel` 由日志器 `boost::log::sources::channel_logger` 定义。构造函数期望一个通道名称。该名称不能直接作为字符串传递。相反，它必须作为命名参数传递。这就是为什么示例使用了 `keywords::channel = "Main"`，即使 `boost::log::sources::channel_logger` 不接受任何其他参数。

### 示例 62.8. 多个日志器、前端和后端

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/severity_logger.hpp>
#include <boost/log/sources/channel_logger.hpp>
#include <boost/log/expressions.hpp>
#include <boost/log/attributes.hpp>
#include <boost/log/utility/string_literal.hpp>
#include <boost/utility/empty_deleter.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>
#include <string>

using namespace boost::log;

BOOST_LOG_ATTRIBUTE_KEYWORD(severity, "Severity", int)
BOOST_LOG_ATTRIBUTE_KEYWORD(channel, "Channel", std::string)

int main()
{
  typedef sinks::asynchronous_sink<sinks::text_ostream_backend>
    ostream_sink;
  boost::shared_ptr<ostream_sink> ostream =
    boost::make_shared<ostream_sink>();
  boost::shared_ptr<std::ostream> clog{&std::clog,
    boost::empty_deleter{}};
  ostream->locked_backend()->add_stream(clog);
  core::get()->add_sink(ostream);

  typedef sinks::synchronous_sink<sinks::text_multifile_backend>
    multifile_sink;
  boost::shared_ptr<multifile_sink> multifile =
    boost::make_shared<multifile_sink>();
  multifile->locked_backend()->set_file_name_composer(
    sinks::file::as_file_name_composer(expressions::stream <<
    channel.or_default<std::string>("None") << "-" <<
    severity.or_default(0) << ".log"));
  core::get()->add_sink(multifile);

  sources::severity_logger<int> severity_lg;
  sources::channel_logger<> channel_lg{keywords::channel = "Main"};

  BOOST_LOG_SEV(severity_lg, 1) << "severity message";
  BOOST_LOG(channel_lg) << "channel message";
  ostream->flush();
}
```

请注意，命名参数 `boost::log::keywords::channel` 与你通过宏 `BOOST_LOG_ATTRIBUTE_KEYWORD` 创建的关键字没有任何关系。



`boost::log::keywords::channel` 与你通过宏 `BOOST_LOG_ATTRIBUTE_KEYWORD` 创建的关键字没有任何关系。`boost::log::sources::channel_logger` 用于识别来自组件的日志条目。

### 示例 62.9：集中处理异常

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/severity_logger.hpp>
#include <boost/log/sources/channel_logger.hpp>
#include <boost/log/expressions.hpp>
#include <boost/log/attributes.hpp>
#include <boost/log/utility/string_literal.hpp>
#include <boost/utility/empty_deleter.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>
#include <string>

using namespace boost::log;

struct handler
{
  void operator()(const runtime_error &ex) {
    std::cerr << "runtime_error: " << ex.what() << "\n";
  }
  void operator()(const std::exception &ex) {
    std::cerr << "exception: " << ex.what() << "\n";
  }
};

int main()
{
  typedef sinks::synchronous_sink<sinks::text_ostream_backend>
    ostream_sink;
  boost::shared_ptr<ostream_sink> ostream =
    boost::make_shared<ostream_sink>();
  boost::shared_ptr<std::ostream> clog{&std::clog,
    boost::empty_deleter{}};
  ostream->locked_backend()->add_stream(clog);
  core::get()->add_sink(ostream);

  core::get()->set_exception_handler(handler{});

  sources::severity_logger<int> severity_lg;
  sources::channel_logger<> channel_lg{keywords::channel = "Main"};

  try {
    BOOST_LOG_SEV(severity_lg, 1) << "severity message";
    BOOST_LOG(channel_lg) << "channel message";
    throw std::runtime_error("test error");
  } catch (...) {
    // Handled
  }
  ostream->flush();
}
```

请注意，命名参数 `boost::log::keywords::channel` 与你通过宏 `BOOST_LOG_ATTRIBUTE_KEYWORD` 创建的关键字没有任何关系。

### 示例 62.10：定义全局日志器的宏

```cpp
#include <boost/log/common.hpp>
#include <boost/log/sinks.hpp>
#include <boost/log/sources/severity_logger.hpp>
#include <boost/utility/empty_deleter.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>
#include <exception>

using namespace boost::log;

BOOST_LOG_INLINE_LOGGER_DEFAULT(lg, sources::wlogger_mt)

int main()
{
  typedef sinks::synchronous_sink<sinks::text_ostream_backend>
    text_sink;
  boost::shared_ptr<text_sink> ostream =
    boost::make_shared<text_sink>();
  boost::shared_ptr<std::ostream> clog{&std::clog,
    boost::empty_deleter{}};
  ostream->locked_backend()->add_stream(clog);

  core::get()->add_sink(ostream);

  BOOST_LOG(lg::get()) << L"note";
}
```

本章的所有示例都使用本地日志器。如果你想定义全局日志器，请使用 `BOOST_LOG_INLINE_LOGGER_DEFAULT`，如示例 62.10“定义全局日志器的宏”所示。第一个参数是日志器名称，第二个参数是类型。你不需要通过名称访问日志器。相反，调用 `get()`，它会返回一个单例指针。

Boost.Log 还提供了许多值得关注的函数。例如，你可以通过一个带有字符串类型键/值对的容器来配置日志框架。这样，你就不需要实例化类并调用成员函数了。例如，可以将键 `Destination` 设置为 `Console`，这将自动让日志框架使用后端 `boost::log::sinks::text_ostream_backend`。可以通过额外的键/值对对后端进行配置。由于该容器也可以被序列化到 INI 文件中，因此完全可能将配置存储在文本文件中，并使用该文件初始化日志框架。

# 63. Boost.ProgramOptions

[Boost.ProgramOptions](http://www.boost.org/libs/program_options) 是一个可以方便解析命令行选项的库，例如用于控制台应用程序的命令行选项。如果你开发的是具有图形用户界面的应用程序，那么命令行选项通常是不重要的。

要使用 Boost.ProgramOptions 解析命令行选项，需要以下三个步骤：

1. 定义命令行选项。你为它们命名并指定哪些选项可以设置值。如果命令行选项被解析为键/值对，你还需要设置该值的类型——例如，它是字符串还是数字。
2. 使用解析器评估命令行。你通过 `main()` 函数的两个参数获取命令行，这两个参数通常被称为 `argc` 和 `argv`。
3. 存储解析器评估后的命令行选项。Boost.ProgramOptions 提供了一个派生自 `std::map` 的类，将命令行选项以名/值对的形式保存。之后，你可以检查哪些选项被存储了，以及它们的值是什么。

示例 63.1“使用 Boost.ProgramOptions 的基本方法”演示了使用 Boost.ProgramOptions 解析命令行选项的基本方法。

## 示例 63.1：使用 Boost.ProgramOptions 的基本方法

```cpp
#include <boost/program_options.hpp>
#include <iostream>

using namespace boost::program_options;

void on_age(int age)
{
  std::cout << "On age: " << age << '\n';
}

int main(int argc, const char *argv[])
{
  try
  {
    options_description desc{"Options"};
    desc.add_options()
      ("help,h", "Help screen")
      ("pi", value<float>()->default_value(3.14f), "Pi")
      ("age", value<int>()->notifier(on_age), "Age");

    variables_map vm;
    store(parse_command_line(argc, argv, desc), vm);
    notify(vm);

    if (vm.count("help"))
      std::cout << desc << '\n';
    else if (vm.count("age"))
      std::cout << "Age: " << vm["age"].as<int>() << '\n';
    else if (vm.count("pi"))
      std::cout << "Pi: " << vm["pi"].as<float>() << '\n';
  }
  catch (const error &ex)
  {
    std::cerr << ex.what() << '\n';
  }
}
```

要使用 Boost.ProgramOptions，请包含头文件 `boost/program_options.hpp`。你可以在 `boost::program_options` 命名空间下访问该库的所有类和函数。

使用类 `boost::program_options::options_description` 来描述命令行选项。这种类型的对象可以写入如 `std::cout` 等流中，以显示可用命令行选项的概述。传递给构造函数的字符串提供了概述的名称，它作为命令行选项的标题。

`boost::program_options::options_description` 定义了一个成员函数 `add()`，它期望一个类型为 `boost::program_options::option_description` 的参数。你调用此函数来描述每个命令行选项。与其为每个命令行选项都调用此函数，示例 63.1“使用 Boost.ProgramOptions 的基本方法”调用了成员函数 `add_options()`，这使得该任务变得更加简单。

`add_options()` 返回一个代表 `boost::program_options::options_description` 类型对象的代理对象。代理对象的类型并不重要。更有意思的是，代理对象简化了许多命令行选项。它使用了重载的 `operator()`，你可以通过调用它来传递定义命令行选项所需的数据。该运算符返回同一个代理对象的引用，允许你多次调用 `operator()`。示例 63.1“使用 Boost.ProgramOptions 的基本方法”借助代理对象定义了三个命令行选项。第一个命令行选项是 `--help`。该选项的描述被设置为“Help screen”。该选项是一个开关（switch），而不是名/值对。你可以在命令行上设置 `--help` 或省略它。无法为 `--help` 设置值。

请注意传递给 `operator()` 的第一个字符串是“help,h”。你可以为命令行选项指定短名称。命令行选项的短名称必须由一个字母组成，并位于逗号后面。现在帮助信息可以通过 `--help` 或 `-h` 显示。除了 `--help`，还定义两个命令行选项：`--pi` 和 `--age`。这些不是开关，而是名/值对。`--pi` 和 `--age` 期望被设置值。

将类型为 `boost::program_options::value_semantic` 的对象作为 `operator()` 的第二个参数，以定义选项为名/值对。你不需要直接访问 `boost::program_options::value_semantic`。你可以使用辅助函数 `boost::program_options::value()`，它创建一个 `boost::program_options::value_semantic` 对象。`boost::program_options::value()` 返回该对象的地址，你可以通过 `operator()` 将其传递。

`boost::program_options::value()` 是一个模板函数，接受命令行选项值的类型作为模板参数。因此，命令行选项 `--age` 期望整数，`--pi` 期望浮点数。

`boost::program_options::value()` 返回的对象提供实用的成员函数。例如，你可以调用 `default_value()` 提供默认值。示例 63.1“使用 Boost.ProgramOptions 的基本方法”会在命令行上没有使用该选项时将其设置为 3.14。

`notifier()` 将一个函数与命令行选项的值关联。然后，该函数将使用命令行选项的值被调用。示例 63.1“使用 Boost.ProgramOptions 的基本方法”将函数 `on_age()` 与 `--age` 关联。如果命令行选项 `--age` 用于设置年龄，则年龄将传递给 `on_age()`，后者将其输出到标准输出。

使用 `on_age()` 等函数处理值是可选的。你不需要使用 `notifier()`，因为可以通过其他方式访问值。

在定义所有命令行选项后，使用解析器。示例 63.1“使用 Boost.ProgramOptions 的基本方法”调用辅助函数 `boost::program_options::parse_command_line()` 来解析命令行。该函数获取 `argc` 和 `argv`（定义命令行）以及 `desc`（包含选项描述）。`boost::program_options::parse_command_line()` 返回类型为 `boost::program_options::parsed_options` 的解析选项对象。你通常不直接访问该对象。相反，你将其传递给 `boost::program_options::store()`，从而将解析选项存储在容器中。

# 示例 63.1：“Boost.ProgramOptions 的基本方法”

将 `vm` 作为第二个参数传递给 `boost::program_options::store()`。`vm` 是一个类型为 `boost::program_options::variables_map` 的对象。该类派生自 `std::map<std::string, boost::program_options::variable_value>`，因此提供了与 `std::map` 相同的成员函数。例如，你可以调用 `count()` 来检查某个命令行选项是否已使用并存储在容器中。

在示例 63.1“Boost.ProgramOptions 的基本方法”中，在访问 `vm` 并调用 `count()` 之前，调用了 `boost::program_options::notify()`。此函数会触发通过 `notifier()` 与某个值绑定的函数，例如 `on_age()`。如果没有调用 `boost::program_options::notify()`，`on_age()` 将不会被调用。

`vm` 允许你检查某个命令行选项是否存在，同时也允许你访问该命令行选项设置的值。该值的类型是 `boost::program_options::variable_value`，这是一个内部使用 `boost::any` 的类。你可以从成员函数 `value()` 获取类型为 `boost::any` 的对象。

在示例 63.1“Boost.ProgramOptions 的基本方法”中调用的是 `as()` 而不是 `value()`。此成员函数将命令行选项的值转换为作为模板参数传递的类型。`as()` 使用 `boost::any_cast()` 进行转换。

确保传递给 `as()` 的类型与命令行选项的类型匹配。例如，示例 63.1“Boost.ProgramOptions 的基本方法”期望命令行选项 `--age` 被设置为 `int` 类型，因此 `int` 必须作为模板参数传递给 `as()`。

你可以通过多种方式启动示例 63.1。这是一个示例：

```bash
test
```

在这种情况下，显示 `Pi: 14`。由于命令行上没有设置 `--pi`，将显示默认值。

此示例使用 `--pi` 设置了一个值：

```bash
test --pi 1415
```

程序现在显示 `Pi: 1415`。

此示例还传递了 age：

```bash
test --pi 1415 --age 29
```

输出现在是 `On age: 29` 和 `Age: 29`。当调用 `boost::program_options::notify()` 时，写入第一行；这触发了 `on_age()` 的执行。如果未设置 `--age`，程序使用 `else` 语句对 `--pi` 没有输出。

此示例显示帮助信息：

```bash
test -h
```

你获得了所有命令行选项的完整概述：

```text
Options:
  -h Help screen
  --pi Pi
  --age Age
```

如所示，由于定义了命令行选项的短名称，帮助可以通过两种方式显示。对于 `--pi`，显示默认值。命令行选项及其描述会自动格式化。你只需要像示例 63.1 那样将 `boost::program_options::options_description` 对象写入标准输出即可。

现在，这样启动示例：

```bash
test --age
```

输出如下：

```text
the required argument for option '--age' is missing.
```



由于没有设置`--age`，`boost::program_options::parse_line()`中的解析器抛出了`boost::program_options::error`异常。该异常被捕获，错误信息被写入标准输出。`boost::program_options::error`派自`std::logic_error`。Boost.ProgramOptions 定义了更多派自`boost::program_options::error`的异常。其中之一是`boost::program_options::invalid_syntax`，如果你为`--age`提供值，在示例 63.1 中就会抛出该异常。

示例 63.2，“Boost.ProgramOptions 的特殊配置”介绍了 Boost.ProgramOptions 可用的更多配置。

## 示例 63.2. Boost.ProgramOptions 的特殊配置

```cpp
#include <boost/program_options.hpp>
#include <string>
#include <vector>
#include <algorithm>
#include <iterator>
#include <iostream>

using namespace boost::program_options;

void to_cout(const std::vector<std::string> &v)
{
  std::copy(v.begin(), v.end(), std::ostream_iterator<std::string>{
    std::cout, "\n"});
}

int main(int argc, const char *argv[])
{
  try
  {
    int age;

    options_description desc{"Options"};
    desc.add_options()
      ("help,h", "Help screen")
      ("pi", value<float>()->implicit_value(3.14f), "Pi")
      ("age", value<int>(&age), "Age")
      ("phone", value<std::vector<std::string>>()->multitoken()->
        zero_tokens()->composing(), "Phone")
      ("unreg", "Unrecognized options");

    command_line_parser parser{argc, argv};
    parser.options(desc).allow_unregistered().style(
      command_line_style::default_style |
      command_line_style::allow_slash_for_short);
    parsed_options parsed_options = parser.run();

    variables_map vm;
    store(parsed_options, vm);
    notify(vm);

    if (vm.count("help"))
      std::cout << desc << '\n';
    else if (vm.count("age"))
      std::cout << "Age: " << age << '\n';
    else if (vm.count("phone"))
      to_cout(vm["phone"].as<std::vector<std::string>>());
    else if (vm.count("unreg"))
      to_cout(collect_unrecognized(parsed_options.options,
        exclude_positional));
    else if (vm.count("pi"))
      std::cout << "Pi: " << vm["pi"].as<float>() << '\n';
  }
  catch (const error &ex)
  {
    std::cerr << ex.what() << '\n';
  }
}
```

示例 63.2，“Boost.ProgramOptions 的特殊配置”解析命令行选项的方式与之前的示例。然而存在一些显著区别。例如，在定义`--pi`命令行选项时，调用的是`implicit_value()`而不是`default_value()`。这意味着 pi 默认设置为 3.14。必须在命令行上设置`--pi`，pi 才是可用的。但是，如果你使用了`implicit_value()`，则不需要为`--pi`命令行选项提供值。传递`--pi`而不设置值即可。

Example 63.2, “Special configuration settings with Boost.ProgramOptions” 支持一个新的命令行选项`--phone`，用于向程序传递电话号码。事实上，你可以在命令行上传递多个电话号码。例如，以下命令行使用电话号码 123 和 456 启动程序：

```
test --phone 123 456
```

Example 63.2, “Special configuration settings with Boost.ProgramOptions” 之所以支持多个电话号码，是因为在 fact 该命令行选项的值上调用了`multitoken()`。此外，由于调用了`zero_tokens()`，`--phone`也可以在不传递电话号码的情况下使用。

你也可以通过重复使用`--phone`选项来传递多个电话号码，如下方的命令行所示：

```
test --phone 123 --phone 456
```

在这种情况下，两个电话号码 123 和 456 被解析。对`composing()`的调用使得多次使用命令行选项成为可能——值会被组合在一起。

`--phone`参数的值类型为`std::vector<std::string>`。你需要使用一个容器来存储多个电话号码。

Example 63.2, “Special configuration settings with Boost.ProgramOptions” 定义了另一个命令行选项`--unreg`。这是一个无法设置数值的开关（switch）。它在示例的后部分被用于决定是否显示未在`desc`中定义的命令行选项。

虽然 Example 63.1, “Basic approach with Boost.ProgramOptions” 调用函数`boost::program_options::parse_command_line()`来解析命令行选项，但 Example 63.2, “Special configuration settings with Boost.ProgramOptions” 使用类型为`boost::program_options::command_line_parser`的解析器。`argc`和`argv`被传递给构造函数。

`boost::program_options::command_line_parser`提供了几个成员函数。你必须调用`options()`将命令行选项的定义传递给解析器。

与其他成员函数一样，`options()`返回对同一个解析器的引用。这样，就可以方便地链式调用成员函数。Example 63.2, “Special configuration settings with Boost.ProgramOptions” 在`options()`之后调用`allow_unregistered()`，以告诉解析器在检测到未知命令行选项时不抛出异常。最后，调用`style()`告诉解析器可以使用斜杠配合短名称。因此，`--help`选项的短名称可以是`-h`也可以是`/h`。

请注意，`boost::program_options::parse_command_line()`支持第四个参数，该参数会被转发给`style()`。如果你想使用类似`boost::program_options::command_line_style::allow_slash_for_short`的选项，你仍然可以使用`boost::program_options::parse_command_line()`函数。

配置完成后，在解析器上调用`run()`。该成员函数返回一个类型为`boost::program_options::parsed_options`的对象的解析后的命令行选项，你可以将其传递给`boost::program_options::store()`将选项存储在`vm`中。

在代码的后续，Example 63.2, “Special configuration settings with Boost.ProgramOptions” 再次访问`vm`以评估命令行选项。只有调用`boost::program_options::collect_unrecognized()`是新的。该函数为命令行选项`--unreg`调用。该函数期望一个类型为`boost::program_options::parsed_options`的对象（由`run()`返回）。它将所有未知的命令行选项返回到一个`std::vector<std::string>`。例如，如果你用`test --unreg --abc`启动程序，`--abc`将写入标准输出。

当将`boost::program_options::exclude_positional`作为第二个参数传递给`boost::program_options::collect_unrecognized()`时，位置选项会被忽略。对于 Example 63.2, “Special configuration settings with Boost.ProgramOptions”，这并不重要，因为没有定义位置选项。然而，`boost::program_options::collect_unrecognized()`需要此参数。

Example 63.3, “Positional options with Boost.ProgramOptions” 展示了位置选项。

### Example 63.3. Positional options with Boost.ProgramOptions

```cpp
#include <boost/program_options.hpp>
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace boost::program_options;

void to_cout(const std::vector<std::string> &v)
{
  std::copy(v.begin(), v.end(),
    std::ostream_iterator<std::string>{std::cout, "\n"});
}

int main(int argc, const char *argv[])
{
  try
  {
    options_description desc{"Options"};
    desc.add_options()
      ("help,h", "Help screen")
      ("phone", value<std::vector<std::string>>()->
        multitoken()->zero_tokens()->composing(), "Phone");

    positional_options_description pos_desc;
    pos_desc.add("phone", -1);

    command_line_parser parser{argc, argv};
    parser.options(desc).positional(pos_desc).allow_unregistered();
    parsed_options parsed_options = parser.run();

    variables_map vm;
    store(parsed_options, vm);
    notify(vm);

    if (vm.count("help"))
      std::cout << desc << '\n';
    else if (vm.count("phone"))
      to_cout(vm["phone"].as<std::vector<std::string>>());
  }
  catch (const error &ex)
  {
    std::cerr << ex.what() << '\n';
  }
}
```

对类型为`boost::program_options::positional_options_description`的对象调用`add()`，可以使用位置数字将命令行上的值分配给命令行选项。当使用命令行`test 123 456`调用 示例 63.3, “使用 Boost.ProgramOptions 的位置参数”时，123 的位置号为 0，456 的位置号为 1。示例 63.3, “使用 Boost.ProgramOptions 的位置参数”会向`add()`传递 -1，这会将所有值——123 和 456——都分配给`--phone`。如果你将 示例 63.3, “使用 Boost.ProgramOptions 的位置参数”修改为向`add()`传递值 0，则只有 123 会识别为电话号码。如果向`add()`传递 1，则只有 456 会被识别。

`pos_desc`通过`positional()`传递给解析器。解析器以此知道哪些命令行选项是位置参数。

请注意，你必须确保已经定义了位置参数。例如，在 示例 63.3, “使用 Boost.ProgramOptions 的位置参数”中，“phone”只能被传递给`add()`，因为`desc`中已经存在`--phone`的定义。

在所有之前的示例中，Boost.ProgramOptions 都被用于解析命令行选项。然而，该库也支持从文件加载配置选项。如果需要重复设置相同的命令行选项，这将非常有用。

示例 63.4, “从配置文件加载选项”使用两个类型为`boost::program_options::options_description`的对象。`generalOptions`定义了必须在命令行设置的选项。`fileOptions`定义了可以从配置文件加载的选项。

并不是强制要求使用两个不同类型的`boost::program_options::options_description`对象来定义选项。如果命令行和文件使用的选项集相同，则可以使用其中一个。在 示例 63.4, “从配置文件加载选项”中，分离选项是有意义的，因为你不希望允许在配置文件中设置`--help`。如果允许这样做且用户在配置文件中放入了该选项，程序每次运行时都会显示帮助屏幕。

示例 63.4, “从配置文件加载选项”从配置文件加载`--age`。你可以将配置文件的名称作为命令行选项传递。在这个示例中，由于原因，`--config`在`generalOptions`中定义。

在用`boost::program_options::parse_command_line()`解析命令行选项并将其存储在`vm`后，示例检查`--config`是否被设置。如果是，则用`std::ifstream`打开配置文件。将`std::ifstream`对象连同描述选项的`fileOptions`一起传递给函数`boost::program_options::parse_config_file()`。`boost::program_options::parse_config_file()`的作用与`boost::program_options::parse_command_line()`相同，并在类型为`boost::program_options::parsed_options`的对象中返回解析后的选项。将其传递传递`boost::program_options::store()`以将解析后的选项存储在`vm`中。

示例 63.4. 从配置文件加载选项



```cpp
#include <boost/program_options.hpp>
#include <string>
#include <fstream>
#include <iostream>

using namespace boost::program_options;

int main(int argc, const char *argv[])
{
  try
  {
    options_description generalOptions{"General"};
    generalOptions.add_options()
      ("help,h", "Help screen")
      ("config", value<std::string>(), "Config file");

    options_description fileOptions{"File"};
    fileOptions.add_options()
      ("age", value<int>(), "Age");

    variables_map vm;
    store(parse_command_line(argc, argv, generalOptions), vm);
    if (vm.count("config"))
    {
      std::ifstream ifs{vm["config"].as<std::string>().c_str()};
      if (ifs)
        store(parse_config_file(ifs, fileOptions), vm);
    }
    notify(vm);

    if (vm.count("help"))
      std::cout << generalOptions << '\n';
    else if (vm.count("age"))
      std::cout << "Your age is " << vm["age"].as<int>() << '\n';
  }
  catch (const error &ex)
  {
    std::cerr << ex.what() << '\n';
  }
}
```

# 64. Boost.Serialization

该库 [Boost.Serialization](http://www.boost.org/libs/serialization) 使得 C++ 程序中的对象转换为可以保存和加载的字节序列成为可能。提供了不同的数据格式来定义生成字节序列的规则。Boost.Serialization 支持的所有格式都仅供此库使用。例如，为 Boost.Serialization 开发的 XML 格式不应用于与未使用 Boost 的程序进行数据交换。

Boost.Serialization 的核心概念是存档（archive）。存档是表示序列化后 C++ 对象的字节序列。可以将对象添加到存档中进行序列化，稍后从存档中加载。为了恢复之前保存的 C++ 对象，假定类型是相同的。

该库提供了存档类，例如 `boost::archive::text_oarchive`，它定义在 `boost/archive/text_oarchive.hpp` 中。该类使得将对象序列化为文本流成为可能。在 Boost 1.56.0 中，示例 64.1，“使用 `boost::archive::text_oarchive`” 向标准输出流写入 `22 serialization::archive 11 1`。

Boost.ProgramOptions 还定义了函数 `boost::program_options::parse_environment()`，可以从环境加载选项。`environment_iterator` 类允许你遍历环境变量。

### 注意

正如 Boost 库 1.55.0 版本的[发布说明](http://www.boost.org/users/history/version_1_55_0.html)所示，缺少包含会导致 Visual C++ 2013 出现编译错误。该错误在 Boost 1.56.0 中已修复。

## 示例 64.1. 使用 `boost::archive::text_oarchive`

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <iostream>

using namespace boost::archive;

int main()
{
  text_oarchive oa{std::cout};
  int i = 1;
  oa << i;
}
```

由此所示，类型为 `boost::archive::text_oarchive` 的对象 `oa` 可以像流一样使用，通过 `operator<<` 来序列化变量。然而，不应将归档视为存储任意数据的普通流。要恢复数据，你必须按照存储的方式来访问它，并使用相同的数据类型和相同的顺序。示例 64.2，“使用 `boost::archive::text_iarchive`” 序列化并恢复了一个 `int` 类型的变量。

## 示例 64.2. 使用 `boost::archive::text_iarchive`

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <iostream>
#include <fstream>

using namespace boost::archive;

void save()
{
  std::ofstream file{"archive.txt"};
  text_oarchive oa{file};
  int i = 1;
  oa << i;
}

void load()
{
  std::ifstream file{"archive.txt"};
  text_iarchive ia{file};
  int i = 0;
  ia >> i;
  std::cout << i << '\n';
}

int main()
{
  save();
  load();
}
```

`boost::archive::text_oarchive` 类将数据作为文本流序列化，而 `boost::archive::text_iarchive` 类则从这样的文本流中恢复数据。要使用这些类，请包含头文件 `boost/archive/text_iarchive.hpp` 和 `boost/archive/text_oarchive.hpp`。

归档的构造函数期望一个输入或输出流作为参数。该流用于序列化或恢复数据。虽然示例 64.2，“使用 `boost::archive::text_iarchive`” 使用的是文件，但也可以使用其他流，例如 `stringstream`。

## 示例 64.3. 使用 `stringstream` 序列化

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

void save()
{
  text_oarchive oa{ss};
  int i = 1;
  oa << i;
}

void load()
{
  text_iarchive ia{ss};
  int i = 0;
  ia >> i;
  std::cout << i << '\n';
}

int main()
{
  save();
  load();
}
```

示例 64.3，“使用 `stringstream` 序列化” 使用 `stringstream` 序列化数据并向标准输出写入了 `1`。

到目前为止，只有基本类型被序列化了。示例 64.4，“使用成员函数序列化用户定义类型” 显示了如何序列化用户定义类型的对象。为了序列化用户定义类型的对象，你必须定义成员函数 `serialize()`。该函数在对象序列化到字节流或从字节流恢复时被调用。由于 `serialize()` 同时用于序列化和恢复，Boost.Serialization 除了 `operator<<` 和 `operator>>` 之外，还支持 `operator&`。使用 `operator&` 则无需在 `serialize()` 内部区分序列化和恢复。

## 示例 64.4. 使用成员函数序列化用户定义类型

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs) : legs_{legs} {}
  int legs() const { return legs_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version) { ar & legs_; }

  int legs_;
};

void save()
{
  text_oarchive oa{ss};
  animal a{4};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  ia >> a;
  std::cout << a.legs() << '\n';
}

int main()
{
  save();
  load();
}
```

每当对象被序列化或恢复时，`serialize()` 自动调用。它不应该被显式调用，因此应该声明为私有。如果声明为私有，则必须将 `boost::serialization::access` 类声明为它的友元。

## 示例 64.5. 使用全局函数序列化

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

struct animal
{
  int legs_;

  animal() = default;
  animal(int legs) : legs_{legs} {}
  int legs() const { return legs_; }
};

template <typename Archive>
void serialize(Archive &ar, animal &a, const unsigned int version)
{
  ar & legs_;
}

void save()
{
  text_oarchive oa{ss};
  animal a{4};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  ia >> a;
  std::cout << a.legs() << '\n';
}

int main()
{
  save();
  load();
}
```

可能某些情况不允许修改示例 64.5，“使用全局函数序列化” 现有类，该函数期望一个对象的引用作为第二个参数。

将 `serialize()` 实现为全局函数需要类的成员变量可以从外部访问。示例 64.5，“使用全局函数序列化” 中 `legs_` 不再是 `animal` 的私有成员。

Boost.Serialization 为标准库中的许多类提供了 `serialize()` 函数。为了序列化基于标准类的对象，需要包含额外的头文件。

## 示例 64.6. 序列化字符串

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/string.hpp>
#include <iostream>
#include <sstream>
#include <string>
#include <utility>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs, std::string name) :
    legs_{legs}, name_{std::move(name)} {}
  int legs() const { return legs_; }
  const std::string &name() const { return name_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  friend void serialize(Archive &ar, animal &a, const unsigned int version);

  int legs_;
  std::string name_;
};

template <typename Archive>
void serialize(Archive &ar, animal &a, const unsigned int version)
{
  ar & a.legs_;
  ar & a.name_;
}

void save()
{
  text_oarchive oa{ss};
  animal a{4, "cat"};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  ia >> a;
  std::cout << a.legs() << '\n';
  std::cout << a.name() << '\n';
}

int main()
{
  save();
  load();
}
```

示例 64.6，“序列化字符串” 通过增加一个类型为 `std::string` 的成员变量 `name_` 扩展了 `animal` 类。为了序列化该成员变量，必须包含 `boost/serialization/string.hpp` 头以提供相应的全局 `serialize()` 函数。

如前所述，`Boost.Serialization` 为标准库中的许多类定义了 `serialize()` 函数。这些函数定义在头文件中，其文件名与标准库中对应的头文件同名。因此，要序列化 `std::string` 类型的对象，请包含头文件 `boost/serialization/string.hpp`；要序列化 `std::vector` 类型的对象，请包含头文件 `boost/serialization/vector.hpp`。包含哪个头文件是显而易见的。

`serialize()` 函数目前为止被忽略的一个参数是 `version`。该参数有助于使存档具有向后兼容性。示例 64.7，“版本数的向后兼容性” 可以加载由示例 64.5，“使用独立函数进行序列化” 创建的存档。示例 64.5，“使用独立函数进行序列化” 中 `animal` 类的版本不包含名称。示例 64.7，“版本数的向后兼容性” 在加载存档时会检查版本号，并且仅当版本大于 0 时才访问名称。这允许它处理一个在没有名称的情况下创建的旧版本存档。

宏 `BOOST_CLASS_VERSION` 为一个类分配一个版本号。示例 64.7，“版本数的向后兼容性” 中 `animal` 类的版本号为 1。如果没有使用 `BOOST_CLASS_VERSION`，则版本号默认为 0。

## 示例 64.7. 版本数的向后兼容性



```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/string.hpp>
#include <iostream>
#include <sstream>
#include <string>
#include <utility>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs, std::string name) :
    legs_{legs}, name_{std::move(name)} {}
  int legs() const { return legs_; }
  const std::string &name() const { return name_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  friend void serialize(Archive &ar, animal &a, const unsigned int version);

  int legs_;
  std::string name_;
};

template <typename Archive>
void serialize(Archive &ar, animal &a, const unsigned int version)
{
  ar & a.legs_;
  if (version > 0)
    ar & a.name_;
}

BOOST_CLASS_VERSION(animal, 1)

void save()
{
  text_oarchive oa{ss};
  animal a{4, "cat"};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  ia >> a;
  std::cout << a.legs() << '\n';
  std::cout << a.name() << '\n';
}

int main()
{
  save();
  load();
}
```

版本号存储在存档中，并是存档的一部分。虽然通过 `BOOST_CLASS_VERSION` 宏为特定类指定的版本号在序列化期间会被使用，但在恢复时，`serialize()` 的 `version` 参数会被设置为存档中存储的值。如果 `animal` 的新版本访问一个包含用旧版本序列化的对象的存档，那么成员变量 `name_` 将不会被恢复，因为旧版本没有该成员变量。

## 指针和引用

Boost.Serialization 还可以序列化指针和引用。由于指针存储的是对象的地址，因此序列化地址没有太大意义。在序列化指针和引用时，被引用的对象会被序列化。

示例 64.8，“序列化指针”使用 `new` 创建一个 `animal` 类型的新对象，并将其赋值给指针 `a`。然后序列化的是指针——而不是 `*a`。Boost.Serialization 会自动序列化 `a` 引用的对象，而不是对象的地址。

如果恢复了存档，`a` 不一定包含相同的地址。相反会创建一个新对象并将其地址赋值给 `a`。Boost.Serialization 只保证该对象与序列化的对象相同，而不保证其地址相同。

由于智能指针与动态分配内存内存使用，Boost.Serialization 也为它们提供了支持。

### 示例 64.8. 序列化指针

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/string.hpp>
#include <iostream>
#include <sstream>
#include <string>
#include <utility>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs, std::string name) :
    legs_{legs}, name_{std::move(name)} {}
  int legs() const { return legs_; }
  const std::string &name() const { return name_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  friend void serialize(Archive &ar, animal &a, const unsigned int version);

  int legs_;
  std::string name_;
};

template <typename Archive>
void serialize(Archive &ar, animal &a, const unsigned int version)
{
  ar & a.legs_;
  if (version > 0)
    ar & a.name_;
}

BOOST_CLASS_VERSION(animal, 1)

void save()
{
  text_oarchive oa{ss};
  animal a{4, "cat"};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  ia >> a;
  std::cout << a.legs() << '\n';
  std::cout << a.name() << '\n';
}

int main()
{
  save();
  load();
}
```

### 6. .......

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/string.hpp>
#include <iostream>
#include <sstream>
#include <string>
#include <utility>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs, std::string name) :
    legs_{legs}, name_{std::move(name)} {}
  int legs() const { return legs_; }
  const std::string &name() const { return name_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  friend void serialize(Archive &ar, animal &a, const unsigned int version);

  int legs_;
  std::string name_;
};

template <typename Archive>
void serialize(Archive &ar, animal &a, const unsigned int version)
{
  ar & a.legs_;
  if (version > 0)
    ar & a.name_;
}

BOOST_CLASS_VERSION(animal, 1)

void save()
{
  text_oarchive oa{ss};
  animal a{4, "cat"};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  ia >> a;
  std::cout << a.legs() << '\n';
  std::cout << a.name() << '\n';
}

int main()
{
  save();
  load();
}
```

示例 64.9，“序列化指针”使用智能指针 `boost::scoped_ptr` 来管理动态分配的 `animal` 类型对象。包含头文件 `boost/serialization/scoped_ptr.hpp` 以序列化此类指针。要序列化 `boost::shared_ptr` 类型的智能指针，使用头文件 `boost/serialization/shared_ptr.hpp`。

### 示例 64.10. 序列化引用

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs, std::string name) :
    legs_{legs}, name_{std::move(name)} {}
  int legs() const { return legs_; }
  const std::string &name() const { return name_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version) { ar & legs_; }

  int legs_;
  std::string name_;
};

void save()
{
  text_oarchive oa{ss};
  animal a{4};
  animal &r = a;
  oa << r;
}

void load()
{
  text_iarchive ia{ss};
  animal a;
  animal &r = a;
  ia >> r;
  std::cout << r.legs() << '\n';
}

int main()
{
  save();
  load();
}
```

请注意，Boost.Serialization 尚未针对 C++11 更新。C++11 标准库中的智能指针（如 `std::shared_ptr` 和 `std::unique_ptr`）目前不受 Boost.Serialization 支持。

Boost.Serialization 也可以毫无问题地序列化引用（参见示例 64.10，“序列化引用”）。与指针一样，被引用的对象会被序列化。

## 类层次结构对象的序列化

根据类层次结构序列化对象时，派生类必须在成员函数 `serialize()` 访问函数 `boost::serialization::base_object()`。该函数确保基类的继承成员变量被正确地序列化。

示例 64.11，“正确地序列化派生类”使用了一个名为 `bird` 的类，该类派生自 `animal`。`animal` 和 `bird` 都定义了一个私有成员函数 `serialize()`，使得可以基于任何一个类序列化对象。由于 `bird` 派生自 `animal`，`serialize()` 必须确保继承自 `animal` 的成员变量也被序列化。

通过在派生类的成员函数 `serialize()` 内部访问基类并调用 `boost::serialization::base_object()` 来序列化继承的成员变量。你必须使用此函数，例如 `static_cast`，因为只有 `boost::serialization::base_object()` 能确保正确的序列化。

### 示例 64.11. 正确地序列化派生类

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;
std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs) : legs_{legs} {}
  int legs() const { return legs_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version) { ar & legs_; }

  int legs_;
};

class bird : public animal
{
public:
  bird() = default;
  bird(int legs, bool can_fly) :
    animal{legs}, can_fly_{can_fly} {}
  bool can_fly() const { return can_fly_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version)
  {
    ar & boost::serialization::base_object<animal>(*this);
    ar & can_fly_;
  }

  bool can_fly_;
};

void save()
{
  text_oarchive oa{ss};
  bird penguin{2, false};
  oa << penguin;
}

void load()
{
  text_iarchive ia{ss};
  bird penguin;
  ia >> penguin;
  std::cout << penguin.legs() << '\n';
  std::cout << std::boolalpha << penguin.can_fly() << '\n';
}

int main()
{
  save();
  load();
}
```

动态创建对象的地址可以赋值给相应基类类型的指针。示例 64.12，“使用 `BOOST_CLASS_EXPORT` 静态注册派生类”显示了 Boost.Serialization 也能正确地序列化它们。

### 示例 64.12. 使用 `BOOST_CLASS_EXPORT` 静态注册派生类



```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/export.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs) : legs_{legs} {}
  virtual int legs() const { return legs_; }
  virtual ~animal() = default;

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version) { ar & legs_; }

  int legs_;
};

class bird : public animal
{
public:
  bird() = default;
  bird(int legs, bool can_fly) :
    animal{legs}, can_fly_{can_fly} {}
  bool can_fly() const { return can_fly_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version)
  {
    ar & boost::serialization::base_object<animal>(*this);
    ar & can_fly_;
  }

  bool can_fly_;
};

BOOST_CLASS_EXPORT(bird)

void save()
{
  text_oarchive oa{ss};
  animal *a = new bird{2, false};
  oa << a;
  delete a;
}

void load()
{
  text_iarchive ia{ss};
  animal *a;
  ia >> a;
  std::cout << a->legs() << '\n';
  delete a;
}

int main()
{
  save();
  load();
}
```

`BOOST_CLASS_EXPORT` 的优势在于它注册了后续可能不会被使用的类型。

## 示例 64.13. 使用 `register_type()` 动态注册派生类

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/export.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

class animal
{
public:
  animal() = default;
  animal(int legs) : legs_{legs} {}
  virtual int legs() const { return legs_; }
  virtual ~animal() = default;

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version) { ar & legs_; }

  int legs_;
};

class bird : public animal
{
public:
  bird() = default;
  bird(int legs, bool can_fly) :
    animal{legs}, can_fly_{can_fly} {}
  bool can_fly() const { return can_fly_; }

private:
  friend class boost::serialization::access;

  template <typename Archive>
  void serialize(Archive &ar, const unsigned int version)
  {
    ar & boost::serialization::base_object<animal>(*this);
    ar & can_fly_;
  }

  bool can_fly_;
};

void save()
{
  text_oarchive oa{ss};
  oa.register_type<bird>();
  animal *a = new bird{2, false};
  oa << a;
  delete a;
}

void load()
{
  text_iarchive ia{ss};
  ia.register_type<bird>();
  animal *a;
  ia >> a;
  std::cout << a->legs() << '\n';
  delete a;
}

int main()
{
  save();
  load();
}
```

## 用于优化的包装函数

本节引入了包装函数来优化序列化过程。这些函数标记对象，允许 Boost.Serialization 应用某些优化技术。

## 示例 64.14. 不使用包装函数序列化数组

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/array.hpp>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

void save()
{
  text_oarchive oa{ss};
  boost::array<int, 3> a{{0, 1, 2}};
  oa << a;
}

void load()
{
  text_iarchive ia{ss};
  boost::array<int, 3> a;
  ia >> a;
  std::cout << a[0] << ", " << a[1] << ", " << a[2] << '\n';
}

int main()
{
  save();
  load();
}
```

示例 64.14“**不使用包装函数序列化数组**”在未使用任何包装函数的情况下使用了 Boost.Serialization。该示例创建并向字符串写入了值 `22 serialization::archive 11 0 0 3 0 1 2`。使用包装函数 `boost::serialization::make_array()`，写入的值可以缩短为以下字符串：`22 serialization::archive 11 0 1 2`。

## 示例 64.15. 使用包装函数 `make_array()` 序列化数组

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <boost/serialization/array.hpp>
#include <array>
#include <iostream>
#include <sstream>

using namespace boost::archive;

std::stringstream ss;

void save()
{
  text_oarchive oa{ss};
  std::array<int, 3> a{{0, 1, 2}};
  oa << boost::serialization::make_array(a.data(), a.size());
}

void load()
{
  text_iarchive ia{ss};
  std::array<int, 3> a;
  ia >> boost::serialization::make_array(a.data(), a.size());
  std::cout << a[0] << ", " << a[1] << ", " << a[2] << '\n';
}

int main()
{
  save();
  load();
}
```

`boost::serialization::make_array()` 期望数组的地址和长度。然而，由于长度是预知的，因此长度不需要作为数组的一部分进行序列化。

当 `std::array` 或 `std::vector` 等类包含可以直接被序列化的数组时，可以使用 `boost::serialization::make_array()`。通常也会被序列化的其他成员变量会被跳过（请参见示例 64.15“使用包装函数 `make_array()` 序列化数组”）。

Boost.Serialization 还提供了包装器 `boost::serialization::make_binary_object()`。与 `boost::serialization::make_array()` 类似，该函数期望一个地址和一个长度。`boost::serialization::make_binary_object()` 专门用于没有底层结构的二进制数据，而 `boost::serialization::make_array()` 用于数组。

# 65. Boost.Uuid

[Boost.Uuid](http://www.boost.org/libs/uuid) 为 UUID 提供生成器。UUID 是全局唯一标识符，不依赖于中央协调实例。例如，没有任何数据库存储所有生成的 UUID 以便检查新的 UUID 是否已使用。

UUID 用于必须唯一标识组件的分布式系统。例如，微软使用 UUID 来标识 COM 世界中的接口。对于为 COM 开发的新接口，可以很容易地分配唯一标识符。

UUID 是 128 位数。存在多种生成 UUID 的方法。例如，可以使用计算机的网络地址来生成 UUID。Boost.Uuid 提供的生成器基于随机数生成器，以避免生成可以追溯到生成它的计算机的 UUID。

Boost.Uuid 的所有类和函数定义在 `boost::uuids` 命名空间中。没有一个主头文件可以访问它们的所有内容。

## 示例 65.1. 使用 `boost::uuids::random_generator` 生成随机 UUID

示例 65.1“使用 `boost::uuids::random_generator` 生成随机 UUID”生成了一个随机 UUID。它使用了类 `boost::uuids::random_generator`，该类定义在 `boost/uuid/uuid_generators.hpp` 中。此头文件提供了对 Boost.Uuid 的所有生成器的访问。

`boost::uuids::random_generator` 的用法类似于 C++11 标准库或 Boost.Random 中的生成器。该类重载了 `operator()` 来生成随机 UUID。

UUID 的类型是 `boost::uuids::uuid`。`boost::uuids::uuid` 是一个 POD——纯数据。没有生成器无法创建 `boost::uuids::uuid` 类型的对象。但它是一个紧凑类型，正好分配了 128 位。该类定义在 `boost/uuid/uuid.hpp` 中。

`boost::uuids::uuid` 类型的对象可以写入标准输出流。然而，你必须包含 `boost/uuid/uuid_io.hpp`。此头文件提供了重载运算符，用于将 `boost::uuids::uuid` 类型的对象写入输出流。

```cpp
#include <boost/uuid/uuid.hpp>
#include <boost/uuid/uuid_generators.hpp>
#include <boost/uuid/uuid_io.hpp>
#include <iostream>

using namespace boost::uuids;

int main()
{
  random_generator gen;
  uuid id = gen();
  std::cout << id << '\n';
}
```

在使用 `string_generator` 时，请注意 UUID 的拼写。你可以传递不带连字符的 UUID，但如果你使用连字符，它们必须位于正确的位置。大小（大写或小写）是被忽略的。

## 示例 65.4. 转换为字符串

```cpp
#include <boost/uuid/uuid.hpp>
#include <boost/uuid/uuid_generators.hpp>
#include <boost/uuid/uuid_io.hpp>
#include <boost/lexical_cast.hpp>
#include <string>
#include <iostream>

using namespace boost::uuids;

int main()
{
  random_generator gen;
  uuid id = gen();

  std::string s = to_string(id);
  std::cout << s << '\n';

  std::cout << boost::lexical_cast<std::string>(id) << '\n';
}
```

Boost.Uuid 提供了 `boost::uuids::to_string()` 和 `boost::uuids::to_wstring()` 函数将 UUID 转换为字符串（参见示例 65.4“转换为字符串”）。也可以使用 `boost::lexical_cast()` 进行转换。

# 第 XVI 部分. 设计模式

以下库用于设计模式：

- Boost.Flyweight 帮助处理程序中使用了大量相同对象且需要减少内存占用的情况。
- Boost.Signals2 使得使用观察者模式变得简单。该库被称为 Boost.Signals2，是因为其实现了信号/槽（signal/slot）概念。
- Boost.MetaStateMachine 使得将状态机从 UML 转换为 C++ 成为可能。

# 66. Boost.Flyweight

[Boost.Flyweight](http://www.boost.org/libs/flyweight) 是易于使用同名设计模式的库。当许多对象共享数据时，Flyweight 帮助节省内存。通过这种设计模式，不再在对象中多次存储相同的数据，而是将共享数据只保留在一个地方，所有对象都引用该数据。虽然你可以用指针等方式实现这种设计模式，但使用 Boost.Flyweight 会更简单。

## 示例 66.1. 不使用 Boost.Flyweight 的十万个相同字符串

```cpp
#include <string>
#include <vector>

struct person
{
  int id_;
  std::string city_;
};

int main()
{
  std::vector<person> persons;
  for (int i = 0; i < 100000; ++i)
    persons.push_back({i, "Berlin"});
}
```

示例 66.1“不使用 Boost.Flyweight 的十万个相同字符串”创建了十万个类型为 `person` 的对象。`person` 定义了两个成员变量：`id_` 识别人员，`city_` 存储人们居住的城市。在这个示例中，所有人都住在柏林。这就是为什么在所有十万个对象中，`city_` 都设置为“Berlin”。因此，该示例使用了十万个设置了相同值的字符串。使用 Boost.Flyweight，可以使用一个字符串——而不是成千上万个——并减少内存消耗。

## 示例 66.2. 使用 Boost.Flyweight 用一个字符串代替十万个字符串

```cpp
#include <boost/flyweight.hpp>
#include <string>
#include <vector>
#include <utility>

using namespace boost::flyweights;

struct person
{
  int id_;
  flyweight<std::string> city_;
  person(int id, std::string city) : id_{id}, city_{std::move(city)} {}
};

int main()
{
  std::vector<person> persons;
  for (int i = 0; i < 100000; ++i)
    persons.push_back({i, "Berlin"});
}
```



要使用 Boost.Flyweight，请包含`boost/flyweight.hpp`，如示例 66.2，“使用 Boost.Flyweight 用一个字符串代替十万个字符串”所示。Boost.Flyweight 提供了额外的头文件，只有在你需要更改详细的库设置时才需要包含它们。

## 示例 66.3. 多次使用`boost::flyweights::flyweight`

```cpp
#include <boost/flyweight.hpp>
#include <string>
#include <vector>
#include <utility>

using namespace boost::flyweights;

struct person
{
  int id_;
  flyweight<std::string> city_;
  flyweight<std::string> country_;
  person(int id, std::string city, std::string country)
    : id_{id}, city_{std::move(city)}, country_{std::move(country)} {}
};

int main()
{
  std::vector<person> persons;
  for (int i = 0; i < 100000; ++i)
    persons.push_back({i, "Berlin"});
}
```

所有的`boost::flyweights::flyweight`都在`boost::flyweights`中。示例 66.2，“用一个字符串代替十万个字符串”使用`std::string`而不是`flyweight`。这是该库最重要的部分。成员变量`city_`使用`flyweight<std::string>`，Boost.Flyweight 用此减少了程序的内存需求。示例 66.3，“多次使用`boost::flyweights::flyweight`为`person`类增加了第二个成员变量`country_`。在这个示例中，所有人都住在柏林。这就是为什么在所有十万个对象中，`city_`都设置为“Berlin”。因此，该示例使用了十万个设置了相同值的字符串。使用 Boost.Flyweight，可以使用一个字符串——而不是成千上万个——并减少内存消耗。Boost.Flyweight 使用内部容器存储对象。默认情况下，由于`city_`和`country_`都是字符串，因此使用一个容器。如果必须存储不同的城市，最好将城市存储在一个容器中，将国家存储在另一个中。

## 示例 66.4. 使用标签多次使用`boost::flyweights::flyweight`

```cpp
#include <boost/flyweight.hpp>
#include <string>
#include <vector>
#include <utility>

using namespace boost::flyweights;

struct city {};
struct country {};

struct person
{
  int id_;
  flyweight<std::string, tag<city>> city_;
  flyweight<std::string, tag<country>> country_;
  person(int id, std::string city, std::string country)
    : id_{id}, city_{std::move(city)}, country_{std::move(country)} {}
};

int main()
{
  std::vector<person> persons;
  for (int i = 0; i < 100000; ++i)
    persons.push_back({i, "Berlin", "Germany"});
}
```

示例 66.4，“使用标签多次使用`boost::flyweights::flyweight`向`boost::flyweights::flyweight`传递了第二个模板参数。这是一个标签（tag）。标签是用于区分`city_`和`country_`所基础类型的任意类型。示例定义了两个空结构`city`和`country`用作标签。然而，该示例也可以使用`int`、`bool`或任何类型。

标签使得`city_`和`country_`使用不同的类型。现在 Boost.Flyweight 使用两个哈希容器——一个存储城市，另一个存储国家。

## 示例 66.5. `boost::flyweights::flyweight`的模板参数

```cpp
#include <boost/flyweight.hpp>
#include <boost/flyweight/set_factory.hpp>
#include <boost/flyweight/no_locking.hpp>
#include <boost/flyweight/no_tracking.hpp>
#include <string>
#include <vector>
#include <utility>

using namespace boost::flyweights;

struct person
{
  int id_;
  flyweight<std::string, set_factory<>, no_locking, no_tracking> city_;
  person(int id, std::string city) : id_{id}, city_{std::move(city)} {}
};

int main()
{
  std::vector<person> persons;
  for (int i = 0; i < 100000; ++i)
    persons.push_back({i, "Berlin"});
}
```

除了标签之外的模板参数可以传递给`boost::flyweights::flyweight`。示例 66.5，“`boost::flyweights::flyweight`的模板参数”传递了`boost::flyweights::set_factory`、`boost::flyweights::no_locking`和`boost::flyweights::no_tracking`。包含了额外的头文件以使用这些类。

`boost::flyweights::set_factory`告诉 Boost.Flyweight 使用排序容器（如`std::set`）而不是哈希容器。通过`boost::flyweights::no_locking`，禁用了通常默认启用的多线程支持。`boost::flyweights::no_tracking`告诉 Boost.Flyweight 不要跟踪存储在内部容器的对象。默认情况下，当对象不再使用时，Boost.Flyweight 会检测到这一点并将其从容器中移除。当设置了`boost::flyweights::no_tracking`时，检测机制被禁用。这提高了性能。然而，容器将只能增长而永远不会收缩。

Boost.Flyweight 支持额外的设置。如果你对调优的细节感兴趣，请查阅官方文档。

# 67. Boost.Signals2

[Boost.Signals2](http://www.boost.org/libs/signals2) 实现了信号/槽（signal/slot）概念。一个或多个函数（称为槽）与一个可以发射信号的对象关联。每当信号发射时，关联的函数就会被调用。

信号/槽概念在某些情况下非常有用，例如开发带有图形用户界面的应用程序。按钮可以被建模，以便在用户点击它们时发射信号。它们可以支持与许多函数的链接以处理用户输入。通过这种方式，可以灵活地处理事件。

`std::function`也可以用于事件处理。`std::function`和`Boost.Signals2`之间的一个关键区别是，`Boost.Signals2`可以关联多个事件处理器到单个事件。因此，`Boost.Signals2`更适合支持事件驱动开发，每当需要处理事件时，它应该是首选。

`Boost.Signals2`取替了`Boost.Signals`库，后者已被弃用且未在书中讨论。

## 信号

Boost.Signals2 提供了`boost::signals2::signal`类，用于创建信号。该类定义在`boost/signals2/signal.hpp`中。或者，你可以使用头文件`boost/signals2.hpp`，这是一个定义了`Boost.Signals2`中可用所有类和函数的头文件。

`Boost.Signals2`定义了`boost::signals2::signal`和其他类，以及`boost::signals2`命名空间下的所有函数。

### 示例 67.1. 使用`boost::signals2::signal`的“Hello, world!”

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

int main()
{
  signal<void()> s;
  s.connect([]{ std::cout << "Hello, world!\n"; });
  s();
}
```

`boost::signals2::signal`是一个类模板，它期望将作为事件处理器的函数签名作为模板参数。在示例 67.1，“使用`boost::signals2::signal`的‘Hello, world!’”中，只有签名为`void()`的函数才能与信号`s`关联。

Lambda 函数通过`connect()`与信号`s`关联。因为 Lambda 函数符合要求的签名`void()`，所以关联成功建立。每当信号`s`被触发时，该 Lambda 函数就会被调用。

通过像调用普通函数一样调用`s`来触发信号。该函数的签名与作为模板参数传递的签名匹配。括号是空的，因为`void()`不期望任何参数。调用`s`会导致触发，进而执行之前通过`connect()`关联的 Lambda 函数。

示例 67.1，“使用`boost::signals2::signal`的‘Hello, world!’”也可以用`std::function`实现，如示例 67.2，“使用`std::function`的‘Hello, world!’”所示。

```cpp
#include <functional>
#include <iostream>

int main()
{
  std::function<void()> f = []{ std::cout << "Hello, world!\n"; };
  f();
}
```

`Boost.Signals2`提供了更多功能。例如，它可以通过多次调用`connect()`为特定信号关联多个函数。每当信号触发时，函数按照它们与`connect()`关联的顺序执行。

可以通过`connect()`的重载版本显式定义顺序，该版本期望一个`int`类型的值作为额外参数（示例 67.4，“显式的事件处理器”）。

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

int main()
{
  signal<void()> s;
  s.connect(1, []{ std::cout << ", world!\n"; });
  s.connect(0, []{ std::cout << "Hello"; });
  s();
}
```

要从信号中释放关联的函数，请调用`disconnect()`。示例 67.5，“从`boost::signals2::signal`释放事件处理器”仅打印`Hello`，因为在信号触发之前已经释放了与`world()`的关联。

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

void hello() { std::cout << "Hello"; }
void world() { std::cout << ", world!\n"; }

int main()
{
  signal<void()> s;
  s.connect(hello);
  s.connect(world);
  s.disconnect(world);
  s();
}
```

除了`connect()`和`disconnect()`之外，`boost::signals2::signal`还提供了更多成员函数（参见示例 67.6，“`boost::signals2::signal`的其他成员函数”）。`num_slots()`返回关联函数的数量。如果没有关联任何函数，`num_slots()`返回 0。`empty()`告诉事件处理器是否连接。而`disconnect_all_slots()`的作用正如其名：释放所有现有的关联。

### 示例 67.6. `boost::signals2::signal`的其他成员函数

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

int main()
{
  signal<void()> s;
  s.connect([]{ std::cout << "Hello"; });
  s.connect([]{ std::cout << ", world!"; });
  std::cout << s.num_slots() << '\n';
  if (!s.empty())
    s();
  s.disconnect_all_slots();
}
```

在示例 67.7，“处理事件处理器的返回值”中，有两个 lambda 函数关联到信号`s`上。第一个 lambda 函数返回 1，第二个返回 2。

示例 67.7，“处理事件处理器的返回值”向标准输出写入了`2`。这两个返回值都被`s`正确接收了，但除了最后一个之外，所有其他返回值都被忽略了。默认情况下，只有所有关联函数的最后一个返回值会被返回。

### 示例 67.7. 处理事件处理器的返回值

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

int main()
{
  signal<int()> s;
  s.connect([]{ return 1; });
  s.connect([]{ return 2; });
  std::cout << *s() << '\n';
}
```

请注意，`s()`并不直接返回最后一个调用的函数的结果。它返回一个`boost::optional`类型的对象，当解引用时返回数字 2。触发一个未关联任何函数的信号不会产生任何返回值。因此，在这种情况下，`boost::optional`允许 Boost.Signals2 返回一个空对象。`boost::optional`在第 21 章，*Boost.Optional*中引入。

可以自定义信号以便相应地处理各个返回值。要做到，必须将组合器（combiner）作为第二个模板参数传递给`boost::signals2::signal`。

组合器是一个重载了`operator()`的类。该运算符会被带两个迭代器调用，这两个迭代器用于访问与特定信号关联的函数。当迭代器被解引用时，函数会被调用，它们的返回值将在组合器中可用。然后可以使用标准库中的常用算法（如`std::min_element()`）来计算并返回最小值（参见示例 67.8，“使用自定义组合器寻找最小返回值”）。

`boost::signals2::signal`使用`boost::signals2::optional_last_value`作为默认组合器。该组合器返回`boost::optional`类型的对象。用户可以定义一个返回值为任何类型的组合器。例如，示例 67.8，“使用自定义组合器寻找最小返回值”中的组合器`min_element`返回了作为模板参数传递给`min_element`的类型。

无法直接将`std::min_element()`等算法作为模板参数传递给`boost::signals2::signal`。`boost::signals2::signal`要求组合器定义一个名为`result_type`的类型，该类型表示`operator()`返回的值的类型。由于标准算法没有定义此类型，编译器将报告错误。

### 示例 67.8. 使用自定义组合器寻找最小返回值



```cpp
#include <boost/signals2.hpp>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace boost::signals2;

template <typename T>
struct min_element
{
  typedef T result_type;

  template <typename InputIterator>
  T operator()(InputIterator first, InputIterator last) const
  {
    std::vector<T> v(first, last);
    return *std::min_element(v.begin(), v.end());
  }
};

// 注意：示例代码在提示中被截断了；
// 逻辑遵循文本描述。
```

[示例 67.11，“使用 `shared_connection_block` 阻塞连接”](#part0122.html_ex.signals2_11 "Example 67.11. Blocking connections with shared_connection_block") 执行了两次 lambda 函数。信号 `s` 被触发了三次，但 lambda 函数在第二次时没有被调用，因为创建了一个类型为 `boost::signals2::shared_connection_block` 的对象来阻塞调用。一旦该对象超出作用范围，阻塞就会自动移除。也可以通过调用 `unblock()` 显式移除阻塞。由于它在最后一次触发之前被调用，因此 lambda 函数被再次执行。

## 示例 67.12. 多次阻塞连接

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

int main()
{
  signal<void()> s;
  connection c = s.connect([]{ std::cout << "Hello, world!\n"; });
  shared_connection_block b1{c, false};
  {
    shared_connection_block b2{c};
    std::cout << std::boolalpha << b1.blocking() << '\n';
    s();
  }
  s();
}
```

除了 `unblock()` 之外，`boost::signals2::shared_connection_block` 还提供了成员函数 `block()` 和 `blocking()`。前者用于在调用 `unblock()` 后阻塞连接，而后者则允许检查连接当前是否处于阻塞状态。

请注意，`boost::signals2::shared_connection_block` 带有“shared”（共享）一词是有原因：多个类型为 `boost::signals2::shared_connection_block` 的对象可以使用同一个连接进行初始化。

[示例 67.12，“多次阻塞连接”](#part0122.html_ex.signals2_12 "Example 67.12. Blocking a connection multiple times") 访问了两次 `s`，但 lambda 函数仅在第二次时被调用。程序仅向标准输出流写入了一次 `Hello, world!`。

因为将 `false` 作为第二个参数传递给构造函数，第一个类型为 `boost::signals2::shared_connection_block` 的对象没有阻塞信号 `s` 的连接。因此，在对象 `b1` 上调用 `blocking()` 返回 `false`。

尽管如此，当第一次访问 `s` 时，lambda 函数并没有执行，因为该访问发生在第二个类型为 `boost::signals2::shared_connection_block` 的对象实例化之后。通过不向构造函数传递第二个参数，连接被该对象阻塞了。当第二次访问 `s` 时，lambda 函数被执行了，因为一旦 `b2` 超出作用范围，阻塞就被自动移除了。

## 示例 67.13. 成员函数作为事件处理器

```cpp
#include <boost/signals2.hpp>
#include <memory>
#include <functional>
#include <iostream>

using namespace boost::signals2;

struct world
{
  void hello() const
  {
    std::cout << "Hello, world!\n";
  }
};

int main()
{
  signal<void()> s;
  {
    std::unique_ptr<world> w(new world());
    s.connect(std::bind(&world::hello, w.get()));
  }
  std::cout << s.num_slots() << '\n';
  s();
}
```

一旦关联信号的成员函数的对象被销毁，Boost.Signals2 可以释放连接。

[示例 67.13，“成员函数作为事件处理器”](#part0122.html_ex.signals2_13 "Example 67.13. Member functions as event handlers") 借助 `std::bind()` 将对象的成员函数与信号关联。该对象在信号触发之前就被销毁了，这是一个问题，因为传递给 `std::bind()` 的只是一个地址，而不是类型为 `world` 的对象。当调用 `s()` 时，所引用的对象已不存在了。

可以修改程序，使得连接在对象销毁后自动释放。示例 67.14，“自动释放关联成员函数” 就实现了这一点。

## 示例 67.14. 自动释放关联成员函数

```cpp
#include <boost/signals2.hpp>
#include <boost/shared_ptr.hpp>
#include <iostream>

using namespace boost::signals2;

struct world
{
  void hello() const
  {
    std::cout << "Hello, world!\n";
  }
};

int main()
{
  signal<void()> s;
  {
    boost::shared_ptr<world> w(new world());
    s.connect(signal<void()>::slot_type(&world::hello, w.get()).track(w));
  }
  std::cout << s.num_slots() << '\n';
  s();
}
```

现在 `num_slots()` 返回 `0`。示例 67.14，“自动释放关联成员函数” 不会在信号触发时尝试在一个已不存在的对象上调用成员函数。改变是将类型 `world` 的对象绑定到类型为 `boost::shared_ptr` 的智能指针，并将其传递给 `track()`。该成员函数是在传递给 `connect()` 的槽上调用的，用于请求跟踪对象。

## 示例 67.15. 在事件处理器中创建新连接

```cpp
#include <boost/signals2.hpp>
#include <iostream>

boost::signals2::signal<void()> s;

void connect()
{
  s.connect([]{ std::cout << "Hello, world!\n"; });
}

int main()
{
  s.connect(connect);
  s();
}
```

示例 67.15，“在事件处理器中创建新连接” 在 `connect()` 函数内部访问 `s` 以将 lambda 函数与信号关联。由于 `connect()` 是信号触发时被调用的，问题是 lambda 函数是否也会被调用。

程序没有输出任何内容，这意味着 lambda 函数从未被调用。虽然 Boost.Signals2 支持在信号触发时关联函数，但新的关联只会在信号再次触发时才使用。

## 示例 67.16. 在事件处理器中释放连接

```cpp
#include <boost/signals2.hpp>
#include <iostream>

boost::signals2::signal<void()> s;

void hello()
{
  std::cout << "Hello, world!\n";
}

void disconnect()
{
  s.disconnect(hello);
}

int main()
{
  s.connect(disconnect);
  s.connect(hello);
  s();
}
```

示例 67.16，“在事件处理器中释放连接” 并没有创建一个新的关联，而是释放了一个现有的关联。与示例 67.15，“在事件处理器中创建新连接”一样，此示例没有向标准输出流写入任何内容。

这种行为可以非常简单地解释。想象一下，每当信号触发时，都会创建一个槽（slots）的临时副本。新创建的关联不会被添加到临时副本中，因此只能在下一次信号触发时才被调用。另一方面，释放的关联仍然是临时副本的一部分，但组合器（combiner）会在引用时进行检查，以避免对已经销毁的对象调用成员函数。

## 多线程

`Boost.Signals2` 提供的几乎所有类都是线程安全的，可以在多线程应用程序中使用。例如，类型为 `boost::signals2::signal` 和 `boost::signals2::connection` 的对象可以从不同的线程访问。

相反，`boost::signals2::shared_connection_block` 不是线程安全的。这一限制并不重要，因为可以在不同的线程中创建多个类型为 `boost::signals2::shared_connection_block` 的对象，并可以使用同一个连接对象。

### 示例 67.17. `boost::signals2::signal` 是线程安全的

```cpp
#include <boost/signals2.hpp>
#include <thread>
#include <mutex>
#include <iostream>

boost::signals2::signal<void(int)> s;
std::mutex m;

void loop()
{
  for (int i = 0; i < 100; ++i)
    s(i);
}

int main()
{
  s.connect([](int i){
    std::lock_guard<std::mutex> lock{m};
    std::cout << i << '\n';
  });
  std::thread t1{loop};
  std::thread t2{loop};
  t1.join();
  t2.join();
}
```

示例 67.17，“`boost::signals2::signal` 是线程安全的” 创建了两个执行 `loop()` 函数的线程，该函数访问 `s` 百次以调用关联的 lambda 函数。Boost.Signals2 显式支持从不同线程并发访问类型为 `boost::signals2::signal` 的对象。

示例 67.17，“`boost::signals2::signal` 是线程安全的” 显示了从 0 到 99 的数字。由于 `i` 在两个线程中递增并在 lambda 函数中写入标准输出流，数字不仅会显示两次，还会发生重叠。然而，由于 `boost::signals2::signal` 可以从不同的线程访问，程序不会崩溃。

然而，示例 67.17，“`boost::signals2::signal` 是线程安全的” 仍然需要同步。因为两个线程访问 `s`，关联的 lambda 函数在两个线程中并行运行。为了避免两个线程在写入标准输出时相互中断，使用一个互斥锁（mutex）来同步对 `std::cout` 的访问。

对于单线程应用程序，可以在 Boost.Signals2 中禁用多线程支持。

### 示例 67.18. `boost::signals2::signal` 无线程安全

```cpp
#include <boost/signals2.hpp>
#include <iostream>

using namespace boost::signals2;

signal<void()> s;

int main()
{
  typedef keywords::mutex_type<dummy_mutex> dummy_mutex;
  signal_type<void(), dummy_mutex>::type s;
  s.connect([]{ std::cout << "Hello, world!\n"; });
  s();
}
```

在 `boost::signals2::signal` 支持的许多模板参数中，最后一个定义了用于同步的互斥锁类型。幸运的是，Boost.Signals2 提供了一种比传递完整参数列表更简单的方法来禁用同步。

`boost::signals2::keywords` 命名空间包含了许多类，使得通过名称传递模板参数成为可能。`boost::signals2::keywords::mutex_type` 可将互斥锁类型作为第二个模板参数传递给 `boost::signals2::signal_type`。请注意在这种情况下必须使用 `boost::signals2::signal_type` 而不是 `boost::signals2::signal`。用于定义信号 `s` 的等于 `boost::signals2::signal` 的类型可以通过 `boost::signals2::signal_type::type` 获取。

Boost.Signals2 提供了一个名为 `boost::signals2::dummy_mutex` 的空互斥锁实现。如果使用该类定义信号，它将不再支持多线程（参见示例 67.18，“`boost::signals2::signal` 无线程安全”）。

示例 68.1，“带有 eUML 的简单状态机” 使用 eUML 前端来描述灯的状态机。`Boost.MetaStateMachine` 并没有一个主头文件。因此，必须逐个包含所需的头文件。`boost/msm/front/euml/euml.hpp` 和 `boost/msm/front/euml/state_grammar.hpp` 提供了对 eUML 宏的访问支持。`boost/msm/back/state_machine.hpp` 则用于将前端的状态机链接到后端的状态机。虽然前端提供了定义状态机的各种可能性，但状态机的实际实现是在后端找到的。由于 `Boost.MetaStateMachine` 只包含一个后端，因此你不需要选择实现方式。

所有来自 `Boost.MetaStateMachine` 的定义都位于 `boost::msm` 命名空间中。遗憾的是，许多 eUML 宏并没有显式地引用该命名空间中的类。它们使用了 `msm` 命名空间或者完全没有使用命名空间。这就是为什么示例 68.1，“带有 eUML 的简单状态机” 为 `boost::msm` 命名空间创建了一个别名，并通过 `using` 指令使 `boost::msm::front::euml` 中的定义可用。否则，eUML 宏将导致编译错误。

要使用灯的状态机，首先定义关闭（off）和开启（on）的状态。状态通过 `BOOST_MSM_EUML_STATE` 宏定义，该宏期望状态名称作为第二个参数。第一个参数描述该状态。你稍后会看到这些描述看起来是什么样的。在示例 68.1，“带有 eUML 的简单状态机” 中定义的两个状态称为 `Off` 和 `On`。

为了在状态之间切换，需要事件（events）。事件通过 `BOOST_MSM_EUML_EVENT` 宏定义，该宏期望事件名称作为其唯一参数。示例 68.1，“带有 eUML 的简单状态机” 定义了一个名为 `press` 的事件，它代表按下灯开关的动作。由于同一个事件可以切换灯的开启和关闭，因此只定义了一个事件。

当定义了所需的状态和事件后，使用 `BOOST_MSM_EUML_TRANSITION_TABLE` 宏来创建一个转换表（transition table）。该表定义了状态之间的有效转换，以及哪些事件触发了哪些状态转换。

`BOOST_MSM_EUML_TRANSITION_TABLE` 期望两个参数。第一个参数定义转换表，第二个参数是转换表的名称。第一个参数的语法设计旨在便于识别状态和事件之间的关系。例如，`Off + press == On` 意味着处于 `Off` 状态的机器通过 `press` 事件切换到 `On` 状态。转换表直观且自解释其懂的语法是 eUML 前端的优势之一。

在创建转换表后，使用 `BOOST_MSM_EUML_DECLARE_STATE_MACHINE` 宏定义状态机。第二个参数再次变得简单：它设置了状态机的名称。示例 68.1，“带有 eUML 的简单状态机” 中的状态机命名为 `light_state_machine`。

`BOOST_MSM_EUML_DECLARE_STATE_MACHINE` 的第一个参数是一个 `tuple`。第一个值是转换表的名称。第二个值是一个使用 `init_` 的表达式，它是 `Boost.MetaStateMachine` 提供的一个属性。你将学习更多关于属性的知识。表达式 `init_ << Off` 用于将状态机的初始状态设置为 `Off`。



通过`BOOST_MSM_EUML_DECLARE_STATE_MACHINE`定义的状态机`light_state_machine`是一个`class`。你使用这个类从后端实例化一个状态机。在示例 68.1, “带有 eUML 的简单状态机” 中，这是通过将`light_state_machine`作为参数传递给类`boost::msm::back::state_machine`实现的。这了一个名为`light`的状态机。

状态机提供成员函数`process_event()`来处理事件。如果你将一个事件传递给`process_event()`，状态机将根据其转换表改变状态。为了方便查看示例 68.1, “带有 eUML 的简单状态机” 中当多次调用`process_event()`时发生了什么，使用了`current_state()`。

### 示例 68.2. 带有状态、事件和动作的状态机

```cpp
#include <boost/msm/front/euml/euml.hpp>
#include <boost/msm/front/euml/state_grammar.hpp>
#include <boost/msm/back/state_machine.hpp>
#include <iostream>

namespace msm = boost::msm;
using namespace msm::front::euml;

BOOST_MSM_EUML_STATE(Off, {})
BOOST_MSM_EUML_STATE(On, {})

BOOST_MSM_EUML_EVENT(press)

BOOST_MSM_EUML_ACTION(switch_light)
{
  template <class Event, class Fsm>
  void operator()(const Event&, Fsm&, msm::front::euml::state_machine_event_type<Fsm, Off>&)
  {
    std::cout << "Switching on\n";
  }

  template <class Event, class Fsm>
  void operator()(const Event&, Fsm&, msm::front::euml::state_machine_event_type<Fsm, On>&)
  {
    std::cout << "Switching off\n";
  }
};

BOOST_MSM_EUML_TRANSITION_TABLE((
  Off + press / switch_light == On,
  On + press / switch_light == Off
), light_transition_table)

BOOST_MSM_EUML_DECLARE_STATE_MACHINE(
(light_transition_table, init_ << Off),
light_state_machine)

int main()
{
  msm::back::state_machine<light_state_machine> light;
  light.process_event(press());
  light.process_event(press());
}
```

示例 68.2, “带有状态、事件和动作的状态机” 为灯的状态机扩展了动作。动作通过事件触发状态转换来执行。由于动作是可选的，可以定义不带动作的状态机。

（注：上述代码块为根据逻辑补全的完整示例，原文中代码部分为描述性）

当`process_event()`被多次调用时，使用`current_state()`可以更容易地看到发生了什么。它会输出 0, 1, 0。

动作`switch_light`通过`BOOST_MSM_EUML_ACTION`定义，在按下灯开关时执行。转移表已据此进行了相应的修改。第一个转换现在变为`Off + press / switch_light == On`。你在事件之后通过斜杠 `/` 传递动作。此转换意味着，如果当前状态为`Off`且发生了事件`press`，则会调用`switch_light`的运算符`operator()`。在执行动作后，新状态变为`On`。

示例 68.2, “带有状态、事件和动作的状态机” 向标准输出输了`Switching on`，然后是`Switching off`。

示例 68.3, “带有状态、事件、守卫和动作的状态机” 在转移表使用了守卫（guard）。第一个转换的定义为`Off + press [!is_broken] / switch_light == On`。在括号中传递`is_broken`意味着在调用动作`switch_light`之前，状态机会会检查转换是否可以发生。这被称为守卫。守卫必须返回一个`bool`类型的结果。

像`is_broken`这样的守卫是以与动作相同的方式通过`BOOST_MSM_EUML_ACTION`定义的。因此，运算符`operator()`必须对相同的四个参数进行重载。`operator()`必须有一个`bool`类型的返回值才能作为守卫使用。

请注意，你可以在括号内的守卫上使用`operator!`等逻辑运算符。

如果你运行该示例，你会发现标准输出中没有任何写入内容。动作`switch_light`没有被执行——灯保持关**状态。守卫`is_broken`返回了`true`。但是，由于使用了运算符`operator!`，括号中的表达式求值为`false`。

你可以使用守卫来检查状态转换是否可以发生。示例 68.3, “带有状态、事件、守卫和动作的状态机” 使用`is_broken`来检查灯是否坏了。虽然从关到开的转换是可能的，且转移表描述了灯，但在本示例中，灯无法开启。尽管调用了两次`process_event()`，`light`的状态仍然是`Off`。

### 示例 68.3. 带有状态、事件、守卫和动作的状态机

```cpp
#include <boost/msm/front/euml.hpp>
#include <boost/msm/front/state_grammar.hpp>
#include <boost/msm/back/state_machine.hpp>
#include <iostream>

namespace msm = boost::msm;
using namespace boost::msm::front::euml;

BOOST_MSM_EUML_STATE((), Off)
OST_MSM_EUML_STATE((), On)

BOOST_MSM_EUML_EVENT(press)

BOOST_MSM_EUML_ACTION(is_broken)
{
  template <class Event, class Fsm, class Source, class Target>
  bool operator()(const Event &ev, Fsm &fsm, Source &src, Target &trg) const
  {
    return true;
  }
};

BOOST_MSM_EUML_ACTION(switch_light)
{
  template <class Event, class Fsm, class Source, class Target>
  void operator()(const Event &ev, Fsm &fsm, Source &src, Target &trg) const
  {
    std::cout << "Switching\n";
  }
};

BOOST_MSM_EUML_TRANSITION_TABLE((
  Off + press [!is_broken] / switch_light == On,
  On + press / switch_light == Off
), light_transition_table)

BOOST_MSM_EUML_DECLARE_STATE_MACHINE(
(light_transition_table, init_ << Off),
light_state_machine)

int main()
{
  msm::back::state_machine<light_state_machine> light;
  light.process_event(press);
  light.process_event(press);
}
```

### 示例 68.4. 带有状态、事件、进入动作和退出动作的状态机

```cpp
#include <boost/msm/front/euml.hpp>
#include <boost/msm/front/state_grammar.hpp>
#include <boost/msm/back/state_machine.hpp>
#include <iostream>

namespace msm = boost::msm;
using namespace boost::msm::front::euml;

BOOST_MSM_EUML_ACTION(state_entry)
{
  template <class Event, class Fsm, class State>
  void operator()(const Event &ev, Fsm &fsm, State &state) const
  {
    std::cout << "Entering\n";
  }
};

BOOST_MSM_EUML_ACTION(state_exit)
{
  template <class Event, class Fsm, class State>
  void operator()(const Event &ev, Fsm &fsm, State &state) const
  {
    std::cout << "Exiting\n";
  }
};

BOOST_MSM_EUML_STATE((state_entry, state_exit), Off)
BOOST_MSM_EUML_STATE((state_entry, state_exit), On)

BOOST_MSM_EUML_EVENT(press)

BOOST_MSM_EUML_TRANSITION_TABLE((
  Off + press == On,
  On + press == Off
), light_transition_table)

BOOST_MSM_EUML_DECLARE_STATE_MACHINE(
(light_transition_table, init_ << Off),
light_state_machine)

int main()
{
  msm::back::state_machine<light_state_machine> light;
  light.process_event(press);
  light.process_event(press);
}
```

在定义属性后，必须将其附加到对象上。此示例将属性`switched_on`附加到状态机上。这是通过元组中的第五个值实现的，该值作为第一个参数传递给`BOOST_MSM_EUML_DECLARE_STATE_MACHINE`。通过`attributes_`（一个来自 Boost.MetaStateMachine 的关键字），可以使用创建一个 lambda 表达式函数。要将属性`switched_on`附加到状态机，可以像写入流一样使用`operator<<`将`switched_on`写入`attributes_`。

元组中的第三和第四个值均设置为`no_action`。属性作为元组的第五个值传递。第三和第四个值可以用于定义状态机的进入（entry）和退出（exit）动作。如果没有定义这些动作，请使用`no_action`。

属性附加到状态机后，可以使用`get_attribute()`访问它。在示例 68.5, “状态机中的属性” 中，在该成员函数在进入动作`state_entry`中调用以增加属性的值。由于`state_entry`仅链接到状态`On`，因此只有在灯打开时`switched_on`才会递增。

`switched_on`也可以通过守卫`is_broken`进行访问，该守卫检查属性值是否大于 1。如果是，守卫返回`true`。由于属性使用默认构造函数初始化，且`switched_on`被设置为 0，当灯被打开两次后，`is_broken`将返回`true`。

### 示例 68.5. 状态机中的属性

```cpp
#include <boost/msm/front/euml/euml.hpp>
#include <boost/msm/front/euml/state_grammar.hpp>
#include <boost/msm/back/state_machine.hpp>
#include <iostream>

namespace msm = boost::msm;
using namespace boost::msm::front::euml;

BOOST_MSM_EUML_DECLARE_ATTRIBUTE(int, switched_on)

BOOST_MSM_EUML_ACTION(state_entry)
{
  template <class Event, class Fsm, class State>
  void operator()(const Event &ev, Fsm &fsm, State &state) const
  {
    std::cout << "Switched on\n";
    ++fsm.get_attribute(switched_on);
  }
};
BOOST_MSM_EUML_ACTION(is_broken)
{
  template <class Event, class Fsm, class Source, class Target>
  bool operator()(const Event &ev, Fsm &fsm, Source &src, Target &trg) const
  {
    return fsm.get_attribute(switched_on) > 1;
  }
};

BOOST_MSM_EUML_STATE((), Off)
BOOST_MSM_EUML_STATE((state_entry), On)
BOOST_MSM_EUML_EVENT(press)

BOOST_MSM_EUML_TRANSITION_TABLE((
  Off + press [!is_broken] == On,
  On + press == Off
), light_transition_table)

BOOST_MSM_EUML_DECLARE_STATE_MACHINE(
(light_transition_table, init_ << Off, no_action, no_action,
attributes_ << switched_on), light_state_machine)

int main()
{
  msm::back::state_machine<light_state_machine> light;
  light.process_event(press);
  light.process_event(press);
  light.process_event(press);
  light.process_event(press);
  light.process_event(press);
}
```

在示例 68.5, “状态机中的属性” 中，事件`press`发生了五次。灯被开关了两次，然后再次打开。在前两次灯打开时，会显示`Switched on`。然而，在第三次灯打开时没有输出。这是因为在灯打开两次后，`is_broken`返回了`true`，因此没有从`Off`到`On`的状态转换。这意味着状态`On`的进入动作没有执行，且示例没有写入标准输出。

示例 68.6, “在转换表上访问属性” 与示例 68.5, “状态机中的属性” 做了相同的事情：在灯被打开两次后，灯坏了且无法再次打开。虽然上一个示例在动作中访问了属性`switched_on`，但此示例在转换表中使用了属性。

Boost.MetaStateMachine 提供了函数`fsm_()`来访问状态机中的属性。这样就可以定义一个守卫来检查`switched_on`是否小于 2。请注意，守卫中的小于比较是通过`Int_<2>()`完成的。数字 2 必须作为模板参数传递给`Int_`以创建一个实例。`BOOST_MSM_EUML_FUNCTION`宏用于创建一个动作。第一个参数是`BOOST_MSM_EUML_FUNCTION`所需的函数类型。第二个参数是动作的名称。第三和第四五个参数是返回值和参数。

### 其他库

*   Boost.Utility 收集了所有不适合放在 Boost 库其他地方的内容。

*   Boost.Assign 提供了辅助函数，可以更轻松地执行向容器中添加多个值的操作，而无需反复调用`push_back()`。

*   `Boost.Swap`提供了`std::swap()`的变体，并针对 Boost 库进行了优化。

*   `Boost.Operators`允许根据其他运算符轻松地定义运算符。

# 69. Boost.Utility

[Boost.Utility](http://www.boost.org/libs/utility) 库是各种杂用类和函数的集合，这些类和函数太小，不足以作为独立的库来维护。虽然这些工具类体较小且可以快速学习，但它们之间完全没有关联。与其他章节中的示例不同，这里的代码示例并不是相互构建的，因为它们是独立的工具。



虽然大多数工具定义在`boost/utility.hpp`中，但某些工具有自己的头文件。以下示例包含了为介绍的工具引入相应的头文件。

示例 69.1, “使用`boost::checked_delete()`”将函数`boost::checked_delete()`作为参数传递给成员函数`pop_back_and_dispose()`，该成员函数由 Boost.Intrusive 中的`boost::intrusive::list`类提供。`boost::intrusive::list`和`pop_back_and_dispose()`在第 18 章，*Boost.Intrusive*中引入，而`boost::checked_delete()`由 Boost.Utility 提供并定义在`boost/checked_delete.hpp`中。

`boost::checked_delete()`唯一的参数是指向将由`delete`删除的对象的指针。由于`pop_back_and_dispose()`期望一个接收指针以破坏对应对象的函数，因此传递`boost::checked_delete()`是合理的——这样你就不需要定义一个类似的函数了。

与`delete`不同，`boost::checked_delete()`确保被销毁的对象的类型是完整的。`delete`会接受指向不完整类型对象的指针。虽然这涉及 C++ 标准中一个通常可以忽略的细节，但你应该注意`boost::checked_delete()`与调用`delete`并不完全相同，因为它对参数有更高的要求。

### 示例 69.1. 使用`boost::checked_delete()`

```cpp
#include <boost/checked_delete.hpp>
#include <boost/intrusive/list.hpp>
#include <string>
#include <utility>
#include <iostream>

struct animal : public boost::intrusive::list_base_hook<>
{
  std::string name_;
  int legs_;

  animal(std::string name, int legs) : name_{std::move(name)},
    legs_{legs} {}
};

int main()
{
  animal *a = new animal{"cat", 4};

  typedef boost::intrusive::list<animal> animal_list;
  animal_list al;

  al.push_back(*a);

  al.pop_back_and_dispose(boost::checked_delete<animal>);
  std::cout << al.size() << '\n';
}
```

Boost.Utility 还提供了`boost::checked_array_delete()`，它可以用于销毁数组。它调用`delete[]`而不是`delete`。

此外，还有两个类`boost::checked_deleter`和`boost::checked_array_deleter`，用于创建行为类似于`boost::checked_delete()`和`boost::checked_array_delete()`的函数对象。

### 示例 69.2. 使用`BOOST_CURRENT_FUNCTION`

```cpp
#include <boost/current_function.hpp>
#include <iostream>

int main()
{
  const char *funcname = BOOST_CURRENT_FUNCTION;
  std::cout << funcname << '\n';
}
```

示例 69.2, “使用`BOOST_CURRENT_FUNCTION`”使用定义在`boost/current_function.hpp`中的宏`BOOST_CURRENT_FUNCTION`来以字符串形式返回周围函数的名称。

`BOOST_CURRENT_FUNCTION`提供了一种平台无关的方法来获取函数名。从 C++11 开始，你可以使用标准宏`__func__`同样的事情。在 C++11 之前，Visual C++ 和 GCC 等编译器支持作为扩展的宏`__FUNCTION__`。`BOOST_CURRENT_FUNCTION`使用编译器支持的任何宏。

如果使用 Visual C++ 2013 编译，示例 69.2, “使用`BOOST_CURRENT_FUNCTION`”显示`int __cdecl main(void)`。

### 示例 69.3. 使用`boost::prior()`和`boost::next()`

```cpp
#include <boost/next_prior.hpp>
#include <array>
#include <algorithm>
#include <iostream>

int main()
{
  std::array<char, 4> a;
  // ... 为了简洁省略了逻辑
}
```

Boost.Utility 提供了两个函数`boost::prior()`和`boost::next()`，它们返回一个新的迭代器。在示例 69.3, “使用`boost::prior()`和`boost::next()`”中，`it`指向`b`。

与`std::advance()`不同，这两个函数接受第二个参数，表示向前向后移动的步数。步数始终为正，即使对于`boost::prior()`也是如此。

这两个函数在 C++11 中加入了标准库，称为`std::prev()`和`std::next()`。它们定义在头文件`boost/next_prior.hpp`中。

### 示例 69.4. 使用`boost::noncopyable`

```cpp
#include <boost/noncopyable.hpp>
#include <string>
#include <utility>
#include <iostream>

struct animal : boost::noncopyable
{
  std::string name;
  int legs;

  animal(std::string n, int l) : name{std::move(n)},
    legs{l} {}
};

void print(const animal &a)
{
  std::cout << a.name << '\n';
  std::cout << a.legs << '\n';
}

int main()
{
  animal a{"cat", 4};
  print(a);
}
```

Boost.Utility 提供了类`boost::noncopyable`，定义在`boost/noncopyable.hpp`中。该类使得无法拷贝（以及移动）对象。通过将拷贝构造函数和赋值运算符定义为私有成员函数来实现相同的效果，或者从 C++11 开始通过`delete`移除拷贝构造函数和赋值运算符。然而，继承`boost::noncopyable`显式声明了类应该是不可拷贝的。

某些开发者倾向于使用`boost::noncopyable`，而另一些人倾向于用`delete`显式移除函数。你可以在 [Stack Overflow](http://stackoverflow.com/questions/7823990/what-are-the-advantages-of-boostnoncopyable) 等地方找到这两种方法的理由。

示例 69.4, “使用`boost::noncopyable()`”可以编译并运行。但是如果将`print()`函数的签名修改为按值获取`animal`类型对象而不是引用，则结果代码将无法编译。

### 示例 69.5. 使用`boost::addressof()`

```cpp
#include <boost/utility/addressof.hpp>
#include <string>
#include <iostream>

struct animal
{
  std::string name;
  int legs;

  int operator&() const { return legs; }
};

int main()
{
  animal a{"cat", 4};
  std::cout << &a << '\n';
  std::cout << boost::addressof(a) << '\n';
}
```

为了获取特定对象的地址，即使`operator&`已经被重载，Boost.Utility 也提供了`boost::addressof()`函数，该函数定义在`boost/utility/addressof.hpp`中（参见示例 69.5, “使用`boost::addressof()`”）。在 C++11 中，该函数成为标准库的一部分，并在头文件`memory`中作为`std::addressof()`可用。

### 示例 69.6. 使用`BOOST_BINARY`

```cpp
#include <boost/utility/binary.hpp>
#include <iostream>

int main()
{
  int i = BOOST_BINARY(1001 0001);
  std::cout << i << '\n';

  short s = BOOST_BINARY(1000 0000 0000 0000);
  std::cout << s << '\n';
}
```

宏`BOOST_BINARY`允许你以二进制形式创建数字。标准 C++ 只支持十六进制和八进制形式，使用前缀`0x`和`0`。C++11 引入了用户自定义字面量，允许你定义自定义后缀，但在 C++11 中仍然没有标准方法以二进制形式使用数字。

示例 69.6, “使用`BOOST_BINARY`”显示了`145`和`-32768`。存储在`s`中的位序列表示一个负数，因为 16 位类型`short`使用第 16 位——即`short`中的最高有效位——作为符号位。

`BOOST_BINARY`仅仅提供了另一种编写数字的选项。因为在 C++ 中，数字的默认类型是`int`，所以`BOOST_BINARY`也使用了`int`。要定义`long`类型的数字，请使用宏`BOOST_BINARY_L`，它会生成等同于带有字母 L 后的数字。

Boost.Utility 包含了额外的宏，如`BOOST_BINARY_U`，它可以初始化一个没有符号位的变量。所有这些宏都定义在头文件`boost/utility/binary.hpp`中。

### 示例 69.7. 使用`boost::string_ref`

```cpp
#include <boost/utility/string_ref.hpp>
#include <iostream>

boost::string_ref start_at_boost(boost::string_ref s)
{
  auto idx = s.find("Boost");
  return (idx != boost::string_ref::npos) ? s.substr(idx) : "";
}

int main()
{
  boost::string_ref s = "The Boost C++ Libraries";
  std::cout << start_at_boost(s) << '\n';
}
```

示例 69.7, “使用`boost::string_ref`”引入了`boost::string_ref`类，它是对字符串的仅只读引用。在某种程度上，该引用可以与`const std::string&`比较。然而，`const std::string&`需要`std::string`类型的对象。`boost::string_ref`可以在没有`std::string`的情况下使用。`boost::string_ref`的优势在于，它与`std::string`不同，不需要分配内存。示例 69.7, “使用`boost::string_ref`”在字符串中查找单词“Boost”。如果找到，则显示以该单词开头的字符串。如果没有找到“Boost”，则显示空字符串。`main()`中字符串`s`的类型不是`std::string`，而是`boost::string_ref`。因此，没有使用`new`分配内存，也没有创建拷贝。`s`直接指向字面量“The Boost C++ Libraries”。

`start_at_boost()`返回值的类型是`boost::string_ref`而不是`std::string`。该函数没有返回新字符串，而是返回一个引用。该引用是对参数的子字符串或空字符串。`start_at_boost()`要求只要在使用`boost::string_ref`类型的情况下，原始字符串保持有效。如果这一点可以保证（如示例 69.7, “使用`boost::string_ref`”所示），就可以避免内存分配。

还有其他可用工具，但它们超出了本书的范围，因为它们主要供 Boost 开发者或模板元编程使用。Boost.Utility 的文档提供了这些工具的全面概述，如果你感兴趣，可以作为一个起点。

# 70. Boost.Assign

[Boost.Assign](http://www.boost.org/libs/assign) 提供了初始化容器或向容器添加元素的辅助函数。如果容器需要存储许多元素，这些函数特别有用。得益于 Boost.Assign 提供的函数，你不需要反复调用`push_back()`等成员函数向容器逐个插入元素。

如果你使用的开发环境支持 C++11，可以从初始化列表中受益。你可以向构造函数传递任意数量的值来初始化容器。得益于初始化列表，在 C++11 中你不需要依赖 Boost.Assign。然而，Boost.Assign 提供了向现有容器添加多个值的辅助函数。这些辅助函数在 C++11 开发环境中非常有用。

示例 70.1, “初始化容器”引入了一些可以初始化容器的函数。要使用 Boost.Assign 定义的函数，请包含头文件`boost/assign.hpp`。

Boost.Assign 提供了三个初始化容器的函数。最重要的以及你通常使用的是`boost::assign::list_of()`。你使用`boost::assign::map_of()`和`boost::assign::tuple_of()`来用`map`初始化容器。你不必使用`boost::assign::map_of()`或`boost::assign::tuple_of()`。然而，如果你使用`map`或元组，你必须向`boost::assign::list_of()`传递一个模板参数，告诉函数如何存储元素。这个模板参数对于`boost::assign::map_of()`和`boost::assign::tuple_of()`是不是需要的。

### 示例 70.1. 初始化容器

```cpp
#include <boost/assign.hpp>
#include <boost/tuple/tuple.hpp>
#include <vector>
#include <stack>
#include <map>
#include <string>
#include <utility>

using namespace boost::assign;

int main()
{
  std::vector<int> v = list_of(1)(2)(3);

  std::stack<int> s = list_of(1)(2)(3).to_adapter();

  std::vector<std::pair<std::string, int>> v2 =
    list_of<std::pair<std::string, int>>("a", 1)("b", 2)("c", 3);

  std::map<std::string, int> m =
    map_of("a", 1)("b", 2)("c", 3);

  std::vector<boost::tuple<std::string, int, double>> v3 =
    tuple_of("a", 1, 9.9)("b", 2, 8.8)("c", 3, 7.7);
}
```

所有三个函数都返回一个代理对象。该对象重载了运算符`operator()`。你可以多次调用该运算符将值保存到容器中。尽管你访问的是另一个对象而不是容器，但容器通过这个代理发生了变化。

如果你想初始化像`std::stack`这样的适配器，请在代理上调用成员函数`to_adapter()`。代理随后调用所有适配器提供的`push()`成员函数。

`boost::assign::tuple_of()`仅支持`boost::tuple`元组。你不能使用该函数用标准库的元组初始化容器。

示例 70.2, “向容器添加值”说明了如何向现有容器添加值。



```cpp
#include <boost/assign.hpp>
#include <vector>
#include <deque>
#include <set>
#include <queue>

int main()
{
  std::vector<int> v;
  boost::assign::push_back(v)(1)(2)(3);

  std::deque<int> d;
  boost::assign::push_front(d)(1)(2)(3);

  std::set<int> s;
  boost::assign::insert(s)(1)(2)(3);

  std::queue<int> q;
  boost::assign::push(q)(1)(2)(3);
}
```

这四个函数 `boost::assign::push_back()`、`boost::assign::push_front()`、`boost::assign::insert()` 和 `boost::assign::push()` 以这种方式被调用，是因为返回的代理对象会调用容器上同名的成员函数。示例 70.2, “向容器添加值” 通过三次调用 `push_back()` 将三个数字 1、2 和 3 添加到向量 `v` 中。

Boost.Assign 提供了额外的辅助函数，供你向容器中添加值，包括 `boost::assign::add_edge()`，你可以用它来获取 Boost.Graph 中图的代理。

# 71. Boost.Swap

如果你使用了许多 Boost 库并且使用 `std::swap()` 来交换数据，可以考虑使用 `boost::swap()` 作为替代方案。`boost::swap()` 由 [Boost.Swap](http://www.boost.org/libs/core/swap.html) 提供，并在 `boost/swap.hpp` 中定义。

## 示例 71.1. 使用 `boost::swap()`

```cpp
#include <boost/swap.hpp>
#include <boost/array.hpp>
#include <iostream>

int main()
{
  char c1 = 'a';
  char c2 = 'b';

  boost::swap(c1, c2);

  std::cout << c1 << c2 << '\n';

  std::array<int, 1> a1{{1}};
  std::array<int, 1> a2{{2}};

  boost::swap(a1, a2);

  std::cout << a1[0] << a2[0] << '\n';
}
```

`boost::swap()` 的作用与 `std::swap()` 无异。然而，由于许多 Boost 库提供了定义在 `boost` 命名空间中的数据交换特化，`boost::swap()` 可以利用这些特性。在示例 71.1, “使用 `boost::swap()`” 中，`boost::swap()` 通过 `std::swap()` 来交换两个 `char` 变量的值，并使用来自 Boost.Array 的优化函数 `boost::swap()` 来交换数组中的数据。

示例 71.1, “使用 `boost::swap()`” 向标准输出流写入了 `ba` 和 `21`。

# 72. Boost.Operators

[Boost.Operators](http://www.boost.org/libs/utility/operators.htm) 提供了许多类来自动重载运算符。在示例 72.1, “带有 `boost::less_than_comparable` 的大于运算符” 中，即使没有声明，大于运算符也会被自动添加，因为大于运算符可以使用已经定义的小于运算符来实现。

## 示例 72.1. 使用 `boost::less_than_comparable` 的大于运算符

```cpp
#include <boost/operators.hpp>
#include <string>
#include <utility>
#include <iostream>

struct animal : public boost::less_than_comparable<animal>
{
  std::string name;
  int legs;

  animal(std::string n, int l) : name{std::move(n)}, legs{l} {}

  bool operator<(const animal &a) const { return legs < a.legs; }
};

int main()
{
  animal a1{"cat", 4};
  animal a2{"spider", 8};

  std::cout << std::boolalpha << (a2 > a1) << '\n';
}
```

要自动添加运算符，请从 `boost/operators.hpp` 中 Boost.Operators 定义的类派生。如果一个类派生自 `boost::less_than_comparable`，那么 `operator>`、`operator<=` 和 `operator>=` 将被自动定义。

由于许多运算符可以用其他运算符表示，因此自动重载是可能的。例如，`boost::less_than_comparable` 将大于运算符实现为小于运算符的反向；如果一个对象不小于另一个对象，那么假设它们不相等。

如果两个对象可能相等，请使用 `boost::partially_ordered` 作为基类。通过定义 `operator==`，`boost::partially_ordered` 可以判断小于意味着大于还是等于。除了 `boost::less_than_comparable` 和 `boost::partially_ordered` 之外，还提供了允许重载通常由迭代器、指针或数组提供的运算符的类。由于自动重载只有在定义了其他运算符后才是可能的，具体的运算符取决于情况。请查阅文档获取更多信息。

# Index

## Symbols

- `_`, Boost.Xpressive
- `_1`, Boost.Bind
- `_1`, Boost.Lambda
- `_2`, Boost.Lambda
- `_3`, Boost.Lambda
- `_data`, Boost.Bimap
- `_key`, Boost.Bimap
- `_s`, Boost.Xpressive
- `_w`, Boost.Xpressive

## A

- `abort`, `mpi::environment`, Simple Data Exchange
- `absolute`, `filesystem`, Files and Directories
- `acceptor`, `asio::ip::tcp`, Network programming
- `access`, `serialization`, Archive
- `accumulate`, Boost.Range, Algorithms
- `accumulator`, Boost.Accumulators
- `accumulators::accumulator_set`, Boost.Accumulators
- `accumulators::count`, Boost.Accumulators
- `accumulators::features`, Boost.Accumulators
- `accumulators::tag::count`, Boost.Accumulators
- `accumulators::tag::mean`, Boost.Accumulators
- `accumulators::tag::variance`, Boost.Accumulators
- `accumulator_set`, `accumulators`, Boost.Accumulators
- `action`, Boost.Spirit, Actions
- `adaptor`, Boost.Range, Adaptors
- `adaptors::filter`, Adaptors
- `adaptors::keys`, Adaptors
- `adaptors::tokenize`, Adaptors
- `adaptors::values`, Adaptors
- `add`, `program_options::options_description`, Boost.ProgramOptions
- `add`, `program_options::positional_options_description`, Boost.ProgramOptions
- `addressof`, Boost.Utility, Boost.Utility
- `add_block`, `simple_segregated_storage`, Boost.Pool
- `add_child`, `property_tree::ptree`, Boost.PropertyTree
- `add_const`, Boost.TypeTraits, Boost.TypeTraits
- `add_edge`, `assign`, Boost.Assign
- `add_edge`, Boost.Graph, 顶点与边
- `add_global_attribute`, `log::core`, Boost.Log
- `add_options`, `program_options::options_description`, Boost.ProgramOptions
- `add_rvalue_reference`, Boost.TypeTraits, Boost.TypeTraits
- `add_sink`, `log::core`, Boost.Log
- `add_stream`, `log::sinks::text_ostream_backend`, Boost.Log
- `add_vertex`, Boost.Graph, 顶点与边
- `adjacency_list`, Boost.Graph, 顶点与边
- `adjacency_list::clear`, 顶点与边
- `adjacency_list::vertex_descriptor`, 顶点与边
- `adjacency_list::vertex_iterator`, 顶点与边
- `adjacency_matrix`, Boost.Graph, 容器
- `adjacent_vertices`, Boost.Graph, 顶点与边
- `advance`, `fusion`, Boost.Fusion
- `algorithm::all_of`, Boost.Algorithm
- `algorithm::all_of_equal`, Boost.Algorithm
- `algorithm::any_of`, Boost.Algorithm
- `algorithm::any_of_equal`, Boost.Algorithm
- `algorithm::contains`, Boost.StringAlgorithms
- `algorithm::copy_n`, Boost.Algorithm
- `algorithm::copy_until`, Boost.Algorithm
- `algorithm::copy_while`, Boost.Algorithm
- `algorithm::ends_with`, Boost.StringAlgorithms
- `algorithm::equal`, Boost.Algorithm
- `algorithm::erase_all_copy`, Boost.StringAlgorithms
- `algorithm::erase_first_copy`, Boost.StringAlgorithms
- `algorithm::erase_head_copy`, Boost.StringAlgorithms
- `algorithm::erase_tail_copy`, Boost.StringAlgorithms
- `algorithm::find_first`, Boost.StringAlgorithms
- `algorithm::find_head`, Boost.StringAlgorithms
- `algorithm::find_if_not`, Boost.Algorithm
- `algorithm::find_last`, Boost.StringAlgorithms
- `algorithm::find_nth`, Boost.StringAlgorithms
- `algorithm::find_regex`, Boost.StringAlgorithms
- `algorithm::find_tail`, Boost.StringAlgorithms
- `algorithm::hex`, Boost.Algorithm
- `algorithm::ierase_all_copy`, Boost.StringAlgorithms
- `algorithm::iota`, Boost.Algorithm
- `algorithm::iota_n`, Boost.Algorithm
- `algorithm::is_any_of`, Boost.StringAlgorithms
- `algorithm::is_decreasing`, Boost.Algorithm
- `algorithm::is_digit`, Boost.StringAlgorithms
- `algorithm::is_increasing`, Boost.Algorithm
- `algorithm::is_lower`, Boost.StringAlgorithms
- `algorithm::is_partitioned`, Boost.Algorithm
- `algorithm::is_permutation`, Boost.Algorithm
- `algorithm::is_space`, Boost.StringAlgorithms
- `algorithm::is_upper`, Boost.StringAlgorithms
- `algorithm::join`, Boost.StringAlgorithms
- `algorithm::lexicographical_compare`, Boost.StringAlgorithms
- `algorithm::mismatch`, Boost.Algorithm
- `algorithm::none_of`, Boost.Algorithm
- `algorithm::none_of_equal`, Boost.Algorithm
- `algorithm::one_of`, Boost.Algorithm
- `algorithm::one_of_equal`, Boost.Algorithm
- `algorithm::replace_all_copy`, Boost.StringAlgorithms
- `algorithm::replace_first_copy`, Boost.StringAlgorithms
- `algorithm::replace_head_copy`, Boost.StringAlgorithms
- `algorithm::replace_last_copy`, Boost.StringAlgorithms
- `algorithm::replace_nth`, Boost.StringAlgorithms
- `algorithm::replace_tail`, Boost.StringAlgorithms
- `algorithm::split`, Boost.StringAlgorithms
- `algorithm::starts_with`, Boost.StringAlgorithms
- `algorithm::to_lower`, Boost.StringAlgorithms
- `algorithm::to_lower_copy`, Boost.StringAlgorithms
- `algorithm::to_upper`, Boost.StringAlgorithms
- `algorithm::to_upper_copy`, Boost.StringAlgorithms
- `algorithm::trim_copy`, Boost.StringAlgorithms
- `algorithm::trim_copy_if`, Boost.StringAlgorithms
- `algorithm::trim_left_copy`, Boost.StringAlgorithms
- `algorithm::trim_left_copy_if`, Boost.StringAlgorithms



- `algorithm::trim_right_copy`，Boost.StringAlgorithms
- `algorithm::trim_right_copy_if`，Boost.StringAlgorithms
- `algorithm::unhex`，Boost.Algorithm
- `allocator`，`interprocess`，托管共享内存
- `allocator`，`lockfree`，Boost.Lockfree
- `allow_slash_for_short`，`program_options::command_line_style`，Boost.ProgramOptions
- `allow_unregistered`，`program_options::command_line_parser`，Boost.ProgramOptions
- `all_of`，`algorithm`，Boost.Algorithm
- `all_of_equal`，`algorithm`，Boost.Algorithm
- `all_reduce`，`mpi`，集体数据交换
- `any`，`Boost.Any`，Boost.Any
- `any`，`dynamic_bitset`，Boost.DynamicBitset
- `any::empty`，Boost.Any
- `any::type`，Boost.Any
- `any_base_hook`，`intrusive`，Boost.Intrusive
- `any_cast`，`Boost.Any`，Boost.Any
- `any_member_hook`，`intrusive`，Boost.Intrusive
- `any_of`，`algorithm`，Boost.Algorithm
- `any_of_equal`，`algorithm`，Boost.Algorithm
- `any_source`，`mpi`，简单数据交换
- `apply_visitor`，`Boost.Variant`，Boost.Variant
- `archive`，`Boost.Serialization`，存档
- `archive::text_iarchive`，存档
- `archive::text_iarchive::register_type`，类对象的序列化
- `archive::text_oarchive`，存档
- `archive::text_oarchive::register_type`，类对象的序列化
- `arg1`，`phoenix::placeholders`，Boost.Phoenix
- `arg2`，`phoenix::placeholders`，Boost.Phoenix
- `arg3`，`phoenix::placeholders`，Boost.Phoenix
- `array`，`Boost.Array`，Boost.Array
- `array`，`iostreams`，设备
- `array_one`，`circular_buffer`，Boost.CircularBuffer
- `array_sink`，`iostreams`，设备
- `array_source`，`iostreams`，设备
- `array_two`，`circular_buffer`，Boost.CircularBuffer
- `array_view`，`multi_array`，Boost.MultiArray
- `as`，`program_options::variable_value`，Boost.ProgramOptions
- `asio::async_write`，网络编程
- `asio::buffer`，网络编程
- `asio::detail::io_service_impl`，平台特定 I/O 对象
- `asio::detail::task_io_service`，平台特定 I/O 对象
- `asio::detail::win_iocp_io_service`，平台特定 I/O 对象
- `asio::detail::win_iocp_io_service::register_handle`，平台特定 I/O 对象
- `asio::io_service`，I/O 服务和 I/O 对象
- `asio::io_service::run`，I/O 服务和 I/O 对象
- `asio::ip::tcp::acceptor`，网络编程
- `asio::ip::tcp::acceptor::async_accept`，网络编程
- `asio::ip::tcp::acceptor::listen`，网络编程
- `asio::ip::tcp::endpoint`，网络编程
- `asio::ip::tcp::resolver`，网络编程
- `asio::ip::tcp::resolver::async_resolve`，网络编程
- `asio::ip::tcp::resolver::iterator`，网络编程
- `asio::ip::tcp::resolver::query`，网络编程
- `asio::ip::tcp::socket`，网络编程
- `asio::ip::tcp::socket::async_connect`，网络编程
- `asio::ip::tcp::socket::async_read_some`，网络编程
- `asio::ip::tcp::socket::async_write_some`，网络编程
- `asio::ip::tcp::socket::shutdown`，网络编程
- `asio::posix::stream_descriptor`，平台特定 I/O 对象
- `asio::spawn`，协程
- `asio::steady_timer`，I/O 服务和 I/O 对象
- `asio::steady_timer::async_wait`，I/O 服务和 I/O 对象
- `asio::steady_timer::wait`，I/O 服务和 I/O 对象
- `asio::use_service`，平台特定 I/O 对象
- `asio::windows::object_handle`，平台特定 I/O 对象
- `asio::windows::object_handle::async_wait`，平台特定 I/O 对象
- `asio::windows::overlapped_ptr`，平台特定 I/O 对象
- `asio::windows::overlapped_ptr::complete`，平台特定 I/O 对象
- `asio::windows::overlapped_ptr::get`，平台特定 I/O 对象
- `asio::windows::overlapped_ptr::release`，平台特定 I/O 对象
- `assign::add_edge`，Boost.Assign
- `assign::insert`，Boost.Assign
- `assign::list_of`，Boost.Assign
- `assign::map_list_of`，Boost.Assign
- `assign::push`，Boost.Assign
- `assign::push_back`，Boost.Assign
- `assign::push_front`，Boost.Assign
- `assign::tuple_list_of`，Boost.Assign
- `async`，`Boost.Thread`，Futures and Promises
- `async`，`launch`，Futures and Promises
- `asynchronous_sink`，`log::sinks`，Boost.Log
- `async_accept`，`asio::ip::tcp::acceptor`，网络编程
- `async_connect`，`asio::ip::tcp::socket`，网络编程
- `async_read_some`，`asio::ip::tcp::socket`，网络编程
- `async_resolve`，`asio::ip::tcp::resolver`，网络编程
- `async_wait`，`asio::steady_timer`，I/O 服务与 I/O 对象
- `async_wait`，`asio::windows::object_handle`，平台特定 I/O 对象
- `async_write`，`asio`，网络编程
- `async_write_some`，`asio::ip::tcp::socket`，网络编程
- `as_file_name_composer`，`log::sinks::file`，Boost.Log
- `at`，`fusion`，Boost.Fusion
- `at`，`multi_index::random_access`，Boost.MultiIndex
- `atomic`，`Boost.Atomic`，Boost.Atomic
- `atomic::fetch_add`，Boost.Atomic
- `atomic::is_lock_free`，Boost.Atomic
- `atomic::store`，Boost.Atomic
- `atomic_func`，`interprocess::managed_shared_memory`，进程共享内存
- `attr`，`log::expressions`，Boost.Log
- `attributes`，`thread`，创建与管理线程
- `attribute_name`，`log`，Boost.Log
- `attribute_value`，`log`，Boost.Log
- `attribute_values`，`log::attribute_value_set`，Boost.Log
- `attribute_values`，`log::record_view`，Boost.Log
- `attribute_value_set`，`log`，Boost.Log
- `at_key`，`fusion`，Boost.Fusion
- `auto_cpu_timer`，`timer`，Boost.Timer
- `auto_unlink`，`intrusive`，Boost.Intrusive
- `available`，`filesystem::space_info`，文件与目录
- `back`，`fusion`，Boost.Fusion
- `back`，`ptr_vector`，Boost.PointerContainer
- `back_insert_device`，`iostreams`，设备
- `bad_alloc`，`interprocess`，进程共享内存
- `bad_any_cast`，`Boost.Any`，Boost.Any
- `bad_day_of_month`，`gregorian`，日期
- `bad_format_string`，`io`，Boost.Format
- `bad_function_call`，`Boost.Function`，Boost.Function
- `bad_lexical_cast`，`Boost.Conversion`，Boost.LexicalCast
- `bad_month`，`gregorian`，日期
- `bad_numeric_cast`，`numeric`，Boost.NumericConversion
- `bad_year`，`gregorian`，日期
- `base_object`，`serialization`，类层次的序列化
- `basic_ptree`，`property_tree`，Boost.PropertyTree
- `basic_regex`，`Boost.Regex`，Boost.Regex
- `basic_string`，`interprocess`，进程共享内存
- `begin`，`circular_buffer`，Boost.CircularBuffer
- `begin`，`fusion`，Boost.Fusion
- `begin`，`property_tree::ptree`，Boost.PropertyTree
- `begin`，`tokenizer`，Boost.Tokenizer
- `begin`，`uuids::uuid`，Boost.Uuid
- `bernoulli_distribution`，`random`，Boost.Random
- `bidirectional`，`Boost.Graph`，顶点与边
- `big_word`，`spirit::qi`，解析器
- `bimap`，`Boost.Bimap`，Boost.Bimap
- `bimaps_list_of`，Boost.Bimap
- `bimaps_multiset_of`，Boost.Bimap
- `bimaps_set_of`，Boost.Bimap
- `bimaps_set_of_modify_data`，Boost.Bimap
- `bimaps_set_of_modify_key`，Boost.Bimap
- `bimaps_unconstrained_set_of`，Boost.Bimap
- `bimaps_unordered_multiset_of`，Boost.Bimap
- `bimaps_unordered_set_of`，Boost.Bimap
- `bimaps_vector_of`，Boost.Bimap
- `bimaps_data`，Boost.Bimap
- `bimaps_key`，Boost.Bimap
- `bind`，`Boost.Bind`，Boost.Bind
- `bind`，`phoenix`，Boost.Phoenix
- `binomial_heap`，`heap`，Boost.Heap
- `block`，`signals2::shared_connection_block`，连接
- `blocking`，`signals2::shared_connection_block`，连接
- `bool_`，`spirit::qi`，解析器
- `Boost.Accumulators`，Boost.Accumulators
- `Boost.Algorithm`，Boost.Algorithm
- `Boost.Any`，Boost.Any
- `Boost.Array`，Boost.Array
- `Boost.Asio`，Boost.Asio
- `Boost.Assign`，Boost.Assign
- `Boost.Atomic`，Boost.Atomic
- `Boost.Bimap`，Boost.Bimap
- `Boost.Bind`，Boost.Bind
- `Boost.Build`，安装
- `Boost.Chrono`，Boost.Chrono
- `Boost.CircularBuffer`，`Boost.CircularBuffer`
- `Boost.CompressedPair`，`Boost.CompressedPair`
- `Boost.Container`，`Boost.Container`
- `Boost.Conversion`，`Boost.Conversion`
- `Boost.Coroutine`，`Boost.Coroutine`
- `Boost.DateTime`，`Boost.DateTime`
- `Boost.DynamicBitset`，`Boost.DynamicBitset`
- `Boost.EnableIf`，`Boost.EnableIf`
- `Boost.Exception`，`Boost.Exception`
- `Boost.Filesystem`，`Boost.Filesystem`
- `Boost.Flyweight`，`Boost.Flyweight`
- `Boost.Foreach`，`Boost.Foreach`
- `Boost.Format`，`Boost.Format`
- `Boost.Function`，`Boost.Function`
- `Boost.Fusion`，`Boost.Fusion`
- `Boost.Graph`，`Boost.Graph`
- `Boost.Heap`，`Boost.Heap`
- `Boost.Integer`，`Boost.Integer`
- `Boost.Interprocess`，`Boost.Interprocess`
- `Boost.Intrusive`，`Boost.Intrusive`
- `Boost.IOStreams`，`Boost.IOStreams`
- `Boost.Lambda`，`Boost.Lambda`
- `Boost.LexicalCast`，`Boost.LexicalCast`
- `Boost.Lockfree`，`Boost.Lockfree`
- `Boost.Log`，`Boost.Log`
- `Boost.MetaStateMachine`，`Boost.MetaStateMachine`



- `Boost.MinMax`, `Boost.MinMax`

- `Boost.MPI`, `Boost.MPI`

- `Boost.MultiArray`, `Boost.MultiArray`

- `Boost.MultiIndex`, `Boost.MultiIndex`

- `Boost.NumericConversion`, `Boost.NumericConversion`

- `Boost.Operators`, `Boost.Operators`

- `Boost.Optional`, `Boost.Optional`

- `Boost.Parameter`, `Boost.Parameter`

- `Boost.Phoenix`, `Boost.Phoenix`

- `Boost.PointerContainer`, `Boost.PointerContainer`

- `Boost.Pool`, `Boost.Pool`

- `Boost.ProgramOptions`, `Boost.ProgramOptions`

- `Boost.PropertyTree`, `Boost.PropertyTree`

- `Boost.Random`, `Boost.Random`

- `Boost.Range`, `Boost.Range`

- `Boost.Ref`, `Boost.Ref`

- `Boost.Regex`, `Boost.Regex`

- `Boost.ScopeExit`, `Boost.ScopeExit`

- `Boost.Serialization`, `Boost.Serialization`

- `Boost.Signals2`, `Boost.Signals2`

- `Boost.SmartPointers`, `Boost.SmartPointers`

- `Boost.Spirit`, `Boost.Spirit`

- `Boost.StringAlgorithms`, `Boost.StringAlgorithms`

- `Boost.Swap`, `Boost.Swap`

- `Boost.System`, `Boost.System`

- `Boost.Thread`, `Boost.Thread`

- `Boost.Tokenizer`, `Boost.Tokenizer`

- `Boost.Tribool`, `Boost.Tribool`

- `Boost.Tuple`, `Boost.Tuple`

- `Boost.TypeTraits`, `Boost.TypeTraits`

- `Boost.Unordered`, `Boost.Unordered`

- `Boost.Utility`, `Boost.Utility`

- `Boost.Uuid`, `Boost.Uuid`

- `Boost.Variant`, `Boost.Variant`

- `Boost.Xpress`, `Boost.Xpress`

- `BOOST_ATOMIC_LONG`, `BOOST_ATOMIC_LONG`

- `BOOST_ATOMIC_LONG_LOCK`, `BOOST_ATOMIC_LONG_LOCK`

- `BOOST_BINARY`, `BOOST_BINARY`

- `BOOST_DISABLE_ASSERTS`, `BOOST_DISABLE_ASSERTS`

- `BOOST_CURRENT_FUNCTION`, `BOOST_CURRENT_FUNCTION`

- `BOOST_EXPORT`, `BOOST_EXPORT`

- `BOOST_GLOBAL_LOGGER_CTOR_ARGS`, `BOOST_GLOBAL_LOGGER_CTOR_ARGS`

- `BOOST_INLINE_GLOBAL_LOGGER_CTOR_ARGS`, `BOOST_INLINE_GLOBAL_LOGGER_CTOR_ARGS`

- `BOOST_LOG`, `BOOST_LOG`

- `BOOST_LOG_ATTRIBUTE_KEYWORD`, `BOOST_LOG_ATTRIBUTE_KEYWORD`

- `BOOST_CLASS_EXPORT`, `BOOST_CLASS_EXPORT`

- `BOOST_CLASS_VERSION`, `BOOST_CLASS_VERSION`

- `BOOST_LOG_INLINE_GLOBAL_LOGGER_DEFAULT`, `Boost.Log`, `Boost.Log`

- `BOOST_LOG_SCOPED_LOGGER_ATTR`, `Boost.Log`, `Boost.Log`

- `BOOST_LOG_SEV`, `Boost.Log`, `Boost.Log`

- `BOOST_MSM_EUML_ACTION`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_DECLARE_ATTRIBUTE`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_DECLARE_STATE_MACHINE`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_EVENT`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_FUNCTION`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_STATE`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_STATE_NAME`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_MSM_EUML_TRANSITION_TABLE`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `BOOST_NO_INT64_T`, `Boost.Integer`, `Boost.Integer`

- `BOOST_NUMERIC_FUNCTIONAL_STD_COMPLEX_SUPPORT`, `Boost.Accumulators`, `Boost.Accumulators`

- `BOOST_NUMERIC_FUNCTIONAL_STD_ARRAY_SUPPORT`, `Boost.Accumulators`, `Boost.Accumulators`

- `BOOST_NUMERIC_FUNCTIONAL_STD_VECTOR_SUPPORT`, `Boost.Accumulators`, `Boost.Accumulators`

- `BOOST_PARAMETER_CONST_MEMBER_FUNCTION`, `Boost.Parameter`, `Boost.Parameter`

- `BOOST_PARAMETER_FUNCTION`, `Boost.Parameter`, `Boost.Parameter`

- `BOOST_PARAMETER_MEMBER_FUNCTION`, `Boost.Parameter`, `Boost.Parameter`

- `BOOST_PARAMETER_NAME`, `Boost.Parameter`, `Boost.Parameter`

- `BOOST_PARAMETER_TEMPLATE_KEYWORD`, `Boost.Parameter`, `Boost.Parameter`

- `BOOST_PHOENIX_ADAPT_FUNCTION`, `Boost.Phoenix`, `Boost.Phoenix`

- `BOOST_POOL_NO_MT`, `Boost.Pool`, `Boost.Pool`

- `BOOST_POSIX_API`, `Boost.Filesystem`, `Paths`

- `BOOST_REGEX_USE_CPP_LOCALE`, `Boost.Regex`, `Boost.Regex`

- `BOOST_REVERSE_FOREACH`, `Boost.Foreach`, `Boost.Foreach`

- `BOOST_SCOPE_EXIT`, `Boost.ScopeExit`, `Boost.ScopeExit`

- `BOOST_SPIRIT_USE_PHOENIX_V3`, `Boost.Spirit`, `Boost.Spirit`

- `BOOST_SP_ENABLE_DEBUG_HOOKS`, `Boost.SmartPointers`, `Shared Ownership`

- `BOOST_SP_USE_QUICK_ALLOCATOR`, `Boost.SmartPointers`, `Shared Ownership`

- `BOOST_THROW_EXCEPTION`, `Boost.Exception`, `Boost.Exception`

- `BOOST_TRIBOOL_THIRD_STATE`, `Boost.Tribool`, `Boost.Tribool`

- `BOOST_WINDOWS_API`, `Boost.Filesystem`, `Paths`

- `breadth_first_search`, `Boost.Graph`, `Boost.Graph`

- `broadcast`, `mpi`, `Collective Data`

- `buffer`, `asio`, `Network programming`

- `bundled`, `Boost.Graph`, `Boost.Graph`

- `byte_`, `spirit::qi`, `Parsers`

- `cancel`, `mpi::request`, `Asynchronous data`

- `capacity`, `circular_buffer`, `Boost.CircularBuffer`

- `capacity`, `filesystem::space_info`, `Files and Directories`

- `category`, `system::error_code`, `Boost.System`, `Boost.System`

- `category`, `system::error_condition`, `Boost.System`, `Boost.System`

- `ceil`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `channel`, `log::keywords`, `Boost.Log`, `Boost.Log`

- `channel_logger`, `log::sources`, `Boost.Log`, `Boost.Log`

- `characters`, `iostreams::counter`, `Filters`

- `Char_`, `msm::front::euml`, `Boost.MetaStateMachine`, `Boost.MetaStateMachine`

- `char_separator`, `Boost.Tokenizer`, `Boost.Tokenizer`

- `checked_array_delete`, `Boost.Utility`, `Boost.Utility`

- `checked_array_deleter`, `Boost.Utility`, `Boost.Utility`

- `checked_delete`, `Boost.Utility`, `Boost.Utility`

- `checked_deleter`, `Boost.Utility`, `Boost.Utility`

- `chi_squared_distribution`, `random`, `Boost.Random`

- `ceil`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `duration`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `duration_cast`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `floor`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `high_resolution_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `hours`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `nanoseconds`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `microseconds`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `minutes`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `process_cpu_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `process_real_cpu_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `process_system_cpu_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `process_user_cpu_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `round`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `seconds`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `steady_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `symbol_format`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `system_clock`, `chrono`, `Boost.Chrono`, `Boost.Chrono`

- `chrono::system_clock::to_time_t`, `Boost.Chrono`

- `chrono::thread_clock`, `Boost.Chrono`

- `chrono::timezone::local`, `Boost.Chrono`

- `chrono::timezone::utc`, `Boost.Chrono`

- `chrono::time_fmt`, `Boost.Chrono`

- `chrono::time_point`, `Boost.Chrono`

- `chrono::time_point_cast`, `Boost.Chrono`

- `circular buffer`, `Boost.CircularBuffer`, `Boost.CircularBuffer`

- `circular_buffer`, `Boost.CircularBuffer`, `Boost.CircularBuffer`

- `circular_buffer::array_one`, `Boost.CircularBuffer`

- `circular_buffer::array_two`, `Boost.CircularBuffer`

- `circular_buffer::begin`, `Boost.CircularBuffer`

- `circular_buffer::capacity`, `Boost.CircularBuffer`

- `circular_buffer::end`, `Boost.CircularBuffer`

- `circular_buffer::is_linearized`, `Boost.CircularBuffer`

- `circular_buffer::linearize`, `Boost.CircularBuffer`

- `circular_buffer::size`, `Boost.CircularBuffer`

- `circular_buffer_space_optimized`, `Boost.CircularBuffer`, `Boost.CircularBuffer`

- `clear`, `adjacency_list`, 顶点与边

- `clear`, `timer::times`, `Boost.Timer`

- `close`, `iostreams::file_source`, 设备

- `close_handle`, `iostreams`, 设备

- `collective operations`, `Boost.MPI`, 集体数据交换

- `collect_unrecognized`, `program_options`, `Boost.ProgramOptions`

- `combiner`, `Boost.Signals2`, 信号

- `comma separated values`, `Boost.Tokenizer`, `Boost.Tokenizer`

- `command_line_parser`, `program_options`, `Boost.ProgramOptions`

- `communicator`, `Boost.MPI`, 集体数据交换

- `communicator`, `mpi`, 集体数据交换

- `compile`, `xpressive::regex`, `Boost.Xpressive`

- `complete`, `asio::windows::overlapped_ptr`, 平台特定 I/O



- `component`, `iostreams::filtering_stream`，过滤器
- `composing`，`program_options::value_semantic`，Boost.ProgramOptions
- `composite_key`，`multi_index`，Boost.MultiIndex
- `compressed_pair`，`Boost.CompressedPair`，Boost.CompressedPair
- `compressed_pair::first`，`Boost.CompressedPair`，Boost.CompressedPair
- `compressed_pair::second`，`Boost.CompressedPair`，Boost.CompressedPair
- `compressed_sparse_row_graph`，`Boost.Graph`，Boost.Graph
- `condition_variable`，`Boost.Interprocess`，同步
- `condition_variable`，`Boost.Thread`，同步线程
- `condition_variable_any::notify_all`，同步线程
- `condition_variable_any::wait`，同步线程
- `connect`，`signals2::signal`，信号
- `connection`，`signals2`，连接
- `constant_time_size`，`intrusive`，Boost.Intrusive
- `construct`，`interprocess::managed_shared_memory`，托管共享内存
- `construct`，`object_pool`，Boost.Pool
- `const_mem_fun`，`multi_index`，Boost.MultiIndex
- `const_multi_array_ref`，`Boost.MultiArray`，Boost.MultiArray
- `consume_all`，`lockfree::queue`，Boost.Lockfree
- `consume_all`，`lockfree::spsc_queue`，Boost.Lockfree
- `consume_one`，`lockfree::queue`，Boost.Lockfree
- `consume_one`，`lockfree::spsc_queue`，Boost.Lockfree
- `container::flat_map`，`Boost.Container`，Boost.Container
- `container::flat_set`，`Boost.Container`，Boost.Container
- `container::slist`，`Boost.Container`，Boost.Container
- `container::stable_vector`，`Boost.Container`，Boost.Container
- `container::static_vector`，`Boost.Container`，Boost.Container
- `contains`，`boost::date`，日历
- `contains`，`gregorian_date`，日历
- `contains`，`posix_time::local_time`，日历
- `contains`，`posix_time::time_duration`，日历
- `copy`，`boost::range`，Boost.Range
- `copy`，`iostreams::file_source`，设备
- `copy`，`iostreams::filtering_stream`，设备
- `copy_n`，`boost::range`，Boost.Range
- `copy_until`，`boost::range`，Boost.Range
- `copy_while`，`boost::range`，Boost.Range
- `coroutine`，`Boost.Coroutine`，Boost.Coroutine
- `coroutine`，`coroutines`，Boost.Coroutine
- `coroutines::coroutine`，`Boost.Coroutine`，Boost.Coroutine
- `coroutines::coroutine::pull_type`，`Boost.Coroutine`，Boost.Coroutine
- `coroutines::coroutine::push_type`，`Boost.Coroutine`，Boost.Coroutine
- `count`，`accumulators`，Boost.Accumulators
- `count`，`accumulators::tag`，Boost.Accumulators
- `count`，`Boost.MultiIndex`，Boost.MultiIndex
- `count`，`Boost.Range`，算法
- `count`，`dynamic_bitset`，Boost.DynamicBitset
- `count`，`program_options::variables_map`，Boost.ProgramOptions
- `counter`，`iostreams`，Filters
- `counter`，`log::attributes`，Boost.Log
- `cpp_regex_traits`，`Boost.Regex`，Boost.Regex
- `cpu_timer`，`timer`，Boost.Timer
- `create_symlink`，`filesystem`，文件与目录
- `cref`，`Boost.Ref`，Boost.Ref
- `cregex`，`xpressive`，Boost.Xpressive
- `CSV`，`Boost.Tokenizer`（参见逗号分隔值）
- `current_path`，`filesystem`，文件与目录

### D

- `data`，`iostreams::mapped_file_source`，设备
- `date`，`gregorian`，日历日期
- `date`，`posix_time::ptime`，与无关的时间
- `date_duration`，`gregorian`，日历日期
- `date_facet`，`date_time`，格式化输入输出
- `date_from_iso_string`，`gregorian`，日历日期
- `date_input_facet`，`date_time`，格式化输入输出
- `date_period`，`gregorian`，日历日期
- `date_time::date_facet`，格式化输入输出
- `date_time::date_input_facet`，格式化输入输出
- `date_time::next_weekday`，日历日期
- `date_time::not_a_date_time`，日历日期，与无关的时间
- `date_time::time_facet`，格式化输入输出
- `date_time::time_input_facet`，格式化输入输出
- `day`，`gregorian`，日历日期
- `days`，`gregorian::date_duration`，日历日期
- `day_clock`，`gregorian`，日历日期
- `day_iterator`，`gregorian`，日历日期
- `day_of_week`，`gregorian`，日历日期
- `day_of_week_type`，`gregorian::date`，日历日期
- `decrease`，`heap::binomial_heap`，Boost.Heap
- `default_error_condition`，`system::error_code`，Boost.System
- `default_user_allocator_malloc_free`，`Boost.Pool`，Boost.Pool
- `default_user_allocator_new_delete`，`Boost.Pool`，Boost.Pool
- `default_value`，`program_options::value_semantic`，Boost.ProgramOptions
- `deferred`，`launch`，Futures and Promises
- `deleter`，`Boost.SmartPointers`，共享所有权
- `deque`，`fusion`，Boost.Fusion
- `destroy`，`interprocess::managed_shared_memory`，托管共享内存
- `destroy`，`object_pool`，Boost.Pool
- `destroy_ptr`，`interprocess::managed_shared_memory`，托管共享内存
- `detach`，`thread`，创建与管理线程
- `details::pool::null_mutex`，`Boost.Pool`，Boost.Pool
- `device`，`Boost.IOStreams`，Boost.IOStreams
- `diagnostic_information`，`Boost.Exception`，Boost.Exception
- `digit`，`spirit::ascii`，API
- `dijkstra_shortest_paths`，`Boost.Graph`，算法
- `directedS`，`Boost.Graph`，顶点与边
- `directory_iterator`，`filesystem`，目录迭代器
- `disable_interruption`，`thread`，创建与管理线程
- `disconnect`，`signals2::connection`，连接
- `disconnect`，`signals2::signal`，信号
- `disconnect_all`，`signals2::signal`，信号
- `distance`，`fusion`，Boost.Fusion
- `distribution`，`Boost.Random`，Boost.Random
- `dont_post`，`spirit::qi::skip_flag`，API
- `double_`，`spirit::qi`，解析器
- `dummy_mutex`，`signals2`，多线程
- `duration`，`chrono`，Boost.Chrono
- `duration_cast`，`chrono`，Boost.Chrono
- `dynamic_bitset`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::any`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::count`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::none`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::push_back`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::reference::flip`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::resize`，`Boost.DynamicBitset`，Boost.DynamicBitset
- `dynamic_bitset::size`，`Boost.DynamicBitset`，Boost.DynamicBitset

### E

- `edges`，`Boost.Graph`，顶点与边
- `edge_weight_t`，`Boost.Graph`，算法
- `elapsed`，`timer::cpu_timer`，Boost.Timer
- `empty`，`any`，Boost.Any
- `empty`，`function`，Boost.Function
- `empty`，`signals2::signal`，信号
- `enable_error_info`，`Boost.Exception`，Boost.Exception
- `enable_if`，`Boost.EnableIf`，Boost.EnableIf
- `end`，`circular_buffer`，Boost.CircularBuffer
- `end`，`fusion`，Boost.Fusion
- `end`，`property_tree::ptree`，Boost.PropertyTree
- `end`，`tokenizer`，Boost.Tokenizer
- `end`，`uuids::uuid`，Boost.Uuid
- `endpoint`，`asio::ip::tcp`，网络编程
- `ends_with`，`algorithm`，Boost.StringAlgorithms
- `end_of_month`，`gregorian::date`，日期日期
- `environment`，`mpi`，简单数据交换
- `environment_iterator`，`Boost.ProgramOptions`，Boost.ProgramOptions
- `eol`，`spirit::qi`，解析器
- `epoch`，`Boost.Chrono`，Boost.Chrono
- `equal`，`algorithm`，Boost.Algorithm
- `erase_all_copy`，`algorithm`，Boost.StringAlgorithms
- `erase_first_copy`，`algorithm`，Boost.StringAlgorithms
- `erase_head_copy`，`algorithm`，Boost.StringAlgorithms
- `erase_key`，`fusion`，Boost.Fusion
- `erase_tail_copy`，`algorithm`，Boost.StringAlgorithms
- `error`，`program_options`，Boost.ProgramOptions
- `error_category`，`system`，Boost.System
- `error_code`，`system`，Boost.System
- `error_condition`，`system`，Boost.System
- `error_info`，`system`，Boost.Exception
- `escaped_list_separator`，`Boost.Tokenizer`，Boost.Tokenizer
- `event_`，`msm::front`，Boost.StateMachine
- `exception`，`Boost.Exception`，Boost.Exception
- `exception_ptr`，`Boost.Exception`，Boost.Exception
- `exclude`，`mpi::group`，Communicators
- `exclude_position`，`program_options`，Boost.ProgramOptions
- `exclusive lock`，`Boost.Thread`，Synchron Threads
- `exists`，`filesystem`，文件和目录
- `extension`，`filesystem::path`，路径
- `extents`，`Boost.MultiArray`，Boost.MultiArray
- `extract`，`log::attribute_name`，Boost.Log
- `extractor`，`Boost.Accumulators`，Boost.Accumulators
- `extract_or_default`，`log::attribute_name`，Boost.Log
- `extract_or_throw`，`log::attribute_name`，Boost.Log
- `false_type`，`Boost.TypeTraits`，Boost.TypeTraits
- `fast_pool_allocator`，`Boost.Pool`，Boost.Pool
- `feature`，`Boost.Accumulators`，Boost.Accumulators
- `features`，`accumulators`，Boost.Accumulators



- `fetch_add`, `Boost.Atomic`, Boost.Atomic
- `fibonacci_heap`, `Boost.Heap`, Boost.Heap
- `file lock`, `Boost.Interprocess`, Boost.Interprocess
- `filename`, `filesystem::path`, 路径
- `filesystem::absolute`, 文件和目录
- `filesystem::copy_directory`, 文件和目录
- `filesystem::copy_file`, 文件和目录
- `filesystem::create_symlink`, 文件和目录
- `filesystem::current_path`, 文件和目录
- `filesystem::directory_iterator`, 迭代器
- `filesystem::exists`, 文件和目录
- `filesystem::filesystem_error`, 文件和目录
- `filesystem::filesystem_error::path1`, 文件和目录
- `filesystem::filesystem_error::path2`, 文件和目录
- `filesystem::file_size`, 文件和目录
- `filesystem::file_status`, 文件和目录
- `filesystem::is_directory`, 文件和目录
- `filesystem::is_regular_file`, 文件和目录
- `filesystem::is_symlink`, 文件和目录
- `filesystem::last_write_time`, 文件和目录
- `filesystem::ofstream`, 文件流
- `filesystem::ofstream::open`, 文件流
- `filesystem::path`, 路径
- `filesystem::path::extension`, 路径
- `filesystem::path::filename`, 路径
- `filesystem::path::generic_string`, 路径
- `filesystem::path::generic_wstring`, 路径
- `filesystem::path::has_filename`, 路径
- `filesystem::path::has_parent_path`, 路径
- `filesystem::path::has_relative_path`, 路径
- `filesystem::path::has_root_directory`, 路径
- `filesystem::path::has_root_name`, 路径
- `filesystem::path::has_root_path`, 路径
- `filesystem::path::make_absolute`, 路径
- `filesystem::path::make_preferred`, 路径
- `filesystem::path::native`, 路径
- `filesystem::path::operator/=`, 路径
- `filesystem::path::parent_path`, 路径
- `filesystem::path::relative_path`, 路径
- `filesystem::path::remove_filename`, 路径
- `filesystem::path::replace_extension`, 路径
- `filesystem::path::root_directory`, 路径
- `filesystem::path::root_name`, 路径
- `filesystem::path::root_path`, 路径
- `filesystem::path::stem`, 路径
- `filesystem::path::string`, 路径
- `filesystem::path::wstring`, 路径
- `filesystem::recursive_directory_iterator`, 目录迭代器
- `filesystem::space`, 文件和目录
- `filesystem::space_info`, 文件和目录
- `filesystem::space_info::available`, 文件和目录
- `filesystem::space_info::capacity`, 文件和目录
- `filesystem::space_info::free`, 文件和目录
- `filesystem::status`, 文件和目录
- `filesystem::symlink_status`, 文件和目录
- `filesystem_error`, `filesystem`, 文件和目录
- `file_descriptor_sink`, `iostreams`, 设备
- `file_descriptor_source`, `iostreams`, 设备
- `file_sink`, `iostreams`, 设备
- `file_size`, `filesystem`, 文件和目录
- `file_source`, `iostreams`, 设备
- `file_status`, `filesystem`, 文件和目录
- `filter`, `adaptors`, 适配器
- `filtering_istream`, `iostreams`, 过滤器
- `filtering_ostream`, `iostreams`, 过滤器
- `filter_view`, `fusion`, Boost.Fusion
- `find`, `interprocess::managed_shared_memory`, 共享内存
- `find_first`, `algorithm`, 字符串
- `find_-`, `_`, `algorithmpart 0`
- `find_if_not`, `algorithm`, 算法
- `find_last`, `algorithm`, 字符串
- `find_nth`, `algorithm`, 字符串
- `find_or_construct`, `interprocess::managed_shared_memory`, 共享内存
- `find_regex`, `algorithm`, 字符串
- `find_tail`, `algorithm`, 字符串
- `first`, `compressed_pair`, Boost.CompressedPair
- `fixed_sized`, `lockfree`, Boost.Lockfree
- `flat_map`, `container`, Boost.Container
- `flat_set`, `container`, Boost.Container
- `flip`, `dynamic_bitset::reference`, Boost.DynamicBitset
- `float_`, `spirit::qi`, 解析器
- `floor`, `chrono`, Boost.Chrono
- `flush`, `log::sinks::asynchronous_sink`, Boost.Log
- `flyweight`, `flyweights`, Boost.Flyweight
- `flyweights::flyweight`, Boost.Flyweight
- `flyweights::no_locking`, Boost.Flyweight
- `flyweights::no_tracking`, Boost.Flyweight
- `flyweights::set_factory`, Boost.Flyweight
- `format`, `Boost.Format`, Boost.Format
- `format`, `timer::cpu_timer`, Boost.Timer
- `format::operator`, Boost.Format
- `formatting_ostream`, `log`, Boost.Log
- `format_date`, `log`, Boost.Log
- `format_error`, `filesystem`, Boost.Format
- `format_literal`, `regex`, Boost.Regex
- `for_each`, `filesystem`, 目录迭代器
- `free`, `filesystem`, 文件和目录
- `free`, `filesystem`, 文件和目录
- `free`, `filesystem`, 文件和目录
- `free`, `filesystem`, 文件和目录
- `from_iso`, `filesystem`, 文件和目录
- `from_us`, `filesystem`, 文件和目录
- `fsm::front`, Boost.StateMachine
- `function`, `Boost`, Boost.Phoenix
- `function`, `Boost`, Boost.Phoenix
- `function::operator bool`, Boost.Phoenix
- `fusion::advance`, Boost.Fusion
- `fusion::at`, Boost.Fusion
- `fusion::at_key`, Boost.Fusion
- `fusion::back`, Boost.Fusion
- `fusion::begin`, Boost.Fusion
- `fusion::deque`, Boost.Fusion
- `fusion::distance`, Boost.Fusion
- `fusion::end`, Boost.Fusion
- `fusion::erase_key`, Boost.Fusion
- `fusion::filter_view`, Boost.Fusion

## Boost Fusion

- `fusion::for_each`, Boost.Fusion
- `fusion::get`, Boost.Fusion
- `fusion::has_key`, Boost.Fusion
- `fusion::list`, Boost.Fusion
- `fusion::make_pair`, Boost.Fusion
- `fusion::make_tuple`, Boost.Fusion
- `fusion::map`, Boost.Fusion
- `fusion::next`, Boost.Fusion
- `fusion::prior`, Boost.Fusion
- `fusion::push_back`, Boost.Fusion
- `fusion::set`, Boost.Fusion
- `fusion::size`, Boost.Fusion
- `fusion::tuple`, Boost.Fusion
- `fusion::vector`, Boost.Fusion

### Boost.Thread

- `future` (概念), Boost.Thread, 未来与承诺
- `future`, Boost.Thread, 未来与承诺
- `future::get`, 未来与承诺

### G

- `gather`, mpi, 集体数据交换
- `generic path`, Boost.Filesystem, 路径
- `generic_category`, system, Boost.System
- `generic_string`, `filesystem::path`, 路径
- `generic_wstring`, `filesystem::path`, 路径
- `get`, `asio::windows::overlapped_ptr`, 特定平台的 I/O 对象
- `get`, `Boost.Graph`, 算法
- `get`, `Boost.Tuple`, Boost.Tuple
- `get`, `Boost.Variant`, Boost.Variant
- `get`, `fusion`, Boost.Fusion
- `get`, `future`, 未来与承诺
- `get`, `log::core`, Boost.Log
- `get`, `multi_index::multi_index_container`, Boost.MultiIndex
- `get`, `optional`, Boost.Optional
- `get`, `property_tree::ptree`, Boost.PropertyTree
- `get`, `scoped_array`, 独占所有
- `get`, `scoped_ptr`, 独占所有
- `get`, `shared_array`, 共享所有
- `get`, `shared_ptr`, 共享所有
- `get`, `thread_specific_ptr`, 线程本地存储
- `get`, `tuple`, Boost.Tuple
- `get_address`, `interprocess::mapped_region`, 共享内存
- `get_child`, `property_tree::ptree`, Boost.PropertyTree
- `get_child_optional`, `property_tree::ptree`, Boost.PropertyTree
- `get_error_info`, `Boost.Exception`, Boost.Exception
- `get_future`, `packaged_task`, 未来与承诺
- `get_future`, `promise`, 未来与承诺
- `get_id`, `this_thread`, 创建与管理线程
- `get_name`, `interprocess::shared_memory_object`, 共享内存
- `get_next_size`, `object_pool`, Boost.Pool
- `get_optional`, `property_tree::ptree`, Boost.PropertyTree
- `get_optional_value_or`, `Boost.Optional`, Boost.Optional
- `get_size`, `interprocess::mapped_region`, 共享内存
- `get_size`, `interprocess::shared_memory_object`, 共享内存
- `get_value`, `property_tree::ptree`, Boost.PropertyTree
- `get_value_or`, `Boost.Optional`, Boost.Optional
- `generic`, `tuple`, Boost.Tuple
- `generic`, `optional`, Boost.Optional
- `generic`, `future`, 未来与承诺
- `generic`, `fusion`, Boost.Fusion
- `generic`, `property_tree::ptree`, Boost.PropertyTree
- `generic`, `scoped_array`, 独占所有
- `generic`, `scoped_ptr`, 独占所有
- `generic`, `shared_array`, 共享所有
- `generic`, `shared_ptr`, 共享所有
- `generic`, `thread_specific_ptr`, 线程本地存储
- `generic`, `tuple`, Boost.Tuple
- `gregorian`, `bad_day`, 日历
- `gregorian`, `bad_month`, 日历
- `gregorian`, `bad_year`, 日历
- `gregorian`, `date`, 日历
- `gregorian`, `day`, 日历
- `gregorian`, `day_of_week`, 日历
- `gregorian`, `day_of_week_type`, 日历
- `gregorian`, `end_of_month`, 日历
- `gregorian`, `month`, 日历
- `gregorian`, `month_type`, 日历
- `gregorian`, `year`, 日历
- `gregorian::month_iterator`, 日日期
- `gregorian::weeks`, 日日期
- `gregorian::week_iterator`, 日日期
- `gregorian::years`, 日日期
- `gregorian::year_iterator`, 日日期
- `group, io`, Boost.Format
- `group, mpi`, 通信器
- `group, mpi::communicator`, 通信器

### H

- `handler, Boost.Asio`, I/O 服务与 I/O 对象
- `hardware_concurrency, thread`, 创建与管理线程
- `hashed_non_unique, multi_index`, Boost.MultiIndex
- `hashed_unique, multi_index`, Boost.MultiIndex



- `hash_combine`, Boost.Unordered
- `hash_setS`, Boost.Graph, 顶点与边
- `has_filename`, `filesystem::path`, 路径
- `has_key`, fusion, Boost.Fusion
- `has_parent_path`, `filesystem::path`, 路径
- `has_plus`, Boost.TypeTraits
- `has_pre_increment`, Boost.TypeTraits
- `has_relative_path`, `filesystem::path`, 路径
- `has_root_directory`, `filesystem::path`, 路径
- `has_root_name`, `filesystem::path`, 路径
- `has_root_path`, `filesystem::path`, 路径
- `has_trivial_copy`, Boost.TypeTraits
- `has_virtual_destructor`, Boost.TypeTraits
- `heap::binomial_heap`, Boost.Heap
- `heap::binomial_heap::decrease`, Boost.Heap
- `heap::binomial_heap::increase`, Boost.Heap
- `heap::binomial_heap::merge`, Boost.Heap
- `heap::binomial_heap::ordered_begin`, Boost.Heap
- `heap::binomial_heap::ordered_end`, Boost.Heap
- `heap::binomial_heap::push`, Boost.Heap
- `heap::binomial_heap::top`, Boost.Heap
- `heap::binomial_heap::update`, Boost.Heap
- `heap::fibonacci_heap`, Boost.Heap
- `heap::priority_queue`, Boost.Heap
- `hex`, algorithm, Boost.Algorithm
- `high_resolution_clock`, chrono, Boost.Chrono
- `hook`, Boost.Intrusive
- `hours`, chrono, Boost.Chrono
- `hours`, `posix_time::time_duration`, 位置时间
- `I/O object`, Boost.Asio, I/O 服务与 I/O 对象
- `I/O service`, Boost.Asio, I/O 服务与 I/O 对象
- `identity`, multi_index, Boost.MultiIndex
- `ierase_all_copy`, algorithm, Boost.Algorithms
- `if_`, phoenix, Boost.Phoenix
- `if_then`, lambda, Boost.Lambda
- `if_then_else`, lambda, Boost.Lambda
- `if_then_else_return`, lambda, Boost.Lambda
- `imbue`, regex, Boost.Regex
- `implicit_value`, `program_options::value_semantic`, Boost.ProgramOptions
- `include`, mpi, 通信器
- `incomplete type`, Boost.Container
- `increase`, `heap::binomial_heap`, Boost.Heap
- `indeterminate`, Boost.Tribool
- `indeterminate`, logic, Boost.Tribool
- `indexed_by`, multi_index, Boost.MultiIndex
- `index_range`, multi_array, Boost.MultiArray
- `indices`, Boost.MultiArray
- `indirect_fun`, Boost.PointerContainer
- `initialized`, `mpi::environment`, 数据交换
- `insert`, assign, Boost.Assign
- `insert`, Boost.MultiIndex
- `INT64`, Boost.Integer
- `int8_t`, Boost.Integer
- `integer_range`, Boost.Integer, 辅助类
- `interprocess::allocator`, 托管内存
- `interprocess::bad_alloc`, 托管内存
- `interprocess::basic_string`, 托管内存
- `interprocess::interprocess_exception`, 共享内存
- `interprocess::interprocess_mutex`, 同步
- `interprocess::interprocess_mutex::timed_lock`, 同步
- `interprocess::interprocess_mutex::try_lock`, 同步
- `interprocess::interprocess_recursive_mutex`, 同步
- `interprocess::managed_shared_memory`, 托管共享内存
- `interprocess::managed_shared_memory::atomic_func`, 托管共享内存
- `interprocess::managed_shared_memory::construct`, 托管共享内存
- `interprocess::managed_shared_memory::destroy`, 托管共享内存
- `interprocess::managed_shared_memory::destroy_ptr`, 托管共享内存
- `interprocess::managed_shared_memory::find`, 托管共享内存
- `interprocess::managed_shared_memory::find_or_construct`, 托管共享内存
- `interprocess::map`, 托管共享内存
- `interprocess::mapped_region`, 共享内存
- `interprocess::mapped_region::get_address`, 共享内存
- `interprocess::mapped_region::get_size`, 共享内存
- `interprocess::named_condition`, 同步
- `interprocess::named_condition::notify_all`, 同步
- `interprocess::named_condition::wait`, 同步
- `interprocess::named_mutex`, 同步
- `interprocess::named_mutex::lock`, 同步
- `interprocess::named_mutex::timed_lock`, 同步
- `interprocess::named_mutex::try_lock`, 同步
- `interprocess::named_mutex::unlock`, 同步
- `interprocess::named_recursive_mutex`, 同步
- `interprocess::open_or_create`, 共享内存
- `interprocess::read_write`, 共享内存
- `interprocess::remove_shared_memory_on_destroy`, 共享内存
- `interprocess::shared_memory_object`, 共享内存
- `interprocess::shared_memory_object::get_name`, 共享内存
- `interprocess::shared_memory_object::get_size`, 共享内存
- `interprocess::shared_memory_object::remove`, 共享内存
- `interprocess::shared_memory_object::truncate`, 共享内存
- `interprocess::string`, 托管共享内存
- `interprocess::vector`, 托管共享内存
- `interprocess::windows_shared_memory`, 共享内存
- `interprocess_exception`, 共享内存
- `interprocess_mutex`, 同步
- `interprocess_recursive_mutex`, 同步
- `interrupt`, `thread`, 创建与管理线程
- `interruption point`, 创建与管理线程
- `intersection`, `local_time::local_time`, 依赖位置的时间
- `intersection`, `posix_time::time_period`, 位置无关的时间
- `intmax_t`, Boost.Integer
- `intrusive container`, Boost.Intrusive
- `intrusive::any_base_hook`, Boost.Intrusive
- `intrusive::any_member_hook`, Boost.Intrusive
- `intrusive::auto_unlink`, Boost.Intrusive
- `intrusive::constant_time_size`, Boost.Intrusive
- `intrusive::link_mode`, Boost.Intrusive
- `intrusive::list`, Boost.Intrusive
- `intrusive::list::pop_back_and_dispose`, Boost.Intrusive
- `intrusive::list::push_back`, Boost.Intrusive
- `intrusive::list::size`, Boost.Intrusive
- `intrusive::list_base_hook`, Boost.Intrusive
- `intrusive::list_member_hook`, Boost.Intrusive
- `intrusive::member_hook`, Boost.Intrusive
- `intrusive::set`, Boost.Intrusive
- `intrusive::set_member_hook`, Boost.Intrusive
- `intrusive::slist`, Boost.Intrusive
- `intrusive::unordered_set`, Boost.Intrusive
- `intrusive_ptr`, `Boost.SmartPointers`, 特殊智能指针
- `intrusive_ptr_add_ref`, `Boost.SmartPointers`, 特殊智能指针
- `intrusive_ptr_release`, `Boost.SmartPointers`, 特殊智能指针
- `Int_`, `msm::front::euml`, Boost.MetaStateMachine
- `int_`, `spirit::qi`, 解析器
- `int_fast8_t`, `Boost.Integer`
- `int_least8_t`, `Boost.Integer`
- `invalid_syntax`, `program_options`, Boost.ProgramOptions
- `in_edges`, `Boost.Graph`, 顶点与边
- `io::bad_format_string`, `Boost.Format`
- `io::format_error`, `Boost.Format`
- `io::group`, `Boost.Format`

## iostreams

- `iostreams::file_descriptor_source`, 设备
- `iostreams::file_sink`, 设备
- `iostreams::file_source`, 设备
- `iostreams::file_source::close`, 设备
- `iostreams::file_source::is_open`, 设备
- `iostreams::filtering_istream`, 过滤器
- `iostreams::filtering_ostream`, 过滤器
- `iostreams::filtering_ostream::pop`, 过滤器
- `iostreams::filtering_ostream::push`, 过滤器
- `iostreams::filtering_stream::component`, 过滤器
- `iostreams::mapped_file_sink`, 设备
- `iostreams::mapped_file_source`, 设备
- `iostreams::mapped_file_source::data`, 设备
- `iostreams::never_close_handle`, 设备
- `iostreams::regex_filter`, 过滤器
- `iostreams::stream`, 设备
- `iostreams::zlib_compressor`, 过滤器
- `iostreams::zlib_decompressor`, 过滤器

## iota

- `iota`, `algorithm`, Boost.Algorithm
- `iota_n`, `algorithm`, Boost.Algorithm

## asio

- `io_service`, `asio`, I/O 服务与 I/O 对象
- `io_service_impl`, `asio::detail`, 平台特定 I/O 对象

## PropertyTree

- `iptree`, `property_tree`, Boost.PropertyTree

## Range Helpers

- `irange`, `Boost.Range`, 辅助类与函数
- `istream_range`, `Boost.Range`, 辅助类与函数

## mpi

- `irecv`, `mpi::communicator`, 异步数据交换
- `isend`, `mpi::communicator`, 异步数据交换

## Algorithms

- `is_any_of`, `algorithm`, Boost.StringAlgorithms
- `is_arithmetic`, Boost.TypeTraits
- `is_decreasing`, `algorithm`, Boost.Algorithm
- `is_digit`, `algorithm`, Boost.StringAlgorithms
- `is_directory`, `filesystem`, 文件与目录
- `is_floating_point`, Boost.TypeTraits
- `is_increasing`, `algorithm`, Boost.Algorithm
- `is_initialized`, `optional`, Boost.Optional
- `is_integral`, Boost.TypeTraits
- `is_in_range`, `log::expressions`, Boost.Log
- `is_linearized`, `circular_buffer`, Boost.CircularBuffer
- `is_lock_free`, `atomic`, Boost.Atomic
- `is_lower`, `algorithm`, Boost.StringAlgorithms
- `is_nil`, `uuids::uuid`, Boost.Uuid
- `is_partitioned`, `algorithm`, Boost.Algorithm
- `is_permutation`, `algorithm`, Boost.Algorithm



## I

- `is_reference`, `Boost.TypeTraits`, Boost.TypeTraits
- `is_regular_file`, `filesystem`, 文件与目录
- `is_same`, `Boost.TypeTraits`, Boost.TypeTraits
- `is_sorted`, `Boost.Range`, 算法
- `is_space`, `algorithm`, Boost.StringAlgorithms
- `is_symlink`, `filesystem`, 文件与目录
- `is_upper`, `algorithm`, Boost.StringAlgorithms
- `lexicographical_compare`, `algorithm`, Boost.StringAlgorithms
- `lexical_cast`, `Boost.LexicalCast`, Boost.LexicalCast

## Iterators

- `iterator`, `asio::ip::resolver`, 网络编程
- `iterator_range`, `Boost.Range`, 辅助类与函数
- `iterator_range`, `Boost.StringAlgorithms`, Boost.StringAlgorithms

## J

- `join`, `algorithm`, Boost.StringAlgorithms
- `join`, `thread`, 线程管理
- `join_all`, `thread`, 线程管理

## K

- `is_open`, `iostreams::file_source`, 设备
- `kernel`, `Boost.Chrono`, Boost.Chrono
- `kernel`, `Boost.Timer`, Boost.Timer
- `keys`, `Boost.Index`, Boost.Index

## L

- `lambda_if_then`, `Boost.Lambda`, Boost.Lambda
- `lambda_if_then_else`, `Boost.Lambda`, Boost.Lambda
- `lambda_if_then_else_return`, `Boost.Lambda`, Boost.Lambda
- `lambda_1`, `Boost.Lambda`, Boost.Lambda
- `lambda_2`, `Boost.Lambda`, Boost.Lambda
- `lambda_3`, `Boost.Lambda`, Boost.Lambda
- `last_write_time`, `filesystem`, 文件与目录
- `launch::async`, `Futures`, 未来与承诺
- `launch::deferred`, `Futures`, 未来与承诺
- `lazy evaluation`, `Boost.Xpressive`, Boost.Xpressive

## LC

- `LCID`, `Boost.Regex`, Boost.Regex

## L

- `less_than_comparable`, `Boost.Operators`, Boost.Operators
- `lexeme`, `spirit::qi`, 解析器
- `lines`, `iostreams::counter`, 过滤器
- `link_mode`, `intrusive`, Boost.Intrusive
- `list`, `fusion`, `Boost.Fusion`
- `list`, `intrusive`, `Boost.Intrusive`
- `listen`, `asio::ip::tcp::acceptor`, `网络编程`
- `listS`, `Boost.Graph`, `顶点与边`
- `list_base_hook`, `intrusive`, `Boost.Intrusive`
- `list_member_hook`, `intrusive`, `Boost.Intrusive`
- `list_of`, `assign`, `Boost.Assign`
- `list_of`, `bimaps`, `Boost.Bimap`
- `little_word`, `spirit::qi`, `解析器`
- `local`, `chrono::timezone`, `Boost.Chrono`
- `local_clock`, `log::attribute`, `Boost.Log`
- `local_date_time`, `local_time`, `区域时间`
- `local_day`, `gregorian::day_clock`, `日历日期`
- `local_time`, `local_time::local_date_time`, `区域时间`
- `local_time`, `posix_time::second_clock`, `位置无关的时间`
- `local_time`, `local_date_time`, `区域时间`
- `local_time`, `local_date_time::local_time`, `区域时间`
- `local_time`, `local_date_time::local_time_in`, `区域时间`
- `local_time`, `local_time_period`, `区域时间`
- `local_time`, `local_time_period::contains`, `区域时间`
- `local_time`, `local_time_period::intersection`, `区域时间`
- `local_time`, `local_time_period::merge`, `区域时间`
- `local_time`, `posix_time_zone`, `区域时间`
- `local_time`, `time_zone`, `区域时间`
- `local_time`, `time_zone_ptr`, `区域时间`
- `local_time_in`, `local_time::local_date_time`, `区域时间`
- `local_time_period`, `local_time`, `区域时间`
- `lock`, `Boost.Interprocess`, `同步`
- `lock`, `interprocess::named_mutex`, `同步`
- `lock`, `mutex`, `同步`
- `lock`, `weak_ptr`, `智能指针`
- `lockfree`, `allocator`, `Boost.Lockfree`
- `lockfree`, `capacity`, `Boost.Lockfree`
- `lockfree`, `fixed_sized`, `Boost.Lockfree`
- `lockfree`, `queue`, `Boost.Lockfree`
- `lockfree`, `queue::consume_all`, `Boost.Lockfree`
- `lockfree`, `queue::consume_one`, `Boost.Lockfree`
- `lockfree`, `queue::push`, `Boost.Lockfree`
- `lockfree`, `queue::reserve`, `Boost.Lockfree`
- `lockfree`, `spsc_queue`, `Boost.Lockfree`
- `lockfree`, `spsc_queue::consume_all`, `Boost.Lockfree`
- `lockfree`, `spsc_queue::consume_one`, `Boost.Lockfree`
- `lockfree`, `spsc_queue::pop`, `Boost.Lockfree`
- `lockfree`, `spsc_queue::push`, `Boost.Lockfree`
- `lockfree`, `stack`, `Boost.Lockfree`
- `lock_guard`, `Boost.Thread`, `同步`
- `log::attribute::local_clock`, `Boost.Log`
- `log::attributes::counter`, `Boost.Log`
- `log::attribute_name`, `Boost.Log`
- `log::attribute_name::extract`, `Boost.Log`
- `log::attribute_name::extract_or_default`, `Boost.Log`
- `log::attribute_name::extract_or_throw`, `Boost.Log`
- `log::attribute_value`, `Boost.Log`
- `log::attribute_value_set`, `Boost.Log`
- `log::attribute_value_set::attribute_values`, `Boost.Log`
- `log::core::add_global_attribute`, `Boost.Log`
- `log::core::add_sink`, `Boost.Log`
- `log::core::get`, `Boost.Log`
- `log::core::set_exception_handler`, `Boost.Log`
- `log::expressions::attr`, `Boost.Log`
- `log::expressions::or_default`, `Boost.Log`
- `log::expressions::format_date_time`, `Boost.Log`
- `log::expressions::is_range`, `Boost.Log`
- `log::expressions::message`, `Boost.Log`
- `log::expressions::stream`, `Boost.Log`
- `log::formatting_ostream`, `Boost.Log`
- `log::keywords::channel`, `Boost.Log`
- `log::make_exception_handler`, `Boost.Log`
- `log::make_exception_suppressor`, `Boost.Log`
- `log::record`, `Boost.Log`
- `log::record_view`, `Boost.Log`
- `log::record_view::attribute_values`, `Boost.Log`
- `log::sinks::asynchronous_sink`, `Boost.Log`
- `log::sinks::asynchronous_sink::flush`, `Boost.Log`
- `log::sinks::asynchronous_sink::set_filter`, `Boost.Log`
- `log::sinks::asynchronous_sink::set_formatter`, `Boost.Log`
- `log::sinks::file::as_file_name_composer`, `Boost.Log`
- `log::sinks::synchronous_sink`, Boost.Log
- `log::sinks::text_multifile_backend`, Boost.Log
- `log::sinks::text_multifile_backend::set_file_name_composer`, Boost.Log
- `log::sinks::text_ostream_backend`, Boost.Log
- `log::sinks::text_ostream_backend::add_stream`, Boost.Log
- `log::sources::channel_logger`, Boost.Log
- `log::sources::logger`, Boost.Log
- `log::visit`, Boost.Log
- `logger`, `log::sources`, Boost.Log
- `logic::indeterminate`, Boost.Tribool
- `logic::tribool`, Boost.Tribool
- `long_month_names`, `gregorian::date_facet`, 格式化输入输出
- `long_weekday_names`, `gregorian::date_facet`, 格式化输入输出
- `lower_bound`, `multi_index::ordered_non_unique`, Boost.MultiIndex

### M

- `make_absolute`, `filesystem::path`, 路径
- `make_array`, `serialization`, 优化的封装函数
- `make_bfs_visitor`, `Boost.Graph`, 算法
- `make_binary_object`, `serialization`, 优化的封装函数
- `make_error_code`, `system::errc`, Boost.System
- `make_exception_handler`, `log`, Boost.Log
- `make_exception_suppressor`, `log`, Boost.Log
- `make_optional`, `Boost.Optional`, Boost.Optional
- `make_pair`, `fusion`, 格式化输出
- `make_preferred`, `filesystem::path`, 路径
- `make_shared`, `Boost.SmartPointers`, 所有权
- `make_tuple`, `Boost.Tuple`, Boost.Tuple
- `make_tuple`, `fusion`, 格式化输出
- `make_unsigned`, `Boost.TypeTraits`, Boost.TypeTraits
- `malloc`, `object_pool`, `Boost.Pool`, Boost.Pool
- `malloc`, `simple_segregated_storage`, `Boost.Pool`, Boost.Pool
- `malloc`, `singleton_pool`, `Boost.Pool`, Boost.Pool
- `malloc_n`, `simple_segregated_storage`, `Boost.Pool`, Boost.Pool
- `managed_shared_memory`, `interprocess`, 托管共享内存
- `map`, `fusion`, Boost.Fusion
- `map`, `interprocess`, 托管共享内存
- `mapped_file_sink`, `iostreams`, 设备
- `mapped_file_source`, `iostreams`, 设备
- `mapped_region`, `interprocess`, 共享内存
- `mapS`, `Boost.Graph`, 顶点与边
- `map_list_of`, `assign`, Boost.Assign
- `max`, `random::mt19937`, Boost.Random
- `max_element`, `Boost.Range`, 算法
- `mean`, `accumulators::tag`, Boost.Accumulators
- `member`, `multi_index`, Boost.MultiIndex
- `member_hook`, `intrusive`, Boost.Intrusive
- `memory order`, `Boost.Atomic`, Boost.Atomic
- `memory_order_acquire`, `Boost.Atomic`, Boost.Atomic
- `memory_order_relaxed`, `Boost.Atomic`, Boost.Atomic
- `memory_order_release`, `Boost.Atomic`, Boost.Atomic
- `memory_order_seq_cst`, `Boost.Atomic`, Boost.Atomic
- `mem_fun`, `multi_index`, Boost.MultiIndex
- `merge`, `heap::binomial`, Boost.Heap
- `merge`, `local_time::local_period`, 依赖区域的时间
- `merge`, `posix_time::time_period`, 区域无关的时间
- `message`, `system::error_category`, Boost.System
- `microseconds`, `chrono`, Boost.Chrono
- `microsec_clock`, `posix_time`, 区域无关的时间
- `milliseconds`, `chrono`, Boost.Chrono
- `min`, `random::mt19937`, Boost.Random



- `minmax`, `Boost.MinMax`, Boost.MinMax
- `minmax_element`, `Boost.MinMax`, Boost.MinMax
- `minutes`, `chrono`, Boost.Chrono
- `minutes`, `posix_time::time_duration`, 区域无关的时间
- `mismatch`, `algorithm`, Boost.Algorithm
- `modify`, `Boost.MultiIndex`, Boost.MultiIndex
- `modify_data`, `bimaps::set_of`, Boost.Bimap
- `modify_key`, `bimaps::set_of`, Boost.Bimap
- `monotonic time`, `Boost.Chrono`, Boost.Chrono
- `month`, `gregorian::date`, 日历
- `months`, `gregorian`, 日历
- `month_iterator`, `gregorian`, 日历
- `month_type`, `gregorian::date`, 日历
- `mpi::all_reduce`, 集合数据交换
- `mpi::any_source`, 简单数据交换
- `mpi::broadcast`, 集合数据交换
- `mpi::communicator`, 简单数据交换
- `mpi::communicator::group`, 通信器
- `mpi::communicator::irecv`, 异步数据交换

## MPI API 参考

- `mpi::communicator::isend`, 异步数据交换
- `mpi::communicator::rank`, 简单数据交换
- `mpi::communicator::recv`, 简单数据交换
- `mpi::communicator::send`, 简单数据交换
- `mpi::communicator::size`, 简单数据交换
- `mpi::communicator::split`, 通信器
- `mpi::environment`, 简单数据交换
- `mpi::environment::abort`, 简单数据交换
- `mpi::environment::initialized`, 简单数据交换
- `mpi::environment::processor_name`, 简单数据交换
- `mpi::gather`, 集合数据交换
- `mpi::group`, 通信器
- `mpi::group::exclude`, 通信器
- `mpi::group::include`, 通信器
- `mpi::group::rank`, 通信器
- `mpi::reduce`, 集合数据交换
- `mpi::request`, 异步数据交换
- `mpi::request::cancel`, 异步数据交换
- `mpi::request::test`, 异步数据交换
- `mpi::scatter`, 集合数据交换
- `mpi::status`, 简单数据交换
- `mpi::status::source`, 简单数据交换
- `mpi::test_all`, 异步数据交换
- `mpi::test_any`, 异步数据交换
- `mpi::test_some`, 异步数据交换
- `mpi::wait_all`, 异步数据交换
- `mpi::wait_any`, 异步数据交换
- `mpi::wait_some`, 异步数据交换
- `MPICH`, Boost.MPI, 开发与运行时
- `mpiexec`, Boost.MPI, 开发与运行时
- `MPI_Finalize`, 简单数据交换
- `MPI_Init`, 简单数据交换
- `msm::back::state_machine`, Boost.MetaStateMachine
- `msm::back::state_machine::process_event`, Boost.MetaStateMachine
- `msm::front::euml::Char_`, Boost.MetaStateMachine
- `msm::front::euml::event_`, Boost.MetaStateMachine
- `msm::front::euml::fsm_`, Boost.MetaStateMachine
- `msm::front::euml::Int_`, Boost.MetaStateMachine
- `msm::front::euml::state_`, Boost.MetaStateMachine
- `msm::front::euml::String_`, Boost.MetaStateMachine
- `mt19937`, random, Boost.Random
- `multiset_of`, bimaps, Boost.Bimap
- `multitoken`, `program_options::value_semantic`, Boost.ProgramOptions
- `multi_array`, Boost.MultiArray, Boost.MultiArray
- `multi_array::array_view`, Boost.MultiArray
- `multi_array::origin`, Boost.MultiArray
- `multi_array::reference`, Boost.MultiArray
- `multi_array_ref`, Boost.MultiArray, Boost.MultiArray
- `multi_array_types::index_range`, Boost.MultiArray
- `multi_index::composite_key`, Boost.MultiIndex
- `multi_index::const_mem_fun`, Boost.MultiIndex
- `multi_index::global_fun`, Boost.MultiIndex
- `multi_index::hashed_non_unique`, Boost.MultiIndex
- `multi_index::hashed_unique`, Boost.MultiIndex
- `multi_index::identity`, Boost.MultiIndex
- `multi_index::indexed_by`, Boost.MultiIndex
- `multi_index::member`, Boost.MultiIndex
- `multi_index::mem_fun`, Boost.MultiIndex
- `multi_index::multi_index_container`, Boost.MultiIndex
- `multi_index::multi_index_container::get`, Boost.MultiIndex
- `multi_index::multi_index_container::nth_index`, Boost.MultiIndex
- `multi_index::ordered_non_unique`, Boost.MultiIndex
- `multi_index::ordered_non_unique::lower_bound`, Boost.MultiIndex
- `multi_index::ordered_non_unique::upper_bound`, Boost.MultiIndex
- `multi_index::random_access`, Boost.MultiIndex
- `multi_index::random_access::at`, Boost.MultiIndex
- `multi_index::random_access::operator[]`, Boost.MultiIndex
- `multi_index::sequenced`, Boost.MultiIndex
- `multi_index_container`, `multi_index`, Boost.MultiIndex
- `mutex` (concept), Boost.Thread, 同步线程
- `mutex`, Boost.Thread, 同步线程
- `mutex::lock`, 同步线程
- `mutex::try_lock`, 同步线程
- `mutex::unlock`, 同步线程
- `mutex_type`, `signals2::keywords`, 多线程

### N

- `name`, `system::error_category`, Boost.System
- `named_condition`, `interprocess`, 同步
- `named_mutex`, `interprocess`, 同步
- `named_recursive_mutex`, `interprocess`, 同步
- `nanoseconds`, `chrono`, Boost.Chrono
- `native path`, `Boost.Filesystem`, 路径
- `native`, `filesystem::path`, 路径
- `negative_overflow`, `numeric`, Boost.NumericConversion
- `never_close_handle`, `iostreams`, 设备
- `next`, `Boost.Utility`, Boost.Utility
- `next`, `fusion`, Boost.Fusion
- `next_weekday`, `date_time`, 日历日期
- `nil_generator`, `uuids`, Boost.Uuid
- `non-deterministic random number generator`, `Boost.Random`, Boost.Random
- `noncopyable`, `Boost.Utility`, Boost.Utility
- `none`, `dynamic_bitset`, Boost.DynamicBitset
- `none_of`, `algorithm`, Boost.Algorithm
- `none_of_equal`, `algorithm`, Boost.Algorithm
- `normal_distribution`, `random`, Boost.Random
- `notifier`, `program_options::value_semantic`, Boost.ProgramOptions
- `notify`, `program_options`, Boost.ProgramOptions
- `notify_all`, `condition_variable_any`, 同步线程
- `notify_all`, `interprocess::named_condition`, 同步
- `not_a_date_time`, `date_time`, 日历日期, 与无关的时间
- `no_locking`, `flyweights`, Boost.Flyweight
- `no_property`, `Boost.Graph`, 算法
- `no_tracking`, `flyweights`, Boost.Flyweight
- `NO_ZLIB`, `Boost.IOStreams`, 过滤器
- `nth_index`, `multi_index::multi_index_container`, Boost.MultiIndex
- `null_mutex`, `details::pool`, Boost.Pool
- `numeric::bad_numeric_cast`, Boost.NumericConversion
- `numeric::negative_overflow`, Boost.NumericConversion
- `numeric::positive_overflow`, Boost.NumericConversion
- `numeric_cast`, `Boost.NumericConversion`, Boost.NumericConversion
- `num_edges`, `Boost.Graph`, 顶点与边
- `num_slots`, `signals2::signal`, 信号
- `num_vertices`, `Boost.Graph`, 顶点与边

### O

- `object_handle`, `asio::windows`, 特定平台的 I/O
- `object_pool`, `Boost.Pool`, Boost.Pool
- `object_pool::construct`, `Boost.Pool`, Boost.Pool



- `object_pool::destroy`, `Boost.Pool`, Boost.Pool
- `object_pool::get_next_size`, `Boost.Pool`, Boost.Pool
- `object_pool::malloc`, `Boost.Pool`, Boost.Pool
- `object_pool::set_next_size`, `Boost.Pool`, Boost.Pool
- `offset_separator`, `Boost.Tokenizer`, Boost.Tokenizer
- `ofstream`, `filesystem`, 文件流
- `one_of`, `algorithm`, Boost.Algorithm
- `one_of_equal`, `algorithm`, Boost.Algorithm
- `on_tree`, `Boost.Graph`, 算法
- `on_time`, `asio::windows`, 特定平台的 I/O
- `on_error`, `filesystem`, 文件流
- `on_notify`, `interprocess`, 同步
- `on_`, Boost.Random
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `open_`, Boost.Algorithm
- `ordered_begin`, `heap::binomial_heap`, [Boost.Heap](https://part0031.html_TI1E2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `ordered_end`, `heap::binomial_heap`, [Boost.Heap](https://part0031.html_TI1E2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `ordered_free`, `singleton_pool`, [Boost.Pool](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `ordered_malloc`, `singleton_pool`, [Boost.Pool](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `ordered_non_unique`, `multi_index`, [Boost.MultiIndex](https://part0026.html_OPEK2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `origin`, `multi_array`, [Boost.MultiArray](https://part0033.html_VF2I2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `or_default`, `log::expressions::attribute_keyword`, [Boost.Log](https://part0112.html_3APV02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `out_edges`, `Boost.Graph`, [Vertices and Edges](https://part0049_split_001.html_boost.graph-vertices-and-edges)
- `overlapped_ptr`, `asio::windows`, [Platform-specific I/O Objects](https://part0057.html_1MBG22-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `owns_lock`, `unique_lock`, [Synchronizing Threads](https://part0083.html_2F4UM2-4acad2cb18c04a1fb9fdf66a8cc19f92)

### P

- `packaged_task`, `Boost.Thread`, [Futures and Promises](https://part0085.html_2H1VQ2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `packaged_task::get_future`, [Futures and Promises](https://part0085.html_2H1VQ2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `parallel computing`, `Boost.MPI`, [Development and Runtime](https://part0088.split_001.html_boost-mpi-development-runtime)
- `parameter::optional`, `Boost.Parameter`, [part0100.html_2VBO82-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parameter::parameters`, `Boost.Parameter`, [part0100.html_2VBO82-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parameter::required`, `Boost.Parameter`, [part0100.html_2VBO82-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parameter::value_type`, `Boost.Parameter`, [part0100.html_2VBO82-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parameter::void_`, `Boost.Parameter`, [part0100.html_2VBO82-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parameters`, `Boost.Parameter`, [part0100.html_2VBO82-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parent_path`, `filesystem::path`, [part0064.split_001.html_boost-filesystem-paths]
- `parse`, `spirit::qi`, [API](https://part0019_split_001.html_boost.spirit-api)
- `parsed_options`, `Boost.ProgramOptions`, [part0113.html_3BOFI2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parse_command_line`, `Boost.ProgramOptions`, [part0113.html_3BOFI2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parse_config_file`, `Boost.ProgramOptions`, [part0113.html_3BOFI2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `parse_environment`, `Boost.ProgramOptions`, [part0113.html_3BOFI2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `partially_ordered`, `Boost.Operators`, [part0129.html_3OI11-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `path`, `filesystem`, [part0064.split_001.html_boost-filesystem-paths]
- `path1`, `filesystem::filesystem_error`, [Files and Directories](https://part0065.html_1TKI2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `path2`, `filesystem::filesystem_error`, [Files and Directories](https://part0065.html_1TKI2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `path_type`, `property_tree::ptree`, [Boost.PropertyTree](https://part0040.html_164MG2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `phoenix::bind`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `phoenix::function`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `phoenix::if_`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `phoenix::placeholders::arg1`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `phoenix::placeholders::arg2`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `phoenix::placeholders::arg3`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `phoenix::ref`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `phoenix::val`, `Boost.Phoenix`, [https://part0076.html_28FAO2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `phrase_parse`, `spirit::qi`, [API](https://part0019_split_001.html_boost.spirit-api)
- `polymorphic_cast`, `Boost.Conversion`, [https://part0101.html_30A8Q-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `polymorphic_downcast`, `Boost.Conversion`, [https://part0101.html_30A8Q-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `pool_allocator`, `Boost.Pool`, [Boost.Pool](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `pop`, `iostams::filtering_ostream`, [Filters](https://part0063.html_1SJE2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `pop`, `lockfree::spsc_queue`, [Boost.Lockfree](https://part0087.html_2IV02-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `pop_back_and_dispose`, `intrusive::list`, [Boost.Intrusive](https://part0032.html_UGI02-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `positional`, `program_options::command_line`, [Boost.ProgramOptions](https://part0113.html_3BOFI2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `positional_options_description`, `Boost.ProgramOptions`, [https://part0113.html_3BOFI2-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `positive_overflow`, `Boost.Numeric`, [https://part0110.html_38STS1-4acad2cb18c04a1fb9fdf66a8cc19f2]
- `posix_time::from_iso_string`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::microsec_clock`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::ptime`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::ptime::date`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::ptime::time_of_day`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::second_clock`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::second_clock::local_time`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::second_clock::universal_time`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_duration`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_duration::hours`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_duration::minutes`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_duration::seconds`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_duration::total_seconds`, [Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)



- `posix_time::time_iterator`，[Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_period`，[Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_period::contains`，[Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_period::intersection`，[Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time::time_period::merge`，[Location-independent Times](https://part0070.html_2O7C2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `posix_time_time_zone`、`local_time`，[Location-dependent Times](https://part0071.html_23MNU2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `postskip`、`spirit::qi::skip_flag`，[API](https://part0019_split_001.html_boost.spirit-api)
- `predecessor_map`、`Boost.Graph`，[Algorithms](https://part0050.html_1FLS42-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `prior`、`Boost.Utility`，[Boost.Utility](https://part0126.html_3O56S2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `prior`、`fusion`，[Boost.Fusion](https://part0096.html_2RHM02-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `priority_queue`、`heap`，[Boost.Heap](https://part0031.html_TI1E2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `processor_name`、`mpi::environment`，[Simple Data Exchange](https://part0089.html_2KS222-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `process_cpu_clock`、`chrono`，[Boost.Chrono](https://part0073.html_25JP22-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `process_event`、`msm::back::state_machine`，Boost.MetaStateMachine
- `process_real_cpu_clock`、`chrono`，Boost.Chrono
- `process_system_cpu_clock`、`chrono`，Boost.Chrono
- `process_user_cpu_clock`、`chrono`，Boost.Chrono
- `program_options::collect_unrecognized`，Boost.ProgramOptions
- `program_options::command_line_parser`，Boost.ProgramOptions
- `program_options::command_line_parser::allow_unregistered`，Boost.ProgramOptions
- `program_options::command_line_parser::options`，Boost.ProgramOptions
- `program_options::command_line_parser::positional`，Boost.ProgramOptions
- `program_options::command_line_parser::run`，Boost.ProgramOptions
- `program_options::command_line_parser::style`，Boost.ProgramOptions
- `program_options::command_line_style::allow_slash_for_short`，Boost.ProgramOptions
- `program_options::error`，Boost.ProgramOptions
- `program_options::exclude_positional`，Boost.ProgramOptions
- `program_options::invalid_syntax`，Boost.ProgramOptions
- `program_options::notify`，Boost.ProgramOptions
- `program_options::options_description`，Boost.ProgramOptions
- `program_options::options_description::add`，Boost.ProgramOptions
- `program_options::options_description::add_options`，Boost.ProgramOptions
- `program_options::parsed_options`，Boost.ProgramOptions
- `program_options::parse_command_line`，Boost.ProgramOptions
- `program_options::parse_config_file`，Boost.ProgramOptions
- `program_options::parse_environment`，Boost.ProgramOptions
- `program_options::positional_options`，Boost.ProgramOptions
- `program_options::positional_options::add`，Boost.ProgramOptions
- `program_options::store`，Boost.ProgramOptions
- `program_options::value`，Boost.ProgramOptions
- `program_options::value_semantic`，Boost.ProgramOptions
- `program_options::value_semantic::composing`，Boost.ProgramOptions
- `program_options::value_semantic::default_value`，Boost.ProgramOptions
- `program_options::value_semantic::implicit_value`，Boost.ProgramOptions
- `program_options::value_semantic::multitoken`，Boost.ProgramOptions
- `program_options::value_semantic::notifier`，Boost.ProgramOptions
- `program_options::value_semantic::zero_tokens`，Boost.ProgramOptions
- `program_options::variables_map`，Boost.ProgramOptions
- `program_options::variables_map::count`，Boost.ProgramOptions
- `program_options::variable_value`，Boost.ProgramOptions
- `program_options::variable_value::as`，Boost.ProgramOptions
- `program_options::variable_value::value`，Boost.ProgramOptions
- `promise`（概念）、`Boost.Thread`，Futures and Promises
- `promise`、`Boost.Thread`，Futures and Promises
- `promise::get_future`，Futures and Promises
- `promise::set_value`，Futures and Promises
- `property map`、`Boost.Graph`，Algorithms
- `property`、`Boost.Graph`，Algorithms
- `property_tree::basic_ptree`，Boost.PropertyTree
- `property_tree::info_parser::read_info`，Boost.PropertyTree
- `property_tree::info_parser::write_info`，Boost.PropertyTree
- `property_tree::ini_parser::read_ini`，Boost.PropertyTree
- `property_tree::ini_parser::write_ini`，Boost.PropertyTree
- `property_tree::iptree`，Boost.PropertyTree
- `property_tree::json_parser::read_json`，Boost.PropertyTree
- `property_tree::json_parser::write_json`，Boost.PropertyTree
- `property_tree::ptree`，Boost.PropertyTree
- `property_tree::ptree::add_child`，Boost.PropertyTree
- `property_tree::ptree::begin`，Boost.PropertyTree
- `property_tree::ptree::end`，Boost.PropertyTree
- `property_tree::ptree::get`，Boost.PropertyTree
- `property_tree::ptree::get_child`，Boost.PropertyTree
- `property_tree::ptree::get_child_optional`，Boost.PropertyTree
- `property_tree::ptree::get_optional`，Boost.PropertyTree
- `property_tree::ptree::get_value`，Boost.PropertyTree
- `property_tree::ptree::path_type`，Boost.PropertyTree
- `property_tree::ptree::put`，Boost.PropertyTree
- `property_tree::ptree::put_child`，Boost.PropertyTree
- `property_tree::xml_parser::read_xml`，Boost.PropertyTree
- `property_tree::xml_parser::write_xml`，Boost.PropertyTree
- `pseudo-random number generator`、`Boost.Random`，Boost.Random
- `ptime`、`posix_time`，Location-independent Times
- `ptree`、`property_tree`，Boost.PropertyTree
- `ptr_back_inserter`、`ptr_container`，Boost.PointerContainer
- `ptr_back_insert_iterator`、`ptr_container`，Boost.PointerContainer
- `ptr_container::ptr_back_inserter`，Boost.PointerContainer
- `ptr_container::ptr_back_insert_iterator`，Boost.PointerContainer
- `ptr_container::ptr_front_inserter`，Boost.PointerContainer
- `ptr_container::ptr_inserter`，Boost.PointerContainer
- `ptr_deque`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_front_inserter`、`ptr_container`，Boost.PointerContainer
- `ptr_inserter`、`ptr_container`，Boost.PointerContainer
- `ptr_list`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_map`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_set`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_unordered_map`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_unordered_set`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_vector`、`Boost.PointerContainer`，Boost.PointerContainer
- `ptr_vector::back`，Boost.PointerContainer
- `pull_type`、`coroutines::coroutine`，Boost.Coroutine
- `purge_memory`、`singleton_pool`，Boost.Pool
- `push`、`assign`，Boost.Assign
- `push`、`heap::binomial_heap`，Boost.Heap
- `push`、`iostreams::filtering_ostream`，Filters
- `push`、`lockfree::queue`，Boost.Lockfree
- `push`、`lockfree::spsc_queue`，Boost.Lockfree
- `push_back`、`assign`，Boost.Assign
- `push_back`、`Boost.Range`，Algorithms
- `push_back`、`dynamic_bitset`，Boost.DynamicBitset
- `push_back`、`fusion`，Boost.Fusion
- `push_back`、`intrusive::list`，Boost.Intrusive
- `push_front`、`assign`，Boost.Assign
- `push_type`、`coroutines::coroutine`，Boost.Coroutine
- `put`、`property_tree::ptree`，Boost.PropertyTree
- `put_child`、`property_tree::ptree`，Boost.PropertyTree

### Q

- `query`、`asio::ip::tcp::resolver`，网络编程
- `queue`、`lockfree`，Boost.Lockfree

### R

- `RAII`、`Boost.ScopeExit`，Boost.ScopeExit
- `random::bernoulli_distribution`，Boost.Random
- `random::chi_squared_distribution`，Boost.Random
- `random::mt19937`，Boost.Random
- `random::mt19937::max`，Boost.Random
- `random::mt19937::min`，Boost.Random
- `random::mt19937::result_type`，Boost.Random



- `random::normal_distribution`, Boost.Random
- `random::random_device`, Boost.Random
- `random::uniform_int_distribution`, Boost.Random
- `random_access`, `multi_index`, Boost.MultiIndex
- `random_device`, `random`, Boost.Random
- `random_generator`, `uuids`, Boost.Uuid
- `random_shuffle`, Boost.Range 辅助类与函数
- `random_spanning_tree`, `Boost.Graph`, Algorithms
- `range`, `Boost.Range`, Algorithms
- `rank`, `mpi::communicator`, 简单数据交换
- `rank`, `mpi::group`, 通信器
- `read_info`, `property_tree::info_parser`, Boost.PropertyTree
- `read_ini`, `property_tree::ini_parser`, Boost.PropertyTree
- `read_json`, `property_tree::json_parser`, Boost.PropertyTree
- `read_write`, `interprocess`, 共享内存
- `read_xml`, `property_tree::xml_parser::read_xml`, Boost.PropertyTree
- `record`, `log`, Boost.Log
- `record_distances`, `Boost.Graph`, Algorithms
- `record_predecessors`, `Boost.Graph`, Algorithms
- `record_view`, `log`, Boost.Log
- `recursive_directory_iterator`, `filesystem`, 目录迭代器
- `recv`, `mpi::communicator`, 简单数据交换
- `reduce`, `mpi`, 集体数据交换
- `ref`, `Boost.Ref`, Boost.Ref
- `ref`, `phoenix`, Boost.Phoenix
- `ref`, `xpressive`, Boost.Xpressive
- `reference`, `multi_array`, Boost.MultiArray
- `regex`, `Boost.Regex`, Boost.Regex
- `regex::imbue`, Boost.Regex
- `regex_constants::format_literal`, Boost.Regex
- `regex_filter`, `iostreams`, 过滤器
- `regex_iterator`, `xpressive`, Boost.Xpressive
- `regex_match`, `Boost.Regex`, Boost.Regex
- `regex_match`, `xpressive`, Boost.Xpressive
- `regex_replace`, `Boost.Regex`, Boost.Regex
- `regex_replace`, `xpressive`, Boost.Xpressive
- `regex_search`, `Boost.Regex`, Boost.Regex
- `regex_search`, `xpressive`, Boost.Xpressive
- `regex_token_iterator`, `Boost.Regex`, Boost.Regex
- `regex_token_iterator`, `xpressive`, Boost.Xpressive
- `register_handle`, `asio::detail::win_iocp_io_service`, 特定平台的 I/O 对象
- `register_type`, `archive::text_iarchive`, 类层次结构对象的序列化
- `register_type`, `archive::text_oarchive`, 类层次结构对象的序列化
- `regular expression`, `Boost.Regex`, Boost.Regex
- `regular expression`, `xpressive`, Boost.Xpressive
- `relative_path`, `filesystem::path`, 路径
- `release`, `asio::windows::overlapped_ptr`, 特定平台的 I/O 对象
- `release`, `unique_lock`, 线程同步
- `release_memory`, `singleton_pool`, Boost.Pool
- `remove`, `interprocess::shared_memory_object`, 共享内存
- `remove_erase`, `Boost.Range`, 算法
- `remove_filename`, `filesystem::path`, 路径
- `remove_pointer`, `Boost.TypeTraits`, Boost.TypeTraits
- `remove_shared_memory_on_destroy`, `interprocess`, 共享内存
- `remove_all_copy`, `algorithm`, Boost.StringAlgorithms
- `replace_extension`, `filesystem::path`, 路径
- `replace_first_copy`, `algorithm`, Boost.StringAlgorithms
- `replace_head_copy`, `algorithm`, Boost.StringAlgorithms
- `replace_last_copy`, `algorithm`, Boost.StringAlgorithms
- `replace_nth_copy`, `algorithm`, Boost.StringAlgorithms
- `replace_tail_copy`, `algorithm`, Boost.StringAlgorithms
- `request`, `mpi`, 异步数据
- `required`, `parameter`, Boost.Parameter
- `reserve`, `lockfree::queue`, Boost.Lockfree
- `reset`, `scoped_array`, 独占所有
- `reset`, `scoped_ptr`, 独占所有
- `reset`, `shared_array`, 共享所有
- `reset`, `shared_ptr`, 共享所有
- `reset`, `thread_specific_ptr`, 线程本地存储
- `resize`, `dynamic_bitset`, Boost.DynamicBitset
- `resolver`, `asio::ip::tcp`, 网络编程
- `result_type`, `random::mt19937`, Boost.Random
- `resume`, `timer::cpu_timer`, Boost.Timer
- `root_directory`, `filesystem::path`, 路径
- `root_name`, `filesystem::path`, 路径
- `root_path`, `filesystem::path`, 路径
- `round`, `chrono`, Boost.Chrono
- `rule`, `spirit::qi`, 规则
- `run`, `asio::io_service`, I/O 服务与 I/O 对象
- `run`, `program_options::command_line_parser`, Boost.ProgramOptions

### S

- `scatter`, `mpi`, 集体数据交换
- `scoped_array`, `Boost.SmartPointers`, 独占所有
- `scoped_array::get`, 独占所有
- `scoped_array::operator bool`, 独占所有
- `scoped_array::operator[]`, 独占所有
- `scoped_array::reset`, 独占所有
- `scoped_ptr`, `Boost.SmartPointers`, 独占所有
- `scoped_ptr::get`, 独占所有
- `scoped_ptr::operator bool`, 独占所有
- `scoped_ptr`, 独占所有
- `scoped_ptr::reset`, 独占所有
- `scoped_thread`, `Boost.Thread`, 管理线程
- `scatter`, `mpi`, 集体数据交换
- `second`, `pair`, Boost.Tuple
- `seconds`, `chrono`, Boost.Chrono
- `seconds`, `posix_time::duration`, 位置无关
- `second`, `posix_time`, 位置无关
- `segment`, `Boost.interprocess`, 托管内存
- `selector`, `Boost.Graph`, 顶点与边
- `semaphore`, `Boost.interprocess`, 同步
- `send`, `mpi::communicator`, 简单数据交换
- `sequenced`, `multi_index`, Boost.MultiIndex
- `sequential consistency`, `Boost.Atomic`, Boost.Atomic
- `serialization::access`, 存档
- `serialization::base_object`, 类层次结构对象的序列化
- `serialization::make_array`, 优化封装函数
- `serialization::make_binary_object`, 优化封装函数
- `serialize`, `Boost.Serialization`, 存档
- `set`, `fusion`, Boost.Fusion
- `set`, `intrusive`, Boost.Intrusive
- `setS`, `Boost.Graph`, 顶点与边
- `set_exception_handler`, `log::core`, Boost.Log
- `set_factory`, `flyweights`, [Boost.Flyweight (权重重量模式)](https://part0120.html_3IE3G2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_file_name_composer`, `log::sinks::text_multifile_backend`, [Boost.Log](https://part0112.html_3APV02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_filter`, `log::sinks::asynchronous_sink`, [Boost.Log](https://part0112.html_3APV02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_formatter`, `log::sinks::asynchronous_sink`, [Boost.Log](https://part0112.html_3APV02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_member_hook`, `intrusive`, [Boost.Intrusive](https://part0032.html_UGI02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_next_size`, `object_pool`, [Boost.Pool](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_of`, `bimaps`, [Boost.Bimap](https://part0027.html_PNV62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `set_stack_size`, `thread::attributes`, [创建与管理线程 (Creating and Managing Threads)](https://part0082_split_001.html_boost.thread-management)
- `set_value`, `promise`, [Future 与 Promise (Futures and Promises)](https://part0085.html_2H1VQ2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `severity_logger`, `sources`, [Boost.Log](https://part0112.html_3APV02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared lock`, `Boost.Thread`, [线程同步 (Synchronizing Threads)](https://part0083.html_2F4UM2-4acad2cb18c04a1fb9df66a8cc19f92)
- `shared_array::get`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_array::operator bool`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_array::operator[]`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_array::reset`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_connection_block`, `signals2`, [连接 (Connections)](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_lock`, `Boost.Thread`, [线程同步 (Synchronizing Threads)](https://part0083.html_2F4UM2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_memory_object`, `interprocess`, [共享内存 (Shared Memory)](https://part0058_split_001.html_boost.interprocess)
- `shared_mutex`, `Boost.Thread`, [线程同步 (Synchronizing Threads)](https://part0083.html_2F4UM2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_ptr`, `Boost.SmartPointers`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_ptr::get`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_ptr::operator bool`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_ptr::operator*`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_ptr::operator->`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `shared_ptr::reset`, [共享所有权 (Shared Ownership)](https://part0007.html_6LJU2-4acad2cb18c04a1fb9fdf66a8cc19f92)



- `shutdown`, `asio::ip::socket`, [网络编程（Network programming）](https://part0055.html_1KEEU2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `signal`, `signals2`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::connection`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::connection::disconnect`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::dummy_mutex`, [多线程（Multithreading）](https://part0023.html_3L9L61-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::keywords::mutex_type`, [多线程（Multithreading）](https://part0023.html_3L9L61-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::optional_last_value`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::shared_connection_block`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::shared_connection_block::block`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::shared_connection_block::blocking`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::shared_connection_block::unblock`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::signal`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::signal::connect`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::signal::disconnect`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::signal::disconnect_all_slots`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::signal::empty`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::signal::num_slots`, [信号（Signals）](https://part0121_split_001.html_boost.signals2)
- `signals2::signal::slot_type::track`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::signal::slot_type::foreign`, [连接（Connections）](https://part0122.html_3KB4K2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::signal_type`, [多线程（Multithreading）](https://part0023.html_3L9L61-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signals2::signal_type::type`, [多线程（Multithreading）](https://part0023.html_3L9L61-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `signal_type`, [多线程（Multithreading）](https://part0023.html_3L9L61-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple segregated storage`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple_segregated_storage`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple_segregated_storage::add_block`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple_segregated_storage::free`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple_segregated_storage::free_n`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple_segregated_storage::malloc`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `simple_segregated_storage::malloc_n`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool::free`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool::malloc`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool::ordered_free`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool::ordered_malloc`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool::purge_memory`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `singleton_pool::release_memory`, [Boost.Pool（Boost.Pool）](https://part0011.html_AFM62-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `size`, `circular_buffer`, [Boost.CircularBuffer（Boost.CircularBuffer）](https://part0030.html_SJGS2-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `size`, `dynamic_bitset`, [Boost.DynamicBitset（Boost.DynamicBitset）](https://part0041.html_173721-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `size`, `fusion`, [Boost.Fusion（Boost.Fusion）](https://part0096.html_2RHM02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `size`, `intrusive::list`, [Boost.Intrusive（Boost.Intrusive）](https://part0032.html_UGI02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `size`, `mpi::communicator`, [简单数据交换（Simple Data Exchange）](https://part0089.html_2KS22-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `size`, `uuids::uuid`, [Boost.Uuid（Boost.Uuid）](https://part0118.html_3GH2C-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `sleep_for`, `this_thread`, [创建与管理线程（Creating and Managing Threads）](https://part0082_split_001.html_boost.thread-management)
- `slist`, `container`, [Boost.Container（Boost.Container）](https://part0034.html_10DJ4-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `slist`, `intrusive`, [Boost.Intrusive（Boost.Intrusive）](https://part0032.html_UGI02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `smatch`, `Boost.Regex`, [Boost.Regex（Boost.Regex）](https://part0016.html_F8902-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `smessage`, `log::expressions`, [Boost.Log](https://part0112.html_3APV02-4acad2cb18c04a1fb9fdf66a8cc19f92)
- `socket`, `asio::ip::tcp`, [网络编程（Network programming）](https://part0055.html_1KEEU2-4acad2cb18c04a1fb9fdf66a8cc19f2)
- `space_type`, `spirit::ascii`, 规则
- `spawn`, `asio`, 协程
- `spirit::ascii::digit`, API
- `spirit::ascii::space`, API
- `spirit::ascii::space_type`, 规则
- `spirit::qi::big_word`, 解析器
- `spirit::qi::bool_`, 解析器
- `spirit::qi::byte_`, 解析器
- `spirit::qi::double_`, 解析器
- `spirit::qi::eol`, 解析器
- `spirit::qi::float_`, 解析器
- `spirit::qi::grammar`, 语法
- `spirit::qi::int_`, 解析器
- `spirit::qi::lexeme`, 解析器
- `spirit::qi::little_word`, 解析器
- `spirit::qi::parse`, API
- `spirit::qi::phrase_parse`, API
- `spirit::qi::rule`, 规则
- `spirit::qi::skip_flag::dont_postskip`, API
- `spirit::qi::skip_flag::postskip`, API
- `spirit::qi::word`, 解析器
- `split`, `algorithm`, Boost.StringAlgorithms
- `split`, `mpi::communicator`, 通信器
- `spsc_queue`, `lockfree`, Boost.Lockfree
- `sregex`, `xpressive`, Boost.Xpress
- `stable_vector`, `container`, Boost.Container
- `stack`, `lockfree`, Boost.Lockfree
- `start`, `timer::cpu_timer`, Boost.Timer
- `starts_with`, `algorithm`, Boost.StringAlgorithms
- `state_`, `msm::front::euml`, Boost.MetaStateMachine
- `state_machine`, `msm::back`, Boost.MetaStateMachine
- `static_vector`, `container`, Boost.Container
- `static_visitor`, `Boost.Variant`, Boost.Variant
- `status`, `filesystem`, 文件和目录
- `status`, `mpi`, 简单数据
- `steady_clock`, `chrono`, Boost.Chrono
- `steady_timer`, `asio`, I/O 服务和 I/O 对象
- `stem`, `filesystem::path`, 路径
- `stop`, `timer::cpu_timer`, Boost.Timer
- `store`, `atomic`, Boost.Atomic
- `store`, `program_options`, Boost.ProgramOptions
- `stream`, `Boost.IOStreams`, Boost.IOStreams
- `stream`, `iostreams`, 设备
- `stream`, `log::expressions`, Boost.Log
- `stream_descriptor`, `asio::posix`, 平台特定 I/O 对象
- `string`, `filesystem::path`, 路径
- `string`, `interprocess`, 托管共享内存
- `String_`, `msm::front::euml`, Boost.MetaStateMachine
- `string_generator`, `uuids`, Boost.Uuid
- `string_ref`, `Boost.Utility`, Boost.Utility
- `style`, `program_options::command_line`, Boost.ProgramOptions
- `sub_match`, `Boost.Regex`, Boost.Regex
- `sub_range`, `Boost.Range`, 辅助类和函数
- `swap`, `Boost.Swap`, Boost.Swap
- `swap`, `uuids::uuid`, Boost.Uuid
- `symbol_format`, `chrono`, Boost.Chrono
- `symlink_status`, `filesystem`, 文件和目录
- `synchronous_sink`, `log::sinks`, Boost.Log
- `system`, `timer::times`, Boost.Timer



- `system::errc::make_error_code`, Boost.System
- `system::error_category`, Boost.System
- `system::error_category::message`, Boost.System
- `system::error_category::name`, Boost.System
- `system::error_code`, Boost.System
- `system::error_code::category`, Boost.System
- `system::error_code::default_error_condition`, Boost.System
- `system::error_code::value`, Boost.System
- `system::error_condition`, Boost.System
- `system::error_condition::category`, Boost.System
- `system::error_condition::value`, Boost.System
- `system::generic_category`, Boost.System
- `system::system_category`, Boost.System
- `system::system_error`, Boost.System
- `system_category`, `system`, Boost.System
- `system_clock`, `chrono`, Boost.Chrono
- `system_error`, `system`, Boost.System

### T

- `tag`, `Boost.Exception`, Boost.Exception
- `tag`, `Boost.Flyweight`, Boost.Flyweight
- `tag`, `Boost.Graph`, 算法
- `tag`, `Boost.MPI`, 简单数据
- `tag`, `Boost.Pool`, Boost.Pool
- `test`, `mpi::request`, 异步数据交换
- `test_all`, `mpi`, 异步数据交换
- `test_any`, `mpi`, 异步数据交换
- `test_some`, `mpi`, 异步数据交换
- `text_iarchive`, `archive`, 存档
- `text_multifile_backend`, `log::sinks`, Boost.Log
- `text_oarchive`, `archive`, 存档
- `text_ostream_backend`, `log::sinks`, Boost.Log
- `this_`, `Boost.ScopeExit`, Boost.ScopeExit
- `this_thread::disable_interruption`, 创建与管理线程
- `this_thread::get_id`, 创建与管理线程
- `this_thread::sleep_for`, 创建与管理线程
- `thread local storage`, `Boost.Thread`, 线程本地存储
- `thread`, `Boost.Thread`, 创建与管理线程
- `thread::attributes`, 创建与管理线程
- `thread::attributes::set_stack_size`, 创建与管理线程
- `thread::detach`, 创建与管理线程
- `thread::hardware_concurrency`, 创建与管理线程
- `thread::interrupt`, 创建与管理线程
- `thread::join`, 创建与管理线程
- `thread_clock`, `chrono`, Boost.Chrono
- `thread_group`, `Boost.Thread`, 创建与管理线程
- `thread_group::join_all`, 创建与管理线程
- `thread_interrupted`, `Boost.Thread`, 创建与管理线程
- `thread_specific_ptr`, `Boost.Thread`, 线程本地存储
- `thread_specific_ptr::get`, 线程本地存储
- `thread_specific_ptr::operator*`, 线程本地存储
- `thread_specific_ptr::operator->`, 线程本地存储
- `thread_specific_ptr::reset`, 线程本地存储
- `tie`, `Boost.Tuple`, Boost.Tuple
- `tier`, `Boost.Tuple`, Boost.Tuple
- `timed_lock`, `interprocess::interprocess_mutex`, 同步
- `timed_lock`, `interprocess::named_mutex`, 同步
- `timed_mutex`, `Boost.Thread`, 同步线程
- `timed_mutex::try_lock`, `Boost.Thread`, 同步线程
- `timer::auto_timer`, `Boost.Timer`, Boost.Timer
- `timer::cpu_timer`, `Boost.Timer`, Boost.Timer
- `timer::cpu_timer::elapsed`, `Boost.Timer`, Boost.Timer
- `timer::cpu_timer::format`, `Boost.Timer`, Boost.Timer
- `timer::cpu_timer::resume`, `Boost.Timer`, Boost.Timer
- `timer::cpu_timer::start`, `Boost.Timer`, Boost.Timer
- `timer::cpu_timer::stop`, `Boost.Timer`, Boost.Timer
- `timer::times`, `Boost.Timer`, Boost.Timer
- `timer::times::clear`, `Boost.Timer`, Boost.Timer
- `timer::times::system`, `Boost.Timer`, Boost.Timer
- `timer::times::user`, `Boost.Timer`, Boost.Timer
- `timer::times::wall`, `Boost.Timer`, Boost.Timer
- `times`, `timer`, Boost.Timer
- `time_duration`, `posix_time`, 位置无关的时间
- `time_facet`, `date_time`, 格式化输入与输出
- `time_fmt`, `chrono`, Boost.Chrono
- `time_input_facet`, `date_time`, 格式化输入与输出
- `time_iterator`, `posix_time`, 位置无关的时间
- `time_of_day`, `posix_time::ptime`, 位置无关的时间
- `time_period`, `posix_time`, 位置无关的时间
- `time_point`, `chrono`, Boost.Chrono
- `time_point_cast`, `chrono`, Boost.Chrono
- `time_zone`, `local_time`, 依赖位置的时间
- `time_zone_ptr`, `local_time`, 依赖位置的时间
- `TLS (see thread local storage, Boost.Thread)`
- `tokenize`, `adaptors`, 适配器
- `tokenizer`, `Boost.Tokenizer`, Boost.Tokenizer
- `tokenizer::begin`, `Boost.Tokenizer`, Boost.Tokenizer
- `tokenizer::end`, `Boost.Tokenizer`, Boost.Tokenizer
- `top`, `heap::binomial_heap`, Boost.Heap
- `total_seconds`, `posix_time::time_duration`, 位置无关的时间
- `to_adapter`, `Boost.Assign`, Boost.Assign
- `to_lower`, `algorithm`, Boost.StringAlgorithms
- `to_lower_copy`, `algorithm`, Boost.StringAlgorithms
- `to_string`, `uuids`, Boost.Uuid
- `to_time_t`, `chrono::system_clock`, Boost.Chrono
- `to_upper`, `algorithm`, Boost.StringAlgorithms
- `to_upper_copy`, `algorithm`, Boost.StringAlgorithms
- `to_wstring`, `uuids`, Boost.Uuid
- `track`, `signals2::signal::slot_type`, 连接
- `track_foreign`, `signals2::signal::slot_type`, 连接
- `transition table`, `Boost.MetaStateMachine`, Boost.MetaStateMachine
- `translators`, `Boost.PropertyTree`, Boost.PropertyTree
- `tribool`, `logic`, Boost.Tribool
- `trim_copy`, `algorithm`, Boost.StringAlgorithms
- `trim_copy_if`, `algorithm`, Boost.StringAlgorithms
- `trim_left_copy`, `algorithm`, Boost.StringAlgorithms
- `trim_left_copy_if`, `algorithm`, Boost.StringAlgorithms
- `trim_right_copy`, `algorithm`, Boost.StringAlgorithms
- `trim_right_copy_if`, `algorithm`, Boost.StringAlgorithms
- `true_type`, `Boost.TypeTraits`, Boost.TypeTraits
- `truncate`, `interprocess::shared_memory_object`, 共享内存
- `try_lock`, `interprocess::interprocess_mutex`, 同步
- `try_lock`, `interprocess::named_mutex`, 同步
- `try_lock`, `mutex`, 线程同步
- `try_lock_for`, `timed_mutex`, 线程同步
- `try_lock_for`, `unique_lock`, 线程同步
- `try_to_lock`, `Boost.Thread`, 线程同步
- `tuple`, `Boost.Tuple`, Boost.Tuple
- `tuple`, `fusion`, Boost.Fusion
- `tuple::get`, Boost.Tuple
- `tuple_list_of`, `assign`, Boost.Assign
- `type`, `any`, Boost.Any
- `type`, `signals2::signal_type`, 多线程

### U

- `uint64_t`, `Boost.Integer`, Boost.Integer
- `UINT8_C`, `Boost.Integer`, Boost.Integer
- `uintmax_t`, `Boost.Integer`, Boost.Integer
- `uint_fast16_t`, `Boost.Integer`, Boost.Integer
- `uint_least32_t`, `Boost.Integer`, Boost.Integer
- `unblock`, `signals2::shared_connection`, 连接
- `unconstrained_set_of`, `bimaps`, Boost.Bimap
- `undirected`, `Boost.Graph`, 顶点与边
- `unhex`, `algorithm`, Boost.Algorithm
- `uniform_int_distribution`, `random`, Boost.Random
- `unique_lock`, `Boost.Thread`, 线程同步
- `unique_lock::owns_lock`, 线程同步
- `unique_lock::release`, 线程同步
- `unique_lock::try_lock_for`, 线程同步
- `universal_day`, `gregorian::day_clock`, 日历
- `universal_time`, `posix_time::second_clock`, 位置无关时间
- `unlock`, `interprocess::named_mutex`, 同步
- `unlock`, `mutex`, 线程同步
- `unordered_map`, `Boost.Unordered`, Boost.Unordered
- `unordered_multimap`, `Boost.Unordered`, Boost.Unordered
- `unordered_multiset`, `Boost.Unordered`, Boost.Unordered
- `unordered_multiset_of`, `bimaps`, Boost.Bimap
- `unordered_set Boost.Unordered`, Boost.Unordered
- `unordered_set`, `intrusive`, Boost.Intrusive
- `unordered_set_of`, `bimaps`, Boost.Bimap
- `update`, `heap::binomial_heap`, Boost.Heap
- `upper_bound`, `multi_index::ordered_unique`, Boost.MultiIndex
- `user space`, `Boost.Chrono`, Boost.Chrono
- `user space`, `Boost.Timer`, Boost.Timer
- `user`, `timer::times`, Boost.Timer
- `use_service`, `asio`, 平台特定 I/O
- `utc`, `chrono::timezone`, Boost.Chrono
- `UUID`, `Boost.Uuid`, Boost.Uuid
- `uuid`, `bimaps`, Boost.Bimap
- `uuid`, `Boost.Uuid`, Boost.Uuid
- `uuid::random`, `Boost.Uuid`, Boost.Uuid
- `uuid::generator`, `Boost.Uuid`, Boost.Uuid
- `uuid::to_string`, `Boost.Uuid`, Boost.Uuid
- `uuid::to_wstring`, `Boost.Uuid`, Boost.Uuid
- `uuid::begin`, `Boost.Uuid`, Boost.Uuid
- `uuid::end`, `Boost.Uuid`, Boost.Uuid
- `uuid::is_nil`, `Boost.Uuid`, Boost.Uuid
- `uuid::size`, `Boost.Uuid`, Boost.Uuid
- `uuid::swap`, `Boost.Uuid`, Boost.Uuid
- `uuid::variant`, `Boost.Uuid`, Boost.Uuid
- `uuid::version`, `Boost.Uuid`, Boost.Uuid

### V

- `val`, `phoenix`, Boost.Phoenix
- `value`, `program_options`, Boost.ProgramOptions
- `value`, `program_options::variable_value`, Boost.ProgramOptions
- `value`, `system::error_code`, Boost.System
- `value`, `system::error_condition`, Boost.System
- `values`, `adaptors`, 适配器
- `value_semantic`, `program_options`, Boost.ProgramOptions
- `value_type`, `parameter`, Boost.Parameter
- `variables_map`, `program_options`, Boost.ProgramOptions



- `variable_value`，`program_options`，Boost.ProgramOptions
- `variance`，`accumulators::tag`，Boost.Accumulators
- `variant`，`Boost.Variant`，Boost.Variant
- `variant`，`uuids::uuid`，Boost.Uuid
- `vecS`，`Boost.Graph`，顶点与边
- `vector`，`fusion`，Boost.Fusion
- `vector`，`interprocess`，托管共享内存
- `vector_of`，`bimaps`，Boost.Bimap
- `version`，`uuids::uuid`，Boost.Uuid
- `vertex_descriptor`，`adjacency_list`，顶点与边
- `vertex_iterator`，`adjacency_list`，顶点与边
- `vertices`，`Boost.Graph`，顶点与边
- `view`，`Boost.Fusion`，Boost.Fusion
- `view`，`Boost.MultiArray`，Boost.MultiArray
- `visit`，`log`，Boost.Log
- `visitor`，`Boost.Graph`，算法
- `void_`，`parameter`，Boost.Parameter

### W

- `w32_regex_traits`，`Boost.Regex`，Boost.Regex
- `wait`，`asio::steady_timer`，I/O 服务与 I/O 对象
- `wait`，`condition_variable_any`，线程同步
- `wait`，`interprocess::named_condition`，同步
- `wait_all`，`mpi`，异步数据交换
- `wait_any`，`mpi`，异步数据交换
- `wait_some`，`mpi`，异步数据交换
- `wall`，`timer::times`，Boost.Timer
- `wcregex`，`xpressive`，Boost.Xpressive
- `weak_ptr`，`Boost.SmartPointers`，特殊智能指针
- `weak_ptr::lock`，特殊智能指针
- `weeks`，`gregorian`，日期
- `week_iterator`，`gregorian`，日期
- `weight_map`，`Boost.Graph`，算法
- `windows_shared_memory`，`interprocess`，共享内存
- `win_iocp_io_service`，`asio::detail`，特定平台的 I/O 对象
- `word`，`spirit::qi`，解析器
- `write_info`，`property_tree::info_parser`，Boost.PropertyTree
- `write_ini`，`property_tree::ini_parser`，Boost.PropertyTree
- `write_json`，`property_tree::json_parser`，Boost.PropertyTree
- `write_xml`，`property_tree::xml_parser`，Boost.PropertyTree
- `wsregex`，`xpressive`，Boost.Xpressive
- `wstring`，`filesystem::path`，路径

### X

- `xpressive::cregex`，Boost.Xpressive
- `xpressive::ref`，Boost.Xpressive
- `xpressive::regex_iterator`，Boost.Xpressive
- `xpressive::regex_match`，Boost.Xpressive
- `xpressive::regex_replace`，Boost.Xpressive
- `xpressive::regex_search`，Boost.Xpressive
- `xpressive::regex_token_iterator`，Boost.Xpressive
- `xpressive::sregex`，Boost.Xpressive
- `xpressive::sregex::compile`，Boost.Xpressive
- `xpressive::wcregex`，Boost.Xpressive
- `xpressive::wsregex`，Boost.Xpressive
- `xpressive::_`，Boost.Xpressive
- `xpressive::_s`，Boost.Xpressive
- `xpressive::_w`，Boost.Xpressive

### Y

- `year`，`gregorian::date`，日期
- `years`，`gregorian`，日期
- `year_iterator`，`gregorian`，日期

### Z

- `zero_tokens`，`program_options::value_semantic`，Boost.ProgramOptions
- `zlib_compressor`，`iostreams`，过滤器
- `zlib_decompressor`，`iostreams`，过滤器
- `ZLIB_LIBPATH`，`Boost.IOStreams`，过滤器
- `ZLIB_SOURCE`，`Boost.IOStreams`，过滤器
