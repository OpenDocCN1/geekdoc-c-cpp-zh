
在列表 28.2 捕获 `std::bad_alloc` 时，你实际上捕获了由 `new` 抛出的 `std::bad_alloc` 类对象。`std::bad_alloc` 是一个继承自 C++ 标准类 `std::exception` 的类，该在头文件 `<exception>` 中声明。

`std::exception` 是以下重要异常的基类：

- `bad_alloc`—当使用 `new` 请求内存失败时抛出

- `bad_cast`—当你尝试捕获错误的类型（即没有继承关系的类型）时，由 `dynamic_cast` 抛出

- `ios_base::failure`—由 `iostream` 库中的函数和方法抛出

基类 `std::exception` 支持一个非常有用且重要的虚方法 `what()`，它能对导致异常的问题性质提供更具描述性的名称。在列表 28.2 中，第 18 行的 `exp.what()` 提供了信息“bad array length”，告诉你哪里出了问题。你可以利用 `std::exception` 是许多异常的基类这一特性，创建一个 `catch(const exception&)`，它可以捕获所有以 `std::exception` 为基类的异常：

```
void SomeFunc() {
  try {
    // 代码已实现异常安全
  }
  catch (const std::exception& exp) // 捕获 bad_alloc, bad_cast 等
  {
    cout << "Exception encountered: " << exp.what() << endl;
  }
}
```

# 继承自 std::exception 的自定义异常类

你可以抛出任何你类型的异常。然而，继承自 `std::exception` 有一个好处——所有现有的 `catch(const std::exception&)` 并处理 `bad_alloc`、`bad_cast` 等异常的异常处理器将自动扩展到捕获你的新异常类，因为它们具有共同的基类。这在列表 28.5 中得到了证明。

## 列表 28.5 继承自 std::exception 的类 CustomException

```
0: #include <exception>
1: #include <iostream>
2: #include <string>
3: using namespace std;
4: 
5: class CustomException: public std::exception
6: {
7:     string reason;
8: public:
9:     // 构造函数，需要 reason
10:    CustomException(const char* why):reason(why) {}
11: 
12:    // 重定义虚函数以返回 'reason'
13:    virtual const char* what() const throw
14:    {
15:        return reason.c_str();
16:    }
17: };
18: 
19: double Divide(double dividend, double divisor)
20: {
21:     if(divisor == 0)
22:         throw CustomException("CustomException: Dividing by 0 is a crime");
23: 
24:     return (dividend / divisor);
25: }
26: 
27: int main()
28: {
29:     cout << "Enter dividend: ";
30:     double dividend = 0;
31:     cin >> dividend;
32:     cout << "Enter divisor: ";
33:     double divisor = 0;
34:     cin >> divisor;
35:     try
36:     {
37:         cout << "Result is: " << Divide(dividend, divisor);
38:     }
39:     catch(exception& exp)// 捕获 CustomException, bad_alloc, bad_cast
40:     {
41:         cout << "Exception encountered: " << exp.what() << endl;
42:     }
43:     }
44:     return 0;
45: }
46: }
```

## 总结

在本节中，你学习了 C++ 的一个重要部分。开发稳定的应用程序对于客户满意度和直观的用户体验至关重要，而这正是异常可以帮助提供的。你发现分配资源或内存的代码可能会失败，因此需要异常安全的。你学习了 C++ 异常类 `std::exception`，以及如果你需要编写自定义异常类，理想情况下应该继承自它。

## 问答

- 为什么要抛出异常而不是返回错误？

你不总是有返回错误的权利。当 `new` 调用失败时，你需要处理 `new` 抛出的异常以防止应用程序崩溃。此外，如果错误严重到导致应用程序未来无法运行，你应该考虑抛出异常。

- 为什么我的异常类应该继承自 `std::exception`？

这当然是强制性的，但它可以帮助你重用所有捕获 `std::exception` 类型异常的 `catch()` 块。你可以编写不继承任何其他内容的自定义异常类，但你需要在所有相关点插入新的 `catch(MyExceptionType&)`。

- 我有一个函数抛出了异常。它需要被同一个函数捕获吗？

完全不需要。只需确保抛出的异常类型被调用栈中的某一个调用函数捕获即可。

- 构造函数可以抛出异常吗？

构造函数实际上没有选择！它们不返回值，抛出异常是演示反对的最佳方式。

- 析构函数可以抛出异常吗？

技术上可以。但这是一种坏习惯，因为在栈回溯异常时析构函数也会被调用。因此，由于异常而调用的析构函数本身又抛出异常，显然会让尝试干净退出的已经不稳定应用程序陷入非常糟糕的局面。

## 工作坊

工作坊包含测验题，旨在帮助你巩固对所涵盖内容的理解，并提供练习题以提供使用所学内容的经验。在检查附录 E 中的答案之前，请尝试回答测验和练习题，并在进入下一节之前确保你理解了答案。

### 测验

- 1. 什么是 `std::exception`？

- 2. 当使用 `new` 分配失败时会抛出什么类型的异常？

