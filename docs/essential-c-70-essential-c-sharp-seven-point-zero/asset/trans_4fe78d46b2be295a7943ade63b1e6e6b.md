

**列表 21.20 的结果显示在输出 21.6 中。**

**输出 21.6**

```
Processor Id: GenuineIntel
```

## 摘要

正如整本书所展示的那样，C# 提供了强大的功能、灵活性、一致性以及出色的结构。本章重点强调了 C# 程序执行非常低层机器代码操作的能力。

在结束本书之前，第 22 章简要介绍了底层的执行框架，并将重点从 C# 语言转移到 C# 程序执行的更广泛上下文。

## 22

### 公共语言基础设施

C# 程序员在语法之外遇到的首要事项之一是 C# 程序执行的上下文。本章讨论了 C# 如何处理内存分配与释放、类型检查、与其他语言的互操作性、跨平台执行以及对编程元数据的支持的基础。换句话说，本章探讨了 C# 在编译时和运行时所依赖的公共语言基础设施。它介绍了在运行时管理 C# 程序的执行引擎，并考虑了 C# 如何融入由同一执行引擎管理的一组更广泛的语言中。由于 C# 与该基础设施的紧密联系，该基础设施提供的许多功能都可以供 C# 使用。

![](img/ef6a8a417630b222bfb3f3b949facff0_959_0.png)

### 定义公共语言基础设施

C# 编译器并不直接生成处理器可以解释的指令，而是生成中间语言 **公共中间语言** (CIL) 的指令。在通常发生在执行时间，会产生第二次编译步骤，将 CIL 转换为处理器可以理解的 **机器代码**。然而，转换为机器代码对于代码执行来说仍然不够。C# 程序也需要在某个代理的上下文中执行。负责管理 C# 程序执行的代理是 **虚拟执行系统** (VES)，通常更通俗地称为 **运行时**。（请注意，在此上下文中，运行时并不指时间，如执行时间；而是指负责管理 C# 程序执行的虚拟执行系统。）运行时负责加载和运行程序，并在程序执行过程中为程序提供额外的服务（安全、垃圾回收等）。

CIL 和运行时的规范包含在一个称为 **公共语言基础设施** (CLI) 的国际标准中。¹ CLI 是理解 C# 程序执行上下文以及如何与其他程序和库无缝交互（即使它们是用其他语言编写的）的关键规范。请注意，CLI 并未规定标准的具体实现，而是标识出 CLI 框架一旦符合标准后应如何行为的要求。这为 CLI 实现者提供了在必要之处进行创新的灵活性，同时提供了足够的结构，使得由一种 CLI 实现创建的程序可以在不同的实现甚至不同的操作系统上执行。

> **注意**
> 请注意 CIL 和 CLI 缩写与其全称之间的相似性。现在就区分它们将有助于你避免后期的混淆。

CLI 标准中包含以下规范：

- 虚拟执行系统
- 公共中间语言
- 公共类型系统
- 公共语言规范
- 元数据
- 框架

本章拓宽了你对 C# 的看法，将其包含 CLI，这对 C# 程序的运行方式及其与程序和操作系统的交互至关重要。

### CLI 实现

当今 CLI 的主要实现包括 .NET Core，它运行在 Windows 以及 UNIX/Linux 和 Mac OS 上；用于 Windows 的 .NET Framework；以及 Xamarin，它旨在用于 iOS、Mac OS 和 Android 应用程序。每个 CLI 实现都包含一个 C# 编译器，一组框架类库；每个实现支持的 C# 版本以及库中确切的类集差异很大，许多实现现在只有历史意义。表 22.1 描述了这些实现。

**表 22.1：CLI 的实现**

| 编译器 | 描述 |
| :------- | :---------- |
| Microsoft .NET Framework | 这是传统（也是第一个）版本的 CLR，用于创建在 Windows 上运行的应用程序。它包含对 Windows Presentation Foundation、Windows Forms 和 ASP.NET 的支持。它使用 .NET Framework 基类库 (BCL)。 |
| .NET Core/CoreCLR | .NET Core 项目，顾名思义，包含了所有新的 .NET 实现中通用的核心功能。它是 .NET Framework 的开源和跨平台可移植重写版本，专为高性能应用程序设计。CoreCLR 是该项目的 CLR 实现。在本书写作时，.NET Core 2.0 已发布在 Windows、macOS、Linux、FreeBSD 和 NetBSD 上。更多详情见 https://github.com/dotnet/coreclr。 |

