

尼基·劳达居住在奥地利维也纳。

卡洛斯·鲁埃特曼居住在阿根廷圣菲。

塞巴斯蒂安·维特尔居住在瑞士图尔高。

## 摘要

本章介绍了 Type 和 Assembly 类的使用，它们是通过反射访问所提供广泛功能的主要入口点。

此外，本章演示了反射的一个特定方面，即自定义属性的检查，你很可能会比其他任何方面更频繁地使用它。你学习了如何定义和应用自己的自定义属性，以及如何在运行时检索有关自定义属性的信息。

本章的第二个重点是使用动态类型。使用 ExpandoObject 代替多个对象可以显著减少代码行数。此外，使用 DLR 并添加 Python 或 Ruby 等脚本语言可以帮助你构建一个更具多态性的应用程序，该应用程序可以在不重新编译的情况下轻松更改。

下一章详细介绍了 Visual Studio 2015 可用的许多功能。

## 17

## Visual Studio 2015

## 本章内容？

- 使用 Visual Studio 2015
- 创建和处理项目
- 调试
- 使用 Visual Studio 重构
- 处理各种技术：WPF、WCF 等
- 架构工具
- 分析应用程序

## 本章 Wrox.com 代码下载

本章没有代码下载。

## 使用 Visual Studio 2015

到目前为止，你应该熟悉 C# 语言，并且几乎准备好进入本书的应用部分，这些部分涵盖了如何使用 C# 编程各种应用程序。在此之前，了解如何使用 Visual Studio 以及 .NET 环境提供的一些功能来充分发挥程序的作用非常重要。

本章解释了在 .NET 环境中编程在实践中意味着什么。它涵盖了 Visual Studio，即你编写、编译、调试和优化 C# 程序的主要开发环境，并提供了编写良好应用程序的指导。Visual Studio 是用于众多目的的主要 IDE，包括编写 ASP.NET 应用程序、Windows Presentation Foundation (WPF) 应用程序以及通用 Windows 平台 (UWP) 应用，以及访问由 ASP.NET Web API 创建的服务，或使用 ASP.NET MVC 的 Web 应用程序。

本章还探讨了构建以 .NET Core 1.0 和 .NET Framework 4.6 为目标的应用程序所需的条件。

Visual Studio 2015 是一个完全集成的开发环境。它旨在使编写代码、调试它并将其编译为要发布的程序集的过程尽可能简单。这意味着 Visual Studio 为你提供了一个非常复杂的多个文档界面应用程序，你可以在其中完成与开发代码相关的几乎所有事情。它提供以下功能：

• 文本编辑器—使用此编辑器，你可以编写 C#（以及 Visual Basic、C++、F#、JavaScript、XAML、JSON 和 SQL）代码。此文本编辑器相当复杂。例如，随着你的输入，它会自动通过缩进行、匹配代码块的开始和结束括号以及为关键字着色来布局你的代码。它还在你输入时执行一些语法检查，并对导致编译错误的<|message|> 进行下划线，这也称为设计时调试。此外，它还具有 IntelliSense 功能，会在你开始输入时自动显示类、字段或方法的名称。随着你开始为方法输入参数，它还会显示可用重载的参数列表。图 17.1 显示了 IntelliSense 功能在 UWP 应用中的实际效果。

![](img/3d365b72b289213a91ade7eb366b8f35_596_0.png)

> 注意 通过按 Ctrl+Space，你可以在需要时或出于任何原因不可见时重新调出 IntelliSense 列表框。如果想在 IntelliSense 框下方查看一些代码，只需一直按住 Ctrl 键即可。

• 设计视图编辑器—此编辑器使你能够在项目中放置用户界面和数据访问控件；Visual Studio 会自动向你的源文件添加必要的 C# 代码，以在项目中实例化这些控件。（这是可能的，因为所有 .NET 控件都是特定基类的实例。）

• 支持窗口—这些窗口使你能够查看和修改项目的各个方面，例如源代码中的类，以及 Windows Forms 和 Web Forms 类的可用属性（及其启动值）。你还可以使用这些窗口指定编译选项，例如构建中包含哪些程序集。

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

