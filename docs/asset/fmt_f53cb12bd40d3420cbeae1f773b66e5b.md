
为了完成书中的许多实操示例，拥有一个 Team Foundation Server 2012 环境或可以用于测试产品中不同功能的 Team Foundation Service 账户将非常有帮助。你并不需要专门的硬件，因为你现在可以在 Windows 8 和 Windows 7 等客户端操作系统上安装 Team Foundation Server 2012。不用担心设置和配置新的 Team Foundation Server 2012 环境，因为你将在第 2 章和第 3 章学习相关知识。

第 1 章讨论了获取 Team Foundation Server 的几种方案，包括用于演示目的的完整虚拟机。第 4 章还讨论了在本书中所需的连接到你的 Foundation Server 环境的不同工具。

示例的源代码可以从 Wrox 网站下载：

`http://www.wrox.com/remitle.cgi?isbn=9781118314098`

## 进一步学习

每位作者都会定期撰写关于 Team Foundation Server 和其他 Visual Studio 产品的技术文章，这些文章可能对你的进一步学习有所帮助。欢迎查看作者的博客站点，并在你喜欢的 RSS 阅读器中订阅它们。

- Ed Blankenship—`www.edssquared.com`

- Martin Woodward—`www.woodwardweb.com`

- Grant Holloway—`http://blogs.msdn.com/b/granth`

- Brian Keller—`http://blogs.msdn.com/b/briankel`

此外，我们还推荐你关注以下两个博客和 RSS Feed送，以获取所有新闻和更新：

- Brian Harry—`http://blogs.msdn.com/b/bharry`

- Visual Studio ALM 产品团队—`http://blogs.msdn.com/b/visualstudio`

## 持续的产品更新与发布计划

未来从微软学习 Visual Studio 和 Team Foundation Server 产品的主要的一点是，团队将更频繁地发布更新——每三个月一次。这些更新将包含性能改进、错误修复，以及已完成的新功能。对于那些使用托管版 Team Foundation Service 的用户，新的更新和功能将每三周自动部署一次。

需要记住的是，你要确保安装了 Visual Studio 产品的开发机器以及你的 Team Foundation 服务器始终保持最新版本。本书是针对发布版本编写的，包含了第一季度更新中的内容和功能。

你可以在 `http://aka.ms/TFSShippingCadence` 获取更多关于 Visual Studio 和 Team Foundation Server 这种新发布节奏的信息。

## 惯例

为了帮助你充分利用这些内容并跟踪进度，我们在书中使用了许多惯例。

| 类型 | 描述 |
| :--- | :--- |
| WARNING | 警告词汇包含重要的、不容忽视的信息，与周围文本直接相关。 |
| NOTE | 注释表示当前讨论的备注、提示、暗示、技巧或旁白。 |

### 侧边栏

对当前讨论的旁注以如下方式缩进。

关于文中的样式：

- 我们在引入新术语和重要词汇时会进行高亮显示。

- 我们这样显示按键操作：`Ctrl+A`。

- 我们在文中这样显示文件名、URL 和代码：例如：`persistence.properties`。

- 我们通过两种方式展示代码：

  我们使用等宽字体。

  我们使用加粗来强调重要内容。

## 源代码

在你阅读本书时，你可以在此处找到代码：

`http://www.wrox.com/remitle.cgi?isbn=9781118314098`

如果你在书中发现任何错误，请通过以下地址告诉我们：

`http://wrox.com/contact/techsupport`

## 勘误表

我们尽力确保书中没有错误。然而，没有人是完美的，错误在所难免。如果你在其中一书中发现错误，我们将非常感谢你的反馈。通过提交勘误表，你帮助我们提供更高质量的内容。

要查找本书的勘误表，请访问：

`http://www.wrox.com/remitle.cgi?isbn=978111831498`

## P2P.WROX.COM

