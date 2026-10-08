

# ASP.NET Ajax Control Toolkit 和 jQuery

在第 19 章中，你重新学习了 Ajax 的改进，并看到了几个使用 ASP.NET Ajax 库的示例。你还阅读了 jQuery 库，并在几个样本中使用了 jQuery。

Ajax 和 jQuery 主要是客户端技术。它们基于 JavaScript 构建。如果你没有任何服务器端技术，而只有一个带有标准 HTTP/HTTPS 协议的简单 Web 服务器，你仍然可以使用这两种技术。然而，大多数应用程序都是处理信息的，这些应用程序的本质是在服务器端（即互联网云端的某处）存储和处理数据，而不是在客户端。

本章将深入探讨 ASP.NET Ajax Control Toolkit 和 jQuery 技术。这些是完整工具set中的两个重要部分，你可以将它们与 ASP.NET 应用程序配合使用，提高用户体验。

本章涵盖了以下主要主题：

- 首先初识 Ajax Control Toolkit —— 你将把一个使用“闪烁”式回传（postbacks）的 ASP.NET Web 应用程序改为使用 Ajax Control Toolkit 的改进版本。
- 使用 Toolkit 的控件 —— 本节将详细介绍 Toolkit 随附的大多数服务器端控件和扩展器（extenders）。你将通过许多小样本学习更多关于它们的信息。
- jQuery 库 —— 在这一节中，你将学习 jQuery 库，旨在让你更容易导航文档、选择文档对象模型（DOM）元素、创建动画、处理事件以及开发 Ajax 应用程序。

> 第 19 章对使用 ASP.NET 库提供了非常好的概述，包含了许多示例和代码段。它还解释了 Ajax 的基本概念。如果你是 Ajax 编程的新手，或者不是该领域的资深开发者，强烈建议阅读第 19 章，以充分理解此处涉及的概念。

# 初识 Ajax Control Toolkit

ASP.NET Ajax Control Toolkit 包含一套丰富的 ASP.NET 服务器端控件，你可以使用这些控件来构建响应迅速且交互的启用 Ajax 的 Web 应用程序。它通常被简单地称为 Ajax Control Toolkit，本章将其称为“Toolkit”。

Toolkit 包含 40 多个常用控件，包括 AutoCompleteExtender、ComboBox、CollapsiblePanelExtender、Accordion（手风琴控件）等。其中大多数控件非常简单，能为你的网站增加动力、功能性，并提升用户体验。尽管根结底在客户端使用的是 JavaScript，但 Toolkit 中的控件从你的任务列表中消除了大多数与 JavaScript 相关的编程挑战。

使用 Ajax Control Toolkit，你可以通过将 Visual Studio 工具箱（Toolbox）中的控件拖放到 Web 页面，然后像使用任何其他 ASP.NET 服务器端控件一样使用它们，构建启用 Ajax 的 ASP.NET Web Forms。

