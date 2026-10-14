
## 说明

- 要使用 WCF 服务，请为该服务创建客户端对象或代理。为此，请使用由定义服务的类名加上“Client”组成的类型。
- 创建服务对象后，可以使用与执行任何对象方法相同的技术来执行其操作。
- 为了更容易地使用服务，可以为包含服务的命名空间包含 using 语句。

## 展望

虽然本章介绍的 WCF 服务很简单，但它展示了你可以用来开发更大型 WCF 服务的技术。因此，你在这里学到的基本技能足以让你开始开发自己的 WCF 服务。此外，当需要时，你也将准备好学习 WCF 服务编程的更复杂方面。

例如，在部署 WCF 服务之前，你可能想了解更多关于配置其端点的信息，以改进服务的功能或安全性。或者，如果你想使用 REST 而不是 SOAP，可以学习更多关于创建支持 REST 的 WCF 服务的信息。或者，如果你不想使用网站作为 WCF 服务的宿主或客户端，可以了解更多关于提供和使用 Web 服务的其他选项。

* * *

在本书中，我们尽力呈现了开发电子商务 Web 应用程序所需的所有技能。现在，如果你已经阅读了全部 23 章，我们希望你觉得已经为此做好了充分准备。你还应该觉得，在开发 Web 应用程序时，你已经拥有了学习任何其他所需知识所需的概念、技能和视角。如果是这样，这本书就完成了它的任务。感谢你的阅读。

## 术语

- web service：Web 服务
- ASMX web service：ASMX Web 服务
- WCF (Windows Communication Foundation)：WCF（Windows 通信基础）
- service-oriented development：面向服务的开发
- service：服务
- provide a service：提供服务
- consume a service：使用服务
- WAS (Windows Process Activation Service)：WAS（Windows 进程激活服务）
- endpoint：端点
- SOAP (Simple Object Access Protocol)：SOAP（简单对象访问协议）
- binding：绑定
- MTOM (Message Transmission Optimization Mechanism)：MTOM（消息传输优化机制）
- TCP (Transmission Control Protocol)：TCP（传输控制协议）
- named pipes：命名管道
- MSMQ (Microsoft Message Queuing)：MSMQ（Microsoft 消息队列）
- metadata exchange (mex) binding：元数据交换（mex）绑定
- mex endpoint：mex 端点
- REST (Representational State Transfer)：REST（表述性状态转移）
- JSON (JavaScript Object Notation)：JSON（JavaScript 对象表示法）
- POX (plain old XML)：POX（普通旧 XML）
- operation：操作
- attribute：属性
- member：成员
- proxy：代理

## 附录 A

### 如何安装以及使用软件和可下载文件

要开发 ASP.NET 4 应用程序，你需要在 PC 上安装 Visual Studio 2010 或 Visual Web Developer 2010 Express Edition。这两款产品都包含一个开发 Web 服务器，可用于运行你的应用程序。然而，由于该服务器的限制，你还希望使用 IIS 测试你的应用程序。最简单的方法是在自己的 PC 上安装 IIS。

如果你要开发使用存储在自己 PC 而非远程服务器上的数据库的应用程序，你还需要在 PC 上安装 SQL Server。最简单的方法是安装 SQL Server 2008 Express Edition。事实上，当你安装大多数版本的 Visual Studio 2010 时，此版本的 SQL Server 默认会被安装。

本附录向你展示如何安装 Visual Studio 和 IIS。此外，它还展示如何安装 SQL Server 2008 Express Edition 以及如何创建本书中使用的 SQL Server 数据库。但首先，它描述了可从我们网站下载的本书文件，并向你展示如何下载、安装和使用它们。我们建议你在开始开发第一个 Web 应用程序之前阅读这些主题，以确保你拥有所需的所有软件和文件。

- 如何下载和安装本书的文件 .................................... 778
- 如何在 Windows 7 或 Windows Vista 下安装 IIS ................................ 780
- 如何在 Windows XP 下安装 IIS ................................................... 782
- 如何安装 Visual Studio 2010 ...................................................... 784
- 如何安装和使用 SQL Server 2008 Express ....................................... 786
- 如何创建 Halloween 数据库 .................................................. 788
- 如何使用下载的 Web 应用程序 ........................................... 790

