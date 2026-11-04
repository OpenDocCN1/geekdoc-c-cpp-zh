
| 版本 | 描述 |
|---|---|
| Windows 10 和通用 Windows 平台 | Windows 10 于 2015 年发布，是当前版本的 Windows，目前占据操作系统市场 15% 的份额（且仍在增长）(https://www.netmarketshare.com/operating-system-market-share.aspx)。除了许多用户界面和其他更新之外，Windows 10 还引入了通用 Windows 平台（UWP），其设计目标是在所有 Windows 设备上提供共同的平台（应用程序运行所依赖的底层系统）和用户体验，包括个人计算机、智能手机、平板电脑、Xbox，甚至 Microsoft 的新款 HoloLens 增强现实全息头显——所有这些设备都使用几乎相同的代码。 |

**图 1.2** | Windows 操作系统的演变。（第 2 部分，共 2 部分。）

### Windows 商店

你可以在 Windows 商店中出售应用或免费提供应用。撰写本书时，注册开发者的费用为个人 19 美元、公司 99 美元。Microsoft 保留购买价格的 30%（某些市场更高）。更多信息请参阅应用开发者协议：

https://msdn.microsoft.com/en-us/library/windows/apps/hh694058.aspx

Windows 商店为你的应用提供多种盈利商业模式。你可以在下载前对应用收取全价，价格从 1.49 美元起。你还可以提供限时试用版或功能受限试用版，让用户在购买完整版之前试用应用；使用应用内购买出售虚拟商品（例如额外的应用功能）等。要详细了解 Windows 商店以及如何通过应用盈利，请访问

https://msdn.microsoft.com/windows/uwp/monetize/index

### 1.6 Visual Studio 集成开发环境

C# 程序可以使用 Microsoft 的 Visual Studio 创建——Visual Studio 是一组称为集成开发环境（IDE）的软件工具。Visual Studio Community 版 IDE 使你能够快速方便地编写、运行、测试和调试 C# 程序。它还支持 Microsoft 的 Visual Basic、Visual C++ 和 F# 编程语言以及许多其他语言。本书的大多数示例都是使用 Visual Studio Community 构建的，它可在 Windows 7、8 和 10 上运行。本书有少数示例需要 Windows 10。

### 1.7 在 Visual Studio Community 中试运行 Painter

**步骤 1：检查你的设置**

阅读本书前言之后的“开始之前”部分，确认你已正确设置计算机和软件。

**步骤 2：找到 Painter 应用的目录**

打开“文件资源管理器”（Windows 8 和 10）或“Windows 资源管理器”（Windows 7）窗口，并导航到

```
C:\Users\yourUserName\Documents\examples\ch01
```

双击 Painter 文件夹查看其内容（图 1.3），然后双击 Painter.sln 文件，在 Visual Studio 中打开该应用的解决方案。应用的解决方案包含该应用的所有代码文件、支持文件（如图像、视频、数据文件等）和配置信息。我们将在下一章更详细地讨论解决方案的内容。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_46_0.png)

**图 1.3** | C:\examples\ch01\Painter 的内容。

根据你的系统配置，文件资源管理器或 Windows 资源管理器可能仅将 Painter.sln 显示为 Painter，而不显示文件扩展名 .sln。要在 Windows 8 及更高版本中显示文件扩展名：

- 1. 打开文件资源管理器。
- 2. 单击“查看”选项卡，然后确保选中“文件扩展名”复选框。

要在 Windows 7 中显示它们：

- 1. 打开 Windows 资源管理器。
- 2. 按 Alt 显示菜单栏，然后从 Windows 资源管理器的“工具”菜单中选择“文件夹选项...”。
- 3. 在出现的对话框中，选择“查看”选项卡。
- 4. 在“高级设置”窗格中，取消选中“隐藏已知文件类型的扩展名”文本左侧的框。[注意：如果此项已取消选中，则无需采取任何操作。]
- 5. 单击“确定”应用设置并关闭对话框。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_48_0.png)

**图 1.5** | 在 Windows 10 中运行的 Painter 应用。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_48_1.png)

