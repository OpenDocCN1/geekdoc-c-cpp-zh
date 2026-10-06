
为了将 CSchwefelMT 对象的性能与 CSchwefelP 进行比较，我们将属性 `CSchwefelMT::ThreadNumber` 设置为 8。通过这些设置，我们得到了上述结果。

现在，我们将使用改进后的公式：

```
$l = \frac{T(S)}{T(P)}$
```

第一个输出属于使用顺序算法和单线程的 CSchwefel 对象。其执行时间为 4 秒 57 毫秒。T(S) 为 4057（毫秒）。第二个输出属于具有 8 个线程的 CSchwefelMT 对象，其执行时间为 955 毫秒。通过第二种方法，我们实现了以下改进：

```
$l = \frac{4057}{955} = 4.248$
```

结果 $l < P$，$l=4.248$ 且 $P=8$ 表示亚线性提升，这是最常见的提升。线性提升更难实现，因为你的程序中几乎肯定会有某种同步机制，并且经常有线程间通信。这一切都会影响完美的线性提升，使其更难实现。与这两个两种情况相比——线性提升几乎是不可能的；如果我们有 X 个处理器，是否可能执行运行速度快 X 倍的任务？嗯，在某些情况下，共享对象可能通过存储中间结果来加速应用程序——这是可能的——比如这种情况可以存储已经计算出来的一半树*斐波那契*序列。

第三个输出属于具有 8 个线程的 CSchwefelP 对象，因为我们没有显式地使用 `num_threads{ int }` 设置 omp parallel 构造。在这种情况下，编译器在创建动态线程池时会使用所有可用线程。其执行时间为 959 毫秒。通过第三种方法，我们实现了以下改进：

```
$l = \frac{4057}{959} = 4.231$
```

$I < P$ 也表示亚线性提升。与 CSchwefelMT 对象相比，性能提升略小，这可能与等位基因大小、OpenMP API 实现、调度器优先级等许多因素有关。我们的意图是向你展示，从设计到代码的正确方法必须分步骤计划和执行。开始时，必须仔细确定使用描述的技术是否会带来收益和改进。实践始终是最好的指标。你做的工作越成功，产出的解决方案就越好。

## 参见

- 你可以在 http://openmp.org/wp/ 或 http://msdn.microsoft.com/en-us/library/tt15eb9.aspx 更多关于 OpenMP 的信息

# 8

## 高级线程管理

在本章中，我们将涵盖以下主题：

- 使用线程池
- 自定义线程池调度器
- 使用远程线程

## 引言

当我们想要创建一个复杂的应用程序时，我们必须包含某种复杂的机制来支持复杂的设计。在我多年的工作经验中，我看到许多设计良好的项目由于软件方案选择不当而遭受了损失。这些选择可能是错误的类设计或不正确的例程用法。此外，如果添加了并行性，你就需要一个管理机制来分发和控制并发线程。

大多数现代应用程序以及 Windows 操作系统都有此类机制。一种机制是 Windows 调度器（Dispatcher）对象，它管理进程线程、在 CPU 上调度它们的执行，并处理同步问题。另一种机制是 Windows 虚拟内存管理器，它管理内存操作并维护不可访问内存（为操作系统或零指针分配保留）以及用于应用程序的可用用户空间内存。

## 高级线程管理

此类机制的一个共同点是抽象负责管理任务的根对象。这对于保持正确的同步和独占访问非常重要。这样的对象——管理器（manager）应该创建并管理任务，确保必要的资源可用。它还必须控制任务的执行，以确保没有两个或多个任务执行无效或不同步的操作。它还应该正确销毁任务并释放已使用的资源供未来使用。

这些抽象之一是用于并行执行任务的线程池。在设计具有复杂或重要并发操作的应用程序时，用户必须涉及某种线程层次结构——其中一个线程比其他线程重要，并在某种程度上管理其他线程。在这些情况下，用户必须处理已使用的系统资源、授予独他访问正确方法、同步等。由于所有这些原因，用户应该首先设计一个智能对象，能够满足所有上述要求，同时提供舒适的开发。

## 使用线程池

在这里我们将解释线程池，它可以被表示为工作线程列表，当这些线程可用时将执行所需的任务。当应用程序想要减少大量线程并为工作线程提供管理时，这是很好的。另一个应用程序受益的场景是存在大量线程负责小任务。在这种情况下，创建和销毁大量线程的开销是巨大的，应该通过执行全部工作的的少量线程来避免。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_356_0.png)

我们在设计 `ThreadPool` 类时将遵循此模式。我们将使用一个可用于分发的线程列表。换句话说，应用程序将从池中请求工作线程，而不是创建线程。池管理器——Dispatcher——将根据应用程序的请求管理和调度工作线程。

Dispatcher 负责资源管理、警报和通知、正确的同步以及问题解决。使用系统资源以便应用程序良好地并行执行很重要，但同时要注意不要过度过载系统。此外，还需要一种警报机制以便在发生某些事件时通知工作线程，例如用户有某些输入或后台 I/O 操作结果的情况。

由于并发执行，工作项之间需要同步。必须使用如线程本地存储（thread local storage）等功能来保存成功任务执行所需的任何内容。另一个非常重要的功能是解决问题。可能会由于随机情况出现潜在问题。尽管应用程序看起来设计得当，但也可能像第 7 章《理解并发代码设计》中解释的那样发生死锁情况。在设计线程池时，共享独占访问的保护机制应该仔细计划。然而，如果突然发生死锁情况，Dispatcher 必须具备解决问题情况的能力并确保任务的正常执行。

我们接下来的示例将实现线程池并使用它在两个银行账户之间转移资金。

## 准备工作

确保 Visual Studio 已启动并运行。

## 如何实现...

现在让我们创建一个空程序并解释其结构。执行以下步骤：

1. 创建一个名为 ThreadPool 的新空 C++ 控制台应用程序。
2. 打开解决方案管理器，右键点击“头文件”（Header files）。添加一个名为 `main` 的新头文件。打开 `main.h`。复制并粘贴以下代码：

```
#ifndef __MAIN__
#define __MAIN__
#include <Windows.h>
#include <tchar.h>
#include <time.h>

#endif
```

3. 打开解决方案管理器，右键点击“头文件”。添加一个名为 `CBankAccount` 的新头文件。打开 `CBankAccount.h`。复制并粘贴以下代码：

```cpp
#ifndef BANKACCOUNT__
#define BANKACCOUNT__

#include "main.h"

class Clock {
public:
    Clock(TCHAR* szMutexName);
    ~Clock();
private:
    HANDLE hMutex;
};

inline Clock::Clock(TCHAR* szMutexName) {
    hMutex = CreateMutex(NULL, FALSE, szMutexName);
    WaitForSingleObject(hMutex, INFINITE);
}

inline Clock::~Clock() {
    ReleaseMutex(hMutex);
    CloseHandle(hMutex);
}

class CBankAccount;
class CParameters {
public:
    CParameters(CBankAccount* fromAccount, CBankAccount* toAccount, double dAmount, bool bPrintOutput = true) {
    this->fromAccount = fromAccount;
    this->toAccount = toAccount;
    this->dAmount = dAmount;
    this->bPrintOutput = bPrintOutput;
    }
    CBankAccount* fromAccount;
    CBankAccount* toAccount;
    double dAmount;
};
```