关于作者和同行的讨论，请加入 `http://p2p.wrox.com`。论坛是一个基于 Web 的系统，可以在其中发布与 Wrox 书籍及相关技术的消息，并与其他读者互动。论坛提供了订阅功能，当有新帖子时会发送电子邮件。Wrox 的作者、编辑、其他行业专家和同行都在这些论坛中。

加入论坛，请按照以下步骤操作：

1. 访问 `http://p2p.wrox.com` 并点击 Register 链接。

2. 阅读使用条款并点击 Agree。

3. 完成加入所需的信息以及你想提供的任何可选信息，然后点击 Submit。

4. 你将收到一封电子邮件，说明如何验证你的账户并完成加入流程。

> NOTE 你可以在不加入 P2P 的情况下阅读论坛消息，但为了发布自己的消息，你必须加入。

## 第一部分

## 入门

- 第 1 章：介绍 Team Foundation Server 2012

- 第 2 章：规划部署

- 第 3 章：安装与配置

- 第 4 章：连接到 Team Foundation Server

## 1

### 介绍 Team Foundation Server 2012

本章内容概览：

- 了解 Team Foundation Server 2012

- 了解 Team Foundation Server 2012 的新功能

- 获取 Team Foundation Server 2012

本章将向你介绍 Microsoft Visual Studio Team Foundation Server 2012。在这里，你将学习它是什么、使用它时所需的概念，以及如何获取它。

对于已经熟悉 Team Foundation Server 的人员，本章的讨论重点强调了新特性或发生重大变化的领域。然而，理解某技术的历史传承总是有帮助的，本章还包含了 Team Foundation Server 的部分历史，这将有助于解释它是如何演变成今天样子的。

本章还讨论了改进的发布模型，包括利用 Team Foundation Service 让微软管理托管、频繁升级和备份的能力。后续章节将深入探讨 Team Foundation Server 产品的架构。

## 什么是 TEAM FOUNDATION SERVER？

软件开发是困难的——许多失败的项目都印证了这一事实。任何软件开发团队成功的关键因素之一是团队成员之间的沟通顺畅，以及与最初要求开发软件的人员之间的沟通情况。

## 第 1 章 介绍 TEAM FOUNDATION SERVER 2012

Team Foundation Server 在一个非常紧凑的产品中为你的软件开发团队提供了核心协作功能。Team Foundation Server 提供的功能包括：

- 项目管理

- 工作项跟踪 `WIT`

- 版本控制

- 测试用例管理

- 编译自动化

- 报告

- 实验室与环境管理

- 反馈管理

本书对这些主题中的每一个都进行了广泛的探讨。

Team Foundation Server 是一种专为软件工程团队设计的服务器产品，团队包括开发者、测试人员、架构师、项目经理、业务分析师以及任何对软件开发发布和项目做出贡献的人。从逻辑上讲，Team Foundation Server 由以下两个层组成，可以物理地部署在一台或多台机器上：

1. 应用层——该层主要由一组 Web 服务组成，客户端使用高度优化的基于 Web 服务的协议与其通信。它包含了丰富的 Web 站点访问，无需安装如 Visual Studio 等客户端即可访问服务器。

2. 数据层——该层由 SQL Server 数据库组成，包含 Team Foundation Server 应用程序的数据库逻辑以及你的 Team Foundation Server 实例数据。存储在数据库中的数据供 Team Foundation Server 的功能使用。存储在数据库中的所有数据都存储在此 SQL Server 数据库中，易于备份。

Team Foundation Server 在设计时考虑了扩展性。它可以集成一个全面的 API，使其能够作为“一等公民”与外部工具集成。微软使用 .NET 编程模型和事件系统来构建 Team Foundation Server，以及客户端与 Visual Studio 的集成。

Team Foundation Server 有许多竞争对手，包括其他企业级应用生命周期管理 `ALM` 系统和特定用途的产品（如源代码控制系统）。在产品中提供所有不同系统的主要优势在于 Team Foundation 充分地整合了这些不同的系统。这允许开发工具领域实现真正的创新，正如你在这一最新版本中提供的几个新工具中会注意到的那样。你不再需要担心自己去整合这些系统，而是利用微软已经为你完成的工作。