### 如何下载和安装本书的文件

在整本书中，你会看到完整的应用示例来说明各章介绍的材料。为了帮助你理解这些应用程序的工作原理，你可以从我们网站 www.murach.com 下载这些应用程序的源代码和数据库。然后，你可以在 Visual Studio 中打开并运行它们。这些文件以单个下载包提供，如图 A-1 所总结。该图还描述了如何下载和安装这些文件。

当你下载单个安装文件并执行它时，它会将本书的所有文件安装到 C 盘的 `Murach\aspnet4_cs` 目录中。在此目录中，你会找到一个名为 `book_applications` 的目录，其中包含本书中的所有应用程序。你可以像图 A-7 中所述作为文件系统应用程序在 Visual Studio 中打开并运行这些应用程序。例外的是第 8 章和第 21 章的应用程序，它们必须在 IIS 下运行，因为它们使用应用程序状态，以及第 18 章的应用程序，它必须在 IIS 下运行，因为它需要数字安全证书。图 A-7 中也介绍了在 IIS 下运行文件系统 Web 站点的过程。有关应用程序状态的更多信息，请参阅第 8 章。有关数字安全证书的更多信息，请参阅第 18 章。

下载还包括本书前两部分部分应用程序使用的 Halloween 数据库的 Access 版本。由于 Access 数据库很小，我们已将其包含在每个使用它的应用程序的 `App_Data` 文件夹中，以便你可以毫无问题地运行这些应用程序。

要使用 Halloween 数据库的 SQL Server 版本，你需要使用 `C:\Murach\database` 目录中的 `create_database.bat` 和 `create_database.sql` 文件来创建数据库。你可能还需要使用该目录中的其他文件来授予 ASP.NET 访问数据库的权限。你将在图 A-6 中了解有关所有这些文件的更多信息。

为了帮助你练习在本书前三部分中学到的技能，我们在这些章节末尾提供了练习。我们还在 `C:\Murach\aspnet4_cs\exercise_starts` 目录中提供了许多这些练习的起点。当你执行安装文件时，`exercise_starts` 目录的内容将被复制到 `C:\aspnet4_cs` 目录（如果需要则创建该目录）。这使得你在完成练习时可以轻松找到练习起点。

#### 本书可下载的应用程序文件包含的内容

- 书中介绍的所有应用程序的源代码
- 这些应用程序中使用的 Halloween 数据库的 Access 和 SQL Server Express 版本
- 可用于处理 SQL Server Express 版本的 Halloween 数据库的文件
- 本书练习的起点

#### 如何下载和安装本书的文件

- 1. 前往 www.murach.com，并进入 *Murach’s ASP.NET 4 Web Programming with C# 2010* 的页面。
- 2. 点击“FREE download of the book applications.” 的链接。然后下载“All book files。” 这将下载一个名为 `a4cs_allfiles.exe` 的文件到你的 C 盘。
- 3. 使用 Windows 资源管理器在 C 盘上找到下载的文件。然后双击该文件并响应后续的对话框。这会将文件安装到以 `C:\Murach\aspnet4_cs` 开头的目录中。

#### 如何为练习准备你的系统

- 其中一些练习要求你从现有应用程序开始。这些应用程序的源代码位于 `C:\Murach\aspnet4_cs\exercise_starts` 目录中。安装文件安装下载中的文件后，它会运行一个名为 `exercise_starts_setup.bat` 的批处理文件，该文件将 `exercise_starts` 目录的内容复制到 `C:\aspnet4_cs` 目录。然后，你可以在像 `C:\aspnet4_cs\Ch01Cart` 和 `C:\aspnet4_cs\Ch04Cart` 这样的目录中找到所有练习的起点。

#### 如何为使用 SQL Server 数据库准备你的系统

- 要在你的 PC 上使用随书附带的数据库，你需要确保已按图 A-5 中所述安装 SQL Server 2008 Express。然后，你需要运行我们提供的批处理文件来创建数据库并将其附加到 SQL Server Express，如图 A-6 中所述。

#### 注意

- Halloween 数据库的 Access 版本包含在每个使用它的应用程序的 `App_Data` 文件夹中。

