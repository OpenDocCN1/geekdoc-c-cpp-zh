
最后这条消息不是程序产生的结果。它是 Visual Studio 的提醒，说明我们的程序已完成执行，并留给我们时间查看结果。如果我们只按 `[F5]` 运行程序，该消息将不会出现，结果将在出现后立即消失，因为程序将完成执行，窗口将关闭。这就是为什么我们总是通过按下 `[Ctrl+F5]` 来启动控制台应用程序。

并不是所有项目类型都可以执行。为了执行 C# 项目，它需要有一个按照本章前面描述的方式声明 `Main()` 方法的类。

## 调试程序

当我们的程序包含错误（也称为 bug）时，我们必须找到并删除它们，即需要调试程序。调试过程包括：

- 注意到问题（bug）；
- 找到导致问题的代码；
- 修复代码使程序能够正常运行；
- 测试以确保在更改后程序按预期工作。

该过程可以重复多次，直到程序开始正常工作。在我们发现问题后，我们需要找到导致问题的代码。Visual Studio 可以帮助我们，允许我们逐步检查它是否按计划运行。

为了在指定位置停止程序执行，我们可以放置断点。断点与某行代码关联，程序会停止执行。每一步都允许我们检查值。调试让我们有机会了解错误发生何处。

一旦我们确切知道问题在哪里，就可以很容易地纠正它。要这样做，首先需要在程序完成之前停止程序。我们选择 `调试（Debug）` -> `停止调试（Stop Debugging）` 或 `[Shift+F5]`。

这就是为什么我们总是通过按下 `[Ctrl+F5]` 来启动控制台应用程序。

让我们在程序中故意创建一个错误来来说明它是如何工作的：

| HelloCSharp.cs |
| :--- |
| class HelloCSharp { |
| static void Main(string[] args) { |
| Console.WriteLine("Hello World!"); |
| throw new System.NotImplementedException("This is an intentional error."); |
| } |
| } |

等等，上面的 OCR 文本乱码了。让我们根据提供的逻辑和视觉上下文正确重构代码：

```csharp
class HelloCSharp
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
        throw new System.NotImplementedException("This is an intentional error.");
    }
}
```

实际上，让我遵循“保留原始语言和所有信息，不要删除或总结”的指令来修复损坏的 OCR……OCR 文本显示：“class HelloCSharp... static void Main... Console.WriteLine("Hello World!"); throw new System.NotImplementedException("This is an intentional error.");"。

以下是根据 OCR 流程修正后的代码：

```csharp
class HelloCSharp
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
        throw new System.NotImplementedException("This is an intentional error.");
    }
}
```

等等，提示说“如果出现表格形式的文本，将其转换为 Markdown 表格”。第 101 页上的 OCR 文本是交织文本的混乱。让我们按照要求提供清晰的文本版本。

# 第 1 章 编程简介

- 我们想要检查一个给算法是如何实现的，但我们没有源代码，例如为了检查 `Array.Sort()` 在内部是如何工作的。
- 在使用某些 .NET 库时有很多选择，我们想要找到最佳选择。我们想查看如何使用某些 API 并深入研究它使用的某些编译代码。
- 我们没有关于某个库如何工作的信息，但我们有使用它的编译代码（.NET 程序集），我们想确切找出该库是如何工作的。
- 我们丢失了源代码并想要将其恢复。从反编译中恢复代码会导致变量名、注释、格式等的丢失，但总比没有要强。

反编译是借助工具的帮助完成的，这些工具不是 Visual Studio 的标准部分。第一个流行的 .NET 反编译器是 Red Gate 的 Reflector（在 2011 年初商业化之前）。

Telerik 提供了一个非常优秀且完全免费的 .NET 反编译器，名为 JustDecompile。它可以从公司网站下载：`http://www.telerik.com/products/decompiler.aspx`。JustDecompile 允许直接在 Visual Studio 中进行反编译，并提供了一个外部独立的 GUI 应用程序用于浏览和反编译你需要的内容。

## JustDecompile - DefaultAssemblyList

```c
public void WriteLine(string value)
{
    if (value == null)
    {
        int length = this.CoreNewLine.Length;
        int num = this.CoreNewLine.Length;
        char[] coreNewLine = new char[length + num];
        value.CopyTo(coreNewLine, 0, length);
        if (num == 1)
        {
            Buffer.InternalCopy(this.CoreNewLine, 0, coreNewLine, 0, length);
        }
        else
        {
            coreNewLine[length] = this.CoreNewLine;
            coreNewLine[length + 1] = this.CoreNewLine;
            this.Write(coreNewLine, 0, length + num);
        }
    }
}
```

# C# 编程基础

另一个良好的 .NET 反编译工具是 ILSpy，它是基于 SharpDevelop 项目开发的。可以在 `http://ilspy.net` 下载。该程序不需要安装。启动后，ILSpy 会加载一些标准的 .NET 库。通过 `File -> Open` 菜单，我们可以打开 .NET 程序集。我们也可以从 GAC（全局程序集缓存）组装。ILSpy 看起来像这样：![](img/251ffe9d2b15f8a5624bb12_105.png)

