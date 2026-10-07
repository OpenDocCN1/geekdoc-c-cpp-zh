
# 第三部分：K2 blackpearl 流程规划与设计要点

一个无需大量开发工作即可实现业务流程自动化的平台。即使结合了 SharePoint Designer 2007 或 Visual Studio，你所创建的流也无法直接复用，且无法提供企业所需的额外功能，例如报告之外的、动态任务分配、任务重定向和委托。再次，你可以实现这些，但意味着需要更多的开发工作。此外，在 SharePoint Designer 或 Visual Studio 中构建工作流还缺少安全性和管理功能，但你可以通过更多的开发工作来实现。终而言之，工作流（WF）需要大量的开发工作才能达到企业就绪状态。而通过 K2 blackpearl，额外的企业级功能已经就绪，你大部分的流程开发都是以拖放、视觉化和声明式的方式完成的。如果你必须进入代码层，你将在 K2 画布之前看到你的工作流计划，并根据需要对它们进行修改、插入和删除。

在本章和下一章中，我们将讨论 K2 blackpearl 的功能，但就涉及 SharePoint 集成而言，许多功能在 K2 blackpoint 中同样可用，K2 blackpoint 是 K2 blackpearl 相关功能的廉价版本。由于它是基于 K2 blackpoint 的，当需要出现时，K2 blackpoint 流程可以升级到 K2 blackpearl。阅读本章时请记住这一点。每当我们提到 K2 blackpearl 时，该功能在 K2 blackpoint 中也有。

本章涵盖了以下主题：

- SharePoint 的关键方面
- WSS 和 MOSS 之间的区别
- K2 集成如何工作
- K2/SharePoint 集成功能
- 用于 SharePoint 的 K2 Web Designer
- K2 Worklist Web part
- K2 SharePoint/SmartObject 集成
- 在用于 SharePoint 的 K2 Web Designer 中创建工作流
- K2 blackpearl 用的场景

# SharePoint 概述

出于本章和下一章的目的，我们将从高层次介绍一些基本功能。这并不是为了提供 SharePoint 功能的全景，而是为了介绍一些关键概念，帮助你将 K2 集成功能置于环境中。

# 站点与站点集 (Sites and Site Collections)

SharePoint 世界中最高级别的对象是 Web 应用（Web application）。Web 应用、Internet 信息服务（IIS）网站和 SharePoint 内容数据库之间存在一一对应的关系。次高级别的对象是站点集（site collection）。它顾如其名——一个站点的集合。这些可以是顶层门户、单个团队站点、项目工作空间、记录中心或发布站点，仅举几例。从技术上讲，当你创建一个新的站点集时，你实际上并没有创建站点，而是在放置站点的容器。

# 第 12 章：使用 SharePoint

站点集是 SharePoint 中一个非常有用的构造结构，它允许一组站点被视为单个实体。例如，备份站点集可以简单地备份和恢复一组相关的站点。如果你需要，也可以备份单个站点。

站点集内部的站点之间存在层级关系，这意味着单个顶层门户可能有许多不同的站点，而其中每个站点都可能有自己的额外的子站点，这种站点层级关系可以持续下去。通常情况下，在顶层，你应该将 SharePoint 的站点数量限制在 125 个。对于站点集中的站点总数，尝试将其限制在 2000 个站点。无论出于什么原因，2000 是 SharePoint 中的一个魔数字，因为你正在一个地方启动 2000 个项目——即站点集、列表和库中的，或者列表或库中的项目——你可能会遇到一些性能问题。SharePoint 的扩展性非常好，很多时候你会发现自己可以轻松地超过这些限制，但在规划 SharePoint 站点集时，请记住你的精力。一个经验法是，如果你按照应用程序拆分站点，那么是有保障的。或者按照受控站点（作为公司门户结构）和非受控站点（用于协作）进行拆分。或者按地区或子公司拆分。请记住，如果没有像 K2 之类的工具，跨站点集边界共享数据是不容易的。关于此的更多信息，请参阅 TechNet 上的“规划软件边界”主题（http://technet.microsoft.com/en-us/library/cc262787.aspx）。

站点集内部的站点也可以共享信息，因为内容类型、导航和安全性通常是从父级继承的。在创建新站点时，你可以选择不继承父级属性。这非常有用，例如在构建部门站点时，但层级关系将保留在站点集内部。权限的继承至少延伸到列表或库中的单个项目（包括文件夹）。就像管理 NTFS 文件系统上的权限一样，你应该尝试在尽可能高的级别上管理权限（靠近驱动器上的第一个文件夹，或站点集中的第一个站点），并使用组而不是单个用户。但像 NTFS 一样，SharePoint 允许你在需要时在项目级别上进行控制。如果你发现难以管理，可以随时将权限恢复为从父级继承。

# 内容类型与站点列

内容类型（Content types）贯穿于整个 中，用于创建文档和列表项、更新内容的属性，并根据这些属性搜索和定位信息。你根据公司的核心内容将内容类型做得越精细，你的 SharePoint 实现就越有用。请记住，内容类型是在站点集层级共享的（但子内容类型也可以被限定在站点），如果你有多个站点集，你可能不想多次创建相同的内容类型。

# 第三部分：K2 blackpearl 流程规划与设计要点

与内容类型相关的概念是站点列（size column），它可以被认为是内容类型的垂直轴。它允许在列表和库中基于属性的方式管理数据，这在某些时候是有用的，但在大多数实现中起次要作用。多个内容类型可以关联到单个列表或库，与之前的版本不同，不同类型的文档可以存储在同一个库中但保留其元数据。

# 列表与库 (Lists and Libraries)

从 SharePoint 用户的角度来看，列表和库是 SharePoint 中的主要工作区域。列表跟踪信息，而库是存放文档的地方。在底层它们是同一个东西，只是显示方式不同：项目被添加到列表，文件被添加到库。每个都可以根据跟踪的数据类型拥有多个属性，基本上文档是一个关联了类型的列表项。

在之前的 SharePoint 版本中，引入内容类型概念之前，为文档或列表项跟踪数据的唯一方法是将它们作为列添加到库本身中。在 WSS 3.0 和 MOSS 中你仍然这样做，但根据你的信息架构使用内容类型要更具扩展性且有用。然而，如果你已经在环境中让 SharePoint 运行，这可能需要一些先期规划或 SharePoint 重构。

## 第 12 章：使用 SharePoint

### 关于 SharePoint 工作流（Workflow）？

开箱即用的功能提供了工作流模板，用于为列表和文档库实现简单的工作流。你可以使用 Microsoft SharePoint Designer 2007 构建自定义工作流，以自动化同一个 SharePoint 站点中的操作。

Microsoft SharePoint 不包含供浏览器直接使用的工作流设计和创建工具，它开箱即用的仅包含少量工作流模板（在 WSS 和 MOSS 中用于收集反馈和收集签名等的模板）。这些模板对于某些操作很有用，但无法通过 Microsoft SharePoint Designer 2007 真正真正的自定义。

当你想要开发一种可在不同环境中复用的、**定制的且复杂的**工作流时，你必须使用 Visual Studio。虽然可以使用 Visual Studio 开发新的工作流活动甚至开发用于 SharePoint 的工作流模板，但这需要专门的 Windows Workflow Foundation (WF) 技术技能，这会增加项目的成本和完成时间，根据你的开发人员技能和资源，有时时间甚至会增加数倍。

通过 K2 提供的额外功能，流程所有者可以在不需要开发人员帮助的情况下实现其高级的企业级工作流场景。当他们需要帮助时，可以轻松共享他们的工作。有关共享工作的更多信息，请参阅第 14 章。有关将表单与 K2 流程集成更多信息，请参阅第 11 章。

SharePoint 和 K2 black 都基于 WF 调度运行。但两者都需要计划来运行。换句话说，客户端或服务器上的应用程序需要托管框架以运行 WF 调度。对于 SharePoint 的开箱即用方式，是 SharePoint 本。对于 K2 blackpearl（以及对 K2 而言），是 K2 服务器托管了框架和调度。这从可扩展性、维护和隔离的角度来看特别重要，而且从跨站点访问 SharePoint 数据以及封装可能跨越多个 SharePoint 站点集合的单个工作流活动的技术角度来看也同样重要。这以及平台的所有其他功能共同使 K2 blackpearl 提升到了企业级工作流平台的高度，并且由于 K2 blackpearl 声明式地使用 WF 调度作为基础，将 WF 开发技能转移到 K2 blackpearl 是非常简单的。

### WSS 和 MOSS 之间有什么区别？

SharePoint 实际上是两个产品：Microsoft SharePoint Services 3.0 (WSS) 和 Microsoft Office SharePoint Server (MOSS) 2007，它们的区别通常不为人知、被低估且最容易误解。

WSS 是免费的入门级 Web 解决方案，允许信息共享和协作服务。MOSS 扩展了 WSS 提供的功能和服务，为 WSS 提供的协作基础带来了企业级就绪的功能集。

WSS 提供站点置备和内容管理，包括文档存储和文档管理功能（如元数据、版本控制、签入/签出、移动设备支持和回收站），以及警报、博客和维基（wiki）等其他协作功能。WSS 还包含了许多不同站点的定义，包括团队站点（Team Site）、文档工作空间（Document Workspace）、空白站点（Blank Site）、博客、Wiki 和会议空间（Meeting Workspaces）。

MOSS 标准包含以下功能：

- Internet 门户和 Web 内容管理。此功能部分源于已弃的 Microsoft Content Management Server 2002 产品并集成到 MOSS 中。
- 企业门户功能，带有内容设计和导航的工具，如站点目录 (Site Directory)、目标用户 (Target Audiences)、我的站点 (My Sites) 和社交网络 (Social Networking)。
- 企业搜索工具，通过强大且完全可自定义的搜索引擎实现。
- MOSS 的其他功能包括 RSS 馈、站点目录、站点管理器、受众定位以及额外的模板和 Web 端口。

MOSS 中有很多功能被称为“企业级功能”，因为它们包含在企业级访问许可中：

- InfoPath 表单服务 (IPFS)：允许用户在 Web 浏览器中显示 Microsoft InfoPath 2007 表单。
- Excel 计算服务 (ECS)：允许用户将 Excel 工作簿发布到 SharePoint 站点，并在专用服务器上执行计算密集型操作。一项名为 Excel Access 的功能可以在 Web 浏览器中显示电子表格。
- 业务数据目录 (BDC)：允许用户将 SharePoint 与外部数据库和 Web 服务集成，以添加业务 (LOB) 信息。部分 BDC 组件用于浏览业务数据，MOSS 能够结合标准 SharePoint 信息一起返回这些信息。
- 业务智能 (BI)：允许用户创建仪表板和报告。

| 功能 | WSS (3.0) | MOSS (2007) |
| :--- | :--- | :--- |
| 免费的入门级 Web 解决方案 | 企业级就绪的功能集 |
| 站点置备 | 包含 | 包含 |
| 内容管理 | 包含 | 包含 |
| 文档存储 | 包含 | 包含 |
| 元数据、版本控制 | 包含 | 包含 |
| 签入/签出 | 包含 | 包含 |
| 移动设备支持 | 包含 | 包含 |
| 回收站 | 包含 | 包含 |
| 警报、博客、维基 | 包含 | 包含 |
| 团队站点、博客等 | 包含 | 包含 |
| Internet 门户 | 否 | 包含 |
| 企业门户功能 | 否 | 包含 |
| 企业搜索工具 | 否 | 包含 |
| InfoPath 表单服务 (IPFS) | 否 | 包含 |
| Excel 计算服务 (ECS) | 否 | 包含 |
| 业务数据目录 (BDC) | 否 | 包含 |
| 业务智能 (BI) | 否 | 包含 |

## 第三部分：K2 blackpearl 流程规划与设计核心

### K2 集成如何工作

当安装并配置 K2 集成点时，SharePoint 中央管理中会出现新的“K2 for SharePoint”选项卡，如图 12-1 所示。该页面作为 SharePoint 节点部署，与大多数 K2 集成功能的部署方式相同。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_476_0.png)

图 12-1

通过此页面，你可以管理站点集合的 K2 集成功能。内容站点只是包含 SharePoint 站点的站点集合（例如门户、团队站点、会议工作空间等），它与中央管理和共享服务提供者的站点不同。请注意，无法向站点集合中的特定站点部署 K2 集成功能。你可以在站点集合上单独关闭某些功能，但这将影响整个站点集合的功能。

你可能会问：“那么 K2 集成功能提供了什么？”以下是完整列表：

- K2 SmartObject 集成：允许将 SharePoint 数据封装在 SmartObject 中，并如图 12-2 所示，发布 Update K2 SmartObject 服务定义项。
- K2 站点管理集成：在站点设置页面上添加管理链接。
- K2 工作流集成 ASP.NET 页面内容类型：为 SharePoint 添加 ASP.NET 实例化和任务表单，用于 SharePoint 工作流集成流程。
- K2 Web 设计器集成：添加 K2 Web Designer 链接（如图 12-3 所示）以及用于 SharePoint 的 K2 Web Designer 设计画布。有关如何使用针对 SharePoint 的 K2 Web Designer 的更多信息，请参阅第 14 章。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_477_0.png)

图 12-2

![](img/20dd98d522a8a8d52ab6ce563d548ca5_477_1.png)

图 12-3

当将 K2 SharePoint 工作流集成进程部署到 SharePoint 站点时，它将作为功能出现在“站点集合功能”（Site collection features）页面以及“K2 工作流集成”页面中，该页面可以在“站点设置”（Site Settings）的“站点集合管理”（Site Collection Administration）中找到。站点集合功能中还显示了其他 K2 功能，但请不要禁用这些功能，而应使用 K2 工作流集成页面来管理工作流。以标准方式管理进程是一项良好的做法，以便于管理，特别是当 K2 工作流列表不断增长时。在“站点管理”（Site Administration）部分，你可以管理 K2 集成的 SharePoint 事件。这种集成允许在 SharePoint 列表或库中添加、更新或删除项目时启动进程。站点设置页面中的额外链接允许你根据需要管理工作流和功能。

441

# 第三部分：K2 blackpearl 进程规划与设计核心

K2 工作列表（Worklist）作为一种解决方案而非功能存在，显示在 SharePoint 中央管理（SharePoint Central Administration）的“解决方案管理”（Solution Management）页面上。点击“操作”（Operations）选项卡，然后点击操作页面“全局配置”（Global Configuration）部分中的“解决方案管理”链接进入此页面。该解决方案允许你将 K2 Web 工作列表（Web Worklist）部署到任何 SharePoint 站点集合，甚至是存有“我的站点”（My Sites）的站点，以便用户可以在他们的个人我的站点中使用 K2 工作列表。

与 SharePoint 协作的 K2 功能通过托管在安装 K2 Workspace 的 IIS 服务器上的 Web 服务与 K2 服务器进行通信。在 `RuntimeServices` 文件夹下，特别有两个 Web 服务用于 SharePoint 场景。第一个是 `SharePointService`，允许 K2 功能在 SharePoint 和 K2 服务器之间执行集成。例如，K2 集成工作流会在 K2 工作列表以及 SharePoint 任务列表中维护任务。有关任务的信息会被写入 SharePoint Web 服务。提供集成是为了让 SharePoint 用户无需前往其他位置查看他们的任务，这与管理开箱的 SharePoint 工作流任务是一致的。然而，你可以使用 Workspace 中的 K2 工作列表、K2 Web 工作列表（在 SharePoint 中）或 SharePoint 任务列表来管理任务。

与 SharePoint 协作时，其他起作用的服务还包括 InfoPath 和 OpenInfoPath。第一个服务允许 InfoPath 表单（无论是基于客户端还是基于浏览器的）与 K2 服务器通信，以检索可用数据、SmartObject 数据并提交任务表单等。第二个服务允许打开 InfoPath。

关于如何与 InfoPath 表单配合（工作）的更多信息，请参阅第 11 章。

中央管理中 K2 for SharePoint 页面的剩余部分允许你为 SmartObject 数据创建 BDC 定义，该部分将在第 13 章中介绍。

# 使用 K2 的 SharePoint 功能

让我们更仔细地查看 K2 SharePoint 集成功能以及如何使用它们。这些 K2 功能的管理将不再超出已提到的范围。。其他功能，如浏览器内工作流设计器、工作列表部分以及 SmartObjects 集成将在此处详细介绍。

介绍 SharePoint K2 Web 设计器功能的最佳方法是执行一个简单的进程。你可以尝试在你自己的已启用 K2 Web 设计器的 SharePoint 站点上进行，或者跟随本节操作。之后，你将能够通过观察其实际运行发现此工具是多么强大。

# 关于审批流程

示例场景是一个用于创建产品和服务手册的假设审批流程。

这是一个虚构的审批流程，用于创建产品和服务手册。

有关任务的信息会被写入 SharePoint Web 服务。提供集成是为了让 SharePoint 用户无需前往其他位置查看他们的任务，这与管理开箱的 SharePoint 工作流任务是一致的。然而，你可以使用 Workspace 中的 K2 工作列表、K2 Web 工作列表（在 SharePoint 中）或 SharePoint 任务列表来管理任务。

这是一个虚构的审批流程，用于创建产品和服务手册。

## 第三部分：K2 blackpearl 流程规划与设计核心

在设计画布中，你将再次看到一条从“已批准”（Approved）活动引出的新行和空白框。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_482_0.png)

要添加电子邮件通知功能：

- 1. 从侧边栏将“邮件向导”（Mail Wizard）拖到“通知”（Notify）区域。向导活动（Wizard Activity）对话框将要求您指定一个名称（在我们的场景中为为“营销警报”）和一个可选的描述。
- 2. 点击“下一步”（Next）开始为电子邮件消息构建模板。
- 3. 从对象浏览器（Object Browser）将“进程电子邮件”（Process Email）对象拖到“发件人”（From）字段以定义发送者。
- 4. 在“收件人”（To）字段中输入接收者的电子邮件地址（您可以使用任何电子邮件地址，甚至是如 marketing@denallix.com 的邮件列表）以及可选的主题（Subject）。
- 5. 现在您可以编写消息正文，交替使用固定文本和从对象浏览器拖入消息正文的可选动态元素（如图 12-8 所示）。完成电子邮件后，点击“下一步”以定义进一步的流程选项，或点击“完成”（Finish）以结束向导。

图 12-7

## 第 12 章：使用 SharePoint

![](img/20dd98d522a8a8d52ab6ce563d548ca5_483_0.png)

为了处理该流程，您需要定义如果建议的资产被拒绝时会发生什么。根据初始分析，应通过电子邮件通知发起者。

