
| 用户名 (User Name) | 用于 IIS 连接的用户名。 |
| 密码 (Password) | 用于 IIS 连接的密码。 |
| 保存密码 (Save password) | 指定 Visual Studio 发布功能将密码保存在配置文件中。 |

除了使用 MSDeploy 外，您会发现通过新的“发布 Web”对话框提供的其他选项更加简单。图 36-11 显示了其他三个部署选项的设置。

![](img/7040c21013b8e6c23c612d6da3599ff8_1406_0.png)

## 发布 Web

![](img/7040c21013b8e6c23c612d6da3599ff8_1407_0.png)

图 36-11

在此图中，您可以看到使用 FTP、文件系统或 FrontPage 服务器扩展程序进行部署的一些标准设置。

Visual Studio 2010 现在支持的 MSDeploy 功能的有趣之处在于，您不需要连接到远程 MSDeploy 处理程序并实时运行部署，您还可以创建一个可以随时运行的 MSDeploy 包。

Visual Studio 2010 包含了如何创建这些包，这些包可以通过电子邮件或其他方式提供给他人以便在他们的系统上运行。要创建 Web 部署包，请在 Visual Studio 解决方案管理器中右键点击项目，并从提供的菜单中选择“创建包”（Create Package）选项。

当您选择“创建包”选项时，包的创建进度出现在 Visual 状态栏中。在收到发布成功的通知后，您可以在应用程序的对象文件夹中找到整个包，例如：

```
C:\Users\Evjen\Documents\Visual Studio 10\nProjects\MyWebApplication\MyWebApplication\obj\Release\Package
```

该文件夹内包含构成包的所有文件。

## Web 应用程序的部署方法

![](img/7040c21013b8e6c23c612d6da3599ff8_1406_0.png)

由于 Visual Studio 2010 现在支持的 MSDeploy 功能的有趣之处在于，您不需要连接到远程 MSDeploy 处理程序并实时运行部署，您还可以创建一个可以随时运行的 MSDeploy 包。

Visual Studio 2010 包含了如何创建这些包，这些包可以通过电子邮件或其他方式提供给他人以便在他们的系统上运行。要创建 Web 部署包，请在 Visual Studio 解决方案管理器中右键点击项目，并从提供的菜单中选择“创建包”（Create Package）选项。

当您选择“创建包”选项时，包的创建进度出现在 Visual 状态栏中。在收到发布成功的通知后，您可以在应用程序的对象文件夹中找到整个包，例如：

```
C:\Users\Evjen\Documents\Visual Studio 10\nProjects\MyWebApplication\MyWebApplication\obj\Release\Package
```

该文件夹内包含构成包的所有文件。

## MSDeploy 包

Visual Studio 2010 现在支持的 MSDeploy 功能的有趣之处在于，您不需要连接到远程 MSDeploy 处理程序并实时运行部署，您还可以创建一个可以随时运行的 MSDeploy 包。

Visual Studio 2010 包含了如何创建这些包，这些包可以通过电子邮件或其他方式提供给他人以便在他们的系统上运行。要创建 Web 部署包，请在 Visual Studio 解决方案管理器中右键点击项目，并从提供的菜单中选择“创建包”（Create Package）选项。

当您选择“创建包”选项时，包的创建进度出现在 Visual 状态栏中。在收到发布成功的通知后，您可以在应用程序的对象文件夹中找到整个包，例如：

```
C:\Users\Evjen\Documents\Visual Studio 10\nProjects\MyWebApplication\MyWebApplication\obj\Release\Package
```

该文件夹内包含构成包的所有文件。

- 向注册表读取或写入值的能力
- 在安装过程中从终端用户收集信息的能力
- 运行脚本的能力
- 在安装过程中包含对话框和启动屏幕等功能的能力

## 创建基础安装程序

你可以对构建的安装程序进行大量的自定义。不过，请先从查看如何为你的 ASP.NET Web 应用程序创建一个基础安装程序开始。要为应用程序创建安装程序，需要在 Visual Studio 中为想要创建部署项目的项目为你的程序添加一个安装程序。要执行此操作，你需要在同一个解决方案中将设置程序选择为新项目。此时会弹出“新建项目”（New Project）对话框。

在“新建项目”对话框中，从左侧窗格展开“其他项目类型”（Other Project Types），并选择“设置和部署”（Setup and Deployment）。将出现 Visual Studio 中所有可用的部署项目列表。在本例中，选择“Web 安装项目”（Web Setup Project，如图 36-13 所示）。

![](img/7040c21013b8e6c23c612d6da3599ff8_1410_0.png)

图 36-13

点击此对话框中的“确定”会将 Web 安装项目类型添加到你的解决方案中。它使用默认名称 Setup1。Visual Studio 还会在文档窗口中打开“文件系统编辑器”（File System Editor），如图 36-14 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_1411_0.png)