> 注意：Visual Studio 公司副总裁 Jason Zander 在一篇最初关于 Team Foundation Server 2010 的博客文章中很好地说明了这一点。你可以在 `http://aka.ms/IntegratedALMSSolution` 找到该博客文章。

当我们比较目前市场上的企业产品时，你会发现 Team Foundation Server 设计得非常易于定制和扩展。Team Foundation Server 确保使用任何开发平台的开发者都可以参与并使用 Team Foundation Server，包括 Visual Studio、基于 Eclipse 的开发、Xcode 等许多平台。

## TEAM FOUNDATION SERVER 2012 的新功能

如果你使用过旧版本的 Team Foundation Server，你可能对最新版本中的新功能感到好奇。本书将介绍 Team Foundation Server 2012。其改进的发布模型，包括让微软管理托管、频繁升级和备份的能力（通过利用 Team Foundation Service）。后续章节将深入探讨 Team Foundation Server 产品的架构。

关于工作空间，这些新功能将在后续章节中详细介绍。

### 版本控制

如果你使用过旧版本的 Team Foundation Server，你可能对最新版本中的新功能感到好奇。正如正如本书所展示的，这些新功能将贯穿始终。

Team Foundation Server 的一个目标是极大地改进开发人员的体验，例如在 Visual Studio 2012 中引入的改进。

#### 代码审查

Team Foundation Server 2012 还引入了一套内置的请求、响应和管理代码审查的体验。这套功能后台使用了强大的工作项跟踪体验来帮助你讨论。

#### 管理个人工作

在 Visual Studio 2012 中，连接到 Team Foundation Server 2012 时，还有新的体验用于管理你的个人内容和工作。

#### Web 访问

Team Web Access 在 Team Foundation Server 2012 中经过了重新设计，为那些没有任何传统客户端的用户提供了更好的体验。它支持现代浏览器（包括移动浏览器），并适用于多种设备形态。

## 项目管理

在 Team Foundation Server 2010 的 Service Pack 1 以及该发布版本的相关功能包中，产品团队引入了 Team Foundation Server 中的项目管理工作项与 Project Server 中的任务之间的双向同步支持。此同步已包含在 Team Foundation Server 2012 版本中。您可以在第 15 章了解更多关于 Project Server 集成的信息。

## 敏捷与 Scrum 产品管理

Team Web Access 新增的体验包括敏捷项目管理和产品规划。新的敏捷计划 `Agile Planning` 工具专为实践 Scrum 原则的用户设计，但实际上对使用任何流程的用户也大有益。

此版本中引入的主要工具包括：发布待办列表 `Release Backlog` 规划；冲刺/迭代规划 `包括团队负载能力`；速率和冲刺报告；以及一个适用于每日 Scrum 任务的新任务板。这些每项工具都以团队为导向，以便不同团队可以管理自己的待办列表和进度。

这些工具引入的优点之一是能够按日期跟踪和结束迭代 `Iterations`。这些迭代随后用于 Team Foundation Server，以提供更丰富的体验。

## 利益者反馈

团队和产品所有现在现在从其应用程序和软件的运行版本向利益者、业务用户和客户请求反馈。这些利益者将收到一封电子邮件，其中包含连接到 Team Foundation Server 的链接，并可以使用一个命名为 Microsoft 反馈客户端 `Microsoft Feedback Client` 的新轻量级客户端立即提供反馈。

## 构建

此版本还对内置构建系统进行了若干改进，包括对门禁检查 `gated-check-ins` 进行批量处理的能力。如果您一天内收到许多需要快速验证的检查。此外，新的 Team Explorer 包含了一些用户体验改进，包括将构建标记为公共或团队收藏，以及当您的团队包含大量定义时对定义进行过滤。

