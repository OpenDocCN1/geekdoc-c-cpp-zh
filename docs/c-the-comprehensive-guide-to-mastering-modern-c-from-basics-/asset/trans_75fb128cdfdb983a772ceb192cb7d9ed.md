

```cpp
implementation
}
```

**Listing 26.4** 算法的不同实现，通过概念进行区分。

在 C++20 引入 ranges、concepts 和 constexpr-if 之前，这并不是那么容易实现的。当时的方法是通过迭代器标记（iterator tags），通过它你可以为函数提供多个重载。这会导致代码变得复杂得多。

有了 `constexpr if`，你拥有比使用重载更大的灵活性。在这里，`random_access_range` 首先检查特殊情况，然后 `bidirectional_range` 检查更通用的情况。

# 27 流、文件和格式化

# 章节 Telegram

- *Stream（流）*
  输入和输出的类模型。
- *istream, ostream 和 iostream*
  输入和输出流的基类。
- *operator<< 和 operator>>*
  输出和输入的重要运算符。
- *cin, cout, cerr 和 clog*
  用于标准输入、输出和错误输出的标准流。
- `<filesystem>`
  包含用于文件系统中操作文件的工具的头文件。
- *来自 <format> 的 format*
  C++20 提供的灵活格式化函数。
- *来自 <print> 的 print 和 println*
  使用 C++23 format 的输出。

通过特殊且可扩展的流模型在 C++ 中处理文件和输入/输出。本章将详细解释 C++ 的这一基础流模型。

流有时——但并非总是——指的是文件。硬盘上文件名称和其他属性的处理将在本章末尾描述。

有时，使用流感觉有点有些繁琐，特别是涉及到更改格式化时。从 C++20 开始，`<format>` 头文件中有一个新的格式化库，它允许方便的格式化属性并且是可扩展。它完全独立于流。从 C++23 开始，可以通过 `<print>` 头文件的 `print` 和 `println` 实现直接格式化输出。我们在本章末尾讨论两者。

## 27.1 带流的输入输出概念

在接下来的页面中，你会经常读到流（stream）或流对象的术语。`cout` 或 `cin` 就是此类（全局预定义的）流对象的示例。流是按特定方向移动的数据流。每个流对象都有自己的属性，这些属性由相应的流类定义。

整个原理基于类模板的层次结构，`ios_base` 类位于类层次结构的顶端，所有其他流类都派自它。图 27.1 显示了输入/输出类层次结构的简化表示。

![](img/290cf954dfcaad53865de6b98cca8e6f_1369_0.png)

图 27.1 流层次结构的简化表示。

I/O 流库及其所有方面都极其详尽，因此此处无法涵盖库的所有细节。

在图 27.1 的表示中，已经显示了基本类型的特化。除了 `ios_base` 之外，`basic_` 前缀会出现在每个类模板之前。因此，一个特化版本的形式如下：

```cpp
using ostream = basic_ostream<char>;
```

这是对 `basic_ostream` 类模板中 `char` 数据类型的特化。此类特化也可以用于其他字符类型，如 `wchar_t`、`char16_t` 等。

## 27.2 全局、预定义标准流

I/O 流库提供了预定义的全局流对象，你实际上从写第一个 C++ 程序开始就在使用它们，而并不知道它们是什么。当然，我们说的是 `std` 中的标准流对象 `cin`、`cout`、`cerr` 和 `clog`。

对于输出，`<ostream>` 头文件包含 `cout`（标准输出）、`cerr`（标准错误输出，缓冲）和 `clog`（标准错误输出，缓冲）流对象。对于输入，`<iostream>` 头文件包含 `cin` 流对象，它可以用于典型的用户输入。

### 27.2.1 流运算符 << 和 >>

流最初是一段不可读的字节，通过特化 `operator<<` 进行输出，通过特化 `operator>>` 进行输入。

在 `<ostream>` 头文件中，你会发现针对所有内置类型重载了 `operator<<`：

```cpp
ostream& operator<<(bool val);
ostream& operator<<(short val);
ostream& operator<<(unsigned short val);
ostream& operator<<(int val);
```

`<iostream>` 头文件中的 `operator>>` 也是：

```cpp
ostream& operator>>(bool val);
ostream& operator>>(short val);
ostream& operator>>(unsigned short val);
ostream& operator>>(int val);
```

通过返回引用流 `operator<<` 和 `operator>>`，可以连续多次使用这些运算符，如下：

```cpp
#include <iostream>
int main() {
    int vall, val2;
    std::cout << "Please enter 2 values: ";
    std::cin >> vall >> val2;
    std::cout << vall << " : " << val2 << std::endl;
}
```

**Listing 27.1 通过引用返回流**

许多标准类（如 `string`）也实现了 `operator<<` 和 `operator>>`。对于自定义类型，你需要实现它们。

使用 `<<` 和 `>>` 运算符的标准输入输出非常强大。但在某些情况下它们并不适用：

- **数值类型**
  处理数值类型时，精度和格式化可能很复杂。例如，你可能想指定小数。
- **char\***
  使用 `char*`（字符串）如果想输出非空结尾的字符串可能会出现问题。与 `<<` 和 `>>` 运算符不同，这些方法处理的是原始字节。
- **bool**
  `bool` 的输出被转换为 0 或 1。如果你想要 "true" 或 "false"，必须使用 `std::boolalpha`。

## 27.3 流输入输出方法

除了常用的 `<<` 和 `>>` 运算符，你还可以使用 `<ostream>` 提供的方法。这些方法在处理文件时变得非常有趣。你可以在第 27.6 节学习更多信息。这些方法使用 `streamsize`，这意味着例如不会忽略空格。

### 27.3.1 非格式化输出方法

I/O 流库提供了 `<ostream>` 中的 `put()` 和 `write()` 方法。`put()` 输出单个字符，而 `write()` 输出指定数量的字符。以下代码演示了这些方法：

```cpp
std::string sdata("raw data");
for(auto c : sdata)
    std::cout.put(c);
std::cout << 10, // = 10
std::cout.put(10); // 换行 \n
char cdata[] = ("raw data");
std::cout.write(cdata, 4); // = raw
std::cout.put(10); // 换行 \n
std::cout.flush();
```

通过 `put(c)`，你将 `sdata` 字符串的单个字符非格式化地输出到屏幕。通过 `<< 10` 和 `put(10)`，你可以清晰地看到格式化输出和非格式化输出之间的对比。`std::cout << 10` 输出格式化的值 10，而 `std::cout::put(10)` 在屏幕上输出非格式化的（通常是 ASCII）。查看 ASCII 表可知值 10 代表换行符。

随后，演示了使用 `write()` 进行非格式化输出。它简单地将 `cdata` 中的指定数量的字符（这里是四个）非格式化输出到屏幕。这里显然存在风险，因为指定的字符可能多于实际可用。最后，我们还通过 `flush()` 强制立即输出流缓冲区中的所有数据。

流定位

要对流进行定位，你可以使用 `<ostream>` 中包含的 `tell()` 和 `seekp()` 方法。这些方法在处理文件时变得非常有趣。你可以在第 27.6 节学习更多信息。

以下是 `<ostream>` 中非格式化输出方法的概述：

- ostream&put(char c);
  将参数 c 写入流。
- ostream& write(char* s, streamsize n);
  将 s 中的 n 个字符写入流。调用者必须确保 n 的值不会大于 s 中的字符数。write() 的输出不会以 '\0' 结束。

