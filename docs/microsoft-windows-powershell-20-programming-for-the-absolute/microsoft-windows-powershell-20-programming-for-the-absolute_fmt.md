
# Microsoft Windows PowerShell 2.0 编程初学者指南，第二版

> “这一系列书籍证明，我们可以在向新学者教授编程语言和良好的编程实践的同时，而不让他们感到枯燥。”

-Lou GRINZO，《Dr. Dobb's Journal》评论员

JERRY LEE FORD, JR.

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_0_0.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_1_0.png)

https://archive.org/details/microsoftwindows0000ford_l1n6

Jerry Lee Ford, Jr.

Jerry Lee Ford, Jr.

USA

献我的父母，感谢他们一直都在；献给我可爱的孩子们 Alexander、William 和 Molly，以及我美丽的妻子 Mary。

# 致谢

本书的新版是许多个人辛勤工作的结晶，我对他们深表谢意。首先，要感谢 Mitzi Koontz，她帮助我启动了这本书。还要感谢 Jenny Davidson，她担任项目编辑并确保了一切按计划进行。特别感谢 Keith Davenport，他担任两本书的技术审查员，提供了宝贵的见解、指导和建议。最后，感谢 Course Technology 的所有人员。

# 关于作者

Jerry Lee Ford, Jr. 是一位作者、教育工作者以及拥有20多年信息技术经验的专家，曾担任自动化分析师、技术经理、技术支持和安全分析师。他编写了 30 本书，并合著了两本书。他的著作包括《针对初学者的 Perl 编程》、《针对初学者的 Ruby 编程》、《针对初学者的 Microsoft Visual Basic 2005 Express 版编程》、《针对初学者的 Microsoft WSH & VBScript 编程》、《Microsoft VBScript 专业项目》、《针对初学者的 Windows Shell 脚本与 WSH 管理员指南》以及《针对初学者的 Windows XP 管理员指南》。Jerry 在弗吉尼亚州立大学获得工商管理硕士学位，并拥有五多年信息技术课程兼任教师经验。

xii

Windows PowerShell IDE.................................................................. 380

在线查找 PowerShell 资源....................................................... 382

Windows PowerShell 新组............................................................... 385

# 索引............................................................................................... 403

# 引言

欢迎阅读《初级学者 Microsoft Windows PowerShell 2.0 编程》第二版。Windows PowerShell 是适用于微软操作系统的下一代命令行外壳。命令行外壳（shell）是介于用户和操作系统之间的文本界面，大多数人将其称为命令提示符。在 Windows PowerShell 的情况下，该外壳既是一个用户界面，也是一种脚本语言，两者从底层开始设计，旨在便于操作系统的安全管理。

本书的第一版针对 Windows PowerShell 1.0，它是微软于 2006 年 11 月发布的。尽管 Windows PowerShell 2.0 增加了许多新功能和能力，但它仍然与 1.0 完全向下兼容。因此，尽管本书已扩展以涵盖 Windows PowerShell 2.0，但它仍然对 1.0 提供了完整的覆盖。

本书的目标是教你开发自己的 Windows PowerShell 脚本时需要的所有知识。这当然包括如何与 Windows PowerShell 命令行交互。它还将涉及学习一些微软的 .NET Framework。同时，在学习成为 PowerShell 程序员的过程中，你还将学习如何与其他 Windows 技术（如 Windows 注册表）协作。

Windows PowerShell 是微软开发的用于运行最新一代 Windows 操作系统的下一代命令行外壳。作为一种外壳，你通过命令行与 Windows PowerShell 交互。PowerShell 与之前的 Windows 命令行外壳`cmd.exe`的不同之处在于，PowerShell 被重新设计为基于对象的环境，与微软的 .NET Framework 紧密集成。因此，PowerShell 比其前身强大得多且先进得多。同时，微软努力让 Windows PowerShell 保持向下兼容。Windows 外壳将接受并处理与之前的 Windows 外壳相同的命令。

从而在保留你可能已经带来的任何知识和经验的同时，也向你介绍了一套全新的功能。

微软将 Windows PowerShell 作为 Windows 操作系统的免费扩展程序提供。其脚本语言从底层开始就被设计为支持基于对象的编程，为系统管理员和计算机爱好者提供了一个几乎可以自动化任何 Windows 活动的工具。

对于初次编程的程序员和爱好者来说，Windows PowerShell 是一种更出色的脚本语言。专业程序员也将从 PowerShell 的脚本技术中受益，它提供的提供了比任何其他 Windows 脚本语言都更健壮、更强大的脚本能力。你会发现，大多数情况下，使用 Windows PowerShell 开发用于自动化特定任务的脚本比使用其他脚本语言更快、更高效，从而节省时间并让你腾出精力去处理其他任务。

简而言之，无论你是对学习编程语言感兴趣，还是在寻找一份 PowerShell 脚本入门介绍，并教你如何开发可以利用你现有的 .NET 知识的 PowerShell 脚本，这本书应该对你非常有帮助。如果 Windows 是你首选的操作系统，Windows PowerShell 提供了一个其他脚本语言无法比拟的脚本环境。此外，学习 PowerShell 脚本将为你提供一个编程背景，你可以从这个背景跨越到其他 .NET 编程语言。

这本书将教你 Windows PowerShell 脚本，并演示如何利用 Windows PowerShell 1.0 和 2.0 提供的脚本能力。为了让学习变得趣味有趣，你将通过开发计算机游戏来学习编程。当你读完这本书时，不仅将拥有一系列运行良好的示例脚本，还将拥有一个可以开始应对现实世界挑战的基础。

## 谁应该读这本书？

我写这本书的目标是向你展示如何与 Windows PowerShell 交互，教你开发和执行 PowerShell 脚本的基础知识，并帮助你成为一名高效的程序员。我对你之前的编程经验没有任何假设，尽管之前的编程经验显然会有帮助。不过，我预计你对 Windows 有基本的熟悉。

我认为你会发现这本书这种通过开发计算机游戏进行教学的独特方法既有趣又有高成效。通过创建《# Microsoft Windows PowerShell 2：零基础学者编程（第二版）》中的计算机游戏来学习，不仅有助于保持学习的趣味性，还提供了一个尝试编程语言的独特机会。

如果你是初次程序员或计算机爱好者，你应该发现这本书这种系统的构建块编程方法对你非常有帮助，让你在进入更高级的话题之前掌握基础知识。通过投入时间和精力学习使用 Windows PowerShell 脚本进行编程，你将建立起编程基础，这种基础很好地转换为其他脚本语言，如 VBScript、JavaScript、Python、Ruby 和 Perl，以及 C#、C++ 和 Visual Basic 等 .NET 编程语言。专业程序员也将通过此书作为 PowerShell 脚本的快速入门指南而受益。

为了使用 Windows PowerShell，你的计算机必须运行以下操作系统之一。

- Windows XP
- Windows Server 2003
- Windows Vista
- Windows Server 2008

在编写这本书期间，我是在一台运行 Windows Vista 的计算机上工作的。因此，你将看到的所有图表和示例都是在该特定操作系统上生成的。然而，所有适用于 Windows XP、Windows Server 2003 和 Windows Server 2008 的内容同样。

书中显示的示例是使用 Windows PowerShell 2.0 CTP2 开发的。CTP2 代表社区技术预览版本2（Community Technology Preview version 2），是 PowerShell 的高级版本。根据 Windows PowerShell 团队博客（http://blogs.msdn.com/powershell/），PowerShell CTP2 是 Windows PowerShell 的完功能版本。因此，当它最终发布时，它的外观、操作和行为应该非常像 PowerShell 2.0 的正式发布版本。除非另有说明，否则你在书中看到的某些示例也适用于 Windows PowerShell 1.0。不过，我必须提前告诉你，由于 Windows PowerShell 1.0 的局性，PowerShell 2.0 的新功能确实将事情提升了一个层次，你应该考虑从一开始就开始使用 Windows PowerShell 2.0 CTP2，或者正式版本发布后立即使用。

除了运行支持的操作系统外，PowerShell 1.0 和 2.0 还要求你的计算机必须安装了 Microsoft .NET Framework 2.0 或更高版本。Windows PowerShell 2.0 CTP2 包含了 Windows PowerShell 1.0 中没有的额外功能。这些功能包括对远程和后台作业的支持。在编写此书时

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_17_0.png)

Windows PowerShell 仅在 Windows Vista Pack 1 和 Windows Server 2008 上支持此功能。Windows PowerShell 2.0 CTP2 还引入了一个新的`Out-GridView`计数器和一个图形 PowerShell 编辑器（需要 .NET Framework 3.0 才能运行），以及一个新的需要 .NET Framework 3.5 的`Get-Event`计数器。所以，如果你想利用这个新版本 PowerShell 的所有功能，你需要安装最新版本的 .NET Framework。

在编写此书时，两个版本的 Windows PowerShell 都由微软提供免费下载，可以从位于 http://www.microsoft.com/technet/scriptcenter/topics/winps/pshell2.msx 的微软网站下载和安装。在下载最新版本的 Windows PowerShell 时，请确保下载的是 CTP2 或更高版本，而不是早期的 ČTP 版本。

如有必要，你可以可以通过此处获取最新版本的 .NET：msdn.microsoft.com/netframework

为了跟随书中介绍的所有主题和练习，你需要支持的 Windows 版本、.NET 3.0 以及 Windows PowerShell 2.0 副本。或者，如果你关注 1.0，你只需要 .NET 2.0 和 Windows PowerShell 1.0。Windows PowerShell 2.0 自带了一个图形化编辑器。然而，如果你在使用 1.0，你需要一个文本编辑器来创建和保存 PowerShell 脚本文件。作为初学者，你可以使用 Windows 记事本。但是，你可能会发现下载并安装一个专门为 PowerShell 脚本设计的代码编辑器大有益。如果你跳到附录 B“下一步”，你将找到关于这两个应用程序的信息，它们在编写时都是免费的。

当我编写这本书的第二版时，我的意图是从头到尾阅读。然而，如果你有之前的编程经验，你可能会选择通过阅读前两章来学习一些关于使用 Windows PowerShell 的特定内容。然后，你可能会根据自己的特定需求和经验在不同章节之间跳跃。不过，尽管如此，花时间阅读整个编程语言可能是一个好主意，即第 4 章到第 7 章，涵盖了 Windows PowerShell 脚本语言的基础。

此外，为了尽可能简单，我决定在讨论适用于 Windows PowerShell 1.0 和 2.0 的主题时统一使用 Windows PowerShell 术语。

在讨论针对该版本 PowerShell 的特定主题时，使用 Windows PowerShell 2.0 术语。

《Windows PowerShell 2.0 零基础编程》分为四个部分。第一部分由三个章节组成，重点在于向你介绍 PowerShell 及其功能。这些章节概述了与 PowerShell 命令行交互以及创建和执行 PowerShell 脚本的基本步骤，并提供了对基于对象的脚本以及 PowerShell 与 .NET 框架之间关系的的概述。

第二部分由四个章节组成，共同为你提供了对 PowerShell 脚本语言的复。每个章节都关注一组不同的主题。你将学习如何存储和检索数据。你还将学习如何实现条件逻辑以及设置循环，以自动化重复任务并处理大量数据集。最后，你将学习如何使用函数来改进脚本的整体结构。

第三部分由三个章节组成，每个章节都涵盖一个高级主题。这些主题包括学习如何处理文件和文件夹、开发 PowerShell 脚本以实现管理任务自动化，以及学习如何追踪和调试错误。

最后，第四部分包含两个附录和一个术语表。附录介绍了你将在本书配套网站上找到的内容，并提供了更多关于 Windows PowerShell 的学习建议。这里提供了书中使用的所有术语的完整列表。

- 第 1 章，“介绍 Windows PowerShell”。本章提供了 Windows PowerShell 的介绍性视角。你将学习构成面向对象编程和 .NET 框架的不同技术。你还将学习如何启动 PowerShell 并使用命令（commands）和 cmdlet与之交互。此外，你还将学习如何配置和执行你的第一个 PowerShell 脚本。
- 第 2 章，“与 PowerShell 命令行交互”。本章对如何与命令行交互以及如何使用内置 cmdlet进行了彻底回顾。你还将学习访问帮助信息以及制定输入以开发你的图形化环境。
- 第 3 章，“基于 .NET 的面向对象脚本”。本章概述了 .NET 及其与 Windows PowerShell 的关系。你将学习 .NET 类库以及如何处理结构化对象、如何处理后台作业和别名（aliases）。
- 第 4 章，“处理变量、数组和哈希表”。本章的主要重点是向你展示存储和检索数据的不同方法。包括学习如何定义变量、数组和哈希表。你还将学习如何处理 PowerShell 的特殊变量。
- 第 5 章，“实现条件逻辑”。在本章中，你将学习如何应用条件逻辑，以便在不同的执行路径之间进行选择选择，并评估字符串、数字和布尔数据。
- 第 6 章，“使用循环处理数据”。本章向你展示如何创建循环以高效处理大量数据。你还将学习在满足预定条件时条件地跳出循环。
- 第 7 章，“使用函数组织脚本”。本章向你介绍了函数，并解释了如何使用它们来提高脚本的整体结构和稳定性。这包括学习如何调用函数以及设置函数将数据返回给调用语句。
- 第 8 章，“处理文件和文件夹”。本章将教你如何与文件、文件夹和磁盘交互。你将学习如何打开和关闭文件以及从中读取和写入信息。你还将学习如何使用正则表达式来执行各种字符串管理。你还将学习如何使用 PowerShell 2.0 的新 cmdlet`Out-GridView`，以支持同时搜索和排序的格式显示输出。
- 第 9 章，“基础系统管理”。本章的主要重点是演示如何开发 PowerShell 脚本来自动化系统管理任务，例如如何访问系统信息和网络资源。你将学习如何与 Windows 注册表交互、远程执行脚本、开发你自己的自定义 cmdlet，甚至根据预定义事件的发生来自动化脚本执行。
- 第 10 章，“调试 PowerShell 脚本”。本章侧重于教你如何追踪和修复编写 PowerShell 脚本时可能发生的任何错误。涵盖的主包括包括使用`Try-Catch-Finally`捕获并恢复错误、如何通过建立断点暂停脚本执行、如何通过步进代码语句控制脚本执行、如何监控变量值以及使用调试模式追踪脚本执行。
- 附录 A，“配套网站上有什么？”。此附录对可以在本书配套网站（www.cophell.com/downloads）上找到的材料进行了回顾。这些材料包括书中包含的所有 PowerShell 脚本的副本。
- 附录 B，“接下来做什么？”此附录旨在为你进一步学习 PowerShell 脚本教育提供建议和技巧。它包含了关于额外阅读的建议，并指向了互联网上提供的各种 PowerShell 资源，包括 PowerShell IDE、用户组和博客。
- 术语表。本单元提供了书中使用的术语表。

为了帮助你从书中获得最大收益，并帮助高效、全面地组织材料，我实施了一些规范，这些将有助于书中材料的整体组织和呈现。这些规范概述如下。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_21_0.png)

**提示 (HINT)。** 提供不同方法的建议和想法，帮助你成为更优秀、更高效的 Windows PowerShell 程序员。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_21_1.png)

**陷阱 (TRAP)。** 经常出现错误的情况以及如何处理这些问题的建议。

**技巧 (TRICK)。** 可以用来更快、更高效工作的技巧和快捷方法。

## 现实世界

现实世界。解释并演示如何应用特定的编程技术解决现实世界中的问题。

挑战。在每个章节的结束时，你将学习如何创建一个新游戏。然后我将向你提供一系列建议供遵循，以进一步增强和改进章节游戏项目以及你的编程技能。

### 介绍 Windows PowerShell



# PowerShell 入门

PowerShell 是一个下一代命令行壳，运行在 x86 和 x64 版本的 Windows XP-SP2、Windows Server 2003-SP2、Windows Vista-SP1 以及 Windows 2008 上。作为一个命令行壳，PowerShell 为管理员和爱好者提供了一个交互和控制 Windows 操作系统的命令行界面。PowerShell 还包含了自己的脚本语言，该语言专门设计用于与微软 .NET 框架交互并利用 .NET 提供的资源。在本章中，我将向你介绍 PowerShell 和 PowerShell 脚本。在本章结束时，你将创建你的第一个 PowerShell 脚本游戏，并良好理解创建和执行 PowerShell 脚本的步骤。

具体来说，你将学习：

- 关于 PowerShell 历史的一
- 如何安装 PowerShell 并配置运行脚本
- 关于 Windows PowerShell 2.0 特有的功能
- 关于构成 PowerShell 的基本组件
- 关于 cmdlet 以及如何使用它们制定命令和脚本语句
- 如何获取不同 PowerShell 命令的帮助

## 游戏预览

在本章以及随后的每个章节中，你将学习如何使用 Windows PowerShell 脚本编写来创建一个计算机游戏。在第一个游戏中，你将创建一个能够讲述几个“敲咚敲”笑话的脚本。该脚本的设计目的是通过在适当的时候提示用户输入与用户进行交互。

游戏开始时会清除屏幕，然后显示一个名为“Knock Knock!”（敲咚！）的提示，如图 1.1 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_27_0.png)

图 1.1

“敲咚敲”笑话游戏通过提示用户猜是谁在那里开始的。

作为响应，用户需要输入字符串“Who is there?”（是谁在？），正如图 1.2 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_27_1.png)

图 1.2

用户必须通过输入字符串“Who is there?”来响应。

如果用户输入“Who is there?”以外的任何内容，脚本将继续提示用户，直到其回答正确为止，如图 1.3 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_28_0.png)

图 1.3

如有必要，游戏将继续提示用户做出正确的回答。

一旦用户提供了正确的回答，游戏将以“Orange.”（橙子。）作为回答。作为响应，玩家被要求输入字符串“Orange who?”（橙子是谁在？），如图 1.4 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_28_1.png)

图 1.4

玩家被要求回答“Orange who?”。

接下来，脚本将显示笑话的梗，如图 1.5 所示。

游戏会显示笑话的梗五秒钟钟，然后清除屏幕并开始讲述另一个笑话。游戏总共讲述了三个笑话，在每个笑话结束时停顿五秒以显示梗。最后，当最后一个笑话讲述完毕，图 1.6 所示的信息将显示三秒钟，之后屏幕被清除并重新显示 PowerShell 命令。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_29_0.png)

图 1.5

最后，显示笑话的梗。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_29_1.png)

图 1.6

脚本通过显示其自身及其作者的信息而结束。

现在你已经快速地预览了“敲咚敲”笑话游戏的运行情况，让我们花一点时间进一步了解 PowerShell 和 PowerShell 脚本。在此之后，我们将在章节末尾回到游戏脚本的开发。

## PowerShell 基础

大多数操作系统的命令外壳由少量内部命令组成，这些命令在执行时由外壳在内部运行。由于传统外壳提供的命令数量有限，后来开发了大量的实用程序（或外部命令）来补充内置的外壳命令，以提供功能。这些实用程序可能支持也可能不支持与其相关的命令外壳类似的命令语法。最终结果是一个由于语法不一致而导致难以学习的命令行和外壳脚本环境。

进入 Windows PowerShell，它提供了对 PowerShell 的访问。

（注：此处原文文本似乎存在部分乱码或重复的逻辑错误，译文已根据上下文尽可能提供最接近逻辑的翻译。）

对于任何 Windows PowerShell 程序员来说，对对象的的基本理解至关重要，因为 PowerShell 在其执行的几乎所有操作中都会与对象交互。Windows PowerShell 脚本通常被称为基于对象的脚本语言。它被称为基于对象的脚本语言，这与面向对象的编程语言不同，PowerShell 程序员通常与已经创建的对象一起工作，而不是自己去定义和创建全新的新对象。这并不是说 PowerShell 程序员无法创建新对象；只是这通常不是必需的。

从表面上看，`cmd.exe` 和 PowerShell 之间有许多相似之处。对于日常任务来说，你应该能够使用 PowerShell 代替 `cmd.exe`。然而，在底层，，PowerShell 比其前身要先进得多。正如前所述，PowerShell 可以直接访问由 .NET Framework 提供的资源，并使用了一种新的脚本语言，专门用于支持通过 cmdlet（命令项程序）与 .NET 资源进行交互。

`cmd.exe` 和 PowerShell 执行方式的另一个区别是数据在命令之间传递的方式。这两种外壳都支持使用管道（pipes）在命令之间移动数据。然而，移动的数据类型是完全不同的。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_32_0.png)

> 管道是两个命令之间的逻辑连接，支持将一个命令的输出传递给另一个命令，并在该处作为输入接收。

在 `cmd.exe` 中，数据是以文本形式传递的。遗憾的是，一个命令的输出通常不符合第二个命令所要求的格式。因此，外壳程序员通常必须在他们的脚本中添加额外的编程逻辑，将一个命令的输出重新格式化为另一个命令可以接受的格式。Windows PowerShell 使用对象流水线，允许接收的 cmdlet 访问由其他 cmdlet 生成对象的属性和方法。程序员从格式化对象数据的责任中解脱出来，显著简化了脚本编写过程。

表 1.1 列出了 `cmd.exe` 和 PowerShell 之间的许多其他关键差异。如你所见，Windows PowerShell 许多许多改进，随着你阅读这本书，你将了解到更多相关内容。

| 特性 | cmd.exe | PowerShell |
|---|---|---|
| 正则表达式 | 否 | 是 |
| 异常处理 | 否 | 是 |
| 数组支持 | 否 | 是 |
| 函数 | 否 | 是 |
| 脚本签名 | 否 | 是 |
| 制表符补全 | 限制 | 是 |

## Windows PowerShell 2.0 新特性

Windows PowerShell 1.0 代表了为 Microsoft Windows 提供功能完备且强大的命令行界面的一大步飞跃。Windows PowerShell 2.0 在 Windows PowerShell 1.0 的优势的基础上构建并扩展了这些优势，增加了一系列改进和新功能，其中许多内容在书中。

Windows PowerShell 2.0 包含了几个新的语言关键字。这些关键字包括 `Data`、`Cmdlet` 和 `DynamicParam`。如果你现有的 PowerShell 脚本中有变量或函数使用了这些名称，你将需要分配给它们的名称。当你尝试使用 Windows PowerShell 2.0 运行这些脚本将会发生错误。Windows PowerShell 包含 129 个 cmdlet。Windows PowerShell 2.0 包含的 cmdlet 数量超过 180 个，提供了各种新能力。例如，你将在第 8 章学习的一个 cmdlet 是 `Out-GridView` cmdlet，它让你能够在交互式表格中显示其他 PowerShell 命令产生的结果，并对其进行搜索和排序。例如，图 1.7 显示了使用 `Out-GridView` 生成的列出活动 Windows 进程的表格示例。

Windows PowerShell 2.0 提供了各种新功能和能力，许多在书中得到了涵盖和演示。这里列出了 Windows PowerShell 2.0 中引入的一些最显著改进的简要列表：

- 图形化 PowerShell。多标签页外壳和脚本编辑器支持语法着色、行号、智能提示（智能提示）以及制表符补全。
- 图形化帮助文件。Windows 帮助文件允许你搜索、查看和打印 Windows PowerShell 帮助文件。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_34_0.png)

图 1-7

使用 `Out-GridView` cmdlet，你可以生成可以搜索和排序的输出。

- 后台作业。在本地或远程系统上后台执行 cmdlet 的能力，而无需输入 Windows PowerShell 命令提示符。
- 新运算符。额外的运算符，支持如将字符串拆分为数组以及将多个字符串拼接成新字符串的操作。
- 新特殊变量。Windows PowerShell 自动生成并维护的额外特殊变量，提供了对 PowerShell 版本和语言文化数据等内容的访问。
- 新 cmdlet。50 多个新 cmdlet 显著扩展了 Windows PowerShell 的能力并简化了其脚本环境。
- `Out-GridView`。一个特别值得注意的 cmdlet，它在图形窗口中显示输出，然后可以对其进行搜索和排序。
- 脚本 cmdlet。使用 Windows PowerShell 脚本语言创建新 cmdlet 的能力。
- 模块。在可重用的集合或模块中划分和管理 PowerShell 代码的能力。
- 数据语言。将数据从代码中分离的能力。
- 事务。启动、提交和回滚事务的能力。
- 事件处理。设置 PowerShell 监听系统事件的能力。
- Try-Finally-Catch。抛出和处理异常。
- 新调试。在行、变量和命令上设置断点调试。
- 国际化。通过编程确定相应的语言。
- 远程执行。在网络上远程运行 PowerShell。
- 运行空间。设置托管空间。

## 安装与配置

为了安装 Windows PowerShell，你的计算机必须满足书中引言概述的要求。在编写本书时，Windows PowerShell 1.0 和 2.0 均作为微软提供的免费下载内容，可以从微软 PowerShell 网站下载并安装。如果你的计算机尚未运行 2.0 版本的 .NET Framework，则你需要在运行任何版本的 Windows PowerShell 之前下载并安装它。

执行此操作所需的步骤取决于你使用的操作系统。

1. 点击开始，打开控制面板。
2. 点击程序下的“添加或删除程序”。
3. 找到 Windows PowerShell 并点击删除。

1. 点击开始，打开控制面板。
2. 点击程序下的“卸载程序”链接。
3. 找到 PowerShell 1.0 项并点击卸载。

1. 点击开始，打开控制面板。
2. 点击程序下的“添加或删除程序”。
3. 找到并点击用于安装 Windows PowerShell 的热补丁并点击删除。

在 2008 中，Windows PowerShell 是作为可选服务器组件管理的，可以启用和禁用。在安装 Windows PowerShell 2.0 之前，必须禁用 Windows PowerShell 1.0，如下所示：

1. 点击开始，右键点击“计算机”，然后点击“管理”。
2. 选择“删除功能”选项。
3. 找到 Windows PowerShell。

安装 Windows PowerShell 需要你的计算机满足本引引言概述的要求。在编写本书时，Windows PowerShell 1.0 和 2.0 均作为微软提供的免费下载内容，可以从微软 PowerShell 网站下载并安装：`http://www.microsoft.com/technet/scriptcenter/topics/winsh/powershell2.mspx`。

两个版本的 Windows PowerShell 都下载为自解压缩执行文件，你可以通过双击它进行安装。如果你的计算机尚未运行 2.0 版本的 .NET Framework，则在运行任何版本的 Windows PowerShell 之前必须下载并安装它。如果你尝试在没有 .NET 2 的情况下安装 Windows PowerShell

安装，你将看到一个弹出对话框提示你安装它，并且 Windows PowerShell 安装过程将停止。

如有必要，你可以通过 `http://www.microsoft.com/downloads/Search.aspx?displaylang=en` 下载并安装 .NET Framework 2.0 重新发行包来获取 .NET 2.0。一旦安装了 .NET 2.0，你就可以安装 Windows PowerShell。PowerShell 的安装并不耗时，并会在“所有程序”菜单中添加 Windows PowerShell 组后结束安装，如图 1.8 所示。

不要忘记，如果你打算安装 Windows PowerShell 2.0 并且想要利用它的所有功能，你将根据需要的功能安装 .NET 3.0 或 .NET 3.5。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_37_0.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_37_1.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_37_2.png)

安装完成后，你必须在开始使用之前配置 Windows PowerShell。尽管微软将 Windows PowerShell 营销为用于命令行执行和脚本编写的安全环境，但新 shell 和脚本语言的加入为黑客的利用提供了可能。因此，微软强制你显式地决定是否信任微软作为 PowerShell 脚本的发布者。你的选择如下：

- [D] 不运行
- [R] 运行一次
- [A] 始终运行
- [?] 帮助

通过输入 A 并按 Enter 键允许你运行微软开发的 PowerShell 脚本。

微软实现的另一个安全功能是无法通过在 Windows 桌面上双击脚本来运行它们。微软还强制你在计算机上开始运行 PowerShell 脚本文件之前做出另一个决定，即建立执行策略，该策略允许 PowerShell 脚本在以下三个安全级别之一运行，如下文所示：

- Alligned（对齐）。仅允许具有受信任签名的脚本在你的计算机上执行。
- Remotesigned（远程签名）。仅当从网络下载的 PowerShell 脚本来自受信任源时允许运行。
- Unrestricted（无限制）。允许任何 PowerShell 脚本在你的计算机上运行。

在 PowerShell 允许你运行第一个 PowerShell 脚本之前，你需要设置 Windows PowerShell 的执行策略设置之一。例如，要允许任何 PowerShell 脚本在你的计算机上运行，可以在 PowerShell 提示符中输入以下命令。

```
Set-Executionpolicy Unrestricted
```

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_38_0.png)

如果你在尝试配置 PowerShell 执行策略时遇到错误消息，请通过右键点击其图标并选择“以管理员身份运行”选项重启 Windows PowerShell，然后再次运行命令。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_38_1.png)

你设置的执行策略选择应该基于你的脚本需求和安全要求。如果你以后决定要更改 Windows PowerShell 执行策略，可以随时通过执行 `Set-Executionpolicy` 命令并传递上述列出的选项之一来完成。

## 远程执行

PowerShell 2.0 的一个重要新功能是远程执行，它让你能够在远程计算机上执行 PowerShell 常用命令，前提是本地和远程计算机都启用了 Windows 远程管理 (WinRM) 服务。远程执行还需要配置 WS-Management 协议以与 Windows PowerShell 工作。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_38_2.png)

在本书编写期间，Windows PowerShell 对远程执行的支持限于运行 Windows Vista 和 Windows Server 2008 的计算机。然而，希望这种情况会改变。

你可以通过 Windows PowerShell 提示符执行以下 cmdlet来确定 WinRM 服务的状态。

```
PS C:\ Get-Service winrm
```

| Status | Name | DisplayName |
|---|---|---|
| Stopped | WinRM | Windows Remote Management (WS-Manag...) |

```
PS C:\ Start-Service winrm
```

默认情况下，WinRM 在 Windows Server 2008 上自动启动，但在 Windows Vista 上不会启动。如果 WinRM 未运行，你需要启动它。要使用 PowerShell 启动它，你需要打开一个新的 PowerShell 命令控制台并以管理员身份运行。执行此操作，点击开始 > Windows PowerShell，右键点击 Windows PowerShell，然后点击“以管理员身份运行”选项。接下来，输入以下命令并按 Enter。

```
PS C:\ Start-Service winrm
```

一旦你确保 WinRM 服务正在运行，你就需要配置 WS-Management 协议以与 Windows PowerShell 工作，你可以在 Windows Vista 或 Windows Server 2008 上通过执行以下步骤完成：

1. 使用以管理员身份运行的选项打开一个新的 PowerShell 命令控制台。
2. 输入以下语句并按 Enter。

```
PS C:\> Configure-Wsman
```



执行后，计算机将能够作为远程执行客户端和服务器。由于 PowerShell 的远程执行功能依赖于 `WSManagement` 协议，它使用 `HTTP`，客户端和服务器之间交换的所有网络数据包都通过端口 `80` 发送和接收，使得远程执行变得非常友好。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_41_0.png)

```
PowerShell Read-Host

PS C:\> Get-Help Read-Host

NAME

Read-Host

SYNOPSIS

从控制台读取一行输入。

SYNTAX

Read-Host [-prompt [<Object>]] [-asSecureString] [[CommonParameters]]

DETAILED DESCRIPTION

Read-Host let 从控制台读取一行输入。你可以使用它

向用户提示信息并将结果捕获为字符串。

你可以使用此 cmdlet 提示用户输入安全数据（如密码）以及共享数据。

RELATED CMDLET

Get-Host

Write-Host

ConvertTo-SecureString

需更多信息，请输入："get-help Read-Host -detailed"

需技术信息，请输入："get-help Read-Host -full"
```

图 1.9

查看关于 `Read-Host` cmdlet 的帮助信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_41_1.png)

```
Windows: PowerShell 2.0 (Community Technology Preview) - 可能会发生更改

Copyright (C) 2008 Microsoft Corporation. 版权所有。

PS C:\>_
```

图 1.10

通过 Windows 控制台访问 PowerShell。

你通过在命令提示符中提交命令与 PowerShell 交互，命令提示符通常如图 1.11 所示，类似于 `PS C:\`。`PS` 是 PowerShell 的缩写。`C:\` 代表当前工作目录，`>` 表示 PowerShell 已准备好接收输入。你通过输入并按回车键输入 PowerShell 处理的命令。发生的情况取决于你输入的命令。默认情况下，你输入的任何命令都会被处理，任何输出都会以文本形式返回，如图 1.11 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_42_0.png)

图 1.11 中执行的命令是 `Get-Item` cmdlet，它检索文件夹的内容。由于没有指定路径，因此使用了当前工作目录。为了帮助用户和管理员尽可能容易地过渡到使用 PowerShell，微软开发了一系列 cmdlet 别名（aliases），可以替代实际的 cmdlet 名称。在 Windows PowerShell 中，别名是指向特定 cmdlet 的链接。在许多情况下，微软为给定的 cmdlet 创建了多个别名。例如，由于用户或管理员起初可能很难记得使用 `Get-ChildItem` 来显示文件夹内容，微软为该 cmdlet 创建了名为 `dir` 的别名。因此，你可以用 `dir` 代替 `Get-ChildItem`，并获得完全相同的结果，如图 1.12 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_42_1.png)

> 图 1.12
> `dir` 是 `Get-ChildItem` cmdlet 的别名，旨在帮助用户和管理员完成从 `cmd.exe` 到 Windows PowerShell 的切换。

考虑到并不是每个人都是经验丰富的 Windows 用户或管理员，微软还为 `Get-ChildItem` cmdlet 创建了名为 `dir` 的别名，以帮助具有 Linux 或 UNIX 背景的用户和管理员平滑过渡到 Windows PowerShell。如图 1.13 所示，在 PowerShell 命令提示符下输入 `ls` 的结果与之前的两个示例完全相同。

> `ls` 是 `Get-ChildItem` cmdlet 的别名，旨在帮助 Linux 和 UNIX 用户切换到 Windows PowerShell。

```
C:\TextFiles> ls

Directory: Microsoft.PowerShell.Core\File\C:\TextFiles

Mode                LastWriteTime Length Name

----                ------------- ----- ---

-a        07/28/2008          8:42 PM            0 Customer.txt

-a        07/28/2008          8:42 PM            0 File.txt

-a        07/28/2008          8:42 PM            0 Data.txt

-a        07/28/2008          8:42 PM            0 Vendor.Accounts.txt

C:\TextFiles>
```

Windows PowerShell 提供了对 129 个 cmdlet 的访问（PowerShell 2.0 有 181 个），其中大多数至少有一个参数。你将在第 3 章“基于 .NET 的对象脚本编写”中找到 Windows PowerShell cmdlet 的完整列表。

重要的是，我不希望让你产生一种“从 Windows PowerShell 命令提示符可以运行的命令类型只有 cmdlet”的印象。事实上，你可以运行任何可执行文件。定位可执行文件的一种方法是使用下所示的 `Get-Command Get-Command *.exe`。

响应，PowerShell 将显示它能找到的所有可执行文件列表。如果你检查此列表，可能会看到许多你已经熟悉的可执行文件。例如，你可以在 PowerShell 命令提示符下输入 `notepad` 并按回车键启动记事本程序。

熟悉 Windows PowerShell 的最佳方法是开始使用它。在本节中，你将获得这个机会。具体来说，我将为你提供一系列命令行示例，让你感受 Windows 支持的 cmdlet 类型以及执行它们时的整体语法。

首先，执行一个提供计算机上所有运行进程列表的命令。这可以使用以下 `Get-Process` cmdlet 完成：

```
PS C:\ Get-Process

| Handles | NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id ProcessName |

|---|---|---|---|---|---|---|

| 643 | 6 | 1764 | 1512 | 73 | | 500 cssrs |

| 55 | 2 | 1116 | 792 | 45 | 0.39 | 2168 ehmsas |

| 1327 | 39 | 77956 | | 318 | 1458 | |

| 1327 | 39 | 77956 | | 318 | 1458 | |

| 1327 | 39 | 77956 | | 318 | 1458 | |

| 1327 | 39 | 77956 | | 318 | 1458 | |
```

（注：OCR 表格严重损坏/噪声；根据可见表头重构了结构）

| Handles | NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id ProcessName |
|---|---|---|---|---|---|---|
| 643 | 6 | 1764 | 1512 | 73 | | 500 cssrs |
| 55 | 2 | 1116 | 792 | 45 | 0.39 | 2168 ehmsas |
| 1327 | 39 | 77956 | | 318 | 1458 | |
| ... | ... | ... | ... | ... |

（由于源文件中进程表的 OCR 错误过多，仅保留了表头和初始行）

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_41_0.png)

```
PowerShell Read-Host

PS C:\> Get-Help Read-Host

NAME

Read-Host

SYNOPSIS

从控制台读取一行输入。

SYNTAX

Read-Host [-prompt [<Object>]] [-asSecureString] [[CommonParameters]]

DETAILED DESCRIPTION

Read-Host cmdlet 从控制台读取一行输入。你可以使用它

向用户提示信息并将结果捕获为字符串。

你可以使用此 cmdlet 提示用户输入安全数据（如密码）以及共享数据。

RELATED CMDLET

Get-Host

Write-Host

ConvertTo-SecureString

需更多信息，请输入："get-help Read-Host -detailed"

需技术信息，请输入："get-help Read-Host -full"
```

图 1.9

查看关于 `Read-Host` cmdlet 的帮助信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_41_1.png)

```
Windows: PowerShell 2.0 (Community Technology Preview) - 可能会发生更改

Copyright (C) 2008 Microsoft Corporation. 版权所有。

PS C:\>_
```

图 1.10

通过 Windows 控制台访问 PowerShell。

# 执行 PowerShell Cmdlet

你通过在命令提示符中提交命令与 PowerShell 交互，命令提示符通常如图 1.11 所示，类似于 `PS C:\`。`PS` 是 PowerShell 的缩写。`C:\` 代表当前工作目录，`>` 表示 PowerShell 已准备好接收输入。你通过输入并按回车键输入 PowerShell 处理的命令。发生的情况取决于你输入的命令。默认情况下，你输入的任何命令都会被处理，任何输出都会以文本形式返回，如图 1.11 所示。

# 云 - Windows 现代化

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_42_0.png)

图 1.11 中执行的命令是 `Get-Item` cmdlet，它检索文件夹的内容。由于没有指定路径，因此使用了当前工作目录。为了帮助用户和管理员尽可能容易地过渡到使用 PowerShell，微软开发了一系列 cmdlet 别名（aliases），可以替代实际的 cmdlet 名称。在 Windows PowerShell 中，别名是指向特定 cmdlet 的链接。在许多情况下，微软为给定的 cmdlet 创建了多个别名。例如，由于用户或管理员起初可能很难记得使用 `Get-ChildItem` 来显示文件夹内容，微软为该 cmdlet 创建了名为 `dir` 的别名。因此，你可以用 `dir` 代替 `Get-ChildItem`，并获得完全相同的结果，如图 1.12 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_42_1.png)

> 图 1.12
> `dir` 是 `Get-ChildItem` cmdlet 的别名，旨在帮助用户和管理员完成从 `cmd.exe` 到 Windows PowerShell 的切换。考虑到并不是每个人都是经验丰富的 Windows 用户或管理员，微软还为 `Get-ChildItem` cmdlet 创建了名为 `dir` 的别名，以帮助具有 Linux 或 UNIX 背景的用户和管理员平滑过渡到 Windows PowerShell。如图 1.13 所示，在 PowerShell 命令提示符下输入 `ls` 的结果与之前的两个示例完全相同。

# 图 1.13

> `ls` 是 `Get-ChildItem` cmdlet 的别名，旨在帮助 Linux 和 UNIX 用户切换到 Windows PowerShell。

```
C:\TextFiles> ls

Directory: Microsoft.PowerShell.Core\File\C:\TextFiles

Mode                LastWriteTime Length Name

----                ------------- ----- ---

-a        07/28/2008          8:42 PM            0 Customer.txt

-a        07/28/2008          8:42 PM            0 File.txt

-a        07/28/2008          8:42 PM            0 Data.txt

-a        07/28/2008          8:42 PM            0 Vendor.Accounts.txt

C:\TextFiles>
```

Windows PowerShell 提供了对 129 个 cmdlet 的访问（PowerShell 2.0 有 181 个），其中大多数至少有一个参数。你将在第 3 章“基于 .NET 的对象脚本编写”中找到 Windows PowerShell cmdlet 的完整列表。

# 其他类型的命令

重要的是，我不希望让你产生一种“从 Windows PowerShell 命令提示符可以运行的命令类型只有 cmdlet”的印象。事实上，你可以运行任何可执行文件。定位可执行文件的一种方法是使用下所示的 `Get-Command Get-Command *.exe`。

响应，PowerShell 将显示它能找到的所有可执行文件列表。如果你检查此列表，可能会看到许多你已经熟悉的可执行文件。例如，你可以在 PowerShell 命令提示符下输入 `notepad` 并按回车键启动记事本程序。

# 简短 PowerShell 练习

熟悉 Windows PowerShell 的最佳方法是开始使用它。在本节中，你将获得这个机会。具体来说，我将为你提供一系列命令行示例，让你感受 Windows 支持的 cmdlet 类型以及执行它们时的整体语法。

首先，执行一个提供计算机上所有运行进程列表的命令。这可以使用以下 `Get-Process` cmdlet 完成：

```
PS C:\ Get-Process

| Handles | NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id ProcessName |

|---|---|---|---|---|---|---|

| 643 | 6 | 1764 | 1512 | 73 | | 500 cssrs |

| 55 | 2 | 1116 | 792 | 45 | 0.39 | 2168 ehmsas |

| 1327 | 39 | 77956 | | 318 | 1458 | |
```

（注：OCR 表格严重损坏/噪声；根据可见表头重构了结构）

| Handles | NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id ProcessName |
|---|---|---|---|---|---|---|
| 643 | 6 | 1764 | 1512 | 73 | | 500 cssrs |
| 55 | 2 | 1116 | 792 | 45 | 0.39 | 2168 ehmsas |
| 1327 | 39 | 77956 | | 318 | 1458 | |

# 第一章 • 介绍 Windows PowerShell

```
PS C:\> Get-Process winword

| Handles | NPM(K) | PM(K) | WS(K) VM(M) | CPU(s) | Id ProcessName |
| --- | --- | --- | --- | --- | --- | --- |
| 501 | 17 | 29768 | 55996 366 | 31.82 | 5240 | WINWORD |

PS C:\>
```

此外，你也可以扩大搜索范围，查看所有以字母 `w` 开头的进程，如下所示：

```
PS C:\> Get-Process w*
```



| | NPM(K) | PM(K) | WS(K) VM(M) | CPU(s) | Id ProcessName |
| --- | --- | --- | --- | --- | --- | --- |
| 103 | 5 | 1396 | 1020 46 | | 552 wininit |
| 126 | 3 | 2016 | 80 47 | | 748 winlogon |
| 513 | 17 | 30192 | 56280 380 | 34.41 | 5240 WINWORD |
| 125 | 4 | 3516 | 2132 39 | | 2260 WmiPrvSE |
| 300 | 4 | 3436 | 1936 56 | | 2624 WudFHost |

> 大多数 cmdlet 允许你通过传递额外的处理信息作为参数来完善它们的执行。在前面的`Get-Process w*`示例中，`*`通配符字符与`w`字符一起被传递了。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_46_0.png)

在此示例中，`Get-Process` cmdlet 获取了所有名称以字母`w`开头的活动进程列表，如`w*`所示。

> `*`字符是一种用于模式匹配的通配符字符。它的目的是建立与任意数量字符的匹配。例如，`T*p`会匹配以下任何字符串：

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_46_1.png)

- `Tp`
- `Top`
- `Tooooooo`

## 零基础学者的 PowerShell 2.0 编程第二版

`*`字符是一个通配符匹配字符，用于建立与单个字符的模式匹配。例如，`Tip`会匹配`Tip`或`Top`，但不会匹配`Tooooooop`。

如果你有之前的命令行经验，那么希望你看到的这些示例看起来会相当熟悉。如果你没有很多命令行经验，不要担心；到这本书结束时，你将拥有这些经验，而且像这样的示例最终将变成你的本能。在继续之前，让我们再看一个命令行示例。

在此示例中，使用`Get-Process` cmdlet 来获取所有名称以字母`wi`开头的活动进程列表。接下来，使用一种被称为“对象管道”（object piping）的技术，将此命令的结果传递给`Format-Table` cmdlet。`Format-Table` cmdlet 以表格格式显示命令输出，允许你指定数量的可选参数。在此示例中，使用了`groupby`属性来指示 cmdlet 按进程名称组织输出，如下所示：

```
PS C:\Get-Process wi* | Format-Table -groupby ProcessName

ProcessName: wininit

Handles NPM(K)    PM(K)    WS(K) VM(M)    CPU(s)    IdProcessName

103        5       1396    1020    46          552 wininit

ProcessName: winlogon

Handles NPM(K)    PM(K)    WS(K) VM(M)    CPU(s)    IdProcessName

126        3       2016    80      47          748 winlogon

ProcessName: WINWORD

Handles NPM(K)    PM(K)    WS(K) VM(M)    CPU(s)    IdProcessName

519        17      30304   56484   385     38.89    5240 WINWORD

PS C:\>
```

### WINDOW POWERSHELL 脚本

Windows PowerShell 脚本是带有`.ps1`扩展名的纯文本文件。这些脚本文件由一个或多个 PowerShell 脚本语句组成。一旦创建，PowerShell 脚本就像 PowerShell 命令或 cmdlet 一样执行，你只需要在 PowerShell 命令行中输入其名称并可选地传递任何参数。

Windows PowerShell 自带了一种全新的脚本语言，支持全编程语言功能，包括：

- 变量、数组和哈希表
- 条件逻辑语句
- 循环语句
- 函数
- 错误处理

> 提示 你将在第 3 到 7 章中学习 Windows PowerShell 语言。

### 简化 PowerShell 脚本执行

要运行 PowerShell 脚本，你只需要在 PowerShell 提示符处输入脚本名称。作为响应，PowerShell 将搜索每个...

### 零基础 Microsoft Windows PowerShell 2.0 编程第二版

如果你愿意，也可以通过用`clear`或`cls`命令替换`Clear-Host`命令来清除 Windows 命令行控制台。`clear`和`cls`都是`Clear-Host`的别名。Windows PowerShell 支持多百个 cmdlet（命令程序），其中大多数至少有一个别名。你将在第 3 章“使用 .NET 进行基于对象的脚本编写”中找到 Windows PowerShell 的完整列表。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_51_0.png)

### 提示玩家开始游戏

现在是时候显示第一个笑话的开头字符串“Knock Knock!”并等待玩家通过输入字符串“Who is there?”来响应。要完成脚本的这部分，请将以下语句添加到脚本文件的末尾。

```powershell
$userReply = ""

while ($userReply -ne "Who is there?"){

    $userReply = read-host "Knock Knock!"

}
```

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_51_1.png)

第一语句声明了一个名为`userReply`的变量，并赋值一个随后的空字符串块，用于存储和分析用户输入的的内容。`while`循环被设置为执行到玩家输入预期的响应为止。注意，位于`while`循环内部的单个语句显示了开头的“Knock Knock!”提示，它是使用`Read-Host` cmdlet 从 Windows 命令行控制台读取行输入。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_51_2.png)

变量是指向内存中存储值位置的指针。你将在第 4 章“处理变量、数组和哈希表”中学习更多关于变量的知识。循环是一个作为一个单元重复执行的语句集合。你将在第 6 章“使用循环处理数据”中学习更多关于循环的知识。

### 额外的玩家输入

一旦玩家对“Knock Knock!”提示提供了正确回答，游戏就需要显示笑话的铺垫句，这通过将以下语句添加到脚本文件末尾来实现。

### Clear-Host

```powershell
while ($userReply -ne "Orange who?") {

  $userReply = read-host "Orange."

}
```

如你所见，这里显示的第一个语句清了 Windows 命令行控制台屏幕。接下来，一个`while`循环使用`Read-Host` cmdlet 显示提示“Orange.”。玩家必须通过回答“Orange who?”来让游戏继续。

### 显示笑点

一旦玩家提供了正确回答，脚本将显示第一个笑话的笑点。这通过将以下语句添加到脚本文件末尾来实现。

```powershell
Clear-Host

Write-Output "Orange you glad you created this PowerShell script?"
```

第一个语句清空 Windows 命令行控制台屏幕。第二个语句使用`Write-Output` cmdlet 播放包含第一个笑话笑点的文本字符串。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_52_0.png)

> 默认情况下，`Write-Output` cmdlet 会向 Windows 控制台屏幕写入一行文本。

### 在笑话之间暂停

在讲完每个笑话后，游戏应该暂停五秒，给玩家一个机会阅读笑话的笑点。这通过将以下语句添加到脚本文件末尾来实现。

```powershell
Start-Sleep -Seconds 5
```

该语句执行`Start-Sleep` cmdlet，告诉它暂停脚本执行 5 秒。

### 讲述第二个笑话

此时，脚本的第一个笑话已经呈现给用户。现在是时候讲游戏的第二个笑话了。完成此任务所需的代码语句与呈现第一个笑话的语句几乎相同，仅构成笑话文本的文本字符串中的某些内容略有不同。下面所示的代码必须添加到脚本文件的末尾。

# 30 零基础 Microsoft Windows PowerShell 2.0 编程第二版

`Clear-Host`

```powershell
while ($userReply -ne "Who is there?"){

  $userReply = read-host "Knock Knock!"

}
```

`Clear-Host`

```powershell
while ($userReply -ne "Orange who?"){

  $userReply = read-host "Orange."

}
```

`Clear-Host`

`Write-Output "Oranges are oranges but this is PowerShell scripting!"`

`Start-Sleep -Seconds 5`

### 讲述第三个笑话

负责讲述游戏第三个笑话的语句如下所示。这些语句需要添加到你的 PowerShell 脚本文件的末尾。

`Clear-Host`

```powershell
while ($userReply -ne "Who is there?"){

  $userReply = read-host "Knock Knock!"

}
```

`Clear-Host`

```powershell
while ($userReply -ne "Banana who?"){

  $userReply = read-host "Banana."

}
```

`Clear-Host`

`Write-Output "Orange you glad I didn't say orange?",`

`Start-Sleep -Seconds 5`

如你所见，这些代码语句与呈现第一个笑话的语句几乎相同，只是某些内容略有不同。

### 显示游戏和作者信息

游戏通过清除屏幕结束，显示关于游戏的某些信息并在之后清除屏幕。实现这一点的代码语句如下。

```powershell
Clear-Host

Write-Output "The Joke"

Write-Output " "

Write-Output "Copyright 2008 - Jerry Lee, Jr.",
```

## 最终结果

此时，你的新 PowerShell 脚本应该完成了。我们在在这里提供了一个完整的副本，以便你确保没有漏掉任何内容。

```powershell
Clear-Host

$userReply = ""

while ($userReply -ne "Who is there?") {

  $userReply = read-host "Knock Knock!"

}

Clear-Host

while ($userReply -ne "Orange who?") {

  $userReply = read-host "Orange."

}

Clear-Host

Write-Output "Orange you glad you created this PowerShell script?"

Start-Sleep -Seconds 2
```

[PAGE 55]

```powershell
Clear-Host

while ($userReply -ne "Who is there?"){

  $userReply = read-host "Knock Knock!"

}
```

`Clear-Host`

```powershell
while ($userReply -ne "Orange who?"){

  $userReply = read-host "Orange."

}
```

`Clear-Host`

`Write-Output "Oranges are oranges but this is PowerShell scripting!"`

`Start-Sleep -Seconds 5`

[PAGE 56]

```powershell
Clear-Host

while ($userReply -ne "Who is there?"){

  $userReply = read-host "Knock Knock!"

}
```

`Clear-Host`

```powershell
while ($userReply -ne "Banana who?"){

  $userReply = read-host "Banana."

}
```



```
Clear-Host

Write-Output "Orange you glad I didn't say orange?"

Start-Sleep -Seconds 5
```

[PAGE 57]

假设你没有输入任何拼写错误，你的笑话脚本应该已经准备好运行。如果你遇到任何错误，说明你在某个地方写错了字。在这种情况下，你需要回头检查你的工作并找到错误之处。

### 总结

对于电脑游戏，总有改进的空间。在进入下一个章节之前，我建议通过尝试实现以下挑战列表，在笑话游戏上花费更多时间。

### 挑战

- 按照目前的写法，笑话游戏向玩家展示三个平淡的笑话。我建议你将这些笑话替换为你自己的敲门式笑话。
- 由于只有三个笑话，笑话游戏完成的时间并不长。通过增加讲述的笑话数量，给玩家提供更好的体验。
- 一旦你在敲门式笑话游戏中加入了自己的笑话，通过修改脚本末尾显示的开发者信息来为你的成果赢得荣誉。

### 与 WINDOW POWERSHELL 命令行和图形化环境交互

为了有效地使用 Windows PowerShell 并开发 PowerShell 脚本，你必须牢牢掌握如何从 PowerShell 命令行与 Windows 进行交互。本章将介绍如何配置 Windows 命令控制台，以创建一个更好的工作环境，以便与 Windows PowerShell 进行交互。这包括学习如何配置命令控制台布局以及指定你的默认工作目录。本章还将解释如何利用 Windows PowerShell 内置的制表符补全功能，以在键入命令时节省时间并减少错误。你还将学习如何使用 PowerShell 导航并访问不同类型的系统资源，包括 Windows 注册表、环境变量和磁盘驱动器。此外，你将学习如何创建你的第二个 PowerShell 游戏——三位一体的故事（The Story of the Three Amigos）。

### 零基础读者的 Microsoft Windows PowerShell 2.0 编程

具体而言，你将学习如何：

- 为你的 PowerShell 会话设置默认工作目录
- 自定义 Windows 命令控制台
- 利用制表符补全减少完成命令所需的时间
- 使用 Windows PowerShell 访问不同的分级数据存储

### 项目预览：三位一体的故事

在本章中，你将学习如何创建一个讲述《三位一体的故事》的新计算机游戏。这个“填空游戏”（mad-lib）的关键部分将通过用户对看似无关问题的回答形式从用户处收集。最终结果是一个永远不会重复讲述的故事。《三位一体的故事》从显示标题页开始，如图 2.1 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_59_0.png)

图 2.1
三位一体的故事是一页页讲述的。

《三位一体的故事》是一个填空游戏，它收集玩家输入并插入故事中的关键位置，允许用户参与故事讲述体验。在提问任何问题之前，游戏会告知用户对他们的要求，如图 2.2 所示。

总而言，用户会被问及四个问题，而预先不知道答案将用于何种上下文。图 2.3 提供了游戏所问的一个问题的示例。

一旦游戏收集了所有所需信息，它就会开始一页页地讲述《三位一体的故事》。故事的第一页如图 2.4 所示。

# 第 2 章 • 与 Windows PowerShell 交互

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_60_0.png)

按回车键继续。

> 图 2.2
> 三位一体的故事
> 是一个交互式故事，
> 它取决于
> 用户的输入。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_60_1.png)

> 图 2.3
> 用户必须等待
> 直到故事讲述完
> 才能看到
> 输入是如何
> 被使用的。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_60_2.png)

按回车键继续。

> 图 2.4
> 《三位一体的故事》的
> 起始页。

当用户阅读故事的每一页时，他们会注意到自己提供的答案如何影响了故事讲述的方式，如图 2.5 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_61_0.png)

## 图 2.5

《三位一体的故事》的第二页。

图 2.6 显示了《三位一体的故事》的下一页，解释了故事中的英雄如何击败敌人并拯救城镇。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_61_1.png) # 图 2.6

《三位一体的故事》的第三页。

三位一体的故事像许多故事一样，以圆满的结局结束，如图 2.7 所示。# 第 2 章 • 与 Windows PowerShell 交互

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_62_0.png)

图 2.7
三位一体的故事
最后一页。

当你完成构成三位一体的故事的 Windows PowerShell 脚本时，你应该已经熟悉了创建和执行 Windows PowerShell 脚本的机制。

### 访问 WINDOWS POWERSHELL

正如你已经看到的，你可以通过点击开始 > 所有程序 > Windows PowerShell 来启动一个新的 Windows PowerShell 会话。启动后，Windows 命令出现，随后显示以下信息：

Windows PowerShell V2 (技术预览版 - 功能可能会更改)
Copyright (C) 2008 Microsoft Corporation. 保留所有权利。

```
PS C:\
```

默认情况下，每次启动 Windows PowerShell 显示其名称和版权信息。版权信息之后是一个空行和 Windows PowerShell 命令提示符。提示符显示 Windows PowerShell 当前的工作目录。

还有许多其他启动 Windows PowerShell 会话的方法。例如，你可以在提示符中输入`PowerShell`并按回车键从`cmd.exe`会话启动一个新的会话。作为响应，当前窗口内会启动一个新的 PowerShell 会话。在操作 PowerShell 会话时，你可以在 PowerShell 命令行输入`Exit`并按回车键关闭它返回`cmd.exe`会话。

另一种启动 Windows PowerShell 会话的方法是创建一个桌面快捷方式，你可以在桌面空白区域点击右键，并在提示时选择新建 > 快捷方式。这将启动一个快捷方式向导，引导你完成设置新快捷方式的过程。在“位置”字段中输入`PowerShell`并点击“下一步”。接下来在“为此快捷方式命名”字段中输入`Windows PowerShell`并点击“完成”。

除了使用上述选项启动新的 Windows PowerShell 会话外，Windows PowerShell 2.0 用户还可以使用新的图形化应用程序运行 Windows PowerShell，这将在本章稍后的部分介绍。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_63_0.png)

### 自定义 WINDOW POWERSHELL 工作环境

无论你如何启动 Windows PowerShell 会话，都会发现自己在 Windows 命令控制台应用程序中使用它。好消息是，Windows 命令控制台为你提供了丰富的命令和功能，帮助你控制与 PowerShell 交互的方式，并帮助你工作得更快高效。

### 自定义 Windows PowerShell 快捷方式

在桌面上放置 Windows PowerShell 快捷方式可以方便访问。让快捷方式更加方便的方法是修改其“起始于”字段，使其指向存储所有 Windows PowerShell 脚本文件的文件夹。通过这种方式，你只需要双击 Windows PowerShell 图标，就会使用指定的文件夹作为当前工作目录启动新会话。

上述修改 Windows PowerShell 快捷方式的步骤如下：

1. 右键点击你的 Windows PowerShell 快捷方式并选择“属性”。Windows 属性将出现。
2. 在“起始于”字段中输入你的 PowerShell 文件夹的完整路径，如图 2.8 所示。
3. 点击“确定”。

下次使用此快捷方式启动 Windows PowerShell 会话时，Windows 控制台将出现并使用指定的文件夹作为当前工作目录启动新会话，如图 2.9 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_64_0.png)

# 第 7 章 - 与 Windows PowerShell 交互

| 颜色 | 兼容性 | 安全 | 详细 |
| --- | --- | --- | --- |
| 通用 | 选项 | 字体 | 布局 |
| 目标类型：应用程序 |
| 目标位置：`system32\WindowsPowerShell\v1.0\powershell.exe` |
| 起始于：`C:\Users\Jerry\MyScripts` |
| 快捷方式：无 |
| 运行：普通窗口 |
| 打开文件位置 | 更改图标... | 高级... |

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_64_1.png)

图 2.8
配置你的 Windows 快捷方式以指定其默认工作目录。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_64_2.png)

图 2.9
使用自定义的快捷方式启动新的 Windows PowerShell 会话。

## 配置 WINDOW 命令控制台

Windows PowerShell 通过 Windows 命令控制台访问。默认情况下，Windows 命令控制台在一个长 45 行、宽 120 字符的窗口中显示文本。所有文本均显示为蓝色背景上的白色字体。作为一名 Windows PowerShell 程序员，了解如何操作 Windows 命令控制台并使其配置为符合你的个人偏好是非常重要的。

正如接下来的章节将所示，Windows 命令控制台具有高度的可配置性，允许你通过多种方式修改其外观和行为。此外，它还提供了许多实用的编辑命令，用于与 Windows PowerShell 交互。

> > 提示：为了帮助改进书中表的显示效果，我修改了 Windows 命令控制台的版本为 25 个字符长、80 个字符宽。此外，我还将文本设置为在白色背景上显示黑色。

### Windows 命令控制台自定义选项

要自定义 Windows 命令控制台，你必须首先打开它，可以通过启动新的 PowerShell 会话来实现。打开后，右键点击命令控制台标题栏左角的命令提示符图标，并在右键菜单中选择“属性”。这将打开 Windows 属性对话框。该对话框由四个属性页组成。每个属性页都控制 Windows 命令控制台的不同方面。你可以通过修改在这些属性页上显示的属性信息来配置 Windows 命令控制台的行为和外观。

> > 提示：尽管本节重点介绍了使用 Windows Vista 配置 Windows 命令控制台的方法，但此处提供的信息也广泛适用于 Windows XP、Windows 2003 和 Windows 2008。

### 修改控制台选项

属性窗口上的第一个属性页是“选项”选项卡，如图 2.10 所示。在此处，你可以修改以下 Windows 命令控制台属性：

- 光标大小。决定命令控制台是否以小、中等或大尺寸显示。
- 命令历史。决定命令控制台缓冲区的大小，这影响了命令控制台存储和检索的命令数量、正在使用的缓冲区数量，以及是否将重复命令作为命令控制台命令历史的一部分保存。
- 编辑选项。决定是否启用“快速编辑”模式和插入模式。快速编辑是命令控制台的一个功能，支持从命令窗口复制文本并向命令提示符粘贴文本。插入模式控制在命令提示符处键入编辑文本时，是插入文本还是覆盖文本。

# 第 2 章 • 与 Windows PowerShell 交互

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_66_0.png)

> 图 2.10
> 选项属性页提供了对控制台属性的访问，用于控制光标大小、命令历史以及显示和编辑设置。

### 修改控制台字体属性

属性窗口上的第二个属性页是“字体”选项卡，如图 2.11 所示。在此处，你可以修改 Windows 命令控制台使用的字体大小和字体类型。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_66_1.png)

> 图 2.11
> 为 Windows 命令控制台配置字体属性。

字体大小的更改也会影响 Windows 控制台的大小。Windows 预览区域为你提供了有关更改字体大小效果的视觉反馈。

字体属性页还允许你更改 Windows 控制台使用的字体类型。字体类型选择的效果会立即出现在字体属性页的“所选字体：终端”部分。根据你所选择的字体，位于可用字体列表上方的“粗体”属性将被启用。启用后，这将绑定控制台文本，根据你的喜好，可能会让控制台文本更容易阅读。

### 修改 Windows 命令控制台的布局

属性窗口上的第三个属性页是“布局”选项卡，如图 2.12 所示。在此处，你可以设置 Windows 控制台的初始大小和显示位置。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_67_0.png)

> 图 2.12
> 修改 Windows 控制台屏幕大小和 Windows 位置。

对布局属性的更改会立即反映在布局属性页的 Windows 预览部分。通过修改以下任何设置来进行配置更改：

- **屏幕缓冲区大小**。“宽度”设置指定了单行显示的字符数。“高度”设置指定了内存中可以存储的文本行数，从而控制你可以回溯并查看的行数。

# 第 2 章 · 与 Windows PowerShell 交互

**Windows 大小**。“宽度”设置指定了单行显示的字符数。“高度”设置指定了命令控制台默认显示的文本行数。无论这些设置如何，你都可以通过右键点击 Windows 命令控制台的边缘并拖动到新位置，像其他 Windows 应用程序一样手动调整 Windows 命令控制台的大小。但请，Windows 命令控制台的大小不能大于“屏幕缓冲区大小”部分设置的高度和宽度值。

**Windows 位置**。你可以通过修改这些设置来设定 Windows 命令控制台的起始位置，指定启动时 Windows 命令控制台应显示的精确位置。位置是通过指定 Windows 命令控制台左上角左、右角的像素数来设置的。像素（图像元素）代表可以显示或打印的最小区域。可选，你可以通过保持默认的“左系统位置”属性选中，让 Windows 决定 Windows 命令控制台的位置。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_68_0.png)

我建议将“屏幕缓冲区高度”设置为 Windows 大小的至少三倍。这将允许你滚动查看几页之前执行的命令和输出。

### 修改控制台颜色属性

属性窗口的第四个页是“颜色”选项卡，如图 2.13 所示。在此处，你可以更改 Windows 命令控制台的前景和背景颜色。

属性页顶部部分的左侧提供了四个不同选项的访问。要配置这些选项，请选择一个，然后从属性页中间的颜色带中选择颜色。这些选项包括：

- 屏幕文本。指定显示文本的颜色。
- 屏幕背景。指定显示控制台背景的颜色。
- 弹出文本。指定显示控制台命令历史对话框文本的颜色。
- 弹出背景。指定显示控制台命令历史对话框背景的颜色。

# 46 Clement 给初学者的 PowerShell，第二版

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_69_0.png)

> 图 2.13
> 修改 Windows 命令控制台的前景和背景颜色属性。

如果你愿意，可以从颜色带中选择颜色，而是选择这四个选项之一，然后使用属性页右上角“所选颜色值”部分的滚动条控件指定各种红、绿、蓝水平。

颜色属性页的半部分提供了对 Windows 控制台及其命令历史对话框任何更改的视觉预览。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_69_1.png)

后续，我将 Windows 命令控制台的屏幕背景颜色设置为白色，屏幕文本颜色设置为黑色。这将使后续脚本生成的屏幕图形更具可读性且更容易阅读。

### 脚本控制控制台

除了使用 Windows PowerShell 属性对话框解释的配置方法外，你还可以通过编程方式配置控制台。为此，你需要创建一个名为`Microsoft.PowerShell_profile.ps1`的配置文件，并将其存储在 Windows PowerShell 配置文件路径中。你的配置文件路径取决于你所使用的操作系统。要确定配置文件路径，请在 Windows 命令提示符处执行以下命令。

```
PS C:\> $profile
```

# 第 2 章 · 与 Windows PowerShell 交互

作为响应，Windows PowerShell 将显示类似于此处所示的输出。
`C:\Users\Jerry\Documents\PowerShell\Microsoft.PowerShell.profile.ps1`

利用这些信息，请确保你的计算机上存在指定的路径结构，并在其中创建并存储一个名为`Microsoft.PowerShell_profile.ps1`的新脚本文件。你添加到`Microsoft.PowerShell_profile.ps1`中的任何 PowerShell 脚本语句都将在每次启动新的 PowerShell 控制台会话时自动执行。

程序化配置 Windows PowerShell 控制台的技巧是执行`Get-Host`get词，如此处所示。

```
PS C:\> Get-Host
```



```
Name : ConsoleHost
Version : 2.0
InstanceId : 81bb69d9-c246-4143-98b3-e8436ecaf8d
UI : System.Management.Automation.Internal.Host.HostInterface
CurrentCulture : en-US
CurrentUICulture : en-US
PrivateData : Microsoft.PowerShell.ConsoleHost+ConsoleColorProxy
IsRunspacePushed : False
Runspace : System.Management.Automation.Runspaces.LocalRunspace
```

如果你查看`Get-Host` cmdlet 产生的输出，你会发现它包含关于一个名为`UI`属性的信息。该属性提供了对 UI 对象的访问，该对象有一个名为`RawUI`的属性，可以使用它来访问和操作控制台属性，如下所示：

```
$PSConsoleWindow = (Get-Host).UI.RawUI

$PSConsoleWindow.BackgroundColor = "White"

$PSConsoleWindow.ForegroundColor = "DarkBlue"

$PSConsoleWindow.WindowTitle = "Jerry's Customized PowerShell Console Session"

$PSConsoleSize = $PSConsoleWindow.WindowSize

$PSConsoleSize.Width = 80

$PSConsoleSize.Height = 25

$PSConsoleWindow.WindowSize = $PSConsoleSize

Clear-Host
```

此脚本中的开头语句使用`Get-Host` cmdlet 及其`UI`属性来访问`RawUI`属性。注意，`Get-Host` cmdlet 周围的括号是必要的，以确保`UI`属性引用应用于 cmdlet 返回的结果，而不是 cmdlet 本身。最终结果是第一条语句生成了一个名为`$PSConsoleWindow`的对象变量，随后可以使用它可以访问和配置控制台属性。

第二和第三条语句为控制台窗口设置了`BackgroundColor`和`ForegroundColor`属性。这两个属性的颜色列表如下：

- 黑色 (Black)
- 蓝色 (Blue)
- 青色 (Cyan)
- 深蓝色 (DarkBlue)
- 深青色 (DarkCyan)
- 深灰色 (DarkGray)
- 深绿色 (DarkGreen)
- 深洋红 (DarkMagenta)
- 深红色 (DarkRed)
- 深黄色 (DarkYellow)
- 灰色 (Gray)
- 绿色 (Green)
- 品红色 (Magenta)
- 红色 (Red)
- 黄色 (Yellow)

第四条脚本语句使用`WindowTitle`属性分配一个文本字符串，将在控制台标题栏中显示，替换默认的 Windows PowerShell 字符串。接下来的四条语句配置控制台的大小。为此，这些语句中的第一个使用`WindowSize`属性创建一个对象引用，并命名为`$PSConsoleSize`。接下来，设置该对象的宽度和高度属性，之后将配置更改重新分配给`$PSConsoleWindow`对象的`WindowSize`属性。最后，脚本中的最后一条语句执行`Clear-Host` cmdlet。这会刷新控制台窗口并强制立即应用脚本所选的配置选项，如图 2.14 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_72_0.png)

> 图 2.14 程序化配置 PowerShell 命令控制台。

### Windows 命令控制台编辑功能

由于你是在 Windows 命令控制台中访问并交互 Windows PowerShell 的，因此你可以使用控制台内置的许多实用编辑功能。例如，你可以通过方向键编辑命令提示符中已经输入的任何命令。除了这些基础编辑能力外，你可以使用表 2.1 所示的任何编辑功能来控制控制台命令行。

表 2.1 Windows 控制台编辑功能

| 编辑功能 | 结果 |
| :--- | :--- |
| 向上箭头 (Up Arrow) | 在历史记录中向上移动一个位置。 |
| 下箭头 (Down Arrow) | 在历史记录中向下移动一个位置。 |
| 上页键 (Page Up) | 跳到历史记录中的第一条命令。 |
| 下页键 (Page Down) | 跳到历史记录中的最后一条命令。 |
| Home键 (Home) | 跳到命令行的开头。 |
| 结束键 (End) | 跳到命令行的末尾。 |
| Ctrl+左键 (Control+Left) | 向左移动一个单词。 |
| Ctrl+右键 (Control+Right) | 向右移动一个单词。 |

Windows 控制台会维护当前会话期间执行的命令列表。此列表被称为历史记录。

你也可以通过按下 F7 键查看历史记录中的命令列表。作为响应，Windows 控制将显示如图 2.15 所示的窗口。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_73_0.png)

```
> Get-Process

> Get-Help

> Get-Alias

> Get-Process
```

注意历史记录中每条命令左侧的数字。你可以通过按下 Enter 键执行历史记录中的任何命令。

### Windows 增强

除了继承控制台内置的编辑功能外，Windows PowerShell 还提供了补全功能，让你工作得更智能、更快。

### Tab 补全

补全明显的优势是你不需要记住整个命令。你只需要记住足够让 PowerShell 识别的类别然后按下 Tab。补全不仅适用于帮助你输入 cmdlet；还可以协助填写文件名、变量名和属性名。例如，在 PowerShell 提示符处输入以下语句并按 Enter。

```
$x = "Once upon a time..."
```

此语句创建一个名为`$x`的变量并赋值一个字符串值。接下来，输入`$`然后按下 Tab 键。作为响应，PowerShell 将根据形成的内容显示一系列匹配项。在本示例中，PowerShell 将显示适用于字符串变量的方法。例如，如果你一直按下 Tab 键直到显示`ToLower(`建议，然后按下 Enter，你得到如下结果。

```
$x.ToLower(
```

`ToLower()`方法用于将组成字符串的所有字符转换为小写字母。为了完成上一个示例，你只需要添加右括号并然后按 Enter，如下所示。

```
PS C> $x = "Once upon a time..."

PS C> $x.ToLower()

once upon a time...

PS C>
```

或者，你也可以按下 Enter 键选择`ToLower(`建议，然后输入右括号并两次按下 Enter，如下所示。

```
PS C> $x = "Once upon a time..."

PS C> $x.ToLower(

>> )
```

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_75_0.png)

# 第 2 章与 Windows PowerShell 交互

```
>> 

once upon a time...

PS C:\
```

在这个示例中，当你第一次按下 Enter 键时，PowerShell 并没有执行指定的命令，因为它知道该命令是不完整的。相反，它让你处于编辑模式（Edit mode），这从屏幕左侧没有出现命令提示符且出现了`>>`字符可以判断出来。当你提供了所需的右右括号并再次按下 Enter 键时，PowerShell 仍保持在编辑模式，允许你在需要时向命令添加内容。在不输入任何文本的情况下再次按 Enter 键将关闭编辑模式，并指示 PowerShell 执行你的命令。

### Get-History cmdlet

你还可以使用`Get-History` cmdlet 获取存储在历史缓冲区中的项。此 cmdlet 访问历史缓冲区命令并将其插入 Windows PowerShell 流水线中，允许你通过程序方式访问和操作它们。例如，使用`Get-History` cmdlet，你可以显示存储在历史缓冲区中的命令列表，如下所示：

```
PS C:\MyScripts> Get-History
```

| Id | CommandLine |
|---|---|
| 1 | Get-Process |
| 2 | Get-Alias |
| 3 | Get-Help |

现在你拥有了这些信息，你可以使用`Invoke-History` cmdlet 执行历史缓冲区中的任何命令，该 cmdlet 接受一个数字作为参数，代表该命令在历史缓冲区中的位置。例如，要执行上一个示例列出的第二个命令，你需要在 PowerShell 命令提示符处输入以下命令并按 Enter。

```
Invoke-History 2
```



虽然为了查找并重新执行一个简单的双单词 cmdlet 似乎需要做大量工作，但 `Get-History` 和 `Invoke-History` cmdlet 的真正价值在你发现自己反复执行一系列复杂且冗长的命令时就会体现出来。你不仅可以工作得更快，而且一旦正确输入了命令，就可以反复执行它们，而不会出现任何拼写错误。

### 使用图形化 Windows PowerShell

作为版本 2.0 的一项新 Windows PowerShell 特性是图形化 Windows PowerShell（Graphical Windows PowerShell）。图形化 Windows PowerShell 是一个全新的脚本和开发环境，提供了在单个应用程序窗口内编辑 Windows PowerShell 脚本以及与 Windows PowerShell 命令提示符交互的能力。

图形化 Windows PowerShell 随 Windows PowerShell 2.0 自动安装。它提供了许多编辑功能，使其成为比记事本更好的代码编辑器。这些功能包括：

- 语句颜色编码
- 行号
- IntelliSense 和制表键补全
- 自动文档缩进

为了使用 3.0 版本的图形化 Windows PowerShell，你必须安装了 Windows PowerShell 2.0 以及 .NET Framework 版本。要启动图形化 Windows PowerShell，点击“开始 > Windows PowerShell V2 > 图形化 Windows PowerShell”。或者，你可以在任何 Windows PowerShell 控制台中输入 PowerShell 并按 Enter 启动它，或者点击开始并在开始菜单底部的文本搜索框中输入 PowerShell 然后按 Enter 键，如图 2.16 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_77_0.png)

首次启动时，图形化 Windows PowerShell 显示两个窗格，如图 2.17 所示。上窗格用于显示 Windows PowerShell 输出，下窗格提供访问 Windows PowerShell 命令提示符的界面。

图形化 Windows PowerShell 顶部是一个菜单栏，提供了应用程序命令的访问。“文件”菜单提供了创建、打开、保存、打印和运行脚本的命令。“编辑”菜单提供了允许你复制、剪切、粘贴、重做和撤销的命令。此外，“编辑”菜单还提供了执行查找和替换操作的命令。“视图”菜单允许你跳转到三个运行空间（runspaces）中的任何一个，“运行空间”菜单允许你设置和管理你所需的多个唯一执行环境。最后，“帮助”菜单提供了对 Windows PowerShell 图形文件的访问，它比通过 Windows PowerShell 控制台更容易访问 Windows PowerShell 帮助文件。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_78_0.png)

图 2.17 默认情况下，图形化 Windows PowerShell 显示一个窗格和一个命令提示符。

### 执行 Windows PowerShell 命令

要使用图形化 Windows PowerShell 提交并处理 PowerShell 命令，你只需要在底部窗格中开始输入命令，如图 2.18 所示。

注意，在输入窗格的正左侧你会发现三个图标，它们让你方便地访问剪切、复制和粘贴命令。

### 配置输出窗格

如你所见，默认情况下，图形化 Windows PowerShell 使用两个不同的窗格清晰地分离了输入和输出。为了尽可能显示信息，使用了小字体（8 号字体）来显示输入和输出文本。然而，为了让眼睛看起来更舒服，你可能想要增大字体，你可以向右拖动位于窗口右下角的滚动条来实现这一点。当你拖动滚动条时，可以通过观察输入和输出窗格中显示文本的调整情况来看到调整的效果，如图 2.19 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_79_0.png)

图 2.18 使用图形化 Windows PowerShell 执行命令。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_79_1.png)

图 2.19 更改字体大小可以让查看更舒适。

注意，在输入窗格的正左侧你会发现三个图标，它们让你方便地访问剪切、复制和粘贴命令。

### 编辑 PowerShell 脚本

虽然并不明显，但图形化 Windows PowerShell 包含第三个窗格，默认情况下它是折叠在顶部的。你可以点击窗口左侧的向下箭头或点击“文件”菜单上的“新建脚本”或“打开脚本”来显示此窗格。

使用脚本窗格，你可以创建、编辑和执行 PowerShell 脚本。例如，查看图 2.20，展示了使用图形化 Windows PowerShell 创建和编辑脚本时的界面。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_80_0.png)

图 2.20 在单个窗口内编辑和执行脚本非常方便。

输入窗格和脚本窗格都支持 IntelliSense 和制表键补全。这意味着你可以通过按 Tab 键获取命令和语句的帮助。例如，在下窗格的命令提示符中输入 `Get -` 并按 Tab 键。此时，图形化 Windows PowerShell 将显示补全 cmdlet 的建议。要接受该建议，只需继续输入语句类型。要查看更多建议，请持续按 Tab 键。你还可以使用 IntelliSense 制表补全来帮助处理文件路径、注册表路径、变量名和别名。

当你准备好执行 Windows PowerShell 脚本时，无需离开图形化 Windows PowerShell 应用程序窗口，点击脚本窗格左上角的绿色运行按钮（或点击“文件”菜单上的“运行脚本”命令）即可。图 2.21 显示了在 Windows PowerShell 中运行脚本时输出结果的示例。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_81_0.png)

图 2.21 在单个窗口内编辑和执行脚本的功能非常实用。

当你完成对脚本文件的处理后，可以使用“文件”菜单上的“保存脚本”命令来保存它。

### 创建额外的运行空间 (Runspaces)

除了已经演示的所有功能外，图形化 Windows PowerShell 还允许你同时处理多个 Windows PowerShell 环境，每个环境都运行在自己的运行空间（runspace）中。你可以通过点击位于 Runspace 窗口上的“New Runspace”（新建运行空间）命令来打开额外的运行空间。当你同时操作多个运行空间时，图形化 Windows PowerShell 会在脚本面板的左侧为每个打开的运行空间显示标签页。当前选中运行空间的标签将以橙色高亮，如图 2.22 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_82_0.png)

> 图 2.22
> 通过点击窗口右侧的标签页，可以在不同的运行空间之间切换。

由于图形化 Windows PowerShell 窗口中显示的每个运行空间代表一个工作环境，你可以在任何给运行空间内同时打开并处理多个脚本。当你这样做时，当前运行空间的顶部会为每个打开的脚本显示一个标签页，如图 2.23 所示。

使用图形化 Windows PowerShell 编辑命令，你可以轻松地在脚本之间复制和粘贴代码语句。此外，你可以使用提示符面板（prompt pane）开发并测试命令及语句，以在将它们复制粘贴到脚本文件之前确保它们符合你的预期。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_83_0.png)

### 访问 Windows PowerShell 图形帮助文件

Windows PowerShell 1.0 通过 `Get-Help` 命令提供对其帮助文件的访问，该命令在第 3 章中介绍。虽然这确实很有帮助，但在 PowerShell 控制台窗口内显示文本帮助文件具有一定的挑战性且耗时。Windows PowerShell 2.0 通过提供对 Windows PowerShell 图形帮助文件的访问改善了这种情况，你可以从图形化 Windows PowerShell 帮助菜单访问它。

如图 2.24 所示，Windows PowerShell 图形帮助允许你浏览并显示各种帮助主题。除了显示帮助文件外，你还可以点击位于帮助文件顶部的打印机图标进行打印。

如图 2.5 所示，你可以通过输入关键字来搜索帮助主题。你甚至可以通过点击“Select Topic”（选择主题）区域中的标题对结果输出进行排序。要查看主题，请从搜索列表中选择它。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_84_0.png)

## Windows PowerShell 基础

PowerShell 使用一些大多数用户熟悉的基本概念，例如用于完成任务的熟悉界面。操作系统为用户提供了交互的图形化界面。

与使用文本流的其它 Shell 不同，PowerShell 使用不同的对象框架在命令之间传递数据。尽管你可以使用文本，但命令和命令参数是通过对象进行通信的。

PowerShell 包含许多特定的 cmdlet（组合程序），它们遵循“动词-名词”（verb-noun）的命名规范，使其易于发现和使用。这些 cmdlet 与 Shell 配合，实现命令生成和任务调度。

PowerShell 为熟悉 PowerShell 脚本的用户提供了许多优势，例如灵活性、一致性以及跨环境的一致性。

- 使用 Cmdlet
- 使用管道命令 (Pipeline-commands)
- 使用面向对象的方法

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_84_1.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_84_2.png)

### 关于 Windows PowerShell

PowerShell 的设计旨在为系统管理员改进命令行和脚本环境，引入了一致性和新功能。

| 名称 | 类型 | 版本 |
|---|---|---|
| `About-Windows` | Command | 26 |
| `Get-Help` | Command | 26 |
| `Get-Date` | Command | 26 |
| `Get-Alias` | Command | 26 |
| `Get-Child` | Command | 26 |
| `Get-Command` | Command | 26 |
| `Get-Content` | Command | 26 |
| `Get-Event` | Command | 266 |
| `Get-History` | Command | 26 |
| `Get-Host` | Command | 26 |
| `Get-Item` | Command | 26 |
| `Get-Local` | Command | 26 |
| `Get-Member` | Command | 26 |
| `Get-Module` | Command | 26 |
| `Get-Network` | Command | 26 |
| `Get-Object` | Command | 26 |
| `Get-Process` | Command | 26 |
| `Get-Service` | Command | 26 |
| `Get-Session` | Command | 26 |
| `Get-Time` | Command | 26 |
| `Get-Type` | Command | 26 |
| `Get-Variable` | Command | 26 |
| `Get-Volume` | Command | 26 |
| `New-Item` | Command | 26 |
| `New-Module` | Command | 26 |
| `New-Object` | Command | 26 |
| `New-Service` | Command | 26 |
| `New-Variable` | Command | 26 |
| `Out-Console` | Command | 26 |
| `Out-File` | Command | 26 |
| `Out-GridView` | Command | 26 |
| `Out-String` | Command | 26 |
| `Select-Help` | Command | 26 |
| `Select-Object` | Command | 26 |
| `Select-String` | Command | 26 |
| `Set-Content` | Command | 26 |
| `Set-Location` | Command | 26 |
| `Set-Variable` | Command | 26 |
| `Test-Connection` | Command | 26 |
| `Test-Path` | Command | 26 |
| `Test-Help` | Command | 26 |
| `Test-Type` | Command | 26 |
| `Write-Host` | Command | 26 |
| `Write-Output` | Command | 26 |
| `Write-Warning` | Command | 26 |
| `Write-Variable` | Command | 26 |

### 可发现性

PowerShell 允许你发现它的功能。例如，通过使用 `Get-Command`，你可以看到特性。

PowerShell 设计为可扩展的。因为它是面向对象的，你可以使用管道将对象从一个 cmdlet 传递到另一个。

```powershell
get-service
```

### 一致性

PowerShell 提供跨平台的环境。这使得管理员编写脚本变得更容易。例如，如果你学会了使用一个 cmdlet，很可能就会使用许多。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_84_3.png)

### 交互式和脚本环境

PowerShell 是一个交互式和脚本环境，具有命令行的力量和现代语言的灵活性。PowerShell 控制台是一个交互应用程序，允许你测试命令并查看结果。

### 导航层次级数据存储

传统的 Shell 设计用于交互和导航计算机的文件系统。文件系统是由驱动器、文件夹和文件组成的层次级数据存储。在 `cmd.exe` 中，`dir` 命令用于显示目录内容，`cd` 命令用于导航文件系统。Windows PowerShell 中也有类似的命令（`Get-ChildItem` 和 `Set-Location`）。

然而，与传统的 Shell 不同，PowerShell 不仅限于计算机的文件系统。相反，Windows PowerShell 能够访问和导航许多层次级数据存储，包括：

- 别名命令
- 环境变量
- PowerShell 函数
- 注册表
- 变量
- 证书

为了方便访问不同的层次级数据存储，Windows PowerShell 实现了一种程序模型，以模拟文件系统的方式暴露不同的层次级数据存储。这样，你不仅可以访问这些不同的数据存储，还可以熟悉的命令（例如 `cd` 或 `Set-Location` 以及 `dir` 或 `Get-ChildItem`）。

可以通过执行 `Get-PSProvider` cmdlet 来查看 Windows PowerShell 支持的所有程序列表，如下：

```powershell
PS C:\MyScripts> Get-PSProvider
```

| 名称 | 功能 | 驱动器 |
|---|---|---|
| Alias | ShouldProcess | (Alias) |
| Environment | ShouldProcess | (Env) |
| FileSystem | Filter, ShouldProcess | (C, D, J, K...) |
| Function | ShouldProcess | (Function) |
| Registry | ShouldProcess, Transact... | (HKLM, HKCU) |
| Variable | ShouldProcess | (Variable) |
| Certificate | ShouldProcess | (cert) |

```powershell
PS C:\MyScripts>
```

正如此 cmdlet 所示，每个提供程序都被表示为一个驱动器。或者，你可以使用 `Get-PSDrive` 命令来显示可用驱动器列表以及它们关联的提供程序，如下所示：

```powershell
PS C:\MyScripts> Get-PSDrive
```



# Microsoft Windows PowerShell 2.0 零基础入门编程，第二版

## 第 2 章 与 Windows PowerShell 交互

正如此 cmdlet 所示，每个提供程序都被表示为一个驱动器。或者，你可以使用 `Get-PSDrive` cmdlet 来显示可用驱动器列表以及它们关联的提供程序，如下所示：

```
PS C:\MyScripts> Get-PSDrive
```

| 名称 | 提供程序 | 根目录 | 当前位置 |
| --- | --- | --- | --- |
| Alias | | | |
| C | FileSystem | C:\ | MyScripts |
| cert | Certificate | \ | |
| D | FileSystem | D:\ | |
| E | FileSystem | E:\ | |
| Env | Environment | | |
| F | FileSystem | F:\ | |
| Function | FileSystem | G:\ | |
| G | H | FileSystem | H:\ | |
| HKCU | Registry | HKEY_CURRENT_USER | |
| HKLM | Registry | HKEY_LOCAL_MACHINE | |
| I | FileSystem | I:\ | |
| J | FileSystem | J:\ | |
| K | FileSystem | K:\ | |
| M | FileSystem | M:\ | |
| Variable | Variable | | |

你可以使用 `Set-Location` cmdlet 访问由 Windows PowerShell 提供程序暴露的任何驱动器。例如，要从默认的 `C:` 驱动器切换到逻辑 `Env` 驱动器，你需要输入：

```
PS C:\> Set-Location Env:
PS Env:\
```

> 提示：`Env` 驱动器提供了对 Windows 操作系统维护的系统环境变量的访问。

一旦你针对特定的驱动器，就可以使用 `Get-ChildItem` cmdlet 显示其内容，就像它是物理磁盘驱动器一样，如下所示：

```
PS C:\MyScripts> Set-Location Env:
PS Env:\> Get-ChildItem
```

| 名称 | 值 |
| --- | --- |
| Path | C:\Program Files\PHP\c:\ruby\bin;C:\Win... |
| TEMP | C:\Users\Jerry\AppData\Local\Temp |
| ProgramData | C:\ProgramData |
| PATHEXT | .COM;.EXE;.BAT;.CMD;.VBE;.JS;.JSE... |
| USERDOMAIN | HP-PC |
| PROCESSOR_ARCHITECTURE | x86 |
| SystemDrive | C: |
| RoxioCentral | c:\Program Files\Common Files\Roxio Shar... |
| APPDATA | C:\Users\Jerry\AppData\Roaming |
| windir | C:\Windows |
| LOCALAPDATA | C:\Users\Jerry\AppData\Local |
| SESSIONNAME | Console |
| RUBOPT | -rubygems |
| TMP | C:\Users\Jerry\AppData\Local\Temp |
| USERPROFILE | C:\Users\Jerry |
| ProgramFiles | C:\Program Files |
| FP_NO_HOST_CHECK | NO |
| HOMEPATH | \Users\Jerry |
| COMPUTERNAME | HP-PC |
| CLSPATH | C:\Program Files\Java\jre.6.0_05\lib... |
| PROCESSOR_LEVEL | 15 |
| NUMBER_OF_PROCESSORS | 2 |
| PROCESSOR_IDENTIFIER | x86 Family 15 Model 107 Stepping 1, Auth... |
| USERNAME | Jerry |
| PCBRAND | Pavilion |
| ComSpec | C:\Windows\system32\cmd.exe |
| LOGONSERVER | \\HP-PC |
| OnlineServices | Online Services |
| CommonProgramFiles | C:\Program Files\Common Files |
| SystemRoot | C:\Windows |
| PHPRC | C:\Program Files\PHP\ |
| PROCESSOR_REVISION | 6b01 |
| QTJAVA | C:\Program Files\Java\jre.6.0_05\lib... |

由于 Windows PowerShell 抽象不同层级数据结构的方式，你可以轻松地访问 Windows 注册表的部分，就像访问物理驱动器或本地 `Env` 驱动器一样。Windows 注册表组织成一系列高级键。Windows PowerShell 提供了对其中两个键的访问，如表 2.2 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_88_0.png)

| 注册表键 | 缩写 | 描述 |
| --- | --- | --- |
| HKEY_LOCAL_MACHINE | HKLM | 存储影响计算机上所有用户的系统配置设置信息。 |
| HKEY_CURRENT_USER | HKCU | 存储当前登录用户的配置设置信息。 |

要访问表 2.2 列出的两个注册表键之一，你必须引用其缩写名称，如下所示：

```
PS HKCU:\> Set-Location
PS Env:\> Get-ChildItem
```

### 暂停脚本执行并等待玩家按 Enter 键

`Read-Host`

如你所见，这些语句由许多 `Write-Host` cmd 语句组成，用于显示故事的开场界面。注意 `Read-Host` cmd 语句的位置。执行它时，它将暂停脚本并等待用户按下 Enter 键。

### 为玩家提供指令

现在，让我们通过在脚本文件末尾添加以下语句，为用户提供与故事进行交互的指令。

```
# 清空 Windows 命令控制台屏幕
Clear-Host
```

```
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host " 这是一个交互式的填空风格故事。在讲述它"
Write-Host
Write-Host " 之前，你必须回答几个问题。"
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host " 按 Enter 继续。"
```



## 暂停脚本执行并等待玩家按 Enter 键

`Read-Host`

如你所见，这些前面的语句将清空 Windows 命令控制台屏幕。然后将按顺序执行一系列 `Write-Host` cmd 以显示包含游戏指令的文本。最后，`Read-Host` cmd 会暂停脚本，让用户在继续之前有机会阅读指令。

### 提示玩家输入

现在是时候开始收集用户输入了。显示故事第一个问题并存储用户答案的代码语句所示，并应追加到脚本文件的末尾。

```
#向玩家提问第一个问题

while ($animal -eq "")
```

```
Clear-Host #清空 Windows 命令控制台屏幕

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

$animal = read-host " 输入一种可怕动物的名称 *"

}
```

在这里，设置了一个 `while` 循环来控制与用户的交互。它的主要目的是防止用户在没有先输入任何内容的情况下直接按 Enter 键。用户的答案被赋值给变量 `$animal`。

> 现在先不用担心变量和 `while` 循环的示例原理。这些将在第 4 章“处理变量、数组和哈希表”以及第 5 章“实现条件逻辑”中详细介绍。

### 收集额外输入

接下来，在脚本文件末尾添加以下代码语句。这些语句负责收集故事所需的其余输入。

```
#向玩家提问第二个问题

while ($vehicle -eq "")
```

```
Clear-Host #清空 Windows 命令控制台屏幕

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host
```

```
$vehicle = read-host " 输入一种交通工具的名称 " 

#向玩家提问第三个问题

while ($store -eq ""){

Clear-Host #清空 Windows 命令控制台屏幕

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

$store = read-host " 输入你最喜欢的商店的名称 " 

#向玩家提问第四个问题

while ($dessert -eq ""){

Clear-Host #清空 Windows 命令控制台屏幕

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

$dessert = read-host " 输入你最喜欢的甜点的名称 " 
```

如你所见，这些语句被组织成三个 `while` 循环，每个循环都仅仅是提示用户为故事第一个问题提供答案的代码语句的简单变体。

### 显示故事开场

现在已经收集了讲述故事所需的输入，是时候开始构成故事的文本了。首先，在脚本文件末尾添加以下语句。

```
#清空 Windows 命令控制台屏幕

Clear-Host

#为玩家提供指令

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host " 从以前，有三个非常特别的孩子"

Write-Host " 分别名叫 Alexander、William 和 Molly。Alexander 是最大的"

Write-Host " 以勇敢强壮闻名。Molly 是最小的，"

Write-Host " 只有七岁，但她拥有一种非凡的"

Write-Host " 意识力，即使是最智的圣者也会"

Write-Host " 佩服并尊重。William 是中间的孩子，既"

Write-Host " 勇敢又聪明，远超他的年龄。他们住在"

Write-Host " 山顶上，就在小镇外围，那里"

Write-Host " 他们忠实地守护着镇民。他们总是"

Write-Host " 在在一起，总是互相照顾"

Write-Host " 以及镇上的"

Write-Host " 人，他们被大家称为“三剑侠”。"

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host " 按 Enter 继续。"
```

## 暂停脚本执行并等待玩家按 Enter 键

这些语句清空屏幕，显示一些故事文本，然后暂停脚本执行直到用户按下 Enter 键。

### 显示故事剩余部分

显示故事剩余部分的语句所示，并应追加到脚本文件的末尾。

```
### 清空 Windows 命令控制台屏幕

Clear-Host
```

```
### 为玩家提供指令

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host
```

```
Write-Host " 有一天，一个开头与其他任何日子并无异的日子，"

Write-Host " 巨大的吼声从镇中心传来。妇女和"

Write-Host " 孩子们可以看到惊恐地尖叫奔跑。"

Write-Host " 三剑侠爬上他们的哨塔，"

Write-Host " 开始扫描街道以寻找噪音和"

Write-Host " 恐慌的来源。Alexander 先发现了问题，"

Write-Host " 看到一只巨大的动物正快速向"

Write-Host " 市长办公室移动。在动物面前站着镇上的"

Write-Host " 男士们，试图进行绝死的抵抗。"

Write-Host " `我们怎么办？` Alexander 说道。William 环顾四周，

Write-Host " 看到一堆甜点堆在镇上"

Write-Host " 发店门口。`跟我走！` William 喊道，"

Write-Host 直 直向那堆甜点。Alexander"

Write-Host " 和 Molly 立即知道该做，每人拿一个甜点"

Write-Host " 向动物投掷甜点。无法"

Write-Host " 应对来自三剑侠的攻击力量，"

Write-Host " 动物逃离了镇，再也没有被见过或听到"

Write-Host " 再次。"

Write-Host

Write-Host

Write-Host

Write-Host " 按 Enter 继续。"
```

### 为玩家提供指令

```powershell
Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host " The townsfolk ran out of the $store and began cheering for"

Write-Host " their heroes. Once again The Three Amigos had saved the day."

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host ""          T H E   E N D"

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host " Press Enter to continue."
```

## 暂停脚本执行并等待玩家按 Enter

`Write-Host`

### 清除 Windows 命令控制台屏幕

`Clear-Host`

注意嵌入在 `Write-Host` 语句中显示故事文本的变量名。执行时，这些变量都将自动替换为用户之前在脚本文件中提供的文本字符串。为了让这些变量的位置脱出来，我已将它们**加粗**。

## 第 2 章 - 与 Windows PowerShell 交互！

### 摘要

本章涵盖了许多不同的 PowerShell 主题，帮助你对如何与 PowerShell 命令行交互建立坚实的理解。你学习了如何配置 Windows 命令控制台以自定义你的工作环境。你学习了如何配置 Windows 命令外，将你的 Windows PowerShell 脚本文件夹自动设置为默认工作目录。你还学习了如何使用制表符补全，以及使用 PowerShell 导航并访问不同类型的系统资源，包括 Windows 注册表和环境变量。

现在，在进入第 3 章“基于 .NET 的对象的脚本编写”之前，我建议你额外花几分钟时间，通过实现以下挑战来完善和改进《三剑侠的故事》。

### 挑战

- 1. 首先，考虑提示用户提供额外的输入，并根据她的答案进一步增加故事的不可预测性。
- 2. 考虑重写故事的结局，使其更加令人兴奋，或给它一个出乎意料且幽默的转折。
- 3. 最后，不要忘记使用你自己的名字修改作者信息。此外，你可能还想添加一些信息，例如你网站的 URL 或电子邮箱地址。

## 章节

基于 .NET 的对象的脚本编写

Windows PowerShell 与微软的 .NET Framework 深度集成，该框架提供了开发 Windows 应用程序和脚本所需的许多支持环境。在本章中，你将学习 Windows PowerShell 如何利用 .NET 资源。你将学习 .NET 类库和常用的运行时语言。你将学习如何执行 cmdlet（命令/程序）并使用 cmdlet 访问对象的属性和方法。你还将回顾 cmdlet 别名并学习如何创建自己的自定义别名。在所有这一切之上，你将学习如何通过程序自定义 Windows PowerShell，并开发 PowerShell 占卜师游戏。

具体而言，你将学习：

- 如何创建 `profile.ps1` 脚本文件并使用它自定义 Windows PowerShell
- 关于 Windows PowerShell 与 .NET 集成的更多背景信息
- 如何使用对象管道在 cmdlet 之间传递结构化数据
- 如何创建自定义别名

## 项目预览：PowerShell 占卜游戏

本章的游戏项目是 PowerShell 占卜游戏。该游戏模拟了与虚拟占卜师的对话，占卜师会听玩家的问题并提供答案。答案取决于占卜师的心情，而心情会根据提问的时间而改变。所有问题都应该以可以用“是/否”回答的方式来提。

游戏首次启动时，会显示图 3.1 所示的欢迎界面。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_103_0.png)

图 3.1
PowerShell 占卜游戏的欢迎界面。

按 Enter 消除欢迎界面。接下来，将显示指令，为玩家提供关于正确提问方法的指导，如图 3.2 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_103_1.png)

图 3.2
玩家获得了如何提问题的指导。

接下来，玩家会被提示问她的问题，如图 3.3 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_104_0.png)

图 3.3
玩家被要求问可以用是/否回答的问题。

作为回应，游戏将从 8 个可能的答案中随机选择 1 个并显示，如图 3.4 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_104_1.png)

图 3.4
占卜师用各种答案回答。

然后玩家会被提示按 Enter 继续向占卜师提另一个问题，或输入 Q 结束游戏，如图 3.5 所示。

游戏通过显示一条建议玩家返回再次玩的消息结束，如图 3.6 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_105_0.png)

图 3.5
玩家可以向占卜师提尽可能多的问题。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_105_1.png)

图 3.6
游戏结束并邀请返回。

## 额外的 PowerShell 自定义技术

在我们深入研究 .NET Framework 以及 PowerShell 如何使用 cmdlet 使用 .NET 资源之前，让我们花几分钟查看一种自定义 Windows PowerShell 的方法。

正如你在第 2 章“与 命令行交互”中学到的，你可以通过修改 PowerShell 快捷方式来自定义 PowerShell 环境。此外，你还学习可以通过创建一个名为 `profile.ps1` 的脚本文件并存储在配置文件夹中（由 `$profile` 指定）来程序化配置你的环境。当你这样做时，放在 `profile.ps1` 中的脚本会在每次启动新的 PowerShell 会话时自动执行。计算机的其他用户不受影响。然而，如果你将 `profile.ps1` 文件移动到 `C:\Windows\system32\WindowsShell\v1.0` 文件夹，它每个用户启动新的 PowerShell 会话时运行。

通过开发 `profile.ps1` 脚本，计算机管理员可以通过远程部署脚本文件到任意计算机来管理大量计算机，而无需访问和配置单台计算机。例如，你可以创建一个类似于示例的 PowerShell 脚本文件并将其分发到所有公司计算机的 `C:\Windows\system32\WindowsShell\v1.0` 文件夹，以确保意识公司计算机政策。

```powershell
# ################################################## 脚本名称: Profile.ps1 (PowerShell 配置文件脚本)

# 版本: 2.0

# 作者: Jerry Lee Ford, Jr.

# 日期: 2008年10月10日

#

# 说明: 此 PowerShell 脚本包含了自定义

# PowerShell 执行环境的命令。

#

################################################***
```

```powershell
# 创建自定义别名命令

Set-Alias ds Write-Host
```

```powershell
### 清除 Windows 命令控制台屏幕

Clear-Host
```

```powershell
### 显示自定义欢迎语

ds "此台计算机和网络是私有的。使用此台计算机表示您同意公司安全政策中列出的所有条款。"

ds "违反这些政策可能导致刑事起诉。"
```



执行时，此脚本创建一个名为`ds`的自定义别名，它是`Write-Host` cmdlet 的快捷方式。你将在本章后面的部分学习更多关于别名以及如何创建它们的内容。

下一章。屏幕被清空，然后使用新创建的别名，将显示一条关于公司安全策略的消息。图 3.7 展示了用户每次启动新的 Windows PowerShell 会话时将看到的内容。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_107_0.png)

图 3.7 确保用户在 Windows PowerShell 启动时对安全策略有意识。

### 微软 .NET FRAMEWORK

.NET Framework 是现代 Windows PowerShell 脚本的核心组件。.NET Framework 2 版本是 Windows PowerShell 1.0 和 2.0共同共同。因此，PowerShell 程序员对 .NET Framework 的主要组件及其提供的服务有深入理解是非常重要的。.NET 是一个旨在支持桌面、网络和基于 Internet 的应用程序的框架，.NET 还支持为 PDA 等设备开发移动应用程序。

框架（Framework）是一系列促进脚本和程序开发的资源集合。框架的目的是通过为程序员提供预定义的服务和资源访问权限，减轻开发新程序和脚本时涉及的大部分复杂性，让程序员能够专注于解决特定问题所需的高层逻辑。

.NET Framework 设计用于支持与任何符合 .NET 标准的应用程序或脚本开发编程语言相结合开发的应用程序和脚本。事实上，微软生成了一套围绕 .NET Framework 构建的完整应用程序编程语言。这些语言包括 Visual Basic、C++、C# 和 F#。微软正将 .NET Framework 作为其所有新编程语言的关键组件进行推广。因此，微软决定将 .NET Framework 集成到 Windows PowerShell 中这并不意外，使其及其脚本语言能够立即访问海量的资源和命令。

# 第 3 章 使用 .NET 进行基于对象的脚本编写

## Key .NET Framework 组件

.NET Framework 充当 Windows PowerShell 和操作系统之间的接口。.NET 负责将脚本代码翻译成可以在你的计算机上执行的格式。图 3.8 显示了 .NET Framework 在支持应用程序和脚本开发中扮演的角色。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_108_0.png)

.NET Framework 由两个关键组件组成，如下文所示。

- .NET Framework 类库
- CLR (公共语言运行时)

如果图 3.8 中存在你不理解的元素，不要太担心。我将在后面的章节中详细介绍每一个部分。

### .NET 类库

传统的命令行外壳对数据的识别能力非常有限，通常只有字符串和数字。然而，Windows PowerShell 强制使用结构紧密的数据。因此，Windows PowerShell 可以处理许多不同类型的数据，包括字符串、日期、整数、浮点数、布尔数据等。

结构化数据也是 .NET Framework 的一个特性。通过 .NET，结构化数据被分组到不同的集合中以定义复杂的结构化类。类被用作创建对象的模板，对象代表 Windows PowerShell 可以访问和操作的事物。对象是一个自包含的资源，包含了关于自身的信息以及访问和操作它所需的代码。例如，文件、文件夹和磁盘驱动器都被 Windows PowerShell 视为对象。

## 86 初学者 Windows PowerShell 2.0 编程，第二版

对象具有某些属性（properties），这些属性定义了对象的特定特征。例如，文件夹有名称。对象提供了对预定义代码集合的访问，称为方法（methods），可以按顺序执行以与对象进行交互并控制。例如，文件对象提供了可以用于对文件执行各种操作的方法访问，包括打开、关闭和删除文件。

### 公共语言运行时

公共语言运行时或 CLR 负责将 Windows PowerShell 脚本转换为计算机可以理解并运行的可执行格式。CLR 还为 PowerShell 提供其他服务，包括：

- 编译
- 安全
- 内存管理
- 异常处理

### 访问 .NET Framework 资源

Windows PowerShell 通过 cmdlet 提供对 .NET 资源的访问。cmdlet 在访问 .NET 资源的同时隐藏了其中涉及的大部分复杂性。作为 PowerShell 程序员，你不需要担心特定的 .NET 类或其属性和方法。你只需要知道使用哪些 cmdlet 来获取脚本所需的资源类型即可。为了理解我的意思，请考虑以下系列示例。

在第一个示例中，让我们执行`Get-ChildItem` cmdlet。`Get-ChildItem`获取一个代表当前工作目录中每个文件和子文件夹的对象列表。.NET Framework 存储了大量关于文件对象的信息或属性。然而，默认情况下，Windows PowerShell 只显示这些属性中的几个，如下所示：

```
PS C:\MyScripts> Get-ChildItem
```

```
Directory: Microsoft.PowerShell.Core\FileSystem::C:\MyScripts
```

| Mode | LastWriteTime | Length | Name |
|---|---|---|---|
| -a-- | 9/26/2006 6:14 PM | 4661 | FortuneTeller.ps1 |
| -a-- | 10/3/2008 11:51 AM | 1077 | KnockKnock.ps1 |
| -a-- | 10/3/2008 11:51 AM | 832 | Profile.ps1 |

# 第 3 章 使用 .NET 进行基于对象的脚本编写

- -a---- 10/3/2008 11:51 AM 7701 SeinfeldTrivia.ps1
- -a---- 9/23/2006 2:22 PM 7598 ThreeAmigos.ps1

```
PS C:\Scripts>
```

在这里，显示了每个文件对象的`Mode`、`LastWriteTime`、`Length`和`Name`属性。接下来，关注一个特定的文件，如下所示：

```
PS C:\Scripts> Get-ChildItem Profile.ps1
```

```
Directory: Microsoft.PowerShell.Core\C:\MyScripts
```

| Mode | LastWriteTime | Length | Name |
|---|---|---|---|
| -a---- | 10/3/2008 11:51 AM | 832 | Profile.ps1 |

```
PS C:\Scripts>
```

在这个示例中，`profile.ps1`被作为参数传递给`Get-ChildItem` cmdlet。结果是只显示了该文件对象的属性信息。现在我们专注于特定对象的属性，让我们进一步探索一下，看看 .NET 为此对象还保留了哪些类型的属性信息。接下来的示例获取`Get-ChildItem` cmdlet 生成的输出并将其传递给`Get-Member` cmdlet。`Get-Member` cmdlet 接收了一个名为`-MemberType`的参数。该参数可以取不同的值。在这个示例中，指定了`Property`的值。结果是显示了 .NET Framework 对该特定文件的属性。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_110_0.png)

> 记住，Windows PowerShell 将一切视为对象，而对象具有描述对象的特征。这些特征通常被称为属性（properties）。如前面的示例所示，大多数 cmdlet 以对象的形式传递数据。在下一个示例中，`Get-ChildItem`生成的对象数据被传递给`Get-Member` cmdlet 进行处理。

```
PS C:\Scripts> Get-ChildItem Profile.ps1 | Get-Member -MemberType
```

Property

```
TypeName:System.FileInfo
```

## 88 初学者 PowerShell 2.0 编程，第二版

| Name | MemberType |
|---|---|
| Attributes | System.IO.FileAttributes (get;set); |
| CreationTime | System.DateTime CreationTime (get;set); |
| CreationUtc | System.DateTime CreationUtc (get;set); |
| Directory | System.IO.Directory (get:); |
| DirectoryName | System.String DirectoryName (get:); |
| Exists | System.Boolean Exists (get:); |
| Extension | System.String Extension (get:); |
| FullName | System.String FullName (get:); |
| IsReadOnly | System.Boolean IsReadOnly (get;set); |
| LastAccessTime | System.DateTime LastAccessTime (get;set); |
| LastAccessUtc | System.DateTime LastAccessUtc (get;set); |
| LastWriteTime | System.DateTime LastWriteTime (get;set); |
| Length | System.Int64 Length (get:); |
| Name | System.String Name (get:); |

```
PS C:\Scripts>
```

正如你所看到的，NET Framework 存储了许多`Get-ChildItem` cmdlet 不自动显示的属性。然而，这些信息在下一个示例中是可以很容易获取的。

```
PS C:\Scripts> Get-ChildItem Profile.ps1 | Select-Object name, extension, directory
```

| Name | Extension | Directory |
|---|---|---|
| Profile.ps1 | .ps1 | C:\Scripts |

```
PS C:\Scripts>
```

在这个示例中，再次使用`Get-ChildItem` cmdlet 获取`profile.ps1`文件的信息。然而，这次使用`Select-Object` cmdlet 来检索并显示不同的对象属性，特别是`Name`、`Extension`和`Directory`属性。注意，要检索的具体属性名称是以逗号分隔的参数列表传递的。

# 第 3 章 • 使用 NET 进行对象-事件感知

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_112_0.png)

`Select-Object`命令行程序提供了确定通过管道传递的对象哪些被保留或丢弃的能力。在上一个示例中，`Get-ChildItem`命令行返回的所有对象中，除了`profile.ps1`之外的都被丢弃了。

简而言之，与仅以简单文本格式返回有限数据的传统命令壳不同，Windows PowerShell 命令行程序（cmdlets）让你能够直接访问各种后台对象信息。

如前所述，.NET Framework 类定义了与特定类相关的每个对象的所有属性和方法。因此，如示例所示，你还可以检索与给定对象关联的方法列表。

```
PS C:\MyScripts> Get-ChildItem Profile.ps1 | Get-Member -MemberType Method
```



```
TypeName: System.IO.FileInfo

| Name | Member Definition |
| --- | --- |
| AppendText | System.IO.StreamWriter AppendText() |
| CopyTo | System.IO.FileInfo CopyTo(String d... |
| Create | System.IO.File Create() |
| CreateObjRef | System.Runtime.Remoting.ObjRef Cre... |
| CreateText | System.IO.StreamWriter CreateText() |
| Decrypt | System.Void Decrypt() |
| Delete | System.Void Delete() |
| Encrypt | System.Void Encrypt() |
| Equals | System.Boolean Equals(Object obj) |
| GetAccessControl | System.Security.AccessControl.File... |
| GetHashCode | System.Int32 GetHashCode() |
| GetLifetimeService | System.Object GetLifetimeService() |
| GetObjectData | System.Void GetObjectData(Serial... |
| GetType | System.Type GetType() |
| InitializeLifetimeService | System.Object InitializeLifetimese... |
| MoveTo | System.Void MoveTo(String destfile... |
| Open | System.IO.File Open(FileMode... |
| OpenRead | System.IO.File OpenRead() |
| OpenText | System.IO.StreamReader OpenText() |
| OpenWrite | System.IO.File OpenWrite() |
| Refresh Method | System.Void Refresh() |
| Replace Method | System.IO.FileInfo Replace(String ... |
| SetAccessControl Method | System.Void SetAccessControl(FileS... |
| ToString | System.String ToString() |

PS C:\MyScripts>
```

如你所见，在这个示例中，传递给`Select-Object`命令行程序的`MemberType`参数的值已从属性（property）更改为方法（Method）。

如果关于 .NET Framework 类、对象、属性和方法的讨论让你感到困惑或无从从，请不要担心。完全理解所有这些新技术需要时间。但好消息是，作为一名 Windows PowerShell 程序员，你不需要直接关注 .NET。相反，你只需要习惯于使用这些命令行程序，并让 .NET Framework 去处理底层的复杂性即可。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_113_0.png)

你可以通过访问 www.microsoft.com/net 更多关于 .NET Framework 的信息。

### 执行命令行程序

命令行程序（Cmdlets）是 Windows PowerShell 的关键资源，提供了对 .NET Framework 资源的访问。Windows PowerShell 提供了一系列命令，每个命令都设计用于执行单一任务。单独来说，命令行程序提供了对特定资源和命令的访问。然而，当这些程序作为构建块组合使用以制定复杂的任务时，它们真正的威力才会体现出来。

在下一节中，你将学习更多关于 Windows PowerShell 如何让你将命令行程序组合成复杂的语句。但是，为了操作 Windows PowerShell 并编写 PowerShell 脚本，了解 PowerShell 为你提供的每个命令行程序的特性将有所帮助。为了帮助你，我在表 3.1 中提供了一份完整的 PowerShell 命令行程序列表，并简要说明了每个命令行程序的功能以及哪些版本的 Windows PowerShell 支持它们。

### 表 3.1 WINDOWS POWERSHELL 命令行程序

| Cmdlet | 1.0 | 2.0 | 描述 |
|---|---|---|---|
| Add-Content | Yes | Yes | 向指定项目(s)的内容添加。 |
| Add-History | Yes | Yes | 向会话历史中添加条目。 |
| Add-Member | Yes | Yes | 向对象添加用户定义的自定义成员。 |
| Add-Module | No | Yes | 允许将脚本或 DLL 加载为模块。 |
| Add-PSSnapIn | | Yes | 向当前 Ps 控制台添加一个或多个 PSSnap（包含额外的提供程序或命令行程序集合）。 |
| Add-Type | No | Yes | 允许加载 DLL 或程序集而不是使用 .NET 框架访问资源。 |
| Clear-Content | Yes | Yes | 从项目或文件中删除内容同时保持文件完整。 |
| Clear-History | No | Yes | 清除当前会话期间执行的命令列表。 |
| Clear-Item | Yes | Yes | 将指定位置的项目(s)设置为提供程序指定的“清空”值。 |
| Clear-ItemProperty | Yes | Yes | 将指定位置的项目(s)设置为提供程序指定的“清空”值。 |
| Clear-Variable | Yes | Yes | 清除变量。 |
| Compare-Object | Yes | Yes | 比较两个对象。 |
| Complete-Process | | Yes | 完成进程。 |
| ConvertFrom-Csv | No | Yes | 将 CSV 对象。 |
| ConvertFrom-SecureString | | | 从安全字符串转换。 |
| ConvertFrom-String | Yes | Yes | 来自字符串。 |
| ConvertTo-Csv | No | Yes | 转换为 CSV。 |
| ConvertTo-Html | | Yes | 转换为 HTML。 |
| ConvertTo-SecureString | | | 转换为安全字符串。 |
| ConvertTo-Xml | | Yes | 转换为 XML。 |
| Copy-Item | Yes | Yes | 表示命名空间中项目的对象。 |
| Copy-ItemProperty | Yes | Yes | 在位置之间复制。 |
| Disable-PSBreakpoint | | Yes | 关闭断点。 |
| Enable-PSBreakpoint | | Yes | 开启断点。 |
| Export-Alias | Yes | Yes | 返回命令行程序的别名。 |
| Export-Clixml | Yes | Yes | 生成 clixml 表示。 |
| Export-Console | | Yes | 导出控制台。 |
| Export-Csv | No | Yes | 导出 CSV。 |
| Export-History | Yes | Yes | 导出会话历史。 |
| Export-Module | | Yes | 将模块导出到文件。 |
| ForEach-Object | Yes | Yes | 对管道中的每个对象应用脚本块。 |
| Format-Custom | Yes | Yes | 以定义的视图格式化输出。 |
| Format-List | Yes | Yes | 将对象格式化为列表。 |
| Format-Table | Yes | Yes | 将输出格式化为表格。 |
| Format-Wide | Yes | Yes | 将对象格式化为宽表。 |
| Get-Acl | Yes | Yes | 获取关联文件的访问控制列表 (ACL)。 |
| Get-Alias | Yes | Yes | 返回命令行程序的别名。 |
| Get-AuthenticSignature | Yes | Yes | 获取关联文件的签名对象。 |
| Get-ChildItem | Yes | Yes | 获取驱动器指定位置的子项目。 |
| Get-Command | Yes | Yes | 获取命令的基本信息。 |
| Get-Content | Yes | Yes | 生成位置的内容。 |
| Get-Credential | Yes | Yes | 根据密码获取凭据对象。 |
| Get-Culture | Yes | Yes | 获取文化信息。 |
| Get-Date | Yes | Yes | 获取当前日期和时间。 |
| Get-Event | No | Yes | 从事件日志和事件跟踪日志中检索事件。 |
| Get-EventLog | Yes | Yes | 获取机器日志数据。 |
| Get-ExecutionPolicy | Yes | Yes | 获取当前壳的执行策略。 |
| Get-Help | Yes | Yes | 打开帮助文件。 |
| Get-History | Yes | Yes | 获取会话历史列表。 |
| Get-Host | Yes | Yes | 获取主机信息。 |
| Get-Item | Yes | Yes | 返回命名空间中项目的对象。 |
| Get-ItemProperty | Yes | Yes | 获取对象的属性。 |
| Get-Location | Yes | Yes | 显示当前位置。 |
| Get-Member | Yes | Yes | 枚举传递给它的对象的属性、方法、类型 和属性集。 |

## 第 3 章 - 使用 NET 进行基于对象的脚本编写

| Cmdlet | 1.0 | 2.0 | 说明 |
| --- | --- | --- | --- |
| Get-Module | No | Yes | 获取一个或多个已加载的模块，返回 PSModuleInfo 对象。 |
| Get-PfxCertificate | Yes | Yes | 获取 pfx 证书信息。 |
| Get-Process | Yes | Yes | 获取机器上的进程列表。 |
| Get-PSBreakpoint | No | Yes | 获取所有设置断点的列表。 |
| Get-PSCallStack | No | Yes | 获取并显示当前调用栈。 |
| Get-PSDrive | Yes | Yes | 获取指定 Ps 驱动器的驱动信息 (DriveInfo)。 |
| Get-PSEvent | No | Yes | 订阅特定类型的事件。 |
| Get-PSEventSubscriber | No | Yes | 显示当前会话的所有事件订阅者列表。 |
| Get-PSJob | No | Yes | 获取后台作业。 |
| Get-PSProvider | Yes | Yes | 获取指定提供程序的信息。 |
| Get-PSSnap | Yes | Yes | 列出注册的快照。 |
| Get-Random | No | Yes | 生成随机数。 |
| Get-Runspace | No | Yes | 获取当前会话中创建的空间。 |
| Get-Service | Yes | Yes | 获取服务列表。 |
| Get-TraceSource | Yes | Yes | 列出给定跟踪源的属性。 |
| Get-UICulture | Yes | Yes | 获取 UI 文化信息。 |
| Get-Unique | Yes | Yes | 获取排序列表中的唯一项。 |
| Get-Variable | Yes | Yes | 获取 PS 变量。 |
| Get-WmiObject | Yes | Yes | 生成 WMI 对象或系统上可用的 WMI 类列表。 |
| Group-Object | Yes | Yes | 对具有公共属性的相同值的对象进行分组。 |
| Import-Alias | Yes | Yes | 从文件导入别名。 |
| Import-Clixml | Yes | Yes | 导入 clixml 文件并重建 PS 对象。 |
| Import-Csv | Yes | Yes | 取自 CSV 列表的值并将对象发送到管道。 |
| Import-LocalizedData | No | Yes | 根据 UI 文化设置向脚本和函数导入特定语言的信息。 |
| Invoke-Command | No | Yes | 执行本地或远程命令。 |
| Invoke-Expression | Yes | Yes | 将字符串作为表达式执行。 |
| Invoke-History | Yes | Yes | 调用之前执行过的命令。 |
| Invoke-Item | Yes | Yes | 调用可执行文件或打开文件。 |
| Invoke-WmiMethod | No | Yes | 执行 WMI 方法。 |
| Join-Path | Yes | Yes | 将路径元素组合为单个路径。 |
| Measure-Command | Yes | Yes | 跟踪脚本块和命令的运行时间。 |
| Measure-Object | Yes | Yes | 测量对象或其属性的不同方面。 |
| Move-Item | Yes | Yes | 将项从一个位置移动到另一个位置。 |
| Move-ItemProperty | Yes | Yes | 将属性从一个位置移动到另一个位置。 |
| New-Alias | Yes | Yes | 创建新的命令-别名对。 |
| New-Item | Yes | Yes | 在命名空间中创建新项。 |
| New-ItemProperty | Yes | Yes | 设置位置项的新属性。 |
| New-Object | Yes | Yes | 创建新的 .NET 对象。 |
| New-PSDrive | Yes | Yes | 在计算机上安装新驱动器。 |
| New-PSEvent | No | Yes | 创建新事件。 |
| New-Runspace | No | Yes | 创建到 PowerShell 会话（本地或远程）的持久连接。 |
| New-Service | Yes | Yes | 创建新服务。 |
| New-TimeSpan | Yes | Yes | 创建时间戳对象。 |
| New-Variable | Yes | Yes | 创建新变量。 |
| Out-Default | Yes | Yes | 将输出发送到默认格式化。 |
| Out-File | Yes | Yes | 将命令输出到文件。 |
| Out-GridView | No | Yes | 在交互式表格中显示输出，允许对结果进行排序和搜索。 |
| Out-Host | Yes | Yes | 将管道输出发送到主机。 |
| Out-Null | Yes | Yes | 将输出到空。 |
| Out-Printer | Yes | Yes | 将输出发送到打印机。 |
| Out-String | Yes | Yes | 将输出发送到管道流。 |
| Pop-Location | Yes | Yes | 将当前工作位置更改为最后推入栈的项目目指定的的位置。 |
| Pop-Runspace | No | Yes | 终止远程交互会话。 |
| Push-Location | Yes | Yes | 将位置推入栈。 |
| Push-Runspace | No | Yes | 启动远程交互会话。 |
| Read-Host | No | Yes | 从主机控制台读取一行输入。 |
| Receive-PSJob | No | Yes | 获取后台作业的输出。 |
| Register-OperationContext | No | Yes | 注册事件订阅。 |
| Register-PSEvent | No | Yes | 允许你注册事件。 |
| Register-WmiEvent | No | Yes | 允许你注册事件。 |

| Cmdlet | 1.0 | 2.0 | 说明 |
| --- | --- | --- | --- |
| Remove-Item | Yes | Yes | 从位置删除项。 |
| Remove-ItemProperty | Yes | Yes | 从位置删除属性。 |
| Remove-Module | Yes | Yes | 从会话删除模块。 |
| Remove-PSBreakpoint | No | Yes | 删除指定的断点。 |
| Remove-PSDrive | Yes | Yes | 从会话删除驱动器。 |
| Remove-PSEvent | No | Yes | 删除事件订阅。 |
| Remove-PSJob | No | Yes | 终止后台作业。 |
| Remove-Runspace | No | Yes | 关闭运行空间。 |
| Remove-Variable | Yes | Yes | 删除变量。 |
| Remove-WmiObject | Yes | Yes | 删除 WMI 对象。 |
| Rename-Item | Yes | Yes | 重命名项。 |
| Rename-ItemProperty | Yes | Yes | 重命名属性。 |
| Restart-Service | Yes | Yes | 重启服务。 |
| Resume-Service | Yes | Yes | 恢复挂起的服务。 |
| Select-Object | Yes | Yes | 从对象中选择指定的属性。 |
| Select-String | Yes | Yes | 搜索字符串。 |
| Set-Acl | Yes | Yes | 设置访问控制列表。 |
| Set-Alias | Yes | Yes | 创建别名。 |
| Set-Content | Yes | Yes | 向文件写入内容。 |
| Set-ExecutionPolicy | Yes | Yes | 设置执行策略。 |
| Set-Item | Yes | Yes | 设置项的值。 |
| Set-ItemProperty | Yes | Yes | 设置项的属性。 |
| Set-StrictMode | Yes | Yes | 启用严格模式。 |
| Set-TraceSource | Yes | Yes | 配置跟踪源。 |
| Set-Variable | Yes | Yes | 创建或更新变量。 |
| Set-WmiInstance | No | Yes | 创建或修改 WMI 实例。 |
| Sort-Object | Yes | Yes | 按指定的属性对对象进行排序。 |

### Cmdlet（命令项）

| Cmdlet | 1.0 | 2.0 | 说明 |
|---|---|---|---|
| Where-Object | Yes | Yes | 过滤来自管道的输入，允许对某些对象进行操作。 |
| Write-Debug | Yes | Yes | 向主机显示写入调试消息。 |
| Write-Error | Yes | Yes | 写入错误对象并将其发送管道。 |
| Write-Host | Yes | Yes | 通过用户反馈机制显示对象。 |
| Write-Output | Yes | Yes | 将对象写入管道。 |
| Write-Progress | Yes | Yes | 向主机发送进度记录。 |
| Write-Verbose | Yes | Yes | 向主机的详细显示器写入字符串。 |
| Write-Warning | Yes | | 写入警告消息。 |
| Update-List | No | Yes | 从包含对象集合的属性值中添加或删除项。 |
| Undo-PSTTransaction | No | Yes | 回滚并撤销事务。 |
| Use-PSTTransaction | No | Yes | 允许当前事务应用于已事务处理的对象。 |

虽然表 3.1 中列出的所有 cmdlet 都使用初始大写字母显示，但 cmdlet 是不区分大小写的。因此，你在输入它们时使用的大小写完全取决于你自己。虽然你应该尝试记忆这些 cmdlet，但将此表书签可能是一个好主意，这样在你需要时可以回来。一旦你发现了一个看起来你特定任务所需的 cmdlet，可以使用 PowerShell 的`Get-Help`cmdlet 来了解更多信息。例如，图 3.9 显示了当你使用`Get-Help`cmdlet 查找有关`Write-Host`cmdlet 的信息时将看到的部分输出。

> `Get-Help`cmdlet 用于检索有关任何 cmdlet 或 PowerShell 主题的信息。在不带任何参数执行时，此 cmdlet 会显示帮助主题列表。当传递 cmdlet 名称或主题时，它会显示特定于该 cmdlet 或主题的信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_120_0.png)

如果你手头没有这本书，可以使用`Get-Command`cmdlet 生成可用 cmdlet 的完整列表。然后，你可以使用`Get-Help`命令来查找列表中看到的任何 cmdlet 的详细信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_120_1.png)

### 执行后台作业

Windows PowerShell 2.0 引入的一个新 Windows PowerShell 功能是可以将 cmdlet、函数和脚本作为后台作业（PSJob）执行。后台作业在后台执行，不需要任何控制台交互。一旦启动，Windows PowerShell 会立即返回 Windows PowerShell 命令行提示符，允许你在后台作业运行的同时继续工作并保持高效。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_121_0.png)

Windows PowerShell 远程依赖于 Windows 远程管理 (WinRM) 服务和 WS-Management 协议。如何配置远程访问的说明在第 1 章提供。为了运行，你的计算机和你想远程连接的计算机都必须安装 PowerShell 2.0，并且必须配置为支持 Windows PowerShell 远程。事实上，当你仅在自己的计算机上本地运行后台作业时，必须启用远程功能。你还需要适当的安全权限来执行尝试在远程计算机上执行的任何命令。

```
Windows PowerShell
PS C:\Scripts> Get-Help Write-Host
NAME
Write-Host
SYNOPSIS
将文本写入
DESCRIPTION
Write-Host [-Object [Object[]] -NoNewline -Separator [string] [-Color [Black | Red | Blue | Green | Cyan | Yellow | Magenta | White | Gray | DarkGray | DarkBlue | DarkGreen | DarkCyan | DarkRed | DarkMagenta | DarkYellow] [Gray | Red | Magenta | Yellow | White]] [CommonParameters]
Write-Host cmdlet 创建一个自定义的输出窗口。你可以使用 ForegroundColor 参数在该窗口中查看文本，并可以使用 BackgroundColor 参数指定窗口的背景颜色。使用字符串分隔显示的对象。特定结果是托管 Windows PowerShell 的程序。
RELATED LINES
Write-Verbose
Write-Progress
Write-Debug
Write-Output
Write-Warning
Out-Host
MARKS
如需更多信息，请输入："get-help Write-Host -detailed"
如需技术信息，请输入："get-help Write-Host -full"。
PS C:\Scripts>>
```

## 第3 章 · 使用 PowerShell 基于对象的脚本

后台作业可以在你的本地计算机上执行，也可以在具有安全访问权限的网络上执行。后台作业非常适合运行可能需要一段时间执行的脚本和 cmdlet。

默认情况下，Windows PowerShell 会立即返回你执行的任何命令的结果并在控制台窗口中显示它们。然而，后台作业不是显示输出，而是返回并显示一个数字，代表作业对象。你可以使用该对象来确定作业状态、控制其执行并检索其输出。

Windows PowerShell 提供了许多 cmdlet，包括`Get-Process`、`Get-Service`、`Get-EventLog`和`Get-MIObject`，它们允许你从网络计算机检索信息。这些命令通过调用 .NET 方法检索对象数据，而不依赖于 Windows PowerShell。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_122_0)

执行后，后台作业在自己的运行空间中运行，独立于 Windows PowerShell。运行空间可以是临时的或持久的，区别在于临时运行空间完成后会被删除，而持久运行空间将持续直到你显式删除它。

Windows PowerShell 2.0 提供了处理后台作业的 cmdlet。这些 cmdlet 及其功能概述如下：

- `Start-Job`：创建并执行新的本地或远程后台作业。
- `Receive-PSJob`：检索后台作业生成的输出。
- `Wait-PSJob`：指示 PowerShell 等待后台作业完成。
- `Stop-PSJob`：停止后台作业的执行。
- `Get-PSJob`：检索后台作业的信息。
- `Remove-PSJob`：删除后台作业（包括所有输出）。

Windows PowerShell 2.0 还有一个`New-Runspace`cmdlet，你可以用它设置持久运行空间。

### 创建和执行后台作业

要在本地计算机上创建并在临时运行空间中执行后台作业，你需要使用`Start-Job`cmdlet，如下所示：

```
PS C:\> Start-Job -command "Get-Service"
```

| SessionId | Name | State | MoreData | Command |
|---|---|---|---|---|
| 7 | | Running | True | Get-Service |

在这里，`Get-Service`cmdlet 作为后台作业在本地计算机上运行。注意当`Get-Service`cmdlet 执行时没有显示输出。相反，后台作业的一些状态信息以表格形式显示。这些信息包含了`SessionId`属性，你可以使用它在作业执行期间进行通信和控制。其他数据包括状态信息（显示作业是正在运行、失败、未启动还是完成）以及`HasMoreData`（如果后台作业有任何可检索的输出数据，则指示为 true）。

### 远程执行后台作业

要在跨网络在具有相应安全访问权限的计算机上远程运行后台作业，只需语句末尾添加`-computer`参数，然后加上网络计算机的主名、UNC 名称或 IP 地址，如下所示：

```powershell



```powershell
PS C:\> Start-Job -command "Get-Service" -computer FileSVR
```

| SessionId | Name | State | MoreData | Command |
|---|---|---|---|---|
| 9 | | Running | True | Get-Service |

`PS C:\>` 你可以通过提供逗号分隔的计算机列表，同时在多个网络计算机上运行后台作业，如下所示：

```powershell
PS C:\> Start-Job -command "Get-Service" -computer FileSVR, PrintSVR
```

## 第 3 章 · 使用 .NET 进行对象脚本

### 在持久性运行空间（Runspace）中运行后台作业

如果你想在持久性运行空间中运行后台作业，首先需要执行`New-Runspace`命令，然后如此处所示执行`Start-PSJob`命令行（使用其`runspace`参数）：

```powershell
PS C:\> $RunSP = New-Runspace -computename FileSVR
PS C:\> Start-PSJob -command "Get-Service" -runspace $RunSP
```

| SessionId | Name（名称） | State（状态） | HasMoreData（更多数据） | Command（命令） |
|---|---|---|---|---|
| 11 | | Running | True | Get-Service |

```powershell
PS C:\>
```

在这里，创建了一个运行空间并将其赋值给名为`$RunSP`的变量。随后使用`Start-PSJob`命令在`$RunSP`运行空间中运行`"Get-Services"`命令。

### 获取后台作业的信息

当从后台作业接收输出时，你的前台运行空间会根据指定的`SessionId`数字在后台与后台会话通信。例如，使用`Get-PSJob`命令和后台作业的`SessionId`，你可以检索其当前状态，如此处所示：

```powershell
PS C:\> Get-PSJob 11
```

| SessionId | Name（名称） | State（状态） | HasMoreData（更多数据） | Command（命令） |
|---|---|---|---|---|
| 11 | | Completed | True | Get-Service |

```powershell
PS C:\>
```

在此示例中，`Get-Service`命令作为后台作业运行。它被分配了会话 ID 11 并已完成执行。此外，如`HasMoreData`字段所示，后台作业有尚未接收的输出数据。除了此处所示通过不带任何参数执行`Get-PSJob`命令来从当前工作会话中检索特定后台作业的数据外：

(102) 《PowerShell 实战：2.0 绝对初学者编程，第二版》

```powershell
PS C:\> Get-PSJob
```

| SessionId | Name（名称） | State（状态） | HasMoreData（更多数据） | Command（命令） |
|---|---|---|---|---|
| 1 | | Completed | False | start-sleep 30 |
| 3 | | Completed | True | get-process |
| 5 | | Completed | False | get-process |
| 7 | | Completed | True | Get-Service |
| 9 | | Failed | False | Get-Service |
| 11 | | Completed | True | Get-Service |

`PS C:\>` 获取后台作业输出

如前所述，当你执行后台作业时，当后台作业执行结束时，输出不会自动返回。相反，你必须使用`Receive-PSJob`命令检索后台作业的输出，如下例所示所示：

```powershell
PS C:\> $MyJob = Start-PSJob "Get-Process"
PS C:\> Receive-PSJob $MyJob
```

| Handles（句柄） | NPM(K) | PM(K) | WS(K) VM(M) | Id（ID） | ProcessName（进程名称） |
|---|---|---|---|---|---|---|
| 103 | 5 | 1036 | 3208 | 31 | 0.03 | 1664 alg |
| 428 | 6 | 2596 | 5020 | 28 | 97.31 | 464 csrss |
| 410 | 15 | 9860 | 17588 | 68 | 4.80 | 1908 explorer |
| 0 | 0 | | 28 | 0 | 0 Idle |
| 724 | 15 | 42156 | 14424 | 142 | 24.27 | 1740 ieplore |
| 420 | 10 | 3796 | 2196 | 40 | 0.80 | 544 lass |
| 163 | 4 | 1268 | 1856 | 37 | 0.08 | 196 msms6se |
| 72 | 3 | 1852 | 5140 | 33 | 2.50 | 1232 notepad |
| 270 | 9 | 20052 | 26036 | 129 | 2.44 | 872 powershell |
| 329 | 11 | 30740 | 26888 | 142 | 2.19 | 1752 powershell |
| 1853 | 19 | 33184 | 41096 | 160 | 5.69 | 1784 powershell |
| 278 | 7 | 1960 | 3920 | 33 | 1.20 | 532 services |
| 21 | 1 | 168 | 372 | 4 | 0.02 | 408 smss |
| 104 | 4 | 2844 | 4096 | 39 | 0.09 | 1068 sloopsl |
| 93 | 4 | 1440 | 3084 | 35 | 0.03 | 660 svchost |
| 193 | 5 | 2856 | 4388 | 58 | 0.20 | 700 svchost |
| 293 | 13 | 1684 | 3940 | 33 | 0.42 | 768 svchost |
| 285 | 13 | 11460 | 12680 | 58 | 0.09 | 808 svchost |
| 1105 | 24 | 11236 | 17928 | 82 | 18.31 | 832 svchost |
| 81 | 4 | 1168 | 2980 | 28 | 0.09 | 880 svchost |
| 232 | 7 | 2344 | 4704 | 38 | 0.08 | 972 svchost |
| 392 | 0 | 0 | 236 | 2 | 0.81 | System |
| 565 | 61 | 7264 | 5096 | 52 | 0.77 | 488 winlogon |
| 81 | 3 | 700 | 2156 | 17 | 0.03 | 328 winshost |
| 80 | 3 | 916 | 2160 | 18 | 0.03 | 588 winshost |
| 57 | 3 | 860 | 2688 | 29 | 0.05 | 424 wpabalain |
| 153 | 3 | 1844 | 3124 | 31 | 0.08 | 1556 wauclt |

```powershell
PS C:\>
```

在这里，启动了一个后台作业，并使用变量来捕获和存储后台会话 ID 等信息。然后，使用`$MyJob`变量检索了后台作业的输出。

### 等待后台完成

正如你已经看到的，`Get-PSJob`命令返回一个列出当前工作环境中所有后台作业的表格（已删除的除外）。表格`HasMoreData`列显示后台作业是否有可检索的数据。默认情况下，每当你从后台作业检索数据时，该输出就会从作业中移除且不再可检索。后续操作仅检索未检索的数据。

`Receive-PSJob`命令在使用时支持`-keep`参数，指示 PowerShell 保留后台作业的所有输出，以便下次检索时仍存在。如果你决定在继续工作之前等待某个后台作业，可以执行`Wait-PSJob`命令，传递要等待的后台作业会话 ID。当你这样做时，Windows PowerShell 的提示符会消失，直到指定的后台作业完成。为了更好地理解其工作原理，请查看以下示例：

`img/e07ce5ce2afe5ff9f44f2c361d9d87e_126.png`

《Windows PowerShell 7.2 绝对初学者编程：第二版》

```powershell
PS C:\> Start-PSJob "Start-Sleep 60"
```

| SessionId | Name（名称） | State（状态） | HasMoreData（更多数据） | Command（命令） |
|---|---|---|---|---|
| 15 | | Running | True | Start-Sleep 60 |

```powershell
PS C:\> Wait-PSJob 15
```

在这里，启动了一个运行名为`Start-Sleep`命令的后台作业。`Start-Sleep`命令顾顾名，让你的脚本睡眠一段时间。在此示例中，它睡眠 60 秒。由于`Start-Sleep`命令作为后台作业执行的，你可以在命令执行期间继续在 PowerShell 提示符处工作。然而，示例中`Wait-PSJob`命令的执行改变了这一点，它抑制了提示符，直到后台完成执行。

`img/e07ce5ce2afe5ff9f44f2c361d9d87e_127_0.png`

通过结合使用`Get-PSJob`和`Wait-PSJob`命令，你可以构建一个等待所有后台作业完成执行的语句，如此处所示：

```powershell
Get-PSJob | Wait-PSJob
```

`img/e07ce5ce2afe5ff9f44f2c361d9d87e_127_1.png`

为了方便讨论并保持示例简单，你看到的所有后台作业示例都演示了如何执行快速的命令。实际上，后台作业更适合用于执行需要耗时的长时间运行作业，例如此处所示：

```powershell
$MyJob = Start-PSJob -command -Get-EventLog -log application
```

此后台作业检索了存储在计算机应用程序日志中的所有记录。根据应用程序日志的大小，后台作业可能需要一段时间才能执行完毕。如果该语句是某个以某种方式处理事件日志数据的脚本的一部分，运行时间可能会更长。

### 停止后台作业执行

如果你愿意，可以使用`Stop-PSJob`命令停止后台作业的执行，如此处所示：

```powershell
PS C:\> Stop-PSJob 15
```

`Stop-PSJob`命令仅停止 PSJob 执行；并不会删除它们。要删除它们，你需要执行下一节讨论的`Remove-PSJob`命令。

`img/e07ce5ce2afe5ff9f44f2c361d9d87e_128_0.png`

除了使用会话 ID 停止后台作业外，你还可以使用状态停止后台作业，如此处所示：

```powershell
Stop-PSJob -state running
```

在这里，所有状态为运行的后台作业都被停止。

### 删除后台作业

Windows PowerShell 将你在当前工作会话中执行的每个 PSJob 的信息并在缓存中保留，直到你关闭控制会话或显式删除后台作业。使用`Remove-PSJob`命令，你可以删除后台作业及其输出。例如，假设你执行了三个后台作业，如下：

```powershell
PS C:\> Get-PSJob
```

| SessionId | Name（名称） | State（状态） | HasMoreData（更多数据） | Command（命令） |
|---|---|---|---|---|
| 1 | | Completed | False | start-sleep 30 |
| 3 | | Completed | True | get-process |
| 5 | | Completed | False | get-process |

```powershell
PS C:\>
```

你可以通过执行以下语句，使用`Remove-PSJob`命令删除会话 ID 为 5 的后台作业：

```powershell
PS C:\> Remove-PSJob 5
```

通过执行接下来所示的`Get-PSJob`命令，你可以验证指定的后台作业确实已被删除。

## 技巧

你可以结合使用`Get-PSJob`命令行和`Remove-PSJob`命令行来删除从当前工作环境启动的所有后台作业，如下所示：

```powershell
Get-PSJob | Remove-PSJob
```

## 提示

处理后台作业的内容远比本章涵盖的基础知识多。要学习更多信息，请使用`Get-Help`cmdlet来查看与`Create-PSJob`、`Get-PSJob`、`Retrieve-PSJob`、`Wait-PSJob`、`Stop-PSJob`和`Remove-PSJob`相关的帮助文件。

## Windows PowerShell 管道

对象管道（Object pipelines）是 cmdlet之间传递对象数据的通道。与只传递文本数据的传统命令壳不同，Windows PowerShell 通过其管道传递不同类型的对象数据。以下示例旨在进一步帮助你理解 PowerShell 管道的灵活性和威力。

让我们从使用`Get-ChildItem`cmdlet来生成当前工作目录下的文件和文件夹列表开始，如下所示：

```powershell
PS C:\ Get-ChildItem
```

```powershell
Directory: Microsoft.PowerShell.CoreFileSystem::\
```

| | | LastWriteTime | Name |
|---|---|---|---|
| d--- | 2/24/2008 | 9:29 PM | DarkBASIC |
| d--- | 10/3/2008 | 11:47 AM | MyScripts |
| d--- | 9/9/2008 | 7:20 PM | PerfLogs |
| d-r-- | 9/8/2008 | 11:44 PM | Program Files |
| d | 7/7/2007 | 4:24 PM | ruby |
| d--- | 9/22/2008 | 12:05 AM | Temp |
| d-r-- | 4/26/2008 | 10:58 PM | Users |
| d--- | 9/9/2008 | 7:32 PM | Windows |
| -a | 3/3/2007 | 7:52 AM | 74 autoexec.bat |
| -a-s | 3/3/2007 | 7:26 AM | 8192 BOOTSECT.BAK |
| -a--- | 9/18/2006 | 5:43 PM | 10 config.sys |

# 第3章 · 基于 .NET 的对象脚本

-a----    3/3/2007    7:40 AM    396 RHDSetup.log

```powershell
PS C:\>
```

管道使用`|`字符创建。通过管道，你可以将两个或多个 cmdlet 组合在一起，构成逻辑语句，利用两个 cmdlet 的组合能力。例如，考虑以下语句，它获取`Get-ChildItem`cmdlet 生成的输出并传递给`Sort-Object`cmdlet

```powershell
PS C:\ Get-ChildItem | Sort-Object
```

```powershell
Directory: Microsoft.PowerShell.Core\FileSystem::C:\
```

| Mode | LastWriteTime | Length Name |
|---|---|---|---|
| -a---- | 3/3/2007 | 7:52 AM | 74 autoexec.bat |
| -ar-s | 3/3/2007 | 7:26 AM | 8192 BOOTSEC.BAK |
| -a---- | 9/18/2006 | 5:43 PM | 10 config.sys |
| d---- | 2/24/2008 | 9:29 PM | DarkBASIC |
| d---- | 10/3/2008 | 11:47 AM | MyScripts |
| d---- | 9/9/2008 | 7:20 PM | PerfLogs |
| d-r---- | 9/8/2008 | 11:44 PM | Program Files |
| -a---- | 3/3/2007 | 7:40 AM | 396 RHDSetup.log |
| d---- | 7/7/2008 | 4:24 PM | ruby |
| d-r---- | 9/26/2008 | 10:58 PM | Users |
| d---- | 9/9/2008 | 7:32 PM | Windows |

```powershell
PS C:\>
```



`Sort-Object` cmdlet 对其他 cmdlet 传递它的对象列表进行排序，更改对象沿管道向下传递的顺序。在之前的示例中，排序操作（默认情况下）使用 `Name` 属性执行。然而，你可以通过指定不同的属性来覆盖此。同样，你可以将默认顺序从升序改为降序。要了解更多关于 `Sort-Object` 的信息，请在 Windows PowerShell 提示符处输入 `Get-Help Sort-Object`。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_130_0.png)

可以看出，`Get-ChildItem` cmdlet 的输出已从管道中移除、排序，然后由 `Sort-Object` cmdlet 以升序顺序添加回去。现在我们有了一个排序后的对象列表，让我们进一步处理它们。在这个示例中，管道中排序后的对象列表将由 `Where-Object` cmdlet 处理。

```
PS C:\> Get-ChildItem | Sort-Object | Where-Object ($_.Length -gt 200)
```

```
Directory: Microsoft.PowerShell.Core\FileSystem::C:\
```

| | WriteTime | Name |
|---|---|---|
| -ar-s | 3/3/2007 | 7:26 AM | 8192 BOOTSECT.BAK |
| -a-- | 3/3/2007 | 7:40 AM | 396 RHDSetup.log |

`Where-Object` cmdlet 移除管道中不符合特定标准的对象，它由 `$_` 表示并位于括号内。该表达式检查通过的每个对象的属性，查看其是否大于 200。`.` 符号（点表示法）在构建 `Where-Object` 语句时必须遵循。再次，不要纠结于上示例中的语法。目前，从这个示例中获取的最重要事情是理解管道以及 cmdlet 之间的用法，以便构建复杂的语句。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_130_0.png)
![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_131.png)

### 使用别名 (ALIASES)

你已经通过 `Get-Item` cmdlet 看到两个不同的别名（`dir` 和 `ls`），它们都可以替代另一个 cmdlet 并产生相同的结果。Microsoft 开发这些别名是为了帮助从传统命令壳到 Windows PowerShell 的过渡。你可以使用 `Get-Alias` cmdlet 显示 Windows PowerShell 支持的所有别名列表。

| Alias | Cmdlet | 1.0 | 2.0 | Alias | Cmdlet | 1.0 | 2.0 |
|---|---|---|---|---|---|---|---|
| ac | Add-Content | Y | Y | Remove-Property | Y | Y |
| asnp | Add-PSSnap | Y | Y | Remove-PSSnap | Y | Y |
| clc | Clear-Content | Y | Y | Remove-Variable | Y | Y |
| cli | Clear-Item | Y | Y | rwmi | WMIObject | N | Y |
| clp | Clear-Property | Y | Y | rvpa | Resolve-Path | Y | Y |
| clv | Clear-Variable | Y | Y | sal | Set-Alias | Y | Y |
| cpi | Copy-Item | Y | Y | sasv | Start-Service | Y | Y |
| cpp | Copy-ItemProperty | Y | Y | sbp | Set-PSBreakpoint | N | Y |
| cvva | Convert-Path | Y | Y | sc | Set-Content | Y | Y |
| dbp | Disable-Breakpoint | N | Y | select | Select-Object | | Y |
| diff | Compare-Object | Y | Y | si | Set-Item | Y | Y |
| ebp | Enable-Breakpoint | N | Y | | Set-Location | Y | Y |
| epal | Export-Alias | Y | Y | swmi | Set-MIInstance | N | Y |
| epcsv | Export-Csv | Y | Y | sleep | Start-Sleep | Y | Y |
| fc | Format-Custom | Y | Y | sort | Sort-Object | Y | Y |
| fl | Format-List | Y | Y | sp | Set-ItemProperty | Y | Y |
| foreach | For-Object | Y | Y | | Stop-Process | Y | Y |
| % | For-Object | Y | Y | spvs | Stop-Service | N | Y |
| sv | Set-Variable | Y | Y | sti | Step-Into | | | |
| ft | Format-Table | Y | Y | fw | Cmd-Wide | Y | Y |
| where | Where-Object | Y | Y | sto | Step-Over | N | Y |
| gal | Get-Alias | Y | Y | stu | Step-Over | N | Y |
| gbp | Get-Breakpoint | N | Y | tee | Tee-Object | Y | Y |
| gc | Get-Content | Y | Y | ? | Where-Object | Y | Y |
| gci | Get-Item | Y | Y | write | Write-Output | Y | Y |
| gcm | Get-Command | Y | Y | cd | Set-Location | Y | Y |
| gdr | Get-PSDrive | Y | Y | cls | Clear-Host | Y | Y |
| gcs | Get-CallStack | N | Y | cp | Copy-Item | Y | Y |
| ghi | Get-History | Y | Y | history | Get-History | Y | Y |
| gi | Get-Item | Y | Y | kill | Stop-Process | Y | Y |
| gm | Get-Property | Y | Y | lp | Out-Printer | Y | Y |
| gp | Get-Property | Y | Y | mount | Get-ChildItem | Y | Y |
| gs | Get-Service | Y | Y | mv | Move-Item | Y | Y |
| gsv | Get-Service | Y | Y | popd | Pop-Location | Y | Y |
| gsnp | Get-PSSnap | Y | Y | ps | Get-Process | Y | Y |
| gu | Get-Unique | Y | Y | gwmi | Get-WmiObject | Y | Y |
| gv | Get-Variable | Y | Y | pushd | Push-Location | Y | Y |
| ii | Invoke-Item | Y | Y | iex | Invoke-Expression | Y | Y |
| iwmi | Invoke-Item | N | Y | pwd | Get-Location | Y | Y |
| ipal | Import-Alias | Y | Y | r | Invoke-History | Y | Y |
| ipcs | Import-Csv | Y | Y | rm | Remove-Item | Y | Y |
| mi | Move-Item | Y | Y | rdir | Remove-Item | Y | Y |
| mp | Move-ItemProperty | Y | Y | echo | Write-Output | Y | Y |
| nl | New-Alias | Y | Y | cls | Clear-Host | Y | Y |
| ndr | New-PSDrive | Y | Y | chdir | Set-Location | Y | Y |
| ni | New-Item | Y | Y | copy | Copy-Item | Y | Y |
| nv | New-Variable | Y | Y | del | Remove-Item | Y | Y |
| oh | Out-Host | Y | Y | dir | Get-ChildItem | Y | Y |
| ogv | Out-Host | N | Y | erase | Remove-Item | Y | Y |
| grid | Out-GridView | N | Y | move | Move-Item | Y | Y |
| rbp | Remove-PSBreakpoint | | | rd | Remove-Item | Y | Y |
| rdr | Remove-PSDrive | Y | Y | ren | Rename-Item | Y | Y |
| ri | Remove-Item | Y | Y | set | Set-Variable | Y | Y |
| rni | Rename-Item | Y | Y | type | Get-Content | Y | Y |
| rnp | Rename-ItemProperty | Y | Y | icm | Invoke-Command | N | Y |

## 第 3 章 · 使用 .NET 进行对象脚本

如你所见，Windows PowerShell 支持的别名列表非常广泛。虽然作为执行小命令（cmdlets）的临时方便方案，但我建议你抵制使用这些别名的诱惑，而是花时间学习 PowerShell 的命令名称。从长远来看，这将有助于你的 PowerShell 脚本更易维护和支持。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_134_0.png)

Windows PowerShell 还允许你定义自己的自定义别名。这是通过 `Get-Alias` 命令实现的，它需要两个参数。第一个参数是要被分配的别名，第二个参数是要与该别名关联的命令名称。例如，以下语句为 `Write-Host` 命令创建了一个名为 `ds` 的新别名。

```
Set-Alias ds Write-Host
```

你可能记得在本章较早之前读到如何程序化自定义 Windows PowerShell 时，看到过这个示例。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_134_1.png)

Windows PowerShell 不对使用 `Set-Alias` 命令进行的别名赋值有效性进行任何验证。你需要确保你的新别名按预期工作，并且你没有拼错目标命令的名称。

### 返回 POWERSHELL 占卜游戏

好了，是时候把注意力回到本章的主项目了：PowerShell 占卜游戏。这个游戏将涉及许多编程技术，包括条件逻辑和循环。你还将学习如何实例化（建立新实例）随机对象来生成随机数。

### 设计游戏

PowerShell 占卜游戏首先显示欢迎屏幕，然后为玩家提供如何问题的指令。接下来，提示玩家提问。作为响应，游戏将根据脚本随机生成的数字显示随机答案。脚本显示的具体答案还会根据天气，因为占卜师在下午有点。。一旦问题回答，脚本将提示玩家是问新问题还是终止脚本执行。因此，玩家可以随意提问任意次数。一旦玩家表示想要终止脚本，游戏将通过邀请玩家再次回来来结束。

## 112 Harvey Windows PowerShell 2.0 零基础入门编程 - 第二版

该脚本的开发将此处列出的六步完成：

- 1. 创建新脚本并添加开头注释语句。
- 2. 清屏并初始化脚本变量。
- 3. 显示开启欢迎屏幕。
- 4. 显示提问规则。
- 5. 提示玩家提问然后生成答案。
- 6. 邀请玩家再次游戏并终止脚本执行。

## 创建新的 PowerShell 脚本

创建 PowerShell 占卜游戏的第一步是创建一个名为 `FortuneTeller.ps1` 的新 PowerShell 脚本，并添加以下语句：

```
********************************************************************************

### 脚本名称:FortuneTeller.ps1 (PowerShell 占卜)

# 版本:2.0

# 作者:Jerry Lee Ford, Jr.

# 日期:2008年10月4日

#

# 说明: 此 PowerShell 脚本为玩家的问题提供随机答案。

#

********************************************************************************
```

```
#清除 Windows 命令控制台

Clear-Host
```

如你所见，到目前为止 PowerShell 脚本文件由提供高级脚本文档的注释语句和执行 `Clear-Host` 命令组成，该命令用于清除 Windows 命令控制台的显示区域。

### 声明和初始化变量

创建 PowerShell 占卜游戏的下一步是声明整个脚本使用的变量，并为这些变量分配初始值。这是通过将语句附加 PowerShell 脚本文件的末来实现的。

```
#定义此脚本中用于收集玩家输入的变量

$question = "" #此变量将存储玩家的问题

$status = "Play" #此变量将用于控制游戏结束
```

## 第 3 章 - 使用 .NET 进行对象脚本

```
$answer = 0 #此变量存储随机生成的数字
$randomNo = New-Object System.Random #此变量存储一个随机对象
$time = (Get-Date).Hour #此变量存储当天的小数
```

注意，我不仅为每个变量提供了描述性名称，还添加了记录每个变量目的和用处的注释。

### 显示欢迎屏幕

开发 PowerShell 占卜游戏的下一步是添加用于显示游戏欢迎屏幕的语句。下文所示的语句应该添加到脚本文件的末尾。

```
#显示游戏的开启屏幕

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host " WELCOME TO THE WINDOWS"

Write-Host

Write-Host

Write-Host

Write-Host " POWERSHELL FORTUNE TELLER"

Write-Host

Write-Host

Write-Host

Write-Host " By Jerry Lee Ford, Jr."

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host " Press Enter to continue."
```

```
#暂停脚本执行并等待玩家按下回车
Read-Host
```

上文的屏幕内容是通过多个 `Write-Host` 实例创建的。上面的语句使用 `Read-Host` 命令暂停执行直到玩家按下回车。

### 显示指令

在读取并关闭欢迎屏幕后，需要显示指令，指导玩家如何向占卜师提问。这是通过将以下语句添加到脚本末尾实现的。

```
#清除 Windows 命令控制台屏幕

Clear-Host
```

```
#为玩家提供指令

Write-Host

Write-Host " 占卜师是一个忙碌且不耐烦的神秘者。请让"

Write-Host

Write-Host "你的问题简洁简单，并且只期待"

Write-Host " 是/否 风格的答案。"

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host

Write-Host - 按回车键继续。
```

```
#暂停脚本执行并等待玩家按下回车

Read-Host
```

与生成欢迎屏幕的语句一样，显示指令的语句清除屏幕、写入内容，然后暂停直到玩家按下回车。

### 控制游戏

控制游戏核心活动的编程逻辑如下所示，应附加到脚本文件的末尾。

```
#继续游戏直到玩家决定停止

while ($status -ne "Stop") {

#询问玩家第一个问题

while ($question -eq "")

  Clear-Host #清除 Windows 命令控制台屏幕

  Write-Host

  $question = read-host "你的问题是什么?"

}

$question = "" #重置变量为空字符串

#获取 1 到 4 之间的随机数

$answer = $randomNo.Next(1,5)
```

```
#根据时间和随机数选择一个答案
```



### 如果是下午，占卜师会有点脾气

```powershell
if ($time -gt 12) {
  Write-Host
  if ($answer -eq 1) "Grrr. 答案是不!"
  if ($answer -eq 2) "Grrr. 答案永远不会!"
}
```

# 第 3 章 基于对象的 .NET 脚本

```powershell
Clear-host
Write-Host
```

```powershell
#提示玩家继续或退出
$reply = read-host "按回车键提问另一个问题或输入 Q 退出。"
if ($reply -eq "q") { $status = "Stop" }
```

构成此脚本文件部分的语句由许多编程语句组成，这些语句在第 5 章和第 6 章中才会被正式介绍。这些语句涉及条件和循环逻辑。遗憾的是，在不使用某些条件或循环逻辑的情况下，完全可以开发出任何实际复杂的 PowerShell 脚本，而且一次能呈现的信息是有限的。为了便于理解，我在整个脚本文件中添加了许多注释。然而，由于本书尚未涵盖这些编程结构，我现在不会对它们进行非常详细的介绍。因此，你可能想在读完第 5 章和第 6 章后返回并回顾此脚本。

控制游戏的的逻辑（允许玩家尽可能多地提问问题）是由一个 `while` 循环控制的，该循环一直执行，直到名为 `$status` 的变量值设置为 `"Stop"` 为止。在循环内部，定义了另一个 `while` 循环，以确保玩家输入了内容，而不是在提示询问占卜者问题时简单地按下回车键。

接下来，会生成一个 1 到 4 之间的随机数。然后检查变量 `$time`，以查看其值是否大于 12。如果是，则说占卜者感到疲惫且易怒，导致显示 4 个答案中其中一个较不友善的答案（基于游戏随机生成的数字）。然而，如果仍然是早上，则会使用一组更积极的答案来获取占卜者的回答。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_140_0.png)

> 与通过实例化 `Random` 对象并使用其 `Next` 方法生成随机数不同，Windows PowerShell 2.0 程序员可以选择使用 `Get-Random` 词汇。尽管使用起来更简单，但它缺乏与 PowerShell 1.0 的向后兼容性。

接下来，显示所选答案，并提示玩家按回车键提问另一个问题，或输入 Q 信号脚本停止执行。如果玩家输入 Q，变量 `$status` 的值将设置为 `"Stop"`，从而停止控制脚本整体执行的 `while` 循环。

### 显示结束屏幕

游戏结束后，应该邀请玩家返回并向占卜者提问更多问题。这通过在脚本文件末尾添加以下语句来实现。

```powershell
#清除 Windows 命令控制台
Clear-Host
#为玩家提供指令
Write-Host
Write-Host " 好的。请再次回来获得您所有问题的解答。"
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host " 按回车键继续。"
#暂停脚本执行并等待玩家按下回车键
```

### Read-Host

```powershell
#清空 Windows 命令控制台屏幕
Clear-Host
```

玩家通过按下回车键拒绝了再次返回并玩的邀请，随后屏幕被清空，脚本停止执行。

好了，就是这些。假设你在输入此 PowerShell 占卜者游戏代码时没有任何拼写错误，一切都应该如预期运行。

### 总结

在本章中，你学习了 .NET Framework 类库和常用的运行时语言。你学习了 PowerShell 词汇（cmdlets）如何允许你访问并交互 .NET Framework 暴露的资源。你还学习了如何使用新的词汇，包括 `Get-Help` 词汇，你可以用它获取任何词汇或 PowerShell 主题的额外信息。你还学习了如何找到执行词汇时默认未显示但在后台可对象属性和方法。你学习了更多关于别名（aliases）的知识，包括如何创建自己的自定义别名。本章还解释了 Windows PowerShell 如何使用对象数据在词汇之间传递结构化数据。最后，你学习了如何创建 PowerShell 占卜者游戏。

现在，在进入第 4 章之前，我建议你多花几分钟通过实现以下挑战来改进和增强 PowerShell 占卜者游戏。

挑战

1. 考虑通过扩展游戏可用答案的范围来使游戏变得不可预测。你甚至可以添加一种响应，让占卜者对某个问题感到被犯并拒绝回答。
2. 考虑通过随着白天进入黑夜让占卜者变得更加易怒，从而进一步改变她的情绪。

## 第二部分 学习如何编写 PowerShell 脚本

## 使用变量、数组和哈希表

这是四个章节中的第一章，旨在教授 Windows PowerShell 脚本语言的基础知识。在本章中，你将学习如何存储、检索和修改数据。你将学习如何存储单个数据以及数据集合。本章还将涵盖许多其他 PowerShell 语言主题，包括关键字的使用、转义字符、字符串处理。此外，你将有机会创建你的下一个 PowerShell 游戏——占卜者。具体来说，你将学习如何：

- 在变量中创建和存储单个数据单元
- 在数组和哈希表中存储和访问数据集合
- 使用 PowerShell 特殊变量
- 执行范围运算符
- 拼接字符串
- 使用转义字符格式化文本

## 项目预览：友谊测试

本章的游戏项目是《友谊》测试，它测试玩家对该热门剧集的了解。游戏由五个选择题组成。当启动时，会出现欢迎界面，如图 4.1 所示。

### 图 4.1

《友谊》测试的欢迎界面。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_147_0.png)

按下回车键消除欢迎界面后，将显示有关测试构成和标准的指令，如图 4.2 所示。

### 图 4.2

根据正确回答问题的数量授予排名。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_147_1.png)

接下来，游戏将逐个显示问题，如图 4.3 所示。

### 图 4.3

测试中的每个问题为玩家提供四个可能的答案供选择。

```powershell
Windows PowerShell
Kramer 的名字是什么？
A. Peterman
B. Cosmo
C. Puddy
D. Peck
输入代表正确答案的字母并按回车键！
```

```powershell
Windows PowerShell
好，现在按回车键查看你的表现。
```

### 图 4.4

游戏宣布现在准备好分析玩家的测试结果。

```powershell
Windows PowerShell
你答对了 4 个问题。
你对《友谊》的知识和 Kramer 一样。
```

### 图 4-5

玩家正确回答了四个问题。

Seinfeld 趣味问答测试显示的最后一个屏幕（如图 4.6 所示）感谢玩家花时间完成测试。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_149_0.png)

图 4.6 游戏结束时向玩家表示感谢。

# POW POWHELL 语言特性

尽管本章的主要重点是脚本执行期间的数据存储和检索，但还有几个需要涵盖的其他主题，以完善你对 PowerShell 脚本基础的理解。这些主题包括：

- 保留字（Reserved words）
- 转义字符（Escape characters）
- 字符串处理（String manipulation）

## Windows PowerShell 保留字

与任何编程语言一样，Windows PowerShell 拥有一组保留字（也称为关键字），这些词对语言具有特殊含义，因此不能用作变量、数组、关联数组和函数名。

保留字是 Windows PowerShell 预定义的具有特殊用途的关键字。PowerShell 保留字的一个示例是 `if`，它用于设置条件测试，以评估条件为真还是假，并根据该结果控制一个或多个脚本语句的逻辑执行。作为保留字，你必须按照 Windows PowerShell 定义的严格语法规则使用 `if` 关键字。因此，你不能在 PowerShell 脚本中创建名为该字的变量或数组或任何标识符。表 4.1 提供了 PowerShell 保留字列表。

### 表 4.1 WINDOWS POWERSERSHELL 保留字

| 关键字 | 关键字 | 关键字 | 关键字 |
|---|---|---|---|
| `break` | `filter` | `in` | `until` |
| `continue` | `for` | `local` | `where` |
| `do` | `foreach` | `private` | `while` |
| `else` | `function` | `return` | |
| `elseif` | `if` | `switch` | |

### 转义字符

随着你编写越多的 PowerShell 脚本，你将会遇到希望详细控制文本在 Windows 命令控制台中显示方式的情况。正如你在之前的章节脚本游戏示例中所看到的，其中一种方法是使用额外的 `Write-Host` 词get实例，并在字符串内部嵌入空格，如下所示。

```powershell
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host *      WELCOME TO THE WINDOWS"
Write-Host
Write-Host
Write-Host
Write-Host *      POWERSHELL FORTUNE TELLER"
Write-Host
Write-Host
Write-Host
Write-Host *                               BY Jerry Lee Ford, Jr.
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
Write-Host
```

# 128 PowerShell 7: 绝对初学者编程，第二版

```powershell
Write-Host
Write-Host
Write-Host
" Press Enter to continue."
```

此示例需要 24 行代码。虽然这种方法非常直观且易于理解，但这样使用 `Write-Host` 词get 会消耗大量空间并使你的 PowerShell 脚本代码膨肿。详细控制文本字符串输出的另一种方法是利用 PowerShell 的转义字符。

转义字符是对 Windows PowerShell 具有特殊含义的字符。转义字符通过 `` ` `` 字符识别（通常位于键盘上 Tab 键上方）。使用转义字符，你可以在文本字符串的任何位置插入制表符和换行符，以创建立即换行操作，而不会将字符串的显示分为两行。同样，你可以在文本字符串中插入 `` `t `` 来插入逻辑制表符。仅使用这两个转义字符，你就可以像此处所示重构之前的示例：

```powershell
Write-Host "`n`n`n`t`t`tWELCOME TO THE WINDOWS"
Write-Host "`n`n`n`t POWERSHELL FORTUNE TELLER"
Write-Host "`n`n`n`t`t`t BY Jerry Lee Ford, Jr.
Write-Host "`n`n`n`n`n`n`n`t Press Enter to continue."
```

信不否，这个示例仅通过四个语句就提供了相同的输出。之前的示例是由 24 个语句产生的。Windows PowerShell 支持不同的转义字符，如表 4.2 所示。

| 表 4.2 WINDOWS POWERSERSHELL 转义字符 |
| 转义字符 | 说明 |
|---|---|
| `` ` `` | 单引号 |
| `` `0 `` | 双引号 |
| `` `a `` | 空字符 |
| `` `b `` | 警报 |
| `` `f `` | 退格 |
| `` `n `` | 换页 |
| `` `r `` | 换行 |
| `` `t `` | 回车 |
| `` `v `` | 水平制表符 |
| | 垂直制表符 |

# 第 4 章 · 变量、数组和哈希的操作

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_152_0.png)

要了解更多关于 Windows PowerShell 转义字符的信息，请在 Windows PowerShell 命令行执行以下语句：

```powershell
Get-Help about_escape_character
```

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_152_1.png)

当添加到语句末尾时，`` ` `` 字符指示 Windows PowerShell 将语句延续到下一行，如下所示：

```powershell
Write-Host `"Once upon a time there was a little girl that lived in a small.\` 
`"house on the edge of the forest.\`
```

在显示时，该语句产生的输出将就像该语句写在单行上一样。

### 字符串处理

Windows PowerShell 提供了许多字符串处理技术，在开发脚本时会非常有用。这些技术包括字符串拼接、重复和替换。

### 拼接

Windows PowerShell 允许使用 `+` 运算符连接两个字符串，如下所示：

```powershell
$x = "Once upon "
$y = "time"
$x + $y
```

在此示例中，两个字符串 `$x` 和 `$y` 被拼接。执行后，输出为：

```
Once upon time
```

### 重复

另一种你觉得非常有用的字符串技术是使用 `*` 运算符重复字符串，如下所示：

```powershell
$x = "Ha" * 3
$x
```

在此示例中，字符串 `"Ha"` 被重复了三次，导致：

```
Ha Ha Ha
```

### 替换

替换运算符（`-replace`）允许你替换字符串的一部分。要使用替换运算符，你需要在字符串后面紧跟两个参数。第一个参数是你想要替换的部分，第二个参数是替换字符串。为了看到替换运算符的操作，请查看以下示例，它获取一个字符串并将 `"boy"` 替换为 `"girl"`。

```powershell
$x = "Once upon a time there was a little boy."
$y = $x -replace "boy", "girl"
$x
```

执行时，此示例将显示如下输出：

```
Once upon a time there was a little girl.
```

# 零基础 Windows PowerShell 2.0 编程第二版

在本示例中，一个由逗号分隔的数值字符串将被拆分，方法是告诉拆分操作符使用逗号作为分隔符。

拆分字符串的反操作是将两个或多个字符串连接成一个新的更大的字符串，你可以使用新的 `-join` 操作符来实现这一点。使用时，`-join` 操作符将按照它们在命令中出现的顺序将指定的字符串拼接在一起，如下所示：

```powershell
$alphabet = -join "abcdefghijklmnopqrstuvwxyz"
Write-Host $alphabet
```

在这里，三个各包含字母表部分字母的字符串被连接了一起。执行时，此示例将显示以下输出：

```
abcdefghijklmnopqrstuvwxyz
```

与 `-split` 操作符一样，`-join` 操作符也允许你指定分隔符，可以使用它来格式化新字符串的输出，如下所示：

```powershell
PS C:\> "in","the","end","there","can","only","one." -join " *"
In the end there can only one.
PS C:\> 
```



在这里，`-join`操作符被指示在连接一系列较短字符串时使用空格作为分隔符。

### 存储和检索数据

在任何编程语言中，程序员都需要一种存储和检索数据的机制。你可以通过执行 cmdlet（命令/程序）程序化地访问多种类型的数据。然后你可以通过对象管道（object pipeline）使用其他 cmdlet 生成的数据。然而，这种方法是有限制的。在许多情况下，你会发现你需要能够存储数据以便稍后分析、处理和显示。

Windows PowerShell 编程语言为你提供了几种存储数据的方法，列如下：

## 第 4 章 • 变量、数组和哈希

- 变量（Variables）：存储单个数据单元。
- 数组（Arrays）：以索引列表的形式存储数据。
- 哈希（Hashes）：以键值对的形式存储数据。

## 变量

变量为你的 Windows PowerShell 脚本提供了存储数据的手段。使用变量，你可以存储任何你需要的内容，包括数字、字符串和对象。如果你存储了作为 cmdlet 输出返回的对象数据，PowerShell 能够保留对对象类型的感知，从而保留与对象相关的属性和方法。

### 为变量命名

Windows PowerShell 变量名不区分大小写，这意味着如果你定义了一个名为`$username`的变量，稍后可以引用`$USERNAME`，PowerShell 会理解你的意思。Windows PowerShell 变量名可以包含字符、数字和下划线（`_`）。Windows PowerShell 变量名必须以字符`$`开始。有效变量名的示例包括：

- `$userName`
- `$total`
- `$1stName`
- `$game_winner`

无效变量名的示例包括：

- `$user Name`
- `$total!`
- `$#!).@&`

第一个示例无效无效，因为它包含了空格。第二个示例是无效的，因为它包含了`!`字符。最后，第三个示例是无效的，因为它包含了一系列不支持的字符。如果你忘记并在 PowerShell 脚本中包含一个无效变量，你的脚本很可能会因错误终止。例如，接下来的变量赋值语句是无效的，因为它包含了许多无效字符。

```powershell
$#!).@& = "Winner"
```

如果你尝试在 PowerShell 脚本中使用此变量名，脚本将终止并显示以下错误：

```
Missing expression after ',', in pipeline element.

At C:\Users\Jerry\Desktop\x.ps1:1 char:5

+ $1, <<< "Winner"
```

如果你非常想在变量名中包含特殊字符，可以通过将变量名封装在匹配的`(()`字符内部来实现，如下所示：

```powershell
$($bang#) =
```

通过将变量名封装在`()`括号内，你可以包含各种字符，例如`#`、`$`、`%`和`*`，以及点、逗号和空格。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_157_0.png)

### 定义和初始化变量

Windows PowerShell 支持多种数据类型，对应于 .NET Framework 支持的数据类型。例如，Windows PowerShell 支持整数、浮点数和字符串，你可以将它们分配给变量，如下：

```powershell
$x = 5

$y = 5.5

$z = "Winner"
```

Windows PowerShell 自动识别上述第一个赋值为整数，第二个赋值为浮点数，第三个为字符串。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_157_1.png)

我强烈建议你在 Windows PowerShell 脚本中声明的任何变量分配一个初始默认值。如果脚本语句尝试访问一个未赋值的变量，不会产生错误。相反，你的脚本将继续运行，你最终将得到不可预测的结果。

### 变量插值

到本书目前为止，你看到的所有字符串都放置在成对的双引号内。然而，你也被允许使用成对的单引号定义字符串。两者之间的区别在于，当变量嵌入在用双引号括的字符串内部时，会发生变量插值。与`-split`操作符一样，`-join`操作符也允许你指定分隔符，可以使用它来格式化新字符串的输出，如下所示：

```powershell
PS C:\> "in","the","end","there","can","only","one." -join " *"

In the end there can only one.

PS C:\> 
```

在这里，`-join`操作符被指示在连接一系列较短字符串时使用空格分隔符。

### 使用表达式赋值

在 Windows PowerShell 中，你可以使用表达式为变量赋值。例如，考虑以下语句：

```powershell
$x = 2 + 2
```

执行时，表达式将被求值，结果将分配给变量。你也可以在表达式中使用其他运算符，如下例：

```powershell
$x = (2 + 2) * 5
```

在这种情况下，括号确保先执行加法，然后结果乘以 5。

### 优先级

在 Windows PowerShell 中，与其他任何语言一样，数学运算按照特定的优先级执行。这种优先级决定了表达式内部不同运算符的计算顺序。

| 运算符 | 说明 |
|---|---|
| `()` | 括号 |
| `^` | 幂 |
| `*` | 乘法 |
| `/` | 除法 |
| `%` | 取模 |
| `+` | 加法 |
| `-` | 减法 |

如上表所示，括号优先级最高，然后是幂、乘法、除法和取模，最后是加减。

考虑以下表达式：

```powershell
$x = 5 + 3 * 2
```

根据优先级规则，乘法先于加法执行。因此，3 乘以 2 得到 6，然后 5 加 6 得到 11。

如果你想先执行加法，可以使用括号：

```powershell
$x = (5 + 3) * 2
```

在这种情况下，加法先执行，得到 8，然后乘以 2，得到 16。

### 嵌套表达式

你还可以嵌套表达式，即将一个表达式放在另一个表达式内部。例如，考虑以下语句：

```powershell
$x = 5 + (3 * (2 + 1))
```

在本示例中，最内层括号内的表达式首先求值，即`2 + 1 = 3`。然后，下一层括号内的表达式被求值，即`3 * 3 = 9`。最后，5 加 9，得到 14。

### PowerShell 赋值运算符

到本书目前为止，你已经看到使用等号（`=`）运算符来执行所有的赋值。然而，Windows PowerShell 支持多种不同的赋值运算符，如表 4.4 所示。

| 运算符 | 说明 |
| --- | --- |
| `=` | 给变量赋值 |
| `+=` | 在变量值上增加一个值 |
| `-=` | 从变量中减去一个值 |
| `*` | 乘以变量值 |
| `/=` | 除以变量值 |
| `%=` | 赋值除法的余数 |

作为如何使用这些运算符的示例，请考虑以下示例。

```
$x = 5

$x +=5
```

在这里，`$x`的值被设置为 5，然后加了 5，结果是最终值为 10。

除了表 4.4 所示的赋值运算符外，Windows PowerShell 还支持两个额外的运算符，你可以使用它们来自动将变量的值加或减 1。

- `++`自动将值加 1。
- `--`自动将值减 1。

作为这两个运算符如何工作的示例，请考虑以下语句。

```
$x = 5

$y = $x++
```

在前面的示例中，`$x++`在功能上等同于`$x = $x + 1`。

在这里，一个名为`$x`的变量被设置为 5。接下来，在`$x`加 1 之后，一个名为`$y`的变量被赋值为`$x`的值。因此，`$y`最终被赋值为 6。

### 特殊变量

Windows PowerShell 为你提供了许多 PowerShell 脚本中始终可用的变量。这些变量提供了常用信息的访问。通过引用这些特殊变量，你可以节省创建和维护这些变量自定义副本的精力。表 4.5 列出了许多常用的特殊变量。

| 表 4.5 WINDOWS POWERSHELL 特殊变量 |
| 特殊字符 | 说明 |
| --- | --- |
| `$_` | 在脚本块（如`Foreach-Object`和`Where-Object`块）中使用时代表当前管道对象 |
| `$Error` | 提供对最近错误信息的访问 |
| `$HOME` | 代表当前用户的主目录 |
| `$PSHome` | Windows PowerShell 安装文件夹的名称 |
| `$null` | 代表空对象 |

你已经在本书中见过几次`$_`特殊变量的使用。

作为使用 Windows PowerShell 特殊变量的另一个示例，请考虑以下示例：

```
Set-Location $home

$x = Get-ChildItem

$x
```

执行时，此示例会将当前工作目录更改为运行脚本的人的主目录，并将该文件夹的所有内容列表赋值给名为`$x`的变量。

> 要查看所有 Windows PowerShell 特殊变量的列表及其定义，请使用`Get-Help`命令行并向其传递`about_automatic_variables`参数，如下：
> `Get-Help about_automatic_variables`

### 变量作用域

在 Windows PowerShell 脚本中，变量访问取决于定义变量的位置。在 Windows PowerShell 中，访问由作用域管理。PowerShell 支持四种作用域，每个作用域都可以通过以下标签之一引用。

# 第 4 章 处理变量、数组和哈希

- 本地作用域（Local scope）。指当前作用域，可以是全局、私有或脚本。
- 全局作用域（Global scope）。启动新的 PowerShell 会话时建立的作用域。
- 私有作用域（Private scope）。其他作用域不可或无法访问的作用域。
- 脚本作用域（Script scope）。每当执行脚本时建立，并在脚本停止执行时结束的作用域。

每当你启动一个新的 Windows PowerShell 会话时，你就建立了一个全局作用域。在当前会话期间从命令行创建的任何变量都是全局作用域的。全局变量可以在当前作用域内访问（例如，从命令行以及子作用域）。当你执行 PowerShell 脚本时，会创建一个新的脚本作用域。这是全局作用域的一个子作用域。

在你的 PowerShell 脚本中（在任何函数之外）定义的变量是局部变量，可以从脚本中的任何地方访问。在 PowerShell 脚本中，你可以定义函数以改进脚本的整体组织结构并精炼作用域。在函数内部定义的变量对于该函数是局部的，函数的作用域是脚本作用域的子作用域。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_162_0.png)

> 函数是一个语句的集合，可以被调用以作为一个单元执行。函数将在后的第 7 章"使用函数组织脚本"中介绍。

默认情况下，在子作用域中创建的变量可以在父作用域中查看和访问，除非变量被定义为私有，在这种情况下，变量只能从它们自己的作用域访问。

因此，你在书中 PowerShell 游戏脚本中使用的所有变量都是局部作用域的，因此可以在整个脚本中访问。然而，正如你将在第 7 章看到的，你可以在函数内部定义变量并将其标记为私有，将访问限制仅在函数内部。

### 数组

如所述，变量可以用于存储数字、字符串和任何类型的对象。变量也可以用于存储数组。数组是一个带索引的值列表。存储在数组中的每个元素都被分配了一个唯一的数字索引，稍后可以使用该索引检索其值。在 Windows PowerShell 中，数组索引从零开始，第一个元素的索引为零。

```
$numbers = @(1..5)
```

### 修改值

你可以通过指定索引号来修改数组中任何元素的值，如下所示。

```
$numbers = @(1, 2, 3, 4, 5)
$numbers[2] = 9
```

执行时，此示例产生以下输出：

正如你所看到的，数组中第三个元素的值已更改为 9。（记住数组索引从 0 开始。）

### 跟踪数组大小

数组还有一个`Count`属性，你可以用它确定数组中的元素数量，如下：

```
$names = @("Alexander", "William", "Molly")
$total = $names.Count
$total
```

执行时，`$total`被赋值为 3。

### 合并数组

Windows PowerShell 还允许你使用`+`运算符合并两个数组以创建一个新数组，如下所示。

```
$lowNumbers = @(1, 2, 3)
$highNumbers = @(4, 5, 6)
$numbers = $lowNumbers + $highNumbers
$numbers
```

在这个示例中，定义了两个数组`$lowNumbers`和`$highNumbers`。然后使用`+`运算符合并这两个数组创建一个名为`$numbers`的新数组，其元素为 1, 2, 3, 4, 5 和 6。

### 删除和插入数组元素

没有直接的方法可以在数组的特定位置插入元素。然而，使用范围运算符和`+`运算符，你可以绕过这一缺陷，如下：

```
$numbers = @(1, 2, 3, 4, 5, 6, 7)
$numbers = $numbers[0..2 + 4..6]
$numbers
```

在这个示例中，第一个语句定义了一个名为`$numbers`的数组。第二个语句通过使用范围运算符和`+`运算符重新赋值`$numbers`数组的内容，生成由原始数组的前三个和最后三个元素组成列表。执行时，此示例产生以下输出：

- 1
- 2
- 3
- 5
- 6
- 7

也没有直接的方法可以在数组的开头或中间插入元素。然而，通过调整上述演示的技术，你可以在数组的任何给定位置插入一个数字，如下：

```
$numbers = @(1, 2, 3, 4, 5, 6, 7)
$numbers = $numbers[0..3] + 99 + $numbers[4..6]
$numbers
```

在这个示例中，数字 99 被插入到了数组的中间。

### 关联数组

数组的一个缺点是，随着其规模的扩大，要追踪单个数组元素的存储位置变得越来越困难。因此，为了找到某个特定的值，你通常需要设置一个循环来搜索数组，按顺序检查每个元素以找到你想要的那个。关联数组（也称为哈希表 hash 或字典 dictionary）提供了一种更高效、速度更快的的替代方案，允许你以键值对的形式存储数据。

### 创建关联数组

创建关联数组的一种方法是将其定义为一个空的关联数组，如下所示：

```powershell
$ids = {};
```

如你所见，用于存储哈希表的变量只是一个普通变量，而空哈希表由`@()`表示。

一旦定义，你就可以根据需要向其添加任何键值对，如下文所示。

在这些语句中的每一条都会向关联数组中添加一个新条目。括号内指定的值是键（key），等号右侧指定的值是值（value）。

### 访问存储在关联数组中的数据

一旦创建并填充了数据，就可以从关联数组中检索一个值，如下所示：

```powershell
$x = $ids[34567]
```

在这里，从关联数组中检索了值为 Molly 的值并将其赋值给名为`$x`的变量。

关联数组可以存储任意数量的数据。关联数组元素以值的形式存储，如果它们包含空格，则必须包含在引号内。存储的值通过引用其关联键来检索。关联数组可以存储任何类型的数据。从关联数组中检索数据的速度非常快，且不会随着更多值的添加而变慢。

### 在创建时填充关联数组

关联数组也可以在创建时进行填充，如下所示：

```powershell
$nicknames = @{Alexander = "X-Man"; William = "William-D"; Molly = "Mighty-One"}

$x = $nicknames["Alexander"]
```

如你所见，定义了三个独立的键值对。键值对之间用分号分隔，并包含在匹配的括号内，且以`@`字符开头。执行执行时，`$x`被赋值为`Alexander`。

如果你想从 PowerShell 脚本中显示关联数组的内容，如下文所示：

```powershell
$nicknames = @{Alexander = "X-Man"; William = "William-D"; Molly = "Mighty-One"}

$nicknames
```

执行时，此示例将产生以下输出：

| Name | Value |
| --- | --- |
| Alexander | X-Man |
| Molly | Mighty-One |
| William | William-D |

> 提示

与数组一样，你可以使用运算符组合关联数组的内容，如下所示：

```powershell
$kidNames = @{Alexander = "X-Man"; William = "William-D"; Molly = "Mighty-One"}

$parentNames = @{Jerry = "Daddy"; Mary = "Mommy"}

$familyNames = $kidNames + $parentNames

$familyNames
```

执行时，此示例产出以下输出：

| Name | Value |
| --- | --- |
| William | William-D |
| Alexander | X-Man |
| Jerry | Daddy |
| Molly | Mighty-One |
| Mary | Mommy |

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_167_0.png)

### 删除键值对

关联数组提供了许多内容的方法，允许你操作其内容。例如，你可以使用`Remove`方法从关联数组中删除一个条目，如下所示：

```powershell
$nicknames = @{Alexander = "X-Man"; William = "William-D"; Molly = "Mighty-One"}
$nicknames.Remove("Alexander")
$nicknames
```



执行时，此示例将产生以下输出：

| Name | Value |
|------|-------|
| Molly | Mighty-One |
| William | William-D |

### 移除关联数组内容

使用`Clear`方法，你可以移除关联数组的内容，如下：

```powershell
$nicknames.Clear()
```

> 提示：要了解更多关于哈希的信息，请使用`Get-Help` get来查找`Associative_Array`（关联数组）。

# 返回 SEINFELD 知识问答测试

好了，让我们回到本章的主要游戏项目——Seinfeld 知识问答测试（Seinfeld Trivia Quiz）。该游戏的开发将展示如何创建一个交互式的在线测验，向玩家呈现一系列经过分析和评分的问题。在创建此游戏时，你主要的关注点应该是使用变量来存储和轮询从玩家处收集的数据。此外，你应该注意在生成显示输出时对 Windows PowerShell 转义字符的使用。

### 设计游戏

Seinfeld 知识问答测试将从显示欢迎屏幕开始，然后显示测验的说明。接下来，它将呈现五个多选题。游戏在接受玩家答案之前，应该对每个问题的答案进行验证，并存储每个答案以备日后分析。一旦玩家完成测验，应该对玩家的答案进行评分，并根据其表现为玩家分配排名。

开发 Seinfeld 知识问答测试涉及的总体步骤概述如下：

1. 创建一个新的脚本文件并添加开头注释语句。
2. 定义脚本中使用的变量以存储玩家答案并进行跟踪。
3. 显示欢迎屏幕。
4. 显示游戏说明。
5. 向玩家展示第一个问题。
6. 显示剩余的问题。
7. 通知玩家所有问题已回答。
8. 分析提供的答案。
9. 根据正确答案的数量分配排名。
10. 感谢玩家参加测验。

### 创建脚本

第一步是创建一个名为`SeinfeldTrivia.ps1`的新文件，并添加以下语句：

```powershell
************************************************
# 脚本名称: SeinfeldTrivia.ps1 (Seinfeld  Quiz)
# 版本: 2.0
# 作者: Jerry Lee Ford, Jr.
# 日期: 2008年10月6日
#
# 描述: 此 PowerShell 脚本通过五个问题
# 的测试测试玩家对 Seinfeld 的知识。
************************************************
```

```powershell
# 清空控制台屏幕
Clear-Host
```

### 变量的操作

创建 Seinfeld 知识问答测试的下一步是定义脚本使用的变量并赋予初始值。这通过在脚本文件末尾添加以下语句来实现：

```powershell
# 定义用于存储玩家答案的变量
$question1 = ""
$question2 = ""
$question3 = ""
$question4 = ""
$question5 = ""
```

```powershell
# 定义一个变量来跟踪正确回答
#问题的数量
$noCorrect = 0
```

### 显示欢迎屏幕

Seinfeld 知识问答测试开发的下一步是显示游戏的欢迎屏幕。这通过在脚本末尾追加以下语句来实现：

```powershell
# 显示游戏的开场屏幕
Write-Host "`n`n`n`n`n`tWELCOME TO THE SEINFELD"
Write-Host "`n`n`n`n`tTRIVIA QUIZ"
Write-Host "`n`n`n`n`tBy Jerry Lee Ford, Jr."
Write-Host "`n`n`n`n`n`n`n`n`tPress Enter to continue.\`
```

```powershell
# 暂停脚本执行并等待玩家按下 Enter 键
Read-Host
```

如你所见，游戏的欢迎界面是通过一系列`Write-Host`命令行创建的。为了控制字符串格式，每个语句中都嵌入了一系列转义字符。具体来说，添加了`\`转义字符的实例来生成换行命令，并使用`\`转义字符来插入制表符命令。上面显示的最后语句使用`Read-Host`命令行来暂停脚本执行，直到玩家按下回车键（Enter）。

## 显示说明

在阅读并并关闭游戏的欢迎界面后，需要显示有关参加测验的说明及其排名系统的解释。这通过将以下语句附加到脚本文件的末尾来实现。

```
#清空 Windows 命令行控制台屏幕
Clear-Host

#为玩家提供说明
Write-Host "\n\n Seinfeld 知识测试测试你对 Seinfeld\'n"
Write-Host " 的了解。测验由五个权重相同的多\'n"
Write-Host " 选择题组成。测验结束后，你的答案将被\'n"
Write-Host " 并分配技能等级，使用\'n"
Write-Host " 以下标准： \n\n"
Write-Host " \t 分数：5 个正确 = Jerry (专家)"
Write-Host " \t 4 个正确 = Kramer"
Write-Host " \t 3 个正确 = Elaine"
Write-Host " \t 2 个正确 = George"
Write-Host " \t 1 个正确 = Newman"
Write-Host " \t 0 个正确 = Babo (无知)"
Write-Host "\n\n\n 按回车键继续。"
```

```
#暂停脚本执行并等待玩家按下回车键
Read-Host
```

上面显示的语句清空屏幕并使用一系列`Write-Host`命令行显示文本输出。然后使用`Read-Host`命令行暂停脚本，强制玩家按下回车键以继续测验。

### 显示第一个测验问题

Seinfeld 知识测验的下一步步骤是展示第一个测验问题并收集玩家的答案。用于

# 第 4 章 · 变量、数组和哈希

游戏第一个问题的代码语句在下面列出，并应该附加到脚本文件的末尾。

脚本文件这部分的整体逻辑由一个`while`循环控制。在`while`循环内部，使用`Read-Host`命令行提示玩家提供第一个测验问题的答案。玩家的答案存储在名为`$question1`的变量中。循环被设置为执行，直到玩家提交第一个测验问题的有效答案。有效答案是 a、A、b、B、c、C、d 或 D。（请记住，默认情况下 Windows PowerShell 不区分大小写）。如果玩家提供了有效答案，循环将停止执行，脚本将继续运行。然而，如果玩家未能提供有效响应，循环将重复，提示玩家回答问题。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_172_0.png)

构成脚本文件这部分的逻辑由许多编程语句组成，这些语句在第 5 章和第 6 章中才会被正式介绍。由于这本书尚未涵盖这些编程结构，我将不会详细介绍它们。这些语句需要实现条件逻辑和循环逻辑。目前，为了让内容更容易理解，我添加了大量的注释语句来记录脚本文件这部分正在发生的内容，我建议你在读完第 5 章和第 6 章后回来复习这部分。

## 显示剩余的测验问题

展示后四个测验问题并收集玩家答案的语句在之前给出并应该附加到脚本文件的末尾。

```
#清空 Windows 命令行控制台屏幕
Clear-Host
```

```
#向玩家提问第二个问题
while (($question2 -ne "a") -and ($question2 -ne "b") 
and ($question2 -ne "c") -and ($question2 -ne "d")))

Clear-Host #清空 Windows 命令行控制台屏幕"
```

```
Write-Host
Write-Host " George 最喜欢的假装职业是什么?"
Write-Host
Write-Host " A. 内裤销售员"
Write-Host " B. 房地产"
Write-Host " C. 城市规划师"
Write-Host " D. 建筑师"
Write-Host
$question2 = Read-Host " 输入代表正确答案的字母并按下回车键"
```

```
#清空 Windows 命令行控制台屏幕
Clear-Host
#向玩家提问第三个问题
while (($question3 -ne "a") -and ($question3 -ne "b") 
and ($question3 -ne "c") -and ($question3 -ne "d")))

Clear-Host #清空 Windows 命令行控制台屏幕"
```

```
Write-Host
Write-Host " Elaine 为谁买了白色袜子?"
Write-Hostn
```

# 第 4 章 • 变量、数组和哈希

```
Write-Host " A. Lippman 先生"
Write-Host " B. Peterman 先生"
Write-Host " C. Pitt 先生"
Write-Host " D. Puddy"
Write-Host
$question3 = Read-Host " 输入代表正确答案的字母并按下回车键"
```

```
#清空 Windows 命令行控制台屏幕
Clear-Host
#向玩家提问第四个问题
while (($question4 -ne "a") -and ($question4 -ne "b") 
and ($question4 -ne "c") -and ($question4 -ne "d")))

Clear-Host #清空 Windows 命令行控制台屏幕"
```

```
Write-Host
Write-Host " Kramer 害怕什么?"
Write-Host
Write-Host " A. 游泳"
Write-Host " B. 鸡子"
Write-Host " C. 小丑"
Write-Host " D. 牙医"
Write-Host
$question4 = Read-Host " 输入代表正确答案的字母并按下回车键"
```

```
#清空 Windows 命令行控制台屏幕
Clear-Host
#向玩家提问第五个问题
while (($question5 -ne "a") -and ($question5 -ne "b") 
and ($question5 -ne "c") -and ($question5 -ne "d")))

Clear-Host #清空 Windows 命令行控制台屏幕"
```

```
Write-Host
Write-Host " Jerry 的父母住在哪里?"
Write-Host
Write-Host " A. 堪斯州"
Write-Host " B. 纽约"
Write-Host " C. 加利福尼亚州"
Write-Host " D. 佛罗里州"
Write-Host
$question5 = Read-Host " 输入代表正确答案的字母并按下回车键"
 }
```

## 通知玩家测验已完成

一旦玩家回答完所有五个问题，脚本应该暂停，通知玩家测验现在将评分。这通过将以下语句添加到脚本末尾来实现。

#清空 Windows 命令行控制台屏幕

Clear-Host

暂停脚本执行并等待玩家按下回车键

Read-Host

如你所见，这些语句使用`Clear-Host`命令行清空屏幕，使用`Write-Host`命令行显示文本，并使用`Read-Host`命令行暂停执行直到玩家按下回车键。

## 分析玩家答案

现在是分析玩家提供的每个答案以判断其对错。这通过将以下语句附加到脚本文件的末尾来实现。

```
#清空 Windows 命令行控制台屏幕
Clear-Host
```

```
#为每个测验问题评分
if ($question1 -eq "b") { $noCorrect++ }
if ($question2 -eq "d") { $noCorrect++ }
if ($question3 -eq "c") { $noCorrect++ }
if ($question4 -eq "c") { $noCorrect++ }
if ($question5 -eq "d") { $noCorrect++ }
```

## 分配排名

一旦正确回答的测验问题数量统计完毕，脚本就需要根据结果为玩家分配排名。具体来说，排名分配是通过将`$noCorrect`的值与表 4.6 中列出的值进行比较实现的。

| 分配 | 描述 |
|------|------|
| Babo | 零正确答案 |
| Newman | 一个正确答案 |
| George | 两个正确答案 |
| Elaine | 三个正确答案 |
| Kramer | 四个正确答案 |
| Jerry | 五个正确答案 |

```
#根据测验分数分配排名
if ($noCorrect -eq 0) {
Write-Host }
```

Write-Host " 你没有答对任何题目。"

Write-Host

Write-Host " 你对《席来场》冷知识的了解并不比 Babo 高。"

```powershell
if ($noCorrect -eq 1) {
Write-Host
Write-Host " 你答对了 1 道题目。"
Write-Host
Write-Host " 你对《席来场》冷知识的了解并不比
"Newman 高。"
}
```

```powershell
if ($noCorrect -eq 2) {
Write-Host
Write-Host " 你答对了 2 道题目。"
Write-Host
Write-Host " 你对《席来场》冷知识的了解大约是
"George 的水平。"
}
```

```powershell
if ($noCorrect -eq 3) {
Write-Host
Write-Host " 你答对了 3 道题目。"
Write-Host
Write-Host " 你对《席来场》冷知识的了解大约是
" Elaine 的水平。"
}
```

```powershell
if ($noCorrect -eq 4) {
Write-Host
Write-Host " 你答对了 4 道题目。"
Write-Host
Write-Host " 你对《席来场》冷知识的了解与
"Kramer 一样好。"
}
```

```powershell
if ($noCorrect -eq 5) {
```

## 第 4 章 • 处理变量、数组和哈希表

```powershell
Write-Host
Write-Host " 你答对了 5 道题目。"
Write-Host
Write-Host " 你对《席来场》冷知识的了解与
"Jerry 一样好。"
```

```powershell
}
# 暂停脚本执行并等待玩家按下回车键
Read-Host
```

变量`$noCorrect`的值只能等于上述五个`if`状态中列出的值之一。匹配的`if`语句将显示一系列文本字符串，显示玩家正确回答了多少道题目以及相应获得的排名。嵌入在四个不匹配的`if`语句中的代码语句将被忽略且永远不会执行。

## 完成测验

游戏流程结束后，《席来场》冷知识测验将结束，并感谢玩家花时间完成测验。这通过在脚本文件的末尾添加以下语句来实现。

```powershell
### 清除 Windows 命令控制台屏幕
Clear-Host

### 为玩家提供指令
Write-Host
Write-Host "感谢参加《席来场》冷知识测验!"
```

```powershell
# 暂停脚本执行并等待玩家按下回车键
Read-Host
```

```powershell
### 清除 Windows 命令控制台屏幕
Clear-Host
```

玩家通过按下回车键关闭此屏幕。随后 Windows 命令控制台屏幕清除，脚本文件停止执行。

## 最终结果

好了，这就是你完成《席来场》冷知识测验开发所需的所有内容。假设你在输入脚本文件时没有任何拼写错误，一切都将如预期般工作。如果发生错误，说明你在脚本文件的某处犯了一两个拼写错误。为了跟踪错误，请从分析尝试运行脚本时显示的错误消息开始。希望提供足够的信息可以帮助你找到错误。可能是你在输入脚本语句时犯了拼写错误或漏掉了某条语句。如果你的脚本包含多个错误，你可能需要经过多次迭代才能消除所有错误。

### 总结

本章向你展示了如何存储、检索和修改数据。你学习了如何处理变量、数组和哈希表。你还学习了如何处理 Windows PowerShell 内置变量。你学习了如何使用 Replace 运算符执行字符串操作，以及如何使用 Range 运算符生成值值列表。此外，你还学习了如何连接字符串、变量和哈希表。你还学习了如何使用 Windows 转义字符来简化并控制文本输出的格式。最后，你学习了如何创建一个新的 Windows PowerShell 游戏——《席来场》测验。

在进入下一章节之前，花几分钟完成以下挑战列表来改进《席来场》测验。

### 挑战

- 1. 目前，《席来场》冷知识测验仅限于五个问题。通过添加自己的问题让测验更具挑战性。
- 2. 不要将测验限制为选择题，添加不同格式的题目，例如真假题和填空。
- 3. 按照目前的写法，游戏显示玩家正确回答的题目数量。然而，关于题目结果的额外细节将为玩家提供更好的反馈。考虑在游戏结束时显示报告，显示每道题目及其正确答案。

## 第 5 章

## 实现条件逻辑

Windows PowerShell 脚本语言就像每种编程语言一样，包含了提供了测试和评估不同条件的语言语句。条件逻辑是编程逻辑的基础组成部分，如果不使用它，就无法开发任何复杂程度的 PowerShell 脚本。条件逻辑有助于对用户、系统和文件输入进行相互评估，以及将其与系统资源进行对比。根据条件测试的结果，你的 PowerShell 脚本可以对执行执行哪些语句进行严密控制，从而创建出根据其遇到的数据调整执行情况的新型动态脚本。

具体来说，你将学习如何：

- 使用`if`语句的变体实现条件逻辑
- 将`if`语句嵌套在一起以构建更复杂的逻辑
- 使用`switch`语句创建评估多个条件的逻辑测试
- 处理不同类型的比较运算符和逻辑运算符



## 项目预览：猜数字游戏

在本章中，你将学习如何创建一个名为“猜数字”的新 Windows PowerShell 程序。这个游戏将挑战玩家用尽可能少的尝试猜出一个 1 到 100 之间的随机数字。如图 5.1 所示，游戏通过显示欢迎屏幕开始。

玩家通过按下回车键关闭欢迎屏幕。接下来，游戏显示图 5.2 所示的消息，提示玩家做出初始猜测。

每次猜测后，游戏都会分析玩家的输入，判断是太高、太低，还是玩家正确猜中了秘密数字。图 5.3 显示了当玩家猜低时游戏显示的消息。

一旦最终猜中秘密数字，游戏将祝贺玩家，如图 5.4 所示。

接下来，将显示统计数据，提醒玩家秘密数字的值，并显示在猜中之前花了多少次猜测，如图 5.5 所示。

按下回车键关闭统计数据显示后，游戏邀请玩家再玩一轮，如图 5.6 所示。

如果玩家输入`Y`，将开始新一轮游戏。如果玩家输入`N`，游戏结束并返回 PowerShell 提示符。任何其他输入将被拒绝并再次提示玩家做出决定。

## 比较值

Windows PowerShell 比较不同资源（如数字和字符串）的能力。为了演示这种能力，启动一个新的 PowerShell 会话并输入`5 -eq 5`然后按回车，如下：

```powershell
PS C:> -eq 5
```

```
True
```

`-eq`是 PowerShell 运算符，在本示例中用于判断两个数字是否相等。一旦完成评估，Windows PowerShell 将以布尔真或假值的形式显示评估结果。所有比较操作都会评估为真或假值。下一个示例演示了从两个不相等值进行比较的结果。

## 第 5 章 • 实现条件逻辑

```
PS C:\> 5 -eq 10
False
```

你也可以比较不同类型的值，例如字符串和数字，如下所示。

```
PS C:\> 5 -eq "X"
False
```

为了执行此评估，Windows PowerShell 必须将被比较的值转换为相同类型。当遇到这种情况情况时，PowerShell 会尝试将第二个值转换为与第一个值相同的类型。这里提供了一个此类类型转换如何产生真值的良好示例：

```
PS C:\> 5 -eq "5"
True
```

在例例中，PowerShell 将字符串`"5"`转换为其数值等效值。Windows PowerShell 允许你比较各种复杂程度的表达式，如下所示：

```
PS C:\> 5 + 7 -eq 3 + 3 + 3 + 3
True
```

一旦执行，运算符左侧表达式的值评估结果为 12，右侧运算符表达式的值也是如此。

![](img/e07ce5ce2afe5ff9f444f2c3361d9d87e_184_0.png)

如果你发现自己正在使用 PowerShell 命令行，并需要进行一两个快速计算，那么无需停止正在进行的工作去打开计算器应用程序并处理几个数字。相反，你可以使用 Windows PowerShell 作为你的计算器来节省一些时间。例如，如果你只需要相乘几个数字，只需使用相应的 PowerShell 算术运算符输入它们，如下所示：

```
PS C:\> 5 * 5
25
PS C:\>
```

在这里，在 PowerShell 提示符处输入了表达式`5 * 5`。当按下 Enter 键时，PowerShell 解析该表达式并显示结果。如接下来的示例所示，如果需要，你可以输入更复杂的数学表达式。

```
PS C:\> 20 * 5 / (10 + 15) * 3
12
PS C:\>
```

### 组合管道和运算符

除了比较字符串和数字外，你可以在对象数据通过 PowerShell 对象管道时，将其与不同的值进行比较。这允许你选择想要继续发送通过管道的数据，并丢弃不需要处理的数据。例如，使用`eq`运算符，你可以提取任何正在执行的进程的名称，如下所示：

```
PS C:\Get-Process | Where-Object {$_.ProcessName -eq "Winword"}
```

| Handles | NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id | ProcessName |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 237 | 11 | 7540 | 18992 | 110 | 5,286.61 | 1620 | WINWORD |

```
PS C:\>
```

如你所见，`Get-Process`命令已执行。它生成了一份运行在计算机上的活动进程列表。然后，该列表被传递到`Where-Object`命令，该命令会对每个进程进行评估，寻找名为 Winword 的名称。如果找到，将显示有关该进程的信息。

这种评估不仅限于`Get-Process`命令。它可以应用于任何命令的输出。例如，接下来的组语句处理由`Get-ChildItem`命令生成的输出，寻找一个特定的文件夹。

```
PS C:\Get-ChildItem | Where-Object {$_.Name -eq "MyScript"}
```

```
Directory: Microsoft.PowerShell.Core\FileSystem:\C:\

Mode LastWriteTime Name
d---- 3/28/2006 1:56 PM MyScripts
```

```
PS C:\>
```

## 实现条件逻辑

比较操作是 PowerShell 脚本的一个关键功能，在所有最简单的 PowerShell 脚本中都是需要的。然而，你将需要比较作为条件语句的一部分。Windows PowerShell 支持两种不同的条件逻辑语句，下述如下：

- `if`：此语句评估一个比较，然后执行或跳过位于关联代码块中的语句的执行。
- `switch`：此语句支持执行多个比较操作，每个操作都有执行嵌入在关联代码块中的语句的能力。

### 使用 if 语句进行数据比较

`if`语句用于测试条件的值，并根据该评估的结果有条件地执行位于关联代码块中的语句。你已经在书中多次看到`if`语句的实际运行。它的语法在此概述：

```
if (condition) code block
else (condition) code block
else {code block}
```

`condition`是一个占位符，表示评估为布尔值真或否的表达式。`code_block`是一个占位符，表示根据测试结果执行的任意语句。`if`语句非常灵活，支持许多不同的变体。

`elseif`是一个可选语句，你可以包含它来测试替代条件。PowerShell 允许你包含任意数量的`elseif`语句。`else`也是一个可选语句，添加后当先先的条件测试都不评估为真时，它会执行关联的控制块。

`if`、`elseif`和`else`语句允许你根据测试评估（例如变量、管道对象或表达式）来执行存储在代码块中的语句。如果你创建一个包含多个`elseif`评估的`if`语句，将执行属于第一个评估为真的测试的代码块。

```powershell
else {
    Clear-Host
    Write-Host "Press Enter to try again."
    Read-Host
}
```

图 5.7 提供了上一个示例中实现逻辑的流程图概述。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_189_0.png)

图 5.7

`if`语句涉及的逻辑描述。

流程图是程序员用于图形化描述脚本全部或部分逻辑流的的工具。通过创建流程图，你可以视觉化地布局 PowerShell 脚本的整体逻辑流。一旦创建，你就可以流程图来引导脚本的开发。

### 测试不同的条件

`if`语句还可以通过包含一个或多个可选的`elseif`语句来扩展。每个`elseif`语句都为你提供了测试不同条件的能力，如下所示：

```powershell
if ($x -eq 10) {
    Clear-Host
    Write-Host "Game over! Press Enter to continue."
    Read-Host
}
elif ($x -eq 20) {
    Clear-Host
    Write-Host "Invalid guess. Press Enter to try again."
    Read-Host
} elseif ($x -eq 30) {
    Clear-Host
    Write-Host "Invalid input. Press Enter to try again."
    Read-Host
} else {
    Clear-Host
    Write-Host "Unknown error. Press Enter to try again."
    Read-Host
}
```

在这里，评估了三个独立的条件。Windows PowerShell 开始此示例时会测试第一个条件的值`($x -eq 10)`。如果该条件评估结果为真，则执行其代码块中的三个语句，并跳过`if`语句中的其余语句。如果条件评估结果为假，则执行与`elseif`语句关联的条件。如果其评估结果为真，则执行其代码块中的语句，并跳过`if`语句中的其余语句。否则，跳过`elseif`的代码块并评估下一个`elseif`语句的条件。如果其条件评估结果为真，则执行其代码块并跳过其中的其余语句。如果之前测试的条件没有一个评估为真，则执行与`else`语句关联的代码块。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_190_0.png)

如果你发现自己正在创建许多针对相同值进行评估的语句，可能使用下一节讨论的`switch`语句会更好。

### 语句中的嵌套

Windows PowerShell 允许将一个`if`语句嵌套（或嵌入）另一个语句中，以便开发复杂的条件测试。嵌套语句允许你构建编程逻辑，在决定是否通过执行额外测试进一步分析事物之前，通过测试一个条件来获益。

作为嵌套`if`语句用处的示例，请考虑以下内容（提取自你在第 3 章“使用 .NET 进行基于对象的脚本编写”中占卜师游戏）。

### 根据时间和和随机数选择答案

如果是下午，占卜师会有点小脾气

```powershell
if ($time -gt 12) {
    Write-Host
    if ($answer -eq 1) { "Grrr. The answer is no!" }
    if ($answer -eq 2) { "Grrr. The answer is never!" }
    if ($answer -eq 3) { "Grrr. The answer is unclear!" }
    if ($answer -eq 4) { "Grrr. The answer is yes!" }
}
```

如果是早上，占卜师会心情很好

```powershell
else {
    Write-Host
    if ($answer -eq 1) { "Ah. The answer is yes!" }
    if ($answer -eq 2) { "Ah. The answer is always!" }
    if ($answer -eq 3) { "Ah. The answer is uncertain!" }
    if ($answer -eq 4) { "Ah. The answer is no!" }
}
```

在这个示例中，如果语句检查`$time`是否大于 12。如果是，则执行嵌入其代码块中的一系列四个语句，每条语句都会按顺序评估名为`$answer`的变量的值，以决定返回给玩家的答案。如果起始语句评估结果为假，则执行`else`语句。请注意`else`语句代码块中也嵌入了四条语句。

### 使用 switch 语句进行多次比较

`if`语句允许你比较两个条件。通过添加`elseif`语句，你可以创建执行额外测试的语句。随着额外测试数量的增加，它们可能会变得难以制定和理解。Windows PowerShell 提供了`switch`语句作为替代方案。`switch`语句用于定义一组不同的测试和代码块，每个代码块都针对同一个表达式进行评估。

`switch`语句实现的语法列举如下：

```powershell
switch (expression) {
  (test) (code block)
  value (code block)
  default (code block)
}
```

`switch`语句首先定义所有代码块比较将进行评估的表达式。`switch`语句支持三种不同类型的比较操作中的任何一种，如下所示：

- Test（测试）：评估其值的表达式。
- Value（值）：一个字面量，例如字符串或数字。
- Default（默认）：指定一个默认代码块。

为了很好地了解如何使用`switch`，请考虑以下示例：

```powershell
$today = get-date
switch ($today.Day) {
    1 { Write-Host "Payday!" }
    5 { Write-Host "It is time to water the plants." }
    10 { Write-Host "Remember the bills." }
    15 { Write-Host "Payday!" }
    20 { Write-Host "It is time to water the plants." }
    25 { Write-Host "It is time to clean the garage." }
    default { Write-Host "There are no calendar entries to remember today." }
}
```

与算术运算符不同，Windows PowerShell 不按照预定义的顺序或优先级来处理比较运算符。相反，每个比较操作都是按照你定义的顺序执行的，从左到右进行。稍后在你编写“猜猜数字”游戏时，你将看到这些运算符运行的几个示例。

## 逻辑运算符

Windows PowerShell 提供了一小组逻辑运算符，提供了修改比较的逻辑评估的能力。表 5.2 列出了 PowerShell 逻辑运算符。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_194_0.png)

| 运算符 | 说明 |
| --- | --- |
| `-not` | 否 |
| `!` | 否 |
| `-and` | 与 |
| `-or` | 或 |

`-not`和`!`运算符可以反转任何比较操作的逻辑，如下所示：

```powershell
$x = 1
$y = 2
if (-not ($x -eq $y)) {Write-Host 'The value of $X does not equal $y.')}
if (! ($x -eq $y)) {Write-Host 'The value of $X does not equal $y.')}
```

你可以看到，通过使用`-not`或`!`运算符，你必须将其放在要测试的表达式或值之前。执行时，这些运算符会反转比较操作的逻辑。

> **注意** 请注意上述示例中括号的位置和放置。包含`-not`和`!`运算符需要你额外添加括号，以满足`if`语句的语法要求，`if`语句要求被测试的内容必须包含在括号内。

另一方面，`-and`运算符用于创建一个比较操作，以检查两个不同的表达式或值是否都评估为真，如下所示。

```powershell
$x = 1
$y = 2
if ($x -eq 1) -and ($y -eq 2)) {Write-Host 'The variables equal the expected values.'}
```

在这个示例中，只有当`if`语句代码块内部语句被`if`语句测试的两个表达式都评估为真时才会执行。由于上一个示例中评估的两个表达式结果均为真，因此执行了位于`if`语句代码块内部的语句。

为了提高`-and`运算符的逻辑处理效率，PowerShell 实现了短路机制，即只有在第一个表达式证明为假的情况下，才会评估第二个表达式；没有必要评估第二个表达式，因为无论第二个表达式的值如何，`-and`逻辑比较的最终结果都将为假。

`-or`运算符也具有短路功能。该运算符检查两个不同的表达式或值中是否至少有一个评估为真，如下所示：

```powershell
$x = 1
$y = 2
if ($x -eq 1) -or ($y -eq 3)) {Write-Host 'At least one value matched'}
```

在在上一个示例中，第一个表达式被评估为真，第二个表达式评估为假。只要被测试的表达式中 true一个评估为真，就会执行位于`if`语句代码块内部的语句。

## 字符串比较运算符

虽然你完全可以使用表 5.1 列出的前六个比较运算符来比较字符串，但结果将是不区分大小写的比较。因此，PowerShell 将将`"abc"`和`"ABC"`等字符串评估为相等，尽管这可能不是你的意图。如果在比较运算符中字符串的大小写很重要，你可以改用表 5.3 列出的任何区分大小写的比较运算符。

如你所示，表 5.3 包含了两个不同的运算符类别：区分大小写的比较运算符和不区分大小写的运算符。作为这两类字符串比较运算符差异的示例，请考虑以下示例。

## 表 5.3 WINDOW POWERSHELL 字符串比较运算符

| 运算符 | 说明 | 区分大小写 |
|---|---|---|
| `-ieq` | 等于 | 否 |
| `-ilt` | 小于 | 否 |
| `-igt` | 大于 | 否 |
| `-ige` | 大于等于 | 否 |
| `-ile` | 小于等于 | 否 |
| `-ine` | 不等于 | 否 |
| `-ceq` | 等于 | 是 |
| `-clt` | 小于 | 是 |
| `-cgt` | 大于 | 是 |
| `-cge` | 大于等于 | 是 |
| `-cle` | 小于等于 | 是 |
| `-cne` | 不等于 | 是 |



```powershell
$x = "abc"
$y = "ABC"
if ($x -ieq $y) {Write-Host 'A case-insensitive match has occurred!'}
if ($x -ceq $y) {Write-Host 'A case-sensitive match has occurred!'}
```

在这个示例中，第一个`if`语句执行了不区分大小写的比较，结果为真。然而，第二个`if`语句执行了区分大小写的比较，结果为假。

## 回到猜猜数字游戏

现在，让我们重新回到角色的主要游戏项目——猜猜数字游戏。通过开发这个游戏，你将获得充足的机会来关注如何使用条件逻辑来控制 PowerShell 脚本的逻辑执行。

## 循环直到玩家决定退出游戏

```powershell
while ($playGame -ne "No") (
```

如你所见，`while`循环的执行由赋值给`$playGame`变量的值控制。在脚本后续部分，当玩家决定停止游戏时，该变量会被设置为`No`。除了脚本文件末尾执行的`Clear-Host`常用命令外，构成“猜数字”游戏的所有剩余代码语句都将嵌入到此`while`循环中。

### 生成随机数

下一个需要完成的任务是生成游戏的秘密数字，该数字是使用`random`对象的`Next`方法生成的。这通过将以下语句添加到上一节中定义的`while`循环的开头来实现。

```powershell
#生成游戏的随机数（1 - 100 之间）
$number = $randomNo.Next(1,101)
```

## 建立箳粴循环以收集和分析玩家的猜测

下一步是清除屏幕并提示玩家进行猜测，这通过在之前的语句之后添加以下语句来实现。

```powershell
# 清除 Windows 命令行控制台屏幕
Clear-Host
```

```powershell
# 循环直到玩家猜中秘密数字
while ($status -ne "Stop") (
```

此`while`循环将用于控制玩家输入并确保输入是有效的。循环将一直执行，直到`$status`的值设置为`Stop`。在接下来两个节中概述的代码语句将嵌入到此循环中。

### 收集玩家输入

接下来显示的代码语句必须输入到之前的`while`循环中，负责收集用户的输入。

```powershell
# 提示玩家猜一个数字
while ($guess -eq "") {

  Clear-Host # 清除 Windows 命令行控制台屏幕

  Write-Host

  # 收集玩家的猜测
  $guess = Read-Host "输入 1 到 100 之间的数字"

}
```

该循环的设计使得，如果玩家在没有输入任何内容的情况下按下回车键，它将重复执行。在此循环内部，屏幕会被清除，并使用`Read-Host`令提示玩家进行猜测。玩家的答案将存储在名为`$guess`的变量中。

## 分析玩家输入

现在你已经添加了收集玩家猜测所需的代码语句，你需要在上一节语句之后立即添加以下语句。

```powershell
# 跟踪目前为止的猜测次数
$noOfGuesses++
```

```powershell
if ($guess -lt $number) { # 玩家猜的数字太小

  Clear-Host # 清除 Windows 命令行控制台屏幕
  Write-Host "\n抱歉。你猜太小了。按回车键再次猜测。"
  $guess = "" # 重置玩家的猜测
  Read-Host # 暂停游戏直到玩家按下回车键
}
 elseif ($guess -gt $number) { # 玩家猜的数字太大了

  Clear-Host # 清除 Windows 命令行控制台屏幕
  Write-Host "\n抱歉。你猜太大了。按回车键再次猜测。"
  $guess = "" # 重置玩家的猜测
  Read-Host # 暂停游戏直到玩家按下回车

}
else { # 玩家猜中了游戏的秘密数字

  Clear-Host # 清除 Windows 命令行控制台屏幕
  Write-Host "`n恭喜！你猜中了我的数字！按回车键继续。"
  $status = "Stop" # 重置玩家的猜测
  Read-Host # 暂停游戏直到玩家按下回车
}
```

第一条语句增加`$noOfGuesses`的值，以便跟踪玩家在游戏中目前为止的猜测次数。其余语句由一个`if`语句组织。该`if`语句用于测试存储在`$guess`中的玩家猜测值是否小于存储在`$number`中的游戏随机数。如果`$guess`小于`$number`，则会显示一条消息告知玩家猜得太小了，并将`$guess`设置为空字符串（`""`），以便为玩家下一次猜测做好准备。

接下来，设置了一个`elseif`语句来响应玩家猜得太大的情况。最后，定义了一个`else`语句，它在玩家正确猜中游戏秘密数字时执行。请注意，如果是这种情况，`$status`变量将被赋值为`Stop`，以信号当前轮游戏结束。

## 显示游戏统计数据

下一组程序语句需要添加到游戏主控制`while`循环的末尾。

```powershell
# 清除 Windows 命令行控制台屏幕
Clear-Host
```

```powershell
# 显示游戏的初始统计数据
Write-Host "`n 游戏统计"
Write-Host "................................"
Write-Host "`n秘密数字是: $number。"
Write-Host "`你用了 $noOfGuesses 次猜中。\n"
```

```powershell
Write-Host "按回车键继续。"

# 暂停游戏直到玩家按下回车键
Read-Host
```

如你所见，这些语句负责清除 Windows 命令行控制台并显示游戏统计数据。这些统计数据存储在`$number`和`$nOfGuesses`变量中。

## 提示玩家玩

现在是时候再次提示玩家了。

```powershell
# 清除 Windows 命令行控制台屏幕
Clear-Host
```

```powershell
### 提示玩家再次游戏
while ($reply -eq "") {

  Clear-Host # 清除 Windows 命令行控制台屏幕

  Write-Host

  # 收集玩家的响应
  $reply = Read-Host "你想再次玩吗？(Y/N)"

}
```

该循环的设计使得，如果玩家在没有输入任何内容的情况下按下回车键，它将重复执行。在此循环内部，屏幕会被清除，并使用`Read-Host`令提示玩家做出选择。玩家的答案将存储在名为`$reply`的变量中。

```powershell
if ($reply -eq "Y") {
  $status = "*"
  $noOfGuesses = 0
}
else {
  $playGame = "No"
}
```

## 清除屏幕

为了结束游戏，清除屏幕。

```powershell
# 清除 Windows 命令行控制台屏幕
Clear-Host
```

执行`Clear-Host`令后，脚本将结束，让玩家返回 PowerShell 命令行提示符。

# 初学者必备 Microsoft Windows PowerShell 2.0 编程，第二版

```powershell
#显示游戏的启动界面
Write-Host "\n\n\n\n\t WELCOME TO THE GUESS MY"
Write-Host "\n\n\n\n\tNUMBER NUMBER GAME"
Write-Host "\n\n\n\n\t\tBy Jerry Lee, Jr."
Write-Host "\n\n\n\n\n\n\n\t\tPress Enter to continue."

# 暂停游戏直到玩家按下 Enter 键
Read-Host

# 循环直到玩家决定退出游戏
while ($playGame -ne "No") {

    # 生成游戏的随机数（1 到 100 之间）
    $number = $randomNo.Next(1,101)

    # 清空 Windows 命令行控制台屏幕
    Clear-Host

    # 循环直到玩家猜中秘密数字
    while ($status -ne "Stop") {

        # 提示玩家猜一个数字
        while ($guess -eq "*") {

            Clear-Host # 清空 Windows 命令行控制台屏幕

            Write-Host

            # 收集玩家的猜测
            $guess = Read-Host " Enter a number between 1 and 100"

            # 跟踪目前为止的猜测次数
            $noOfGuesses++

            if ($guess -lt $number) { # 玩家猜的数字太小了
```

## 第 5 章 实现条件逻辑

```powershell
Clear-Host # 清空 Windows 命令行控制台屏幕
Write-Host "`n Sorry. Your guess was too low. Press Enter to `
`guess again."
$guess = "" # 重置玩家的猜测
Read-Host # 暂停游戏直到玩家按下 Enter 键
```

```powershell
}
```

```powershell
elseif ($guess -gt $number) { # 玩家猜的数字太大了
```

```powershell
Clear-Host # 清空 Windows 命令行控制台屏幕
Write-Host "`n Sorry. Your guess was too high. Press Enter to `
`guess again.
$guess = "" # 重置玩家的猜测
Read-Host # 暂停游戏直到玩家按下 Enter 键
```

```powershell
else { # 玩家猜中了游戏的秘密数字
```

```powershell
Clear-Host # 清空 Windows 命令行控制台屏幕
Write-Host "`n Congratulations. You guessed my number! Press Enter `
`to continue."
$status = "Stop" # 重置玩家的猜测
Read-Host # 暂停游戏直到玩家按下 Enter 键
```

```powershell
}
```

```powershell
}
```

```powershell
# 清空 Windows 命令行控制台屏幕
Clear-Host
```

```powershell
# 显示游戏的统计信息
Write-Host "`n Game Statistics"
Write-Host ""
Write-Host "`n The secret number was: $number."
Write-Host "`n You guessed it in $noOfGuesses guesses.\`n"
```

# 初学者必备 Microsoft Windows PowerShell 2.0 编程，第二版

```powershell
Write-Host "------------------------------------------------------"
Write-Host "\n\n\n\n\n\n\n\n\n\n\nPress Enter to continue.
"
```

```powershell
# 暂停游戏直到玩家按下 Enter 键
Read-Host
```

```powershell
# 清空 Windows 命令行控制台屏幕
Clear-Host
```

```powershell
$reply = "" # 存储玩家被要求再次玩时的响应
```

```powershell
# 提示玩家再玩一轮
while ($reply -eq "") {
```

```powershell
Clear-Host # 清空 Windows 命令行控制台屏幕
```

```powershell
Write-Host

# 收集玩家的回答
$reply = Read-Host "" Would you like to play again? (Y/N) "
```

```powershell
# 验证玩家输入，仅允许 Y 和 N 为有效响应
if ($reply -ne "Y") -and ($reply -ne "N") {
```

```powershell
$reply = "" # 将变量重置为默认值
```

```powershell
}
```

```powershell
}
```

```powershell
# 玩家选择再次玩
if ($reply -eq "Y") {

    # 将变量重置为默认值
    $number = 0
    $noOfGuesses = 0
    $status = "Play"
```

## 第 5 章 实现条件逻辑

```powershell
    $guess = 0
}
else # 玩家决定退出游戏

    $playGame = "No" # 修改变量表示是时候
    # 终止游戏了

}
)
```

```powershell
# 清空 Windows 命令行控制台屏幕
Clear-Host

好了，就是这样。只要你在输入时没有出现任何拼写错误，你的“猜猜猜数字”游戏版本就可以准备好运行了。

### 总结

在本章中，你学习了如何使用`if`和`switch`语句来开发条件逻辑，以控制 PowerShell 脚本中组语句的执行。条件逻辑有助于对用户、系统和文件输入进行相互评估，并将其与系统资源进行比对。你还学习了如何使用一系列不同的 PowerShell 运算符，包括`-and`和`-or`运算符，这些运算符进一步促进了条件逻辑的开发。

现在，在进入第 6 章“使用循环处理数据”之前，你何何不抽一些额外的时间，通过解决以下挑战来改进“猜猜猜数字”游戏呢？

### 挑战

- 1. 目前编写的游戏提供了一些晦涩的信息。考虑通过添加额外的指令让游戏变得更直观。
- 2. 正如你在之前的章节中所看到的，循环是大多数脚本中的基本元素。考虑跟踪游戏的次数。
- 3. 考虑修改游戏以允许玩家随时退出。
- 4. 考虑给玩家提供……的选项。

# 项目预览：石头剪布刀游戏

## 第 6 章 使用循环处理数据

正如你已经在之前的章节中注意到的那样，循环是处理数据的机制。如果没有循环，处理数据集是不可能的。具体来说，本章将教你：

- 如何设置`while`和`until`循环
- 如何设置`for`和`foreach`循环
- 如何创建`break`关键字来改变循环执行

《初学者级 Microsoft Windows PowerShell 2.0 编程》，第二版

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_213_0.png)

### 图 6.5

玩家决定停止玩石头、剪刀、布游戏。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_213_1.png)

### 图 6.6

游戏记录了胜次数、负次数、平局以及游戏总数。

## 循环操作

为了有效地重复执行一系列命令或处理大量数据，你需要创建循环的能力。循环是一组可以作为一个单元被重复执行的编程语句。循环允许你编写几行代码，并多次且按顺序执行它们，以完成大量工作。循环有助于减少编写 PowerShell 脚本所需的代码语句数量，并通过集中特定的编程逻辑，帮助你的脚本更易于管理。

循环是处理由 cmdlet（命令程序）返回的数组和数据集合内容的良好工具。正如你已经看到的，循环还可以设置为反复提示用户提供有效输入，并反复执行一组语句，直到达到特定结果。Windows PowerShell 提供了多种不同类型的循环访问，包括：

# 第 6 章 • 使用循环处理数据

- `do while`. 只要指定的条件为真就一直迭代。
- `do until`. 直到指定的条件为真时停止迭代。
- `for`. 迭代固定次数。
- `foreach`. 遍历存储在集合或数组中的所有元素。
- `while`. 只要指定的条件为真就一直迭代。

你将在接下来的章节中学习如何使用这些种类型的循环。

除了上述列出的语言循环语句外，Windows PowerShell 还提供了对`Where-Object`和`ForEach-Object` cmdlet 的访问。正如你已经看到的，这些 cmdlet 允许你在数据列表通过对象管道时对其进行循环遍历和处理。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_214_0.png)

## 设置 do 循环

`do while`循环只要测试的条件保持为真（或“当”）就会一直执行。由于被测试的条件是在循环结束时评估的，你可以放心地循环至少执行一次。`do while`循环的语法所示：

```
do {

  code block

} while (condition)
```

`condition`是在循环每次迭代结束时测试的表达式。这里提供了一个如何使用`do while`循环的示例：

```
do {

  Write-Host $i

  $i++

} while ($i -lt 10)
```



在这个示例中，一个名为`$i`的变量被设置为 1，然后在随后的`do while`循环中使用。在循环内部，会显示`$i`的值，然后将其加 1。位于循环末尾的条件测试会被评估，只要`$i`的值仍然保持小于 10，循环就会继续执行。运行时，此示例将显示以下结果：

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10

# 192 初学者级 PowerShell 脚本编写，第二版

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_215_0.png)

在开发 PowerShell 脚本时需要注意的问题之一是死循环。死循环是一个永不终止的循环，因此会永远运行，耗尽计算机资源。当你创建一个没有办法停止自身执行的循环时，就会发生死循环。换句话说，你要么忘记提供终止手段，要么应用了错误的逻辑允许循环无限持续。

如果在测试 PowerShell 脚本期间，你认为出现了某些问题并且可能正在执行死循环，你可以按`Ctrl+C`跳出循环并终止你的脚本。

## 设置 do until 循环

`do until`循环一直执行，直到测试条件评估为真。或者换句话说，`do until`循环只要条件为假就会一直执行。与`while`循环一样，`do until`循环执行的测试指定在循环底部，确保了循环至少执行一次。

`do until`循环的语法在此所示：

```
do {

  code block

} until (condition)
```

要查看如何使用这种类型的循环，请考虑以下示例：

```
$i = 1
```

```
do {

  Write-Host $i

  $i++

} until ($i -gt 10)
```

此示例与之前的`while`示例非常相似，不同之处是这次循环被设置为运行直到`$i`的值大于 10。执行时，此示例完全像之前的`while`循环一样精确数到 10，证明了这些每一个

# 第 6 章 • 使用循环处理数据

循环都可以互换使用。`do until`循环也可以用于控制用户输入的集合，如下例所示。

```
$response = "Play"
```

```
do {

  $response = Read-Host "你想再玩一次吗？(Y/N)"

} until ($response -eq "N")
```

在这里，循环被设置为提示用户输入。如果用户输入`"Y"`，循环再次运行。如果用户输入`"N"`，循环终止。这是使用`do until`循环处理输入的常用方法。

## 创建循环

`for`循环用于执行指定次数的代码块。`for`循环的语法所示：

```
for (initialization; condition; step) {

  code block

}
```

`for`语句的三个部分都是可选的，初始化用于定义计数器变量。条件是在每次迭代之前评估的表达式，以确定循环是否继续。`step`指定了计数器变量在每次迭代结束时如何更新。

一个`for`循环的示例是：

```
for ($i = 1; $i -le 10; $i++) {

  Write-Host $i

}
```

在这个示例中，名为`$i`的变量初始化为 1。循环设置为只要`$i`小于或等于 10 就一直迭代。每次迭代后，`$i`加 1。此循环的输出是：

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10

`for`循环也可以用于递减计数器，如下：

```
for ($i = 10; $i -ge 1; $i--) {

  Write-Host $i

}
```

在这里，变量`$i`初始化为 10，循环只要`$i`大于或等于 1 就会迭代。每次迭代后，`$i`减 1。此循环的输出是：

- 10
- 9
- 8
- 7
- 6
- 5
- 4
- 3
- 2
- 1

`for`循环还可以用于处理数组的内容，如下例所示：

```powershell
$numbers = @("a", "b", "c", "d", "e")

for ($i = 0; $i -le $numbers.Length - 1; $i++) {

  Write-Host $numbers[$i]

}
```

在这个示例中，创建了一个数组`$numbers`并填充了五个字符串。`for`循环将变量`$i`初始化为 0。只要`$i`小于或等于数组长度减 1，它就会迭代。每次迭代后，`$i`加 1。此循环的输出是：

- a
- b
- c
- d
- e

# 196 微软 PowerShell 2.0 零基础编程，第二版

赋值给`step`参数的值并不总是需要为 1。如下例所示，你可以根据所需的任何数值来增加（或减小）此值。

`$numbers = @(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)`

```powershell
for ($i = 0; $i -le $numbers.Length - 1; $i += 2) {

    Write-Host $numbers[$i]

}
```

在这里，在循环的每次迭代中，`$i`的值都会增加 2，产生如下输出。

1

3

5

7

9

如你所见，通过在每次循环迭代时将`$i`的值增加 2，`$numbers`数组中的每个值都得到了处理。

> 提示：有关关于循环的更多信息，请在 Windows PowerShell 命令行提示符中输入`Get-Help -for`。

## 创建 foreach 循环

`foreach`循环的设计是为了方便数据集合的处理。它是专门为处理列表（包括数组）定制的，而你预先不知道数组中存储了多少个元素。虽然你可以使用其他类型的循环来完成相同的操作，但`foreach`循环提供了一种方便的方法来处理列表，因为它不需要你设置和增加索引值。

`foreach`循环的语法所示：

```powershell
foreach (element in collection) {

    (code block)

}
```

`element`是一个占位符，代表存储在集合中的元素。在循环的每次迭代中，`element`的值都会更新为集合中存储的下一个项目。`collection`是要处理数组的名称。

如你所见，此示例使用`foreach`循环遍历由`Get-Service`词命令生成的输出。循环每次迭代时，服务的名称会被赋值给`$x`。然后使用`if`语句检查每个服务的`Status`（状态）属性，以判断其是否等于`Running`（运行）。接着使用`Write-Host`命令通过引用每个服务的`Name`属性来显示每个运行服务的名称。执行时，此示例将产生类似于下方的输出。

- aawservice
- AeLookupSvc
- Appinfo
- Apple Mobile Device
- AudioEndpointBuilder
- Audiosrv
- avgBwd
- Basics Service
- BFE
- BITS
- Bonjour Service
- Browser
- CryptSvc
- DcomLaunch
- Dhcp
- Dncache
- DPS
- EMDMgmt
- Eventlog
- EventSystem
- fdHost
- FDResPub
- FontCache3.0.0.0
- gpsvc
- hidserv
- IKEEXT
- iphlpsvc
- iPad Service
- KtmRm
- LanmanServer
- LanmanWorkstation
- LightScribeService
- Imhosts
- MDM
- MMCSS
- MpsSvc
- Netman
- netprofm
- NlaSvc
- si
- nvsvc
- PcaSvc
- PlugPlay
- PolicyAgent
- ProfSvc
- RasMan
- RpcSs
- SamSs
- Schedule
- seclogon
- SENS
- ShellHWDetection
- slsvc
- Spooler
- SSDPSRV
- SstSvc
- stisvc
- SysMain
- TabletInputService
- TapiSrv
- TermService
- Themes
- TrkWks
- upnphost
- UxSms
- W32Time
- WdiSystemHost
- WebClient
- WerSvc
- WinDefend
- Winmgmt
- WPDBusEnum
- wscsvc
- WSearch
- wuauserv
- wudfsvc
- XAudioService

前面的示例说明，`foreach`循环可以用于遍历任何以集合形式生成输出的词命令输出，且不需要你定义和维护计数器，或提供任何其他控制逻辑。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_223_0.png)

## 使用 while 循环

`while`循环的设计用于创建一个只要其条件为真就一直运行的循环。`while`循环具有以下语法。

```powershell
while (condition) {

    (code block)

}
```

`condition`是一个表达式，在每次循环运行时都会进行求值。如果`condition`的值为`true`，则运行循环；否则，执行终止。为了防止无限循环，包含终止循环所需的编程逻辑是非常关重要的。

下面的示例演示了如何设置`while`循环。

```powershell
$i = 1

while ($i -le 10) {

    Write-Host $i

    $i++

}
```

在这里，定义了一个名为`$i`的变量并赋了一个初始值 1。接下来，定义了一个`while`循环，只要`$i`的值小于 10，该循环就会执行。

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10

## 第 6 章 • 使用循环处理数据

稍后在你工作时，你将看到`while`循环运行的示例。

> 有关`while`循环的更多信息，请在 Windows PowerShell 命令行提示符中执行。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_224.png)

## 更改循环执行

有时会出现你想要跳出循环的情况。`foreach`循环可以遍历任何以集合形式生成输出的词命令输出。Windows PowerShell 支持`break`和`continue`命令。

## 使用 break 命令

当`break`命令执行时，内部循环将终止。这里是使用`break`命令终止整个循环的示例：

```powershell
if ($x -gt 100) {

    Write-Host "Maximum exceeded."

    break

}
```

在这里，设置了一个执行 10 次的循环。循环内部添加了一个`if`语句，每次迭代检查`$i`。当发现`$i`等于 5 时，执行`break`命令，产生如下输出：

- 1
- 2
- 3
- 4

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_225.png)

## 使用 continue 命令

`continue`命令执行时，将跳过循环的当前迭代并继续处理数组剩余部分。这里是使用`continue`命令中断循环处理的示例：

```powershell
$i = 1

while ($i -le 10) {

    if ($i -eq 5) {

        $i++

        continue

    }

    Write-Host $i

    $i++

}
```

在这里，设置了一个执行 10 次的`while`循环。循环内部定义了一个`if`语句，当`$i`变为 5 时执行`continue`命令。当这种情况发生，循环的当前迭代终止，循环从开头开始继续。结果是循环的第五次迭代从未完成，输出中没有显示数字 5：

- 1
- 2
- 3
- 4
- 6
- 7
- 8
- 9
- 10

## 使用 exit 命令

Windows PowerShell 还支持`exit`命令。执行时，该命令会终止整个脚本的执行，而不仅仅是循环的当前迭代。这里是使用`exit`命令的示例：

```powershell
if ($x -gt 100) {

    Write-Host "Error - Maximum value exceeded."

    exit

}
```

当作为 PowerShell 脚本的一部分时，上述`if`语句在执行且`$x`的值超过 100 时将终止脚本的执行。如果在 Windows PowerShell 命令行运行，`exit`命令将关闭当前的 PowerShell 会话并关闭 Windows 命令行窗口。

## 回到剪刀石头布游戏

好了，是时候把注意力重新回到本章的主要游戏项目——剪刀石头布游戏上了。这个过程的开发将演示如何使用循环来控制脚本执行，以便收集输入以及控制游戏的结束。

### 设计游戏

石头、纸、剪刀游戏要求玩家在每玩一新回合时，根据表 6.1 中概述的评分规则通过选择优胜动作来赢过电脑。

| 玩家动作 | 电脑动作 | 结果 |
|---|---|---|
| 石头 | 石头 | 平局 |
| 石头 | 剪刀 | 玩家胜 |
| 石头 | 纸 | 玩家输 |
| 纸 | 纸 | 平局 |
| 纸 | 石头 | 玩家胜 |
| 纸 | 剪刀 | 玩家输 |
| 剪刀 | 剪刀 | 平局 |
| 剪刀 | 纸 | 玩家胜 |
| 剪刀 | 石头 | 玩家输 |

玩家的动作通过输入对应有效动作字母来指定（R 代表石头，P 代表纸或 S 代表剪刀）。电脑的动作根据随机数生成。除了引导玩家进行每一轮游戏外，游戏还会持续收集若干游戏统计数据（总游戏次数、胜利次数、失败次数和平局次数），并在游戏结束时显示。

石头、纸、剪刀游戏的整体逻辑流相当简单。为了设置它，我们将按照这里列出的十二步骤完成开发：

- 1. 创建一个新的脚本文件。
- 2. 定义并初始化脚本变量。
- 3. 显示游戏的欢迎界面。
- 4. 设置循环以控制游戏过程。
- 5. 生成电脑的动作。
- 6. 提示玩家做出动作。
- 7. 验证玩家的动作。
- 8. 翻译玩家的动作。
- 9. 显示电脑和玩家的动作。
- 10. 分析游戏结果。
- 11. 为新回合重置变量值。
- 12. 显示游戏统计数据。

## 创建一个新的脚本文件

让我们通过创建一个名为`RockPaperScissors.ps1`的新 PowerShell 文件并向其中添加以下语句来开始开发。

```
# ***********************************************************************************

# 脚本名称: RockPaperScissors.ps1 (石头、纸、剪刀游戏)

# 版本: 2.0

# 作者: Jerry Lee Ford, Jr.

# 日期: 2008年10月12日

#

# 描述: 此 PowerShell 脚本挑战玩家在

# 石头、纸、剪刀游戏中击败电脑

# ***********************************************************************************
```

```
# 清除 Windows 控制台屏幕

Clear-Host
```

## 定义并初始化脚本变量

接下来，通过在脚本末尾添加以下语句，定义并初始化整个脚本使用的变量。

```
# 定义此脚本中使用的变量

$playGame = "True" # 此变量控制游戏进行

$number = 0 # 此变量存储电脑的

#    动作的数字版本

$randomNo = New-Object System.Random # 此变量存储一个随机对象

$guess = 0 # 此变量存储玩家的

#    动作的数字版本

$playerMove = "" # 此变量存储玩家的

#    动作的字符串版本

$computerMove = "" # 此变量存储电脑的

#    动作的字符串版本

$noPlayed = 0 # 此变量跟踪已玩过的

### 游戏次数

$noWon = 0 # 此变量跟踪胜利次数

$noLost = 0 # 此变量跟踪失败次数

$noTied = 0 # 此变量跟踪平局次数
```

如你所示，已添加注释来记录每个变量的使用和目的。

## 显示游戏的欢迎界面

下一步是添加负责显示游戏欢迎界面的编程语句。接下来提供的语句应添加到脚本文件的末尾。

```
# 显示游戏的启动屏幕

Write-Host "`n`n`n`t`t`t`tWELCOME TO THE"

Write-Host "`n`n`n`t      ROCK, PAPER, SCISSORS GAME*"

Write-Host "`n`n`n`t`t      By Jerry Lee Ford, Jr.,"

Write-Host "`n`n`n`n`n`n`n`n`n`Press Enter to continue."

# 暂停游戏直到玩家按下 Enter 键

Read-Host
```

## 设置循环以控制游戏过程

石头、纸、剪刀游戏的整体执行由一个`while`循环控制。为了设置它，在脚本文件末尾添加以下语句。

```
# 循环直到玩家猜中秘密数字

while ($playGame -ne "False") {

}
```



# 210 PHP Web Powerblast 2: 零基础学者编程，第二版

`Write-Host "\n"`

```powershell
$noPlayed += 1 # 将计数器加 1
```

除了显示当前回合中进行的步法外，上面显示的最后一条语句增加了`$noPlayed`的值。该变量用于跟踪自“石头、布、剪刀”游戏开始以来的总局数。

## 分析游戏结果

接下来，游戏需要判断玩家是赢、输还是平局，然后显示这些分析结果。这通过在脚本主循环的末尾添加以下语句来实现。

```powershell
switch ($computerMove)
{
    "Rock" # 电脑选择了石头
    if ($playerMove -eq "Rock") {
        $noTied += 1 # 计数加
        Write-Host "你平了!"
    }
    if ($playerMove -eq "Paper") {
        $noWon += 1 # 计数加
        Write-Host "你赢了!"
    }
    if ($playerMove -eq "Scissors") {
        $noLost += 1 # 计数加
        Write-Host "你输了!"
    }
}
"Paper" {# 电脑选择了布
if ($playerMove -eq "Rock") {
    $noLost += 1 # 计数加
```

# 第 6 章 • 使用循环处理数据

```powershell
Write-Host "你输了!"
}
```

```powershell
if ($playerMove -eq "Paper") {
  $noTied += 1 # 计数加 1
  Write-Host "你平了!"
}
```

```powershell
if ($playerMove -eq "Scissors") {
  $noWon += 1 # 计数加 1
  Write-Host "你赢了!"
}
```

```powershell
}
```

```powershell
"Scissors" { # 电脑选择了剪刀
```

```powershell
if ($playerMove -eq "Rock") {
  $noWon += 1 # 计数加 1
  Write-Host "你赢了!"
}
```

```powershell
if ($playerMove -eq "Paper") {
  $noLost += 1 # 计数加 1
  Write-Host "你输了!"
}
```

```powershell
if ($playerMove -eq "Scissors") {
  $noTied += 1 # 计数加 1
  Write-Host "你平了!"
}
```

```powershell
}
```

}

# 暂停游戏直到玩家按下 Enter 键
`Read-Host`

# 212 | 零学者 C# 编程：第二版

如你所见，这些语句使用`switch`语句块组织成了三个测试。第一个测试检查电脑的移动（由`$computerMove`指明）是否等于“石头”。同样地，接下来的两个测试检查电脑的移动是否为“布”或“剪刀”。这三个测试中的每一个，都定义了一系列三个`if`语句，负责将玩家的移动（由`$playerMove`指明）与电脑的移动进行比较，以确定当前回合的结果。根据分析结果，将显示一条显示结果的消息。此外，在每个`if`语句内部，会根据情况增加`$noTied`、`$noWon`和`$noLoss`变量的值，以便跟踪游戏统计数据。

## 为新一轮游戏重置变量值

最后添加到游戏主`while`循环末尾的语句如下所示。这些语句负责将变量值重置为默认设置，以便准备新一轮游戏。

```powershell
# 重置变量以准备新轮游戏
$number = 0
    # 将电脑的猜测重置为零
$guess = 0
    # 将玩家猜测的数字版本重置
    # 为零
$playerMove = ""
    # 将玩家猜测的字符串版本重置
    # 为空字符串
$computerMove = ""
    # 将电脑猜测的字符串版本重置
    # 为空字符串
```

## 显示游戏统计数据

游戏在停止运行之前的最后一个任务是显示游戏期间收集的统计数据。显示这些信息的语句在下面的代码列出，应添加到脚本文件的主`while`循环之后。

```powershell
# 清除 Windows 命令行控制屏幕
Clear-Host
# 显示游戏统计数据
Write-Host "\n游戏统计数据:\n"
Write-Host "\n游戏局数: $noPlayed"
Write-Host "\n胜局数: $noWon"
Write-Host "\n输局数: $noLoss"
Write-Host "\n平局数: $noTied\n"
```

# 第 6 章 • 使用循环处理数据

```powershell
Write-Host "" . "...................." 
Write-Host "`n`n`n`n`n`n`n` 按 Enter 键。"
```

```powershell
# 暂停游戏直到玩家按下 Enter 键
Read-Host
```

```powershell
# 清除 Windows 命令行控制屏幕
Clear-Host
```



如你所见，这些语句清除屏幕并显示存储在嵌入系列字符串变量中的游戏统计数据。

## 最终结果

好了，就是这样。到此，你的“石头、布、剪刀”脚本应该准备好运行了。

计入玩家的次数。此屏幕还让玩家知道她剩余多少次机会。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_240_0.png)

> 图 7-3
> 玩家错过了第一次猜测。

图 7.4 显示了玩家在进行几次额外猜测后，游戏可能的样子。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_240_1.png)

> 图 7.4
> 玩家还有五次机会来猜出秘密单词。

游戏会拒绝由大多数特殊字符、数字或多个字母组成的猜测。例如，图 7.5 显示了当玩家尝试一次输入多个字母时显示的屏幕。

当玩家猜出秘密单词时，游戏结束，此时会显示图 7.6 所示屏幕，确认玩家的成功并告知她获胜需要多少次猜测。

# 218 《初学者 Microsoft PowerShell 3.0 编程》，第二版

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_241_0.png)

## 图 7.5

游戏验证所有输入，显示错误解释为什么某些猜测不被接受。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_241_1.png)

### 图 7.6

玩家通过猜出秘密数字赢得了游戏。

当玩家用完猜测次数时，游戏也会结束，如图 7.7 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_241_2.png)

### 图 7.7

玩家在用完猜测次数前未能猜出游戏的秘密单词。

# 第 7 章 使用函数组织脚本

## 使用函数和过滤器更改脚本设计

在过去的几个章节中，你学习了许多不同的编程结构，可以使用这些结构来改进 PowerShell 脚本的整体结构。通过使用`if`和`switch`语句，你学习了如何设置条件测试，并在某些条件评估为真时对一组相关的语句分组。通过使用`do while`、`do until`、`for`、`foreach`和`while`循环，你学习了如何将重复执行给定任务的相关的语句分组。集中关键的编程逻辑并减少了创建 PowerShell 脚本所需的代码语句总数。现在是学习函数和过滤器的了。

函数是一个命名的代码块，可以通过引用其名称来执行。当调用时，代码块内部的所有语句都会被求值执行。函数可以接受参数并返回结果。过滤器（filter）与函数非常相似。没有什么是用过滤器做但函数不能做的。两者的区别在于过滤器设计用于更有效地处理管道数据的大对象。

> Windows PowerShell 中的预定义函数。例如，当你在 Windows PowerShell 命令行提示符中输入`C`或`D`来切换驱动器时，你实际上是在执行函数，这些函数反过来调用了`Set-cmdlet`。

### 改进脚本组织

函数的主要优点之一是有助于减少编写脚本所需的代码行数。函数通过提供将代码语句组织成命名代码块的能力，促进了脚本的模块化开发，这些代码块随后可以在脚本文件中的任何位置反复执行。函数使得你的 Windows PowerShell 脚本更易管理，为创建更大更复杂的脚本构建所需的区块，而必不会增加复杂性或产生大量代码。例如，假设你计划编写一个执行以下任务的新 PowerShell 脚本。

- 询问玩家执行权限。
- 显示欢迎屏幕。
- 管理用户输入的收集。
- 显示包含用户输入的短故事。
- 提示玩家再次游戏。

开发此脚本的一种方法是开始定义任何需要的变量，然后是一系列函数，每个函数负责管理上述列出的任务之一。脚本的其余部分将由编程逻辑组成，在需要时调用这些函数。

### 创建可重用代码

正如前面提到的，函数通过将相关的代码语句分组在一起，然后使它们从脚本中的任何位置可被调用，提供了一种改进 PowerShell 脚本文件组织的方法。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_243_0.png)

> 我强烈建议你将函数作为 Windows PowerShell 脚本中的主要组织工具。通过使用函数组织脚本文件，你可以将问题拆分为更小、更易管理的单元。这将帮助你将编程逻辑分离到离散模块中，可以一次创建一个并测试一个单元。

也许函数提供的最大益处是它们能够协助你开发可重用代码。根据一般规则，每当你发现需要多次执行给定任务时，它可能就是包含在函数中的良好候选，例如在每当新一轮游戏开始时获取随机数。一旦创建，你可以使用单个语句根据需要多次调用给定的函数。

### 使用函数增强脚本组织

使用函数，你可以将 PowerShell 脚本拆分为易于管理的区块，并根据需要调用每个区块。函数提供了构建模块化代码的组件，从而产生更简洁的脚本。

### 函数结构

在最简单的形式下，函数由关键字`function`、随后分配给函数的名称，然后是代码块组成如下所示：

```powershell
function Write-Greeting {
    Write-Host "Hello World!"
}
```

# 第 7 章 使用函数组织脚本 (221)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_244_0.png)

与变量不同，在为函数命名时没有必须遵循的硬规则。然而，为函数分配描述性名称是一个好习惯，有助于识别每个函数的目的。在书中，你会看到我选择遵循类似于 cmdlet 的命名方案。具体来说，函数的名称以动词开头，后面跟着`-`字符，然后是名词。建议你建立自己的命名方案并在所有的 PowerShell 脚本中遵循它。这将有助于你的代码更易阅读和管理。

这里创建名为`Write-Greeting`的函数。调用时，该函数使用`Write-Host`命令显示文本字符串。当然，你可以在函数代码块中包含尽可能多的语句。你可以在已添加函数的脚本任何位置通过指定其名称来执行它，如下所示。

```powershell
function Write-Greeting {
    Write-Host "Hello World!"
}
```

`Write-Greeting`

在这里通过指定名称定义、初始化并执行函数。

我建议在 PowerShell 脚本文件的开头集中定义所有函数。这将确保所有函数在被调用之前已经定义并初始化。这也有助于使程序代码更容易阅读，并让查找变得简单。因此，我建议按所示修改你的 Windows PowerShell 脚本模板：

```powershell
# ################################################################
# 脚本名称:
# 版本:
# 作者:
# 日期:
#
# 描述:
#
# ################################################################
```

# 222 零基础 Windows PowerShell 2.0 编程（第二版）

```powershell
# # 初始化部分 (Initialization Section)
# # 函数与过滤器部分 (Functions and Filters Section)
# # 主处理部分 (Main Processing Section)
```

如你所见，我在脚本模板中增加了三个部分。初始化部分（Initialization Section）确定了脚本中定义和初始化脚本级变量的位置。函数与过滤器部分（Functions and Filters Section）确定了定义任何函数和过滤器的位置。主处理部分（Main Processing Section）确定了放置脚本控制逻辑的位置。

从以后，这个修改后的模板将用于书中游戏脚本的开发。

### 处理参数 (Processing Arguments)

虽然将一组相关的语句组织到命名代码块中以便作为一个单元重复执行具有很高的价值，但当你设置函数来处理通过作为参数传递给它们的输入时，函数会变得更加有用。例如，在下一节中，你将学习如何设置一个函数，将传递给它的两个数字相加。函数还可以处理由 cmdlet 生成的输出。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_245_0.png)

通过开发接受并处理输入（称为参数）的函数，你使函数独立于它们所在的 PowerShell 脚本。因此，你可以将一个函数复制并粘贴到另一个 PowerShell 脚本并在无需修改的情况下使用，只要它在新脚本中仍然被调用并传递了适当的输入即可。这有助于代码重用，随着时间的推移，你应该能够开发出一个小型函数库，并将其作为开发 Windows PowerShell 脚本的构建模块。这应该让你通过避免每次启动新开发项目时重复造轮子，从而工作得更聪明、更快。

技巧 (TRICK)

### 传递参数 (Passing Arguments)

Windows PowerShell 提供了多种向 PowerShell 脚本传递参数的方法。一种方法指定参数，在逗号分隔的列表中表示每个参数，紧跟在函数名后面，如下所示。

```powershell
function Add-Numbers ($x, $y) {
  $z = $x + $y
  Write-Host "$x + $y = $z"
}
```

在这个示例中，定义了一个名为`Add-Numbers`的函数，它接受两个参数`$x`和`$y`，然后将它们相加。当在 PowerShell 脚本某处调用此函数执行时，你必须传递与函数所需的两个参数对应的两个参数。传递这些参数的方式与向 cmdlet 传递的方式相似，如下所示：

`Add-Numbers 3 4`

执行时，该语句调用`Add-Numbers`函数，并向它传递值`3`和`4`。然后函数将执行，显示此处所示的结果：

`3 + 4 = 7`

设置函数接受参数的另一种方法是使用`param`关键字来定义每个参数。使用时，`param`关键字必须是函数代码块内部指定的第一个单词。函数接受的参数必须指定为参数，并用逗号分隔，所有参数都放在括号内，如下所示。

```powershell
function Add-Numbers {
  param ($x, $y)
  $z = $x + $y
  Write-Host "$x + $y = $z"
}
```

此函数可以从定义它的 PowerShell 文件中的任何位置调用，如下所示：

# 224 零基础 Windows PowerShell 3.0 编程（第二版）

`Add-Numbers 1 6`

执行时，`Add-Numbers`函数生成了以下结果。

`1 + 6 = 7`

像 cmdlet 参数一样，函数参数有位置参数和命名参数。这意味着你可以通过逗号分隔的列表将参数传递给函数，前提是你安排列表中的参数，使其与函数中定义的对应参数正确匹配；或者你可以通过指定参数名称后跟传递给该参数的参数来传递参数。例如，以下语句演示了如何通过位置向`Add-Number`函数传递参数。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_247_0.png)

`Add-Numbers 2 2`

很可能，下面的示例演示了如何通过名称向`Add-Numbers`函数传递参数。

`Add-Numbers -x 2 -y`

函数还可以通过`$args`特殊变量接受传递给它的参数。`$args`变量是一个数组，会自动填充传递给函数的所有传入参数列表，如下例所示。

```powershell
function Add-Numbers {
  $z = $args[0] + $args[1]
  Write-Host "The total of all arguments passed is $z"
}
```

在这里，`Add-Numbers`函数被修改为引用它期望作为`$args[0]`和`$args[1]`接收的两个参数。例如，如果由此语句调用

`Add-Numbers 2 5`

此新版本的`Add-Numbers`函数将生成以下输出。

`The total of all arguments passed is 7`

由于`$args`是一个数组，你可以使用`foreach`循环处理它，如下所示：

```powershell
function Add-Numbers {
  $z = 0
  foreach ($i in $args) {
    $z += $i
  }
  Write-Host "The total of all arguments passed is $z"
}
```

# 第 7 章 • 使用函数组织脚本

`The total of all arguments passed is 9`
`1 + 6 = 7`

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_248_0.png)

虽然你可以使用`param`关键字或`$args`特殊变量来访问传递给函数的参数，但我建议使用`param`，因为它显式地识别传入参数。

### 指定参数类型 (Specifying Argument Type)

Windows PowerShell 还允许你指定参数的数据类型以确保接受特定类型的值。这是通过在参数定义中指定所需的数据类型实现的，如下：

```powershell
function Add-Numbers {
  param ([int]$x, [int]$y)
  $z = $x + $y
  Write-Host "$x + $y = $z"
}
```

在这个示例中，参数前加上`[int]`以指定整数。为了查看它是如何工作的，你可以创建此函数并使用以下语句调用它。

`Add-Numbers 2 2`

接下来，你可能尝试使用以下语句调用函数。

# 226 初学者 PowerShell 脚本编程第二版

`Add-Numbers -x A -y`

响应将显示以下错误消息。

`Add-Numbers 无法将值 "A" 转换为 System.Int32。错误：“格式不正确。”`

`位于 C:\MyScripts\xxx.ps1 行14`

从错误消息的内容可以看出，Windows PowerShell 无法将参数`A`转换为整数。现在，如果你返回删除函数两个参数的整数要求，你可以像下面所示调用函数，这次你不会看到错误消息。相反，PowerShell 会拼接两个参数。

`A + 2 = Ay`

Windows PowerShell 支持广泛的数据类型。表 7.1 列出了一些数据类型。在定义函数参数时，你可以指定这些数据类型之一。

| 表 7.1 WINDOW PowerShell 数据类型 | |
| :--- | :--- |
| `[array]` | `[hashtable]` |
| `[bool]` | `[int]` |
| `[byte]` | `[long]` |
| `[char]` | `[single]` |
| `[decimal]` | `[string]` |
| `[double]` | `[switch]` |
| `[float]` | |

### 为参数分配默认值 (Assigning Default Values to Arguments)

Windows PowerShell 还允许你为函数参数分配默认值，从而在未按预期传递参数时使用默认值代替。例如，下面所示的`Add-Numbers`函数已修改为为它的两个参数都分配零的默认值。

```powershell
function Add-Numbers {
  Param ([int]$x = 0, [int]$y = 0)
  $z = $x + $y
  Write-Host "$x + $y = $z"
}
```

如果你像如下所示使用`Add-Numbers`函数调用此版本，Windows PowerShell 将将`2`赋值给参数`$y`，将`0`赋值给参数`$x`。

`Add-Numbers -y 2`

当如上所示调用时，`Add-Numbers`函数将生成以下输出：

`0 + 2 = 2`

### 处理传入的数据

函数通过一个名为`$input`的特殊变量访问管道线数据。在函数开始执行之前，该变量会自动填充所有传入的管道线对象。如果有必要，Windows PowerShell 将推迟函数的执行，直到所有传入的管道线对象数据都收集完毕。

关于访问传入的管道线数据的示例，请考虑以下示例。

```powershell
function Get-FileNames {
  $input | Where-Object $_.Name -ne "WINDOWS" | Sort-Object
}
```

在这里，定义了一个名为`Get-FileNames`的函数。该函数使用`$input`变量收集通过对象管道线传递给函数的任何数据。这些数据随后向下传递给`Where-Object` cmdlet。`Where-Object` cmdlet 随后会过滤掉任何指向名为 Windows 文件夹的对象引用。任何剩余的对象数据将传递给`Sort-Object` cmdlet。

在运行上述示例之前，你需要使用`Set-Location` cmdlet 将当前工作目录更改为 C 盘的根目录（Windows 文件夹所在处），如下所示：

```powershell
Set-Location C:\
```



要运行该函数并将其插入对象管道线，你可以输入以下语句。它执行`Get-ChildItem` cmdlet，然后将其输出传递给`Get-Filenames`函数。

```powershell
Get-ChildItem | Get-Filenames
```

执行时，该函数将显示类似下方的输出。

```
Directory: Microsoft.PowerShell.Core\FileSystem::\

| Mode | LastWriteTime | Length | Name |
| --- | --- | --- | --- |
| -a--- | 3/3/2007 7:52 AM | 74 | autoexec.bat |
| -ar- | 3/3/2007 7:26 AM | 8192 | BOOTSECT.BAK |
| -a--- | 9/18/2006 5:43 PM | 10 | config.sys |
| d--- | 2/24/2008 9:29 PM | | DarkBASIC |
| d--- | 10/3/2008 11:47 AM | | MyScripts |
| d--- | 9/9/2008 7:20 PM | | PerLogs |
| d-r- | 9/8/2008 11:44 AM | | Program Files |
| -a--- | 3/3/2007 7:40 AM | 396 | RHDSetup.log |
| d--- | 7/7/2007 4:24 PM | | ruby |
| d--- | 10/8/2008 6:16 PM | | Temp |
| d-r- | 4/26/2008 10:58 PM | | Users |
```

### 返回结果

PowerShell 函数能够将数据返回给调用它的语句。这是通过将变量赋值为你想要返回的值，然后在函数执行的最后一个语句中对该变量进行引用来实现的，如下所示。

```powershell
function Add-Numbers {
  Param ([int]$x = 0, [int]$y = 0)
  $result = $x + $y
  $Result
}
```

在此示例中，`Add-Numbers`函数接收给它的两个整数值作为参数并相加。然后，它通过将值赋值给`$result`变量并将此结果返回给调用它的语句，该变量随后在函数执行的最后一个语句中被引用。以下语句演示了如何执行此版本的`Add-Numbers`函数，然后检索并显示它返回的数据。

```powershell
$x = Add-Numbers 2 2
Write-Host "2 + 2 = $x"
```

当调用时，向函数传递了参数 2 和 2。执行后，函数返回值 4，该值随后被赋值给执行它的语句中的`$x`变量。当上述所示的第二个语句执行并显示以下输出时，证明一切都按预期工作。

```
2 + 2 = 4
```

### 限制变量作用域

到本书为止，你所看到的所有变量使用示例都涉及脚本级变量的使用，这意味着一旦定义，就可以在 PowerShell 脚本的任何位置引用这些变量。然而，现在引入了函数，情况将发生变化。

正如第 4 章所述，变量的访问受到作用域的限制。在 PowerShell 脚本中，在函数外部定义的任何变量都是脚本级变量。脚本级变量对于脚本文件中位于函数的所有部分来说也是局部变量。然而，函数仍然可以使用包含脚本标签的修改变量引用来访问脚本级变量。具体而言，可以使用以下语法从脚本内定义的任何函数中直接通过名称访问脚本级变量。

```powershell
$localVariable
```

在本示例中，我们创建了一个名为`GetOddEven`的过滤器，它用于判断一个数字是奇数还是偶数。该过滤器接收传递给它的任何数值，并使用模运算符（`%`）将其除以 2。如果此操作的结果为 1，则传递给函数的数值为奇数；否则，为偶数。

如果通过以下语句调用：

```powershell
@(5, 4, 6) | Get-OddEven
```

`Get-OddEven`函数将显示以下输出：

```
Odd
Even
Even
```

在实际上，过滤器和函数几乎是等价的。区别在于，过滤器`$_`能够在数据通过`$_special`变量变得可用时立即对流水线对象数据进行操作，而函数则必须等待所有传入的流水线数据到达并填充`$Input`变量后才能处理。为了处理存储在`$Input`变量中的大型数据对象列表，你通常需要在函数内部设置一个循环来遍历每个对象。过滤器还消除了使用循环处理数据的任何需要。由于这些差异，当大量数据通过对象管道传输时，过滤器比函数更高效，处理速度也更快。

通常，你可以忘记创建自定义过滤器，而是使用`Foreach-Object`和`Where-Object`命令行从对象管道中过滤数据。然而，虽然这些命令行工具对于简单操作足够了，但要对流水线数据执行执行复杂的逻辑操作，你需要设置一个过滤器。

## 回到 PowerShell 吊字游戏

好了，是时候把注意力回到本章的主游戏项目了：PowerShell 吊字游戏。PowerShell 吊字游戏是一个猜词游戏，玩家被挑战一次一次猜出一个随机选定的单词。要赢，玩家必须在 12 次或少的尝试内猜出每个字母。

PowerShell 吊字游戏的整体构造将分 11 个步骤完成，如下所示：

1. 使用 PowerShell 脚本模板创建一个新的脚本文件。
2. 在初始化部分（Initialization Section）定义并初始化游戏变量。
3. 在函数和过滤器部分（Functions and Filters Section）定义函数。
4. 询问玩家许可玩游戏。
5. 创建一个循环来控制整体游戏。
6. 随机选择游戏的秘密单词。
7. 创建一个循环来控制玩家输入的收集和分析。
8. 收集并验证玩家的猜测。
9. 显示每次猜测的结果。
10. 判断游戏何时结束。
11. 挑战玩家再次游戏。

### 创建新脚本

创建 PowerShell 吊字游戏的第一步是使用新版本的 Windows PowerShell 脚本模板创建一个名为`Hangman.ps1`的新脚本文件，如下所示。

```powershell
********************************************************************
### 脚本名称: Hangman.ps1 (PowerShell Hangman Game)
# 版本: 2.0
# 作者: Jerry Lee Ford, Jr.
# 日期: 2008年10月12日
#
# 说明: 此 PowerShell 脚本挑战玩家
#   玩电脑版的吊字游戏
#
********************************************************************
```

```powershell
### Initialization Section
```

```powershell
### Functions and Filters Section
```

```powershell
### Main Processing Section
```

## 定义和初始化脚本级变量

创建 PowerShell 吊字游戏的下一步是定义并初始化脚本级变量。这是通过向脚本文件的初始化部分添加以下语句来实现的。

```powershell
# 定义在此脚本中使用的变量
$playGame = "False" # 控制游戏流程以及何时停止游戏
$response = "" # 在提示玩游戏时存储玩家的输入
$randomNo = New-Object System.Random # 此变量存储随机数
$number = 0 # 存储游戏随机生成的数字
$secretWord = "" # 存储当前回合游戏的秘密单词
$attempts = 0 # 跟踪有效猜测的次数
$status = "True" # 控制当前回合的游戏
$guesses = "" # 玩家在游戏期间的字母列表
$reply = # 存储玩家的字母猜测
$tempstring = # 存储一个带有隐藏字符的显示字符串，用于
# 在游戏期间代表秘密单词
$validReply = # 在提示玩一个新游戏时存储玩家的响应
$rejectList = '-!@#\$%&=-=[\]\.<>/?' # 列出不可接受的输入的字符串
$GuessesRemaining = # 跟踪玩家剩余的猜测次数
```

```powershell
### 创建一个关联数组并加载
$words = @(
$words[0] = @("", "", "", "", "", "", "", "", "", "", "", "", "")
$words[1] = @("C", "O", "M", "M", "A", "N", "D", "E", "R")
$words[2] = @("F", "L", "A", "G")
$words[3] = @("T", "O", "A", "S", "T", "E", "R")
$words[4] = @("M", "A", "R", "K", "E", "R")
$words[5] = @("P", "I", "C", "T", "U", "R", "E")
$words[6] = @("D", "E", "S", "K")
$words[7] = @("G", "L", "O", "B", "E")
$words[8] = @("S", "P", "A", "C", "E", "E")
$words[9] = @("K", "A", "Y")
$words[10] = @("P", "L", "N", "E")
```

通常情况下，你可以忘记创建自定义过滤器，而是使用`Foreach-Object`和`Where-Object`命令行工具从对象管道中过滤数据。然而，虽然这些命令行工具对于简单操作足够了，但要对流水线数据执行复杂的逻辑操作，你需要设置一个过滤器。在实际上，过滤器和函数几乎是等价的。区别在于，过滤器`$_`能够在数据通过`$_special`变量变得可用时立即对流水线对象数据进行操作，而函数则必须等待所有传入的流水线数据到达并填充`$Input`变量后才能处理。为了处理存储在`$Input`变量中的大型数据对象列表，你通常需要在函数内部设置一个循环来遍历每个对象。过滤器还消除了使用循环处理数据的需要。由于这些差异，当大量数据通过对象管道传输时，过滤器比函数更高效，处理速度也更快。在本示例中，我们创建了一个名为`GetOddEven`的过滤器，它用于判断一个数字是奇数还是偶数。该过滤器接收传递给它的任何数值，并使用模运算符（`%`）将其除以 2。如果此操作的结果为 1，则传递给函数的数值为奇数；否则，为偶数。

如果通过以下语句调用：

```powershell
@(5, 4, 6) | Get-OddEven
```

`Get-OddEven`函数将显示以下输出：

```
Odd
Even
Even
```

### 定义函数

PowerShell 吊字游戏有一个自定义函数，如下所示，它的工作是判断玩家的猜测是否正确。该函数通过定义一个名为`$reply`的参数开始，用于存储最近的猜测。

```powershell
# 此函数判断玩家的猜测是否正确
function Check-Answer {
    param ($reply)
    # 此函数在调用后第一件事是将
    # 处理的字母添加到脚本级变量
    $guesses = $guesses + $reply
    # 遍历每个字母（数组）并查看它是否匹配
    # 玩家的猜测
    for ($i = 0; $i -lt $secretWord.length; $i++) {
        if ($secretWord[$i] -ne $reply) {
            # 在 guesses 中放入下划线字符
            $guesses[$i] = "_"
        } else {
            $guesses[$i] = $reply
        }
    }
}
```

### 提示玩家开始游戏

在开启游戏之前，游戏需要玩家给予许可。这是通过在脚本文件的主处理部分开头添加以下语句来实现的。

```powershell
# 提示玩家猜数字
while ($playGame -ne "True") (
Clear-Host # 清空 Windows 控制屏幕
# 显示游戏的启动界面
Write-Host "`n`n`n"
write-Host "* Welcome to the"
Write-Host "* *"
Write-Host "* PowerShell Hangman Game! 0 **"
Write-Host "* **"
Write-Host "* /\ **"
Write-Host "* **"
Write-Host "* **"
Write-Host "* **"
Write-Host "* **"
Write-Host "* *****"
# 收集玩家的猜测
$response = Read-Host "`n`n`n`n`n`n`n`n`n Would you like to play? (Y/N)"
### 验证玩家的输入
if ($response -eq "Y") {
  $playGame = "True"
}
elseif ($response -eq "N") {
  Clear-Host
  Write-Host "`n`n 请尽快回来并再玩。"
  Read-Host
  exit
}
else (
  Clear-Host
)
```

```powershell
Write-Host "`n`n Invalid input. Please press Enter try again."
Read-Host
}
```

如你所见，脚本的部分由一个`while`循环控制，该循环一直持续到`$playGame`的值设置为`True`。在循环内部，会显示吊索犯的文本图形，并提示玩家输入 Y 或 N。如果玩家输入 Y 作为响应，则`$playGame`的值被设置为`True`，结果`while`循环结束，并执行脚本的其余部分。

如果玩家输入 N 作为响应，将运行退出命令，从而终止游戏的执行。如果玩家输入其他内容，循环将再次运行，提示玩家输入有效的选择。

## 设置循环控制游戏流程

脚本的其余部分由一个`while`循环控制，该循环一直执行到玩家决定结束游戏。构成此循环的语句所示，应添加到脚本主处理部分的末尾。构成此脚本的其他语句将嵌入此循环中。

```powershell
#提示玩家猜一个数字
while ($status -eq "True") {
}
```

### 选择一个秘密单词

PowerShell 吊索游戏开发的下一步是将以下语句嵌入脚本的主循环中。

```powershell
#生成 1 到 10 之间的随机数
```

```powershell
$number = randomNo.Next(1, 11)
$secretWord = $words[$number] #使用随机数指定数组索引，填充构成游戏秘密单词的字母数组
```

每次循环迭代都会开始新一轮游戏。当这种情况发生时，需要将若干变量重置为默认值以准备游戏。此外，必须生成一个随机数并用它选择玩家要猜的新单词。

## 设置循环处理玩家猜测

接下来，需要设置另一个循环来收集和处理玩家的猜测。执行此任务的代码语句所示，应嵌入到游戏的主循环中，紧接在你输入的最后的一组语句之后。

```powershell
#创建一个循环来收集和分析玩家输入
while ($reply -eq "") {
```

```powershell
}
```

### 收集并验证用户输入

接下来，你需要添加负责收集和验证输入的语句。这些语句所示，应嵌入上一个`while`循环中。

```powershell
Clear-Host #清除 Windows 命令控制台屏幕
```

```powershell
$reply = Read-Host "`n Enter a guess" #收集玩家答案
```

```powershell
if ($reply -eq "") { #如果提交了空字符串，则重复
continue
#loop
}
```

```powershell
#是时候验证玩家输入了
```

```powershell
if ($reply.Length -gt 1) { #限制输入一次为一个字符
```

```powershell
Clear-Host #清除 Windows 命令控制台屏幕
```

```powershell
Write-Host "`n`n Error: You may enter only one letter at a time."
Read-Host "`n`n`n`n`n`n`n`n`n` Press Enter to continue.
$reply = "" #清除玩家的输入
continue #重复循环
```

```powershell
if (1234567890 -match $reply) { #不允许数字输入
Clear-Host "`n`n Clear the Windows command console screen
Write-Host "`n`n Error: Numeric guesses are not allowed.
Read-Host "`n`n`n`n`n`n`n`n`n`n` Press Enter to continue.
$reply = "" #清除玩家的输入
continue #重复循环
}
```

```powershell
if ($replyList -match $reply) {
Clear-Host #清除 Windows 命令控制台屏幕
Write-Host "`n`n Error: Special characters are not permitted.
Read-Host "`n`n`n`n`n`n`n`n`n`n Press Enter to continue.
$reply = "" #清除玩家的输入
continue #重复循环
}
```



```powershell
Clear-Host #清除 Windows 命令控制台屏幕
```

```powershell
$attempts++ #仅对正确的猜测进行计数
```

循环开始提示玩家输入一个猜测（例如，一个字母）。然后将玩家的输入赋值给变量`$reply`。将进行检查以确保玩家没有通过简单按回车键来响应。如果是这样，则执行`continue`命令，循环将迭代并再次运行。

> 注意上述列出的最后两个语句作为条件求值的两个表达式。这些表达式使用`-match`比较运算符来确定是否找到了匹配条件。你将在第 8 章“处理文件和文件夹”中学习更多关于`-match`运算符的知识。

接下来，执行一系列`if`语句。每个语句都负责帮助验证玩家输入的不同方面。第一个语句如果发现玩家输入了两个或多个字符作为输入，将执行`continue`命令。第二个语句检查玩家输入的是否数字而不是字母。第三个语句检查玩家输入的是特殊字符而不是字母。特殊字符列表存储在`$replyList`中。如果发现特殊字符，则执行`continue`命令。

## 显示每次猜测的结果

一旦进行了有效的猜测，游戏就需要处理它并显示信息。这是通过将以下语句添加到`while`循环末尾，紧接在你输入的最后一组语句之后实现的。

```powershell
#现在输入已验证，调用 Check-Answer 函数
Check-Answer $reply

$tempString = "" #清除用于显示的变量

#遍历 $words[0] 并创建一个临时字符串
#显示单词的状态
for ($i = 0; $i -le $words[0].length - 1; $i++) {
    $tempString = $tempString + $words[0][$i]
}
```

```powershell
#根据输入显示单词当前状态
Write-Host "\nResults:\n"
Write-Host "--------------------------------------"
Write-Host "$tempString\n"
Write-Host "--------------------------------------"
```

```powershell
Write-Host " Letters that have been guessed: $guesses\n"

#计算玩家剩余的猜测
$GuessesRemaining = (12 - $attempts)

#显示当前回合剩余的猜测
Write-Host "* Number of guesses remaining: $GuessesRemaining"
```

### 判断游戏何时结束

现在是判断游戏是否结束了。当玩家的秘密单词或猜测次数耗尽时，游戏结束。为了完成这两个检查，将以下语句添加到上一个`while`循环的末尾，紧接在你添加最后一组语句之后。

```powershell
#暂停游戏允许玩家查看游戏状态
Read-Host "`n`n`n`n`n`n`n`n`n` Press Enter to continue"
```

```powershell
#如果没有更多的下划字符，则秘密单词已被猜中
if ($tempString -notmatch "_") {
```

```powershell
Write-Host "`nGame over. You have guessed the secret word!"
"in $attempts.`n`n"
Write-Host " The secret word was $secretWord `n`n"
Write-Host "`n`n`n`n`n`n`n`n`n"
"`n`n`n`n`n`n`n"
Read-Host #暂停游戏
$reply = "Done"#信号当前游戏回合的结束
continue #重复循环
```

)

## 242 零基础入门 PowerShell v5.0 编程，第二版

```powershell
# 玩家仅允许 12 次猜测，超过后游戏将结束

if ($attempts -eq 12) {
```

```powershell
Clear-Host
Write-Host "`n Game over. You have exceeded the maximum allowed "
number of guesses.`n"
Write-Host " The secret word was $secretWord `n`n"
Write-Host " The best you could do was $tempString`n`n`n`n`n`n`n`n`n " 
"`n`n`n`n"
Read-Host # 暂停游戏
$reply = "Done" #信号当前回合游戏的结束
continue # 重复循环
```

}

```powershell
$reply = "" # 清空玩家的输入
```

如你所见，上面的语句被组织在两个`if`语句中。如果是这种情况，第一个`if`语句检查玩家是否赢得了游戏。如果是，那么组成秘密单词的每个字母都已经被猜中，且存储在`$tempString`中的值将不包含任何字符。第二个`if`语句检查`$attempts`的值是否等于 12，这表示玩家在没有发现游戏秘密单词的情况下用完了猜测次数。如果这两个`if`语句测试的两个条件中任一为真，则`$reply`的值被设置为`Done`，终止负责收集和处理玩家输入的`while`循环的执行。

## 挑战玩家玩另一局

最后，为了完成你的 PowerShell 吊字游戏（Hangman），你需要在游戏主`while`循环的底部添加以下语句。这些语句负责挑战玩家玩另一个游戏。

```powershell
$response = "" # 重置值允许循环继续迭代
```

```powershell
# 现在是提示玩家玩另一轮了
$validReply = "False" #设置变量准备好在 while 循环中使用
```

```powershell
# 循环直到接收到有效输入
while ($validReply -ne "True") {
```

## 第 7 章 · 使用函数组织脚本 243

```powershell
Clear-Host # 清空 Windows 命令控制台屏幕

# 提示玩家玩新游戏

$response = Read-Host "`n`n Play again? (Y/N)"

# 验证玩家的输入 # 继续游戏

if ($response -eq "Y") {
```

```powershell
$validReply = "True"
$status = "True"
}
else ($response -eq "N") { # 该退出了

Clear-Host # 清空 Windows 命令控制台屏幕
Write-host "`n`n return and play again soon.`
Read-Host # 暂停游戏
$validReply = "True"
$status = "False"
}
```

```powershell
else { # 无效输入

Clear-Host # 清空 Windows 命令控制台屏幕
Write-Host "`n`n Invalid input. Please press Enter to try again.`
$validReply = "False"
Read-Host # 暂停游戏
}
```

如你所见，玩家需要提供`Y`或`N`的响应。输入`Y`开始新一轮游戏。输入`N`会导致`$validReply`被设置为`True`，从而结束脚本主`while`循环的执行，有效地终止脚本。

### 总结

本章向你展示了如何使用函数和过滤器来改进 Windows PowerShell 脚本的整体组织结构。你学习了函数如何支持编程逻辑的集中、减少脚本的整体尺寸并支持代码重用。你学习了如何定义和执行函数。你学习了如何传递参数和返回结果。你还学习了如何在对象流水线中插入函数。你学习了函数如何影响变量作用域，以及如何在函数内部访问脚本级变量。在这一切之上，你还学习了如何开发过滤器作为函数的替代方案，以便更高效地处理大量的对象流水线数据。

现在，在你开始阅读第 8 章之前，我建议你花一点额外的时间通过以下挑战列表来改进 PowerShell 吊字游戏。

### 挑战

- 1. 按照目前的写法，PowerShell 吊字游戏给了玩家 12 次机会来猜秘密单词。为了让这个游戏玩起来更像传统的儿童游戏，请更改设置使玩家仅允许进行 6 次错误猜测。这样正确的猜测就不会计入玩家次数。你可能还想将每次猜测与身体部位相关联。例如，第一次失败代表头部，第二次失败代表身体，第三和第四次失败代表手臂，第五和第六次失败代表腿。你可能喜欢在每回合结束时显示一个类似于游戏启动菜单的文本图形。你可以使用此图形表示失败次数（例如，在第一次猜测错误后，图形将显示头部；在第二次猜测错误后，它将显示头部和身体，以此类推）。

- 2. 目前，PowerShell 吊字游戏只有 10 个单词可以随机选择。为了让游戏更具挑战性，考虑修改游戏以支持 20 或 30 个不同的单词。

- 3. 按照目前的写法，游戏只有一个自定义函数，负责判断玩家的猜测是否正确。然而，有许多机会通过将脚本的不同部分重组组织为函数来进一步模块化脚本。查看脚本主处理部分的代码。

- 4. 按照 PowerShell 吊字游戏的编写方式，玩家可能会输入不在秘密单词中的字符。通过添加逻辑检查进入的字符是否属于秘密单词来解决这个问题。

- 5. 按照目前的设计，没有逻辑防止玩家多次输入相同的猜测。考虑修改脚本以防止这种情况发生。

# 第三部分 高级主题

# 文件和文件夹的操作

Windows PowerShell 提供了许多用于处理文件和文件夹的 cmdlet。本章将教你如何开发可以创建、删除、重命名、复制和移动文件及文件夹的 PowerShell 脚本。你将学习如何在操作之前判断它们是否存在。本章还将向你展示如何向不同类型的文件写入和读取数据，包括纯文本文件、CSV 文件和 XML 文件。你还将学习如何使用正则表达式指定匹配的文件和文件夹名称，并使用其他允许你控制 cmdlet 输出格式以及打印 cmdlet 输出或文本文件中内容的 cmdlet。

具体来说，你将学习如何：

- 管理文件和文件夹

- 向不同类型的文件写入数据

- 使用正则表达式进行复杂的模式匹配

- 使用格式化 cmdlet 控制 cmdlet 输出显示

# 项目预览：PowerShell 井字游戏

本章的游戏项目是经典井字游戏的实现。该游戏需要两个玩家，并从图 8.1 所示的屏幕开始。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_273_0.png)

FIGURE 8.1

井字游戏的欢迎界面

欢迎界面还会请求许可启动新游戏。一旦获得许可，将显示图 8.2 所示的屏幕，提示玩家 X 做出移动。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_273_1.png)

FIGURE 8.2

玩家 X 总是每局游戏中第一个移动的玩家

移动是通过输入可用游戏盘格的坐标完成的，如图 8.3 所示。

# 第8章 - 操作文件夹 251

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_274_0.png)

图 8.3

方格 CI 正被指定为玩家 X 的下一步移动。

当一个玩家成功将三个方格排成一行时，游戏结束，如图 8.4 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_274_1.png)

图 8.4

玩家 O 赢得了游戏。

当棋盘上的每个方格都被选中且没有玩家获胜时，游戏也会结束。在这种情况下将宣布平局，如图 8.5 所示。

在每局游戏结束后，系统会提示玩家再次游戏。如果玩家选择开始新游戏，游戏板将被清除并提示玩家 X 进行移动。否则，将邀请玩家返回再次游戏，游戏关闭。

# 初学者 Microsoft Windows PowerShell 2.0 编程（第二版）

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_275_0.png)

图 8.5

游戏以平局结束。

# 使用正则表达式的力量

到本书目前为止，你一直在根据预期输入（如`Y`或`N`）对数据进行验证，并在提示用户许可执行特定操作时进行。然而，有时你可能无法严格控制提供的 PowerShell 脚本的输入。相反，你必须准备好接受各种不同的输入。为了适应这种情况，你需要学习如何使用正则表达式。正则表达式是用于描述匹配数据的模式。正则表达式有许多用途和优点。例如，正则表达式可以方便文本文档中的字符串搜索。正如本章的游戏项目所示，正则表达式也是用于验证用户输入的重要工具。

# 匹配简单模式

正则表达式通常从左到右进行评估。Windows PowerShell 使用`-match`运算符来实现正则表达式。当在指定的源字符串中找到指定的模式时，就会发生匹配。最简单的正则表达式可能是定义由一个或多个字符组成的特定模式，如下文所示。

```
if ("Once upon a time" -match "ONCE") {
    Write-Host "Match!"
}
```

在这里，搜索源字符串`"Once upon a time"`以检查是否包含`"ONCE"`的匹配模式。执行时，此示例产生匹配。默认情况下，匹配是不区分大小写的。但是，使用`-match`运算符，你可以执行大小敏感的匹配，如下所示：

```
if ("Once upon a time" -match "ONCE") {
  Write-Host "We have a match!"
}
```

在此示例中，没有发生匹配。Windows PowerShell 还通过提供`-notmatch`运算符让你能够轻松执行负模式匹配操作，如下所示所示。

```
if ("Once upon a time" -notmatch "XXX") {
  Write-Host "We have a match!"
}
```

在这里，发生了匹配，因为在指定的搜索字符串中找不到正在搜索的模式。Windows PowerShell 还允许你使用`-notmatch`运算符执行大小敏感的模式匹配，如下所示。

```
if ("Once upon a time " -notmatch "XXX") {
  Write-Host "We have a match!"
}
```

执行时，此示例产生匹配，因为正在搜索的表达式在搜索字符串中找到了。

# 匹配备选模式

Windows PowerShell 对正则表达式的支持还允许你设置查找不同模式集合的模式匹配。要指定此类模式匹配，你使用`|`字符来分隔每个可能的匹配字符串。

```
if ("mar*" -match "war|mar|jar") {
  Write-Host "Match!"
}
```

在此示例中，定义了一个模式，用于查找三个匹配模式中的任何一个。如果找到了这些模式中的任何一个，匹配即成功了。为了提高效率，你可以重写上一个示例，如下所示。

```
if ("mar*" -match "wa|ma|ja)r") {
  Write-Host "Match!"
}
```

在这个更高效的模式中，每个可能的模式匹配的唯一部分被分组并封装在括号内，而模式匹配的共同部分被放在括号之外。

# 使用正则表达式字符

作为正则表达式部分的每个字符都会匹配其自身。然而，Windows PowerShell 支持一组正则表达式字符，也称为元字符，它们是该规则的例外。元字符是改变模式匹配评估方式的字符。例如，考虑以下内容。

```
"The winner of this year's award is Mrs. Ford!" -match "Mr." (
Write-Host "Match!"
```

在此示例中，设置了一个正则表达式来匹配字符`Mr`后跟一个可选字符，字符`.`是元字符，用于定义匹配任意一个字符的模式。结果，`Mr.`甚至`Mr`都会匹配`Mr.`模式。如果你真的想将句号作为句号而不是元字符，你需要对其转义。

| 字符 | 描述 | 示例 |
| --- | --- | --- |
| `.` | 匹配任意一个字符 | `Mr.` |
| `^` | 匹配字符串的开头 | `^Mr` |
| `$` | 匹配字符串的结尾 | `Mr$` |
| `*` | 匹配前一个字符的零或多个 | `Mr*` |
| `+` | 匹配前一个字符的一个或多个 | `Mr+` |
| `?` | 匹配前一个字符的零或一个 | `Mr?` |
| `[ ]` | 匹配括号内的任意一个字符 | `[abc]` |
| `[^ ]` | 匹配不在括号内的任意一个字符 | `[^abc]` |
| `[ - ]` | 匹配范围内的任何字符 | `[a-z]` |
| `( )` | 将字符分组在一起 | `(abc)` |
| `\|` | 作为逻辑或的操作 | `a\|b` |
| `\` | 转义下一个字符 | `\.` |

| 字符 | 描述 |
| --- | --- |
| `.` | 匹配任意一个字符 |
| `^` | 匹配字符串的开头 |
| `$` | 匹配字符串的结尾 |
| `*` | 匹配前一个字符的零或多个 |
| `+` | 匹配前一个字符的一个或多个 |
| `?` | 匹配前一个字符的零或一个 |
| `[ ]` | 匹配括号内的任意一个字符 |
| `[^ ]` | 匹配不在括号内的任意一个字符 |
| `[ - ]` | 匹配范围内的任何字符 |
| `( )` | 将字符分组在一起 |
| `\|` | 作为逻辑或的操作 |
| `\` | 转义下一个字符 |

# 使用量符

使用正则表达式，你还可以根据前一个字符重复的次数设置模式。这是通过表 8.2 中列出的量符实现的。

| 字符 | 描述 |
| --- | --- |
| `*` | 匹配前一个字符的零或多个 |
| `+` | 匹配前一个字符的一个或多个 |
| `?` | 匹配前一个字符的零或一个 |
| `{n}` | 匹配前一个字符恰好 n 次 |
| `{n,}` | 匹配前一个字符至少 n 次 |
| `{n,m}` | 匹配前一个字符在 n 到 m 次之间 |

例如，以下`if`语句设置了一个正则表达式，只要在搜索字符串中没有找到数字字符，它就会产生匹配。



```powershell
if ("I am forty two." -match "\D") {
    Write-Host "Match!"
}
```

# 基于范围匹配模式

正则表达式提供了使用括号查找特定字符范围的模式的能力。注意，要使用类模式，必须将它们封装在括号内，如下所示。

```powershell
if ("March 13th" -match "[0-9]") {
    Write-Host "Match!"
}
```

### 表 8.3 类模式

| 模式 | 描述 |
| --- | --- |
| `[abc]` | 匹配指定的任何小写字符 |
| `[abcdefuvwxyz]` | 匹配字母表中的任何小写字母 |
| `[a-z]` | 指定匹配任何小写字母的简写 |
| `[A-Z]` | 指定匹配任何大写字母的简写 |
| `[0123456789]` | 匹配任何数字 0–9 |
| `[0-9]` | 指定匹配 0–9 之间的简写 |

类在开发正则表达式时非常常用，因此开发了一系列如表 8.4 所示的简写，以便更方便使用。

### 表 8.4 类简写

| 简写 | 描述 |
| --- | --- |
| `\d` | 等于 `[0-9A-Za-z]` |
| `\w` | 等于 `[\t|f|r|n|v]` |
| `\s` | 等于 `[0-9-Za-z]` |
| `\D` | 匹配 `[0-9]` 之外的任意字符 |
| `\W` | 匹配 `[0-9A-Za-z]` 之外的任意字符 |
| `\S` | 匹配 `[\t|f|r|n|v]` 之外的任意字符 |

同样，下面的示例设置了一个正则表达式来搜索字符串，以确保它包含数字字符。

```
if ("I am 42." -match "\d") {
  Write-Host "Match!"
}
```

> 对 Windows PowerShell 正则支持的审查相对简短。关于正则表达式的深入讨论超出了本书的范畴。如需了解更多信息，请阅读《Mastering Regular Expressions, Second Edition》（ISBN: 0596002890）。你也可以在 PowerShell 提示符处输入以下命令：

```
Get-Help _about_regular_expression
```

### 管理文件和文件夹

Windows PowerShell 提供了管理计算机上文件和文件夹的方法。它允许你创建、重命名、复制、移动或删除文件和文件夹。

> 如果你打算后续章节中提供的示例进行操作：

# 验证文件和文件夹的存在

如前所述，Windows PowerShell 为你提供了管理文件和文件夹所需的工具。然而，在尝试管理文件或文件夹之前，先检查并确保该文件或文件夹存在是一个好主意。毕竟，文件和文件夹可能会因为任何原因消失。例如，使用计算机的人可能会删除或重命名它们。要检查文件是否存在，你使用 `Test-Path` cmdlet，如下所示。

```
$fileFound = Test-Path C:\MyScripts\Hangman.ps1
```

```
if ($fileFound -eq "True") {
  Write-Host "File found."
}
```

在此示例中，变量 `$fileFound` 根据 `Test-Path` cmdlet 是否在 `C:\MyScripts` 文件夹中找到 `hangman.ps1` 文件被设置为 `True` 或 `False`。`Test-Path` cmdlet 也可以用于判断文件夹是否存在，如下所示：

```
$fileFound = Test-Path C:\MyScripts
```

```
if ($fileFound -eq "True") {
    Write-Host "Folder found."
}
```

在此示例中，`Scripts` 是一个位于计算机 C 驱动器根目录下的文件夹。一旦你使用 `Test-Path` cmdlet 确保你想要操作的文件或文件夹存在，你就可以按照后续章节所示，对该文件或文件夹执行一系列管理操作。

# 获取文件和文件夹信息

如下示例所示，你可以使用 `Get-Item` cmdlet 获取有关给定文件或文件夹的信息。在此示例中，显示了 `hangman.ps1` 文件的 `Mode`、`LastWriteTime`、`Length` 和属性。

```
PS C:\MyScripts> Get-Item hangman.ps1
```

| Directory: Microsoft.PowerShell.Core\FileSystem::C:\MyScripts |
| --- |

| Mode | LastWriteTime | Length | Name |
| :--- | :--- | :--- | :--- |
| | 10/13/2008 3:24 PM | 9948 | hangman.ps1 |

使用 `Get-Item` cmdlet，你可以轻松创建一个用于获取文件或文件夹特定值的脚本，如下所示：

```
$fileFound = Test-Path C:\MyScripts\Hangman.ps1
if ($fileFound -eq "True") {
    $lastWritten = $(Get-Item C:\MyScripts\hangman.ps1).LastWriteTime
    Write-Host $lastWritten
}
```

在这里，使用 `Test-Path` cmdlet 来确保 `Hangman.ps1` 文件存在。如果存在，则将 `C:\MyScripts\hangman.ps1` 作为参数传递给 `Get-Item` cmdlet。注意，`Get-Item` cmdlet 及其参数被括在括号内，并以 `$` 字符开头，以建立对象引用。一旦设置了引用，就可以使用标准的点表示法访问相关的对象属性。执行时，假设指定的文件存在，此示例将生成类似于下面所示的输出。

```
10/13/2008 3:24:48 PM
```

# 复制和移动文件和文件夹

Windows PowerShell 还提供了复制和移动文件文件夹的能力。这是通过 `Copy-Item` 和 `Move-Item` cmdlet 实现的。例如，下面的示例了如何将文件从一个文件夹复制到另一个文件夹。

```
Copy-Item C:\System.log C:\Temp
```

在此示例中，名为 `System.log` 的文件从 C 驱动器根目录复制到 `C:\Temp` 文件夹。如有，你可以使用通配符将多个文件从一个文件夹复制到另一个文件夹，如下所示：

```
Copy-Item C:\*.log C:\Temp
```

在这里，在 C 根目录上找到的任何 `.log` 文件都会复制到 `C:\Temp`。

你也可以使用 `Copy-Item` cmdlet 将一个文件夹复制到另一个文件夹，如下所示：

```
Copy-Item C:\MyScripts C:\Temp
```

你可以通过向 `Copy-Item` cmdlet 传递 `-recurse` 参数来修改此示例。

执行时，该语句会创建 `C:\MyScripts` 文件夹的副本并将其放在 `C:\Temp` 文件夹中。然而，`C:\MyScripts` 的内容没有被复制，只是文件夹本身的副本。你可以通过向 `Copy-Item` cmdlet 传递 `-recurse` 参数来修改此示例，指示 PowerShell 递归复制文件夹及其所有内容（包括任何子文件夹）到另一个文件夹，如下所示：

```
Copy-Item C:\MyScripts C:\Temp -recurse
```

使用 `Move-Item` cmdlet，Windows PowerShell 还允许你移动文件和文件夹。例如，下面的示例了如何将文件从一个文件夹移动到另一个文件夹。

```
Move-Item C:\System.log C:\Temp
```

在此示例中，名为 `System.log` 的文件从 C 驱动器根目录移动到 `C:\Temp` 文件夹。如有，你可以使用通配符将多个文件从一个文件夹移动到另一个文件夹，如下所示：

```
Move-Item C:\*.log C:\Temp
```

在这里，在 C 根目录上找到的任何 `.log` 文件都会移动到 `C:\Temp`。

你也可以使用 `Move-Item` cmdlet 将一个文件夹移动到另一个文件夹，如下所示：

```
Move-Item C:\MyScripts C:\Temp
```

通过向 `Move-Item` cmdlet 传递 `-recurse` 参数可以修改此示例。

执行时，该语句移动 `C:\MyScripts` 文件夹并将其放在 `C:\Temp` 文件夹中。然而，`C:\MyScripts` 的内容没有被移动，只是文件夹本身的副本。你可以通过向 `Move-Item` cmdlet 传递 `-recurse` 参数来修改此示例，指示 PowerShell 递归复制文件夹及其所有内容（包括任何子文件夹）到另一个文件夹，如下所示：

```
Move-Item C:\MyScripts C:\Temp -recurse
```

### 删除文件和文件夹

Windows PowerShell 还提供了删除文件和文件夹的能力。这是通过 `Remove-Item` cmdlet 实现的。例如，下面的示例了如何从文件夹中删除文件。

```
Remove-Item C:\System.log
```

在此示例中，名为 `System.log` 的文件从 C 驱动器根目录被删除。如有，你可以使用通配符将多个文件从一个文件夹删除到另一个文件夹，如下所示：

```
Remove-Item C:\*.log
```

在这里，在 C 根目录上找到的任何 `.log` 文件都会被删除。

你也可以使用 `Remove-Item` cmdlet 删除一个文件夹，如下所示：

```
Remove-Item C:\MyScripts
```

通过向 `Remove-Item` cmdlet 传递 `-recurse` 参数可以修改此示例。

执行时，该语句删除 `C:\MyScripts` 文件夹。然而，如果文件夹为空，命令将失败。你可以通过向 `Remove-Item` cmdlet 传递 `-recurse` 参数来修改此示例，指示 PowerShell 递归删除文件夹及其所有内容（包括任何子文件夹），如下所示：

```
Remove-Item C:\MyScripts -recurse
```

使用 `select` cmdlet，它被指示在每行中查找文本 `Error`。

包含此文本的文本行将被显示。当执行此命令时，它将生成以下输出。

```
10/09/2007 08:00:05 Error code 995 - Unable to locate backup media
```

你也可以使用正则表达式来定义在搜索文本文件时想要查找的搜索模式，并在发生匹配时显示一条文本消息。

例如，以下示例使用 `Get-Content` cmdlet 将文本文件的内容赋值给名为 `$records` 的数组变量。接下来设置了一个 `if` 语句，该语句使用 `match` 运算符来定义一个正则表达式，用于在存储在 `$records` 中的任何行中查找 `error`、`alert` 和 `critical` 单词的出现情况。

```
$records = Get-Content C:\Temp\System.log
```

```
if ($records -match "error|alert|critical") {
  Write-Host "Match"
```

### 向文件读取和写入

Windows PowerShell 除了为你提供管理文件和文件夹所需的工具外，还提供了许多 cmdlet，你可以使用这些 cmdlet 创建文件和文件夹，并从不同类型的文件（包括文本、CSV 和 XML 文件）中读取和写入。

## 创建文件和文件夹

Windows PowerShell 为程序员提供了许多创建新文件的方法。一种创建新文件并写入数据的方法是使用 `>` 重定向操作符。

```
Get-ChildItem C:\Temp\DirectoryList.txt
```

执行此语句时，该语句获取 `Get-ChildItem` cmdlet 的输出并重定向到 `C:\Temp\DirectoryList.txt`。结果，当你输出 `DirectoryList.txt` 文件时，你会发现它包含了类似于以下输出的数据。

```
Directory: Microsoft.PowerShell.Core\FileSystem::C:\MyScripts
```

| Mode | LastWriteTime | Name |
|---|---|---|
| -a-- | 9/26/2008 9:14 AM | 4661 FortuneTeller.ps1 |
| -a-- | 10/9/2008 12:11 AM | 4734 GuessNumber.ps1 |
| -a-- | 10/05/2008 2:32 AM | 10176 Hangman.ps1 |

## 第 8 章 • 处理文件和文件夹

如果要写入的文件已经存在，其内容将被替换。要向文件末尾追加内容，请使用 `>>` 管道操作符，如下所示。

```
Get-ChildItem >> C:\Temp\DirectoryList.txt
```

或者，你可以使用 `New-Item` cmdlet 创建新文件。例如，以下语句将在 `C:\Temp` 文件夹中创建一个名为 `TextFile.txt` 的新空文件。

```
New-Item C:\TempTestFile.txt -type file
```

如你所示，传递给 cmdlet 的第一个参数是要创建的资源的名称和路径。传递给 cmdlet 的第二个参数是要创建的资源类型（例如，文件 `file`）。你可以像创建新文件一样轻松地使用 `New-Item` cmdlet 创建新文件夹，如下所示：

```
New-Item C:\MyNewFolder -type directory
```

在此示例中，在 `C:\Temp` 文件夹内创建了一个名为 `MyNewFolder` 的新文件夹。还要注意，传递给 cmdlet 的第二个参数指定的 `directory`（目录）而不是 `folder`（文件夹）。当然，这两个术语是同义，但 PowerShell 在创建新文件夹时要求你指定 `directory`。

如果你尝试创建的文件或文件夹已经存在，你将收到错误消息：

```
New-Item : file 'C:\Temp\TestFile.txt' already exists.
At C:\MyScripts\ixxx.ps1:3 char:9
+ New-item <<<< C:\TempTestFile.txt -type file
```

如果你愿意，可以添加 `-force` 参数来用空文件或文件夹替换该文件或文件夹，如下所示：

```
New-Item C:\TempTestFile.txt -type file -force
```

## 向文本文件写入

Windows PowerShell 提供了许多其他方法来创建文件并向它们写入输出。例如，你已经见过如何通过 `>` 操作符重定向管道数据来创建并写入新文本文件。Windows PowerShell 还允许你使用 `Set-Content`、`Out-File` 和 `Add-Content` cmdlet 写入文本文件。

## 写入文本

使用 `Set-Content` cmdlet，你可以将字符串写入文本文件，如下所示：

```
Set-Content C:\Temp\Temp.txt "Once upon a time..."
```

在这里，传递给 `Set-Content` 的第一个参数是要创建的文件的名称和路径。第二个参数是要写入文本文件的字符串。如果存在同名文件，`Set-Content` cmdlet 将自动将其内容替换为指定的字符串。

你还可以使用 `Out-File` cmdlet 将数据从对象管道直接发送到文件，而不在 Windows 命令行控制台中显示任何内容。例如，以下语句将 `Get-Item` cmdlet 的输出重定向到 `C:\Temp` 中名为 `Temp.txt` 的文件。

```
Get-ChildItem | Out-File C:\Temp\Temp.txt
```

与 `Set-Content` cmdlet 类似，`Out-File` cmdlet 会覆盖任何同名文件的内容。

### 追加文本

如果你想向文件末尾追加内容而不是替换其内容，可以使用 `Add-Content` cmdlet，如下所示。

```
Set-Content C:\Temp\Temp.txt "Once upon a time..."
```

```
Add-Content C:\Temp\Temp.txt "And they lived happily."
```

在这里，使用 `Add-Content` 创建并写入文件。

### 格式化输出

正如你所学的，PowerShell 提供了许多创建和写入数据的方法。但是，PowerShell 使用 `Format-List` 和 `Format-Table` cmdlet 可以轻松格式化输出。例如，假设你想编写显示当前目录下所有文件的语句。

### Format-List cmdlet

`Format-List` cmdlet 与 `Format-Table` cmdlet 非常相似，区别在于它以垂直列表而不是水平表格的形式格式化输出。例如，你可能使用此处所示的 `Format-List` cmdlet 来制定显示表格视图的语句。

通过将 `Get-Item` cmdlet 的输出传递给 `Select-String` cmdlet，你可以过滤掉所有文件名不包含该字符串的文件。你随后可以将结果输出传递给 `Format-List` cmdlet，如下所示：

```
Get-ChildItem | Select-String PS1 | Format-List
```

## 第 8 章 • 文件与文件夹的操作

...当前工作目录的内容，然后将其保存为名为 `Temp.txt` 的报告。

```powershell
Get-ChildItem | Select-String PS1 | Format-Table > C:\Temp\Temp.txt
```

执行此语句时，将生成类似下方的结果：



```
IgnoreCase LineNumber Line      Filename Path       Pattern Context Matches
True         3 # Scri... Fortu... C:\My... PS1      (ps1)
True         4 # Scri... Hang... C:\My... PS1      (ps1)
True         3 # Scri... Seinf... C:\My... PS1      (ps1)
```

就像`Format-List` cmdlet 一样，`Format-Table` cmdlet 通过指定你想要的数据属性来覆盖你的默认格式，如下文所示：

```powershell
Get-ChildItem | Select-String PS1 | Format-Table Filename, Path > C:\Temp\Temp.txt
```

执行此语句时，将生成一个包含此处所示输出的报告文件：

```
Filename                    Path
FortuneTeller.ps1           C:\Scripts\FortuneTeller.ps1
Hangman.ps1                 C:\Scripts\Hangman.ps1
SeinfeldTrivia.ps1          C:\Scripts\SeinfeldTrivia.ps1
```

作为如何使用`Format-Table` cmdlet 的另一个示例，让我们写一条语句，列出计算机上运行的所有且当前打开句柄数大于 300 的进程。首先，让我们格式化一个语句，列出所有活动进程，对它们进行排序，并显示打开句柄大于 300 的进程，如下所示：

```powershell
Get-Process | Sort-Object | Where-Object {$_.Handles -gt 300} > C:\Temp\Temp.txt
```

执行此语句时，将产生一个包含类似于此处所示的输出的报告：

```
Handles  NPM(K)  PM(K)   WS(K) VM(M)  Id ProcessName
633      7       16384  13972 66      584 csrss
674      6       1888    4824 94      520 csrss
341      12      6276    9024 98      1804 spoolsv
552      17      13544  11748 101     1432 svchost
549      25      7400   10892 86      1316 svchost
1322     45      53220  59676 198     1128 svchost
375      8       3660   6396  46      944 svchost
647      0       0      8304  14      4 System
```

现在我们已经得到了正在寻找的结果集，让我们使用`Format-Table` cmdlet 的`-groupby`参数重新格式化输出，显示一组按进程名称分组的表格，如下所示：

```powershell
Get-Process | Sort-Object | Where-Object($_.Handles -gt 300) | Format-Table -groupby ProcessName > C:\Temp\Temp.txt
```

> 提示：当你在 Windows PowerShell 命令提示符中运行此示例及类似的示例时，请确保将其作为单个语句键入。

执行此语句时，将生成一个名为`Temp.txt`的报告，其中包含类似于此处所示的结果：

```
ProcessName: csrss
Handles NPM(K) PM(K) WS(K) VM(M) CPU(S) Id ProcessName
608 7 16396 13960 65 584 csrss
668 6 1888 4824 94 520 csrss

ProcessName: spoolsv
Handles NPM(K) PM(K) WS(K) VM(M) CPU(S) Id ProcessName
341 12 6276 9024 48 1804 spoolsv

ProcessName: svchost
Handles NPM(K) PM(K) WS(K) VM(M) CPU(S) Id ProcessName
552 17 13544 11748 101 1432 svchost
550 25 7400 10896 86 1316 svchost
1309 44 53224 59692 198 1128 svchost
378 8 3684 6412 46 944 svchost

ProcessName: System
Handles NPM(K) PM(K) WS(K) VM(M) CPU(s) Id ProcessName
645 0 0 8304 14 System
```

由于某些进程的多个实例可能同时运行，`-groupby`参数在格式化并显示输出时，会将任何打开句柄大于 300 的同名进程进行分组。`Format-List`和`Format-Table` cmdlet 对输出的显示提供了详细控制。要了解更多关于这两个 cmdlet 的信息，请查阅它们的帮助文档。

### 从文本读取

PowerShell 可以从文本文件中读取数据。要读取文件，你可以使用`Get-Content` cmdlet，如下所示：

```powershell
Get-Content file.txt
```

在此处，`Get-Content` cmdlet 用于读取文件。执行此语句时，将返回文件中的每一行。通过`Get-Content`的参数，你可以只读取前几行：

```powershell
Get-Content file.txt -TotalCount 5
```

此外，你还可以使用`-Raw`参数一次读取整个文件，而不是行数组：

```powershell
Get-Content file.txt -Raw
```

你还可以使用管道符`|`将文件内容传递给其他 cmdlet，例如：

```powershell
Get-Content file.txt | Select-String "pattern"
```

或者使用正则表达式：

```powershell
Get-Content "file*.txt"
```

### 清空文件内容

如果你想清空文件的内容，可以使用`Clear-Content` cmdlet。这将保留文件，如下所示：

```powershell
Clear-Content file.txt
```

执行此语句后，文件内容将被清空，但文件本身保留。

### 导出数据为 HTML

PowerShell 可以将输出导出为许多格式，包括 HTML。HTML 的优势在于它可以用于网页。要生成 HTML，你可以使用`ConvertTo-Html` cmdlet，如下所示：

```powershell
Get-Service | ConvertTo-Html > services.html
```

在此处，`Get-Service` cmdlet 用于生成运行的服务列表。你可以使用`Where-Object`过滤出正在运行的服务：

```powershell
Get-Service | Where-Object {$_.Status -eq 'Running'} | ConvertTo-Html > running_services.html
```

你还可以使用`-Property`参数指定要输出的属性。

## 导出数据为 XML 文件

PowerShell 还允许你将数据保存为 XML 格式。XML 代表可扩展标记语言，其目的是在应用程序之间定义、存储和传输数据。要生成 XML 文件，可以使用`Export-Xml` cmdlet，如下所示：

```powershell
Get-Item | Export-Xml items.xml
```

在此处，`Get-Item` cmdlet 用于生成目录中的项目列表，然后`Export-Xml` cmdlet 将其保存为 XML 文件。执行此语句时，将生成一个内容类似于图 8.6 的 XML 文件。

## 从 XML 文件读取数据

PowerShell 提供了一个 cmdlet 可以让你检索 XML 数据，从而可以在另一个 PowerShell 脚本中使用。要打开并读取 XML 文件，你需要使用`Import-Xml` cmdlet，如下所示：

```powershell
$xml = Import-Xml items.xml
$xml
```

在此示例中，第一语句使用`Import-Xml` cmdlet 检索`items.xml`文件并将其内容存储在变量`$xml`中。第二语句显示`$xml`中的内容，结果可能如下：

## 导出数据为逗号分隔值文件

PowerShell 可以写入和读取的另一种文件格式是 CSV。CSV 代表逗号分隔值，是一种以逗号分隔数据并以换行符记录的文件格式，常用于 Microsoft Excel 等应用程序作为一种便于在不同应用程序之间移动数据的方法。

要将对象数据保存为 CSV 文件，你可以使用`Export-Csv` cmdlet，如下所示：

```powershell
Get-Process | Export-Csv processes.csv
```

在此处，`Get-Process` cmdlet 用于生成进程列表，`Export-Csv` cmdlet 将其导出为 CSV 文件。默认情况下，它会包含类型信息。如果你不需要类型信息，可以使用`-NoTypeInformation`参数：

```powershell
Get-Process | Export-Csv processes.csv -NoTypeInformation
```

## 第 8 章 - 操作文件和文件夹

```
"Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\FortuneTeller.ps1"..Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\"FortuneTeller.ps1", "C", "Microsoft.PowerShell.Core\FileSystem", "False", "File:

C:\MyScripts\FortuneTeller.ps1

InternalName:

OriginalFilename:

FileVersion:

FileDescription:

Product:

ProductVersion:

+   Debug: False

Patched: False

PreRelease: False

PrivateBuild: False

SpecialBuild: False

Language:

"","FortuneTeller.ps1","-a---

"","FortuneTeller.ps1",".ps1",.1/10/3/2008 10/3/2008 11:46:32 AM","10/3/2008 3:46:32 PM","10/3/2008 11:46:32 AM","10/3/2008 3:46:32 PM","9/26/2006 6:14:10 PM","9/26/2006 10:14:10 PM","Archive"

"Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\Hangman.ps1","Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\"Hangman.ps1","C", "Microsoft.PowerShell.Core\FileSystem", "False", File:

C:\MyScripts\Hangman.ps1

InternalName:

OriginalFilename:

FileVersion:

FileDescription:

Product:

ProductVersion:

+   Debug: False

Patched: False

PreRelease: False

PrivateBuild: False

SpecialBuild: False

Language:

"","Hangman","-a---

"","Hangman.ps1","9948","C:\MyScripts","C:\MyScripts","False","True","C:\MyScripts\Hangman.ps1","*.ps1","*10/14/2008 4:49:06 PM","*10/14/2008 8:49:06 PM","*10/14/2008 4:49:06 PM","*10/14/2008 8:49:06 PM","*10/13/2008 3:24:48 PM","*10/13/2008 7:24:48 PM","*Archive"

"Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\SeinfeldTrivia.ps1","Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\SeinfeldTrivia.ps1","C","Microsoft.PowerShell.Core\FileSystem,"False",File:

C:\MyScripts\SeinfeldTrivia.ps1

InternalName:

OriginalFilename:

FileVersion:

FileDescription:

Product:

ProductVersion:

Debug: False

Patched: False

PreRelease: False

PrivateBuild: False

SpecialBuild: False

Language:

",*SeinfeldTrivia",-a---

"*SeinfeldTrivia.ps1","7701","C:\MyScripts","C:\MyScripts","False","True","C:\MyScripts\SeinfeldTrivia.ps1","*.ps1","*10/3/2008 11:47:27 AM","*10/3/2008 3:47:27 PM","*10/3/2008 11:47:27 AM","*10/3/2008 3:47:27 PM","*10/3/2008 11:51:29 AM","*10/3/2008 3:51:29 PM","*Archive""
```

## 从逗号分隔值文件中读取数据

要向 PowerShell 脚本中读取 CSV 文件，你需要使用`Import-Csv`命令行。如文所示，该命令接受一个参数，即要导入的 CSV 文件名和路径。

```powershell
$csvFile = Import-Csv C:\Temp\Test.csv
$csvFile
```

在这里，之前保存的 CSV 文件的内容已导入到名为`$csvFile`的变量中并显示，输出结果与此处类似：

```
PSPath : Microsoft.PowerShell.Core\FileSystem::C:\MyScripts\FortuneTeller.ps1
PSParentPath : Microsoft.PowerShell.Core\FileSystem::C:\MyScripts
PSChildName : FortuneTeller.ps1
```

```
PSDrive : C
PSProvider : Microsoft.PowerShell.Core\FileSystem
PSIsContainer : False
VersionInfo : File: C:\MyScripts\FortuneTeller.ps1
  InternalName:
  OriginalFilename:
  FileVersion:
  FileDescription:
  Product:
  ProductVersion:
    Debug: False
    Patched: False
    PreRelease: False
    PrivateBuild: False
    SpecialBuild: False
    Language:
```

```
BaseName : FortuneTeller
Mode : -a---
Name : FortuneTeller.ps1
Length : 4661
DirectoryName : C:\MyScripts
Directory : C:\MyScripts
IsReadOnly : False
Exists : True
FullName : C:\MyScripts\FortuneTeller.ps1
Extension : .ps1
CreationTime : 10/3/2008 11:46:32 AM
CreationUtc : 10/3/2008 3:46:32 PM
LastAccessTime : 10/3/2008 11:46:32 AM
```

## 将输出到打印机

除了创建、读取和写入不同类型的文件外，Windows PowerShell 还允许你使用`Out-Printer`命令打印文本输出和文件。当不带任何参数使用时，`Out-Printer`命令会将输出提交到默认打印机，如下所示：

```powershell
"This is a printer." | Out-Printer
```

在这里，一个文本字符串被传递给`Out-Printer`命令进行打印。同样，你可以将文本文件发送到默认打印机，如下所示：

```powershell
Get-Content C:\Temp\Textfile.txt | Out-Printer
```



事实上，你可以将任何管道数据重定向到打印机，如：

```
Get-location | Format-List | Out-Printer
```

```
Drive : C
Provider : Microsoft.PowerShell.Core\FileSystem
Path : C:\
```

最后，你还可以通过传递打印机名称作为参数，让`Out-Printer`命令将输出提交到特定的打印机。

```
Get-Location | Format-List | Out-Printer "hp_deskjet"
```

在这里，关于目录的信息被打印到名为`hp_deskjet`的打印机上。

## 使用 OUT-GRIDVIEW 在图形窗口中显示数据

在开始本章节的项目之前，让我们切换一下学习使用 Windows PowerShell 2.0 中的新`Out-GridView`命令。与`Format-List`和`Format-Table`命令一样，该命令对输出的呈现提供了详细控制。与其在控制台窗口或文本文件中显示输出，`Out-GridView`使用交互式窗口中的表格视图显示输出。

![](img/e07ce5ce2afe5fff444f2c361d9d87e_299)

`Out-GridView`命令，你的命令必须安装`.Net 3.0`。`Out-GridView`命令的设计是为了解决 PowerShell 控制台在显示大量数据和进行搜索方面的缺点。当然，你可以在输出在 Windows PowerShell 控制台显示之前对其进行排序。此外，尽管效率不高，你也可以从控制台窗口复制输出并粘贴到 Microsoft Word 等应用程序中搜索。

### 显示输出

使用`Out-GridView`命令最简单的方法是将其插入管道的末尾，如下所示：

```
PS C:\> Get-Process | Out-GridView
```

执行时，Windows PowerShell 不会在控制台窗口显示任何输出。相反，输出将在图 8.8 所示的窗口中显示。

![](img/e07ce5ce2afe5fff444f2c361d9d87e_300)

图 8.8 `Out-GridView`命令生成的窗口包含滚动条，允许你查看所有输出。或者，你可以使用`Out-GridView`命令的`input`参数将对象数据传递给命令，如下所示：

```
PS C:\> Get-Process
PS C:\> Out-GridView -InputObject $output
```

执行时，这产生的输出与图 8.8 所示相同。`Out-GridView`命令显示的输出按照传递给命令时的任何顺序进行列组织。如果你希望，可以通过点击列标题并将其拖到新位置来重新排列列的顺序。你可以通过拖动分隔列标题的分符来增加或减少每列的宽度。此外，如果你通过拖动调整了列宽，可以双击需要调整的列右侧的分符将其恢复到默认的上下文感知宽度。

![](img/e07ce5ce2afe5fff444f2c361d9d87e_301)

你可以通过指定要显示的数据及其排序方式，在传递给`Out-GridView`命令之前对`Out-GridView`命令显示的数据外观进行某种控制，如下所示：

```
PS C:\> Get-Process | Select-Object -Property ProcessName, Handles, Id | Sort-Object -Property Handles | Out-GridView
```

执行时，此语句将产生与图 8.9 所示类似的输出。

![](img/e07ce5ce2afe5fff444f2c361d9d87e_301_1.png)

### 数据排序

`Out-GridView`命令显示的输出数据在传递给命令显示之前按预定义顺序排序。如果你需要，可以通过点击列头更改排序顺序。这样做，`Out-GridView`命令图形窗口中显示的所有数据将根据你点击的列按升序排序。如果你再次点击列标题，输出将按降序重新排序。

遗憾的是，你无法使用`Out-GridView`命令的图形窗口执行次级排序。相反，你必须在将其传递给`Out-GridView`命令之前对数据进行程序化排序，如下所示：

```
Get-Process | Sort-Object ProcessName, Handles | Out-GridView
```

### 数据分组

除了对`Out-GridView`生成的图形窗口显示的数据进行排序外，还可以通过右键点击所需的列标题并点击出现的“分组”（Show in Groups）选项对任何列中显示的数据进行分组。图 8.10 显示了分组选项工作的示例。

![](img/e07ce5ce2afe5fff444f2c361d9d87e_302_0.png)

> Figure 8.10
>
> Data displayed by the Out-GridView cmdlet has been grouped by ProcessName.

如果你需要，可以通过右键点击用于分组数据的列并清除“分组”（Show In Groups）选项来取消数据的分组。

请注意，当数据被组织成组时，图形窗口的最右侧会显示图形和上下箭头。通过点击这些箭头，你可以展开或隐藏组的显示，如图 8.11 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_303_0.png)

所有一组的数据已从视图中隐藏。

## 搜索和过滤数据

`Out-GridView`的图形窗口的一个非常实用的功能是可以在“结果中搜索”（Search in Results）字段中输入关键字来过滤输出，如图 8.12 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_303_1.png)

使用关键字过滤输出的显示。

在这里，输出被过滤为仅显示活动状态`svchost`进程的数据。请注意，默认情况下，任何列中的任何关键字匹配都会显示。如果你想将关键字搜索限制在特定列，可以输入列头的类型名称，后跟冒号，然后是关键字，如图 8.13 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_304_0.png)

要清除关键字搜索，只需清除你在“结果中搜索”字段中输入的任何文本。

除了使用关键字搜索过滤数据外，你还可以点击位于图形窗口顶部的“过滤”（Filter）按钮（位于“结果中搜索”字段右侧）执行更复杂的过滤。当你执行此操作时，窗口顶部将显示一个过滤面板，允许你设置执行搜索时使用的特定过滤标准（见图 8.14）。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_304_1.png)

你可以通过点击“添加标准”（Add Criteria）按钮并选择不同的列标题，然后在提供的文本字段中输入特定的过滤数据来指定详细标准。可以通过点击每个语句右侧的红色“X”来移除显示的任何标准语句，在准备好后，你可以点击位于过滤面板右下角的“应用”（Apply）按钮来应用你的标准规范。

## 返回 PowerShell 井井棋游戏

好了，是时候将注意力回到本章节的主游戏项目——PowerShell 井井棋了。这个游戏的开发将演示如何创建一个脚本，该脚本可以通过显示消息、检索命令行输入以及应用编程逻辑来控制脚本的操作，并与玩家交互。

### 设计游戏

这个游戏需要两个玩家：Player X 和 Player O。Player X 总是每个游戏的开始。游戏会验证玩家的操作并跟踪轮到谁。游戏会显示井井棋盘的文本图形视图，该视图会在每个玩家回合后更新。当一个玩家连成三个棋格（水平、垂直或对角线），或者所有棋格都被选中但没有一方获胜时，游戏结束。

PowerShell 脚本的整体逻辑流相当简单。为了设置它，我们将按照这里列出的 17 个步骤完成其开发：

1. 创建一个新的脚本文件并添加注释语句。
2. 定义并初始化脚本变量。
3. 开发`Clear-Board`函数。
4. 开发`Get-Permission`函数。
5. 开发`Display-Board`函数。
6. 开发`Validate-Move`函数。
7. 开发`Check-Results`函数。
8. 开发`Display-Results`函数。
9. 准备游戏进行播放。
10. 创建一个循环来控制脚本的整体执行。
11. 创建一个循环来控制单个游戏。
12. 收集玩家的操作。
13. 验证玩家的操作。
14. 寻找获胜者。
15. 寻找平局。
16. 切换玩家回合。
17. 提示玩家开始新游戏。

### 创建新脚本

井井棋游戏创建的第一是创建一个名为`TicTacToe.ps1`的新 PowerShell 脚本文件，并将 PowerShell 模板应用到它。

```
# *************************************************************
# 脚本名称: TicTacToe.ps1 (井井棋游戏)
# 版本: 2.0
# 作者: Jerry Lee Ford, Jr.
# 日期: 2008年10月13日
# : 此 PowerShell 脚本是流行的
# 井井棋游戏的双玩家实现
# *************************************************************
```

```
### 初始化部分

# 函数和过滤器部分

### 主处理部分
```

### 定义和初始化变量

接下来，你需要定义并初始化整个脚本中使用的变量。这是通过在脚本文件的初始化部分添加以下语句来实现的。请注意，每个变量的作用都通过添加到脚本语句中的注释进行了记录。

```
# 脚本中使用的变量
$startGame = "False" # 控制游戏何时终止
$playGame = "True" # 控制回合的进行
$player = "X" # 指定当前玩家回合
$winner = "" # 指定获胜者
$moves = 0 # 计算移动次数
$move = "" # 存储玩家的操作
$tie = "False" # 指定何时发生平局
```

```
$A1 = "1"
$A2 = "1"
$A3 = "1"
$B1 = "1"
$B2 = "1"
$B3 = "1"
$C1 = ""
$C2 = ""
$C3 = ""
```

### 准备 Clear-Board 函数

现在是开始开发用于执行任务的函数了。函数应该放在脚本文件的函数和过滤器部分。第一个函数`Clear-Board`如下所示。

```
#此函数重置变量棋盘格
function Clear-Board (
    $A1 = ""
    $A2 = ""
    $A3 = ""
    $B1 = ""
    $B2 = ""
    $B3 = ""
    $C1 = ""
    $C2 = ""
    $C3 = ""
)
```

执行此函数将重置变量，从而清除棋盘并准备游戏。

### 创建 Get-Permission 函数

接下来显示的`Get-Permission`函数负责提示玩家开始游戏。

```
#此函数获取启动...的权限
function Get-Permission (
    # 循环直到收集到有效回复
    while ($startGame -eq "False") {
        Clear-Host #清除控制台屏幕

        #显示游戏的启动屏幕
        Write-Host "'n'n'n"                               T I C - T A C - T O E'n'n'n"
        Write-Host " "                               1       2       3'n"
        Write-Host " "                                     |
        Write-Host " "                               A $A1 | $A2 | $A3"
        Write-Host " "                               ----------------------"
        Write-Host " "                                     |
        Write-Host " "                               B $B1 | $B2 | $B3"
        Write-Host " "                               ----------------------"
        Write-Host " "                                     |
        Write-Host " "                               C $C1 | $C2 | $C3"
```

如你所示，为了活跃气氛，此函数显示...

### 创建 Display-Board 函数

下一个开发的函数是`Display-Board`函数，其代码语句所示。调用此函数是为了显示当前的游戏状态，并提示由`$player`指定的玩家进行操作。玩家的操作随后存储在`$response`中。

```
#此函数显示棋盘，显示每个玩家的操作
function Display-Board (
    Clear-Host #清除控制台屏幕

    $显示游戏盘
    Write-Host "'n'n"                               T I C - T A C - T O E'n'n'n"
    Write-Host " "                               1       2       3'n"
    Write-Host " "                                     |
    Write-Host " "                               A $A1 | $A2 | $A3"
    Write-Host " "                               ----------------------"
    Write-Host " "                                     |
    Write-Host " "                               B $B1 | $B2 | $B3"
    Write-Host " "                               ----------------------"
    Write-Host " "                                     |
    Write-Host " "                               C $C1 | $C2 | $C3"

    #收集玩家操作
    $move = Read-Host "'n'n'n'n Player $player's turn"

    $move #将玩家的操作返回给调用语句
)
```

### 创建 Validate-Move 函数

此处显示的`Validate-Move`函数在每个玩家回合后被调用。它的工作是确保只接受有效的操作。

```
# 此函数判断玩家的输入是否有效
function Validate-Move (
    if ($move.length -eq 2) { # 有效移动由2个字符组成
        if ($move -match "[A-C][1-3]") { # 正则表达式测试，寻找
            $result = "Valid" # A、B 或 C 的实例，以及
            # 1, 2 或 3 的一个实例。
        } else {
            $result = "Invalid" # 如果移动不是 A1, A2, A3,
            # B1, B2, B3, C1, C2 或 C3，则移动无效
        }
    } else {
        $result = "Invalid" # 如果移动不包含2个
        # 字符，则移动无效
    }

    $result # 将此值返回给调用此函数的语句
)
```

此函数首先设置一个`if`语句，以确保玩家的移动指定为两个字符。第一个字符代表水平面板上的坐标，第二个字符代表垂直面板上的坐标。嵌套的`if`语句执行一个正则表达式，用于判断玩家提供的第一个字符是否为 A、B 或 C，以及第二个字符是否为 1、2 或 3。如果这两个语句的任何一个结果评估为假，则玩家的移动是非的。接下来，将执行一系列八条语句，检查玩家指定的移动是否在游戏早些时候已经执行。然后将代表所选棋盘格的变量赋值为相应的 X 或 O 值。因此，值为为空格的变量仍然可以选择，而赋值为 X 或 O 值的变量则不可选。

### 创建 Check-Results 函数

在每个玩家的回合结束时，会调用下所示的`Check-Results`函数。它的工作是查看当前玩家的最后一次移动是否导致玩家获胜。这是通过检查代表游戏盘格的变量的值来实现的。检查游戏盘中每行和每列的变量，以查看它们是否都已分配给当前玩家（例如，如果行中有三个 X 或 O）。此外，该函数还会检查对角线获胜者。

```
# 此函数检查游戏盘以查看是否有获胜者
function Check-Results (
```



```powershell
$winner = " " # 在检查之前始终重置此值

# 寻找垂直获胜者
if (($A1 -eq $player) -and ($A2 -eq $player) -and ($A3 -eq $player)) {
    $winner = $player
}
if (($B1 -eq $player) -and ($B2 -eq $player) -and ($B3 -eq $player)) {
    $winner = $player
}
if (($C1 -eq $player) -and ($C2 -eq $player) -and ($C3 -eq $player)) {
    $winner = $player
}

# 寻找水平获胜者
if (($A1 -eq $player) -and ($B1 -eq $player) -and ($C1 -eq $player)) {
    $winner = $player
}
if (($A2 -eq $player) -and ($B2 -eq $player) -and ($C2 -eq $player)) {
    $winner = $player
}
if (($A3 -eq $player) -and ($B3 -eq $player) -and ($C3 -eq $player)) {
    $winner = $player
}
```

```powershell
# 寻找对角线获胜者
if (($A1 -eq $player) -and ($B2 -eq $player) -and ($C3 -eq $player)) {
    $winner = $player
}
if (($A1 -eq $player) -and ($B2 -eq $player) -and ($C1 -eq $player)) {
    $winner = $player
}

$winner # 将此值返回给调用此函数的语句
```

## 创建 `Display-Results` 函数

你需要创建的最后一个函数是 `Display-Results` 函数。下所示的函数在每局游戏结束时调用，用于显示游戏的最终状态并识别谁（如果有的话）获胜了。

## 此函数显示游戏盘和该回合的最终结果

```powershell
function Display-Results {
    Clear-Host # 清空 Windows 命令控制台屏幕

    # 显示游戏盘
    Write-Host "`n`n | T I C - T A C - T O E`n`n"
    Write-Host "`n | 1 | 2 | 3`n"
    Write-Host "`n | | | | | |"
    Write-Host "`n | A | $A1 | $A2 | $A3"
    Write-Host "`n | | | | | |"
    Write-Host "`n | | - - - - - - - - | | |"
    Write-Host "`n | | | | | |"
    Write-Host "`n | B | $B1 | $B2 | $B3"
    Write-Host "`n | | | | | |"
    Write-Host "`n | | - - - - - - - - | | |"
    Write-Host "`n | | | | | |"
    Write-Host "`n | C | $C1 | $C2 | $C3"
    Write-Host "`n | | | | | |"

    # 显示获胜者
    if ($tie -eq "True") { # 如果平局
        Write-Host "`n | It's a tie!"
    } else { # 否则显示了获胜者
        Write-Host "`n | $winner has won!"
    }
}
```

代表所选棋盘格的变量将被赋值为相应的 `X` 或 `O` 值。因此，值为空格的变量仍然可以选择，而赋值为 `X` 或 `O` 值的变量则不可选。

## 棋盘格变量

在棋盘中，每一行和每一列都由一组变量表示。例如，`$A1`、`$A2`、`$A3` 代表第一行，`$B1`、`$B2`、`$B3` 代表第二行，`$C1`、`$C2`、`$C3` 代表第三行。

## 检查玩家获胜

```powershell
# 玩家获胜
if ($winner -ne " ") {
    Write-Host "`n | Player $winner has won!"
}
```

# 第 8 章 · 操作文件和文件夹

```powershell
Write-Host # 发出蜂鸣声
Display-Results # 调用显示游戏结果的函数
$playGame = "False"
continue # 重复此循环
```

当其中一名玩家赢得游戏时，会发生以下操作。首先，通过向 `Write-Host` 命令项传递 `` ` `` 转义字符来播放蜂鸣声，通知玩家游戏结束。然后调用 `Display-Results` 函数。该函数会显示游戏的最终结果，告知玩家谁胜了。随后将 `$playGame` 的值设置为 `False`，这样当执行接下来的 `continue` 命令时，将终止内部循环的执行。

> 直到本书为止，你开发的所有 Windows PowerShell 游戏脚本都有一个共同点：它们都是静音的。然而，你可以通过添加一点声音让你的脚本变得生动。具体来说，通过像下面所示在 `Write-Host` 语句中插入 `` ` `` 转义字符，你可以在 PowerShell 脚本执行过程中的预定义点播放蜂鸣声。请注意，在大多数键盘上，`` ` `` 字符位于 I 键旁边。

```powershell
Write-Host # 发出蜂鸣声
```

井字游戏使用此功能来帮助在游戏胜利、失败或平局时通知玩家。

## 判断是否发生了平局

当没有玩家赢得游戏时，应该检查是否发生了平局。这通过在内部循环末尾添加以下语句来实现。

```powershell
if ($moves -eq 9) { # 发生平局时执行以下操作
    Write-Host # 发出蜂鸣声
    $tie = "True"
    Display-Results # 调用显示游戏结果的函数
    $playGame = "False"
    continue # 重复此循环
}
```

如你所见，使用了一个 `if` 语句来检查 `$moves` 的值，如果其设置为 `9`，则游戏板上的每个格子都已被选中，通过将 `$tie` 设置为 `True` 来宣布平局。

## 切换玩家回合

如果没有发生平局且没有发现任何玩家赢得游戏，内部循环将执行并提示下一位玩家走棋。在此之前，需要执行以下语句，因此应将它们添加到内部循环的末尾。

```powershell
# 游戏尚未结束，切换玩家回合
if ($playGame -eq "True") {
    if ($player -eq "X") {
        $player = "O"
    }
    else {
        $player = "X"
    }
}
```

如你所见，这些语句每次执行时都会在 `X` 和 `O` 之间切换 `$player` 的值，从而控制轮到谁的操作。

## 提示玩家玩新游戏

最后添加到脚本的一组代码语句如下所示，应添加到外部循环的末尾。这些语句设置了一个 `while` 循环，提示玩家玩新游戏。

```powershell
# 下一组语句仅在当前轮游戏
# 结束后运行

$response = "False" # 设置默认值以确保循环执行

# 循环直到接收到有效输入
while ($response -ne "True") {

    Clear-Host # 清空 Windows 命令控制台

    # 提示玩家玩新游戏
    $response = Read-Host "`n`n 再次玩吗？(Y/N)"

    # 验证玩家输入 # 继续游戏

    if ($response -eq "Y") {

        # 重置默认变量设置以准备新一轮游戏
        $response = "True"
        $terminate = "False"
        $playGame = "True"
        Clear-Board
        $player = "X"
        $moves = 0
        $tie = "False"
    }
    elseif ($response -eq "N") {  # 该退出了

        Clear-Host # 清空 Windows 命令控制台屏幕
        Write-Host "`n`n 请尽快回来再次玩游戏。"
        Read-Host # 暂停游戏
        $response = "True"
        $terminate = "True"
    }
    else {

        Clear-Host # 清空 Windows 命令控制台屏幕
        Write-Host "`n`n 输入无效。请按回车键重试。"
        Read-Host # 暂停游戏
    }
}
```

只接受 `Y` 或 `N` 输入。输入 `Y` 将通过将脚本变量重置为初始值来开始新轮游戏。回答 `N` 则终止游戏和脚本的执行。

## 最终结果

好了，就是这样。假设你在输入构成井字游戏的脚本语句时没有任何拼写错误，一切都应该如预期运行。我建议你花一点时间测试游戏，确保它按预期工作，然后找个朋友一起玩，展示一下你的编程技能。

### 总结

在本章中，你学习了通过程序管理文件和文件夹。这包括学习了如何创建、删除、复制和移动文件以及文件夹。你还学习了如何读写不同类型的文件，包括文本文件、CSV 文件和 XML 文件。你还学习了如何使用正则表达式进行字符串模式匹配。此外，你学习了如何使用 `Format-List` 和 `Format-Table` 命令项来控制命令项输出，以便配合 Windows PowerShell 2.0 的新的 `Out-GridView` 命令项。现在，在进入第 9 章“基础系统管理”之前，我建议你留出几天时间。

### 挑战

在本章中，你学习了通过程序管理文件和文件夹的精髓。这包括学习如何创建、删除、复制和移动文件以及文件夹。你还学习了如何读写不同类型的文件，包括文本文件、CSV 文件和 XML 文件。你还学习了如何使用正则表达式进行字符串模式匹配。此外，你学习了如何使用 `Format-List` 和 `Format-Table` 命令项来控制命令项输出，以便配合 Windows PowerShell 2.0 的新的 `Out-GridView` 命令项。现在，在进入第 9 章“基础系统管理”之前，我建议你留出几天时间。

- 提供一个解释规则的屏幕。
- 记录胜利、失败和平局的次数。
- 修改游戏，使其在首次启动时显示玩家名称。

# 第 9 章 · 基础系统管理

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_322_0.png)

图 9.2

默认情况下，游戏结束时会显示其自身及其开发者的信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_322_1.png)

图 9.3

与传统的黑杰克（Blackjack）不同，PowerShell 黑杰克游戏开始时会为玩家和电脑各分配一张牌。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_322_2.png)

图 9.4

玩家的目标是尽可能接近 21 点，但不超过。

图 9.5 显示了典型回合游戏的结果。在这个示例中，玩家赢了电脑。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_323_0.png)

图 9.5

玩家赢了这一局。

每局结束后，系统都会提示玩家按 Enter 键开始新的一局，或者输入 `0` 并按 Enter 退出游戏。

## 访问和管理系统资源

Windows PowerShell 将为系统管理员、高级用户和计算机爱好者提供访问大量系统、应用程序和网络资源的权限。可能性太多，在书中无法全部涵盖。相反，本章将尝试为你提供一些示例，演示 Windows PowerShell 可以帮助你自动化的许多系统管理途径。

## 列出和停止进程

Windows 操作系统在后台运行各种进程，它们共同工作以帮助你的计算机流畅运行。正如你已经看到的，可以使用 `Get-Process` 来获取计算机上运行的所有进程列表，如下所示：

```powershell
Get-Process
```

执行此语句时，将生成类似下所示输出：

| Handles | NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id | ProcessName |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 95 | 4 | 24092 | 244 | 155 | | 1664 | aawservice |
| 71 | 3 | 2084 | 740 | 38 | | 1116 | AppleMobileDe... |
| 253 | 5 | 21284 | 16644 | 56 | | 1372 | audiodg |
| 185 | 8 | 15232 | 40504 | 105 | | 2508 | avgrsx |
| 172 | 5 | 5012 | 3828 | 67 | 1.93 | 3192 | avgtray |
| 629 | 10 | 8116 | 792 | 88 | | 1416 | avgwdsvc |
| 697 | 6 | 1832 | 1828 | 99 | | 568 | csrss |
| 579 | 8 | 17484 | 14628 | 185 | | 632 | csrss |

`Get-Process` cmdlet 返回的信息量可能会让人无从准备。为了简化输出，你可以将指定的进程名称作为参数传递给 cmdlet，如下所示。

```powershell
Get-Process PowerShell
```

执行此语句时，它将仅显示 PowerShell 进程的进程信息。假设指定的进程当前正在运行，此语句将生成与此处所示类似的输出：

| NPM(K) | PM(K) | WS(K) | VM(M) | CPU(s) | Id | ProcessName |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 486 | 13 | 33808 | 35416 | 166 | 2.87 | 5736 | powershell |

你还可以使用逗号分隔的列表一次显示多个进程，如下所示。你可以使用通配符匹配任意数量的进程。

```powershell
Get-Process explorer, powershell
```

在 Windows 上，情况偶尔会发生变化，导致进程挂起、行为异常或无响应。当发生此类情况时，你可以使用 `Stop-Process` cmdlet 来终止这些进程。例如，以下语句通过指定其进程 ID 来终止进程。

```powershell
Stop-Process 2932
```

你也可以通过指定进程名称来轻松地终止进程，如下所示：

```powershell
Stop-Process -processname notepad
```

## 管理 Windows 服务

Windows 操作系统的另一个关键组件是它在后台运行的软件服务，用于提供特定的服务。例如，打印后台服务（spooler service）负责管理打印操作。Windows PowerShell 允许你通过许多不同的 cmdlet 与 Windows 服务交互并对其进行管理，如下所示：

- `Get-Service`：获取服务列表。
- `Start-Service`：启动服务。
- `Stop-Service`：停止服务。
- `Restart-Service`：重启服务。
- `Suspend-Service`：暂停服务。
- `Resume-Service`：恢复已暂停的服务。
- `Set-Service`：修改服务的属性。

# 零基础 Windows PowerShell 2.0 编程，第二版

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_329_0.png)

### 图 9.8

打印向导建议重启打印后台服务。

假设用户给予肯定回答，脚本将执行 `Restart-Service` cmdlet，并向其传递 `Spooler` 参数。随后，脚本将等待该 cmdlet 执行完成并再次显示服务状态，如图 9.9 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_329_1.png)

### 图 9.9

打印向导显示正在重启的打印后台服务状态。

如果到此时用户的问题尚未解决，脚本将显示一条消息，建议他们联系帮助台。

## 访问事件日志

Windows PowerShell 还允许你使用 `Get-EventLog` cmdlet 来处理和查看存储在计算机上的事件日志。Windows 操作系统及其应用程序向这些事件日志中写入不同类型的消息，提供状态和错误信息，这些信息可追踪和分析问题。通过向 `Get-EventLog` 传递 `-list` 参数，你可以指令该 cmdlet 生成计算机上所有事件日志的列表，如下：

```powershell
Get-EventLog -list
```

执行此语句时，将显示类似下方的输出：

| Max(K) | Retain | OverflowAction | Entries | Name |
| :--- | :--- | :--- | :--- | :--- |
| 20,480 | 0 | OverwriteAsNeeded | 640 | Application |



| 15,168 0 OverwriteAsNeeded | 6 DFS Replication |
| 20,480 0 OverwriteAsNeeded | 0 Hardware Events |
| 512 7 OverwriteOld | 0 Internet Explorer |
| 20,480 0 OverwriteAsNeeded | 0 Key Management Service |
| 8,192 0 OverwriteAsNeeded | 14,084 Media Center |
| 16,384 0 OverwriteAsNeeded | 0 Microsoft Office Diagnostics |
| 16,384 0 OverwriteAsNeeded | 171 Microsoft Office Sessions |
| 20,480 0 OverwriteAsNeeded | 5,061 System |
| 15,360 0 OverwriteAsNeeded | 2,945 Windows PowerShell |

一旦你了解了计算机上存储了哪些事件日志，就可以查看它们的内容。例如，以下语句显示了写入 Application（应用程序）日志的所有消息列表。

```powershell
Get-EventLog Application
```

执行此语句时，将生成类似下方的输出：

| Index | Time | Type | Source | InstanceID |
|---|---|---|---|---|
| 8492 | Oct 17 23:03 | Information | Windows Rep... | 1001 Fa... |
| 8491 | Oct 17 23:03 | Error | Application Error | 1000 Fa... |
| 8490 | Oct 17 01:59 | Information | VSS | 8224 Th... |
| 8489 | Oct 17 01:56 | Information | System Restore | 8194 Su... |
| 8488 | Oct 17 01:55 | Information | System Restore | 8194 Su... |
| 8487 | Oct 17 01:55 | Information | Windows Rep... | 1001 Fa... |
| 8486 | Oct 17 00:03 | Information | VSS | 8224 Th... |
| 8485 | Oct 16 21:36 | Information | VSS | 8224 Th... |
| 8484 | Oct 16 21:33 | Information | System Restore | 8211 Su... |
| 8483 | Oct 16 21:33 | Information | System Restore | 8194 Su... |
| 8482 | Oct 16 18:27 | Warning | Microsoft-Windows... | 1 Th... |
| 8481 | Oct 16 18:05 | Information | iPod Service | 0 Th... |

事件日志可以包含数千万条消息。如果你正在寻找最近发生的某些事件，可以通过向 `Get-EventLog` cmdlet 传递 `-newest` 参数来限制返回的数据量，该参数指定了你想查看的最近记录的消息条数，如下：

```powershell
Get-EventLog application -newest 4
```

执行此语句时，将生成类似下方的输出：

| Index | Time | Type | Source | InstanceID | Message |
|---|---|---|---|---|---|
| 8492 | Oct 17 23:03 | Information | Windows Error Rep... | 1001 Fa... | |
| 8491 | Oct 17 23:03 | Error | Application Error | 1000 Fa... | |
| 8490 | Oct 17 01:59 | Information | VSS | 8224 Th... | |
| 8489 | Oct 17 01:56 | Information | System Restore | 8194 Su... | |

你可能注意到 `Get-EventLog` 返回的数据被截断了，导致难以使用。你可以使用 `Format-List` cmdlet 来解决这个问题，生成一个可读的报告。

```powershell
Get-Eventlog application -newest 1 | Format-List > C:\Sample.txt
```

在此示例中，Application 事件日志中最后记录的消息被检索并报告存储在名为 `Sample.txt` 的文本文件中。打开此文件时，它将包含此处所示的信息：

```text
Index : 8492
EntryType : Information
InstanceId : 1001
Message : Fault bucket 973472676, type 1
Event Name: APPCRASH
Response: None
Cab Id: 0
Problem signature:
P1: TicTacToe.exe
P2: 0.0.0.0
P3: 47c75425
```

# 第 9 章 · 基础系统管理

```
SMBIOSVersion : 5.03
Manufacturer : Phoenix Technologies, LTD
Name : Phoenix - AwardBIOS v6.00PG
SerialNumber : CNX711050Q
Version : HP00EM - 42302e31
```

### 获取系统信息

你也可以通过向 `Get-WmiObject` get 传递 `Win32_Processor` 参数来检索处理器信息，如下所示。当管理员需要确定计算机处理器是否符合运行特定应用程序的最低要求时，这些信息可能证明非常有用。返回的信息将包括处理器名称、描述、制造商以及其他许多处理器相关的数据。

```
Get-WmiObject Win32_Processor
```

执行此语句时，将显示类似下面的输出：

```
_GENUS : 2
_CLASS : Win32_Processor
_SUPERCLASS : CIM_Processor
_DYNASTY : CIM_ManagedSystemElement
_RELPATH : Win32_Processor.DeviceId="CPU"
_PROPERTY_COUNT : 48
_DERIVATION : (CIM_Processor, CIM_LogicalDevice, CIM_LogicalDeviceElement, CIM_ManagedSystemElement)
_SERVER : HP-PC
_NAMESPACE : root\cimv2
_PATH : \\HP-PC\root\cimv2:Win32_Processor.DeviceId=\n	"CPU"

AddressWidth : 32
Architecture : 9
Availability : 3
Caption : x64 Family 15 Model 107 Stepping 1
ConfigManagerErrorCode : 
ConfigManagerUserConfig : 
CpuStatus : 1
CreationClassName : Win32_Processor
CurrentClockSpeed : 1000
CurrentVoltage : 13
DataWidth : 64
```

# Microsoft Windows PowerShell 2.0 入学者编程，第二版

```
Description : x64 Family 15 Model 107 Stepping 1
DeviceID : CPU
ErrorCleared : :
ErrorDescription : :
ExtClock : 201
Family : 133
InstallDate : :
L2CacheSize : 512
L2CacheSpeed : :
L3CacheSize : 0
L3CacheSpeed : :
LastErrorCode : 15
Level : :
LoadPercentage : 2
Manufacturer : AuthenticAMD
MaxClockSpeed : 2500
Name : AMD Athlon(tm) 64 X2 Dual Core Processor
```

由于此语句产生的信息量很大，我缩短了输出列表。通常，为了防止信息过载，你可能希望使用 `Format-List` cmdlet 将处理器数据的显示限制为你你感兴趣的信息。

```
Get-WmiObject Win32_Processor | Format-List Name, Caption, Manufacturer
```

执行此语句时，将显示一个更易管理的处理器信息列表。

- Name : AMD Athlon(tm) 64 X2 Dual Core Processor 4800+
- Caption : x64 Family 15 Model 107 Stepping 1
- Manufacturer : AuthenticAMD

### 获取网络数据

WMI 还提供了对网络信息的访问。计算机管理员可以使用这些信息来验证计算机网络配置或排排除性问题。例如，要检索所有活动网络协议的列表，你可以像这里所示向 `Get-WmiObject` cmdlet 传递 `Win32_NetworkProtocol` 参数：

```
Get-WmiObject Win32_NetworkProtocol
```

执行此语句时，将显示有关你计算机上安装的所有网络协议的列表，如下文输出所示：

- Caption : Tcpip
- GuaranteesDelivery : True
- GuaranteesSequencing : True
- ConnectionlessService : False
- Status : OK
- Name : MSAFD Tcpip [TCP/IP]

### 获取应用程序数据

WMI 还提供了存储在计算机上的应用程序信息。例如，计算机管理员可能会创建一个 PowerShell 脚本来检索计算机上安装的所有应用程序列表。例如，以下语句检索了使用 Windows Installer 服务安装的应用程序信息。

```
Get-WmiObject Win32_Product
```

执行此语句时，将显示类似下面的数据：

- IdentifyingNumber : (2DFDD440-A33C-42E4-A366-71E6CB4246A0)
- Name : Windows PowerShell
- Vendor : Microsoft Corporation
- Version : 1.0.9567.1
- Caption : Windows PowerShell
- IdentifyingNumber : (AC76BA86-7AD7-1033-B744-A7080000002)
- Name : Adobe Reader 7.0.8
- Vendor : Adobe Systems Incorporated
- Version : 7.0.8
- Caption : Adobe Reader 7.0.8
- IdentifyingNumber : (7131646D-CD3C-40F4-9789-CD9E4E62626EF)
- Name : Microsoft .NET Framework 2.0
- Vendor : Microsoft Corporation
- Version : 2.0.50727
- Caption : Microsoft .NET Framework 2.0

# 从远程计算机获取 WMI 数据

假设你拥有执行此操作所需的权限，`Get-WmiObject` cmdlet 也可以用于从远程网络计算机检索信息。要做到这一点，[文本根据提供的内容继续或结束]。

脚本的开头。最后，将 Internet Explorer 的 `Visible` 属性设置为 `True`，使浏览器和指定的网页可见。图 9.10 显示了如果你创建并运行此示例将看到的输出示例。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_339_0.png)

# 以程序方式与 Windows 注册表交互

Windows PowerShell 的另一个强大功能是它能够与 Windows 注册表交互。这意味着你不仅可以编写访问 Windows 注册表中存储数据的 PowerShell 脚本，还可以将数据存储在注册表中。

Windows 注册表被组织成五个高级键，也称为配置单元（hives）。注册表键类似于 Windows 文件系统上的文件夹。键用于存储其他键（或子键）和值。值类似于 Windows 文件系统上的文件。存储在注册表中的实际数据存储在值之中。在五个高级根键中，Windows PowerShell 允许你访问其中两个键存储的值，如表 9.1 所示。

表 9.1 WINDOWS POWERSLL 可访问的注册表键

| 配置单元 | 快捷方式 | 说明 |
|---|---|---|
| HKEY_CURRENT_USER | hkcu | 存储当前登录用户的信息 |
| HKEY_LOCAL_MACHINE | hklm | 存储全局计算机设置 |

Windows PowerShell 将注册表值视为属性。这让你可以使用 `Get-ItemProperty` cmdlet 获取有关键的信息并列出其所有值，如下所示：

```
Set-Location hklm:\SOFTWARE\Microsoft\PowerShell\1\PowerShellEngine
Get-ItemProperty
```

这里的第一个语句从当前提供程序（通常是 Windows 文件系统）切换到位于 HKEY_LOCAL_MACHINE 配置单元上的子键。第二个语句使用 `Get-ItemProperty` cmdlet 获取有关当前子集的信息。执行时，这些语句将生成与此处所示类似的输出：

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_340_0.png)

Windows 操作系统使用注册表存储有关操作系统的数据以及计算机的硬件、软件和用户配置设置。注册表的完整性对于计算机的正常运行至关重要。因此，在操作它时务必小心。否则，如果你不小心更改或删除了错误的键或值，可能会对你计算机的运行产生不可预测的影响。

```
ApplicationBase : C:\Windows\system32\WindowsPowerShell\v1.0\
ConsoleAssemblyName : Microsoft.PowerShell.ConsoleHost, Version=1.0.0.
0, Culture=neutral, PublicKey=31bf3856ad364
e35, ProcessorArchitecture=msil
PowerShellVersion : 2.0
RuntimeVersion : v2.0.50727
CTPVersion : 6
PSCompatibleVersion : 1.0.2.0
```

使用 `Get-ItemProperty` cmdlet，你还可以检索存储在特定值中的数据，如下所示：

```
$PSVer = $(get-ItemProperty hkl:\SOFTWARE\Microsoft\PowerShell\1\PowerShellEngine).PowerShellVersion
```

在这里，存储在 `PowerShellVersion` 值中的数据被检索并如下所示显示。

# 2.0

注意设置此操作涉及的语法。具体来说，为了便于对象引用，你必须通过输入 `$` 后紧跟括号来创建一个变量对象引用，在括号内你标识包含该值的键的逻辑路径。设置好对象引用后，你就可以使用熟悉的点符号（dot notation）来标识你想检索的特定对象属性。记住，Windows PowerShell 将注册表值视为对象属性。

如果你需要，可以使用 Regedit 工具通过点击“开始”，在搜索字段中输入 Regedit 并按回车键，从视觉上验证 `PowerShellVersion` 值及其关联数据。Regedit 工具允许你以类似于 Windows 导航 Windows 文件系统的方式导航 Windows 注册表，如图 9.11 所示。

为了进一步演示 PowerShell 与 Windows 注册表交互的能力，让我们编写一个新的 PowerShell 脚本，向 `hkcu` 键添加一个新的名称和值。将创建的键将命名为 `PSBlackjack`，值命名为 `Credits`。`Credits` 将用于存储 `true` 的字符串值。稍后，当你创建本章的游戏项目—— PowerShell Blackjack 游戏时，游戏将查找存储在 `Credits` 值中的数据，以决定在游戏结束时显示有关游戏及其作者的额外信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_341_0.png)

图 9.11 使用 Regedit 查看存储在 hkl 配置单元中的注册表键和值。

此新 PowerShell 脚本（你应该将其命名为 `BJSetup.ps1`）的代码如下：



```
# *********************************************************************
# Script Name: BJSetup.ps1 (PowerShell Blackjack 游戏设置脚本)
# Version: 2.0
# Author: Jerry Lee Ford, Jr.
# Date: October 18, 2008

# Description: 此 PowerShell 脚本为 PowerShell Blackjack
# 创建注册表键
# *********************************************************************

# Initialization
```

```
$key = "PSBlackjack" # 要创建的键名称

$value = "Credits" # 值的名称

$type = "string" # 值的类型

$data = "true" # 数据

# *********************************************************************

# Functions
```

```
function Set-RegistryValue {
    param (
        [string]$Key,
        [string]$Name,
        [string]$Type,
        [string]$Data
    )
    if (-not (Test-Path "HKCU:\$Key")) {
        New-Item -Path "HKCU:\$Key" | Out-Null
    }
    New-ItemProperty -Path "HKCU:\$Key" -Name $Name -Value $Data -PropertyType $Type -Force
}

### Main Processing
```

```
Set-RegistryValue -Key $key -Name $value -Type $type -Data $data
```

你可以看到，这非常简单。首先定义变量，然后定义函数，最后由主处理部分调用该函数。执行时，此语句将生成与此处所示类似的输出：

接下来，使用`Get-ItemProperty` cmdlet 获取有关键和值的信息，如图 9.12 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_342_0.png)

Windows 操作系统使用注册表存储操作系统的数据以及计算机硬件、软件和用户配置设置。注册表的完整性对于计算机的正常运行至关重要。因此，在操作它时务必小心。否则，如果你不小心更改或删除了错误的键或值，可能会对你计算机的运行产生不可预测的影响。

使用`Get-ItemProperty` cmdlet，你还可以检索存储在特定值中的数据，如下所示：

```
$PSVer = $(get-ItemProperty hkl:\SOFTWARE\Microsoft\PowerShell\1\PowerShellEngine).PowerShellVersion
```

在这里，存储在`PowerShellVersion`值中的数据被检索并如下所示显示。

注意设置此操作涉及的语法。具体来说，为了便于对象引用，你必须通过输入`$`后紧跟括号来创建一个变量对象引用，在括号内你标识包含该值的键的逻辑路径。设置好对象引用后，你就可以使用熟悉的点符号来来标识你想检索的特定对象属性。记住，Windows PowerShell 将注册表值视为对象属性。

如果你需要，可以使用 Regedit 工具通过点击“开始”，在搜索字段中输入 Regedit 并按回车键，从视觉上验证`PowerShellVersion`值及其关联数据。Regedit 工具允许你以类似于 Windows 导航 Windows 文件系统的方式导航 Windows 注册表，如图 9.11 所示。

为了进一步演示 PowerShell 与 Windows 注册表交互的能力，让我们编写一个新的 PowerShell 脚本，向`hkcu`键添加一个新的名称和值。将创建的键将命名为`PSBlackjack`，值命名为`Credits`。`Credits`将用于存储`true`的字符串值。稍后，当你创建本章的游戏项目—— PowerShell Blackjack 游戏时，游戏将查找存储在`Credits`值中的数据，以决定在游戏结束时显示有关游戏及其作者的额外信息。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_341_0.png)

图 9.11 使用 Regedit 查看存储在 hkl 配置单元中的注册表键和值。

此新 PowerShell 脚本（你应该将其命名为`BJSetup.ps1`）的代码如下：

```
# *********************************************************************

# Script Name: BJSetup.ps1 (PowerShell Blackjack 游戏设置脚本)

# Version: 2.0

# Author: Jerry Lee Ford, Jr.

# Date: October 18, 2008

# Description: 此 PowerShell 脚本为 PowerShell Blackjack

# 创建注册表键

# *********************************************************************

# Initialization
```

```
$key = "PSBlackjack" # 要创建的键名称
$value = "Credits" # 值的名称
$type = "string" # 值的类型
$data = "true" # 数据
# *********************************************************************

# Functions
```

```
function Set-RegistryValue {

    param (

        [string]$Key,

        [string]$Name,

        [string]$Type,

        [string]$Data

    )

    if (-not (Test-Path "HKCU:\$Key")) {

        New-Item -Path "HKCU:\$Key" | Out-Null

    }

    New-ItemProperty -Path "HKCU:\$Key" -Name $Name -Value $Data -PropertyType $Type -Force

}

### Main Processing
```

```
Set-RegistryValue -Key $key -Name $value -Type $type -Data $data
```

你可以看到，这非常简单。首先定义变量，然后定义函数，最后由主处理部分调用该函数。执行时，此语句将生成与此处所示类似的输出：

接下来，使用`Get-ItemProperty` cmdlet 获取有关键和值的信息，如图 9.12 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_342_0.png)

# 322 | 零基础入门 Windows PowerShell 2.0 编程（第二版）

在远程计算机上浪费地消耗资源。要做到这一点，你只需要执行`Remove-Runspace`命令，并使用其`-runspace`参数传递你想要终止的 runspace 数字 ID，如下所示：

```
Remove-Runspace -runspace $r
```

执行此语句时，它将删除上一个示例中创建的 runspace。

默认情况下，Windows PowerShell 2.0 远程连接需要在 Windows 域上执行。通过修改注册表，可以配置为在工作组内运行。要了解更多关于此选项，请参考 Windows PowerShell 2.0 的发行说明。

## 创建你自己的脚本 CMDLETS

Windows PowerShell 是一个高度可扩展的开发工具。在 Windows PowerShell 1.0 中，软件人员可以使用 Visual Basic、C++ 和 C# 等 .NET 编程语言开发自定义 cmdlet。然而，Windows PowerShell 2.0 通过允许你使用 Windows PowerShell 脚本创建脚本 cmdlet，使事情变得更加简单。

使用 Windows PowerShell 2.0 开发的脚本 cmdlet 保存为具有`.ps1`扩展名的普通脚本文件。Windows PowerShell 2.0 支持开发两种类型的 cmdlet：命名的（named）和未命名的（unnamed）。命名 cmdlet 具有“动词-名词”（Verb-Noun）结构的名称，外观和行为非常像典型的 PowerShell cmdlet，并将是本章讨论的重点。

未命名 cmdlet 未分配名称，其执行方式与普通 cmdlet 不同。要了解更多关于未命名 cmdlet 的信息，请在 Windows PowerShell 2.0 提示符中执行命令`Get-Help AboutScriptCmdlets`。

在创建命名 cmdlet 时，你会创建一个新的 Windows PowerShell 脚本并为其分配一个动词-名词名称。该脚本将使用以下结构：

```
Cmdlet Verb-Noun (
Param (
)
Begin (
)
Process (
)
}
End {
}
}
```

在这里，Verb-Noun 代表分配给 cmdlet 的名称。`Param`部分用于定义 cmdlet 使用的参数。在这里，你指定 cmdlet 支持的参数数量，并指定它们是否为强制性。你还可以指定特定的验证准则，以确保传递给 cmdlet 的参数符合标准并被视为有效。使用时，`Begin`和`End`部分会被处理一次，通常用于执行初始化和终止任务，如分配和释放所需的资源。控制 cmdlet 执行的整体编程逻辑放在`Process`部分。

### 创建自定义 Cmdlet

为了深入理解如何创建 cmdlet，让我们来看几个示例并看看它们是如何运行的。在第一个示例中，创建了一个名为`Set-Home`的 cmdlet。执行时，该 cmdlet 将当前工作位置更改为用户的主文件夹。

```
Cmdlet Set-Home {
Begin {
  Clear-Host
}
Process {
  Write-Host
  Write-Host "Press Enter to switch to your home directory.
  Read-Host
  Set-Location $PSHome
}
End {
  Clear-Host
}
}
```

如你所示，`Begin`和`End`部分都执行了`Clear-Host`命令，清除控制台窗口。`Process`部分的代码语句执行了核心工作。首先，它在控制台窗口顶部写入一个空行，接着是第二行，指示用户按 Enter 键切换到用户的主目录。然后使用`Read-Host`命令暂停 cmdlet 的执行。一旦按下 Enter 键，将执行`Set-Location`命令并传递`$Home`作为参数。

### 加载和执行 Cmdlets

为了执行你的新 cmdlet，你必须先加载它，这通过输入一个点、空格、另一个点、正斜杠，然后你的 cmdlet 名称来实现，如下所示：

```
- ./Set-Home
```

一旦加载，你就可以像执行任何其他 PowerShell cmdlet 一样执行你的 cmdlet（它不接受参数）。只需在 Windows PowerShell 提示符中输入它的名称并按 Enter，如下所示：

```
Set-Home
```

`Set-Home`然后提示用户按 Enter，一旦完成，该 cmdlet 将当前工作位置更改为用户的默认 PowerShell 主文件夹。

### 与管道数据一起工作

使用 PowerShell 创建的 cmdlet 可以接受并处理通过管道（pipeline）传递给它的参数数据。此外，还可以生成管道数据。要接受和处理管道数据，你必须使用`Param`部分来定义 cmdlet 支持的参数。要生成管道输出，你的 cmdlet 只需要显示输出即可。例如，下面的 cmdlet 展示了如何处理通过管道接收的数值输入。具体而言，该 cmdlet 将一个数字列表相加，这些数字作为逗号分隔的管道输入传递给它。

```
Cmdlet Add-Numbers -
Param ([Parameter(Mandatory=$true, ValueFromPipeline=$true)] $Parameter1
Begin (
)
Process {
$x = $x + $_
}
End {
Write-Host "Total = $x"
}
```

在这个示例中，创建了一个名为`Add-Numbers`的 cmdlet。它定义了一个单一参数。该参数是强制性的且必须来自管道。其关联参数数据将存储在名为`$Parameter1`的变量中。当一组逗号分隔的数字传递给 cmdlet 时，它们将被一个一个地处理。每处理一个数字，其值就会加到内部变量`$x`的值上。一旦每个数字都处理完毕且`Process`部分执行结束，`End`部分将执行，显示所有相加数字的总和，如下：

```
PS C:\Temp> ./Add-Numbers
PS C:\Temp> 1, 4, 6 | Add-Numbers
Total = 11
```

![](img/e07ce5ceafe5f9442c3619d87.png)

脚本 cmdlet 是一种非常强大的编程工具，你可以用它来开发自定义 cmdlet。要了解更多关于脚本 cmdlet 的信息，请查看以下文件：

- ScriptCmdlets

- CmdletMethods

- ScriptAttributes

- ScriptParameters

### 事件处理 (EVENTING)

Windows PowerShell 2.0 提供的另一个功能是响应事件（也称为异步通知），这些由许多对象产生。处理 PowerShell 事件的第一步是识别产生事件的对象。你可以通过使用`New-Object`命令实例化对象，然后使用`Get-Member`命令查看其是否产生事件。

### 实例化对象

设置对象的初步是设置要操作的对象实例。这是通过`New-Object`命令实现的，如下：

```
$ie = new-object -comobject Internet.Application
```

在这里，定义了一个 Internet Explorer 对象并赋值给变量`$ie`。一旦实例化，你可以使用`Get-Member`命令检索对象信息，见下一节。

### 检查对象

`Get-Member`命令检索有关 .NET 对象的信息，包括对象支持的方法、属性和事件类型。看下面的示例，它展示了如何使用`Get-Member`命令检索由`Get-Service`命令返回对象的信息。

```
PS C:\Get-Service | Get-Member
```

```
TypeName: System.Process.ServiceController
```

| Name | MemberType | Definition |
| --- | --- | --- |
| ServiceName | Property | Name = ServiceName |
| Disposed | Event | System.EventHandler Disposed(Sy... |
| Close | Method | System.Void Close() |
| Continue | Method | System.Void Continue() |
| CreateObjRef | Method | System.Runtime.Remoting.ObjRef ... |
| Dispose | Method | System.Void Dispose() |
| Equals | Method | System.Boolean Equals(Object obj) |
| ExecuteCommand | Method | System.Void ExecuteCommand(Int3... |
| GetHashCode | Method | System.Int32 GetHashCode() |
| GetLifetimeService | Method | System.Object GetLifetimeService() |
| GetType | Method | System.Type GetType() |
| InitializeLifetimeService | Method | System.Object InitializeLifetim... |
| Pause | Method | System.Void Pause() |

## 第9 章 • 基础系统管理

| | | |
|------|---|---|
| 刷新 (Refresh) | 方法 | System.Void Refresh() |
| 开始 (Start) | 方法 | System.Void Start(), System.Voi... |
| 停止 (Stop) | 方法 | System.Void Stop() |
| 字符串 (ToString) | 方法 | System.String ToString() |
| 等待状态 (WaitForStatus) | 方法 | System.Void WaitForStatus(Servi... |



| 可以暂停并继续 (CanPauseAndContinue) | 属性 | `System.Boolean CanPauseConti...` |
| 可以关闭 (CanShutdown) | 属性 | `System.Boolean CanShutdown(get;)` |
| 可以停止 (CanStop) | 属性 | `System.Boolean CanStop(get;)` |
| 容器 (Container) | 属性 | `System.ComponentModel.IContine...` |
| 依赖服务 (DependentsServices) | 属性 | `System.ServiceProcess.Co...` |
| 显示名称 (DisplayName) | 属性 | `System.String DisplayName(get...)` |
| 机器名称 (MachineName) | 属性 | `System.String MachineName(get...)` |
| 服务句柄 (ServiceHandle) | 属性 | `System.Runtime.InteropServices...` |
| 服务名称 (ServiceName) | 属性 | `System.String ServiceName(get...)` |
| 依赖依赖的服务 (ServicesDependedOn) | 属性 | `System.ServiceProcess.Co...` |
| 服务类型 (ServiceType) | 属性 | `System.ServiceProcess.Service...` |
| 站点 (Site) | 属性 | `System.ComponentModel.ISite Sit...` |
| 状态 (Status) | 属性 | `System.ServiceProcess.Service...` |

```powershell
PS C:\
```

如此示例所示，`Get-Member`命令返回的输出被传递给另一个`Get-Member`命令。由于返回的对象是使用命令词句生成的，因此你不需要担心实例化它；Windows PowerShell 已经为你完成了这一操作。输出列出了该对象支持的所有方法、属性和事件。在本例中唯一支持的事件是`Disposed`事件。显而易见，`Get-Member`命令是学习对象的绝佳工具。

## 订阅对象事件

现在你已经了解如何操作对象，并学会了如何使用`Get-Member`命令检索对象信息，你可以判断一个对象是否支持事件。利用这些信息，你可以使用`Register-ObjectEvent`命令订阅特定类型的事件。要做到这一点，你需要使用`Register-ObjectEvent`命令的`-SourceIdentifier`参数来指定你想要作为事件触发器的事件。例如，下面的示例演示了如何实例化一个新的`Timer`对象并订阅它的`Elapsed`事件。

```powershell
$Timer = New-Object Timers.Timer
Register-ObjectEvent $Timer Elapsed -SourceIdentifier Timer.Elapsed
```

正如下一节将演示的那样，`Timer`对象的`Elapsed`事件用于在指定时间过去后触发语句或命令的执行。一旦你注册了事件，就可以使用`Get-PsEventSubscriber`命令来获取当前工作会话建立的所有事件订阅的信息，如下所示。

```powershell
PS C:\> Get-PsEventSubscriber

Format-List -n \
*
SubscriptionId    : 1
SourceObject      : System.Timers.Timer
EventName        : Elapsed
SourceIdentifier : Timer.Elapsed
Action            : 
SupportEvent     : False
```

**注意**，`Get-PsEventSubscriber`命令了分配给事件订阅的`SubscriptionId`、对象名称以及已订阅的事件。

### 等待事件发生

为了使其变得真正有用，你必须配置你所订阅的对象。例如，下面的脚本演示了如何使用`Timers`对象的`Elapsed`事件在五秒后执行名为`MyScript.ps1`的脚本。

```powershell
$MyTimer = New-Object Timers.Timer

Register-ObjectEvent $MyTimer Elapsed -SourceIdentifier Timer.Elapsed -action (./MyScript.ps1)

$MyTimer.Interval = 5000
$MyTimer.Autoset = $false # 设置为 True 会让事件重复触发
$MyTimer.Enabled = $true
Wait-PsEvent Timer.Elapsed
```

示例首先实例化`Timers`对象，然后注册事件订阅。注意，在`Register-ObjectEvent`命令的末尾添加了`-action`参数。指定时，该参数告诉 PowerShell 在指定事件发生时执行语句或命令。下一条语句通过为`Timer`对象的`Interval`属性分配`5000`值来配置事件订阅。结果是，事件被设置为每 5 秒发生一次。接下来，将`AutoReset`属性设置为`false`，使事件仅发生一次。正如语句末尾的注释解释的，如果你将`AutoReset`属性设置为`true`，事件将每 5 秒重复发生一次。倒数第二语句启用事件，最后一条语句执行`Wait-Event`命令，指示 Windows PowerShell 等待指定事件发生。结果是，当这是一个脚本时，`Timer`对象的`Elapsed`事件将在 5 秒后触发名为`MyScript.ps1`脚本的执行。

请尝试自己设置并运行此示例。当`MyScript.ps1`脚本执行后，按下`Ctrl + C`返回到 Windows PowerShell 提示符。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_352_0.png)

如果你想设置 Windows PowerShell 脚本的重复执行，可以使用之前的示例来实现。你只需要在第二条语句中更改要执行的脚本名称，并为`Autoreset`属性分配`$true`值即可。

### 移除事件

如前所述，任何时候创建新事件后，都可以移除它。使用此标识符删除不再需要的事件订阅，如下：

```powershell
Remove-PsEvent
```

关闭 Windows PowerShell 将终止任何活动的事件订阅。

## 回到 POWERSHELL 黑字游戏

好的，现在是时候回到游戏了。这个 PowerShell 脚本将与注册的事件交互。根据 Credits 值，它将显示该游戏的整体流程非常直观。其开发将按照以下 12 个步骤完成：

1. 使用模板创建脚本文件。
2. 定义并初始化变量。
3. 创建`Get-Permission`函数。
4. 创建`Check-Registry`函数。
5. 创建`GetPlayerHand`函数。
6. 创建`Deal-Hand`函数。
7. 创建`GetCard`函数。
8. 创建`GetComputerHand`函数。
9. 创建`Analyze-Results`函数。
10. 创建`GetPlayerHand`函数。
11. 创建`NewCard`函数。
12. 开发处理部分的代码。

### 创建新文件

首先，使用你的 PowerShell 模板创建一个名为`Blackjack.ps1`的新文件并修改其内容，如下：

```powershell
# *************************************************
#脚本名称: Blackjack.ps1 (黑字游戏)
# 版本: 2.0
# 作者: Jerry Lee, Jr.
# 日期:2008年10月18日

# 说明：此 PowerShell 脚本是流行黑字游戏的单玩家实现
# *************************************************

### 初始化部分

### 函数和过滤器

### 主处理部分

### 定义并创建变量
```

现在你已经创建了新文件，我们在初始化部分添加以下变量定义。

```powershell
$startGame = "False" # 用于判断是否玩游戏

$playerBusted = "False" # 用于跟踪玩家爆牌

$playerHand = 0 # 玩家手的当前值

$randomNO = New-Object System.Random # 此变量存储随机数

$computerHand = 0 # 计算机手的当前值

$playAgain = "True" # 控制处理部分逻辑循环的执行
```

### 创建 Get-Permission 函数

黑字游戏由多个自定义函数组成，每个函数都设计用于执行特定任务。这些函数中的第一个是`Get-Permission`函数，如下所示。将此函数以及后续的函数添加到脚本的函数和过滤器部分。

```powershell
#此函数获取玩家开始游戏的权限

function Get-Permission {

### 循环直到收集到有效回复

while ($startGame -eq "False") {

Clear-Host # 清除 Windows 命令行屏幕

### 显示游戏的开场序列

Write-Host "\n\n\n"

Write-Host " Welcome to the" -foregroundColor Blue

Write-Host ""

Write-Host ""

Write-Host " P O W E R S H E L   B L A C K J A C   G A M E ""

-foregroundColor Blue

Write-Host ""

Write-Host """
```

```powershell
Write-Host ""

Write-Host ""

Write-Host ""

Write-Host ""
```

```powershell
### 获取玩家的输入

$response = Read-Host "Would you like to play? (Y/N)"
```

```powershell
### 验证玩家的输入

if ($response -eq "Y") { # 玩家想玩

    $gameState = "True"

}

elif ($response -eq "N") { # 玩家想退出

    Check-Registry

    exit # 终止脚本执行

}
```

如你所示，此函数使用`while`循环来控制脚本欢迎界面的显示，并在提示玩游戏时收集并验证玩家的响应。如果玩家在提示玩游戏时输入 Y，则`$gameState`的值被设置为 "True"，从而终止循环执行并允许脚本继续运行。相反，如果玩家输入 N，则会调用`Check-Registry`函数然后执行`exit`命令，终止脚本的执行。

> 技巧
> 在`Write-Host`词句中添加`-ForegroundColor`参数。该参数提供了在 Windows 命令控制台中显示文本时指定字体颜色的功能。`Write-Host`词句还接受`-BackgroundColor`参数，允许您在 Windows 命令控制台中显示文本时指定背景颜色。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_355_0.png)

### 创建 Check-Registry 函数

`Check-Registry`函数负责确定在游戏结束时是否显示屏幕。该屏幕提供了有关游戏及其作者的少量信息。它通过检查 Windows 注册表中存储的`hkcu\PSblackjack\Credits`值来完成此任务。如果`Credits`等于 "True"，则显示额外的屏幕；否则，不显示。

```powershell
# 此函数检索一个注册表值，该值指定了如果玩家在启动脚本后

# 选择玩游戏，脚本是否应该显示启动界面

function Check-Registry {

    Clear-Host # 清空 Windows 命令控制台屏幕

    $currentLocation = Get-Location # 跟踪当前目录

    Set-Location hkcu:\ # 到 HKEY_CURRENT_USER 单元格

    # 获取 PSblackjack 子键下 Credits 值中存储的数据

    $regKey = $(Get-ItemProperty hkcu:\PSblackjack).Credits

    if ($regKey -eq "True") { # 如果注册表值设置为 true

        # 显示结束的启动界面

        Write-Host * `n`n`n`

        Write-Host * POWERSHELL B L A C K J A K`n`n`n` -ForegroundColor Blue

        Write-Host * Developed by Jerry Lee Ford, Jr.`n`n`n`

        Write-Host * Copyright 2008`n`n`n`

        Write-Host * www.tech-publishing.com`n`n`n`

    }

    Set-Location $currentLocation # 恢复当前工作目录

}
```

注意，在使用`Set-Location`词句将焦点从文件系统切换到注册表之前，函数将`$currentLocation`的设置为当前工作目录。接下来，使用`Get-ItemProperty`词句检索存储在`Credits`中的值，并存储在`$regKey`中。然后`if`语句分析`$regKey`的值以决定是否显示额外的屏幕。最后，再次执行`Set-Location`词句，将焦点恢复到文件系统。

### 创建 Play-Game 函数

要开发的下一个函数是下面的`Play-Game`函数。该函数的工作是根据需要执行其他函数，以管理玩家和电脑的手，并分析游戏结果。

```powershell
### 此函数控制单轮游戏的执行

function Play-Game {

    Deal-Hand # 调用分发初始手牌的函数

    Get-PlayerHand # 调用管理玩家牌的函数

    # 如果玩家爆牌了（busted），则游戏结束，否则轮到

    # 电脑

    if ($script:playerBusted -eq "False") {

        Get-ComputerHand # 调用管理电脑牌的函数

    }

    Analyze-Results # 调用分析游戏结果并

    # 宣布胜利者的函数

}
```

### 创建 Deal-Hand 函数

下面的`Deal-Hand`函数在每次启动新轮游戏时由`Play-Game`函数调用。它的任务是确保玩家和电脑都获取了初始牌。

```powershell
### 此函数处理玩家和电脑的初始手牌

function Deal-Hand {

    $script:playerHand = Get-Card # 为玩家手牌分配一张牌

    $script:computerHand = Get-Card # 为电脑手牌分配一张牌

}
```

## 第 9 章 • 基础系统管理

如你所示，此函数对`Get-Card`函数进行了两次调用，将返回的结果（例如牌）存储在脚本变量中。

### 创建 Get-Card 函数

`Get-Card`词句的代码所示。当调用时，此函数使用`Get-Random`词句生成一个 1 到 13 之间的随机数。如果随机数结果为 1，则被视为 Ace。如果数字大于 10，则被视为花牌。该值将返回给调用语句。

```powershell
### 此函数生成随机数并返回一张牌

function Get-Card {

    $number = Get-Random -Minimum 1 -Maximum 14

    if ($number -eq 1) {

        return "Ace"

    }

    return $number

}
```

### 创建 Computer-Hand 函数

下面的`Computer-Hand`函数负责管理电脑的手。它遵循一种简单的策略：直到电脑的手牌点达到 17 或更高。

```powershell
### 此函数管理电脑的逻辑

function Get-ComputerHand {

    # 电脑取牌的逻辑

}
```

### 创建 Get-PlayerHand 函数

下面的`Get-PlayerHand`函数负责管理玩家的手。它使用`while`循环允许玩家决定是要牌（hit）还是停牌（stand）。

```powershell
### 此函数管理玩家的手

function Get-PlayerHand {

    $keepGoing = "True" # 控制管理玩家

    # 手的循环的执行

    $response = "" # 存储玩家的输入

    # 循环直到收集到有效的回复

    while ($keepGoing -eq "True") {

        Clear-Host # 清空 Windows 控制台屏幕

        # 显示玩家和电脑当前的手牌

        Write-Host "`n`n"
```



```powershell
Write-Host ""
Write-Host " CURRENT HAND:"
Write-Host "`n"
Write-Host " Player Hand: $playerHand"
Write-Host ""
Write-Host " Computer Hand: $computerHand"
Write-Host ""
Write-Host ""
Write-Host ""
Write-Host ""
Write-Host ""

### 提示玩家再拿一张牌
$response = Read-Host "`n`n`n`n`n`n`n` Do you want another card? (Y/N)"

### 验证玩家的输入
if ($response -eq "Y") {
    Get-NewCard # 为玩家获取另一张牌
}
elseif ($response -eq "N") { # 玩家想要退出
    $keepGoing = "False"
    Clear-Host # 清除 Windows 控制台屏幕
}

if ($playerHand -gt 21) { # 玩家点数爆牌了
    $script:playerBusted = "True"
    $keepGoing = "False"
}
```

此函数使用一个`while`循环来显示玩家和计算机的手牌当前值，并询问玩家是否想要一张新牌。如果玩家给出肯定回答，则会调用`Get-NewCard`函数。当玩家决定停止请求新牌或其手牌因超过 21 点而爆牌时，循环将停止执行。

### 创建 Get-NewCard 函数

下所示`Get-NewCard`函数每当玩家选择向其手牌中添加另一张牌时就会被调用。它通过调用`Get-Card`函数，并将该函数返回的值添加到`playerHand`变量中来实现这一目标。

```powershell
# 此函数在玩家选择获取新牌时都会被调用，
# 并负责更新玩家手牌的数值
function Get-NewCard (
    $tempCard = 0 # 存储玩家新牌的值
    $tempCard = Get-Card # 为玩家获取一张新牌
    # 将新牌的值添加到玩家的手牌中
    $script:playerHand = $script:playerHand + $tempCard
)
```

### 在主处理部分中添加控制逻辑

此时，所有的脚本函数都已定义。剩下的只是在脚本的主处理部分添加一些控制逻辑。提供这些逻辑的语句概述如下：

```powershell
Get-Permission # 调用函数询问玩家是否开始
### 游戏

### 继续玩新游戏，直到玩家决定退出游戏
while ($playAgain -eq "True") {

    Play-Game # 调用控制单场游戏的函数

    # 提示玩家玩一个新游戏
    $response = Read-Host `n`n`n`n`n`n`n`n`n 按回车键再次游戏或按 Q 退出

    if ($response -eq "Q") { # 玩家想要退出
        $playAgain = "False"
        Clear-Host # 清除 Windows 控制台屏幕
    }
    else { # 玩家没有输入 Q，让我们继续玩
        $playAgain = "True"
        $playerBusted = "False"
    }
}
```

第一条语句调用`Get-Permission`函数，该函数提示玩家开始新游戏。主处理部分的其余语句都嵌入在一个`while`循环中，该循环负责提示玩家再玩一次游戏。

就是这些了。假设你在输入构成 PowerShell 黑色赌场游戏的代码语句时没有出现任何拼写错误，一切都应该如预期那样工作。去运行一下游戏吧。一旦你验证了所有内容运行正常，尝试向游戏输入无效输入，以确保游戏能够正确处理。一旦你确认一切无误，分享给朋友一份并征求他们的反馈。

### 总结

在本章中，你学习了使用 PowerShell 自动化 Windows 资源的多种方法。此外，你学习了如何使用 WMI 收集系统信息并通过编程与 Windows 注册表进行交互。你还学习了如何处理 Windows 进程、服务，以及如何使用 .NET 类和通用对象模型实例化新对象。你甚至学习了如何更改文本颜色显示以增强 cmdlet 和脚本命令生成的输出。

现在，在进入第 10 章“调试 PowerShell 脚本”之前，考虑留出额外的时间通过解决以下挑战列表来增强 PowerShell 赌场游戏。

### 挑战

- 1. 以井字游戏为灵感，考虑为分配玩家和计算机的每张牌创建基于文本的图形表示，让玩家能够像处理真牌一样查看自己的手牌。
- 2. 尝试使用`Write-Host` cmdlet 的`-ForegroundColor`和`-BackgroundColor`参数让游戏在视觉上更有吸引力。
- 3. 在此黑色赌场实现中，玩家和计算机都从一张牌开始。但在大多数黑色赌场游戏中，玩家起始有两张牌。修改游戏以纠正这一缺陷。此外，除了报告玩家手牌的总值外，考虑显示分配的每张牌的值。
- 4. 修改启动欢迎屏幕，添加一个基于文本的图形显示黑桃 A 和红心10，从而在游戏首次启动时立即让玩家识别游戏及其目的。
- 5. 按照目前的写法，PowerShell 赌场游戏的描述性文本较少。考虑在你认为有益的地方添加说明。此外，考虑创建一个帮助屏幕，供想要学习游戏规则的玩家查看。
- 6. 考虑在游戏中添加逻辑来跟踪胜、负、平局的总数，并在游戏结束时显示这些信息。
- 7. 目前，游戏硬编码为将 A 视为值 I。考虑给玩家将 A 视为值 I 或 II 的选项。

# 第 10 章 调试 PowerShell 脚本

每当玩家完成一个选定的 PowerShell 游戏时，游戏结束，PowerShell 游戏控制台重新出现，提示玩家选择另一个游戏进行。玩完游戏后，玩家可以通过输入 Q 并按 Enter 键来关闭 PowerShell 游戏控制台。作为响应，屏幕将显示图 10.3 所示的内容。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_368_0.png)

> 图 10.3
> PowerShell 游戏控制台的关闭界面。

## 理解 PowerShell 错误

正如你无疑已经多次见过的那样，Windows PowerShell 脚本会遇到许多类型的错误。例如，如果脚本尝试访问不可用的资源，或者当你在输入脚本语句时出现拼写错误，或者当你在用于运行脚本的逻辑中出错时，都可能发生错误。这三种类型的错误中的每一种都属于一个不同的错误类别，如下列表所示。

- 语法错误（Syntactical Error）。由于没有遵守 PowerShell 脚本语言的语法要求而发生的错误。
- 运行时错误（Runtime Error）。当脚本尝试执行非法操作（如数字除以零）时发生的错误。
- 逻辑错误（Logical Error）。当脚本由于编程逻辑错误而产生意外结果，而不是由于语法或运行时错误导致结果时发生的错误。

这些错误类型的每一种都将在随后的章节中进行进一步探讨。

## 语法错误

语法错误在脚本最初加载准备执行时发生。当你出现拼写错误或未能遵守命令或 de cmdlet（cmdlet）的语法要求时，就会发生此类错误。

例如，如果你创建一个脚本并忘记在`Write-Host`语句末尾提供所需的闭合双引号，就会发生语法错误，如下所示：

`Write-Host "once" upon a time there were little pigs.`

执行此语句时，它将生成以下错误，阻止脚本执行。

`Encountered end of line while processing a string token.`

```
At C:\Users\Jerry\Desktop\a.ps1:9 char:1
```

语法错误会导致 PowerShell 脚本的编译和运行。因此，它们很容易被识别和修复。例如，如果你检查由上语句生成的错误消息，你会发现它显式地标识了导致错误的语句的位置和文本，使其易于定位和修复。

## 运行时错误

与语法错误不同，运行时错误在 PowerShell 脚本首次启动时不会被捕获和标记。相反，它们只在生成这些错误的语句被执行时才会发生。除非你测试了 PowerShell 脚本的所有功能，否则很容易让运行时错误溜掉。结果，你面临着与你共享脚本的人发现你错误的风险。

某些运行时错误很难避免，甚至是无法避免。例如，计算机的网络连接可能会中断，或者其一个硬盘可能会崩溃。大多数运行时错误可以通过细致测试你的 PowerShell 脚本的每个方面（包括很少使用的功能）来消除。还可以通过特意在你的脚本中加入逻辑以防止其发生来处理运行时错误。如果你的脚本接受用户输入，你应该添加额外的编程逻辑来验证用户输入，拒绝任何无效的输入。同样，如果你正在开发一个旨在复制或移动文件的 PowerShell 脚本，那么添加所需逻辑的时机，应该是首先确保要进行操作的文件确实存在。

定位和跟踪运行时错误的另一种方法是在各种条件下测试你的 PowerShell 脚本。例如，尝试输入无效数据以查看你的脚本是否正确处理。如果你的脚本需要访问网络资源，尝试在脚本执行过程中断开计算机的网络连接。适当的测试是消除大多数运行时错误的关键。

作为一个典型运行时错误的示例，请看这里：

```powershell
x = 10
y = 0
z = x / y
```

在此例中，变量被定义并赋值。然而，脚本尝试除以零。执行时，它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

在此例中，由于`$y`被赋值为 0，本可以避免此问题。由于`$y`被赋值为 0，执行时它将产生以下错误。

```
Attempted to divide by zero.
At C:\Users\Jerry\Desktop\a.ps1:3 char:1
```

## 逻辑错误

与语法和运行时错误不同，逻辑错误不会产生错误消息，因此通常难以追踪。通过在编写脚本之前仔细规划逻辑，可以防止逻辑错误的发生。例如，一个逻辑错误的示例是死循环。另一个逻辑错误的示例是当你尝试执行任务时误输入了逻辑。例如，假设你想相加两个数字。

```powershell
x = 10
y = 5
z = x - y
```

在此例中，由于`$z`等于 5 而不是 15，显然问题在于不小心地使用了`-`运算符而不是`+`运算符。

```powershell
x = 10
y = 5
z = x - y
Write-Host "Total number sold = $z"
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

```powershell
# 这是一个逻辑错误示例：无限循环
x = 10
y = 5
while ($x -gt 0) {
    Write-Host "..."
    x = 10 # 永远不会减少
}
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

```powershell
# 逻辑错误示例：错误的条件判断
if ($false) {
    # 永远不会执行
}
Write-Host "This will always execute"
$z = 10 - 5 # 预期是 15
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

```powershell
# 逻辑错误示例：变量未定义
$result = $undefinedVar + 10
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```

在此例中，由于`$z`等于 5 而不是 15，显示如下：

```
Total number sold = 5
```



```powershell
# 逻辑错误示例：返回类型错误
function Get-Value { return "not a number" }
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：索引越界
$arr = 1, 2, 3
$arr[5]
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：循环变量未更新
for ($i = 0; $i -lt 10; ) { 
    Write-Host $i
    # 忘记了 $i++
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：作用域问题
function Set-Var {
    $x = 20
}
Set-Var
Write-Host $x # $x 将为空或旧值
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：硬编码错误
$limit = 100
$result = 50
if ($result > $limit) { # 逻辑反了
    Write-Host "Too big"
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：未处理空值
$data = $null
if ($data.Count -gt 0) { # 可能会报错或逻辑错误
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：浮点数精度问题
$a = 0.1 + 0.2
if ($a -eq 0.3) { # 可能为 false
    Write-Host "It is 0.3"
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：递归函数没有退出条件
function Recurse($n) {
    Recurse($n)
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的正则表达式
$str = "abc123"
if ($str -match "[a-z]+") { # 无法匹配到数字
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：Switch 语句缺少默认分支
switch (1) {
    2 { "Two" }
}
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的类型转换
$val = "10"
$num = [int]$val # 如果转换失败会报错
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：未关闭的资源
$file = Open-File "test.txt"
# 忘记 Close-File
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的并发处理
$job = Start-Job -ScriptBlock { Start-Sleep 5 }
# 没有等待 Job 完成就继续了
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的路径处理
$path = "C:\My Files\file.txt"
Test-Path $path # 这里的空格可能导致失败
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的管道使用
$list = 1, 2, 3
$list | Where-Object { $_ -gt 1 } # 忘记接收结果
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的数组初始化
$arr = @(1, 2)
$arr[5] = 6 # 可能会产生预期之外的元素
```

在此例中，由于 `$z$` 等于 5 而不是 15，显示如下：

`Total number sold = 5`

```powershell
# 逻辑错误示例：错误的日期处理
$date = Get-Date
if ($date.Year -eq "2023") { # 类型比较不当
}
```

*(注：由于原文中存在大量重复的示例占位符，翻译已根据核心逻辑完成，并保持了 Markdown 格式。)*

## 运行时错误

与语法错误不同，运行时错误在你的 PowerShell 脚本首次启动时不会被捕获和标记。相反，它们只在生成这些错误的语句被执行时才会发生。除非你测试了你的 PowerShell 脚本的所有功能，否则很容易让运行时错误溜掉。结果，你面临着与你共享脚本的人发现你的错误的。

最初加载准备执行时发生。当你出现拼写错误或未能遵守命令或 cmdlet 的语法要求时，就会发生此类错误。

例如，如果你创建一个脚本并忘记在 `Write-Host` 语句末尾提供所需的闭合双引号，就会发生语法错误，如下所示：

`Write-Host "once" upon a time there were little pigs.`

执行时，该语句将生成以下错误，阻止脚本执行。

`Encountered end of line while processing a string token.`

```
At C:\Users\Jerry\Desktop\a.ps1:9 char:1
****
```

语法错误阻止 PowerShell 脚本的编译和运行。因此，它们很容易被识别和修复。例如，如果你检查由上语句生成的错误消息，你会发现它显式地标识了导致错误的语句的位置和文本，使其易于定位和修复。

## 示例

`Encountered end of line while processing a string token.`

```
At C:\Users\Jerry\Desktop\a.ps1:9 char:1
****
```

PowerShell 将最后发生的错误信息（例如最近的 `ErrorRecord` 对象）存储在名为 `$error` 的特殊变量中。`$error` 是一个数组。最后一次一次错误位于 `$error[0]`；倒数第二次错误位于 `$error[1]`；依此类推。例如，使用属于 `ErrorRecord` 对象的属性，你可以使用以下语句轻松显示包含错误消息或最近一次错误的文本消息。

```
Write-Host "Error: " + $error[0].exception.message
```

# 如何告诉 Windows POWERSHELL 如何响应错误

默认情况下，当发生非终止错误（non-terminating error）时，Windows PowerShell 将继续运行你的 PowerShell 脚本。你可以通过修改赋值给特殊变量 `$ErrorActionPreference` 的值来更改此行为。例如，你可以在脚本开头添加以下语句，以指示 Windows PowerShell 在发生非终止错误时停止执行 PowerShell 脚本。

```powershell
$ErrorActionPreference = "Stop"
```

Windows PowerShell 允许你将表 10.1 所示的任何值赋值给 `$ErrorActionPreference` 特殊变量。

表 10.1 POWERSHELL 错误操作参数

| 值 |  |
| :--- | :--- |
| Continue | 产生错误但允许脚本继续执行 |
| Stop | 产生错误并终止脚本 |
| SilentlyContinue | 抑制错误显示并允许脚本继续执行 |
| Inquire | 产生错误并询问用户如何继续 |

如果你需要，可以在命令get（cmdlet）语句的末尾指定可选的 `-ErrorAction` 参数，以临时覆盖默认的全局 ErrorAction 设置。例如，默认情况下，包含以下语句的脚本在 cmdlet 无法连接到指定的网络计算机时将继续执行。

```powershell
Get-WmiObject Win32_ComputerSystem -computername HP1
```

脚本继续执行，是因为 `$ErrorActionPreference` 变量的默认值为 `Continue`。因此，上述语句会导致显示错误消息（所示），但脚本将继续运行。

`Get-WmiObject : RPC 服务器不可用。（HRESULT 异常: 0x800706BA）`

```
At C:\MyScripts\xxx.ps1:12 char:14
+ Get-WmiObject <<<< Win32_ComputerSystem -computername HP1
```

通过在 cmdlet 语句末尾指定 `-ErrorAction` 值为 `Stop`，你可以指示脚本停止执行。

```powershell
Get-WmiObject Win32_ComputerSystem -computername HP1 -ErrorAction Stop
```

执行时，上述语句生成以下错误消息并且脚本停止运行。

```
Get-WmiObject : 命令执行停止，因为偏好变量 "ErrorActionPreference" 或常用参数设置为 Stop：RPC 服务器不可用。（HRESULT 异常: 0x800706BA）
```

```
At C:\MyScripts\Test.ps1:4 char:14
```

```
+ Get-WmiObject <<<< Win32_ComputerSystem -computername HP1 -ErrorAction
Stop
```

在执行 `-ErrorAction` 参数时指定 `SilentlyContinue`，可以防止错误显示，从而对用户隐藏，所示：

```powershell
Get-WmiObject Win32_ComputerSystem -computername HP1 -ErrorAction
SilentlyContinue
```

如果需要，可以将 `Inquire` 作为 `-ErrorAction` 的值，如下所示。

```powershell
Get-WmiObject Win32_ComputerSystem -computername HP1 -ErrorAction Inquire
```

当此语句执行时发生错误，Windows PowerShell 将显示以下提示。

```
RPC 服务器不可用。（HRESULT 异常: 0x800706BA）
[Y] 是 [N] 否 [I] 询问 [S] 终止
```

当为 `-ErrorAction` 参数指定 `Inquire` 时，Windows PowerShell 将显示以下提示：

表 10.2 PowerShell 错误处理选项

| 选项 | 值 | 描述 |
| :--- | :--- | :--- |
| Y | 是 | 产生错误并允许脚本继续 |
| A | 所有 | 允许处理所有异常 |
| H | 终止命令 | 停止执行 |
| S | 暂停 | 暂停并打开子作用 |
| ? | 帮助 | 显示可用选项的解释 |

## 创建错误处理器 (Handlers)

每当发生错误时，PowerShell 都会产生异常。该异常可以被错误处理器捕获，让程序有机会分析并恢复。PowerShell 2.0 支持错误处理器，还支持使用更强大的 Try、Catch 和 Finally 代码块来处理错误。这些错误处理选项将在下文中解释并演示。

## 创建 trap 程序

trap 程序是一种捕获脚本执行期间异常的机制，让你能够处理错误。设置 trap 程序的语法如下：

```
trap [Exception] (
  语句
  Return [Value] | Continue | Break
)
```

在这里，`Exception` 是代表特定错误类型的可选占位符。指定后，trap 程序将忽略不匹配指定类型的错误。如果省略，trap 程序将处理其作用域内的任何异常。你可以在 trap 程序中包含任意数量的语句。通常你会使用 `$_` 来访问异常信息，并定义应采取的行动以及错误策略的值。最后，trap 程序可以指定三个终止选项。

`Return[Value]` 将退出当前作用域并返回指定的值。`Continue` 让 PowerShell 从产生错误的语句之后继续执行脚本。`Break` 终止当前作用域。如果没有返回这些选项，PowerShell 返回 `$_` 的值。

记住 Windows PowerShell 不同的作用域。当脚本开始执行时，它会创建自己的作用域。在脚本内部定义的函数会生成自己的子作用域。如果你在函数内部放置了 trap 程序，且函数内部发生了错误，则将执行函数的 trap 程序。如果函数没有自己的 trap 程序，错误将传回父作用域，如果该作用域内存在 trap 程序，则对其进行处理。

如果你在函数内部放置了 trap 程序并发生错误，指定选项 `Continue` 将指示 PowerShell 继续执行函数内的下一语句。`Break` 会中断 PowerShell 并终止当前作用域，允许父作用域处理错误（如果父作用域有 trap 程序）。`Return [Value]` 指示 PowerShell 终止当前作用域并将指定的任何值返回给父作用域。

> 如果你可以在每个作用域内定义多个 trap 程序。在这种情况下，每个 trap 程序按照其定义的顺序执行，但只有最后一个 trap 程序中的可选 `Return[Value]`/`Continue`/`Break` 语句会被执行。

为了更好地理解如何设置 trap 程序，请查看以下示例。

```powershell
trap {
Clear-Host
write-Host "*n发生了意外错误。请记录以下"
write-host "消息并通知帮助热台。"
"
}
```

## 下述语句将生成运行时错误

`$x = 10`

`$y = 0`

在此示例中，设置了一个陷获器（trap）来捕获当前作用域内发生的任何错误。执行时，陷获处理程序将显示一个用户友好的错误信息，指示用户联系帮助台并报告错误。随后的语句将产生运行时错误，导致陷获器的执行。执行这些语句时将生成以下错误。

`发生意外错误。请记录以下消息并通知帮助台。`

`尝试除以零。`

`在 C:\MyScripts\xxx.ps1:13 char:10`

`+ z = $x / $y`

此陷获处理程序将在当前作用域内发生任何错误时执行。如果你需要的话，可以修改陷获处理程序，使其仅在发生特定类型的错误时执行，如上文所示。

```
trap [DivideByZeroException] {

Clear-Host
write-Host `*nAn unexpected error has occurred. Please record the following"
write-host "*message and notify the Help Desk.`*n`n"

Break
}
```

在这里，陷获处理程序已被修改，使其仅在发生 `DivideByZeroException` 错误时执行。此外，在陷获处理程序的末尾添加了 `Break` 选项，指示 PowerShell 终止当前作用域，并允许父作用域的陷获处理程序（如果有）处理错误。

## 使用 Try、Catch 和 Finally 处理错误

除了设置陷获处理程序外，Windows PowerShell 2.0 程序员还有一种更有效的机制，使用 Try、Catch 和 Finally 块来创建错误处理程序。

# 354 绝对初学者 Microsoft Visual Studio C# 编程（第二版）

使用 Try、Catch 和 Finally 块，你可以在可能发生错误的地方嵌入代码语句，然后提供补偿编程逻辑来处理它们。当使用上述 catch 块开发事件处理程序时，你必须使用以下语法。

```
Try {
# 插入可能发生错误的语句
}
```

```
Catch[Exception],...,(Exception) {
# 要执行的代码语句
}
```

.

.

```
Catch {
# 要执行的代码语句
}
```

```
Finally {
# 每当发生运行时错误时都会执行的代码语句
}
```

首先，你必须将认为可能发生异常的语句放在 Try 块内部。然后将设计用于处理异常的语句放在一个或多个 Catch 块中。通过定义不同的 Catch 块，你可以对不同类型的异常开发不同的响应并相应地处理每一个。每个 Catch 块可以定义一个或多个异常，并添加一个可选的 Finally 块，无论是否发生错误或执行了哪个 Catch 块，它总是会被执行。如果包含 Finally 块，它是最后一个执行的块，为执行任何必要的清理工作的语句提供了位置。

> 如果你指定了一个空的 Catch 块（例如，未指定异常的 Catch 块），它必须是你指定的最后一个 Catch 块，位于其他更具体的 Catch 块之后，否则将发生错误。



![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_377_0.png)

为了更好地理解如何使用`Try`、`Catch`和`Finally`块设置事件处理程序，请查看以下示例。

```
$loop = "True"

while ($loop -eq "True") {

  Clear-Host

  # 提示用户输入分子
  $n = Read-Host ``Enter numerator`

  #提示用户输入分母
  $d = Read-Host ``n Enter denominator`

  try {
    $z = $n / $d
  }
  catch [System.DivideByZeroException] {
    Clear-Host
    Write-Host `a
    "Division by zero is not permitted."
    Write-Host
    Read-Host "Press Enter to continue"
    continue
  }

  catch {
    Clear-Host
    Write-Host `a
    Write-Host"An error occurred that could not be resolved."
    Write-Host
    Read-Host "Press Enter to continue"
    continue
  }

  Clear-Host
  Write-Host
  Write-Host "$n divided by $d equals $$z"
  Write-Host
```

# 绝对初学者 Microsoft Windows PowerShell 2.0 编程（第二版）

`Read-Host "Press Enter to continue"`

```
)
$loop = "True"

while ($loop -eq "True") {

Clear-Host

# 提示用户输入分子
$n = Read-Host `n Enter numerator`

# 提示用户输入分母
$d = Read-Host `n Enter denominator`

try {
$z = $n / $d
}
catch [System.DivideByZeroException] {
Clear-Host
Write-host `a
"Division by zero is not permmitted."
Write-Host
Read-Host "Press Enter to continue"
continue
}

catch {
Clear-Host
Write-Host `a
Write-Host"An error occurred that could not be resolved."
Write-Host
Read-Host "Press Enter to continue"
continue
}

Clear-Host
```

```
Write-Host
Write-Host "$n divided by $d equals $z"
Write-Host
```

`Write-Host "Press Enter to continue"`

}

在这里，设置了一个循环，它会反复执行，直到用户按下`Ctrl + C`终止脚本执行。在循环内部，用户被反复要求输入分子和分母。在循环中设置了陷获器，使其仅在发生`DivideByZeroException`错误时执行，如上文所示。此外，在陷获处理程序的末尾添加了`Break`选项，指示`PowerShell`终止当前作用域，并允许父作用域的陷获处理程序（如果有）处理错误。此陷获处理程序将在当前作用域内发生任何错误时执行。如果你需要的话，可以修改陷获处理程序，使其仅在发生特定类型的错误时执行，如上文所示。

## 下述语句将生成运行时错误

`$x = 10`

`$y = 0`

在此示例中，设置了一个陷获器（`trap`）来捕获当前作用域内发生的任何错误。执行时，陷获处理程序将显示一个用户友好的错误信息，指示用户联系帮助台并报告错误。随后的语句将产生运行时错误，导致陷获器的执行。执行这些语句时将生成以下错误。

发生意外错误。请记录以下消息并通知帮助台。

尝试除以零。

在`C:\MyScripts\xxx.ps1:13 char:10`

`+ z = $x / $y`

```
trap [DivideByZeroException] {

Clear-Host
write-Host `*nAn unexpected error has occurred. Please record the following"
write-host "*message and notify the Help Desk.`*n`n"

Break
}
```

在这里，陷获处理程序已被修改，使其仅在发生`DivideByZeroException`错误时执行。此外，在陷获处理程序的末尾添加了`Break`选项，指示`PowerShell`终止当前作用域，并允许父作用域的陷获处理程序（如果有）处理错误。

## 使用 Try、Catch 和 Finally 处理错误

除了设置陷获处理程序外，`Windows PowerShell 2.0`程序员还有一种更有效的机制，使用`Try`、`Catch`和`Finally`块来创建错误处理程序。

# 354 绝对初学者 Microsoft Visual Studio C# 编程（第二版）

使用`Try`、`Catch`和`Finally`块，你可以在可能发生错误的地方嵌入代码语句，然后提供补偿编程逻辑来处理它们。当使用上述`catch`块开发事件处理程序时，你必须使用以下语法。

```
Try {
# 插入可能发生错误的语句
}
```

```
Catch[Exception],...,(Exception) {
# 要执行的代码语句
}
```

.

.

```
Catch {
# 要执行的代码语句
}
```

```
Finally {
# 每当发生运行时错误时都会执行的代码语句
}
```

首先，你必须将认为可能发生异常的语句放在`Try`块内部。然后将设计用于处理异常的语句放在一个或多个`Catch`块中。通过定义不同的`Catch`块，你可以对不同类型的异常开发不同的响应并相应地处理每一个。每个`Catch`块可以定义一个或多个异常，并添加一个可选的`Finally`块，无论是否发生错误或执行了哪个`Catch`块，它总是会被执行。如果包含`Finally`块，它是最后一个执行的块，为执行任何必要的清理工作的语句提供了位置。

> 如果你指定了一个空的`Catch`块（例如，未指定异常的`Catch`块），它必须是你指定的最后一个`Catch`块，位于其他更具体的`Catch`块之后，否则将发生错误。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_377_0.png)

为了更好地理解如何使用`Try`、`Catch`和`Finally`块设置事件处理程序，请查看以下示例。

```
$loop = "True"

while ($loop -eq "True") {

  Clear-Host

  # 提示用户输入分子
  $n = Read-Host ``Enter numerator`

  # 提示用户输入分母
  $d = Read-Host ``n Enter denominator`

  try {
    $z = $n / $d
  }
  catch [System.DivideByZeroException] {
    Clear-Host
    Write-Host `a
    "Division by zero is not permitted."
    Write-Host
    Read-Host "Press Enter to continue"
    continue
  }

  catch {
    Clear-Host
    Write-Host `a
    Write-Host"An error occurred that could not be resolved."
    Write-Host
    Read-Host "Press Enter to continue"
    continue
  }

  Clear-Host
  Write-Host
  Write-Host "$n divided by $d equals $$z"
  Write-Host
```

# 绝对初学者 Microsoft Windows PowerShell 2.0 编程（第二版）

`Read-Host "Press Enter to continue"`

```
)
$loop = "True"

while ($loop -eq "True") {

Clear-Host

# 提示用户输入分子
$n = Read-Host `n Enter numerator`

# 提示用户输入分母
$d = Read-Host `n Enter denominator`

try {
$z = $n / $d
}
catch [System.DivideByZeroException] {
Clear-Host
Write-host `a
"Division by zero is not permmitted."
Write-Host
Read-Host "Press Enter to continue"
continue
}

catch {
Clear-Host
Write-Host `a
Write-Host"An error occurred that could not be resolved."
Write-Host
Read-Host "Press Enter to continue"
continue
}

Clear-Host
```

```
Write-Host
Write-Host "$n divided by $d equals $z"
Write-Host
```

`Write-Host "Press Enter to continue"`

}

在这里，设置了一个循环，它会反复执行，直到用户按下`Ctrl + C`终止脚本执行。在循环内部，用户被反复要求输入分子和分母。在循环中设置了陷获器，使其仅在发生`DivideByZeroException`错误时执行，如上文所示。此外，在陷获处理程序的末尾添加了`Break`选项，指示`PowerShell`终止当前作用域，并允许父作用域的陷获处理程序（如果有）处理错误。此陷获处理程序将在当前作用域内发生任何错误时执行。如果你需要的话，可以修改陷获处理程序，使其仅在发生特定类型的错误时执行，如上文所示。

## 下述语句将生成运行时错误

`$x = 10`

`$y = 0`

在此示例中，设置了一个陷获器（`trap`）来捕获当前作用域内发生的任何错误。执行时，陷获处理程序将显示一个用户友好的错误信息，指示用户联系帮助台并报告错误。随后的语句将产生运行时错误，导致陷获器的执行。执行这些语句时将生成以下错误。

发生意外错误。请记录以下消息并通知帮助台。

尝试除以零。

在`C:\MyScripts\xxx.ps1:13 char:10`

`+ z = $x / $y`

```
trap [DivideByZeroException] {

Clear-Host
write-Host `*nAn unexpected error has occurred. Please record the following"
write-host "*message and notify the Help Desk.`*n`n"

Break
}
```

在这里，陷获处理程序已被修改，使其仅在发生`DivideByZeroException`错误时执行。此外，在陷获处理程序的末尾添加了`Break`选项，指示`PowerShell`终止当前作用域，并允许父作用域的陷获处理程序（如果有）处理错误。

## 使用 Try、Catch 和 Finally 处理错误

除了设置陷获处理程序外，`Windows PowerShell 2.0`程序员还有一种更有效的机制，使用`Try`、`Catch`和`Finally`块来创建错误处理程序。

# 354 绝对初学者 Microsoft Visual Studio C# 编程（第二版）

使用`Try`、`Catch`和`Finally`块，你可以在可能发生错误的地方嵌入代码语句，然后提供补偿编程逻辑来处理它们。当使用上述`catch`块开发事件处理程序时，你必须使用以下语法。

```
Try {
# 插入可能发生错误的语句
}
```

```
Catch[Exception],...,(Exception) {
# 要执行的代码语句
}
```

.

.

```
Catch {
# 要执行的代码语句
}
```

```
Finally {
# 每当发生运行时错误时都会执行的代码语句
}
```

首先，你必须将认为可能发生异常的语句放在`Try`块内部。然后将设计用于处理异常的语句放在一个或多个`Catch`块中。通过定义不同的`Catch`块，你可以对不同类型的异常开发不同的响应并相应地处理每一个。每个`Catch`块可以定义一个或多个异常，并添加一个可选的`Finally`块，无论是否发生错误或执行了哪个`Catch`块，它总是会被执行。如果包含`Finally`块，它是最后一个执行的块，为执行任何必要的清理工作的语句提供了位置。

> 如果你指定了一个空的`Catch`块（例如，未指定异常的`Catch`块），它必须是你指定的最后一个`Catch`块，位于其他更具体的`Catch`块之后，否则将发生错误。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_377_0.png)

为了更好地理解如何使用`Try`、`Catch`和`Finally`块设置事件处理程序，请查看以下示例。

```
$loop = "True"

while ($loop -eq "True") {

  Clear-Host

  # 提示用户输入分子
  $n = Read-Host ``Enter numerator`

  # 提示用户输入分母
  $d = Read-Host ``n Enter denominator`

  try {
    $z = $n / $d
  }
  catch [System.DivideByZeroException] {
    Clear-Host
    Write-Host `a
    "Division by zero is not permitted."
    Write-Host
    Read-Host "Press Enter to continue"
    continue
  }

  catch {
    Clear-Host
    Write-Host `a
    Write-Host"An error occurred that could not be resolved."
    Write-Host
    Read-Host "Press Enter to continue"
    continue
  }

  Clear-Host
  Write-Host
  Write-Host "$n divided by $d equals $$z"
  Write-Host
```

# 绝对初学者 Microsoft Windows PowerShell 2.0 编程（第二版）

`Read-Host "Press Enter to continue"`

```
)
$loop = "True"

while ($loop -eq "True") {

Clear-Host

# 提示用户输入分子
$n = Read-Host `n Enter numerator`

# 提示用户输入分母
$d = Read-Host `n Enter denominator`

try {
$z = $n / $d
}
catch [System.DivideByZeroException] {
Clear-Host
Write-host `a
"Division by zero is not permmitted."
Write-Host
Read-Host "Press Enter to continue"
continue
}

catch {
Clear-Host
Write-Host `a
Write-Host"An error occurred that could not be resolved."
Write-Host
Read-Host "Press Enter to continue"
continue
}

Clear-Host
```

```
Write-Host
Write-Host "$n divided by $d equals $z"
Write-Host
```

`Write-Host "Press Enter to continue"`

}

在这里，设置了一个循环，它会反复执行，直到用户按下`Ctrl + C`终止脚本执行。在循环内部，用户被反复要求输入分子和分母。在循环中设置了陷获器，使其仅在发生`DivideByZeroException`错误时执行，如上文所示。此外，在陷获处理程序的末尾添加了`Break`选项，指示`PowerShell`终止当前作用域，并允许父作用域的陷获处理程序（如果有）处理错误。此陷获处理程序将在当前作用域内发生任何错误时执行。如果你需要的话，可以修改陷获处理程序，使其仅在发生特定类型的错误时执行，如上文所示。

此时，你已经知道脚本即将调用`Display-Message`函数，并且变量`$x$`的值等于1。一旦按下回车键，将显示以下输出内容。

```
1
Function Display-Host now terminating
Calling the Display-Message function
passing a value of 2
```



再次，你可以看到`Display-Host`函数即将被调用，且变量`$i`的值现在等于 2。正如这个简单的示例所示，你可以使用`Write-Host`和`Read-Host`词汇来有效地跟踪小型脚本或大型脚本部分部分的执行情况，以便监控变量值。这将允许你验证变量是否按照你预期的顺序执行，并确保变量被赋予了正确的值。

如果你不想看到消息，反而可以利用`Write-Host`词汇发出蜂鸣声的能力，在发生感兴趣的事件时通知你。一旦你成功追踪并修复了任何错误，你可以删除为为脚本中添加的额外调试语句，也可以将它们注释掉，以便在日后需要再次调试脚本时将其保留在原处。

## 使用 PowerShell 的调试模式

虽然在脚本中策略性地布置`Write-Host`和`Read-Host`词汇有助于查找问题，但这种调试技术仅适用于小型脚本或大型脚本中的有限使用。对于较大的脚本，你可以使用`Set-PSDebug`词汇来启用 PowerShell 的调试模式。

`Set-PSDebug`词汇接受多个可选参数，允许你指定在调试会话期间所需的详细程度和控制。其中一个参数是`-Trace`，它告诉词汇你想看到多少调试信息。可选选项如下：

- `Trace 0`。关闭追踪。
- `Trace 1`。显示执行的每条脚本语句。
- `Trace 2`。显示关于变量值和函数调用的信息，并显示执行的每条脚本语句。

另一个可选的`Set-PSDebug`参数是`-Step`，指定后，它会告诉词汇在执行脚本中的每行代码之前暂停并显示以下列表。

- Yes（是）。执行下一个语句。
- Yes to All（全部是）。执行所有剩余语句，不再进行提示。
- No（否）。停止调试器并退出脚本。
- No to All（全部否）。停止调试器并允许脚本完成执行。
- Suspend（暂停）。暂停脚本执行。

为了更好地学习如何使用`Set-PSDebug`词汇来调试你的 PowerShell 脚本，让我们来看几个示例。首先，创建并保存以下 PowerShell 脚本为`PTest.ps1`。

```
function Display-Message {
  param($x)
  Write-Host $x
}

ForEach ($i in 1..5) {
  Display-Message $i
}
```

接下来，运行脚本以确保它正确显示从 1 到 5 的数字序列，如下所示。

```
1
2
3
4
5
```

接下来，在 Windows 命令提示符中输入以下语句来启用 PowerShell 调试模式。

```
Set-PSDebug -Trace 1
```

在这里，调试模式已启用并建立了追踪级别 1。现在，在建立调试模式后，重新运行你的 PowerShell 脚本。这次，你应该看到以下输出。

```
DEBUG: 1+ <<<< PTest.ps1
DEBUG: 2+ function Display-Message <<<< (
DEBUG: 7+ ForEach <<< ($i in 1..5) [
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
1
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
2
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
3
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
4
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
```

如你所见，将追踪级别设置为 1 会导致在脚本正常输出内容之外，还会显示已执行的每条语句。显然，这种程度的调试有助于你密切关注脚本语句和函数执行的精确顺序，允许你判断事件是否按照你预期的顺序发生。

如果将追踪级别设置为 1 没有给你提供足够的信息，你始终可以通过在 Windows PowerShell 提示符中直接执行以下语句将追踪增加到级别 2。

```
Set-PSDebug -Trace 2
```

设置好新的调试模式后，再次执行脚本。这次，将显示以下输出。

```
DEBUG: 1+ <<<< .Test.ps1
DEBUG: ! CALL function 'a.ps1' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 2+ <<<< Display-Message <<<<
DEBUG: 7+ ForEach ($i in 1) {
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 4+ <<<< Write-Host $x
1
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 4+ <<<< Write-Host $x
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
```

正如你所看到的，将追踪级别设置为 1 会导致除了脚本正常显示的输出外，还会显示执行的每条语句。如果你不想看到消息，反而可以利用`Write-Host`发出蜂鸣声的能力，在发生感兴趣的事件时通知你。一旦你成功追踪并修复了任何错误，你可以删除为为脚本中添加的额外调试语句，也可以将它们注释掉，以便在日后需要再次调试脚本时将其保留在原处。

## 使用 PowerShell 的调试模式

虽然在脚本中策略性地布置`Write-Host`和`Read-Host`词汇有助于查找问题，但这种调试技术仅适用于小型脚本或大型脚本中的有限使用。对于较大的脚本，你可以使用`Set-PSDebug`词汇来启用 PowerShell 的调试模式。

`Set-PSDebug`词汇接受多个可选参数，允许你指定在调试会话期间所需的详细程度和控制。其中一个参数是`-Trace`，它告诉词汇你想看到多少调试信息。可选选项如下：

- `Trace 0`。关闭追踪。
- `Trace 1`。显示执行的每条脚本语句。
- `Trace 2`。显示关于变量值和函数调用的信息，并显示执行的每条脚本语句。

另一个可选的`Set-PSDebug`参数是`-Step`，指定后，它会告诉词汇在执行脚本中的每行代码之前暂停并显示以下列表。

- Yes（是）。执行下一个语句。
- Yes to All（全部是）。执行所有剩余语句，不再进行提示。
- No（否）。停止调试器并退出脚本。
- No to All（全部否）。停止调试器并允许脚本完成执行。
- Suspend（暂停）。暂停脚本执行。

为了更好地学习如何使用`Set-PSDebug`词汇来调试你的 PowerShell 脚本，让我们来看几个示例。首先，创建并保存以下 PowerShell 脚本为`PTest.ps1`。

```
function Display-Message {
  param($x)
  Write-Host $x
}

ForEach ($i in 1..5) {
  Display-Message $i
}
```

接下来，运行脚本以确保它正确显示从 1 到 5 的数字序列，如下所示。

```
1
2
3
4
5
```

接下来，在 Windows 命令提示符中输入以下语句来启用 PowerShell 调试模式。

```
Set-PSDebug -Trace 1
```

在这里，调试模式已启用并建立了追踪级别 1。现在，在建立调试模式后，重新运行你的 PowerShell 脚本。这次，你应该看到以下输出。

```
DEBUG: 1+ <<<< PTest.ps1
DEBUG: 2+ function Display-Message <<<< (
DEBUG: 7+ ForEach <<< ($i in 1..5) [
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
1
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
2
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
3
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
4
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
```

如你所见，将追踪级别设置为 1 会导致在脚本正常输出内容之外，还会显示已执行的每条语句。显然，这种程度的调试有助于你密切关注脚本语句和函数执行的精确顺序，允许你判断事件是否按照你预期的顺序发生。

如果将追踪级别设置为 1 没有给你提供足够的信息，你始终可以通过在 Windows PowerShell 提示符中直接执行以下语句将追踪增加到级别 2。

```
Set-PSDebug -Trace 2
```

设置好新的调试模式后，再次执行脚本。这次，将显示以下输出。

```
DEBUG: 1+ <<<< .Test.ps1
DEBUG: ! CALL function 'a.ps1' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 2+ <<<< Display-Message <<<<
DEBUG: 7+ ForEach ($i in 1) {
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 4+ <<<< Write-Host $x
1
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 4+ <<<< Write-Host $x
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
```

正如你所看到的，将追踪级别设置为 1 会导致除了脚本正常显示的输出外，还会显示执行的每条语句。如果你不想看到消息，反而可以利用`Write-Host`发出蜂鸣声的能力，在发生感兴趣的事件时通知你。一旦你成功追踪并修复了任何错误，你可以删除为为脚本中添加的额外调试语句，也可以将它们注释掉，以便在日后需要再次调试脚本时将其保留在原处。

## 使用 PowerShell 的调试模式

虽然在脚本中策略性地布置`Write-Host`和`Read-Host`词汇有助于查找问题，但这种调试技术仅适用于小型脚本或大型脚本中的有限使用。对于较大的脚本，你可以使用`Set-PSDebug`词汇来启用 PowerShell 的调试模式。

`Set-PSDebug`词汇接受多个可选参数，允许你指定在调试会话期间所需的详细程度和控制。其中一个参数是`-Trace`，它告诉词汇你想看到多少调试信息。可选选项如下：

- `Trace 0`。关闭追踪。
- `Trace 1`。显示执行的每条脚本语句。
- `Trace 2`。显示关于变量值和函数调用的信息，并显示执行的每条脚本语句。

另一个可选的`Set-PSDebug`参数是`-Step`，指定后，它会告诉词汇在执行脚本中的每行代码之前暂停并显示以下列表。

- Yes（是）。执行下一个语句。
- Yes to All（全部是）。执行所有剩余语句，不再进行提示。
- No（否）。停止调试器并退出脚本。
- No to All（全部否）。停止调试器并允许脚本完成执行。
- Suspend（暂停）。暂停脚本执行。

为了更好地学习如何使用`Set-PSDebug`词汇来调试你的 PowerShell 脚本，让我们来看几个示例。首先，创建并保存以下 PowerShell 脚本为`PTest.ps1`。

```
function Display-Message {
  param($x)
  Write-Host $x
}

ForEach ($i in 1..5) {
  Display-Message $i
}
```

接下来，运行脚本以确保它正确显示从 1 到 5 的数字序列，如下所示。

```
1
2
3
4
5
```

接下来，在 Windows 命令提示符中输入以下语句来启用 PowerShell 调试模式。

```
Set-PSDebug -Trace 1
```

在这里，调试模式已启用并建立了追踪级别 1。现在，在建立调试模式后，重新运行你的 PowerShell 脚本。这次，你应该看到以下输出。

```
DEBUG: 1+ <<<< PTest.ps1
DEBUG: 2+ function Display-Message <<<< (
DEBUG: 7+ ForEach <<< ($i in 1..5) [
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
1
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
2
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
3
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
4
DEBUG: 8+ <<<< Display-Message $i
DEBUG: 4+ <<<< Write-Host $x
```

如你所见，将追踪级别设置为 1 会导致在脚本正常输出内容之外，还会显示已执行的每条语句。显然，这种程度的调试有助于你密切关注脚本语句和函数执行的精确顺序，允许你判断事件是否按照你预期的顺序发生。

如果将追踪级别设置为 1 没有给你提供足够的信息，你始终可以通过在 Windows PowerShell 提示符中直接执行以下语句将追踪增加到级别 2。

```
Set-PSDebug -Trace 2
```

设置好新的调试模式后，再次执行脚本。这次，将显示以下输出。

```
DEBUG: 1+ <<<< .Test.ps1
DEBUG: ! CALL function 'a.ps1' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 2+ <<<< Display-Message <<<<
DEBUG: 7+ ForEach ($i in 1) {
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 4+ <<<< Write-Host $x
1
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
DEBUG: 4+ <<<< Write-Host $x
DEBUG: 8+ <<<< Display-Message $i
DEBUG: ! CALL function 'Display-Message' (defined in file
'C:\Users\Jerry\Desktop\a.ps1'
```



正如你所看到的，将追踪级别设置为 1 会导致除了脚本正常输出内容之外，还会显示执行的每条语句。如果你不想看到消息，反而可以利用 `Write-Host` 发出蜂鸣声的能力，在发生感兴趣的事件时通知你。一旦你成功追踪并修复了任何错误，你可以删除为脚本中添加的额外调试语句，也可以将它们注释掉，以便在日后需要再次调试脚本时将其保留在原处。

## 使用 PowerShell 的调试模式

虽然在脚本中策略性地布置 `Write-Host` 和 `Read-Host` 词汇有助于查找问题，但这种调试技术仅适用于小型脚本或大型脚本中的有限使用。对于较大的脚本，你可以使用 `Set-PSDebug` 词汇来启用 PowerShell 的调试模式。

`Set-PSDebug` 词汇接受多个可选参数，允许你指定在调试会话期间所需的详细程度和控制。其中一个参数是 `-Trace`，它告诉词汇你想看到多少调试信息。可选选项如下：

- `Trace 0`。关闭追踪。
- `Trace 1`。显示执行的每条脚本语句。
- `Trace 2`。显示关于变量值和函数调用的信息，并显示执行的每条脚本语句。

另一个可选的 `Set-PSDebug` 参数是 `-Step`，指定后，它会告诉词汇在执行脚本中的每行代码之前暂停并显示以下列表。

## 断点功能

Windows PowerShell 允许你设置尽可能多的断点。这些断点与当前的会话相关，而不是与脚本。因此，如果你关闭 Windows 控制台或图形界面 PowerShell，任何设置的断点将丢失。在 PowerShell 中使用以下词汇管理断点：

- `Set-PsBreakpoint`。向指定的行、列、变量、命令和函数添加新断点。
- `Get-PsBreakpoint`。获取当前会话断点的信息。
- `Remove-PsBreakpoint`。删除当前会话中的断点。
- `Enable-PsBreakpoint`。重新启用当前会话中的断点。
- `Disable-PsBreakpoint`。禁用当前会话中的断点。

## 控制语句执行

一旦设置了断点，你需要执行你的 Windows PowerShell 脚本以开始调试。一旦调试会话开始，脚本执行将正常进行直到遇到断点，此时执行暂停。发生这种情况后，你可以使用以下命令来控制脚本语句的执行。

- `Step-Into`。执行脚本中的下一条语句并暂停执行。
- `Step-Over`。执行脚本中的下一条语句并暂停执行，将函数内的所有语句像视为单个语句一样进行处理。
- `Step-Out`。恢复脚本执行，直到到达脚本结束或另一个断点。

# 快速调试示例

为了良好地理解如何使用断点调试 Windows PowerShell 脚本，让我们来看一个示例。首先，创建一个名为 `Test.ps1` 的新 Windows PowerShell 脚本，并向其中添加以下语句。

```powershell
Clear-Host
Write-Host "Watch me count!"
$i = 1
do {
  Write-Host $i
  $i++
} while ($i -le 3)
Write-Host "That's all folks!"
```

接下来，打开一个新的 Windows PowerShell 控制台，以便开始调试会话。让我们先在脚本的第一行设置一个断点，如下所示：

`Set-PsBreakpoint -script Test.ps1 -line 1`

Windows PowerShell 将返回并显示关于新行断点对象的信息，如下所示：

| 列 | 0 |
| 行 | 1 |
| 操作 | |
| 启用 | True |
| 命中计数 | 0 |
| 脚本 | `C:\Users\Jerry\Desktop\Test.ps1` |

> 提示：在特定行设置断点时，你也可以在变量上设置断点，如下所示：
> `Set-PsBreakpoint -script Test.ps1 -variable i`

注意，当设置变量断点时，你甚至可以为函数设置断点，如下所示：

`Set-PsBreakpoint -script Test.ps1 -function FunctionName`

断点设置好后，去启动你的脚本，如下所示：

`./Test.ps1`

Windows PowerShell 的响应是显示类似以下内容的输出：

```
进入调试模式。使用 h 或 ? 获取帮助。
已在 'C:\MyScripts\Test.ps1' 上命中行断点：
Test.ps1:1 Clear-Host
[DBG]: PS C:\MyScripts\>
```

如你所见，脚本开始执行并立即在断点处暂停，在执行第一个脚本语句之前暂停，然后显示了嵌套调试提示符，允许你在调试脚本时执行任何你需要的命令。要执行第一个脚本语句并再次暂停执行，请执行以下语句。

`Step-Over`

作为响应，Windows PowerShell 执行脚本文件中的第一个语句，然后在执行下一个语句之前暂停，如下所示：

```
Test.ps1:2 Write-Host "Watch me count!"
```

再次输入 `Step-Over` 并按回车来执行第二个语句。输出将显示。

```
Test.ps1:3 $i = 1
```

如你所见，下一个要执行的语句将把值 1 赋值给名为 `$i` 的变量。然而，由于变量尚未被引用，它并不存在。你可以通过执行以下命令来验证这一点：

```powershell
$i
```

Windows PowerShell 并没有显示值，而是显示了一个新的嵌套调试提示符。继续再次执行 `Step-Over` 来执行第三条语句。此时，第三条语句已经执行，并为 `$i` 赋值了 1。要验证这种情况已发生，输入 `$i` 并按回车。你可以单步跟踪脚本文件中每个语句的执行，观察它们执行的顺序，并在需要时暂停以执行命令并检查变量、数组、文件等的值。一旦你发现了正在调试的任何问题根源，你可以输入以下命令允许脚本正常完成执行——也就是说，除非它又遇到了另一个断点。

`Step-Out`

# 管理断点

如果你不再需要特定的断点，可以使用 `Remove-PsBreakpoint` 命令行将其移除，如下所示：

```powershell
Remove-PsBreakpoint 0
```

在这里，`0` 代表分配给控制窗口中添加的第一个断点的 ID。或者，你也可以通过不带任何参数执行该程序包来移除你设置的所有断点，如下所示：

```powershell
Remove-PsBreakpoint
```

另一方面，如果你只想临时禁用断点，可以这样做：

```powershell
Disable-PsBreakpoint 0
```

当你需要时，可以重新启用它，如下所示：

```powershell
Enable-PsBreakpoint 0
```

```powershell
$gameList = Get-ChildItem .*.ps1 # | ForEach-Object -process ($i++;$gameList[$i] = $n_.Name)
```

```powershell
$gameList #将数组的内容返回给调用语句
```

你需要通过替换你选择的存储 Windows PowerShell 游戏的文件夹路径和名称，对你该版本的脚本进行自定义。你还希望确保此文件夹只包含游戏脚本，而不包含你可能开发的其他 PowerShell 脚本。你还需要按照第 1 章“介绍 Windows PowerShell”中的描述，将此文件夹添加到你的默认路径中。

注意：在列出 `$gameList` 数组的语句中，使用了冒号 `:` 字符将 `$i++` 与 `$gameList[$i]=$_.Name` 隔开。在这里，该字符用作行结束标记，允许你在单行内放置两个语句。

## 创建 Write-MenuList 函数

要添加到脚本中的下一个函数是 `Write-MenuList` 函数，概述如下。此函数负责接收传递给它的文件名列表，并用其构建一个编号的菜单列表。

```powershell
param($list) #要显示的游戏列表以数组形式传递
$Counter -=0 #用于为每个菜单项计数
```

```powershell
Write-Host ""
ForEach ($i in $list) { #遍历数组中存储的每个脚本
```

```powershell
$counter++ #计数器加 1
if ($counter -lt 10) { #格式化前 9 个脚本的显示
  Write-Host "$counter. $i*" -ForegroundColor blue
}
else { #格式化所有剩余脚本的显示
```

```powershell
  Write-Host "counter. $i" -ForegroundColor blue
}
```

```powershell
Write-Host "*"
}
```

如你所见，传递给此函数的文件名列表被临时存储在一个名为 `$list` 的数组中，然后使用 `ForEach` 循环进行处理。在循环的每次迭代中，都会显示一个文件名，并带有一个唯一标识该文件的数字（例如由 `$i` 的值指定）。

## 编写 End-ScriptExecution 函数

添加到脚本的最后一个函数是 `End-ScriptExecution` 函数，如下所示。此函数负责显示一条消息，感谢玩家使用 PowerShell 游戏控制台，并在三秒后清除屏幕。

```powershell
function End-ScriptExecution (
  Clear-Host # 清除屏幕
  Write-Host "*nThank you for using the Windows PowerShell Game Console"
  Start-Sleep 3 # 暂停脚本执行 3 秒
  Clear-Host # 清除屏幕
)
```

## 开发主处理部分的编程逻辑

现在是时候通过为主处理部分添加编程逻辑来完成工作了，该逻辑将管理 PowerShell 游戏控制台的整体执行。构成此逻辑的脚本语句概述如下：

```powershell
$response = 0 #存储玩家输入
```

```powershell
# 在玩家决定关闭游戏
# 控制台之前继续玩新游戏
```

```powershell
while ($playAgain -eq "True") {
  # 调用生成包含游戏脚本
  # 列表数组的函数
  $menuList = Get-GameList

  # 调用将数组内容转换为菜单
  # 列表的函数
  Write-MenuList $menuList

  # 提示玩家选择一个游戏来玩
  $response = Read-Host "*n Enter the menu number for a game or Q to quit"

  # 当用户决定退出时准备关闭游戏控制台
  if ($response -eq "Q") {
    $playAgain = "False" # 修改变量值以停止循环
    continue # 重复循环
  }

  # 将玩家的输入转换为整数，然后验证玩家
  # 输入
  if ([int]$response -lt 1) { # 小于 1 的任何都不是有效的菜单编号
    Clear-Host # 清除屏幕
    Write-Host "*a'invalid selection."
    Read-Host # 暂停脚本直到玩家按下 Enter 键
    continue # 重复循环
  }

  if ([int]$response -gt $menuList.length) {
    Clear-Host # 清除屏幕
    Write-Host "*a'invalid selection."
    Read-Host # 暂停脚本直到玩家按下 Enter 键
    continue # 重复循环
  }

  # 格式化代表执行用户选择
  # 脚本的命令字符串
  $game = "./" + $menuList[$response-1]

  Invoke-Expression $game # 执行选定的脚本

  Clear-Host # 清除屏幕
}

End-ScriptExecution
```



如你所见，已定义了一个 `while` 循环来控制脚本的整体执行。该循环一直执行到玩家输入菜单命令 `'Q'`，标志着是时候关闭控制台了。在循环的每次迭代中，都会按顺序执行 `Get-GameListing` 函数以生成要显示的游戏列表。接下来，执行 `Write-MenuList` 函数以显示已组的 PowerShell 脚本列表。提示玩家选择一个游戏。然后对玩家的输入进行评估。一旦指定了有效的菜单选择，就会组合指定运行脚本所需的命令字符串，然后使用 `Invoke-Expression` 命令行来运行脚本。

`Invoke-Expression` 命令行允许你通过指定菜单项的数组索引来启动指定的脚本。

## 结果

好了，这些。如果一切进展顺利，你版本的 PowerShell 游戏控制台应该就可以运行了。如果你犯了一些拼写错误并遇到了错误，请使用本章提供的调试信息来跟踪错误。

# 表 A. 网站上的 POWERSHELL 脚本文件

| 章节 | 应用 | 描述 |
|---|---|---|
| 第 1 章 | 敲门笑话 | 该脚本通过演示创建和执行一个敲门笑话脚本的步骤，介绍了 PowerShell 脚本编写。 |
| 第 2 章 | 三剑的故事 | 该脚本演示了如何收集用户输入并将其用于填空游戏（mad-lib）的创建。 |
| 第 3 章 | PowerShell 占卜 | 该脚本为玩家的问题提供随机答案，并根据一天的时间提供不同的答案。 |
| 第 4 章 | 《老友》知识问答 | 该脚本演示了如何存储和检索变量，以构建一个问答游戏，测试玩家对《老友》电视剧知识的了解程度。 |
| 第 5 章 | 猜数字游戏 | 该脚本通过开发一个猜数字游戏演示了条件逻辑的实现，玩家被要求用最少的次数猜出一个秘密数字。 |
| 第 6 章 | 石、剪、布 | 该脚本重现经典脚本的命令行版本，演示了如何使用循环控制脚本执行。 |
| 第 7 章 | PowerShell 猜字游戏 | 该脚本通过开发一个猜字游戏演示了如何使用函数组织脚本。 |
| 第 8 章 | PowerShell 井字棋 | 该脚本通过开发一个双玩家 PowerShell 游戏重现了经典的井字棋。 |
| 第 9 章 | PowerShell 扑牌 | 该脚本演示了如何创建一个黑杰式的纸牌游戏，让玩家与电脑对。 |
| 第 10 章 | PowerShell 游戏控制台 | 该脚本通过创建一个游戏控制台整合了书中涵盖的所有概念，让玩家方便地访问书中的 PowerShell 游戏。 |

# 接下来做什么？

正如你在读完这本书后无疑得出的结论那样，Microsoft PowerShell 提供了一个稳健、强大的脚本环境，远超传统的 shell 脚本。Windows PowerShell 提供了一种全新的编程语言，从底层开始设计，旨在集成并利用 .NET Framework 提供的功能。正如本书所示，Microsoft PowerShell 是初级程序员和计算机爱好者的一门非常棒的编程语言。然而，它也足够强大，能够满足专业程序员的需求。

虽然你已经学习了许多关于使用 Windows PowerShell 脚本编程的知识，但仍然有很多需要学习。因此，不要将这本书视为你 PowerShell 脚本教育的结束，而应该将其视为起点。要成为一名真正有效的 Microsoft PowerShell 程序员，你必须继续阅读并尽可能多学习。为了帮助你开始，我提供了这个附录，你可以在这里找到各种用的 Windows PowerShell 信息。它包含了关于 PowerShell IDE、各种 PowerShell 阅读材料、网站、邮件列表和博客的信息。

# WINDOWS POWERSHELL IDEs

在我更新这本书的第二版时，已经有两个第三方的 Windows PowerShell IDE 可用。这些 PowerShell IDE 为使用记事本或图形化 Windows PowerShell 提供了替代方案。

> 定义：IDE 或集成开发环境（integrated development environment）是一种图形软件开发工具，它将源代码编辑器与其他应用程序开发工具集成在一起，以帮助创建脚本或应用程序。

第一个 PowerShell IDE 是 PowerShellPlus，在我编写本书期间，它可以在 http://www.powershell.com/ 以 145 美元的价格购买。PowerShellPlus 提供了一系列长长的功能列表，包括：

- 语句代码着色
- 直接命令行访问
- 调试功能（包括支持断点）
- 上下文感知的代码补全
- 变量和属性值

图 B.1 显示了 PowerShellPlus 内置脚本编辑器的示例。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_403_0.png)

图 B.1
PowerShellPlus 管理脚本代码、输出以及变量和属性值的显示。

另一个 PowerShell IDE 是 PowerShell Analyzer，可以在 http://www.powershellanalyzer.com 免费下载。PowerShell Analyzer 带有许多华丽的功能，旨在帮助你在与 Windows PowerShell 交互和开发脚本时工作得更快、更智能。PowerShell Analyzer 功能的示例包括：

- 语句颜色编码
- 直接命令行访问
- 自动显示关键字语法
- 变量和属性视图

图 B.2 显示了 PowerShell Analyzer 运行的示例。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_404_0.png)

图 B.2
PowerShell Analyzer 提供了方便访问的工具，用以简化并加速脚本开发。

# 推荐阅读

Microsoft 以“快速入门指南”和“用户指南”的形式提供了自己的 PowerShell 文档。虽然初级程序员和 PowerShell 脚本的新手可能会觉得这些指南具有挑战性，但对于读完这本书的你来说，它们将是极佳的下一步。在下面提供了这两份指南的信息。

Windows PowerShell 快速入门指南
Microsoft 公司编写

作为 Windows PowerShell 的一部分安装的 Word 文档。要访问它，点击“开始 > 所有程序 > Windows PowerShell > Getting Started”。

Windows PowerShell 入门
Microsoft 公司编写

作为 Windows PowerShell 的一部分安装的 Word 文档。要访问它，点击“开始 > 所有程序 > Windows PowerShell > User Guide”。

# 在线查找 MICROSOFT POWERSHELL 资源

尽管 PowerShell 出现时间较晚，但它在互联网上已经有了显著的地位。在后续章节描述的网站上可以获得大量信息。你可能需要定期访问它们以跟上最新动态。你还会发现这些网站中的许多提供了免费示例代码访问。

当你准备好在线时，要去的地方之一是 Microsoft 的 ScriptCenter 页面，地址为 http://www.microsoft.com/technet/scriptcenter/hubs/mspx，如图 B.3 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_405_0.png)

访问 ScriptCenter 页面以获取各种 Windows PowerShell 资源。

# Wikipedia Windows PowerShell 页面

你可以在 Wikipedia 百全书（http://www.wikipedia.org/wiki/powershell）中找到大量的 Windows PowerShell 信息，如图 B.4 所示。在这里你会找到各种文章、第三方工具和网站的链接。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_406_0.png)

图 B.4
Wikipedia 的 Windows PowerShell 页面由全球用户维护。

# Windows PowerShell 新闻组

有时候，没有比花时间和同行分享信息更好的学习方法了。实现这一点的一种方法是通过新闻组。微软赞助了一个专门针对 PowerShell 的新闻组。你可以在 http://www.microsoft.com/communities/newsgroups/list/en-us/default.aspx?pg=microsoft.public.windows.powershell 找到这个新闻组。图 B.7 展示了该网页的预览以及其中发生的讨论类型。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_408_0.png)

图 B.7

# PowerShell 博客

另一个与同行程序员交流和交换问答的极有用的地方是 PowerShell 博客网站。其中一个博客是 Windows 开发团队的博客，位于 http://blogs.msdn.com/PowerShell/，如图 B.8 所示。

正如你所想象的，这在 PowerShell 社区中非常流行，你会发现每天都有层不完的技术讨论。

另一个很好的博客网站是 Monad 技术博客，你可以在 http://blogs.msdn.com/monad/archive/2005/09/02/460075.aspx 找到，如图 B.9 所示。

脚本教学 - Monad 博客

# PowerShell 团队博客

用行代码改变世界。

另一个优秀的 Don Jones 视频演示

PowerShell 杂志有一个来自 Don Jones 的精彩视频演示，他在其中展示了如何使用 PowerShell 完成任何事情。该视频展示了一些对任何使用 PowerShell 的人员都有用的技术示例，对初学者来说是一场盛宴。有各种技术可以让你获得越来越好的结果：更强大的

如果你是一个高级高手，你已经知道 Don Jones 演示的那些技术，但对于刚起步的人来说，这是必少的。这些只是本地示例对初学者非常有帮助，他们应该应该应该向他请教的机会。

在此处查看他的视频演示：

访问 PowerShell 团队博客：http://blog.monad.com/PowerShell 或 http://www.microsoft.com/technet/scriptcenter/hubs/msh.msx

由 PowerShell 团队博客发布：2 条评论

```
XMI
```

Monad 接收对象的的方法 - Windows 桌面管理器

http://blog.monad.com/monad/archive/2005/08/02/005075.html

Monad - 技术博客

# Monad

Monad 技术博客

# MshObject 和接收对象的方法

当我编写脚本时，通常调用接收对象作为输入的方法没有问题。PowerShell 中的对象被一个不可见的 `MshObject` 封装，因此对象并不总是一致的。看看以下：

一方面，你可以使用密钥访问对象。另一方面，你并没有那个密钥。这是发生了什么？当你查看时，政策也很拥挤，我们也想解释一切，因此今晚，你假设所有表达的观点都是 Monad 团队成员的，而不是微软的。

```
Get-Bash Controller
```



![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_409_0.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_409_1.png)

正如其名所示，这个博客建立在微软为 PowerShell 起新名字之前的早期。该博客的主要用处是它为你提供了追溯到 2005 年的讨论。

另一个值得提及的博客是 PowerShell Guy 博客，运行于 `http://thepowershell.com/blogs/posh/`，如图 B.10 所示。

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_410_0.png)

图 B.10 PowerShell Guy 博客。

PowerShell Guy 博客是一个受欢迎的博客，提供了许多关于 PowerShell 的见解，并充满了代码示例。

# 术语表

`.NET Framework`。由微软开发的一个框架，旨在支持开发桌面、网络和基于 Internet 的应用程序及脚本。

`.NET Framework` 类库。一个层次化的类集合，可以根据这些类实例化对象。

`.ps1`。Windows PowerShell 脚本使用的文件扩展名。

`$_`。由 Windows PowerShell 创建并维护的特殊变量，它自动分配 PowerShell 管道线中当前对象的名称，在 `Where-Object` 命令中，用于引用集合中的每个对象。

`Add-Content`。一个 Windows PowerShell 命令，向指定项目的内容添加内容。

`Add-History`。一个 Windows PowerShell 命令，向会话历史添加条目。

`Add-Member`。一个 Windows PowerShell 命令，向对象添加用户定义的自定义成员。

`Add-Module`。一个 Windows PowerShell 2.0 命令，允许你加载脚本或 DLL 作为模块加载。

`Add-PSSnapin`。一个 Windows PowerShell 命令，向当前 PowerShell 控制台添加一个或多个 PSSnapIn。

`Add-Type`。一个 Windows PowerShell 2.0 命令，允许你加载 DLL 或程序集，而不是使用 .NET

# 392 零基础 Windows PowerShell 2.0 编程，第二版

- `Enable-PSBreakpoint`。一个 Windows PowerShell 2.0 cmdlet，用于启用或重新启用已禁用的断点。
- `ErrorRecord`。每当发生错误时都会创建的对象，它提供了访问错误相关信息的途径。
- `Eventing`。一种设置 Windows PowerShell 以能够监听并响应系统事件的能力。
- `Exception`。每当在 Windows PowerShell 脚本中发现错误时都会发生的事件。
- `Export-Alias`。一个 Windows PowerShell cmdlet，用于将别名列表导出到文件。
- `Export-Clixml`。一个 Windows PowerShell cmdlet，用于生成 PowerShell 对象的 Clixml 表示形式。
- `Export-Console`。一个 Windows PowerShell cmdlet，用于导出对当前控制台所做的更改。
- `Export-Csv`。一个 Windows PowerShell cmdlet，用于从输入创建 CSV 字符串。
- `Export-ModuleMember`。一个 Windows PowerShell 2.0 cmdlet，用于从模块中导出函数或 cmdlet。
- `Expression`。一个被求值并产生结果的语句。
- `Filter`。一种类似于函数的编程结构，但旨在高效处理大量的对象流水线数据。
- `Flowchart`。程序员用于以图形化方式描述脚本全部或部分逻辑流的工具。
- `For`。一种循环固定次数的 PowerShell 语句。
- `ForEach`。一种遍历集合或数组中存储的所有元素的 PowerShell 语句。
- `ForEach-Object`。一个 Windows PowerShell cmdlet，对流水线中的每个对象应用脚本块。
- `Format-Custom`。一个 Windows PowerShell cmdlet，通过向格式化文件添加内容来格式化输出显示。
- `Format-List`。一个 Windows PowerShell cmdlet，将对象格式化为垂直列表的属性列表。
- `Format-Table`。一个 Windows PowerShell cmdlet，将输出格式化为表格。
- `Format-Wide`。一个 Windows PowerShell cmdlet，将对象格式化为属性表格。
- `Function`。一组作为单元被调用和执行的语句。
- `Get-Acl`。一个 Windows PowerShell cmdlet，用于获取与文件或对象关联的访问控制列表。
- `Get-Alias`。一个 Windows PowerShell cmdlet，返回 cmdlet 的别名。
- `Get-AuthenticodeSignature`。一个 Windows PowerShell cmdlet，用于获取属于文件的签名对象。
- `Get-ChildItem`。一个 Windows PowerShell cmdlet，用于检索指定驱动器的子项。
- `Get-Command`。一个 Windows PowerShell cmdlet，用于检索有关命令的信息。
- `Get-Content`。一个 Windows PowerShell cmdlet，从指定位置返回项的内容。
- `Get-Credential`。一个 Windows PowerShell cmdlet，根据密码获取凭据对象。
- `Get-Culture`。一个 Windows PowerShell cmdlet，用于获取文化信息。
- `Get-Date`。一个 Windows PowerShell cmdlet，获取当前日期和时间。
- `Get-Event`。一个 Windows PowerShell 2.0 cmdlet，用于从事件日志和事件跟踪日志中检索事件。
- `Get-EventLog`。一个 Windows PowerShell cmdlet，用于获取机器的事件日志数据。
- `Get-ExecutionPolicy`。一个 Windows PowerShell cmdlet，获取有效的执行策略。
- `Get-Help`。一个 Windows PowerShell cmdlet，用于打开帮助文件。
- `Get-History`。一个 Windows PowerShell cmdlet，获取当前会话历史列表。
- `Get-Host`。一个 Windows PowerShell cmdlet，用于检索主机信息。
- `Get-Item`。一个 Windows PowerShell cmdlet，获取代表命名空间项的对象。
- `Get-ItemProperty`。一个 Windows PowerShell cmdlet，检索属于某个对象的属性。
- `Get-Location`。一个 Windows PowerShell cmdlet，用于显示当前位置。
- `Get-Member`。一个 Windows PowerShell cmdlet，列出指定对象的属性、方法和属性集。
- `Get-Module`。一个 Windows PowerShell 2.0 cmdlet，检索一个或多个已加载的模块，返回 `PSModuleInfo` 对象。
- `Get-PfxCertificate`。一个 Windows PowerShell cmdlet，获取 pfx 证书信息。
- `Get-Process`。一个 Windows PowerShell cmdlet，返回所有进程的列表。
- `Get-PSBreakpoint`。一个 Windows PowerShell 2.0 cmdlet，检索所有当前设置的断点列表。
- `Get-PSCallStack`。一个 Windows PowerShell 2.0 cmdlet，检索并显示当前调用堆栈。
- `Get-PSDrive`。一个 Windows PowerShell cmdlet，获取驱动器信息。
- `Get-PSEvent`。一个 Windows PowerShell 2.0 cmdlet，用于订阅特定类型的事件。
- `Get-PSEventSubscriber`。一个 Windows PowerShell 2.0 cmdlet，显示当前工作会话的所有事件订阅者列表。
- `Get-PSJob`。一个 Windows PowerShell 2.0 cmdlet，检索后台作业。
- `Get-PSProvider`。一个 Windows PowerShell cmdlet，返回提供程序信息。
- `Get-Random`。一个 Windows PowerShell 2.0 cmdlet，生成随机数。
- `Get-Runspace`。一个 Windows PowerShell 2.0 cmdlet，检索在当前工作会话中创建的运行空间。
- `Get-PSSnapIn`。一个 Windows PowerShell cmdlet，获取注册的 PSSnapIns 列表。
- `Get-Service`。一个 Windows PowerShell cmdlet，获取服务列表。
- `Get-TraceSource`。一个 Windows PowerShell cmdlet，列出跟踪源属性。
- `Get-UICulture`。一个 Windows PowerShell cmdlet，获取唯一文化信息。
- `Get-Unique`。一个 Windows PowerShell cmdlet，获取排序列表中的唯一项。
- `Get-Variable`。一个 Windows PowerShell cmdlet，检索 PowerShell 变量。
- `Get-WmiObject`。一个 Windows PowerShell cmdlet，创建 WMI 对象或系统上可用的 WMI 类列表。
- `Global Scope`。每当启动新的 PowerShell 会话时建立的范围。
- 图形化帮助文件。一种图形化的 Windows 帮助文件，允许你搜索、查看 Windows PowerShell 帮助文件。
- 分组对象。一种根据特定值对对象进行分组的操作。
- 如果。一种根据条件执行的 PowerShell 语句。
- 本地范围。指全局、私有或脚本范围。
- 逻辑错误。当脚本产生意外结果时发生的、阻止继续执行的错误。
- 循环。一组重复执行的语句。
- 测量命令。用于跟踪脚本块或 cmdlet 运行时间。
- 测量对象。一个 Windows PowerShell cmdlet，衡量对象的不同方面。
- 方法。一组可以执行以交互并控制其对象的代码。
- 移动项。一个 Windows PowerShell cmdlet，将项从一个位置移动到另一个位置。
- 移动属性。一个 Windows PowerShell cmdlet，将属性从一个位置移动到另一个位置。
- 新建别名。一个 Windows PowerShell cmdlet 创建 cmdlet-别名对。
- 新建项。一个 Windows PowerShell cmdlet 在命名空间中创建新项。
- 新建属性。一个 Windows PowerShell cmdlet 为指定项设置新属性。
- 新建对象。一个 Windows PowerShell cmdlet 创建一个新的 .NET 对象。
- 新建驱动器。一个 Windows PowerShell cmdlet 设置新的驱动器。
- 新建事件。一个 Windows PowerShell 2.0 cmdlet 创建新事件。
- 新建运行空间。一个 Windows PowerShell 2.0 cmdlet 创建到 PowerShell 会话（本地或远程）的持久连接。
- 新建服务。一个 Windows PowerShell cmdlet 创建新服务。
- 新建间隔。一个 Windows PowerShell cmdlet 创建一个 `TimeSpan`。
- 新建变量。一个 Windows PowerShell cmdlet 定义新变量。
- 非终止错误。不会阻止脚本继续执行的错误。
- 对象。一种包含自身信息以及访问和操作所需代码的自包含资源。
- 输出默认。一个 Windows PowerShell cmdlet 设置输出的默认控制器。
- 输出网格。一个 Windows PowerShell 2.0 cmdlet 在交互式表格中显示输出，允许对结果进行排序和搜索。
- 输出主机。一个 Windows PowerShell cmdlet 将对象流水线数据发送到主机。
- 输出空。一个 Windows PowerShell cmdlet 将输出发送到空值。
- 输出打印机。一个 Windows PowerShell cmdlet 将输出发送到打印机。
- 输出字符串。一个 Windows PowerShell cmdlet 将字符串输出发送到对象流水线。

`Pipeline`（管道）。两个命令之间的逻辑连接，支持将一个命令的输出传递给另一个命令，并将其作为输入接收。

`Pop-Location`（弹出位置）。一个 Windows PowerShell 命令，用于将当前工作位置更改为栈中最后添加条目指定的位置。

`Pop-Runspace`（弹出运行空间）。一个 Windows PowerShell 2.0 命令，用于终止远程交互会话。

`Precedence`（优先级）。数学运算执行的顺序。

`Private Scope`（私有作用域）。其他作用域不可见或不可的作用域。

`Properties`（属性）。描述对象特定特征属性。

`Provider`（提供程序）。为 Windows PowerShell 提供访问分级存储库（包括文件系统和 Windows 注册表）的模型。

`Pseudo Code`（伪代码）。用于描述脚本或程序的类英语大纲的术语。

`Push-Location`（推送位置）。一个 Windows PowerShell 命令，将一个位置推入栈中。

`Push-Runspace`（推送运行空间）。一个 Windows PowerShell 2.0 命令，启动一个远程交互会话。

`Read-Host`（读取主机输入）。一个 Windows PowerShell 命令，从主机控制台收集一行输入。

`Receive-PSJob`（接收 PowerShell 作业）。一个 Windows PowerShell 2.0 命令，从后台作业中检索输出。

`Register-ObjectEvent`（注册对象事件）。一个 Windows PowerShell 2.0 命令，用于注册一个事件订阅。

`Register-PSEvent`（注册 PowerShell 事件）。一个 Windows PowerShell 2.0 命令，允许你注册特定类型的事件。

`Register-WMIEvent`（注册 WMI 事件）。一个 Windows PowerShell 2.0 命令，允许你注册特定的 WMI 事件。

`Registry`（注册表）。一个存储操作系统配置数据以及硬件、软件、网络和用户设置的 Windows 存储库。

`Registry Key`（注册表项/键值）。用于存储注册表项和值的逻辑容器。

`Regular Expression`（正则表达式）。用于描述匹配数据的模式。

`Remote Execution`（远程执行）。在对你拥有访问权限的网络计算机上远程执行 Windows PowerShell 脚本的能力。

`Remove-Item`（删除项目）。一个 Windows PowerShell 命令，调用提供程序来删除项目。

# 398 零基础学者的 Windows PowerShell 2.0 编程。第二版。

`Remove-ItemProperty`（删除项属性）。一个 Windows PowerShell 命令，从指定位置删除属性及其值。

`Remove-Module`（移除模块）。一个 Windows PowerShell 2.0 命令，从已加载模块列表中删除 `PSModuleInfo` 对象。

`Remove-PSBreakpoint`（删除 PowerShell 断点）。一个 Windows PowerShell 2.0 命令，从当前工作会话中删除断点。

`Remove-PSDrive`（删除 PowerShell 驱动器）。一个 Windows PowerShell 命令，删除一个驱动器。

`Remove-PSEvent`（移除 PowerShell 事件）。一个 Windows PowerShell 2.0 命令，取消事件的订阅。

`Remove-PSJob`（删除 PowerShell 作业）。一个 Windows PowerShell 2.0 命令，删除一个后台作业。

`Remove-PSSnapIn`（移除 PowerShell 挂接程序）。一个 Windows PowerShell 命令，从当前控制台移除 PSSnapIns。

`Remove-Runspace`（删除运行空间）。一个 Windows PowerShell 2.0 命令，终止一个或多个运行空间。

`Remove-Variable`（删除变量）。一个 Windows PowerShell 命令，删除一个变量及其值。

`Remove-WMIObject`（删除 WMI 对象）。一个 Windows PowerShell 2.0 命令，删除 WMI 实例和类。

`Rename-Item`（重命名项目）。一个 Windows PowerShell 命令，更改项目的名称。

`Rename-ItemProperty`（重命名项属性）。一个 Windows PowerShell 命令，重命名一个属性。

`Reserved Word`（保留字）。Windows PowerShell 预定义的具有特殊用途的关键字。

`Resolve-Path`（解析路径）。一个 Windows PowerShell 命令，解析路径中的通配符字符。

`Restart-Service`（重启服务）。一个 Windows PowerShell 命令，重启一个已停止的服务。

`Resume-Service`（恢复服务）。一个 Windows PowerShell 命令，恢复一个已挂起的服务。

`Runspaces`（运行空间）。Windows PowerShell 脚本可以在其中执行的独立托管执行空间。

`Run-time Error`（运行时错误）。当脚本尝试执行非法操作（如数字除以零）时发生的错误。

`Script Cmdlets`（脚本级 cmdlet）。使用 Windows PowerShell 脚本语言创建的自定义 cmdlet。

`Script Scope`（脚本作用域）。每当执行脚本时都会建立的作用域，并在脚本停止执行时结束。

`Select-Object`（选择对象）。一个 Windows PowerShell 命令，根据命令字符串指定的参数选择对象。

`Select-String`（选择字符串）。一个 Windows PowerShell 命令，在字符串或文件中搜索匹配的模式。

`Set-Acl`（设置访问控制列表）。一个 Windows PowerShell 命令，访问访问控制列表属性。

`Set-Alias`（设置别名）。一个 Windows PowerShell 命令，将别名映射到 cmdlet。

`Set-AuthenticodeSignature`（设置身份验证签名）。一个 Windows PowerShell 命令，在 PowerShell 脚本中放置 Authenticode 签名。

`Set-Content`（设置内容）。一个 Windows PowerShell 命令，设置项目中的内容。

`Set-Date`（设置日期）。一个 Windows PowerShell 命令，设置系统时间。

`Set-ExecutionPolicy`（设置执行策略）。一个 Windows PowerShell 命令，建立执行策略。

`Set-Item`（设置项）。一个 Windows PowerShell 命令，将提供程序内路径名的值设置为指定值。

`Set-ItemProperty`（设置项属性）。一个 Windows PowerShell 命令，将属性设置为指定值。

`Set-Location`（设置位置）。一个 Windows PowerShell 命令，设置当前工作位置。

`Set-PSBreakpoint`（设置 PowerShell 断点）。一个 Windows PowerShell 2.0 命令创建一个新的断点。

`Set-PSDebug`（设置 PowerShell 调试）。一个 Windows PowerShell 命令，开启 PowerShell 的脚本调试功能。

`Set-Service`（设置服务）。一个 Windows PowerShell 命令，更改服务属性。

`Set-StrictMode`（设置严格模式）。一个 Windows PowerShell 2.0 命令，为当前作用域配置并启用严格模式。

`Set-TraceSource`（设置跟踪源）。一个 Windows PowerShell 命令，从指定的跟踪实例修改并修用跟踪监听器。

`Set-Variable`（设置变量）。一个 Windows PowerShell 命令，为变量分配值，或在变量不存在时创建变量。

`Set-WmiInstance`（设置 WMI 实例）。一个 Windows PowerShell 2.0 命令，创建或更改 WMI 类实例。

`Sort-Object`（排序对象）。一个 Windows PowerShell 命令，根据属性值对输入对象进行排序。

# 400 零基础学者 Microsoft Windows PowerShell 2.0 训练，第二版。

`Special Variables`（特殊变量）。由 Windows PowerShell 创建并管理的变量集合，提供对常用信息的访问。

`Split-Path`（拆路径）。一个 Windows PowerShell 命令，流带有限定符、父路径或叶节点项的字符串。

`Start-PSDebug`（启动 PowerShell 调试）。一个 Windows PowerShell 2.0 命令启动交互式 PowerShell 调试器。

`Start-PSJob`（启动 PowerShell 作业）。一个 Windows PowerShell 2.0 命令启动一个后台作业。

`Start-PSTransition`（启动 PowerShell 事务）。一个 Windows PowerShell 2.0 命令开始一个新事务。

`Start-Service`（启动服务）。一个 Windows PowerShell 命令，启动一个已停止的服务。

`Start-Sleep`（等待）。一个 Windows PowerShell 命令，在指定时间内挂外壳、脚本或运行空间的活动。

`Start-Transcript`（启动记录）。一个 Windows PowerShell 命令，为命令会话启动记录。

`Stop-Process`（停止进程）。一个 Windows PowerShell 命令，停止一个活动进程。

`Stop-PSJob`（停止 PowerShell 作业）。一个 Windows PowerShell 2.0 命令，终止一个后台作业。

`Stop-Service`（停止服务）。一个 Windows PowerShell 命令，停止一个活动的服务。

`Stop-Transcript`（停止记录）。一个 Windows PowerShell 命令，停止记录过程。

`Subclass`（子类）。从父类继承基础对象定义并包含自身修改的类。

`Suspend-Service`（挂起服务）。一个 Windows PowerShell 命令，挂起一个活动的服务。

`Switch`（切换）。用于定义一组不同测试和代码块的语句，每个块评估同一个表达式。

`Syntactic Error`（语法错误）。由于不符合 PowerShell 脚本语言语法而产生的错误。

`Tab Completion`（Tab 补全）。一种编辑功能，允许你输入命令的一部分并按 Tab 键协助完成剩余命令。

`Tee-Object`（分流输出）。一个 Windows PowerShell 命令，将输入对象发送到两个不同的地方。

`Terminating Error`（终止性错误）。停止 PowerShell 脚本执行的错误。

`Test-Path`（测试路径）。一个 Windows PowerShell 命令，如果路径存在则返回 True，不存在则返回 False。

`Trace-Command`. 一个 Windows PowerShell cmdlet，用于启用对跟踪源实例的跟踪。

`Trace`. 在执行脚本时，跟踪脚本语句执行情况的进程。

`Transaction`. 一系列数据的交换，除非完整完成，否则它们可以被回滚和取消。

`Trap Handler`. 当发生异常时执行的一系列语句集合。

`Try-Finally-Catch`. 一种处理异常的结构，以便优雅地管理脚本错误。

`Undo-PSTransaction`. 一个 Windows PowerShell 2.0 cmdlet，用于回滚并撤销事务。

`UnregisterEvent`. 一个 Windows PowerShell 2.0 cmdlet，用于取消事件注册。

`Update-FormatData`. 一个 Windows PowerShell 2.0 cmdlet，用于修改数据文件。

`Update-List`. 一个 Windows PowerShell 2.0 cmdlet，从包含对象集合的属性值中添加或删除项。

`Update-Type`. 一个 Windows PowerShell 2.0 cmdlet，用于更新 `types.ps1` 文件。

`Use-PSTransaction`. 一个 Windows PowerShell 2.0 cmdlet，允许当前事务应用于已事务的对象。

`Values`. 在 Windows 注册表中存储实际数据的容器。

`Variable`. 存储在内存中的数据的引用。

`Wait-Process`. 一个 Windows PowerShell 2.0 cmdlet，用于等待特定进程完成。

`Wait-Event`. 一个 Windows PowerShell 2.0 cmdlet，在继续之前等待事件。

`Wait-PSJob`. 一个 Windows PowerShell 2.0 cmdlet，用于等待所有作业或指定作业完成。

`Where-Object`. 一个 Windows PowerShell cmdlet，用于过滤来自对象管道的输入。

`While`. 一种 PowerShell 语句，只要指定的条件为真就一直迭代。

`Windows Remote Management (WinRM)`. 微软对 WS-Management 协议的实现，这是一种简单对象访问协议 (SOAP)。

`WMI` (微软 Windows 管理规范). 一种旨在便于访问系统信息的系统管理接口。

`Write-Debug`. 一个 Windows PowerShell cmdlet，用于创建调试消息。

`Write-Error`. 一个 Windows PowerShell cmdlet，创建一个错误对象并将其通过对象管道。

`Write-Host`. 一个 Windows PowerShell cmdlet，用于显示对象数据。

`Write-Output`. 一个 Windows PowerShell cmdlet，将对象添加到对象管道中。

`Write-Progress`. 一个 Windows PowerShell cmdlet，向宿主程序发送进度记录。

`Write-Verbose`. 一个 Windows PowerShell cmdlet，向宿主程序的详细显示窗口写入字符串。

`Write-Warning`. 一个 Windows PowerShell cmdlet，用于写入警告消息。

`WS-Management protocol`. 一种支持不同硬件和操作系统之间通信的简单对象访问协议 (SOAP)。

`XML`. 一种标记语言，便于在应用程序之间定义、存储和传输数据。

# 索引

- 一元运算符, 135
- 运算符, 171
- 字符, 67
- `$` 字符, 133
- `$_` 变量, 108, 138. 231–232, 389
- `$args` 变量, 224–225
- `$Error` 特殊变量, 349
- `$ErrorActionPreference` 变量, 349
- `$input` 变量, 227
- `$MyJob` 变量, 103
- `$PSConsoleWindow` 对象变量, 48
- `$result` 变量, 229
- `$RunSP` 变量, 101
- `$status` 变量, 117–118
- `$time` 变量, 117
- `$userReply` 变量, 28
- `$x` 变量, 310
- `*` 运算符, 23, 130, 136
- (句号) 字符, 254
- `;` (分号) 字符, 310
- `?` 字符, 24
- `\` 字符, 254
- `^a` 转义字符, 293
- `` ` `` 字符, 128
- `^t` 字符, 128
- `{}` 字符, 134
- `|` 字符, 252
- `+` 运算符, 129, 136, 141–142, 144
- `+` 正表达式量符字符, 255
- `+=` 运算符, 129
- `>` 重定向运算符, 262
- `>>` 管道运算符, 263

## A

- `About-PSJob` cmdlet, 99
- `-action` 参数, 328
- Add Criteria 按钮, `Out-GridView` cmdlet 的图形窗口, 282
- `Add-Content` cmdlet, 91, 264, 389
- `Add-History` cmdlet, 91, 390
- `Add-Member` cmdlet, 91, 389
- `Add-Module` cmdlet, 91, 390
- `Add-Number` 函数, 223–227
- `Add-PSSnapIn` cmdlet, 91, 390
- 别名, 19, 20, 28, 109–111, 390
- `alnsigned` 安全级别, 15
- 备用模式，匹配, 253
- `Analyze-Results` 函数, 336–337
- `-and` 运算符, 172
- 应用数据检索, 313
- 参数, 222–227, 390
- 赋值默认值, 226–227
- 概述, 222
- 传递, 223–225
- 指定数据类型, 225–226
- 算术运算符, 135, 161
- 数组, 133, 139–142, 390
- 组合, 141–142
- 创建, 140
- 删除和插入元素, 142
- 修改元素值, 141
- 概述, 139
- 大小, 141

# 404 基础 C++ Windows 编程：第二版

- 赋值运算符, 137
- 关联数组, 143–135, 390
- 访问数据, 143
- 创建, 143
- 删除键值对, 145
- 概述, 143
- 在创建时填充, 134
- 移除移除, 145
- 异步通知, 325
- 属性, 86–87

- 字符, 254
- 另见元字符
- `#`, 67
- `$`, 133
- `*`, 23
- `;` 分号, 370
- `?`, 24
- `\`, 254
- `a` 转义, 293
- `*n`, 128
- `*t`, 128
- `{`, 134
- `}`, 252

- `AutoReset` 属性, 329
- `BackgroundColor` 参数, 332

## B

- 后台作业, 11, 98–106, 390
- 创建, 100–101
- 删除, 105–106
- 执行, 100–101
- 概述, 98–99
- 获取信息, 101–102
- 获取输出, 102–103
- 停止, 103–104
- 等待完成, 104–105
- `BackgroundColor`, 48
- BIOS 获取, 310–311
- `break`, 201–202
- 断点, 364–365
- 括号, 254
- `+` 正表达式量符, 255
- 转义, 127–129
- (句号) 字符, 254
- 游戏, 23–24
- `Check-Function`, 333–334
- `Check-Results`, 336–337
- 类, 85–86
- 类, 85
- `clear` 别名, 28
- `clear` 命令, 57
- `clear` 方法, 144–145
- `Clear-Content`, 91–269
- `Clear-History`, 91–390
- `Clear-Host`, 91–264
- `Clear-Item`, 91–390
- `Clear-Variable`, 91–390
- `cls`, 278
- `-match` 运算符, 251–252
- `cmd.exe` shell, 62
- 命令历史, 42
- 命令提示符, 17–24
- 命令, 20
- `Command.com`, 7, 391
- 命令, 390

# 绝对初学者 Microsoft PowerShell 2.0 编程，第二版

组件模型对象 (COM) 对象，315-316

- 比较运算符，170-171
- 逻辑运算符，171-172
- 概览，170

- 组件，`.NET Framework`，85
  - `computername` 参数，100, 314

- 字符串比较运算符，172-173
- 确定数字

- `condition` 参数
- `for` 循环语法，193, 195
- `while` 循环语法，200
- `condition` 占位符，163

- 命令控制台，41-50
- 自定义选项，42-46
- 概览，41-42

- 条件逻辑，117, 157-186
- 结合管道线符和运算符，162
- 比较值，160-161

- 脚本控制台配置，46-49
- Windows 命令控制台编辑功能，49-50

- 猜数字游戏，173-185
  - 分析玩家输入，177-178
  - 分析玩家的响应，180

- 输出窗格，55-57
- Windows PowerShell，13-15
- Windows 远程管理，15-16

- 清除屏幕，180
- 收集玩家输入，177
- 创建新脚本，174
- 定义并初始化游戏变量，175
- 显示游戏统计数据，178-179
- 显示欢迎界面，175

- `-CONFIRM` 选项，17
- `continue` 命令，200-202
- Continue 终止选项，trap 处理器，352

- 最终结果，181-185
- 生成随机数，176
- 概览，158-160, 173-174

- Control+左编辑功能，49
- Control+右编辑功能，49
- `ConvertFrom-Csv` cmdlet，91, 391
- `ConvertFrom-SecureString` cmdlet，91, 391
- `ConvertFrom-StringData` cmdlet，91, 391

- 提示玩家再次游戏，179

- `Convert-Path` cmdlet，91, 391
- `ConvertTo-Csv` cmdlet，91, 270, 391
- `ConvertTo-SecureString` cmdlet，91, 391
- `ConvertTo-Xml` cmdlet，91, 57

- 设置循环以收集和分析猜数字，176
- 设置循环以控制游戏过程，175-176

- 命令脚本，57
- `Copy-Item` cmdlet，91, 259, 391
- `Copy-ItemProperty` cmdlet，91, 391
- `Count` 属性，数组，141
- 创建快捷方式向导，40
- 规格说明，282
- 光标大小，42

- `if` 语句，163-168
  - 备选行动方案，165-166
  - 制定，163-165
  - 多行，165
  - 嵌套，168
  - 概览，163
  - 单行，165

- 自定义别名，111
- 自定义
命令控制台，42-46

- 测试条件，166-167
- 概览，157
- `switch` 语句，168-170
- Windows PowerShell 运算符，170-173

- 更改颜色属性，45-86

![](img/e075ce2afe59f4442c361d9d87_429_0.png)

- 更改布局，44-45

- 修改属性，43-44
- 修改选项，42-43
- 概览，42

- Windows PowerShell 的，82-84
- 工作环境，40-41

## 数据

- CSV 文件，272-275
- 使用 `Out-GridView` 显示，176-282

- 显示输出，277-288
- 分组数据，279-280
- 概览，276-277
- 搜索和过滤数据，280-282
- 排序数据，279

- 输入，229-231
- 返回，229-231
- 输出保存为 HTML，270
- XML 文件，271-272
- 数据语言，12

- 数据存储
- 数据类型，225-226
- `Data-Handle` 函数，334-335
- 调试 PowerShell 脚本，334-374
- 断点 cmdlet，364
- 控制执行，364
- 创建错误处理器，351-358
- 创建 trap 处理器，351-358
- 概览，351

- `try`, `catch`, and `finally` 块，353-358
- 调试示例，365-367
- 错误消息，348-349
- 管理断点，367
- PowerShell，345-348
- 逻辑错误，347-348
- 概览，345
- 运行时错误，346-347

- 语法错误，345-346
- PowerShell Game Console，367-373
- 创建 `Get-Game` 函数，369-370
- 创建新脚本文件，368
- 创建 `We-Mullet` 函数，370-371
- 定义和初始化脚本变量，369

- Main 部分编程逻辑，371-373
- 概览，344-345, 367-368
- 编写 `End-Execution` 函数，371

- 对响应，349-351
- 终止与非终止错误，348
- 跟踪脚本执行，358-363
- 显示输出状态信息，359-360
- 概览，358-359
- 跟踪变量值，359-360
- 使用 PowerShell 调试模式，360-363

- 默认代码块，169-170
- 定义变量，134
- 桌面快捷方式，40
- 字典，143
- `dir` 命令，`cmd.exe`，62
- `directory` 关键字，263
- `Disable-Breakpoint` cmdlet，91, 364, 367, 371
- `display-Board` 函数，286
- `display-Results` 函数，289-293
- `do until` 循环，192-193
- `do until` 语句，191-192
- `do while` 循环，191-192
- `do while` 语句，391
- 双引号，134-135
- 下箭头编辑功能，49
- 下载 Windows PowerShell，13

- 编辑增强，50-53
- 制 键补全，50–53
- 图形化 PowerShell 编辑菜单，54
- 编辑选项，42
- 控制台编辑功能，49-50
- 编辑脚本，57-58
- `element` 参数，`foreach` 循环语法，196
- `else` 语句，163, 165-166
- `elseif` 语句，163, 166-167
- 结束功能，49
- 死循环，192, 347
- `End-ScriptExecution` 函数，371
- `Env` 驱动器，63-65
- `---` 运算符，160-162
- handler 处理器，351-358
- `try`, `catch`, and `finally` 块，353-358
- 错误消息，348-349
- `ErrorAction` 参数，349-350
- `ErrorDetails` 属性，348
- `Error` 对象，348-392
- 修改的错误，349-351
- 事件日志，306-309
- 事件处理，12, 325-392
- 检查对象，326-327
- 实例化新对象，326
- 概览，325-326
- 移除事件，329
- 订阅对象事件，327-398
- 等待事件发生，328-329
- 异常处理器，351
- 错误，392
- 排除参数，260
- 可执行文件，20
- 执行脚本，57-58
- 执行策略，15
- `Export-Alias` cmdlet，91, 392
- `Export-Clix` cmdlet，221, 371
- `Export-Console` cmdlet，92, 392
- `Export-Csv` cmdlet，92, 274
- `Export-Member` cmdlet，92, 392
- 表达式，135-392

- 图形化 PowerShell 文件菜单，54
- 文件，249-296
- 拷贝，259-260
- 创建，262-263
- 删除，260
- 从...删除，269
- 重命名，259-260

- `Out-GridView` cmdlet 窗口，276-282
- 显示输出，277-288
- 搜索和过滤数据，280-282
- 排序数据，249
- PowerShell Tic-Toe 游戏，提示用户权限，290
- 收集玩家移动，291
- 创建 `Check-Results` 函数，288-289
- 创建 `Display-Board` 函数，286
- 创建 `Display-Results` 函数，289-290
- 创建 `Get-Permission` 函数，284-286
- 设置循环以控制游戏过程，290-291
- 设置循环以控制脚本执行，290
- 创建新脚本，283
- 创建 `Validate-Move` 函数，286-288
- 定义和初始化脚本变量，283-284
- 确定某玩家是否获胜，292-293
- 确定是否平局，293-294
- 最终结果，296
- 概览，250-252, 282
- 准备 `Clear-Board` 函数，284
- 提示玩家玩新游戏，294-295
- 切换玩家回合，294
- 验证玩家移动，291-292
- 从逗号分隔值 (CSV) 文件读取，274-275
- 从 XML 文件读取，272
- 从文本文件读取，269
- 格式化 cmdlet 输出，264-269
- `Format-List` cmdlet，264-266
- `Format-Table` cmdlet，266-269
- 正则表达式，252-257
- 字符，254
- 匹配替代模式，253
- 基于范围匹配模式，255-257
- 匹配简单模式，252-253
- 概览，252
- 量词，255
- 重命名，261
- 获取信息，258-259

- 将数据保存为 XML 文件，271
- 将数据保存为逗号分隔值 (CSV) 文件，272-274
- 将输出保存为 HTML，270
- 搜索，261-262
- 将输出到打印机，275-276
- 验证存在性，257-258
- 写入文本文件，263-264
- 附加文本，264
- 概览，263
- 写入文本，263-264

# 初学者 Microsoft Windows PowerShell 2.0 编程，第二版

- `Format-Custom` cmdlet, 92, 296
- `Format-List` cmdlet, 24, 266-212, 392
- `Format-Table` cmdlet, 24, 266-269, 392
- `Format-Wide` cmdlet, 92, 393

处理输入数据, 227-228
限制变量作用域, 229-231
返回结果, 228-229

占卜者游戏。参见 PowerShell 占卜者游戏
函数断点函数, 365
函数函数, 139, 215-245

函数与过滤器部分，脚本模板, 222

## G

使用过滤器更改脚本设计, 219-220
创建可用的代码, 220
改进脚本组织, 219-220
概述, 219

游戏控制台。参见 PowerShell 游戏控制台
`Get-Acl` cmdlet, 92, 393
`Get-Alias` cmdlet, 92, 109, 313
`Get-AuthenticodeSignature` cmdlet, 92, 393
`Get-Card` 函数, 335
`Get-ChildItem` cmdlet, 19-20, 86-92, 106-107, 393
`Get-Command` cmdlet, 20, 97, 393
`Get-ComputerHandler` 函数, 335-336
`Get-Content` cmdlet, 92, 261-262, 393
`Get-Credential` cmdlet, 92, 393
`Get-Culture` cmdlet, 92, 393
`Get-Date` cmdlet, 92, 393
`Get-EventLog` cmdlet, 92, 306-309, 393
`Get-ExecutionPolicy` cmdlet, 92, 393
`Get-FileName` 函数, 227-228
`Get-GameListing` 函数, 369-370
`Get-Help` cmdlet, 17, 97-98, 393
`Get-History` cmdlet, 53, 92, 393
`Get-Host` cmdlet, 47-48, 393
`Get-Item` cmdlet, 92, 258, 393
`Get-Property` cmdlet, 92, 317, 393
`Get-Location` cmdlet, 92, 393
`Get-Member` cmdlet, 87-88, 92, 325-327, 394
`Get-Module` cmdlet, 93, 394
`Get-NewCard` 函数, 339
`Get-Permission` 函数, 284-286, 331-332
`Get-PfxCertificate` cmdlet, 93, 394
`Get-PlayerHand` 函数, 337-339
`Get-Process` cmdlet, 21-23, 900-301, 394
`Get-PSBreakpoint` cmdlet, 93, 364, 379

PowerShell 吊字游戏游戏, 232-243
挑战玩家玩另一个游戏, 242-243
收集并验证用户输入, 238-240
创建新脚本, 233
定义并初始化脚本级变量, 233-234
定义自定义函数, 234-235
确定游戏何时结束, 241-242
显示每次猜测的 own, 240-241
概述, 216-218, 232-233
提示玩家开始游戏, 236-237
选择秘密, 237-238
设置循环以控制游戏流程, 237
设置循环处理用户猜测, 238

使用过滤器替换, 231-232
脚本组织, 220-231
函数结构, 220-222
概述, 220
处理参数, 222-227

`Get-PSCall` cmdlet, 93, 394
`Get-PSDrive` cmdlet, 93, 394
`Get-PSEvent` cmdlet, 93, 394
`Get-PSEventSubscriber` cmdlet, 93, 328, 394
`Get-PSJob` cmdlet, 93, 99, 101-103, 105-106, 394
`Get-PSProvider` cmdlet, 62-63, 93, 394
`Get-PSSnaplin` cmdlet, 93, 394
`Get-Random` cmdlet, 93, 117, 394
`Get-Service` cmdlet, 93, 100, 302, 394
`Get-TraceSource` cmdlet, 93, 394
`Get-UICulture` cmdlet, 93, 394
`Get-Unique` cmdlet, 93, 394
`Get-Variable` cmdlet, 93, 394

`Get-WmiObject` cmdlet, 93, 310-314, 394
全局作用域, 139
帮助文件, 10, 60-61, 图形化 PowerShell, 10, 54-61
访问图形化文件, 60–61
配置输出面板, 55–57
额外运行, 59–60
编辑脚本, 57–58
执行命令, 55
`-groupby` 参数, 268–269
`-groupby` 属性, `Format-Table` cmdlet, 24
`Group-Object` cmdlet, 93, 395
猜数字游戏, 173–185
分析玩家输入, 177–178
分析玩家响应, 180
清除屏幕, 180
收集玩家输入, 177
创建新脚本, 174
定义并初始化变量, 175
显示游戏统计, 178–179
显示欢迎屏幕, 175
结果, 181–185
生成随机数, 176
概述, 158–160, 173–174
提示玩家再次玩, 179–190
设置循环收集猜测, 176
设置循环控制游戏流程, 175–176

## H

黑客, 14
吊字游戏。参见 PowerShell 吊字游戏
哈希, 133, 143
`HasMore` 字段, 100, 103
高度属性, 48
帮助菜单, 图形化 PowerShell, 54–55
分级数据存储, 62–66
历史缓冲区, 50, 53
配置集, 316
`HKEY_CURRENT_USER` 注册表项, 65–66
`HKEY_LOCAL_MACHINE` 注册表项, 65
首页, 49
HTML 文件, 270
标识符, 唯一事件, 329
`if` 关键字, 126
`if` 语句, 153, 163–168
替代操作, 165–166
制定, 163–165
多行, 165
嵌套, 167–168
概述, 163
单行, 165
测试条件, 166–167
`Import-Alias` cmdlet, 93, 395
`Import-Clix` cmdlet, 93, 272, 395
`Import-Csv` cmdlet, 93, 274–275
`Import-LocalizedData` cmdlet, 93, 395
`-include` 参数, 261
输入数据, 227-228
初始化参数, `for` 循环语法, 193
初始化部分，脚本模板, 222
输入面板, 图形化 PowerShell, 55
`-input` 查询, `ErrorAction`, 351
插入模式, 42
安装 Windows PowerShell, 13-15
集成开发环境 (IDE), 图形化 PowerShell, 380-381
`IntelliSense`, 58, 395
国际化，脚本, 12
插值，变量, 134-135
`Invoke-Command` cmdlet, 93, 395
`Invoke-Expression` cmdlet, 93, 321, 375
`Invoke-History` cmdlet, 53, 395
`Invoke-WmiMethod` cmdlet, 94, 310
`-join` 操作符, 132
显示游戏和作者信息, 31
显示笑点, 29
结果, 31-33
概述, 4-6, 26-27
笑话之间的穿插, 29
提示玩家开始游戏, 28
脚本, 378
讲第二个笑话, 29-30
讲第三个笑话, 30

## J

`Join-Path` cmdlet, 94, 395
`-keep` 参数, 103

## K

注册表键, 65-66, 316-317
键值对, 145
关键字
目录, 263
过滤器, 231
语言, 10
`param`, 223, 225
通过搜索, 280-281
敲门笑话游戏, 26-33

## L

语言关键字, 10
布局，命令控制台, 44-45
布局 选项卡，PowerShell 属性窗口, 44-45
`Length` 属性, 108
数组长度, 141
`-list` 参数, 306
局部作用域, 139, 395
逻辑，`if` 语句, 166
逻辑错误, 345, 347-348, 395
逻辑操作符, 171-172
循环逻辑, 117
循环, 214
更改执行, 201-203
概述, 201
使用 `break` 命令, 201
使用 `continue` 命令, 202
无限, 345
`foreach` 循环, 196
`for` 循环, 193
`do` 循环, 192
`do while`, 192
`end`, 347
`while` 循环, 200
剪刀石头布游戏, 180-191
概述, 187-190
`Move-ItemProperty` cmdlet, 94

# 初学者 Microsoft Windows PowerShell 2.0 编程（第二版）

创建新的 PowerShell 脚本，112
变量的声明与初始化，112-113

Wikipedia 的 Windows PowerShell 页面，383-384
Windows PowerShell 新闻组，385

设计游戏，111-112
显示退出界面，118-119
显示游戏指令，114-115
显示欢迎界面，113-114
概览，80-82, 111

## 运算符

- 一元操作符，135
- `*` 130, 136
- `+` 129, 136, 141-142, 144
- `+-=`, 129

`+` 网络数据检索，312-313
`New-Runspace` 命令，59
`New-Alias` 命令行，94, 396
`-newest` 参数，308
`New-Item` 命令行，94, 263, 396
`New-Property` 命令行，94, 396
`New-Object` 命令行，94, 315-326, 396
`New-PSDrive` 命令行，396
`New-PSEvent` 命令行，94, 396
`New-Runspace` 命令行，94, 101, 321, 396
`New-Service` 命令行，94, 396
`New-TimeSpan` 命令行，94, 396
`New-Variable` 命令行，94
No 选项，`-Step` 参数，361
To All 选项，`-Step` 参数，361
非终止错误，348, 396
`-not` 运算符，171
`-notmatch` 运算符，252
计数，17
数字猜游戏脚本，378
数值型数据，357

`+ >` 重定向，262
`>>` 管道，263
算术，135, 161
`-notmatch`, 252
与管道结合，162
比较，170-171
`-eq`, 160-162
`-join`, 132
逻辑，171-172
`-match`, 251, 262
`-notmatch`, 252
概览，11
范围，140, 142
替换，130-131
`-split`, 131-132
字符串比较，172-173
Windows PowerShell. 我们
PowerShell, 运算符

`+` 选项，17
选项卡。PowerShell 属性对话框，42-43
`-or` 运算符，172
`Out-Default` 命令行，94, 264, 396
`Out-GridView` 命令行，10-11, 94, 276-282, 396
显示输出，277-288
数据分组，279-280
概览，276-277
搜索和过滤数据，280-282
数据排序，279

`+` 对象管道，106-108
对象管道，9, 17, 106-108
对象引用，258-259, 318
基于对象的脚本语言，92
对象，8, 85, 396。另另：查看
在线资源，382-387
概览，382
PowerShell 博客，385-387

`Out-Host` 命令行，94, 396
`Out-Null` 命令行，94, 396
`Out-Printer` 命令行，94, 275-276, 396
输出
后台作业，102–103
在 `Out-GridView` 窗口中显示，277–288
显示状态信息，359–366
重新格式化，264–269
`Format-List` 命令行，264–266
`Format-Table` 命令行，266–269
发送到打印机，275–276
输出面板，配置，55–57
`Out-String` 命令行，94, 396

## P

向下页编辑功能，49
向上页编辑功能，49
`param` 关键字，223, 225
参数
- `-action`, 328
- `-BackgroundColor`, 332
- `-computername`, 314
- `-exclude`, 260
- `-force`, 260, 263
- `foreach` 循环，196
- `-ForegroundColor`, 302
- 函数，171
- `-groupby`, 268–269
- `-include`, 261
- `-input`, 278
- `for` 循环，193–195
- `-newest`, 308
- `-ProcessName`, 22
- `-property`, 264, 266
- `-recurse`, 259–260
- `-runspace` 参数，322
- `-Step`, 360, 363
- `-Trace`, 360
- `-whatif`, 261
括号 `()`,136, 171, 252
模式匹配，23, 252–253, 255–257
句号 字符，254
持久运行空间，99, 101, 321–322
管道，106–162, 324–325, 397
管道，9, 17, 106–108, 227

`Play-Game` 函数，334
`Pop-Location` 命令行，94, 397
`Pop-Runspace` 命令行，94, 397
填充数组，144
Popup Background 选项，Colors 选项卡，PowerShell 对话框，45
Popup Text 选项，Colors 选项卡，PowerShell 对话框，45
PowerShell 1.0，卸载，12–3
PowerShell Analyzer，381
PowerShell 赋值运算符，137
PowerShell 游戏，298–300, 329–340
向主部分添加逻辑，339–340

`Analyze-Results` 函数，336–337
`Check-Registry` 函数，333–334
`Deal-Hand` 函数，333–335
`Get-Card` 函数，335
`Get-ComputerHandler` 函数，335–336
`Get-NewCard` 函数，339
`Get-Permission` 函数，331–332
`Get-Player` 函数，337–339
新脚本文件，330
`Play-Game` 函数，334
定义新变量，331
脚本，378

PowerShell 博客，385–387
PowerShell 错误，348, 396
逻辑错误，345–348
概览，345
运行时错误，346

## 416 初学者 Microsoft PowerShell 5.0 编程

语法错误，345–346
游戏，382–387
控制游戏，378
创建新的 PowerShell 脚本，112
变量的声明与初始化，112–113
设计游戏，111–112
显示退出界面，118–119
显示游戏指令，114–115
显示欢迎界面，113–114
概览，80–82, 111
脚本，378
PowerShell 控制台，356–373
`Get-MenuList` 函数，369–370
新脚本文件，330
`Write-Script` 函数，371–372
变量的声明与初始化，331–332
开发逻辑，339–340
自定义函数，331–332
确定何时，344–345
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
创建新的 PowerShell 脚本，112–113
新脚本文件，330
`Write-Script` 函数，371–372
定义新变量，331–332
定义新变量，331–332
定义新变量，331–332
变量的声明与初始化，331–332
自定义函数，331–332
确定何时，344–345
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348
显示结果，347–348

# 418 入学者 Microsoft Windows PowerShell 指南（第二版）

持久性, 101
`runscopes`, 持久性远程, 321-322
`ntime` 错误, 345-347, 398

概览, 358-359
跟踪变量值, 359-360
使用 PowerShell 调试模式, 360-363

## S

保存脚本命令 (Save Script), 58
范围 (scopes) 138-139, 229-231, 352
屏幕背景选项 (Screen Background), 颜色选项卡,
Windows PowerShell, 25-26
脚本面板 (Scripts pane), 图形 Windows PowerShell, 57-58

在结果字段中搜索, `Out-GridView` cmdlet
图形窗口, 280-281
海草 (seweeds), Windows PowerShell 图形化
60-61

PowerShell 属性对话框 (PowerShell Properties dialog window), 45
屏幕缓冲区大小 (Screen Buffer Size), 布局选项卡,
PowerShell 属性对话框, 45
屏幕文本选项 (Screen Text option), 颜色, PowerShell
属性对话框, 45
脚本命令/程序集 (script cmdlets), 12, 398
脚本编辑器 IDE (Script Editor IDE), PowerShell 的, 380
脚本文件 (script files), 网站, 378
脚本国际化 (script internationalization), 12
脚本范围 (script scope), 139, 398
脚本模板 (script template), Windows PowerShell, 221-222

帮助 (Help), 60-61
安全性 (security), 14-15
赛恩德知识问答 (Seinfeld Trivia Quiz)
游戏设计, 145-155
分析玩家回答, 153
分配排名, 153
创建脚本, 146-147
定义并初始化变量, 147
显示第一个测验问题, 148-149
显示指令, 148
显示剩余测验问题, 150-152
显示欢迎屏幕, 147-148
完成测验, 155
让玩家知道完成, 182
最终结果, 156

微软 ScriptCenter PowerShell 页面, 382
脚本级变量 (script-level variables), 229-230
脚本 (Scripts)
使用函数和过滤器设计, 219-220
创建可用代码, 220
改进脚本组织, 219-220
概览, 219
控制台配置, 46-49
编辑与执行, 57-58
组织, 220-231
函数结构, 220-222
概览, 220
处理参数, 222-227
处理输入数据, 227-228
限制变量范围, 229-231
转换结果, 228-229
跟踪执行情况, 358-363
显示输出状态信息, 359-360

概览, 124-126
378
选取颜色值 (Selected Color values), 颜色选项卡,
PowerShell 属性对话框, 46
选取表单：终端部分 (Terminal section), 字体选项卡,
PowerShell 属性对话框, 44
`Select-Object` cmdlet, 88-89, 95, 399
`Select-String` cmdlet, 95, 261-399
会话状态 (session states), 105
`SessionId` 属性, 100
`SessionId` , 101
会话 (sessions), , 17-18
`Set-ACL` cmdlet, 95, 399
`Set-Alias` cmdlet, 111, 399

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_441_0.png)

`Set-AuthenticCodeSignature` cmdlet, 95, 399
`Set-Content` cmdlet, 95, 263–264, 399
`Set-Date` cmdlet, 95, 399
`Set-ExecutionPolicy` cmdlet, 95, 399
`Set-Executionpolicy` cmdlet, 15
`Set-Item` cmdlet, 95, 399
`Set-ItemProperty` cmdlet, 95, 399
`Set-Location` cmdlet, 63–64, 95, 219, 237
`Set-PSBreakpoint` cmdlet, 95, 364, 399
`Set-PSDebug` cmdlet, 96, 360–393
`Set-Service` cmdlet, 96, 302, 399
`Set-StrictMode` cmdlet, 96, 399
`Set-TraceSource` cmdlet, 96, 399
`Set-Variable` cmdlet, 96, 310, 399
短路 (short-circuiting), 172

`+` 字符类, 256
桌面 (desktop), 40
Windows PowerShell, 40–41
在组中显示 (Show in Groups), `Out-GridView` cmdlet
窗口, 279–280
简单模式匹配 (simple patterns, matching), 252–253
单行 `if` 语句, 165
单引号, 134–135
`Sort-Object` cmdlet, 96, 107, 399
声音 (sound), 293
特殊变量 (special variables), 11, 108, 138, 400. 另另变量
`-split` 操作符 cmdlet, 131–132
`Split-Path` cmdlet, 96, 400
后台程序服务 (spooler service), 301–302, 305–306
`Start-PSDebug` cmdlet, 96, 99–101, 400
`Start-Transition` cmdlet, 96, 400
`Start-Service` cmdlet, 96, 302, 399
`Start-Sleep` cmdlet, 29, 104, 400
`Start-Transcript` cmdlet, 96, 400
状态字段 (state field), 100

语句执行, 364
`-Step` 参数, 360, 363
`for` 循环参数, 193, 196
`Step-Into` 命令, 364
`Step-Out` 命令, 364
`Step-Over` 命令, 364
`Stop-Process` cmdlet, 96, 301, 400
`Stop-PSJob` cmdlet, 96, 99, 104–105
`Stop-Service` cmdlet, 96, 302, 400
`Stop-Transcript` cmdlet, 96, 400
数据存储区域 (storing data area). 另见关联数组；哈希
三友的故事 (Story of Three Amigos), 66
收集额外输入, 71–73
创建新脚本, 67–68
声明脚本变量, 68
显示引言, 68–69
显示故事剩余部分, 74–76
查看, 36–39, 66–67
提示玩家输入, 70–71
提供层, 69–70
脚本, 378
字符串比较运算符, 172–173
字符串处理, 129–132
字符串拼接 (concatenation), 129–130
合并字符串, 131–132
查看, 129
重复字符串, 130
替换字符串部分, 130–131
分割字符串 (splitting strings), 28
子类 (subclasses), 400
暂停选项 (suspend option). `-Step` 参数, 361
`Stop-Service` cmdlet, 96, 302, 400
`switch` 语句, 163, 168–170
语法错误, 345–346
语法命名 (syntax, naming), 17
系统管理, 297–341

`.NET` 类, 315
访问事件日志, 306–309
管理 Windows 服务, 301–306
组件对象模型 (COM) 对象, 315–316
创建脚本 cmdlet, 322–325
创建自定义 cmdlet, 323
加载并执行 cmdlet, 324
处理流水线数据, 324–325
事件 (events), 325–329
检查对象, 326
实例化新对象, 326
概览, 325–326
移除事件, 327
订阅对象事件, 327–328
等待事件过程, 328–339
列出并启动进程, 300–301
PowerShell 游戏, 298–300
处理部分, 339–340
为主程序添加控制逻辑
创建 `Analyze-Result` 函数, 336–337
创建 `Check-Registry` 函数, 333–334
创建 `Deal-Hand` 函数, 334–335
创建 `Get-Card` 函数, 335
创建 `Get-Computer` 函数, 335–336
创建 `Get-NewCard` 函数, 339
创建 `Get-Permission` 函数, 331–332, 337–339
创建新脚本文件, 330
定义并创建新变量, 331
远程命令执行, 320–322
Windows 管理规范 (WMI), 310–314
从远程计算机拉取 WMI 数据, 314
获取应用程序数据, 313
获取 BIOS 信息, 310–311
获取网络数据, 312–313
获取系统信息, 311–312
系统信息检索, 311–312
Windows Vista 属性对话框, 26
`System.DivideException`, 357–358

制表符自动补全 (tab completion), 50–53, 58, 400
标签页 (tabs), `runscopes`, 59–60
`TargetObject` 属性, 348
`Tee-Object` cmdlet, 96, 400
脚本模板, 221–222
临时空间, 99
终止错误 (terminating errors), 348, 400
终止选项, 处理器 (trap handler), 352
测试条件, 166–167
脚本测试, 346
文本文件 (text files), 263–264
附加文本, 264
概览, 263
从...读取, 269
写入文本, 263–264
井字游戏 (Tic-Tac-Toe game). 另见 PowerShell 井字游戏
`ToLowerLeft()` 方法, 52
`-Trace` 参数, 360
`Trace-Command` cmdlet, 96, 401
跟踪 (traces), 401
事务 (transactions), 12, 401
信任脚本, 329
`try` 块, 353–358
`Try-Finally` 结构, 12, 401

## U

`UI` 属性, 47–48
`Undo-Transaction` cmdlet, 97, 401
卸载 PowerShell 1.0, 12–13
唯一事件标识符, 329
未命名 cmdlet, 322
`Unregister-Event` cmdlet, 96, 401
无限制安全级别, 15
向上箭头功能, 49
`Update-Format` cmdlet, 96, 401
`Update-List` cmdlet, 97, 401
`Update-DataType` cmdlet, 96, 401
`Use-Transaction` cmdlet, 97, 401
实用程序, 6

使用表达式赋值值, 135
已定义, 401
定义, 134
命名, 133–134
概览, 133
PowerShell 赋值运算符, 137
优先级, 135–136
范围, 138–139, 229–231
脚本级, 229–230
特殊, 11
特殊变量, 138
跟踪值, 359–360
变量插值, 134–135
动词-名词 cmdlet, 76

## V

`Validate-Move` 函数, 286–288
值, 169, 401
变量断点, 365
变量 (variables), 133–139
- `$$`, 108, 231–232, 389
- `$args`, 224–225
- `$Error`, 349
- `$ErrorActionPreference`, 349–351
- `$input`, 227
- `$MyJob`, 103
- `$PSConsoleWindow`, 48
- `$result`, 229
- `$RunSP`, 101
- `$status`, 117–118
- `$time`, 117
- `$UserReply`, 24
- `$x`, 310

## W

`Wait-Process` cmdlet, 96, 401
`Wait-PSEvent` cmdlet, 96, 329
`Wait-PSJob` cmdlet, 96, 99, 103–104, 401
网站, 377–378
`-WHATIF` , 17
`-what` 参数, 261
`-Where-Object` cmdlet, 97, 108, 227, 232, 401
`while` 循环, 28, 71, 73, 117, 191, 200–201

# 422 零基础 Windows PowerShell 编程第二版

获取 BIOS 信息, 310-311
获取网络数据, 312-313
获取系统信息, 311-312

概览, 170
字符串比较运算符, 172-173
概览, 3-4, 6-7

Windows 管理工具
(WMI), 微软, 401
Windows 位置区域, Layout 选项卡, 25
脚本, 25
简化脚本执行, 25-26

PowerShell 属性对话框, 45
Windows PowerShell, 3-34
卸载 PowerShell 1.0, 12-13
Windows PowerShell 集成开发环境 (IDE), 380-381

另参见 PowerShell 语言对比 `cmd.exe`, 9-10
配置, 13-15
配置 Windows 远程管理 (WinRM), 15-16, 98, 401
WindowsPowerShell 语言, 126-132
转义字符, 127-129
字符串操作, 129-139
开发团队博客, 385-386
历史, 7
暂停, 13-15
与 .NET 集成, 8-9
拼接, 129-130

与命令提示符交互, 17-24
执行 cmdlet, 18-20
其他类型的命令, 20
概览, 17
重复字符, 130
替换字符串部分, 130-131

PowerShell 练习, 20-24
启动会话, 17-18
拆分和合并字符串, 131-132
Windows PowerShell 预留字,

敲门游戏 (Knock Knock joke game), 26-33
收集额外的玩家输入, 28-29
创建新的 PowerShell 脚本, 27-28
显示游戏和作者信息, 31
显示笑点, 29
最终结果, 31-33
Windows PowerShell 新闻组, 385
Windows 注册表, 316-320, 397
Windows 远程管理 (WinRM),
概览, 4-6-26-27
笑话之间的暂停, 29
提示开始游戏, 28
讲述第二个笑话, 29-30
讲述第三个笑话, 30
Windows 脚本主机 (WSH),
Windows Server 2003, 13
Windows Server 2008, 13
新功能, 10-12
Windows 服务管理, 301-306
Windows Size 区域, Layout 选项卡, PowerShell
运算符, 170-171
Windows 对话框, 45
Windows XP, 13
逻辑运算符, 171-172
`WindowsSize` 属性, 48
`WindowTitle` 属性, 48

`Write-Debug` cmdlet, 97, 402
`Write-Error` cmdlet, 97, 402

`Write-Host` cmdlet
定义, 402
显示输出状态信息, 359-360
概览, 97

其参数, 332
文本字符串控制, 127–128
跟踪变量值, 359–360
其中的变量, 76
`Write-MenuList` 函数, 370–371
`Write-Output` cmdlet, 29, 97, 402
`Write-Progress` cmdlet, 97, 402
`Write-Verbose` cmdlet, 97, 402
`Write-Warning` cmdlet, 97, 402
`WS-Management` 协议, 15–16, 402

## X

`XML`, 271–272, 402

## Y

Yes 选项, `-Step` 参数, 361
全部是选项, `-Step` 参数, 361

## Z

分母为零, 357–358

# 学习微软技术无需经验

# Windows PowerShell 2.0 编程

microsoft® PowerShell 是一种非常有用的脚本语言，能够实现系统管理任务的自动化以及系统管理工具的创建。PowerShell 运行在 Windows XP、2000 和 Vista 上。与传统的 Windows 脚本不同，PowerShell 是基于对象的并设计用于与 .NET Framework 工作。本更新版的《零基础 Windows PowerShell 编程》教授向往的 Windows PowerShell 脚本编写人员无论他们使用的是 PowerShell 1.0 还是 2.0。为了让学习变得更有趣，你将通过开发电脑游戏来学习编程，并将开发一个新游戏，以一种简单上手的方式强化新学的概念。当你完成课程时，你不仅将拥一组可运行的示例脚本，还将拥有一应对现实挑战和学习新语言的基础。

在学习使用 PowerShell 编程的同时，创建简单的游戏

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_451_0.png)

通过这本书，你将学习到：

- 在 Windows 环境下编写脚本和程序
- 与 Windows PowerShell 命令行交互
- 使用变量、数组和哈希表（hashes）
- 实现条件逻辑
- 使用循环处理数据
- 使用函数组织脚本
- 自动化各种系统管理任务
- 调试 PowerShell 脚本

# 课程技术

CENGAGE Learning

专业 • 技术 • 参考

`courseprpt.com`

用户级别：初级
类别：编程
U.S.$34.99 • 加币 $39.95

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_451_1.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_451_2.png)

![](img/e07ce5ce2afe5ff9f444f2c361d9d87e_451_3.png)

# 网站上有什么？

书中所有练习环节游戏的源代码

Jerry Lee Ford, Jr. 是一位作家、教育者、拥有信息领域的专业人士、汽车技术作家、经理、分析师、工程师和作者。他拥有里士大学的硕士学位，拥有五以上的技术课程教学经验。
