
以下服务器平台受支持：

- Windows Server 2003 系列 SP2
- Windows Server 2008 系列（不支持 Server Core 角色）

以下体系结构受支持：

- x86
- x64
- ia64（某些功能不受支持）

其他要求为 Windows Internet Explorer 版本 5.01 或更高版本、MDAC 版本 2.8 或更高版本（如果应用程序设计为访问数据），以及用于 ASP.NET 应用程序的 Internet Information Services（IIS）。

部署 .NET 应用程序时，您还必须考虑硬件要求。客户端和服务器的最低硬件要求均为 Pentium 400 MHz 和 96 MB RAM

为了获得最佳性能，请增加 RAM 容量——RAM 越多，.NET 应用程序运行越好。这对于服务器应用程序尤其如此。

## 部署 .NET 运行时

使用 .NET 开发应用程序时，存在对 .NET 运行时的依赖。这似乎显而易见，但有时显而易见的事情会被忽略。下表显示了版本号以及需要分发的文件名：

| .NET 版本 | 文件名 |
|---|---|
| 2.0.50727.42 | dotnetfx.exe |
| 3.0.4506.30 | dotnetfx3.exe (包含 x86 和 x64) |
| 3.5.21022.8 | dotnetfx35.exe (包含 x86、x64 和 ia64) |
| 4.0.0.0 | dotnetfx40.exe (包含 x86、x64 和 ia64) |

## 简单部署选项

如果部署是应用程序原始设计考虑的一部分，部署可以简单到将一组文件复制到目标计算机。对于 Web 应用程序，它可以是 Visual Studio 2010 中的一个简单菜单选项。本节讨论这些简单部署方案。

要了解各种部署选项的设置方式，您必须有一个要部署的应用程序。www.wrox.com 上的示例下载包含四个项目：

- ClientWinForms
- ClientWPF
- WebClient
- AppSupport

ClientWinForms 和 ClientWPF 分别是使用 WinForms 和 WPF 的智能客户端应用程序。WebClient 是一个简单的 Web 应用。AppSupport 是一个类库，其中包含一个简单的类，该类返回包含当前日期和时间的字符串。

示例应用程序使用 AppSupport 用包含当前日期的字符串填充标签。要使用示例，首先加载并构建 AppSupport。然后，在其他每个应用程序中，将引用设置为新构建的 AppSupport.dll。

## Xcopy 和 Web 应用程序

Xcopy 部署也可以与 Web 应用程序一起使用，但文件夹结构除外。您必须建立 Web 应用程序的虚拟目录并配置适当的用户权限。此过程通常使用 IIS 管理工具完成。

在设置虚拟目录后，Web 应用程序文件可以复制到虚拟目录。复制 Web 应用程序的文件可能有点棘手。需要考虑几个配置文件以及页面可能使用的图像。

## 发布网站

发布网站是 Web 项目的另一种部署选项。发布网站将预编译整个站点并将编译后的版本放置到指定位置。该位置可以是文件共享、FTP 位置或任何可以通过 HTTP 访问的位置。编译过程会从程序集中删除所有源代码并创建用于部署的 DLL。这也包括 ASPX 源文件中的标记。ASPX 文件不再包含常规标记，而是包含指向程序集的指针。每个 ASPX 文件都与一个程序集相关。此过程无论模型如何都有效：代码隐藏或单文件。

发布网站的优点是速度和安全性。速度得到增强，因为所有程序集都已预先编译。否则，第一次访问页面时会有延迟，因为页面和依赖代码会被编译并缓存。安全性得到增强，因为源代码未被部署。此外，由于在部署之前已预编译所有内容，因此所有编译错误都会被发现。

您从 Build - Publish 菜单选项发布网站。在“发布方法”下拉菜单中，您可以选择 MSDeploy Publish、FTP 或文件系统。FTP 选项会要求输入 FTP 地址以及所需的任何登录凭据。文件系统选项会要求输入目标位置的路径。MSDeploy Publish 选项是有趣的选项。