### 如何在 Windows 7 或 Windows Vista 下安装 IIS

当你从 Visual Studio 运行 ASP.NET Web 应用程序时，默认情况下它会在内置开发服务器下运行。因此，你不必安装 IIS 即可开发本书中的应用程序或运行从我们网站下载的应用程序（上一主题中所述的例外情况除外）。请记住，内置服务器有一些限制，你将在第 4 章中了解这些限制。正因为如此，你希望安装 IIS，以便彻底测试你开发的应用程序。（请注意，随 Windows Vista Home Basic 版和 Starter 版以及 Windows 7 Home Basic 版和 Starter 版提供的 IIS 版本无法配置为 ASP.NET 开发。因此，你必须使用随 ASP.NET 提供的开发服务器来测试你的应用程序，或者你需要访问单独的 Web 服务器。）

图 A-2 显示了如何在 Windows 7 或 Windows Vista 下安装 IIS。首先，你按此处所述显示 Windows 功能对话框。此对话框列出了所有可用的 Windows 功能。如果组件的所有功能都已安装，则该组件前面的复选框中会有一个勾号。如果仅安装了部分功能，则该组件的复选框将被着色。

要安装 IIS 的默认功能，你只需选中其框，然后单击确定按钮。如果想要安装除默认功能之外的其他功能，你可以展开 Internet Information Services 节点及其任何下级节点以选择所需的功能。默认情况下，本图步骤 3 中列出的功能应被选中。然而，在某些情况下它们未被选中，因此你需要选中它们。同样，如果你想使用 IIS 作为 FTP 服务器以便通过 Internet 开发应用程序，你需要按步骤 4 中所述选择 FTP Server 功能。

请注意，随 Windows Vista（IIS 7.0）和 Windows 7（IIS 7.5）提供的 IIS 版本不包含 FrontPage Server Extensions（FPSE）。因此，你无法在远程服务器上处理 Web 站点。然而，自 IIS 7.0 发布以来，一种适用于 IIS 7.0 及更高版本的 FPSE 版本已变得可用。你可以按本图所示从 IIS 网站下载此产品。

![](img/c024ccf88e28c30c07dd410d4342288f_800_0.png)

#### “Windows 功能”对话框

#### 如何安装 IIS
- 1. 打开控制面板，单击“程序”链接。然后，在“程序和功能”类别中单击“打开或关闭 Windows 功能”链接，以显示“Windows 功能”对话框。
- 2. 从显示的功能列表中选择 Internet 信息服务（IIS）。
- 3. 展开 Internet 信息服务节点，并确保选中以下功能：
  - Web 管理工具 ➔ IIS 6 管理兼容性
  - Web 管理工具 ➔ IIS 管理控制台
  - 万维网服务 ➔ 应用程序开发功能 ➔ ASP.NET
- 4. 如果要将 IIS 配置为 FTP 服务器，请展开 Internet 信息服务节点，并选择“FTP 服务器”功能。
- 5. 单击“确定”按钮完成安装。

#### 说明
- 如果要从本地 IIS 服务器运行应用程序，请在安装 Visual Studio 之前安装 IIS。
- Windows Vista 自带 IIS 7.0，Windows 7 自带 IIS 7.5，但二者都不包含 FPSE（FrontPage 服务器扩展）。因此，在你可以创建或访问远程计算机上的网站之前，必须先下载 FPSE。为此，请访问 www.iis.net/downloads，单击“管理”类别的链接，再单击“用于 IIS 7.0 的 FrontPage 2002 服务器扩展”的链接。
- 如果某个组件的复选框带有阴影，则表示只安装了该组件的部分功能。若要查看所有功能，可以展开该组件。

图 A-2    如何在 Windows 7 或 Windows Vista 下安装 IIS

### 如何在 Windows XP 下安装 IIS

