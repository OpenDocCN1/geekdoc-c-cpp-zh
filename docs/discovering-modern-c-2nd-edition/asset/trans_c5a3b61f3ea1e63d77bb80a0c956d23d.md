

## 为宏使用 `LONG_AND_UGLY_NAMES_IN_CAPITALS`！

- 从技术上讲，宏来自 Windows.h 而非 Visual Studio 本身，但一旦我们为此惹上麻烦，这种区别就只起很小的作用，而且这种情况并不罕见，因为这个头文件被频繁使用。

宏几乎可以以各种可想象和不可想象的方式制造奇怪的问题。为了让你大致了解，我们将在附录 A.2.9 中查看一些示例，并提供一些处理它们的技巧。请随时推迟阅读，直到你遇到问题。

## 宏的使用

尽可能用其他语言特性替换每个宏，只有在别无他法时才使用宏。

如你在本书中将看到的，C++ 提供了更好的替代方案，例如常量、`inline` 函数、模板和 `constexpr`。

## 1.9.2.2 包含

为了保持 C 语言的简单性，许多诸如 I/O 之类的特性被排除在核心语言之外，转而由库来实现。C++ 遵循这种设计，尽可能通过标准库来实现新特性，然而却没有人会称 C++ 为一种简单的语言。

因此，几乎每个程序都需要包含一个或多个头文件。最常见的是用于 I/O 的头文件，如前面所示：

```
#include <iostream>
```

预处理器在类 Unix 系统的标准包含目录（如 `/usr/include` 和 `/usr/local/include`）中搜索该文件。我们可以使用编译器标志向此搜索路径添加更多目录——在 Unix/Linux/Mac OS 世界中通常是 `-I`，在 Windows 中是 `/I`。

当我们在双引号内写文件名时，例如：

```
#include "herberts_math_functions.hpp"
```

编译器通常首先在当前目录中搜索，然后在标准路径中搜索。这等同于使用尖括号引用并将当前目录添加到搜索路径。有些人认为尖括号应仅用于系统头文件，而用户头文件应使用双引号（但我们不同意他们的观点）。

- 然而，使用双引号文件名时搜索哪些目录取决于实现，标准未作规定。

为了避免名称冲突，通常会将包含文件的父目录添加到搜索路径中，并在指令中使用相对路径：

点击此处查看代码图像

```
#include "herberts_includes/math_functions.hpp"
#include <another_project/math_functions.h>
```

斜杠具有可移植性，在 Windows 下也可用（在 Windows 中，常规斜杠和反斜杠都可用于子目录）。

-**包含保护：** 由于间接包含，频繁使用的头文件可能在一个源文件中被多次包含。为了避免禁止的重复并限制文本扩展，所谓的*包含保护*确保仅执行第一次包含。这些保护是普通宏，用于声明某个文件的包含。典型的包含文件如下所示：

点击此处查看代码图像

```
// Author: me
// License: Pay me $100 every time you read this

#ifndef HERBERTS_MATH_FUNCTIONS_INCLUDE
#define HERBERTS_MATH_FUNCTIONS_INCLUDE

#include <cmath>

double sine(double x);
...

#endif // HERBERTS_MATH_FUNCTIONS_INCLUDE
```

因此，仅当保护尚未定义时才包含文件的内容。在内容中，我们定义保护以抑制进一步的包含。

与所有宏一样，我们必须密切关注名称的唯一性，不仅在我们的项目中，而且在我们直接或间接包含的所有其他头文件中也是如此。理想情况下，名称应代表项目和文件名。它还可以包含项目相对路径或命名空间（第 3.2.1 节）。通常的做法是以 _INCLUDE 或 _HEADER 结尾。

意外重用保护可能会产生多种不同的错误消息。根据我们的经验，发现该问题的根源可能需要非常长的时间。高级开发人员会根据上述信息或使用随机生成器自动生成它们。

