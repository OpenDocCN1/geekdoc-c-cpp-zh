# C 编程口袋入门





```
char *EXP_COM[] = {
char *RV_TIME[] = {


int summary(void *arg, void *arg)
```

> *谨以此书献给我的父母——愿这为他们的生活带来欢乐与幸福。*

如果你准备充分且有动力，你将学会编写涉及各种 C 数据类型、循环、条件逻辑、内置函数、自定义函数和递归的 C 程序。

本书帮你节省了搜索相关代码示例并将其适配到特定需求所需的时间，而这可能是一个耗时耗力的过程。无论如何，如果你不确定能否吸收本书的内容，可以浏览代码示例以了解其复杂程度。

## 本书的优势是什么？

本书的三大优势可总结如下：

- 1. 这是一本现代教材，提供了关于 C11 标准的相关最新信息
- 2. 代码示例有详细的解释，因为没有任何假设，这意味着初学者可以与解释并行地学习示例
- 3. 不假设读者的编程技能水平

还有一点需要注意：正如你可能注意到的，许多入门书籍都是在假设计算机科学背景下编写的：本书据说在没有该理论基础的情况下也是可读的。

“四 C”：它们必须清晰、简洁、完整，并且在本书规模允许的范围内尽可能正确。

## 为什么 C 中有两章关于指针的内容？

对指针的误解是 C 程序崩溃的最常见原因。虽然 C 指针可以快速解释，但涉及指针的代码示例很快就会变得难以理解（并且容易出错）。如果你不熟悉此功能，这是一个困难的主题（即使对于高级初学者也是如此）。因此，仅仅一章关于 C 指针的内容不足以让你对该主题感到自在。

正如你将看到的，第 5 章包含涉及指针的基础代码示例，这足以用于简单的 C 程序。如果你想更深入地了解如何使用指针，请阅读第 6 章中的代码示例，并尝试自己的代码变体。如果你想精通一门编程语言，你需要积极练习编写代码，对于涉及指针的 C 程序尤其如此。

## 哪些主题被排除？

本书不涵盖哈希、搜索和排序、文件 I/O、数据结构、线程、套接字、IPC、管道、共享内存、消息队列以及其他与高级和专家级开发人员相关的系统级功能。这些主题被排除是因为它们不适合入门 C 书籍，而且你需要学习许多其他概念才能编写 C 程序。请注意，第 7 章简要介绍了位操作和更复杂的 C 运算符，如果你成为全职 C 开发人员，你需要学习这些运算符。

## 如何设置命令外壳？

如果你是 Mac 用户，有三种方法可以做到。第一种方法是使用 Finder 导航到“应用程序 > 实用工具”，然后双击“实用工具”应用程序。接下来，如果你已经有一个命令外壳可用，你可以通过输入以下命令启动新的命令外壳：

```
open /Applications/Utilities/Terminal.app
```

对于 Mac 用户的第二种方法是从已可见的命令外壳中打开新的命令外壳，只需在该命令外壳中点击 command+n，你的 Mac 就会启动另一个命令外壳。

如果你是 PC 用户，你可以安装 Cygwin（开源 https://cygwin.com/）来模拟 bash 命令，或使用其他工具包，如 MKS（商业产品）。请阅读描述下载和安装过程的在线文档。请注意，如果自定义别名是在主启动文件以外的文件中定义的（例如 .bash_login），则不会自动设置。

## 完成本书后的“下一步”是什么？

这个问题的答案差异很大，主要是因为答案在很大程度上取决于你的目标。最好的答案是在你关心的问题或任务上尝试书中的新工具或技术，无论是专业还是个人。具体是什么取决于你是谁，因为数据科学家、经理、学生或开发人员的需要各不相同。此外，在处理新的数据清洗或操作挑战时，请记住你所学的内容。有时知道一种技术是可行的会使找到解决方案变得更容易，即使你必须重新阅读该部分以记住确切的语法。

如果你已经达到了在这里所学内容的极限，并且想要更深入地了解 C 的技术细节，有各种在线资源和文献描述了 C 的更复杂特性。




## 关于技术编辑

**安塞尔·瑟默斯海姆** 从事计算机开发工作近二十年，使用 C、C++、Lisp、Java 和 Perl 进行编程，在 TCP/IP 和多线程设计方面拥有丰富知识。他曾多次在 CppCon 2015、CppNow 2016、CppNow 2017、CppCon 2017、CppCon 2018 以及旧金山湾区的多次 ACCU（C 和 C++ 用户协会）会议上发表演讲。

大学之前，他曾在一家初创公司工作两年，开发基于 Java 的实时数据仓库。大学期间，他曾在 NASA 担任系统管理员，负责管理包含 Windows、Linux、Solaris、OS X 和 Irix 的混合环境。获得计算机科学学位后，他在一家通信公司担任软件工程师，设计可扩展、高性能、多线程的网络守护进程。目前，他是一名独立顾问。

他是 CopperSpice（一个开源 C++ GUI 库）的联合创始人之一，也是 DoxyPress（一个用于从 C、C++ 及其他几种语言编写的代码生成文档的开源程序）的联合创始人。他还是 libGuarded 的主要开发者，这是一个用于在多线程 C++ 应用程序中管理共享数据访问的开源库。

有关 CopperSpice 项目的更多信息，请访问 www.copperspice.com 或 www.youtube.com/copperspice。

安塞尔·瑟默斯海姆  
邮箱：ansel@copperspice.com

## 第 1 章

### C 语言简介

由于本书面向高级初学者，第一章包含的内容将帮助你准备编译和执行简单的 C 程序。因此，关于 C 语言历史细节的覆盖较少：它们很少能帮助你学习 C 语言，而且如果你真的感兴趣，可以在各种在线文章中找到这些细节。此外，本章并未包含 C 语言的所有细枝末节，因为在一本 C 语言入门编程书中这些内容根本没有必要（此外，如果你成为一名全职 C 程序员，你会根据需要逐步学习这些细节）。

简而言之，本章的目标是使其内容与本书其他章节一样有用和相关（即，不因为这是第 1 章就加入填充材料）。具体来说，本章从 C 语言的基础方面开始，并展示了如何创建、编译和执行 C 程序，所有这些都在本章前半部分讨论。

尽管本章内容主题混杂，但技术材料的流程基本上是顺序且逻辑清晰的。非顺序的代码示例包含一些尚未正式介绍的 C 语言特性。幸运的是，这些非顺序特性的用途是明确的：例如，printf() 函数显然用于打印内容。

因此，尽管本书中的代码示例尽量减少“前向引用”的技术细节，但有时这也是让代码示例更有趣和更有用的好方法。例如，第 2 章中关于 for 循环的部分包含条件逻辑（尽管 if/else 语句在该章后面才讨论），以便呈现更有意义且仍然易于理解的代码示例。

考虑到以上各点，让我们快速浏览一下本章的主要部分。第一部分简要讨论了一些可用于 C 程序的命令行工具，例如 gcc（必需）、make（可选，在附录中讨论）和 lint（同样可选），以及用于创建 C 源代码的编辑器。本节还讨论了你在 C 程序中经常使用的其他“标准”文件的位置。

本章第二部分简要介绍 C 编程语言，包括 C 语言的一些优势、一些可用的 C 语言版本以及 C 程序结构概述。你还会看到 C 语言中的“hello world”程序，以及如何从命令行编译该程序。

本章第三部分讨论 C 语言中的数据类型、二元和三元运算符，以及 C 程序中变量的命名约定。接下来的部分包含字母类型（alphabetic types）的代码示例，以及如何在 C 语言中计算数学量，例如上限值、下限值、绝对值和三角函数值。

本章第四部分简要介绍 C 语言中的数组以及如何将数组中的数字相加。本节为第 2 章（包含有关数组的详细信息和代码示例）以及第 5 章（包含 C 数组和指针的示例）提供了某种过渡。

完成本章中琳琅满目的主题后，你将能够很好地吸收本书其余章节的内容。

### 命令行工具

尽管编译、链接和加载程序的底层细节很重要，但你只需了解少量细节即可学会如何编译 C 程序。本节介绍各种命令行工具，其中一些是可选的（至少目前如此）。

#### gcc 编译器

gcc 实用程序编译 C 程序并生成一个可执行文件，你可以从命令行启动它。该实用程序有许多选项，本书代码示例所需的一个选项是“-o”。使用此选项可以指定编译相关 C 程序后要创建的可执行文件名。

例如，如果你有一个名为 MyTest.c 的 C 程序，可以使用以下命令创建可执行文件 MyTest：（-std=c11 选项将在第 2 章讨论）：

```
gcc -std=c11 MyTest.c -o MyTest
```

如果你的 Mac 上还没有 `gcc`，你可以注册一个免费的 Apple 账户，并在 Apple 开发者页面中勾选“Developer Tools”复选框，然后在“Command Line Tools for Xcode”选项中下载 `dmg` 文件。启动 `dmg` 文件安装 `gcc` 后，在命令行中调用以下命令：

```
gcc -v
```

如果 `gcc` 安装正确，你将看到类似于以下的输出：

```
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/opt/local/libexec/gcc/x86_64-apple-darwin16/7.2.0/lto-wrapper
Target: x86_64-apple-darwin16
Configured with:
/opt/local/var/macports/build/_opt_bblocal_var_buildworker_ports_build_port_s_lang_gcc7/gcc7/work/gcc-7.2.0/configure
--prefix=/opt/local --build=x86_64-apple-darwin16
--enable-languages=c,c++,objc,obj-c++,lto,fortran
--libdir=/opt/local/lib/gcc7
gcc version 7.2.0 (MacPorts gcc7 7.2.0_0)
```

本书中的代码示例使用 GNU `gcc` 编译器，如果你机器上还没有它，可以从以下网址为你所在平台下载编译器：

[https://gcc.gnu.org/releases.html](https://gcc.gnu.org/releases.html)

#### gcc 命令的有用开关（可选）

其中一些开关现在可能不太理解，但它们集中放在一起，以便你在后续章节的代码示例中需要时可以参考。

使用 -std 开关检查 C11 一致性：

```
gcc -std=c11 -o test test.c
```

使用 -Wall 开关显示所有警告消息：

```
gcc -std=c11 -Wall -o test test.c
```

使用 -c 开关创建目标文件：

```
gcc -std=c11 -c test.c
```

使用 -S 开关创建汇编文件：

```
gcc -std=c11 -S test.c
```

使用 -g 开关包含调试信息：

```
gcc -std=c11 -g test.c
```

如果之后决定移除调试信息，可以重新编译时不加 -g 开关，或者使用 strip 命令。

使用 -v 开关显示每个编译步骤应用的所有选项：

```
gcc -std=c11 -v test.c
```

使用 -L 开关指定路径 /usr/lib/：

```
gcc -std=c11 -L/usr/lib test.c -o test
```

显示 gcc 的帮助信息：

```
gcc --help
```

gcc 命令还有一些环境变量，例如 TMPDIR，它指定临时目录的位置。TMPDIR 变量的值示例：

```
/var/folders/3g/4s50gz4d22147815q8jz6gzm0000gn/T/
```

进行在线搜索以了解 gcc 命令的其他环境变量。

#### 与 lint 相关的实用程序（可选）




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



The C11 keywords include: _Alignas, _Alignof, _Atomic, _Generic, _Noreturn, _Static_assert, and _Thread_local.

在此阶段，你已经拥有足够的基础知识来创建简单的“Hello World”程序。这个代码示例是创建有趣且实用的 C 程序的第一步，这些程序涉及数据类型、变量、条件逻辑等等。

在继续之前，请不要忘记在你的机器上安装 gcc（从命令行输入 which gcc 来查看 gcc 的位置），你需要它来编译 C 程序。现在让我们继续下一节，该节将解释如何创建、编译和启动一个简单的 C 程序。

## C 中的 Hello World 程序

如本章前面所述，有时你会在 C 程序中看到 C 函数（如 `printf()` 函数）在完全解释之前就被引入。然而，这类函数通常直观且易于理解，并且在章节后面也会更详细地解释。

考虑到上述观点，清单 1.1 显示了 *HelloWorld.c* 的内容，这是一个极简的 C 程序，演示了如何使用 `printf()` 函数在命令行上显示字符串“Hello World”。

**清单 1.1：HelloWorld.c**

```c
#include <stdio.h>

int main()
{
    printf("Hello World\n");
    return 0;
}
```

清单 1.1 中的第一行可能比较晦涩：它是一个“include”语句（始终以“#”符号开头），引用文件 `stdio.h`（通常称为“头文件”）。许多 C 程序都包含此头文件，其中包含 `printf()` 函数（以及许多其他函数）的“原型”定义。让我们将有关头文件的详细内容推迟到下一节；现在我们可以忽略细节，只讨论清单 1.1 的其余部分。

如你所见，清单 1.1 的剩余部分很直接：有一个名为 `main()` 的函数，它不接受参数并返回类型为 `int` 的值。在 `main()` 函数内部有两行简单的代码。第一行是 `printf()` 函数，用于打印字符串“Hello World。”（我们稍后会更详细地查看 `printf()` 函数）。第二行是 `return` 语句，返回值为 `0`，因为这是 `main()` 函数的返回类型。有些人认为在 `main()` 函数中包含显式的“return 0”语句是不必要的，而另一些人则认为这额外的代码行只涉及最小的额外工作。

无论你是否相信，你刚刚完成了第一个 C 程序！如果你很着急，可以跳过接下来的几个章节（但请确保在某个时候阅读它们），并转到解释如何编译此 C 程序的章节。

## C 头文件和库

按惯例，C 程序中的头文件以“.h”后缀命名（并且 `.hpp` 扩展名对于 C++ 程序的头文件也很常见）。你在 [清单 1.1](#) 中看到的头文件 `stdio.h` 物理上位于目录 `/usr/lib/include` 中，这里也是许多其他标准头文件的位置。除了标准头文件之外，你还可以定义自己的自定义头文件，这在 [第7章](#) 中简要讨论。

除了头文件之外，还有一些称为“库”文件的二进制文件，在编译 C 程序时会自动包含。目录 `/usr/lib` 是许多标准库文件的标准位置，这些文件作为 C 编程环境的一部分提供（而且是的，你也可以创建自定义库，但此主题超出了本书的范围）。

如果你好奇的话，也可以从命令行以及所谓的“makefile”内部指定额外的“头”文件和库。附录包含有关 make 文件的更多信息。

### main() 函数的有效语法

[清单 1.1](#) 中的 `main()` 函数具有符合 C11 的最简单有效格式，并且在此时它是解释起来最容易的格式。以下 `main()` 函数的声明在 C11 中有效：

- `int main(void)`
- `int main()`
- `int main(int argc, char **argv)`
- `int main(int argc, char *argv[])`

前述列表中的第三和第四个声明涉及指针，这将在 [第5章](#) 和第6章中讨论。另一个需要注意的点是以下格式在某些操作系统中有效：

```c
int main(int argc, char **argv, char **envp)
```

第四段代码片段包含第三个参数 envp，它“指向” C 程序启动的环境（即环境变量）。然而，你可以通过 getenv() 和 putenv() 分别访问和更新环境变量，这将在第6章中讨论。

如果你想指定可在 C 程序内部访问的命令行参数，你需要使用以下语法（这是一种常用的语法）：

```c
int main(int argc, char **argv)
```

第一个参数 argc 是一个等于命令行参数数量的数字。前述片段中的第二个参数 argv 是一个指向指针的指针，我们将在后面的章节中看到。请注意，你可以在清单 1.1 中使用前述语法，代码编译的方式相同。

## C 程序语法

在 C 程序中放置大括号有几种约定，本节中的注释通常适用于 C 中的代码块。我们将使用清单 1.1 中的代码作为程序语法的简单示例。根据你的喜好，你可以将清单 1.1 中的初始大括号放在同一行，如下所示：

```c
int main() {
    printf("Hello World\n");
}
```

事实上，你甚至可以使用以下语法（不推荐使用以保持代码可读性）：

```c
int main() { printf("Hello World\n"); }
```

## 编译 C 程序

编译过程涉及将 C 程序转换为“目标”文件，这些文件包含二进制代码（此类文件具有“.o”扩展名）。在本书记述的代码示例涉及单个 C 程序（[第7章](#) 讨论如何编译多个自定义 C 程序），因此编译步骤很直接。

编译步骤之后，目标文件会自动与其它文件（如本章前面讨论的库文件）一起“组装”。此过程的结果是一个可执行文件，你可以从命令行启动它。

如果你好奇的话，Unix、Linux 和 OS X 有多个 C 编译器可用。原始的 C 编译器是 `cc`，而该 C 编译器的开源版本是 `gcc`。你可以按如下方式检查这些编译器的存在：

```
$ which cc
/usr/bin/cc
$ which gcc
/opt/local/bin/gcc
```

本书使用 `gcc` 编译 C 程序，并且 `gcc` 编译器的调用示例编译了 [清单 1.1](#) 中的程序，如下所示：

```
gcc -std=c11 HelloWorld.c -o HelloWorld
```

前提是没有编译错误，前述命令会生成以下可执行文件：

```
HelloWorld
```

现在用以下命令启动前述可执行文件：

```
./HelloWorld
```

输出如下：

Hello World

请注意，你也可以在不使用 -o 开关的情况下编译清单 1.1 中的程序，如下所示：

```
gcc HelloWorld.c
```

前述命令会生成以下可执行文件：

```
a.out
```

你可以通过从命令行调用 a.out 来启动前述可执行文件，你将看到相同的输出。事实上，你可以使用 -o 开关指定任何合法的文件名，但通常的做法是指定源文件名称而不带其后缀（在本例中为 HelloWorld）。

此外，C 程序可能依赖于其他 C 程序（由你或其他人编写），并且你可以将这些 C 程序包含在命令行中。例如，如果 C 程序 main1.c 依赖于 C 程序 depend1.c 和 depend2.c，你可以使用 make 实用程序（在附录中讨论）来指定这些依赖关系，并确保它们被编译和链接以创建二进制文件 main1。

## C 中的变量名



C 中的变量必须在声明语句中定义，该语句包含 1）变量名和 2）变量类型。变量的值是可选的。C 程序中的变量声明可以出现在 `main()` 代码块之前、`main()` 函数内部或用户定义函数内部。一些开发者认为，最好在函数顶部或在使用变量的代码块附近定义变量。尽管观点不一，但后者在 C++ 等面向对象编程语言中很常见。

作为一个简单示例，以下代码片段声明（但不初始化）一个整型变量，接着声明第二个整型变量，并且该变量还用一个整数值进行了初始化：

```
int myInt1;
int myInt2 = 7;
```

注意，变量声明以分号结尾。你也可以在单条语句中定义多个相同类型的变量，如下所示：

```
int myInt1, myInt2 = 7, myInt3 = 25;
```

变量声明的一般形式为：

```
type name; /* comment */
```

其中 type 是 C 变量类型之一（int、float 等），name 是 C 中任何有效的变量名。

## 赋值语句

赋值语句用于给变量赋值。以下代码片段是一个非常简单赋值语句示例：

```
num = (1 + 2) * 4;
```

等号运算符（=）左侧的变量 num 在 C 程序中较早声明（此处未显示），并被赋值为表达式 (1 + 2) * 4 的值，因此变量 num 被赋值为 12。

C 中赋值语句的一般形式为：

```
variable = expression ;
```

= 符号用于赋值，它的字面意思是：计算 expression 的值，并将 expression 的值赋给等号左侧的变量。

> 注意：第2章讨论全局变量、局部变量和形参。

## 缩进与代码格式

使用缩进使程序更易于理解（对你自己和其他人都是如此）。C 程序对每个新代码块或条件语句缩进一级。有两种流行的缩进风格：一种将起始花括号放在与代码同一行，另一种将起始花括号放在单独一行。

尽管你大概能猜出 if/else 代码块和 while 语句的用途，但让我们等到第2章再深入探讨下一组代码块的含义，这里仅从缩进风格的角度来看这些代码。考虑到这一点，下面是第一种缩进风格的示例：

```c
if (total <= 0) {
    printf("You owe nothing\n");
    total = 0;
} else {
    printf("You owe %d dollars\n", total);
    all_totals = all_totals + total;
}
```

注意，前一个代码块中的起始花括号与 if 和 else 关键字在同一行。以下代码块展示了第二种缩进风格：

```c
while (!done)
{
    printf("Processing\n");
    next_entry();
}

if (total <= 0)
{
    printf("You owe nothing\n");
    total = 0;
}
else
{
    printf("You owe %d dollars \n", total);
    all_totals = all_totals + total;
}
```

使用你偏好的格式（如果有选择的话），除非你所在组织要求遵循不同的编码规范。由于在 C 程序中你会遇到这两种格式，因此值得熟悉这两种风格。

还有一个细节：缩进通常是两个或四个空格，不鼓励使用制表符，因为制表符的处理方式取决于文本编辑器。一致性比缩进大小更重要。

## printf() 函数

在 **清单 1.1** 中，你看到了使用 `printf()` 函数打印文本字符串的示例。其他类型变量的值也使用 `printf()` 函数打印，该函数使用格式说明符来匹配不同的数据类型。具体来说，格式 `%c`、`%d` 和 `%f` 分别指定字符、整数和浮点数。此外，还有一组语义与 `printf()` 函数类似的“家族”函数，例如用于将数据放入缓冲区的 `sprintf()` 函数，以及用于将数据打印到文件的 `fprintf()` 函数。

C 支持以下输出格式：

```
%d    // print as decimal integer
%6d   // print as decimal integer, at least 6 characters wide
%f    // print as floating point
%6f   // print as floating point, at least 6 characters wide
%.2f  // print as floating point, 2 characters after decimal point
%6.2f // print as floating point, at least 6 wide and 2 after decimal point
```

`printf()` 函数还能识别 `%o`（八进制）、`%x`（十六进制）、`%c`（字符）、`%s`（字符串）以及 `%%`（表示 `%` 本身）（八进制和十六进制数将在后面讨论）。

**清单 1.2** 展示了 `IntExample.c` 的内容，说明如何初始化一个整数值变量，然后使用 `printf()` 函数显示对该变量的算术运算。

***清单 1.2：IntExample.c***

```c
#include <stdio.h>
```

C 还支持字符类型（但不支持字符串类型），以及可包含基本类型的数组。在本章后面，你将看到包含字符、字符串和数组的代码示例。

举例来说，C 支持以下数据类型（括号中为示例）：

```
int    // integer (ex: 8)
float  // floating point (ex: 5.1234)
char   // character (ex: 'a')
short  // short integer
long   // long integer
double // double-precision floating point
```

除了前面的基本数据类型列表之外，C 还支持指针，这是一个非常强大的特性，在许多语言（例如 Java）中不可用。C 指针实际上是一组指针数据类型。每当你声明一个指针时，还必须指定它将指向何种数据，以构成具体的数据类型。

事实上，C 指针可以指向更复杂的内置数据类型（例如 C 结构体）以及自定义数据类型。指针的概念将在第5章和第6章中变得更加清晰，这两章将深入探讨指针的细节（并附代码示例）。

## C 中的 sizeof() 运算符

内置的 sizeof() 运算符是一种简单方法，用于确定分配给变量或结构体的内存量（字节数）（内置结构体和自定义结构体将在第7章讨论）。

清单 1.3 展示了 SizeOfDataType.c 的内容，说明如何使用 sizeof() 函数来确定

算术运算符、自增/自减运算符和三目运算符。以下小节提供每种运算符的更多细节。

### 算术运算符

算术运算符分别是“+”、“-”、“*”和“/”，用于加法、减法、乘法和除法。在不包含括号的表达式中，算术运算符具有以下优先级：

- `*` 和 `/` 具有相同优先级（若两者都出现，则从左到右）
- `+` 和 `-` 具有相同优先级（若两者都出现，则从左到右）

括号可以覆盖默认优先级（也可以嵌套）。括号的主要用途是改变包含算术运算符的表达式的默认执行顺序，如下所示：

```
7-5+8 = 2+8 = 10 (left-to-right precedence)
7-(5+8) = 7 - 13 = -6
3*8/4 = 24/4 = 6 (left-to-right precedence)
3*(8/4) = 3*2 = 6
```

如有疑问，请在表达式中使用括号。例如，表达式 8*x+y*z/10 与 (8*x)+(y*z)/10 相同，但后者更清晰。

另一个算术运算符是取模 % 运算符，它给出一个整数除以非零整数后的整数余数：

```
7 % 4 = 3
10 % 10 = 0
```



幂运算具有最高优先级，除非被括号覆盖，如下所示：

2**4-3 = 16-3 = 13
2**(4-3) = 2**1 = 2

代码清单 1.4 展示了 Arithmetic.c 的内容，它说明了如何执行算术运算。

### 代码清单 1.4：Arithmetic.c

```c
#include <stdio.h>

int main()
{
    int x = 5 + 3;
    int y = 5 - 3;
    int z = 5 * 3;
    int w = 5 / 3;

    printf("5 + 3 = %d\n",x);
    printf("5 - 3 = %d\n",y);
    printf("5 * 3 = %d\n",z);
    printf("5 / 3 = %d\n",w);

    return (0);
}
```

代码清单 1.4 包含一个 main() 函数，该函数初始化 4 个整数变量 x、y、z 和 w，随后是 4 个 printf() 语句，用于显示这些相同变量的值。运行代码清单 1.4 中的 C 程序后，输出如下：

5 + 3 = 8
5 - 3 = 2
5 * 3 = 15
5 / 3 = 1

## 递增/递减运算符

在 C 中，有两种方法可以将变量递增或递减 1。一种方法如下面的代码块所示：

```c
int a=5, b=9;
a += 1;
b -= 1;
```

上述代码块执行后，a 的值为 6，b 的值为 8。但是，前面的结构不能与 == 运算符组合使用：必须先执行递增或递减操作，然后才能执行 if 逻辑。

第二种方法是使用递增和递减运算符，分别是 ++ 和 --。当这些运算符出现在变量的*左*侧时，递增或递减操作会在任何其他操作*之前*执行。然而，当这些运算符出现在变量的*右*侧时，递增或递减操作会在其他算术操作*之后*执行。以下代码块说明了这些要点：

```c
int x=0, y=1;
if(++x == 1) { //first add 1 to x and then compare (this is true)
               // do something
}

if(y++ == 1) { //first compare and then add 1 to y (this is true)
               //do something
}
```

上述代码块执行后，x 的值为 1，y 的值为 2，并且*两个* if 语句都会执行。

现在考虑下面的代码块，其中 x 和 y 分别初始化为值 6 和 2：

```c
int x=6, y=2;
if(--x == 6) {
//subtract 1 from x and then compare (this is false)
    // do something
}

if(y++ == 3) { // first compare then add 1 to y (this is false)
    // do something
}
```

执行前面的一对 if 语句后，x 等于 5，y 等于 3，但*两个* if 语句都不会执行（请将此结果与前面的一对 if 语句进行比较）。

## 三元运算符

三元运算符是执行 if/else 条件逻辑的一种简写方式。作为一个简单示例，考虑以下代码块：

```c
if (a < b)
{
    x = 1;
}
else
{
    x = 2;
}
```

前面的代码片段可以用更抽象的条件形式表示如下：

```c
if (expr1)
{
    expr2;
}
else
{
    expr3;
}
```

简化前面 if/else 逻辑的另一种方式是使用具有以下形式的三元运算符：

```
expr1 ? expr2 : expr3
```

例如，本节开头的代码块可以表示如下：

```
x = (a<b ? 1 : 2);
```

在前面的代码片段中，如果不等式 a<b 为真，则将 x 赋值为 1；否则，将 x 赋值为 2。

本章接下来的部分包含代码示例，说明如何使用 C 内置函数计算一个数的向上取整值和向下取整值、一个数的绝对值以及一些三角函数。第 4 章提供了更多 C 内置函数（然后向你展示如何在 C 中定义自定义函数）。

## 计算向上取整值和向下取整值

C 提供了各种执行算术和数学计算的内置函数，例如 ceil() 函数和 floor() 函数。代码清单 1.5 展示了 MathValues.c 的内容，它说明了如何计算小数值的向上取整值和向下取整值。

### 代码清单 1.5：MathValues.c

```c
#include <math.h>
#include <stdio.h>

int main()
{
   double y, z;

   y = ceil(1.05);      // y = 2.0
   z = ceil(-1.05);     // z = -1.0
   printf("y = %.2f ; z = %.2f\n", y, z);

   y = floor(2.8);
   z = floor(-2.8);
   printf("y = %.2f ; z = %.2f\n", y, z);

   return 0;
}
```

**代码清单 1.5** 包含一个 `main()` 函数，该函数通过两次调用 C 内置的 `ceil()` 函数来初始化变量 `y` 和 `z`。接下来，一个 `printf()` 语句显示 `z` 和 `y` 的值，然后通过调用 C 内置的 `floor()` 函数为 `y` 和 `z` 赋予不同的值，之后显示它们的值。编译并执行 **代码清单 1.5** 中的代码后，输出如下：

```text
The absolute value of x1 is 4.
fabs( -11.230000 ) = 11.230000
```

## 计算绝对值

C 提供了对浮点数执行算术计算的内置函数，例如 `fabs()` 函数。**代码清单 1.6** 展示了 `AbsValues.c` 的内容，它说明了如何计算整数和小数值的绝对值。

### 代码清单 1.6：AbsValues.c

```c
#include <math.h>
#include <stdlib.h>
#include <stdio.h>

int main()
{
    int x1 = -4, y1;
    double x2=-11.23,y2;

    y1 = abs(x1);
    printf("The absolute value of x1 is %d\n", y1);

    y2 = fabs(x2);
    printf("fabs( %lf ) = %lf\n", x2, y2);

    return 0;
}
```

代码清单 1.6 包含一个 main() 函数，该函数初始化变量 x1、y1 和 y2。变量 y1 和 y2 分别通过调用内置函数 abs() 和 fabs() 进行初始化。两个 printf() 语句显示 x1、y1、x2 和 y2 的值。编译并执行代码清单 1.6 中的代码后，输出如下：

The absolute value of x1 is 4.
fabs( -11.230000 ) = 11.230000

## 在 C 中计算三角函数值

C 还提供了执行三角函数计算的内置函数。代码清单 1.7 展示了 TrigValues.c 的内容，它说明了如何使用 sin()、cos() 和 tan() 函数分别返回 x 的正弦、余弦和正切值。

### 代码清单 1.7：TrigValues.c

```c
#include <math.h>
#include <stdio.h>

#define PI 3.1415926535

int main()
{
    double pi, x, y1, y2, y3;

    x = PI/4;
    y1 = sin(x);
    y2 = cos(x);
    y3 = tan(x);

    printf("sin( %lf ) = %lf\n", x, y1);
    printf("cos( %lf ) = %lf\n", x, y2);
    printf("tan( %lf ) = %lf\n", x, y3);

    return 0;
}
```

代码清单 1.7 包含一个 main() 函数，该函数将变量 x 初始化为 PI/4，然后分别通过调用 C 内置函数 sin()、cos() 和 tan() 来初始化变量 y1、y2 和 y3。三个 printf() 语句显示 y1、y2 和 y3 的值。编译并执行代码清单 1.7 中的代码后，输出如下：

sin( 0.785398 ) = 0.707107
cos( 0.785398 ) = 0.707107
tan( 0.785398 ) = 1.000000

## 在 C 中使用不同的进制

整数和十进制数默认以 10 为基数，但你可以使用其他进制，例如二进制、八进制和十六进制。代码清单 1.8 展示了 OtherBases.c 的内容，其中包含各种代码片段，说明如何在 C 中处理二进制、八进制和十六进制数。

请注意以下注意事项：二进制整数字面量是 C++14 的特性，并不属于任何 C 标准。虽然二进制整数在 C 中是 GCC 的非标准扩展，但当需要执行位级操作（第 7 章讨论）时，这个特性可能很有用。

### 代码清单 1.8：OtherBases.c

```c
#include <stdio.h>

// binary values start with 0b:
int a=0b0101; // decimal value is 5

// octal values start with 0:
int b=016;   // decimal value is 14

// hex values start with 0x or 0X:
int x1=0x18, x2=0X37, x3=0xAB;

int main()
{
    int a1=0b0101, b1=0x16, c1=123;
    int x1=0x18, x2=0X37, x3=0xAB;

    printf("a1=%d b2=%d c3=%d\n",a1, b1, c1);
    printf("x1=%d x2=%d x3=%d\n",x1, x2, x3);
}
```




```c
    return 0;
}
```

**清单 1.8** 首先将变量 `a1` 和 `b1` 分别初始化为二进制值和八进制值。下一段代码将变量 `x1`、`x2` 和 `x3` 初始化为十六进制值。注意，所有这些变量都是全局变量。

下一段代码是一个 `main()` 函数，它将局部变量 `a1`、`b2` 和 `c1` 分别初始化为二进制值、十六进制值和整数值。最后一段代码是两个 `printf()` 语句，用于显示所有这些变量的值。编译并执行 **清单 1.8** 中代码的输出如下：

```text
a1=5 b2=22 c3=123
x1=24 x2=55 x3=171
```

现在让我们简要看看 C 程序中的 `char` 类型和数组，作为第 2 章中你将看到的一些代码示例的前奏。

## 在 C 中使用 char 类型

**清单 1.9** 显示了 `ReverseChars.c` 的内容，它说明了如何初始化三个字符，然后按“逆序”打印它们。

### 清单 1.9：ReverseChars.c

```c
#include <stdio.h>

char char1; char char2; char char3;

int main()
{
    // first character
char1 = 'A';

// second character
char2 = 'B';

// third character
char3 = 'C';

printf("%c%c%c reversed is %c%c%c\n",
    char1, char2, char3,
    char3, char2, char1);

return (0);
}
```

编译代码并启动可执行文件，你将看到以下输出：

ABC reversed is CBA

既然我们已经看过使用简单内置 C 函数的代码示例，现在让我们学习 C 中的数组和字符串，这些是本章其余部分的主题。

## 什么是 C 数组？

本节对 C 数组做一个非常简短的介绍，作为深入第 2 章数组细节之前的一种预览。

“数组”是一组用于存储数据的连续内存位置。数组中的每一项称为“元素”。数组中元素的数量称为数组的“维度”。一个典型的数组声明如下所示：

```
int mylist[3];
```

```
data[0] = 45.0;
data[1] = 82.0;
data[4] = 22.0;

total = data[0] + data[1] + data[2] + data[3] + data[4];
average = total / 5.0;
printf("Total %f Average %f \n", total, average);

return (0);
}
```

清单 1.10 首先将变量 data、total 和 average 声明为 float 变量。下一部分是 main() 函数，它初始化 data 数组的 5 个值。变量 total 用 data 数组中各值之和初始化，随后变量 average 是 data 数组中数字的平均值。最后一段代码显示变量 total 和 average 的值。

按如下方式编译清单 1.10 中的代码：

```
gcc -std=c11 AddArray.c -o AddArray
```

现在启动二进制可执行文件，你将看到以下输出：

Total 210.000000 Average 42.000000

## 小结

本章向你介绍了 C 编程语言以及 C 的不同版本。你学习了 C 程序的结构、编码指南和 C 中的关键字。然后你了解了如何创建、编译和启动一个简单的 C 程序。

你还学习了 C 中的数据类型和 C 运算符（例如算术运算符、自增/自减运算符和三目运算符）。你还学习了 C 中的变量、缩进/代码格式以及 C 中的赋值语句。最后，你学习了 C 中的数组以及如何对数组中的数字求和。

## 第 2 章

### 条件逻辑和简单任务

本章本质上是第 1 章内容的延续，其中的代码示例在 C 程序中使用条件逻辑，随后是执行 C 中常规任务的示例。请注意，本章的代码示例涵盖了各种主题，但其覆盖范围仅限于基本功能。同时，这些代码示例包含一些“构建块”，可供后续章节中更有趣的代码示例使用。

第一部分从 C 程序中的注释示例开始，随后是用于处理诸如检查给定年份是否为闰年、找出三个数中的最大值以及计算三角形第三个角等任务的各种条件逻辑示例。本章第二部分包含一个代码示例，展示局部变量和全局变量之间的区别，随后介绍 C 程序中的类型转换和整数提升。

第三部分解释如何在 C 程序中使用 C 函数 gets()、puts()、scanf() 和 printf() 处理用户输入。你将看到如何读取格式化和非格式化输入值，以及如何读取整行用户输入。

最后一部分简要讨论 stdin、stdout 和 stderr，它们分别表示标准输入、标准输出和标准错误，可以重定向以接受来自文件的输入（对于标准输入），也可以重定向到输出文件（对于标准输出和标准错误）。

## C 程序中的注释

尽管本书中的 C 程序非常短，几乎（如果有的话）不会从注释中获益，但请记住，代码中的注释可以帮助其他人理解你的代码（也许还能帮助你自己，如果你已经很长时间没有看过自己的代码了）。在 C 程序中有几种包含注释的方法，这里展示了其中一些：

```
/* this is a comment */
// this is a second comment
/* this is
a third comment */
```

经验法则很简单：包含注释（或注释块）来解释某段可能难以理解其用途的代码。显然，当代码本身不言自明时，你不需要包含注释，例如以下内容：

```
int x = 3;     // an integer
float y = 4.5; // a decimal
int *ptr;      // a pointer to an integer
return x;      // return the value of x
```

## 简单条件逻辑

本节向你展示一个在 C 程序中使用 if-else 语句的非常简单的示例。请注意本章中的条件逻辑示例，因为（正如你将在第 3 章中看到的）C 程序中的 for 循环总是包含某种类型的条件逻辑（提供报告相关功能的 C 程序可能除外）。

清单 2.1 显示了 IfElse.c 的内容，它说明了如何在 C 程序中使用 if-else 逻辑。

### 清单 2.1：IfElse.c

```
    #include <stdio.h>

    int main()
    {
      int z = 10;

      if(z % 2 == 0)
      {
        printf("z is even: %d\n", z);
      }
      else
      {
        printf("z is odd: %d\n", z);
      }

      return 0;
    }
```

清单 2.1 很直接：变量 z 被初始化为值为 10 的整数，随后是一个条件代码块，如果 z 是偶数则打印一条消息，如果 z 是奇数则打印另一条消息。编译并启动清单 2.1 中代码的输出如下：

z is even: 10

## 带有逻辑错误的条件逻辑

清单 2.2 显示了 IfElse2.c 的内容，它说明了如何在 C 程序中使用稍微复杂一些的 if-else 逻辑。

### 清单 2.2：IfElse2.c

```c
#include <stdio.h>

int main()
{
    int z=10, y=-123, w=0;

    w = (z/2)*2;
    if(z == w)
    {
        printf("z is even: %d\n", z);
    }
    else
    {
        printf("z is odd: %d\n", z);
    }

    if(z = y) // do you mean == instead of =?
    {
        printf("z is even: %d\n", z);
    }
    else
    {
        printf("z is odd: %d\n", z);
    }

}

return 0;
```

清单 2.2 初始化整数值变量 *z*、*y* 和 *w*，随后是一个算术表达式，它是在确定整数是否为偶数时使用 `%` 运算符的一种替代方法。如果你将一个整数除以 2，然后将该数乘以 2，仅当该整数为偶数时，结果才等于初始整数：这是成立的，因为除以 2 会截断非整数部分。

例如，3 是奇数，因为 `(3/2)*2 = 1*2 = 2`，它不等于 3；而 4 是偶数，因为 `(4/2)*2 = 2*2 = 4`。

清单 2.2 的下一部分包含条件逻辑，如果 *z* 是偶数则显示一条消息，如果 *z* 是奇数则显示另一条消息。第二个代码块包含涉及一个简单逻辑错误的条件逻辑：使用了“=”（这是一个赋值运算符）而不是“==”（这是一个逻辑运算符）。逻辑错误不会导致编译错误：它们产生的结果通常不正确，但更难检测（尽管在此示例中输出显示了明显的错误）。

编译并启动清单 2.2 中代码的输出如下（第二行输出可能不是你期望的）：

```
z is even: 10
z is even: -123
```

第二行输出来自清单 2.2 中的错误语法，其中使用了单个“=”号而不是两个“=”号。代码片段 **`if(z = y)`** 是一个赋值表达式，其计算结果为值


被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此，if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间：如果为真，则打印相应的消息（否则打印适当的[content]
被赋值为 -123。 由于 -123 不等于 0，代码的 if 部分为真。因此 if 部分内部的代码被执行，这就是为什么会打印以下错误输出的原因：

z is even: -123

虽然这种特定的逻辑错误很容易被发现，但逻辑错误可能更难以检测，尤其是在长而复杂的 C 程序中。

## 算术运算符和条件逻辑

列表 2.3 显示了 IfElse3.c 的内容，说明如何在 C 程序中使用多个 if-else 代码块。 回想一下第 1 章中使用的代码示例，其中在 printf() 函数中使用 %d 用于格式化目的。

### 列表 2.3：IfElse3.c

```
#include <stdio.h>

int main()
{
    int x=8, y=-12, z=10;

    printf("x: %d y: %d z: %d\n",x,y,z);

    if( x == 3 ) { z = 0; }
    else    { z = 8; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( y < 0 ) { z *= 3; }
    printf("x: %d y: %d z: %d\n",x,y,z);

    if( z % 2 == 0 ) { x /= 4; }
```

```c
int main()
{
   int x=-8, z=10;

   if((z > 5) && (z < 15))
   {
      printf("z between 5 and 15: %d\n", z);
   }
   else
   {
      printf("z NOT between 5 and 15: %d\n", z);
   }

   if((x < 0) || (z > 4))
   {
      printf("x negative or z greater than 4: %d\n", z);
   }
   else
   {
      printf("x non-negative or z less than 4: %d\n", z);
   }

   return 0;
}
```

列表 2.4 包含两个涉及条件逻辑的代码块。第一个代码块检查 z 的值是否在 5 到 15 之间，若为真则打印相应消息，否则打印适当消息。第二个代码块检查 x 是否为负或 z 是否大于 4，若任一条件为真则显示适当消息，否则显示反事实陈述。

编译并运行列表 2.4 中代码的输出如下：

```
   z between 5 and 15: 10
```

## 什么是“短路”

一般来说，如果表达式包含多个 and 语句，只要其中任一 and 语句为假，结果就为假，因此无需检查剩余的 and 项。这种行为称为“短路”，这里给出一个简单示例：

```
int x = 3;
if( (x < 4 ) && (x > 5)
&& (x < 0))
{
    // do something
}
else
{
    // do something else
}
```

在前面的复合 if 表达式中，(x > 5) 为假，因此无需评估 if 表达式的其他部分，else 部分被执行。

短路也发生在其他类型的条件逻辑中。例如，如果复合 if 表达式在中间点成功，则不会评估复合 if 表达式的剩余部分。示例如下：

```
int x = 3;
if(x > 5)
{
    // do something
}
else if (x < 4)
{
    // do something else
}
else if (x < 0)
{
    // do yet another thing
}
```

前面的代码块在第一个 else 语句中为真，因此无需检查表达式的剩余部分。

短路的第三个示例是前两个示例的组合，如下所示：

```
int x = 3, y = 7;
if(x > 5)
{
    // print something
}
else if (x < 4)
{
    if (y < 2)
    {
        // print something
    }
    else if (y < 4)
    {
        // print something else
    }
    else if (y < 6)
    {
        // print yet another thing
    }
}
else if (x < 0)
{
    // do yet another thing
}
```

前面的代码块在第一个 else 语句中为真，因此不执行涉及 x 的复合 if 表达式的剩余部分。然而，涉及 y 的所有表达式都为假，这意味着在涉及变量 y 的嵌套 if 表达式中没有任何内容被执行。如果需要，请再次阅读此示例，直到清楚地知道没有任何内容被打印。

## 使用 if-else 语句对数字进行排序

**列表 2.5** 显示了 OrderedValues.c 的内容，说明如何在 C 程序中使用 if-else 逻辑以降序显示三个数字。

### 列表 2.5：OrderedValues.c

```c
#include <stdio.h>

int main()
{
    int a1=3, a2=8, a3=6, temp;

    printf("ORIGINAL a1: %d a2: %d a3: %d\n", a1, a2, a3);

    if( a1 < a2 )
    {
        temp = a1;
        a1 = a2;
        a2 = temp;
    }

    if( a2 < a3 )
    {
        temp = a2;
        a2 = a3;
        a3 = temp;
    }

    printf("ORDERED a1: %d a2: %d a3: %d\n", a1, a2, a3);

    return 0;
}
```

[列表 2.5](#) 初始化变量 a1、a2 和 a3，并打印其初始值。第一个代码块仅在 a1 小于 a2 时交换 a1 和 a2 的值。类似地，第二个代码块仅在 a2 的值小于 a3 时交换 a2 和 a3 的值。编译并运行列表 2.5 中代码的输出如下：

```text
ORIGINAL a1: 3 a2: 8 a3: 6
ORDERED a1: 8 a2: 6 a3: 3
```

## 顺序 if 语句

[列表 2.6](#) 显示了 `MaxAndMin.c` 的内容，说明如何在 C 程序中使用 if-else 逻辑以找到三个数字的最大值和最小值。

### 列表 2.6：MaxAndMin.c

```c
#include <stdio.h>

int main()
{
    int a1=3, a2=8, a3=6,max=0, min=0;
    max = a1;
    min = a1;

    if( max < a2 ) { max = a2; }
    if( min > a2 ) { min = a2; }
    if( max < a3 ) { max = a3; }
    if( min > a3 ) { min = a3; }

    printf("ORIGINAL a1: %d a2: %d a3: %d\n", a1, a2, a3);
    printf("MAXIMUM: %d\n", max);
    printf("MINIMUM: %d\n", min);

    return 0;
}
```

列表 2.6 首先将 max 和 min 的值设为 a1。下一对语句将 max 和 min 的值与 a2 的值进行比较，并相应地更新它们。类似地，第二个代码块将 max 和 min 的值与 a3 的值进行比较，并相应地更新它们。

编译并运行列表 2.6 中代码的输出如下：

ORIGINAL a1: 3 a2: 8 a3: 6
MAXIMUM: 8
MINIMUM: 3

## 嵌套 if-else 语句

列表 2.7 显示了 AngleSum.c 的内容，说明如何在 C 程序中使用 if-else 逻辑根据前两个角的值确定三角形的第三个角。请记住，所有角必须大于 0 且小于 180，并且一对角的和必须小于 180。

### 列表 2.7：AngleSum.c

```c
#include <stdio.h>

int main()
{
   int a1=40, a2=80, a3=0;
   // ensure the following are true:
   // 1) a1>0 and a1 < 180
   // 2) a2>0 and a2 < 180
   // 3) a1+a1 < 180

   if( ((a1 <= 0) || (a1 >= 180)) ||
       ((a2 <= 0) || (a2 >= 180)) )
   {
      printf("angles out of range: a1 = %d a2 = %d\n", a1, a2);
   }
   else
   {
      if( a1+a2 >= 180)
      {
         printf("a1 + a2 is too large: %d\n", a1+a2);
      }
      else
      {
         a3 = 180 - (a1+a2);
         printf("a1: %d a2: %d a3: %d\n", a1, a2, a3);
      }
   }

   return 0;
}
```

> > [列表 2.7](#) 首先确保 a1 和 a2 都在 0 到 180 度之间。如果此测试成功，下一个代码部分检查 a1+a2 是否至少为 180：如果为真，则值太大而无法形成三角形。否则，a3 的值设为 180-(a1+a2)，并显示适当的消息。

本章涉及条件逻辑的部分到此结束。在 [第 1 章](#) 中你学习了变量的作用域，接下来几节

包含 C 程序中具有不同作用域的变量的示例。

## C 中的变量作用域

变量的作用域是程序中可以访问已定义变量的区域。C 程序中有三种变量作用域类型：

- 在函数定义或代码块内部（局部变量）
- 在任何函数定义之外（全局变量）
- 作为函数定义中的参数（形式参数）

如果全局定义了与形式参数或函数定义内部相同的名称的变量，则全局变量的优先级较低。请注意，变量不能被定义两次，无论是全局还是局部，这意味着它们必须在不同的作用域中定义。

## C 程序中的全局变量

关于全局变量的规则很简单：尽可能避免使用它们。OOP（面向对象编程）语言流行的一个原因是封装的概念：变量保留在它们所属的类中。变量的值通过“getters”和“setters”（也称为“accessors”和“mutators”）进行访问和修改。

尽管 OOP 语言并不在所有情况下都消除对全局变量的需求，但它们使你能够极大地


减少应用程序中的全局变量数量。本章后面你将看到 C 中使用全局变量的代码示例。

## 全局变量与局部变量

局部变量是在函数或代码块内部声明的，并且它们只能在声明它们的函数或代码块内部访问。因此，局部变量对位于其定义所在块之外的其他函数或代码块不可用。换句话说，当函数返回给调用者时，局部变量的值会被“丢失”。

另一方面，全局变量是在函数之外定义的，通常在 C 程序的初始部分。全局变量在其整个生命周期内保留其值，即直到程序退出为止。

Listing 2.8 显示了 LocalVars.c 的内容，该内容说明了如何定义局部变量。

**清单 2.8：LocalVars.c**

```c
#include <stdio.h>

// global variable declaration
int a=1, b=2, c=3;

void printGlobalVariables()
{
    printf ("Inside the printGlobalVariables function\n");
    printf ("GLOBAL value of a = %d, b = %d and c = %d\n",a,b,c);
}

int main()
{
    printf ("GLOBAL value of a = %d, b = %d and c = %d\n",a,b,c);

    // local variable declaration
    int a, b, c;

    // actual initialization
    a = 10;
    b = 20;
    c = a + b;

    printf ("LOCAL value of a = %d, b = %d and c = %d\n",a,b,c);

    printGlobalVariables();

    return 0;
}
```

Listing 2.8 很简单：整数值 *全局* 变量 a、b 和 c 被声明并初始化，之后其值立即在 main() 函数内部打印。main() 函数内部的下一部分代码声明并初始化 *局部* 整数值变量 a、b 和 c，然后打印它们的值。main() 函数的最后一部分调用 printGlobalVariables() 函数，该函数仅打印 *全局* 整数值变量 a、b 和 c 的值。

Listing 2.8 的输出如下：

```text
GLOBAL value of a = 1, b = 2 and c = 3
LOCAL value of a = 10, b = 20 and c = 30
Inside the printGlobalVariables function
GLOBAL value of a = 1, b = 2 and c = 3
```

请记住，如果以相同名称在全局和局部定义了变量，则在包含该局部变量的函数执行时，局部变量的值优先于全局变量。在函数之外则相反（这必须如此，因为在函数内部定义的局部变量在定义它的函数之外不可访问）。

## C 中的类型转换

类型转换允许你将变量的数据类型转换为另一种数据类型。例如，一组整数的和是整数，但平均值通常是 double 而不是整数。

由于每个 long 数据类型都可以不丢失任何精度地表示任何 int 值，因此 int 值可以自动转换为 long 类型的值。但是，如果你想将 long 视为 int，则可能会丢失精度。同样，如果将 double 值转换为 int 值，也会丢失精度。

通过以下方式使用转换运算符将值从一种类型转换为另一种类型：

`(type_name) expression`

Listing 2.9 显示了 TypeCast.c 的内容，该内容说明了将平均值计算为 int 数据类型与将平均值计算为 double 数据类型之间的区别。

**清单 2.9：TypeCast.c**

```c
#include <stdio.h>

int main()
{
    int x1=11, x2=4, x3=0;
    double x4;

    x3 = x1/x2;
    x4 = (double) x1/x2;

    printf("x1: %d\n",x1);
    printf("x2: %d\n",x2);
    printf("x3: %d\n",x3);
    printf("x4: %f\n",x4);

    return 0;
}
```

Listing 2.9 初始化整数值变量 x1、x2 和 x3。下一段代码块更新 x3，然后初始化 x4 的值。

编译并执行 Listing 2.9 中的代码的输出如下：

```text
x1: 11
x2: 4
x3: 2
x4: 2.750000
```

> **注意**
>
> *类型转换运算符的优先级高于除法。*

sum 的值被转换为 double 类型，然后除以 count，这反过来又产生一个 double 值。类型转换可以是隐式的（由编译器自动执行），也可以使用转换运算符显式进行。

### 整数提升

整数提升是将整数类型“小于” int 或 unsigned int 的值转换为 int 或 unsigned int 的过程。

Listing 2.10 显示了 PromoteVar.c 的内容，该内容说明了将字符添加到具有 int 数据类型的变量的结果。

**清单 2.10：PromoteVar.c**

```c
#include <stdio.h>

int main()
{
   char c = 'A';
   int x = 10;
   int s1 = x + c;
   char s2 = x + c;

   printf("x:  %d\n", x);
   printf("c: %d\n", c);
   printf("s1: %d\n", s1);
   printf("s2: %c\n", s2);

   return 0;
}
```

编译并执行 Listing 2.10 中的代码的输出如下：

```text
x:  10
c: 65
s1: 75
s2: K
```

下一节讨论两个有用的内置函数，它们使你能够复制字符串。在第 4 章中，你将看到 C 中其他有用的内置函数列表。

## C 中的 strcpy() 和 strncpy() 函数

`strcpy(string1, string2)` 函数将 `string2`，包括结束空字符，复制到由 `string1` 指定的位置（请注意，这是一个从右到左的操作）。`strcpy()` 函数对以空字符结尾的字符串进行操作。传递给 `strcpy()` 函数的字符串参数应包含一个空字符（\0）来标记字符串的结尾，因为不会执行长度检查。避免对 `string1` 使用字面字符串，但 `string2` 可以是字面字符串。

*清单 2.11* 显示了 `CopyFunction.c` 的内容，该内容说明了如何使用 `strcpy()` 函数。

**清单 2.11：CopyFunction.c**

```c
#include <stdio.h>
#include <string.h>

#define BUFFER_SIZE 80

int main()
{
   char source[BUFFER_SIZE] = "The initial string";
   char destination[BUFFER_SIZE] = "The target string";
   char *result;

   printf("Before: %s\n", destination);
   result = strcpy(destination, source);
   printf("After:  %s\n", destination);

   return 0;
}
```

*清单 2.11* 使用 `#define` 预处理器（在 *第 7 章* 中更详细地讨论）将 `BUFFER_SIZE` 设置为 80。

接下来，`main()` 函数将字符数组 `source` 和 `destination` 初始化为硬编码字符串。`printf()` 语句显示 `destination` 的内容，然后调用 `strcpy()` 方法将 `source` 的内容复制到变量 `destination`，之后另一个 `printf()` 语句显示 `destination` 的新内容。启动 `Listing 2.11` 的输出如下：

```text
Before: The target string
After: The initial string
```

## 字符串和字符串相关函数

C 中的字符串由一系列字符组成。与 Java 等语言不同，C 不提供内置的字符串类型。C 使用字符数组来表示字符串，该字符串始终以 `\0` 结尾。

`Listing 2.12` 显示了 `CharArray.c` 的内容，该内容说明了如何初始化字符数组。

**清单 2.12：CharArray.c**

```c
#include <stdio.h>

char name[4];

int main()
{
  name[0] = 'a';
  name[1] = 'b';
  name[2] = 'c';
  name[3] = '\0';

  return (0);
}
```

Listing 2.12 声明了一个包含 4 个元素的字符数组 name（当前未初始化）。接下来，main() 函数使用字符 "a"、"b" 和 "c" 初始化 name 数组的每个元素。最后一个位置以 '\0' 终止。

### strcpy() 函数

字符串常量由双引号 (“”) 括起来的文本组成，如下所示：

```c
char str[] = "abcd";
```

虽然其他语言（如 Java）允许你将一个字符串赋给另一个字符串，但在 C 中以下语句是非法的：

```c
str = "another string"; // illegal in C
```

正如你在之前的代码示例中看到的，C 提供了内置的 strcpy() 函数将字符串复制到另一个位置。Listing 2.13 显示了 CopyString.c 的内容，该内容说明了如何使用 strcpy() 函数。

**清单 2.13：CopyString.c**

```c
#include <string.h>

char str[4];

int main()
{
    strcpy(str, "abc");
    return (0);
}
```

Listing 2.13 非常简洁：在声明由 4 个元素组成的字符字符串 str 之后，main()

函数将字符串 "abc" 复制到变量 str 中。

此外，您可以指定变长字符串。作为示例，Listing 2.14 显示了 Array50.c 的内容，说明了如何定义一个最多可包含 50 个字符的变量。

### LISTING 2.14: Array50.c

```
#include <string.h>
#include <stdio.h>

char name[50];

int main()
{
    strcpy(name, "abcd"); // Initialize the name
    printf("The name is %s\n", name);

    return (0);
}
```

Listing 2.14 声明了一个长度为 50 的字符变量 name，随后是 main() 函数，该函数调用 strcpy() 命令将字符串 abcd 复制到变量 name。

尽管 name 数组的大小为 50，但前述代码块中字符串 abcd 的长度为 4。您可以将长度最多为 49 个字符的任意字符串复制到变量 name：一个位置（通常是最右边的那个）保留给 '\0'，用于指示字符串结束。字符串变量的维度为 50，因为我们假设所有名称最多为 49 个字符长。

然而，如果您尝试将长度大于 49 的字符串赋给 name 变量，此复制操作需要未分配给封闭程序的内存。因此，程序将异常执行，或提供错误结果，甚至崩溃。

`Listing 2.15` 显示了 `Strcpy1.c` 的内容，说明了如何使用 `strcpy()` 函数初始化三个字符数组。

### LISTING 2.15: Strcpy1.c

```c
#include <stdio.h>
#include <string.h>

char first[100];
char last[100];
char fullName[200];

int main()
{
    strcpy(first, "John");
    strcpy(last, "Smith");
    strcpy(fullName, first);

    strcat(fullName, " ");
    strcat(fullName, last);
    printf("The full name is %s\n", fullName);

    return 0;
}
```

`Listing 2.15` 声明了字符变量 `first`、`last` 和 `fullName`，其长度分别为 100、100 和 200。

接下来，`main()` 函数调用 `strcpy()` 函数将字符串 `John`、`Smith` 和变量 `first` 分别复制到变量 `first`、`last` 和 `fullName` 中。

代码的最后一部分调用 `strcat()` 函数将变量 `fullName` 与空格（ " " ）连接起来，并且 `strcat()` 的第二次调用将 `last` 的值追加到变量 `fullName`。最后的 printf() 语句显示变量 fullName 的值。此程序的输出为：

The full name is John Smith

## 处理 C 中的用户输入

有三对内置 C 函数用于读取用户输入然后打印结果。三个输入函数分别读取一个字符、一行以及指定格式的一行。第一个输入函数是 getchar()，它从标准输入读取单个字符（并返回一个 int）。

第二个输入函数是 gets()，它返回一个字符指针。使用此方法的使用被推迟到您学习 C 指针时（第 5 章和第 6 章）。第三个输入函数是 scanf()，它从标准输入流读取输入并根据提供的格式扫描该输入。scanf() 函数也涉及指针（因此将在讨论指针之后推迟）。

### The getchar() & putchar() Functions: Single Character Functions

标准并未指定 getchar() 和 putchar() 是否为宏。然而，其返回值是 int（而不是 char 值）的原因是它们面向流并且可以与文件交互。如果您想遵循安全的编码实践，这一要点很重要。

键盘输入提供 char 值，但文件输入可以生成 int 值，例如 EOF 或文件结束值，它是一个 int。文件输出可以生成 int

printf() 函数的形式为 printf(const char *format,...)，正如您在 [Chapter 1] 中看到的那样，此函数根据特定调用中指定的格式将输出写入标准输出流。例如，[Listing 2.16] 显示了 PrintSamples.c 的内容，说明了 printf() 函数与各种数据类型和格式一起使用。

### LISTING 2.16: PrintSamples.c

```c
#include <stdio.h>

int main()
{
    int x1 = 23;
    double x2 = 1234.56789;

    printf("Hello World\n");
    printf("%s\n", "Hello World");
    printf("%d\n", 17);
    printf("%s %d %5.2f\n", "Hello World", x1, x2);

    return 0;
}
```

[Listing 2.16] 包含一个 main() 函数，将变量 x1 初始化为 23，将变量 x2 初始化为 1234.56789。下一部分由四个 printf() 语句组成，用于显示各种数字和字符串。

通过 printf() 函数显示的值的格式可以是一个简单的常量字符串，但您可以指定 %s、%d、%c、%f 等，以便分别打印或读取字符串、整数、字符或浮点数。根据您的需求，还有许多其他格式选项可用。[Listing 2.13] 的输出如下：

Hello World

compiler. 此外，如果您想确保安全函数不可见，请将前述宏设置为 0 而不是 1。

除了 C11 中的新边界检查安全函数外，您还应使用 fgets() 函数代替 gets() 函数。避免使用后者函数，因为您无法确定该函数将读取多少个字符（除非您事先知道）。由于您无法预测 gets() 为了存储用户输入的字符串而需要在内存中占用多少“空间”，字符串可能会破坏不属于当前正在执行的 C 程序的内存。因此，gets() 不能在每种情况下都安全使用。本章后面您将看到 fgets() 函数和 gets() 函数行为的示例。

C11 的 ANSI/ISO 委员会还寻求标准化在大多数大型编译器中已存在的知名工作范式和功能（而不是实现新功能）。C11 标准 N1570 草案在此处：

[www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf)

描述从 C99 到 C11 的更改的文档在此处：

[https://en.wikipedia.org/wiki/C11_(C_standard_revision)#Changes_from_C99](https://en.wikipedia.org/wiki/C11_(C_standard_revision)#Changes_from_C99)

目前似乎没有任何完全符合 C11 的编译器实现。

除了新的安全函数外，C11 还对 C 语言进行了补充，其中一些是：

- Unicode support
- floating point support for IEC 60559 (optional)
- multi-threading support (optional)
- anonymous structs and unions
- the alignas and alignof keywords
- bounds checking functions (string library)

执行在线搜索以获取有关此列表中各项的更多信息。

## Checking for C11 Compliance

检查 C11 合规性的第一种（也是最简单）方法是在编译 C 程序时指定开关 -std=c11，其示例如下所示：

```
gcc -std=c11 HelloWorld.c -o HelloWorld
```

然而，直到您启动可执行文件时才不会看到不合规的警告消息（即编译步骤不会生成不合规消息），如本节后面所示。

其次，将在先前的 C 语言标准修订版 ISO/IEC 9899:1999/Cor.3:2007(E) 中弃用的 gets 函数替换为名为 gets_s 的新安全替代方案（如果可用），或使用 fgets 函数。

作为一个简单的说明，这里有一个名为 SafeStrcpy1.c 的代码示例，尝试使用 strcpy_s 函数：

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
#include <string.h>

char first[100];

int main()
{
    strncpy_s(first, "John");
    return 0;
}
```

以下是编译 SafeStrcpy1.c 期间的输出：

```
SafeStrcpy1.c: In function 'main':
SafeStrcpy1.c:9:4: warning: implicit declaration of function 'strncpy_s'; did you mean 'strcpy'? [-Wimplicit-function-declaration]
    strncpy_s(first, "John");
    ^~~~~~~~
    strcpy
Undefined symbols for architecture x86_64:
    "_strcpy_s", referenced from:
    _main in cck3IS8F.o
ld: symbol(s) not found for architecture x86_64
collect2: error: ld returned 1 exit status
```

前述代码在配备 MacOS Sierra（版本 10.12.6）的 Macbook Pro 上，并且以下是编译步骤中使用的 gcc 的信息：

```
$ gcc --version
gcc (MacPorts gcc7 7.2.0_0) 7.2.0
Copyright (C) 2017 Free Software Foundation, Inc.
```

## What about C17 Compliance?

C17 中没有包含新功能。然而，C17 将包含所有已接受的 C11 缺陷报告，但没有新功能。根据 GCC 参考，C17 是 C11 标准的错误修复版本，其中集成了 DR（缺陷报告）解决方案。C17 提供开关 -std=c17（对应于 C11 的 -std=c11），以及 -std=gnu17（而不是 -std=gnu11）。

如果您感兴趣，C17 报告可在此处购买（USD 116）：




## fgets() 函数（C11 兼容）

本节包含一个代码示例，展示 fgets() 函数的行为与 gets() 函数（将在下一节讨论）有何不同。无论你是否阅读代码示例，都请务必记住使用 fgets() 函数并 *永远不要* 使用 gets() 函数。

列表 2.17 显示了 C 程序 `testfgets.c` 的内容，该程序说明了 fgets() 函数的使用。

### 列表 2.17：testfgets.c

```c
#include <stdio.h>
#define MAX 10
int main()
{
    char buf[MAX];
    fgets(buf, MAX, stdin);
    printf("string is: %s\n", buf);
    return 0;
}
```

代码非常简单：用户会被提示输入一个字符串，然后该字符串会在命令行中重新显示。现在按如下方式编译列表 2.17 中的代码：

```
gcc -std=c11 testfgets.c -o testfgets
```

启动可执行文件并输入一个字符串：

```
$ ./testfgets
this is a long string and let's see what happens
prompt.
```

现在按如下方式编译列表 2.18 中的代码：

```
gcc -std=c11 testgets.c -o testgets
```

启动可执行文件并输入一个字符串：

```
$ ./testgets
warning: this program uses gets(), which is unsafe.
Enter a string: this is a long string and let's see what happens
string is: this is a long string and let's see what happens
Segmentation fault: 11
```

> 注意  只有在启动可执行文件时才会显示不安全消息，而在编译/链接步骤期间不会显示。

使用安全字符串函数存在一个显著的阻碍：尽管自 C11 起 C 标准中规定了安全函数（如 `strcpy_s` 和 `strtok_s` 等），但在 C11 中它们实际上是可选的，因为并非所有标准库实现都需要提供可选特性。因此，为了将 `strcpy_s` 和 `strtok_s` 以及所有其他安全字符串函数引入你的系统，你需要 1) 找到一个实现它们全部的库，或 2) 自己实现它们。

最后，以下网站允许你将代码片段复制/粘贴到其网页中以检查 C11 合规性：

- https://godbolt.org/
- https://wandbox.org/

## 从命令行读取单个字符

列表 2.19 显示了 `ReadSingleChar.c` 的内容，说明如何在 C 程序中使用 `getchar()` 函数从标准输入读取单个字符，然后使用 `putchar()` 函数打印该字符。

### 列表 2.19：ReadSingleChar.c

```c
#include <stdio.h>

int main()
{
    int c;

    printf( "Enter a value :");
    c = getchar();

    printf( "\nYou entered: ");
    putchar( c );

    return 0;
}
```

列表 2.19 包含一个 `main()` 函数，该函数声明了整数变量 `c`，随后是一个提示用户输入的 `printf()` 语句。用户在键盘上按下键后，内置的 `getchar()` C 函数会将该值赋给变量 `c`。代码的下一部分显示用户在键盘上输入的值。启动列表 2.19 中代码的示例调用如下：

```
Enter a value :f
You entered: f
```

## 从命令行读取未格式化行

列表 2.20 显示了 `ReadLine.c` 的内容，说明如何从键盘读取一行文本并显示其长度。

### 列表 2.20：ReadLine.c

```c
#include <string.h>
#include <stdio.h>

char line[100];

int main()
{
    printf("Enter a line: ");
    fgets(line, sizeof(line), stdin);
    printf("The length of the line is: %d\n", strlen(line));

    return (0);
}
```

列表 2.20 声明了一个长度为 100 的字符数组 `line`，随后是一个包含提示用户输入的 `printf()` 语句的 `main()` 函数。这次用户可以输入多个字符（即长度最多为 99 的完整句子）。用户提供输入后，内置的 `fgets()` C 函数会将该输入赋给变量 `line`。代码的下一部分显示用户在键盘上输入的输入字符串的长度。启动列表 2.20 中代码的示例调用如下：

```
Enter a line: this is a simple input line
The length of the line is: 28
```

**启动列表 2.20 中代码的另一个调用如下：**

```
Enter a line: abcd
The length of the line is: 5
```

请注意，字符串 abcd 只有四个字符：额外的字符从何而来？函数 fgets() 也将换行符 `'\n'` 包含在字符串中（即第五个字符）。

sizeof() 函数还提供了一种方便的方法来将读取的字符数限制为变量所能容纳的最大数量。

这里有一个有趣的问题：给定一个未知原始数据类型和未知长度的数组 myarr，如何确定数组中的项目数？

简单（优雅？）的答案涉及 sizeof() 运算符，如下所示：

```
// myarr is defined elsewhere
int len = sizeof(myarr)/sizeof(myarr[0]);
```

由于数组 myarr 的元素具有相同的数据类型，它们都具有相同的大小，这意味着数组 myarr 的长度是数组中第一个（或任何其他）元素的大小的倍数。该运算符将在第 6 章中更详细地讨论。

## 从命令行读取格式化行

列表 2.21 显示了 `ReadFormattedLine.c` 的内容，说明如何在 C 程序中通过 `scanf()` 函数从标准输入读取格式化行。

### 列表 2.21：ReadFormattedLine.c

```c
#include <stdio.h>

int main( )
{
    char str[100];
    int i, numfilled;

    printf(" Enter a string and an int :");
    numfilled = scanf("%s %d", str, &i);

    printf("\nNumber of filled values: %d\n",numfilled);
    printf("\nYou entered values for the string and the int");
    printf("\nYou entered the string %s and the number %d ", str, i);

    return 0;
}
```

列表 2.21 包含一个 `main()` 函数，该函数声明了一个长度为 100 的字符数组 `str`，并声明了一个整数值变量 `i`。接下来，一个 `printf()` 语句提示用户输入。这次用户可以输入一个字符串和一个整数，之后内置的 `scanf()` C 函数会将输入字符串赋给 `str`，将输入整数赋给 `i`。

有两点需要注意。首先，如果你输入一个字符串并按下 <RETURN> 键，程序似乎会“挂起”，因为它等待你输入一个数字。其次，超出你输入的数字的任何额外输入都会被忽略（见下面的示例）。

用户提供输入后，`printf()` 函数会显示这两个变量的值。启动列表 2.21 中代码的示例调用如下：

```
Enter a string and an int: abc 3

Number of filled values: 2

You entered values for the string and the int
You entered the string abc and the number 3
```

另一个启动 *列表 2.21* 中代码的示例调用如下：

```
Enter a string and an int: abc 3 4 5

Number of filled values: 2

You entered values for the string and the int
You entered the string abc and the number 3
```

## scanf() 函数的行为（可选）

*列表 2.21* 中 `scanf()` 函数的行为取决于提供的输入类型。具体来说，如果提供的输入与格式字符串不匹配，变量永远不会被初始化。C 规范非常明确：一旦输入中出现一个字符与 `scanf()` 函数试图匹配的格式字符串的“当前部分”不匹配，匹配过程就会 *立即* 停止，而不会再读取任何字符或为更多变量赋值。此外，匹配过程失败后发生的任何事情都是“未定义行为”。

例如，考虑在启动 *列表 2.21* 中的代码后，用户提供以下输入值时会发生什么：

```
Enter a string and an int: abc x y z

Number of filled values: 1

You entered values for the string and the int
You entered the string abc and the number 1
```



显然，输入值 x 与报告值 1 之间存在不匹配，而二者完全无关。如何检测这种情况？一种方法是在调用 `scanf()` 之前为变量赋予已知值。如果变量有一个已知值，然后在 `scanf()` 失败的过程中将其设置为 1，那将是 `scanf()` 实现中的一个严重缺陷，而这极不可能发生。

试图对“未定义行为”进行推理本质上是在浪费时间，因为绝对*任何事情*都可能发生。不过，如果你想要某种直观理解，这里概述一下可能正在发生的情况。由于变量 `i`（在之前的调用中）尚未初始化，因此从编译器的角度来看，它的“生命周期”尚未开始。该变量与另一个变量共享一个寄存器，而那个变量的生命周期在该变量初始化之前就结束了。另一个变量在某些条件下恰好获得了值 1，并且由于该变量未初始化，它只是获得寄存器中残留的任何内容。因此，*绝不能读取未初始化的变量*：编译器可以假定变量在初始化之前永远不会被读取，并且它可以并且确实基于这些假设进行优化。

请注意，未定义行为不仅没有意义，而且一旦编译器可能确定它不可避免，它就可能发生。按照清单 2.21 中代码的写法，一旦 `scanf()` 函数以不完整的结果结束，你就有了“未定义行为”。

在本节开头的示例中，“绝对做任何事情”恰好是“在某些特定情况下，偶尔将变量 i 的值设置为 1”。这不是编译器缺陷，因为根据定义，一旦你有了“未定义行为”，就不存在编译器缺陷这回事。此时，对编译器生成什么代码没有任何要求。

当你想从命令行读取字符串和数字时，还有一些其他有趣的场景，其中一些在此处描述：

[https://stackoverflow.com/questions/20867382/c-programming-scanf-not-working-correctly](https://stackoverflow.com/questions/20867382/c-programming-scanf-not-working-correctly)

## 从命令行读取多个字符串

清单 2.22 显示了 `FirstLastName.c` 的内容，它说明了如何提示用户输入一个人的名字和姓氏。

### 清单 2.22：FirstLastName.c

```c
#include <stdio.h>
#include <string.h>

char first[100];
char last[100];
char full[200];

int main()
{
    printf("Enter first name: ");
    fgets(first, sizeof(first), stdin);

    // see comment below about this snippet:
    // first[strlen(first)-1] = '\0';
    printf("Enter last name: ");
    fgets(last, sizeof(last), stdin);

    strcpy(full, first);
    strcat(full, " ");
    strcat(full, last);

    printf("The name is %s\n", full);

    return (0);
}
```

清单 2.22 声明了字符变量 first、last 和 fullName，长度分别为 100、100 和 200。接下来，main() 函数使用 2 个不同的 printf() 语句提示用户输入名字和姓氏，并使用内置的 gets() C 函数捕获这些输入值。

代码的下一部分使用内置的 strcpy() C 函数将 first 复制到变量 full。接下来，内置的 strcat() 函数追加一个空格（" "），然后将 last 追加到变量 full。下面是启动清单 2.22 中代码的示例调用：

```
Enter first name: john
Enter last name: smith
The name is john
smith
```

请注意，全名显示在单独的行上，这是因为用户输入名字后必须按 <RETURN>，而 <RETURN> 字符被包含在变量 full 中。我们可以通过取消注释以下代码片段来简单地移除 <RETURN> 字符：

```
first[strlen(first)-1] = '\0';
```

然而，如果变量 first 是空字符串，启用前面的代码片段可能会产生未定义行为，如果该程序接收空文件作为输入，就可能发生这种情况。清单 2.22 中代码的这一方面说明了在代码中无意引入缺陷是多么容易。解决方案很简单：*在通过前面的代码片段截断变量 first 中的字符串之前，测试 strlen(first) 的值以确保它不是 0。*

重新编译修改后的代码并在命令行重新启动，以下是一个示例调用：

```
Enter first name: john
Enter last name: smith
The name is john smith
```

还有一点需要记住：如果变量 first 是空字符串，移除 <RETURN> 字符的前述代码片段会导致未定义行为。因此，你需要修改清单 2.22 中的代码，在截断字符串之前测试 strlen(first) 的值以确保它不是 0。

## 用于数值计算的用户输入

清单 2.23 显示了 SimpleAdder.c 的内容，它说明了如何提示用户输入，然后使用 fgets() 和 sscanf() 函数获取输入，所有这些都发生在 while 循环内。

### 清单 2.23：SimpleAdder.c

```c
#include <stdio.h>

char line[100]; // line of data from the input
int result;  // the result of the calculations
char operator; // operator the user specified
int value;    // value specified after the operator

int main()
{
    result = 0; // initialize the final result

    while (1) {
        printf("Result: %d\n", result);
        printf("Enter operator and number: ");

        fgets(line, sizeof(line), stdin);
        sscanf(line, "%c %d", &operator, &value);

        if (operator == '+') { // why does "=" also work?
            result += value;
        }
        else if (operator == '-') {
            result -= value;
        }

        else {
            printf("Exiting loop: unknown operator: %c\n",
                   operator);
            break;
        }
    }

    return 0;
}
```

清单 2.23 首先将变量 result 初始化为 0。程序的主体是一个 while 循环，重复执行直到遇到 break 语句。while 循环的主体包含一个代码块，提示用户输入运算符和数字，如下所示：

```
printf("Enter operator and number: ");
```

函数以及使用 scanf()
函数进行格式化输入。

## 第3章

### 循环和数组

本章包含演示如何在 C 中使用简单循环、嵌套循环和数组的代码示例。这些代码示例执行与字符串相关的任务，以及使用数字数组和字符串数组的各种任务。此外，许多代码示例包含 `if/else` 条件逻辑，这些逻辑在[第2章](#)中介绍过（如果你还没有阅读该章，请先阅读）。

本章第一部分讨论基本循环、一维和多维数组，以及如何在数组中执行线性搜索。本章第二部分计算数字数组中的最大值和最小值，如何向数组中插入元素，以及如何从数组中删除元素。

本章第三部分包含 `while` 循环、`do-while` 循环，以及涉及 while 循环的字符串相关示例。本节的代码示例还包含条件逻辑，这些逻辑在[第2章](#)中介绍过。最后一节包含确定正整数因子的代码示例，以及如何检查一个数是否为质数。

## 使用 for 循环

清单 3.1 显示了 ForLoop.c 的内容，向你展示如何在 C 中使用 for 循环。

### 清单 3.1：ForLoop.c

```c
#include <stdio.h>

int main()
{
   int max=5;
   for(int i=0; i<max; i++)
   {
      printf("i : %d\n", i);
   }

   return 0;
}
```

清单 3.1 很直接：一个 `main()` 函数初始化整型变量 max（其值为 5），然后是一个 for 循环，打印 0 到 max 之间的整数。

启动清单 3.1 中的 C 程序后的输出如下：

```
i : 0
i : 1
i : 2
i : 3
i : 4
```

## 在 for 循环中使用 break 和 continue



清单 3.2 展示了 BreakContinue.c 的内容，它向你展示如何在 C 的 for 循环中使用 break 和 continue 语句。

### 清单 3.2：BreakContinue.c

```c
#include <stdio.h>

int main()
{
    int max=5;

    for(int i=0; i<max; i++)
    {
        if(i == 3 ) continue;
        if(i == 4 ) break;
        printf("i : %d\n", i);
    }

    return 0;
}
```

清单 3.2 包含一个带有条件逻辑的 for 循环，用于检查循环变量 i 的值。如果 i 的值等于 3，代码会“跳转”到循环顶部并递增 i 的值。如果 i 的值等于 4，代码会退出循环，并实际上结束该 C 程序的执行。

因此，只有在变量 i 等于 0、1 或 2 时，才会执行 printf() 语句。运行清单 3.2 中 C 程序后的输出如下：

i : 0
i : 1
i : 2

## 检查闰年

快速提醒一下，*闰年*是满足以下两个条件的正（整数值）年份：

- 该年份是 4 的倍数，并且
- 如果该年份是世纪年，则该年份必须是 400 的倍数

闰年的示例包括：400、1492、1776、2000、2012 和 2472（注意，这些世纪年是 400 的倍数）。不是闰年的年份示例包括：100、1370、1510、1900 和 2011（注意，这些世纪年*不是* 400 的倍数）。

清单 3.3 展示了 `LeapYear.c` 的内容，它说明如何在 C 程序中使用 if-else 逻辑来判断某一年是否为闰年。

### 清单 3.3：LeapYear.c

```c
#include <stdio.h>

int main()
{
    int years[6] = {1900, 1953, 1958, 2000, 2004, 2006};
    int year=0, leapyear=0;

    int len = sizeof(years)/sizeof(years[0]);

    for(int i=0; i<len; i++)
    {
        year = years[i];

        if( year % 4 == 0)
        {
            leapyear = 1;
        }
        // "leap centuries" must be multiples of 400
        if( (year % 100 == 0) && (year % 400 != 0) )
        {
            leapyear = 0;
        }
        else // not a multiple of 4
        {
            leapyear = 0;
        }

        if( leapyear == 0)
        {
            printf("%d: not a leap year\n",year);
        }
        else
        {
            printf("%d: leap year\n",year);
        }

    }

    return 0;
}
```

清单 3.3 定义了“标志”变量 leapyear，以及包含六个正整数的整数值数组 years。接下来，for 循环遍历 years 数组的元素，以确定哪一年（如果有）是闰年。

外层 if 语句检查当前年份是否为 4 的倍数：如果是，则它是闰年（并将 leapyear 设为 1）；如果不是，则 else 子句将 leapyear 设为 0（因为它不是闰年）。

还必须执行一项额外检查。内层 if 语句检查当前年份是否为 100 的倍数且不是 400 的倍数：如果情况如此，则当前年份不是闰年，因此必须将变量 leapyear 设为 0（因为它的值已被外层 if 语句设为 1）。

for 循环的底部包含条件逻辑，它会根据变量 leapyear 的值显示相应消息。

清单 3.3 的输出如下：

1900: not a leap year
1953: not a leap year
1958: not a leap year
2000: leap year
2004: leap year
2006: not a leap year

## 检查字母类型

字母和数字都有 ASCII 值，并且可以检查它们的类型。清单 3.4 展示了 Alphabetic.c 的内容，它说明如何在 C 中检查字母字符。

### 清单 3.4：Alphabetic.c

```c
#include <stdio.h>
#include <ctype.h>

<｜｜begin▁of▁sentence｜｜>## 清单 3.5

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char ch, str1[] = "This is a String";
    int lcount=0, ucount=0;

    int len1 = strlen(str1);

    for(int i=0; i<len1; i++)
    {
        ch = str1[i];
        if(('a' <= ch) && (ch <= 'z'))
        {
            lcount++;
        }
        else if (('A' <= ch) && (ch <= 'Z'))
        {
            ucount++;
        }
    }

    printf("Original:  %s\n",str1);
    printf("Lower count: %d\n",lcount);
    printf("Upper count: %d\n",ucount);

    return 0;
}
```

清单 3.5 首先定义字符串 str1，然后用字符串 str1 的长度初始化整数值变量 len1。清单 3.5 的下一部分包含一个 for 循环，其循环变量 i 在 0 到 len1 之间迭代，并用 str1 数组中第 i 个位置的字符初始化变量 ch。

接下来，条件逻辑检查 ch 是否位于字母 “A” 和 “Z” 之间，在这种情况下变量 lcount

### 清单 3.6

```c
{
  ch = line[i];

  if(isblank(ch))
  {
    printf("%c is a blank\n", ch);
  }
  else if(isdigit(ch))
  {
    printf("%c is a digit\n", ch);
  }
  else if(isupper(ch))
  {
    printf("%c is uppercase\n", ch);
  }
  else if(islower(ch))
  {
    printf("%c is uppercase\n", ch);
  }
  else if(ispunct(ch))
  {
    printf("%c is punctuation\n", ch);
  }
  else
  {
    printf("%c is other type\n", ch);
  }

  return 0;
}
```

清单 3.6 定义字符串变量 line，然后是一个 for 循环，它遍历字符串 line 中的每个字符。接下来，if/else 条件逻辑调用 C 内置函数 isblank(ch)、isdigit(ch)、isupper(ch)、islower(ch) 和 ispunct(ch)，分别检查字符是空白、数字、大写字母、小写字母还是标点符号。如果条件检查为真，则打印相应的文本消息。

编译并执行清单 3.6 中代码后的输出如下：

A is uppercase
b is uppercase
c is uppercase
3 is a digit
  is a blank
: is punctuation

清单 3.6 包含各种用于测试给定字符类型的内置函数。此外，C 还支持以下有用的内置字符相关函数：

- iscntrl() 测试控制字符。
- isgraph() 测试可打印字符（不包括空格）。
- isprint() 测试可打印字符（包括空格）。
- ispunct() 测试区域设置中定义的标点字符。
- isspace() 测试空白字符。
- isxdigit() 测试宽十六进制数字 0 到 9、a 到 f 或 A 到 F。

## 使用数组

正如你在第 1 章所见，C 中的数组声明需要元素类型以及数组所需的元素数量：

```
type arrayName [ arraySize ];
```

前面的代码片段用于定义一维数组。arraySize 的值必须是大于零的整数常量，而类型可以是任何有效的 C 数据类型。例如，要声明一个名为 balance、类型为 double 的 10 元素数组，请使用以下语句：

```
double balance[10];
```

如你所见，balance 数组最多可容纳 10 个 double 数字，以下小节包含使用 balance 数组的示例。

### 初始化数组

C 数组的索引值从 0 开始，数组中最后一个元素的索引值是数组大小减 1。C 允许通过两种方式初始化数组中的值：一次初始化一个元素，或通过单条语句初始化。后者的示例如下：

```
double balance[5] = {1.5, 2.0, 3.4, 997.0, 25.0};
```

请注意，花括号 { } 内的值数量等于方括号 [ ] 中指定的数量。你也可以省略数组大小，编译器会处理初始化，示例如下：

```
double balance[] = {1.5, 2.0, 3.4, 997.0, 25.0, -123, 777};
```

初始化数组后，你还可以更新元素的值，如下所示：

```
balance[2] = 3000.0;
```

### 数组值

通过元素在数组中的索引来访问数组元素。例如，假设 balance 数组已按上述方式初始化：


```c
balance[2] *= 3;
```

清单 3.7 显示了 ArrayElems.c 的内容，该内容说明了如何访问数组中的元素。

### 清单 3.7：ArrayElems.c

```c
#include <stdio.h>

int main()
{
    int arr1[10];

    // initialize element i with value i+100
    for (int i=0; i<10; i++ )
    {
        arr1[i] = i + 100;
    }

    for (int j=0; j<10; j++ )
    {
        printf("Element[%d] = %d\n", j, arr1[j] );
    }

    return 0;
}
```

清单 3.7 包含一个 main() 函数，该函数定义了包含 10 个元素的整数数组 arr1，然后是一个循环，将每个元素初始化为其索引位置加 100。第二个循环 simply 显示数组 arr1 中每个元素的值。运行清单 3.7 中的代码，你将看到以下输出：

```text
Element[0] = 100
Element[1] = 101
Element[2] = 102
Element[3] = 103
Element[4] = 104
Element[5] = 105
Element[6] = 106
Element[7] = 107
Element[8] = 108
Element[9] = 109
```

## C 函数与数组

C 支持多维数组（将在下一节讨论），你可以将其传递给函数（将在第 4 章讨论）。你也可以初始化一个指向数组的指针并将该指针传递给函数。此外，你可以定义返回数组或指向数组的指针的 C 函数。正如你稍后会看到的，只需指定数组的名称（不带索引）即可初始化指向数组第一个元素的指针。

## 多维数组

以下每个代码片段都说明了在 C 中初始化 2 x 3 整数数组的几种方法：

```c
int arr1[2][3] = {{1,2,3}, {4,5,6}};
int arr2[][3] = {{1,2,3}, {4,5,6}};
int arr3[2][3] = {1,2,3,4,5,6};
```

清单 3.8 显示了 MultiDimArray1.c 的内容，展示了如何计算多维数组中条目的总和。

### 清单 3.8：MultiDimArray1.c

```c
#include <stdio.h>

int main()
{
    double total=0.0, rowSum=0.0;
    int row=2, col=3;

    int arr1[2][3] = {{1,2,3}, {4,5,6}};

    for(int i=0; i<row; i++)
    {
        rowSum=0.0;
        for(int j=0; j<col; j++)
        {
            total +=  arr1[i][j];
            rowSum += arr1[i][j];
        }

        printf("Sum of row %d: %f\n", i, rowSum);
    }

    printf("Total Sum: %f\n", total);

    return 0;
}
```

清单 3.8 包含变量 total 和 rowSum，分别用于存储数组中所有元素的总和以及一行元素的总和。接下来，数组 arr1 是一个 2x3 数组（即它由两行三列组成），已用一组值进行初始化。

清单 3.8 中的下一部分包含一个外层 for 循环，用于遍历 arr1 的行。在将 rowSum 初始化为 0.0 之后，内层循环遍历当前行的列。请注意，total 变量和 rowSum 变量都通过 arr1[i][j] 的量递增。当内层循环完成后，printf() 语句会显示正确行中元素的总和。

请注意（与变量 rowSum 不同），变量 total 没有重新初始化为 0，因为我们想要计算数组 arr1 中所有元素的总和。事实上，当外层循环执行完毕后，清单 3.8 中 `main()` 函数的底部包含一个 `printf()` 语句，用于打印所有元素的总和。清单 3.8 的输出如下：

```text
Sum of row 0: 6.000000
Sum of row 1: 15.000000
Total Sum:   21.000000
```

另一个需要注意的点：C11 支持变长数组，但它们不能被初始化。例如，如果你使用变量 `row` 和 `col`（值分别为 2 和 3）来定义 `arr1` 的维度，在编译期间你将看到以下错误：

```text
MultiDimArray1.c:7:13: error: variable-sized object may not be initialized
    int arr1[row][col]={{1,2,3}, {4,5,6}};
           ^~~
1 error generated.
```

## 计算方阵的转置

方阵的转置是将行和列位置互换的结果。换句话说，如果矩阵 A 中 `(i,j)` 位置元素的数值为 `a(i,j)`，则矩阵 A 转置中 `(i,j)` 位置元素的数值为 `a(j,i)`。

清单 3.9 显示了 `Transpose.c` 的内容，说明了如何计算方阵的转置。

### 清单 3.9：Transpose.c

```c
#include <stdio.h>

int main()
{
    int row=3, col=3, temp=0;
    int arr1[3][3]= {{1,2,3},
                  {4,5,6},
                  {7,8,9}};

    // display original matrix
    printf("Original\n");
    for(int i=0; i<row; i++)
    {
        printf("Row %d: ", i);
        for(int j=0; j<col; j++)
        {
            printf("%d ", arr1[i][j]);
        }
        printf("\n");
    }

    for(int i=1; i<row; i++)
    {
        for(int j=0; j<i; j++)
        {
            temp = arr1[i][j];
            arr1[i][j] = arr1[j][i];
            arr1[j][i] = temp;
        }
    }

    // display transposed matrix
    printf("Transpose\n");
    for(int i=0; i<row; i++)
    {
        printf("Row %d: ", i);
        for(int j=0; j<col; j++)
        {
            printf("%d ", arr1[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

清单 3.9 包含一个 main() 函数，首先初始化几个标量变量，然后用整数值初始化 3x3 数组 arr1。接下来，一个嵌套循环显示数组 arr1 中的值。

第二个循环包含一个嵌套循环，通过一个名为 temp 的临时存储变量将位置 (i,j) 中的条目与位置 (j,i) 中的条目进行“交换”。这个代码块是一种标准技术，你将在几乎每种编程语言中都看到它，因此值得将其记在心里。

第三个循环包含一个嵌套循环，用于显示数组 arr1 中的新值。清单 3.9 的输出如下：

```text
Original
Row 0: 1 2 3
Row 1: 4 5 6
Row 2: 7 8 9
Transpose
Row 0: 1 4 7
Row 1: 2 5 8
Row 2: 3 6 9
```

如你所见，清单 3.9 包含两个相同的代码块：更好的解决方案是使用一个函数（将在第 3 章讨论）来打印数组的内容。

## 数组中的线性搜索

清单 3.10 显示了 LinearSearch.c 的内容，展示了如何使用简单的循环来确定给定的整数是否在 C 整数数组中。

### 清单 3.10：LinearSearch.c

```c
#include <stdio.h>

int main()
{
    int numbers[] = {15, 3, 99, -4, 25, 8};
    int value = 25, pos = -1;
    int count = sizeof(numbers)/sizeof(numbers[0]);

    for(int i=0; i<count; i++)
    {
        if(value == numbers[i])
        {
            pos = i;
            break;
        }
    }

    printf("Array: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    printf("Value: %d\n",value);
    printf("Pos:  %d\n",pos);

    return 0;
}
```

清单 3.10 包含一个 main() 函数，用 6 个整数初始化 numbers 数组，以及几个标量变量。接下来，代码片段（以粗体显示）计算整个数组的大小除以第一个元素的大小，结果赋给变量 count。该值等于数组 numbers 中元素的数量。

下一部分代码是一个循环，遍历数组 numbers 中的元素以查找等于变量 value 的元素。如果找到匹配项，则数组中的索引将被赋给变量 pos。最后一部分代码显示 value 和 pos（如果未找到匹配项，则为 -1）。清单 3.10 的输出如下：

```text
Array: 15 3 99 -4 25 8
Value: 25
Pos:  4
```

## 反转数字数组

清单 3.11 显示了 `ReverseArray1.c` 的内容，其中包含一个 for 循环，用于在 C 程序中反转数字数组。

### 清单 3.11：ReverseArray1.c

```c
#include <stdio.h>

int main()
{
    int numbers[6] = {15, 3, 99, -4, 25, 8};
    int reverse[6];
    int count=6;

    for(int i=0; i<count; i++)
    {
        reverse[count-1-i] = numbers[i];
    }

    printf("Array:  ");
    for(int i=0; i<count; i++)
    {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    printf("Reverse: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ", reverse[i]);
    }
    printf("\n");

    return 0;
}
```

清单 3.11 包含一个 main() 函数，用 6 个整数初始化 numbers 数组，然后声明一个包含 6 个整数的 reverse 数组，然后是初始值为 6 的 count 变量。

第一个循环以相反的顺序用 numbers 数组中的值初始化 reverse 数组的内容。例如，reverse[0] 被赋值为 numbers[5]，reverse[1] 被赋值为 numbers[4]，以此类推。

第二个循环显示 numbers 数组的内容，第三个循环显示 reverse 数组的内容。运行清单 3.11 中的 C 程序的输出如下：

```text
Array: 15 3 99 -4 25 8
Reverse: 8 25 -4 99 3 15
```

## 查找数组中的最大值和最小值



清单 3.12 显示了 MaxAndMinValue.c 的内容，该内容展示了如何在 C 中使用简单的循环（带条件逻辑）来查找数组中的最大值和最小值。

### LISTING 3.12: MaxAndMinValue.c

```
    #include <stdio.h>

    int main()
    {
        int numbers[] = {15, 3, 99, -4, 25, 8};
        int min=numbers[0], max=numbers[0];
        int count=sizeof(numbers)/sizeof(numbers[0]);

        for(int i=0; i<count; i++)
        {
            if(min > numbers[i])
            {
                min = numbers[i];
            }

            if(max < numbers[i])
            {
                max = numbers[i];
            }
        }

        printf("Array: ");
        for(int i=0; i<count; i++)
        {
            printf("%d ", numbers[i]);
        }
        printf("\n");

        printf("Max:  %d\n",max);
        printf("Min:  %d\n",min);
        return 0;
    }
```

清单 3.12 包含一个 main() 函数，该函数使用 6 个整数初始化 numbers 数组，随后是整数变量 min 和 max，两者均初始化为 numbers[0] 的值。

第一个循环包含条件逻辑，如果当前元素小于 `min` 则更新 `min` 的值，如果当前元素大于 `max` 则更新 `max` 的值。第二个循环显示 `numbers` 数组中元素的数值，然后显示 `min` 和 `max` 的值。启动清单 3.12 中的 C 程序的输出如下：

```
Array: 15 3 99 -4 25 8

Max:  99

Min:  -4
```

## 从数组中删除元素

清单 3.13 显示了 `DeleteArrayElement.c` 的内容，展示了如何在 C 程序中使用 for 循环从数字数组中删除一个元素。

### LISTING 3.13: DeleteArrayElement.c

```
#include <stdio.h>

int main()
{
    int pos = 4;
    int numbers[] = {15, 3, 99, -4, 25, 8};
    int count=sizeof(numbers)/sizeof(numbers[0]);

printf("Initial: ");
for(int i=0; i<count; i++)
{
    printf("%d ",numbers[i]);
}
printf("\n");

printf("Removed: %d\n",numbers[pos]);
for(int i=pos; i<count-1; i++)
{
    numbers[i] = numbers[i+1];
}
numbers[count-1] = 0;

printf("Updated: ");
for(int i=0; i<count; i++)
{
    printf("%d ",numbers[i]);
}
printf("\n");

return 0;
}
```

清单 3.13 包含一个 main() 函数，该函数使用 6 个整数初始化 numbers 数组，随后是整数变量 pos，指定将要删除的 numbers 数组的索引位置。

第一个循环显示 numbers 数组的内容，随后第二个循环执行删除操作。该循环本质上将位置 pos 右侧的元素“左移”一个位置。例如，由于 pos[4] 将被删除，我们可以用 pos[5] 替换其值。接下来，用 pos[6] 的值替换 pos[5]。重复此过程，直到到达 numbers 数组中最后一个（最右侧）元素。

最后的循环显示 numbers 数组的更新内容。启动清单 3.13 中的 C 程序的输出如下：

```
Initial: 15 3 99 -4 25 8
Removed: 25
Updated: 15 3 99 25 8 0
```

## 字符串和 for 循环

清单 3.14 显示了 ForLoopStr.c 的内容，展示了如何在 C 程序中使用简单的 for 循环显示文本字符串中的字符。此代码示例包含 C 中指针使用的预览，该内容要到第 5 章才会详细讨论。如有需要，请在阅读完第 5 章的材料后再跳过此代码示例。

### LISTING 3.14: ForLoopStr.c

```
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "hello";
    char *p = str;
    int len = strlen(str);

    printf("First Loop\n");
    printf("---------\n");
    for(int i=0; i<len; i++)
    {
        printf("i : %c\n", str[i]);
    }

    printf("\nSecond Loop\n");
printf("---------\n");
for(int i=0; i<len; i++)
{
    printf("i : %s\n", p);
    ++p;
}

return 0;
}
```

清单 3.14 包含一个 main() 函数，将字符指针 str 初始化为硬编码字符串，然后将字符指针 p 初始化为 str 的地址。第一个循环使用语法 (char)str[i] 显示 str 中的每个字符。

第二个循环也显示 substrings of str，这次使用语法 (char *)p。指针 p 从 str 的地址开始，在 for 循环的每次迭代中，指针 p 的地址通过代码片段 ++p 增加（也可以与之前的代码片段合并）。随着指针 p 在 str 的每个位置推进，输出为更短的子字符串。清单 3.14 的输出如下：

### 第一个循环

```
---------
i : h
i : e
i : l
i : l
i : o
```

### 第二个循环

```
---------
i : hello
i : ello
i : llo
i : lo
```

## 统计一行文本中的单词数

清单 3.15 显示了 CountWords.c 的内容，说明了如何统计一行文本中的单词数（单词由空格或制表符分隔）。

### LISTING 3.15: CountWords.c

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char str1[] = " This is a  String";
    int i=0, wCount=0;

    int len1 = strlen(str1);

    // skip over leading whitespace
    for(i=0; i<len1; i++)
    {
        if((str1[i]!=' ')&&(str1[i]!='\t'))
        {
            break;
        }
    }

    for(; i<len1; i++)
    {
        // found a whitespace => found a word
        if((str1[i]==' ')||(str1[i]=='\t'))
        {
wCount++;
}

// handle the case where there are
// multiple whitespaces between words
}

wCount++;

printf("Line of Text:  %s\n",str1);
printf("Word Count:  %d\n",wCount);

return 0;
}
```

清单 3.15 包含一个 main() 函数，将字符字符串 str1 初始化为硬编码字符串，然后初始化一些标量值。第一个循环跳过任何初始空白字符（可以是简单的空格或制表符）。

第二个循环在 str1 中遇到空白字符时每次递增变量 wCount。其基本假设是空白字符的出现意味着存在新单词。然而，如果单词之间存在多个空白字符，则需要修改此代码以跳过这些“额外”的空白字符，其方式与跳过初始空白字符类似（留作练习）。启动 CountWords 的输出如下：

```
Line of Text:  This is a  String
Word Count:  6
```

## 使用嵌套 for 循环

清单 3.16 显示了 `NestedForLoop.c` 的内容，展示了如何在 C 程序中使用嵌套 for 循环。

### LISTING 3.16: NestedForLoop.c

```
#include <stdio.h>

int main()
{
   int max=5;

   for(int i=0; i<max; i++)
   {
      printf("(i,j): ");
      for(int j=0; j<max; j++)
      {
         printf("%d %d ", i, j);
      }
      printf("\n");
   }

   return 0;
}
```

清单 3.16 包含一个 `main()` 函数，其中嵌套循环遍历 0 到 4 之间的数字，并使用 `printf()` 函数显示当前 (i,j) 位置（其中 i 是外层循环的索引，j 是内层循环的索引）。清单 3.16 的输出如下：

```
(i,j): 0,0 0,1 0,2 0,3 0,4
(i,j): 1,0 1,1 1,2 1,3 1,4
(i,j): 2,0 2,1 2,2 2,3 2,4
(i,j): 3,0 3,1 3,2 3,3 3,4
(i,j): 4,0 4,1 4,2 4,3 4,4
```

下一节将向您展示如何在 C 程序中使用 while 循环。

## 使用 while 循环

清单 3.17 显示了 WhileLoop.c 的内容，展示了如何使用 while 循环在 C 中打印一列整数。

### LISTING 3.17: WhileLoop.c

```
#include <stdio.h>

int main()
{
   int i=0, max=5;
   while(i<=max)
   {
      printf("i : %d\n", i);
      ++i;
   }

   return 0;
}
```

清单 3.17 包含一个 main() 函数，将变量 i 和 max 分别初始化为值 0 和 5。下一段代码是一个 while 循环，只要 i 的值小于或等于 5 就执行。在循环体内部，printf() 函数显示 i 的当前值，之后 i 的值递增。启动清单 3.17 的输出如下：

```
i : 0
i : 1
i : 2
i : 3
i : 4
```

## 从命令行读取整行

Listing 3.18 显示了 `ReadEntireLine.c` 的内容，该内容说明了如何在 C 程序中从标准输入读取整行输入。

### 列表 3.18：ReadEntireLine.c

```c
#include <stdio.h>

#define LINE_SIZE 100

int main()
{
    int charCount=0, inputChar;
    char line[LINE_SIZE];
    char lineFeed = '\n';

    while( (inputChar = getchar()) != lineFeed )
    {
        if(charCount < LINE_SIZE)
        {
            line[charCount] = inputChar;
        }

        charCount++;
    }

    printf("Input length = %d\n", charCount);

    return 0;
}
```

Listing 3.18 与第 2 章中的一个代码示例类似。不同之处在于此代码包含一个 while 循环，该循环会用用户输入“填充”一个字符数组，直到检测到换行符为止，此时 while 循环将停止执行。此外，最多可接受 100 个字符作为输入（`LINE_SIZE` 的值），之后 while 循环将停止向数组中放入元素。Listing 3.18 的下一部分显示了用户键入的字符数。来自 Listing 3.18 的输出示例如下：

```text
this is a line

Input length = 14
```

## switch 语句

本节向您展示如何使用 C switch 语句，以便打印出与随机生成数字相对应的文本字符串（该数字是通过 rand() 函数生成的）。请注意，您需要使用 srand() 为随机数生成器播种，以便使用不同于 1（默认值）的值。每次运行此代码时都会生成不同的值。

请注意，如果您向此程序添加一个循环并在循环内部调用 rand() 函数，即使不为随机数生成器播种，也会生成不同的结果。

Listing 3.19 显示了 Switch.c 的内容，展示了如何在 C 程序中使用 switch 语句。

### 列表 3.19：Switch.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main()
{
// seed the random number generator:
srand(time(NULL));

int rnd = rand() % 6 + 1;

switch(rnd)
{
    case 1: printf("ONE\n");
        break;
    case 2: printf("TWO\n");
        break;
    case 3: printf("THREE\n");
        break;
    case 4: printf("FOUR\n");
        break;
    case 5: printf("FIVE\n");
        break;
    case 6: printf("SIX\n");
        break;
    default: printf("Other value\n");
}

return 0;
}
```

Listing 3.19 包含一个 main() 函数，该函数调用内置的 srand() C 函数来“播种”一个初始随机数，每次在此部分启动代码时该随机数都会不同。

接下来，整数变量 rnd 被初始化为 1 到 6 之间的随机整数（含）。下一部分代码由一个 switch() 语句组成，该语句根据变量 rnd 的值显示一条消息。多次启动 Listing 3.19 中的代码的输出如下：

```text
Switch
FOUR
Switch
ONE
Switch
TWO
```

如果您“注释掉”Listing 3.19 中的 srand() 代码片段，则新的输出将类似于以下内容：

```text
Switch
TWO
Switch
TWO
Switch
TWO
```

或者，您可以将 switch() 语句放在 while 循环内，并使用适当的退出条件，以便生成多个输出值（而不是多次启动代码）。

## 使用数字数组

Listing 3.20 显示了 Factorial2.c 的内容，说明了如何使用迭代解决方案计算正整数的阶乘值。

### 列表 3.20：Factorial2.c

```c
#include <stdio.h>

int main()
{
    int result=1, num=5;

    for(int i=1; i<=num; i++)
    {
        result *= i;
    }

    printf("%d factorial = %d\n", num, result);

    return 0;
}
```

Listing 3.20 定义了变量 result（将包含计算出的阶乘值）和 num（我们想要计算其阶乘值的数字）。Listing 3.20 的下一部分是一个 for 循环，其循环变量 i 在 1 到 num 之间变化，并且该循环的每次迭代都会将 result 的值乘以 i 的值，从而计算出 num 的阶乘值。

来自 Listing 3.20 的输出如下：

```text
5 factorial = 120
```

第 4 章包含用于计算正整数阶乘值的递归解决方案。

## 使用字符串数组

Listing 3.21 显示了 ArrayOfStrings.c 的内容，展示了如何在 C 程序中定义和填充字符串数组。

### 列表 3.21：ArrayOfStrings.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
char names[3][20];

strcpy(names[0], "Jane Smith");
strcpy(names[1], "John Edwards");
strcpy(names[2], "Steve Anderson");

    for(int i=0; i<3; i++)
    {
        printf("Name: %s\n", names[i]);
    }

    return 0;
}
```

Listing 3.21 包含一个 `main()` 函数，该函数初始化 3x20 字符数组 `names`，随后是三个 `strcpy()` 调用，用于填充 names 数组的三个行。

代码的下一部分是一个循环，用于显示 `names` 数组每一行的内容。启动 Listing 3.21 的输出如下：

```text
Name: Jane Smith
Name: John Edwards
Name: Steve Anderson
```

## 使用 while 循环查找数字的除数

Listing 3.22 包含一个 `while` 循环、条件逻辑和 `%`（模）运算符，以便找到大于 1 的任意整数的因子。

### 列表 3.22：Divisors.c

```c
#include <stdio.h>

int main()
{
    int div=2, num=12;

    printf("Number: %d\n", num);

    while(num > 1)
    {
      if(num % div == 0)
      {
        printf("divisor: %d\n", div);
        num /= div;
      }
      else
      {
        ++div;
      }
    }

    return 0;
    }
```

Listing 3.22 定义了一个整数 `num`，其值为 12，并将变量 `div` 初始化为值 2。`while` 循环用 `div` 除 `num`，如果余数为 0，则打印 `div` 的值，然后用 `div` 除 `num`；如果值不为 0，则 `div` 增加 1。只要 `num` 大于 1，此 `while` 循环就会继续。

查找 12 的除数的 Listing 3.22 的输出如下：

```text
Number: 12
divisor: 2
divisor: 2
divisor: 3
```

为什么代码 Listing 3.22 只找到质数除数而不是合数除数？由于 `if` 语句，代码工作正确。例如，6 永远不会被打印为 12 的除数，因为代码最初确定 2 是 12 的质数除数，然后 `if` 代码块将原始数字从 12 减少到 6。接下来，代码确定 2 是 6 的质数除数，然后 if 代码块将 6 替换为 3。最后，3 是 3 的质数除数，之后 3 被替换为 1，此时 while 循环终止。

## 使用 while 循环查找质数

Listing 3.23 包含一个 while 循环、条件逻辑和 %（模）运算符，以便计算大于 1 的任意整数的质因数个数。如果一个数字只有一个除数，则该数字为质数。

### 列表 3.23：Divisors3.c

```c
#include <stdio.h>

int main()
{
    int count=1, div=2, num=12;

    while(div < num)
    {
        if(num % div == 0)
        {
            ++count;
        }

        ++div;
    }

    if(count == 1)
    {
        printf("%d is prime\n", num);
    }
    else
    {
        printf("%d is composite\n", num);
    }

    return 0;
}
```

**Listing 3.23** 使用值 1、2 和 12 分别初始化变量 `count`、`div`、`num`。下一部分代码是一个 `while` 循环，只要 `div` 的值小于 `num` 的值，该循环就会迭代。

在 `while` 循环内部，如果 `div` 是 `num` 的除数（即 `num % div == 0`），则 `count` 的值会递增，之后 `div` 会无条件递增。

`while` 循环退出后，`printf()` 语句会显示一条消息，说明 `num` 是质数还是合数，这取决于 `count` 的值是否为 1。启动 **Listing 3.23** 的输出如下：

```text
12 is composite
```

## 摘要

本章向您介绍了 `for` 循环、单维和多维数组，以及如何在数组中执行线性搜索。接下来您学习了如何在数字数组中找到最大值和最小值，如何插入元素，以及如何从数组中删除元素。

您还看到了如何使用 `while` 循环、`do-while` 循环以及涉及 `while` 循环的字符串相关示例。此外，您还学习了 C 程序中的条件逻辑，例如 `if` 语句和 `if-else` 语句。然后您学习了如何找到一个数字的除数，以及如何检查一个数字是否为质数。



## 第四章

### C 中的函数

本章向您介绍一些内置的 C 函数，并展示如何在 C 程序中创建自定义函数。您还将学习递归以及如何定义自定义函数，以便使用 C 中的递归解决各种众所周知的任务。

本章的第一部分简要讨论了 C 中可用的各种类型的内置函数。您在前几章中已经见过一些内置函数（例如 isalpha() 和 ispunct()），本节包含其他有用的内置函数。本章的第二部分包含代码示例，说明如何创建包含自定义函数的 C 程序，这些自定义函数使用 C 中的一些内置函数。

本章的第三部分向您展示如何使用递归来计算阶乘值、斐波那契数以及一对整数的最大公约数 GCD（最大公约数），使用欧几里得算法（依赖于递归）。尽管递归通常被认为是一种高级编程语言主题，但递归可以用简单而优雅的方式解决许多问题。

本章的最后一部分向您展示了对数字数组进行排序以及在数字数组中搜索数字的技术。

## 使用 C 中的内置函数

C 中的内置函数可以返回任何受支持的 C 类型，例如字符、字符串、指针、函数指针等。本书中的所有 C 程序都包含一个 `main()` 函数，该函数始终返回 `int` 类型。这个返回值的意义是什么？您需要信息（即某种形式的文档，即使只是一个注释块）来描述给定返回类型的不同值的用途。

然而，一些 C 函数不返回任何值，在这种情况下它们的返回类型为 `void`。请注意，一些语言（如 Fortran）在返回值的函数（称为函数）和不返回任何内容的函数（称为子程序）之间有所区分，但 C 不做这种区分。

另一个场景涉及“按引用调用”与“按值调用”，您有时会在返回类型为 `void` 的函数中看到这一点。思路很简单：前者涉及将参数的内存位置（即引用）传递给函数，而后者涉及将参数的完整副本传递给函数。这两种选项都在下一节中。

### 按引用传递与按值传递

一个通过传递“可更新”参数来调用另一个函数的 C 函数被称为“按引用传递”。这意味着在“被调用”函数中对此类参数的任何更改都会反映在“调用”函数中。如果一个函数包含指向内存位置的指针参数，则在“被调用函数”中对该参数的更新在“被调用函数”中可用。例如，传递大内存块的地址比 1) 将该内存块的内容传递给函数，或 2) 要求“被调用函数”返回一个大的修改后内存块更有效。

另一方面，将在“被调用函数”中无法修改的参数传递称为“按值传递”。无论在“被调用函数”中执行什么计算，传递给该函数的参数在“调用函数”中仍保留其原始值。

通常，对于原始数据类型或相当小的内存块，使用按值传递。如果您决定对参数使用按值传递，则涉及指针（在第 5 章和第 6 章中讨论）；因此，在这样做时请格外小心以避免错误。如前一节所述，如果“被调用函数”对大块内存进行各种更新，则按引用传递是有意义的，因为它比按值传递更有效。

除第 7 章中的一些代码示例外，其他章节中的代码示例涉及按值传递函数。与此同时，以下小节按类型列出了内置函数的列表。

### 内置字符函数

C 支持各种方便的内置函数来对字符执行各种测试，例如确定字符是否为字母数字、字母、控制字符、数字或小写或大写字母。以下是其中许多函数的列表（所有函数的返回类型均为 int），以及简要描述（许多函数名称直观）：

- int isalnum(int c): 测试 c 是否为字母数字
- int isalpha(int c): 测试 c 是否为字母
- int iscntrl(int c): 测试 c 是否为控制字符
- int isdigit(int c): 测试 c 是否为数字
- int islower(int c): 测试 c 是否为小写字符
- int isupper(int c): 测试 c 是否为大写字符
- int isgraph(int c): 如果 c 是 isalnum 或 ispunct 任一返回非零的任何字符，则返回非零。
- int isprint(int c): 如果 c 是空格或 isgraph 返回非零的字符，则返回非零。
- int ispunct(int c): 如果 c 是标点符号则返回非零
- int isspace(int c): 如果 c 是空格字符则返回非零
- int isxdigit(int c): 如果 c 是十六进制数字则返回非零
- int tolower(int c): 如果存在且 isupper(c) 为真，则返回对应的小写字母；否则返回 c。
- int toupper(int c): 如果存在且 islower(c) 为真，则返回对应的大写字母；否则返回 c。

由于前述函数相当简单，您也可以轻松在线找到代码示例，因此我们将跳过本节的代码示例，直接进入下一节，该节提供了 C 中面向字符串的内置函数列表。

### 在数据类型之间转换

在某些情况下，可以在 C 中从一种数据类型转换为另一种数据类型。标准头文件 stdlib.h（头文件在第 7 章中讨论）提供了 C 中的所有字符串转换函数。

例如，函数 atof()、atoi() 和 atol() 分别将 ASCII 值转换为 float、整数和 long 值。

这结束了本章关于面向字符串的内置 C 函数的部分。下一节提供了用户定义 C 函数的简单介绍。

## 定义一个简单的自定义函数

C 函数具有以下格式：每个函数定义都有一个返回类型（可以是 void）、一个名称、零个或多个参数以及一个函数体。上述语句可以通过以下代码片段表达：

```
return-type function-name(argument declarations)
{
    declarations and statements
}
```

如果函数不返回任何内容，则其返回类型为 void。返回内容的函数在函数中（不一定在函数末尾）具有以下类型的语句：

```
return (return-value)
```

### 函数原型

函数原型指定函数的参数（及其类型）和返回类型。尽管旧版本的 C 不要求函数原型，但包含它们是个好主意，因为它们允许编译器检查传递参数的数据类型是否与声明参数的数据类型兼容。

函数原型的示例如下：

```
void findChar(char str[], char c);
```

函数原型可以放在所谓的头文件中（按惯例具有 .h 后缀）。然后将“头”文件（通过 #include 指令）包含在需要函数原型的 C 程序中。这种技术改进了代码模块化和代码重用，从而使您能够为项目创建库。

作为创建头文件并将其包含在 C 程序中的简单示例，假设文件 FindMain2.h 包含以下代码：

```
#include <ctype.h>
#include <stdio.h>

void findChar(char str[], char c);
```

您可以在文件 FindMain2.c 中按如下方式引用 FindMain2.h：

```c
#include "FindChar2.h"
```

这种将包含函数原型的文件与实现代码分开的做法，类似于 Java 中的接口文件与实现文件。虽然你可能要到过了初学者阶段之后才会用到它，但了解一下这个功能是很好的。

## C 语言函数中的函数参数

函数参数属于形式参数，在函数内部被视为局部变量。此外，这些参数优先于全局变量。

清单 4.1 显示了 `FunctionParams.c` 的内容，该文件演示了 C 程序中局部变量和全局变量的使用。

### 清单 4.1：FunctionParams.c

```c
#include <stdio.h>

// global variable declaration
int a = 20;

// function to add two integers
int sum(int a, int b)
{
    printf ("value of a in sum() = %d\n",  a);
    printf ("value of b in sum() = %d\n",  b);

    return a + b;
}

int main()
{
    // local variable declaration in main function
    int a = 10;
    int b = 20;
    int c = 0;

    printf ("value of a in main() = %d\n", a);
    c = sum(a, b);
    printf ("value of c in main() = %d\n", c);

    return 0;
}
```

清单 4.1 首先将全局变量 a 初始化为值 20，然后定义了接受两个参数的函数 sum()。该函数显示参数的值，然后返回它们的和。

接下来，main() 函数将三个局部变量 a、b 和 c 分别初始化为 10、20 和 0。显示变量 a 的值，然后调用 sum()，并将返回值赋给变量 c。跟踪执行逻辑的最佳方法是运行代码并注意显示的值（你是否预测到了相同的结果？）。

运行清单 4.1 中的代码，你将看到以下输出：

```text
value of a in main() = 10
value of a in sum() = 10
value of b in sum() = 20
value of c in main() = 30
```

请注意，在上述输出中并未出现 a 的全局值（你知道为什么吗？）。

## C 语言用户自定义函数的 C99 语法

第 1 章简要提到了 C99 版本的 C 编程语言。本节包含一个代码示例，演示 C99 对用户自定义函数的要求之一。如果在函数定义之前引用该函数，则需要在函数调用位置之前指定“函数原型”。按照惯例，这些声明出现在 C 程序的开头附近，通常在所有函数定义之前。

清单 4.2 显示了 SimpleC99.c 的内容，它演示了如何为自定义函数 message() 指定函数原型（以粗体显示）。

### 清单 4.2：SimpleC99.c

```c
#include <stdio.h>

// prevent "Implicit declaration of function is invalid
// in C99"
void message();

int main()
{
    message();

    return 0;
}

void message()
{
    printf("Hello from message\n");
}
```

清单 4.2 包含函数 message() 的原型，其返回类型为 void，并在代码后面定义。接下来，main() 函数调用 message() 函数，该函数仅显示文本字符串 Hello from message。

编译并运行清单 4.2 中的代码，你将看到预期的输出：

```text
Hello from message
```

另一点要记住：如果将 message() 函数（以及任何其他自定义函数）的定义放在 main() 函数定义之前，则无需包含函数原型。

## K&R 风格的函数定义

清单 4.3 显示了 OldStyleFunction.c 的内容，它演示了如何使用 K&R 风格定义函数。

### 清单 4.3：OldStyleFunction.c

```c
#include <stdio.h>

float perimeter(width, height)
int width;
float height;
{
    return 2 * (width + height);
}

int main()
{
    float perim = perimeter(10.0, 5);
    printf("Perimeter = %f\n", perim);

    return (0);
}
```

清单 4.3 首先定义了 perimeter() 函数，该函数返回宽度 x 高度的矩形周长。注意 width 和 height 参数是如何声明的（以粗体显示）。

接下来，main() 函数调用 perimeter() 函数，并将返回值赋给浮点变量 perim。

运行清单 4.3 的输出如下：

```text
Perimeter = 50.000000
```

K&R 风格的 C 语言允许函数原型；但是，只能声明返回类型，参数列表必须为 ()，如下所示：

```c
extern float atof();
```

上述代码片段中的 () 表示该函数接受数量未知、类型未知的参数。

## 将字符串转换为整数和浮点值

清单 4.4 显示了 ConvertDataTypes.c 的内容，它演示了如何使用 atof()、atoi() 和 atol() 函数将字符串转换为数值。

### 清单 4.4：ConvertDataTypes.c

```c
#include <stdlib.h>
#include <stdio.h>

int main()
{
    int i;
    long l;
    double x;
    char *s;

    s = "-2309.12E-15";
    x = atof(s); /* x = -2309.12E-15 */

    printf("x = %.4e\n", x);

    s = "-9885";
    i = atoi(s);   /* i = -9885 */

    printf("i = %d\n", i);

    s = "98854 dollars";
    l = atol(s);   /* l = 98854 */

    printf("l = %ld\n", l);

    return (0);
}
```

清单 4.4 首先定义了变量 i、l、x 和 s，其类型分别为 int、long、double 和 char 指针。然后初始化变量 s，调用内置的 atof() C 函数，参数为 s，结果赋给变量 x，然后显示 x 的值。使用 s 的另一个值重复这一系列步骤，这次 atoi() 函数的输出被赋给变量 i（并显示其值）。第三次使用 s 的第三个值重复该序列，调用 atol() 函数的结果被赋给变量 l（并显示其值）。执行清单 4.4 中的代码的输出如下：

```text
x = -2.3091e-12
i = -9885
l = 98854
```

以下链接包含可用于将整数转换为其他进制的代码：

www.strudel.org.uk/itoa/#newest

## 使用 SPRINTF() 将字符串打印到缓冲区

`sprintf()` 函数允许你将数字和字符写入缓冲区，支持与 `printf()` 函数相同的格式。此外，每次调用 `sprintf()` 函数都会返回写入数组的字节数（不包括最后的空字符），这使你能够跟踪写入缓冲区的字符数。

清单 4.5 显示了 `PrintToBuffer.c` 的内容，它演示了如何使用 `sprintf()` 来格式化并打印各种数据。

### 清单 4.5：PrintToBuffer.c

```c
#include <stdio.h>

char buffer[200];
int i, j;
double fp;
char *s = "baltimore";
char c;

int main()
{
    c = 'I';
    i = 35;
    fp = 1.7320508;

    // Format and print various data
    j = sprintf(buffer, "%s\n", s);
    j += sprintf(buffer+j, "%c\n", c);
    j += sprintf(buffer+j, "%d\n", i);
    j += sprintf(buffer+j, "%f\n", fp);

    printf("string:\n%s\ncharacter count = %d\n", buffer, j);

    return (0);
}
```

清单 4.5 定义了多个不同类型的变量，随后调用内置的 sprintf() C 函数将字符串 s 的内容复制到缓冲区。对变量 c、i 和 fp 重复此过程。最后的代码片段显示缓冲区的内容和 j 的值。执行清单 4.5 中的代码的输出如下：

```text
string:
baltimore
I
35
1.732051

character count = 24
```

## 缓冲区操作函数

本章前面介绍了一些内置的 C 函数，本节将介绍更多的 C 函数。格式为简洁的一句话描述，后跟内置的 C 函数（包括参数和返回值）。

例如，你可以使用以下方式将 n 个字符从 ct 复制到 s 并返回 s（如果对象重叠，s 可能会被破坏）：


以下函数：

```c
void* memcpy(void* s, const void* ct, int n);
```

比较 cs 和 ct 的前 n 个字符：如果 cs < ct 则返回负值；如果它们相等则返回零；如果 cs > ct 则返回正值：

```c
int memcmp(const void* cs, const void* ct, int n);
```

返回指向 cs 的前 n 个字符中 c 首次出现位置的指针，如果未找到则返回 NULL：

```c
void* memchr(const void* cs, int c, int n);
```

将 s 的前 n 个字符中的每一个都替换为 c，并返回 s：

```c
void* memset(void* s, int c, int n);
```

从 ct 复制 n 个字符到 s，并返回 s（如果对象重叠，s 不会被破坏）：

```c
void* memmove(void* s, const void* ct, int n);
```

你未必需要使用所有这些内置 C 函数，并且你可能会经常使用其中的一个子集（这取决于你需要编写的 C 程序类型）。

## 将一维数组作为参数传递

清单 4.7 显示了 SingleArrayFunction.c 的内容，它说明了如何在 C 程序中将一维数组传递给函数。请注意，自定义函数 addAll() 被放在 main() 函数定义之前，这意味着为符合 C99 规范，不需要函数原型。

***清单 4.7：SingleArrayFunction.c***

```c
#include <stdio.h>

int addAll(int arr[], int size)
{
    int sum=0;

    for(int i=0; i<size; i++)
    {
        sum += arr[i];
    }

    return sum;
}

int main()
{
    // int array with 8 elements
    int arr1[8] = {1,2,3,4,5,6,7,8};
    int sum=0;

    printf("Values: ");
    for(int i=0; i<8; i++)
    {
        printf("%d ",arr1[i]);
    }
    printf("\n");

    sum = addAll(arr1,8);

    // output the returned value
    printf("Sum = %d\n", sum);

    return 0;
}
```

清单 4.7 定义了函数 addAll()，它接受一个整数数组和一个整数作为参数，并返回一个整数，即数组中元素之和。接着，`main()` 函数包含一个循环，用于显示数组 `arr1` 的元素，随后调用 `addAll()` 函数，其返回值被赋给变量 `sum`。`main()` 方法的最后一部分只是打印 `sum` 的值。清单 4.7 的输出如下：

```
Values: 1 2 3 4 5 6 7 8
Sum = 36
```

## 在字符串中查找字符

清单 4.8 显示了 `FindChar1.c` 的内容，它向你展示如何在 C 程序中查找给定字符串中某个字符的出现次数。

***清单 4.8：FindChar1.c***

```c
#include <ctype.h>
#include <stdio.h>

void findChar(char str[], char c)
{
  int matchCount = 0;

  printf("String: %s\n",str);
  printf("Char:  %c\n",c);

  for(int i=0; str[i]; i++)
  {
    if(str[i] == c)
    {
      printf("Match in position: %d\n",i);
      ++matchCount;
    }
  }

  printf("Count: %d\n\n",matchCount);
}

int main()
{
    char str1[] = "pasta";
    findChar(str1, 'a');

    char str2[] = "New York City";
    findChar(str2, 'k');

    char str3[] = "California";
    findChar(str3, 'z');

    return (0);
}
```

清单 4.8 定义了函数 findChar()，它接受一个字符串和一个字符作为参数，返回类型为 void。该函数遍历字符串并统计字符 c 的出现次数。每当找到匹配项时，就显示一条消息，随后显示一条包含该字符串中 c 出现次数的消息。

main() 函数定义了三个字符串 str1、str2 和 str3，并分别用这些字符串以及字符 a、k 和 z 调用 findChar() 方法。清单 4.8 的输出如下：

```
String: pasta
Char:  a
Match in position: 1
Match in position: 4
Count: 2

String: New York City
Char:  k
Match in position: 7
Count: 1

String: California
Char:  z
Count: 0
```

## 将字符串转换为十进制值

本节包含一个 C 内置函数的示例，这些函数使你能够测试字符串中的字符，以确定它们是否为数字。

***清单 4.9：DisplayDigits.c***

```c
#include <ctype.h>
#include <stdio.h>

void checkDigits(char str[])
{
    printf("Number: %s\n",str);

    for(int i=0; str[i]; i++)
    {
        if(isdigit(str[i]))
        {
            printf("Digit: %c\n",str[i]);
        }
        else
        {
            printf("Not Digit: %c\n",str[i]);
        }
    }

    printf("\n");
}

int main()
{
    char str1[] = "123.456";
    checkDigits(str1);
    char str2[] = "-51.203";
    checkDigits(str2);

    return (0);
}
```

清单 4.9 定义了函数 `checkDigits()`，它接受一个字符串，返回类型为 `void`。该函数遍历字符串，并使用内置 C 函数 `isdigit()` 配合条件逻辑来确定每个字符是否为数字，并打印相应的消息。

`main()` 函数定义了两个字符串 `str1` 和 `str2`，并分别用这些字符串调用 `checkDigits()` 函数。清单 4.9 的输出如下：

```
Number: 123.456
Digit: 1
Digit: 2
Digit: 3
Not Digit: .
Digit: 4
Digit: 5
Digit: 6

Number: -51.203
Not Digit: -
Digit: 5
Digit: 1
Not Digit: .
Digit: 2
Digit: 0
Digit: 3
```

## 显示质数列表

`Listing 4.10` 显示了 `DisplayPrimes.c` 的内容，它向你展示如何定义并调用自定义函数 `isPrime()`，该函数从 `main()` 函数内部的 `for` 循环中调用，以显示质数列表。尽管你可以将函数 `isPrime()` 的代码放在 `main()` 函数中的循环内，但使用函数可以使代码模块化。

***清单 4.10：DisplayPrimes.c***

```c
#include <stdio.h>

int isPrime(int idx)
{
    int flag=0, div=2;
    while (div <= idx/2)
    {
        if (idx % div == 0) // composite
        {
            flag = 1;
            break;
        }
        div++;
    }

    return flag;
}


int main()
{
    int maxVal=50, idx=0, result=0;

    for (idx=1; idx<=maxVal; idx++)
    {
        result = isPrime(idx);

        if ( result == 0) // prime
        {
            printf("%d ", idx);
        }
    }

    return 0;
}
```

清单 4.10 包含函数 isPrime()，如果数字是质数则返回 0，如果数字是合数则返回 1。isPrime() 函数包含一个 while 循环，从 2 开始，到 idx/2 结束，并检查这些数字中是否有任何一个是数字 idx 的除数。如果是，则将 flag 变量（初始化为值 0）设置为 1，并退出循环；否则循环正常终止。无论哪种情况，isPrime() 函数都会返回 flag 的值。

接下来，main() 函数的主体包含一个 for 循环，其循环变量 idx 从 1 迭代到 maxVal（初始化为 50）。for 循环的每次迭代都会用 idx 的当前值调用 isPrime() 函数。for 循环的下一部分仅当 idx 是质数（即 isPrime() 返回 0）时才打印 idx 的值。

清单 4.10 的输出如下：

```
1 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
```

至此，关于 C 程序中自定义函数的讨论结束。本章下一部分将向你介绍递归，并提供一些代码示例，说明如何在 C 中使用递归。

## 什么是递归？

递归是一种强大的技术，可以为各种问题提供优雅的解决方案，例如阶乘值、斐波那契数，以及通过欧几里得算法求两个正整数的最大公约数。

一个有趣（也许反直觉）的事实是：基于递归的算法的表达能力与迭代算法相同（即两种算法都不比另一种更“强大”）。然而，在使用算法解决各种任务时，存在某种不对称性。例如，通过递归计算斐波那契数的任务很直接，而迭代解决方案则远非显而易见。一个更有趣的任务称为汉诺塔，它可以通过递归算法以非常优雅的方式解决。如果你有足够的动力，可以尝试通过迭代算法实现该解决方案（祝你好运！）。

还有一个可以优雅解决的任务涉及阿克曼函数的递归定义，它具有“二维”递归，这使得它比你在常见基于递归的任务中看到的典型“一维”递归更复杂（也更有趣？）。阿克曼函数超出了本书的范围，但有关阿克曼函数的详细信息可以通过互联网搜索获得。

然而，我们不要否定迭代解决方案对基于递归任务的适用性。例如，非负整数的阶乘值的定义是递归的，但其迭代解决方案非常直接，并且以其简单性而优雅（如果我们忽略存储需求）。要点很简单：使用最适合你的算法


需求，同时牢记性能成本、代码维护和功能增强。

考虑到上述几点，让我们看一些使用递归计算一些著名数字的示例，这些示例将在下面的小节中详细讨论。

## 计算阶乘值

正整数 n 的阶乘值是 1 到 n 之间所有整数的乘积。阶乘的符号是感叹号（“!”），这里有一些示例阶乘值：

- 1! = 1
- 2! = 2
- 3! = 6
- 4! = 24
- 5! = 120

一个数的阶乘值的公式可以简洁地定义如下：

对于 n > 1，Factorial(n) = n*Factorial(n-1)，且 Factorial(1) = 1

第 3 章展示了如何使用 for 循环计算正整数的阶乘值。清单 4.11 显示了 Factorial.c 的内容，说明了如何使用递归来计算正整数的阶乘值。

### 清单 4.11：Factorial.c

```c
#include <stdio.h>

int factorial(int num)
{
    if(num > 1)
    {
        return num*factorial(num-1);
    }
    else
    {
        return 1;
    }
}

int main()
{
    int result=0, num=5;
    result = factorial(num);

    printf("%d factorial = %d\n", num, result);

    return (0);
}
```

清单 4.11 包含函数 factorial，它实现了本节开头所述的一个数的阶乘值的递归定义。函数 factorial() 通过连续调用自身来递归地“逐层深入”，直到其参数值为 1，此时返回数字 1。每次“逐层深入”还会将递归函数调用与逐渐变小的整数相乘，从而“累积”1 到 num 之间数字的乘积。

清单 4.11 的输出如下：

```text
5 factorial = 120
```

## 通过递归计算斐波那契数

斐波那契数集合代表了自然界中一些有趣的模式（例如向日葵的模式），其递归定义如下：

Fib(0) = 0

Fib(1) = 1

对于 n >= 2，Fib(n) = Fib(n-1) + Fib(n-2)

清单 4.12 显示了 Fib.c 的内容，说明了如何计算斐波那契数。

### 清单 4.12：Fib.c

```c
#include <stdio.h>

int fib(int num)
{
    if((num == 0)|| (num == 1))
    {
        return 1;
    }
    else
    {
        return fib(num-1)+fib(num-2);
    }
}

int main()
{
    int result=0, num=10;
    result = fib(num);

    printf("%d fibonacci = %d\n", num, result);

    return (0);
}
```

清单 4.12 定义了带参数 num 的 fib() 函数。如果 num 等于 0 或 1，则 fib 返回 num 的值；否则，fib 返回 fib(num-1) 与 fib(num-2) 相加的结果。如你所见，用户定义的 fib() 函数正是斐波那契数定义的实现。清单 4.12 的输出如下：

```text
10 fibonacci = 89
```

## 通过递归计算数字的幂

清单 4.13 显示了 `ComputePower.c` 的内容，它使用递归来计算一个数的给定次幂。

### 清单 4.13：ComputePower.c

```c
#include <stdio.h>

long computePower(int b,int e, int r)
{
    if( e == 0 ) return r;
    return computePower(b, e-1, r*b);
}

int main()
{
    int base = 4, exp = 5;
    long int result;

    result = computePower(base, exp, 1);
    printf("%d to the power of %d = %ld\n",base, exp,
           result);

    return 0;
}
```

清单 4.13 定义了函数 `computePower()`，其参数为 `b`、`e` 和 `r`，分别对应底数、指数和结果。该函数使用“尾递归”：递归计算的中间结果作为第三个参数传递。每次调用自定义函数 `computePower()` 时，第三个参数都会更新为新的中间乘积，并且指数 `e` 的值会递减。终止条件在 `e` 的值为 `0` 时发生，此时返回第三个参数 `r` 的值。

清单 4.13 的输出如下：

```text
4 to the power of 5 = 1024
```

## 通过递归计算一个数的位数

清单 4.14 显示了 `CountDigits.c` 的内容，它使用递归来计算一个数的位数。

### 清单 4.14：CountDigits.c

```c
#include <stdio.h>

int countDigits(int num, int result)
{
   if(num == 0) return result;
   return countDigits(num/10, result+1);
}

int main()
{
   int number = 123, result = 0;

   result = countDigits(number, 0);
   printf("Number of digits in %d = %d\n", number, result);
   return 0;
}
```

清单 4.14 定义了自定义函数 `countDigits()`，它也使用*尾递归*来计算一个整数的位数。注意，`countDigits()` 是通过将当前数连续除以 10，同时递增第二个参数的值来调用的。终止条件在第一个参数为 0 时发生，此时第二个参数 `result` 等于原数的位数。清单 4.14 的输出如下：

```text
Number of digits in 123 = 3
```

## 通过递归计算一个数的各位数字之和

清单 4.15 显示了 AddDigits.c 的内容，它使用递归来计算一个数的各位数字之和。

### 清单 4.15：AddDigits.c

```c
#include <stdio.h>

int computeSum(int num, int result)
{
    if (num == 0) return result;
    return computeSum(num/10, result + num % 10);
}

int main()
{
    int number = 123, result = 0;

    result = computeSum(number, 0);
    printf("Sum of digits in %d = %d\n", number, result);

    return 0;
}
```

清单 4.15 定义了函数 computeSum()，它使用尾递归来计算两个数之和。注意，countDigits() 是通过将第一个参数 num 连续除以 10，同时将余数 num % 10 加到第二个参数上来调用的。终止条件在第一个参数为 0 时发生，此时第二个参数 result 等于两个原始数之和。清单 4.15 的输出如下：

```text
Sum of digits in 123 = 6
```

## 通过递归计算两个数的最大公约数

两个正整数的 GCD（最大公约数）是能整除这两个整数且余数为 0 的最大整数。这里显示一些值：

```text
gcd(6,2)  = 2
gcd(10,4) = 2
gcd(24,16) = 8
```

清单 4.16 使用递归和欧几里得算法来求两个正整数的 GCD。请记住，尽管欧几里得算法有一个更“紧凑”的版本，但清单 4.16 中的代码可能更容易理解。

### 清单 4.16：GCD.c

```c
#include <stdio.h>

int gcd(int num1, int num2)
{
  if(num1 % num2 == 0)
  {
    return num2;
  }
  else if(num1 < num2)
  {
    printf("switching %d and %d\n", num1, num2);
    return gcd(num2, num1);
  }
  else
  {
    printf("reducing %d and %d\n", num1, num2);
    return gcd(num1-num2, num2);
  }
}

int main()
{
  int result=0, num1=24, num2=10;
  result = gcd(num1, num2);

  printf("GCD of %d and %d = %d\n", num1, num2, result);

  return (0);
}
```

清单 4.16 定义了函数 `gcd`，其参数为 `num1` 和 `num2`。如果 `num1` 能被 `num2` 整除，函数返回 `num2`。如果 `num1` 小于 `num2`，则通过交换 `num1` 和 `num2` 的顺序来调用 `gcd`。在所有其他情况下，`gcd` 返回用值 `num1-num2` 和 `num2` 计算 `gcd` 的结果。

清单 4.16 的输出如下：

```text
reducing 24 and 10
reducing 14 and 10
switching 4 and 10
reducing 10 and  4
reducing  6 and  4
switching 2 and  4
GCD of  24 and 10 = 2
```

## 通过递归计算两个数的最小公倍数

两个正整数的 LCM（最小公倍数）是这两个整数的倍数中的最小整数。这里显示一些值：

```text
lcm(6,2)   = 6
lcm(10,4)  = 20
lcm(24,16) = 48
```

一般来说，如果 x 和 y 是两个正整数，可以按如下方式计算它们的 LCM：

```text
lcm(x,y) = x/gcd(x,y)*y
```

清单 4.17 使用上一节中定义的 `gcd()` 函数来计算两个正整数的最小公倍数。

### 清单 4.17：LCM.c

```c
#include <stdio.h>

int gcd(int num1, int num2)
{
    if(num1 % num2 == 0)
    {
        return num2;
    }
    else if(num1 < num2)
    {
        //printf("switching %d and %d\n", num1, num2);
        return gcd(num2, num1);
    }
}
```



指定函数原型，以及一些常用的头文件。

你还学习了如何将数组作为参数传递给函数以及如何计算方阵的转置。此外，你还看到了如何在字符串中查找字符，如何按引用与按值传递。然后你学习了递归，以及如何计算阶乘值、斐波那契数、两个数的最大公约数以及两个数的最小公倍数。你还学习了如何计算整数的位数以及如何使用一种称为尾递归的技术计算两个数的和。

大小写字母，如何从字符串中删除空白字符，以及如何统计一行文本中的单词数。本章的最后一节包含 C 程序，说明如何定义指向函数的指针、函数指针作为参数，以及如何定义指向指针的指针。

现在让我们从指针和指针声明的简要介绍开始，以及变量的地址、解引用指针和使用指针算术。正如你将看到的，基于指针的算术模拟了数组索引，而将数组视为索引数据结构或使用指针算术的缓冲区这两种观点对于理解和发展 C 指针的工作原理至关重要。

## 什么是指针？

用“指针”数据类型声明的变量包含一个内存地址，指示实际数据的位置。使用指针数据类型时，通常说指针变量“指向”实际数据，而不是谈论内存地址。以下是指针“指向”的数据的一些示例：

- 一个变量（例如 `int x = 5;`）
- 一个字符串的起始地址（例如 `char *ptr = "Hello";`）
- 通过内置的 C `malloc()` 函数分配（在第 6 章中讨论）

指针数据类型的变量是通过在声明中将星号（“*”）立即放在变量名称之前来声明的。此变量可用于指向任何适当类型的值，或可将其设置为 `NULL` 以表示它当前不指向任何值。指针可以为几乎任何类型的数据声明，例如 `int`、`long`、用户定义的 `struct`（在第 6 章中讨论），甚至是函数。还有一种特定的指针类型，其语法为 `void *`，用于指向类型未知的数据。

“指向指针的指针”是用两个星号（`**`）定义的，并包含一个内存地址，指示另一个指针的位置。指向指针的指针数据类型的最常见用途之一是模拟可调整大小的二维数组。

使用指针时最重要的是要注意，指针在使用之前必须始终指向适当类型的数据。尝试通过无效指针访问值是导致失败的常见原因，必须避免。

还有一个需要注意的细节。当你为指针赋值时，等号右边的内容可以是一个硬编码的字符字符串，例如 `"Hello"`（在之前的示例列表中显示）。为什么这不会违反前一段中指定的规则？带引号的字符串（称为“字符串字面量”）的数据类型为“指向 `char` 的指针”。由于 C 没有内置的字符串数据类型，字符串字面量被视为指向其第一个字符的指针。

如果你对前几段的含义感到不确定，以下小节包含的代码示例将使一切变得清晰。

### 指针的简单示例

本节包含强化上一节信息的示例，并通过扩展解释来强化在 C 中正确定义指针的方法。

正如你在上一节中看到的，在 C 中指针是通过在声明语句中将星号（`*`）放在变量名称前面来声明的，如下所示：

```c
int *p;
```

`*` 运算符解引用一个变量：这意味着每当你有一个指向内存位置的指针时，使用 `*` 运算符即可获取指针变量所引用的内容。

请注意，`*` 字符有多种含义。当它出现在声明中时，它作为数据类型的一部分来声明指针。当它出现在指针左侧的表达式中时，它是解引用运算符，用于访问指针当前指向的数据。当它出现在两个数值之间的表达式中时，它充当乘法运算符。

如果你想访问非指针变量的值怎么办？你可以使用 `&` 运算符获取非指针变量的内存位置，然后可以访问该变量的值。例如，考虑以下代码片段：

```c
int x = 7;
int *p = &x;
```

正如你所见，前一段代码片段中的变量 x 的类型为 int 且值为 7，而变量 p 是指向为变量 x 分配的内存地址的指针。

请注意以下事项：指针 `p` 已在变量 `x` 被声明 *并且已初始化* 为值 7 之后，用变量 `x` 的地址进行了初始化。

实现相同结果的另一种方式如下所示：

```c
int *p;
int x = 7;
p = &x;
```

在前面的代码片段中，`p` 被声明为未初始化的整数指针，然后 `x` 被初始化为值为 7 的整数，之后将 `p` 的值设置为 `x` 的地址（用 `&x` 表示）。

请记住，只有在数据类型匹配时才能进行赋值。例如，赋值 `int x = 7` 是有效的，因为左右两侧的数据类型都是 `int`。

另一个例子，使用 `int *p = &x` 声明并赋值指针是有效的，因为左右两侧的数据类型都是 `int *`。

作为第三个例子，声明 `int *p = 1234` 是无效的，因为左侧的类型是“指向 int 的指针”，右侧的类型是“int”。即使类型匹配，你也 *必须确保分配给指针的地址是程序中数据的有效地址*。根据前面的陈述，我们知道代码片段 `int *p=1234` 因类型错误而无效。

另一方面，以下代码片段是有效的，因为指针 `p` 是用在指针 `p` 被声明和初始化 *之前* 声明的变量 `x` 的地址进行初始化的：

```c
int x = 7;
int *p = &x;
```

限制的原因是指针只能用于访问程序中的其他数据。编译器可以假设你的程序是正确的，并且指针始终引用有效数据。编译器可以根据此假设优化你的代码；如果你违反此规则，则程序可能会崩溃。

另一个需要注意的点：使用指针允许你通过更改给定内存地址的内容来修改它指向的数据。以下是一个示例：

```c
// x is initially 7
int x = 7;

// p points to the location of x
int *p = &x;

// update the contents of x via p
*p = 1234;

// x is now equal to 1234!
```

### const 指针

常量指针，有时称为“指向 const 的指针”，是指不能用于修改其指向的数据的指针，例如：

```c
const char *name_ptr = "Test";
```

如果我们把 const 放在 `*` 之后，那么 const 的含义就会改变。如果声明以 `char * const` 开始，则指针永远不能被修改为指向不同的位置，但它可用于修改其指向的字符。

最后，将 const 放在两个位置以创建一个不可修改的指针和不可更改的数据项，如下所示：

```c
const char *const title_ptr = "Title";
```

## 指向整数变量的指针

列表 5.1 显示了 SimplePointer1.c 的内容，说明如何使用指针更改类型为 int 的变量的值。请确保你已阅读上一节，以便理解本节中的代码。虽然你在本章前面已经看到列表 5.1 的第一部分，但在这里重复是为了提供额外的强化。

### 列表 5.1：SimplePointer1.c

```c
#include <stdio.h>

int main()
{
    int x = 7;
    printf("Value of x:  %d\n", x);

    // ptr "points" to location of x:
    int *ptr = &x;
    *ptr = 45;
    printf("Value of x:  %d\n", x);

    // update value of x to 1234;
    *(&x) = 1234;
    printf("Value of x:  %d\n", x);

    // error: cannot assign x to an explicit address
```


```c
// &x = 1234;
return 0;
}
```

清单5.1包含你在本章前面看到过的相同代码，但这次是以一个完整的C程序出现。再次注意清单5.1末尾附近的注释，它解释了为什么该赋值语句无效。

清单5.1的输出如下：

```text
Value of x:  7
Value of x:  45
Value of x:  1234
```

让我们用一些其他指针示例来扩展前面的代码示例。清单5.2显示了SimplePointer2.c的内容，它演示了如何使用指针来改变类型为int的非指针变量的值。

## 清单5.2：SimplePointer2.c

```c
#include <stdio.h>

int main()
{
    int x = 7;
    printf("Value of x:  %d\n", x);

    // ptr "points" to location of x:
    int *ptr = &x;

    // ptr2 points to same location as ptr:
    int *ptr2 = ptr;

    // update value of x:
    *ptr2 = 5678;

    printf("Value of x:  %d\n", x);
    printf("Value of ptr: %d\n", *ptr2);
    printf("Value of ptr2: %d\n", *ptr2);

    return 0;
}
```

清单5.2包含变量x，其初始值为7，随后是指针ptr，它与清单5.2中的指针ptr相同。接下来，指针ptr2被初始化为指针ptr所指向的位置，之后ptr2的内容被改为5678。结果可能正如你所料：该变量的新值是5678。清单5.2的输出如下：

```text
Value of x:  7
Value of x: 5678
Value of ptr: 5678
Value of ptr2: 5678
```

## 清单5.3：SimplePointer3.c

```c
#include <stdio.h>

int main()
{
    int x = 7;
    printf("Value of x:  %d\n", x);

    // ptr "points" to location of x:
    int *ptr = &x;
    printf("Value of ptr:  %d\n", *ptr);

    // ptr2 points to same location as ptr:
    int *ptr2 = ptr;
    printf("Value of ptr2: %d\n", *ptr2);

    // the address of ptr2 plus one:
    int *ptr3 = ptr2+1;
    printf("Value of ptr3: %d\n", *ptr3);

    // uncomment this block to see the error message:
    //int *ptr4 = *ptr2+1;
    //printf("Value of ptr4: %d\n", *ptr4);

    return 0;
}
```

清单5.3的第一部分与清单5.2相同，随后是指针`ptr3`，它被初始化为表达式`ptr2+1`的值。这里有两种可能性：前面的表达式要么等于`ptr2`的内容加1（等于8），要么等于`ptr2`所保存的内存地址加1。如果你选择了后者，那么你答对了！清单5.3的输出如下：

```text
Value of x:   7
Value of ptr:  7
Value of ptr2: 7
Value of ptr3: 1406395048
```

## 多个指针和整型变量

清单5.4显示了PointersNumbers1.c的内容，它演示了如何在C程序中结合整数和指针。

## 清单5.4：PointersNumbers1.c

```c
#include <stdio.h>

int main()
{
    int x=3, y=5;
    int *ptr;

    printf("x = %d\n", x);
    printf("y = %d\n", y);

    ptr = &x;
    *ptr = 7;

    ptr = &y;
    *ptr = 23;

    printf("x = %d\n", x);
    printf("y = %d\n", y);
}
```

清单5.4包含两个整型变量x和y，其值分别为3和5。接下来，指针ptr被赋予变量x的内存位置，之后该位置的值被改为7。

接下来，指针ptr被赋予变量y的内存位置，之后该地址的值被改为23。清单5.4的输出如下：

```text
x = 3
y = 5
x = 7
y = 23
```

### 指针与字符串

在本章到目前为止，你已经看到了各种关于指针和整型变量的示例。你也可以将指针指向由字符串（例如"John Smith"）占用的内存位置。涉及指针和C结构体的示例将在本章后面和下一章中出现。

C语言中指向字符串的指针可以用多种方式表达，所有方式都能达到相同的结果。在定义C指针时，请记住必须指定数据类型，因为内存位置的内容没有限制：它可以是标准C数据类型或自定义数据结构（第6章讨论）的起始地址。因此，指针需要有关内存位置处数据类型（int、char等）的信息。

## 清单5.5：SimpleString.c

```c
#include <stdio.h>

int main()
{
  char *str = "thisisalongstring";

  char *ptr1 = (char *)&str;  // incorrect
  char *ptr2 = (char *)&str[0];
  char *ptr3 = &str[0];
  char *ptr4 = str;
//char *ptr5 = &str;       // warning

  printf("str: %s\n", str);
//printf("ptr1: %s\n", ptr1);
  printf("ptr2: %s\n", ptr2);
  printf("ptr3: %s\n", ptr3);
  printf("ptr4: %s\n", ptr4);
//printf("ptr5: %s\n", ptr5);

  return 0;
}
```

让我们逐一查看清单5.5中的每个指针声明，以了解它们的相同点和不同点。如果你需要多次阅读下面的描述，这完全没问题（毕竟，C语言中的指针概念对你来说还很陌生）。

清单5.5首先将指针`str`初始化为硬编码字符串`thisisalongstring`的位置。接下来，变量`ptr1`和`ptr5`指向变量`str`的地址，而`ptr2`、`ptr3`和`ptr4`指向字符串字面量中的第一个字符。

`ptr1`的声明使它指向变量`str`，这是无效的，因为`str`不是一个字符，而是一个字符指针。这一行上的类型转换可以防止编译器对类型不匹配发出警告。

可以将`ptr2`的初始化语句理解为“获取`str`所指向的字符串中的第一个字符，然后取其地址，再将其转换为`char*`”，这是有效的，但有点繁琐。这个转换是不必要的，因为数据类型已经是`char *`，而且第一个字符的地址与已经存储在`str`中的值相同。

`ptr3`的声明与`ptr2`具有相同的效果，但省略了不必要的类型转换；`ptr4`的声明还省略了取地址和索引操作。

尽管这种做法可能很诱人，`ptr5`的语法会产生以下编译警告：

```text
SimpleString.c:10:17: warning: initialization from incompatible pointer type
[-Wincompatible-pointer-types]
    char *ptr5 = &str; // warning
         ^
```

清单5.5的下一部分包含六个`printf()`语句，用于打印这六个指针内容的值。清单5.5的输出如下：

```text
str: thisisalongstring
ptr2: thisisalongstring
ptr3: thisisalongstring
ptr4: thisisalongstring
```

在定义指向字符串的指针时，使用`ptr2`、`ptr3`或`ptr4`的语法（`ptr4`的语法最简洁），并保持你的编码风格一致。

## 显示字符串的子串

本节中的示例主要是有趣，但它很有用，因为它演示了如何让指针“走”过字符串并显示部分字符串，这一切都在嵌套循环中完成。

清单5.6显示了Substrings.c的内容，它演示了如何显示给定字符串的子串。

## 清单5.6：Substrings.c

```c
#include <stdio.h>

int main()
{
    char *str = "thisisalongstring";
    int len = strlen(str);

    for(int i=1; i<=len; i++)
    {
        printf("%2d: ",i);
        for(int j=0; j<i; j++)
        {
            printf("%c", (char)str[j]);
        }
        printf("\n");
    }
}
```

清单5.6以一个字符型指针`str`开始，它指向一个字符串。回想本章前面关于字符串的讨论：将指针解引用后的值赋给字符指针，是初始化字符指针的一种合法方式。

清单5.6的下一部分包含一对嵌套循环。外层循环遍历`str`所引用的字符串中的每个字符，内层循环则遍历`str`字符串中在当前字符之前（包括当前字符）的所有字符。

清单5.6引入了C内建函数`strlen()`，它返回字符串的长度。清单5.6的输出如下：

```text
1: t
2: th
3: thi
4: this
5: thisi
6: thisis
7: thisisa
8: thisisal
9: thisisalo
10: thisisalon
11: thisisalong
12: thisisalongs
13: thisisalongst
14: thisisalongstr
15: thisisalongstri
16: thisisalongstrin
17: thisisalongstring
```




## 在 C 中显示命令行参数

你可以确定作为命令行参数传递给 C 程序的参数数量（及其基于字符串的值），使用以下修改后的 main() 函数语法：

```
int main(int argc, char *argv[])
```

参数 argc 是命令参数的数量，而 argv 是一个指向数组的指针，该数组包含在命令行中指定的实际参数。正如你所见，main() 方法中的第二个参数有一个细微的“变化”：char ** argv，实际上与 char *argv[] 相同。我们将使用后一种语法，因为它在概念上更容易（即指向字符串数组的指针）。

列表 5.7 显示了 PrintCmdLineArgs.c 的内容，说明如何打印 C 程序的命令行参数。

### LISTING 5.7: PrintCmdLineArgs.c

```c
#include <stdio.h>

int main(int argc, char *argv[])
{
    int i;

    printf("Display Command Line Arguments\n");
    for( i = 0; i < argc; ++i )
    {
        printf("Argument %d = \"%s\"\n", i, argv[i]);
    }

    return 0;
}
```

列表 5.7 包含一个循环，遍历命令行参数并通过 `printf()` 函数打印它们。编译代码后，按如下方式启动列表 5.7 中的程序（你可以使用不同的参数）：

```
/PrintCmdLineArguments 1 a 2 b 3 c
```

输出如下：

```
Display Command Line Arguments
Argument 0 = "./PrintCmdLineArguments"
Argument 1 = "1"
Argument 2 = "a"
Argument 3 = "2"
Argument 4 = "b"
Argument 5 = "3"
Argument 6 = "c"
```

你可以轻松检查参数数量并使用 `exit()` 函数提前退出，如以下代码块所示：

```c
#include <stdio.h>
#include <stdlib.h> // required for the exit() function

int main(int argc, char *argv[])
{
    if( argc < 3 )
    {
        fprintf(stderr, "Not enough Arguments: %d\n", argc);
        exit(-1);
    }

    // proceed normally...
}
```

尽管你可以使用 `abort()` 函数提前退出，但请记住后者不会刷新打开文件的缓冲区。此外，在 Unix 系统上，abort() 函数会导致核心转储。

## 递增指针：内存位置与值

C 支持指针算术（即加法和减法）。你需要理解在指针 *location* 上加法（递增）与在指针的 *value* 上加法（递增）之间的区别。事实上，我们在列表 5.2 中已经看到过访问指针位置的示例。

为了说明这种区别，请考虑以下代码片段：

```cpp
char array[5];
char *array_ptr = &array[0];
```

在前面的代码片段中，*array_ptr* 与 array[0] 相同，*(array_ptr+1)* 与 array[1] 相同，*(array_ptr+2)* 与 array[2] 相同，以此类推。请注意括号的使用。

然而，(*array_ptr*)+1 与 array[1] 不同，因为 +1 在括号之外，这意味着它是在解引用后添加的。因此，表达式 (*array_ptr*)+1 与 array[0]+1 相同。

回想一下，数组由连续的内存位置组成，每个位置保存数组的一个元素。例如，如果数组 `myarr` 从内存位置 `0xff001320` 开始，则 `myarr[0]` 具有相同的地址，而 `myarr` 占用的内存位置——在整数的情况下——在此位置之后 4 个字节：`0xff001324`（对于 double 则是 8 个字节）。

当你定义一个指针时，你指定指针的数据类型，因此递增指针会使内存位置按数据类型关联的字节数递增：字符为 1 个字节，整数为 4 个字节，double 为 8 个字节。

列表 5.8 显示了 ArrayAndPointer1.c 的内容，说明如何打印简单字符数组的元素（及其地址）。

### LISTING 5.8: ArrayAndPointer1.c

```c
#include <stdio.h>

int main()
{
  int numbers[5] = {2, 3, 5, 7, 11};
  printf("First item in numbers = %i\n", *numbers);

  int *numbers2 = &numbers[1];
  printf("First item in numbers2 = %i\n", numbers2[0]);

  return 0;
}
```

列表 5.8 定义了包含五个整数的数组 numbers，随后是一个 printf() 语句，显示 numbers 数组中的第一个数字。请注意 *numbers2 用于指向 numbers 数组中的第一个元素。

接下来，列表 5.8 定义了指针 numbers2，它使用 numbers 数组中第二个数字的内存位置进行初始化。

编译列表 5.8 中的代码并启动可执行文件，你将看到以下输出：

```
First item in numbers = 2
First item in numbers2 = 3
```

## 指针与数组

列表 5.9 显示了 PointersToNumbers1.c 的内容，说明如何使用索引遍历数组的元素，并展示了一种在自己的代码中最好避免的编码风格。

### LISTING 5.9: PointersToNumbers1.c

```c
#include <stdio.h>

int array[] = {4, 5, 8, 9, 8, 1, 0, 1, 9, 3};

int main()
{
    int index;
    while (array[index] != 0)
        ++index;

    printf("Number of elements before 9: %d\n", index);

    return (0);
}
```

列表 5.9 以全局变量 array 的定义开始，该变量用 10 个整数初始化。main() 函数包含一个 while 循环，遍历 array 的元素，并在每次迭代期间递增变量 index。当遇到值 0 时，while 循环结束，然后显示 index 的值。启动代码的输出如下：

Number of elements before 9: 6

需要注意的是，以下语法简洁但可能被误读（尤其是对新手而言）：

```
while (array[index] != 0)
    ++index;
```

你可能会认为前面的 `while` 循环“卡”在无限循环中，因为变量 `index` 的值 *从未被递增*。事实上，语句 `++index;` 是“附加”到 `while` 循环的，最终循环会终止。

以下代码片段与前面的代码片段等价。然而，语法是明确的，并强调变量 `index` 在 `while` 循环的每次迭代中都会被递增：

```c
while (array[index] != 0)
{
    ++index;
}
```

前面的代码块是 100% 无歧义的（即使对新手也是如此）。前述代码片段的另一个优点是，你可以轻松地在花括号内添加更多代码，而不会意外忘记包含现有的 `++index;` 语句。

## 指针、数组与地址

`Listing 5.10` 显示了 `PointersToNumbers2.c` 的内容，说明如何打印简单字符数组的元素（及其地址）。

### LISTING 5.10: PointersNumbers2.c

```c
#include <stdio.h>

#define ARRAY_SIZE 10
char array[ARRAY_SIZE + 1] = "0123456789";

int main()
{
    int index;

printf("&array[index] (array+index) array[index]\n");

for(index=0; index < ARRAY_SIZE; ++index) {
    printf("0x%-10p 0x%-10p 0x%x\n",
        &array[index],(array+index),array[index]);
}

return 0;
}
```

列表 5.10 以 #define 指令开始（一个执行文本替换的预处理器指令），将 ARRAY_SIZE 设置为值 10。下一个代码片段定义了基于字符的变量 array，它用 10 个数字初始化，这些数字被视为字符。

回想一下，字符占用一个字节，因此连续的数组元素占用连续的内存地址。接下来，short int 占用两个字节，这意味着连续数组元素的内存地址增加两个（而不是一个）。

此外，C 会自动执行正确的指针算术（即按正确数量递增）。因此，表达式 array+1 被正确解释：它指的是索引为 1 的元素（即数组中的第二个元素）。换句话说，array+1 使索引值递增 1，而不是使地址值递增 1。因此，以下代码片段是等价的：

```
array_ptr = &array[0];
array_ptr = array;
```

列表 5.10 的输出如下：

```
&array[index] (array+index) array[index]
0x0x1033e3020 0x0x1033e3020 0x30
```




```c
    return (0);
}
```

注意，当我们希望查看数组中的数据时，我们使用解引用运算符（`*`）。该运算符用于以下语句：

```c
while (*arr_ptr != 0)
```

当我们希望改变指针本身时，不使用其他运算符。例如，下面的代码片段递增指针（而不是数据）：

```c
++arr_ptr;
```

我们再次看到一个编码风格的示例，它有一种更显式的替代写法：

```c
while (*arr_ptr != 0) ++arr_ptr;
```

考虑使用以下替代语法，它只多按几个键，并且可能更不容易出错：

```c
while (*arr_ptr != 0)
{
    ++arr_ptr;
}
```

## 计算方阵的转置

在第 2 章中，你了解到方阵的转置是通过交换行和列位置来交换矩阵元素的结果。换句话说，如果矩阵 A 的 (i,j) 位置处元素的值是 a(i,j)，那么矩阵 A 的转置的 (i,j) 位置处元素的值就是 a(j,i)。

清单 5.12 显示了 Transpose.c 的内容，它说明如何计算方阵的转置，以及如何使用一个函数在计算转置前后显示矩阵的内容。

### 清单 5.12：Transpose.c

```c
#include <stdio.h>

void ptrArray(int *arr, int row, int col)
{
    for(int i=0; i<row; i++)
    {
        printf("Row %d: ",i);
        for(int j=0; j<col; j++)
        {
            printf("%d ", *(arr+i*row+j));
        }
        printf("\n");
    }
}

int main()
{
    int row=3, col=3, temp=0;
    int arr1[3][3] = {{1,2,3}, {4,5,6}, {7,8,9}};

    // display original matrix
    printf("Original\n");
    ptrArray(&arr1[0][0], row, col);

    for(int i=1; i<row; i++)
    {
        for(int j=0; j<i; j++)
        {
            temp = arr1[i][j];
            arr1[i][j] = arr1[j][i];
            arr1[j][i] = temp;
        }
    }

    // display transposed matrix
    printf("Transpose\n");
    ptrArray(&arr1[0][0], col, row);

    return 0;
}
```

清单 5.12 从用户定义函数 `ptrArray()` 开始，该函数显示数组的内容。此函数有三个参数：第一个是指向数组的指针，第二个是数组中的行数，第三个是数组中的列数。函数 `ptrArray()` 包含一个嵌套循环，它遍历数组的行和列，并显示每个位置的值。

接下来，函数 `main()` 初始化一些标量变量以及包含整数值的数组 `arr1`。`main()` 的下一部分包含一个嵌套循环，它使用临时变量 `temp` 来“交换”数组元素 `arr1[i][j]` 和 `arr1[j][i]`，之后 `arr1` 中的元素就是原始值的转置。

`main()` 的底部调用函数 `ptrArray()` 来显示转置矩阵的内容。注意变量 **row** 和 **col** 被交换了（如粗体所示）：如果 A 是 mxn 矩阵，那么 A 的转置是 nxm 矩阵。清单 5.12 的输出如下：

```
Original
Row 0: 1 2 3
Row 1: 4 5 6
Row 2: 7 8 9
Transpose
Row 0: 1 4 7
Row 1: 2 5 8
Row 2: 3 6 9
```

如你所见，清单 5.12 包含两个相同的代码块：更好的解决方案是使用一个函数（在第 3 章讨论）来打印数组的内容。

## 指针与字符串

清单 5.13 显示了 `PointersStrings1.c` 的内容，它说明如何初始化字符串和指针。

### 清单 5.13：PointersStrings1.c

```c
#include <stdio.h>

int main()
{
    char *ptr1 = "Hello World";
    char str1[] = "Hello World";
    char *ptr2 = str1;

    printf("%s\n", ptr1);
    printf("%s\n", str1);
    printf("%s\n", ptr2);

    return 0;
}
```

清单 5.13 包含一个 `main()` 函数，它定义了三个变量 `ptr1`、`str1` 和 `ptr2`，它们分别是指向字符串的指针、字符字符串数组，以及指向该字符串数组的指针。执行清单 5.13 中代码的输出会为所有三个变量显示相同的字符串（它们全都相同）。

请记住，下面的代码会导致错误：

```c
char str2[] = "Hello World";
```

执行清单 5.13 中代码的输出如下：

```
Hello World
Hello World
Hello World
```

## 指针与内置字符串操作函数

C 支持多种多样的内置字符串操作函数。下面的列表大致汇总了提供此类功能的 C 函数，并简要说明其用途（从名称即可相当明显地看出）。

- 使用 `strcpy()` 函数将 src 字符串复制到 dest 字符串：

  ```c
  char *strcpy (char *dest, char *src);
  ```

- 使用 `strncpy()` 函数将 string2 的前 n 个字符复制到 string1：

  ```c
  char *strncpy(char *string1, char *string2, int n);
  ```

- 使用 `strcmp()` 函数比较 string1 和 string2，以确定字母顺序：

  ```c
  int strcmp(char *string1, char *string2);
  ```

- 使用 `strncmp()` 函数比较两个字符串的前 n 个字符：

  ```c
  int strncmp(char *string1, char *string2, int n);
  ```

清单 5.14 显示了 WhileLoopStr.c 的内容，向你展示如何在 C 程序中使用 while 循环。

### 清单 5.14：WhileLoopStr.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "hello";
    char *p = str;
    int i=0;
    int len = strlen(str);

    printf("First Loop\n");
    printf("---------\n");
    while(i<len)
    {
        printf("i : %c\n", str[i]);
        ++i;
    }

    printf("\nSecond Loop\n");
    printf("---------\n");
    while(*p)
    {
        printf("char : %s\n", p);
        ++p;
    }

    return 0;
}
```

清单 5.14 包含一个 main() 函数，它定义了变量 `str` 和 `p`（它们是指向字符串的指针），以及变量 `len`（它是字符串 `str` 的长度）。

接下来，`main()` 函数包含一个循环，它遍历变量 `str` 所引用的字符串中的字符。`main()` 函数包含第二个循环，它遍历同一组字符，但这次是通过推进指针 `p` 的位置来实现的。清单 5.14 的输出如下：

```
First Loop
---------
i : h
i : e
i : l
i : l
i : o

Second Loop
-----------
char : hello
char : ello
char : llo
char : lo
char : o
```

如果你把 `while(*p)` 替换为语句 `while(p)`，你认为会发生什么？如果你的答案是第二个 `while` 循环中会出现“无限循环”，那你就对了。原因很简单：`while(p)` 总是求值为真，因为 `p` 具有非空地址；而当指针 `p` 到达字符串 `str` 的末尾时，`while(*p)` 会求值为假。在使用指针算术时请记住这个细节。

## 统计文本字符串中的元音和辅音

`strchr()` 函数定位字符在文本字符串中第一次出现的位置。清单 5.15 显示了 `CountVowelsConsonants.c` 的内容，它说明如何统计文本字符串中元音、辅音和其他字符的数量。

### 清单 5.15：CountVowelsConsonants.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int charType(char ch)
{
    char ch2 = tolower(ch);

    if(ch2 =='a' || ch2 =='e' || ch2 =='i' || ch2 =='o' || ch2 =='u')
    {
        return 0;
    }
    else if(isalpha(ch2))
    {
        return 1;
    }
    else if(isdigit(ch2))
    {
        return 2;
    }
    else
    {
        return 3;
    }
}

int main()
{
    char str[] = "This is a string with some short words 1 2 3 4 that wraps around and let's see how well the code in this code sample actually works!";

    char *ptr = str;

    int result, counts[4];
    counts[0] = counts[1] = counts[2] = counts[3] = 0;

    while(*ptr)
    {
        result = charType(*ptr);
        ++counts[result];
        ptr++;
    }

    printf("VOWELS:   %d\n",counts[0]);
    printf("CONSONANT: %d\n",counts[1]);
    printf("DIGITS:   %d\n",counts[2]);
    printf("OTHERS:   %d\n",counts[3]);

    return 0;
}
```

清单 5.15 从函数 charType() 的定义开始，该函数接受一个字符作为参数，返回类型为 int。此函数包含条件逻辑，用于判断参数 ch 是元音（通过逐一检查每个元音是否出现）、字母字符（使用 C 内置函数 isalpha()）、数字（使用 C 内置函数 isdigit()），还是其他某个字符。返回值是 0 到 3（含 0 和 3）之间的整数，具体取决于执行条件逻辑的哪一部分。在本节后面，你将看到指定这些返回值的原因。

清单 5.15 的下一部分是 main() 函数，它使用硬编码字符串初始化字符数组 str，随后是字符指针 ptr，该指针是


使用变量 str 的位置进行初始化。counts 数组有四个整数值，所有值初始为 0。

Listing 5.15 的下一部分是一个循环，使用指针 ptr 遍历变量 str 的每个字符。在每次迭代中，当前字符会被传递给 charType() 函数，并使用返回值递增 counts 数组中对应的位置。ptr 的位置递增一，while() 再次执行，直到到达硬编码字符串的末尾。

Listing 5.15 的输出如下：

First Loop
VOWELS: 33
CONSONANT: 66
DIGITS: 4
OTHERS: 25

## 在 C 中查找文本字符串中的单词

`strchr()` 函数定位文本字符串中字符的首次出现。Listing 5.16 显示了 FindChar1.c 的内容，说明如何在一个文本字符串中查找字符。

### LISTING 5.16: FindChar1.c

```c
#include <stdio.h>
#include <string.h>

#define SIZE 80

int main(void)
{
    char line[SIZE] = "New York Pizza";
    char *ptr;
    int ch = 'z';

    ptr = strchr(line, ch);
    printf("The first occurrence of %c in \"%s\" is \"%s\"\n",
           ch, line, ptr);

    return 0;
}
```

[Listing 5.16] 以初始化字符字符串 `line` 与硬编码字符串开始，随后声明字符指针 `ptr` 并将整数值变量 `ch` 初始化为 "z。"

接下来，`ptr` 被赋值为调用内置 C 函数 `strchr()` 时返回的值，参数为 `line` 和 `ch`。正如本章前面所见，此函数返回分配给参数 `ch` 的字符的首次出现。

启动 [Listing 5.16] 中的代码的输出如下：

```
The first occurrence of z in 'New York Pizza' is 'zza'
```

## 在 C 中搜索文本字符串中的单词

`strstr()` 函数定位以 null 结尾的字符串 `s2` 在以 null 结尾的字符串 `s1` 中的首次出现。`strcasestr()` 函数与 `strstr()` 类似，但忽略两个字符串的大小写。后者函数不是标准 C 的一部分；然而，它是常见（但不通用）的厂商扩展。

[Listing 5.17] 显示了 SearchForWordInString.c 的内容，说明如何将文本字符串标记化为单词。

### LISTING 5.17: SearchForWordInString.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "One two Three four";
    char *word1 = "our";
    char *word2 = "three";

    if((strstr(str, word1)) != NULL)
    {
        printf("Current Line: %s\n", str);
        printf("Exact Match: %s\n\n", word1);
    }

    return 0;
}
```

Listing 5.17 以初始化字符字符串 str 与硬编码字符串开始，随后使用字符串 our 和 three 分别初始化字符指针 word1 和 word2。

接下来，代码包含一个条件块，调用内置 C 函数 strstr() 检查 word 是否存在于 str1 中，如果找到匹配项，则显示适当的[content]
使用变量 str 的位置进行初始化。counts 数组有四个整数值，所有值初始为 0。

Listing 5.15 的下一部分是一个循环，使用指针 ptr 遍历变量 str 的每个字符。在每次迭代中，当前字符会被传递给 charType() 函数，并使用返回值递增 counts 数组中对应的位置。ptr 的位置递增一，while() 再次执行，直到到达硬编码字符串的末尾。

Listing 5.15 的输出如下：

First Loop
VOWELS: 33
CONSONANT: 66
DIGITS: 4
OTHERS: 25

## 在 C 中查找文本字符串中的单词

`strchr()` 函数定位文本字符串中字符的首次出现。Listing 5.16 显示了 FindChar1.c 的内容，说明如何在一个文本字符串中查找字符。

### LISTING 5.16: FindChar1.c

```c
#include <stdio.h>
#include <string.h>

#define SIZE 80

int main(void)
{
    char line[SIZE] = "New York Pizza";
    char *ptr;
    int ch = 'z';

    ptr = strchr(line, ch);
    printf("The first occurrence of %c in \"%s\" is \"%s\"\n",
           ch, line, ptr);

    return 0;
}
```

[Listing 5.16] 以初始化字符字符串 `line` 与硬编码字符串开始，随后声明字符指针 `ptr` 并将整数值变量 `ch` 初始化为 "z。"

接下来，`ptr` 被赋值为调用内置 C 函数 `strchr()` 时返回的值，参数为 `line` 和 `ch`。正如本章前面所见，此函数返回分配给参数 `ch` 的字符的首次出现。

启动 [Listing 5.16] 中的代码的输出如下：

```
The first occurrence of z in 'New York Pizza' is 'zza'
```

## 在 C 中搜索文本字符串中的单词

`strstr()` 函数定位以 null 结尾的字符串 `s2` 在以 null 结尾的字符串 `s1` 中的首次出现。`strcasestr()` 函数与 `strstr()` 类似，但忽略两个字符串的大小写。后者函数不是标准 C 的一部分；然而，它是常见（但不通用）的厂商扩展。

[Listing 5.17] 显示了 SearchForWordInString.c 的内容，说明如何将文本字符串标记化为单词。

### LISTING 5.17: SearchForWordInString.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "One two Three four";
    char *word1 = "our";
    char *word2 = "three";

    if((strstr(str, word1)) != NULL)
    {
        printf("Current Line: %s\n", str);
        printf("Exact Match: %s\n\n", word1);
    }

    return 0;
}
```

Listing 5.17 以初始化字符字符串 str 与硬编码字符串开始，随后使用字符串 our 和 three 分别初始化字符指针 word1 和 word2。

接下来，代码包含一个条件块，调用内置 C 函数 strstr() 检查 word 是否存在于 str1 中，如果找到匹配项，则显示适当的[content]
使用变量 str 的位置进行初始化。counts 数组有四个整数值，所有值初始为 0。

Listing 5.15 的下一部分是一个循环，使用指针 ptr 遍历变量 str 的每个字符。在每次迭代中，当前字符会被传递给 charType() 函数，并使用返回值递增 counts 数组中对应的位置。ptr 的位置递增一，while() 再次执行，直到到达硬编码字符串的末尾。

Listing 5.15 的输出如下：

First Loop
VOWELS: 33
CONSONANT: 66
DIGITS: 4
OTHERS: 25

## 在 C 中查找文本字符串中的单词

`strchr()` 函数定位文本字符串中字符的首次出现。Listing 5.16 显示了 FindChar1.c 的内容，说明如何在一个文本字符串中查找字符。

### LISTING 5.16: FindChar1.c

```c
#include <stdio.h>
#include <string.h>

#define SIZE 80

int main(void)
{
    char line[SIZE] = "New York Pizza";
    char *ptr;
    int ch = 'z';

    ptr = strchr(line, ch);
    printf("The first occurrence of %c in \"%s\" is \"%s\"\n",
           ch, line, ptr);

    return 0;
}
```

[Listing 5.16] 以初始化字符字符串 `line` 与硬编码字符串开始，随后声明字符指针 `ptr` 并将整数值变量 `ch` 初始化为 "z。"

接下来，`ptr` 被赋值为调用内置 C 函数 `strchr()` 时返回的值，参数为 `line` 和 `ch`。正如本章前面所见，此函数返回分配给参数 `ch` 的字符的首次出现。

启动 [Listing 5.16] 中的代码的输出如下：

```
The first occurrence of z in 'New York Pizza' is 'zza'
```

## 在 C 中搜索文本字符串中的单词

`strstr()` 函数定位以 null 结尾的字符串 `s2` 在以 null 结尾的字符串 `s1` 中的首次出现。`strcasestr()` 函数与 `strstr()` 类似，但忽略两个字符串的大小写。后者函数不是标准 C 的一部分；然而，它是常见（但不通用）的厂商扩展。

[Listing 5.17] 显示了 SearchForWordInString.c 的内容，说明如何将文本字符串标记化为单词。

### LISTING 5.17: SearchForWordInString.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "One two Three four";
    char *word1 = "our";
    char *word2 = "three";

    if((strstr(str, word1)) != NULL)
    {
        printf("Current Line: %s\n", str);
        printf("Exact Match: %s\n\n", word1);
    }

    return 0;
}
```

Listing 5.17 以初始化字符字符串 str 与硬编码字符串开始，随后使用字符串 our 和 three 分别初始化字符指针 word1 和 word2。

接下来，代码包含一个条件块，调用内置 C 函数 strstr() 检查 word 是否存在于 str1 中，如果找到匹配项，则显示适当的[content]
使用变量 str 的位置进行初始化。counts 数组有四个整数值，所有值初始为 0。

Listing 5.15 的下一部分是一个循环，使用指针 ptr 遍历变量 str 的每个字符。在每次迭代中，当前字符会被传递给 charType() 函数，并使用返回值递增 counts 数组中对应的位置。ptr 的位置递增一，while() 再次执行，直到到达硬编码字符串的末尾。

Listing 5.15 的输出如下：

First Loop
VOWELS: 33
CONSONANT: 66
DIGITS: 4
OTHERS: 25

## 在 C 中查找文本字符串中的单词

`strchr()` 函数定位文本字符串中字符的首次出现。Listing 5.16 显示了 FindChar1.c 的内容，说明如何在一个文本字符串中查找字符。

### LISTING 5.16: FindChar1.c

```c
#include <stdio.h>
#include <string.h>

#define SIZE 80

int main(void)
{
    char line[SIZE] = "New York Pizza";
    char *ptr;
    int ch = 'z';

    ptr = strchr(line, ch);
    printf("The first occurrence of %c in \"%s\" is \"%s\"\n",
           ch, line, ptr);

    return 0;
}
```

[Listing 5.16] 以初始化字符字符串 `line` 与硬编码字符串开始，随后声明字符指针 `ptr` 并将整数值变量 `ch` 初始化为 "z。"

接下来，`ptr` 被赋值为调用内置 C 函数 `strchr()` 时返回的值，参数为 `line` 和 `ch`。正如本章前面所见，此函数返回分配给参数 `ch` 的字符的首次出现。

启动 [Listing 5.16] 中的代码的输出如下：

```
The first occurrence of z in 'New York Pizza' is 'zza'
```

## 在 C 中搜索文本字符串中的单词

`strstr()` 函数定位以 null 结尾的字符串 `s2` 在以 null 结尾的字符串 `s1` 中的首次出现。`strcasestr()` 函数与 `strstr()` 类似，但忽略两个字符串的大小写。后者函数不是标准 C 的一部分；然而，它是常见（但不通用）的厂商扩展。

[Listing 5.17] 显示了 SearchForWordInString.c 的内容，说明如何将文本字符串标记化为单词。

### LISTING 5.17: SearchForWordInString.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "One two Three four";
    char *word1 = "our";
    char *word2 = "three";

    if((strstr(str, word1)) != NULL)
    {
        printf("Current Line: %s\n", str);
        printf("Exact Match: %s\n\n", word1);
    }

    return 0;
}
```

Listing 5.17 以初始化字符字符串 str 与硬编码字符串开始，随后使用字符串 our 和 three 分别初始化字符指针 word1 和 word2。

接下来，代码包含一个条件块，调用内置 C 函数 strstr() 检查 word 是否存在于 str1 中，如果找到匹配项，则显示适当的[content]
使用变量 str 的位置进行初始化。counts 数组有四个整数值，所有值初始为 0。

Listing 5.15 的下一部分是一个循环，使用指针 ptr 遍历变量 str 的每个字符。在每次迭代中，当前字符会被传递给 charType() 函数，并使用返回值递增 counts 数组中对应的位置。ptr 的位置递增一，while() 再次执行，直到到达硬编码字符串的末尾。

Listing 5.15 的输出如下：

First Loop
VOWELS: 33
CONSONANT: 66
DIGITS: 4
OTHERS: 25

## 在 C 中查找文本字符串中的单词

`strchr()` 函数定位文本字符串中字符的首次出现。Listing 5.16 显示了 FindChar1.c 的内容，说明如何在一个文本字符串中查找字符。

### LISTING 5.16: FindChar1.c

```c
#include <stdio.h>
#include <string.h>

#define SIZE 80

int main(void)
{
    char line[SIZE] = "New York Pizza";
    char *ptr;
    int ch = 'z';

    ptr = strchr(line, ch);
    printf("The first occurrence of %c in \"%s\" is \"%s\"\n",
           ch, line, ptr);

    return 0;
}
```

[Listing 5.16] 以初始化字符字符串 `line` 与硬编码字符串开始，随后声明字符指针 `ptr` 并将整数值变量 `ch` 初始化为 "z。"

接下来，`ptr` 被赋值为调用内置 C 函数 `strchr()` 时返回的值，参数为 `line` 和 `ch`。正如本章前面所见，此函数返回分配给参数 `ch` 的字符的首次出现。

启动 [Listing 5.16] 中的代码的输出如下：

```
The first occurrence of z in 'New York Pizza' is 'zza'
```

## 在 C 中搜索文本字符串中的单词

`strstr()` 函数定位以 null 结尾的字符串 `s2` 在以 null 结尾的字符串 `s1` 中的首次出现。`strcasestr()` 函数与 `strstr()` 类似，但忽略两个字符串的大小写。后者函数不是标准 C 的一部分；然而，它是常见（但不通用）的厂商扩展。

[Listing 5.17] 显示了 SearchForWordInString.c 的内容，说明如何将文本字符串标记化为单词。

### LISTING 5.17: SearchForWordInString.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "One two Three four";
    char *word1 = "our";
    char *word2 = "three";

    if((strstr(str, word1)) != NULL)
    {
        printf("Current Line: %s\n", str);
        printf("Exact Match: %s\n\n", word1);
    }

    return 0;
}
```

Listing 5.17 以初始化字符字符串 str 与硬编码字符串开始，随后使用字符串 our 和 three 分别初始化字符指针 word1 和 word2。

接下来，代码包含一个条件块，调用内置 C 函数 strstr() 检查 word 是否存在于 str1 中，如果找到匹配项，则显示适当的[content]
消息。启动 Listing 5.17 中的代码的输出如下：

Current Line: One two Three four

Exact Match: our

## 在 C 中连接两个字符串

Listing 5.18 显示了 ConcatenateStrings.c 的内容，说明如何使用 strcat() 和 strncat() 函数连接两个字符串。请注意以下区别：strcat() 函数将第二个字符串追加到第一个字符串，而 strncat() 函数仅将第二个字符串中指定数量的字符追加到第一个字符串。

### LISTING 5.18: ConcatenateStrings.c

```c
#include <stdio.h>
#include <string.h>

#define BUFFER_SIZE 80

int main()
{
    char line[BUFFER_SIZE] = "New York";
    char *ptr;

    // Call strcat with line and " pizza"
    ptr = strcat(line, " pizza");
    printf("strcat line = %s\n", line);

    // Reset line to contain the original string
    memset(line, '\0', sizeof(line));
    ptr = strcpy(line, "New York");
    strcpy(line, "New York");

    // Call strncat with line and two chars of "pizza"
    ptr = strncat(line, " pizza", 3);
    printf("strncat line = %s\n", line);

    return 0;
}
```

Listing 5.18 首先使用值 80 定义 BUFFER_SIZE（您将在第 7 章看到更多关于 #define 预处理器指令的内容）。接下来，main() 函数使用硬编码字符串初始化字符字符串 line，然后声明字符指针 ptr。

Listing 5.18 的下一部分使用内置 C 函数 strcat() 的返回值初始化 ptr，参数为 line 和字符串 “pizza”，之后显示 line 的新内容。

Listing 5.18 的下一部分使用内置 C 函数 strncat() 的返回值初始化 ptr，参数为 line 和字符串 “ pizza”，之后显示 line 的新内容。代码的最后一部分涉及对 strcat() 函数的第二次调用，以及显示结果。

Listing 5.18 的输出如下：

```
strcat line = New York pizza
strncat line = New York pi
```

## 摘要

本章向您介绍了 C 中指针的概念，以及指向数字、数组和字符串的指针的示例。您看到了如何使用指针分割字符串，以及使用指针查找数字除数的循环。接下来，您学习了如何定义指向数字数组的指针以及指向函数的指针。

您还学习了如何使用指针反转字符串、查找大写和小写字母，以及如何从字符串中删除空白。然后您看到了如何统计文本行中的单词，以及如何在 while 循环中处理单词和字符串。最后，您看到了在字符串中统计元音和辅音的示例，以及如何连接两个字符串。

## 第 6 章

### 使用指针

本章继续第 5 章开始的 C 指针讨论，并包含说明如何在 C 程序中使用指针的更复杂方式的代码示例。完成本章后，您将处于良好位置以理解第 7 章中关于如何将指针与 C 结构体结合使用的部分。

本章的第一部分包含说明如何比较两个字符串以及如何“标记化”文本字符串中的单词，以及如何检查字符串是否为回文的代码示例。

本章的第二部分向您介绍了一些内置的 C 函数，用于动态分配内存，以及一个在不再需要时释放该分配内存的 C 函数（从而避免内存泄漏）。本节还包含用于遍历数字数组的基于指针的代码示例，将字符串转换为大写或小写字母，以及如何找到正整数的素数除数。

本章的最后一部分包含说明如何定义指向函数的指针、函数指针作为参数、指向指针的指针，以及如何处理命令行参数的 C 程序。

尽管本章不会让您成为 C 指针专家，但您将能够理解包含指针的许多 C 程序，如何定义自己的基于指针的函数，并能够识别指针在 C 程序中使用的许多方式。

## 在 C 中比较两个字符串

`strcmp()` 函数是内置的 C 函数，可让您比较两个字符串。Listing 6.1 显示了 CompareStrings.c 的内容，说明如何使用 strcmp() 函数。

### LISTING 6.1: CompareStrings.c

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char *str1 = "abc";
    char *str2 = "abcd";

    int num = strcmp(str1, str2);

    printf("String1: %s\n", str1);
    printf("String2: %s\n", str2);

    if(strcmp(str1, str2) == 0 )
    {
        printf("Strings are equal: %s %s\n", str1, str2);
    }
}
```

```c
else if(strcmp(str1, str2) < 0 )
{
    printf("First < second:   %s %s\n", str1, str2);
}
else
{
    printf("First > second:   %s %s\n", str1, str2);
}

return 0;
}
```

清单 6.1 包含 `main()` 函数，该函数初始化字符指针 `str1` 和 `str2`。接下来，通过调用 `strcmp()` 函数并传入参数 `str1` 和 `str2` 来初始化整数 `num` 的值。

`main()` 函数的下一部分包含条件逻辑，根据 `strcmp()` 函数的值是否为 0、负数或正数来显示消息。输出如下：

```text
String1: abc
String2: abcd
First < second:   abc abcd
```

此外，还有内置的 C 函数 `strnicmp()`，它执行两个字符串的不区分大小写比较，如下所示：

```c
result = strnicmp(str1, str2, 8);
```

`strnicmp()` 的条件逻辑与第 5 章清单 5.18 中 `strcmp()` 的条件逻辑相同。

> 注意 `strnicmp()` 函数是厂商扩展，不是 C 标准的一部分。

## 使用 STRTOK() 对字符串进行标记化

考虑字符串形式为 "Last/First" 的情况，例如 "Smith/John"。任务是将此类字符串拆分为两个独立的字符串：" / " 符号左侧的字符串和右侧的字符串。我们可以通过内置的 C 函数 strtok() 来执行此任务。

strtok() 函数接收指向字符串的指针 (string_ptr) 和要查找的字符（例如 "/"）作为其参数。接下来，我们使用 while 循环在剩余字符串中查找后续标记。

### 清单 6.2：Tokenize.c

```c
#include <stdio.h>
#include <string.h>

char *delim = "/";

void tokenizeString(char *str)
{
    // first token = last name
    char *token = strtok(str, delim);
    char *second = token;
    char *first;
    int count = 0;

    // print token after delimiter
    while (token != NULL)
    {
        token = strtok(NULL, delim);
        first = token;
    }

    printf("NAME: %s %s\n", first, second);
}

int main()
{
    char *str;
    char names[4][20] = {
            "smith/jane",
            "edwards/john",
            "stone/dave",
            "anderson/kenneth",
    };

    for(int i=0; i<4; i++)
    {
        str = names[i];
        tokenizeString(str);
    }

    return 0;
}
```

清单 6.2 从函数 tokenizeString() 开始，该函数调用 strtok() 函数以获取字符串 str 中的第一个标记。此第一个标记被分配给字符串 second，因为它是姓氏（不是名字）。tokenizeString() 的下一部分包含一个循环，反复调用 strtok() 函数，直到读取 str 的末尾。请注意，strtok() 函数的每次调用都被分配给字符串 first。由于 str 中只有两个名字，因此进行此分配是正确的；即 while 循环将在 strtok() 函数的第一次调用后终止。

然而，如果 `str` 包含给定分隔符的多个出现，我们需要将 while 循环替换为以下代码块：

```c
// print token after delimiter
while (token != NULL)
{
    token = strtok(NULL, delim);
    first = token;
    if(++count == 1) break;
}
```

`main()` 函数使用四个按相反顺序排列的名字（例如 “Smith/John”）初始化数组 `names`。`main()` 函数的下一部分包含一个循环，遍历 `names` 数组的元素并调用函数 `tokenizeString()`。输出如下：

```text
NAME: jane smith
NAME: john edwards
NAME: dave stone
NAME: kenneth anderson
```

## 指针、字符串和回文

如果反转后的字符串与初始字符串相同，则该字符串是回文。清单 6.3 显示了 `StringPalindrome.c` 的内容，说明如何确定字符串是否为回文。

### 清单 6.3：StringPalindrome.c

```c
#include <stdio.h>
#include <string.h>

int scanString(char str[])
{
int result = 0;
char *ptr;
int len = strlen(str);

for(int i=0; i<len/2; i++)
{
    if(str[i] != str[len-i-1])
    {
        result = 1;
        break;
    }
}

return result;
}

int main()
{
    int result=0;
    char line1[] = "radar";
    char line2[] = "motion";
    char *results[] = {"YES", "NO"};

    int len1 = strlen(line1);
    int len2 = strlen(line2);

    result = scanString(line1);
    printf("Current Word: %s\n", line1);
    printf("Palindrome:  %s\n", results[result]);

    result = scanString(line2);
    printf("Current Word: %s\n", line2);
    printf("Palindrome:  %s\n", results[result]);

    return 0;
}
```

**清单 6.3** 包含一个 main() 函数，使用相同的硬编码字符字符串 "Hello World" 初始化指针 ptr1 和 str1，然后定义指向变量 `str1` 位置的字符指针 `ptr2`。其余代码由三个 `printf()` 语句组成。

编译并运行 [清单 6.3](#) 中的代码的输出如下：

```
Current Word: radar
Palindrome:  YES
Current Word: motion
Palindrome:   NO
```

## 按引用传递与按值传递

在 [第 4 章](#) 中，曾简要提到过这个主题，在本节中您将看到使用指针将数据结构传递给函数的示例。

在抽象计算机科学术语中，"按引用传递" 和 "按值传递" 之间存在区别。在按值传递的函数调用中，所有参数的本地副本都会被创建，因此函数无法更改调用范围中的任何数据。按引用传递意味着只传递数据的引用，因此函数所做的任何更改都会影响调用者中的实际数据。C 中没有 "按引用传递" 机制，因此这种行为通常通过传递指向实际数据的指针来模拟。在具有按引用传递语法的其他语言（如 C++ 或 C#）中，并不使用指针来实现此目的。

[清单 6.4](#) 显示了 PassByPointer.c 的内容，说明如何按引用和按值传递。

### 清单 6.4：PassByPointer.c

```c
#include <stdio.h>

int addNumbers1(int a, int b);
void addNumbers2(int a, int b, int * sum);

int addNumbers1(int a, int b)
{
    return (a+b);
}

void addNumbers2(int a, int b, int *sum)
{
    *sum = a+b;
}

int main()
{
    int num1=3, num2=5, sum1, *sum2=&sum1;

    sum1 = addNumbers1(num1, num2);
    printf("%d + %d = %d\n", num1, num2, sum1);

    addNumbers2(2*num1, 3*num2, sum2);
    printf("%d + %d = %d\n", 2*num1, 3*num2, *sum2);

    return 0;
}
```

清单 6.4 很简单：它初始化两个整数值变量，声明另一个整数值变量，然后初始化指向第三个变量位置的整数值指针。

接下来，使用 num1 和 num2 调用函数 addNumbers1()，然后使用 2*num1、3*num2 和 sum2 调用函数 addNumbers2()。每次方法调用后，都会打印各种变量的值。

请注意，函数 addNumbers1() 返回一个整数，而函数 addNumbers2() 更新第三个参数 sum 的值（即它不返回值）。整数值变量 sum2 以粗体突出显示，以便您可以轻松跟踪执行顺序并观察结果。

清单 6.4 的输出如下，您可能期望的结果为：

3 + 5 = 8
6 + 15 = 21

## 按指针传递数组

在函数调用的上下文中，数组被视为指向第一个元素的指针。这意味着无法按值传递数组，只能按引用传递。清单 6.5 显示了 PassArrayByPointer.c 的内容，说明如何按引用传递整数数组。

### 清单 6.5：PassArrayByPointer.c

```c
#include <stdio.h>

void multiplyArray2(int factor, int a[], int * result)
{
    for(int i=0; a[i] != '\0'; i++)
    {
        *(result+i) = factor*a[i];
    }
}

int main()
{
    int arr1[] = {1,2,3,4,5}, factor=3, * result=arr1;

    printf("Initial Values:\n");
    for(int i=0; arr1[i] != '\0'; i++)
```

```c
{
    printf( "%d ", arr1[i]);
}
printf( "\n" );

multiplyArray2(factor, arr1, result);

printf( "Updated Values:\n" );
for(int i=0; arr1[i] != '\0'; i++)
{
    printf( "%d ", arr1[i]);
}
printf( "\n" );

return 0;
}
```

**清单 6.5** 包含函数 `multiplyArray2()`，它将数组 `a`（该函数的一个参数）的值乘以一个数，而数组 `a` 和这个数都是该函数的参数。数组 `arr1` 更新后的内容可通过第三个参数访问，该参数是指向整数数组的指针。更新后的数组内容也存在于 `arr1` 中，因为数组没有被复制，而是按引用传递。

接下来，`main()` 函数用一些值初始化数组 `arr1`，将值 3 赋给变量 `factor`，然后用 `arr1` 的地址初始化基于指针的变量 `result`。

`main()` 函数包含两个循环，二者都显示数组 `arr1` 中的值。然而，第一个循环打印数组 `arr1` 的初始值，第二个循环打印在调用 `multiplyArray2()` 函数之后数组 `arr1` 的更新值。请注意，该函数会对数组 `arr1` 中每个元素的值执行乘法。

清单 6.5 的输出如下：

```text
Initial Values:
1 2 3 4 5
Updated Values:
3 6 9 12 15
```

## 使用指向数字的指针的 FOR 循环

清单 6.6 展示了 Palindromes1.c 的内容，说明如何判断一个字符串是否为回文。如果你已经忘了，回文是指自身呈“镜像”的数字或字符串，例如 12321、“rotor”和“radar”，而 1231 和“rattan”不是回文。

### 清单 6.6：Palindromes1.c

```c
#include <stdio.h>
#include <string.h>

int scanString(char str[])
{
    int result = 0;
    char *ptr;
    int len = strlen(str);

    for(int i=0; i<len/2; i++)
    {
        if(str[i] != str[len-i-1])
        {
            result = 1;
            break;
        }
    }

    return result;
}

int main()
{
  int result=0;
  char line1[] = "radar";
  char line2[] = "motion";
  char *results[] = {"YES", "NO"};

  int len1 = strlen(line1);
  int len2 = strlen(line2);

  result = scanString(line1);
  printf("Current Word: %s\n", line1);
  printf("Palindrome:  %s\n", results[result]);

  result = scanString(line2);
  printf("Current Word: %s\n", line2);
  printf("Palindrome:  %s\n", results[result]);

  return 0;
}
```

清单 6.6 包含 C 函数 `scanString`，其中的循环从值 0 开始，最终值为 `len /2`，即字符串 `str` 中元素数量的一半。该循环逐步从左向右移动，将当前位置的字符内容与字符串 `line1` 的“另一端”对应字符进行比较。

例如，数字 1234321 会将左侧数字 1 与该数字右侧对应位置的数字（也是 1）进行比较。接下来，左侧数字 2 与右侧数字 2 匹配，然后比较左侧数字 3 与其右侧对应数字。中间数字没有对应位置，这意味着我们已经验证数字 1234321 实际上是一个回文。

按照上一段描述的相同过程，字符串“rotor”和“radar”是回文，但数字 12345321 不是回文（它缺少对应的数字 4）。

编译清单 6.6 中的代码并运行可执行文件 `Palindromes1`，你将看到以下输出：

```text
Current Word: radar
Palindrome: YES
Current Word: motion
Palindrome: NO
```

## 指针、循环与数字的因数

清单 6.7 包含一个 while 循环、条件逻辑以及 %（取模）运算符，用于找出任何大于 1 的整数的因数。

### 清单 6.7：Divisors2.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    char *primes, prime[20];
    int div=2, num=12;

    printf("Number: %d\n", num);

    while(num > 1)
    {
        if(num % div == 0)
        {
            // convert number to string
            sprintf(prime, "%d", div);

            // append string to main string
            asprintf(&primes, "%s %s", primes, prime);

            num /= div;
        }
        else
        {
            ++div;
        }
    }

    printf("Divisors: %s\n", primes);

    return 0;
}
```

[清单 6.7](#) 与 [清单 6.6](#) 之间的主要区别在于，前者在 *while 循环* 中构造变量 divList（它是某个数的因数的串联列表），然后在 *while 循环* 完成时返回 divList 的值。[清单 6.7](#) 的输出如下：

```text
Number: 12
Divisors: (null) 2 2 3
```

请记住，`asprintf()` 函数最近才在《动态内存技术报告》中标准化，并不属于 C 标准本身。只有当编译器定义了 `__STDC_ALLOC_LIB__`，并且用户在包含 string.h 之前将 `__STDC_WANT_LIB_EXT2__` 定义为 1 时，此函数才可用。

## 指针与数字数组

清单 6.8 展示了 PointersArrayNums1.c 的内容，说明如何初始化字符串和指针。

### 清单 6.8：PointersArrayNums1.c

```c
#include <stdio.h>

int main()
{
 int numbers[] = {1,2,3,4,5};
 int *ptr1 = numbers;
 int size1 = sizeof(numbers)/sizeof(int);

 for(int i=0; i<size1; i++)
 {
 printf("%d\n", *(ptr1+i));
 }

 //see what happens when you use these invalid lines:
 //for(int ptr1=numbers; ptr1 != NULL; ptr1++)
 //for(int *ptr1=&numbers[0]; *ptr1 != '\0'; ptr1++)
 //for(int *ptr1=&numbers[0]; *ptr1; ptr1++)

 return 0;
}
```

清单 6.8 很直接：main() 函数用五个整数值初始化数组 numbers，然后将指针 ptr1 初始化为 numbers 数组的位置。

main() 方法的下一部分包含一个循环，该循环遍历 numbers 数组中的值并打印这些值。运行清单 6.8 中代码后的输出如下：

```text
1
2
3
4
5
```

## 指针数组

清单 6.9 展示了 `ArrayOfPointers.c` 的内容，说明如何初始化指针数组。

### 清单 6.9：ArrayOfPointers.c

```c
#include <stdio.h>

int main()
{
    int a=100, b=-200, c=500;
    int *p[3];

    p[0]= &a;
    p[1]= &b;
    p[2]= &c;

    printf("Initial a: %d b: %d c: %d\n",*p[0],*p[1],*p[2]);

    *p[0] += 100;
    *p[1] += 200;
    *p[2] += 300;

    printf("Updated a: %d b: %d c: %d\n",*p[0],*p[1],*p[2]);

    return 0;
}
```

**清单 6.9** 分别用值 100、-200 和 500 初始化三个整型变量 a、b 和 c。接下来的代码片段是大小为 3 的指针数组 p 的声明。元素 p[0]、p[1] 和 p[2] 分别用变量 a、b 和 c 的地址初始化。

接下来，位置 p[0]、p[1] 和 p[2] 分别增加 100、200 和 300，然后 printf() 语句显示它们的值。运行清单 6.9 中代码后的输出如下：

```text
Initial a: 100 b: -200 c: 500
Updated a: 200 b: 0 c: 800
```

## 指针与函数

本节包含一个示例，说明如何将基于指针的变量传递给函数以修改变量的值。请注意，本章后面会展示一个指向函数的指针的示例（它不同于本节中的概念）。

清单 6.10 展示了 PointersAndFunctions1.c 的内容，说明如何初始化字符串和指针。

### 清单 6.10：PointersAndFunctions1.c

```c
#include <stdio.h>

void test(int *num)
{
    *num += 6;
    printf("num inside test: %d\n", *num);
}

int main()
{
    int num = 7;

    printf("num before test: %d\n", num);

    test(&num);

    printf("num after test: %d\n", num);

    return 0;
}
```

[清单 6.10](#) 包含函数 `test()`，该函数将其基于指针的参数增加 6，然后显示新值。`main()` 函数用值 7 初始化变量 `num`，然后在调用函数 `test()` 之前和之后分别显示 `num` 的值。运行 [清单 6.10](#) 中代码后的输出如下：

```text
num before test: 7
num inside test: 13
num after test: 13
```

## 指针与小数数组

[清单 6.11](#) 展示了 PointersDecimals1.c 的内容，说明如何初始化字符串和指针。

### 清单 6.11：PointersDecimals1.c

```c
#include <stdio.h>

int main()
{
    int ints1[] = {1.0,2.0,3.0,4.0,5.0};
    int *ptr1 = ints1;
    int isize1 = sizeof(ints1)/sizeof(int);
```


int floats1[] = {1.0,2.0,3.0,4.0,5.0};
float *ptr2 = floats1;
int fsize1 = sizeof(floats1)/sizeof(float);

double doubles1[] = {1.0,2.0,3.0,4.0,5.0};
double *ptr3 = doubles1;
int dsize1 = sizeof(doubles1)/sizeof(double);

printf("The ints1 array:\n");
for(int i=0; i<isize1; i++)
{
    printf("%d ", *(ptr1+i));
}
printf("\n");

for(int i=0; i<isize1; i++)
{
    printf("%f ", *(ptr1+i));
}
printf("\n");

printf("The floats1 array:\n");
for(int i=0; i<fsize1; i++)
{
    printf("%d ", *(ptr2+i));
}
printf("\n");

for(int i=0; i<fsize1; i++)
{
    printf("%f ", *(ptr2+i));
}
printf("\n");

printf("The doubles1 array:\n");
for(int i=0; i<dsize1; i++)
{
    printf("%d ", *(ptr3+i));
}
}
    printf("\n");

    for(int i=0; i<dsize1; i++)
    {
        printf("%f ", *(ptr3+i));
    }
    printf("\n");

    return 0;
}
```
清单 6.11 包含三个数组 `ints1`、`floats1` 和 `doubles1`，它们包含同一组十进制值，以及分别“指向”这些数组的指针 `ptr1`、`ptr2` 和 `ptr3`。清单 6.11 的下一部分包含三“对” `for` 循环，每一对都显示其中一个数组的内容。例如，第一对循环以两种方式显示 `ints1` 数组的内容：第一个循环包含一个使用 `%d` 格式的 `printf()` 语句，第二个循环使用一个使用 `%f` 格式的 `printf()` 语句。

仔细观察三个数组的声明以及数组中值的打印方式：结果与你的预测一致吗？运行清单 6.11 中的代码后，输出如下：

```
The ints1 array:
1 2 3 4 5
0.000000 0.000000 0.000000 0.000000 0.000000
The floats1 array:
1 2 3 4 5
0.000000 0.000000 0.000000 0.000000 0.000000
The doubles1 array:
1 2 3 4 5
1.000000 2.000000 3.000000 4.000000 5.000000
```

## “反转”数字数组

本节中用于“反转”数字数组的代码示例由于一个故意设置的错误而无法工作（你能找到这个错误并修复它吗？）。清单 6.12 显示了 ReverseArrayNums1.c 的内容，该程序似乎使用指针来反转数字数组。

### 清单 6.12：ReverseArrayNums1.c

```
#include <stdio.h>

int main()
{
    // int array with 6 elements
    int arr1[6] = {1,2,3,4,5,6};
    int *ptr1, count=6;

    printf("Initial: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ",arr1[i]);
    }
    printf("\n");

    for(int i=0; i<count/2; i++)
    {
        ptr1 = &arr1[i];
        printf("ptr = %d ", *ptr1);

        arr1[i] = arr1[count-i-1];
        printf("left = %d ", arr1[i]);

        arr1[count-i-1] = *ptr1;
        printf("right = %d\n", *ptr1);
    }
```

```
printf("Reversed: ");
for(int i=0; i<count; i++)
{
    printf("%d ",arr1[i]);
}
printf("\n");

return 0;
}
```

清单 6.12 包含一个 main() 函数，它用一组整数初始化数组 arr1，然后声明整数指针 ptr1 和整数 count（其初始值为 6）。

main() 函数的下一部分包含一个循环，它遍历数组 arr1 的元素并显示这些元素的值。第二个循环遍历数组 arr1 的前半部分，并将每个元素与数组 arr1 右半部分中对应的元素“交换”。

该逻辑与检查回文的代码非常相似，代码使用指针 ptr1 作为临时存储位置，以交换两个值。

如代码所示，元素 arr1[i] 的“对应元素”是 arr1[count-i-1]。最后一个循环遍历数组 arr1 的元素（这些元素已被反转）。运行清单 6.12 中的代码得到的输出如下：

```
Initial: 1 2 3 4 5 6
ptr = 1 left = 6 right = 6
ptr = 2 left = 5 right = 5
ptr = 3 left = 4 right = 4
Reversed: 6 5 4 4 5 6
```

清单 6.12 中的循环尝试通过执行以下代码序列来交换：a = b; b = a; a = b; 这显然不会执行交换：它只是将 b 赋值给 a。解决方案是执行一次*正确*的交换。这个代码示例的目的是向你展示编写看起来正确但存在错误的 C 代码是多么容易。

## C 语言中的内存分配函数

C 编程语言支持多个函数，使你能够在 C 程序中动态分配（和释放）内存：

- malloc()
- calloc()
- realloc()
- free()

malloc() 函数在 C 程序中分配一块内存，这在定义自定义结构体时非常有用（如第 6 章所述）。

calloc() 函数分配一块内存（就像 malloc() 函数一样），并将分配的内存初始化为零。

realloc() 函数调整由 malloc() 或 calloc() 分配的内存块的大小。如果内存块之后有足够的空间，或者内存块正在缩小，则可能可以就地重新分配。如果内存块需要在新的位置重新分配，现有数据将被复制到新块，旧块将被释放。

free() 函数的目的相反：它释放由 malloc()、calloc()、realloc() 函数分配的内存。在动态分配内存后未能调用 free() 函数会导致内存泄漏。

使用 `malloc()` 函数复制字符串，并使用 `strncpy()` 函数指定要复制的字符数，或者使用 `strdup()` 函数在一次操作中分配内存并复制整个字符串。

接下来的几节包含代码示例，说明如何在 C 中动态分配内存。

## C 内置的 malloc() 函数

清单 6.13 显示了 CopyFunction2.c 的内容，说明如何使用 malloc() 函数和 strncpy() 函数。

### 清单 6.13：CopyFunction2.c

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
   char *src = "This is one line of text";
   char *dest;
   int len;
   len = strlen(src);

   dest = (char *)malloc(sizeof(src));

   // fill up 'dest'
   strncpy(dest, src, len);

   // not required because 'strncpy' adds a null terminator:
   //dest[len-1] = '\0';
```

而从未释放该内存，那么就会出现通常所说的“内存泄漏”。

## 锯齿数组

本节包含一个 C 程序，说明如何使用锯齿数组，即包含不同长度元素的数组。例如，你可以定义一个名字数组，其中每个名字都是不同长度的字符串。

清单 6.14 显示了 JaggedArray1.c 的内容，向你展示如何计算多维数组中各项的和。

```
**清单 6.14：JaggedArray1.c**

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
   int rowLengths[] = {6,4,3,5};
   int *jagged[4];

   for (int i = 0; i < 4; ++i)
   {
      jagged[i] = (int *)malloc(sizeof(int) * rowLengths[i]);
   }

   for (int i=0; i<4; ++i)
   {
      for (int j=0; j<rowLengths[i]; ++j)
      {
         jagged[i][j] = i + j + i*i;
         printf("element (%d,%d) = %d\n", i, j, jagged[i][j]);
      }
```
```

```
}
}
```

清单 6.14 用 4 行的长度初始化整数数组 `rowLengths`。接下来，变量 `jagged` 被声明为指向包含 4 个整数值指针的数组的指针。

第一个循环遍历 `jagged` 的 4 行，并使用内置的 C 函数 `malloc()` 为 `rowLengths` 数组中指定的整数数量分配内存。例如，`jagged[0]` 被初始化为指向 6 个整数的指针，而 `jagged[1]` 被初始化为指向 4 个整数的指针。

第二个循环是一个嵌套循环，它将位置 (i,j) 处的“单元格”的值初始化为 i + j + i*j，然后立即通过 `printf()` 函数显示该值。运行清单 6.14 中的代码，你将看到以下输出：

```
element (0,0) = 0
element (0,1) = 1
element (0,2) = 2
element (0,3) = 3
element (0,4) = 4
element (0,5) = 5
element (1,0) = 1
element (1,1) = 3
element (1,2) = 5
element (1,3) = 7
element (2,0) = 2
element (2,1) = 5
element (2,2) = 8
element (3,0) = 3
element (3,1) = 7
element (3,2) = 11
element (3,3) = 15
element (3,4) = 19
```




## 用户输入、指针、MALLOC() 和 FREE()

清单 6.15 展示了 `PointersToNumbers1.c` 的内容，它说明了如何打印一个简单字符数组中元素的值（及其地址）。

### 清单 6.15：MallocFree.c

```c
#include <stdlib.h>
#include <stdio.h>

int main()
{
    int size=-1, i;
    int* array;

    do {
        printf("Enter a positive integer: ");
        scanf("%d", &size);
    } while (size <= 0);

    array = (int *)malloc(sizeof(int) * size);

    if (array == NULL) {
        printf("An error creating the dynamic array has occurred.\n");
        return -1;
    }

    for (i = 0; i < size; i++) {
        array[i] = 1;
        printf("array[%d] has been assigned value 1.\n", i);
    }

    free(array);

    return 0;
}
```

清单 6.15 是另一个简单直接的代码示例：它首先初始化一个指向名为 array 的整数数组的指针，接着是一个 do-while 循环，提示用户输入一个正整数（并且只有在输入这样的值时才退出循环）。

代码的下一部分调用内置 C 函数 malloc()，以分配一块长度等于所输入正整数的内存。在确保内存分配成功后，一个循环将名为 array 的数组中的所有元素值初始化为 1。代码的最后一部分调用内置 C 函数 free()，以释放先前分配的内存。

运行清单 6.15 中代码后，此类输出示例如下：

```text
Enter a positive integer: -3
Enter a positive integer: 5
array[0] has been assigned value 1.
array[1] has been assigned value 1.
array[2] has been assigned value 1.
array[3] has been assigned value 1.
array[4] has been assigned value 1.
```

请注意，如果你想让代码更加健壮，就需要额外的代码来禁止非整数小数值、字母和特殊字符。

还有一点。如果变量 size 未初始化，那么当用户输入无效输入时，do/while 循环会出现未定义行为。如果我们用值 -1 初始化变量 size（在清单 6.15 中以粗体显示），这种未定义行为就会被消除。

### 堆与栈

堆和栈可用于在 C 程序中分配内存，并且它们的处理方式略有不同。

前几章代码示例中所有变量的内存分配都在栈上。操作系统执行内存分配，你无需担心释放该内存。另一方面，通过某个与 `malloc` 相关的函数在堆上分配的内存必须显式释放（否则就会发生内存泄漏）。

函数参数和局部变量从栈中分配内存；任何在栈上分配的内容都会在相关函数执行完毕时自动释放。

### C 语言中的大写和小写字符串

`toupper()` 和 `tolower()` 函数分别将字母转换为大写和小写。清单 6.16 展示了 `UpperLowerCase.c` 的内容，它说明了如何将字符转换为大写和小写字母。

### 清单 6.16：UpperLowerCase.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char *src = "This Is A Line";
    char *lower, *upper, *chr;
    int len;
    len = strlen(src);

    lower = (char *)malloc(sizeof(src));
    strncpy(lower, src, len);
    lower[len-1] = '\0';

    upper = (char *)malloc(sizeof(src));
    strncpy(upper, src, len);

    for(int i=0; i<len; i++)
    {
        *(lower+i) = tolower(src[i]);
        *(upper+i) = toupper(src[i]);
    }

    printf("Original: %s\n", src);
    printf("Upper:    %s\n", upper);
    printf("Lower:    %s\n", lower);
}
```

**清单 6.16** 将一个字符串变量 `src` 赋值为硬编码字符串，并声明字符指针 `lower`、`upper` 和 `chr`。

字符指针 `lower` 和 `upper` 通过 `malloc()` 方法被分配到一个动态分配内存块的内存位置，随后硬编码字符串被复制（通过 `strncpy()` 函数）到变量 `lower` 和 `upper` 的位置。正如你在前面的示例中所见，`strncpy()` 函数会自动以空字符终止这两个指针。

代码的下一部分是一个循环，从 0 迭代到 `len`，并通过内置 C 函数 `tolower()` 和 `toupper()` 分别将 `lower` 指针和 `upper` 指针中的字符转换为小写和大写。代码的最后一部分显示由 `src`、`lower` 和 `upper` 指向的字符串。

还有一个细节：本章中的许多代码示例使用语法 *(lower+i)，但你也可以使用更符合习惯的语法 lower[i]。清单 6.16 的输出如下：

```text
Original: This Is A Line
Upper:    THIS IS A LINE
Lower:    this is a line
```

### 反转字符串

本章前面你已经看到一个反转数组整数元素的示例，本节将展示如何反转字符串。清单 6.17 展示了 ReverseString1.c 的内容，它说明了如何反转动态分配内存块中的硬编码字符串。

### 清单 6.17：ReverseString1.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
  char *ptr1 = "this is a string";
  char *ptr2;
  int len=strlen(ptr1);

  ptr2 = (char *)malloc(len);

  for(int i=0; i<len; i++)
  {
    *(ptr2+len-1-i) = *(ptr1+i);
  }

    printf("Original: %s\n", ptr1);
    printf("Reverse: %s\n", ptr2);
}
```

清单 6.17 包含一个 main() 函数，它将字符指针 `ptr1` 初始化为硬编码字符串，并声明字符指针 `ptr2`。`ptr1` 处字符串的长度被赋给整数变量 `len`，而 `ptr2` 被赋值为一块内存的地址，其长度与 `ptr1` 位置处的字符串一样长。

代码的下一部分是一个循环，遍历 `ptr1` 位置处字符串的字符。在每次从左到右遍历字符串 `ptr1` 的过程中，`ptr2` “远端”的位置会被赋值为从左到右遍历 `ptr1` 中字符所得的值。如果你仔细阅读代码，就能看出 `ptr2` 中的字符是 `ptr1` 中字符的逆序。清单 6.17 的输出如下：

```text
Original: this is a string
Reverse: gnirts a si siht
```

### 查找大写和小写字母

清单 6.18 展示了 UpperAndLowerCount.c 的内容，它说明了如何从一个文本字符串构造仅含大写字母和仅含小写字母的字符串。这段代码有一个微妙的错误（你能找到它吗？），会在代码清单之后的讨论中解释。

### 清单 6.18：UpperAndLowerCount.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char str1[] = "This is a String";
    char *lower1, *upper1;
    int lcount=0, ucount=0;

    int len1 = strlen(str1);
    lower1 = (char *)malloc(len1);
    upper1 = (char *)malloc(len1);

    for(int i=0; i<len1; i++)
    {
        if(str1[i] == tolower(str1[i]))
        {
            *(lower1+lcount) = str1[i];
            lcount++;
        }
        else if(str1[i] == toupper(str1[i]))
        {
            *(upper1+ucount) = str1[i];
            ucount++;
        }
    }

/*
    // correct code:
    if(islower(str1[i]))
    {
        *(lower1+lcount) = str1[i];
        lcount++;
    }
    else if(isupper(str1[i]))
    {
        *(upper1+ucount) = str1[i];
        ucount++;
    }
*/

    *(lower1+lcount) = '\0';
    *(upper1+ucount) = '\0';

    printf("Original: %s\n",str1);
    printf("Lowercase: %s\n",lower1);
    printf("Uppercase: %s\n",upper1);

    return 0;
}
```

清单 6.18 与前面使用内置 C 函数 `malloc()` 的代码示例类似，这里该函数为字符指针 `lower1` 和 `upper1` 动态分配内存。一个循环遍历字符数组 `str1` 中的字母，并使用条件逻辑检查当前字母是小写还是大写（第三种情况是任何其他可打印字符，在此代码示例中被忽略）。在前一种情况下，当前字符被“追加”到小写字母列表中；在后一种情况下，当前字符被“追加”到大写字母列表中。

在为新构造的字符串添加空字符终止后，三个 `printf()` 语句显示 `str1`、`lower1` 和 `upper1` 的值。启动 `UpperAndLower` 后的输出如下：

```text
Original: This is a String
Lowercase: his is a tring
Uppercase: TS
```

清单 6.18 中的条件逻辑看起来是正确的；然而，这种逻辑会将空格和标点符号视为小写或大写，而这两者都不会改变

当它们被传递给 tolower() 或 toupper() 函数时。幸运的是，解决方案很简单：使用 if(islower(str1[i])) 和 if(isupper(str1[i])) 分别判断字母是小写还是大写。这个解决方案也比不正确的代码更清晰。

## 从字符串中移除空白字符

清单 6.19 展示了 RemoveWhiteSpaces.c 的内容，说明如何从字符串中移除空白字符。

### 清单 6.19：RemoveWhiteSpaces.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char str1[] = "This is a String";
    char *ptr1;
    int count=0;

    int len1 = strlen(str1);
    ptr1 = (char *)malloc(len1);

    for(int i=0; i<len1; i++)
    {
        if((str1[i] == ' ') || (str1[i] == '\t'))
        {
            continue;
        }
        else
        {
            *(ptr1+count) = str1[i];
            count++;
        }
    }

    *(ptr1+count) = '\0';

    printf("Original: %s\n",str1);
    printf("Stripped: %s\n",ptr1);

    return 0;
}
```

清单 6.19 首先初始化字符数组 str1 并声明字符指针 ptr1。接下来，一个循环遍历字符数组 str1 中的字符，如果任何字符不是空白字符（空格或制表符），则将该字符“追加”到非空白字符列表中。

请注意，变量 i 是循环中的索引变量，而变量 count 记录非空白字符的数量，并且在循环迭代的任意时刻都等于此类字符的数量。编译并启动清单 6.19 中的代码后的输出如下：

```
Original: This is a String
Stripped: ThisisaString
```

## 指针、字符串和字符计数

C 不提供对哈希表等结构的支持，这意味着你必须提供自己的实现，或使用第三方实现（如果第三方实现成熟稳定，则更可取）。

一种折中方案是创建一个数组来记录给定字符串中的不同字符，并创建另一个数组来记录每个字符在该字符串中出现的次数。如果要跟踪大写和小写字母，第一个数组的长度应为 52；如果要容纳标点和特殊字符，则需要一个大小约为 100 的数组。请记住，对于某些其他语言，这个数字会增加，而对于诸如汉字这样的书写系统，这是不切实际的。

请注意，前述场景并不构成哈希表：对于任何字符，哈希表的“查找时间”为 O(1)，而数组的查找时间为 O(n)，其中 n 是数组中的元素数量。注意，上一句中的“查找时间”是指在未排序数组中查找元素所需的时间。如果在数组中执行线性搜索，查找一个元素所需的预期搜索次数为 n/2，而后者是 O(n)。

然而，如果将较大文档（100K 及以上）中的唯一字符存储在一个数组中，并将它们的频率存储在另一个数组中，那么查找时间不会大于文档所用语言中存在的字符数量。

清单 6.20 展示了 CharCounts.c 的内容，说明如何初始化字符串和指针。

### 清单 6.20：CharCounts.c

```c
#include <stdio.h>
#include <stdio.h>
#include <stdlib.h>

        ++counts[k];
//printf("count for %c at pos %d : %d\n", ch, k, counts[k]);
        foundchar = 1;
        break;
    }
}

    if(foundchar == 0)
    {
//printf("inserting char %c at pos: %d\n", ch, pos);
        counts[pos] = 1;
        chars[pos] = ch;
        ++pos;
    }
}

    printf("Full string: %s\n",str1);

    char ch2;
    int count;
    for(int k=0; k<pos; k++)
    {
        printf("char %c count %d at array position: %d\n",
            chars[k], counts[k], k);
    }

    return 0;
}
```

**清单 6.20** 有一个 `main()` 函数，它初始化字符串 `str1`，然后使用 C 内置函数 `malloc()` 为字符指针 `chars` 和整数指针 `counts` 动态分配内存。

然后，一个简单循环将 `chars` 的所有条目初始化为一个空格（`' '`），并将 `counts` 的所有条目初始化为 0。代码的中间部分包含一个大型 `for` 循环，用于统计原始字符串 `str1` 中唯一字符的数量。在每次循环迭代中，内部循环检查当前字符是否已经被检测到；如果是，则递增该字符在 counts 数组中的位置值。如果不是，则将当前字符追加到 chars 数组，并将其在 counts 数组中的对应值设为 1。

清单 6.20 中的最后一个代码块遍历 chars 数组并打印每个元素及其计数（计数存储在 counts 数组中）。编译并启动清单 6.20 中的代码后的输出如下：

```
Full string: This is a string with some short words that wraps around and let's see how well the code in this code sample actually works!
```

```
char T count 1 at array position: 0
char h count 7 at array position: 1
char i count 6 at array position: 2
char s count 12 at array position: 3
char   count 23 at array position: 4
char a count 8 at array position: 5
char t count 9 at array position: 6
char r count 6 at array position: 7
char n count 4 at array position: 8
char g count 1 at array position: 9
char w count 6 at array position: 10
char o count 8 at array position: 11
char m count 2 at array position: 12
char e count 9 at array position: 13
char d count 5 at array position: 14
char p count 2 at array position: 15
char u count 2 at array position: 16
char l count 6 at array position: 17
char ' count 1 at array position: 18
char c count 3 at array position: 19
char y count 1 at array position: 20
char k count 1 at array position: 21
char ! count 1 at array position: 22
```

## 指向 void 类型函数的指针

清单 6.21 展示了 PointersToVoidFunctions1.c 的内容，说明如何定义两个简单函数以及一个函数指针，以便“指向”这些函数并执行它们。

### 清单 6.21：PointersToVoidFunctions1.c

```c
#include <stdio.h>

void one()
{
    printf("Inside function one\n");
}

void two()
{
    printf("Inside function two\n");
}

int main()
{
    void (*ptr1)();

    one();
    ptr1 = &one;
    (*ptr1)();
    //ptr1 = one;
    //ptr1();

    two();
    ptr1 = &two;
    (*ptr1)();
}
```

## 指向非 void 函数的指针

上一节向您展示了如何调用指向返回类型为 void 的函数的函数指针。清单 6.22 展示了自定义函数 PointersToNonVoidFunctions.c 的内容，说明如何调用指向返回类型为非 void 的函数的函数指针。

### 清单 6.22：PointersToNonVoidFunctions1.c

```c
#include <stdio.h>

int add(int x, int y)
{
    printf("Inside add\n");
    return (x+y);
}

int multiply(int x, int y, int z)
{
    printf("Inside multiply\n");
    return (x*y*z);
}

int main()
{
    int result, x=3, y=4, z=5;

    int (*ptr1)(int, int);
    int (*ptr2)(int, int, int);

    result = add(x,y);
    printf("Result1:  %d\n", result);

    ptr1 = &add;
    result = (*ptr1)(x,y);
    printf("Result2: %d\n", result);
    printf("----------\n");

    result = multiply(x,y,z);
    printf("Result3: %d\n", result);

    ptr2 = &multiply;
    result = (*ptr2)(x,y,z);
    printf("Result4: %d\n", result);
}
```

清单 6.22 首先定义函数 add()，它返回两个整数之和；接着定义函数 multiply()，它返回三个整数之积。

清单 6.22 的下一部分包含一个 main() 函数，其中包含函数指针 ptr1 和 ptr2 的两个原型，如下所示：

```
int (*ptr1)(int, int);
int (*ptr2)(int, int, int);
```

接下来，整型变量 result 用执行函数 add() 返回的值初始化，然后显示该结果。现在，函数指针 ptr1 用函数 add() 的地址初始化，当执行 ptr1（使用相同参数）时，结果与前面的输出相同。

下一代码块与上一节类似，但 result 和 ptr2“指向”函数 multiply()。启动清单 6.22 中的代码后的输出如下：

```
Inside add
Result1: 7
Inside add
```



```
Result2:  7
-----------
Inside multiply
Result3:  60
Inside multiply
Result4:  60
```

### 作为参数的函数指针

另一个函数指针的用途是将其指定为函数的参数。列表 6.23 显示了 FunctionPointersAsArgs.c 的内容，该内容说明了如何将指向函数的指针定义为另一个函数的参数。

**列表 6.23：FunctionPointersAsArgs.c**

```c
#include <stdio.h>

void squaredValues(int startValue, int endValue, int (*fp) (int))
{
    printf("Calculating Squared Values\n");
    printf("--------------------------\n");
    for(int x=startValue; x<=endValue; x++)
    {
        printf("%2d   %3d\n", x, (*fp)(x));
    }
    printf("\n");
}

int square(int x) {
    return x*x;
}

void cubedValues(int startValue, int endValue, int (*fp) (int))
{
    printf("Calculating Cubed Values\n");
    printf("--------------------------\n");
    for(int x=startValue; x<endValue; x++)
    {
        printf("%2d  %3d\n", x, (*fp)(x));
    }
}

int cube(int x) {
    return x*x*x;
}

int main()
{
    squaredValues(1, 10, square);
    cubedValues(1, 10, cube);

    return 0;
}
```

列表 6.23 首先定义了 squaredValues() 和 cubedValues() 函数，两者返回类型均为 void，具有两个整数值参数，以及第三个参数为返回类型为 void 的函数指针。此外，还定义了 square() 和 cube() 函数，两者的返回类型均为 int。

列表 6.23 的下一部分包含 main() 函数，其中第一行代码调用 squaredValues() 函数，如下所示：

```c
squaredValues(1, 10, square);
```

列表 6.23 的下一部分调用 cubedValues() 函数，如下所示：

```c
cubedValues(1, 10, cube);
```

如你所见，前两个代码片段分别将函数 square() 和 cube() 指定为其第三个参数。将此代码与之前传递函数指针而不是实际函数名的代码示例进行对比。启动列表 6.23 中的代码的输出如下：

```
Calculating Squared Values
--------------------------
1  1
2  4
3  9
4  16
5  25
6  36
7  49
8  64
9  81

```

```
Calculating Cubed Values
--------------------------
1  1
2  8
3  27
4  64
5  125
6  216
7  343
8  512
9  729
```

如果你宁愿避免使用函数指针，1) 将函数数组定义为函数查找表，或 2) 在 switch 语句内部使用 case 语句。

### 指向指针的指针

在第 5 章中，你了解到可以在 C 程序中定义指向指针的指针，现在我们将来看一个这样的例子。列表 6.24 显示了 PointersToPointers.c 的内容，说明了如何使用指向指针的指针。

**列表 6.24：PointersToPointers.c**

```c
#include <stdio.h>

int main()
{
    char *list[] = {"a", "b", "c", "d", NULL};

    for (char **ptr=list; *ptr != NULL; ptr++){
        printf("array item: %s\n", ptr[0]);
    }

    return 0;
}
```

列表 6.24 定义了一个字符指针 list，其初始化为字母表的最初四个字母。接下来，一个循环遍历字符指针列表的元素，使用字符指针 `ptr`，采用“双星号”语法，表示指向地址的指针的指针。启动列表 6.24 中的代码的输出如下：

```
array item: a
array item: b
array item: c
array item: d
```

### 摘要

本章介绍了 C 中指针的更多示例，以及指向数字、数组和字符串的指针的示例。你看到了如何使用指针来分割字符串、检查回文，以及使用指针查找数字除数的循环。接下来，你学习了如何定义指向数字数组的指针。

然后你看到了如何使用指针来反转字符串，如何查找大写和小写字母，以及如何从字符串中删除空白。然后你看到了如何统计一行文本中的单词数，如何定义指向函数的指针，以及函数指针作为参数。最后，你学习了如何定义指向指针的指针以及如何处理命令行参数。

## 第 7 章：杂项主题

本章包含多种主题，其中一些比前几章涵盖的主题更复杂。如果你是绝对的初学者，那么最好将本章主题的深入研究推迟（至少现在）。然而，值得对其内容进行粗略浏览，以防其中有与你的需求相关的 C 特性的代码示例。无论如何，本章的大多数主题都是以高层次的方式讨论的；如果你成为一名全职 C 开发者，你可能会对这些主题更加熟悉。

本章的第一部分讨论 C 预处理器 `#define`、如何定义 C 宏以及 C 中的位级操作。如果你计划继续学习 C，这些主题很有用，你将在许多 C 程序中遇到它们。

本章的第二部分讨论 C `structs` 以及如何创建保存各种类型数据值的自定义结构。你还将看到代码示例，展示如何定义指向 C 结构体、嵌套 C 结构体以及 C 结构体数组的指针。本章的第三部分涵盖 C 特性，例如 C 联合体、联合体与结构体的组合，以及 C 中的位域。

第四部分提供了关于 C 中系统调用的一些基础信息，以及两个相关的代码示例。最后一部分讨论头文件，以及如何在 C 程序中定义和引用本地头文件。

### 符号常量

与 Java 等语言不同，C 支持 #define 关键字，使你能够定义符号名称或符号常量，通常是一个数字或字符串，其格式如下所示：

```c
#define MYNAME some_text_goes_here
```

例如，以下片段将数字分配给字符串 PI：

```c
#define PI 3.1415962
```

C 预处理器（它在 C 语言之外）使用文本替换，以便用前述代码片段中定义的值替换 C 程序中字符串 PI 的每次出现。

#define 的一个方便用途是表示转义序列的常量。例如，使用以下定义对于换行、回车和换页很方便，其八进制值分别为 012、015 和 014：

```c
#define LF '\012'
#define CR '\015'
#define FF '\014'
```

 alternatively，以下定义分别指定换行、回车和换页的十六进制值：

```c
#define LF '\x0A'
#define CR '\x0D'
#define FF '\x0C'
```

作为一般规则：只要 #define 语句能提高 C 程序的清晰度，就使用它们。

### 在 C 中使用宏

本章前面你学习了如何使用 #define 关键字来定义常量或字符串。你也可以使用 #define 关键字来定义所谓的宏，它们包含一段可执行的 C 代码。C 预处理器使用文本替换来用其对应定义替换每个宏的出现。

列表 7.1 显示了 SimpleMacro.c 的内容，说明了如何在 C 中定义宏。

**列表 7.1：SimpleMacro.c**

```c
#include <stdio.h>

#define add2(num1, num2) { \
    int total=0;      \
    sum = num1 + num2;  \
}

int main()
{
    int sum, num1=5, num2=8;
    add2(num1, num2);
    printf("num1 = %i num2 = %i sum = %i\n", num1, num2,
           sum);
    return 0;
}
```

列表 7.1 首先定义了宏 `add2`，它将两个数字相加并将变量 `sum` 设置为该值。注意 `num1` 和 `num2` 的类型未指定（这与具有参数的函数不同）。

`main()` 函数声明了 `sum`、`num1`（初始值为 5）和 `num2`（初始值为 8），然后调用 `add2` 宏。注意 `add2` 宏不返回 `sum` 的值（本例中为 13）。`sum` 的值在 `add2` 中分配，`main()` 函数中的 `sum` 值会更新为正确值。这种功能大致类似于按引用传递，只是变量 `sum` 并未传递给 `add2` 宏。启动列表 7.1 中的 C 程序的输出如下：

```
num1 = 5 num2 = 8 sum = 13
```

### C 中的其他运算符

C 支持超出你在前几章学到的各种运算符，包括：按位、逻辑、移位和逗号运算符。

C 中的按位运算符对于需要以非平凡方式处理单个位的操作任务很重要。示例包括从串行和并行端口读取以及向这些端口写入数据。

以下小节提供了按位、逻辑和逗号运算符的简要介绍，以及简单的代码示例。

#### 按位运算符



C 中的按位运算符是 `&`、`|`、`^`、`~`、`<<` 和 `>>`，它们分别对应二进制 AND、二进制 OR、二进制 XOR（eXclusive OR）、二进制按位取反（One's complement）、二进制左移和二进制右移。

以下示例说明如何计算两个二进制数的逻辑与：

```text
11001000
& 10111000
-------
= 10001000
```

以下示例说明如何计算两个二进制数的逻辑或：

```text
11001000
| 00001111
-------
= 11001111
```

如果需要使用其他按位运算符，请在线搜索包含这些运算符的代码示例。

## 逻辑运算符

C 中的逻辑运算符是 `&&` 和 `||`，分别表示逻辑与和逻辑或。你已经在 C 中看到过一个逻辑运算符的例子：第 2 章中涉及复合条件逻辑的代码示例。

## 逗号运算符

逗号运算符将两个表达式组合并按从左到右的顺序求值。整个表达式的值返回右侧的值。逗号运算符的示例如下：

```c
for (low=0, high=MAXSIZE; low < high; low=newlow, high=newhigh)
{
    // do something with low and high
}
```

## 累积代码示例

清单 7.2 显示了 BitOperations.c 的内容，说明如何对二进制数执行各种位操作。

### 清单 7.2: BitOperations.c

```c
#include <stdio.h>
int main()
{
    // binary literals are a non-standard extension
    int x1 = 0b11001000;
    int x2 = 0b10111000;
    int x3, x4, x5, x6;

    x3 = x1 & x2;
    x4 = x1 | x2;
    x5 = x1 ^ x2;
    x6 = (x1 << 2);

    printf("x1 = %x %d %o\n", x1, x1, x1);
    printf("x2 = %x %d %o\n", x2, x2, x2);
    printf("x3 = %x %d %o\n", x3, x3, x3);
    printf("x4 = %x %d %d\n", x4, x4, x4);
    printf("x5 = %x %d %o\n", x5, x5, x5);
    printf("x6 = %x %d %o\n", x6, x6, x6);

    return 0;
}
```

清单 7.2 包含一个 main() 函数，声明了整数变量 x3、x4、x5 和 x6。下一段代码使用运算符 `&`、`|`、`^` 和 `<<`（前面已讨论）为 x3、x4、x5 和 x6 初始化值。最后的代码块由六个 printf() 语句组成，用于以十六进制、十进制和八进制格式显示变量 x1 到 x6 的值。清单 7.2 的输出如下：

```text
x1 = c8 200 310
x2 = b8 184 270
x3 = 88 136 210
x4 = f8 248 248
x5 = 70 112 160
x6 = 320 800 1440
```

不幸的是，C 没有提供在 printf() 命令中显示二进制数的机制。然而，清单 7.3 显示了 ShowBits.c（借自维基百科）的内容，说明如何显示二进制数的位数。

### 清单 7.3: ShowBits.c

```c
#include <stdio.h>

void showbits(unsigned int x)
{
    int i;

    for(i=(sizeof(int)*8)-1; i>=0; i--)
    {
        (x&(1u<<i)) ? putchar('1'): putchar('0');
    }

    printf("\n");
}

int main()
{
    int j = 5225, m, n;
    printf("%d in binary \t\t ", j);
    showbits(j);

    // the loop for right shift operation
    for ( m = 0; m <= 5; m++ )
    {
      n = j >> m;
      printf("%d right shift %d gives ", j, m);
      showbits(n);
    }

    return 0;
}
```

清单 7.3 从函数 `showbits()` 开始，该函数包含一个循环，对无符号整数 1 执行逻辑左移。在每次移位操作期间，x 的值与当前左移值进行“与”操作：如果结果非零则显示整数 1，否则显示数字 0。

清单 7.3 的 `main()` 函数首先使用初始值为 5225 的变量 `j` 调用 `showbits()` 函数。`main()` 函数的下一部分是一个 `for` 循环，它使用变量 `n` 调用 `showbits()` 函数，`n` 对变量 `j` 进行逻辑右移。该循环执行六次，并在每次调用 `showbits()` 函数后显示输出。清单 7.3 的输出如下：

```text
5225 in binary       00000000000000000001010001101001
5225 right shift 0 gives 00000000000000000001010001101001
5225 right shift 1 gives 00000000000000000000101000110100
5225 right shift 2 gives 00000000000000000000010100011010
5225 right shift 3 gives 00000000000000000000001010001101
5225 right shift 4 gives 00000000000000000000000101000110
5225 right shift 5 gives 00000000000000000000000010100011
```

## 冒泡排序算法

冒泡排序是一种用于对数字数组进行排序的知名算法。该算法的复杂度为 `O(n^2)`，其中 n 为数组中的项目数。虽然本书不是关于 C 中的算法，但本节包含冒泡排序的 C 代码，以便你熟悉此类算法的 C 语法。

清单 7.4 显示了 BubbleSort.c 的内容，说明如何使用冒泡排序对整数数组进行排序。

### 清单 7.4: BubbleSort.c

```c
#include <stdio.h>

int main()
{
    int numbers[] = {5, 1, 2, 4, 3};
    int count = sizeof(numbers)/sizeof(numbers[0]);
    int temp;

    printf("Original: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ",numbers[i]);
    }
    printf("\n");

    for(int i=0; i<count-1; i++)
    {
        for(int j=i; j<count; j++)
        {
            if(numbers[i] > numbers[j])
            {
                temp = numbers[i];
                numbers[i] = numbers[j];
                numbers[j] = temp;
            }
        }
    }

    printf("Sorted: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ",numbers[i]);
    }
    printf("\n");

    return 0;
}
```

清单 7.4 是一个“经典”的排序算法，其代码结构已在前几章中介绍过。在定义整数数组后，main() 函数包含一个嵌套循环，其中内部循环具有条件逻辑来确定何时交换数组的两个元素。这种条件逻辑的结果是使较大的元素“冒泡”：即排序后的数组以最小的数字开头，以最大的数字结尾。清单 7.4 的输出如下：

```text
Original: 5 1 2 4 3
Sorted:  1 2 3 4 5
```

## 什么是 C 结构体？

C 结构体本质上是一个“结构”，它定义了一组逻辑相关项。可通过 C 结构体定义的逻辑相关项的简单示例包括：员工、学生、邮寄地址 等等。请记住，数据值可能从文件、数据库中访问，或通过 Web 服务检索。

此外，你可以在 C 程序中对 C 结构体执行以下操作：

- 创建 C 结构体数组
- 复制或赋值 C 结构体
- 使用 `&` 运算符与 C 结构体
- 将 C 结构体传递给函数
- 从函数返回 C 结构体

正如你在后续章节中会看到的，你甚至可以在另一个 C 结构体内部定义一个 C 结构体（如客户，其邮寄地址和送货地址作为单独的 C 结构体），以及 C 结构体数组（其中每个都可以代表一个以 C 结构体形式表示的员工）。

然而，请记住你不能比较两个 C 结构体：你必须通过自定义代码逐元素比较两个 C 结构体。

下一节将向你展示创建包含员工相关信息的简单 C 结构体的示例。

### C 结构体的一个示例

清单 7.5 显示了 EmployeeStruct1.c 的内容，说明如何为员工相关数据创建基本结构。员工的完整 C 结构体将包含许多其他字段，你可以将其添加到本代码示例中的 C 结构体中。

### 清单 7.5: EmployeeStruct1.c

```c
#include <stdio.h>
#include <string.h>

typedef struct Employee
{
  char fname[50];
  char lname[50];
  char title[100];
  int emp_id;
} emp;

int main()
{
  struct Employee emp1;

  strcpy( emp1.fname, "John");
  strcpy( emp1.lname, "Smith");
  strcpy( emp1.title, "Developer");
  emp1.emp_id = 2000;

  printf("First name: %s\n",emp1.fname);
  printf("Last name: %s\n",emp1.lname);
  printf("Title:    %s\n",emp1.title);
  printf("Employee id: %d\n",emp1.emp_id);
}
```

清单 7.5 非常直接，从自定义 C `struct` `Employee` 的定义开始，该结构体包含每个员工的姓名、姓氏、职称和员工 ID 字段。正如你所预期的那样，前三个字段是字符字符串，第四个字段具有整数值（但该字段也可以是字符字符串）。

`main()` 函数的下一部分使用内置 C 函数 `strcpy()` 为前三个基于字符的字段赋值，然后使用简单的赋值语句初始化整数值 `emp_id` 字段。

`main()` 函数的最后一部分包含 `printf()` 语句，用于显示字段中的值在

## Employee 结构体。

编译清单 7.5 中的代码并启动可执行文件，你将看到以下输出：

First name: John
Last name: Smith
Title:      Developer
Employee id: 2000

## 指向 C 结构体的指针

本节假设你已经阅读了[第 5 章]中与指针相关的章节；如果尚未阅读，请先阅读那些材料。

清单 7.6 展示了 PointerStructs.c 的内容，说明如何为与员工相关的数据创建结构体，以及指向此类结构体的指针（新代码以粗体显示）。

### 清单 7.6：EmployeeStructs.c

```
#include <stdio.h>
#include <string.h>

typedef struct Employee
{
   char fname [50];
   char lname [50];
   char title [100];
   int emp_id;
} emp;

int main()
{
   struct Employee emp1;

   strcpy( emp1.fname, "John");
```

```
strcpy( emp1.lname, "Smith");
strcpy( emp1.title, "Developer");
emp1.emp_id = 2000;
```

```
printf("First name: %s\n",emp1.fname);
printf("Last name: %s\n",emp1.lname);
printf("Title: %s\n",emp1.title);
printf("Employee id: %d\n",emp1.emp_id);
```

```
struct Employee * empptr = &emp1;
printf("\nPointer of Employee:\n");
printf("First name: %s\n",empptr->fname);
printf("Last name: %s\n",empptr->lname);
printf("Title: %s\n",empptr->title);
printf("Employee id: %d\n",empptr->emp_id);
}
```

清单 7.6 以你在清单 7.5 中看到的 Employee 结构体定义开头，并且还包括 main() 函数的前两部分。第三部分包含所有新代码，它初始化变量 empptr。如你所见，empptr 是 Employee 类型的指针，并用先前初始化的变量 emp1 的地址初始化（emp1 也是 Employee 类型的 C 结构体）。接下来，一组 printf() 语句使用变量 empptr 的“箭头语法”显示 Employee 结构体的内容。

编译清单 7.6 中的代码并启动可执行文件，你将看到以下输出：

First name: John
Last name: Smith
Title: Developer
Employee id: 2000

Pointer of Employee:
First name: John
Last name: Smith
Title: Developer
Employee id: 2000

## 嵌套 C 结构体

清单 7.7 展示了 `NestedStructures.c` 的内容，说明如何为与员工相关的数据定义一个包含另一个 C 结构体的 C 结构体。

### 清单 7.7：NestedStructures.c

```c
#include <stdio.h>
#include <string.h>

struct Address
{
    char street[50];
    char city[50];
};

struct Employee
{
    int id;
    char name[20];
    char title[20];
    struct Address address;
} emp;

int main()
{
    struct Employee emp =
    {1000, "John Smith", "Developer", "123 Main Street", "Chicago"};

    printf("Emp Id: %d \n",  emp.id);
    printf("Name:  %s \n",  emp.name);
    printf("Title: %s \n\n", emp.title);
```

清单 7.8 展示了 ArrayOfEmployees.c 的内容，说明如何用 C 结构体填充数组。

### 清单 7.8：ArrayOfEmployees.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Employee
{
   char  fname [50];
   char  lname [50];
   char  title [100];
   int   emp_id;
} emp;

int main()
{
   int empCount = 5;
   struct Employee emps[empCount];
   struct Employee *empPtr;

   char *fnames= {"John", "Jane", "Steve"};
   char *lnames[4] = {"Smith", "Jones",
                      "Edwards", "Anderson"};
   char *titles[4] = {"Sales", "Marketing",
                      "Development", "Support"};

   // initialize array of Employees
   for(int i=0; i<empCount; i++)
   {
      strcpy(emps[i].fname, fnames[i%3]);
      strcpy(emps[i].lname, lnames[i%4]);
      strcpy(emps[i].title, titles[i%4]);
      emps[i].emp_id = 1000*(i+1);
   }

   // print contents of all Employees
```

```
for(int i=0; i<empCount; i++)
{
    printf("First name: %s\n",emps[i].fname);
    printf("Last name:  %s\n",emps[i].lname);
    printf("Title:      %s\n",emps[i].title);
    printf("Employee id: %d\n",emps[i].emp_id);
    printf("\n");
}

// print contents of all Employees
for(int i=0; i<empCount; i++)
{
    empPtr = &emps[i];

    printf("First name: %s\n",empPtr->fname);
    printf("Last name:  %s\n",empPtr->lname);
    printf("Title:      %s\n",empPtr->title);
    printf("Employee id: %d\n",empPtr->emp_id);
    printf("\n");
}

}
```

清单 7.8 以（现在已熟悉的）Employee C 结构体定义开头，随后是一个较长但并没有你想象中那么复杂的 main() 函数。main() 函数的第一部分定义了一个包含四个 Employee 元素的数组 emps，随后是变量 empPtr，它是指向 Employee 类型变量的指针。下一部分初始化了名字、姓氏和头衔数组。

下一部分包含三个循环。第一个循环使用你在清单 7.6 中看到的代码，为 emps 数组元素的全部字段赋值。第二个循环使用“点”语法显示 Employee 元素的所有值，而第三个循环使用“箭头”语法（见清单 7.7）执行同样的任务。

编译清单 7.8 中的代码并启动可执行文件，你将看到以下输出：

First name: John
Last name: Smith
Title: Sales
Employee id: 1000

First name: Jane
Last name: Jones
Title: Marketing
Employee id: 2000

First name: Steve
Last name: Edwards
Title: Development
Employee id: 3000

First name: John
Last name: Anderson
Title: Support
Employee id: 4000
// 为简洁起见，省略了一些输出

## 用于日期的 STRFTIME() 和 STRPTIME() 函数（可选）

本节包含特定于日期的功能，比前面包含内置 C 函数的代码示例要复杂得多。如果你不打算在 C 程序中使用日期，可以放心跳过本节，这不会影响连续性（也可以以后某个时间再回到本节）。

在 C 中，你可以使用 strftime() 函数将日期和时间转换为字符串，也可以使用 strptime() 函数将字符串转换为格式化时间，二者均在清单 7.9 中说明。

### 清单 7.9：DateTimeString.c

```c
#include <stdio.h>
#include <locale.h>
#include <time.h>

int main()
{
    char buf[100];
    time_t t;
    struct tm *timeptr, result;

    setlocale(LC_ALL,"/QSYS.LIB/EN_US.LOCALE");

    t = time(NULL);

    timeptr = localtime(&t);
    strftime(buf,sizeof(buf), "%a %m/%d/%Y %r", timeptr);

    if(strptime(buf, "%a %m/%d/%Y %r",&result) == NULL)
    {
        printf("\nstrptime failed\n");
    }
    else
    {
        printf("tm_hour: %d\n",result.tm_hour);
        printf("tm_min: %d\n",result.tm_min);
        printf("tm_sec: %d\n",result.tm_sec);
        printf("tm_mon: %d\n",result.tm_mon);
        printf("tm_mday: %d\n",result.tm_mday);
        printf("tm_year: %d\n",result.tm_year);
        printf("tm_yday: %d\n",result.tm_yday);
        printf("tm_wday: %d\n",result.tm_wday);
    }
}
```

## C 中的单链表（可选）

如果你不熟悉链表，可以将本节视为可选内容，或许可以在学习链表之后再回到本节。

如你所见，上一节使用 C 结构体数组来跟踪员工。然而，如果你有数量未知的员工，可以用链表替代数组，以便动态地将每个新员工添加到链表中。

为了简化代码，该 C 结构体中唯一的数据值是一个表示员工 id 的整数字段。阅读完代码示例后，你可以随意修改该 C 结构体以包含其他相关字段。

清单 7.10 展示了 SLinkedList.c 的内容，说明如何在 C 中创建单链表，其中单链表中的每个元素都是一个 C 结构体，包含一个整数字段和一个指向员工元素的前向指针。该 C 结构体还包含一个“被注释掉的”、指向前一个 employee 的指针

字段，这是创建双向链表所必需的。

### 清单 7.10: SLinkedList.c

```c
#include <stdio.h>
#include <stdlib.h>

struct emp {
    int x;
    struct emp *next;
    //struct emp *prev;
};

int main()
{
    int empIdValues[] = {2000, 1000, 5000, 8000, 7500};
    int count = sizeof(empIdValues)/sizeof(empIdValues[0]);

    // the root emp is the first emp
    struct emp *root;

    // current emp and a new emp
    struct emp *currNode, *aNode;

    root = malloc( sizeof(struct emp) );
    root->x = empIdValues[0];
    root->next = NULL;
    currNode = root;

    for(int i=1; i<count; i++)
    {
        aNode = malloc( sizeof(struct emp) );
        aNode->x = empIdValues[i];
        aNode->next = NULL;
        currNode->next = aNode;
        currNode = aNode;
    }

    currNode = root;
    if(currNode != 0)
    {
        int idx = 1;
        while(currNode)
        {
            printf("Employee %d has id: %d\n", idx, currNode->x);
            currNode = currNode->next;
            ++idx;
        }
    }

    return 0;
}
```

清单 7.10 定义了一个 emp C 结构体，其中包含一个整数字段、一个名为 prev 的指向 emp 结构体的指针，以及一个名为 next 的指向 emp C 结构体的指针。该结构跟踪员工的 ID，以及指向前一个员工和下一个员工的指针（当它们存在时）。在实际应用中，数据字段会更广泛，但此示例包含最少的信息，因为这样更容易理解代码。启动清单 7.10 中的 C 程序的输出如下：

Employee 1 has id: 2000
Employee 2 has id: 1000
Employee 3 has id: 5000
Employee 4 has id: 8000
Employee 5 has id: 7500

如前所述，emp C 结构体的定义包含一个额外的名为 prev 的指针，它是指向前一个员工的指针（根节点除外）。因此，每个节点都有一个前一个指针和一个下一个指针，这就是双向链表。

## C 中的联合

如果你需要，你可以扩展 [清单 7.9](#) 中的代码以实现双向链表。如果你很有雄心，你可以修改 [清单 7.9](#) 中的代码以在 C 中创建其他数据结构，例如循环列表、栈、队列和树。

C 提供了 union 数据类型，使你能够在同一内存位置存储不同数据类型。尽管你可以定义一个包含多个成员的 C union，但一次只能有一个成员包含实际值。包含值的成员在程序执行期间可以反复更改，但在任何给定时间点，只有一个成员包含值。

以下示例展示了如何使用 C union 关键字定义 C union 数据类型：

```c
union MyData
{
    int i;
    float f;
    char str[10];
} myunion;
```

分配给 C union 的内存等于 union 中最大成员的大小。因此，MyData 类型需要 10 字节，因为 str 元素占用 10 字节。

[清单 7.11](#) 显示了 `Unions.c` 的内容，说明了如何构造一个包含整数、浮点值和字符字符串的 C union。

### 清单 7.11: Unions.c

```c
#include <stdio.h>
#include <string.h>

union MyData
{
    int i;
    float f;
    char str[10];
};

int main()
{
    union MyData mydata;

    printf("Memory allocated to mydata: %d\n",sizeof(mydata));

    return 0;
}
```

清单 7.11 定义了数据类型为 C union 的变量 Data，随后是 main() 函数，该函数定义了数据类型为 MyData 的变量 myData，然后通过 printf() 语句显示 myData 的大小。

启动清单 7.11 中的 C 程序的输出如下：

Memory allocated to mydata: 10

## 在 C 中组合联合和结构体

你可以在 C 中创建一个自定义数据类型，将 C union 和 C struct 组合在一起。清单 7.12 显示了 Vector.c 的内容，该内容定义了一个 3D 向量（作为自定义 C union），其中还包含一个 2D 向量（定义为 C struct）。

### 清单 7.12: Vector.c

```c
#include <stdio.h>
#include <math.h>

// a 2D vector:
typedef struct {
    double x, y;
} vector2D;

// a 3D vector:
typedef struct {
    union {
        struct {
            double x, y;
        };
        vector2D v2;
    };
    double z;
} vector3D;

double length2D (vector2D v){
    return sqrt(v.x*v.x + v.y*v.y);
}

double length3D (vector3D v){
    return sqrt(v.x*v.x + v.y*v.y + v.z*v.z);
}

int main()
{
    vector3D v = {.x=5, .y=8, .z=4};
    printf("Vector v: (%f,%f,%f)\n", v.x,v.y,v.z);
    printf("Magnitude: %g\n", length3D(v));
    double projected = length2D(v.v2);
    printf("Projection: length of %g\n", projected);

    return 0;
}
```

清单 7.12 定义了表示二维点的 C struct vector2D，随后是 C struct vector3D，其中包含一个 union 数据类型，然后是数据类型为 double 的变量 z。

下一段代码定义了函数 length2D，用于计算 2D 向量的长度，即向量与其自身内积的平方根。下一个函数是 length3D，用于计算 3D 向量的长度（也是向量与其自身内积的平方根）。

清单 7.12 的最后一部分是 main() 函数，它初始化类型为 vector3D 的向量 v，然后是 printf() 语句用于显示其分量和长度。下一个代码块初始化向量 projected，它是一个 2D 向量，通过分量 v.v2 从 v 派生而来，然后显示向量 projected 的长度。启动清单 7.12 中的代码的输出如下：

Vector v: (5.000000,8.000000,4.000000)
Magnitude: 10.247
Projection: length of 9.43398

## C 中的位域

C 中的位域非常适合包含真/假值的 C struct 数据类型。例如，考虑以下 C struct 定义：

```c
struct
{
    unsigned int validDay;
    unsigned int validMonth;
} dateInfo;
```

前面的 C struct 需要 8 字节内存，即使值要么是 0 要么是 1。另外，以下 C 位域定义更紧凑：

```c
struct
{
    unsigned int validDay: 1;
    unsigned int validMonth: 1;
} dateInfo;
```

在 int 为 32 位的典型系统上，前面的 C struct 为 dateInfo 变量使用 4 字节，为其元素使用 2 位内存。如果你指定最多 32 位值，dateInfo 变量需要 4 字节。然而，如果你指定 33 到 63 位之间的值，dateInfo 变量需要 8 字节（你一定能看出这里的规律）。

现在让我们看一下清单 7.13，它显示了 Bitfields.c 的内容，以说明如何在 C 中定义位域。

### 清单 7.13: Bitfields.c

```c
#include <stdio.h>
#include <string.h>

// define simple structure
struct
{
    unsigned int widthValidated;
    unsigned int heightValidated;
} status1;

// define a structure with bit fields
struct
{
    unsigned int widthValidated : 1;
    unsigned int heightValidated : 1;
} status2;

int main()
{
    printf("Memory size occupied by status1: %d\n",sizeof(status1));
    printf("Memory size occupied by status2: %d\n",sizeof(status2));

    return 0;
}
```

```
Memory size of status1: 8
Memory size of status2: 4
```

## 在 C 中显示环境变量

当你启动一个 C 程序时，你可以确定当前环境中变量的值。你也可以为当前环境中的变量分配值。本节和下一节包含使用 C 函数 `getenv()` 和 `putenv()` 实现此操作的示例。

**清单 7.14** 显示了 `PrintEnvVars.c` 的内容，说明了如何使用 `getenv()` 方法以便找到你在其中启动二进制可执行文件 `PrintEnvVars` 的当前命令 shell 中的变量（及其值）。

### 清单 7.14: PrintEnvVars.c

```c
#include <stdlib.h>
```


```c
#include <stdio.h>

int main(int argc, char **argv)
{
   char *pathvar;

   pathvar = getenv("PATH");
   printf("pathvar=%s",pathvar);
}
```

清单 7.14 很直观：`main()` 函数包含与字符串 `PATH` 相关的内置 C 函数 `getenv()`。调用 `getenv()` 的结果是 `PATH` 环境变量的值，该值被赋给字符指针 `pathvar`。`main()` 函数中的最后一行代码是 `printf()` 函数，它显示 `PATH` 环境变量的值。编译并执行清单 7.14 中的代码后的输出如下：

```text
pathvar=/Users/ocampesato/jython2.5.2:/Users/ocampesato/anaconda/bin:/opt/local/bin:/Users/ocampesato/android-sdk-mac_86/platform-tools:/Users/ocampesato/android-sdk-mac_86/tools:/Users/ocampesato/apache-maven-3.1.1/bin:/usr/local/bin:/Users/ocampesato/xalan-j_2.7.1:/Users/ocampesato/lua-5.1.4/src:/Users/ocampesato/.rvm/bin:/Users/ocampesato/mongoose:/Users/ocampesato/android-ndk-r4b:/usr/local/bin:/usr/local/sbin:/usr/local/mysql/bin:/Applications/XAMPP/xamppfiles/bin:/Users/ocampesato/phantomjs/bin:../Users/ocampesato/anaconda/bin:/Library/Frameworks/Python.framework/Versions/3.3/bin:/opt/local/bin:/opt/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/local/CrossPack-AVR/bin:/usr/local/git/bin:/Users/ocampesato/.rvm/bin:/Users/ocampesato/gradle-1.9/bin:/usr/local/go/bin:/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin:/Users/ocampesato/gyp-read-only:/Users/ocampesato/depot_tools:/Users/ocampesato/hadoop-1.1.0/bin:/Users/ocampesato/local/bin:/Users/ocampesato/PebbleSDK-2.0-BETA5/binoswald-campesatos-macbook:manuscript
```

## 在 C 中设置环境变量

清单 7.15 显示了 SetEnvVars.c 的内容，说明了如何使用 putenv() 函数在当前环境中设置（“放置”）变量及其值。

### 清单 7.15：SetEnvVars.c

```c
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char **argv)
{
    char *pathvar;

    pathvar = getenv("PATH");
    printf("The current path is: %s\n\n", pathvar);

    if (-1 == putenv("PATH=:/home/userid"))
    {
        printf("putenv failed \n");
        return EXIT_FAILURE;
    }

    pathvar = getenv("PATH");
    printf("The new path is: %s\n", pathvar);

    return 0;
}
```

清单 7.14 读取 PATH 环境变量的值，而清单 7.15 设置环境变量的值。事实上，清单 7.15 首先调用 getenv() 函数读取 PATH 环境变量的值，然后调用内置 C 函数 putenv() 为 PATH 变量分配新值。请注意条件逻辑：如果 putenv() 命令失败，将显示错误消息。

main() 函数的最后一部分再次调用 getenv() 函数并显示结果，只是为了确认 PATH 变量已正确更新。编译并执行清单 7.15 中的代码后的输出（为简洁起见已截断）如下：

```text
The current path is: /opt/spark/bin:/Users/owner/mongodb-osx-x86_64-3.4.2/bin:/Users/owner/anaconda2/bin:

The new path is: /:/home/userid
```

请记住，程序执行完毕后，PATH 变量将保留其初始值（即更改是临时的）。

## C 中的存储类说明符

C 中有 5 个存储类说明符：

- auto
- extern
- static
- register
- _Thread_local

auto 存储类说明符表示变量具有自动存储期。由于这是默认值，因此很少使用。extern 关键字与外部链接有关，主要用于在头文件中声明全局变量。static 关键字根据上下文有不同的含义。它可以声明具有静态存储期的变量，这意味着其值在函数的多次调用之间持续存在。它也可以声明变量具有内部链接。

`_Thread_local` 存储类在多线程编程中很有用，它声明的变量在每个线程中具有不同的值。register 关键字过去是向编译器提示某个变量使用频繁，应放入处理器寄存器以便快速访问。自 C 语言诞生以来，编译器优化已大幅改进，现代编译器会直接忽略 register 提示。

使用这些 C 说明符的一些示例如下：

```c
register int i;        // i is an int, register keyword
                       // probably ignored
extern int j;          // declaration for j, j must be defined
                       // elsewhere
static int k = 0;      // variable k only visible in this
                       // translation unit
_Thread_local m = 5;   // m has a different instance in each
                       // thread

void f() {
    int n = 2;         // initialized to 2 every function
                       // call
    auto int m = 2;    // same as above, auto is the default
    static int o = 3;  // set to 3 on the first function call
}
```

## 如何编写使用指针的复杂代码

这个标题略带戏谑的小节旨在向你展示最好避免的那类代码，因为很容易犯错。清单 7.16 显示了 `DontDoThis.c` 的内容，说明了如何错误地使用指针。

### 清单 7.16：DontDoThis.c

```c
#include <stdlib.h>

int main()
{
  // a data value and an array
  int value, array[10];

  // point to the first element
  int *arrptr = &array[0];
  printf("arrptr: %d\n", arrptr);

  // get element #0 from arrptr
  value = *arrptr++;
  printf("value1: %d\n", value);

  value = *++arrptr;
  printf("value2: %d\n", value);

  // get element #1 from arrptr
  value = ++*arrptr;
  printf("value3: %d\n", value);
}
```

尽管清单 7.16 中的代码在语法上是正确的，但即使是经验丰富的 C 程序员也可能无意中引用指针的内存位置，而不是指针的内容（这是非常常见的情况）。

运行清单 7.16 中编译后的代码，你将看到以下输出：

```text
arrptr: 1560138064
value1: 280822976
value2: 0
value3: 1
```

再举一个例子，考虑以下代码块，它使用指针将字符串从源（q）复制到目标（p）：

```c
void copy_string(char *p, char *q) {
    while (*p++ = *q++);
}
```

尽管可以确定前一个代码块的用途，但下面这段更长——但等价——的代码更容易理解、维护和调试：

```c
void copy_string(char *dest, char *source)
{
    while (1) {
        *dest = *source;

        // Exit if we copied the end of string
        if (*dest == '\0') return;

        ++source;

        ++dest;
    }
}
```

请注意，if 语句和 return 语句位于同一行。在这个例子中，代码非常直观，不可能产生混淆，这向你表明，关于代码语法的规则可能存在例外。

## C 中的错误处理

尽管 C 不直接支持错误处理，但你可以通过返回值确定程序执行的结果。回想一下，C 程序中的 main() 函数返回类型为 `int`，这意味着你可以返回不同的值来表示程序执行的不同结果。

### errno 全局变量

大多数 C 函数调用在发生错误时返回 -1 或 `NULL`，并通过全局变量 `errno` 设置错误代码。因此，你可以检查该变量的值，以便根据该变量的值决定如何继续。如果你感兴趣，各种错误代码定义在 `<errno.h>` 头文件中。

### perror() 和 strerror() 函数

C 编程语言提供了 `perror()` 和 `strerror()` 函数，用于显示与 `errno` 关联的文本消息。

`perror()` 函数显示你传给它的字符串，随后是一个冒号、一个空格，然后是当前 `errno` 值的文本表示。例如，如果你的 C 程序找不到某个目录，将显示以下消息：

> 错误：没有那个文件或目录

`strerror()` 函数返回指向当前 `errno` 值文本表示的指针，其输出与 `perror()` 函数的输出类似。

### 如何从错误中退出

请记住以下行为：尝试*浮点数除以零*的 C 程序是运行时错误，而*整数除以零*是未定义行为。解决方案包括检查……的值


在执行除法之前先检查分母。清单 7.17 显示了 DivByZero.c 的内容，该文件说明了如何防止除零，并附带合适的文本消息。

### 清单 7.17：DivByZero.c

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int dividend = 20;
    int divisor = 5;
    int quotient;

    if( divisor == 0){
        fprintf(stderr, "Division by zero: exiting program\n");
        exit(EXIT_FAILURE);
    }

    quotient = dividend / divisor;
    fprintf(stderr, "Value of quotient : %d\n", quotient );

    exit(EXIT_SUCCESS);
}
```

清单 7.17 包含一个 `main()` 函数，该函数初始化了三个整数值变量，然后是检查变量 divisor 值的条件逻辑。

请注意，程序在成功时以 EXIT_SUCCESS 的值退出，其中 EXIT_SUCCESS 是一个宏，并在出错时以 EXIT_FAILURE 状态退出。

还有一个细节：C 标准并不要求 EXIT_SUCCESS 和 EXIT_FAILURE 有特定的值。唯一的要求是它们必须被定义，并且其值必须能在 int 中表示。

编译清单 7.17 中的代码并运行，你将看到以下结果：

```text
Value of quotient : 4
```

下一节简要讨论了 C 中的系统调用，这绝对是一个高级主题。然而，这里有两个代码示例在你的掌握范围内，它们为该主题提供了温和的介绍。

## C 中的系统调用（可选）

这个主题是本书的最后一个主题，也是最复杂的主题之一。本节提供了系统调用的极简描述，以便你了解其存在及其目的。本节还包含一个非常简单的 C 程序示例，该程序执行系统调用。

### 删除文件

清单 7.18 显示了 `SystemDeleteFile.c` 的内容，说明了如何调用 `unlink()` 命令来删除文件。

### 清单 7.18：SystemDeleteFile.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
        printf("File %s does not exist\n", filename);
    }
    else
    {
        printf("Successfully removed file %s\n", filename);
    }

    return 0;
}
```

**清单 7.18** 包含一个 `main()` 函数，该函数将变量 `filename` 初始化为值 `text.txt`。代码的下一部分是条件逻辑，调用内置 C 函数 `unlink()` 以删除文件 `text.txt`。如果命令失败，将显示合适的消息。如果结果成功，将显示不同的消息。

现在在包含文件 `SystemDeleteFile.c` 的目录中创建一个名为 `text.txt` 的文件。编译此代码并调用二进制可执行文件，你将看到以下输出：

```text
Successfully removed file text.txt
```

再次调用此命令，这次你将看到不同的消息：

```text
File text.txt does not exist
```

### 列出目录中的文件

**清单 7.19** 显示了 `SystemForkExec.c` 的内容，说明了如何使用 `fork()` 和 `exec()` 系统调用来创建一个新进程以列出目录的内容。请记住，`fork()` 和 `exec()` 系统调用不是 C 语言的一部分，它们仅在支持 POSIX 标准的系统上可用。

### 清单 7.19：SystemForkExec.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    char *ls_args[] = { "/bin/ls", "-l", NULL };

    int pid = fork();

    if(pid == 0) // the child
    {
        execv(ls_args[0], ls_args);
    }
    else if(pid > 0) // the parent
    {
        // wait for the child to complete
        wait(NULL);
    }
    else
    {
        printf("Error: negative process ID\n");
    }

    exit(0);
}
```

清单 7.19 以几个 #include 语句开始，这些语句是执行 fork() 和 exec() 系统调用所必需的。下一节包含 main() 函数，该函数将字符指针初始化为包含三个元素的数组：Unix ls 命令的完整路径、与 ls 命令一起使用的选项以及值 NULL。

接下来，调用 fork() 函数，并使用结果初始化整数 pid 的值。关键点要记住：如果 pid 为零，则我们在子进程中；如果 pid 为正，则我们在父进程中；pid 的任何其他值都是错误（即 fork() 命令失败）。

前述场景通过条件逻辑捕获，其中显示了适当的[content]
在执行除法之前先检查分母。清单 7.17 显示了 DivByZero.c 的内容，该文件说明了如何防止除零，并附带合适的文本消息。

### 清单 7.17：DivByZero.c

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int dividend = 20;
    int divisor = 5;
    int quotient;

    if( divisor == 0){
        fprintf(stderr, "Division by zero: exiting program\n");
        exit(EXIT_FAILURE);
    }

    quotient = dividend / divisor;
    fprintf(stderr, "Value of quotient : %d\n", quotient );

    exit(EXIT_SUCCESS);
}
```

清单 7.17 包含一个 `main()` 函数，该函数初始化了三个整数值变量，然后是检查变量 divisor 值的条件逻辑。

请注意，程序在成功时以 EXIT_SUCCESS 的值退出，其中 EXIT_SUCCESS 是一个宏，并在出错时以 EXIT_FAILURE 状态退出。

还有一个细节：C 标准并不要求 EXIT_SUCCESS 和 EXIT_FAILURE 有特定的值。唯一的要求是它们必须被定义，并且其值必须能在 int 中表示。

编译清单 7.17 中的代码并运行，你将看到以下结果：

```text
Value of quotient : 4
```

下一节简要讨论了 C 中的系统调用，这绝对是一个高级主题。然而，这里有两个代码示例在你的掌握范围内，它们为该主题提供了温和的介绍。

## C 中的系统调用（可选）

这个主题是本书的最后一个主题，也是最复杂的主题之一。本节提供了系统调用的极简描述，以便你了解其存在及其目的。本节还包含一个非常简单的 C 程序示例，该程序执行系统调用。

### 删除文件

清单 7.18 显示了 `SystemDeleteFile.c` 的内容，说明了如何调用 `unlink()` 命令来删除文件。

### 清单 7.18：SystemDeleteFile.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
        printf("File %s does not exist\n", filename);
    }
    else
    {
        printf("Successfully removed file %s\n", filename);
    }

    return 0;
}
```

**清单 7.18** 包含一个 `main()` 函数，该函数将变量 `filename` 初始化为值 `text.txt`。代码的下一部分是条件逻辑，调用内置 C 函数 `unlink()` 以删除文件 `text.txt`。如果命令失败，将显示合适的消息。如果结果成功，将显示不同的消息。

现在在包含文件 `SystemDeleteFile.c` 的目录中创建一个名为 `text.txt` 的文件。编译此代码并调用二进制可执行文件，你将看到以下输出：

```text
Successfully removed file text.txt
```

再次调用此命令，这次你将看到不同的消息：

```text
File text.txt does not exist
```

### 列出目录中的文件

**清单 7.19** 显示了 `SystemForkExec.c` 的内容，说明了如何使用 `fork()` 和 `exec()` 系统调用来创建一个新进程以列出目录的内容。请记住，`fork()` 和 `exec()` 系统调用不是 C 语言的一部分，它们仅在支持 POSIX 标准的系统上可用。

### 清单 7.19：SystemForkExec.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    char *ls_args[] = { "/bin/ls", "-l", NULL };

    int pid = fork();

    if(pid == 0) // the child
    {
        execv(ls_args[0], ls_args);
    }
    else if(pid > 0) // the parent
    {
        // wait for the child to complete
        wait(NULL);
    }
    else
    {
        printf("Error: negative process ID\n");
    }

    exit(0);
}
```

清单 7.19 以几个 #include 语句开始，这些语句是执行 fork() 和 exec() 系统调用所必需的。下一节包含 main() 函数，该函数将字符指针初始化为包含三个元素的数组：Unix ls 命令的完整路径、与 ls 命令一起使用的选项以及值 NULL。

接下来，调用 fork() 函数，并使用结果初始化整数 pid 的值。关键点要记住：如果 pid 为零，则我们在子进程中；如果 pid 为正，则我们在父进程中；pid 的任何其他值都是错误（即 fork() 命令失败）。

前述场景通过条件逻辑捕获，其中显示了适当的[content]
在执行除法之前先检查分母。清单 7.17 显示了 DivByZero.c 的内容，该文件说明了如何防止除零，并附带合适的文本消息。

### 清单 7.17：DivByZero.c

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int dividend = 20;
    int divisor = 5;
    int quotient;

    if( divisor == 0){
        fprintf(stderr, "Division by zero: exiting program\n");
        exit(EXIT_FAILURE);
    }

    quotient = dividend / divisor;
    fprintf(stderr, "Value of quotient : %d\n", quotient );

    exit(EXIT_SUCCESS);
}
```

清单 7.17 包含一个 `main()` 函数，该函数初始化了三个整数值变量，然后是检查变量 divisor 值的条件逻辑。

请注意，程序在成功时以 EXIT_SUCCESS 的值退出，其中 EXIT_SUCCESS 是一个宏，并在出错时以 EXIT_FAILURE 状态退出。

还有一个细节：C 标准并不要求 EXIT_SUCCESS 和 EXIT_FAILURE 有特定的值。唯一的要求是它们必须被定义，并且其值必须能在 int 中表示。

编译清单 7.17 中的代码并运行，你将看到以下结果：

```text
Value of quotient : 4
```

下一节简要讨论了 C 中的系统调用，这绝对是一个高级主题。然而，这里有两个代码示例在你的掌握范围内，它们为该主题提供了温和的介绍。

## C 中的系统调用（可选）

这个主题是本书的最后一个主题，也是最复杂的主题之一。本节提供了系统调用的极简描述，以便你了解其存在及其目的。本节还包含一个非常简单的 C 程序示例，该程序执行系统调用。

### 删除文件

清单 7.18 显示了 `SystemDeleteFile.c` 的内容，说明了如何调用 `unlink()` 命令来删除文件。

### 清单 7.18：SystemDeleteFile.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
        printf("File %s does not exist\n", filename);
    }
    else
    {
        printf("Successfully removed file %s\n", filename);
    }

    return 0;
}
```

**清单 7.18** 包含一个 `main()` 函数，该函数将变量 `filename` 初始化为值 `text.txt`。代码的下一部分是条件逻辑，调用内置 C 函数 `unlink()` 以删除文件 `text.txt`。如果命令失败，将显示合适的消息。如果结果成功，将显示不同的消息。

现在在包含文件 `SystemDeleteFile.c` 的目录中创建一个名为 `text.txt` 的文件。编译此代码并调用二进制可执行文件，你将看到以下输出：

```text
Successfully removed file text.txt
```

再次调用此命令，这次你将看到不同的消息：

```text
File text.txt does not exist
```

### 列出目录中的文件

**清单 7.19** 显示了 `SystemForkExec.c` 的内容，说明了如何使用 `fork()` 和 `exec()` 系统调用来创建一个新进程以列出目录的内容。请记住，`fork()` 和 `exec()` 系统调用不是 C 语言的一部分，它们仅在支持 POSIX 标准的系统上可用。

### 清单 7.19：SystemForkExec.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    char *ls_args[] = { "/bin/ls", "-l", NULL };

    int pid = fork();

    if(pid == 0) // the child
    {
        execv(ls_args[0], ls_args);
    }
    else if(pid > 0) // the parent
    {
        // wait for the child to complete
        wait(NULL);
    }
    else
    {
        printf("Error: negative process ID\n");
    }

    exit(0);
}
```

清单 7.19 以几个 #include 语句开始，这些语句是执行 fork() 和 exec() 系统调用所必需的。下一节包含 main() 函数，该函数将字符指针初始化为包含三个元素的数组：Unix ls 命令的完整路径、与 ls 命令一起使用的选项以及值 NULL。

接下来，调用 fork() 函数，并使用结果初始化整数 pid 的值。关键点要记住：如果 pid 为零，则我们在子进程中；如果 pid 为正，则我们在父进程中；pid 的任何其他值都是错误（即 fork() 命令失败）。

前述场景通过条件逻辑捕获，其中显示了适当的[content]
在执行除法之前先检查分母。清单 7.17 显示了 DivByZero.c 的内容，该文件说明了如何防止除零，并附带合适的文本消息。

### 清单 7.17：DivByZero.c

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int dividend = 20;
    int divisor = 5;
    int quotient;

    if( divisor == 0){
        fprintf(stderr, "Division by zero: exiting program\n");
        exit(EXIT_FAILURE);
    }

    quotient = dividend / divisor;
    fprintf(stderr, "Value of quotient : %d\n", quotient );

    exit(EXIT_SUCCESS);
}
```

清单 7.17 包含一个 `main()` 函数，该函数初始化了三个整数值变量，然后是检查变量 divisor 值的条件逻辑。

请注意，程序在成功时以 EXIT_SUCCESS 的值退出，其中 EXIT_SUCCESS 是一个宏，并在出错时以 EXIT_FAILURE 状态退出。

还有一个细节：C 标准并不要求 EXIT_SUCCESS 和 EXIT_FAILURE 有特定的值。唯一的要求是它们必须被定义，并且其值必须能在 int 中表示。

编译清单 7.17 中的代码并运行，你将看到以下结果：

```text
Value of quotient : 4
```

下一节简要讨论了 C 中的系统调用，这绝对是一个高级主题。然而，这里有两个代码示例在你的掌握范围内，它们为该主题提供了温和的介绍。

## C 中的系统调用（可选）

这个主题是本书的最后一个主题，也是最复杂的主题之一。本节提供了系统调用的极简描述，以便你了解其存在及其目的。本节还包含一个非常简单的 C 程序示例，该程序执行系统调用。

### 删除文件

清单 7.18 显示了 `SystemDeleteFile.c` 的内容，说明了如何调用 `unlink()` 命令来删除文件。

### 清单 7.18：SystemDeleteFile.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
        printf("File %s does not exist\n", filename);
    }
    else
    {
        printf("Successfully removed file %s\n", filename);
    }

    return 0;
}
```

**清单 7.18** 包含一个 `main()` 函数，该函数将变量 `filename` 初始化为值 `text.txt`。代码的下一部分是条件逻辑，调用内置 C 函数 `unlink()` 以删除文件 `text.txt`。如果命令失败，将显示合适的消息。如果结果成功，将显示不同的消息。

现在在包含文件 `SystemDeleteFile.c` 的目录中创建一个名为 `text.txt` 的文件。编译此代码并调用二进制可执行文件，你将看到以下输出：

```text
Successfully removed file text.txt
```

再次调用此命令，这次你将看到不同的消息：

```text
File text.txt does not exist
```

### 列出目录中的文件

**清单 7.19** 显示了 `SystemForkExec.c` 的内容，说明了如何使用 `fork()` 和 `exec()` 系统调用来创建一个新进程以列出目录的内容。请记住，`fork()` 和 `exec()` 系统调用不是 C 语言的一部分，它们仅在支持 POSIX 标准的系统上可用。

### 清单 7.19：SystemForkExec.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    char *ls_args[] = { "/bin/ls", "-l", NULL };

    int pid = fork();

    if(pid == 0) // the child
    {
        execv(ls_args[0], ls_args);
    }
    else if(pid > 0) // the parent
    {
        // wait for the child to complete
        wait(NULL);
    }
    else
    {
        printf("Error: negative process ID\n");
    }

    exit(0);
}
```

清单 7.19 以几个 #include 语句开始，这些语句是执行 fork() 和 exec() 系统调用所必需的。下一节包含 main() 函数，该函数将字符指针初始化为包含三个元素的数组：Unix ls 命令的完整路径、与 ls 命令一起使用的选项以及值 NULL。

接下来，调用 fork() 函数，并使用结果初始化整数 pid 的值。关键点要记住：如果 pid 为零，则我们在子进程中；如果 pid 为正，则我们在父进程中；pid 的任何其他值都是错误（即 fork() 命令失败）。

前述场景通过条件逻辑捕获，其中显示了适当的[content]
在执行除法之前先检查分母。清单 7.17 显示了 DivByZero.c 的内容，该文件说明了如何防止除零，并附带合适的文本消息。

### 清单 7.17：DivByZero.c

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int dividend = 20;
    int divisor = 5;
    int quotient;

    if( divisor == 0){
        fprintf(stderr, "Division by zero: exiting program\n");
        exit(EXIT_FAILURE);
    }

    quotient = dividend / divisor;
    fprintf(stderr, "Value of quotient : %d\n", quotient );

    exit(EXIT_SUCCESS);
}
```

清单 7.17 包含一个 `main()` 函数，该函数初始化了三个整数值变量，然后是检查变量 divisor 值的条件逻辑。

请注意，程序在成功时以 EXIT_SUCCESS 的值退出，其中 EXIT_SUCCESS 是一个宏，并在出错时以 EXIT_FAILURE 状态退出。

还有一个细节：C 标准并不要求 EXIT_SUCCESS 和 EXIT_FAILURE 有特定的值。唯一的要求是它们必须被定义，并且其值必须能在 int 中表示。

编译清单 7.17 中的代码并运行，你将看到以下结果：

```text
Value of quotient : 4
```

下一节简要讨论了 C 中的系统调用，这绝对是一个高级主题。然而，这里有两个代码示例在你的掌握范围内，它们为该主题提供了温和的介绍。

## C 中的系统调用（可选）

这个主题是本书的最后一个主题，也是最复杂的主题之一。本节提供了系统调用的极简描述，以便你了解其存在及其目的。本节还包含一个非常简单的 C 程序示例，该程序执行系统调用。

### 删除文件

清单 7.18 显示了 `SystemDeleteFile.c` 的内容，说明了如何调用 `unlink()` 命令来删除文件。

### 清单 7.18：SystemDeleteFile.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
        printf("File %s does not exist\n", filename);
    }
    else
    {
        printf("Successfully removed file %s\n", filename);
    }

    return 0;
}
```

**清单 7.18** 包含一个 `main()` 函数，该函数将变量 `filename` 初始化为值 `text.txt`。代码的下一部分是条件逻辑，调用内置 C 函数 `unlink()` 以删除文件 `text.txt`。如果命令失败，将显示合适的消息。如果结果成功，将显示不同的消息。

现在在包含文件 `SystemDeleteFile.c` 的目录中创建一个名为 `text.txt` 的文件。编译此代码并调用二进制可执行文件，你将看到以下输出：

```text
Successfully removed file text.txt
```

再次调用此命令，这次你将看到不同的消息：

```text
File text.txt does not exist
```

### 列出目录中的文件

**清单 7.19** 显示了 `SystemForkExec.c` 的内容，说明了如何使用 `fork()` 和 `exec()` 系统调用来创建一个新进程以列出目录的内容。请记住，`fork()` 和 `exec()` 系统调用不是 C 语言的一部分，它们仅在支持 POSIX 标准的系统上可用。

### 清单 7.19：SystemForkExec.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    char *ls_args[] = { "/bin/ls", "-l", NULL };

    int pid = fork();

    if(pid == 0) // the child
    {
        execv(ls_args[0], ls_args);
    }
    else if(pid > 0) // the parent
    {
        // wait for the child to complete
        wait(NULL);
    }
    else
    {
        printf("Error: negative process ID\n");
    }

    exit(0);
}
```

清单 7.19 以几个 #include 语句开始，这些语句是执行 fork() 和 exec() 系统调用所必需的。下一节包含 main() 函数，该函数将字符指针初始化为包含三个元素的数组：Unix ls 命令的完整路径、与 ls 命令一起使用的选项以及值 NULL。

接下来，调用 fork() 函数，并使用结果初始化整数 pid 的值。关键点要记住：如果 pid 为零，则我们在子进程中；如果 pid 为正，则我们在父进程中；pid 的任何其他值都是错误（即 fork() 命令失败）。

前述场景通过条件逻辑捕获，其中显示了适当的[content]
消息。启动清单 7.19 中的代码输出如下：

```text
-rwxr-xr-x 1 owner staff 8560 Jul 24 19:22 SystemForkExec
-rw-r--r-- 1 owner staff    0 Jul 24 19:22 a
-rw-r--r-- 1 owner staff    0 Jul 24 19:22 b
-rw-r--r-- 1 owner staff    0 Jul 24 19:22 c
```

二进制可执行文件 SystemForkExec 在包含该二进制可执行文件和三个文件 a、b 和 c 的目录中被调用，所有文件大小均为 0。

## 在多个文件中定义自定义函数（可选）

本节展示了如何在两个 C 文件中定义自定义函数，然后将它们包含在编译中以创建一个单一的可执行文件。

清单 7.20、清单 7.21 和清单 7.22 显示了文件 FindChar2.h、FindChar2.c 和 FindMain2.c 的内容，它们被编译成一个名为 FindMain2 的二进制可执行文件。

### 清单 7.20：FindChar2.h

```c
#include <ctype.h>
#include <stdio.h>

void findChar(char str[], char c);
```

清单 7.20 是一个非常简短的头文件：它包含两个头文件以及函数 findChar() 的函数原型。

### 清单 7.21：FindChar2.c

```c
#include <ctype.h>
#include <stdio.h>

void findChar(char str[], char c)
{
    int matchCount = 0;

    printf("String: %s\n", str);
    printf("Char:   %c\n", c);

    for(int i=0; str[i]; i++)
    {
        if(str[i] == c)
        {
            printf("Match in position: %d\n", i);
            ++matchCount;
        }
    }

    printf("Count:  %d\n\n", matchCount);
}
```

清单 7.21 包含了你在第 3 章代码示例中看到的函数 `findChar()` 的实现细节。

### 清单 7.22：FindMain2.c

```c
#include "FindChar2.h"

int main()
{
    char str1[] = "pasta";
    findChar(str1, 'a');

    char str2[] = "New York City";
    findChar(str2, 'k');

    char str3[] = "California";
    findChar(str3, 'z');

    return (0);
}
```

**清单 7.22** 包含一个本地头文件 `FindChar2.h`（即它不是 C 语言的一部分），后面跟着一个 `main()` 函数。请注意，`main()` 函数定义了三个字符串并三次调用 `findChar()` 函数（在 `FindChar2.c` 中定义）。

C 程序 `FindChar2.c` 和 `FindMain2.c` 需要在涉及 `gcc` 的编译步骤中指定，如下所示：

```bash
#### do not change the order of the next two lines:
gcc -std=c11 -Wall -c FindChar2.c
gcc -std=c11 FindChar2.o FindMain2.c -o FindMain2
```

前述代码片段的输出是二进制可执行文件 `FindMain2`，而启动 `FindMain2` 的输出如下：

```text
String: pasta
Char: a
Match in position: 1
Match in position: 4
Count: 2

String: New York City
Char: k
Match in position: 7
Count: 1

String: California
Char: z
Count: 0
```

前面的示例是可管理的，因为只有三个文件涉及，你可以从命令行在调用 `gcc` 时指定它们。然而，C 程序可能涉及数十个文件的多个依赖关系，并且跟踪它们（以及对头文件和自定义库的依赖关系）很快就会变得难以承受。一个解决方案涉及 make 实用程序，这在附录中讨论。

## 标准头文件和库

正如你在本书的代码示例中看到的那样，C 程序不可避免地需要在编译成目标文件时需要标准头文件，以及在执行创建可执行文件的链接步骤时需要标准库。

请注意，/usr/include 仅在 Unix 和类 Unix 系统上使用，而 Windows 编译器的“include”文件位于安装目录中的某个位置。

### 标准头文件（类 Unix 系统）

在类 Unix 系统上，目录 /usr/include 包含各种“头”文件，其中一些显示如下（来自 MacBook Pro）：

- AppleTextureEncoder.h
- AssertMacros.h
- Availability.h
- AvailabilityInternal.h
- AvailabilityMacros.h
- Block.h
- CommonCrypto
- ConditionalMacros.h
- MacTypes.h
- [files omitted for brevity]
- wordexp.h



- xar
- xattr_flags.h
- xlocale
- xlocale.h
- xpc
- zconf.h
- zlib.h

/usr/include 目录包含本书中每个 C 程序都会包含的各种“头”文件。你将在下一节看到示例。此外，你可以创建自定义头文件，将其放置在项目中，然后在 C 程序中引用它们。

你可以通过在 C 程序开头放置以下类型的语句来包含头文件：

```
#include <stdio.h>
```

如果你的自定义头文件名为 mystdio.h 且位于与 C 程序相同的目录中，可以使用以下语法引用此头文件：

```
#include "mystdio.h"
```

## 常用头文件

以下列表包含常用的 C 头文件，并附带对其用途的简要说明：

- `<ctype.h>` 定义字符操作例程
- `<math.h>` 定义数学例程
- `<stdio.h>` 定义输入/输出例程
- `<stdlib.h>` 定义数字转换、存储分配和类似任务
- `<stdarg.h>` 定义用于处理可变参数例程的库
- `<string.h>` 定义字符串操作例程
- `<time.h>` 定义时间操作例程

此外，还有以下头文件：

- `<assert.h>` 定义诊断例程
- `<float.h>` 定义 float 类型的常量
- `<limits.h>` 定义 int 类型的常量
- `<setjmp.h>` 定义非局部函数调用
- `<signal.h>` 定义信号处理程序

如有必要，你可以在线搜索以获取有关这些头文件的更多信息。

## 标准库

目录 /usr/lib 包含各种库，其中一些显示如下：

```
PN548_API.dylib
PN548_HAL_OSX.dylib
PN548_OSX.dylib
bundle1.o
charset.alias
cron
crt.1.10.5.o
crt.1.10.6.o
rpcsvc
ruby
sasl2
sqlite3
ssh-keychain.dylib
```

两种主要类型的库是静态库和动态库，本书均有使用。附录展示了如何在 Makefile 中引用头文件和库，该 Makefile 指定了编译 C 代码和创建二进制文件的各种依赖项。

## 摘要

本章你学习了 C 结构体，并看到了创建嵌套 C 结构体、C 结构体指针和 C 结构体数组的示例。你还看到了如何定义 C 联合体和 C 位域。然后你学习了头文件，以及如何在 C 程序中定义和引用本地头文件。然后你学习了系统调用的基础信息以及如何使用 unlink()、fork() 和 exec() 系统命令。最后，你学习了 C 程序中常用 C 头文件和 C 库的标准位置（通常在 makefile 中）。

## 附录

## make 工具

本附录讨论 `make` 工具，该工具可以帮助你管理具有多个依赖项的 C 应用程序。`make` 工具在管理涉及根据修改日期重新编译 C 程序、创建目标文件、更新库和集成其他制品的项目方面表现出色。虽然本附录中的示例针对 C 程序，但 `make` 工具对于 C++ 项目同样适用。

本附录的第一部分首先描述 `make` 工具和 Makefile，然后简要讨论用于管理目标文件和库的 Unix 命令，例如 `ar` 命令和 `ranlib` 命令。你还将学习如何使用 `nm` 命令来查找 C 程序中的符号定义。

本附录的第二部分深入探讨 `make` 工具，这是本附录的大部分内容。你将学习如何使用 `make` 工具进行一些简单示例、在 makefile 中使用宏以及如何创建多个可执行文件。

第三部分展示了如何在 makefile 中指定头文件和库文件，以及如何定义嵌套 makefile。本附录的剩余部分
包含 make 工具的其他各种功能。

## 什么是 make 工具？

make 工具是一个二进制可执行文件，它读取基于文本的“makefile”的内容以执行命令。make 工具会在当前目录中搜索名为 `Makefile` 的文件，如果该文件不存在，则会搜索名为 `makefile` 的文件。如果两者都不存在，则 make 工具会以以下消息失败：

```
make: *** No targets specified and no makefile found. Stop.
```

正如你在本附录后面会看到的，你可以使用 make 工具的 `-f` 开关来指定具有不同名称的 makefile。在本附录中，术语“makefile”将指默认文件 `Makefile`（“大写 Make”）。

## Makefile 中有什么？

文件 `Makefile` 通常包含所谓的规则，用于执行各种命令，例如编译过时的 C 程序。不涉及语法规则（我们稍后会讨论），以下是包含单个规则用于创建名为 hello 的二进制可执行文件的 `Makefile` 的内容：

```
hello: HelloWorld.c
	gcc -Wall HelloWorld.c -o HelloWorld
```

*请注意，前述代码片段中的第二行以一个在该页面不可见的强制 `<tab>` 字符开头。*

你还可以指定编译过程中默认不包含的额外文件。例如，你可以指定自定义“头”文件（带有 `.h` 后缀的文本文件）、其他目标文件（带有 `.o` 后缀的二进制文件）或创建二进制可执行文件所需的额外库（带有 `.a` 或 `.so` 后缀的二进制文件）。

文件 `Makefile` 还可以包含不涉及编译的规则，例如 shell 脚本和 Unix 命令。你还可以创建一个“主” `Makefile`，其中包含使用位于子目录中的 `Makefile` 调用 `make` 工具的规则。这非常有用，因为你可以将大型项目细分为一组模块，其中每个模块的代码位于包含模块特定 `Makefile` 的不同子目录中。

下一节讨论一些有用的命令（例如 `ar`、`ranlib` 和 `nm`），你可以在 `Makefile` 目标中指定这些命令以对你的 `C` 程序执行编译相关步骤。

## 用于库的有用 Unix 命令

在本节中，你一直使用 `gcc` 工具从 `C` 程序创建二进制可执行文件。然而，在中型和大型项目中，`C` 应用程序通常涉及将多个 `C` 文件“组装”成单个二进制文件。这些 `C` 文件被编译成所谓的目标文件，即带有“.o”扩展名的二进制文件。

`ar`（“归档”）命令使你能够将多个“.o”文件组合成库文件，即带有“.a”扩展名的二进制文件（即静态库）。特别是，`ar` 命令使你能够向库文件添加、删除或更新“.o”文件。

另一个非常有用的工具是 nm 命令，用于在“.o”文件或库文件中查找符号定义。此工具帮助你处理“未定义符号”错误，这些错误在未包含创建二进制可执行文件所需的目标文件或库时出现。通常你会从命令行使用此工具，而在 Makefile 中使用较少。

## ar 命令示例

以下命令创建一个名为 HelloWorld.a 的静态库，其中包含目标文件 HelloWorld.o：

```
ar -r HelloWorld.a HelloWorld.o
```

使用以下命令将当前目录中的所有目标文件添加到库 HelloWorld.a：

```
ar -r HelloWorld.a *.o
```

以下命令使用 HelloWorld.o 的内容更新 HelloWorld.a：

```
ar -rcs HelloWorld.a HelloWorld.o
```

在 Makefile 中使用 ar 命令的示例如下：

```
mylib.a: class.o
    ar -r mylib.a class.o
```

在前面的片段中，“r” 开关表示将文件 class.o 插入到归档文件 mylib.a 中。搜索在线示例以了解 ar 命令的其他开关。

## ranlib 命令

每个归档库都包含一个目录表，用于跟踪库中的 .o 文件。ranlib 实用程序添加或更新归档的目录表

库，以便链接编辑器能够链接该库。此外，内容表是归档开头处的一个归档成员，它指明哪些符号定义在哪些库成员中。

## `nm` 命令

`nm` 命令显示静态库中定义或引用的符号。例如，假设库 `HelloWorld.a` 包含目标文件 `HelloWorld.o`。

如果输入以下命令：

```
nm HelloWorld.a
```

输出将类似于：

```
HelloWorld.a(HelloWorld.o):
0000000000000308 s EH_frame0
0000000000000030 s L_.str
0000000000000000 T _main
0000000000000320 S _main.eh
    U _printf

HelloWorld.a(FindChar2.o):
0000000000000420 s EH_frame0
00000000000000c6 s L_.str
00000000000000d2 s L_.str1
00000000000000de s L_.str2
0000000000000f5 s L_.str3
0000000000000000 T _findChar
0000000000000438 S _findChar.eh
    U _printf

HelloWorld.a(FindMain2.o):
0000000000000440 s EH_frame0
00000000000000c0 s L_main.str1
00000000000000c6 s L_main.str2
00000000000000d4 s L_main.str3
U __stack_chk_fail
U __stack_chk_guard
U _findChar
0000000000000000 T _main
0000000000000458 S _main.eh
```

前面输出中第二列的字母 `U` 表示 `U` 右侧指定的函数在关联的 `.o` 文件中被引用，并且其定义位于不同的归档库或目标文件中。

## 一些简单的 Makefile

本节包含一个不涉及任何 C 程序编译的 makefile。它包含执行简单命令的简单规则。注意，由于文件名非标准，必须使用 `-f` 开关。

清单 A.1 显示了 `Simplemake` 的内容，其中包含一个名为 `all` 的顶层“目标”。该目标指定了另外三个用于执行 Unix 命令的目标。

### 清单 A.1：Simplemake

```
all: hello now mymakefiles

hello:
	echo "hello world"; echo

now:
	@echo "now is `date`"; echo

mymakefiles:
	@echo "mymakefiles: `ls *akefile*`"; echo
```

清单 A.1 定义了目标 `all`，它指定了名为 `hello`、`now` 和 `mymakefiles` 的三个目标。通过指定文件 `Simplemake` 调用 make 工具，只需输入以下命令，就会调用所有三个目标：

```
make -f Simplemake
```

我的系统上的输出如下所示：

```
echo "hello world"; echo
hello world

now is Wed May 23 22:50:28 PDT 2018

mymakefiles: Makefile
Makefile-ori
Makefile1
Makefile2
Makefile3
Makefile4
Makefile5
Makefile6
Makefile7
Makefile8
Makefile9
```

如果只想调用第一个目标，则输入以下命令：

```
make -f Simplemake hello
```

我的系统上的输出如下所示：

```
echo "hello world"; echo
hello world
```

如果只想调用第二个目标，则输入以下命令：

```
make -f Simplemake now
```

我的系统上的输出如下所示：

```
now is Wed May 23 22:50:28 PDT 2018
```

最后，如果只想调用第三个目标，则输入以下命令：

```
make -f Simplemake mymakefiles
```

请记住一点：前面的目标将列出包含字符串 `akefile` 的文件。因此，该目标不会列出不匹配此模式的 makefile，例如 `mymake`、`mymakefile`、`yourmakefile` 等。

记住前面的示例，让我们看一个涉及编译 C 程序的 makefile 示例，下一节将对此进行讨论。

## 用于 C 程序的 Makefile

回想第 1 章包含 C 程序 `HelloWorld.c`，你使用以下命令编译它：

```
gcc HelloWorld.c -o HelloWorld
```

前面命令的等效功能涉及在 makefile 中创建一个简单目标，如清单 A.2 所示。

### 清单 A.2：Makefile

```
hello: HelloWorld.c
	gcc HelloWorld.c -o HelloWorld
```

清单 A.2 定义了目标 `hello`，但你可以使用任何方便的名称。

现在将清单 A.2 中的 Makefile 和 C 程序 `HelloWorld.c` 放在同一目录中，然后像上一节那样从命令行启动 make 工具。虽然不会显示任何输出，但你会看到二进制文件 `HelloWorld` 出现在同一目录中；启动该文件，你将看到以下输出：

```
Hello World
```

Makefile 通常包含多个目标，并且可以包含其他结构，例如宏定义，还可以引用其他 makefile。请记住，冒号右侧指定的文件是依赖项，在本例中是 `HelloWorld.c`。第二行具有基于制表符的缩进，这是 makefile 中任何目标都必需的，但在此示例中不可见。如果使用空格而不是制表符，那么调用 make 工具时将看到以下类型的错误消息：

```
Makefile1:13: *** missing separator (did you mean TAB instead of 8 spaces?). Stop.
```

这是开发人员在创建 makefile 时最常犯的错误之一。

> **注意** 规则行中的第一个字符必须是制表符。

下一节将讨论一个包含前面目标的非常简单的 makefile。

## 大 Make 与小 Make

正如你在本附录前面看到的，文件 `Makefile` 称为“大 make”，文件 `makefile` 称为“小 make”。如果在命令行输入 `make`，它将搜索“大 make”并执行该 makefile 中的第一个目标。如果“大 make”不存在，make 工具会搜索“小 make”并执行该 makefile 中的第一个目标。

例如，如果 `hello` 目标定义在 `Makefile`（如清单 A.2 中的那个）或 `makefile` 中，可以按如下方式调用该目标：

```
make hello
```

提醒一下，如果 `Makefile` 和 `makefile` 都不存在，而你调用前面的命令，则会打印以下消息：

```
make: *** No rule to make target `hello'. Stop.
```

## 带宏的 Makefile

清单 A.3 显示了 `Makefile2` 的内容，其中包含两个宏定义和三个目标，它们都会创建二进制可执行文件 `HelloWorld`。

### 清单 A.3：Makefile2

```
CC=gcc
CFLAGS=-g -Wall

hello: HelloWorld.c
	gcc HelloWorld.c -o HelloWorld

hello2: HelloWorld.c
	gcc -g -Wall HelloWorld.c -o HelloWorld

hello3: HelloWorld.c
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld
```

使用以下命令调用第一个目标：

```
make hello -f Makefile2
```

使用以下命令调用第二个目标：

```
make hello2 -f Makefile2
```

使用以下命令调用第三个目标：

```
make hello3 -f Makefile2
```

前面三个目标的结果都是创建二进制可执行文件 `HelloWorld`。但是请注意，只有 `hello3` 的规则引用了 `$(CC)`，这意味着如果你更改 `CC` 的值并运行 `hello` 目标，不会有任何变化。

如果你想知道的话，使用宏的一个优点是，你可以在一个位置替换它们的定义，而无需修改任何目标或其依赖项。例如，清单 A.3 将 `CC` 宏定义为值 `gcc`；但是，你可以将 `gcc` 替换为另一个工具，例如 `g++`（如果你的系统上有的话）。尝试进行此更改并执行与上面相同的命令：

```
make hello -f Makefile2
```

结果相同，都是创建二进制可执行文件 `HelloWorld`。

makefile 中有一些可用的标准目标，下一节将展示其中一些。

## 带标准目标的 Makefile

清单 A.4 显示了 `Makefile3` 的内容，其中包含三个宏定义和三个目标，它们都会创建二进制可执行文件 `HelloWorld`。

### 清单 A.4：Makefile3

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

#### only the 'hello' target
all: hello

# just the 'hello' target
hello: HelloWorld.c
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld

# what to remove
clean:
	$(RM) HelloWorld
```

清单 A.4 只包含目标 `hello`；目标 `hello2` 和 `hello3` 已被移除，因为它们没有任何有用的用途。

作为另一个说明，清单 A.5 显示了 `Makefile4` 的内容，它完全“泛化”了所引用的可执行文件。

### 清单 A.5：Makefile4

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm -f
MAKE=/usr/bin/make
ECHO=echo

# only the 'hello' target
all: hello

# just the 'hello' target
hello: HelloWorld.c
	$(ECHO) "Creating HelloWorld in target hello..."
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld

# what to remove
clean:
	$(RM) HelloWorld
```

清单 A.5 的开头部分包含目标中使用的所有二进制可执行文件的宏，例如 `gcc`、`rm`、`make` 和 `echo`。



checks the timestamp of a file and its dependencies in order to determine whether a target must be invoked. In addition, when dependencies are checked, updates are performed recursively.

For example, if a C source code file has a timestamp that is more recent than its corresponding executable, then the associated target in the makefile is invoked, and the associated commands are executed.

In many cases the purpose of the makefile is to create an executable, and the associated target is often the first target in the makefile. For example, if `FindMain2` is the first target in a makefile, then make will execute the commands for the target `FindMain2`.

> **注意** 默认情况下，“make”总是从 makefile 中的第一个目标运行命令，但不会运行其他目标中的任何命令。

If you do not specify the "-o" switch the compiler will create the default executable whose name is `a.out`.

In general terms, a makefile contains one or more entries, where each entry consists of the following:

- 一个目标（通常是一个文件）
- 其依赖项（目标所依赖的文件）
- 要调用的命令（基于目标和依赖项）

请记住，依赖关系是传递的。例如，如果 A 依赖于 B 而 B 依赖于 C，则 A 依赖于 C。检查你的 C 程序以确定每个文件的依赖关系，然后将适当的目标添加到你的 makefile 中。

你也可以使用 makedepend 程序，它分析 C 程序中的头文件（".h"）以确定依赖关系。

## 多个源文件和 make 工具

前几章中的 C 程序不依赖于其他 C 程序。然而，当存在对其他 C 程序（由你或其他人编写）的依赖时，你可以为这些其他 C 程序定义目标。

例如，假设 C 程序 main1.c 依赖于 C 程序 depend1.c 和 depend2.c，其内容分别显示在列表 A.6、列表 A.7 和列表 A.8 中。

https://www.thegeekstuff.com/2012/03/linux-nm-command/

### 列表 A.6：main1.c

```
#include <stdio.h>
#include "depend1.h"
#include "depend2.h"

int main()
{
    printf("Hello from main1.c\n");
    depend1();
    depend2();
    return 0;
}
```

列表 A.6 包含两个与 main1.c 位于同一目录中的 .h 文件：你可以通过包含语句使用双引号（“”）而不是尖括号（<>）来确定这一事实。接下来，main() 函数以 printf() 语句开始，然后调用 depend1() 和 depend2() 函数，这两个函数均未在此 C 程序中定义。

### 列表 A.7：depend1.c

```
#include <stdio.h>

void depend1()
{
printf("Hello from depend1.c\n");
}
```

列表 A.7 以 depend1() 函数开始，该函数包含一个 printf() 语句，显示当前文件 depend1.c 的名称。此语句的唯一目的是帮助你查看程序执行的流程。

### 列表 A.8：depend2.c

```
#include <stdio.h>

void depend2()
{
printf("Hello from depend2.c\n");
}
```

列表 A.8 以 depend2() 函数开始，该函数包含一个 printf() 语句，显示当前文件 depend2.c 的名称。此语句的唯一目的是帮助你查看程序执行的流程。

列表 A.9 显示了指定所需依赖关系的文件 Makefile5 的内容。

### 列表 A.9：Makefile5

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm -f

OBJECTS = depend1.o depend2.o
HEADERS = depend1.h depend2.h

main1: $(OBJECTS) $(HEADERS)
        $(CC) $(CFLAGS) $(OBJECTS) HelloWorld.c -o HelloWorld

depend1.o: depend1.c
        $(CC) -c depend1.c

depend2.o: depend2.c
        $(CC) -c depend2.c

clean:
        $(RM) main1 $(OBJECTS) 2>/dev/null
```

列表 A.9 包含你在之前的 makefile 中见过的几个宏，以及宏 `OBJECTS` 和 `HEADERS`，它们分别指定对象文件列表和头文件列表。

列表 A.9 的下一部分定义了目标 `main1`，它依赖于对象文件和头文件。下一对目标指定如何编译源文件 `depend1.c` 和 `depend2.c` 以分别生成对象文件 `depend1.o` 和 `depend2.o`。

最后的目标是用于“清理”文件的标准目标，在本例中为 `$(OBJECTS)` 指定的对象文件和二进制可执行文件 `main1`。请注意，如果 `depend1.c` 或 `depend2.c` 中的任何一个被修改，则该文件将被重新编译以创建相应的对象文件，而该对象文件又包含在创建二进制可执行文件 `main1` 的新版本步骤中。

按如下方式使用 `-f` 开关启动 `make` 命令：

```
make -f Makefile5
```

现在启动新创建的可执行文件：

```
./main1
```

输出如下所示：

```
Hello from main1.c
Hello from depend1.c
Hello from depend2.c
```

下一节将向你展示如何创建可以以简洁方式处理多个依赖关系的 makefile。

## 用于多个 C 文件的宏

在 [第7章](#) 中，你使用了以下命令以生成二进制可执行文件 FindMain2：

```
gcc -o FindMain2 FindChar2.c FindMain2.c
```

[列表 A.10](#) 显示了 `Makefile6` 的内容，其中 FindMain2 作为目标，当其任何依赖项被修改时就会生成。

### 列表 A.10：Makefile6

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm -f

EXEC = main1
SRC = $(EXEC).c depend1.c depend2.c
OBJ = $(SRC:.c=.o)
LIB = $(SRC:.c=.h)

all: $(EXEC)

#### this target generates main1
$(EXEC): $(OBJ)
	$(CC) -o $@ $^ $(LDFLAGS) -lm

%.o: %.c ${LIB}
	$(CC) -o $@ -c $< ${CFLAGS}

clean:
	$(RM) main1 2>/dev/null
```

> 列表 A.10 以一些熟悉的宏定义开始，然后是特定于定义这些宏的 makefile 的宏 `EXEC`、`SRC`、`OBJ` 和 `LIB`。

`OBJ` 宏包含一条规则，指定如何从 C 源文件生成对象文件 ".o"。`LIB` 宏包含一条规则，指定如何确定与 C 源文件关联的头文件。

## makefile 中的其他宏

宏是一个简单的字符串，为其分配一个值后，你就可以在 makefile 目标中使用该字符串。一般语法涉及指定名称然后为其分配值，如下所示：

```
macroname = macrovalue
```

宏与你在前几章中见过的 C 程序中的 `#define` 有些相似。每当 `make` 命令遇到宏名时，它都会用其定义的值替换宏名。事实上，本附录中的一个早期 makefile 包含简单的宏，如下所示：

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

hello: HelloWorld.c
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld
```

CFLAGS 指定编译和创建对象文件的标志

你会注意到，一旦宏被定义，就可以用它来定义后续宏。

由于本附录中的 makefile 简单且简短，使用宏的价值有限。尽管如此，养成在 makefile 中使用宏的习惯是个好主意，特别是如果它们可能变得更复杂。

### 自动变量

如果你想真正精通 make 工具，你需要学习许多在 makefile 中具有特殊意义的变量。以下是一些受支持变量的简短列表，以及它们用途的简短描述：

- $@ 是规则的目标文件名
- $% 是目标成员名：如果目标是 foo.a(bar.o)，则 $% 为 bar.o，$@ 为 foo.a。
- $< 是第一个先决条件的名字
- $? 是比目标更新的所有先决条件的名称
- $^ 是所有先决条件的名称

make 工具支持许多其他内置变量，你可以在线搜索以获取更多信息。

## 在 makefile 中创建多个可执行文件



有时你需要创建多个二进制可执行文件，而 make 工具使你能够以直接的方式指定目标。假设你需要创建三个名为 mybin1、mybin2 和 mybin3 的可执行文件，其中每个可执行文件都依赖于其关联的 C 程序以及 HelloWorld.c 程序。

清单 A.11 显示了 Makefile7 的内容，它说明了如何指定目标。

### 清单 A.11：Makefile7

```makefile
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

#### invokes targets mybin1, mybin2, and mybin3
all: mybin1 mybin2 mybin3

# 'mybin1' creates mybin1
mybin1: mybin1.o HelloWorld.o
    $(CC) $(CFLAGS) HelloWorld.c -o mybin1

# 'mybin2' creates mybin2
mybin2: mybin2.o HelloWorld.o
    $(CC) $(CFLAGS) HelloWorld.c -o mybin2

# 'mybin3' creates mybin3
mybin3: mybin3.o HelloWorld.o
    $(CC) $(CFLAGS) HelloWorld.c -o mybin3

# removes mybin1, mybin2, mybin3, and *.o files
clean:
    $(RM) mybin1 mybin2 mybin3 *.o
```

清单 A.11 以若干宏定义开头，接着是 all 目标，它指定了依赖项 mybin1、mybin2 和 mybin3，但没有命令行依赖项。因此，make 工具会尝试构建这些文件的最新版本。

## MAKEFILE 中的其他目标类型

到目前为止，示例 makefile 中的目标涉及创建目标文件或二进制可执行文件，但你也可以定义其他类型的目标。例如，清单 A.12 显示了 MakefileTar 的内容，它说明了如何创建 tar（磁带归档）文件以及提取 tar 文件的内容。

### 清单 A.12：MakefileTar

```makefile
TAR=/usr/bin/tar
CTFLAGS=-cvf
XTFLAGS=-xvf
TARFILE=mytar.tar

ctarfile:
    @echo "### Listing of C Programs:"
    @ls -l *.c
    @echo "### Creating tar file:"
    $(TAR) $(CTFLAGS) $(TARFILE) *.c

xtarfile:
    @echo "### Extracting tar file:"
    $(TAR) $(XTFLAGS) $(TARFILE)
```

清单 A.12 以若干宏定义开头，接着是两个目标。第一个目标是 ctarfile，它会显示当前目录中 C 程序的详细列表，然后用这些 C 程序创建一个 tar 文件。

第二个目标是 `xtarfile`，它将执行与 `ctarfile` 目标相反的操作：提取在 `ctarfile` 目标中创建的 tar 文件 `mytar.tar` 的内容。

调用 `ctarfile` 目标的输出如下：

```text
### Listing of C Programs:
-rw-r--r--  1 ocampesato  staff  2048 Jan 26 12:40 Hello2.c
-rw-r--r--  1 ocampesato  staff    83 Jan 19 21:30 HelloWorld.c
### Creating tar file:
/usr/bin/tar -cvf mytar.tar *.c
a Hello2.c
a HelloWorld.c
```

调用 `xtarfile` 目标的输出如下：

```text
### Extracting tar file:
/usr/bin/tar -xvf mytar.tar
x Hello2.c
x HelloWorld.c
```

## 在 MAKEFILE 中指定头文件和库

你已经看到过若干 makefile，其目标将头文件指定为依赖项。此外，你可以使用 “-I” 前缀加路径限定目录来指定头文件，如下所示：

```text
-I/usr/include
```

上一行使 `make` 工具能够在用户指定的目录中搜索头文件。

上一行中的 -I 选项实际上是由 makefile 传递给编译器的；也就是说，它并不是在命令行上传递给 make 命令的。然而，make 工具也支持 -I 选项，用于为 makefile 设置搜索路径。请注意，目录 `/usr/include` 默认已包含在内，因此没有必要指定此目录。

另一方面，假设你创建了位于 `/usr/local/include` 目录中的头文件 `mytime.h`。那么以下代码片段将使编译器能够在正确的位置找到 `mytime.h`：

```text
-I/usr/local/include
```

上一代码片段的优点是，你无需在自定义头文件或自定义 C 程序中显式引用此目录的内容。

此外，你可以使用以下开关来指示编译器在当前目录中搜索头文件：

```text
-I.
```

还有一种选项涉及指定一个目录——相对于当前目录：

```makefile
CC=gcc
IDIR =../include
CFLAGS=-I$(IDIR)
```

### 指定库

make 工具允许你通过两种方式在 makefile 中指定库。

简写方式包括：1）去掉 “lib” 前缀，2）去掉后缀，3）在执行第 1 步和第 2 步后剩余的部分前加上 “-l”（小写 l）作为前缀。

例如，如果你希望在创建可执行文件的过程中包含库 `/usr/lib/libm.a`，请指定字符串 “-lm” 以包含此库。

完成同样操作的较长方式是在编译步骤中指定库的完整路径（最好作为宏定义），如下所示：

```text
-L/usr/lib/libm.a
```

## MAKEFILE 中的虚拟目标

如果你希望执行命令而不是创建目标，可以定义一个虚拟目标，它不涉及任何文件。

makefile 中使用的一些常见虚拟目标包括：

```text
make clean
make all
```

“clean” 目标通常用于从目录中删除文件（例如目标文件和可执行文件）。删除这些文件会强制 makefile 重新编译所有 “.o” 文件。

## 在一个 MAKEFILE 中包含另一个 MAKEFILE

源代码树通常会在源代码的主目录中放置单独的 makefile，用于处理给定目录本地的依赖项。顶层 makefile 充当“主”makefile，其中包含用于创建一个或多个可执行文件的目标。

清单 A.13 显示了 `BranchMakefile` 的内容，其中包含一个目标，该目标将执行位于 branch 子目录中的 `SubBranchMakefile` 里的一个目标。

### 清单 A.13：BranchMakefile

```makefile
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm
MAKE=/usr/bin/make
BRANCH=./branch
ECHO=echo

#### only the 'hello' target
all: hello

# 'hello' creates HelloWorld
hello: HelloWorld.c
    $(ECHO) top-level directory...
    $(CC) $(CFLAGS) HelloWorld.c -o HelloWorld
    $(ECHO) going to branch...
    cd $(BRANCH); $(MAKE) -f SubBranchMakefile goodbye

# 'HelloWorld.o' creates HelloWorld.o
HelloWorld.o: HelloWorld.c
    $(CC) $(CFLAGS) -c HelloWorld.c

# removes HelloWorld and HelloWorld.o
clean:
    $(RM) HelloWorld HelloWorld.o
```

清单 A.13 以若干宏定义开头，接着是四个目标。第一个目标是 all，它依赖于目标 hello。hello 目标会打印一条语句，编译文件 HelloWorld.c 以创建 HelloWorld，然后打印另一条语句。此目标执行过程中的最后一步涉及进入一个子目录，并使用 -f 开关调用 make 工具，以指定名为 SubBranchMakefile 的 makefile 和目标 goodbye。第三个目标创建目标文件 HelloWorld.o，最后一个目标是 clean 目标，用于删除文件 HelloWorld 和 HelloWorld.o。

### 清单 A.14：SubBranchMakefile

```makefile
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

# 'goodbye' creates GoodbyeWorld
goodbye: GoodbyeWorld.c
    $(CC) $(CFLAGS) GoodbyeWorld.c -o GoodbyeWorld

# 'GoodbyeWorld.o' creates GoodbyeWorld.o
GoodbyeWorld.o: GoodbyeWorld.c
    $(CC) $(CFLAGS) -c GoodbyeWorld.c

# removes GoodbyeWorld and GoodbyeWorld.o
clean:
    $(RM) GoodbyeWorld GoodbyeWorld.o
```

清单 A.14 以若干熟悉的宏定义开头，接着是三个语法你也熟悉的目标。请注意，此 makefile 中的 `goodbye` 目标是通过清单 A.13 中 makefile 的某个目标间接调用的。

现在，在包含清单 A.13 中 `BranchMakefile` 的目录中（而*不是*从子目录中）输入以下命令：

```text
make -f BranchMakefile
```

上述命令的输出如下：

```text
echo top-level directory...
top-level directory...
gcc -g -Wall HelloWorld.c -o HelloWorld
echo going to branch...
going to branch...
cd ./branch; /usr/bin/make -f SubBranchMakefile goodbye
gcc -g -Wall GoodbyeWorld.c -o GoodbyeWorld
```




虽然前面的示例有些人为，但你可以看出如何调整 makefiles 以处理包含项目源代码的多个子目录。

## 从对象文件创建库归档

清单 A.15 显示了 `Makefile8` 的内容，该内容说明了如何创建包含位于当前目录中的一组对象文件的库。

**清单 A.15** Makefile8

```makefile
RM=/bin/rm -f
AR=/usr/bin/ar
MYLIB=mylib.a

# only the 'hello' target
all: lib

# create a library with .o files
lib: FindChar2.o FindMain2.o HelloWorld.o
	$(AR) r $(MYLIB) $?

clean:
	$(RM) $(MYLIB) 2>/dev/null
```

清单 A.15 包含熟悉的宏定义，其后是依赖于 `lib` 目标的 `all` 目标。如你所见，`lib` 目标依赖于三个对象文件，所执行的命令是 `ar` 命令，该命令使用三个对象文件更新库 `mylib.a`。

现在在命令 shell 中输入以下命令：

```sh
make -f Makefile5 lib
```

输出显示如下：

```text
/usr/bin/ar r mylib.a FindChar2.o FindMain2.o HelloWorld.o
ar: creating archive mylib.a
```

现在输入以下命令：

```sh
make -f Makefile5 clean
```

输出显示如下：

```text
/bin/rm -f mylib.a 2>/dev/null
```

## 在 Shell 脚本中创建归档库

你也可以使用 shell 脚本 createlib.sh 来创建包含当前目录中所有对象文件的库，如下所示：

```sh
mylib2="mylib2.a"
```

```sh
for f in `ls *.o`
do
    echo "Adding object file $f"
    ar r $mylib2 $f
done
```

打开一个命令 shell，导航到 createlib.sh 的位置，并输入以下命令：

```sh
chmod +x createlib.sh
./createlib.sh
```

输出显示如下：

```text
Adding object file FindChar2.o
ar: creating archive mylib2.a
Adding object file FindMain2.o
Adding object file HelloWorld.o
```

## 摘要

本附录向你介绍了 make 工具以及如何使用该工具为你的 C 程序自动化编译相关步骤。你看到了如何使用 Unix 命令来管理对象文件和库，例如 `ar` 命令和 `ranlib` 命令。然后你学习了 `nm` 命令以检查对象文件和归档库的内容。

接下来，你看到了如何在 Makefile 中创建简单目标以及如何在 Makefile 中使用宏。此外，你还学习了如何在 Makefile 中指定头文件和库文件，以及如何在 Makefile 中调用 make 工具。最后，你学习了如何创建用于创建归档库的 shell 脚本。

## 索引

### A

- add() 函数, 158
- 美国国家标准学会 (ANSI), 5, 45
- 算术运算符, 16–17, 28–29
- 数组, 55–80, 90–91, 147
  - 地址和指针, 116–117
  - 计算方阵的转置, 65–66
  - 统计一行文本中的单词数, 72–73
  - 从中删除元素, 69–70
  - 查找其中的最大值和最小值, 68–69
  - 不规则的, 145–147
  - 在其中进行线性搜索, 66–67
  - 多维的, 63–65
  - 在其中进行数字反转, 67–68
  - 将一维数组作为参数传递, 90–91
  - 指针和, 114–115
  - 字符串和 for, 70–71
  - Switch 语句, 75–76
  - 使用 while 循环查找数字的除数, 78–79
  - 工作于, 61–63
    - C 函数和, 63
    - 值, 62
    - 初始化, 62
  - 使用字符串工作, 77
  - 使用数字工作, 76
- asprintf() 函数, 138

### B

- Bell Labs, 5
- 冒泡排序算法, 168–169

### C

- calloc() 函数, 144
- C 数组, 23–24
  - 在其中添加数字, 23–24
- C 函数, 81–102
  - 内置函数, 81–83
    - 在数据类型之间转换, 83
    - 带描述的函数, 82–83
    - 按引用传递与按值传递, 82
  - 用户定义函数的 C99 语法, 85–86
  - 将字符串转换为整数和浮点值, 87–88
  - 定义自定义函数, 83–84
    - 函数原型, 84
  - 显示素数列表, 93–94
  - 其中的函数参数, 84–85
  - K&R 风格, 86–87
- 命令行, 2–5, 47–50
  - 其中的参数, 112–113
  - 与 lint 相关的实用程序（可选）, 4
  - 从中读取格式化的行, 49–50
  - 从中读取单个字符, 47
  - 从中读取整行, 74–75
  - 从中读取未格式化的行, 47–48
  - 从中读取多个字符串, 51–52
  - 工具, 2–5, 47–50
  - gcc 编译器, 2–3
  - gcc 命令的有用开关（可选）, 3–4
  - 编辑器和 IDE, 4–5
- 条件逻辑, 1, 25–54
  - 算术运算符和, 28–29
  - C 程序中的注释, 25–26
  - 复合 if-else 语句, 29
    - 排名数字, 31
    - 短路, 30–31
  - 与之相关的逻辑错误, 27–28
  - 简单的, 26
- C 程序, 1–24, 164–165, 182–185
  - 绝对值计算, 20
  - 一个 hello world 程序, 8–10
    - C 头文件和库, 9
    - 语法, 10
    - main() 函数的有效语法, 9–10
  - 高层次视图, 7–8
    - 编码准则, 7–8
    - 其中的关键字, 8
    - 其结构, 7
  - 向上取整计算和向下取整值, 19–20
  - 其中的 Char 类型, 22–23
  - 编译, 10–11
  - 其中的数据类型, 15–16
    - 其中的 sizeof() 运算符, 15
  - 其中的不同进制, 21–22
  - 显示其中的环境变量, 182–183
  - 其中的函数, 81–102
  - 缩进和代码格式, 13
  - 其中的运算符, 16–19, 165–168
    - 算术, 16–17
    - 增量/减量, 17–18
    - 三元, 18–19
  - 设置其中的环境变量, 183–184
  - 其中的单链表, 177–178
  - 其中的存储类说明符, 185
  - printf() 函数, 14–15
    - 三角函数值计算, 21
  - 其中的联合体, 178–180
  - 变量名, 12
    - 赋值语句, 12
  - 什么是 C, 5–7
    - 重大修订, 6
    - 其特别之处, 5–6
  - 使用宏工作, 164–165
- C 结构体, 169–171, 179–182
  - 一个示例, 170
  - 其数组, 173–175
  - 其中的位域, 181–182
  - 组合联合体和, 179–181
  - 嵌套的, 172–173
- cubed() 函数, 159
- 多个文件中的自定义函数, 190–192
- C++, 5
  - 用途, 6
- C11 合规性, 43–45
  - 检查, 44
  - fgets() 函数, 45–46
  - gets() 函数, 46–47
  - 关于, 45
- C99 ISO 标准, 6
  - 特性, 6–7

### E

- 错误处理, 186–188
  - 如何从错误中退出, 187–188
  - errno 全局变量, 186
  - perror() 和 strerror() 函数, 186–187

### F

- free() 函数, 144

### I

- If 语句, 32
  - 顺序的, 32
- if-else 语句, 29
  - 嵌套的, 33
  - 使用其排名数字, 31–32
- 国际标准化组织 (ISO), 5
- C 简介, 1–24
  - 命令行工具, 2–5
  - 什么是 C, 5–7

### K

- Kanji, 153

### L

- localtime() 函数, 176
- 循环, 55–80
  - 检查字母类型, 58–59
  - 检查字符类型, 60–61
  - 检查闰年, 57–58
  - 统计小写和大写字符, 59–60
  - Do-while, 55, 147
  - 使用 while 循环查找素数, 79–80
  - While, 80, 115
  - 使用 while 工作, 74
    - 在 for 中使用 break 和 continue 工作, 56
    - 使用 for 工作, 55–56
  - 使用嵌套 for 工作, 73

### M

- Make 工具, 195–214
  - 大 make 和小 make, 200–202
    - 带宏的 Makefile, 201–202
  - Makefile 的命令行开关, 203
  - 在 shell 脚本中创建归档库, 214
  - 从对象文件创建库归档, 213–214
  - 在 makefile 中创建多个可执行文件, 208–209
  - makefile 中的虚拟目标, 211
  - makefile 中的头文件和库, 210–211
    - 指定库, 211
  - makefiles 如何工作, 203–204
  - 在另一个 makefile 中包含 makefile, 211–213
  - 多个文件的宏, 206–207
  - C 程序的 Makefile, 199–200
  - 带标准目标的 Makefile, 202
  - 多个源文件, 204–206
  - 其中的其他宏, 207–208
    - 自动变量, 208
  - 一些简单的 makefiles, 198–199
  - makefile 中的目标, 209–210
  - 用于库的 Unix 命令, 196–198
    - ar 命令的示例, 197
    - nm 命令, 197–198
    - ranlib 命令, 197
  - 什么是, 195–196
    - Makefile 中有什么, 196
- main() 函数, 133





### M

- malloc() 函数，144–145
- 数学量，2

### O

- C 语言中的运算符，165–168
  - 按位运算符，165
  - 逻辑运算符，166
  - 逗号运算符，166
  - 综合代码示例，166–168

### P

- 指针运算，117–118
- 指针，103–127, 185–186
  - 地址与数组，116–117
  - 数组与指针，114–115
  - 内置字符串处理函数，120–121
  - 计算方阵的转置，118–119
  - 字符串，109–111
  - 连接两个字符串，126–127
  - 统计文本字符串中的元音和辅音，122–124
  - 在文本字符串中查找单词，124–125
  - 递增（内存位置与值），113–114
  - 整型变量，106–109
  - 在文本字符串中搜索单词，125–126
  - 字符串与指针，119–120
  - while 循环与字符串，121–122
  - 什么是指针，103–106
    - const，106
    - 简单示例，104
  - 使用指针编写复杂代码，185–186
- 指针（使用），129–161
  - 数字循环，136–137
  - 参数，158–160
  - 十进制数组与指针，141–142
  - 数字数组，138–139
  - 反转数组，142–144
  - 指针数组，139–140
  - 在 C 中比较两个字符串，129–130
  - 查找大写和小写字母，150–152
  - 函数与指针，140
  - void 类型函数，156–157
  - 循环与一个数的约数，137–138
  - 内存分配函数，144
  - 非 void 函数，157–158
  - 按指针传递数组，135–136
  - 按引用传递与按值传递，133–134
  - 指向指针的指针，160–161
  - 字符串与字符计数，153–156
  - 字符串与回文，132–133
  - 使用 strtok() 将字符串分词，131–132
- printf() 函数，14–15, 146

### R

- 递归，95–102
  - 阶乘值，95–96
  - 用递归计算斐波那契数列，96–97
  - 用递归计算两个数的最大公约数，99–100
  - 用递归计算两个数的最小公倍数，101–102
  - 一个数的位数，98–99
  - 用递归计算一个数的幂，97–98
  - 用递归计算一个数的各位数字之和，99
- 里奇，丹尼斯，5
- 常规任务，1, 25–54

### S

- scanf() 函数，50–51
- strcmp() 函数，129–130
- strtok() 函数，131–132
- 标准头文件，192–193
  - 常用标准头文件，193
- 标准头文件库，193
- 字符串，38
  - 转换为十进制值，92–93
  - 显示字符串的子串，111–112
  - 在字符串中查找字符，91–92
  - 相关函数，38–41
  - 移除字符串中的空白字符，152–153
  - 反转字符串，149–150
  - 大写和小写，148–149
- strcpy() 和 strncpy() 函数，37–41
- 短路求值，30–31
- sprintf() 函数，88–90
  - 缓冲区操作函数，89–90
- squared() 函数，159
- strftime() 和 strptime() 函数处理日期（可选），175–177
- strnicmp() 函数，129
- switch 语句，75–76
- 符号常量，163–164
- 系统调用，188–190
  - 删除文件，188–189
  - 列出目录中的文件，189–190

### T

- test() 函数，140
- toupper() 和 tolower() 函数，148
- 类型转换，35–37
  - 整型提升，36–37

### U

- 用户输入，41–42
  - 数值计算，52–54
    - 标准输入（stdin），54
    - 标准输出（stdout），54
    - 标准错误（stderr），54
  - 指针与用户输入，147–148
    - 堆与栈，148
  - getchar() 和 putchar() 函数：单字符函数，41
  - scanf() 和 printf() 函数：多字符函数，41–42

### V

- 变量，34
  - 全局变量，34
  - 局部变量与全局变量，34–35
  - C 语言中的作用域，34

