

Microsoft .NET（发音为“dot net”）是一种运行在 Windows 操作系统上的软件组件...NET 应用程序。

## .Net Framework

.NET 是一个用于开发软件应用程序的框架。它由 Microsoft 设计和开发，首个 beta 版本于 2000 年发布。

它用于开发 Web、Windows、手机应用程序。此外，它提供广泛的功能和支持。该框架包含大量类库，称为框架类库（FCL）。用 .NET 编写的软件程序在执行环境中执行，该执行环境在语言运行时（CLR）中执行。这些是 .NET 框架的核心和必不可少的部分。

该框架提供各种服务，如内存管理、网络、安全、内存管理和类型安全。.Net Framework 支持超过 60 种编程语言，如 C#、F#、VB.NET、J#、VC++、jscript.NET、APL、COBOL、Perl、Oberon、ML、Pascal、Eiffel、Smalltalk、Python、Cobra、ADA 等。

## 以下是显示框架模块和组件的 .NET 框架堆栈。

.NET Framework 由四个主要组件组成：

通用语言运行时（CLR）框架类库（FCL）、核心语言（winforms、ASP.NET 和 ADO.NET）以及其他模块（WCF、WPF、WF、Card Space、LINQ、Entity Framework、Parallel LINQ、Task Parallel Library 等）

| .NET Framework 版本 | 组件 |
|------------------------|-----------|
| 2.0 | Common Language Runtime, Framework Class Library, WinForms, ASP.NET, ADO.NET |
| 3.0 | WPF, WCF, WF, Card Space |
| 3.5 | LINQ, Entity Framework |
| 4.0 | Task Parallel Library, Parallel LINQ |
| 4.5 | Task-Based Async Model, .NET APIs for Store/UWP apps |

图 1.3：.NET Framework 架构

## CLR（通用语言运行时）

它是一个程序执行引擎，用于加载和执行程序。它将程序转换为本地代码。它充当框架和操作系统之间的接口。它进行异常处理、内存管理和垃圾回收。此外，它提供安全性、类型安全、互操作性和可移植性。CLR 组件列表如下：

### 通用语言运行时

![](img/e7ca4af023a4148a909dd82c11f81893_33_0.png)

## 图 1.4 FCL（框架类库）

它是一个标准库，是由数千个类组成的集合，用于构建应用程序。BCL（基本类库）是 FCL 的核心，并提供基本功能。

![](img/e7ca4af023a4148a909dd82c11f81893_34_0.png)

## Winforms

Windows Forms 是 .NET Framework 的智能客户端技术，一组托管库，可简化

常见应用程序任务，例如读写文件系统。

## ASP.NET

ASP.NET 是由 Microsoft 设计和开发的 Web 框架。它用于开发网站、Web 应用程序和 Web 服务。它提供 HTML、CSS 和 javascript 的出色集成。它于 2002 年 1 月首次发布。

## ADO.NET

ADO.NET 是 .Net Framework 的一个模块，用于在应用程序和数据源之间建立连接。数据源可以是 SQL Server 和 XML 等。ADO .NET 由可用于连接、检索、插入和删除数据的类组成。

## WPF（Windows Presentation Foundation）

Windows Presentation Foundation（WPF）是 Microsoft 用于在基于 Windows 的应用程序中渲染用户界面的图形子系统。WPF，之前称为“Avalon”，最初作为 .NET Framework 3.0 的一部分于 2006 年发布。WPF 使用 directx。

## WCF（Windows Communication Foundation）

它是一个用于构建面向服务应用程序的框架。使用 WCF，您可以将数据作为异步消息从一个服务端点发送到另一个服务端点。

## WF（Workflow Foundation）

Windows Workflow Foundation（WF）是 Microsoft 的一项技术，提供 API、进程内工作流引擎和可重新托管的设计器，以便在 .NET 应用程序中将长期运行的进程实现为工作流。

## LINQ（语言集成查询）

它是一种查询语言，于 .NET 3.5 框架中引入。它用于使用 C# 或 Visual Basics 编程语言为数据源制作查询。