**图 1.6** | 用小号红色画笔绘制花瓣。

**步骤 5：更改画笔颜色和大小**

点击 Green 单选按钮更改画笔颜色。然后，点击 Large 单选按钮更改画笔大小。绘制草和花茎，如图 1.7 所示。

**步骤 6：完成绘图**

点击 Blue 和 Medium 单选按钮。绘制雨滴，如图 1.8 所示，完成绘图。

**步骤 7：停止应用**

从 Visual Studio 运行应用时，你可以通过单击 Visual Studio 工具栏上的停止按钮，或单击正在运行的应用窗口上的关闭框来终止它。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_48_2.png)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_49_0.png)

**图 1.7** | 用大号绿色画笔绘制花茎和草。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_49_1.png)

**图 1.8** | 用中号蓝色画笔绘制雨滴。

现在你已完成试运行，可以开始开发 C# 应用了。在第 2 章“Visual Studio 和可视化编程简介”中，你将使用 Visual Studio 通过可视化编程技术创建你的第一个 C# 程序。正如你将看到的，Visual Studio 将为你生成构建应用 GUI 的代码。在第 3 章“C# 应用编程简介”中，你将开始编写包含你自己编写的常规程序代码的 C# 程序。

## Visual Studio 和可视化编程简介

### 目标

在本章中，你将：

- 了解用于编写、运行和调试应用的 Visual Studio Community 2015 集成开发环境（IDE）概述。
- 使用 Visual Studio 的 Windows 窗体应用程序模板创建新项目。
- 了解 Windows 窗体和用于构建图形用户界面的控件。
- 使用可视化应用开发方便地创建、编译和执行一个显示文本和图像的简单 Visual C# 应用。

- 2.1 简介
- 2.2 Visual Studio Community 2015 IDE 概述
  - 2.2.1 Visual Studio Community 2015 简介
  - 2.2.2 Visual Studio 主题
  - 2.2.3 起始页上的链接
  - 2.2.4 创建新项目
  - 2.2.5 “新建项目”对话框和项目模板
  - 2.2.6 窗体和控件
- 2.3 菜单栏和工具栏
- 2.4 浏览 Visual Studio IDE
  - 2.4.1 解决方案资源管理器
  - 2.4.2 工具箱
  - 2.4.3 属性窗口
- 2.5 帮助菜单和上下文相关帮助
- 2.6 可视化编程：创建一个显示文本和图像的简单应用
- 2.7 总结
- 2.8 Web 资源

### 2.1 简介

Visual Studio 是 Microsoft 的集成开发环境（IDE），用于创建、运行和调试用 C# 及各种其他 .NET 编程语言编写的应用（也称为应用程序）。在本章中，我们概述 Visual Studio Community 2015 IDE，然后展示如何通过将预定义构建块拖放到适当位置来创建简单的 Visual C# 应用——这种技术称为可视化应用开发。

### 2.2 Visual Studio Community 2015 IDE 概述

Visual Studio 有多个版本。本书的示例、屏幕截图和讨论均基于在 Windows 10 上运行的免费 Visual Studio Community 2015。有关安装软件的信息，请参阅前言之后的“开始之前”部分。除少数例外，本书的示例都可以在 Windows 7、8.x 或 10 上创建和运行——我们将指出任何需要 Windows 10 的示例。

这些示例也适用于 Visual Studio 完整版——尽管某些选项、菜单和说明可能有所不同。从现在开始，我们将 Visual Studio Community 2015 简称为“Visual Studio”或“IDE”。

**2.2.1 Visual Studio Community 2015 简介**

> *[注意：我们使用 > 字符表示你应从菜单中选择菜单项。例如，表示法 File > Save All 表示你应从 File 菜单中选择 Save All 菜单项。]*

首先，打开 Visual Studio。在 Windows 10 上，单击

![](img/3f5ef6be1748bb746e5f71a483bba4d0_51_0.png)

然后选择“所有应用”>“Visual Studio 2015”。在 Windows 7 上，单击

![](img/3f5ef6be1748bb746e5f71a483bba4d0_51_1.png)
