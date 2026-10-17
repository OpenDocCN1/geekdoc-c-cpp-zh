
配置 Team Foundation Server 和 Project Server 之间的集成包含一些初始步骤，这些步骤非常简单，且只需执行一次。每创建一个包含与 Team Foundation Server 同步任务的新企业项目时，都需要执行其中一个步骤。在本节中，你将介绍设置集成的要点。

# 必要的权限

作为管理员，你可能希望确保为运行 Team Foundation Server 和 Project Server 的服务账户提供适当权限。这是你需要确保完全完成的领域之一，如果设置不当，这是一个常见的问题区域。以下列表提供了必要权限的摘要：

- 对于 Project Server 2007，你必须授予 Team Foundation 服务账户访问共享服务提供程序（Shared Services Provider）的权限。

- 对于 Project Server 2010 和 Project Server 2013，你必须授予 Team Foundation 服务账户访问 Project Service 的权限。你还需要为每个 PWA 实例授予所需的权限。请务必检查这两项，这似乎是许多团队遗漏的区域。你可以通过阅读 `http://aka.ms/TFSPFPermissions` 的文章获取有关此类集成的必要权限的信息。

# 配置命令行工具

用于管理 Team Foundation Server 和 Project Server 集成的命令行工具名为 `Tfsadmin.exe`。当你安装任何版本的 Visual Studio 2012 时，可以使用该工具。你可以通过打开命令提示符并导航到以下目录找到该工具：

```
cd %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE
```

# Project Server 安装组件

此外，你需要在 Project Server 拓扑中的每个层级安装 Team Foundation Server 扩展，

- 每个托管 Project Server 2007 的应用层服务器，将与 Foundation Server 同步

- 每个托管 Project Server 2010 或 Project Server 2013 的 Web 层和应用层服务器，将与 Foundation Server 同步

Team Foundation Server 扩展现在作为 Team Foundation Server 2012 镜像的一部分（如图 15-4 所示）。这些扩展在 Team Foundation Server 2010 版本中作为功能包单独提供，但现在已包含在 Team Foundation Server 2012 镜像中。

# 一次性集成步骤

如前所述，需要执行一次性步骤来映射 Project Server 和 Foundation Server 实例以便它们同步。以下是这些步骤的简要概述；更多信息可以参考 `http://aka.ms/TFSPFConfiguration`

步骤 1：你需要注册包含与 Team Foundation Server 同步的企业项目的 Project Web Access（PWA）实例。你通过运行此命令行来执行第一步，并根据你的设置替换相应的值：

```
TfsAdmin ProjectServer /RegisterPWA
/pwa:http://project.contoso.local/pwa
/tfs:http://tfs.contoso.local:8080/tfs
```

步骤 2：接下来，你可能希望将 Project Web Access（PWA）实例映射到其同步的项目集。你可以通过运行以下命令行执行此操作，并根据你的设置替换相应的值：

```
TfsAdmin ProjectServer /MapPWATCollection
/pwa:http://project.contoso.local/pwa
/tfs:http://tfs.contoso.local:8080/tfs/DefaultCollection
```

# 第 3 步：你将为参与同步的每个团队项目集合定义字段映射。你可以使用默认字段映射，也可以使用本章稍早描述的自定义字段映射集：

```
TfsAdmin ProjectServer /MapFieldMappings /collection:http://tfs.contoso.local:8080/tfs/DefaultCollection /useDefaultFieldMappings
```

一旦完成这三个步骤，同步就准备就绪了，你不需要再次运行这些命令。对于每个企业项目，你还有最后一步，这将在下一节中介绍。

![](img/aaf6096fc6b4485534c737801bdbc4fd_405_0.png)

图 15-4：带有 Project Server 扩展的 Team Foundation Server ISO/镜像

# 将企业项目映射到团队项目

现在你已经为 Team Foundation Server 和 Project Server 配置了初始集成，对于每个参与同步的企业项目，你将会有最后一个操作。以后当项目经理创建新的企业项目时，这就是你需要执行的步骤，因此你应该告知项目经理，让他们在创建新企业项目后通知 Team Foundation 管理员。