使用 MSTest 之外的第三方测试框架的开发团队很高兴知道，团队现在可以在 Team Foundation Server 2012 的自动化构建过程中在测试运行中包含测试。

## 获取选项

微软极大地改进了获取 Team Foundation Server 的方式。正如后续章节所述，有多种选项供您选择。

许可可能会有些混乱，但 Team Foundation Server 的许可遵循微软其他产品的许可模式。有一个服务器许可。此外，在某些显著例外的情况下，每个连接到服务器的用户都应该拥有 Team Foundation Server 的客户端访问许可 `CAL`。

> 注意：关于这些潜在例外的更多信息，或关于您需要购买什么的问题，您可以寻求具有 ALM 能力的微软合作伙伴、您的本地微软开发专家的帮助，或参考最终用户许可协议 `EULA`。此处还提供了适用于 Visual Studio、MSDN 和 Team Foundation Server 的许可白皮书：`http://aka.ms/VisualstudioLicensing`。

## Team Foundation Service

到目前为止，采用 Team Foundation Service 最简单的方法是通过微软直接提供的名为 Team Foundation Service 的托管选项。它与本地部署的 Team Foundation Server 产品共享大部分代码库，但经过修改以可以托管在 Windows Azure 上并供多个租户使用。可以在 `http://tfs.visualstudio.com` 获取。

使用 Team Foundation Service 的最佳部分是您的团队无需担心备份、高可用性、升级或其他潜在的耗时管理和维护任务。另一个好处是 Team Service 客户和本地客户都会接收包含新功能的更新。

> Brian Harry 宣布，内部产品团队在过去的两三年中改进了他们的工程流程，他们能够快速提供频繁的更新。通过 Team Foundation Server 2012，产品团队计划提供包含典型性能改进和错误修复的更新，同时也带来新功能。频率尚待定，但第一个本地更新将在 2012 年底之前可用。

Team Foundation 客户看到的更新频率将比本地修复更频繁。Brian 提到他的团队能够每三周部署一次热补丁，这与内部冲刺计划相一致。您可以从 Brian Harry 的博客文章 `http://aka.ms/TFReleaseCadence` 了解更多关于此主题的信息。

这次讨论可以获得的一点是，如果您选择本地安装 Team Foundation Server，请确保您的团队始终使用 Team Foundation Server 的最新更新。

使用 Team Foundation Service 的团队能够利用一组弹性标准服务器。这项弹性服务为您的每个构建提供可用且洁洁的标准构建。团队可以将他们的弹性构建与 Windows Azure 账户集成，以便为托管在 Windows Azure 上的应用程序或站点实例提供持续部署。团队还可以利用连接到 Team Foundation Service 的本地构建。

## 获取选项

微软已于 2012 年后期发布了广泛可用的 Team Foundation Service。他们宣布将为最多五人的团队免费提供全套功能集。MSDN 订阅者将可以将 Team Foundation Service 作为其 MSDN 订阅的额外福利。如果您或您的团队不属于上述任何一类，在公布更多细节之前，您将可以免费使用 Team Foundation Service。在任何时候，如果您决定不再继续使用 Team Foundation Service，您可以随时下载您的源代码并关闭账户。

迄为止，Team Foundation Service 与本地产品相比尚未实现完全对等。例如，实验室管理、报告和流程模板自定义功能目前尚不可。随着 Team Foundation Service 时间的推移，它将与本地版本具有更高、乃至完全的对等。

与此同时，对于希望获得全套功能但由他人管理其 Team Foundation Server 实例的团队，可以通过几第三方托管公司获得选项。

## Express

从 Team Foundation Server 2012 开始，小型软件工程团队可以利用 Team Foundation Server 2012 的 Express 版本，该版本对多达五名开发者免费。Team Foundation Server Express 可以在 `http://aka.ms/TFS2012Express` 获取。Express 版本包含但不限于核心开发功能：

- 版本控制

- 工作项跟踪

- 构建自动化