在 ILSpy 中有两种方法可以找到方法的实现。例如，如果我们想查看 `System.Decimal` 方法是如何工作的，首先使用左侧的树找到 `System` 命名空间，最后选择 `Decimal` 方法。点击任何方法，我们都能看到它的 C# 源代码。另一种寻找类的方法是使用 ILSpy 中的搜索引擎。它可以从加载的程序集中搜索所有类、方法、属性等。遗憾的是，本书编写时的 ILSpy 2.1 版本只能反编译 C#、VB.NET 和 IL。

JustDecompile 和 ILSpy 是非常有用的工具，在开发 .NET 软件时每天都能提供帮助。当我们好奇某个方法如何工作或在某个程序集中如何实现时，我们总是可以通过反编译器来找出。

# 第 1 章 编程简介

## Linux、iOS 和 Android 的 C#

与 Windows 相比，Linux 下的 C# 编程并不发达。我们不想完全跳过它，所以将提供一些在 Linux、iOS 和 Android 上开始 C# 编程的指南。

在 Linux 上编写 C# 代码最重要的就是 .NET Framework 实现。Microsoft .NET Framework 不支持 Linux，但有一个名为“Mono”的开源 .NET 实现。我们可以在官方网站下载 Mono：`http://www.mono-project.com`。Mono 允许我们在 Linux 环境和其他操作系统编译并运行 C# 程序。它包含了 C# 编译器、CLR、垃圾回收器以及 Windows Forms 和 ASP.NET 可用的标准 .NET 库。

Mono 不仅支持 Linux，还支持 Solaris、Mac OS X、iOS（iPhone / iPad）和 Android。iOS 版本（MonoTouch）和 Android 版本（Mono Android）是商业项目，而 Mono for Linux 是开源软件。

当然，Visual Studio 在 Linux 环境下运行，但可以使用 MonoDevelop 作为 Linux 中的 C# IDE。

## 其他 .NET 语言

C# 是最流行的 .NET 语言，但还有其他可以编写 .NET 程序的语言：

- **VB.NET** - Visual Basic (VB) 是适配 .NET Framework 的 Basic 语言。它被认为是 Microsoft Visual Basic 6（Windows 3.1 和 Windows 95 的旧开发环境）的继任者。对于 C# 开发者来说它的语法很奇怪，但通常与 C# 相同，只是语法不同。VB.NET 存在的唯一原因是：
- **Managed C++** - C++ 对 .NET Framework 的适配。
- **F#** - 在 .NET Framework 中进行函数式编程的实验。
- **JavaScript** - 可用于开发 Windows 8 应用。

# C# 编程基础

## 练习

- 1. 安装并熟悉 Microsoft Visual Studio 和 Microsoft Developer Network (MSDN) 库。
- 2. 在标准 .NET 文档查找 `System.Console` 的描述。
- 3. 在 MSDN 库查找 `System.Console.WriteLine()` 方法及其不同的可能参数。
- 4. 使用命令行（控制台）和 Visual Studio 编译并执行本章的示例程序。
- 5. 修改示例程序以打印不同的问候，例如“Good Day!”。
- 6. 编写控制台应用程序，在控制台上打印你的姓。
- 7. 编写一个程序，在控制台上打印以下数字：1、101、1001，每个数字占一行。
- 8. 编写一个程序，在控制台上打印当前日期和时间。
- 9. 编写一个程序，打印 12345 的平方根。
- 10. 编写一个程序，打印序列 2, 3, 4, -5, 6, -7, 8 的前 100 个成员。
- 11. 编写一个程序，从控制台读取你的年龄并打印10 年后的年龄。
- 12. 描述 C# 和 .NET Framework 之间的差异。
- 13. 列出其他流行的语言列表。它们与 C# 有何不同？
- 14. 反编译练习 5 中的示例程序。

## 答案与指南

- 1. 如果你有 DreamSpark 账户（`www.dreamspark.com`），或者你的学校或大学提供微软产品的免费访问权限，请安装完整版 Visual Studio。如果你没有机会使用完整版 Microsoft Visual Studio，可以从微软网站下载 Visual Studio Express；它是免费的且适用于教学目的。
- 2. 使用本章 .NET 文档章节中提供的地址。打开它并在左侧树中搜索。使用 Google 搜索同样有效，通常查找特定 .NET 类的文档最快。
- 3. 使用与上一个练习相同的方法。

# 第 1 章 编程导论

