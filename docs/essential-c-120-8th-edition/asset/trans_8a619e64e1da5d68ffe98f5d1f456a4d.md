

## 42 第 1 章：介绍 C#

```assembly
.assembly 'HelloWorld'
{
    custom instance void [System.Runtime]System.Runtime.CompilerServices.
    CompilationRelaxationsAttribute::.ctor(int32) = (01 00 0A 48 65 00 00 00 00
00)
    custom instance void [System.Runtime]System.Runtime.CompilerServices.
    RuntimeCompatibilityAttribute::.ctor() = (01 00 01 00 54 02 16 57 72 61
70 4E 6C 6E 7F 65 47 63 75 72 69 6F 62 72 72 73 03 01)
    custom instance void [System.Runtime]System.Runtime.Versioning.
    TargetFrameworkAttribute::.ctor(string) = (01 00 18 2E 4E 45 54 43 63 6F
72 65 41 70 20 5C 55 65 73 63 6E 6D 33 33 30 31 01 54 54 14 14 n6\ 62 61 65 65 72 64 44 73 63 63 61  6E 61 6D 65 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyCompanyAttribute::.ctor(string) = (01 00 0A 48 65 6C 6F 57 6F
72 6C 64 00 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyConfigurationAttribute::.ctor(string) = (01 00 05 44 65 65 72
67 00 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyFileVersionAttribute::.ctor(string) = (01 00 07 31 2E 30 2E 30
2E 30 33 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyInformationalVersionAttribute::.ctor(string) = (01 00 05 31 2E
30 2E 30 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyProductAttribute::.ctor(string) = (01 00 0A 48 65 6C 6F 57 6F
72 6C 64 00 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyTitleAttribute::.ctor(string) = (01 00 0A 48 65 6C 6F 57 6F
72 6C 64 00 00 00 )
    hash algorithm 0x00000004
. { 1:0:0 }
```

```ilassembly
.module 'HelloWorld.dll'
// MVID: {05b2d1a7-c150-4f20-bd96-c065e4f9a731}
// imagebase 0x00040000
// file alignment 0x00010000
// stackreserve 0x00010000
// subsystem 0x00020003 // WindowsCui
// corflags 0x00000001 // ILOnOnly
```

```assembly
.class private auto ansi HelloWorld.Program
extends[System.Runtime] System.Object
{
  .method private hidebysig static void Main(string[] args) cil managed
  {
    .entrypoint
    // Code size 13
    .maxstack 8
    IL_0000: nop
    IL_0001: ldstr "Hello. My name is Inigo Montoya."
    IL_0006: call void
    System.Console::System.Console::WriteLine(string)
    IL_000b: nop
    IL_000c: ret
    // End of method System.Void
    // HelloWorld.Program::Main(System.String[])
  }

.method public hidebysig rspecialname instance void
  ..ctor() cil managed
  {
    // Code size 8
    .maxstack 8
    IL_0000: ldarg.0;
    IL_0001: call instance void [System.Runtime]System.Object::.ctor()
    IL_0006: nop
    IL_0007: ret
    // End of method HelloWorld.Program::.ctor()
  } // End of class HelloWorld.Program
```

列表的开头是清单信息。它不仅包含了模块的全名（HelloWorld.dll），还包含了它依赖的所有程序集以及它们的版本信息。

也许从列表中最有趣的事情是，相对于尝试理解机器代码（汇编），跟进程序在做什么是容易的。在列表中，显式引用了 `Console.WriteLine()`。但如果开发者想要理解 C# 程序集（或任何基于 CLI 的程序）的内部运作，CIL 代码提供了大量的信息，除非使用了混淆器。

事实上，正如在本章早期简要提到的，存在多个 .NET 框架。大量提供的动力主要是为了跨多个操作系统以及可能的不同的硬件平台提供 .NET 实现。表 1.3 显示了主流实现。

### 表 1.3：主流 .NET 实现

| 类型 | 说明 |
| :--- | :--- |
| .NET 6 及后续 | 从 .NET 6（遵循 .NET 5.0）开始，后缀被删除，表示 .NET 和 .NET Framework 基本上统一为了一个框架。 |
| .NET Core | 一个真正跨平台且开源的 .NET 框架，支持服务器和命令行应用程序的高度模块化 API 集。 |
| Microsoft .NET Framework | .NET 框架第一个——逐渐被 .NET Core 取代。 |
| Xamarin | 随着 .NET 6.0 的发布，实现了从单一代码库开发 iOS 和 Android 移动应用程序的可能。 |
| Mono | .NET 最老的开源实现，Xamarin 和 Unity 构建在其之上。 |
| Unity | 一个用于开发控制台、PC、移动设备甚至网站视频游戏的跨平台游戏引擎。Unity 引擎是第一个支持增强现实领域的公共实现。 |

## 应用程序接口

方法（或更泛地说，成员）发现于数据类型如 Console 的应用程序接口（API）。API 定义了软件程序如何与组件交互。此类，它不仅出现在单个数据类型中，而且更泛地说；所有数据类型的 API 组合创建了一个 API。在 .NET 中，程序集中的类型（以及类型中的成员）被认为是程序集的 API。同样，给定一个 .NET 的程序集组合，程序集的集合形成了更大的 API。通常，这组更大的 API 被称为框架——由 .NET 实现所暴露的 API 术语。

## C# 和 .NET 版本

从历史上看，.NET 框架的开发周期并不总是与 C# 语言一致；因此，底层NET 框架的版本与相应的 C# 语言版本都以数字结尾。这意味着如果你使用 C# 11.0 编译器编译，它默认将针对 .NET 7.0 进行编译，例如。表 1.4 是 Microsoft .NET Framework 和 .NET Core 的 C# 和 .NET 简要概述。

### 表 1.4：C# 和 .NET 版本

| 类型 | 说明 |
| :--- | :--- |
| C# 1.0 与 .NET Framework 1.0/1.1 (Visual Studio 2002 和 2003) | C# 的初始发布。从零开始支持 .NET 编程的语言。 |
| C# 2.0 与 .NET Framework 2.0 (Visual Studio 2005) | 在 C# 语言中增加了泛型，以及支持泛型的 Microsoft .NET Framework 2.0 库。 |
| Microsoft .NET Framework 3.0 | 用于分布式通信（WCF）、富客户端演示（WPF）、工作流（WF）和网络身份验证（Cardspaces）的额外 API 集。 |
| C# 3.0 与 .NET Framework 3.5 (Visual Studio 2008) | 增加了对 LINQ 的支持，这是集合编程 API 的重大改进。Microsoft .NET Framework 3.5 提供了扩展现有 API 使 LINQ 成为可能的库。 |
| C# 4.0 与 .NET Framework 4 (Visual Studio 2010) | 增加了对动态类型的支持，并对编写利用其多个处理器和核心的多线程程序的 API 进行了显著改进。 |
| C# 5.0 与 .NET Framework 4.5 (Visual Studio 2012) 和 WinRT 集成 | 增加了异步方法调用的支持，无需显式注册委托回调。框架的另一个变化是支持与 Windows Runtime (WinRT) 的互操作性。 |
| C# 6.0 与 Microsoft Framework 4.6 和 .NET Core 1.X (Visual Studio 2015) | 增加了字符串插值、空传播成员访问、异常过滤器、字典初始化以及许多其他功能。 |
| C# 7.0 与 .NET Framework 4.7 和 .NET Core 1.1 或 2.0 (Visual Studio 2017) | 增加了元组、析构函数、模式匹配、本地函数、引用返回以及更多功能。 |