**表 22.1：CLI 的实现（续）**

| 编译器 | 描述 |
| :--- | :--- |
| Xamarin | Xamarin 是一套开发工具和跨平台可移植的 .NET 框架库，以及 CLR 的实现，帮助开发者创建在 Microsoft Windows、iOS、Mac OS 和 Android 平台上运行的应用程序，具有非常高的代码重用率。Xamarin 使用 Mono BCL。 |
| Microsoft Silverlight | 此跨平台的 CLI 实现曾用于创建基于浏览器的 Web 客户端应用程序。Microsoft 已于 2013 年停止开发 Silverlight。 |
| .NET Compact Framework | 这是 .NET Framework 的精简版本，设计用于在 PDA、手机和 Xbox 360 上运行。用于开发 Xbox 360 应用程序的 XNA 库和工具基于 Compact Framework 2.0 版本；Microsoft 已于 2013 年停止开发 XNA。 |
| .NET Micro Framework | Micro Framework 是 Microsoft 针对资源受限到无法运行 Compact Framework 的设备而提供的开源 CLI 实现。 |
| Mono | Mono 是针对许多基于 UNIX 的操作系统、Android 等移动操作系统以及 PlayStation 和 Xbox 等游戏主机的开源跨平台 CLI 实现。 |
| DotGNU Portable.NET | 这项创建跨平台 CLI 实现的尝试已于 2012 年停止。 |
| 共享源代码 CLI (Rotor) | 在 2001 年至 2006 年间，Microsoft 发布了 CLI 的共享源代码参考实现，授权用于非商业用途。 |

尽管实现 CLI 所需的工作量很大，但这份列表还是很长的。然而，有三个框架在未来的发展中最为相关。

### Microsoft .NET Framework

Microsoft .NET Framework 是第一个 .NET CLI 实现（于 2000 年 2 月发布）。因此，它是最成熟的框架，拥有最大的 API 集。它支持构建 Web、控制台和 Microsoft Windows 客户端应用程序。.NET Framework 最大的限制是它仅在 Microsoft Windows 上运行——实际上，它是与 Microsoft Windows 捆绑在一起的。Microsoft .NET Framework 中包含许多子框架，其中最突出的是：

- **.NET Framework 基类库 (BCL)**：提供表示内置 CLI 数据类型的类型，包括对文件 IO、基本集合类、自定义特性、字符串操作等的支持。BCL 为 C# 原生类型（如 *int* 和 *string*）的每一个提供了定义。
- **ASP.NET**：用于构建网站和基于 Web 的 API。自 2002 年发布以来，该框架构成了基于 Microsoft 的网站基础，但正逐渐被其替代品 ASP.NET Core 取代，后者提供了操作系统可移植性、显著的性能改进以及具有更高模式一致性的更新 API。
- **Windows Presentation Foundation (WPF)**：一种图形用户界面框架，用于构建在 Microsoft Windows 上运行的富 UI 应用程序。WPF 不仅提供了一组 UI 组件，还提供了一种称为 **可扩展应用程序标记语言 (XAML)** 的声明式语言，该语言允许以层次结构方式定义应用程序的用户界面。

你会经常听到 Microsoft .NET Framework 被简称为 **.NET Framework**。注意大写 *F*，这使它区别于通用的 CLI 实现以及术语 .NET *framework*。

### .NET Core

.NET Core 是未来跨平台的 .NET CLI 实现。此外，.NET Core 是 .NET Framework 的开源重写版本，专注于高性能和跨平台兼容性。

.NET Core 由 .NET Core 运行时 (Core CLR)、.NET Core 框架库以及一组 Dotnet 命令行工具组成，可用于创建和构建所有可用的应用程序场景。这些组件的组合包含在 .NET Core SDK 中。如果你跟随了本书的示例，你已经在 .NET Core 和 Dotnet 工具上了。