- 1. 从侧边栏将“发送邮件”（Send Mail）向导拖到“已拒绝”（Declined）区域，并重复之前的操作以创建消息。
- 2. 使用市场部门的电子邮件地址作为发件人，从对象浏览器中将“进程发起者电子邮件”（Process Originator Email）对象拖到“收件人”（To）中，然后通过具有描述性的主题来完成消息，让接收者能够轻松理解资产已被拒绝。
- 3. 您还可以向消息添加有用的动态元素，例如文档标题或其 URL，以便于识别。这在提交大量资产时特别有用。通过对象浏览器，您可以找到多个标识文档或其作者的元素，这些元素与文档库中的元数据是相同的。
- 4. 点击“下一步”定义进一步的选项，或点击“完成”结束向导。

## 第三部分：K2 blackpearl 流程规划与设计核心

工作流的最后一步是定义由谁来审批资产：

- 1. 注意“营销审批”（Marketing Approval）模块旁边的感叹号。点击该图标访问“目标”（Destinations）窗口，并定义将审批资产的目标用户。
- 2. 点击“添加”（Add）搜索用户。
- 3. 如果您想将他们添加到侧边栏的“收藏”（Favorites）列表中以便将来更快地执行类似操作，请选择“将用户添加到收藏”（Add users to Favorites）（如图 12-9 所示）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_484_0.png)

图 12-9

- 4. 点击侧边栏顶部的“保存”（Save）保存流程，如图 12-10 所示。
- 5. 点击侧边栏顶部的“部署”（Deploy）使流程在 SharePoint 库中可用并可执行。

## 第 12 章：使用 SharePoint

![](img/20dd98d522a8a8d52ab6ce563d548ca5_485_0.png)

在流程部署期间，K2 Web 设计器构建流程向导会检查工作流是否完成，并就问题或遗漏向您发出警告。您应该记住，基于 SharePoint 的框架要求执行流程的站点中至少包含一个“任务列表”（Tasks List）以及一个“K2 工作流历史列表”（K2 Workflow History list）。两者都是必须的。

## 第三部分：K2 blackpearl 流程规划与设计核心

工作流的最后一步是定义由谁来审批资产：

- 1. 注意“营销审批”模块旁边的感叹号。点击该图标访问“目标”（Destinations）窗口，并定义将审批资产的目标用户。
- 2. 点击“添加”（Add）搜索用户。
- 3. 如果您想将他们添加到侧边栏的“收藏”（Favorites）列表中以便将来更快地执行类似操作，请选择“将用户添加到收藏”（Add users to Favorites）（如图 12-9 所示）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_484_0.png)

图 12-9

- 4. 点击侧边栏顶部的“保存”（Save）保存流程，如图 12-10 所示。
- 5. 点击侧边栏顶部的“部署”（Deploy）使流程在 SharePoint 库中可用并可执行。

## 第 12 章：使用 SharePoint

![](img/20dd98d522a8a8d52ab6ce563d548ca5_485_0.png)

在流程部署期间，K2 Web 设计器构建流程向导会检查工作流是否完成，并就问题或遗漏向您发出警告。您应该记住，基于 SharePoint 的框架要求执行流程的站点中至少包含一个“任务列表”（Tasks List）以及一个“K2 工作流历史列表”（K2 Workflow History list）。两者都是必须的。

## 手动启动工作流

在设计工作流时，我们指定如何启动。

为了手动执行与列表或库关联的工作流，从项目或库选择“工作流”上下文菜单（如图 12-11 所示）。请注意，如果与关联的工作流是自动启动的（例如，在创建运行期间指定的），则该菜单不会出现。在 SharePoint 库项目中可以找到它。

## 第三部分：K2 blackpearl 流程规划与设计核心

![](img/20dd98d522a8a8d52ab6ce56d548ca5_486_0.png)

## 启动新工作流

“工作流”页面是一个标准的 SharePoint 页面，允许您通过它启动新实例。如图 12-12 所示，您可以执行以下操作：

- 创建与列表或库关联的新工作流。
- 查看当前工作流的状态。
- 检查哪些工作流正在运行。

![](img/20dd98d522a8a8d52ab6ce56d548ca5_486_1.png)

图 12-12

## 第 12 章：使用 SharePoint

在选择要启动的工作流后，您可以设置特定的工作流选项。例如，在运行期间可以指定目标用户，这在 SharePoint 库中可见。在启动工作流后，请记住您可以通过 SharePoint 文档查看工作流状态。

## 超 K2 Web Designer for SharePoint

K2 与 SharePoint 的集成不仅限于 K2 Web Designer for SharePoint。许多其他 K2 设计器允许 SharePoint 集成，包括 Visual Studio 中的 K2 设计、Microsoft Vision 2007 K2 设计以及即将发布的 K2 Studio。这些设计器共享：

- 流程向导
  - InfoPath 集成
  - SharePoint 集成
- SharePoint 事件
- 客户端事件
- SharePoint 工作流集成
- InfoPath 事件
- 管理事件
- SharePoint 站点和工作区
  - SharePoint 列表和库
  - SharePoint 用户管理
- 内容管理事件
  - SharePoint 列表
  - SharePoint 文档

## 第三部分：K2 blackpearl 流程规划与设计核心

- SharePoint 记录管理
- SharePoint 搜索
- SharePoint 发布

## 使用 K2 List Web Part

提高 K2 与 SharePoint 可用性的有效方法之一是在 SharePoint 页面上使用 K2 List Web Part。这允许用户以更简单直观的方式访问任务任务列表。见图 12-13。

请记住，K2 List 在 K2 Workspace 中同样可用，在那里您可以找到用于该流程的扩展控件。

![](img/20dd98d522a8a8d52ab6ce56d548ca5_488_0.png)

## 部署 K2 List Web Part

安装 K2 List Web Part 的方法与任何 SharePoint 解决方案相同：

1. 访问 SharePoint 中心管理：所有程序 > Microsoft Office Server > SharePoint 3.0 中心管理。
2. 点击“操作”（Operations）选项卡。
3. 在操作页面，点击“解决方案管理”（Solution Management）链接。如果 k2worklistwebpart 解决方案的状态已经是“已部署”（Deployed），则您无需执行任何其他操作。
4. 如果状态显示为“未部署”（Not Deployed），点击解决方案名称然后点击“部署解决方案”（Deploy Solution）。点击“确定”确认您的操作。请注意，您必须拥有 SharePoint 服务器的管理员权限才能执行此操作。

## 第 12 章：与 SharePoint 工作

## 在页面上插入 K2 Worklist Web Part

K2 Worklist Web Part 与任何 SharePoint Web Part一样。它可以被添加到支持 Web Parts 的页面任何部分，而 SharePoint 站点中的几乎每个页面都支持此项。要向页面添加 K2 Worklist Web part（如果您拥有必要的权限）：

- 1. 点击“Site Actions”（站点操作）并选择“Edit Page”（编辑页面）以进入页面布局。
- 2. 在页面布局中选择您想要添加 K2 Worklist Web part 的 Web Part Zone（部件区域），然后点击“Add Web Part”（添加 部件）按钮打开 K2 Web Parts 窗口。
- 3. 点击加号 (+) 展开“All Web Parts”（所有部件）组。
- 4. 滚动查看可用部件的列表，在“Miscellaneous”（杂项）组中选择 K2 Worklist Web part（提示：寻找绿色图标的唯一部件）。点击“Add”（添加）将 K2 Worklist Web part 添加到页面。参见图 12-14。
- 5. 点击 Site Actions 菜单下的“Exit Edit Mode”（退出编辑模式，图中未显示）保存页面的修改。
- 6. 如果您正在使用 SharePoint 发布功能，点击页面顶部编辑工具栏上的“Publish”（发布）。请注意，此操作可能与可选的审批流程相关。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_489_0.png)

图 12-14

一旦您向页面添加了 K2 Worklist Web part，就必须配置它与 K2 服务器的连接。

- 7. 要配置 Web part 的连接，请点击 K2 Worklist Web part 右角的向下箭头，然后修改“Shared Web Part”（共享部件）。
- 8. 在部件 任务窗格的“Main Task List”（主任务列表）中检查您的 K2 环境设置，如图 12-15 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_490_0.png)

K2 Worklist 部分的配置与配置 K2 Workspace 中可用的工作列表的方式非常相似。在部件 任务窗格的“Task List Columns”（任务列表列）部分中选择您的首选设置。如果您在“Set of Columns”（列集）下拉菜单中选择“Custom”（自定义），您可以选择要显示的列以及用于在 K2 Worklist 部分中显示信息的标签，如图 12-16 所示。

您还可以配置“Group By”（分组依据）选项，它允许您管理任务的分组——简化用户对当前任务的视图。如果您认为部件将显示很长的任务列表，请启用“Paging”（分页）选项。启用分页后，部件每次只会加载少数几个元素，从而提高性能。

- 9. 完成配置后，点击“OK”确认您的设置。
- 10. 使用编辑工具栏上的“Publish”（发布）按钮再次发布您的页面（如有必要）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_491_0.png)

## 使用 K2 SmartObjects 功能

我们讨论的第三也是最后一个 K2 集成功能可能是最强大的。在探索此功能之前，请确保您理解 SmartObjects。回顾第 7 章，该章涵盖了 SmartObjects 是什么、Service Object（服务对象）与 SmartObject 的关系、如何使用它们，以及如何用它们扩展 K2 平台。

在 SharePoint 的上下文中，站点内包含的几乎任何用户定义数据都可以封装在 SmartObject 中。如果您想思考如何在过程中使用 SmartObjects（特别是在一个没有 SharePoint 集成的过程中），您将开始理解在新场景中使用此项的可能。除了过程之外，您还可以想象一个完全没有元素的应用程序（例如基于 SmartObject 数据的网站），并意识到这一功能——被封装并暴露的 SharePoint 数据——可以成为您组织内随处使用之数据的存储库。如果您尚未以这种方式使用 SharePoint，可以考虑在有限的场景下尝试。用户发现 SharePoint 非常易于使用，以至于他们想将数据存储在那里，但在过去重用数据很困难。有了 SmartObject 集成，这变得不再困难了。

您不仅可以通过过程或通过 `SourceCode.SmartObjects.client` API 从 SharePoint 获取数据，还可以使用 .NET Data Provider for K2 SmartObjects。这是一个标准的 ADO.NET 组件，可以将其添加到任何 .NET 项目中。该提供程序允许您查询和更新由任何 SmartObject 封装的数据，包括通过 SharePoint Service Object 暴露的数据。

安装 SharePointSmartObject 集成功能允许 SharePoint Service Object 为其部署的 SharePoint 站点创建实例。可以通过以下方式验证 K2 SmartObjects 功能的正确安装：

- 访问 SharePoint Central Administration（中心管理）站点（开始 ⇨ 所有程序 ⇨ Microsoft Server ⇨ SharePoint 3.0 Central Administration）。
- 点击“K2 for SharePoint”选项卡，然后点击“K2 SmartObject Integration”。
- 选择您想要验证的 Site Collection（站点集合）。如果您想验证要验证的站点集合。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_492_0.png)

## 阐释一些场景

您有许多方法可以使用 K2 blackpearl。接下来的章节描述了一些可以实现的示例，以帮助您开始。使用 SharePoint 管理业务数据的一个示例是使用 SharePoint 列表。该列表包含了组织中每个客户的项目经理信息。即使您的客户数据存储在数据库中（因为项目管理职责经常变化），您也不想在 LOB 系统中更新该字段。将其分开保留在 SharePoint 中允许项目经理定期查看和更新信息。通过 SmartObject 功能，您可以构建包含客户信息的 SmartObject，并将其暴露给组织中的任何 .NET 应用程序。这将是一个简单的实现，但您可能需要将 LOB 数据库的多个字段整合到 SmartObject 中。您将开发自定义服务，或者根据 LOB 系统使用内置服务来与其通信。

另一个示例是使用 SharePoint 管理法律记录。尽管 SharePoint 有原生的“Send To”（发送到）功能，但它要求用户发送单个文件。使用 K2 blackpearl，您可以搜索匹配当前状态的文件并将整批文档发送到 Records Center（记录中心）。您还可以以自动方式创建和删除记录，从而及时响应法律或审计请求。

使用 SharePoint 的内容管理功能，您可以设置一个过程，聚合来自 LOB 系统（包括 SharePoint）的内容，并将信息发布到发布页面。这可以按计划设置、作为操作触发过程的一部分，或者在 SharePoint 列表或库中新建项目时触发。您还可以使用基于过程的发布将页面移动到不同的环境（例如从测试到生产环境），并在过程中更新外部连接。

与 InfoPath 2007 的深度集成以及发布可在业务中运行表单的选项，意味着启动和执行过程不需要每次都创建自定义表单。InfoPath 表和 InfoPath 服务提供的灵活性意味着，具有一定技术能力的业务用户可以管理自己的过程。

## 站点创建与维护

SharePoint 没有任何原生过程可以根据某些标准创建站点。使用 K2 blackpearl，您可以实现此过程，并在站点超出预期使用期限后将其退役。

# 第三部分：K2 blackpearl 流程规划与设计核心

通过 SharePointSmartObject 的方法，可以从单个复合 SmartObject 中从 SharePoint 和 LOB（线性业务）系统同时返回数据，这使得来自 SharePoint 和另一个 LOB 系统的数据可以通过单一接口进行暴露、管理和更新。

## SharePoint 集成的运营优势

我们已经涵盖了 K2 blackpearl 与 SharePoint 之间集成实现的一些场景，但这列表绝非详尽。K2 blackpearl 与 SharePoint 集成还带来了其他可能显而易见的运营优势。以下章节将描述这些主要的优势。

## 流程版本控制

默认情况下，当你使用 SharePoint Designer 或 Visual Studio 部署新的 SharePoint 工作流时，并不会像开发者对程序集版本那样干扰流程版本控制。在 K2 blackpearl 中，每次部署流程时，版本都会更新，每个新实例将使用新版本。然而，已经运行的实例将继续使用旧版本的流程，直到它们完成。

## 流程管理

随着即将发布的流程门户（Process Portals），你可以管理安全性、查看运行中的实例、排除错误，甚至实时获取 SharePoint 中流程的图形化表示。这一系列 Web 部（Web parts）允许你通过熟悉的 SharePoint 接口进行通常在 K2 Workspace 中找到的所有基于流程的管理工作。

## 改进工作流历史报告

尽管 SharePoint 提供了工作流历史日志（通常使用标准的工作流历史列表），但在使用 Excel 透视表查看时它们并不实用。K2 添加了两个与报告相关的关键功能改进了这一过程。首先，可以为部署到 K2 服务器的每个流程（包括与 SharePoint 集成的流程）创建工作流报告 SmartObjects。其次，K2 Workspace 中的 K2 报告设计器是一个创建标准 RDL 兼容报告的丰富环境，因此 K2、SQL Reporting Services 和 SharePoint 之间的集成变得简单得多。而且通过将这些报告导出到 SQL Reporting Services 的选项，结合 SharePoint 和 SQL Reporting 的集成，可以在 SharePoint 内部提供企业级报告，用于跟踪组织中的每个流程。这与流程门户类似，流程门户也允许根据业务所需的任何自定义，以便根据实时信息做出更好的业务决策并优化流程。

## 更好的任务可用性与管理

使用 K2 Weblist 部，可以将 SharePoint 作为用户查看其任务列表的中心位置。这与 SharePoint 通常用于分配任务的简单任务相比是一个重大的改进。虽然这些任务列表可能分布在 SharePoint 场的各个站点中，但 K2 Worklist 将所有 K2 blackpearl 任务整合在一个处，为用户提供更多信息和上下文，并允许点击几次即可批量处理相关任务，极大地提高了用户生产力。

## LOB 数据集成

尽管微软正在改进业务数据目录（Business Data Catalog），但要从 LOB 系统向 SharePoint 集成数据并不容易。使用 K2 SmartObjects，创建 BDC 定义不需要任何代码或对长 XML 文件的操作即可在 SharePoint 中显示这些信息。

### 总结

SharePoint 是微软提供的一个强大平台，提供了许多协作所需的功能。当与 K2 blackpearl 结合时，SharePoint 成为一个强大的流程驱动型应用程序平台。通过 K2 blackpearl，SharePoint 可以成为或替换许多其他企业平台。

下一章将重点利用 WSS 和 MOSS 中均可用的 K2 SharePoint 集成功能，包括：

- 每个 SharePoint 向导的概述，包括它们可以用于哪些业务场景场景
- 记录中心（Records Center）
- Web 内容管理（发布）功能
- 业务数据目录（Business Data Catalog）

我们还将涵盖上述功能的的一些场景，以及 SharePoint 搜索结果向导。K2 blackpearl 和 K2 blackpoint 包含的其他 SharePoint 向导在 K2 帮助文件中有详尽介绍，因此在确定向导页面上的特定选项可以使用时，那里应该是你的首选参考。

### 注意事项

- 1. "SharePoint Joins the Microsoft Pantheon" 作者 Scott Becker. Redmond Channel Partner, 2008年6月1日。http://rcpmag.com/columns/article.aspx?editorialid=2640
- 2. 有关 SharePoint 许可的信息，请访问这些网站：
www.microsoft.com/sharepoint/howtobuy/default.mspx
https://partner.microsoft.com/US/licensing/licensing/40048861

# 13
使用 Microsoft Office SharePoint Server

Igor Macori
Mike Talley

在上一章中，我们查看了通过浏览器与 SharePoint 集成的 K2.blackpearl 特性，例如管理页面、用于 SharePoint 的 K2 Web Designer、K2 Worklist Web 部以及 SmartObject 集成。在本章中，我们将注意力转向 K2 设计器，通过其他 K2 设计器中可用的 SharePoint 向导在设计时进行集成，包括你可以用它们做什么，以及关于充分利用 K2 SharePoint 流程和事件向导的一些提示。我们还将更仔细地考虑由 K2 集成实现的企业场景。本章涵盖了你可以用于为 SharePoint 创建高级工作流的 K2.blackpearl 特性，包括：

- 流程与 SharePoint 事件集成
- 控制 SharePoint 内容
- 管理 SharePoint
- 企业级场景：Web 内容管理
- 企业级场景：使用搜索结果
- 企业级场景：使用记录中心创建内容管理规则
- 企业级场景：与业务应用程序和外部数据库交互

# 第三部分：K2 blackpearl 流程规划与设计核心

## 使用 SharePoint 向导

让我们退一步查看所有与 SharePoint 相关的向导。在第9章中我们介绍了所有的向导，但在这里我们将查看所有与 SharePoint 相关的向导，并提供关于如何使用它们的一些建议。有两个向导，即 SharePoint 管理和 SharePoint 发布，它们依赖于 MOSS。这些包含在 K2 中的向导包括：

- SharePoint 工作流集成向导
- SharePoint 事件向导

## SharePoint 工作流集成向导

此向导允许你将 K2 工作流与 SharePoint 列表或库、发布库以及内容类型关联，如图 13-1 所示。结合此向导，SharePoint 事件向导用于用用户可以的操作来填充工作流任务——如果用户没有权限，则 K2 服务器将不提供该操作。

[图 13-1: SharePoint 工作流集成向导（文中未提供图像）]

