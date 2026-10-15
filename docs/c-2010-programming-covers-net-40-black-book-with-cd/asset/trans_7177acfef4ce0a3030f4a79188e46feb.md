

## 部署应用程序的不同编辑器

当你为应用程序创建安装程序文件时，你可能需要指定应用程序的文件应安装在目标计算机上的位置，指定应添加哪些注册表项，或为安装添加自定义对话框。也有可能你需要自定义安装应用程序时显示的用户界面，或运行应用程序在目标计算机上执行某些特定操作。你可以使用 Visual Studio 2010 中提供的部署编辑器来指定和自定义与应用程序部署相关的设置。请注意，这些编辑器仅在你在应用程序中添加设置和部署项目时可用。Visual Studio 2010 提供了以下部署编辑器：

- File System editor
- Registry editor
- File types editor
- User interface editor
- Custom actions editor
- Launch conditions editor

## File System Editor

File System editor 允许你将项目输出、文件、程序集和其他项目添加到部署项目中，并指定这些文件将被部署的目标位置。它默认显示一组标准的部署文件夹。你可以使用编辑器添加自己的文件夹和特殊文件夹。此外，你可以在 File System editor 中指定应用程序的桌面和“开始”菜单快捷方式。部署的一部分的文件必须从 File System editor 中引用。要查看 File System editor，请单击 View→Editor→File System 菜单项。File System editor 出现，如图 21.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1068_0.png)

## Registry Editor

Registry editor 指定你想要添加到目标计算机注册表中的注册表项和数据值。当你第一次打开 Registry editor 时，它会显示一组标准的注册表项。要查看 Registry editor，请单击 View→Editor→Registry。Registry editor 出现，如图 21.2 所示：

## 第 21 章：部署 Windows 和 Web 应用程序

![](img/e073a4882197be4ab61103cbe0bcb394_1069_0.png)

Registry editor 分为两个窗格——左侧窗格称为 Navigation pane，包含注册表配置单元的层级列表，右侧窗格称为 Detail pane，显示注册表配置单元的描述。注册表配置单元是键、子键和值的集合。你可以在 Registry editor 中添加自定义键和值，并为子键和值设置一些属性。

## File Types Editor

File Types editor 在文件和应用程序之间建立关联。例如，当你双击具有 .doc 扩展名的文件时，它会在 MS Word 中打开。要查看 File System editor，请单击 View→Editor→File Types。File Types editor 出现，如图 21.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1069_1.png)

要建立关联，你所需要做的就是将文件扩展名与你的应用程序关联，并为每种文件类型指定允许的操作。

## User Interface Editor

User Interface editor 为一组预定义的对话框指定属性。当你想在安装过程中添加显示的额外信息时，它很有帮助。User Interface editor 分为两个部分，Install 和 Administrative Install。Install 部分包含用户运行安装程序时显示的对话框；而 Administrative Install 部分包含系统管理员将安装程序上传到网络位置时显示的对话框。要查看 User Interface editor，请单击 View→Editor→User Interface。User Interface editor 出现，如图 21.4 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1070_0.png)

### Figure 21.4: Displaying the User Interface Editor

在图 21.4 中，你可以看到 User Interface editor 包含一组预定义的对话框。这些预定义的对话框分为三类——Start、Progress 和 End。Start 对话框在安装开始前显示；Progress 对话框在安装进行中时显示；End 对话框在安装成功完成后显示。

## Custom Actions Editor

Custom Actions editor 允许你在安装过程结束时在目标计算机上定义要执行的自定义操作。自定义操作是预先创建的，必须编译为 .dll 或 exe 文件，或作为脚本或程序集添加到项目中。你可以通过单击 View→Editor→Custom Actions 查看 Custom Actions editor，如图 21.5 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1070_1.png)

### Figure 21.5: Displaying the Custom Actions Editor

在图 21.5 中，你可以看到 Custom Actions editor 中有四个特定的自定义操作阶段。自定义操作阶段的描述如下：

- Install — 在安装阶段结束时执行操作
- Commit — 在安装成功完成后执行操作
- Rollback — 在回滚阶段完成后执行操作
- Uninstall — 在卸载完成后执行操作

自定义操作按其在 Custom Actions editor 中出现的顺序运行。但是，你也可以通过拖动或使用 Cut/Paste 命令重新排序它们。

## Launch Conditions Editor

Launch Conditions editor 允许你指定必须满足的某些条件才能继续安装。例如，如果你想在特定版本的 Windows 操作系统上安装应用程序，安装首先检查特定条件是否存在，并且仅在满足条件时才运行该过程。否则，安装将在该点终止。你可以通过在 Visual Studio 2010 IDE 中选择 View→Editor→Launch Conditions 来查看 Launch Conditions editor，如图 21.6 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1071_0.png)

Figure 21.6: Displaying the Launch Conditions Editor

Launch Conditions editor（图 21.6）显示目标计算机上的以下要求：

- Search Target Machine — 指定搜索条件以确定特定文件、注册表项或 Microsoft Windows Installer 组件是否存在于目标计算机上。搜索条件的一些示例是：File Search、Registry Search 和 Windows Installer Search。
- Launch Conditions — 为应用程序指定预定义的启动条件

接下来，你将学习如何为应用程序部署添加先决条件。

## 为应用程序部署包含先决条件

要在目标计算机上安装和运行应用程序，你应确保目标计算机具有运行应用程序的先决条件。先决条件是必须安装在目标计算机上的组件，因为它需要运行你的应用程序。例如，目标计算机必须具有计算机上特定版本的通用语言运行时（CLR）。你的应用程序的先决条件在 Prerequisites 对话框中选择。这些先决条件作为安装程序应用程序的一部分，在目标计算机上为你的应用程序安装 .NET Framework 和其他依赖项。你可以通过首先在“解决方案资源管理器”中右键单击项目节点并从上下文菜单中选择“属性”选项来访问“先决条件”对话框。结果，项目属性对话框出现。现在，选择项目属性对话框中的 Publish 选项卡，如图 21.7 所示：

### Figure 21.7: Displaying the Publish Tab in the Project Properties Dialog Box

单击 Publish 选项卡中的 Prerequisites 按钮。Prerequisites 对话框打开，如图 21.8 所示：

### Figure 21.8: Displaying the Prerequisites Dialog Box

在图 21.8 中，你可以看到用于部署应用程序的可用先决条件列表。你必须选择要安装的先决条件，然后单击 OK 按钮以将先决条件包含在安装程序中。

在 Visual Studio 2010 中，部署工具具有在安装期间自动检测应用程序执行所需的组件是否存在并安装一组先决条件以确保应用程序成功执行的能力。此过程称为引导程序，由引导程序组件执行，该组件使用引导程序包在目标计算机上安装先决条件组件。此外，引导程序包由一组文件和目录以及描述先决条件如何在目标计算机上安装的清单文件组成。如果你的应用程序有一个先决条件，该先决条件未包含在 Prerequisite Dialog Box 中可用的预定义先决条件中，你可以

