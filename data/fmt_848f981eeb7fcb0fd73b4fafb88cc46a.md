
请注意，如果没有指定策略，默认值将类似于：
`std::launch::async` 或 `std::launch::deferred`。

## C++ mutex 对象

在 C++ 多线程编程中，熟悉 `mutex` 对象和 `<mutex>` 类是非常重要的，后者是 C++11 引入的。`mutex` 是一个可锁对象。它会在代码区域需要独占访问时发出信号。通过这种方式，它将防止任何具有相同保护的线程在访问相同资源时并发执行。

这些线程可以像其他线程一样访问内存位置。例如，在计算机程序的早期（即 80 年代和 90 年代初），人们会双击程序并运行它，而在程序运行时，再次双击它会使其与已经在运行的程序并行再次运行。你可以反复并行运行同一个程序，这导致了许多崩溃和问题。`mutex`（互斥锁）就是解决该问题的方案，它只是互斥锁时代之前许多问题中的一个。

让我们来看一个使用 `mutex` 防止程序同时运行多次的示例：

```cpp
// Mutex.cpp : 此文件包含 'main' 函数。程序的执行从此处开始并在此结束。

#include <iostream>
#include <Windows.h>
#include <mutex>
using namespace std;
int main()
{
    HANDLE myMutex;
    myMutex = CreateMutex(NULL, TRUE, L"RunOnceProgram");
    if (GetLastError() == ERROR_ALREADY_EXISTS)
    {
        cout << "Don't run this program more than once\n";
        exit(0);
    }
    // 我们可以开始运行了
    cout << "Running our program\n";
}
```

事实是，在使用线程时注意这一点非常重要，因为在读取和/或写入共享内存和资源时应该谨慎使用线程，因为它们会导致竞态条件。例如，如果我们从一个账户转账到另一个账户，我们需要等待转账完成后才能进行取款。换句话说，我们可能会遇到操作 X 的结果取决于操作 Y 的情况。这同样适用于死锁的情况。死锁是指在一个至少包含两个线程的集合中，每个线程都在等待某个资源（共享数据也被视为一种资源），而该资源正被集合中的另一个线程锁住。结果是集合中的每个线程都在无限期地等待资源释放。

防止这种情况的最好方法之一是使用 `lock_guard`。在 C++ 中，锁根据 RAII 范式（**资源获取即初始化**）来管理其资源。我们在关于智能指针和 RAII 设计模式的章节中向您介绍过 RAII 范式。简而言之，RAII 术语与 C++ 中的一种设计模式有关，它基于容器对象的寿命。RAII 对象需要资源来执行各种操作，例如将分配内存作为初始化。

我们在这种情况下使用的锁将在其构造函数中绑定 `mutex`，并在析构函数中释放它。C++ 使用两种类型的锁：`std::lock_guard`（我们将在本节中讨论）和 `std::unique_lock`（我们将在本节中不讨论，因为它是一个高级主题）。

正如所解释，`lock_guard` 将绑定 `mutex`：

```cpp
std::lock_guard my_guard;
```

在执行构造函数后，`my_guard` 将锁定 `mutex`（并在析构时解锁）。这实际上是 C++ 简化 `mutex` 使用的一种极佳方式，因为你可以清楚地看到代码非常简单、易于读和写。让我们来看一个使用 `lock_guard` 的代码示例：

```cpp
#include "pch.h"
#include <thread>
#include <mutex>
#include <iostream>
int my_Int = 0;
std::mutex my_Int_mutex; // 保护 my_Int
void safe_increment()
{
    // 在增加 my_Int 之前锁定我们的线程
    std::lock_guard<std::mutex> lock(my_Int_mutex);
    my_Int++;
    // 在线程锁定期间，我们安全地增加 my_Int 直到完成。
}
std::cout << std::thread::get_id() << " " << my_Int << " \n";
```

```cpp
// 当 lock 离开作用域时，my_Int_mutex 会自动释放
int main() {
    std::cout << "Main function: " << my_Int << "\n";
    // 增加 myFirstInt
    std::thread myFirstInt(safe_increment);
    // 增加 mySecondInt
    std::thread mySecondInt(safe_increment);
    myFirstInt.join();
    mySecondInt.join();
    std::cout << "Main function: " << my_Int << "\n";
}
```

当我们运行这段代码时，预期输出如下：

Main function:0
6660: 1
15940: 2
Main function:2

# 使用 std::thread::join()

有时，我们需要采取后续操作之前等待线程完成执行。例如，如果任务是打开文件，我们需要等待线程完成打开文件后再移动到下一个操作。