## 第13章：使用 Microsoft Office SharePoint Server

将工作流与列表或库关联，允许你在向列表或库中添加项时自动启动工作流，你还拥有允许用户手动启动工作流的选项。如果你没有指定手动选项，该工作流将出现在可以手动启动的工作流列表中。这些选项不是互斥的，因此你可以有一个既可以自动启动也可以手动启动的工作流。

将工作流与内容类型关联是一种特别强大的机制，可以确保当在 SharePoint 站点集中使用内容类型时，工作流会自动启动或手动实例化。随着你的 SharePoint 实现列表和库的增长，将工作流与内容类型关联比针对特定的文档库更容易让工作流实现进行扩展。将工作流与文档库关联是 1 对1 的关系，而将工作流与内容类型关联则允许你对站点中任何位置的内容具有一对多的关系。

## SharePoint 事件向导

此向导允许你根据列表和库中的事件来实例化工作流，无论是结构性变化还是列表或库中的项级更改。此向导中的第一个示例（如图 13-2 所示）允许在 SharePoint 列表或库中添加、删除或更新列时实例化工作流。第二个选项允许你根据多个不同的事件实例化工作流，例如在添加项时、向项附加文档时、签入项时或当文件被转换时。对于每个事件级别——在列表或库的结构级别或项级级别——都可以根据指定列表中的一个或多个事件实例化工作流。

[图 13-2: SharePoint 事件向导（文中未提供图像）]

# 第三部分：K2 blackpearl 过程规划与设计要素

当你选择与列表或库进行集成时，可用的事件包括：

- 字段添加（Field Added）：当向列表/库中添加字段时触发。
- 字段删除（Field Deleted）：当从列表/库中删除字段时触发。
- 字段更新（Field Updated）：当列表/库中的字段被更新时触发。

当你与列表或库事件集成时，可用的事件包括：

- 项目添加（Item Added）：当向列表/库中添加项目时触发。
- 附件添加（Attachment Added）：当向列表中的列表项添加附件时触发。
- 附件删除（Item Deleted）：当从库中的列表项中删除附件时触发。
- 项目签入（Item Checked-In）：当项目签入到库中时触发。
- 项目签出（Item Checked-Out）：当项目从库中签出时触发。
- 项目删除（Item Deleted）：当从列表/库中删除项目时触发。
- 文件转换（File Converted）：当列表/库中的文件被转换时触发。
- 项目移动（Item Moved）：当项目从列表/库中移动时触发。
- 项目取消签出（Item Unchecked-Out）：当项目从库中取消签出时触发（更改被丢弃）。
- 项目更新（Item Updated）：当列表/库中的项目被更新时触发。

下一步是元数据映射和 Folio 页面，在其中你可以将有关列表的元数据存储在 K2 字段中，以便后续在工作流中使用。如果你想将工作流与多个列表和库关联，请在向导页面上选择高级模式（Advanced Mode）。

记住，SharePoint 事件主要适用于自动化工作流过程，而不适用于由用户手动启动或在进程开始前需要某种用户交互的过程。如果你需要用户交互，请使用 SharePoint 事件集成过程集成向导。当你需要在 SharePoint 列表或库的结构发生变化，或者项目被添加、删除或更改时总是需要启动任务时，这特别有用。尽管 SharePoint 事件集成的使用不仅限于管理员审核和警报，但它对于这类场景特别有用，而且这些场景代表了创建简单的工作流。然而，由于潜在的性能负面影响，K2 SharePoint 事件集成支持任何异步工作流，这意味着某些类型的工作流（如审批）与 SharePoint 事件集成配合得并不好，因为在管理员分配工作流任务之前，用户操作已经发生。换句话说，没有机制来捕获事件并将其设置为审批。工作流在事件完成后开始。

一旦部署，你可以使用设置（Settings）页面中“站点管理”（Site Administration）部分的“K2 事件集成”链接来查看和管理 K2 SharePoint 集成事件。你还可以通过同一页面上“站点集合”（Site Collection）部分的“K2 工作流集成”链接来管理所有 K2 SharePoint 集成工作流。这两者在图 13-3 中均有。

# 第 13 章：使用 Microsoft Office SharePoint Server

![](img/20dd98d522a8a8d52ab6ce563d548ca5_501_0.png)

图 13-3

# 事件向导

我们现在关注 K2 blackpearl 包含的其余 SharePoint 向导。这些向导允许你对 SharePoint 实体（Entities）执行特定操作。每个 K2 活动中都可以添加一个或多个事件。

我们已经讨论过 SharePoint 工作流集成客户端事件向导，因此我们不再涵盖它。其余的向导没有关联的用户界面（UI）；相反，它们是工具，允许你根据正在创建的过程在 SharePoint 中执行某些操作，无论是移动、复制还是删除文档；在站点中创建站点或列表；或者为某人访问特定的 SharePoint 列表分配权限。这些只是你可以使用 K2 blackpearl 自动化的少数示例。这些选项中的许多在 K2 blackpearl 中也是可用的。我们将这些向导分为两类——管理（Administration）和内容管理（Content Management）。

# 第三部分：K2 blackpearl 过程规划与设计要素

# 管理事件向导

此类向导允许你自动化通常与站点设计师、站点所有者和站点集合管理员相关的 SharePoint 任务。对于那些已经在环境中部署了如野火般扩展的 SharePoint 实现，并正在寻找控制和管理 SharePoint 方法的人来说，这三个向导的力量是显而易见的：

- SharePoint 站点和工作区事件向导（SharePoint Sites and Workspaces Event Wizard）
- SharePoint 列表和库事件向导（SharePoint Lists and Libraries Event Wizard）
- SharePoint 用户管理事件向导（SharePoint User Management Event Wizard）

SharePoint 在这方面功能并不多，而 K2 blackpearl 带来了自动化站点权限的能力。

# SharePoint 站点和工作区事件向导

此向导允许你创建、更新和删除站点，如图 13-4 所示。注意，在创建新站点、列表或项目时，你还有一个在 SharePoint 实体上断开继承的选项。这取决于你创建的类型。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_502_0.png)

图 13-4

# 第 13 章：使用 Microsoft Office SharePoint Server

使用此向导，你可以创建、更新和删除列表，如图 13-5 所示。这取决于你创建的类型。

# SharePoint 列表和库事件向导

此向导允许你创建、更新和删除库，如图 13-5 所示。注意，在创建新站点、列表或项目时，你还有一个在 SharePoint 实体上断开继承的选项。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_503_0.png)

图 13-5

当你执行此向导的操作时，可以创建、更新和删除库。箱箱列表包括公告、日历、问题跟踪、任务和链接，以及文档、表、Wiki 页面和数据连接。请记住，你使用此向导创建列表和库，但要在列表内部创建项目，你需要使用项目事件向导。要在文档库中创建文档，请使用文档事件向导。

# 第三部分：K2 blackpearl 过程规划与设计要素

# SharePoint 用户管理向导

此类向导允许你自动化通常是管理性的 SharePoint 任务。该向导是所有 K2 向导中最难理解的。其复杂部分是因为 SharePoint 的安全性非常复杂。有权限（rights），即用户可以做的基本操作，被称为权限级别（permission levels），这是你在管理权限时初眼看到的。这些权限可以分配给单个用户或用户组，并且通常可以在站点集合的任何一点进行管理，从顶层到单个项目。SharePoint 用户管理向导同样复杂，甚至更复杂。

13-6 显示了 SharePoint 用户管理向导的第一页。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_504_0.png)

13-6

通过此工具，你可以执行任何 SharePoint 管理任务，例如：

- 创建或删除 SharePoint 组。
- 给 SharePoint 用户或组访问站点、列表、文件夹、列表项或另一个组的权限，以便嵌套组。
- 从站点、列表、文件夹或项目中移除 SharePoint 用户或组。
- 重置站点、列表、文件夹或项目的权限继承。当你设置权限时，也可以在当前配置的任何层级断开继承。

# 第 13 章：使用 Microsoft Office SharePoint Server

组。这里是向导的第二个实例所在。该向导非常智能，当你在第一次点击“First”（First）时，它会自动再次启动。它还会预选要执行的操作，因为它获取了你之前在 SharePoint 管理事件向导（SharePoint Management Event Wizard）中所操作的内容，这使得第二次使用向导变得更加容易。如果你在使用此向导时感到困惑，请思考你将如何在 SharePoint UI 中手动配置用户、组和权限，然后重新查看该向导。

有关 SharePoint 权限和安全的更多信息，请参阅 Microsoft Office Online上的“控制访问 SharePoint 站点和内容的介绍”（http://office.microsoft.com/en-us/sharepointserver/HA10255321033.aspx）。

## 内容管理事件向导

内容管理事件向导允许你对 SharePoint 中的内容执行操作，无论这些信息存储在列表、文档、发布页还是记录中心（Records Center）中。我们在此节中包含了搜索结果向导，因为在自动化内容管理任务时，它比 SharePoint 管理任务更常用。

## SharePoint 列表项事件向导

此向导允许你在 SharePoint 列表或库中创建、更新、复制和删除列表项，如图 13-7 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_505_0.png)

图 13-7

469

## 第三部分：K2 blackpearl 规划与设计核心

你会在“更新列表项”（Update List Items）下看到两个选项，它们也适用于“复制列表项”和“删除列表项”。理解这些选项很重要，因为它们可以极大增强过程的威力和动态特性：

- **SharePoint 列表项（SharePoint List Item）：** 将将其 SharePoint 列表库中的特定事件。
- **来自内容字段（From Content Field）：** 这是体现力量和灵活的地方，因为你可以根据存储在过程中的数据更新项目。这允许你在 K2 数据字段中收集信息，或将其作为 SmartObject 查询的结果，然后使用它来更新、复制或删除列表项。

## 普通模式与高级模式

现在是时候提到普通模式（Regular Mode）和高级模式（Advanced Mode）如何改变你在向导中可以的操作了。对于 SharePoint 向导来说，这尤为重要。本章中所示的每个向导都是普通模式，因为普通模式下的某些选项更容易理解。

SharePoint 向导的高级模式通常允许你多次执行你正在使用向导执行的操作——移动对象或创建公告。这适用于有意义的向导。对于“站点和工作区向导”（Sites and Workspaces Wizard），高级模式不允许你创建多个站点，但它允许你指定新站点的权限是否继承，以及新站点是否出现在常规 SharePoint 导航中。

处理多个项目听起来可能很杂乱，但实际上非常强大且易于配置。在 SharePoint 中，很多时候你需要处理一组项目，而不仅仅是单个列表条目或单个文档。使用高级模式下的 SharePoint 向导允许你处理 SharePoint 中的一组项目，并对每个每个项目单独执行你指定的的操作。例如，对于 SharePoint 列表项，你可以指定创建任何数量的项目。对于简单操作使用普通模式，但如果你需要使用高级模式创建多个列表项。如果你正在从 K2 字段创建项目，请使用工具栏上的“添加”拆分按钮（Add split button）来指定项目的来源，因为默认情况下，向导假设你想指定实际的列表项详情，而不是基于 K2 字段。

## SharePoint 文档事件向导

此向导如图 13-8 所示，允许你对 SharePoint 文档执行许多不同的操作，例如：

- 复制
- 移动
- 获取或更新元数据
- 签入（Check In）
- 签出（Check Out）

470

## 第 13 章：使用 Microsoft Office SharePoint Server

- 撤销签出（Undo Check Out）
- 删除

![](img/20dd98d522a8a8d52ab6ce563d548ca5_507_0.png)

与列表项向导一样，你可以直接对存储在 SharePoint 中的文档执行许多这些操作，或者对存储在文件系统或 K2 字段中的文档执行操作。K2 字段提供了更大的威力和活性，因为它允许你指定存储在 K2 字段或 SmartObject 中的文档。

SharePoint 文档事件向导允许你执行通过 UI 可以进行的任何 SharePoint 文档操作，包括签入、签出和撤销文档签出。此外，你还可以检索文档的元数据或属性，并将其存储在 K2 字段中供以后使用。

## SharePoint 记录管理事件向导

此向导允许你在 SharePoint 记录中心创建和删除记录，并对记录放置保留（hold）或移除记录的保留，如图 13-9 所示。它还允许你创建和删除记录保留。保留（hold）是 SharePoint 记录的容器，可能可能适用于诉讼、审计或调查。保留会覆盖记录的信息管理策略，并防止记录过期或被删除。这确保了记录的内容受到保护，并可以由法律人员审查，以符合法律法规或正在进行的法律事务。

有关记录和记录保留的更多信息，请参阅 Microsoft Office Online 上的“记录中心站点介绍”（Introduction to the Records Center site）（http://office.microsoft.com/en-us/sharepointserver/HA10255321033.aspx）和“创建保留”（Create a hold）（http://office.microsoft.com/en-us/sharepointserver/HA10255321033.aspx）。

508

## 第三部分：K2 blackpearl 规划与设计核心

![](img/20dd98d522a8a8d52ab6ce563d548ca5_508_0.png)

图 13-9

## SharePoint 搜索向导

此向导允许你跨列表和库进行搜索，如图 13-10 所示。在同类型的库之间搜索时，你还可以指定搜索范围。默认范围是当前站点，但你可以扩展范围以包含子站点或整个站点集。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_508_1.png)

图 13-10

472

## 第 13 章：使用 Microsoft Office SharePoint Server

使用 SharePoint 搜索结果，你可以在筛选页面指定布尔逻辑。这些标准可以基于过程中的动态数据或 SmartObject。你还可以根据硬编码的数量限制结果数量。但此向导最强大的方面是它允许将结果存储在内容字段中。想想，如果搜索结果不能用于任何地方，那么搜索结果有什么用？将结果存储在内容字段中允许你以后使用，例如将这些文档复制到其他位置、在电子邮件通知中提供结果列表或将这些项目文档放入记录中心。将搜索结果与其他 SharePoint 事件向导结合，允许你自动化某些涉及站点、子站点或整个站点集的复杂任务。

注意，搜索结果向导使用的是所有 SharePoint 版本中包含的协作应用程序标记语言（CAML）搜索技术，而不是标准的 WSS 或 MOSS 技术。使用 CAML 允许你持续比较 SharePoint 元数据，这是其他技术难以实现的。但是，某些情况下你可能想使用 WSS 或 MOSS 搜索引擎。为此，请调用 WSS 搜索（http://<servername>/_vti_bin/ssearch.asmx）或 MOSS 搜索（http://<servername>/_vti_bin/search.asmx）Web 服务。有关这些 Web 服务的更多信息，请参阅 MSDN上的“企业查询 Web 服务概述”（Enterprise Search Query Web Service Overview）（http://mdn.microsoft.com/en-us/library/ms54175.aspx）。

## SharePoint 发布事件向导

此向导允许你对 SharePoint 发布功能执行多个操作，包括：

- 创建、复制、移动、删除和签入发布页。
- 获取和更新发布内容。
- 创建和更新可重用内容。

向导的第一页如图 13-11 所示，允许你选择对 SharePoint 发布功能执行的操作。

# 第三部分：K2 blackpearl 流程规划与设计要点

![](img/20dd98d522a8a8d52ab6ce563d548ca5_510_0.png)

图 13-11

如果您不熟悉这些 SharePoint 功能可以实现的操作，请参阅 Microsoft Office Online 上的“Web 内容管理简介”（http://office.microsoft.com/en-us/sharepointeserver/HA102406301033.aspx），该文档为您提供了关于如何使用这些功能的极佳概述。

通过 SharePoint 发布事件向导（SharePoint Publishing Event Wizard），您可以自动化 Web 内容的发布，利用 K2 平台的强大和灵活性为开箱即用的 SharePoint 功能添加更复杂的工作流能力。您还可以利用 K2 流程数据和 SmartObject（智能对象）查询为这些页面创建更具动态的内容。

关于使用 SharePoint 发布事件向导的基于场景的示例包含在章节后部分的“使用 Web 内容管理”部分中，但请记住，当您使用此向导创建发布页面时，您还可以将其存储在 K2 字段中以便以后重用。

## 使用 K2 SharePoint 集成处理企业场景

本节涵盖了 K2 SharePoint 集成的以下方面，包括它们在企业中可能使用的场景：

- Web 内容管理
- 搜索结果
- 记录中心 (Records Center)
- 业务数据目录 (BDC)

## 第 13 章：使用 Microsoft Office SharePoint 服务器

BDC 在 K2 Designer 中没有向导，因为它是 K2 blackpearl 的 SharePoint 运行时集成点。与其说是内容管理，不如说说是内容分发，您可以通过 BDC 将存储在 SmartObjects 中的信息分发到 SharePoint。我们将讨论一个监控场景来说明此功能的强大之处。

## 使用 Web 内容管理

SharePoint 为 Web 内容管理提供了广泛的功能，允许用户创建内网和互联网站点，并包含供内容发布者和编辑者的工具。开箱即用的，MOSS（Microsoft SharePoint Server）包含一个发布工作流，编辑可以使用它来控制和批准发布到发布站点的内容。K2 ballpark 通过设置自定义的发布工作流来扩展此及整个发布功能，以构建高度清晰的流程，这些流程更接近企业的审核和审批需求。

## SharePoint 发布功能

MOSS 包含两个不同的站点模板，可以自动激活 SharePoint 发布功能，但通过激活发布功能，也可以启用任何 SharePoint 站点（包括团队站点）。要启用这些功能，请通过“操作 (Actions)”菜单进入“设置 (Settings)”选项卡，然后点击“站点功能 (Site Features)”。在此页面上，如图 13 所示，点击“激活 (Activate)”按钮来启用 SharePoint 服务器发布功能。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_511_0.png)

图 13-12

启用发布功能后，整个站点将自动更新，Web 内容管理功能将可以使用。例如，“创建页面 (Create Page)”命令现在可以在“站点 (Sites)”菜单可用。使用它创建新的 Web 页面，以指定页面布局 (Layouts) 并使用 Web 内容管理工具管理内容。您还会注意到更新页面包含了文档签入、一个可选的审批步骤以及与标准 SharePoint 页面编辑过程不同的发布步骤。

## 示例发布场景：发布新闻稿

假设您想创建一个发布新新闻稿的流程。您希望允许编辑人员选择合适的页面布局，并在发布之前更正审核和审批规则。

1. 在适用于 Visual Studio 的 K2 Designer 中启动一个新的 K2 工作流项目，并将 Visual Studio 工具箱中的“SharePoint 发布事件向导”拖到 K2 设计画布上。
2. 勾选“在高级模式下运行 (Run in Advanced Mode)”复选框，然后点击“下一步”。
3. 在“事件 (Event)”字段中为事件输入名称，选择操作“创建发布页面 (Create Publishing Page)”，然后点击“下一步”。
4. 输入将发布新闻稿的 URL，并标记可选参数。
5. 在高级模式下，向导允许您设置发布计划，以便在特定的特定时间发布内容。
   点击“下一步”后，浏览页面布局并选择一个您偏好的布局，或者根据需要 插入一个自定义的布局（如图 13 所示）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_512_0.png)

