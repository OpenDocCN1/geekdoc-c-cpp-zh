
图 1-1 显示了我所说的一些内容。构建统计信息和开发细节可使用 SharePoint 中提供的仪表板收集。

事实就是事实——Team System 是很酷的软件，但如果没有庞大的企业环境围绕它，它就无法正常工作。它需要 SharePoint、Exchange 和 SQL Server 才能正常运行。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_509_0.png)

图 1-1：使用 Team Foundation Server 管理软件开发。

## MSDN

Microsoft Developer Network（MSDN）订阅是获取 Microsoft 产品迄今为止最好的方式。似乎设置一个用于开发任何有意义东西的开发环境会花费难以置信的昂贵。这不一定是事实。

MSDN 订阅正如其名所说——对大多数重要的 Microsoft 产品的订阅。每年大约一千美元，你就能获得所需的一切。这实际上并不是 Visual Studio 的一个版本。

这听起来很多，但换个角度想——即使你一年只做一个业余项目，你的投资也会得到回报。

考虑到仅 Visual Studio 本身就占其中的一半，而且大约每两年就会更新一次，这绝对物有所值。除了 Visual Studio Professional，你还可获得以下所有订阅：

- Microsoft Office
- Windows 客户端平台
- Windows Server 平台
- SQL Server
- 像 SharePoint 和 BizTalk 这样整洁的中间件
- 你以前从未使用过（但现在会使用）的奇怪组件

基本工作原理如下——你去 Amazon 或其他地方购买一个 MSDN 许可代码。然后你去 msdn.microsoft.com 并用你的 Live 账户注册该代码。从那里，根据你的许可级别，你可以仅用于开发目的下载软件。

这点很重要。从 MSDN 获得的产品仅用于开发目的。所以，是的，你可以获得 SQL Server（例如）。不，你不能使用 MSDN 许可在互联网上架设你的新 Widget 商店。

因此 MSDN 许可中的操作系统仅用于开发。这没问题。这是一本开发书籍。如果你能获得 MSDN，就去获得它。

## Academic

如果你买不起 MSDN，但你是学校学生或讲师，请购买专为学习机构设计的 Visual Studio 学术版。它的价格比 MSDN 更便宜，但从许可角度来看限制更大。

学术版现在只需大约一百美元。这意味着它比免费 Express 版贵，但它具有 Professional 的所有功能。如果你只是想学习，这是一个有用的选择。但如果你想部署生产软件，则需要另寻他处。该产品未获得此许可。

学生、老师，去学校书店吧。如果他们没有 Visual Studio Academic，告诉他们应该去获取。

## An edition breakdown

表 1-1 描述了 Microsoft 销售的主要功能以及不同版本中的功能。我每次向客户推荐软件时都会使用它，希望你也觉得它同样有用。

**表 1-1 Visual Studio 版本**

| Visual Studio 2010 | VS 2010 Professional 含 MSDN | VS 2010 Premium 含 MSDN | VS 2010 Ultimate 含 MSDN |
|---|---|---|---|
| 团队基础服务器 | **** | **** | **** |
| 开发平台支持 | **** | **** | **** |
| 测试 | * | *** | **** |
| 数据库开发 |  | **** | **** |
| 调试和诊断 | ** | *** | **** |
| 架构和建模 |  | * | **** |
| 实验室管理 |  |  | *** |

## Installing Visual Studio

Visual Studio Professional，即本书大部分内容使用的版本，与任何其他 Windows 程序的安装方式类似。首先，确保你的机器可以运行 Visual Studio。然后运行安装程序（或它从 DVD 自动运行）并做出一些决定。

然后你等待。Visual Studio 很大。需要一段时间。

Visual Studio 的官方要求如下所示：

- **操作系统：**
  - Windows® XP Professional 已安装 Service Pack 2、Windows Server 2003 或 32 位 Windows Vista
  - Microsoft Windows Server® 2003 with SP1, Standard x64 Edition (WOW)
  - Microsoft Windows Server 2003 with SP1, Enterprise x64 Edition (WOW)
  - Microsoft Windows Server 2003 with SP1, Datacenter x64 Edition (WOW)
  - Microsoft Windows Server 2003 R2, Standard x64 Edition (WOW)
  - Microsoft Windows Server 2003 R2, Enterprise x64 Edition (WOW)
  - Microsoft Windows Server 2003 R2, Datacenter x64 Edition (WOW)
  - Microsoft Windows XP Professional x64 Edition (WOW)
  - Windows Vista