/// <summary>
/// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238
/// </summary>
public sealed partial class MainPage : Page
{
    public MainPage()
    {
        this.InitializeComponent();
    }
}
```

你的代码需要引用。

- **集成调试器**—编程的本质是你的代码第一次尝试运行时不会正确运行。或者第二次。或者第三次。Visual Studio 无缝链接到调试器，使你能够从环境内部设置断点并监视变量。
- **集成 MSDN 帮助**—Visual Studio 使你能够从 IDE 内部访问 MSDN 文档。例如，如果你在文本编辑器中使用关键字时不确定其含义，只需选择该关键字并按 F1 键，Visual Studio 就会访问 MSDN 以显示相关主题。同样，如果你不确定某个编译错误意味着什么，你可以通过选择错误消息并按 F1 来调出该错误的文档。
- **访问其他程序**—Visual Studio 还可以访问许多其他实用程序，使你能够检查和修改计算机或网络的各个方面，而无需离开开发环境。使用可用的工具，你可以检查正在运行的服务和数据库连接，直接查看 SQL Server 表，浏览你的 Microsoft Azure 云服务，甚至使用 Internet Explorer 窗口浏览 Web。
- **Visual Studio 扩展**—一些 Visual Studio 扩展已随 Visual Studio 的正常安装一起安装，还有许多来自 Microsoft 和第三方提供的扩展。这些扩展使你能够分析代码，提供项目或项目模板，访问其他服务等等。随着 .NET Compiler Platform 的出现，工具与 Visual Studio 的集成变得更容易。

Visual Studio 的最新版本取得了有趣的进展。一个重要部分是用户界面，另一个重要部分是后台功能和 .NET Compiler Platform。

就用户界面而言，Visual Studio 2010 将外壳重新设计为基于 WPF 而不是原生 Windows 控件。Visual Studio 2012 在此基础上进行了一些用户界面 (UI) 更改。特别是，UI 增强为更专注于主要工作区——编辑器——并允许直接从代码编辑器执行更多任务，而无需使用许多其他工具。当然，你需要在代码编辑器之外使用一些工具，但更多功能已构建到其中一些工具中，因此通常需要的工具数量可以减少。Visual Studio 2015 对一些 UI 功能进行了更多增强。例如，NuGet 包管理器不再是模态对话框。使用包管理器的新版本，你可以在包管理器从服务器加载信息时继续执行其他任务。

随着 .NET Compiler Platform（代号 Roslyn），.NET 编译器已完全重写；它现在在编译器管道中集成了各种功能，例如语法分析、语义分析、绑定和代码生成。基于此，Microsoft 必须重写许多 Visual Studio 集成工具。代码编辑器、IntelliSense 和重构都基于 .NET Compiler Platform。

> 注意 第 18 章“ .NET Compiler Platform ”演示了可与 .NET Compiler Platform 一起使用的 API。

对于 XAML 代码编辑，Visual Studio 2010 和 Expression Blend 4（现名为 Blend for Visual Studio 2015）具有不同的编辑器引擎。自 Visual Studio 2013 起，团队已合并，虽然在 UI 中提供的功能略有不同，但代码引擎是相同的。不仅代码引擎相同：虽然 Visual Studio 2013 从 Blend 获得了 XAML 引擎，但现在使用 Blend for Visual Studio 2015，Blend 获得了来自 Visual Studio 的外壳。当你启动 Blend for Visual Studio 时，你会看到它看起来像 Visual Studio，并且可以立即开始使用它。

Visual Studio 的另一个特殊功能是搜索。Visual Studio 有如此多的命令和功能，以至于经常很难找到你要查找的菜单或工具栏按钮。只需将你要查找的命令的一部分输入到快速启动中，你就会看到可用的选项。快速启动位于窗口的右上角（见图 17.2）。搜索功能还可从工具箱、解决方案资源管理器、代码编辑器（可通过按 Ctrl+F 调出）、引用管理器的程序集等处获得。

![](img/3d365b72b289213a91ade7eb366b8f35_598_0.png)

图 17.2