为了做到这一点，我们也可以使用 `std::thread::join()` 函数，它确保在继续后续执行之前该线程已完成执行。在其他编程语言（如 C#）中，你可能将其识别为 'wait'。让我们来看代码示例：

```cpp
#include <pch.h>
#include <iostream>
#include <thread>
static bool say_something = false; // 用户需要输入一些
```

```cpp
void wait_for_input() // 这是我们在无限循环中打印的函数
{
    using namespace std::literals::chrono_literals; // 我们使用时间字面量
    std::cout << "Waiting...\n";
    while (!say_something)
    {
        std::cout << "Say something...\n";
        std::this_thread::sleep_for(2s);
    }
}
int main()
{
    std::thread t1(wait_for_input);
    std::cout << "Press enter to stop\n";
    std::cin.get();
    say_something = true;
    t1.join();
    return 0;
}
```

```cpp
void myCallbackFunction(int myInt, std::string stringStr)
{
    std::cout << "The string passed to this function is " << stringStr << std::endl;
    std::cout << "The integer passed to this function is " << myInt << std::endl;
}
int main()
{
    int x = 24;
    std::string str = "This is a string";
    // 启动我们的线程并指定一个回调函数，带发送给它的参数 (int, string)
    std::thread myThreadObject(myCallbackFunction, x, str);
    myThreadObject.join();
    return 0;
}
```

运行这段代码时，我们预期的结果如下：

> The string passed to this function is = This a string
> The integer passed to this function is = 24

关于 C++ 的多线程和并发，你可以学习的内容非常多，这个主题可能相当高级。我们建议你继续探索这个主题，下面的链接是一个很好的起点：
https://www.tutorialspoint.com/cplusplus/cpp_multithreading.htm

## 第 28 章：C++ 协程

C++ 中的协程（Coroutines）是一种控制结构的形式，它们可以在两个不同的程序之间保持流控制而不返回。换句话说，协程是编写异步代码的新方式，允许异步操作并行运行。在某种程度上，使用协程就好像我们忘记了调用者（caller）和可调用者（callable）的概念，而这是普通异步函数或操作的工作方式。将两者都视为协作的对等伙伴。我们可以在各种场景中使用协程，当你想要编写事件驱动的应用程序（如游戏、UI、通信应用、服务器等）时，它们会非常强大。

在协程在新的 C++ 标准中诞生之前，可以使用复杂的方式处理异步操作（使用处理代码处理回调就是一种方法）。尽管如此，这些方法使代码变得复杂且难以追踪。协程是一个极好的抽象——它们让你作为程序员更容易以序列化的方式处理复杂的异步操作。请注意，使用协程并不一定有助于产生更好的性能，但会让编写和处理变得更容易。协程是 C++ 的一个新特性，因此你可以说它正处于用户的实验阶段（自 2020 年 2 月起，它已正式成为 C++ 新标准的一部分）。事实上，协程是 C++ 演进的重要部分，甚至从 C 的早期开始如此，因为它们是我们定义、管理和使用函数的一种真正的演进。全新的 C++ 20 标准发布了协程的又一次演进，这让 C++ 社区非常欣慰。首先，让我们更好地理解 C++ 中协程的概念。

`Coroutines` 这个词实际上由两个单词组成：Co 和 Routines。Co 代表协作（cooperating），而 routines 代表函数（functions）。换句话说，协程是函数协作工作的一种方式。你已经学习了如何在 C++ 中定义、声明和使用函数。我们可以有一个名为 `func1` 的函数，它会调用另一个名为 `func2` 的函数：

```cpp
void func1()
{
    // 语句
```
```cpp
// Func2;
void func2() 
{
    // 语句
}
```

当 `func1()` 调用 `func2()` 时，控制权传递给 `func2()`，在 `func2()` 运行出作用域之前，控制权将一直留在 `func2()` 中。一旦 `func2()` 离开作用域，控制权将返回给 `func1()`。执行过程中控制权不会被传递。

协程改变了游戏规则，这就是为什么自其引入以来，它被认为是现代 C++ 的重大变化。通过协程，`func2()` 的控制权可以在其仅完成部分执行时就返回给 `func1()`。在两个函数的生命周期内，控制权可以在函数之间来回移动。当 `func2()` 完成时，控制权将最后一次返回到 `func1()`。你可以从这个例子理解协程在函数之间提供的这种协作和关系，这可以赋予我们对程序流大量的权力和控制。每个函数在运行时都会准确记住它们停止的地方，并继续执行直到控制权返回给它们。这确实是精妙且强大的。

