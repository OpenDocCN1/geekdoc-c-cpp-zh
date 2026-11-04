
尽管它已经很不错了，Professional 并不具备微软提供的全部功能。全面的团队管理功能、报告、签入和测试功能都保留给了价格昂贵版本：Team System。

## Team System

Visual Studio Team System，通常简称为 VSTS，是微软平台的最高掌权者。它连接到 Team Foundation Server（微软提供软件开发团队度量数据的产品），当团队参与开发时，它能提供大量软件创建度量数据。

图 1-1 显示了我所说的一些内容。构建统计数据和开发细节可以通过 SharePoint 提供的仪表板收集。

事实就是事实——Team System 是很酷的软件，但如果没有庞大的企业环境围绕它，它根本无法正常工作。它需要 SharePoint、Exchange 和 SQL Server 才能正常运行。

![](img/80ff26f06fc9ab951e1cd4257b867366_529_0.png)

**图 1-1：** 使用 Team Foundation Server 管理软件开发。

## MSDN

Microsoft Developer Network（MSDN）订阅是获取微软产品迄今为止最好的方式。似乎搭建一个用于开发任何重要东西的开发环境会贵得离谱。这不一定是真的。

MSDN 订阅正如其名——对大多数重要的微软产品的订阅。每年大约一千美元，你就能获得所需的一切。这实际上并不是 Visual Studio 的一个版本。

听起来很多，但换个角度想——即使你一年只做一个业余项目，你的投资也会回本。考虑到仅 Visual Studio 本身就占了一半，而且大约每两年更新一次，这很划算。除了 Visual Studio Professional，你还获得以下订阅：

- Microsoft Office
- Windows 客户端平台
- Windows Server 平台
- SQL Server
- 像 SharePoint 和 BizTalk 这样不错的中间件
- 你以前从未使用过（但现在会用）的奇怪组件

基本上运作方式是这样的——你去 Amazon 或其他地方购买一个 MSDN 许可证代码。然后你去 `http://msdn.microsoft.com` 用你的 Live 账户注册该代码。从那里，根据你的许可证级别，你只能将软件下载用于开发。

这一点很重要。从 MSDN 获得的产品仅用于开发目的。所以，是的，你可以获得 SQL Server（例如）。不，你不能使用 MSDN 许可证在互联网上架设你的新 Widget 商店。

因此 MSDN 许可证中的操作系统仅用于开发。这没问题。这是一本开发书籍。如果你能获得 MSDN，就去获得它。

## Academic

如果你买不起 MSDN 但你是学校学生或讲师，请购买面向学习机构的 Visual Studio 学术版。它的价格比 MSDN 便宜，但从许可角度来看限制更严格。

![](img/80ff26f06fc9ab951e1cd4257b867366_530_0.png)

学术版现在只需一百美元左右。这意味着它比免费的 Express 版贵，但它拥有 Professional 的所有功能。如果你只是为了学习，这是一个有用的选择。但如果你想部署生产软件，则需要另寻他处。该产品未获得此许可。

学生、老师，去学校书店吧。如果他们没有 Visual Studio Academic，告诉他们应该引进它。

## An edition breakdown under MSDN

表 4-1 描述了微软认为的重要功能以及不同版本中的功能。星号代表对特定功能的支持级别。我在每次向客户推荐软件时都会使用它，希望你也觉得它同样有用。

表 4-1 Visual Studio 版本

| Visual Studio 2012 | VS 2012 Professional with MSDN | VS 2012 Premium with MSDN | VS 2012 Ultimate with MSDN |
|---|---|---|---|
| Team Foundation Server | **** | **** | **** |
| Development Platform Support | **** | **** | **** |
| Testing | * | *** | **** |
| Database Development |  | **** | **** |
| Debugging and Diagnostics | ** | *** | **** |
| Architecture and Modeling |  | * | **** |
| Lab Management |  |  | *** |

## Installing Visual Studio

