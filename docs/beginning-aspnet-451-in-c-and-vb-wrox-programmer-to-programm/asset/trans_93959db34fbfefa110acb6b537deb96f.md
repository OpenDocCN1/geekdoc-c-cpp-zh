

# 在 IIS 下运行你的站点 | 75

- 1. 安装并配置 IIS。
2. 安装并配置 .NET Framework 4.5.1。
3. 配置安全设置。

根据你系统的当前状态，这些操作中的某些是可选的。在接下来的章节中，将介绍如何执行这些步骤。

> 注意：安装和配置 Web 服务器可能是一项复杂的任务。你有许多因素需要考虑，包括你的操作系统、其配置、你用于登录机器的账户、你将要使用的最终 SQL Server 等。如果你遇到困难，请不要惊慌，可以访问 IIS 网站查看详细的步骤说明，或者访问本书自带的讨论论坛 http://piz.prox.com，在那里你将找到可以帮助你成功的程序员（比如我）。

本章余下部分所描述的步骤应该可以在 Windows 7、Windows 8 和 8.1、Windows Server 2008 R2 以及 Windows Server 2012 / 2012 R2 上运行。有关 IIS 的更多信息，包括在本文中未讨论的旧版本 Windows 上安装 IIS 的帮助信息，请访问官方 IIS 网站 www.iis.net。

## 安装并配置 Web 服务器

尽管大多数 Windows 版本都带有 IIS，但它默认并没有安装，因此你需要先进行此操作。你还需要确保你的 Windows 版本支持 IIS。虽然 Windows 7 和 8 的 Starter 版和 Home Basic 版带有 IIS 的部分组件，但你无法在上面运行 ASP.NET 页面，因此你至少需要 Home Premium 版（家庭高级版）。在基于服务器的 Windows 版本上，IIS 是完全支持的。如果你使用外部托管公司托管站点，可以跳过以下安装 IIS 的步骤。

> 注意：尽管 Windows 7 和 Windows 8 等消费级 Windows 版本支持 IIS，但并不意味着这些操作系统是托管你网站的最佳选择。你通常将这些版本的 Windows 用于本地开发和测试，而 Windows 的服务器版本（如 Windows Server 2008 R2 和 Windows Server 2012 / 2012 R2）则用于托管生产环境网站。

要在你的 Windows 机器上安装并配置 IIS，你需要以管理员身份登录。如果你用于登录机器的账户没有管理员权限，你需要请求你的管理员为你安装并配置 IIS。

除了安装 IIS 之外，你还将看到如何在 IIS 中创建和配置网站。由于 Windows 下安全机制的工作，除非更改 Windows 下的某些安全设置，否则你的站点在配置 IIS 之后可能无法运行。你将在“理解 IIS 中的安全”章节以及标题为“配置文件系统”的试练习中看到如何操作。

如果你已经安装了 SQL Server 2012 Express，你将能够更容易地测试你的 IIS 设置。如果你跟做了第 12 章练习的步骤，通常就是这种情况。如果你还没有安装 SQL Server 2012 Express，请参阅第 12 章中的“安装 SQL Server 2012 Express”章节以获取安装说明。如果你拥有 SQL Server 的商业版本之一，或者在远程机器上拥有 SQL Server，请特别注意本章中的“将数据移动到远程服务器”章节以及附录 B。

## 确保 IIS 已安装

安装 IIS 最简单的方法是通过 Web 平台安装程序 (WPI)。WPI 随 Visual Studio 一起安装，因此如果你在开发机器上执行这些步骤，你已经拥有 WPI 了。如果你在另一台机器（例如运行 Windows Server）上执行这些步骤，将需要先下载并安装 WPI。你可以从 www.microsoft.com/web/downloads 下载 WPI，在那里你应该能看到“Download”或“Download It Now”按钮。如果此链接发生变化，请在网上搜索“Web Platform Installer download”以找到允许下载和安装 WPI 的其他位置。

一旦安装了 WPI，它可能会自动启动。发生时，清除任何可能被选择自动安装的程序。从 Windows 开始菜单或开始界面启动 WPI。完成后，切换到屏幕顶部的 Products（产品）选项卡，找到 IIS 项并按回车。WPI 应该列出 IIS 推荐配置，如图 19-5 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_773_0.png)

图 19-5

如果 Add（添加）按钮被禁用，点击 Add 将此项添加到安装项列表中，说明部分 IIS 已经安装。

接下来，再次使用搜索框搜索 IIS: ASP.NET。根据你的 Windows 版本，这应该弹出一个名为 IIS: ASP.NET 或 IIS: ASP.NET 4.5 的项目（以及一些无关的项目）。在 IIS 下运行 ASP.NET 需要 IIS: ASP.NET 或 IIS: ASP.NET 4.5 项目，它是成功运行你站点的关键组件。选择此项目并点击 Add。如果你看到两个项目，请选择 IIS: ASP.NET 4.5。最后，点击屏幕底部的 Install（安装）按钮并接受许可条款。过了一会儿，你应该收到 IIS 及其组件已成功安装的确认。