6. 向导将要求您输入发布元数据。
7. 点击“完成 (Finish)”完成事件。

# 第 13 章：使用 Microsoft Office SharePoint Server

在向导的此阶段，您可以添加其他搜索过滤器并将它们组合起来以构建查询。您可以在添加搜索过滤器的同一页面上，指定搜索过滤子句的布尔逻辑和操作顺序。

- 6. 点击“下一步”将带您进入向导的最后页（参见图 13-15），在该页面中您可以创建一个用于存储搜索结果的内容字段。您将在稍后的过程中使用该字段对搜索结果进行一些有趣的操作。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_515_0.png)

图 13-15

在此页面上，您还需要指定要存储的项目类型，例如文档、列表项、记录或发布页面，以及您想要保留的最大结果数。如果您在整个站点集合中进行搜索，限制搜索结果是一个好主意。在这种情况下，我们正在为每个销售报价（Sales Offers）文档库创建一个工作流，限制结果数量并不是问题。事实上，限制结果可能会导致漏掉已接受的报价（Accepted offers），因此您必须意识到您如何使用搜索结果以及您使用此向导的场景类型，以便实现结果。

此时，搜索结果存储在 SalesOffers 内容字段中。在搜索事件之后向活动中添加 SharePoint 文档事件，将允许您将存储的文档复制到中央位置进行汇总。文档汇总取决于您环境的设置，可以是销售经理的工工过程，但如果您有自动执行此步骤的能力，则可以是一个自动化过程。SharePoint 文档转换可能适用于此步骤，将每个 Word 文档转换为 Web 页面以便稍后更新。或者您可以为每个文档创建可重用的内容，然后将它们合并到单个页面上。这两种选项都可以通过 SharePoint 发布向导实现。

# 第三部分：K2 blackpearl 过程规划与设计核心

从那里开始，您只需创建一个事件，将 Word 或合并后的 Web 页面复制到每个销售站点，以处理该信息的多个副本。

使用 SharePoint 搜索向导的其他选项还包括将记录发送到记录中心（Records Center），其实现方式与搜索场景类似，但不是使用存储文档的内容字段复制到中央站点，而是将文档发送到记录中心，我们将在下一节介绍它。

# 使用记录中心

MOSS 的可用功能之一是名为“记录中心”的站点模板，¹ 这是一个记录存储库，您可以利用它来定义 SharePoint 内容的路由、保留和处置的记录。

SharePoint 允许您在内网门户中实现多个一个记录中心，这让您能够灵活地定义更多的库，用于不同的存档和审计标准，以回答与文档存储和保留相关的法律和程序法请求。

> 注意，有一个特殊的 Records URL 字段应该在环境库（Environment Library）中配置，以便其预填充记录并在整个过程中保持一致使用。有关使用环境库的更多信息，请参见第 10 章和第 15 章。

# 使用记录和锁定

记录可以由 SharePoint 中的任何信息表示。通常，像 Word 文档或 Excel 表格是成为记录的良好候选。记录也可以是电子邮件或即时消息器聊天记录。任何可以支持业务过程中操作和决策的信息元素都可以被视为记录。

记录中心的功能之一被称为“锁定”（hold）。锁定是记录中心内正常存档规则的例外。在覆盖到期策略时，锁定是非常实用的工具，例如在合规审计情况下可能需要这样做。

记录中心使用了 SharePoint 内容类型，这是最重要的功能之一。内容类型允许您以一致的方式为特定内容定义描述性元数据，同时还可以为组织的信息生命周期管理创建工作流、模板和策略。您可以使用内容类型以一致的方式指定信息类型及其适当的路由和存储策略。

# 企业场景：销售部门费用控制

假设您的公司办公室定义了控制公司销售部门费用的新规则。与这些成本相关的每条信息都将被存档，以备可能的审计。

一种方法可能是让 SharePoint 开发人员创建一个新功能，该功能可以根据特定规则分类文档，并将它们移动到目前要求存储的库中。类似的解决方案可以由深谙 SharePoint API 并具有在 Visual Studio 中开发 SharePoint 解决方案经验的人员开发。

480

# 第 13 章：使用 Microsoft Office SharePoint Server

然而，通过 K2 blackpearl，您无需特定的开发知识即可轻松地实现这些目标。使用 SharePoint 搜索向导的两个选项为：

- 将文档发送到记录中心
- 管理锁定

将文档发送到记录中心：

1. 将 SharePoint 记录管理事件拖入工作流设计中。
   事件的第一页将描述所有可能的操作，您可以选择“高级模式”（Advanced Mode）。

2. 如果您从特定文档开始创建记录，请选择操作“创建记录”（Create Record）然后点击“下一步”。
   第二页允许您指定 SharePoint URL、文档名称和文件（File），如图 13-16 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_517_0.png)

图 13-16

3. 找到想要发送到记录中心的元素后，点击“下一步”。在出现的页面上，您可以选择将文档保存到“内容”（Content）中的操作，如图 13-17 所示。

4. 点击“完成”结束向导。

# 第三部分：K2 blackpearl 过程规划与设计核心

![](img/20dd98d522a8a8d52ab6ce563d548ca5_518_0.png)

创建锁定：

1. 将另一个 记录管理事件拖入工作流设计，放置在上一个事件下方。
2. 在指定事件名称（Event Name）后，选择操作“创建锁定”（Create Hold）然后点击“下一步”。
3. 指定源目录（Source Directory），定义 SharePoint URL。锁定 ID 将包含标题（Title）、描述（Description）和管理员（Managed By）字段，如图 13-18 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_518_1.png)

482

# 第 13 章：使用 Microsoft Office SharePoint Server

您还可以使用之前描述的通过创建的活动。您可以构建一个活动来搜索特定状态的文档，例如已批准的费用报告。然后您可以在工作流中定义并执行一个操作，将批准的文档保存到记录中心。

与其他向导一样，在高级模式下运行 SharePoint 记录管理向导允许您指定多个文档、内容字段或两者的组合，以创建记录、添加锁定、取消锁定或删除。锁定也是如此，通过在高级模式下运行向导，可以在同一个事件中创建多个锁定。

# 使用业务数据库（BDC）智能对象数据

MOSS 企业功能之一是业务数据库（BDC）。它可以从 K2 blackpearl 和 SAP 等应用程序以及 SQL 和 Oracle 等数据源将外部业务线（LOB）信息导入到 SharePoint。

一旦您在 SharePoint 共享服务提供程序中定义了 BDC 应用并创建了相关的 XML 定义文件，就可以导入您的数据源，如图 13-19 所示。

BDC 应用通常在 SharePoint 用于：

- 通过业务数据 Web 部件查看业务数据
- 通过业务数据字段在列表和库中集成业务数据
- 通过 MOSS 搜索引擎和业务数据搜索内容源搜索业务数据

483

# 第三部分：K2 blackpearl 过程规划与设计要素

任何 K2 blackpearl SmartObject 都可以通过 BDC（业务数据目录）显示数据。通过 BDC 显示此类信息的威力体现在两个方面：首先，它会自动为你创建 XML 应用定义，这可能是一个复杂的过程。其次，可能更为强大的是，数据被封装在 SmartObjects 中并代表：

- 关于过程的数据（例如用于报告的数据）
- 在过程中被消耗或生成的数据，包括 LOB（业务系统）数据
- 通过 SmartObjects 呈现给其他非过程应用程序的数据

当你通过 BDC 集成 SmartObject 数据时，你创建的解决方案允许 SmartObject 中包含的任何数据都能在 SharePoint 中呈现，而无需进行自定义开发工作。有关 SmartObjects 的更多信息，请参阅第 7 章。

K2 blackpearl提供的内置服务对象允许你从以下数据源导入数据：

- 活动目录 (Active Directory)
- SharePoint
- Salesforce.com
- K2 blackpearl（过程报告）

请参阅第 7 章开发自定义 SmartObject 服务，以通过 SmartObjects 封装来自其他源的数据。参阅第 23 章了解有关使用 K2 connect 从 SAP 呈现数据的更多信息。

# 数据与 BDC

必须意识到，BDC 可以从许多不同的源呈现业务数据，它是一个单向机制。本质上，这些数据是只读的。要修改数据，你必须返回 LOB 系统进行更改或更新。虽然 SmartObjects 允许从 LOB 系统查询和更新数据，但当这些数据通过 BDC 呈现时，无法在 SharePoint 中修改，而必须直接使用 SmartObject 进行修改。这是 BDC 的局限性。

# 将 SmartObjects 与 BDC 集成

SmartObjects 与 BDC 之间的集成始于使用 K2 Designer for Visual Studio 创建一个或多个 SmartObjects。工作流报告 SmartObjects 可以为过程创建。部署 SmartObject 或工作流项目是第一步，一旦部署，通过 SharePoint 中央管理站点中的 K2 for SharePoint 选项卡创建 BDC 应用就是第二步。

# 第 13 章：使用 Microsoft Office SharePoint Server

一旦 SmartObject 数据与 MOSS 搜索引擎集成，该引擎就会检索该数据并将其返回到标准的搜索结果页或搜索 Web。请记住，SmartObject 数据不应暴露给所有使用 MOSS 的人员，也不应通过 BDC 呈现。

若干 SmartObjects 使用数据创建有关过程性能的报告，例如工作流报告 SmartObjects 捕获的实例数量、平均时长和其他信息。这些数据可以轻松被 Business Data 部分使用，快速构建过程控制和监控界面，从而提供了与门户显示类似的信息。

Business Data 部分提供的其他优势之一是通过微应用程序执行数据查询。这允许你通过主/详细视图（Master/Detail view）链接并显示数据。这些 Web 部的渲染也可以使用 XSLT 修改和自定义进行，使用 SharePoint 中的工具面板、过程数据的自定义视图或任何由 SmartObjects 封装的数据，都可以实现高度定制化。

# 配置 K2 BDC 应用

要配置 K2 BDC 应用：

1. 打开 SmartObject 中央管理站点，点击 K2 for SharePoint 选项卡，如图 13-20 所示。

2. 在 Business Data Catalog Integration 中点击 `Create Application` 链接创建新的 SmartObject BDC 应用。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_521_0.png)

图 13-20

# 第三部分：K2 blackpearl 过程规划与设计要素

3. K2 BDC 应用页面允许你选择 SharePoint 共享服务（如果你的 SharePoint 农场中有多个）以及你希望使用的 SmartObject（SmartObjects 列表将帮助你理解这种集成有多强大）。

4. 选择 SmartObject 后，`Create K2 BDC application` 将显示用作 `Input Parameters` 元素的字段。你还可以与其他 SmartObjects 定义关联选项，将其包含在同一个 SmartObject BDC 应用中。

5. K2 BDC 应用页面的最后一个选项启用搜索爬虫（应用索引），允许你为 MOSS 搜索引擎配置设置。请仔细阅读警告，因为你可能希望在搜索结果中暴露敏感的 SmartObject 信息。

在创建 K2 BDC 应用页面后，你可以通过中央管理中的 K2 for SharePoint 使用 `Manage` 链接来修改其选项。`K2 Settings` 链接允许你设置 K2 服务器设置并检索与 SmartObjects 相关的信息。

还应配置 BDC 权限。记住，通过 BDC 应用访问 SmartObject 数据的用户需要每个应用程序的授权。此设置位于共享服务管理站点的 BDC 管理页面上。在 K2 blackpearl 帮助文件中提供了创建应用程序和设置此项的详细说明。

# 企业场景：在 SharePoint 中使用客户信息

你可以想象出几个与通过 SmartObjects 获取并通过使用 BDC 集成的数据相关的实际示例。在我们的场景中，我们将在 SharePoint 中呈现位于自定义客户关系管理 (CRM) 系统中的客户数据。

我们的目标是让 SmartObject “链接”到业务数据。

1. SharePoint 中央管理站点中的 K2 for SharePoint 页面允许你创建一个链接到 Customers SmartObject 的 K2 BDC 应用。

2. 创建 SmartObject BDC 应用后，可以在定义用户访问和定义的共享服务管理站点中的 Business Data Catalogs Applications 部分找到它，如图 13-21 所示。

# 第 13 章：使用 Microsoft Office SharePoint Server

![](img/20dd98d522a8a8d52ab6ce563d548ca5_523_0.png)

图 13-21

一旦创建了应用并设置了授权，用户就可以可以使用述的 Business Data Web Parts和其他功能来访问 SmartObject 数据。

测试 BDC 应用：

1. 向门户页面添加一个 Business Data List 部分。
2. 点击 `Open` 面板链接选择 SmartObject BDC 应用。
3. 点击工具面板底部的 `OK` 确认数据已显示。
4. 点击 `Edit Mode` 模式完成操作。
5. 打开页面后，使用 Business Data List 部分中的相关工具栏启动数据查询。

你还可以配置搜索内容源（Search Content Source）来索引客户数据并使其通过 MOSS 搜索引擎可用。

# 第三部分：K2 blackpearl 过程规划与设计要素

基于客户信息的元数据也可以作为列表和库的属性，这与向 SharePoint 列表或库添加自定义列非常相似。例如，你可以添加有关存储在文档库中的关联报价的数据。要执行此操作：

1. 浏览到库并从设置菜单中选择 `Create` 命令。
2. 使用 `Create Column` 页面选择列名，并选择 `Business Data` 作为列类型。
3. 在页面底部通过 `Additional Column Settings` 选择 BDC 实例，并找到你希望作为库列的字段。
4. 创建新字段后，向库中上传文档。

你会发现新字段（见图 13-22）可以像 SharePoint People Picker 一样进行查询；它允许你以相同的方式浏览和解析 SharePoint 点。Business Data 列允许你处理 LOB 数据（在这种情况下，数据来自 CRM 系统，通过 K2 SmartObject 和 BDC 最后进入 SharePoint）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_524_0.png)

# 第 13 章：使用 Microsoft Office SharePoint Server

新列还允许你创建不同的视图，根据客户名称对文档进行排序、过滤或分组。这不仅提供了显示的灵活性，还确保了客户名称在 SharePoint 和你的 CRM 系统中的显示保持一致。

## 将业务信息集成到 Microsoft Office 应用

SharePoint 与 Microsoft Office 系统应用程序之间的集成允许你在 Office 文档中使用通过 SmartObject BDC 应用程序检索的信息。要使用此功能，请访问文档信息面板，或在 Microsoft Word 2007 等应用程序中使用快速部件（参见图 13-23）。在这些地方结合数据，允许用户在应用程序中查看业务数据和其他 SharePoint 元数据，这在某些场景下特别有用。你还可以自定义文档信息面板，因为它们是呈现这些信息的实际 InfoForms。有关此的更多信息，请参见 MSDN 上的文档信息面板概述 (http://msdn.microsoft.com/en-us/library/ms55003.aspx)。

你还可以在任何潜在的工作流中使用封装了业务信息的新字段，而客户信息现在只是你库中的另一个列。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_525_0.png)

图 13-23

通过 BDC 在 SharePoint 中呈现 LOB（线性业务）信息的场景是无限的，使用集成可以实现过去需要大量时间和资源才能实现显示方式。有了 SmartObjects 和 SharePoint 的企业功能，这些场景变成了无代码解决方案，除非你创建了从 K2 到后端服务器的服务层。

> 有关 SmartObject 和 SAP 集成的更多信息，请分别参考第 7 章和第 23 章。

# 第三部分：K2 blackpearl 流程规划与设计要要

## 使用 InfoPath 表单

我们想要简要介绍的最后一个 MOSS 企业功能之一是 InfoPath 表单服务 (IPFS)。IPFS 允许将 InfoPath 模板转换并部署为 SharePoint 内部的网页。InfoPath 表单的深度介绍包含在第 11 章中，以及与 ASP.NET 表单相比使用 InfoPath 的优势。如果你正在使用 SharePoint，InfoPath 表单是设计自定义 UI 和列出流程可用操作最简单、方便的方法。

请注意，如果你没有 MOSS 企业功能，你仍然可以在 SharePoint 上使用 InfoPath 表单。但是，你无法将表单渲染为网页。K2 blackpearl 与 Microsoft Office Server 2007 集成，这是一个独立的 SKU，仅包含用于在浏览器中渲染 InfoPath 表单的 IPFS。由于此 SKU 是独立的，它无法像企业功能那样添加到 MOSS 中。

IPFS 带来的最大优势是不需要在每台电脑上安装 InfoPath 2007 即可填写 InfoPath 表单。InfoPath 2003 和 SharePoint Portal Server 有某些集成，而 InfoPath 2007 和 Moss 之间的集成通过 IPFS 变得更加强大，允许构建复杂工作流有更多可能性。K2 blackpearl 引入了多项重要功能，帮助你通过 InfoPath 表单添加用户界面，而其他的是基于浏览器或仅客户端的表单。这些功能包括：

- 每个表单多个视图多个视图：允许灵活复用同一个表单来启动和激活工作流，或在必要时使用多个表单

- 用户任务的动态操作查询：消除了操作更改时更新表单的需求

- SmartObject 集成：允许你将来自 SmartObjects 的数据添加到 InfoPath 表单，反过来允许更好的决策

- 自动部署、版本控制和源管理：允许你将 InfoPath 表单视为流程的一部分，而不必担心它将如何部署、版本化和在存储控制中签入

这些是在你的 SharePoint 工作流中使用 InfoPath 2007 表单的高级优势。有关使用它们的更多信息和一些注意事项，请参阅第 11 章。

### 总结

当你发掘了 SharePoint 丰富且强大的功能时，K2 blackpearl 为你提供了更多可能，允许你扩展并增加对 SharePoint 的投资。

如果你购买了企业级 CAL，你就可以在 K2 Designer for Visual Studio 和 K2 Designer for Visio 中使用每一个 SharePoint 相关的事件向导。这些工具允许你创建无代码解决方案来管理 SharePoint 站点、列表和库，并控制内容，这一切都通过可以提供即时且增加投资回报的流程来实现。

# 第 13 章：使用 Microsoft Office SharePoint Server

如果你刚开始实施 SharePoint 部署且以前从未使用过它，希望我们已经让你对 SharePoint 能为你的组织带来的收益有了一些认识，并提供了如何使用 K2 来增加这些收益的想法。如果你是 SharePoint 专家，我们希望已经为你在使用 SharePoint 解决方案时提供了一些新思路。

在下一章中，你将查看不同的 K2 Designer 以及它们如何用于协作流程设计。

### 注意事项

- 1. 有关 Microsoft Office SharePoint Server 2007 记录中心的更多详细信息，请访问网站 http://go.microsoft.com/fwlink/?LinkId=84739。

- 2. K2 通过特定的 Web 服务访问 SharePoint 记录中心信息，你可以通过 URL http://yourportal/Records/_vti_bin/officiafile.asmx 访问。重要：你应该检查 K2 blackpearl 服务账户是否有适当的权限访问它。

