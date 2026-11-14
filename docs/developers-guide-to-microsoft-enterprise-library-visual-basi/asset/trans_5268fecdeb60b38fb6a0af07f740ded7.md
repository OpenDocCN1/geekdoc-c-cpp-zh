
- 对于数据访问应用程序块，还需要以下内容：
  - 运行受 .NET Framework 3.5 Service Pack 1 或 .NET Framework 4.0 数据提供程序支持的数据库的数据库服务器。这包括 Microsoft SQL Server® 2000 或更高版本、SQL Server 2005 Compact Edition 和 Oracle 9i 或更高版本。数据库服务器还可以运行受 .NET Framework 3.5 Service Pack 1 或 .NET Framework 4.0 针对 OLE DB 或 ODBC 的数据提供程序支持的数据库。

- 对于日志记录应用程序块，还需要以下内容：
  - 用于维护日志消息的存储。如果您使用 MSMQ 跟踪侦听器来存储日志消息，则需要安装 Microsoft Message Queuing (MSMQ) 组件。如果您使用数据库跟踪侦听器来存储日志消息，则需要访问数据库服务器。如果您使用电子邮件跟踪侦听器来存储日志消息，则需要访问 SMTP 服务器。

除此之外，您只需要一些空闲时间来坐下来阅读，并尝试示例程序。希望您会发现内容有趣（甚至可能很有趣味），并且是了解 Enterprise Library 的有用来源。

## 为您带来本指南的团队

**创意/愿景** Grigori Melnik
**主要作者** Alex Homer
**参与作者** Nicolas Botto、Bob Brumfield、Olaf Conijn、Grigori Melnik、Erik Renaud、Fernando Simonazzi 和 Chris Tavares。
**审阅者** Scott Densmore、Tom Hollander、Hernan de Lahtite、Ajoy Krishnamoorthy、Ade Miller 和 Don Smith。
**平面设计师** Patrick Lanfear 和 Tom Draper。
**编辑** RoAnn Corbisier 和 Nancy Michell。

## Enterprise Library 5.0 开发团队

**产品/项目管理** Grigori Melnik (Microsoft Corporation)。
**架构/开发** Bob Brumfield 和 Chris Tavares (Microsoft Corporation)；Fernando Simonazzi (Clarius Consulting)；Nicolas Botto (Digit Factory)；以及 Olaf Conijn (Olaf Conijn BV)。
**测试** Carlos Farre、Masashi Narumoto 和 Rohit Sharma (Microsoft Corporation)；Nicolas Botto (Digit Factory)；Lavanya Selvaraj、Magdelene Sona、Mani Krishnaswami、Meenakshi Krishnamoorthy、Santhosh Panneerselvam 和 Ravindra Varman (Infosys Technologies Ltd)；Erik Renaud 和 François Tanguay (nVentive Inc)；以及 Rick Carr (DCB Software Testing, Inc)。
**用户体验** Damon van Vessem、Heidi Adkisson、Jen Amsterlaw 和 Kelly Franzack (Blink Interactive)；以及 Brad Cunningham (Interknowlogy)。
**文档** Alex Homer (Microsoft Corporation) 和 Dennis DeWitt (Linda Werner & Associates Inc)。

**编辑/制作** RoAnn Corbisier 和 Steve Elston (Microsoft Corporation)；Nancy Michiel (Content Master Ltd.)；John Hubbard (Eson) Ted Brian Nevelen (Ballard Indexing Services) 以及 Patrick Lanfear 和 Tom Draper (Twist Creative LLC)。

**发布管理** Richard Burte (ChannelCatalyst.com, Inc.) 和 Jennifer Burch (DCB Software Testing, Inc.)

