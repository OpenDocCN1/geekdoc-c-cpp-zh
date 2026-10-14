

顺便说一下，ASP.NET 4 的应用程序服务器可以处理由 ASP.NET 2.0、3.0 和 3.5 开发的 Web 窗体的请求，也可以处理由 ASP.NET 4 开发的窗体的请求。这意味着你不必将旧应用程序转换为 ASP.NET 4。需要注意的是，在 IIS 7 下，由 ASP.NET 2.0、3.0 或 3.5 开发的窗体必须与由 ASP.NET 4 开发的窗体在不同的应用程序池中运行。

## ASP.NET 应用程序中状态的处理方式

尽管在前面的图中并不明显，但应用程序在生成网页后即结束。这意味着应用程序维护的任何数据，例如变量或控件属性的当前状态，都会丢失。换句话说，HTTP 不维护应用程序的 *state*。这在图 1-5 中有所说明。

在这里，你可以看到客户端上的浏览器向 Web 服务器请求一个页面。服务器处理请求并将页面返回给浏览器后，会断开连接。然后，如果浏览器发出额外的请求，服务器就没有办法将浏览器与其之前的请求关联起来。正因为如此，**HTTP** 被称为 *stateless protocol*。

尽管 HTTP 不维护状态，但 ASP.NET 提供了几种方法来实现这一点，如本图所示。首先，你可以使用 *view state* 来维护服务器控件属性的值。例如，你可以使用 view state 来保留在 Web 窗体处理过程中被更改的标签控件的 Text 属性，或维护下拉列表中的项目列表。由于 ASP.NET 默认实现了 view state，因此你无需编写任何特殊代码即可使用它。

其次，你可以使用 *session state* 在应用程序的执行之间维护数据。为此，ASP.NET 会在用户开始新会话时在服务器上创建一个 *session state object*。该会话对象包含一个唯一的 *session ID*，并且每次用户请求页面时，该 ID 都会在服务器和浏览器之间来回传递。然后，当服务器收到用户的新的请求时，它可以为该用户检索正确的会话对象。在你的 Web 窗体的代码中，你可以将数据项添加到会话对象中，以便每次执行 Web 窗体时其先前的值都可用。

第三，你可以使用 *application state object* 来保存 *application state* 数据，该数据适用于应用程序的所有用户。例如，你可以使用应用程序状态来维护全局计数器，或维护当前登录到应用程序的用户列表。

第四，你可以使用 *profile feature* 来跟踪用户数据。尽管配置文件与会话状态对象类似，但它在用户会话之间保持持久，因为它存储在数据库中。当你使用配置文件时，例如，你可以跟踪用户在上次会话中查看的最后三个产品。然后，当用户开始新会话时，你可以在“最近查看的项目”列表中显示这些产品。由于配置文件使用频率不高，我将在本书中不介绍它们。

## 为什么在 Web 应用程序中跟踪状态很困难

![](img/c024ccf88e28c30c07dd410d4342288f_32_0.png)

### Concepts

- *State* 指的是应用程序为单个用户维护的属性、变量和其他数据的当前状态。应用程序必须为当前访问应用程序的每个用户维护单独的状态。
- HTTP 是一个 *stateless protocol*。这意味着它不会在往返之间跟踪状态。一旦浏览器发出请求并收到响应，应用程序就会终止，其状态就会丢失。

### Four ASP.NET features for maintaining state

- ASP.NET 使用 *view state* 来维护应用程序在执行之间更改的窗体控件属性的值。由于 view state 默认实现，因此不需要特殊编码。
- 当用户开始新会话时，ASP.NET 会创建一个包含 *session ID* 的 *session state object*。该 ID 从服务器传递到浏览器再传回服务器，以便服务器可以将浏览器与现有会话关联起来。要维护 *session state*，你可以将程序值添加到会话状态对象中。
- 当应用程序开始时，ASP.NET 会创建一个 *application state object*。要维护 *application state*，你可以将程序值添加到应用程序状态对象中。这些值在应用程序结束之前可供应用程序的所有用户使用。
- ASP.NET 还可以为应用程序的每个用户维护一个 *profile*。由于配置文件存储在数据库中，因此配置文件数据在用户会话之间得以维护。这使得个性化应用程序变得更容易。

