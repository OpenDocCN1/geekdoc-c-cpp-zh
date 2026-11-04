
- 第14章介绍 .NET 3.5 中的一项新功能：语言集成查询（LINQ）。它涵盖了 LINQ 的所有重要实现——LINQ to Objects、LINQ to XML、LINQ to Dataset 和 LINQ to SQL。

- 第15章探讨程序集的概念。在 .NET 中，可部署的基本单元称为程序集。程序集在开发过程中起着重要作用，理解它们的工作方式有助于你开发可缩放且高效的 .NET 应用程序。

## 第II部分：使用 C# 进行应用程序开发

- 第16章演示如何使用 C# 语言构建 Windows 应用程序。示例应用程序说明如何使用 .NET Framework 中可用的类执行 FTP。你还将了解如何在 .NET 应用程序中执行打印，以及如何使用 ClickOnce 技术部署 Windows 应用程序。

- 第17章带你构建一个使用 C# 的 ASP.NET Web 应用程序。你使用新的 LinqDataSource 控件执行数据绑定，并了解如何让网页支持 AJAX。

- 第18章说明如何使用 .NET Compact Framework（.NET Framework 的一个子集）进行 Windows Mobile 开发。它考察 Windows Mobile 开发的基础知识，并构建一个示例 RSS 阅读器应用程序。最后，它展示如何为你的应用程序创建专业的安装包，以便分发给你的读者进行安装。

- 第19章帮助你开始使用 Silverlight，并让你有机会体验 Silverlight 开发的工作方式。它涵盖 Silverlight 1.0 和 2，并包含若干示例展示 Silverlight 的能力，包括动画、媒体和 .NET 集成。

- 第20章简要介绍新的 Windows Communication Foundation（WCF）技术，并说明它如何解决当今 Web 服务技术的一些局限性。虽然大多数书籍和会议非常注重 WCF 背后的理论，但本章展示如何构建 WCF 服务，然后解释其背后的理论。本章最后给出一个创建票务应用程序的示例，允许多个客户端实时获取更新的座位信息。

## 第III部分：附录

- 附录A列出 C# 中各种预定义且对编译器有特殊意义的关键字。

- 附录B总结 .NET Framework 各个版本的功能，并说明如何使用 Visual Studio 2008 中的对象浏览器功能浏览 .NET Framework 中可用的命名空间和类。

- 附录C展示如何使用 Visual Studio 2008 和第三方文档生成工具 Sandcastle 为你的项目生成 MSDN 风格的文档。

## 使用本书所需的条件

对于本书演示的所有示例，我使用的是 Microsoft Visual Studio Team System 2008。不过，Microsoft 已经发布了大量 Visual Studio 版本，旨在满足不同类型的 C# 开发人员的需要：

- [ ] Visual Web Developer 2008 Express Edition
- [ ] Visual C# 2008 Express Edition
- [ ] Visual Studio 2008 Standard Edition
- [ ] Visual Studio 2008 Professional Edition
- [ ] Visual Studio 2008 Team System Architecture Edition
- [ ] Visual Studio 2008 Team System Database Edition
- [ ] Visual Studio 2008 Team System Development Edition
- [ ] Visual Studio 2008 Team System Test Edition
- [ ] Visual Studio 2008 Team System Team Suite

*有关每个版本中可用功能的详细讨论，请查看以下 URL：*
http://msdn.microsoft.com/en-us/vs2008/products/cc149003.aspx。

Express 版专为爱好者设计，可免费下载。这是开始使用 Visual Studio 2008 的好方法，非常适合学生和初级程序员。但是，如果你是一名专业开发人员，则应购买 Standard 版或 Professional 版。如果你要开发 Windows Mobile 应用程序，则需要 Professional 版（或更高版本）。如果你在大型开发环境中工作，并且需要在大型项目中与其他开发人员协作开发，请查看 Team System 版本。

*如果你还没有准备好购买 Visual Studio 2008，可以随时从* http://msdn.microsoft.com/en-us/vs2008/products/cc268305.aspx 下载 Visual Studio 2008 Professional 的90天试用版。

根据你使用的 Visual Studio 版本，本书中演示的某些步骤在你的屏幕上可能不完全相同。不过，这些差异很小，按照每章概述的步骤操作应该不会有任何问题。