**行政支持咨询委员会** Tracy Emory (Microsoft Corporation)；Brian Button (Asynchrony Solutions)；Kyle Huntley (Avanade)；David Starr (Pluralsight)；Wallin Ludwik (Volvo)；Bill Wilder (Fidelity)；Andrej Golcov (Hermes SoftLab)；John Askew、Nicholas Blumhardt、Martin Bennedik 和 Serge Baranovsky (Independent)；Evgeny Sorokin 和 Ksenia Mukhortova (Intel)；Scott Nichols (Idaho Central)；Eng Chong Lim 和 Isabel Niu (McDonald's Corporation)；Aaron Hanks、Glenn Block、Hugo Batista、Jason Hogg、Jason Olson、John Czerneszka、Josh Joseph、Lenny Fenster、Massimo Mascari、Matthew Podwysocki、Tom Hollander、Piyush Gupta 和 Scott Densmore (Microsoft Corporation)；Matthew Buonomo 和 Nikolar Malovic (Monster.com)；Daniel Piessens 和 Phill Van Hoven (Red Prairie)；以及 Walter Wu (Royal Bank of Canada)。

**社区** 在 patterns & practices 峰会、PDC、TechReady 和 TechEd 会议上提供非正式反馈的与会者；以及在 CodePlex 上、通过我们的博客、调查和电子邮件对本指南发表评论的 Enterprise Library 用户。

谢谢！

## 欢迎使用库

## 会见管理员

在开始探索 Microsoft® Enterprise Library 及其包含的奇妙功能和机会范围之前，您需要会见管理员。有时我们称他为 Tom，有时称他为 Chris，有时称他为 Grigori。但是，尽管名称有些令人不安的变化，他——与行业和其他内部 Microsoft 产品组的专家顾问委员会以及大量其他社区贡献者合作——是 Microsoft Enterprise Library 的守护者和保护者。

自其作为单个应用程序块的松散集合诞生以来，管理员一直在指导、推动、激励和鼓励他的团队，将其转变为一个全面、强大、易于使用且经过验证的代码库，该库可以帮助最大限度地减少设计和维护的痛苦，最大限度地提高开发效率，并降低成本。现在，在 5.0 版本中，它包含更多内置的优点，应该能让您的工作更轻松。甚至有可能，通过您节省的时间和精力，Enterprise Library 可以降低您的高尔夫差点，帮助您掌握滑雪场，让您与孩子共度更多时光，或者只是让您成为一个更好的人。但是，请注意，如果您最终只是看更多电视或发现自己其实有生活，作者、出版商及其员工不承担责任。

## 使用 Enterprise Library 获得的内容

Enterprise Library 由一系列应用程序块组成，每个块旨在管理特定的横切关注点。如果这个概念不熟悉，横切关注点是指您需要在应用程序的多个位置完成的那些烦人任务。在尝试管理横切关注点时，通常存在这样一种风险：您会在应用程序的每个位置为每个任务实现略有不同的解决方案，或者干脆完全忘记它们。将条目写入系统日志文件或 Windows® 事件日志、缓存数据以及验证用户输入是典型的横切关注点。虽然有几种方法可以管理它们，但 Enterprise Library 应用程序块可以集中管理。

什么是应用程序块？我们使用的定义是“可插拔且可重用的软件组件，旨在帮助开发人员解决常见的企业开发挑战。”应用程序块有助于解决开发人员从一个业务线项目到下一个项目时通常面临的问题。其设计封装了针对基于 Microsoft .NET Framework 的应用程序的 Microsoft 推荐做法，开发人员可以将它们添加到基于 .NET 的应用程序中，并快速轻松地进行配置。

除了应用程序块，Enterprise Library 还包含配置工具，以及一组管理适用于所有块的任务的核心功能。其中一些功能（例如处理配置和序列化的例程）已公开，可供您在自己的应用程序中使用。

而且，鉴于您需要学习如何使用比锤子或螺丝刀更复杂的任何新工具，Enterprise Library 包含一系列示例应用程序、每个块的关键场景描述、实验室以及全面的参考文档。您甚至可以获得团队在构建每个块时创建的所有源代码和单元测试（团队遵循测试驱动设计方法，先编写测试再编写代码）。因此，您可以了解其工作原理，了解团队如何遵循良好实践来创建它，然后如果您希望它做不同的事情，可以对其进行修改。图 1 显示了 Enterprise Library 的全景。

## Enterprise Library 全景

![](img/d7009d38323c3b86f2dfbc5155fbf141_22_0.png)

## 使用 Enterprise Library 可以做的事情

如果您查看已安装的文档，您会发现 Enterprise Library 今天实际上包含九个应用程序块。但是，实际上只有七个块“执行操作”——这些块被称为功能块。另外两个块涉及“连接事物”（连接块）。这实际上意味着，有七个块针对特定的横切关注点，例如缓存、日志记录、数据访问和验证。另外两个块（Unity 依赖注入机制和策略注入应用程序块）旨在帮助您实现更松散耦合、可测试且易于维护的系统。所有块中还使用了一些共享的核心组件。图 2 显示了这一点。

![](img/d7009d38323c3b86f2dfbc5155fbf141_23_0.png)

**图 2** Enterprise Library 的组成部分

在本书中，我们将专注于七个功能块。如果您想了解有关如何使用 Unity 和策略注入应用程序块的更多信息，请查看本指南的附录。它们更详细地描述了 Unity 作为依赖注入机制的功能以及策略注入的使用。

- **缓存。** 缓存应用程序块允许您在应用程序中集成本地缓存，该缓存使用内存缓存，并可选地使用数据库或独立存储后备存储。该块提供检索、添加和删除缓存数据所需的所有功能，并支持可配置的过期和清理策略。您还可以通过创建自己的可插拔