有关手动设置 IIS 的详细说明，请查看官方 IIS 网站上的这些文章或搜索 www.iis.net：

```
http://bit.ly/IISOnServer2008
```

```
http://bit.ly/IISOnServer2012
```

成功安装 IIS 后，你需要确保你拥有 Microsoft .NET Framework 版本 4.5.1。

## 安装并配置 ASP.NET

如果你在目标机器上安装了 Visual Studio 2013（任何版本），你已经安装了 .NET Framework 4.5.1。否则，你需要从 Microsoft 网站 http://mdn.microsoft.com/en-us/framework 下载重新发行包。点击 Download 或 Install 链接，或者使用搜索选项“download .NET Framework 4.5.1”。

确保下载的是 .NET 4.5.1 Framework 的完整版本，而不是早期版本或 Client Profile。下载 .NET Framework 后，运行安装程序并按照屏幕上的说明操作。如果你收到显示框架已安装的消息，可以关闭安装程序。

如果你的机器上已经有了 .NET Framework 4.5.1 之后安装了 IIS，你需要告诉 IIS 框架的存在。通常这在安装 .NET Framework 期间完成，但如果你后安装了 IIS，则需要手动执行。你只需要在 Windows 7 上这样做：

- 1. 以管理员身份打开命令提示符。这样做请点击开始按钮，在搜索框中输入 cmd 并按回车。

- 2. 输入以下命令进入 .NET Framework：

```
cd \Windows\.NET\v4.0
```

注意，如果你使用的是 64 位的 Windows，在进入命令提示符前应使用 Framework64 文件夹。

 3. 输入 aspnetreg -i 并按回车。

过了一会儿，你会收到 ASP.NET 已在 IIS 中注册的消息。

现在 IIS 已成功安装，你需要确保你拥有 Microsoft .NET Framework 版本 4.5.1。

## 安装并配置 ASP.NET

如果你在目标机器上安装了 Visual Studio 2013（任何版本），你已经安装了 .NET Framework 4.5.1。否则，你需要从 Microsoft 网站 http://mdn.microsoft.com/en-us/framework 下载重新发行包。点击 Download 或 Install 链接，或者使用搜索选项“download .NET Framework 4.5.1”。确保下载的是 .NET 4.5.1 Framework 的完整版本，而不是早期版本或 Client Profile。下载 .NET Framework 后，运行安装程序并按照屏幕上的说明操作。如果你收到显示框架已安装的消息，可以关闭安装程序。

如果你的机器上已经有了 .NET Framework 4.5.1 之后安装了 IIS，你需要告诉 IIS 框架的存在。通常这在安装 .NET Framework 期间完成，但如果你后安装了 IIS，则需要手动执行。你只需要在 Windows 7 上这样做：

- 1. 以管理员身份打开命令提示符。这样做请点击开始按钮，在搜索框中输入 cmd 并按回车。

- 2. 输入以下命令进入 .NET Framework：

```
cd \Windows\.NET\v4.0
```

注意，如果你使用的是 64 位的 Windows，在进入命令提示符前应使用 Framework64 文件夹。

 3. 输入 aspnetreg -i 并按回车。

过了一会儿，你会收到 ASP.NET 已在 IIS 中注册的消息。

现在 IIS 已成功安装，你需要确保你拥有 Microsoft .NET Framework 版本 4.5.1。

## 安装并配置 ASP.NET

（注：此处原文内容存在重复，根据指令“不要重复输出原文”的原则，此处不再重复翻译重复内容）

## 确保 IIS 已安装

（注：此处原文内容存在重复，根据指令“不要重复输出原文”的原则，此处不再重复翻译重复内容）

## 配置你的站点

在本练习中，你将看到如何配置 IIS 带的标准“Default Site”。虽然在 Windows 7、Windows 8 / 8.1、Windows Server 2008 R2 以及 Windows Server 2012 / 2012 R2 上可以在 IIS 下创建多个站点，但本文未讨论该选项。联系你的系统管理员或阅读随附附的文档以了解在 IIS 下创建网站。Windows 8 中的大部分步骤与 Windows 7、Windows Server 2008 R2 以及 Windows Server 2012 完全。然而，你在练习中看到的截图是在 Windows 8.1 中拍摄的，与其他操作系统不同。

如果你不在用于构建 Planet Wrox 站机器上操作，请确保将 BEPRET 文件夹拷贝到目标机器的 C 盘。同时确保该机器可以访问 SQL Server 2012，无论是本地安装还是在远程机器上。

- 1. 打开信息服务 (IIS) 管理器。你可以在控制面板的管理工具中找到它。或者，点击开始按钮或开始屏幕，输入 inet 并按回车。如果弹出关于了解 WPI 的问题，点击否（如果你想了解分类则可以点击是）；如果是这样，你将被带到 Microsoft 网站的主页。

- 2. 展开左侧的树，直到看到 Application Pools（应用程序池）和 Default Web Site（默认网站），如图 19-6 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_775_0.png)

图 19-6