图 36-14

文件系统编辑器显示单个文件夹：Web 应用程序文件夹（Web Application Folder）。这是要在目标机器上安装内容的表示。现在，从 WebSite 向此文件夹添加文件，通过在 Visual Studio 菜单中选择“项目（Project） > 添加项目输出（Add Project Output）”来实现。“添加项目输出”对话框（如图 36-15 所示）允许你选择想要包含在安装程序中的项。

从此对话框中，你可以看到项目 Wrox 已选中。高亮“内容文件”（Content Files）选项并点击“确定”。这会将 Wrox 项目的所有文件添加到 WebSetup 安装程序中。此添加随后也会注册在文件系统编辑器中。

将此内容添加到安装程序后，点击解决方案管理器中的“启动条件编辑器”（Launch Conditions Editor）（见图 36-16）以打开启动条件编辑器。启动条件编辑器也会出现在 Visual Studio 窗口中。从这里开始，你可以看到已经为你定义了几个条件。显然，对于 Web 应用程序来说，安装 IIS 是重要的。在本地，其中一个条件是程序在安装应用程序之前必须搜索以检查是否安装了 IIS。你还应该规定安装服务器必须安装了版本 4 的 .NET Framework。

![](img/7040c21013b8e6c23c612d6da3599ff8_1411_1.png)

图 36-15

要建立此条件，右键点击“目标机器上的要求”（Requirements On Target machine）节点。然后选择“添加 .NET Framework 启动条件”（Add .NET Framework Launch Condition）（如图 36-17 所示）。

## 部署 Web 应用程序的方法

![](img/7040c21013b8e6c23c612d6da3599ff8_1412_0.png)

图 36-16 Microsoft Visual Studio

![](img/7040c21013b8e6c23c612d6da3599ff8_1412_1.png)

创建项目 'WebSite1' - 项目创建成功。

图 36-17

这会将 .NET Framework 要求添加到成功安装 Web 应用程序所需的启动条件列表中。

作为最后一步，在 Visual Studio 资源管理器中高亮 WebSetup1 程序，以便在“属性”窗口中修改某些属性。现在，只需更改一些说明性属性，但你将在本章稍后的部分再次查看这些属性。对于此示例，只需更改以下属性：

- 作者 (Author): Wrox
- 描述 (Description): 这是一个测试项目。
- 制造商 (Manufacturer): Wrox
- 制造商 URL (ManufacturerUrl): http://www.wrox.com
- 支持电话 (SupportPhone): 1-800-555-5555
- 支持 URL (SupportUrl): http://www.wrox.com/support/

现在，安装已简化到最基本的实例。在 Visual Studio 工具栏中，将“生成”发布到活动解决方案配置；然后通过从菜单选择“生成（Build） > WebSetup1”来生成安装程序。

查看 `C:\Documents\username\My Documents\Visual Studio 2010\Projects\WroxSetup1\Release`，你会发现以下内容：

- `Setup.exe`：这是安装程序。它用于没有安装 Windows Installer 的机器。
- `WebSetup1.msi`：这是已安装 Windows Installer 服务的机器的安装程序。

就是这样！现在你已经将 ASP.NET Web 应用程序封装在一个可以以你喜欢的任何方式分发的安装程序中。然后它可以供终端用户运行和安装。快速查看下一节，了解当消费者实际安装时会发生什么。

## 安装应用程序

安装应用程序是一个简单的过程。双击 `WebSetup1.msi` 文件启动安装程序。出现图 36-18 所示欢迎界面。从此对话框，你可以看到正在安装的程序名称为 WebSetup1。点击“下一步（Next）”将进入 36-19 界面。

![](img/7040c21013b8e6c23c612d6da3599ff8_1413_0.png)

图 36-18

![](img/7040c21013b8e6c23c612d6da3599ff8_1413_1.png)

图 36-19

## 部署 Web 应用程序的方法

此屏幕告诉你你正在安装默认站点（Default Site）以及为部署创建的虚拟目录。消费者可以自由更改提供框中的虚拟目录名称。对话框中的按钮允许估计安装应用程序所需的磁盘空间。.NET 4 安装程序还允许用户选择感兴趣的应用程序池。接下来的屏幕安装 Web 应用程序（如图 36-20）。

应用程序完成后，你可以在 `C:\inetpub\wwwroot` 找到 WebSetup 文件夹和应用程序文件。应用程序现在可以从此位置运行。

![](img/7040c21013b8e6c23c612d6da3599ff8_1414_0.png)

图 36-20

## 卸载应用程序

要安装应用程序，消费者有几个选项。一种是重新启动 .msi 文件并使用修复（repair）或删除安装（remove the installation）选项（如图 36-21 所示）。