您可以从项目属性页面的 Package and Publish 选项卡定义网站部署的许多属性。您可以定义应包含哪些文件，包括调试信息。可以包含来自 Deploy Sql 选项卡的数据库信息。此信息包括连接字符串、架构信息和数据库脚本选项。

您也可以在此处选择打包选项。将生成包含安装网站所需的一切的 zip 文件。除 zip 文件外，还将生成另外三个文件：

- `projectname.deploy.cmd` — MSDeploy 用于安装网站的命令文件。
- `projectname.SetParameters.xml` — 包含传递给 Web 部署工具的不同参数的 XML 文件。这可用于部署到不同的服务器或在不同的环境中。
- `projectname.SourceManifest.xml` — Visual Studio 2010 用于创建包的设置。

Projectname 是正在打包的项目的名称。包可以使用 Visual Studio 或 MSBuild 部署。

| 项目属性 | 描述 |
|---|---|
| SearchPath | 表示依赖程序集、文件或合并模块的搜索路径的字符串。在开发机器上构建安装程序包时使用。 |
| Subject | 有关应用程序的其他信息。此信息显示在 msi 包属性对话框的摘要页面上。 |
| SupportPhone | 应用程序或组件支持的电话号码。此信息显示在添加/删除对话框的 SupportInfo 页面上的支持信息字段中。 |
| SupportURL | 应用程序或组件支持的 URL。此信息显示在添加/删除对话框的 SupportInfo 页面上的支持信息字段中。 |
| TargetPlatform | 支持 Windows 的 32 位或 64 位版本。 |
| Title | 安装程序的标题。这显示在 msi 包属性对话框的摘要页面上。 |
| UpgradeCode | 表示同一应用程序不同版本的共享标识符的字符串 GUID。UpgradeCode 对于应用程序的不同版本或不同语言版本不应更改。由 DetectNewerInstalledVersion 和 RemovePreviousVersion 使用。 |
| Version | 安装程序、.cab 文件或合并模块的版本号。请注意，这不是正在安装的应用程序的版本。 |

设置属性后，您可以开始添加程序集。在此示例中，您需要添加的唯一程序集是主可执行文件（ClientWinForms.exe）。为此，您可以右键单击解决方案资源管理器中的项目或从项目菜单中选择添加。您有四个选项：

- Project Output — 您将在下一个示例中探索此选项。
- File — 用于添加自述文本文件或任何不属于构建过程的一部分的文件。
- Merge Module — 单独创建的合并模块。
- Assembly — 使用此选项选择安装的一部分的程序集。

为此示例选择 Assembly。您将看到 Component Selector 对话框，其外观类似于您用于向项目添加引用的对话框。浏览到应用程序的 \bin\release 文件夹。选择 ClientWinForms.exe 并在 Component Selector 对话框中单击 OK。现在您可以在部署项目的解决方案资源管理器中看到 ClientWinForms.exe。 在“检测到的依赖项”部分中，您可以看到 Visual Studio 询问 ClientWinForms.exe 以查找其所依赖的程序集；在这种情况下，AppSupport.dll 会自动包含。您将继续此过程，直到部署项目的解决方案资源管理器中包含应用程序中的所有程序集。

接下来，您必须确定程序集将被部署到何处。默认情况下，Visual Studio 2010 中显示的是文件系统编辑器。文件系统编辑器分为两个窗格：左侧窗格显示目标机器上的文件系统层次结构；右侧窗格提供所选文件夹的详细视图。文件夹名称可能不是您期望看到的名称，但请记住，这些是针对目标机器的。例如，标记为 User's Programs Menu 的文件夹映射到目标客户端上包含用户程序菜单的文件夹。这会根据所使用的 Windows 版本而有所不同。

此时您可以添加其他文件夹，无论是特殊文件夹还是自定义文件夹。要添加特殊文件夹，请确保在左侧窗格中突出显示 File System on Target Machine，然后在主菜单上选择 Action 菜单。Add Special Folder 菜单选项提供可添加的文件夹列表。例如，如果您想在 Application 文件夹下添加一个文件夹，您可以在左侧选择 Application Folder 文件夹