此步骤每个项目仅需执行一次，你应该通过映射管理器指定应参与同步的工作项类型：

```
TfsAdmin ProjectServer /MapPlanToTeamProject /collection:http://tfs.contoso.local:8080/tfs/DefaultCollection /enterpriseproject:"E-Commerce Site Project Plan" /teamproject:"Engineering" /workitemtypes:"User Story,Task"
```

工作项类型的最后一个选项将取决于你的团队项目所使用的过程模板。上一个示例的命令行输入使用了 MSF Agile 过程模板。如果你使用的是 Scrum 过程模板，可能希望指定使用产品积压列表（Product Backlog Items）和任务（Tasks）。对于 MSF CMMI 过程模板，你可能会指定需求（Requirements）和任务（Tasks）。

你会注意到工作项列表包含空格字符来分隔每个工作项类型，但每个列表项之间不包含空格。系统不接受空格，因此在将来运行此命令行输入时，请务必使用正确的语法。

# 项目经理所需的软件

下一个需要记住的一点是，使用 Project Server 的项目经理如果想输入已发布的企业项目，则需要在他们的机器上安装适当的软件。项目经理机器所需的最小安装如下：

- Microsoft Office Project 2007 Professional、Microsoft Office Project 2010 Professional 或 Microsoft Office Project 2013 Professional

- Team Explorer for Visual Studio 2012 (`http://aka.ms/TeamExplorer2012`)

| 项目经理的 TEAM FOUNDATION SERVER CAL 要求 |

| 尽管需要安装 Team Explorer 才能在 Microsoft Project 中获取项目插件，但如果项目经理仅连接到 Project Server，则不需要 Team Foundation Server 访问许可 (CAL)。如果他们需要查看详情并以其他方式与 Team Foundation Server 交互，则需要 CAL，此时你仍然需要为项目经理准备一个 CAL。你可以在 MSDN 文章 `http://aka.ms/TFSPSConfiguration` 中找到更多关于此要求的信息。 |

## 总结

如你所示，Project Server 和 Team Foundation Server 的集成对于某些团队和组织非常有益，可以让他们项目经理和软件工程团队之间保持一致。

在本章中，你学习了 Project Server 和 Team Foundation Server 之间的集成。你回顾了 Project Server 何何合理以及在哪些方面具有优势的场景，以及集成可能有利的情况类型。

你还回顾了集成中引入的概念以及设置集成所需的步骤。最后，你回顾了项目经理在机器上安装的必要条件。

在第 16 章中，你将开始学习的的一部分，讨论 Team Foundation Server 的自动化构建系统。

# 第四部分

# Team Foundation Build

- 第 16 章：构建自动化概述

- 第 17 章：使用 Team Foundation Build

- 第 18 章：自定义构建过程

# 16

# 构建自动化概述

**本章包含哪些内容？**

- 了解构建自动化

- 编写构建脚本

- 使用构建自动化服务器

- 采用构建自动化

在版本控制之后，控制构建是你提高软件质量所能做的第二重要的事情。本章定义了构建自动化，并研究了它为什么对整个软件工程过程有益。随后将介绍 Team Foundation Server 的高级能力和局限性，并与目前使用的常用构建系统进行比较。最后，提供了一些通用建议，以帮助现在就在你的环境中采用构建自动化。

本书的后续章节将深入探讨 Team Foundation Server 的构建能力，讨论如何自定义构建过程，并通过在现实场景中处理常见的构建自定义来演示这一点。

# 让我们构建些什么

想象正在盖一栋房子。你每天都去现场，看到的只有一片泥泞的空地。施工团队告诉你：“是的，我们进展非常顺利。门都做好了，看起来很棒。墙好了 80%。水路准备就绪，厨房也准备好安装了。”你每天看到的都是同一片泥泞的空地。施工团队告诉你进展多么顺利。他们用各种故事来调节你，说他们如何决定门不符合要求，于是把它们扔进火堆，从头开始建造了新的双向开启门，甚至在你决定养猫之前，这些门就都准备好了合页。

你从未见过任何进展——只有一片泥泞的空地和一群忙碌且焦虑的人。

