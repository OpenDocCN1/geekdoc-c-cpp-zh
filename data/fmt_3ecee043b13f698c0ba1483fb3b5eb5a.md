
```cpp
thread t1{Counter(1, 20)};

// 使用命名变量

Counter c(2, 12);

thread t2(c);

// 使用临时对象

thread t3(Counter(3, 10));

// 等待线程完成

t1.join();

t2.join();

t3.join();

}
```

如果你比较 `t1` 的创建和 `t3` 的创建，似乎唯一的区别是第一种方法使用了大括号，而第三种方法使用了括号。然而，当你的函数对象构造函数不需要任何参数时，这里编写的第三种方法将无法工作。例如：

```cpp
class Counter {

public:

    Counter() {}

    void operator()() const { /* 为了简洁已省略 */ };

};

int main() {

    thread t1(Counter()); // 错误！

    t1.join();

}
```

这会导致编译错误，因为 C++ 将 `main()` 中的第一行解释为名为 `called` 的函数声明，该函数返回一个 `thread` 对象并接受一个参数，而不是返回 `Counter` 对象。出于这个原因，建议使用统一初始化语法：

```cpp
thread t1{Counter()}; // OK
```

如果你的编译器不支持统一初始化，你必须额外添加一组括号以防止编译器将该行解释为函数声明：

```cpp
thread t1((Counter())); // OK
```

> 注意：函数对象总是被复制到线程的某些内部存储中。如果你想在你的函数对象的特定实例上执行 `operator()` 而不是复制它，应该使用来自 `<functional>` 头文件的 `std::ref()` 来通过引用传递你的实例。

# 使用 Lambda 的线程

Lambda 表达式与标准 C++ 线程库配合得非常完美，如下例所示：

```cpp
int main() {

    int id = 1;

    int numIterations = 5;

    thread t1([&] {

        for (int i = 0; i < numIterations; ++i) {

            cout << "Counter " << id << " has value " << i << endl;

        }

    });

    t1.join();

}
```

# 使用成员函数的线程

你也可以指定类的类的成员函数在线程中执行。下面的示例定义了一个带有 `process()` 方法的基础 `Request` 类。`main()` 函数创建了一个 `Request` 类实例并启动了一个新线程，该线程执行 `Request` 实例 `req` 的 `process()` 成员函数：

```cpp
class Request {

  public:

    Request(int id) : mID(id) { }

    void process() {

        cout << "Processing request " << mID << endl;

    }

  private:

    int mID;

};

int main() {

  Request req(100);

  thread t(&Request::process, &req);

  t.join();

}
```

# 线程本地存储

标准库支持线程存储的概念。通过 `thread_local` 关键字，你可以将任何变量标记为线程本地，这意味着每个线程都有自己的副本，并且每个线程初始化一次。例如，在以下代码中：

```cpp
thread_local int n;

void doWork() {

  // 每个线程都有自己的 n 副本

}
```

> 注意：函数对象总是被复制到线程的某些内部存储中。如果你想在你的函数对象的特定实例上执行 `operator()` 而不是复制它，应该使用来自 `<functional>` 头文件的 `std::ref()` 来通过引用传递你的实例。

# 取消线程

标准库没有包含任何从另一个内部取消正在运行线程的机制。实现这一点的最佳方法是提供两个线程同意的通信机制。最简单的机制是设置一个共享变量，目标线程定期检查以确定应该关闭。必须注意避免竞态条件和对此共享变量的写入。原子变量或条件变量（在本章稍后部分都会讨论）可以帮助避免这些问题。

# 获取线程结果

如你在之前的示例所示，启动一个新线程非常简单。然而，在大多数情况下，你对线程产生的结果感兴趣。例如，如果你的线程执行了一些计算，你真的想从线程获取结果。一种方法是传递一个共享变量的指针或引用给线程，从中存储结果。另一种方法是将结果存储在函数对象的成员变量中，在线程完成后对其进行检索。然而，还有另一种更容易获取线程结果的方法：未来（future）。它们也让处理线程内部的错误变得更容易。未来将在本章之后讨论。

# 复制和重抛异常

只要在线程内部，C++ 的整个异常机制运行良好。每个线程都可以抛出异常，但它们需要在自己的线程内被捕获。在一个线程中抛出的异常无法在另一个线程中捕获。当你想要将异常处理与多线程结合时，这引入了一些问题。

