

class on which the service is based, while the ServiceName property changes the name of the service as known to the Service Control Manager.

- 4. 向项目添加安装程序。返回 FileWatcherService 的设计 surface 并右键单击它。选择 Add Installer。会创建一个名为 ProjectInstaller1.vb 的新文件并添加到项目中。ProjectInstaller1.vb 文件在其设计 surface 上添加了两个组件：ServiceProcessInstaller1 和 ServiceInstaller1。

- 5. 在 ProjectInstaller.vb 设计 surface 上，突出显示 ServiceProcessInstaller1 控件。在其 Properties 窗口中，将 Account 属性更改为 LocalSystem。

- 6. 突出显示 ServiceInstaller1 控件。在其 Properties 窗口中，将 DisplayName 属性的值输入为 FileWatcherService。（ServiceName 属性已具有此值。）

- 7. 通过右键单击解决方案并从菜单中选择 Build 来构建项目。服务将创建一个名为 FileWatcherService.exe 的 EXE。

此时，你拥有一个已编译并准备安装的 Windows 服务，但它还没有做任何事情。前面的步骤对于你创建的每个 Windows 服务都非常相似；变化的主要点是名称和你选择使用的账户类型。然而，下一步是特定于某个 Windows 服务的：创建应用程序逻辑以支持 Windows 服务中所需的功功能。

## 向服务添加 .NET 组件

此示例服务将具有监视目录文件更改并记录事件以报告其活动的能力。两个 .NET 组件将促进这些功能：FileSystemWatcher 组件和 EventLog 组件。

## FileSystemWatcher 组件

FileSystemWatcher 组件用于监视特定目录。该组件实现了 Created、Changed、Deleted 和 Renamed 事件，当文件被放置到目录中、更改、删除或重命名时分别触发。

当其中一个事件触发时发生的操作由应用程序开发人员决定。最常见的是包含读取和处理新文件或更改文件的逻辑。然而，你只会将一条消息写入日志文件。

要在项目中实现该组件，请从 Toolbox 的 Components 选项卡将 FileSystemWatcher 控件拖放到 FileWatcherService.vb 的设计 surface 上。（请确保不要将组件拖放到 ProjectInstaller.vb 上。如果 ProjectInstaller.vb 仍是显示的设计 surface，你需要单击 FileWatcherService.vb 设计 surface 的选项卡。）此控件自动命名为 FileSystemWatcher1。

## EnableRaisingEvents 属性

FileSystemWatcher 组件不应在服务初始化并准备好处理事件之前生成任何事件。为防止这种情况，将 FileSystemWatcher1 的 EnableRaisingEvents 属性设置为 False。这会阻止组件触发任何事件。你将在服务中的 OnStart 事件期间启用它。这些由 FileSystemWatcher 组件触发的事件使用稍后讨论的 NotifyFilter 属性进行控制。

## Path 属性

你想要监视的路径是 C: 驱动器上的 TEMP 目录，因此将 Path 属性设置为 C:\TEMP（请确保 C: 驱动器上存在 TEMP 目录）。当然，此路径可以根据你的系统更改为监视任何目录，包括任何网络或可移动驱动器。

## NotifyFilter 属性

对于此示例，你只想监视文件刚刚创建或文件的最后修改值已更改时。为此，将 NotifyFilter 属性设置为 FileName, LastWrite。请注意，你可以通过包含以逗号分隔的列表来指定要监视的多个更改。即使该属性有下拉菜单，你也需要输入值以获得其两部分。

你也可以通过将这些选项作为 NotifyFilter 属性的一部分包含在内来监视其他更改，例如属性、安全、大小和目录名称更改。

## Filter 属性

你将查找的文件类型是文本文件，因此将 Filter 属性设置为 *.txt。请注意，如果你要监视所有文件类型，则 Filter 属性的值将设置为 *.*（这是默认值）。

## IncludeSubdirectories 属性

如果你想监视子目录，你将 IncludeSubdirectories 属性设置为 True。此示例将其保留为 False，即默认值。图 30-2 显示了属性应如何设置。

![](img/d99870e80390742f93963da7be0b2e61_990_0.png)

## 向 OnStart 和 OnStop 添加 FileSystemWatcher 代码

