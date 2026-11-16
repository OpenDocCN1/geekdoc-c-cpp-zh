

## 恭喜！你已完成本章。在进入下一章之前，花一分钟思考一下你所取得的成就...

### 列出你在本章学到的三件事：

- 1
- 2
- 3

你认为为什么需要知道这些东西才能成为一名 C# 程序员？

本章中有什么是你觉得需要更详细理解的吗？如果有，你打算怎么做？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_50_0.png)

## .NET 平台

上一章我们探讨了应用程序开发的工作流程，并考察了规范过程和编译方法。在本章中，我们将开始通过了解 .NET 平台来缩小关注范围，这是大多数 C# 应用程序运行的环境。

.NET 平台（朋友们管它叫“dot Net”），包括 .NET FRAMEWORK，即我们将要学习的编程和运行时基础设施，以及像管理数据的 SQL Server 这样的服务器，和像 Visual Studio 和 Expression Studio 这样的工具。

本章我们还将通过编写你的第一个真实应用程序来初涉编程，即所有初学者程序员的必经之路——传统的“Hello, World!”。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_51_0.png)

### 独立练习

还记得你想开发的应用程序列表吗？其中大多数都将使用 .NET Framework，但在阅读本章过程中，请记下你认为可能对你有用的其他 .NET 平台组件。

## 如何契合

你将在设计时和运行时都使用 .NET 平台组件。

你编写的代码将使用 .NET Framework 的一部分——Framework Class Library。

你将使用 .NET 工具 Visual Studio 来开发你的应用程序。

你的应用程序可能会使用 .NET 平台服务器，例如用于关系型数据库的 SQL Server 或用于文档管理的 Sharepoint。

.NET 应用程序在 Common Language Runtime 的上下文中运行，这是 .NET Framework 的关键组件。

.NET 平台由 .NET Framework、Framework Tools 和 Framework Servers 组成。

## 任务列表

上一章我们从抽象层面探讨了开发。现在是时候开始了解 .NET Framework 和 C# 的具体内容了。我们将从以下内容开始：

## .NET 平台组件

尽管 Neil 和 Gordon 很有才华，但他们也无法在厨房里包办一切。他们不必如此。同样，你也不必完成应用程序中所有需要做的事情。但就像这两位小伙子一样，如果你想控制一切，就需要对每个组件的功能有基本了解。因此，我们将从考察 .NET 平台的主要组件开始本章。

## 说声你好

一旦我们了解了 .NET 平台的各个组成部分，就该初涉编程了。程序员学习新语言时，第一件事通常是让它向世界问好，我们将通过创建一个应用程序来向世界介绍自己，以此来实现。

## 说什么？

当然，你读这本书不仅仅是为了学习如何遵循指示，所以在说声你好之后，我们会稍微回顾一下，检查刚才所做的事情。理解这个过程很重要，因为你在构建的每个应用程序中都会或多或少做同样的事情。

## .NET 平台组件

### .NET 服务器

- SQL Server
- IIS
- Biztalk Server
- Sharepoint Server

### .NET 工具

- Visual Studio
- Expression Studio
- Framework SDK

### .NET Framework

### 专用框架

- Compact
- Micro
- Windows Phone
- CLR
- Languages
- Class Library
- Base Class Library
- FCL Technologies

## 动动脑筋

你能使用这张图回答这些问题吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_55_0.png)

以下是 .NET 平台组件的三个主要类别：

C# 是其中之一：

这是创建 .NET 应用程序时 Visual Studio 的替代品：

例如，如果你要为手机编写代码，就会使用其中之一：

这代表 Framework Class Library：

这是 .NET 运行时环境。这些字母代表：

这是 .NET 的主要开发环境：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_56_0.png)

## 做得怎么样？

以下是 .NET 平台组件的三个主要类别：

- .NET Servers
- .NET Tools
- .NET Framework

C# 是其中之一：

- Framework language

这是创建 .NET 应用程序时 Visual Studio 的替代品：

- Framework SDK

例如，如果你要为手机编写代码，就会使用其中之一：

- Specialty Framework

这代表 Framework Class Library：

- FCL

这是 .NET 运行时环境。这些字母代表：

- CLR — Common Language Runtime

这是 .NET 的主要开发环境：

- Visual Studio

## .NET 平台组件

### .NET 服务器

这些为其他应用程序提供服务。

- SQL Server
- IIS
- Biztalk Server
- Sharepoint Server

### .NET 工具

你使用这些来创建 .NET 应用程序。

- Visual Studio
- Expression Studio
- Framework SDK

### .NET Framework

这是本书的主要关注点。

我们不会深入研究这些，但你在这里学到的大部分内容都将适用。

### 专用框架

- Compact
- Micro
- Windows Phone
- CLR
- Languages
- Class Library

这提供了可用于任何应用程序的有用代码。我们将从第 10 章开始详细考察它。

- Base Class Library
- FCL Technologies

Framework Technologies 包括用于开发 Web 应用程序的 ASP.NET 和 Silverlight 等内容，用于处理数据的 Entity Framework，以及我们将用来构建 Windows 界面的 WPF/XAML。

## 框架的价值

为了了解 .NET Framework 为我们提供了什么，让我们来看一个常见的编程需求。

这是一个非常简单的表单。几乎任何通用编程语言都能让你轻松创建类似的东西。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_58_0.png)

当用户将表单变宽时，你希望标签保持原有大小，但文本框变大，如下所示：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_58_1.png)

很简单，对吧？你在无数不同的应用程序中见过无数次。你可能会觉得任何不这样做的应用程序都相当笨拙，对吧？让我们来看看程序员需要做什么才能实现这一点。

在 .NET 发布之前，Visual Basic 6 是开发 Windows 应用程序最流行的语言。现存的 VB6 应用程序数不胜数，VB6 程序员也几乎同样多。以下是调整我们表单大小的 VB6 代码（它可能对其他表单不起作用）：

创建一个变量来存储表单的原始宽度。

在表单首次加载时获取该变量的值。

遍历表单上的所有控件并调整文本框的大小。

重置该变量。

```
originalWidth As Integer
Sub Form_Load()
    originalWidth = Me.ScaleWidth
End Sub
Sub Form_Resize()
    If Me.WindowState <> vbMinimized Then
        Dim ctrl As Control
        For Each ctrl In Controls
            If typeof ctrl is TextBox Then
                ctrl.Width = ctrl.Width * (Me.Width / originalWidth)
            End If
        Next
    End If
    originalWidth = Me.ScaleWidth
End If
```

实际上，调整大小的例程会复杂得多。至少，它需要考虑高度和宽度的变化。当然，需要调整的确切控件以及调整方式，对于每个表单和每种控件类型都会不同。

那 .NET 版本呢？没有。Windows Presentation Foundation 是 .NET Framework 技术之一，它会为你完成所有这些工作...

## 休息一下

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_60_0.png)

在本书剩余部分中，我们将更详细地探讨 .NET Framework，但现在你应该了解 Framework 在整体 .NET 平台中的位置，所以在我们处理下一个任务之前，先休息一下。

## 复习

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_60_1.png)

.NET 平台组件的三个类别是什么，它们各自起什么作用？

使用 C# 编程时，你将始终使用哪个组件？

