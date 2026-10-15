

意味着一旦页面在 WebBrowser 控件的 HTML 容器中加载，如果在此过程中 URL 发生变化，则新的 URL 将显示在文本框中。例如，如果你采用这些步骤并导航到 Wrox 网站（www.wrox.com），页面的 URL 将立即更改为 http://www.wrox.com/WileyCDA/。此过程还意味着如果最终用户点击 HTML 视图中包含的其中一个链接，则新请求页面的 URL 也将显示在文本框中。

现在如果在进行了上述更改后运行应用程序，窗体的标题和地址栏将像在 Microsoft 的 Internet Explorer 中一样工作，如图 29-11 所示。

![](img/d99870e80390742f93963da7be0b2e61_980_0.png)

FIGURE 29-11

### SUMMARY

直接对网络进行编程提供了很大的功能和灵活性。当然，所有这些功能和灵活性都伴随着成本。许多内置于更高层技术中的服务，例如 Web 服务或远程处理，并未内置于 WebRequest 或 Socket 类中，通常必须重新创建。然而，在必须与现有应用程序通信或需要终极控制和速度的情况下，使用 System.Net 命名空间中的类会使生活比否则更容易。

本章研究了许多公开网络编程的类。你已经学习了如何在没有浏览器的情况下进行 Web 请求，以便在应用程序中使用 Internet 上的数据；你已经看到如何利用裸套接字层来编写自己的通信协议，并且你已经了解了 Visual Basic 2010 中用于创建 FTP 客户端和 Web 服务器的一些类。

## 30 Application Services

### WHAT YOU WILL LEARN IN THIS CHAPTER

- Choices for implementing application services
- Characteristics of one of the most common technologies for application services, namely Windows Services
- How to interact with a Windows Service using Visual Studio 2010 and the management applets in the Windows Control Panel
- How to create, install, and communicate with a Windows Service using Visual Basic
- How to debug a Windows Service from within Visual Studio 2010

现代多任务操作系统通常需要运行在后台运行且独立于已登录用户的应用程序。例如，提供服务接口以获取数据的应用程序需要服务外部的数据请求，而不管是否有当前用户。

随着时间的推移，实现应用程序服务的选择数量有所增加。最初，主要选择是 Windows Services，但随着 .NET 和 Windows 的发展，其他选择也被添加。

### USING IIS FOR APPLICATION SERVICES

根据所使用的 Windows 版本和已安装的 Windows 选项，有多种方法可以在后台托管 .NET 程序。第 14 章涵盖了 Web 服务和 Windows Communication Foundation（WCF）服务，两者都是可使用 Internet Information Services（IIS）加载程序并使其独立于用户运行的技术示例。

如果你使用的是 IIS 7.0 或更高版本，你还可以使用 Windows Process Activation Service（通常称为 WAS）运行 WCF 服务。这允许使用非 HTTP 协议（如 TCP）托管 WCF 服务。与 IIS 一样，无需编写代码；只需要适当的配置。

另一种提供对后台程序何时以及如何加载更多控制的选项称为 Windows Services。基本概念可以追溯到 Windows NT，当时该功能称为 NT Services，但名称在 Windows 2000 及更高版本中已更改。它需要特殊的安装程序；只需点击编译好的 Windows 服务 EXE 就不会运行它。程序必须在操作系统的特殊上下文中运行，并且需要特定的安装过程来执行 Windows Service 在此特殊上下文中运行所需的配置。

### INTERACTING WITH WINDOWS SERVICES

你可以通过打开服务控制管理器用户界面来查看计算机上使用的服务。要在 Windows 2000 中执行此操作，请在控制面板中选择 管理工具 ⇨ 服务。在 Windows XP Professional 中，选择 开始 ⇨ 所有程序 ⇨ 管理工具 ⇨ 服务。在 Windows Vista 中，选择 开始 ⇨ 控制面板 ⇨ 系统和维护 ⇨ 管理工具。在 Windows 7 中，选择 开始 ⇨ 控制面板 ⇨ 管理工具 ⇨ 服务。