- 3. 通过 URL http://yourportal/Records/_vti_bin/officiafile.asmx 访问特定的 Web 服务访问 SharePoint 记录中心信息。重要：你应该检查 K2 blackpearl 服务账户是否有适当的权限访问它。

# 14

## K2 Designer 与协作流程设计

K2 平台通过改变流程设计的范式允许允许协作建模。本章将讨论各种 K2 Designer 以及它们如何协同工作。本章还将涵盖以下主题：

- 设计流程时涉及的角色

- K2 blackpearl 提供的 Designer，包括 K2 Designer for Visio、K2 Designer for SharePoint 和 K2 Designer for Visual Studio

- 协作流程

## 适合合适人的工具

人们参与应用程序和流程设计是常识。有趣的是可以参与的人员。K2 平台以声明的方式处理流程设计，这意味着流程定义独立于创建它的 Designer。这为不同类型的人提供了不同的设计体验。

# 第三部分：K2 blackpearl 流程规划与设计要素有些组织对构建和部署业务解决方案有相当严格的标准。无论你是强制 IT 负责所有的软件构建和更改，还是允许业务其他人员积极参与，K2 blackpearl 的设计都可以处理这些场景以及之间的任何情况，如图 14-1 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_530_0.png)

图 14-1
协作的光谱

由于流程设计人员可能具备多种技能，K2 流程 Designer 针对各种技术和非技术用户。例如，Microsoft Office Visio 2007 可供业务所有者绘制流程。在所有者视觉化描述流程后，业务分析师可以使用 Visio 添加额外的流程定义信息。一旦流程达到其技术能力的极限，可以将流程定义传递给开发人员使用 Visual Studio 完成流程。

K2 现在提供三种类型的流程 Designer，并计划了更多的设计画布。每个画布都针对特定类型的人员，如图 14-2 所示。

所有的 K2 设计画布都是可视化的，利用拖放和向导驱动的界面来引导设计者，而不需要显著的技术。无论使用哪种 Designer，都会自动创建 Microsoft .NET Framework 3.0 Windows Workflow Foundation 以及相关的 Microsoft .NET 代码，以实现互操作性和扩展性。

## 第 14 章：K2 设计器与协作流程设计

![](img/20dd98d522a8a8d52ab6ce563d548ca5_531_0.png)

图 14-2

从左到右，流程设计器从技术复杂型转向易于使用型：

- Visual Studio 的 K2 设计器适用于习惯在 Microsoft Visual Studio 2005 环境中工作的 IT 专业人士。
- Visio 的 K2 设计器可任何熟悉 Microsoft Visio 的人员使用，但通常由业务分析师使用。
- SharePoint 的 K2 Web 设计器适用于 SharePoint 2007 用户或高级用户，他们希望在 SharePoint 环境中设计和运行工作流。

我们将在后面的章节中详细讨论每个设计器，以及计划在 K2 blackpearl 后续版本中发布的设计器。在详细介绍设计界面之前，从一些定义开始是至关重要的。

## 了解你的角色

正如第 3 章所定义的那，有多个角色在 K2 自动化项目中发挥作用。当涉及到设计流程的任务时，我们将讨论三个关键角色或受众：

- 业务分析师
- 流程设计师
- 开发者

虽然 K2 项目中的其他角色也很重要，但这三个角色是真正坐下来并使用 K2 设计工具设计流程的人。

## 第三部分：K2 blackpearl 流程规划与设计核心要素

## 业务分析师

虽然业务分析师的主要工作之一是流程文档（包括业务需求、案例、表单设计和数据需求），但 K2 允许业务分析师在设计流程中也发挥关键作用。使用 Visio K2 设计器等工具，业务分析师可以根据项目设计阶段收集的需求，使用常用的业务模板绘制流程图。

## 流程设计师

流程设计师通常负责应用程序的设计。很多时候，流程设计师也可以兼任业务分析师，并使用 Visio K2 设计器等工具来开发业务流程。流程设计师不仅使用形状定义流程，还通过适当的 K2 向导连接这些形状以开发流程。对于不需要代码的简单流程，流程设计师可以快速构建并部署流程。对于更复杂的流程，流程设计师可以导出流程并发送给开发者进行增强。

## 开发者

开发者负责任何所需的自定义代码开发，以及将集成点到业务系统中。开发者将使用 Visual Studio K2 设计器等工具，根据流程设计师在 Visio K2 设计器等工具中设计的流程来纳入自定义代码。开发者还负责 SmartObjects（智能对象）的创建，因为该功能未包含在 Visio K2 设计器中。

与其他设计师共享流程

在开展业务自动化项目时，许多人将同时处理同一个项目。根据场景（例如之前提到的示例），业务流程所有者、业务分析师和开发者都可能参与 K2 流程的定义。K2 流程定义框架确保了无论使用什么设计画布进行建模，核心定义都是相同的。该框架将流程定义（即 K2 运行流程所需的逻辑和路由信息）与视图信息（活动、事件和线条的布局及视觉表示）抽象离开来。流程框架允许流程建模体验的每个参与者使用最符合其技能组的流程设计。同时，通过拥有通用的定义，参与者可以使用各种工具进行协作。

## 为什么这种方法有效

每个 K2 设计表面都使用相同的项目文件系统。所有设计器都采用 K2 API 来维护项目 (.csproj) 文件并创建支持的生成文件，无论机器上是否安装了 Visual Studio。每个设计画布中工作流集成的呈现可能不同，但构成工作流的核心部分无论设计环境如何都是相同的。通过这种方式，工作流的设计与工作流的可视化完全分离，这正是 K2 平台上可以进行协作设计的原因。

## 第 14 章：K2 设计器与协作流程设计

## 创建你的设计表面

尽管该主题超出了本书的范围，但你可以使用 `SourceCode.Workflow`、`SourceCode.Workflow.Design`、`SourceCode.Workflow.VisualDesigners`、`SourceCode.Workflow.WizardFramework` 和 `SourceCode.Workflow.Wizards` 程序集在自定义应用程序中集成相同的基于向导的可视化设计画布。有关这些程序集的更多信息，请参阅从 K2 客户和合作伙伴门户下载的 K2 black 开发者参考。

设计器之间的工作流构建和部署也是相同的。部署到 K2 服务器的 MSBuild 脚本和机制对于每个设计环境都是相同的，因为所有设计器都使用相同的 API。此外，Visual Studio K2 设计器和 Visio K2 设计器（K2 Studio 设计器，在编写时尚未发布）使用相同的向导，因此流程、活动和事件的配置在设计器之间是相同的。这允许跨设计器使用任何向导，使得业务用户使用 K2 Studio 或 Visio K2 设计器可以使用与使用 Visual Studio 的开发者相同的界面。

每个 K2 设计器都会创建相同的项目、文件夹和文件结构。是 K2 API 定义了这种结构，允许多个设计师灵活地处理 K2 项目。

此外，由于流程的可视化设计和流程文件的编写是分离的，视觉模型和流程定义之间可能会脱节。例如，在 Visio K2 设计器中，你可能会看到孤立的活动和事件。这些孤立项可能在 Visual Studio 中添加但未与流程关联。尽管它们在画布上没有视觉表示，但它们将按照流程定义中的表示被执行。

这好比建筑的蓝图。如果你取了房屋的蓝图，你会看到房间、入口、窗口等的布局。然而，你可能看不到电气或 HVAC 系统的细节。尽管它们在房屋蓝图中没有视觉化表示，但它们被定义在另一个层中，并在执行房屋建造期间（以及房屋的日常维护期间，例如空调启动时）被使用。

使用如 Visio K2 设计器之类的设计器，你可以用形状表示大型活动或人工交互，就像房屋中的房间一样。然后，使用如 Visual Studio K2 设计器之类的设计器，你可以为流程添加细节，就像 HVAC 系统一样。查看完全定义的流程时，技术细节可能不会出现在 Visio 页面上；它们表示在流程定义中。很多时候，流程赞助人或业务分析师对技术细节不，只想查看高层概览。

## 第三部分：K2 blackpearl 流程规划与设计核心要素

| 通过代码完全定义流程 |
| :--- |
| 由于视觉表示和流程文件的编写是独立的，你可以通过代码完全创建流程。你可以通过 K2 API 定义 .kpx，这可以在 Visual Studio 中打开或导入到 Visio。更多信息请参阅 K2 black 开发者参考。查看“流程 (Processes)”部分。 |

## 导出和导入能力

作为 K2 API 的一部分，流程定义可以从各种设计表面导出。这创建了必要的项目、文件夹和文件结构，其他设计师可以使用该流程设计。

然而，哪些设计师可以共享流程存在某些限制。以下列表显示了各种 K2 设计器的流程共享能力。

- Visual Studio K2 设计器保存：
    - Visio K2 设计器：可以打开并将孤立活动映射到新形状。
    - SharePoint Web 设计器：无法打开。
- 从 Visio K2 设计器保存：
    - Visual Studio K2 设计器：可以打开并继续设计，无需额外任务。
    - SharePoint Web 设计器：无法打开。
- 从 SharePoint Web 设计器保存：
    - Visual Studio K2 设计器：可以打开并继续设计；流程应作为新流程部署。
    - Visio K2 设计器：可以打开并将孤立活动映射到新形状；流程应作为新流程部署。

## 第14章：K2 设计器与协作流程设计

## 设计师选择

K2 提供了一种独特的建模体验，支持多个可切换的画布和工具。K2 将视图信息从流程定义中抽象出来，以确保无论使用何种画布或工具，核心定义都是相同的。其结果使得流程建模体验中的每个参与者（无论角色如何，例如：业务分析师、开发人员、流程所有者），都可以使用他们最熟悉的建模环境。接下来，我们将介绍撰本文时 K2 blackpearl 所具备的设计工具。

## 用于 Visio 的 K2 设计器

K2 Designer for Visio 是 Microsoft Office Visio 2007 的一个插件，它将 K2 Designer for Visual Studio 中提供的工具引入了 Visio 环境。通过使用图层模板（stencils），可以将事件和规则与 Visio 画布上的任何形状关联起来。这种关联不限于某一个活动或某一个阶段。例如，如果业务需求和现有图纸需要，可以将多个活动附加到单个形状上。这对于那些不是建模流程但需要用于构建和部署流程的图纸非常有用，例如平面图或网络架构图。

Microsoft Visio 帮助人们创建各种类型的专业图表。大多数此类程序依赖于用户的艺术技能来制作高级图表。但通过 Microsoft Office 2007，只需打开模板并在画布上绘制图标和模板即可，非常简单。许多公司已经拥有了 Visio，而且它通常已经部署给流程所有者的开发人员了。

Visual Studio 工具箱中显示的所有 K2 blackpearl 组件都可以插入到新的或现有的 Visio 图纸中。Visual Studio 中可用的相同向导也被用于在 Visio 中设计流程的特定部分，例如添加一个 SharePoint 文档事件以移动或复制存储在 SharePoint 站点上的文档。

K2 对象浏览器（显示环境库、流程和活动数据）以及工作流数据和用户浏览器（Workflow Data and User browsers）在 Visio 和 Visual Studio 中均可用。大多数在 Visual Studio 中构建的流程都可以 K2 Designer for Visio 进行构建；然而，Visio 中不支持自定义代码和流程调试。

通过使用 K2 Designer for Visio，可以在 Visio 环境中构建并部署流程。Visio 设计器利用了用户熟悉的工具集，并并扩展了 K2 工具，以便将图纸与流程建模轻松集成。现在，K2 Designer for Visio 可以获取这些图表并赋予其生命。图 14-3 显示了一个已连接到 K2 工作流的 Visio 图表示例。

## 第三部分：K2 blackpearl 流程规划与设计要点

![](img/20dd98d522a8a8d52ab6ce563d548ca5_536_0.png)

图 14-3

K2 信息存储在 Visio 图纸之上的另一个层。通过这种方式，原始图纸得以保留。你可以开启或关闭 K2 层的可见性，这样额外信息（绿色线条和 K2 图标）就不会混淆用户对原始 K2 层的操作。对于图 14-3 所示的简单图表，这不会引起问题。但对于复杂的图表，额外的 K2 层可能会导致混淆。

K2 Designer for Visio 还利用了易于使用的向导。这些向导在许多设计中都是相同的，包括 Visio 和 Visual Studio。通过使用通用的向导，可以在多个设计中利用 K2 平台的功能，同时允许最终用户在简单的基于 Visio 的体验中进行设计。

设计流程的人员可以在两种启用 Visio 图表流程的方法之间进行选择：按活动或按流程。设计师可以以即时（ad hoc）的方式自动化流程，选择形状并将这些形状绑定到事件。例如，设计师可能会打开一个事件型 Visio 2007 图表，然后通过选择形状、右键点击并通过向导配置事件（例如发送电子邮件或发布文档）来手动启用活动。或者，设计师可以创建一个新流程并启用整个表面，从而在用户首次将形状拖到设计表面上时，提示用户将形状绑定到事件或规则。

这里没有特定的“一对一”步骤限制。对于某些高级流程或遵循替代绘图方法（例如平面图）的流程来说，这种限制过于严格了。可以使用多个形状来定义不同的步骤、参与者和需要做出的决策。这些内容可以在 Visio 中组合在一起并被视为一个 K2 活动。然后，流程就可以开始为每个模板或一组模板分配工作流步骤。

## 目标读者

K2 Designer for Visio 旨在供业务分析师使用流程。然而，其设计体验足够健壮，开发人员也可以选择使用 Visio 对流程进行建模。

为了成功使用 K2 Designer for Visio，用户应该熟悉 Visio 概念（如使用形状、标签和线条），以及 K2 概念（如操作、结果、事件和规则）。

## 使用 K2 Designer for Visio

当 K2 Designer for Visio 安装在已安装了 Microsoft Office Visio 2007 的客户端机器上时，Visio 内部将出现一个新的 K2 工具栏。该工具栏如图 14-4 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_537_0.png)

图 14-4

从左到右，按钮包括：

- 启用/禁用工作流 (Enable/Disable Workflow)：允许 K2 集成
- 向形状添加工作流项 (Add Workflow Item to Shape)：将形状绑定到工作流
- 从形状移除工作流项 (Remove Workflow Item from Shape)：从工作流中移除形状
- 投放时添加工作流项 (Add Workflow Item to Drop)：在投放形状时配置工作流
- 切换工作流层 (Toggle Workflow Layers)：显示或隐藏 K2 层
- 切换工作流窗口 (Toggle Workflow Window)：打开 K2 设计器
- 导入 (Import)：导入现有工作流
- 导出 (Export)：导出设计的工作流
- 部署 (Deploy)：将设计的工作流部署到服务器
- 构建 (Build)：构建工作流
- 设置 (Settings)：更改 K2 设置

若要在 Microsoft Office Visio 2007 中创建 K2 集成流程，你必须先启用图表。通过启用 K2 集成，任何形状都可以绑定到工作流。绑定形状非常简单，只需鼠标点击几次即可。

## 第三部分：K2 blackpearl 流程规划与设计要点

当你右键点击一个形状并选择集成（Integration）项时，将显示可用的菜单项。例如，图 14-5 显示了一个已与 K2 工作流集成的图表。通过右键点击形状，你可以更改该形状的属性。连接到 K2 活动的形状将在形状旁边显示 K2 图标，如下所示。图标显示在 K2 层上，如果关闭此工作流层，图标和线条将被隐藏。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_538_0.png)

图 14-5

通过 Visio 图表，你可以通过将形状与新的工作流活动集成，从零构建 K2 流程。你可以将任何形状绑定到任何可用的 K2 向导。K2 Designer for Visio 将引导你通过一系列向导，将形状关联到活动。根据所选的事件，将显示额外的子向导，引导你完成配置事件的过程。这些事件与 Visual Studio 中显示的向导完全相同。

关于 K2 向导的更多细节，请参阅第 8 章。

一旦所有形状都与工作流事件关联，你就需要连接它们。通过使用集成菜单并配置线条来连接活动。这与在 Visual Studio 中连接有所不同，你可以拖放线条来连接活动。

## 导入

与其在 Visio 中从头构建流程，业务分析师还可以导入开发人员在 Visual Studio 中创建的现有流程，并将流程活动映射到形状。一旦流程被导入到 Visio，用户就可以将未绑定的活动映射到形状。

可以通过选择 K2 工具栏上的导入按钮将流程导入到 Visio。

# 第 14 章：K2 设计器与协作流程设计

## 导出

要从 Visio 导出流程，请点击 K2 工具栏上的“导出”按钮。导出后，可以将指定导出位置中的文件交给开发人员以扩展流程。导出到到的文件夹将包含一个完整的 K2 blackpearl 项目（.k2proj 文件）和流程（.kpx 文件），这些文件可以交给开发人员进行进一步的定制。该流程可以直接在 Visual Studio 中打开，由开发者进行修改并保存。

一旦开发者完成修改，业务分析师将检阅 Visio 图表并导入新的流程定义。任何绑定的活动和线条都将显示在 K2 层上。在 Visual Studio 中向流程定义中添加的任何活动将显示为未绑活动。这些新活动可以与 Visio 中的形状（Shape）集成以进行视觉表示。然而，即使没有绑定到 Visio 形状上，流程层和流程定义也能正确执行。只要流程定义是完整的，流程就能正常运行。

## 协作体验

Visio 中的流程可以在 K2 Designer for Visual Studio 中进行设计、修改、扩展，并导入到 Visio 中进行进一步的更改或调整。这使得 Visio 和 Visual Studio 用户能够在舒适且符合技能的环境中协作进行流程设计。

协作体验是双向的，这意味着流程定义可以在 Visio 或 Visual Studio 中构建，并来回共享。例如，业务分析师可以从空白的 Visio 页面开始，使用形状和线条设计流程，然后连接到新的 K2 活动和事件。或者，开发者可以构建一个 K2 流程，业务分析师将其导入到新的或现有的 Visio 图表中，并将活动附加到相应的形状上。

对于表单开发，无法在 Visio 中创建自定义的 ASPNET 表单。然而，它们必须使用 Visual Studio 等开发工具进行创建。开发者可以创建必要的页面，并将 URL 信息提供给流程设计师，以便在 Visio 中使用客户端事件。如果已创建 InfoPath 表单，流程设计师可以将 Visio 图表与 InfoPath 流程集成，从而使用 InfoPath 表单完全实现流程。InfoPath 表单的设计必须在 Microsoft Office InfoPath 2007 中完成。

## 可扩展性

K2 Designer for Visio 的体验并不限于开箱即用的功能。该平台旨在用于协作和扩展。开发者可以创建自定义的 ASPNET 表单以及带有步骤和操作的预配置形状，供流程设计师使用。

