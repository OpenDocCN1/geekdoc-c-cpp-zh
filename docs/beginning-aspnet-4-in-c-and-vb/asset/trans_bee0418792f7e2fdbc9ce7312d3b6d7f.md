
抽象类 `SyndicationFeedFormatter` 的具体实现定义了使用哪些属性以及它们如何被翻译为特定格式。

本章结束了本书的通信部分。你已阅读过直接使用套接字以及所提供的抽象层的通信技术。Windows Communication Foundation 是在多章中讨论过的技术。借助消息队列（第 46 章，“消息队列”），WCF 提供了断开式通信模型。

仍有更多内容可读。附录涵盖了 Windows API 代码包，即 Windows 7 和 Windows Server 2008 R2 的 .NET 扩展，以及在这些平台上开发应用程序的指南。

你的 .NET 应用程序。你可以从 http://code.msdn.microsoft.com/WindowsAPICodePack 下载 Windows API Code Pack。此工具包与本附录中的大多数示例一起使用。你可以使用此工具包附带的库，或将源代码复制到你的应用程序中。通常，此工具包中的类是对 Windows API 的薄封装。

另一个可用于面向 Windows 平台应用程序的工具包是 Windows 软件徽标工具包。在 Microsoft 下载页面上，你可以找到 Windows 7 客户端软件徽标计划文档和工具包，其中包含有关应用程序获得 Windows 7 软件徽标所需信息的说明。即使你对为应用程序获取徽标不感兴趣，此文档和工具包仍然很有趣，因为它解释了应用程序在 Windows 操作系统上被视为良好行为所需的条件。

应用程序获得徽标的要求是什么？以下是要求简要列表；你可以在 Windows 7 客户端软件徽标文档中获取更多详细信息。

- 应用程序不得包含间谍软件或恶意软件。当然，这是每个应用程序都应满足的要求。有趣的是，这在徽标合规性方面会得到验证。
- 不得替换 Windows 资源受保护的文件。
- 错误必须使用 Windows 错误报告 (WER) 报告。
- 应用程序必须能够干净地安装和卸载。阅读第 17 章“部署”，了解创建安装程序的信息。应用程序不应在安装时强制重新启动。
- 应用程序应安装到正确的文件夹中。用户数据不应写入应用程序文件夹。在本附录的“目录结构”部分中，你可以阅读如何找到应用程序和用户数据的正确文件夹。
- 文件和驱动程序必须经过数字签名。阅读第 21 章“安全”，了解如何签名应用程序的信息。
- 必须支持 64 位系统。这意味着不允许 16 位代码。在 64 位系统上运行 32 位应用程序是可以的。对于 .NET 应用程序，你可以将平台配置设置为 Any CPU、x86、x64 或 Itanium。Any CPU 使你的应用程序在 32 位平台上以 32 位运行，在 64 位平台上以 64 位运行。当你将配置设置为 Any CPU 时，不能在程序集中直接使用平台调用封装本地代码。使用本地代码会将你限制为所使用的本地代码本地 API 调用，因此 Any CPU 在两个版本上都无法工作。
- 安装时必须进行版本检查，以检查操作系统是否具有所需的最低版本，但不允许检查特定版本。
- 必须遵循用户账户控制指南。这在本附录中进行了详细讨论。
- 应用程序不得阻止关机。你可以使用重启管理器在重新启动或故障后将应用程序恢复到工作状态。这在“应用程序恢复”部分中进行了讨论。
- 必须支持多用户会话。一个系统上的不同用户应能够使用该应用程序。此要求是由于 Windows 的快速用户切换功能。

## 应用程序恢复

也许你已经看到过某些应用程序在崩溃或系统重新启动后会恢复到之前的状态。此类应用程序（例如 Microsoft Office 和 Visual Studio）使用 Application Recovery and Restart (ARR) API，该 API 自 Windows Vista 起就是 Windows API 的一部分。

应用程序可以向重启管理器注册，如果应用程序崩溃或变得无响应（运行至少 60 秒后），Windows 错误报告 (WER) 会重新启动应用程序。应用程序还可以注册恢复，以便在应用程序挂起时进行恢复。

为了实际演示，此示例展示了简单 WPF 编辑器的创建。此应用程序在失败时注册重启和恢复。用于读写文件的类 CurrentFile 定义了 IsDirty