一个方便的替代方案是 #pragma once。前面的示例简化为：

点击此处查看代码图像

```
// Author: me
// License: Pay me $100 every time you read this

#pragma once

#include <cmath>

double sine(double x);

...
```

Pragma 是编译器特定的扩展，这就是为什么我们不能指望它们具有可移植性。然而，#pragma once 得到所有主要编译器的支持，并且无疑是可移植性最高的 pragma。除了更简短的表示法外，我们还可以将避免重复包含的责任委托给编译器。

在文件中组织代码的高级技术是通过 C++20 中的模块引入的。我们将在第 7.3 节中介绍它们。

## 1.9.2.3 条件编译

预处理器指令的一个重要且必要的用途是控制条件编译。预处理器提供 #if、#else、#elif 和 #endif 指令用于分支。条件可以是比较、定义检查或其逻辑表达式。指令 #ifdef 和 #ifndef 分别是以下内容的快捷方式：

```
#if defined(MACRO_NAME)

#if !defined(MACRO_NAME)
```

当定义检查与其他条件组合时，必须使用长形式。同样，#elif 是 #else 和 #if 的快捷方式。

在理想世界中，我们只会编写可移植的标准合规 C++ 程序。在现实中，我们有时不得不使用不可移植的库。假设我们有一个仅在 Windows 上可用的库，更准确地说是仅在 Visual Studio 上可用（其中宏 _MSC_VER 预定义）。对于所有其他相关编译器，我们都有一个替代库。平台相关实现的最简单方法是为不同的编译器提供替代代码片段：

```
#ifdef _MSC_VER
... Windows code
#else
... Linux/Unix code
#endif
```

同样，当我们想要使用在所有目标平台上都不可用的新语言特性时，也需要条件编译，例如模块（第 7.3 节）：

点击此处查看代码图像

```
#ifdef MY_LIBRARY_WITH_MODULES
... well-structured library as modules
#else
... portable library in old-fashioned way
#endif
```

在这里，我们可以在特性可用时使用它，同时仍然保持对不支持该特性的编译器的可移植性。当然，我们需要可靠的工具，仅在特性确实可用时才定义宏。

C++20。或者，我们可以依赖编译器开发者对该特性是否得到适当支持的看法。为此，C++20 为自 C++11 以来引入的每个特性引入了一个宏——例如，用于模块支持的 __cpp_modules——因此我们的示例现在读取为：

点击此处查看代码图像

```
#ifdef __cpp_modules
... well-structured library as modules
#else
... portable library in old-fashioned way
#endif
```

该宏的值是该特性添加到标准（草案）中的年份和月份。对于不断发展的核心语言和库特性，这使我们能够找出实际支持的版本。例如，<chrono> 库（第 4.5 节）随着时间的推移而发展，要检查其 C++20 功能是否在我们的系统上可用，可以使用 __cpp_lib_chrono 的值：

```
#if __cpp_lib_chrono >= 201907L
```

条件编译功能非常强大，但代价是：源代码的维护和测试更加费力且容易出错。这些缺点可以通过设计良好的封装来减轻，以便不同的实现通过通用接口使用。

## 1.9.2.4 可嵌套注释

指令 #if 可用于注释掉代码块：

点击此处查看代码图像

```
#if 0
... Here we wrote pretty evil code! One day we will fix
it. Seriously.
#endif
```

相对于 /* ... */ 的优势在于它可以嵌套：

点击此处查看代码图像

```
#if 0
... Here the nonsense begins.
#if 0
... Here we have nonsense within nonsense.
#endif
... The finale of our nonsense. (Fortunately ignored.)
#endif
```

尽管如此，这种技术应适度使用：如果四分之三的程序都是注释，我们应该考虑进行严重的修订。

更多详情：在附录 A.3 中，我们展示了一个现实世界示例，回顾了本章的许多特性。我们没有将其包含在主阅读轨道中，以便为不耐烦的读者保持快节奏。对于