流程设计师可以与开发者合作，扩展仅通过可用小组件启用的功能。可以通过从 Visio 导出流程并使用 K2 Designer for Visual Studio 打开流程来共享流程。来自 Visio 的所有配置过的活动、事件和属性都可以在 Visual Studio 中访问。开发者可以使用全套 K2 工具、Visual Studio 工具和自定义代码来完成流程逻辑。开发者可以提交文件（check in）供流程设计师验证。流程设计师可以在 Visio 中重新打开流程。如果开发者创建了 Visio 无法解释的对象，K2 Designer for Visio 将允许用户在 Visio 形状与孤立对象之间建立关联。

# 第三部分：K2 blackpearl 流程规划与设计核心

## 何时使用它

K2 Designer for Visio 旨在让业务分析师能够快速连接图表中的关键的 K2 活动和事件。在以下情况下应使用 Visio Designer：

- 业务分析师需要编写需求并将其转换为流程流的视觉表示。通过从 Visio 开始，关于流程的视觉信息可以在 Visual Studio 中重用，为开发者提供快速启动的帮助。
- 业务分析师对 K2 有足够的了解，能够根据流程定义连接图表。你可以既从图表开始，也可以从 Visio Studio 的预构建流程开始。最后，你将获得一个完全定义的、准备好部署和测试的 K2 流程。

## 何时不使用它

Visio 并不是所有用户的合适设计界面。在以下情况下不应使用 Visio designer：

- 开发者不熟悉 Visio 或不习惯使用 Visio。你应该使用你最熟悉的设计界面来快速开发你的 K2 流程。
- 在向导程序之前需要创建自定义代码。Visio designer 不暴露定义 K2 平台能力的代码。当需要创建自定义代码时，Visual Designer 更合适。然而，如果代码模块已经编写并作为 K2 向导程序暴露出来，则可以在 Visio designer 中使用它们。
- 需要首次创建 SmartObjects。K2 Designer for Visio 不包含 SmartObjects 的设计画布；这些对象必须在 Visual Studio 中创建。然而，一旦 SmartObject 经过设计和部署，它就可以通过 K2 Object Browser 在 Visio Designer 中使用。

## 用于 SharePoint 的 K2 Web Designer

以下信息基于编写本文时 K2 blackpearl 0803 当前提供的 K2 Web Designer for SharePoint 版本 (1.0)。Web Designer 正在发生一些变化，将在后续进行讨论。

业务用户可以使用 SharePoint 2007 中的 K2 Web Designer for SharePoint 可视化建模、构建并部署流程。K2 Web Designer for SharePoint 适用于站点集合内的库或列表设计工作流。使用 K2 Designer 的最大优势之一是 SharePoint 内容是内置的。你可以使用来自列表项的 K2 Designer 元数据，或使用人员作为目标规则。由于 K2 Designer 理解此上下文，因此这些信息对你是可用的。

为了使用 K2 Web Designer 加速设计，输出模板描述了用户在流程某点可以的操作。向导程序用于定义用户操作后 SharePoint 项目（即启动流程的文档或列表项）发生的情况。K2 为在 Web 浏览器内构建 SharePoint 的流程提供了视觉拖放和向导驱动界面。SharePoint 用户可以构建跨文档、站点、库、列表的流程，无需构建表单或理解技术概念。

## 用于 SharePoint 的 K2 Web Designer

该设计适用于 Microsoft SharePoint Server (MOSS) 2007 和 Windows SharePoint Services (WSS) 3.0。一旦在站点集合上激活了该功能，即可从任何文档或列表使用 K2 Web Designer for SharePoint。设计界面显示在浏览器中，与 SharePoint 站点位于同一框架内，如图 14-6 所示。

![](img/20dd98d522a8a8d52ab6ce563d54ca5541_0.png)

图 14-6

K2 Web Designer for SharePoint 适用于高级用户和业务分析师，侧边栏包含系列可在 K2 流程上下文使用的结果模板和向导。这将在后面的部分详细说明。

由于向导程序限于 K2 Web Designer for SharePoint，该设计界面不如 Visio Designer 或 Visual Studio Designer 强大。然而，对于终端用户来说，围绕文档或列表项设计简单流程更容易。

## 读者群体

K2 Web Designer for SharePoint 适用于高级用户或业务分析师创建简单的 SharePoint 流程。该设计器为不需要编写自定义代码的业务用户在 Web 浏览器内提供图形化工作流设计体验。

## 第三部分：K2 blackpearl 流程规划与设计要素

为了成功使用 SharePoint 版 K2 Web Designer，用户应熟悉 SharePoint 概念，如文档、列表、库、记录管理和权限，以及 K2 概念，如操作、结果、活动和事件。

此外，需要 SharePoint 管理员将此服务部署到 SharePoint 服务器群集中。虽然管理员可能不了解 Web Designer 的细节，但他/她应该熟悉在 SharePoint 内部部署功能的操作。有关部署 K2 Web Designer 的更多信息，请参阅第 12 章。

## 使用 K2 Web Designer

在已激活该功能的站点中，可以在任何列表或库的设置菜单中访问 SharePoint 版 K2 Web Designer。有关如何激活 Web Designer 功能的更多信息，请参见第 12 章。图 14-7 显示了带有 K2 Web Designer 选项的设置菜单。只有在拥有相应权限时才会显示此选项。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_542_0.png)

打开 Web Designer 后，您将看到您的个人流程列表以及他人共享的流程。您可以选择列出的流程之一进行编辑、共享、导出，或者可以创建一个新流程。这些选项显示在 K2 Web Designer 的工具栏中，如图 14-8 所示。如果您从列表打开 K2 Web Designer，则只会显示为列表设计的流程。同样，如果您从文档库查看 K2 Web Designer，则会列出为文档库设计的流程。

 506

## 第 14 章：K2 设计器与协作式流程设计

| K2 Web Designer | | |
| --- | --- |
| 新流程 | 编辑流程 | 共享流程 | 导出流程 |
| 个人流程 | | |
| 名称 | 状态 | |
| 共享流程 | | |
| 名称 | 状态 | |

图 14-8

共享流程将允许其他具有使用 K2 Web Designer 权限的用户在主页的“共享流程”部分中看到该流程。任何具有足够权限的站点成员都可以对共享流程进行修改和重新部署。

导出流程将构建流程定义并确保只导出完整的流程。导出流程会创建一个自解压的 .zip 文件（*exe*），您可以将其保存到本地并解压。这将创建必要的项目和流程文件，可以直接在 Visual Studio 中打开，或导入到 Visio 图表中。

点击“新流程”会产生提示，要求您输入流程名称并提供不同的选项，例如手动启动、在创建项目或更改项目时启动。对于表单库流程，您必须在创建新流程之前向该库发布一个 InfoPath 表单。InfoPath 流程的启动选项是“启动视图”（Start View）。输入信息后，将显示 K2 Web Designer 画布。

侧边栏包含了在 K2 Web Designer 中设计流程时可以使用的所有功能，如图 14-9 所示。

## 第三部分：K2 blackpearl 流程规划与设计要素

![](img/20dd98d522a8a8d52ab6ce563d548ca5_544_0.png)

这些侧边栏项目将被详细讨论，包括：

- **操作菜单**：允许您保存、另存为模板或更改流程属性的按钮。
- **模板**：结果模板定义了流程的活动流。
- **收藏**：将用户和组存储为收藏夹可以方便您快速引用频繁使用的项目，从而提高体验。
- **向导**：根据设计流程的位置（列表、文档库或表单库），可用向导列表将发生变化并显示在此菜单中。
- **流程模板**：可以使用已保存为模板的流程进行快速复用的功能。
- **用户和组**：类似于 Visio 或 Visual Studio 中的用户浏览器（User Browser），此项将显示可在流程内使用的 SharePoint 用户或组。

## 操作菜单

侧边栏顶部有一是操作菜单按钮。在设计流程时，您可以将其保存（在频繁设计大型流程时，强烈建议这样做）；将其部署到 K2 服务器，使其能够根据您的启动选项运行；使用“保存模板”选项，这允许其他人在设计新流程时将此流程作为起点；或者编辑流程的属性（如名称、描述和启动选项）。

部署流程将允许向导针对缺失信息启动流程定义，并在成功验证后，将流程部署到 K2 服务器上。在检查流程时发现的任何错误都将列出来，以便您可以修复问题并再次尝试部署。部署过程与从其他 K2 设计器部署项目类似，但由于环境上下文已知，它更加自动化。您无法将 K2 Web Designer 流程部署到不同的 SharePoint 环境。换句话说，您不能在测试 SharePoint URL 上设计流程并将其部署到生产环境。要在环境之间移动，您必须导出流程并使用不同的 K2 设计器进行部署。

 508

## 第 14 章：K2 设计器与协作式流程设计

## 模板

结果模板描述了用户可以采取的操作，且无法修改。
预建模板包括：

- 批准-拒绝（Approve-Decline）
- 批准-拒绝-更多信息（Approve-Decline-More Info）
- 批准-拒绝-审核（Approve-Decline-Review）
- 批准-拒绝-重做（Approve-Decline-Rework）
- 批准-重试（Approve-Retry）
- 返回（Back）
- 关闭结果（Close Outcome）
- 无结果（No Outcome）
- 重试关闭（Retry-Close）

使用模板可以定义，基本上定义了 K2 流程的活动。通过将模板拖到画布上，会打开一个向导，询问活动名称和描述，以及作为该活动可选的操作和结果。根据您使用的模板，可以添加、编辑或删除操作和结果。有关操作和结果的更多信息，请参阅第 8 章。

## 向导

一旦确定了活动，就需要描述事件。由于 K2 Web Designer 只能设计基于 SharePoint 的流程，并非所有的 K2 向导可用。根据设计流程的位置（列表、文档库或表单库），可用向导将发生变化。每个向导使用启动工作流的项目上下文。换句话说，如果设置为添加新项目时启动，则新添加的项目成为工作流上下文。向导对该项目进行操作。

## 第三部分：K2 blackpearl 流程规划与设计要素

向导根据下表限制：

| 文档向导 | 描述 | 所在 |
| --- | --- | --- |
| 签入文档 | 使用版本控制功能签入文档。 | 文档库 |
| 签出文档 | 使用版本控制功能签出文档。 | 文档库 |
| 复制文档 | 将文档复制到目标库，但在源库中保留文档。 | 文档库 |
| 删除文档 | 删除文档。 | 文档库 |
| 移动文档 | 将文档从源库移动到目标库。 | 文档库 |
| 邮件向导 | 描述 | 所在 |
| --- | --- | --- |
| 发送邮件 | 发送电子邮件通知，可以包含来自表单、文档或项目的元数据。 | 文档列表表单库 |
| 列表项目向导 | 描述 | 所在 |
| --- | --- | --- |
| 创建项目 | 在目标列表中创建新项目。 | 文档库 |
| 复制项目 | 将项目从源列表复制到目标列表。 | 文档库列表 |
| 删除项目 | 删除源列表中的项目。 | 文档库 |
| 记录管理向导 | 描述 | 所在 |
| --- | --- | --- |
| 将文档发送到记录中心 | 使用记录管理功能将文档发送到记录中心。 | 文档库 |
| 对记录设置锁定 | 使用记录管理功能对记录中心已有文档设置锁定。 | 文档库 |
| 取消记录锁定 | 使用记录管理功能取消记录中心已有文档的锁定。 | 文档库 |
| 删除记录 | 使用记录管理功能删除记录中心中的文档。 | 文档库 |

# 第14 章：K2 设计师与协作流程设计

在设计工作流之前，表单库必须在库中发布 InfoPath 表单。只有在设计带有 InfoPath 表单的工作流时，才能使用唯一的邮件向导。对于更复杂的流程，请勿使用 K2 Web Designer。

有关 SharePoint 向导用途的更多详细信息，请参阅第 13 章。

# 收藏 (Favorites)

当您为各种活动设置终点时，有能力将用户存储为收藏，如图 14-10 所示。一旦用户或组被添加为收藏，它将显示在侧边栏的“收藏”部分。对于您在流程中频繁使用的用户或 SharePoint 组，将它们保存为收藏是一个好主意，可以快速地将它们拖放到活动中，从而加快设置终点的速度。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_547_0.png)

# 流程模板

一旦您设计并配置了一个流程，就可以将其保存为流程模板。这允许您将流程或流程的部分保存为模板，以加速设计过程。例如，您可以配置一个两步审批流程，其中拒绝步骤会向发起者发送电子邮件，并将其保存为流程模板。下一次您构建具有此类类型两步审批流程的流程时，无需再次从头开始并重新配置审批步骤，只需拖入流程模板即可节省一些时间。

流程模板会在您正在设计的流程中创建模板定义的副本。它不是对原始流程的引用，因此如果您更改了流程，该更改不会反映在其他使用该流程作为模板的流程中。流程模板无法进行编辑，只能释放到默认的“表单提交”（Form Submitted）活动中。这意味着它们可以在流程开始使用，但不能作为构建块进行堆叠。

# 第三部分：K2 blackpearl 流程规划与设计核心要

# 用户和组

在您正在设计流程的集合中，可用的“用户和组”将显示在侧边栏中。您可以将 SharePoint 组拖放到活动中，以快速地将该组设为终点。请记住，侧边栏仅显示对您访问 K2 Web Designer 的列表或库授予显式权限的特定用户和组。如果您没有看到想要使用的组，请尝试打开活动的终点属性。如果仍然没有列出该组，请在站点集合的上下文中搜索用户或组。他们可能没有访问站点集合的权限。检查 SharePoint 权限并重试。

# 协作体验

在 K2 Web Designer 中创建的流程可以导出。这会使用 K2 API 创建必要的项目、文件夹和文件结构，以便该流程可以在其他设计界面中使用。一旦完成，该流程可以导入到 K2 Designer for Visio 中并附加到图表上。该流程也可以在 K2 Designer for Visual Studio 中打开，以进行更复杂的活动和集成。

一旦流程被 Visio 或 Visual Studio 修改，它将无法再使用 K2 Web Designer for SharePoint 进行修改。这是由于 K2 Web Designer 中向导的局限性。还强烈建议，如果 K2 Web Designer 流程被其他工具修改，在部署流程之前应更改名称。因为在 Web Designer 中创建流程的用户仍然可以对“旧”流程进行更改并部署，这可能会导致流程的版本问题并带来一般的困扰。通过在从另一个设计器部署之前更改流程名称，您可以缓解这一问题并防止 K2 Designer 覆盖它。

这种协作体验的关键在于沟通。务必告诉使用 Web Designer 设计流程的人员，流程已被修改，他们不应使用 Web Designer 进行更改，而应通过其他设计器按照必要的程序来进行更改。

# 扩展性

虽然在其他设计工具中使用的向导在 K2 Web Designer 中可用，但存在一些扩展点。

K2 Web Designer 具有模板概念，用户可以将流程保存为模板，从而进行设计并复用。例如，流程可以定义并配置以相同的方式启动，并根据表单的值以不同的方式进行处理。通过将流程的启动配置保存为模板，用户可以在 K2 Web Designer 的“收藏”中快速访问常用项目（如用户或组）。K2 Web Designer 不包含 SmartObjects 的设计画布；这些必须在 Visual Studio 中创建。

# 第14 章：K2 设计器与协作流程设计

虽然流程设计器感知其启动的列表或库，但部署的工作流可以在整个 SharePoint 站点集合中使用，并与所设计的列表或库关联。这是设计和复用流程的另一种方法。

# 使用场景

K2 Designer for SharePoint 是一种简单的设计工具，在以下情况下应使用：

- 用户希望创建简单的基于 SharePoint的工作流，且可用向导已满足流程所需。请记住，K2 Web Designer 中的文档和列表项向导有所减少；对于所有可用向导请使用另一个 K2 Designer。
- 当流程以 SharePoint 为中心，这意味着流程中的所有项目都围绕文档、列表项或表单。

# 不使用场景

在以下情况下不应使用 K2 Designer for SharePoint：

- 需要更复杂的工作流，预定义的模板不够灵活。例如，复杂的工作流解决方案无法使用 K2 Web Designer 创建。此外，无法使用 K2 Designer 修改 SharePoint 集成的任务和工作流历史列表。
- 需要创建自定义代码。K2 Web Designer 无法创建自定义代码或自定义向导。需要创建自定义代码时 Visual Studio 更合适。
- 需要首次创建 SmartObjects。K2 Web Designer 不包含 SmartObjects 的设计画布；这些必须在 Visual Studio 中创建。而且，K2 Web Designer 无法使用 SmartObjects，因此任何依赖业务数据的流程都应使用其他 K2 设计工具进行设计。
- 需要使用未导入 SharePoint 组或用户的 Active Directory 组或用户。K2 Web Designer for SharePoint 中的用户浏览器中仅可用 SharePoint 组和用户。

#### K2 Designer for Visual Studio

K2 Designer for Visual Studio 是 Visual Studio 2005 的一个完全集成扩展，提供了强大的设计体验，允许访问所有 K2 工具以及针对适当 K2 对象生成的 Microsoft .NET Framework 3.0 Windows Foundation Schedules 和相关的 Microsoft .NET 代码。

## 第三部分：K2 blackpearl 流程规划与设计核心

在编写时，Visual Studio 2008 的支持已计划并在开发中，但 K2 blackpearl 0803 仅支持 Visual Studio 2005。

在 Visual Studio 版 K2 Designer 环境中（如图 14-11 所示），开发者可以简化组件拖拽到流程设计画布的操作。基于 Windows Presentation 的向导——包括与 SharePoint 等技术集成、发送电子邮件以及显示 ASP.NET 或 Microsoft Office Path 2007 功能的向导——引导开发者配置底层的 Workflow 函数、规则和活动。开发者可以使用 K2 提供的开发者参考（Developer Reference）来开发自定义向导。在 K2 中构建的流程是扩展性的。.NET 3.0 —— 包括 Workflow Foundation (WF)、Windows Communication Foundation (WCF) 和 Windows Presentation Foundation (WPF) —— 因此开发者可以在 WF 设计画布内或通过自定义 C# 代码打开并扩展流程。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_550_0.png)

除了 K2 设计工具外，开发者还可以使用向导驱动的模板，并且开发者可以选择根据需要访问生成的 Microsoft .NET 组件。

## 第 14 章：K2 Designer 与协作流程设计

解决方案管理器（Solution Explorer）用于浏览 K2 项目及相关依赖。它包含一个用于生成、部署和向 K2 项目添加新项目的右菜单。在后台，MSBuild 用于生成、打包和部署 K2 解决方案。当创建新的 K2 项目或流程定义时，会自动添加所有项目引用。K2 项目也可以包含在标准的 .NET 接口文件中，例如 ASP.NET 页面和 Windows Forms。InfoPath 解决方案已集成到项目系统中，确保 InfoPath 表单模板及其相关的 K2 项目在版本控制和部署方面保持同步。此外，开发者可以一键访问 K2 项目包含的所有 InfoPath 表单模板。

### 目标读者

Visual Studio 版 K2 Designer 供开发者使用模型和业务实体。要成功使用 Visual Studio 版 K2 Designer，开发者应该熟悉 Visual Studio 概念（如生成、设置属性、部署和处理错误信息），以及 K2 概念（如操作/actions、结果/outcomes、活动/activities 和规则/rules）。