- 3. 在异常处理器（catch 块）中分配一百万个整数来例如为了备份现有数据是正确的吗？

- 4. 你将如何捕获类型继承自 `std::exception` 的类 `MyException` 的异常对象？

### 练习题

- 1. 故障排除：以下代码哪里有问题？

```cpp
class SomeIntelligentStuff
{
    bool isStuffGoneBad;
public:
    ~SomeIntelligentStuff()
    {
        if(isStuffGoneBad)
            throw "Big problem in this class, just FYI";
    }
};
```

- 2. 故障排除：以下代码哪里有问题？

```cpp
int main()
{
    int* millionNums = new int [1000000];
    // do something with the million integers

    delete []millionNums;
}
```

- 3. 故障排除：以下代码哪里有问题？

```cpp
int main()
{
    try {
        int* millionNums = new int [1000000];
        // do something with the million integers

        delete []millionNums;
    } catch(exception& exp) {
        int* anotherMillion = new int [1000000];
        // take back up of millionNums and save it to disk
    }
}
```

# 第 29 节

## 展望

你已经学习了 C++ 编程的基础。事实上，你在理解方面已经超越了理论边界，掌握了如何通过使用标准模板库 `STL`、模板和标准库来帮助你编写高效且紧凑的代码。现在是时候关注性能并获得编程最佳实践的视角了。

在本节中，你将学习：

- 你的 C++ 应用如何最充分地利用处理器的能力

- 线程与多线程

- C++ 编程中的最佳实践

- C++17 预期的新特性

- 在本书之外提升你的 C++ 技能

## 如今的处理器有什么不同？

直到最近，计算机通过使用具有更快处理速度的处理器来变快，速度以赫兹 `Hz`、兆赫兹 `MHz` 或吉赫兹 `GHz` 为单位。例如，`Intel 8086`（见图 29.1）是 1978 年推出的 16 位微处理器，时钟频率约为 10MHz。

图 29.1

`Intel 8086` 微处理器。

![](img/ccb6520e9d7dbb1b25f5e4ac7152a7c5_707_0.png)

那是处理器在定期显著变快速的时代，你的 C++ 应用也是如此。在那时，依靠“等待游戏”来利用改进的硬件性能并借此提高软件的响应速度是很容易。虽然如今的处理器正在越来越快，但真正的创新在于它们部署的内核数量。在编写本书时，即使是流行的智能手机也配备了四核 64 位处理器，处理能力超过了十年前的桌面计算机。

你可以将多核处理器理解为一个在一个内部并行运行多个处理器的单个芯片。每个处理器都有自己的 L1 缓存，并且可以独立于其他内核工作。

更快的处理器增加你的应用程序速度是逻辑性的。处理器中的多个内核是如何提供帮助的？每个内核显然都能够并行运行应用程序，但除非你对其进行了编程，否则这并不一定会让你的应用程序变快。虽然如今的处理器正在越来越快，但真正的创新在于它们部署的内核数量。在编写本书时，即使是流行的智能手机也配备了四核 64 位处理器。如图 29.2 所示。

## 图 29.2

单线程应用程序

![](img/ccb6520e9d7dbb1b25f5e4ac7152a7c5_707_0.png)

*(注：由于原文文本中存在多处重复和乱码，上述翻译已根据上下文进行了逻辑化处理。)*

尽管这是一个简单的例子——一个线程创建信息，另一个线程消耗信息。但如果多个线程对同一个位置进行读写操作会发生什么呢？某些线程可能在其他线程尚未完成写入时就开始读取数据。这种情况下，相关数据的完整性将受到破坏。

这就是为什么线程需要进行同步的原因。

### 使用互斥锁和信号量同步线程

线程是操作系统层面的实体，你用于同步它们的对象也是由操作系统提供的。大多数操作系统都提供了信号量 `semaphore` 和互斥锁 `mutex` 来执行线程同步活动。

你使用互斥锁 `mutex`（一种互斥同步对象）来确保一次只有一个线程可以访问一段代码。换句话说，互斥锁用于封装一段代码，线程必须等待，直到当前正在执行该代码的线程完成并释放互斥锁。下一个线程获取互斥锁，完成工作，然后释放互斥锁。从 C++11 开始，C++ 在 `std::mutex` 类中提供了 `mutex` 的实现。

通过信号量，你可以控制执行某段代码的线程数量。允许一次只有一个线程访问的信号量也称为二进制信号量。

### 多线程引起的问题

多线程需要线程间良好的同步，但当这种同步无效（即：有 Bug）时，也会导致许多不眠眠。多线程应用程序面临的两个常见问题如下：

- 竞态条件 `Race conditions`——两个或多个线程尝试写入同一数据。谁会胜出？该对象的状态是什么？

- 死锁 `Deadlock`——两个线程互相等待对方完成，导致两者都处于“等待”状态。你的应用程序挂起了。

你可以通过良好的同步来避免竞态条件。通常，当允许线程写入共享对象时，你必须额外小心以确保：

- 一时间只有一个线程在写入。

- 在写入线程完成之前，不允许任何线程读取该对象。

