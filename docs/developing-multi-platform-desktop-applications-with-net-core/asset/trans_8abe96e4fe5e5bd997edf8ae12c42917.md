


![](img/3d310cc066dda6e2dfa67a650614076f_242_0.png)

此应用程序在 QML 代码中使用了动画和交互式更新，该应用程序未使用 C# 后端。“photoshopGUIForm”示例的目的是展示 QML 语言在动画和效果领域可以实现的效果。

这只是 QT 为实现图形动态界面所提供功能的一个缩影，但此示例将帮助你熟悉 QML 语言及其在 .NET Core 3 应用程序中的用法。

以下是该应用程序在各操作系统上运行的最终效果。

### 在 macOS 上：

![](img/3d310cc066dda6e2dfa67a650614076f_243_0.png)

### 在 Ubuntu 上：

![](img/3d310cc066dda6e2dfa67a650614076f_243_1.png)

### 在 Windows 上：

![](img/3d310cc066dda6e2dfa67a650614076f_244_0.png)

如你所见，该应用程序在各平台上的渲染效果是一致的。如果你的项目开发目标是实现这一目标，使用 Photoshop 设计的 GUI 来构建 QML.NET 应用程序似乎是一种理想的解决方案。

该应用程序的源代码及相关的 .psd 文件可在 GitHub 上找到。

## 8.7 Avalonia GUI 应用程序 (XAML)

以下是为使用 .NET Core 3 实现多平台桌面应用程序 GUI 所介绍的最后一种解决方案。这是 .NET 开发者社区中最著名、最流行的解决方案之一，因为它被视为 .NET Core 框架实现 GUI 的逻辑扩展。

### 8.7.1 Avalonia 是什么？

Avalonia 是一个基于 XAML 的多平台 GUI 框架。它于 2015 年由三位独立开发者创建：Dan Walmsley、Nikita Tsukanov 和 Steven Kirk。

Avalonia 受到 Microsoft XML 声明式界面语言 WPF 的启发，其名称也源于此。“Avalon”是 Microsoft 在 WPF 早期开发阶段使用的代号。

Avalonia 提供 XAML 支持，但也包含来自 CSS 的界面样式功能。Avalonia 采用与其他 XAML 框架（如 WPF）类似的逻辑概念，但它支持多种操作系统，如 Windows、Linux、macOS、Android 和 iOS。

经过数年的 alpha 和 beta 版本后，Avalonia 发行版于 2019 年 4 月 5 日发布（当前版本为 2019 年 7 月的 0.81 版，包含一些错误修复）。

作为一个开源项目，当前开发的源代码可在 GitHub 上免费获取，Avalonia 目前根据 MIT 许可证授权。

参考网站提供了关于 API 的丰富文档，以及开发 Avalonia 应用程序的教程和 QuickStart。

![](img/3d310cc066dda6e2dfa67a650614076f_246_0.png)

除了框架之外，Avalonia 还提供了一系列工具以实现流畅的应用程序开发，例如 Visual Studio 2019 扩展，它为 Avalonia 应用程序的开发提供多个模板和 IDE 扩展。

还可以使用其他几个有用的开源工具，例如“Avalonia Design Studio”（专用的 Avalonia IDE）和“Avalonia Themes Designer”（用于定义新主题方案）。

### 8.7.2 Avalonia Visual Studio 扩展

适用于 Visual Studio 2019 的 Avalonia 扩展可在 Visual Studio 市场上获取（当然也可以通过 Visual Studio 内部的“工具/扩展”菜单获取），你可以在下方找到下载 .vsix 文件（Visual Studio 的扩展安装程序类型）的链接。

![](img/3d310cc066dda6e2dfa67a650614076f_246_1.png)

此扩展提供多个项目模板（2个）用于创建 Avalonia 应用程序，还提供 Avalonia XAML 预览器。该扩展还提供用于创建新窗体的项目模板。

以下是安装 Avalonia 扩展后的新建项目窗口副本。

![](img/3d310cc066dda6e2dfa67a650614076f_247_0.png)

### (Avalonia 新建项目类型)