但并非于此，由于协程的生命周期，函数可以传递值。例如，如果 `func1()` 将控制权移交给 `func2()` 且 `func2()` 执行了计算，它可以将结果返回给 `func1()`，`func1()` 将使用该结果并从它停止的地方继续执行。然后 `func1()` 可以计算某些内容并向 `func2()` 返回一个新值，正如你猜到的那样，当它返回时。

`func1()` 的情况是调用者，而 `func2()` 是“等待（await）”。协程处理两者在共同工作时的关系。我们稍后会进一步解释这些主题。

正如你想象的，协程在线程方面可以产生重大影响，因为它们可以在程序的生命周期内管理我们的多任务执行。

为了在代码中使用 await 协程，我们可以使用三个表达式：

- `co_await`：挂起或恢复函数的执行。
- `co_return`：用作返回语句。
- `co_yield`：在函数之间的迭代过程中携带值和流。

请请注意，`co_return` 和 `co_await` 需要编译器对 C++20 标准的支持（参见 https://en.cppreference.com/w/cpp/keyword 和 https://en.cppreference.com/w/cpp/keyword）。

为了在我们的代码中使用 await 协程，我们可以使用三个表达式：

- `co_await`：挂起或恢复函数的执行。
- `co_return`：用作返回语句。
- `co_yield`：在函数之间的迭代过程中携带值和流。

## co_return 操作符

在使用返回语句的普通函数中，返回值存储在调用者可以访问的位置（通常在函数帧或激活帧中），然后它会被销毁。协程改变了调用和返回的方式，为了这个目的，使用了三种方法：**挂起（Suspend）、恢复（Resume）和销毁（Destroy）**。同样，正如我们在 `co_await` 中看到的一样，这些方法的名称非常清晰，你可以理解它们的用途。

- `Suspend` 操作挂起协程的执行，并负责将执行传回给调用者或恢复状态（取决于情况）。此时，激活帧将保持完好。
- `Resume` 操作负责恢复挂起协程的执行。
- `Destroy` 操作负责销毁激活帧以及协程作用域内的对象，同时释放使用的内存。

## co_yield 操作符

`co_yield` 与 `co_await` 一起负责挂起协程的操作——这是一个强大的选项。`co_yield` 可以在执行过程中挂起函数。一旦执行被挂起，它将传回给调用者或协程的恢复者。这意味着如果我们使用 `co_yield` 挂起 `func1()`（调用者）的操作，操作将移动到 `func2()`（恢复者）等等——这一切取决于我们如何定义协程。

需要指出的是，如果你在非协程函数中使用这些表达式，编译器将将其转换为协程函数。

让我们看看不使用协程的简单函数语法。在这种情况下，函数计算并返回前 10 个斐波那契数：

```cpp
#include "pch.h"
#include <iostream>
```
```cpp
using namespace std;
```

```cpp
int fib(int x) {
    if ((x == 1) || (x == 0)) {
        return(x);
    }
    else {
        return(fib(x - 1) + fib(x - 2));
    }
}
int main() {
    int x = 10;
    int i;
    while (i < x) {
        cout << " " << fib(i);
        i++;
    }
}
```

当我们运行这段代码时，预期的结果如下：

![](img/989605394af9c1cdcfc5a952af3b7bd1_823_0.png)

现在让我们看看如何使用协程（Coroutines）显示斐波那契数列：

```cpp
#include "pch.h"
#include <iostream>
#include <future>
using namespace std;
future<int> my_async(int a, int b) {
    auto fib = std::async([=]() {
        int c = a + b;
        return c;
    });
    return fib;
}
future<int> my_fib(int n)
{
    if (n <= 2)
        co_return 1;
    int a = 1;
    int b = 1;
    // 迭代斐波那契数列
    for (int i = 0; i < n - 2; ++i)
    {
        int c = co_await my_async(a, b);
        a = b;
        b = c;
    }
    co_return b;
}
```

```cpp
future<void> test_async_fib()
{
    for (int i = 1; i < 10; ++i)
    {
        int result = co_await my_fib(i);
        cout << "Coroutine (" << i << ") for Fibonacci is the number " << result << endl;
    }
}
```

```cpp
int main()
{
    auto fib = test_async_fib();
    fib.wait();
    return 0;
}
```

运行这段代码时，预期的结果如下：

```
Microsoft Visual Studio Debug Console
Coroutine (1) for Fibonacci is the number 1
Coroutine (2) for Fibonacci is the number 1
Coroutine (3) for Fibonacci is the number 2
Coroutine (4) for Fibonacci is the number 3
```