然后，在你搬进去的前一天，所有东西同时到达了。这花费的时间比大家想象的要长得多。天黑了，夜降了，大家精疲力竭，他们拼命地试图把这些东西组合在一起。

第二天早晨，你看了你的房子。这确实是一栋房子。几个房间还没有完工，因为它们到达时没有对齐。缺少几个螺丝，漆不是你选择的颜色，很多地方不像你几个月前规划时想象的那样。更让你尴尬的是，当你看到房子时，想到了某些本该有额外插座的地方，意识到你可能永远用不上那个昂贵的浴缸。现在，想象一下你的客户在面对软件这种瞬态物时的感受如何。你如何向客户展示进度？你如何知道他们是否满意？你如何知道它是否有效？你如何知道你是否完成了某个功能，或者某个功能是否足够进入下一个？

知道这一切的唯一方法就是组装你的软件并进行测试，运行你的应用程序或访问网站。有些区域缺失或尚未完全功能，但一旦你能看到你的应用程序，就能知道离完成还有多远；一旦客户看到它，他可能会说你认为只实现部分的功能实际上已经满足了他的需求。但你不需要为此做太大修改。

问题是，组装应用程序需要时间。通过在软件开发过程中对这种体验进行投资，你不仅可以准确衡量和展示进度，还消除了最后冲刺阶段巨大的错误来源。

如果你认真交付软件的质量，你就需要认真对待构建自动化。

# 什么是构建自动化？

构建自动化是简化构建过程的过程，以便通过简单的单操作将应用程序组装成可用的产品。这不仅涉及特定开发者正在工作的代码部分，还包括其他典型活动：

- 将代码编译为二进制文件

- 将二进制文件封装成 MSI 文件、XAP 文件、JAR 文件、DMG 镜像等可安装模块

- 运行测试

- 创建文档

- 部署结果已就绪并可以使用

只有当应用程序的各个组合在一起后，你才能判断应用程序是否正常工作以及它的预期功能。组装应用程序的各个通常是一个复杂、耗时且容易出错的过程。构建应用程序有许多部分，如果没有自动化构建，这些活动通常会落在团队中一两位掌握“秘诀”的个人身上。如果没有自动化构建，即使他们犯了错误，这种毁灭性的后果直到后期才发现，使得修复任何错误的成本都非常高昂。

想象一下，你必须回想整个错过的 DVD 运行过程来发现漏了一个重要文件。糟糕糟糕，想象一下在广泛分发时不不小心包含了应用程序的源代码，或者在部署到生产环境时留下了尴尬的测试数据。当这些事情发生在软件开发机构时，曾登上头条新闻，而它们本可以轻松避免这些问题。

软件组件的集成是最困难的部分。开发者在隔离状态下开发功能，对系统其他部分的工作方式做出各种假设。如果你整合了所有内容，并且这些集成随着假设的测试而进行组装，它们就能在开发过程中尽早发生——从而降低修复不可避免的问题的成本。

对于参与项目的每个人来说，运行最新构建的副本应该是轻而易举的。只有这样，你才能知道软件是否正常以及它的预期功能。只有这样，你才能按时完成你的工作。定期的自动化构建是你系统的心跳。

在 Visual Studio 2012 中，开发者通常可以通过按 F5 键运行调试模式来运行应用程序。这会在本地工作站上将代码汇编并执行。这使得开发者测试其代码库部分变得轻而易举。但这不能确保代码与团队其他成员提交的所有最新更改兼容。此外，按 F5 键仅仅完成了代码的编译，供你手动运行和测试。

作为自动化构建的一部分，你不仅可以测试代码是否正确编译，还可以确保它运行全套的自动化测试。这会立即带给你极大的信心，确保没有引入任何破坏其他内容的更改。

对于开发者来说，按 F5 键很容易。但当你想要自动化构建让运行你的应用程序变得同样容易——甚至更简单时，这就是构建自动化服务器发挥用场的地方。

构建自动化服务器是一台加载版本控制中的更改并自动重新构建项目的机器。这可以按需进行、按照定期计划（例如每晚或每日构建）进行，也可以在开发者每次提交代码时执行——这一过程被称为持续集成。当某些内容被提交时，软件开发团队有机会在提交者脑海中对该内容记忆新鲜时立即修复它。通过尽早修复问题，可以将修复该问题的成本降至最低，并防止团队中的其他人员由于某人破坏了他们所依赖的内容而无法构建或测试他们的组件。

