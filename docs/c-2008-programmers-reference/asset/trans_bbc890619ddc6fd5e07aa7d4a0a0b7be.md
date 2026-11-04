
在这个特定示例中，如果继续执行删除操作，您将收到运行时错误。这是因为 *titles* 表与 *titleauthor* 表相关（也是 *pubs* 数据库的一部分），而在 *titles* 表中删除记录会违反数据库的引用完整性。

## 摘要

本章开发了一个简单的 ASP.NET Web 应用程序，用于显示存储在数据库中的数据。ASP.NET 3.5 的新功能之一是 `LinqDataSource` 控件，它使您能够直接绑定到 LINQ 启用数据模型而不是数据库，因此不必为查询数据指定 SQL 语句，您可以使用 LINQ 查询。您还了解了如何使用 ASP.NET 3.5 内置的 AJAX 支持来创建响应式的 AJAX 应用程序。

## Windows Mobile 平台

Windows Mobile 平台定义了一种运行 Windows CE 操作系统并定制了标准 Microsoft 设计的用户界面外壳和应用程序的设备。使用 Windows Mobile 平台的设备包括：

- Pocket PCs
- Smartphones
- Portable Media Centers
- Automobile computing devices

对于本章，讨论仅限于前两类——Pocket PCs 和 Smartphones。（后两类使用不同的外壳，并且在当今市场上并不广泛使用。）

截至撰写本文时，Windows Mobile 平台的最新版本是 Windows Mobile 6.1。随着此次新发布，出现了一些新的命名约定。以下是微软多年来使用的 Pocket PC 和 Smartphone 名称列表。

| Pocket PCs | Smartphones |
|---|---|
| Pocket PC 2000/Pocket PC 2000 Phone Edition |  |
| Pocket PC 2002/Pocket PC 2002 Phone Edition | Smartphone 2002 |
| Windows Mobile 2003 for Pocket PC/Windows Mobile 2003 for Pocket PC Phone Edition | Windows Mobile 2003 for Smartphone |
| Windows Mobile 2003 SE (Second Edition) for Pocket PC/Windows Mobile 2003 SE (Second Edition) for Pocket PC Phone Edition | Windows Mobile 2003 SE for Smartphone |
| Windows Mobile 5.0 for Pocket PC/Windows Mobile 5.0 for Pocket PC Phone Edition | Windows Mobile 5.0 for Smartphone |
| Windows Mobile 6 Classic/Windows Mobile 6 Professional | Windows Mobile 6 Standard |

从 Windows Mobile 6 开始，Microsoft 将具有触摸屏但没有电话功能的设备定义为 Windows Mobile 6 Classic 设备（以前称为 Pocket PC 或 Windows Mobile）。图 18-1 显示了一台 Windows Mobile 6 Classic 设备（iPaq 211）。

![](img/a977a875c7c627b45d939729705a252e_599_0.png)

图 18-3

## 使用 .NET Compact Framework 开发 Windows Mobile 应用程序

为 Windows Mobile 平台开发的最简单方法是使用 Microsoft .NET Compact Framework（.NET CF）。.NET CF 是 .NET Framework 的精简版，旨在在基于 Windows CE（Windows OS 的精简版，支持 Win32 API 子集）的设备上运行。.NET CF 包含桌面版 .NET Framework 可用的类库子集，并包含一些专门为移动设备设计的新库。

截至撰写本文时，.NET CF 的最新版本是 3.5 版。以下是 .NET CF 的各种版本名称及其对应的版本号列表：

| Version Name | Version Number |
|---|---|
| 1.0 RTM | 1.0.2268.0 |
| 1.0 SP1 | 1.0.3111.0 |
| 1.0 SP2 | 1.0.3316.0 |
| 1.0 SP3 | 1.0.4292.0 |
| 2.0 RTM | 2.0.5238.0 |
| 2.0 SP1 | 2.0.6129.0 |
| 2.0 SP2 | 2.0.7045.0 |
| 3.5 Beta 1 | 3.5.7066.0 |
| 3.5 Beta 2 | 3.5.7121.0 |
| RTM | 3.5.7283.0 |

来源: http://en.wikipedia.org/wiki/.NET_Compact_Framework

知道设备上安装的 .NET CF 的版本号在开发时很有用，因为它有助于确定目标设备/模拟器上安装的确切 .NET CF 版本。

作为开发人员，您可以使用 C# 或 VB.NET 语言为 Windows Mobile 平台编写应用程序。应用程序所需的所有功能均可由以下方式满足：

