
`unique_ptr` 适用于存储动态分配的旧 C 风格数组。例如，以下示例创建了一个持有 10 个整数的动态分配 C 风格数组的 `unique_ptr`：

```cpp
auto myVariableSizeArray = make_unique<int[]>(10);
```

尽管可以使用 `unique_ptr` 存储动态分配的 C 风格数组，但推荐使用 STL 容器，如 `std::array` 或 `std::vector`。

默认情况下，`unique_ptr` 使用标准的 `new` 和 `delete` 操作符来分配和释放内存。你可以如下更改这种行为：

```cpp
int* malloc_int(int value)
{
    int* p = (int*)malloc(sizeof(int));
    *p = value;
    return p;
}
int main() 
{
    auto deleter = [] (int* p){ free(p); };
    unique_ptr<int, decltype(deleter)> mySmartPtr(malloc_int(42), deleter);
    return 0;
}
```

这段代码使用 `malloc_int()` 为整数分配内存。`unique_ptr` 通过调用命名的 lambda 表达式 `deleter` 来释放内存，该表达式使用了标准的 `free()` 函数。如所述，在 C++ 中你不应该使用 `malloc()` 而应该使用 `new`。然而，`unique_ptr` 的这一特性对于管理内存以外的资源非常有用。

引用计数的 `shared_ptr` 类表现如所示。然而，根据 C++ 标准，这是正确的行为。你不应该像之前的 `doubleDelete()` 函数中那样使用 `shared_ptr` 来创建两个指向同一个对象的 `shared_ptr`。相反，你应该使用 `make_shared()`，并使用拷贝构造函数来创建拷贝：

```cpp
void noDoubleDelete() {
    auto smartPtr1 = make_shared<Nothing>();
    shared_ptr<Nothing> smartPtr2(smartPtr1);
}
```

这段代码的输出是：

```
Nothing::Nothing()
Nothing::~Nothing()
```

尽管有两个 `shared_ptr` 指向同一个对象，`Nothing` 对象也只会被销毁一次。记住 `unique_ptr` 是不是引用计数的。事实上，`unique_ptr` 不允许你在 `noDoubleDelete()` 函数中使用拷贝构造函数。

> 注意：如果你的程序通过拷贝、赋值或按值传递智能指针作为函数参数来使用智能指针，那么 `shared_ptr` 是完美的解决方案。

如果你需要编写像之前的 `doubleDelete()` 函数中的代码，你将需要实现自己的智能指针以防止双重删除。但是，建议使用标准的 `shared_ptr` 模板来共享资源。避免使用 `doubleDelete()` 函数中的代码，而改用拷贝构造函数：

```cpp
shared_ptr<Nothing> smartPtr2(smartPtr1);
```

## 移动语义

`shared_ptr` 和 `unique_ptr` 都支持第 10 章中讨论的移动语义，以提高它们的效率。正因如此，从函数返回 `shared_ptr` 或 `unique_ptr` 是高效的。例如，你可以编写以下 `func()` 函数并像 `main()` 中演示那样使用它：

```cpp
// 为了简洁，这里显示了 Simple 的定义
shared_ptr<Simple> func() {
    auto ptr = make_shared<Simple>();
    // 对 ptr 进行一些操作...
    return ptr;
}
int main() {
    shared_ptr<Simple> mySmartPtr = func();
    return 0;
}
```

这是高效的，因为 C++ 会在 `func()` 的返回语句上自动调用 `std::move()`，从而触发 `shared_ptr` 的移动语义。如果你使用 `unique_ptr`，情况也是一样。`unique_ptr` 不支持标准的拷贝赋值运算符和拷贝构造函数，但它支持移动赋值运算符和移动构造函数，这解释了为什么你可以从函数返回 `unique_ptr`。

看以下 `unique_ptr` 语句：

```cpp
auto p1 = make_unique<int>(24);
unique_ptr<int> p2 = p1; // 错误：无法编译
unique_ptr<int> p3 = move(p1); // 确
```