Visual Studio Professional，即本书大部分内容使用的版本，像其他 Windows 程序一样安装。首先，确保你的机器能够运行 Visual Studio。然后运行安装程序（或从 DVD 自动运行）并做出一些决定。

然后你等待。Visual Studio 体积很大。需要一段时间。

Visual Studio 的官方要求如下所示：

- **操作系统：**
  - Windows 7 SP1
  - Windows 8
  - Windows Server 2008 R2 SP1
  - Windows Server 2012
- **支持的架构：**
  - 32 位 (x86)
  - 64 位 (x64)
- **硬件：**
  - 1.6 GHz 或更快的处理器
  - 1GB of RAM
  - 10GB of available hard disk space
  - 5400 RPM drive
  - DirectX 9-capable video card at 1024x768

你可以在此配置上运行——我试过，可以工作。只是不美观。Visual Studio 2012 全部用 WPF 编写，这对于如此庞大的应用程序来说可能很耗资源。

既然如此，我相信你不会对我有一套安装 Visual Studio 的建议感到惊讶。

首先，这里是我认为 Visual Studio 的一个现实基础配置：

- 2.4 GHz 64 bit dual core processor
- 64-bit Windows 8 with 8GB of RAM
- 250GB of available HDD space
- Dual monitors (or a laptop with an external monitor) with one being a touch screen

- 2.4 GHz 64 位双核处理器
- 配备 8GB RAM 的 64 位 Windows 8
- 250GB 可用 HDD 空间
- 双显示器（或带外接显示器的笔记本电脑），其中一个为触摸屏

看起来过分？并不。首先，我建议你对任何会影响 Windows 基础安装的项目使用虚拟机。Virtual PC 是免费的，而且你通常可以毫无问题地获得 Windows 8 的 180 天试用版。将 Virtual PC 设置为仅在机器运行时运行时钟，你就拥有了一个完美的测试环境。

![](img/80ff26f06fc9ab951e1cd4257b867366_533_0.png)

要查找 Virtual PC，请在 http://download.microsoft.com 上搜索 Virtual PC。要查找更改虚拟机时钟的技巧，请访问 Virtual PC Guy 的博客 http://www.virtualpcguy.com 并搜索 "clock only while active"。

不过这个方案需要资源。你必须有 4GB RAM，这样才能分配 2GB 给虚拟机。虚拟硬盘通常约为 13GB，所以你需要空间。双显示器使你可以在虚拟机全屏运行的同时轻松查看主机操作系统。

即使你不打算在虚拟 PC 中运行（但我建议你这样做），你仍然需要一个可靠的双核处理器和大量 RAM。为什么要节省？硬件很便宜，你的时间可不便宜！

## Breaking Down the Projects

在运行安装程序并设置默认设置后，剩下的就是开始一个项目并动手实践。第一、二本迷你书中的所有项目类型（可能一两个除外）都是控制台应用程序，意味着它们 intended 在命令行提示符下运行。还有很多其他项目可用。

请注意 Visual Studio 新建项目对话框中的四种主要项目类型。

- **Windows Store projects** 是面向 Windows 8 用户的全屏打包应用，可放入 Windows Store。它们通常不是（为分发而打包），而是部署到商店以便在那里分发。
- **Windows projects** 是丰富的客户端应用程序，编译为 .EXE 并在你的计算机上运行。Microsoft Word 就是一个 Windows 应用程序。
- **Web projects** 用于创建网站，需要 Web 服务器运行。（Visual Studio 为开发目的包含了一个 Web 服务器。）Microsoft.com 就是一个 Web 应用程序的例子。
- **Special projects** 包括诸如安装项目（构建安装程序的项目）和数据库项目（为数据库提供框架的项目）等。它们通常与 Windows 或 Web 应用程序一起使用。你在上一节中运行以安装 Visual Studio 的 Setup.exe 程序就是这些特殊项目之一——一个安装项目。
