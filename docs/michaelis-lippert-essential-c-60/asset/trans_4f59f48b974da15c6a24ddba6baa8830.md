

- *垃圾回收：* 内存管理，自动释放运行时先前分配的内存。
- *平台可移植性：* 支持在多种操作系统上运行相同的程序集。 一个明显的限制是未使用任何平台相关的库；因此，与 Java 类似，存在一些需要解决的平台相关的特异性。
- *BCL：* 提供一个庞大的代码基础，供开发人员在所有 CLI 实现中依赖（），以便他们不必自行开发代码。

> **注意**
> 
> 本节简要概述了 CLI，以便您熟悉 C# 程序执行的上下文。 它还提供了本书中出现的一些术语的摘要。 第 21 章专门讨论 CLI 主题及其与 C# 开发人员的相关性。 尽管该章节出现在本书的最后，但它不依赖于任何前面的章节，因此如果您想更熟悉 CLI，可以随时跳转到该章节。

# C# 和 .NET 版本

微软对 .NET Framework 和相应的 C# 语言版本分配不一致的版本号，仅仅因为不同的团队有不同的版本机制。 这意味着如果您使用 C# 5.0 编译器编译，它默认会针对“.NET Framework 版本 4.6”进行编译，例如。 表 1.3 是 C# 和 .NET 版本的简要概述。

只要编译器版本对应于所需代码的版本，本书中的大部分代码就可以在 Microsoft 以外的平台上运行。 尽管为每个 C# 平台提供完整细节对某些读者有帮助，但这也可能分散学习 C# 的重点，因此本文的主要内容仅限于微软平台 .NET 的信息。 做出这一选择仅仅是因为微软拥有（远远）占主导地位的实现。 此外，翻译到另一个平台是相当简单的。

# 表 1.3：C# 和 .NET 版本

| Comment Type | Description |
|---|---|
| C# 1.0 with .NET Framework 1.0/1.1 (Visual Studio 2002 and 2003) | C# 的初始发布。 一种从头开始构建以支持 .NET 编程的语言。 |
| C# 2.0 with .NET Framework 2.0 (Visual Studio 2005) | 向 C# 语言添加了泛型，并向 .NET Framework 2.0 添加了支持泛型的库。 |
| .NET Framework 3.0 | 用于分布式通信（Windows Communication Foundation [WCF]）、丰富客户端展示（Windows Presentation Foundation [WPF]）、工作流（Windows Workflow [WF]）和 Web 身份验证（Cardspaces）的附加 API 集合。 |
| C# 3.0 with .NET Framework 3.5 (Visual Studio 2008) | 添加了对 LINQ 的支持，这对用于编程集合的 API 是一个重大改进。 .NET Framework 3.5 提供了扩展现有 API 以实现 LINQ 的库。 |
| C# 4.0 with .NET Framework 4 (Visual Studio 2010) | 添加了对动态类型的支持，以及对编写利用多处理器和处理器内多个核心的多线程程序的 API 的重大改进。 |
| C# 5.0 with .NET Framework 4.5 (Visual Studio 2012) and WinRT integration | 添加了对异步方法调用的支持，而无需显式注册委托回调。 框架中的另一个更改是对 Windows 运行时（WinRT）互操作性的支持。 |
| C# 6.0 with .NET Framework 4.6 (Visual Studio 2015 ) | 添加了字符串插值、空传播成员访问、异常过滤器、字典初始化器以及许多其他功能。 |

也许与 C# 6.0 一起添加的最重要的框架功能是跨平台编译的支持。 换句话说，.NET Framework 不仅在 Windows 上运行，而且微软还提供了一个实现（称为“CoreFX”）的 .NET Core，可在 Linux 和 OS X 上运行。 尽管 .NET Core 并不是与完整的 .NET Framework 相当的功能集，但它包含足够的功能，可以将整个（ASP.NET）网站托管在 Windows 以外的操作系统上

及其 Internet Information Server（IIS）。 这意味着使用相同的代码库，可以编译和执行在跨平台上运行的应用程序。 .NET Core 包括从 .NET 编译器平台（“Roslyn”）开始，后者本身可在 Linux 和 OS X 上执行，到 .NET Core 运行时，以及诸如 .NET 版本管理器（DNVM）和 .NET 执行环境（DNX）之类的工具。

# 通用中间语言和 ILDASM

如前一节所述，C# 编译器将 C# 代码转换为 CIL 代码，而不是机器代码。 处理器可以直接理解机器代码，但 CIL 代码需要在处理器执行之前进行转换。 给定一个程序集（DLL 或可执行文件），可以使用 CIL 反汇编实用程序查看 CIL 代码，以将程序集解构为其 CIL 表示形式。 （CIL 反汇编程序通常以其 Microsoft 特定的文件名 ILDASM 命名，代表 IL Disassembler。）此程序将反汇编程序或其类库，显示 C# 编译器生成的 CIL。

用于 CIL 反汇编程序的确切命令取决于使用的 CLI 实现。 您可以通过命令行执行 .NET CIL 反汇编程序，如输出 1.8 所示。

```
Output 1.8

>ildasm /text HelloWorld.exe
```

/text 部分用于使输出出现在命令控制台而不是新窗口中。 执行这些命令后产生的输出流是包含在 HelloWorld.exe 程序中的 CIL 代码转储。 请注意，CIL 代码比机器代码更容易理解。 对于许多开发人员来说，这可能会引起担忧，因为程序更容易被反编译，算法可以在不明确重新分发源代码的情况下被理解。

与任何程序一样，无论是否基于 CLI，阻止反汇编的唯一万无一失的方法是完全禁止访问编译后的程序（例如，只将程序托管在网站上而不是分发到用户的机器上）。 但是，如果只需要降低对源代码的访问权限，则有几种混淆器可用。
这些混淆器打开 IL 代码并对其进行转换，使其以更难以理解的方式执行相同的操作。 这可以防止普通开发人员访问代码，并创建反编译为可理解代码更困难和繁琐的程序集。 除非程序需要高度的算法安全性，否则这些混淆器通常是足够的。

# 高级主题

# HelloWorld.exe 的 CIL 输出

列表 1.19 显示了 ILDASM 创建的 CIL 代码。

```
```text
//  Microsoft (R) .NET Framework IL Disassembler.  Version 4.6.81.0
//  Copyright (c) Microsoft Corporation.  All rights reserved.


// Metadata version: v4.0.30319
.assembly extern mscorlib
{
    .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )              //
    .ver 4:0:0:0
}
.assembly HelloWorld
{
    .custom instance void [mscorlib]System.Runtime.CompilerServices.
CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 00 00 00 00 00 00 )
    .custom instance void [mscorlib]System.Runtime.CompilerServices.
RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70
4E 6F 6E 45 78   // ....t..WrapNonEx
63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )     // ceptionThrows.

    // --- The following custom attribute is added automatically, do not
    // uncomment ------
    // .custom instance void [mscorlib]System.Diagnostics.
DebuggableAttribute::.ctor valuetype [mscorlib]System.Diagnostics.
DebuggableAttribute/DebuggingModes = ( 01 00 07 01 00 00 00 00 )

    .hash algorithm 0x00008004
    .ver 0:0:0:0
}
.module HelloWorld.exe
// MVID: {1FB5153C-639E-401D-8C94-22A66C18DC7A}
```
```