如果希望在 Windows XP 机器上测试你在 IIS 下开发的 Web 应用程序，则需要使用图 A-3 中的过程来安装 IIS。（请注意，如果使用 Windows XP 家庭版，则无法安装 IIS；在这种情况下，IIS 对你不可用，你必须使用开发服务器，或者必须能够访问单独的 Web 服务器。）首先，显示“添加/删除程序”对话框，然后点击所显示对话框左侧的“添加/删除 Windows 组件”按钮。执行此操作后，Windows 组件向导启动，并显示本图所示的第一个对话框。此对话框列出所有可用的 Windows 组件。当前已安装的组件前面带有复选标记。要安装另一个组件（此处为 IIS），只需选中它，单击“下一步”按钮，然后完成所显示的对话框即可。

在本书中，你将学习如何使用本地 IIS 服务器开发 ASP.NET 应用程序。不过，你也应该知道，还可以使用 Visual Studio 在远程服务器上或通过 Internet 开发 ASP.NET 应用程序。若要在远程服务器上开发应用程序，则需要安装 FrontPage 服务器扩展。若要通过 Internet 开发应用程序，则可以将 IIS 用作 FTP 服务器。

若要使用其中任一功能，必须安装默认未安装的 IIS 组件。要安装这些组件，请在 Windows 组件向导中选择 IIS，然后点击“详细信息”按钮，以显示此处所示的 Internet 信息服务 (IIS) 对话框。然后，如果要将 IIS 用作 FTP 服务器，请选择“文件传输协议 (FTP) 服务”组件。另外，如果要创建远程 IIS 网站，请选择“FrontPage 2000 服务器扩展”组件。完成后，点击“确定”，然后继续使用 Windows 组件向导。

#### Windows 组件向导

![](img/c024ccf88e28c30c07dd410d4342288f_802_0.png)

#### 如何安装 IIS
- 1. 双击控制面板中的“添加或删除程序”。然后，单击“添加/删除 Windows 组件”以显示 Windows 组件向导，并从显示的组件列表中选择 Internet 信息服务 (IIS)。
- 2. 如果要安装 FPSE，或者要将 IIS 配置为 FTP 服务器，请单击“详细信息”按钮，从显示的 Internet 信息服务 (IIS) 对话框中选择相应选项，并单击“确定”。
- 3. 单击“下一步”按钮完成安装。

#### 说明
- 如果要从本地 IIS 服务器运行应用程序，请在安装 Visual Studio 之前安装 IIS。
- 要在远程计算机上创建或访问 IIS 网站，该计算机必须安装 FPSE。要将 IIS 用作 FTP 服务器，必须安装 FTP 服务。

图 A-3  如何在 Windows XP 下安装 IIS

### 如何安装 Visual Studio 2010

如果你以前安装过 Windows 应用程序，那么安装 Visual Studio 2010 应该不会有任何困难。只需插入 DVD 或第一张 CD，安装程序便会自动启动。该安装程序将引导你完成安装 Visual Studio 的步骤，如图 A-4 所示。

当你单击“安装 Microsoft Visual Studio 2010”链接时，安装程序会开始加载所需的安装组件。然后，在单击“下一步”并接受许可条款后，程序会允许你选择安装类型。在大多数情况下，你会执行完整安装，以便安装最常用的功能，包括 .NET Framework 4、Visual Studio、C#、开发 Web 服务器和 SQL Server Express。

安装完成后，你将有机会在本地系统上安装 Visual Studio 文档。如果不这样做，默认将使用在线提供的文档。你以后可以在 Visual Studio 中使用“帮助→管理帮助设置”命令更改此默认设置。

如果你使用的是 Visual Web Developer 2010 Express Edition，则必须分别下载并安装 Web Developer 2010 和 SQL Server Express。但如果你在下载这些产品时遵循 Microsoft 网站上的说明，安装它们应该不会有任何困难。

最后的安装步骤是应用自产品发布以来可用的任何更新。不过，如果不执行此步骤，你可以在 Visual Studio 中使用“帮助→检查更新”命令检查更新。事实上，你应该定期使用此命令，以确保 Visual Studio 保持最新。

顺便说一下，第一次启动 Visual Studio 时，系统会要求你选择默认环境设置。然后，你可以选择 Web 开发设置，使菜单与本书中的菜单一致。

如果你先安装 Visual Studio，之后再决定安装 IIS，则应该知道需要将 ASP.NET 注册到 IIS。为此，请在命令提示符下运行以下命令：

```