- 4. 遵循“编译和执行 C# 程序”章节中的说明。
- 5. 使用本章中的 C# 示例程序代码，并更改打印的消息。
- 6. 查找如何使用 `System.Console.Write()` 方法。
- 7. 使用 `System.Console.WriteLine()` 方法。
- 8. 查找 `System.DateTime` 类提供的功能。
- 9. 查找 `System.Math` 类提供的功能。
- 10. 尝试自己学习如何在 C# 中学习循环。你可以阅读“循环”章节中关于 `for` 循环的内容。
- 11. 使用 `System.Console.ReadLine()`、`int.Parse()` 和 `System.DateTime.AddYears()` 方法。
- 12. 在网上（例如维基百科）研究它们，并仔细观察它们之间的区别。你会发现 C# 是一种编程语言，而 .NET Framework 是 .NET 的开发平台和运行时。务必阅读本章的“C# 语言与 .NET 平台”章节。
- 13. 找出哪些是最流行的语言并检查用它们编写的一些示例程序。将它们与 C# 进行比较。你可以查看 C、C++、Java、C#、VB.NET、PHP、JavaScript、Perl、Python 和 Ruby。
- 14. 先下载并安装 JustDecompile 或 ILSpy（信息可以在“代码反编译”章节中找到）。运行其中一个后，打开你的编译文件。它可以在 C# 项目的 `bin\Debug` 子目录下找到。例如，如果你的项目名为 `TestCSharp` 位于 `C:\Projects`，那么程序的编译程序集（可执行文件）将是文件 `C:\Projects\TestCSharp\bin\Debug\TestCSharp.exe`。

## 第 2 章 原生类型与变量

## 本章简介

在本章中，我们将熟悉 C# 中的原生类型和变量——它们是什么以及如何使用它们。首先，我们将考虑数据类型——整数类型、带浮点的实型、布尔型、字符和对象类型。我们将继续学习变量、它们的特征、如何赋值以及什么是变量初始化。我们将熟悉 C# 中的两大类数据类型——值类型和引用类型。最后，我们将检查不同类型的字面量及其用法。

## 什么是变量？

一个典型的程序会在执行过程中使用各种变化的值。例如，我们创建了一个程序，对用户输入的值进行某些计算。一个用户输入的值显然与另一个用户输入的值不同。这意味着在创建程序时，程序员并不知道将输入哪些值，这使得有必要处理用户可能输入的所有值。

当用户输入一个将将用于计算过程的新值时，我们可以将其（临时地）保存在计算机的随机访问内存中。这部分内存中的值在执行过程中会变化（变化），这导致了它们的名称——变量。

## 数据类型

数据类型是具有相似特征的值集合（范围）。例如，`byte` 指定了 `[0 ... 255]` 范围内的整数集合。

## 特征

数据类型的特征包括：

- 名称——例如，`int`；
- 大小（使用多少内存）——例如，4 字节；
- 默认值——例如，0。

## 类型

C# 中的基本数据类型分为以下类型：

- 整数类型——`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`
- 实型浮点型——`float`, `double`；
- 带小数精度的实型——`decimal`；
- 布尔类型——`bool`；
- 字符类型——`char`；
- 字符串——`string`；
- 对象类型——`object`。

这些数据类型被称为原生类型（内置类型），因为它们在底层嵌入在 C# 语言中。下表表示了上述数据类型、它们的范围和默认值：

| 数据类型 | 默认值 | 最小值 | 最大值 |
| :--- | :--- | :--- | :--- |
| sbyte | 0 | -128 | 127 |
| byte | 0 | 0 | 255 |
| short | 0 | -32768 | 32767 |
| ushort | 0 | -2147483648 | 2147483647 |
| int | 0 | -2147483648 | 2147483647 |
| uint | 0u | 0 | 4294967295 |
| long | 0L | -9223370236854775808 | 9223370236854775807 |
| ulong | 0u | 0 | 184467403709551616 |
| float | 0.0f | ±1.5x10⁻⁴⁵ | ±3.4x10³⁸ |
| double | 0.0d | ±5.0x10⁻³⁴⁴ | ±1.7x10³⁰⁸ |
| decimal | 0.0m | ±1.0x10⁻²⁸ | ±7.9x10⁻²⁸ |
| bool | false | 两个可能的值: true 和 false |  |
| char | '\u0000' | '\u0000' | '\uffff' |
| object | null | - | - |
| string | null | - | - |

第 2 章 原生类型与变量

## C# 与 .NET 类型的对应关系

C# 中的原生数据类型与 .NET Framework 中的通用类型系统 (CTS) 类型有直接对应关系。例如，C# 中的 `int` 类型对应 CTS 中的 `System.Int32` 类型以及 VB.NET 语言中的 `Integer` 类型，而 C# 中的 `long` 类型对应 CTS 中的 `System.Int64` 类型以及 VB.NET 语言中的 `Long` 类型。由于 .NET Framework 中的通用类型系统 (CTS)，不同的编程语言（如实例、C#、托管 C++、VB.NET 和 F#）之间具有兼容性。由于相同的原因，`int`、`Int32`、C#、托管 C++、VB.NET 和 F# 是兼容的。

## 整数类型