## Entity Framework

它是一个基于 ORM 的开源框架，用于使用 .NET 对象与数据库进行工作。它消除了开发人员处理数据库的大量工作。它是 Microsoft 推荐的处理数据库的技术。

## 1.6 垃圾回收

- 垃圾收集器（GC）管理内存的分配和释放。垃圾收集器充当自动内存管理器。
- 您无需知道如何分配和释放内存或管理使用该内存的对象的生命周期。
- 每次使用“new”关键字声明对象或值类型被装箱时都会进行分配。分配通常非常快。
- 当没有足够的内存来分配对象时，GC 必须收集和处理垃圾内存以使内存可用于新分配。

此过程称为垃圾回收。

C# 中的垃圾回收具有以下优点：

- 在开发应用程序时，您无需手动释放内存。
- 它还有效地在托管堆上分配对象。
- 当对象不再使用时，它将通过清除其内存来收回这些对象，并使内存可用于将来分配。
- 托管对象会自动获得干净的内容来开始，因此它们的构造函数不必初始化每个数据字段。

## CHAPTER 2

## C# 基础

## 2.1 什么是 C#？

C# 发音为“C-Sharp”。

它是一种由 Microsoft 创建的面向对象编程语言，运行在 .NET Framework 上。C# 源自 C 家族，该语言接近其他流行语言，如 C++ 和 Java。

第一个版本于 2002 年发布。最新版本 C# 8 于 2019 年 9 月发布。

C# 用于：

- 移动应用程序
- 桌面应用程序
- Web 应用程序
- Web 服务
- 网站
- 游戏
- VR
- 数据库应用程序

### 2.1.1 为什么使用 C#？

- 它是世界上最流行的编程语言之一
- 它易于学习且简单易用
- 它拥有庞大的社区支持
- C# 是一种面向对象的语言，为程序提供清晰的结构并允许代码重用，降低开发成本。
- 由于 C# 与 C、C++ 和 Java 接近，因此程序员在 C# 和其之间切换变得容易

### 2.1.2 C# 安装

下载并安装 Visual Studio Installer 后，选择 .NET 工作负载并单击 Modify/Install 按钮：

![](img/e7ca4af023a4148a909dd82c11f81893_39_0.png)

安装完成后，单击 Launch 按钮开始使用 Visual Studio。在开始窗口中，选择 Create a new project：

然后单击“Install more tools and features”按钮：

![](img/e7ca4af023a4148a909dd82c11f81893_40_0.png)

![](img/e7ca4af023a4148a909dd82c11f81893_40_1.png)

从列表中选择“Console App (.NET Core)”并单击 Next 按钮：

![](img/e7ca4af023a4148a909dd82c11f81893_41_0.png)

为您的项目输入名称，然后单击 Create 按钮：

![](img/e7ca4af023a4148a909dd82c11f81893_41_1.png)

Visual Studio 将自动为您的项目生成一些代码：

![](img/e7ca4af023a4148a909dd82c11f81893_42_0.png)

代码应如下所示：

```
Program.cs
Using System;
Namespace helloworld
{
Class Program
{
Static void Main(string[] args)
{
Console.writeline("Hello World!");
}
}
}
```

通过按键盘上的 F5 按钮运行程序（或单击“Debug”->“Start Debugging”）。这将编译并执行您的代码。结果应如下所示：

![](img/e7ca4af023a4148a909dd82c11f81893_43_0.png)

## 2.2 示例：解释

第 1 行：using System 表示我们可以从 System 命名空间使用类。

第 2 行：一个空行。C# 忽略空白。然而，多行使代码更具可读性。

第 3 行：namespace 用于组织您的代码，并且是类和其他命名空间的容器。

第 4 行：大括号 {} 标记代码块的开始和结束。

第 5 行：class 是数据和方法容器的容器，为您的程序带来功能。在 C# 中运行的每一行代码都必须在类内部。在我们的示例中，我们将类命名为 Program。