定义 `p2` 的行将无法编译，因为它尝试使用拷贝构造函数，而 `unique_ptr` 不可用该函数。`std::move()` 的定义（定义在 `<utility>` 头文件中，见第 10 章）用于触发 `unique_ptr` 的移动构造函数。在 `p3` 创建后，它将变为 `nullptr`，你只能通过 `p3` 访问整数 24；所有权已从 `p1` 移动到 `p3`。

## weak_ptr

C++ 中还有一个与 `shared_ptr` 相关的类，叫做 `weak_ptr`。`weak_ptr` 可以包含一个指向 `shared_ptr` 管理的内存的引用。`weak_ptr` 不拥有内存，因此当 `shared_ptr` 超出范围时，不会阻止销毁指向的内存；它可以判断内存是否已由关联的 `shared_ptr` 或另一个 `weak_ptr` 参数释放。`weak_ptr` 的构造需要一个 `shared_ptr`。要访问存储在 `weak_ptr` 中的指针，必须将其转换为 `shared_ptr`。有两种方法可以：

- 在 `weak_ptr` 实例上使用 `lock()` 方法，它返回一个 `shared_ptr`，或
- 创建一个新的 `shared_ptr` 实例，并将 `weak_ptr` 作为参数传递给 `shared_ptr` 构造函数。

在这两种情况下，如果与 `weak_ptr` 关联的 `shared_ptr` 已经被释放，这个新的 `shared_ptr` 将是 `nullptr`。

## 内存陷阱

很难确定导致内存相关错误的具体情况。每个内存泄漏或无效指针都有其细微差别。解决内存问题没有万妙药，但有几种常见的问题类型以及一些你可以用来检测和解决它们的工具。

### 字符串分配不足

C 风格字符串最常见的问题是程序员未能分配额外的字符。这发生在程序员假设一个固定大小时。在大多数情况下，这是由于字符串没有正确终止。以下函数演示了这个问题：

```cpp
void fillWithM(char* inStr) {
    int i = 0;
    while (inStr[i] != '\0') {
        inStr[i] = 'm';
    }
}
```

有三种解决方法，按偏好程度从高到低排序：

1. 使用 C++ 字符串，它们管理所有的内存。
2. 使用 `vector` 等更高级构造结构代替 C 风格字符串。
3. 确保缓冲区足够容纳数据。

### 访问越界内存

如果将一个未正确终止的字符串交给此函数，内存被覆盖只是时间问题。考虑一下如果程序的内存突然被 'm' 覆盖会发生什么。

```cpp
char buffer[1024] = {};
while (true) {
  char* nextChunk = getData();
  if (nextChunk != nullptr) {
    break;
  } else {
    strcat(buffer, nextChunk); // Bug！
  }
  delete nextChunk;
}
```

导致写入数组末尾的错误通常被称为缓冲区溢出。这些漏洞已被多个著名的恶意软件利用，例如病毒和蠕虫。狡猾的黑客可以利用覆盖内存的部分向运行中的程序注入代码。许多内存检查工具可以检测缓冲区溢出。此外，使用 C++ 字符串和 vector 等现代构造可以防止许多与 C 风格字符串相关的错误。

> 警告避免使用提供任何保护的旧 C 风格字符串和数组。使用现代且安全的构造，如管理内存的 C++ 字符串和 vector。

## 内存泄漏

寻找和修复内存泄漏可能是 C 或 C++ 编程中最令人沮丧的部分之一。内存泄漏发生在你分配内存但忘记释放时。当你开始注意到程序在运行时消耗越来越多的内存时，它就存在内存泄漏。起初，这似乎是粗心编程的结果，本可以避免。毕竟，如果你写的每个类中每个 `new` 都有对应的 `delete`，就不应该有内存泄漏吗？实际上，事实并非如此。在以下代码中，`Simple` 类在实际代码中编写了良好的删除逻辑，这里的 `Simple` 类实现仅用于演示目的。在实际中，你应该使 `MintPtr` 成为 `unique_ptr`。

当调用 `doSomething()` 时，`outSimple` 指针指向另一个 `Simple` 对象而没有删除它。`doSomething()` 函数故意不删除对象以演示内存泄漏。一旦丢失了对象的指针，就几乎无法删除它。

