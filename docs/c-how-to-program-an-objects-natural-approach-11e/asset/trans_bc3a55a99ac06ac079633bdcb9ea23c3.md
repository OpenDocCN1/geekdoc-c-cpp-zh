

帮助你通过更早地发现并修复开发中的错误，构建更健壮的软件。这样，最终产品中存在的错误可能会更少。³⁵

### 检查点

- **1.** *(填空)* ______ 是一种开发风格，即程序不会捕获异常、处理异常并将程序置于可能在之后失败的状态，而是立即终止程序。  
  - **答案：** 快速失败（Fail-fast）。
- **2.** *(填空)* ______ 通过在开发过程中捕获潜在的错误并识别可能的逻辑错误，帮助确保程序的有效性。  
  - **答案：** 断言（Assertions）。
- **3.** *(对/错)* 具有常见错误的函数应始终抛出异常。  
  - **答案：** 错误。实际上，具有常见错误的函数通常应返回 `nullptr`、`0` 或其他合适的值（如 `bool`），而不是抛出异常。

## 12.7 构造函数、析构函数与异常处理

在构造函数和析构函数的上下文中，存在一些微妙的问题。在本节中，你将看到：

- 为什么构造函数在遇到错误时应该抛出异常，
- 如何捕获构造函数成员初始化器中发生的异常，
- 以及为什么析构函数不应抛出异常。

### 12.7.1 从构造函数抛出异常

考虑一个我们已提及但尚未解决的问题。当在构造函数中检测到错误时会发生什么？例如，当对象的构造函数接收到无效数据时应该如何响应？**构造函数无法返回一个值来指示错误**，那么我们如何指示对象未被正确构造呢？一种方案是返回一个构造不当的对象，并希望使用它的人会进行适当的测试以确定其处于不一致的状态。另一种方案是设置构造函数之外的变量，例如全局错误变量，但这被认为是糟糕的软件工程实践。首选的替代方案是要求构造函数抛出一个包含错误信息的异常。但是，不要从全局对象的构造函数中抛出异常。此类异常无法被捕获，因为它们是在 `main` 执行*之前*构造的。

如果在初始化对象时出现问题，构造函数应抛出异常。如果构造函数在没有使用智能指针的情况下管理动态分配的内存，它应在抛出异常之前释放该内存以防止内存泄漏。析构函数不会被调用来释放资源，但已构造完成的数据成员的析构函数会被调用。**始终使用智能指针来管理动态分配的内存。**

35. Jim Shore，“快速失败[软件调试]。”*IEEE Software* 21，第 5 期（2004 年 9 月/10 月）：21–25 页。由 Martin Fowler 编辑。https://martinfowler.com/ieeeSoftware/failFast.pdf。

### 检查点

- **1.** **(讨论)** 构造函数如何指示发生了错误？
  - **答案：** 由于构造函数无法返回一个值来指示错误，构造函数可以抛出一个包含错误信息的异常。
- **2.** **(讨论)** 如果构造函数在没有使用智能指针的情况下分配内存，当发生错误时构造函数应当怎么做？
  - **答案：** 由于析构函数不会被调用来释放资源，构造函数应在抛出异常前释放内存。

### 12.7.2 通过函数 try 块捕获构造函数中的异常

回顾一下，基类初始化器和成员初始化器在构造函数体执行之前执行。因此，如果你希望捕获这些初始化器抛出的异常，不能简单地将构造函数体语句包装在 try 块中。相反，你必须使用函数 try 块，我们在图 12.5 中演示了这一点。

```cpp
// fig12_05.cpp
// Demonstrating a function try block.
#include <format>
#include <iostream>
#include <limits>
#include <stdexcept>

// Class Integer purposely throws an exception from its constructor
class Integer {
public:
   explicit Integer(int i) : value{i} {
      std::cout << std::format("Integer constructor called\n", value);
      // Purposely throwing exception from Integer constructor
      throw std::runtime_error("Integer constructor failed");
   }
private:
   int value{};
};

class ResourceManager {
public:
   ResourceManager(int i) try : myInteger{i} {
      std::cout << "ResourceManager constructor called\n";
   }
   catch (const std::runtime_error& ex) {
      std::cout << std::format(
         "Exception while constructing ResourceManager: {}", ex.what())
         << "\nAutomatically throwing the exception\n";
   }
private:
   Integer myInteger;
};
```

**图 12.5** | 演示函数 try 块。（第 1 部分，共 2 部分。）

