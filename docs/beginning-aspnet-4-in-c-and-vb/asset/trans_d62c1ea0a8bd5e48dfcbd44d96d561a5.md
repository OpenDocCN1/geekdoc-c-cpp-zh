
```
textStatus.Text += String.Format("{0:T}: Registered for recovery\n", DateTime.Now);
App.Source.TraceEvent(TraceEventType.Verbose, 0, "Registered for recovery");
}
```

DoRecovery() 是由 RegisterForApplicationRecovery() 方法调用定义的回调方法，并由 WER 调用。在处理程序中，通过调用 ApplicationRecoveryInProgress() 方法通知恢复管理器恢复正在进行中。该方法在用户取消恢复时返回 true。可以在恢复期间验证用户是否取消，以便在用户取消时停止恢复。在这里，TextBox 的内容被写入在应用程序重新启动时使用的临时文件。恢复过程结束时，通过调用 ApplicationRecoveryFinished() 通知重启管理器其成功。

```
private int DoRecovery(object state)
{
    App.Source.TraceEvent(TraceEventType.Verbose, 0, "begin Recovery");
    this.tempPath = (string)state;
    bool canceled = ApplicationRestartRecoveryManager.
        ApplicationRecoveryInProgress();
    if (canceled)
    {
        textStatus.Text += String.Format
            ("{0:T}: Recovery canceled, shutting down\n", DateTime.Now);
        App.Source.TraceEvent(TraceEventType.Verbose, 0,
            "end Recovery with cancel");
        ApplicationRestartRecoveryManager.ApplicationRecoveryFinished(
            false);
        return 0;
    }
    SaveFile(tempPath);
    App.Source.TraceEvent(TraceEventType.Verbose, 0, "end Recovery");
    ApplicationRestartRecoveryManager.ApplicationRecoveryFinished(true);
    return 0;
}
```

完成以上设置后，您可以运行应用程序，如图 A-2 所示。底部的 TextBlock 提供状态信息，例如何时进行重启和恢复注册，以及在 60 秒后，应用程序现在可以崩溃的信息。

![](img/d7d2ffa0a76feaab821930e95daace93_1464_0.png)

图 A-2

选择菜单 Action ▸ Crash 会调用处理程序方法 OnCrash()，该方法执行快速失败。Environment.FailFast() 方法可用于快速终止进程。该方法在进程终止前写入应用程序事件日志并创建应用程序转储。仅执行 CriticalFinalizerObject 对象。Try-finally 块和终结器不会执行。

```
private void OnCrash(object sender, ExecutedRoutedEventArgs e)
{
    Environment.FailFast("RestartDemo stopped from Menu command");
}
```

崩溃后，应用程序将被重新启动，您可以看到图 A-3 所示的对话框。

![](img/d7d2ffa0a76feaab821930e95daace93_1464_1.png)

图 A-3

## 用户账户控制

作为开发者，用户账户控制 (UAC) 是在 Windows Vista 中即可立即看到的功能之一：每次执行管理任务时，都会弹出对话框要求管理员权限。在 Windows 7 中，您现在可以配置此功能，如图 A-4 所示。默认设置是如果操作系统自带应用程序需要管理员更改，则不提供通知。

![](img/d7d2ffa0a76feaab821930e95daace93_1465_0.png)

图 A-4

这些对话框的麻烦背后有什么目的？虽然 Windows 指南一直提到如果不是真正必要，应用程序不应要求管理员权限，但许多应用程序仍需要以管理员账户运行。例如，普通用户不允许向程序文件目录写入数据；需要管理员权限。由于许多应用程序因开发者未遵循指南而在没有管理员权限的情况下无法运行，许多用户使用管理员账户登录系统。通过在日常工作中使用管理员账户，您可能会无意中安装特洛伊木马程序。

Windows Vista 及更高版本通过默认情况下管理员不具有管理员权限来避免此问题。进程与其关联有两个安全令牌，一个具有普通用户权限，一个具有管理员权限（当以管理员账户登录时）。对于需要管理员权限的应用程序，用户可以将应用程序提升为以管理员权限运行。这可以通过上下文菜单中的“以管理员身份运行”选项完成，或者可以配置应用程序的兼容性属性，使其始终需要管理员权限才能运行。此设置在注册表中添加应用程序兼容性标志，位置为 `HKCU\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers`，值为 `RUNASADMIN`。

### 需要管理员权限的应用程序

对于需要管理员权限的应用程序，您还可以添加应用程序清单。Visual Studio 2010 具有向应用程序添加应用程序清单的项目模板。此类清单可以通过向现有应用程序添加清单文件或在程序集中嵌入 Win32 资源文件来创建。在项目属性的应用程序选项卡中，您可以选择作为本机资源包含的应用程序清单文件。

应用程序清单是一个类似于应用程序配置文件的文件。虽然应用程序配置文件的文件扩展名为 .config，但清单以 .manifest 结尾。文件名必须设置为应用程序的名称，包括 .exe 文件扩展名后跟 .manifest。Visual Studio 重命名并复制 app.manifest 文件，就像处理应用程序配置文件一样。清单文件包含 XML 数据，如下所示。根元素是 <assembly>，它包含子元素 <trustInfo>。管理员要求由 <requestedExecutionLevel> 元素的 level 属性定义。

```
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1" xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
    <security>
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
        <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
      </requestedPrivileges>
    </security>
  </trustInfo>
</asmv1:assembly>
```

*代码片段 AdminRightsRequired\app.manifest*

以这种方式启动应用程序时，会出现提升提示，询问用户是否信任该应用程序以管理员权限运行。

使用 requestedExecutionLevel 设置，您可以指定值 requireAdministrator、highestAvailable 和 asInvoker。值 highestAvailable 表示应用程序获得用户拥有的权限——但只有在获得用户同意后。值 requireAdministrator 需要管理员权限。如果用户未以管理员身份登录系统，则会出现登录对话框，用户可以在其中以管理员身份为该应用程序登录。值 asInvoker 表示应用程序以用户的身份令牌运行。

uiAccess 属性指定应用程序是否需要向桌面上更高权限级别的窗口输入。例如，屏幕键盘需要向桌面上的其他窗口驱动输入，因此应将设置设为 true，以便应用程序显示屏幕键盘。非 UI 访问应用程序应将此属性设置为 false。

![](img/d7d2ffa0a76feaab821930e95daace93_1466_0.png)

### 盾形图标

如果应用程序或应用程序中的任务需要管理员权限，用户会通过易于识别的盾形图标得到通知。盾形图标附加到需要提升的控件上。用户期望在单击带有盾牌的项目时看到提升提示。图 A-5 和图 A-6 显示了盾牌的使用情况。任务管理器需要提升权限才能查看所有用户的进程。在用户账户中，添加或删除用户账户以及设置家长控制都需要提升权限。

