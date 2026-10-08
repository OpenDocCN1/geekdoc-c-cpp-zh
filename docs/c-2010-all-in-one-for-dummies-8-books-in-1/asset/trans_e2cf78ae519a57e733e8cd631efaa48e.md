

## 492 拆解项目

- WPF 用户控件库：这种松散控制格式的最终产品不会出现在工具箱中，但构建起来要容易得多，因为不需要用 C# 编写整个代码。

- Windows Forms 控件库：类似于 WPF 控件库，但用于 Windows Forms。它可以帮助你构建一个可以从工具箱中使用的控件。

- Web 项目：Web 项目是需要服务器运行（通常情况下是这样）并从浏览器使用的程序。它们向浏览器渲染 HTML，而不是像 Silverlight 那种花哨的格式。项目包括：

- ASP.NET Web 应用程序：这是 Web 开发领域的核心。它创建了一个可以在 IIS 上运行的应用程序，并向用户呈现 Web 页面。

- ASP.NET 服务应用程序：这是一个用于面向服务应用程序的类库。如果你打算在几台机器上分发应用程序，或提供广泛分布的应用程序，你的项目类型将为你的服务提供基于标准的实现。

- ASP.NET AJAX 服务器控件：异步 JavaScript 和 XML（AJAX）是一种开发风格，可以在 Web 浏览器中提供大量的用户交互。这允许你构建支持这种模式的控件。

- WCF 服务应用程序：此项目属于通信基础（Communication Foundation）部分。它类似于 ASP.NET Web 服务应用程序，不同在于它为你的服务提供了多种不同的基于标准的实现。ASP.NET Web 服务仅提供一种。

- ASP.NET 服务器控件：此控件会出现在工具箱中，允许你在开发时将选择功能直接拖到 Web 页面。

- ASP.NET AJAX 服务器控件扩展器：此控件扩展了另一个 AJAX 控件的功能。它针对某个控件并添加特性。

- Dynamic Data Linq to SQL 应用程序：这是一个使用 Linq 创建数据交互 Web 页面的 ASP.NET Web 应用程序。

- Dynamic Data Entities Web ：此 ASP.NET 应用程序使用 ADO.NET Entities 创建数据交互 Web 页面。

- Office 项目：Office 项目是 Visual Studio Tools for Office 软件包的一部分，它们使用 Office 作为平台而不是 Windows 或 Web 浏览器。要了解更多信息，请参阅我与 Peter Jaunovich 合著的书籍《Office 傻瓜》。Office 项目包括：

- Excel 2007 工作簿：以 Microsoft Excel 工作簿（Excel 表格集合）作为输出。

- Word 2007 模板：以 Microsoft Word 2007 模板（.dot 文件）作为输出。

- Project 2007 插件：为 Microsoft Project 创建插件。

- Visio 2007 插件：为 Microsoft Visio 创建插件。

- Word 2007 插件：为 Microsoft Word 创建插件。

- Excel 2007 插件：为 Microsoft Excel 创建插件。

- Outlook 2007 插件：为 Microsoft Outlook 创建插件。

- Word 2007 文档：以 Microsoft Word 2007 文档作为输出。

- Excel 2007 模板：以 Microsoft Excel 2007 模板（.xlt 文件）作为输出。

- InfoPath 插件：为 Infopath 创建插件。

- PowerPoint 2007 插件：为 Microsoft PowerPoint 创建插件。

**通信基础项目 (Communication Foundation Projects)：** Windows Communication Foundation 是微软提供的一种机制，用于让程序之间进行通信：

- 订阅分发服务库：创建一个支持 ATOM 或 RSS 的馈送服务 (RSS)。

- WCF 服务库：用于通信基础的类库。

- 声明式流程图服务库：创建一组使用流程图工作流来提供服务。

**工作流项目 (Workflow Projects)：** Foundation Workflow 是微软程序中创建工作流的标准库。你可以设置标准的审批、文档移动等功能：

- 活动设计器库：此项目帮助你创建一个用于创建活动的用户界面。

- 活动库：如果你没心情为创建活动去创建用户界面，你可以创建一个活动库。

- 流程图工作流控制台应用程序：此项目（以及顺序工作流项目）提供了一种在安全环境中测试 WF 工作流的方法。

- 顺序工作流控制台应用程序：这与流程图 WF 项目一样，但用于顺序工作流。

**特殊项目 (Special Projects)：** 指任何不符合前述项目符号列表的项目：

- 测试项目：如果你在 Visual Studio 中工作，右键点击一个方法并选择“创建单元测试”，你就会得到这种项目。如果你想手动创建一个测试项目，这就是你的项目。

- Silverlight：诚然，Microsoft Expression 是你使用 Silverlight 的最佳选择。但是，如果你想使用 Visual Studio，可以使用此项目。

- SQL Server 项目：再次，我会使用 Microsoft SQL Server Management Studio 来管理数据库项目。如果出于某些原因必须使用 Visual Studio，那么这就是你的项目。

- 报告应用程序：你可以将报告直接包含在 Windows 或 Web 应用程序中。如果你直接部署到报告服务（Reporting Services），此项目就能胜任。

**其他类型的项目：** 创建一种项目类型很容易，而且有很多种类。其中一些是模式，一些是语言，另一些是新的输出格式：

- ASP.NET MVC：模型-视图控制器 (MVC)，一种允许开发团队之间实现职责分离的项目类型。搜索 MSDN 了解更多信息。

- MVC4WPF：允许为 Windows Foundation 进行模型-视图控制器开发。它拥有与普通应用程序一样的模板。可以在 www.mvc4f.com 查看。

- IRONRuby：在 Visual Studio 中的 Ruby 实现。

- IRONPython：在 Visual Studio 中的 Python 实现。

## 第 2 章：使用界面

本章内容

- 使用设计器
- 探索解决方案管理器
- 使用代码视图进行编码
- 使用工具菜单

集成开发环境（IDE）是程序员工具箱中的“瑞士军刀”。IDE 提供了一种用于存储程序代码、组织和构建代码，以及通过设计编辑器查看产品的机制。IDE 让事情变得，并作为回报节省了数小时的时间。