```
{
    Source.TraceEvent(TraceEventType.Verbose, 0,
        "*RestartDemo begin OnStartup*");
    foreach (var arg in e.Args)
    {
        Source.TraceEvent(TraceEventType.Verbose, 0,
            String.Format("argument {0}: {1}", arg));
        if (arg.StartsWith("/restart:", StringComparison.InvariantCultureIgnoreCase))
        {
            Source.TraceEvent(TraceEventType.Verbose, 0,
                "/restart: argument found");
            RestartPath = arg.Substring(9);
            Source.TraceEvent(TraceEventType.Verbose, 0,
                String.Format("RestartPath: {0}", RestartPath));
        }
    }
    public string RestartPath { get; private set; }
}
```

代码片段 EditorDemo/App.xaml.cs

主窗口（见图 A-1）仅包含中间区域用于编辑文本的 TextBox、底部区域用于状态消息的 TextBlock 控件以及一个菜单控件。

MainWindow 类的构造函数通过检查 App 类中的 RestartPath 属性来检查应用程序是否从恢复中启动。如果应用程序因恢复而启动，则分配给 RestartPath 属性的文件名将用于加载该文件并将其分配给 TextBox 的 DataContext。如果应用程序正常启动，则会创建一个新的恢复文件名。

![](img/d7d2ffa0a76feaab821930e95daace93_1461_0.png)

图 A-1

在构造函数内部，还创建了一个 DispatcherTimer，它在 60 秒后触发。这用于通知用户应用程序只能在运行至少 60 秒后从崩溃中恢复。

在此场景中，最重要的调用是辅助方法 RegisterForRestart() 和 RegisterForRecovery()，它们用于向重启管理器注册。

```
using System;
using System.Diagnostics;
using System.Threading;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Input;
using System.Windows.Threading;
using Microsoft.WindowsAPICodePack.ApplicationServices;

namespace Wrox.ProCSharp.Windows7
{
    public partial class MainWindow : Window
    {
        private DispatcherTimer minuteTimer;
```

```
private void On60Seconds(object sender, EventArgs e)
{
    this.textStatus.Text += String.Format("{0:T}: Application can crash " +
        "\\n\\r\\n", DateTime.Now);
    minuteTimer.Stop();
}
```

RegisterForRestart() 方法调用 ApplicationRestartRecoveryManager 类的 RegisterForApplicationRestart() 方法。ApplicationRestartRecoveryManager 定义在命名空间 Microsoft.WindowsAPICodePack.ApplicationServices 中。RegisterForApplicationRestart() 方法封装了 Windows API 调用 RegisterApplicationRestart() 函数。通过此方法，你可以定义用于重新启动应用程序的命令行参数以及不重新启动应用程序的情况。在此示例中，定义应用程序不应在重新启动或安装补丁时重新启动。你还可以指定应用程序不应在应用程序崩溃和应用程序挂起时重新启动。

```
private void RegisterForRestart()
{
    var settings = new RestartSettings(
        String.Format("/restart:{0}", tempPath),
        RestartRestrictions.NotOnReboot | RestartRestrictions.NotOnPatch);
    ApplicationRestartRecoveryManager.RegisterForApplicationRestart(
        settings);
    textStatus.Text += String.Format("{0:T}: Registered for restart\\n",
        DateTime.Now);
    App.Source.TraceEvent(TraceEventType.Verbose, 0,
        "Registered for restart");
}
```

在 Windows API Code Pack 中，Windows API 调用被定义为使用 P/Invoke 调用：

```
[DllImport("kernel32.dll")]
[PreserveSig]
internal static extern HRESULT RegisterApplicationRestart(
    [MarshalAs(UnmanagedType.BStr)] string commandLineArgs,
    RestartRestrictions flags);
```

![](img/d7d2ffa0a76feaab821930e95daace93_1463_0.png)

通过此功能，如果应用程序崩溃或挂起，则会重新启动。通过重启管理器，你还可以定义一个在应用程序因崩溃或挂起而停止之前调用的处理程序方法。这是通过调用 ApplicationRestartRecoveryManager 类的 RegisterForApplicationRecovery() 方法完成的。此方法封装了 Windows API 函数 RegisterApplicationRecoveryCallback()。RegisterForApplicationRecovery() 可以使用 RecoverySettings 类型的对象进行配置。通过 RecoverySettings，你分配 RecoveryData 类型的对象和恢复 ping 间隔。此 ping 间隔以 100 ns 为单位定义，并且回调方法必须在此时间范围内向恢复管理器提供进度信息。默认情况下，值为 0 时时间间隔为 5 秒。可以设置的最大值为 5 分钟。通过 RecoveryData，你指定由重启管理器调用以执行恢复的方法，以及传递给该方法的参数：

```
private void RegisterForRecovery()
{
    var settings = new RecoverySettings(new RecoveryData(
        DoRecovery, tempPath), 0);
    ApplicationRestartRecoveryManager.RegisterForApplicationRecovery(
        settings);
}
```