现在一些属性已设置，让我们为 FileWatcherService.vb 的 OnStart 事件添加一些代码。你想要启动 FileSystemWatcher1 组件，以便在文件创建或复制到你正在监视的目录时开始触发事件，因此将 EnableRaisingEvents 属性设置为 True：

```
Protected Overrides Sub OnStart(ByVal args() As String)
' Add code here to start your service. This method should set things
' in motion so your service can do its work.
' Start monitoring for files
FileSystemWatcher1.EnableRaisingEvents = True
End Sub
```

来自 FileWatcherService 的代码片段

在文件监视属性初始化后，你就可以开始监视了。当服务停止时，你需要停止文件监视过程。将以下代码添加到 OnStop 事件：

```
Protected Overrides Sub OnStop()
' Add code here to perform any tear-down necessary to stop your service.
' Stop monitoring for files
FileSystemWatcher1.EnableRaisingEvents = False
End Sub
```

来自 FileWatcherService 的代码片段

## EventLog 组件

现在你可以在服务中放置一个 EventLog 组件以便于记录事件。事件日志在 Windows 操作系统下可用，并在第 6 章中进行了讨论。与许多其他系统级功能一样，.NET 中使用事件日志变得简单，因为 .NET Framework 基类为你完成了大部分工作。

根据你的系统配置和已安装的软件，系统上应该有几个事件日志。通常，你的应用程序应仅写入 Application Log。日志条目的一个属性称为 Source，标识写入消息的应用程序。此属性不必与应用程序的可执行文件具有相同的名称，但通常会赋予该名称以便轻松识别消息的来源。

你可以通过使用事件查看器查看事件日志。在 Windows 2000 上选择 控制面板 ➝ 管理工具 ➝ 事件查看器；在 Windows XP 上选择 开始 ➝ 所有程序 ➝ 管理工具 ➝ 事件查看器；在 Windows Vista 和 Windows 7 上选择 开始 ➝ 控制面板 ➝ 系统和维护 ➝ 管理工具 ➝ 事件查看器。示例使用事件查看器来确保服务正在生成事件。

本章前面提到 ServiceBase 类的 AutoLog 属性决定服务是否自动将事件写入 Application Log。AutoLog 属性指示服务使用 Application 事件日志报告命令失败，以及服务上的 OnStart、OnStop、OnPause 和 OnContinue 事件的信息。实际记录到事件日志的是指示服务是否成功启动和成功停止的条目，以及可能发生的任何错误。

你可以通过在服务的 Properties 窗口中将 AutoLog 属性设置为 False 来关闭事件日志报告，但在此示例中将其保留为 True。这意味着一些事件将自动记录（无需你包含任何代码）。如果需要，你可以向服务添加一些代码以记录 AutoLog 属性未涵盖的额外事件。

从 Toolbox 的 Components 选项卡将 EventLog 控件拖放到 FileWatcherService.vb 的设计器 surface 上。此控件自动命名为 EventLog1。

将 Eventlog1 的 Log 属性设置为 Application，并将 Source 属性设置为 FileWatcherService。

## Created 事件

接下来，你将在 FileSystemWatcher 组件的 Created 事件中放置一些逻辑以记录文件何时被创建。当文件被放置或创建在你正在监视的目录中时触发此事件。它触发是因为文件上的最后修改信息已更改。

在代码编辑器中打开 FileSystemWatcher1.vb。从左侧下拉列表中选择 FileSystemWatcher1，然后从右侧下拉列表中选择 Created。Created 事件将被添加到你的代码中。按如下方式向 Created 事件添加代码：

```
Public Sub FileSystemWatcher1_Created(ByVal sender As Object, _
    ByVal e As System.IO.FileSystemEventArgs) _
    Handles FileSystemWatcher1.Created
    Dim sMessage As String
    sMessage = "File created in directory - file name is " + e.Name
    EventLog1.WriteEntry(sMessage)
End Sub
```

来自 FileWatcherService 的代码片段

请注意，事件参数的对象（事件参数中名为“e”的对象）包含一个名为 Name 的属性。此属性保存生成事件的文件的名称。

此时，你可以以类似的方式添加 FileSystemWatcher 的其他事件（Changed、Deleted、Renamed）并为这些事件创建相应的日志消息。为了保持示例简单，你将仅在此服务中使用 Created 事件。

再次构建服务以编译新功能。你现在准备安装服务并对其进行测试。

