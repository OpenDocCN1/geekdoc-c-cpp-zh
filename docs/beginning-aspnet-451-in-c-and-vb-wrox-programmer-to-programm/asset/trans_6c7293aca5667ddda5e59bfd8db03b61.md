

在 p2p.wrox.com 你会找到多个不同的论坛，它们不仅在你阅读本书时能帮助你，也能在你开发自己的应用程序时提供帮助。要加入论坛，只需按照以下步骤操作：

- 1. 前往 p2p.wrox.com 并点击 Register New 链接。
- 2. 阅读使用条款并点击 Agree。
- 3. 填写加入所需的必填信息以及你希望提供的任何可选信息，然后点击 Submit。
- 4. 你将收到一封电子邮件，其中包含有关如何验证你的账户并完成加入流程的信息。

你可以在不加入 P2P 的情况下阅读论坛中的消息，但要发布自己的消息，你必须加入（免费）。

加入后，你可以发布新消息并回复其他用户的消息。你可以在首页的 ASP.NET 4.5.1 类别下找到本书专属的论坛。你可以随时在网上阅读消息。如果你希望收到来自特定论坛的新消息，请在论坛列表中论坛名称旁点击 Subscribe to this Forum 图标。

有关如何使用 Wrox P2P 的更多信息，请务必阅读 P2P FAQs，以获取有关论坛软件工作原理以及与 P2P 和 Wrox 书籍相关的许多常见问题的答案。要阅读常见问题解答，请点击任何 P2P 页面上的 FAQ 链接。

## 1
开始使用 ASP.NET 4.5.1

本章你将学习的内容：

- 如何获取和安装 Visual Studio Express 2013 for Web 和 Visual Studio Express
- 如何使用 Visual Studio Express 2013 创建你的第一个网站
- ASP.NET 页面如何被服务器处理并发送到浏览器
- 你如何使用和自定义开发环境

自 2002 年初发布 .NET Framework 1.0 以来，Microsoft 就投入了大量精力和开发时间用于 ASP.NET，即 .NET Framework 中用于构建 Web 应用程序的部分。此次首次发布意味着从旧的 Microsoft 用于构建网站的技术 Active Server Pages（ASP），现称为经典 ASP，发生了根本性的变化。ASP.NET 1.0 的引入以及随附的 Visual Studio .NET 为开发人员相比经典 ASP 带来了以下优势：

- 表现层与代码之间的清晰分离。在经典 ASP 中，你的编程逻辑通常散布在页面的 HTML 中，使得日后更改页面变得困难。
- 更接近桌面应用程序编程方式的开发模型。这使得许多 Visual Basic 桌面程序员更容易转向 Web 应用程序。
- 功能丰富的开发工具（称为 Visual Studio .NET），使开发人员能够以可视化方式创建和编码其 Web 应用程序。

## CHAPTER 1 GETTING STARTED WITH ASP.NET 4.5.1

- 在多种面向对象编程（OOP）语言中进行选择，其中 Visual Basic .NET 和 C#（发音为 C-Sharp）现在是最受欢迎的。

- 访问 .NET Framework，首次 Web 开发人员拥有统一且易于访问的方式来使用高级功能来处理数据库、文件、电子邮件、网络工具等。

尽管 ASP.NET 相比旧模型有很多优势，使用 ASP.NET 也意味着复杂性的增加以及构建应用程序所需的知识增加，使得许多新程序员更难开始使用 ASP.NET。

在 2002 年首次发布后，Microsoft 发布了另一个版本的 .NET Framework（称为 .NET 1.1）以及开发 IDE（称为 Visual Studio .NET 2003）。许多人认为这是对初始发布的服务包，尽管它也在框架和开发工具中带来了大量增强。

在 2005 年 11 月，Visual Studio 2005 和 ASP.NET 2.0 发布。对世界各地的许多开发人员来说令人愉快的是，Microsoft 能够大幅改进和扩展产品，添加了许多功能和工具，有助于降低 ASP.NET 1.0 引入的复杂性。新的向导和智能控件使得可以减少构建应用程序所需的代码，降低了新开发人员的学习曲线并提高了他们的生产力。