```cpp
class Simple
public:
    Simple( MintPtr = new int(); );
    virtual ~Simple() { delete mintPtr; }
    void setPtr(int inInt) { *mintPtr = inInt; }
};
```

# 常见内存陷阱 | 737

private:

```
int* mIntPtr;
};
void doSomething(Simple*&outSimplePtr)
{
    outSimplePtr = new Simple(); // 错误！没有删除原始对象。
}
int main()
{
    Simple* simplePtr = new Simple(); // 分配一个 Simple 对象。
    doSomething(simplePtr);
    delete simplePtr; // 只清理了第二个对象。
    return 0;
}
```

在像上述的情况下，内存泄漏可能源于程序员之间的沟通不畅或代码文档说明不全。`doSomething()` 的调用者可能没有意识到变量是通过引用传递的，因此没有理由预期该指针会被重新赋值。如果他们注意到参数是一个指向指针的非 `const` 引用，他们可能会怀疑发生了某些奇怪的事情，但并没有关于 `doSomething()` 的注释解释这种行为。

## 在 Windows 中使用 Visual C++ 查找和修复内存泄漏

当你无法方便查看内存并观察哪些对象未在使用以及它们最初是在哪里分配的时，内存泄漏将很难追踪。然而，有一些程序可以为你完成这项工作。内存泄漏检测工具从昂贵的软件软件包到免费的可下载工具应都有。如果你已经在使用 Microsoft C++，它的调试库内置了对内存泄漏检测的支持。除非你创建一个 MFC 项目，否则内存泄漏检测默认是不启用的。要启用它，你首先需要在代码开头包含以下三行：

```cpp
#define _CRTDBG_MAP_ALLOC
#include <cstdlib>
#include <crtdbg.h>

#ifdef DEBUG
#ifndef DEBUG_NEW
    #define DEBUG_NEW ( _NORMAL_BLOCK, __FILE__, __LINE__)
    #define DEBUG_NEW
#endif
#endif // _DEBUG
```

这些行的顺序应该与所示完全一致。接下来，你需要如下所示重新定义 `new` 运算符：

请注意，这是位于一个 `#ifdef DEBUG` 语句内部，`new` 的重新定义只在编译应用程序的调试版本时才会进行。这通常是你所需要的。发布版本通常不会进行任何内存检测。

`www.it-ebooks.info`

## 第 22 章 内存管理

你所做的最后一件事是将以下行作为 `main()` 函数的第一行：

```cpp
_CrtSetDebugFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF);
```

这告诉 Visual C++ CRT（运行时）库在应用程序退出时将所有检测到的内存泄漏写入调试输出中。对于之前的泄漏程序，调试控制台将包含类似以下内容的行：

```
Detected memory leaks:
Dumping objects ->
c:leaky.cpp(15) : {147} normal block at 0x014FAB8B8, 4 bytes.
Data: > 00 00 00 00
c:leaky.cpp(33) : {146} normal block at 0x014F5048, 8 bytes.
Data: < 00 9C 77 00 F8 48 01
Object dump complete.
```

输出显示了内存是在哪个文件的哪一行被分配但从未被释放的。行号在文件名旁括号内。大括号之间是内存分配的计数器。例如，[147] 是你启动的程序中第 147 次分配。你可以使用 VC++ `_CrtSetBreakAlloc()` 函数在执行特定分配时断入调试器。例如，在 `main()` 函数的开头添加以下行，让调试器在第 147 次分配时断开：

```cpp
_CrtSetBreakAlloc(147);
```

在这个泄露程序中，有两个泄漏——第一个简单对象。

# 23

# 使用 C++ 进行多线程编程

## 本章内容概览

- 什么是多线程编程以及如何编写多线程代码
- 什么是死锁和竞态条件，以及如何使用互斥来防止它们
- 如何使用原子类型和原子操作
- 解释线程池

本章 WROX 下载

请注意，本章的所有代码示例均可以在书籍网站 `www.wrox.com/go/procC++3e` 的“Download Code”（下载代码）选项卡中作为本章代码下载的一部分找到