然而，在构建服务器上设置持续集成构建之前，你必须为你的构建编写脚本，使其能够通过单个命令运行。

# 马丁·福勒论持续集成

持续集成（CI）一术语源于世纪末的敏捷软件开发方法，如极端编程（XP）。马丁·福勒（Martin Fowler）在 2000 年发表的关于持续集的论文，在今天于 `www.martinfowler.com/articles/continuousIntegration.html` 仍然值得阅读。

请注意，按照最初的描述，该术语指的是通过增加集成频率来提高软件交付的速度和质量，而不是为每次提交都构建一个版本的实践。福勒所展示的许多实践得到了 Team Foundation Server 中工具的支持——不仅仅是构建服务中的这一项小功能。然而，“持续集成”术语已成为提交后进行构建的同义词，因此 Team Foundation Server 将其作为此类触发器的名称，正如第 17 节讨论。

# 编写构建脚本

构建自动化最基本的形式是编写一个执行清理构建所需所有操作的脚本。这可以是 shell 脚本、批处理文件、PowerShell 脚本等。然而，由于你在构建期间执行的常见任务（如依赖跟踪、编译文件、合并批文件等），多年年来开发了一些专门的构建脚本语言。

# Make

专门构建脚本语言的鼻祖是 Make。Make 最初由 Stuart Feldman 博士于 1977 年在贝尔实验室创建，它现在在 UNIX 平台上仍被广泛使用，用于通过读取存储在名为 `makefile` 的文本文件中的构建配置来从源代码创建程序。通常，为了构建一个可执行文件，你必须输入多个命令来编译和链接源代码，同时确保每个依赖项都已正确编译和链接。Make 的设计专门用于帮助 C 语言程序员以高效的方式管理这一过程。

`makefile` 定义了一系列目标，每个命令在冒号内部使用制表符缩进：

```
#注释
目标: 依赖项
<TAB>命令
```

例如，一个简单的 Hello World 应用程序可以如下 `makefile`：

```
# 定义 C 编译器和编译器标志
CC=gcc
CFLAGS=-g
```

当执行 `make` 时没有指定目标，则调用的默认目标。

```
all: helloworld

helloworld: helloworld.o
	CC ($CFLAGS) -o $@ $	# 注意：行以制表符开头

helloworld.o: helloworld.c
	CC ($CFLAGS) -c -o $@ $
```

```
clean:
	rm -f *helloworld
```

注意，Make 的主要功能之一是简化了依赖管理。也就是说，为了制作可执行文件 helloworld.o，它会检查 helloworld.o 是否存在以及其依赖项是否满足。helloworld.o 依赖于 C 源文件 helloworld.c。只有 helloworld.c 自上次执行 Make 后发生变化时，才会创建 helloworld.o。

之前的脚本等同于命令行中顺序执行的以下命令：

`gcc -c -o helloworld`

在所示的简单 makefile 中，一切都非常易读。对于执行打包和部署活动的复杂 makefile，可能需要一段时间才能弄清楚哪些命令按顺序执行。Make 使用声明式语言，对于习惯于使用命令式语言（大多数现代编程语言都是）的开发者来说可能难以阅读。对于许多开发者来说，这感觉你必须反向查看——即查看目标，然后跟踪它的依赖项，然后是它们的依赖项，以跟踪实际发生的顺序。

自从诞生以来，Make 经历了多次重写，并有很多在使用相同文件格式和基本原理的同时提供了自己的功能的衍生版本。许多平台都有 Make 的实现，包括来自 Windows 平台的 NMAKE。

# Apache Ant

Ant 是类似于 Make 的构建自动化工具，但它从底层就被设计为跨平台工具。James Davidson 最初在太阳公司开发了 Ant。它于 2000 年发布。根据 Davidson 的说法，“Ant”是 Another Neat Tool（另一个巧妙工具）的缩写。它是一个基于 Java 的工具，并使用存储在 `build.xml` 文件中的 XML 文件。