在 2007 年 11 月，Microsoft 发布了 Visual Studio 2008 和 ASP.NET 3.5 框架，随后在 2010 年 3 月发布了 Visual Studio 2010 和 ASP.NET 4，在 2012 年 9 月发布了 Visual Studio 2012 和 .NET 4.5。每个版本都增加了大量功能，包括 LINQ（在第 14 章讨论）、AJAX Framework 的集成（你在第 10 章中了解更多）、ADO.NET Entity Framework（在第 14 章讨论）、jQuery 的包含（在第 11 章讨论）等。

当前版本 Visual Studio 2013 和 ASP.NET 4.5.1 建立在 Visual Studio 2012 和 ASP.NET 4.5 发布成功的基礎上，保留了其他领域的大量功能和工具。在接下来的 19 章中，你将学习如何使用 Visual Studio Express 2013 for Web 构建功能齐全的 ASP.NET 网站，它也是完整 Visual Studio 2013 套件的一部分。本书指导你完成创建功能齐全的数据库驱动网站的过程，从下一章的简陋开始，一直到第 19 章将其部署到生产环境。

本书附带的示例网站和所有示例都是使用 Visual Studio 2013 for Web（VSEW）构建的，因此确保你已将其安装在开发机器上非常重要。下一节将向你展示如何获取和安装 VSEW。一旦你将其运行起来，你将看到如何创建你的第一个网站，然后对 VSEW 的众多功能进行广泛的巡览。

### MICROSOFT VISUAL STUDIO EXPRESS FOR WEB

Microsoft Visual Studio（VS）拥有大量工具，可帮助你快速创建复杂的 ASP.NET Web 应用程序。

Visual Studio for Web 有两种形式：作为独立的免费版本称为 Microsoft Visual Studio 2013 for Web，以及作为更大的开发套件的一部分称为 Visual Studio 2013，后者也有不同版本，每个版本都有自己的价格标签。使用 Visual Studio 的商业版本，Web 组件完全集成。你只需启动 Visual Studio 2013 并创建 Web Site Project 或 Web Application Project，这反过来又启用了 Visual Studio 的 Web 组件。

尽管 Visual Studio 的 Express 版本是免费的，但它包含创建和功能丰富的 Web 应用程序所需的所有功能和工具。书中你找到的所有示例都可以用免费版本构建，因此无需花费大笔资金购买 Visual Studio 2013 的商业版本即可跟随本书学习。

我将使用术语 Visual Studio（VS）来指代 Visual Studio 的商业和免费版本。当专门谈论免费版本时，我将使用术语 Visual Studio Express 2013 for Web。

获取 Visual Studio 很简单。你可以从 Microsoft 网站下载，如下所述。

### Getting Visual Studio

你可以在 www.microsoft.com/express/ 的 Microsoft 网站上获取免费的 Visual Studio Express 2013 for Web。在 Express 首页上，依次点击 Downloads 链接，直到到达提供 Express 产品下载的页面，包括 VSEW。从此页面，你可以下载 VSEW 作为 Web Install，在此你只下载安装程序，而剩余文件在安装过程中下载。确保从页面中选择 Visual Studio Express 2013 for Web，而不是其他免费的 Express 产品或其他的 Visual Studio。

不要被 Web Install 的大小所迷惑，它只有几兆字节。你下载的文件只是安装程序，它会通过 Internet 下载所需文件。总下载量取决于你的当前系统，将在 500MB 到 1GB 之间。

如果你想尝试包含组件的 Visual Studio 2013 完整版，你可以在 Microsoft 网站 http://msdn.microsoft.com/vstudio 上注册免费试用。你可以选择下载 ISO 以便刻录到 DVD，或选择下载 Web Installer。

最后，你可以使用 Microsoft Web Installer（WPI）应用程序下载 VSEW，该应用程序可在 www.microsoft.com/web/platform 和 www.asp.net/downloads/ 上获取。除了 VSEW 之外，此工具还为你提供访问许多其他与 Web 开发相关的工具和程序。WPI 是一个优秀的工具，可以一次性获取大量与 Web 开发相关的程序和工具。我经常使用它在干净的开发机器上快速启动。

### Installing Visual Studio Express for Web (VSEW)

安装 VSEW 是一个直接的、尽管有些冗长的过程。根据你的安装方法、计算机和 Internet 连接速度，安装 VSEW 可能需要 20 分钟到一个小时——甚至更长时间。