```cpp
int main() {
    try {
        const ResourceManager resource{};
    }
    catch (const std::runtime_error& ex) {
        std::cout << std::format("Rethrown exception caught in main: {}\n",
            ex.what());
    }
}
```

```text
Integer constructor: 7
Purposely throwing exception from Integer constructor
Exception while constructing ResourceManager: Integer constructor failed
Automatically rethrowing the exception
Rethrown exception caught in main: Integer constructor failed
```

**图 12.5** | 演示函数 try 块。（第 2 部分，共 2 部分。）

为了帮助演示函数 try 块，类 Integer（第 9–18 行）通过从其构造函数中故意抛出异常（第 14 行）来模拟“获取资源”失败。类 ResourceManager（第 20–32 行）包含一个 Integer 类的对象（第 31 行），该对象将在 ResourceManager 构造函数的成员初始化器列表中被初始化。

在构造函数中，你通过将 try 关键字放在构造函数的参数列表之后、引入成员初始化器列表的冒号（:）之前来定义函数 try 块（第 22 行）。成员初始化器列表后跟构造函数体（第 22–24 行）。成员初始化器列表或构造函数体中发生的任何异常都可以由构造函数体之后的 catch 块处理——在此示例中，即第 25–29 行的 catch 块。此示例中的控制流如下：

- 第 36 行的 main 创建了一个 ResourceManager 类的对象，该对象调用了类的构造函数。
- 构造函数中的第 22 行调用 Integer 类的构造函数（第 11–15 行）来初始化 myInteger 对象，产生前两行输出。第 14 行故意抛出异常，以便我们演示 ResourceManager 构造函数的函数 try 块。这会终止 Integer 类的构造函数，并将异常抛回给第 22 行的初始化器，该初始化器位于 ResourceManager 构造函数的函数 try 块中。
- 函数 try 块（也包括构造函数体）终止。
- ResourceManager 构造函数第 25–29 行的 catch 处理程序捕获该异常，并显示接下来两行输出。
- 构造函数函数 try 块的主要目的是使你能够进行初步的异常处理，例如记录异常或抛出一个更适合你的代码的不同异常。**你的对象无法被完全构造，因此函数 try 块之后的每个 catch 处理程序都必须抛出新的异常或重新抛出现有的异常——显式地或隐式地（通过编译器的隐式 `throw;` 行为）**。

如果在对象构造期间发生异常，析构函数可能会被调用：

- 如果在对象完全构造之前抛出异常，则会为迄今已构造的任何成员对象或基类子对象调用析构函数。
- 如果对象数组在发生异常时已被部分构造，则只会为该数组中已构造的对象调用析构函数。

当 catch 处理程序开始执行时，栈展开保证已经完成。如果**因栈展开而调用的析构函数抛出了异常，程序将会终止。** 根据 isocpp.org 常见问题解答，³⁸ 选择终止是因为 C++ 不知道应该：

- 继续处理最初导致栈展开的异常，还是
- 处理从析构函数抛出的新异常。

### ✓ 检查点

- **1.** **(对/错)** 编译器会隐式地将所有析构函数声明为 noexcept，除非你通过声明析构函数为 noexcept(false) 来明确说明，或者直接或间接基类的析构函数被声明为 noexcept(false)。
  - **答案：对。**
- **2.** **(对/错)** 如果在对象构造期间发生异常，成员对象和基类子对象的析构函数将不会被调用。
  - **答案：** 错误。如果在对象构造期间发生异常，则会为迄今已构造的任何成员对象或基类子对象调用析构函数。如果对象数组在发生异常时已被部分构造，则只会为该数组中已构造的对象调用析构函数。
- **3.** **(对/错)** 在销毁派生类对象期间，如果基类析构函数可能抛出异常，你可以在派生类析构函数上使用函数 try 块，以确保有机会捕获该异常。
  - **答案：对。**

## 12.8 处理 new 失败

第 11.4 节演示了使用 new 动态分配内存。然后，第 11.5 节展示了使用 RAII（**资源获取即初始化**）、类模板 unique_ptr 和函数模板 make_unique 进行现代 C++ 内存管理，它们在“幕后”使用 new 运算符。如果 new 未能分配所请求的内存，它会抛出一个 bad_alloc 异常（定义在头文件 <new> 中）。

在本节中，图 12.6–12.7 展示了两个 new 失败的示例。每个示例都试图获取大量动态分配的内存：

- 第一个示例演示了 new 抛出 bad_alloc 异常。
- 第二个示例调用 set_new_handler 来指定一个在 new 失败时调用的函数。此技术主要用于在编译器支持抛出 bad_alloc 异常之前编写的旧式 C++ 代码中。

