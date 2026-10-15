

构建 FileWatcherService 服务，重新安装它并启动它。

现在你可以增强之前创建的 FileWatcherPanel 应用程序以设置过滤器。为了让用户选择文件过滤器，你将使用单选按钮。在 FileWatcherPanel 程序的 Form1 上（目前包含三个按钮），放置三个单选按钮。设置其文本标签如下：

```
RadioButton1 - TXT files
RadioButton2 - DOCX files
RadioButton3 - DAT files
```

在这几个选项按钮正下方放置一个按钮。将其命名为 btnSetFilter 并将其文本设置为 Set Filter。在此按钮的单击事件中，放置以下代码：

```vb
Dim nFilterCommand As Integer = 201
If RadioButton1.Checked Then
    nFilterCommand = 201
End If
If RadioButton2.Checked Then
    nFilterCommand = 203
End If
If RadioButton3.Checked Then
    nFilterCommand = 210
End If
myController.ExecuteCommand(nFilterCommand)
```

此时，Form1 应类似于图 30-5 所示的屏幕。

启动 FileWatcherPanel 控制程序并测试更改过滤器的功能，通过在每种过滤器设置下添加不同类型的文件并检查 resulting 日志事件。

## PASSING STRINGS TO A SERVICE

由于 OnCustomCommand 事件仅接受数字代码作为输入参数，因此你无法直接将字符串传递给服务。例如，如果你想重新配置服务的目录名，就不能直接发送目录名。相反，有必要将要传递给服务的信息放在磁盘上某个已知位置的文件中。然后服务的自定义命令可以指示它查看标准文件位置并读取文件中的信息。服务对文件内容的处理当然是为该服务定制的。

## DEBUGGING THE SERVICE

由于服务必须在服务控制管理器（Service Control Manager）的上下文中运行，而不是在 Visual Studio 2010 中运行，因此调试服务并不像调试其他 Visual Studio 2010 应用程序类型那样简单。要调试服务，你必须启动服务，然后将调试器附加到其运行的进程中。然后你可以使用 Visual Studio 2010 的所有标准调试功能来调试应用程序。

> 除非你知道该进程是什么并且了解附加到该进程并可能终止该进程的后果，否则不要附加到进程。

![](img/d99870e80390742f93963da7be0b2e61_998_0.png)

为了避免花费这额外的精力，你可能希望在标准的 Windows Forms 应用程序中测试服务中的大部分代码。此测试平台应用程序可以具有与 Windows 服务相同的组件（FileSystemWatchers、EventLogs、Timers 等），因此将能够在事件中运行相同的逻辑。一旦你在此上下文中检查了逻辑，就可以将其复制并粘贴到 Windows 服务应用程序中。

然而，有时服务本身需要直接调试，因此了解如何附加到服务的进程并进行直接调试非常重要。你只能在服务运行时调试服务。当你将调试器附加到服务时，你会中断它。服务在你附加时会被暂停一段时间。当你设置断点并逐步执行代码时，它也会被中断。

附加到服务的进程使你能够调试服务的大部分，但不是全部代码。例如，由于服务已经启动，因此你无法以这种方式调试服务 OnStart 方法中的代码，也无法调试用于加载服务的 Main 方法中的代码。要调试 OnStart 事件或任何 Visual Studio 2010 设计器代码，你必须添加一个虚拟服务并先启动该服务。在虚拟服务中，你将创建要调试的服务的实例。你可以在 Timer 对象中放置一些代码，并在 30 秒左右后创建要调试的对象的新的实例。在新的实例创建之前，留出足够的时间附加调试器。同时，如果需要调试启动代码，请在启动代码中设置断点。

按照以下步骤调试服务：

1. 安装服务。
2. 从服务控制管理器或代码启动服务。
3. 在 Visual Studio 2010 中，加载服务的解决方案。然后从 Debug 菜单中选择 Attach to Process。Attach to Process 对话框出现（见图 30-6）。