如果没有标准库，跨线程处理异常非常甚至不可能。标准库通过以下异常相关函数解决了这个问题。这些函数仅适用于 `std::`，但适用于所有类型的异常、整数、字符串、自定义异常等：

```cpp
exception_ptr current_exception() noexcept;
```

该函数旨在在 `catch` 块内部调用，并返回一个指向正在处理的异常的 `exception_ptr` 对象，或者当前处理异常的副本；如果没有处理异常，则返回空 `exception_ptr`。只要有引用它的 `exception_ptr` 对象，该引用的异常对象就是有效的。

```cpp
[[noreturn]] void retrow_exception(exception_ptr ptr);
```

此函数重新抛出由 `exception_ptr` 参数引用的异常。重新抛出引用的异常并不需要在最初生成异常的同一个线程中进行，这使得该特性非常适用于跨线程处理异常。`[noreturn]` 属性明确了函数永远不会正常返回。属性在第 10 章中介绍。

```cpp
template<class E> exception_ptr make_exception_ptr(E e) noexcept;
```

此函数创建一个 `exception_ptr` 对象，该对象引用给定异常的拷贝。这基本上是以下代码的简写形式：

```cpp
try {

  throw e;

} catch(...) {

  return current_exception();

}
```

让我们看看如何使用这些特性实现跨线程异常处理。以下代码定义了一个执行某些工作并抛出异常的函数。该函数最终将在独立的后台线程中运行：

```cpp
void doSomeWork() {

  for (int i = 0; i < 5; ++i) {

    cout << "Thread throwing a runtime error..." << endl;

    throw runtime_error("Exception from thread");

  }

}
```

接下来的 `threadFunc()` 函数在 `try/catch` 块中调用前面的函数，捕获 `doSomeWork()` 可能抛出的所有异常。为 `threadFunc()` 提供了一个类型为 `exception_ptr` 的参数。一旦捕获到异常，就会使用函数 `current_exception()` 获取正在处理的异常的引用，并将其赋值给 `exception_ptr` 参数。之后，线程正常退出：

```cpp
void threadFunc(exception_ptr err) {

  try {

    doSomeWork();

  } catch (...) {

    cout << "Thread caught exception, returning exception..." << endl;

    err = current_exception();

  }

}
```

接下来的 `doInThread()` 函数从主线程调用。它的职责是创建一个新线程并在其中执行 `threadFunc()`。一个 `exception_ptr` 类型对象的引用作为参数传递给 `threadFunc()`。一旦线程创建，`doInThread()` 使用 `join()` 方法等待线程完成，然后检查错误对象。由于 `exception_ptr` 的类型是 `NullablePointer`，你可以轻松地使用 `if` 来检查它。如果是非空值，则在当前线程（在此是主线程）中重新抛出异常。通过在主线程中重新抛出异常，异常从一个线程传输到了另一个线程。

```cpp
void doWorkThread()

{

    exception_ptr error;

    // 启动后台线程

    thread t{ throw threadFunc, ref(error) };

    // 等待线程完成

    t.join();

    // 查看线程是否抛出了任何异常

    if (error)

    {

        cout << "Main thread received exception, rethrowing it..." << endl;

        rethrow_exception(error);

    }

    else

    {

        cout << "Main thread did not receive any exception." << endl;

    }

}
```

```cpp
int main()

{

    try {

        doWorkThread();

    } catch (const exception& e) {

        cout << "Main function caught: " << e.what() << endl;

    }

}
```

`main()` 函数非常简单。它调用 `doWorkThread()` 并将调用封装在 `try/catch` 块中，以捕获由 `doWorkThread()` 生成的任何线程抛出的异常：

输出如下：

为了保持此示例紧凑易于理解，`doWorkThread()` 函数使用 `join()` 来阻塞并等待线程完成。当然，在实际应用中，你并不希望阻塞主线程。例如，在 GUI 应用程序中，你可能会让 `threadFunc()` 向 UI 线程发送消息，其参数是 `current_exception()` 结果的拷贝。

# 原子操作库

