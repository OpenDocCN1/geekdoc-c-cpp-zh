

```cpp
double kilo2 = power(10.0, n);
std::cout << "kilo2: " << kilo2 << '\n';

std::cout << '\n';

}
```

有两个有趣的观察我想分享。

- 你可以在函数 `constantEvaluated.cpp` 的运行时分支中使用非 `constexpr` 函数，例如 `std::pow`<sup>22</sup>。
- 可以在声明为 `consteval` 的函数中，或只能在运行时运行的函数中使用 `std::is_constant_evaluated`。在这种情况下，将执行编译时分支或运行时分支。

## 5.7.3 `std::ssize`

根据 `std::ranges::ssize`，C++20 中的 `std::ssize` 返回有符号值。相比之下，容器的成员函数 `size` 返回无符号值。

`size`、`std::size` 和 `std::ssize`

```cpp
std::vector myVec{1, 2, 3};

for (int i = 0; i <= myVec.size(); i++) { }
for (int i = 0; i <= std::size(myVec); i++) { }
for (int i = 0; i <= std::ssize(myVec); i++) { }
```

表达式 `myVec.size()`（第 3 行）和 `std::size(myVec)`（第 4 行）返回无符号值，而 `std::ssize(myVec)`（第 5 行）返回有符号值。因此，取决于编译器选项，编译器可能会对第 3 行和第 4 行产生警告。该警告是由于比较 `i` 的有符号值和向量大小的无符号值。此外，如果容器的大小超过有符号 `int i` 的最大值，这种比较就会失败。

得益于实参依赖查找<sup>23</sup>，你可以不加限定地使用 `std::size` 和 `std::ssize`：

<sup>22</sup> https://en.cppreference.com/w/cpp/numeric/math/pow
<sup>23</sup> https://www.modernescpp.com/index.php/argument-dependent-lookup-and-hidden-friends/

不加限定地使用 `std::size` 和 `std::ssize`

```cpp
std::vector myVec{1, 2, 3};

for (int i = 0; i <= size(myVec); i++) { }
for (int i = 0; i <= ssize(myVec); i++) { }
```

## 5.7.4 `std::source_location`

`std::source_location` 表示关于源代码的实现定义信息。这些信息包括文件名、行号、列号和函数名。如果你需要调用点信息用于调试、日志记录或测试目的，这些信息非常宝贵。类 `std::source_location` 是比预定义 C++11 宏 `__FILE__` 和 `__LINE__` 更好的替代方案，应改用它。

`std::source_location` 可以为你提供以下信息。

| 函数 | 描述 |
| --- | --- |
| `std::source_location::current()` | 创建一个新的 source_location 对象 src |
| `src.line()` | 返回行号 |
| `src.column()` | 返回列号 |
| `src.file_name()` | 返回文件名 |
| `src.function_name()` | 返回函数名 |

静态 `consteval` 函数 `std::source_location::current()` 创建一个新的源位置对象 `src`，它表示调用点的信息。你可以将该对象存储在容器 `std::vector<std::source_location>` 中，或显示其信息。

### 用 `std::source_location` 显示调用点信息

```cpp
// sourceLocation.cpp

#include <format>
#include <iostream>
#include <string_view>
#include <source_location>

void log(std::string_view message,
         const std::source_location& logMessage = std::source_location::current()) {
    std::cerr << std::format("{}\n{}:{}:{}\n",
                message,
                logMessage.file_name(), logMessage.function_name(),
                logMessage.line(), logMessage.column());
}

void func() {
    log("Hello world from func");
}

int main() {
    log("Hello world from main");
    func();
}
```

程序 sourceLocation.cpp 会为每条日志消息（第 17 行和第 21 行）显示源文件、函数名以及行号和列号。

首先，以下是 MSVC 编译器的输出：

![](img/c60a87adb7f61e2e82071d081bbb389a_433_0.png)

使用 MSVC 编译器显示日志信息

此外，以下是 GCC 在 Compiler Explorer 上的输出：

```text
Hello world from main: /app/example.cpp:int main() in (21, 8)

Hello world from func: /app/example.cpp:void func() in (17, 8)
```

使用 GCC 编译器显示日志信息

## 5.7.5 `std::to_address`

`std::to_address(p)` 返回 p 的地址，而不会形成对 p 所指向对象的引用。工具函数 `std::to_address` 能以统一方式处理原始指针和花式指针（智能指针）。

