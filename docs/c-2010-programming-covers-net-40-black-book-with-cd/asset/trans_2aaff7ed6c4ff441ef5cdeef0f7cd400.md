

![](img/e073a4882197be4ab61103cbe0bcb394_1091_0.png)

# 图 21.38：配置 Web 安装项目

你还可以在属性窗口中为 Web 安装项目设置各种属性，例如 Author、Description、Manufacturer、ManufacturerURL 和 SupportURL。

+   9. 选择 Build→Build DeploymentTestWebSetup 选项以创建 DeploymentTestWebApplication 应用程序的 Windows Installer 文件和 Setup 可执行文件。此步骤将在 DeploymentTestWebApplication\DeploymentTestWebSetup\Debug 文件夹中创建 DeploymentTestWebSetup.msi 和 Setup.exe 文件，你可以使用它们来部署 DeploymentTestWebApplication 应用程序。

当 Windows Installer 文件创建完成后，你可以轻松地在服务器上部署 Web 应用程序。让我们执行以下步骤在目标计算机上部署 DeploymentTestWebApplication Web 应用程序：

+   1. 双击安装文件 DeploymentTestWebSetup.msi 或 Setup.exe。DeploymentTestWebSetup 向导打开，如图 21.39 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1091_1.png)

# 图 21.39：显示 DeploymentTestWebSetup 向导

+   2. 单击 Next 按钮（图 21.39）。Select Installation Address 页面打开，如图 21.40 所示：

# 第 21 章：部署 Windows 和 Web 应用程序

安装完成后，Installation Complete 页面出现，如图 21.43 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1093_0.png)

图 21.43：显示安装完成页面

5. 单击 Close 以成功关闭 DeploymentTestWebSetup 向导（图 21.43）。

现在，你可以从部署的位置运行 DeploymentTestWebApplication 应用程序。为此，打开浏览器并输入 Web 应用程序部署的虚拟目录地址，如图 21.44 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1093_1.png)

图 21.44：运行已安装的应用程序

让我们现在学习如何使用 XCopy 命令部署 Web 应用程序。

# XCopy 部署

要使用 XCopy 部署技术部署 Web 应用程序，请从 Windows 开始菜单打开运行对话框。在运行对话框的打开文本框中输入 cmd，然后单击确定按钮。此步骤打开命令提示符，在其中你需要输入以下命令：

```
xcopy /I /S c:\inetpub\wwwroot\DeploymentTestWebSetup d:\MyWebApp
```

在前面的命令中，源文件夹 DeploymentTestWebSetup 存在于 c 盘中，目标文件夹 MyWebApp 存在于 d 盘中。当你执行此命令时，DeploymentTestWebSetup 文件夹内的所有文件和文件夹都会部署到目标文件夹。/I 参数允许 XCopy 命令在目标文件夹不存在时创建它。图 21.45 显示了前述命令的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1094_0.png)

现在，你需要在目标服务器上创建一个虚拟目录，并将该虚拟目录映射到 XCopy 命令在目标服务器上创建的物理目录。

接下来，你将学习如何部署 WPF 应用程序。

# 部署 WPF 应用程序

要部署 WPF 应用程序，你可以使用多种技术，例如使用 XCopy 部署、Microsoft Windows Installer 和 ClickOnce 部署。在我们的例子中，我们创建了一个名为 LocalAnimation 的 WPF 应用程序。LocalAnimation 应用程序的设计和源代码可在光盘上获得。

现在，让我们执行以下步骤了解 LocalAnimation 应用程序如何使用 Windows Installer 部署技术进行部署：

+   1. 在解决方案资源管理器中右键单击 LocalAnimation 解决方案名称并选择 **Add→New Project** 选项。Add New Project 对话框打开（图 21.46）。
+   2. 选择 **Other Project Types→Setup and Deployment→Visual Studio Installer** 类别。
+   3. 在中间窗格中选择 Setup Project 模板，并在 Name 文本框中输入项目名称。在我们的例子中，我们输入了 `deploymentTestWPFApplication`，如图 21.46 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1094_1.png)

+   4. 单击 OK 按钮（图 21.46）。
+   5. Setup 项目已添加到现有的 WPF 应用程序中。
+   6. 在解决方案资源管理器中右键单击 DeploymentTestWPFApplication 图标并从上下文菜单中选择 Add→Project Output 以打开 Add Project Output Group 对话框（图 21.47）。
+   7. 在 Project 下拉框中选择 LocalAnimation，并在列表框中选择 Primary output。现在，单击 OK 按钮将应用程序的主要程序集添加到 Setup 项目，如图 21.47 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1095_0.png)