此外，使用 Windows Vista 的读者应以管理员模式启动 Visual Studio 2008（以及命令提示符窗口）。具体操作如下：

- [ ] 单击 Vista“开始”按钮。
- [ ] 找到要启动的程序（Visual Studio 2008 或命令提示符）。
- [ ] 右键单击该程序，然后选择“以管理员身份运行”。

## 约定

本书通篇使用若干约定，以帮助你充分利用正文并跟踪正在发生的事情。

像这样的方框包含与周围正文直接相关的重要且不可忘记的信息。

*提示、技巧、窍门以及与当前讨论相关的题外话会单独列出，并像这样以斜体显示。*

至于正文中的样式：

- 新术语和重要词语会被突出显示并加以介绍。
- 键盘按键如下所示：Ctrl+A。
- 正文中的文件名、URL 和代码如下所示：`persistence.properties`。
- 代码以两种不同方式呈现：

```
Code examples nearly always look like this.
```

灰色高亮用于显示在现有代码中添加新代码的位置，或指出正文中正在解释的特定代码段。

## 源代码

在学习本书中的示例时，你可以选择手动输入所有代码，也可以使用本书附带的源代码文件。本书使用的所有源代码均可在 www.wrox.com 下载。进入该网站后，只需找到本书的书名（通过使用搜索框或使用其中一个标题列表），然后单击图书详情页上的 Download Code 链接，即可获取本书的所有源代码。

## 勘误

我们尽一切努力确保正文或代码中没有错误。然而，人无完人，错误确实会发生。如果你在我们的一本书中发现错误，例如拼写错误或代码缺陷，我们将非常感谢你的反馈。通过提交勘误，你可能会为另一位读者节省数小时的烦恼，同时也会帮助我们提供更高质量的信息。

## 引言

要查找本书的勘误页面，请访问 www.wrox.com，并使用搜索框或其中一个标题列表找到书名。然后，在图书详情页上单击 Book Errata 链接。在此页面上，你可以查看已为本书提交并由 Wrox 编辑发布的所有勘误。包含每本书勘误链接的完整图书列表也可在 www.wrox.com/misc-pages/booklist.shtml 获取。

如果你在 Book Errata 页面上没有发现“你的”错误，请访问 www.wrox.com/contact/techsupport.shtml，并填写那里的表单，将你发现的错误发送给我们。我们将检查这些信息，并在适当的情况下将消息发布到本书的勘误页面，并在本书的后续版本中修复该问题。

## p2p.wrox.com

如需与作者和同行讨论，请加入 p2p.wrox.com 上的 P2P 论坛。这些论坛是一个基于 Web 的系统，供你发布与 Wrox 图书及相关技术有关的消息，并与其他读者和技术用户互动。论坛提供订阅功能，可在论坛有新帖子发布时，通过电子邮件向你发送你所选择感兴趣的主题。Wrox 作者、编辑、其他行业专家以及你的读者同伴都会出现在这些论坛中。

在 http://p2p.wrox.com 上，你会发现许多不同的论坛，它们不仅在你阅读本书时对你有所帮助，而且在你开发自己的应用程序时也会有所帮助。要加入论坛，只需按照以下步骤操作：

1. 访问 p2p.wrox.com，然后单击 Register 链接。
2. 阅读使用条款，然后单击“同意”。
3. 填写加入所需的必填信息以及你希望提供的任何可选信息，然后单击“提交”。
4. 你将收到一封电子邮件，其中说明如何验证账户并完成加入流程。

> > 你无需加入 P2P 即可阅读论坛中的消息，但要发布自己的消息，必须加入。

加入后，你可以发布新消息并回复其他用户发布的消息。你可以随时在 Web 上阅读消息。如果你希望将特定论坛的新消息通过电子邮件发送给你，请单击论坛列表中论坛名称旁的 Subscribe to this Forum 图标。

有关如何使用 Wrox P2P 的更多信息，请务必阅读 P2P FAQs，以获取有关论坛软件工作原理的问题的答案，以及许多针对 P2P 和 Wrox 图书的常见问题。要阅读 FAQs，请单击任何 P2P 页面上的 FAQ 链接。