原子类型允许原子访问，这意味着在没有额外同步的情况下允许并发读写。如果没有原子操作，增加变量的值不是线程安全的：编译器首先将值从内存加载到寄存器中，对其递增，然后将结果存回内存。另一个线程可能在递增操作期间接触同一块内存，这就是竞态条件。例如，以下代码不是线程安全的，并且包含竞态条件。这种竞态条件在本章开头进行了讨论：

```cpp
int counter = 0; // 全局变量

++counter; // 在多个线程中执行
```

为了在不显式使用任何锁的情况下实现线程安全，请使用原子类型：

```cpp
atomic<int> counter(0); // 全局变量

++counter; // 在多个线程中执行
```

你需要包含 `<atomic>` 头文件来使用这些原子类型。标准定义了所有基本类型的整数类型。下表列出了：

| 命名的原子类型 | 等效原子类型 |
|---|---|
| atomic_bool | atomic<bool> |
| atomic_char | atomic<char> |
| atomic_uchar | atomic<unsigned char> |
| atomic_int | atomic<int> |
| atomic_uint | atomic<unsigned int> |
| atomic_long | atomic<long> |
| atomic_ulong | atomic<unsigned long> |
| atomic_llong | atomic<long long> |
| atomic_ullong | atomic<unsigned long long> |
| atomic_wchar_t | atomic<wchar_t> |

当从多个线程访问数据时，原子操作解决了缓存一致性、内存顺序和编译器优化等问题。

# 原子类型

本节解释了为什么你应该使用原子类型。假设你有一个整数，并想从多个线程对其递增。如果你使用普通整数，可能会因为竞态条件得到错误的结果。以下代码展示了如何使用原子类型修复这个问题：

```cpp
#include <atomic>

#include <thread>

#include <vector>

#include <chrono>

#include <iostream>

void func(std::atomic<int>& counter) {

  for (int i = 0; i < 100; ++i) {

    counter++;

    std::this_thread::sleep_for(std::chrono::milliseconds(1));

  }

}

int main() {

    std::atomic<int> counter(0);

    std::vector<std::thread> threads;

    for (int i = 0; i < 10; ++i) {

        threads.emplace_back(func, std::ref(counter));

    }

    for (auto& t : threads) {

        t.join();

    }

    std::cout << "Result: " << counter << std::endl;

    return 0;

}
```

输出始终为 1000：

```
Result: 1000
```

然而，如果你不使用原子类型，可能会得到不同的值：

```
Result: 982
Result: 977
Result: 984
```

# 使用 C++ 进行线程编程

本节详细解释了如何在 C++ 中使用线程。

```cpp
#include <atomic>

#include <thread>

#include <vector>

#include <chrono>

#include <iostream>

using namespace std;

void func(atomic<int>& counter) {

  for (int i = 0; i < 100; ++i) {

    counter++;

    this_thread::sleep_for(chrono::milliseconds(1));

  }

}

int main() {

    atomic<int> counter(0);

    vector<thread> threads;

    for (int i = 0; i < 10; ++i) {

        threads.emplace_back(func, ref(counter));

    }

    for (auto& t : threads) {

        t.join();

    }

    cout << "Result: " << counter << endl;

    return 0;

}
```

```cpp
return true;

} else {

    *expected = *object;

    return false;

}
```

第二个示例是 `atomic<T>::fetch_add()`，它适用于整数原子类型，在给定对原子值增量的情况下，获取该原子类型的当前值，并返回未增加之前的原始值。例如：

```cpp
atomic<int> value(10);

cout << "Value = " << value << endl;

int fetched = value.fetch_add(4);

cout << "Fetched = " << fetched << endl;

out << "Value = " << value << endl;
```

如果没有其他线程触碰 `fetched` 和 `value` 变量的内容，输出如下：

```
Value = 10
Fetched = 10
Value = 14
```

原子类型支持以下原子操作：`fetch_add()`、`fetch_sub()`、`fetch_and()`、`fetch_or()`、`fetch_xor()`、`++`、`--`、`+=`、`-=`、`*=`、`&`、`^` 和 `-`。原子指针类型支持 `fetch_add()` 和 `fetch_sub()`。

大多数原子操作可以接受一个额外的参数，指定你想要的内存顺序。例如：

```cpp
T atomic<T>::fetch_add(T value, memory_order = memory_order_seq_cst);
```