- .NET CF 中的类库，和/或
- 通过 Platform Invoke (P/Invoke) 在操作系统级别的 API，和/或
- 替代第三方类库，例如 OpenNETCF 的 Smart Device Extension (SDE)

您可以通过转到 开始 ➔ 文件资源管理器 并启动位于 \Windows 中的 cgacutil.exe 实用程序来确定当前安装在 Windows Mobile 设备上的 .NET Compact Framework 版本。

图 18-4 显示了安装在 Windows Mobile 模拟器上的 .NET CF 版本（稍后会详细介绍）。

![](img/a977a875c7c627b45d939729705a252e_600_0.png)

图 18-4

Windows Mobile 5.0 设备随附预装在 ROM 中的 .NET CF 1.0，而更新的 Windows Mobile 6 设备随附预装在 ROM 中的 .NET CF 2.0。如果您的应用程序使用更新的 .NET CF v3.5，则需要在基于它的应用程序执行之前将其安装到设备上。

## 获取适当的 SDK 和工具

要使用 .NET CF 开发 Windows Mobile 应用程序，您需要下载每个平台的 SDK。以下是您需要的 SDK：

- [ ] Windows Mobile 5.0 SDK for Pocket PC
- [ ] Windows Mobile 5.0 SDK for Smartphone
- [ ] Windows Mobile 6 Professional and Standard Software Development Kits Refresh

您可以从 Microsoft 网站 (http://microsoft.com/downloads) 免费下载 SDK。使用 Visual Studio IDE 开发 Windows Mobile 应用程序的最佳工具是使用 Visual Studio 2005 Professional 或更高版本。

如果您使用的是 Visual Studio 2005，则需要下载 Windows Mobile 5.0 SDK for Pocket PC 和 Smartphone（如前所述）。如果您使用的是 Visual Studio 2008，则 Windows Mobile 5.0 SDK for Pocket PC 和 Smartphone 已默认安装。对于两个版本，您都需要下载 Windows Mobile 6 SDK 以开发 Windows Mobile 6 设备的应用程序。

安装相关 SDK 后，迈向 Windows Mobile 开发的第一步是启动 Visual Studio 2008 并创建一个新项目。选择 Smart Device 项目类型，然后选择 Smart Device Project 模板（见图 18-5）。

![](img/a977a875c7c627b45d939729705a252e_601_0.png)

图 18-5

“添加新 Smart Device 项目”对话框打开。您可以选择目标平台以及要使用的 .NET CF 版本（见图 18-6）。

![](img/a977a875c7c627b45d939729705a252e_602_0.png)

图 18-6

您现在可以开始为 Windows Mobile 开发。图 18-7 显示了 Visual Studio 2008 设计器中 Windows Mobile Form 的设计视图。

![](img/a977a875c7c627b45d939729705a252e_603_0.png)

图 18-7

## 构建 RSS Reader 应用程序

随着 Windows Mobile 6 平台的最近推出，我们现在开始看到支持 Windows Mobile 6 Standard（又名 Smartphone）的新设备不断涌现。由于 Windows Mobile 6 Standard 设备没有触摸屏，因此在为其开发应用程序时存在某些挑战。因此，在本节中，您将学习如何开发 Windows Mobile 6 Standard 应用程序，允许用户订阅 RSS 源。

RSS Reader 应用程序具有以下功能：

- 可以订阅 RSS 源以及取消订阅源
- 可以将源缓存为设备上的 XML 文件，以便设备离线时源仍然可用
- 使用 Web 浏览器查看帖子的内容

## 构建用户界面

开始时，启动 Visual Studio 2008 并使用 .NET CF 3.5 创建一个新的 Windows Mobile 6 Standard 应用程序。将应用程序命名为 `RSSReader`。

*不要忘记下载免费的 Windows Mobile 6 Standard SDK (http://microsoft.com/downloads)。您需要它来创建本章中详细描述的应用程序。*

默认的 `Form1` 使用标准表单因子 176x180 像素。由于此应用程序针对宽屏设备用户，请将 `Form1` 的 `FormFactor` 属性更改为 `Windows Mobile 6 Landscape QVGA`。

使用以下控件填充默认的 `Form1`（另见图 18-8）：

- 一个 `TreeView` 控件
- 四个 `MenuItem` 控件

![](img/a977a875c7c627b45d939729705a252e_604_0.png)

向 `Form1` 添加一个 `ImageList` 控件，并在其 `Images` 属性中添加三张图像（见图 18-9）。

*您可以从本书在 Wrox 网站上的源代码下载图像。*