![](img/d99870e80390742f93963da7be0b2e61_999_0.png)

FIGURE 30-6

4. 对于 Windows 服务，要附加的目标进程不是前台进程；请确保启用“Show processes from all users”和“Show processes in all sessions”选项旁边的复选框。
5. 在 Available Processes 部分，单击由服务的可执行文件名指示的进程，然后单击 Attach。
6. 现在你可以调试你的进程。在你想要调试的服务的代码中设置断点。通过（例如在监视的目录中放置一个文件）使服务中的代码执行。
7. 完成后，从 Debug 菜单中选择 Stop Debugging。

让我们通过一个实际场景，使用你之前的 FileWatcherService 示例。将 FileWatcherService 项目和 FileWatcherPanel 项目在 Visual Studio 2010 IDE 的两个独立实例中打开。确保 FileWatcherService 服务已启动。

在 FileWatcherService 项目中，选择 Debug → Attach to Process；你将得到一个类似于图 30-6 所示的对话框。选中“Show processes from all users”和“Show processes in all sessions”复选框。这将扩展进程列表，列表中的一个进程将是 FileWatcherService.exe。突出显示它并单击 Attach。现在你已附加到后台运行的 FileWatcherService 进程。

在 OnCustomCommand 事件的第一行设置断点：

```vb
Select Case command
```

现在你已准备好检查调试。打开 FileWatcherPanel 程序并启动它。按下其中一个单选按钮以更改监视的文件扩展名。切换回 FileWatcherService 项目。光标将位于 OnCustomCommand 中的断点行上。你现在可以使用正常命令逐步执行代码。

## SUMMARY

本章介绍了 Windows 服务的一般概述以及如何使用 Visual Basic 创建它。本章中的技术可用于许多不同类型的后台服务，包括以下内容：

- 自动地将统计文件从数据库服务器移动到 Web 服务器
- 在计算机和平台之间推送通用文件
- 看门狗计时器以确保连接始终可用
- 用于移动和处理 FTP 文件，或实际上来自任何来源的文件的应用程序

虽然 Visual Basic 不能用于创建每种类型的 Windows 服务，但它对于创建许多最有用的服务是有效的。.NET Framework 的 Windows 服务类使这种创建相对简单。设计器生成了大部分例行代码，使你作为开发人员能够专注于特定于你的 Windows 服务的代码。

## 31 Assemblies and Reflection

### WHAT YOU WILL LEARN IN THIS CHAPTER

- 什么是程序集以及如何使用它们
- 程序集的一般结构
- 程序集如何进行版本控制
- 全局程序集缓存（GAC），包括何时以及如何使用它
- CLR 如何定位和加载程序集
- 使用反射检查程序集以确定它们包含的类型以及这些类型的接口
- 动态加载程序集，允许你的应用程序注入编译时不可用的功能

到目前为止，你可能已经在 .NET 中开发了一些程序，因此你已经看到了 .NET 编译器生成的模块，其文件扩展名为 .dll 或 .exe。大多数 .NET 模块都是 DLL，包括类库和用作 ASP.NET 代码隐藏的模块。Windows 应用程序、控制台应用程序和 Windows 服务是 .NET 模块的示例，它们是可执行文件，因此扩展名为 .exe。

这些 .NET 编译模块，无论是 DLL 还是 EXE，都被称为程序集。程序集是 .NET 中的部署单元，包含编译后的代码和 .NET 公共语言运行时（CLR）运行代码所需的元数据。元数据包括代码的标识和版本、对其他程序集的依赖关系，以及程序集公开的类型和资源的列表。

在 .NET 中的基本开发不需要你知道更多内容。然而，随着你的应用程序变得更复杂，并且当你开始考虑代码的部署和维护等问题时，你需要更深入地了解程序集。对于高级场景，你还需要知道如何检查程序集以找出它们包含的类型以及这些类型的接口。这种检查能力被称为反射。

熟悉这些基础知识后，第 34 章将使用这些信息深入讨论部署。

