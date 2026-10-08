

# .NET 架构的服务

.NET Framework 不仅提供基础设施，还为开发者提供可靠的架构服务。.NET Framework 的这些部分具有重大的价值和内容，有助于多层架构的开发。通过它们，你可以构建健壮且可扩展的应用程序，同时保留 .NET Framework 的简单性和灵活性。

.NET Framework 的服务非常广泛且丰富，以至于关于每一项服务都可以写一整本书。然而，以下章节提供了最重要组件的简要总结。

## ASP.NET

ASP.NET 用于开发 Web 应用，能够支持各种架构层——从 UI 到基于 Web 业务功能。ASP.NET 是 .NET Framework 最复杂的部分之一。

## Windows Forms

所有富客户端（rich clients）都需要对话框、表单、用户消息和复合 UI 元素等。.NET Framework 提供了 Windows Forms 来实现这一目标。借助对象层次结构，可以非常简单地管理 UI 元素，并通过简单的继承创建新的视觉组件。

## Web 服务 (Web Services)

在软件技术演进过程中，平台和系统之间的集成一直非常重要。有了 .NET Framework，Web 服务变得非常流行，成为系统集成（即使在不同平台之间）的一种易用技术。

## ADO.NET

ADO.NET 是一组可以访问数据和数据服务的 .NET 组件。它通常用于访问和修改关系型数据库中的数据，也可以用于访问其他结构化数据源（通过 ADO.NET 提供程序）。

## Workflow Foundation (Workflow Foundation, WF)

自 .NET Framework 3.0 发布以来，Workflow Foundation（WF）提供了工作流定义和执行的基础设施。在 WF 的帮助下，开发者可以定义以下两种工作流：

- 序列（Sequence）：过程步骤按时间顺序排列。
- 状态机（State machine）：过程是一组状态，这些状态之间的步骤是基于事件的。

WF 具有作为人类自动化工作流基础的能力。

## Windows Communication Framework (WCF)

自首次发布以来，.NET Framework 就包含了特殊的基础服务（例如 .NET 远程调用、Web 服务和队列管理），为分布式系统的组件之间提供通信。在 WCF 之前，开发者必须在实现期间决定为特定解决方案使用哪种技术。

WCF 发布于 .NET 3.0，为分布式组件之间的通信提供了统一解决方案，并允许在不重新编译项目的情况下更改通信通道的行为和运行时属性。

## Windows Presentation Framework (WPF)

随着 Windows Vista 的推出，微软重新定义了计算机图形子系统的概念，并提供了一种最大化图形处理器能力的全新解决方案。在此背景下，WPF 作为 Vista 和 .NET Framework 3.0 的一部分发布。

WPF 包含了全新的 UI 概念和开发方法。WPF 可以在物理上分离视觉设计和行为，允许程序员编写功能代码，允许设计师创建 UI。

## CardSpace

身份形而学（identity metaphysics）概念是存储和处理数字 ID 的统一平台。.NET Framework 3.0 的 CardSpace 是这一概念的重要部分，提供了使用数字 ID 的安全方法。

如今，每个人都有无数数字 ID（例如各种网站注册）。当然，CardSpace 不仅存储这些 ID，还为操作和事务提供了统一的接口。

## Entity Framework

.NET Framework 3.5 中的 ADO.NET 较于以前显著超过了以前的数据管理方法。ADO.NET 的形式在关系型数据库之上建立了一个抽象层，提供了使用存储在各种数据库中的数据进行统一方法。

Entity Framework 将这种抽象引入了概念层面。借助对象关系映射（ORM）技术，它提供了一种管理高层实体而非数据库表和关系的方法。

# .NET Framework 的主要优势

以下是 .NET Framework 提供的一些主要优势：

- 安全的多语言开发平台 —— .NET 是为开发者和 IT 专业人员提供的一种强大且可靠的技术，因为它在安全、管理和更新方面提供了更强大的能力，并且在构建、测试和部署可靠安全的软件方面也是如此。.NET 提供了一个真正的多语言开发者平台，让开发者可以使用他们偏好的语言进行工作。CLR 为静态语言（例如，VB 和 C#）提供支持，但也支持动态语言（例如，IronRuby 和 Managed Jscript）。
- 下一代体验 —— WPF 为构建具有 UI 的富应用程序（rich applications）提供了一种统一的方法。WPF 为二维和三维图形、硬件加速效果、可扩展性、交互式可视化和卓越的内容可读性提供了支持。此外，设计师可以借助文件格式 XAML 成为开发过程的活跃组成部分。
- 跨浏览器、跨平台、跨设备 —— .NET Silverlight 中的另一种 UI 的 工具，它帮助开发者创建跨浏览器、跨平台、跨设备的插件，用于创建下一代丰富的、交互式的应用程序。
- 高级 Web 开发 —— .NET 为 Web 开发提供了一种免费、先进的技术。ASP.NET 可以是开发者手中从小型个人网站到大型企业 Web 应用的优选工具。此外，ASP.NET 异步 JavaScript 和 XML (Ajax) 允许开发者在所有流行的浏览器上创建更高效、更丰富的 Web UI。
- 安全且强大的 Web 服务 —— WCF 为开发具有可扩展架构、安全通信、消息模式等的真实分布式系统提供了许多功能。
- 业务过程 —— 作为 .NET Framework 的一部分，WF 可用于以更高效的方式开发业务过程，从而提高开发者和最终用户的生产力。
- 灵活的数据访问选项 —— 带有 Entity Framework 和 ADO.NET Data Services 的 ADO.NET 为开发分布式的、以数据为中心的应用程序提供了丰富的组件集。ADO.NET 支持许多通用开发需求，包括多层应用程序的创建。Entity Framework 通过为任何数据库提供统一模型简化了数据访问，并使该模型能够反映业务需求。ADO.NET Data Services 为下一波互联网应用程序提供了顶级基础设施。

# 总结

本章让你一览展示了 .NET Framework 的历史和演进。在章节早期，你学习了 .NET Framework 最重要的前身，包括 Win/Win32 编程、C++ 编程、Visual Basic 编程、Delphi 编程和 COM 编程。

.NET Framework 的演进是以前开发者工具和语言缺陷的结果，它添加了新的架构和许多新功能。.NET Framework 的主要目标是一个独立的运行时环境、整洁的面向对象基础、语言之间的完全集成、与现有编程范式的完全互操作性、无需管线代码、简单的部署模型、开箱即用的基础对象以及通用的安全模型。

基于这些目标，.NET Framework 1.0 在 2002 年诞生。从那时起发布了许多新版本，越来越多的新功能回答了不断更新的开发者需求。本章简要回顾了从 1.0 到当前的 4.0 的所有 .NET Framework 版本，并讨论了它们每个的主要功能。

你还学习了 .NET Framework 架构以及所有的 .NET Framework 服务。

第 8 章将详细介绍 .NET Framework 4.0 的组件。