图 21.47：将项目输出添加到解决方案

现在，你可以定义要在用户桌面或用户程序菜单上创建的项目，例如应用程序的快捷方式，如图 21.48 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1095_1.png)

图 21.48：配置 DeploymentTestWPFApplication 项目

创建 Setup 项目并向项目添加快捷方式后，你需要构建项目。

+   8. 选择 Build→Build DeploymentTestWPFApplication 选项。此步骤创建 DeploymentTestWPFApplication.msi 和 Setup.exe 文件，你可以使用它们来部署 LocalAnimation 应用程序。

要部署 LocalAnimation 应用程序，请将 DeploymentTestWPFApplication.msi 文件复制到目标计算机。双击 DeploymentTestWPFApplication.msi 文件，它将打开 DeploymentTestWPFApplication 向导，如图 21.49 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1096_0.png)

图 21.49：Windows Installer 的欢迎页面

要安装 LocalAnimation 应用程序，后续步骤完全与通过 Windows Installer 部署技术安装 Windows 应用程序时所遵循的步骤相同。安装完成后，你可以从桌面快捷方式或部署的位置运行 WPF 应用程序，如图 21.50 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1096_1.png)

图 21.50：运行 LocalAnimation 应用程序

接下来，你将学习如何使用 Windows Installer 部署技术部署 XBAP 应用程序。

# 使用 Windows Installer 部署 XBAP 应用程序

XBAP 是可托管在 Web 浏览器上的编译应用程序。这些托管应用程序在部分受信任的安全环境中运行；因此，它们仅限于使用计算机的有限资源。XBAP 的编译会创建三个文件——ApplicationName.exe、ApplicationName.xbap 和 ApplicationName.exe.manifest，并且部署需要部署这三个文件。

你可以使用 XCopy 或 Windows Installer 部署技术部署 XBAP 应用程序。但是，一旦 XBAP 部署后，当发布新版本时它不会自动更新。让我们执行以下步骤使用 Windows Installer 部署技术部署 XBAP 应用程序：

+   1. 创建 WPF 浏览器应用程序。在我们的例子中，我们创建了 XBAPApplication（也可在光盘上获得）。
+   2. 在解决方案资源管理器中右键单击解决方案名称并选择 Add→New Project 选项。Add New Project 对话框打开（图 21.51）。
+   3. 在 Recent Templates 类别中选择 Other Project Types→Setup and Deployment→Visual Studio Installer。
+   4. 在中间窗格中选择 Web Setup Project 模板，并在 Name 文本框中输入项目名称。在我们的例子中，我们输入了 DeploymentTestXBAP，如图 21.51 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1097_0.png)

# 图 21.51：创建 Setup 项目

+   5. 单击 OK 按钮创建 Web 安装项目（图 21.51）。
+   6. 在解决方案资源管理器中右键单击 DeploymentTestXBAP 图标并从上下文菜单中选择 Add→Project Output。Add Project Output Group 对话框打开。
+   7. 在 Project 下拉框中选择 XBAP Application，并在 Add Project Output Group 对话框的列表框中选择 Primary output。
+   8. 单击 OK 按钮将主要输出添加到 XBAPApplication 解决方案。
+   9. 选择 Build→Rebuild DeploymentTestXBAP 以生成 XBAPApplication.exe.manifest 和 XBAPApplication.xbap 文件。
+   10. 在解决方案资源管理器中右键单击 DeploymentTestXBAP 图标并从上下文菜单中选择 Add→File。Add Files 对话框打开，在其中你需要选择 XBAPApplication.exe.manifest 和 XBAPApplication.xbap 文件。
+   11. 单击 Open 按钮将两个文件都添加到安装项目中。
+   12. 选择 Web Application Folder 并在文件系统编辑器中的属性窗口中将 DefaultDocument 属性的值设置为 XBAPApplication.xbap。
+   13. 选择 Build→Rebuild DeploymentTestXBAP 以编译 Setup 项目。

编译项目后，打开项目的 Debug 文件夹，你可以看到两个文件，DeploymentTestXBAP.msi 和 Setup.exe。将 DeploymentTestXBAP.msi 文件复制并粘贴到