### 使用 Visual Studio 版 K2 Designer

由于 Visual Studio 版 K2 Designer 是开发者群体的首选 K2 Designer，因此在本书一直使用。在第 7 章中，你学习了如何使用 Visual Studio 创建智能对象（SmartObjects）。在第 9 章中，你初次接触使用 Visual Studio 设计 K2 流程。第 11 章涵盖了用于与流程交互的自定义 ASP.NET 表单。有关如何使用 Visual Studio 设计流程、智能对象或自定义 ASP.NET 页面的更多细节，请参考这些章节。

### 协作体验

在 SharePoint 版 K2 Web Designer 或 Visio 版 K2 Designer 中设计的任何流程都可以导出到 Visual Studio 版 K2 Designer，允许开发者增强这些流程。在 Visio 版 K2 Designer 中创建的流程也可以从 Visual Studio 发回，允许业务分析师和开发者对流程进行双向修改。

### 扩展性

K2 设计体验不受限于开箱可用的功能。该平台旨在协作和扩展。例如，开发者可以创建 ASP.NET 页面以及带有步骤和操作的预配置向导，供其他流程设计师使用。使用 K2 开发者参考，可以开发自定义向导，然后在 Visio 版 K2 Designer 中使用。有关创建自定义向导的更多信息，请参阅 K2 blackpearl 开发者参考。

流程设计师也可以与开发者合作，扩展无法通过可用向导启用的能力。流程可以从 Visio 导出并在 Visual Studio 中打开。开发者能够在 Visual Studio 版 K2 Designer 中直接使用流程模型和任何预配置的向导。开发者可以使用全套 K2 工具、Visual Studio 工具和自定义代码来完成流程逻辑。开发者可以提交文件供流程设计师进行验证。流程设计师可以在 Visio 中重新打开流程。如果开发者发现 Visio 无法解析，Visio 版 K2 Designer 将允许用户在 Visio 形状与孤立对象之间建立关联。## 第三部分：K2 blackpearl 流程规划与设计核心

### 何时使用

Visual Studio 版 K2 Designer 是开发者最强大的工具。在以下情况下应使用它：

- 开发者熟悉 Visual Studio。
- 开发者需要创建或编辑代码。
- 开发者需要使用 K2 工具。
- 开发者需要处理自定义 ASP.NET 页面。

### 何时不使用

在以下情况下不使用 Visual Studio 版 K2 Designer：

- 业务分析师希望在不使用 Visual Studio 的情况下设计流程。
- 开发者不熟悉 Visual Studio。

### 未来设计工具

Visual Studio 版 K2 Designer 可能会发生变化。以下功能将在未来的版本中可用：

### K2 Studio

通过 K2 Studio，业务用户可以轻松设计流程。K2 Studio 提供了一个用户熟悉的 Office 风格环境。它旨在允许业务分析师开发工作流。

## 第 14 章：K2 Designer 与协作流程设计

K2 Studio 的一些关键功能：

- **K2 工具箱（K2 Toolbox）**：方便访问 K2 组件和向导。
- **解决方案管理器（Solution Explorer）**：启动 K2 项目时会自动更新所有项目引用。
- **流程助手（Process Helper）**：缩短开发周期并原型化。
- **可视化流程设计器（Visual Process Designer）**：用于可视化建模流程的可扩展画布。
- **智能对象设计器（SmartObject Designer）**：提供构建数据实体的可视界面。
- **流程指南（Process Guides）**：通过步骤指南帮助新手流程设计师。

# 第三部分：K2 blackpearl 流程规划与设计核心

下一版本的 K2 Web Designer 将不再依赖 SharePoint 即可设计流程。它仍然具有对 SharePoint 的感知能力，允许根据启动它的站点集合和库来快速构建流程。然而，K2 Web Designer 也将作为一个独立的网站运行，以消除对 SharePoint 的依赖。

与第一版一样，K2 Web Designer 旨在供分析师或高级用户用于开发流程驱动的应用程序。虽然画布绘图和思考业务流程的范式可能会发生，但用户应该熟悉 SharePoint 的概念（如文档、列表、库、记录管理和权限）以及 K2 的概念（如操作 actions、结果 outcomes、活动 activities 和事件 events）。

## 协作工作

由于项目团队可以使用各种不同的设计器，因此在协作处处理 K2 项目时，理解一些准则至关重要。对于任何技术项目，都存在项目范围之外挑战。接下来的章节将讨论与 K2 成功协作工作的挑战和最佳实践。

## 示例场景

在讨论细节之前，让我们来看过一个协作开发的示例场景。假设你已经设置好了项目，选择了要自动化的流程（在本例中，让我们使用新员工入职的 HR 流程），并召开会议讨论了业务需求并记录了用例。

业务分析师获取需求并开始使用 Visio 创建流程模型。该图表使用适当的形状创建，以准确描述流程，从职位发布开始、面试流程、录用信等，直到员工被录用并开始第一天工作。一旦该图表获得相关利益相关者的批准，业务分析师就开始开发该流程。他们开始用适当的活动和事件连接形状，从一个上传到 HR 站点 SharePoint 文档的帖子开始。业务分析师理解 K2 的概念和向导，这些向导可以轻松地连接流程中的许多活动。一旦申请人提交了申请并安排了面试（在 HR 站点的面试日历上），并且做出了提供录用信的决定，录用信实际上由薪资部门使用其遗留系统来处理工资、加薪和奖金。

由于流程现在进入了系统集成的领域，而且业务分析师并不了解工资系统的底层技术，他们需要开发者的帮助。他们可以保存 Visio 图表并导出 K2 流程。当他们导出流程时，会自动创建必要的 K2 项目和流程。开发者随后可以在 Visual Studio 中打开 K2 流程，并开发必要的代码以与薪资系统集成。

## 第14 章：K2 设计器与协作流程设计

一旦开发者完成了集成任务（例如，可能使用自定义代码事件，或者使用一系列 SmartObjects 向薪资系统暴露数据并更新数据），他将保存流程并告诉业务分析师工作已完成。他们随后可以将流程修改回 Visio 图表。之前连接的所有事件将仍然保持连接状态。开发者创建的新事件（在 Visio 中显示为活动）可以与 Visio 图表上的形状关联，业务分析师可以继续处理该流程。

K2 平台通过提供一个定义 K2 解决方案、项目和构件的通用框架，允许团队成员之间进行紧密协作。然而，技术只能告诉你目前在协作方面进展得如何。还有一些技术之外的考虑因素是你应该 same。

## 识别角色并制定计划

任何成功项目的一部分都是拥有明确定义的范围、项目计划和责任矩阵。通过识别谁负责哪些任务以及何时截止，你就可以尽早建立预期目标。此外，你可以利用此机会查看团队成员并识别他们的优缺点。利用这些来帮助他们学习将要使用的新工具，例如 K2 设计器或你使用的项目报告工具。如果某个团队成员不会成为开发者，就不要教他们如何使用 Visual Studio 版 K2 Designer。相反，将他们的精力放在 Visio 版 K2 Designer或其他画布上。

通过明确识别之前的示例场景，业务分析师知道他们负责尽可能地创建流程。此外，他们知道谁负责与薪资系统的集成。在任何流程自动化工作之前定义这些信息，将使团队成员能够有效地一起工作。

## 根据项目计划管理

业务流程自动化项目与其他任何项目都一样。如果你有一个大型团队，请确保尽早设定责任和截止日期。让人们对分配给他们的任务负责，使用你环境中的任何方法，如每日电子邮件或每周会议，或者可能是你环境中的 SharePoint 或 Microsoft Project 来管理项目。利用工具来帮助你掌控项目。虽然确保项目按计划进行主要是项目经理的工作，但团队中每个人的责任都是了解他们应该在工作什么。

## 源代码控制

对于任何开发项目，将应用程序的代码提交到源代码管理工具都是好主意。这种方法既是工作代码的备份，又提供了版本控制和锁定功能，防止在大型开发团队中发生更改覆盖。

# 第 14 章：K2 设计器与协作流程设计

### K2 blackpearl 的旧版本
使用 K2 blackpearl (0807)，该流程是无缝且完全集成的。如果您在使用旧版本的 K2 blackpearl，在提交添加到项目文件结构中的扩展项目（extender projects）时会出现问题。请务必确保运行的是最新版本的 K2 blackpearl，以确保拥有最新的修复程序和功能。

如果您运行的是旧版本的 K2 blackpearl，仍然可以将您的 K2 项目提交到源代码控制中。请确保仅提交 `.kpxrx` 文件；不要提交由 K2 向导自动创建的扩展项目。这些扩展项目会在需要时重新创建，所有的自定义和配置信息都存储在 `.kpxrx` 文件中。

# 沟通、沟通、沟通

无论您使用什么技术来帮助管理源代码，如果团队没有有效沟通，您将始终遇到问题。尽早制定准则，让每个人在每天结束时提交文件，并在第二天开始工作前获取前一天的最新版本。或者，设定准则要求项目在提交之前必须在本地构建，这有助于确保源码控制中的代码始终是可运行的副本。

这些准则应该在项目开始时制定，经常提醒大家这些规则是一个好主意。记住，提醒是保持这些准则处于项目重点的好方法，以确保团队协作。

此外，不要依赖技术来推动协作。紧密地工作（字面意思是，让项目团队彼此邻近）可以帮助项目高效运行。如果项目是虚拟的，使用电子邮件和即时消息等工具进行定期状态会议或维护中央问题列表，也是帮助管理项目团队之间沟通的好主意。

### 总结

K2 平台的通用项目框架允许许多设计工具以及设计师与项目文件系统之间的无缝集成。通过诸如 Visio 的 K2 Designer、SharePoint 的 K2 Web Designer 以及 Visual Studio 的 K2 Designer 等，无论技术能力如何，都能找到匹配项目技能的设计器。作为团队协作时，经常沟通、管理项目计划并使用源代码仓库控制源码和流程文件是很好的。这将有助于 K2 项目的成功，无论项目或团队规模有多大。

在之前的章节中，您已经学习了如何使用 K2 blackpearl 的各种部分和组件创建流程，并在本章最后学习了如何与其他流程设计师协作。在下一章中，您将转向 K2 blackpearl 的管理功能，包括 K2 服务器和组件的管理。

## 第四部分
## K2 blackpearl 的管理

# 15
## 服务器与组件管理

Eric Schaffer

本章将完成两件事：

- 向您介绍构成 K2 blackpearl 环境的主要组件
- 导引您对这些组件进行日常维护和管理

每个组件都承担着特定的角色，确保这些组件正常运行是 K2 管理员的一项重要任务。本章不是安装指南，也不是故障排除指南。请参阅产品文档获取安装和故障排除信息。

# 服务器架构

作为 K2 管理员，对 K2 blackpearl 服务器的底层架构有一个基本的理解至关重要。

K2 blackpearl 服务器的核心运行在 Microsoft Windows 2003 服务器上的服务。该服务利用了标准的微软技术，如 .NET Framework 3.0、微软消息队列 (MSMQ)、微软分布式事务协调器 (MSDTC)、互联网信息服务 (IIS)、Microsoft SQL Server 2005 以及 Microsoft SQL 报告服务。

K2 blackpearl 服务被设计为可插拔的主机服务器（Host Server）。这种可插拔框架允许支持 K2 环境的服务被单独开发和管理，同时为其他服务提供了一组核心接口。该框架也对开发者开放，允许构建自己的服务，从而提供了高度的可扩展性。

## 第四部分：K2 blackpearl 的管理

这可以用到的一个例子是身份验证程序。K2 blackpearl 自带了两个身份验证程序（Active Directory 和 SQL Server）。

图 15-1 显示了高层架构。下表提供了在主机服务器内运行的服务简要概述：

| 服务 | 描述 |
| :--- | :--- |
| SmartObject Server | 处理与 K2 环境中 SmartObjects 的交互。 |
| SmartObject Management | 处理 K2 环境中 SmartObjects 的管理。 |
| Workflow Server | 负责 K2 环境中流程实例的执行。 |
| Workflow Management | 处理环境中的特定特定接口。 |

# 第四部分：K2 blackpearl 的管理

## 工作空间控制台

工作空间控制台是系统和进程管理员使用的管理应用程序中心，用于配置从 K2 平台到每个进程的角色以及用户权限的所有内容。

当加载管理（Management）选项卡时，列栏（Column Bar）包含每个管理应用程序（参见图 15-2）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_564_0.png)

图 15-2

大多数 K2 管理任务都通过工作空间控制台处理，本章的第一部分涵盖了这些管理功能。然而，K2 环境中的某些组件是在不同的应用程序中管理的，例如本章后面“K2 SharePoint 组件管理”部分讨论的 K2 SharePoint。

## 通用工作流服务器设置

K2 管理员的首要工作是确保管理应用程序已正确配置。可以通过工作空间控制台为工作流服务器配置通用管理设置。要访问这些设置，右键点击工作流服务器（Workflow server）并选择编辑设置（Edit Settings）。下表解释了如何配置这些设置：

| 选项卡 | 说明 |
|---|---|
| General（常规） | 用于配置常规服务器设置，包括服务器名称和端口。 |
| Database Settings（数据库设置） | 用于配置数据库和日志数据库设置，包括名称和身份验证设置。 |
| Advanced Settings（高级设置） | 用于设置更高级的属性，包括线程数、Microsoft .Net Framework 版本、跟踪设置和托管用户（Managed Users）设置。 |
| User Settings（用户设置） | 用于配置用户设置，包括允许匿名用户和运行动态查询。 |

常规（General）选项卡（参见图 15-3）具有指向适当 K2 工作流服务器和端口的设置。通常的管理不需要更改这些设置。此外还有一个处理器配置（Processors Configuration）设置。该设置适用于基于处理器的许可模型，您可能需要指定 K2 工作流服务器将利用哪些处理器；如果您在双 CPU 机器上拥有单 CPU 许可，则需要输入 1（指定 K2 将使用处理器 1）或 2（指定 K2 将使用处理器 2）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_565_0.png)

图 15-3

数据库设置（Database Settings）选项卡配置工作流服务器的数据库连接。K2 blackpearl 安装将为您配置这些信息，但如果您迁移了数据库或希望更改工作流服务器验证数据库连接的方式，这就是您可以进行这些更改的界面。

高级设置（Advanced Settings）选项卡具有工作流服务器的其他设置。下表提供了该选项卡上每个设置的简要描述：

| 设置 | 说明 |
| --- | --- |
| Thread Count（线程数） | 工作流服务器执行进程使用的线程数。 |
| Thread Priority（线程优先级） | 工作流服务器执行进程使用的线程优先级。 |
| Framework Version（框架版本） | 工作流服务器执行进程使用的 .NET Framework 版本。 |
| Trace（跟踪） | 配置服务器日志的旧版设置。 |
| File（文件） | 配置服务器日志文件的旧版设置。 |
| IPC Retry Count（IPC 重试次数） | 服务器对失败的进程间通信调用进行的重试次数。 |
| IPC Retry Interval（IPC 重试间隔） | 失败的进程间通信调用重试尝试之间的时间间隔（分钟）。 |
| Display Worklist of Managed Users（显示托管用户的工作列表） | 如果勾选此项，Active Directory 中定义了直接汇报的用户将能够看到并管理这些用户的工作列表。 |
| Worklist Remove（移除工作列表） | K2 blackpearl 不使用的旧版设置。 |
| Default Platform（默认平台） | 服务器使用的默认工作列表平台。 |

用户（User）选项卡定义了与身份验证相关的设置，例如是否允许匿名连接或使用动态队列。其他设置是专门用于与工作流服务器配合的用户管理界面设置，除非开发了自定义用户界面管理来替换默认界面，否则不应进行修改。

## 许可管理

您环境中的每台 K2 blackpearl 服务器都需要一个有效的许可密钥才能运行。许可密钥基于系统密钥（system key），系统密钥是由内部 K2 算法生成的唯一特定密钥。大多数许可密钥是永久的，只需要在安装期间设置。然而，在某些情况下，需要更新许可密钥。例如，如果服务器硬件发生变化，系统密钥可能会发生变化并导致现有的许可密钥失效。另一个例子是如果您对许可协议进行了更改。如果您有 30 天试用密钥并随后购买了许可，您可以更新试用密钥而无需重新安装软件。

许可管理（License Management）界面位于 K2 工作空间的管理（Management）部分。
许可管理界面（参见图 15-4），您可以在此处查看和编辑您的许可密钥。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_567_0.png)

图 15-4

要编辑您的许可密钥：

1. 从列表中选择密钥并点击编辑（Edit）。
2. 弹出的窗口，您可以在其中输入新的许可密钥。
3. 点击确定（OK）应用更改。
4. 需要重启 K2 服务器使许可更改生效。

许可管理下还有一个名为 K2 用户（K2 Users）的区域。K2 可用的许可模型之一是命名用户（Named User）。此界面允许管理员查看哪些用户正在消耗许可，并移除不再需要的用户的许可。如果您有命名用户许可，已分配许可的数量和剩余许可的数量将与许可密钥一起显示在许可界面中。要移除用户的许可，只需勾选要移除的用户名称旁边的复选框（参见图 15-5）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_568_0.png)

图 15-5

您会发现没有添加用户的界面。用户在登录工作空间或应用程序时会自动接收许可。

## 环境库和字符串表管理

环境库（Environment Library）在最基础的层是一组名称-值对或字段的集合，进程设计人员可以在设计期间使用这些值并将其部署到多个环境。字符串表（String Table）是环境库的运行时反射。对于每个库，可以配置环境（例如，开发、测试和生产环境）。当进程被部署时，设计人员选择其中一个环境，与该环境关联的值将用于部署到所选环境，并作为字符串表值与进程一起部署。

在本节中，我们将涵盖围绕环境库的基础管理。有关在设计进程时使用环境库的最佳实践和用法的信息，请参阅第 10 章。

在工作空间的管理部分，环境库标题下，有三个主要的管理部分：

- 插件类型（Plugin Types）
- 字段类型（Field Types）
- 模板（Templates）

插件类型允许在 K2 对象浏览器中显示更多功能（参见图 15-6）。例如，由于 SharePoint 服务器插件提供的功能，您可以在 K2 对象浏览器中动态钻取 SharePoint 站点的结构。通常的管理不需要添加、删除或编辑这些插件类型，但该界面供管理员执行这些功能。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_569_0.png)

字段类型（Field Types）部分是环境库模板可以使用的字段类型全局列表。每个字段类型都与一个插件类型关联，并有一个设置来决定该字段类型是否应默认添加到模板中。通常的管理不需要添加、删除或编辑字段类型。如果添加了新的插件类型，需要将该插件所需的字段类型添加到字段类型列表中。