![](img/7040c21013b8e6c23c612d6da3599ff8_1414_1.png)

图 36-21

另一个选项是从服务器的控制面板打开“添加/删除程序”对话框。在控制面板上，你会看到列出的 WebSetup1（如图 36-22 所示）。

![](img/7040c21013b8e6c23c612d6da3599ff8_1415_0.png)

图 36-22

此对话框包含已安装应用程序的大小，如果你使用的是 Windows XP，它还会显示如何使用应用程序。此外，如果你使用的是 Windows XP，点击支持链接将打开你早些输入的项目属性信息对话框（见图 36-23）。

然而，如果你使用的是 Windows 7，可以通过右键点击列标题并从提供的菜单中选择更多（More）选项获取相同信息。这将为你提供与 Windows XP 相同的选项列表（如图 36-24）。

![](img/7040c21013b8e6c23c612d6da3599ff8_1415_1.png)

图 36-23

图 36-24

在“添加/删除程序”对话框中，可以通过点击选中程序的删除按钮来移除安装。

## 详细查看安装选项

Windows Installer 可以轻松安装简单的 ASP.NET Web 应用程序。安装程序负责将文件封装成 .msi 文件，然后进行分发。接下来，msi 文件负责创建虚拟目录并安装应用程序文件。安装程序同样让从服务器卸载应用程序变得简单。所有这些强大的服务用户只需少量工作。

尽管这涵盖了 ASP.NET 安装程序所需的所有内容，但由 Visual Studio 开发的 Web 应用程序设置和部署项目提供了更多选项和自定义功能。下一节列出了你可以修改程序的各种方式。

## 部署项目属性

你可以通过多种方式在 Visual Studio 中处理安装程序的项目属性。第一种方法是在 Visual Studio 的解决方案管理器中右键点击安装程序，并在 36-25 所示的 WebSetup 属性页中选择属性（Properties）。

此对话框对你的安装程序具有重要设置。注意，与其他项目不同，此设置和部署允许不同的活动配置设置。例如，你可以将活动配置设置为 Release 或 Debug。你还可以点击“配置管理器”（Configuration Manager）按钮来访问所有相关项目的配置设置。此外，这允许你从项目中添加或删除配置。

![](img/7040c21013b8e6c23c612d6da3599ff8_1416_0.png)

图 36-25

### 输出文件名

输出文件名（Output File Name）设置指定生成的 .msi 文件名称。默认情况下，它是项目名称，但你可以将其更改为任何想要的值。属性设置还允许你修改构建发生后 MSI 放置在系统中的位置。

### 包文件

此部分属性页的“包文件”（Package files）允许配置应用程序文件在 .msi 文件中的封装方式。可用选项包括：

- 作为松散、未压缩的文件（As loose, uncompressed files）：此选项构建项目，使生成的 MSI 文件在创建时不包含所需的应用程序文件。相反，这些应用程序文件是与 MSI 文件分离，并复制到与 MSI 文件相同的位置。使用这种结构，你必须同时分发 MSI 文件和相关的应用程序文件。
- 在设置文件中（In setup file）：此选项（默认选项）将应用程序文件封装在 .msi 文件内部。这使得分发变成一项简单任务，因为只需要分发单个文件。
- 在箱文件 (cabinet file(s)) 中：此选项将所有应用程序文件打包到箱文件中。箱文件的大小可以通过此对话框（稍后讨论）进行控制。如果你需要将安装程序分发到 DVD、CD 或软磁盘上，这种安装过程是十分理想的。

### 安装 URL

不可避免的是，你构建的 .NET 应用程序具有某些依赖项。大多数情况下，你的应用程序依赖于某个版本的 .NET Framework。这些依赖项或组件的安装可以在安装过程中完成。这也称为引导（bootstrapping）。点击 URL 框旁边的体系条件（Prerequisites）按钮可以获得 Visual Studio 内置的所有组件列表，用于引导你正在构建的安装程序（见图 36-26）。

从此对话框可以看出，.NET Framework 4 和 Windows Installer 3.1 默认启用，只有当你的应用程序对它们有某些依赖关系时，你才选择其他组件（从而启用它们）。

通过此对话框，你可以看到依赖组件是如何部署到正在安装的服务器上的。选项包括从 Microsoft 下载、从应用程序源服务器下载或从文本框指定的定义位置 (URL) 下载。

![](img/7040c21013b8e6c23c612d6da3599ff8_1417_0.png)

图 36-26

### 压缩

Windows Installer 服务可以处理构建过程中包含的应用程序文件的压缩，使其针对速度或大小进行优化。你还可以选择关闭所有压缩优化。默认设置是“针对速度优化 (Optimized for Speed)”。

### CAB 大小