以一种独特方式显示原始指针和智能指针的地址

```cpp
// toAddress.cpp

#include <iostream>
#include <memory>

int main() {

    std::cout << '\n';

    int myInt[5];

    int* pMyInt{&myInt};
    std::cout << "std::to_address(pMyInt): " << std::to_address(pMyInt) << '\n';

    auto uniq = std::make_unique<int>(5);
    std::cout << "std::to_address(uniq): " << std::to_address(uniq) << '\n';
    std::cout << "std::to_address(uniq.get()): " << std::to_address(uniq.get()) << '\n';

    auto shar = std::make_shared<int>(5);
    std::cout << "std::to_address(shar): " << std::to_address(shar) << '\n';
    std::cout << "std::to_address(shar.get()): " << std::to_address(shar.get()) << '\n';

    std::cout << '\n';

}
```

![](img/c60a87adb7f61e2e82071d081bbb389a_435_0.png)

以一种独特方式显示原始指针和智能指针的地址

与 `std::addressof(*p)`<sup>24</sup> 相比，即使 `p` 未引用已构造对象的存储，也可以使用 `std::to_address(p)`。

### 提炼信息

- `std::bind_front` 是 `std::bind`（C++11）更易用的变体。与 `std::bind` 相比，`std::bind_front` 不允许重新排列其参数。
- 函数 `std::is_constant_evaluated` 判断函数是在编译时还是运行时执行。
- `std::source_location` 表示关于源代码的信息。这些信息包括文件名、行号和函数名，对调试、日志记录或测试非常有价值。
- `std::to_address(p)` 返回 `p` 的地址，而不会形成对 `p` 所指向对象的引用。

<sup>24</sup>https://en.cppreference.com/w/cpp/memory/addressof

## 6. 并发

![](img/c60a87adb7f61e2e82071d081bbb389a_436_0.png)

随着 C++11 标准的发布，C++ 获得了多线程库和内存模型。该库包含原子变量、线程、锁和条件变量等基本构建块。这是 C++20 等 C++ 标准建立更高层抽象的基础。

### 6.1 协程

![](img/c60a87adb7f61e2e82071d081bbb389a_437_0.png)

协程是能够在保持状态的同时暂停和恢复执行的函数。C++ 中函数的演进又向前迈进了一步。

### 理解协程的挑战

理解协程对我来说相当具有挑战性。我强烈建议你不要按顺序阅读本章的各节。在第一遍阅读时跳过“框架”“可等待对象与等待器”和“工作流程”这几节。此外，阅读案例研究“Future 的变体”“生成器的修改与泛化”和“各种作业工作流”。阅读、研究并动手尝试所提供的示例，应该能让你获得深入理解协程细节和工作流程所需的初步直觉。

我在本节中作为 C++20 新思想介绍的内容其实相当古老。“协程”一词由梅尔文·康威¹ 创造。他在 1963 年关于编译器构造的出版物中使用了该词。唐纳德·克努特² 称过程是协程的一种特例。有时，让自己的想法被接受只是需要一段时间。

¹https://en.wikipedia.org/wiki/Melvin_Conway
²https://en.wikipedia.org/wiki/Donald_Knuth

![](img/c60a87adb7f61e2e82071d081bbb389a_438_0.png)

你只能调用函数并从函数返回，而你可以调用协程、暂停和恢复它，并销毁一个已暂停的协程。

借助新关键字 `co_await` 和 `co_yield`，C++20 用两个新概念扩展了 C++ 函数的执行。

得益于 `co_await` 表达式，可以暂停和恢复该表达式的执行。如果在函数 `func` 中使用 `co_await` 表达式，那么当函数结果尚不可用时，对 `getResult = func()` 的调用不会阻塞。你不再进行消耗资源的阻塞，而是进行对资源友好的等待。

`co_yield` 表达式支持生成器函数。生成器函数每次被调用时都会返回一个新值。生成器函数是一种可以从中提取值的数据流。该数据流可以是无限的。因此，我们正处于 C++ 惰性求值的核心。

### 6.1.1 生成器函数

以下程序尽可能简单。函数 `getNumbers` 返回从 `begin` 到 `end` 的所有整数，按 `inc` 递增。值 `begin` 必须小于 `end`，且 `inc` 必须为正。