` 和 

# 第15章：服务器与组件管理

![](img/20dd98d522a8a8d52ab6ce563d548ca5_575_0.png)

15-10

在“区域详情”（Zone Details）选项卡上，您可以指定时区（GMT）并为区域提供名称（Name）和描述（Description）。此外，您可以标记该区域是否默认区域（Default Zone）。当流程设计人员没有专门选择其他区域时，默认区域将用于升级和启动规则。

在“工作时间”（Working hours）选项卡上，您将看到一个分为 30 分钟区块的日历。点击并拖动这些区块可以选择这些区块作为活动时间。活动时间用绿色区块表示，非工作时间用黑色区块表示。

在“特殊与例外日期”（Special & Exceptions Dates）选项卡上，您可以指定假期和其他日期范围，将其从工作时间区域中排除。

要保存对新区域的更改，请点击页面底部的保存（Save）。该区域将供流程设计人员在指定升级和启动规则时使用。创建新区域后，您可以通过工作空间控制台（Workspace Management Console）中用户部分下的“工作时间访问”界面向此区域添加用户和组。要向时区添加或删除用户和组，请从下拉列表中选择所需的时区并使用添加（Add）和删除（Delete）选项。

# 第四部分：K2 blackpearl 管理

如果用户通过工作空间被定义为某个特定时间的一部分，则该设置将覆盖客户端事件升级（Client Event Escalations）的默认时间。例如，如果流程设计人员在包含客户端事件的活动上配置了默认时间的升级，而运行时接收任务的用户是默认区域之外其他区域的成员，则升级将根据用户的时区运行。

# 流程实例管理

作为管理员，实时查看在服务器上执行的流程实例状态至关重要。通过管理界面，有两种方法可以流程实例的状态视图。您可以通过工作空间管理工具钻取某个流程并使用实例界面，该界面将自动过滤该流程；或者，您可以右键点击“进程”（Processes）标题并选择“管理实例”（Manage Instances）。在未指定过滤标准的情况下，后者将显示服务器上所有的流程实例。两个界面都会显示有关流程实例状态的相同基本信息。

获取流程实例状态信息的另一种方法是通过第 20 章中讨论的报告界面。与管理界面不同，报告界面是流程的只读视图，不允许进行任何流程操作。

状态（Status）字段标识流程实例所处的状态。下表标识了各种状态及其含义：

| 状态 | 描述 |
|---|---|
| Active (活动) | 流程实例正在等待外部输入。通常，这意味着已分配了一个任务项，并在任务完成后流程将继续。 |
| Running (运行中) | 流程实例正在执行流程代码。服务器事件和规则逻辑属于此类。除非流程包含大量的代码级级处理，否则流程实例不应长时间处于运行状态。 |
| Stopped (停止) | 管理员通过管理界面暂停了流程实例的执行。 |
| Error (错误) | 流程实例进入错误状态。 |
| Completed (已完成) | 流程实例已完成。（此状态在流程管理界面被过滤，但在流程报告中显示。） |
| Deleted (已删除) | 流程实例已被删除，但保留了报告信息。（此状态在流程管理界面被过滤，但在流程报告中显示。） |

# 第15章：服务器与组件管理

从任一界面，您都可以对选定的流程实例执行若干操作。下表描述了这些各种操作：

| 操作 | 描述 |
|---|---|
| Start (启动) | 启动操作将恢复已停止的实例。启动操作仅适用于停止的实例。同样，停止（Stop）操作将暂停流程实例的执行，且仅适用于活动和运行中的实例。 |
| Delete (删除) | 删除操作将删除流程实例。当您选择删除流程实例时，系统会询问是否要保留日志目。删除日志目将删除有关该流程实例的所有报告信息。保留日志目将保留实例的报告信息，但流程显示为删除状态。 |
| GoTo (跳转) | 跳转操作允许您将流程从当前活动移动到流程定义中的任何其他活动。 |
| New (新建) | 新建操作允许您启动流程的新实例。这对于测试特定版本的流程非常有用。 |

# 流程版本管理

此界面可以完成的一项主要管理任务是设置默认流程版本标记，该标记决定了新实例将使用哪个流程版本。K2 workflow.client API 还支持传递版本参数，该参数将覆盖默认标记并允许开发人员启动特定版本的流程。

此界面还允许管理员下载任何已部署流程版本的源代码。这在流程设计人员机器上的源代码丢失的灾难情况下是一个方便的功能。然而，它并不是源代码控制的替代品，因为它存储的是已部署的流程版本，而不是通过 K2 设计界面保存的版本。

# 第四部分：K2 blackpearl 管理

![](img/20dd98d522a8a8d52ab6ce563d548ca5_578_0.png)

如图 15-11 所示，存储了每个版本的信息。下表是对这些列的每个描述：

| 设置 | 描述 |
|---|---|
| Version (版本) | 流程的数字标识符。 |
| Label (标签) | 给的名称。 |
| Description (描述) | 部署人员对流程的描述。 |
| Date (日期) | 流程版本部署的时间。 |
| Source (源) | 允许从服务器下载版本文件的链接。 |
| Export User (导出用户) | 导出版本的用户 ID。 |
| Default (默认) | 指定默认启动哪个版本的标记。 |

图 15-11

# 第15章：服务器与组件管理

K2 black 服务器会捕获流程实例执行期间发生的任何未处理异常。任何产生未处理异常的实例都会进入错误状态。它会停止该实例的执行，并允许服务器继续处理其他实例，而无需解决错误之前停止一切。在本节中，我们将讨论工作空间和 Visual Studio 中的错误管理功能。有关错误日志的更多信息，请参阅第 19 章。

K2 管理员可以通过工作空间的管理部分查看所有错误状态的流程实例列表。错误配置文件（Error Profiles）界面（见图 15-12）位于所需服务器的工作流服务器标题下方。

图 15-12

# 第四部分：K2 blackpearl 管理

请注意，在“Error Profiles”（错误配置文件）标题下，你会发现列出的多个配置文件。配置文件允许管理员配置过滤后的错误视图。默认的错误配置文件是“All”（全部）视图，它显示系统上的所有错误。

为每个部署的进程创建一个错误配置文件可能会很有帮助。这样，你就可以逐进程处理错误。

若要配置新的错误配置，请在树形视图中右键点击“Error Profiles”，并选择“Add New Error Profile”（添加新错误配置）。将出现“Create New Error Profile”（创建新错误配置）页面。

“Properties”（属性）选项卡允许你为配置命名（Name）、选择进程（Processes）过滤器以及选择日期范围过滤器。

“Specific”（特定）选项卡为你提供了错误类型的复选框列表。通过勾选错误类型的复选框，你为你的配置选择了该类型。取消勾选错误类型的复选框则会在你的配置中排除该错误类型。

> 除非你计划为每个错误类型创建一个过滤器，否则通常不要在配置中取消勾选错误类型。如果知道某个进程处于错误状态，但由于过滤条件而无法找到该错误，将是非常令人沮丧的。

要查看新配置（见图15-13），只需点击该配置（在我们的示例中为 RepairErrorRepairExample）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_580_0.png)

图 15-13

# 第15章：服务器和组件管理

如图15-13所示，“Error Profiles”视图向你显示进程 ID、进程名称（Process name）、源事件名称（Source event name）以及错误描述（Description）。点击“Retry”（重试）将为列表中的每个进程实例返回生成异常的事件。此功能对于解决超时或文件锁定等问题很有帮助。

Workspace（工作区）是确认进程状态的好地方，但它并不是调试平台。任何需要进程实例化的实例都需要通过 Visual Studio 内的 K2 Process管理工具进行处理。该工具允许你检查实例是否处于错误状态，以便进行打开、操作和重新部署。这种能力需要具备进程设计的知识，并可能需要代码层面的修改；进程开发人员比典型的 K2 管理员更适合执行这些修复。然而，我们将简要介绍此功能，因为它是解决运行时错误的强大工具。

可以通过 Visual Studio 的“View”（视图）菜单访问 K2 Process管理工具（见图15-14）。
该工具有三个窗口：

- Environments（环境）
- Error Profile（错误配置）
- View Flow（查看流程）

![](img/20dd98d522a8a8d52ab6ce563d548ca5_581_0.png)

图 15-14

# 第四部分：K2 blackpearl 管理

左侧的“Environments”窗口允许你选择想要查看的错误配置。浏览器中显示的错误配置与 Workspace Management Console（工作区管理控制台）显示的配置相同。在“Environments”窗口中选择配置将更新右上角的“Error Profile”窗口，显示所选配置的错误列表。选择特定错误将填充右下角的“View Flow”窗口，向你显示进程的图形表示。

当发生错误时，有两种选项可用：

- 你可以重试事件，这与 Workspace Management Console 中显示的功能相同。
- 你可以在设计器中打开进程实例，并编辑导致问题的事件项。

为了说明修复错误的功能，图15-14所示的进程是一个带有服务器事件的单步进程。服务器事件背后的代码尝试执行除零操作并进入了错误状态。

我们可以打开进程实例并修改代码。

一旦完成修正，我们就可以重新部署实例并验证实例不再处于错误状态。

图15-15 显示该进程现在关联了一个额外的版本。我们对进程所做的更改已作为新版本部署，而之前处于错误状态的部分将针对进程的下一个版本执行。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_582_0.png)

图 15-15

# 第15章：服务器和组件管理

目前修复错误界面支持的进程更改仅限于导致错误的事件的更改。所有其他进程更改将被忽略。

修复错误功能是强大的，确切了解幕后正在发生什么至关重要。当你修复错误时，你正在直接操作存储在 K2 服务器上的进程定义。这些更改不会更新进程设计人员意图部署解决方案的设计文件，因为这些文件存储在开发人员机器上或源代码控制系统中。这意味着，如果进程设计人员返回源文件修复问题，或者不从 K2 服务器下载修复后的定义，他们部署的下一个版本将重新引入该错误。

将其想象成一个文档库。如果你将存储在本地机器上的文档上传到文档库，然后某人修复了文档库中存储的文档拼写错误，你的本地副本就过时了，再次上传文档将重新引入该错误。

## 工作列表管理 (Worklist Administration)

K2 用户有能力管理分配给他们的所有任务。Worklist 位于 Management Console（见图15-16）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_583_0.png)

图 15-16

# 第四部分：K2 blackpearl 管理

通过此界面，K2 管理员可以对当前可用工作列表项进行过滤搜索。你可以根据进程名称（Process Name）、活动名称（Activity Name）、事件名称（Event Name）、目标（Destination）和 Folio 进行过滤。对于每种过滤器，你可以指定搜索类型。要查看未过滤的任务列表，请将所有标准留空并点击“Find”（查找）。

管理员可以对选定的任务采取三种操作：

- Delegate（委托）
- Redirect（重定向）
- Release（释放）

委托任务允许额外用户查看并对任务项执行操作。执行委托：

1. 选择你想要委托的任务或多个任务，点击“Delegation”。这将弹出一个搜索界面，你可以在其中搜索要委托任务的用户。
2. 一旦你搜索并选择了委托用户，点击“Next”（下一步）。
3. 在下一个屏幕上，选择你想要委托给他们的操作，并点击“OK”完成委托操作。

重定向任务将从当前用户处移除任务，并将任务交给重定向用户。执行重定向：

1. 选择你想要重定向的任务或任务，点击“Redirect”。这将弹出一个搜索界面，你可以在其中搜索重定向的用户。
2. 一旦你搜索并选择了重定向用户，点击“OK”完成操作。

释放任务将把任务项的状态从“Open”（打开）/“Allocated”（已分配）更改为“Available”（可用）。这在限制目标槽场景下非常有用，此时任务不需要队列中的每个用户都完成——例如，当任务被分配给10个用户时，但只有这10个人中的1个需要完成该项。当第一个用户打开任务项时，该用户的任务状态将从“Allocated”更改为“Open”。对于其他用户，任务状态将变为“Allocated”，这实际上将其从他们的列表中移除。释放任务项将把项交回10个用户的队列，并允许另一个用户打开。你只能释放处于“Open”状态的任务。要执行释放操作，选择你想要释放的任务或任务并点击“Release”。

# SmartObject 服务管理

SmartObject 服务用于在 K2 平台与业务数据（无论是数据库还是业务系统中的）之间创建接口。因此，SmartObject 服务包含了可以连接到 Microsoft SQL Server、Oracle、Salesforce、Active Directory 以及通用 Web 服务的服务。这些服务是应用程序协议，为 K2 平台暴露其他应用程序的属性和方法。





# 第 15 章：服务器与组件管理

服务由服务实例（Service Instances）和服务对象（Service Objects）组成。服务实例代表业务对象，而服务对象代表业务对象的属性和方法。通过 K2 平台暴露的服务与其系统中可用的服务相同，不会重新创建。

某些服务在安装 K2 black 时自带。可以编写自定义服务与其他服务以及 LOB（线性业务）应用程序进行交互。请参考 K2 文档获取标准服务的详细列表以及如何编写自定义服务。

SmartObjects 是使用工作流控制台开发的（见图 15-17）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_585_0.png)

图 15-17

有关管理 SmartObject 更多信息，请参考第 10 章。

## 存档

数据库是 K2 black 环境中最关键组件。所有关于完成和运行流程的状态信息都存储在数据库中。此外，所有已部署流程定义和所有 SmartObject 定义也都存储在数据库中。有效恢复 K2 black 环境取决于能否恢复数据库。为数据库制定良好的备份策略至关重要。事实上，它是如此重要，以至于我们专门分配了一个章节。更多信息请参阅第 18 章。

在本节中，我们将介绍存档，这是另一个主要的数据库维护任务。工作流引擎使用两个数据库：

- K2Server
- K2ServerLog

K2Server 数据库是事务数据库，活动和运行中的流程实例位于其中。K2ServerLog 数据库正如其名，是日志数据库，存储所有流程实例的报告。关注日志数据库：与事务数据库不同，随着更多流程实例的运行，日志数据库随时间持续增长。在某一点，你将耗尽数据库空间，或者由于数据库的大小导致报告性能下降。在这两种情况下，答案都是存档。

存档过程相当简单。你需要做的第一件事是在 K2ServerLog 数据库所在的数据库服务器上创建一个空数据库。你可以在存档后移动存档数据库，存档过程要求该数据库必须位于同一台服务器上。

> 为存档流程创建新数据库将要求你将此数据库添加到灾难恢复计划中。有关此的更多信息，请参阅第 18 章。

现在你已经创建了存档数据库，可以导航到工作区管理控制台（Workspace Management console）中 Workflow server 下的 Archiving 应用程序。

应用程序首先询问如何连接到存放 K2ServerLog 和存档数据库的数据库服务器。提供服务器名称和凭据，并点击 OK。

设置存档时，选择你的 K2ServerLog 数据库，为存档实例提供日期范围，并选择存档数据库。空的存档数据库将更新正确的表和结构。在数据库格式化正确后，你可以点击 Archive（存档）执行存档任务。根据存档数据量，此过程可能需要一些时间。最好在非工作时间执行此任务，因为可能会降低性能。

将存档数据还原到主数据库的过程与存档完全相同，只是你需要点击 Restore（还原），这会将日期范围报告信息从存档数据库中取出并放回标准报告数据库。

## Workspace Web 应用程序管理

Workspace（工作区）是 K2 blackpearl 的开箱可用界面。第 20 章将向你介绍 K2 blackpearl 接口的各个部分，并展示如何利用 Workspace 功能。本节的目的是理解保持 Workspace 应用程序运行所需的管理任务。

K2 blackpearl Workspace 是一个运行在 Microsoft 信息服务（IIS）上的 .NET 2.0 应用程序，并利用 AJAX 技术提供丰富的用户体验。

Workspace 应用程序是在 K2 blackpearl 安装时作为配置的。然而，作为管理员，了解某些配置设置是非常重要的，以防以后需要进行手动配置。

Workspace 应用程序本身的所有管理都是通过 IIS 完成。你可以点击“开始”并导航到“管理工具”来访问 IIS 管理工具。在这里找到 IIS 管理器。

Workspace 应用程序的位置取决于安装期间使用的设置，默认位置位于 Default Web Site（默认站点）下。要访问 Workspace 应用程序设置，右键点击树视图中的 Workspace 节点并选择 Properties（属性）。这将打开 Workspace 属性对话框。

Virtual Directory（虚拟目录）选项卡有几个设置。这些设置在下表中描述。

| 设置 | 说明 |
| :--- | :--- |
| Local Path（本地路径） | 此设置指向 K2 blackpearl 安装路径下的 Workspace Site 目录。 |
| Application Name（应用程序名称） | 指定应用程序名称，如果更改会影响指向 Workspace 站点的 URL 链接。 |
| Execute Permissions（执行权限） | 此指定执行权限，应始终设置为 Scripts and Executables（脚本和可执行文件），以确保 Workspace 功能正常。 |
| Application Pool（应用程序池） | 指定 Workspace 运行所在的应用程序池。我们将更深入地讨论应用程序池。Workspace 的默认应用程序池是 K2 blackpearl 应用程序池。 |

在 Directory Security（目录安全）选项卡上，确保 Authentication and Access Control（身份验证和访问控制）配置正确。点击 Authentication and Access Control 下的 Edit（编辑）查看详情。

使用 Active Directory 作为默认身份验证程序时，Workspace 的正确配置是仅勾选 Integrated Windows Authentication（集成 Windows 身份验证）。如果勾选 Enable Anonymous Access（匿名访问），会导致身份验证问题，因为 Workspace 将无法应用任何策略。

ASP.NET 选项卡允许管理员更改应用程序使用的 .NET 框架版本。Workspace 是 .NET 2.0 应用程序，应该始终选择该框架。

除了 IIS 中的设置外，还有一个与 Web 应用程序相关的配置文件 (web.config)，它存储在安装目录下的 Workspace site 文件夹中。常规管理不需要编辑 web.config 文件，但该文件包含一组环境密钥和连接字符串，指向报告服务器、K2 服务器服务、K2 Web 服务、K2 SQL 数据库以及 Active Directory。如果有影响这些组件位置的环境变化，你需要手动编辑 web.config 或重新运行 K2 blackpearl Configuration Manager。

## Runtime Services 管理

一组 Web 服务也随 K2 blackpearl Workspace 一起安装并位于 IIS 中的 Runtime Services 下（见图 15-18）。这些服务对于 Microsoft InfoPath 和 Microsoft Office SharePoint Server 的集成至关重要，并为 Forms Generation Event Client 和出差功能提供其他功能。

Web 服务应用程序的设置应与 Workspace 应用程序设置相同，但 Local Path 应指向 K2 blackpearl 安装文件夹下的 WebServices/RuntimeServices 目录。

## 第 15 章：服务器与组件管理

Web 服务应用程序在运行时服务（Runtime Services）目录下也有一个配置文件 (web.config)。常规管理不需要编辑 web.config，但其中有三项关于 InfoPath 集成的设置可以通过此配置进行设置：

- 异步提交（Submit Asynchronously）：这是一个标志，用于设置 InfoPath 提交操作应该是同步还是异步的。