## 编写优秀的 C++ 代码

通过确保在任何情况下都不存在两个线程互相等待，你可以避免死锁。你可以设置一个主线程来同步工作线程，或者通过编写程序使任务分布在线程之间，并产生清晰的负载分布。线程 A 等待 B，但 B 永远不应该等待 A。

编写多线程应用程序本身就是一种专业领域。因此，详细向你解释这个有趣且兴奋的话题超出了本书的范围。你应该参考关于该主题的大量在线文档，或者通过实践编程来学习多线程。一旦你掌握了它，面对未来发布的多核处理器，你将使你的 C++ 应用程序处于最优位置。

C++ 自最初概念以来并没有发生重大演变，但主要编译器厂商的标准化努力以及工具和函数的可用有助于你编写紧凑整洁的 C++ 代码。编写可读且可靠的 C++ 应用程序确实很容易。

以下是帮助你创建良好 C++ 应用程序的最佳实践短列表：

- 给变量起有意义的名字（对他人也对你自己）。多花一秒钟给变量起更好的名字是值得的。

- 始终初始化 `int`、`float` 等变量。

- 始终将指针值初始化为 `NULL` 或有效地址——例如由 `operator new` 返回的地址。

- 使用数组时，永远不要越数组缓冲区的边界。这被称为缓冲区溢出，可能会被用作安全漏洞。

- 不要使用 char 字符串或如 `strlen()` 和 `strcpy()` 等函数。`std::string` 更安全并提供了许多有用方法，包括帮助你查找长度、复制和追加的方法。

- 仅在你确定其包含的元素数量时才使用静态数组。如果你不确定，请选择 `std::vector` 等动态数组。

- 在声明和定义接受非 POD（纯旧数据）类型作为输入的函数时，考虑将参数声明为引用参数，以避免在调用函数时出现不必要的拷贝步骤。

- 如果你的类包含原始指针成员（或多个成员），考虑在拷贝或赋值时需要如何管理内存资源所有权。即，考虑编写拷贝构造函数和拷贝赋值运算符。

在编写管理动态数组或类似的工具类时，记住编写移动构造函数 `move constructor` 和移动赋值运算符 `move assignment operator` 以获得更好的性能。

记住让你的代码符合 `const` 正确（const-correct）。一个 `get()` 函数理想上不应该修改类的成员，因此它应该是 `const`。同样，函数参数应该是 `const` 引用，除非你想改变它们所包含的值。

避免使用原始指针。尽可能选择合适的智能指针。

在编写工具类时，花精力支持所有能让该类易于消费和使用的运算符。

在有选项的情况下，选择模板版本优于宏 `macro`。模板是类型安全且通用的。

在编写将放入容器（如 `vector` 或 `list`）中的类时，记住在 `map` 中使用作为键元素，以支持 `operator<`，这将有助于定义默认排序标准。

如果你的 lambda 函数太大，你可能应该考虑将其转换为函数——即一个带有 `operator()` 作为仿函数的类 `functor`，它是可复用的且具有单一维护点。

永远不要认为 `operator new` 的成功理所当然。执行资源分配的代码应该始终是异常安全的——封装在 `try` 块中并带有相应的 `catch()` 块。

永远不要在类的析构函数中抛出异常。

这不是一个详尽的列表，但它涵盖了一些帮助你编写良好且可维护的 C++ 的重要要点。

## C++17：预期特性

C++ 的伟大之处之一是标准委员会非常活跃并不断改进语言。就像它的前身 C++11 一样，C++17 预计将引入下一波特性。让我们研究一些可能改进它的特性。

### if 和 switch 初始化器

这是 `if` 和 `switch` 语句的一个小但重要的扩展，可以表示为：

```cpp
if (initializer; condition)
{
    // 执行 if 语句
}
```

或

```cpp
switch (initializer, condition)
{
    // case 语句
}
```

初始化器中定义的变量在语句结束时被销毁。当用于示例 20.3 中的代码时：

```cpp
auto pairFound = mapToStr.find(key);
if (pairFound != mapToStr.end())
{
cout << "Key " << pairFound->first << " points to Value: ";
cout << pairFound->second << endl;
}
```

该特性将其改进为：

```cpp
if (auto pairFound = mapToStr.find(key); pairFound != mapToStr.end())
{
    cout << "Key " << pairFound->first << " points to Value: ";
    cout << pairFound->second << endl;
}
```

这不仅仅减少了一行代码。它确保了在 `if` 块中需要的变量 `pairFound` 在外部可用，限制了作用域。如果你拷贝改进后的 `if` 块，你就包含了完整的逻辑。

### 拷贝消除保证

当你将变量初始化为函数的返回值时，编译器可能会在初始化变量 `num` 之前创建函数返回的整数的临时拷贝：

```cpp
int num = ReturnInt();
```

C++17 要求编译器消除这种临时拷贝；即避免这种拷贝。

### std::string_view 避免分配开销

考虑一个接受 `std::string` 作为参数的函数：

```cpp
void DisplayString(const std::string& strIn)
{
    cout << strIn << endl;
}
```
