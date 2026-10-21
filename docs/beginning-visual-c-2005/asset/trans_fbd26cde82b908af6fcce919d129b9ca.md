

你也可以为 std 添加一个 using 指令，这样就不需要限定标准库名称了，但这违背了命名空间的初衷。一般来说，如果你在程序中使用命名空间，就不应该在程序各处添加 using 指令；否则，你一开始就没必要使用命名空间。话虽如此，为了让代码更简洁、更易于阅读，我们将在所有示例中为 std 添加一个 using 指令。当你开始学习一种新的编程语言时，你可以不需要这些冗余，无论它们在实践中多么有用。

## 多个命名空间

一个真实世界的程序很可能涉及多个命名空间。你可以对给定名称的命名空间进行多次声明，并且所有具有给定名称的命名空间块的内容都在同一个命名空间中。例如，你可能有一个包含两个命名空间的程序文件：

```
namespace sortStuff
{
    // Everything in here is within sortStuff namespace
}
```

```
namespace calculateStuff
{
    // Everything in here is within calculateStuff namespace
    // To refer to names from sortStuff they must be qualified
}
```

```
namespace sortStuff
{
    // This is a continuation of the namespace sortStuff
    // so from here you can refer to names in the first sortStuff namespace
    // without qualifying the names
}
```

对给定名称的命名空间的第二次声明只是对第一次的延续，因此你可以从第二个命名空间块中引用第一个命名空间块中的名称，而无需限定它们。它们都在同一个命名空间中。当然，你通常不会故意以这种方式组织源文件，但在使用包含到程序中的头文件时，它可能会自然地出现。例如，你可能有这样的情况：

```
#include <iostream>      // Contents are in namespace std
#include "myheader.h"      // Contents are in namespace myStuff
#include <string>           // Contents are in namespace std

// and so on...
```

这里，<iostream> 和 string 是 ISO/ANSI C++ 标准库头文件，而 myheader.h 代表包含我们程序代码的头文件。你对命名空间的情况与之前的插图完全平行。

这给了你一个关于命名空间如何工作的基本概念。命名空间比我在这里讨论的要多得多，但如果你掌握了这一部分，你应该能够在需要时毫无困难地了解更多。

请注意，前一段代码片段中的两种 #include 指令形式会导致编译器以不同的方式搜索文件。当你将要包含的文件指定在尖括号之间时，你是在指示编译器沿着 /I 编译器选项指定的路径搜索文件，如果失败则沿着 INCLUDE 环境变量指定的路径搜索。这些路径定位 C++ 库文件，这就是为什么这种形式保留给库头文件的原因。INCLUDE 环境变量指向存放库头的文件夹，而 /I 选项允许指定包含库头的额外目录。当文件名在双引号之间时，编译器将搜索包含 #include 指令的文件所在的文件夹。如果找不到文件，它将搜索包含当前文件的任何目录。如果仍然找不到文件，它将搜索库目录。

## C++/CLI 编程

C++/CLI 为我到目前为止在本章中讨论的内容提供了许多扩展和额外功能。我将首先在进入细节之前总结这些额外功能。额外的 C++/CLI 功能是：

- 所有 ISO/ANSI 基本数据类型都可以在 C++/CLI 程序中使用，正如我所描述的那样，但在某些上下文中它们具有一些额外的属性，我将对此进行说明。
- C++/CLI 为控制台程序中的命令行提供了自己的键盘输入和输出机制。
- C++/CLI 引入了 safe_cast 运算符，可确保类型转换操作生成可验证的代码。
- C++/CLI 提供了基于类的替代枚举功能，其灵活性比你见过的 ISO/ANSI C++ enum 声明更高。

你将在第 4 章开始学习 CLR 引用类类型，但由于我已经为原生 C++ 引入了全局变量，我现在要提到，CLR 引用类类型的变量不能是全局变量。

我将首先从 C++/CLI 中的基本数据类型开始。

## C++/CLI 特定：基本数据类型

你可以在 C++/CLI 程序中使用 ISO/ANSI C++ 基本数据类型名称，并且在算术运算中它们的工作方式与你在原生 C++ 中看到的完全相同。此外 C++/CLI 定义了两种额外的整数类型：

| Type | Bytes | Range of Values |
|---|---|---|
| long long | 8 | From 9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| unsigned long long | 8 | From 0 to 18,446,744,073,709,551,615 |

