

## aspnet_compiler 命令的语法

```
aspnet_compiler -v virtual-directory [-u] [-d] [-f] [target-directory]
```

### 开关

| 开关 | 描述 |
|---|---|
| -v | 在其后跟随要预编译的现有网站的虚拟目录名称。 |
| -u | 预编译的网站将是可更新的。 |
| -d | 调试信息将被包含在编译后的程序集中。 |
| -f | 如果目标目录已存在，则覆盖它。 |

### 示例

预编译现有网站

```
aspnet_compiler -v Ch14ProductList c:\Deploy\Ch14ProductList
```

就地预编译网站

```
aspnet_compiler -v Ch14ProductList
```

创建可更新的预编译网站并包含调试信息

```
aspnet_compiler -v Ch14ProductList -u -d c:\Deploy\Ch14ProductList
```

### 描述

- 你可以使用 aspnet_compiler 命令从命令提示符预编译网站。
- 如果你指定目标目录，预编译的网站将存储在你指定的目录中。如果未指定目标目录，网站将就地预编译。
- 如果目标目录不是应用程序的最终目的地，你可以使用 XCopy 部署将预编译的网站移动到该目的地。

### 注释

- aspnet_compiler 命令位于 .NET Framework 4 目录中，即 %systemroot%\Microsoft.NET\Framework\v4.0.xxxxx，其中 %systemroot% 是 Windows 的根目录，xxxxx 是五位数的内部版本号。

## 如何创建 Web Setup 项目

部署 Web 应用程序的另一种方法是开发一个 *Web Setup 项目*，该项目创建一个标准的 Windows *Setup 程序*，你可以使用它将 Web 应用程序安装到 IIS 服务器上。如图 22-8 所示，你首先向现有网站添加 Web Setup 项目。然后，你配置 Web Setup 项目以安装 Web 应用程序所需的文件。你还可以使用设置编辑器配置许多自定义选项来控制应用程序的安装方式。

你可以使用本图所示的 File System Editor 向设置项目添加文件和文件夹。例如，要添加 Readme 文件，你可以右键单击 File System Editor 左窗格中的 Web Application Folder，然后选择 Add→File。请注意，Web Application Folder 表示 Web 应用程序将被安装的虚拟目录，并且它具有定义该虚拟目录的属性。你最有可能更改的两个属性是 VirtualDirectory，它指定虚拟目录的名称，以及 DefaultDocument，它指定默认显示的页面。

你可以使用 Registry Editor 指定应添加到目标计算机注册表中的键和值。并且你可以使用 File Types Editor 在目标计算机上的文件扩展名和应用程序之间建立文件关联。由于大多数 Web 应用程序不需要调整注册表设置或创建文件类型关联，因此你不需要这两个编辑器。然而，其他三个编辑器可能很有用。

User Interface Editor 让你自定义在运行 Setup 程序安装 Web 应用程序时显示的对话框。例如，你可以更改任何对话框的 BannerBitMap 属性，以在该对话框中显示公司的徽标。此编辑器还让你更改在对话框中显示的文本，并让你向 Setup 程序显示的对话框添加自己的对话框。

Custom Actions Editor 让你指定在安装的安装、提交、回滚或卸载阶段结束时在用户计算机上执行的操作。Visual Studio 提供了五个预定义的操作来安装各种组件。此外，你可以通过开发执行该操作程序或组件来创建自己的自定义操作。例如，你可以使用自定义操作在安装应用程序时创建 SQL Server 数据库。但是请注意，自定义操作可能很难开发。

最后，Launch Conditions Editor 让你设置在应用程序可以安装之前必须满足的条件。例如，你可以使用启动条件检查操作系统版本或查看目标系统上是否存在特定文件。如果条件不满足，Setup 程序将中止安装。

除了使用设置编辑器之外，你还可以设置 Setup 项目的属性。其中一些属性提供支持信息，并在卸载或更改程序窗口（Windows 7 和 Windows Vista）或从添加或删除程序窗口（Windows XP）可用的支持信息对话框中显示。其他属性提供有关应用程序的附加信息，例如 Setup 程序显示的产品名称。

### 带 File System Editor 显示的 Web Setup 项目

![](img/c024ccf88e28c30c07dd410d4342288f_766_0.png)

### 如何创建 Setup 项目

- 选择 File→Add→New Project 命令以显示 Add New Project 对话框。然后，展开 Other Project Types 和 Setup and Deployment 组，选择 Visual Studio Installer 选项，选择 Web Setup Project 模板，输入 Web Setup 项目的名称，然后单击 OK。
- 在 Solution Explorer 中，右键单击 Web Setup 项目并选择 Add→Project Output 命令以显示 Add Project Output Group 对话框。然后，单击 OK 将网站的内容文件添加到 Web Setup 项目。
- 当 Web Setup 项目被选中时，使用在 Solution Explorer 顶部显示的按钮来访问设置编辑器，让你自定义 Web Setup 项目的各个方面。

### 描述

- Web Setup 项目创建标准的 Windows Setup 程序，将 Web 应用程序安装到 IIS 服务器上。要创建 Web Setup 项目，请向要部署的网站添加 Web Setup 项目，然后使用设置编辑器进行配置。
- 你可以设置项目属性，为应用程序提供支持和其他信息。你还可以设置提供有关应用程序将被安装的虚拟目录信息的属性，该虚拟目录在上图所示的 File System Editor 中由 Web Application Folder 表示。

## 如何创建和使用 Setup 程序

配置 Web Setup 项目后，你可以创建 Setup 程序并按图 22-9 所述安装应用程序。首先，你应该选择是否要创建应用程序的调试版或发布版。由于调试版包含生产应用程序中通常不需要的符号调试信息，并且该版本未优化，因此你通常会创建发布版。另一方面，在测试期间，你可能想要创建调试版。要确定创建哪个版本，你可以使用本图所示的 Solution Configurations 下拉列表。

接下来，你构建 Setup 项目。这会在 Web Setup 项目的 Debug 或 Release 文件夹中创建设置文件（Setup.exe 和 Setup.msi），具体取决于是否创建调试版或发布版。然后，在大多数情况下，你会将这些文件复制到网络服务器或刻录到 CD 或 DVD 上。最后，你可以通过从将托管应用程序的服务器运行 Setup.exe 程序来安装应用程序。

请注意，Setup 程序本身是标准的 Windows 应用程序，而不是 Web 应用程序。因此，Setup.exe 和 Setup.msi 文件不在与 Web 应用程序相同的目录中。相反，你会在 Web Setup 项目的项目目录中找到这些文件，默认情况下你可以在 My Documents\Visual Studio 2010\Projects 下找到它。

当你在主机服务器上运行 Setup 程序安装 Web 应用程序时，它会引导你完成安装过程。在此图中，例如，你可以看到典型 Setup 程序步骤之一的屏幕。在这里，应用程序将被部署到默认网站中的名为 HalloweenProductList 的虚拟目录。

