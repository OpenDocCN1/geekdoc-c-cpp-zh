
原始 lint 工具会检查 C 程序的语法不规则性并提供各种类型的警告信息。例如，printf() 函数的返回类型为 int（返回类型在第 4 章讨论）。因此，由于 printf() 函数的返回值是“未使用”，lint 会对以下代码片段生成警告信息：

```
printf("%s\n", "Hello World");
```

在 C 的早期版本中，避免 lint 警告信息的方法是使用以下语法：

```
(void)printf("%s\n", "Hello World");
```

然而，lint 工具相当老旧，现代编译器会捕获许多以前由 lint 处理的编码异常。如果你感兴趣，可以安装并分析代码的类似 lint 的工具（在互联网上搜索此类工具）。

其中一种工具是 splint，它支持 C99 标准的大部分（第 2 章讨论），可在此下载：

www.splint.org/

另一种工具是 cppcheck，它可用于 C 代码和 C++ 代码，你可以在 Mac 上用以下命令安装此工具：

```
brew install cppcheck
```

请注意，即使 printf() 函数的返回值未使用，cppcheck 也不会报告警告。有关 cppcheck 的更多详细信息请见：

http://cppcheck.sourceforge.net/

顺便说一下，如果你听到人们使用术语“linter”，他们指的是分析源代码以查找各种异常的工具，例如编程错误、语法错误和其他不规则性。

## Editors and IDEs

本书中的代码示例使用 vim 编辑器编写，该编辑器可在所有 Unix/Linux 机器上使用，但你也可以使用任何方便的文本编辑器。

此外，还有 IDE 可用，但对于本书中的代码示例并非必需。如果你偏好使用 IDE，Code::Blocks 是一个合理的选择，或者你可以尝试 Eclipse 或 NetBeans。

现在你已经了解了创建和编译 C 程序的工具，以及一些可选的命令行工具，让我们来看一下 C 编程语言，这是下一节的主题。

## WHAT IS C?

C 是一种具有静态类型系统的命令式编程语言。C 能高效地“映射”到机器指令，有时被称为“高级汇编语言”。事实上，C 出现在操作系统中，并在从嵌入式系统到超级计算机的计算机中使用。

Dennis Ritchie 在贝尔实验室（1969 年至 1973 年间）开发了 C，它构成了 Unix 操作系统的基础。此外，C 于 1989 年由美国国家标准学会（ANSI）标准化（ANSI C），随后由国际标准化组织（ISO）标准化。

编译后的 C 提供了对内存的低级访问，需要最少的运行时支持，其目的是鼓励跨平台编程。确实，可移植编写的 C 程序可以在各种计算机平台和操作系统上编译，只需对 C 代码做少量修改。

C 是一种紧凑但复杂的低级语言，需要付出不小的努力才能学好。例如，C 支持不同大小的整数变量，以及一套复杂的低级运算符。另一个例子是，C 支持 Unicode（第 7 章简要讨论），其规则和例外情况比其他语言更复杂。

### What is Special About C?

C 是系统编程的语言，各种操作系统都是用 C 编写的（尽管也包含部分汇编代码）。C 也是小型微控制器的语言。此外，C 让你得以窥见计算机内部工作原理，这是其他高级语言无法实现的。你可能会惊讶地发现，Java 和 Python 虚拟机最初是以 C 程序实现的，然后再从 C 代码编译为二进制文件。

顺便说一下，C++ 语言（是 C 的扩展）也是一种低级结构化编程语言。你可以创建一个 C struct（第 7 章讨论的数据类型），其内存布局与特定设备的物理硬件寄存器相匹配，这在编写操作系统设备驱动程序时非常有用（在绝大多数其他语言中是不可能的）。

虽然本书是关于 C 而不是 C++，这里列出 C++ 的一些用途，以防你感兴趣：

- Web browsers
- robotics
- games
- device drivers
- hardware controllers
- low level mathematics
- office applications
- graphics editors
- operating systems

因此，如果你的意图是编写能够处理低级任务的程序，那么花时间学习如何编写 C 程序绝对是值得的。

### Major Revisions to C

本书不讨论早于 1999 年发布的 C99 ISO 标准的 C 版本。请注意，C 语言的早期版本包括 K&R C、ANSI C 和 C90。C99 标准引入了许多新特性，例如：

- inline functions
- new data types (such as long long int and a complex type)
- variable-length arrays and flexible array members
- improved support for IEEE 754 floating point
- support for variadic macros (macros that take a variable number of arguments)
- support for one-line comments beginning with //

虽然 C99 在很大程度上与 C90 向后兼容，但请记住存在一些限制。

C 标准的一个更近期的主要修订（始于 2007 年左右）称为 C11，它增加了众多新特性，包括：

- type generic macros
- anonymous structures
- improved Unicode support
- atomic operations
- multi-threading
- bounds-checked functions
- improved compatibility with C++

C11 使现有 C99 库的某些部分变为可选。

> NOTE 第 2 章包含有关检查源代码是否符合 C11 标准规则的信息。

另一个修订涉及嵌入式 C 编程，此前需要对 C 语言进行非标准扩展以支持诸如定点算术、多个不同的内存 bank 和基本 I/O 操作等特性。然后在 2008 年，C 标准委员会扩展了 C 语言，以为所有实现提供一个共同的标准。这些附加特性包括定点算术、命名地址空间和基本 I/O 硬件寻址。

## A HIGH-LEVEL VIEW OF C PROGRAMS

本节简要讨论 C 程序的结构、编码准则和 C 中的关键字。随着你练习编写 C 程序，以下小节中的信息会变得更有意义，因此在阅读本书的几章后值得重新阅读本节。

### The Structure of C Programs

正如你在本书的代码示例中看到的，C 程序可以包含以下内容的组合：

- comments (Chapter 2)
- statements/expressions (Chapter 2)
- variables (Chapter 2)
- if-else conditional logic (Chapter 2)
- for/while/do loops (Chapter 2)
- functions (Chapter 4)
- preprocessor commands (Chapter 7)

如果你有一些编程经验，你可能已经熟悉条件逻辑、循环和函数。然而，预处理器指令可能对你来说是新的，它们在第 7 章中讨论。

### Coding Guidelines

简单清晰的程序，附带适当注释的代码块，是首选，因为它们更容易理解、调试和增强（作为一般规则）。一些准则包括：

- Keep functions (discussed in Chapter 4) short and meaningful
- Each function has one primary purpose
- Avoid complex logic involving multiple nested if-blocks
- Avoid comment code blocks that are complex or non-intuitive
- Avoid commenting every line of code

请记住，前述规则旨在作为一般准则，如果能提高代码清晰度，可以打破它们（但请尽量少做）。

### Keywords in C

C 语言支持一组关键字，你不能在 C 程序中将它们用作变量：如果尝试这样做，你的代码将无法正确编译。其中一些关键字出现在其他语言中，而一些是 C 特有的。

以下是 C 语言中一个 extensive（尽管不一定完整）的关键字列表（无特定顺序）：

auto, double, int, struct, break, else, long, switch, case, enum, register, typedef, char, extern, return, union, const, float, short, unsigned, continue, for, signed, void, default, goto, sizeof, volatile, do, if, static, while, inline, restrict, _Bool, _Complex, and _Imaginary.