使用服务控制管理器，可以将服务设置为在系统启动时自动启动，或手动启动。服务也可以停止或暂停。服务控制管理器中包含的服务列表包括每个服务的当前状态。图 30-1 显示了 Windows Vista 中的服务控制管理器。

![](img/d99870e80390742f93963da7be0b2e61_983_0.png)

FIGURE 30-1

状态列指示服务的当前状态。如果此列为空，则自上次计算机启动以来服务尚未启动。状态的其他可能值是 Started、Stopped 和 Paused。你可以通过双击它来访问有关服务的其他设置和详细信息。

当服务启动时，它会自动使用以下帐户之一登录到系统：

- User account — 一个允许程序与系统交互的常规 Windows 帐户；本质上，服务冒充一个用户。
- LocalSystem account — 不与特定用户关联。此内置帐户具有很多特权，可以大致认为是服务的管理员帐户的等价物。
- LocalService account — 不与特定用户关联。此内置帐户具有更有限的特权，通常用于常规服务。
- NetworkService account — 不与特定用户关联。此内置帐户与 LocalService 类似，但专为在本地网络上通信而非仅在本地系统上工作的服务而设计。

图 30-1 中显示的服务控制管理器是操作系统（OS）的一部分，即支持 Windows Services 的部分；它不是 .NET Framework 的一部分。由 OS 运行的任何服务都通过服务控制管理器公开，无论服务是如何创建或安装的。你还可以通过 Visual Studio 2010 中的服务器资源管理器检查已安装的 Windows Services。

### CREATING A WINDOWS SERVICE

在 .NET 中创建 Windows Service 需要使用几个 .NET 类，它们提供 Windows Service 所需的操作系统接口。

### The .NET Framework Classes for Windows Services

创建 Windows Service 需要几个基类：

- System.ServiceProcess.ServiceBase — 为 Windows Service 提供基类。将在服务中运行的逻辑的类继承自 ServiceBase。单个可执行文件可以包含多个服务，但可执行文件中的每个服务都是继承自 ServiceBase 的单独类。
- System.Configuration.Install.Installer — 这是一个执行各种组件安装任务的通用类。Windows Service 进程中的一个类必须继承并扩展 Installer，以便在各种 Windows 操作系统下提供安装服务的必要接口。

每个继承自 Installer 的类都需要包含以下每个类的实例：

- System.ServiceProcess.ServiceProcessInstaller — 此类包含安装包含 Windows Services 的 .NET 可执行文件所需的信息（即包含继承自 ServiceBase 的类的可执行文件）。用于 Windows Services 的 .NET 安装实用程序（InstallUtil.exe，后面会讨论）调用此类以获取执行安装所需的信息。
- System.ServiceProcess.ServiceInstaller — 此类也与 InstallUtil.exe 安装程序交互。而 ServiceProcessInstaller 包含将整个可执行文件安装为服务所需的信息，ServiceInstaller 包含可执行文件中特定服务的有关信息。如果可执行文件包含多个服务，则每个服务都需要一个 ServiceInstaller 实例。

对于你开发的大多数 Windows Services，你可以让 Visual Studio 2010 处理 Installer、ServiceProcessInstaller 和 ServiceInstaller。你只需要设置几个属性。你应该彻底理解的类是 ServiceBase，因为这是包含 Windows Service 基本功能的类。

### The ServiceBase Class

ServiceBase 类包含几个有用的属性和方法，但最初更重要的是了解当服务状态发生变化时由服务控制管理器触发的方法。表 30-1 描述了其中最重要的这些方法。

**TABLE 30-1: Important ServiceBase Events**

| EVENT | DESCRIPTION |
| --- | --- |
| OnStart | 在服务启动时发生。这是通常放置服务初始化逻辑的地方。 |
| OnStop | 在服务停止时发生。清理和关闭逻辑通常放在这里。 |