ASP.Net Ajax Control Toolkit 于 2006 年 5 月作为一个开源项目诞生，至今仍然是一个活跃的项目。你可以在 Codeplex (http://www.codeplex.com/AjaxControlToolkit) 上找到它。它是微软和 ASP.NET 社区共同努力。项目提供的控件构建在 Microsoft ASP.NET 框架之上。Toolkit 的设计不仅支持 Internet Explorer，还支持 Firefox、Safari、Opera 和 Chrome。大多数控件可以与你使用的浏览器无缝独立地工作。然而，存在某些兼容性问题。该项目跟踪这些问题并定期提供服务版本。

# 安装 Ajax Control Toolkit

你可以通过点击 Codeplex 首页页上的“Downloads”选项卡下载最新版本的 ASP.NET Ajax Control Toolkit。在编写本文时，最新版本是 ASP.NET Ajax Library Beta 0911（于 2009 年 11 月 18 日发布）。正如下载名称所示，这不仅是 Ajax Toolkit，现在的 ASP.NET Ajax Library 现在还包含了原始 Ajax Control Toolkit 中的所有 ASP.NET Web Forms 控件。

当你下载并解压库时，可以在解压下载文件的根目录下的 `AjaxNetLibrary\WebForms` 子中找到 Ajax Control Toolkit。你也会在那里找到 `ReleaseToolkit.dll` 文件，如下所示

**20-1. Debug 文件夹也包含此程序集的 Debug 生成版本。**

你可以通过将控件添加到工具箱（Toolbox）来将 Toolkit 与 Visual Studio 集成。在 Visual Studio 2010 中打开一个 ASP.NET Web 应用程序，或创建一个 ASP.NET Web 应用程序项目。添加一个表单（Form）并命名，例如 Default.aspx。

打开一个 .aspx 文件（例如 Default.aspx）以便显示 Visual Studio 工具箱。右键点击工具箱中的任何项（Extensions 选项卡）并添加“Add”选项卡。会出现一个新的空白选项卡。将其命名为“Ajax Toolkit”。此选项卡只是控件的占位符，因为它不包含任何控件。右键点击此选项卡并运行“Choose Items（选择项目）”。

当“Choose Toolbox Items”对话框出现时，选择 .NET Frameworks Components 选项卡。点击“Browse（浏览）”按钮从图 20-1 所示的 Release 文件夹选择 `AjaxControlToolkit.dll`。Visual Studio 会警告你正在添加一个从网络位置下载的文件，这可能会损坏你的计算机。确认你确实想这样做。AjaxControlToolkit.dll 中找到的新控件将在对话框中被选中，并标记为将添加到选项卡。点击 OK 按钮关闭对话框，Visual Studio 将程序集中的所有控件添加到选项卡中，如图 20-2 所示。

当然，在图 20-2 中你只能看到已添加的部分控件。Ajax Control Toolkit 提供了 40 多个你可以添加到页面的控件。

![](img/b5597c749e848b27b0d305153ae16106_936_0.png)
**20-1: 结构中的 Ajax Control Toolkit**

![](img/b5597c749e848b27b0d305153ae16106_936_1.png)
**20-2: 新添加的 Ajax Control Toolkit**

# Toolkit 安装的控件

当你查看安装的控件名称时，你会发现：

- 标准控件 —— 它们命名简单，如 Rating、Accordion、TabContainer 等。这些是像其他控件一样工作的简单控件。
- 扩展器（Extenders）—— 它们以“Extender”结尾，易于识别（少数例外）。正如名称所示，扩展器扩展了现有控件的功能。

# 升级到新版本

如果你已安装旧版本的 Toolkit，或者下载了新版本并想更改你的项目，可以通过以下建议步骤避免烦人的版本问题：

1. 打开打算升级的 ASP.NET Web 项目（解决方案），删除对 AjaxControlToolkit.dll 的引用。
2. 在解决方案管理器中右键点击项目，运行 Open Folder 命令。当 资源管理器打开时，进入 bin 文件夹并删除 AjaxToolkit.dll。
3. 为项目添加一个新的 Default.aspx 文件。进入工具箱并右键点击 Ajax 选项卡。移除之前添加的所有控件。
4. 按照之前说明的步骤将新版本的控件添加到工具箱。
5. 临时拖动一个控件（例如 ComboBox）从 Ajax Control Toolkit 拖到 Default.aspx。Visual Studio 将引用 AjaxControlToolkit 程序集（当然，是对你刚刚安装的新版本）。
6. 删除 Default.aspx。

如果你的解决方案中有多个 ASP.NET Web 应用程序，请每个项目重复这些步骤。当然，你只需从工具箱移除 Ajax 选项卡并添加一次新控件。

# 使用 Toolkit 创建简单的 Web 应用程序

学习 Toolkit 的最佳方法是创建一个应用程序。在本节中，你将修改从书籍配套网站 (www.wrox.com) 下载的 FindExpertDemo 示例。

# FindExpertDemo 项目

FindExpertDemo 是一个简单的 ASP.NET 应用程序，用于显示所选专家的信息。页面上有两个列表。第一个允许你选择专业。第二个下拉列表填充了选择该专业的人。当你选择其中一人时，会显示专家的照片和简短描述。

图 20-3 显示了该程序的运行情况。

![](img/b5597c749e848b27b0d305153ae16106_937_0.png)

**FIGURE 20-3: FindExpertDemo 的截图**