## ASP.NET 应用程序开发简介

在接下来的三个主题中，你将了解到开发 ASP.NET Web 应用程序所需的软件、.NET Framework 的组件是什么，以及你可以使用的开发环境。

### The software you need

图 1-6 中的第一个表格总结了开发 ASP.NET 应用程序所需的客户端和服务器软件。在你自己的 PC 上，你需要像 Windows XP、Windows Vista 或 Windows 7 这样的操作系统、Microsoft .NET Framework 4，以及像 Microsoft Internet Explorer 这样的浏览器。如果你想从使用该集成开发环境（IDE）中获益，你还需要 Visual Studio 2010。

如果你使用服务器进行开发，它将需要像 Windows Server 2003 或更高版本这样的服务器操作系统、Microsoft .NET Framework 4 和 Internet Information Services。如果你要从远程计算机开发应用程序，它还需要 FrontPage Server Extensions。而如果你要为 Internet 开发应用程序，它还需要一个 FTP 服务器。在附录 A 中，你可以获取有关为客户端和服务器安装软件的信息。

由于大多数 ASP.NET 应用程序需要数据库访问，因此你还需要一个数据库服务器，例如 Microsoft SQL Server。对于在你自己的 PC 上的开发工作，你可以使用 SQL Server 2008 Express Edition，它是随 Visual Studio 2010 提供的 SQL Server 的精简版。但对于生产应用程序，你可能需要在服务器上使用 SQL Server 本身。

如果你正在开发生产应用程序，你还应该在 PC 上下载并安装其他 Web 浏览器，包括 Mozilla Firefox 和 Chrome。这样，你就可以使用各种流行的浏览器测试你的应用程序。

该图中的第二个表格显示 Visual Studio 2010 有多个版本。大多数专业开发人员将使用 Professional Edition 或 Premium Edition。但大型开发团队可能会使用 Ultimate Edition，其中包含为架构师、开发人员和测试人员等专业开发角色设计的特性。

一个免费的替代方案是 Visual Web Developer 2010 Express Edition。该产品面向个人开发人员、学生和业余爱好者设计，本书中的大多数功能都适用于此版本。

## Software requirements for ASP.NET 4 application development

| Client | Server |
| :--- | :--- |
| Windows XP or later | Windows Server 2003 or later |
| Microsoft .NET Framework 4 | Microsoft .NET Framework 4 |
| A browser like Internet Explorer (6.0 or later) | Internet Information Services 6.0 or later |
| Visual Studio 2010 | Microsoft SQL Server or equivalent database server |
|  | FrontPage Server Extensions (for remote development only) |

## Visual Studio 2010 Editions

| Edition | Description |
| :--- | :--- |
| Visual Web Developer 2010 Express Edition | Free, downloadable edition for Web development in Visual Basic or C#. There is also an Express Edition of SQL Server called SQL Server 2010 Express. |
| Visual Studio 2010 Professional Edition | Designed for individual developers who want to build a wide variety of Windows, Web, mobile, and Office-based solutions. |
| Visual Studio 2010 Premium Edition | Designed for individuals and teams who want to build scalable applications and includes standard testing tools, database deployment and change-management tools, and basic lifecycle management tools. |
| Visual Studio 2010 Ultimate Edition | Designed for teams and includes full testing, modeling, database, and lifecycle management tools. |

### Description

- 要开发 ASP.NET 4 应用程序，你需要在自己的 PC 上安装上面显示的客户端软件。此外，如果你没有单独的服务器可用，你通常还需要 IIS 和数据库服务器，例如 SQL Server 2008 Express Edition。有关更多信息，请参阅图 1-8。
- Visual Studio 2010 有四个不同的版本，提供开发 ASP.NET 应用程序所需的所有基本功能。你选择的版本取决于你需要的额外功能。