在具有多个处理器单元的计算机系统中，多线程编程非常重要。它允许你编写程序来并行使用所有这些处理器单元。系统有多种方式使用多个处理器单元。系统可以拥有多个离散处理器芯片，每个芯片都是独立的 CPU（中央处理器）。或者，系统可以拥有单个离散处理器芯片，其内部由多个独立的 CPU（也称为核心）组成。这类处理器被称为多处理器。系统也可以是这两者的结合。拥有多个处理器的系统已经存在很长时间；但在消费级系统中很少使用。今天，所有主要的 CPU 供应商都在销售多处理器。如今，多处理器被应用于从服务器到消费级电脑以及智能手机的各个领域。由于多处理器的泛滥，编写多线程应用程序变得愈发重要。一名专业的 C++ 程序员需要知道如何编写正确的多线程代码，以充分利用所有可用处理器单元。编写多线程应用程序过去依赖于特定平台和操作系统的 API。这使得编写跨平台的多线程代码变得困难。C++11 通过引入标准线程库解决了这个问题。

多线程编程是一个复杂的课题。本章将向你介绍如何使用标准线程库进行多线程编程，但由于空间限制，无法涉及所有细节。关于开发多线程程序有整本书的介绍。如果你对更多细节感兴趣，请参阅附录 B 中多线程部分的参考文献之一。

如果你的编译器不支持标准线程库，你可以使用其他尝试让多线程编程更具平台无关性的第三方库，例如 pthreads 库和 boost::thread 库。然而，由于它们不是 C++ 标准的一部分，因此本书书中不会讨论它们。

## 引言

多线程编程允许你并行执行多次计算。通过这种方式，你可以利用今天大多数系统内部的多个处理器单元。年前，处理器市场竞争最高频率，这对于单线程应用程序是非常理想的。大约在 2005 年，由于电源管理和热管理问题的共同，这种竞争停止了。今天，处理器市场正转向单个处理器芯片上的核心数量。在编写本文时，双核和四核处理器已经很常见，并且已经发布了 12 核、16 核和 80 核处理器的公告。

同样，如果你查看显卡（GPU）上的处理器，你会发现它们是海量并行处理器。今天，高端显卡拥有超过 2000 个核心，这个数字将迅速增加。这些显卡不仅用于游戏，还用于执行计算密集型任务。例如图像和视频处理、蛋白质折叠（有助于发现新药）、如 SETI 项目（搜寻地外文明）的信号处理等。

C++98/03 不支持多线程编程，也不支持你操作系统的多线程 API。由于 C++11 包含了标准多线程库，编写跨平台的多线程应用程序变得更加简单。目前的 C++ 标准仅针对 CPU 而非是 GPU。这在未来可能会发生变化。

启动多线程代码有两个原因。首先，如果你有一个计算问题，并成功将其拆分为可以相互独立运行的小切部分，那么你可以预期在多个处理器单元上运行时会获得性能提升。其次，你可以沿着正交轴对计算进行模块化；例如，在线程中进行长时间计算，而不是阻塞 GUI（用户界面）线程，这样在长时间计算在后台进行时，用户界面可以保持响应。

图 23-1 显示了一个非常适合并行运行的问题示例。例如，用某种算法处理图像的像素，该算法不需要相邻像素的信息。该算法可以将图像分成四部分。在单核上，每个部分都按顺序处理；在双核处理器上，并行处理两个部分；在四核处理器上，并行处理四个部分，从而使性能随着核心数量的增加产生近乎线性的扩展。

| 单核 | 核心 1 | 处理部分 1 | 处理部分 2 | 处理部分 3 | 处理部分 4 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 双核 | 核心 1 | 处理部分 1 | 处理部分 3 | | |

| | 核心 2 | 处理部分 2 | 处理部分 4 | | |

| 四核 | 核心 1 | 处理部分 1 | | | | |

| | 核心 2 | 处理部分 2 | | | | |

| | 核心 3 | 处理部分 3 | | | | |

| | 核心 4 | 处理部分 4 | | | | |

图 23-1