- **客户端软件：**
  - Internet Explorer® 6.0 with Service Pack 1、Microsoft Office 2003 with Service Pack 1 或 Microsoft Office 2007、MDAC 9.0、.NET Framework 2.0
- **硬件：**
  - *最低：* 2.0 GHz CPU、512MB RAM、8GB HDD
  - *推荐：* 2.6 GHz CPU、1GB RAM、20GB HDD

你可以在此配置上运行——我试过，可以工作。只是不漂亮。Visual Studio 2010 全部用 WPF 编写，这对于如此规模的应用程序来说可能是一个资源占用大户。

鉴于情况如此，我相信你不会对我有一套安装 Visual Studio 的建议感到惊讶。

首先，这里是我认为 Visual Studio 的一个现实基础配置：

- 2.4 GHz 64 位双核处理器
- 配备 8GB RAM 的 64 位 Windows 7
- 250GB 可用硬盘空间
- 双显示器（或带外接显示器的笔记本电脑）

似乎过分？并不。首先，我建议你对任何会影响 Windows 基础安装的项目使用虚拟机。Virtual PC 是免费的，而且你通常可以毫无问题地获得 Windows 7 的 180 天试用版。将 Virtual PC 的设置更改为仅在机器运行时运行时钟，你就拥有了一个完美的测试平台。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_512_0.png)

**提示：** 要找到 Virtual PC，请在 download.microsoft.com 上搜索 Virtual PC。要找到更改虚拟 PC 时钟的技巧，请访问 Virtual PC Guy 的博客 www.virtualpcguy.com 并搜索 'clock only while active'。

不过，这个计划需要强大的性能。你必须拥有 4GB RAM，以便将其中 2GB 分配给虚拟机。虚拟硬盘通常约为 13GB，所以你需要空间。双显示器使你能够在虚拟机全屏运行的同时轻松查看主机操作系统。

## Breaking Down the Projects

在运行安装程序并设置默认设置后，剩下的就是开始一个项目并动手实践。第一、二本迷你书中的所有项目类型（可能一两个除外）都是控制台应用程序，意味着它们旨在在命令提示符下运行。还有很多其他项目可用。

请注意 Visual Studio 新建项目对话框中的三种主要项目类型。

- **Windows 项目** 是丰富的客户端应用程序，编译为 .EXEs 并在你的计算机上直接运行。Microsoft Word 是一个 Windows 应用程序。
- **Web 项目** 创建网站并需要 Web 服务器运行。（Visual Studio 包含用于开发目的的 Web 服务器。）Microsoft.com 就是一个 Web 应用程序的例子。
- **特殊项目** 包括诸如安装项目（构建安装程序的项目）和数据库项目（为数据库提供框架的项目）等内容。它们通常与 Windows 或 Web 应用程序一起使用。你在前一节中运行以安装 Visual Studio 的 Setup.exe 程序就是其中一个特殊项目的例子——一个安装项目。

### Exploring the New Project dialog box

让我们从对新建项目对话框的分解开始，如图 1-2 所示。此屏幕是 Visual Studio 可用性的重要组成部分。你可以通过点击开始页上的新建项目链接来打开它。

对话框最左侧的部分是一个树视图选择器，与 Outlook 中的类似。你有三个选项——最近使用的模板、已安装的模板和在线模板。已安装的模板处于选中状态。这些模板，如 Visual Studio 所称，是项目类型。

选择器内有一个 WPF 风格的树查看器。不同于枫树和橡树，这个树查看器包含本章后续部分描述的所有项目类别。

如果你例如在树视图中点击 Visual C# 选项，所有 Visual C# 项目都会出现在右侧的窗口中。如果你点击其中一个子选项，只有那些项目类型——针对 Visual C#——会出现。

要指定你想要开发的 .NET Framework 版本，你可以使用项目列表上方当前显示为 .NET Framework 4.0 的下拉列表。要更改排序选项，使用右侧的 Sort By：下拉列表。再向右一步，你可以更改视图选项。