在此屏幕中，你可以找到两种新的 Avalonia 应用程序类型：

- Avalonia MVVM（模型-视图-视图模型）应用程序。
- Avalonia 客户端应用程序（经典架构）。

你可以在网站上找到关于使用这些模板创建 Avalonia 项目的详细教程。

http://avalonui.net/docs/tutorial/creating-the-project

这些模板面向多个框架：.NET Core 2 和 .NET Framework 4.6。你需要手动编辑 .csproj 文件，将 .NET Core 3 设置为唯一的目标框架。

### 8.7.3 AvalonStudio

AvalonStudio 是由英国公司 VitalElement 开发的一款开源应用程序，用于设计 Avalonia 所使用的 XAML 格式的 GUI（这与 WPF 不兼容）。

该原始应用程序可供开发者免费用于开发和设计自己的应用程序。不过，AvalonStudio 不是图形用户界面设计器（你无法在设计器中拖放控件），你需要手动编写界面代码，并在应用程序的设计器视图中可视化结果（实时）。

以下是该应用程序的发布截图。

![](img/3d310cc066dda6e2dfa67a650614076f_249_0.png)

你可以在 GitHub 上获取该应用程序的源代码

https://github.com/VitalElement/AvalonStudio/

你也可以直接为你的平台下载原生二进制文件。提供 Windows、Linux 和 macOS 版本。

http://www.vitalElement.co.uk

AvalonStudio 是 Visual Studio 扩展设计器的一个有趣的替代方案，但对 XAML 文件类型的编辑能力并无增减。

### 8.7.4 Avalonia ThemeEditor

与 WPF 类似，Avalonia 为其提供的小部件提供主题支持。这种主题支持允许开发者根据其自身应用程序（或需求）的特性自定义控件的外观。

开发者可以考虑使用一个特定工具来开发这种自定义；该工具名为“Avalonia ThemesEditor”。

![](img/3d310cc066dda6e2dfa67a650614076f_250_0.png)

（ThemeEditor 应用程序）

如上所示，此工具允许你指定颜色、字体、对齐方式……一切用于为你的应用程序构建原创 XAML 主题所需的内容。

这是一个开源工具，源代码可在 GitHub 上获取（你还会找到用于 Avalonia 开发的几个工具）。

### 8.7.5 使用 Avalonia 的示例 GUI 程序

为了帮助你开发 Avalonia 应用程序，我们将审查两个不同的项目：

- 一个使用几乎所有 Avalonia 控件的应用程序（来自 AvaloniaUI 网站的参考）。
- 一个可用作你自己的开发项目起点的基础应用程序。

这两个示例均使用 .NET Core 3 和 Visual Studio 2019 开发（即使你需要使用 SDK CLI 命令行工具构建第一个示例）。

#### 8.7.5.1 “ControlCatalog” 程序示例

本节审查的示例程序是经典的“ControlGallery”程序，该示例来自 Avalonia 主仓库，本身就是 Avalonia 框架中已提供的大量小部件（控件、对话框和窗口）使用的参考。

我们已将原始示例升级为面向 .NET Core 3 框架，在各平台上均未遇到任何特殊问题。此示例程序的代码可在 GitHub 上下载（原始版本和 .NET Core 3 版本）。

https://github.com/AvaloniaUI/ControlCatalogStandalone

.NET Core 3 版本：
https://github.com/netcore3/CodeBook/Chapter8/7/ControlCatalogStandalone

此示例名为“ControlCatalogStandalone”，是一个多页应用程序，展示了你可以在 Avalonia 应用程序中使用的主要小部件。

该项目的架构很独特，因为主要应用程序功能不在主程序项目（“ControlCatalog.Netcore”）中，而是在依赖项目（“ControlCatalog”）的 .dll 文件中。

此 .dll 文件使用 .NET Standard 2.0 开发，这种架构提高了应用程序的整体可移植性。当然，你不必为自己的项目使用相同的实现架构，但这对 Avalonia 的多平台能力是一个很好的保证。

你可以通过下方的“解决方案资源管理器”视图快速预览项目架构。

