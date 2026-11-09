
语言 (XML)，以下代码片段展示了转换文件的内容，其中连接字符串被 customErrors 元素替换：

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <connectionStrings>
    <add name="SampleDB"
      connectionString="value of the deployed
      Web.config file" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
  </connectionStrings>
  <system.web>
    <customErrors defaultRedirect="CustomError.htm" mode="RemoteOnly" xdt:Transform="Replace">
      <error statusCode="500" redirect="InternalError.htm" />
    </customErrors>
  </system.web>
</configuration>
```

## 数据库部署

在 Visual Studio 2010 中，部署包包含依赖项，例如 SQL Server 数据库上的日志文件。包定义包含你为数据库提供的连接字符串。它还包括与数据库架构和数据相关的结构化查询语言 (SQL) 脚本。使用依赖项，你还可以创建自定义 SQL 脚本，并可以创建它们应执行的顺序。在部署时，部署过程会为目标服务器使用适当的连接字符串，该连接字符串用于在服务器上运行 SQL 脚本，以创建数据库架构。

## Web 应用程序的一键发布

在 Visual Studio 2010 中，IIS 远程管理服务用于在远程服务器上发布 Web 应用程序。你必须为测试或暂存服务器创建发布配置文件，以安全地存储凭据。创建发布配置文件后，你可以使用 Web 一键发布工具栏一键将 Web 应用程序部署到目标服务器。你也可以使用 MSBuild 命令行发布 Web 应用程序。

## 部署 Windows 应用程序

软件或应用程序的部署可以视为使其可供多个用户使用的一项活动。如你所知，Windows 应用程序在用户计算机上本地运行。当你开发 Windows 应用程序时，它会在你开发它的计算机上执行。但是，你可以部署该应用程序，以便使用 Windows Installer 轻松地将其安装到另一台计算机上，而无需共享应用程序的代码。在本节中，你将学习使用以下技术部署应用程序：

- Windows Installer
- ClickOnce

让我们逐一讨论这些技术。

### 使用 Windows Installer

**Windows Installer** 是一种借助交互式安装向导部署应用程序的技术。它允许你通过创建 Windows Installer 包来部署 Windows 应用程序。安装程序包的扩展名为 .msi，包含要部署的应用程序、依赖文件和注册表项。只需将此包复制到目标计算机上，即可将其分发给各种最终用户。然后，最终用户可以运行安装程序包，将应用程序安装到其计算机的硬盘上。一旦你的应用程序安装在目标计算机上，最终用户就可以从目标计算机打开该应用程序。

让我们执行以下步骤，使用 **Windows Installer** 部署并安装名为 **PictureBoxControl** 的 Windows 应用程序（该应用程序也位于光盘上）：

- 1. *打开* **Microsoft Visual Studio 2010**。
- 2. 从菜单栏中*选择* **File→Open→Project/Solution**，如图 App-A.1 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_736_0.png)

图 App-A.1

出现 **Open Project** 对话框（图 App-A.2）。

- 3. *浏览*到该应用程序，并选择要打开以进行部署的解决方案名称。在本例中，我们选择了在本书 Visual Basic 部分的第 3 章 **Windows Forms Controls-I** 中创建的 **PictureBoxControl** 应用程序（图 App-A.2）。
- 4. *单击* **Open** 按钮，如图 App-A.2 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_736_1.png)

图 App-A.2

**PictureBoxControl** 应用程序打开。

- 5. 在应用程序中，从菜单栏*选择* **File→Add→New Project**。
- 6. 从“已安装的模板”窗格中*选择* **Other Project Types→Setup and Deployment→Visual Studio Installer**（图 App-A.3）。
- 7. 从“模板”窗格中*选择* **Setup Wizard** 选项（图 App-A.3）。
- 8. 在 **Name** 文本框中*输入* **DeploySetup**，以指定项目名称（图 App-A.3）。该安装程序位于光盘中的 PictureBoxControl 文件夹内。
- 9. *单击* **OK** 按钮，如图 App-A.3 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_737_0.png)

出现 **Setup Wizard**，显示 **Welcome to the Setup Project Wizard** 页面（图 App-A.4）。

- 10. 单击 **Next** 按钮，如图 App-A.4 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_737_1.png)

出现 **Choose a project type** 页面（图 App-A.5）。

- 11. 选择一个单选按钮，以指定要在其中部署应用程序的项目类型。在本例中，我们选择了 **Create a setup for a Windows application** 单选按钮（图 App-A.5）。
- 12. 在向导中单击 **Next** 按钮，如图 App-A.5 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_737_2.png)

出现 **Choose project outputs to include** 页面（图 App-A.6）。

在此页面中，你可以指定要随应用程序一起部署的其他文件。例如，你可以部署程序本身，或者部署程序及其源代码。在本例中，选中 **Which project output groups do you want to include?** 列表框中的所有复选框，以在 **PictureBoxControl** 应用程序中部署文件（图 App-A.6）。

- 13. 单击 **Next** 按钮，如图 App-A.6 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_738_0.png)

图 App-A.6

出现 **Choose files to include** 页面（图 App-A.7）。

在此页面中，你可以包括要部署的其他文件，例如 **readme.txt** 文件和许可协议。在本例中，我们不包括此类文件。

- 14. 单击 **Next** 按钮，如图 App-A.7 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_738_1.png)

图 App-A.7

出现 **Create Project** 页面（图 App-A.8）。

- 15. 单击 **Finish** 按钮，如图 App-A.8 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_739_0.png)

图 App-A.8

安装程序完成后，会将一个名为 **DeploySetup** 的新项目添加到解决方案中（图 App-A.9）。在 **Properties** 窗口中，你可以为 **DeploySetup** 项目设置各种属性，例如 **ManufacturerUrl**、**ProductCode** 和 **ProductName**。你还可以定义要在用户桌面或用户 **Programs** 菜单上创建的项，例如应用程序的快捷方式。让我们继续执行以下步骤，以在用户桌面和 **Programs** 菜单上创建快捷方式。

- 16. 选择“目标计算机上的文件系统”下的 **User’s Desktop** 文件夹（图 App-A.9）。
- 17. 右键单击“文件系统编辑器”右侧窗格中的任意位置，然后从上下文菜单中选择 **Create New Shortcut** 选项，如图 App-A.9 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_739_1.png)

图 App-A.9

出现“在项目中选择项”对话框（图 App-A.10）。

- 18. 从“查找范围”下拉列表框中*选择* **Application Folder**（图 App-A.10）。
- 19. 选择来自 **PictureBoxControl** (Active) 的“主输出”项（图 App-A.10）。
- 20. 单击 **OK** 按钮，如图 App-A.10 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_740_0.png)

图 App-A.10

这会在右侧窗格中创建一个快捷方式文件（图 App-A.11）。

- 21. 将快捷方式的名称设置为要在桌面上显示的名称。在我们的示例中，我们将其设置为 DeployTest，如图 App-A.11 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_740_1.png)

图 App-A.11

- 22. 选择“目标计算机上的文件系统”下的“用户 **Programs** 菜单”文件夹（图 App-A.12）。
- 23. 右键单击“文件系统编辑器”右侧窗格中的任意位置，然后从上下文菜单中选择 Create New Shortcut 选项，如图 App-A.12 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_740_2.png)

图 App-A.12

出现“在项目中选择项”对话框（图 App-A.13）。