## 第 2 章

要指定 long long 类型的字面量，你在整数值后附加 LL 或小写 ll。例如：

```
long long big = 123456789LL;
```

unsigned long long 类型的字面量，你在整数值后附加 ULL 或 ull：

```
unsigned long long huge = 999999999999999ULL;
```

虽然所有基本类型的所有操作在 C++/CLI 中以相同的方式工作，但在 C++/CLI 程序中，基本类型名称具有不同的含义，并在某些情况下引入了额外的功能。C++/CLI 程序中的基本类型是值类类型，可以根据需要表现得像普通值或像对象。

在 C++/CLI 语言内部，每个 ISO/ANSI 基本类型名称都映射到 System 命名空间中定义的值类类型。因此，在 C++/CLI 程序中，ISO/ANSI 基本类型名称是其关联值类类型的简写。这使得基本类型的值可以简单地作为值处理，或在必要时自动转换为其关联值类类型的对象。基本类型、它们占用的内存以及相应的值类类型显示在下表中：

| Fundamental Type | Size(bytes) | CLI Value Class |
| --- | --- | --- |
| bool | 1 | System::Boolean |
| char | 1 | System::SByte |
| signed char | 1 | System::SByte |
| unsigned char | 1 | System::Byte |
| short | 2 | System::Int16 |
| unsigned short | 2 | System::UInt16 |
| int | 4 | System::Int32 |
| unsigned int | 4 | System::UInt32 |
| long | 4 | System::Int32 |
| unsigned long | 4 | System::UInt32 |
| long long | 8 | System::Int64 |
| unsigned long long | 8 | System::UInt64 |
| float | 4 | System::Single |
| double | 8 | System::Double |
| long double | 8 | System::Double |
| wchar_t | 2 | System::Char |

默认情况下，类型 char 等同于 signed char，因此关联的值类类型是 System::SByte。请注意，你可以通过设置编译器选项 /J 将 char 的默认值更改为 unsigned char，在这种情况下，关联的值类类型将为 System::Byte。System 是定义 C++/CLI 值类类型的根命名空间名称。System 命名空间中定义了许多其他类型，例如用于表示字符串的类型 String，你将在第 4 章中遇到。C++/CLI 还在 System 命名空间中定义了 System::Decimal 值类类型，Decimal 类型的变量存储具有 28 位十进制数字精度的精确十进制值。

正如我所说，每个基本类型名称关联的值类类型为此类变量在 C++/CLI 中添加了重要的额外功能。根据需要，编译器将安排从原始值到关联类类型的自动转换，反之亦然；这些过程分别称为装箱和拆箱。这允许任何这些类型的变量根据情况表现得像简单值或像对象。你将在第 6 章中了解何时以及如何发生这种情况。

由于 ISO/ANSI C++ 基本类型名称是 C++/CLI 程序中值类类型名称的别名，原则上你可以在 C++/CLI 代码中使用两者。例如，你已经知道可以这样编写创建整数和浮点变量的语句：

```
int count = 10;
double value = 2.5;
```

你可以使用与基本类型名称相对应的值类名称，程序也可以毫无问题地编译，像这样：

```
System::Int32 count = 10;
System::Double value = 2.5;
```

虽然这是完全合法的，但你应该在代码中使用 int 和 double 等基本类型名称，而不是 System::Int32 和 System::Double 等值类名称。原因是，我所描述的基本类型名称与值类类型的映射适用于 Visual C++ 2005 编译器；其他编译器不必实现相同的映射。基本类型名称由 C++/CLI 语言标准固定，但对于大多数类型，映射到值类类型是实现相关的。Visual C++ 2005 中的类型 long 映射到类型 Int32，但它完全可能在某些其他实现中映射到类型 Int64。

将基本类型的数据表示为值类类型的对象是 C++/CLI 的一个重要特性。在 ISO/ANSI C++ 中，基本类型和类类型是完全不同的，而在 C++/CLR 中，所有数据都存储为类类型的对象，要么是值类类型，要么是引用类类型。你将在第 7 章学习引用类类型。

接下来，你将尝试一个 CLR 控制台程序。

## 试一试  一个水果 CLR 控制台程序

创建一个新项目并选择项目类型为 CLR，模板为 CLR 控制台应用程序。然后你可以将项目名称输入为 Ex2_12，如图 2-13 所示。

