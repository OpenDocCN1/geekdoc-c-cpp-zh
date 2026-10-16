

```csharp
[CallerMemberName] string propertyName = null)
{
    if (!EqualityComparer<T>.Default.Equals(field, value))
    {
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
    public event PropertyChangedEventHandler PropertyChanged;
}
```

> **注意** 实现 INotifyPropertyChanged 接口时使用了 CallerMemberNameAttribute 特性。该特性在第 14 章“错误和异常”中讲解。

QuoteInformation 类的一个实例被赋给 Window 类 MainWindow 的 DataContext，以便直接对其进行数据绑定（代码文件 QuoteClientWPF/MainWindow.xaml.cs）：

```csharp
using System;
using System.Net.Sockets;
using System.Text;
using System.Windows;
using System.Windows.Input;

namespace Wrox.ProCSharp.WinServices
{
    public partial class MainWindow : Window
    {
        private QuoteInformation _quoteInfo = new QuoteInformation();

        public MainWindow()
        {
            InitializeComponent();
            this.DataContext = _quoteInfo;
        }
    }
```

你可以在项目属性的“设置”选项卡中配置用于连接服务器的服务器和端口信息（参见图 39.5）。在这里，你可以为 ServerName 和 PortNumber 设置定义默认值。当 Scope 设置为 User 时，这些设置可以放入特定于用户的配置文件中，因此应用程序的每个用户都可以有不同的设置。Visual Studio 的这一“设置”功能还会创建一个设置类，以便可以使用强类型类来读写这些设置。

![](img/3d365b72b289213a91ade7eb366b8f35_1495_0.png)

**图 39.5**

客户端的主要功能位于“获取引语”按钮的 Click 事件处理程序中：

```csharp
protected async void OnGetQuote(object sender, RoutedEventArgs e)
{
    const int bufferSize = 1024;
    Cursor currentCursor = this.Cursor;
    this.Cursor = Cursors.Wait;
    _quoteInfo.EnableRequest = false;

    string serverName = Properties.Settings.Default.ServerName;
    int port = Properties.Settings.Default.PortNumber;

    var client = new TcpClient();
    NetworkStream stream = null;
    try
    {
        await client.ConnectAsync(serverName, port);
        stream = client.GetStream();
        byte[] buffer = new byte[bufferSize];
        int received = await stream.ReadAsync(buffer, 0, bufferSize);
        if (received <= 0)
        {
            return;
        }
        _quoteInfo.Quote = Encoding.Unicode.GetString(buffer).Trim('\0');
    }
    catch (SocketException ex)
    {
        MessageBox.Show(ex.Message, "Error Quote of the day", MessageBoxButton.OK, MessageBoxImage.Error);
    }
    finally
    {
        stream?.Close();

        if (client.Connected)
        {
            client.Close();
        }
    }

    this.Cursor = currentCursor;
    _quoteInfo.EnableRequest = true;
}
```

启动测试服务器和这个 Windows 应用程序客户端后，你可以测试功能。图 39.6 显示了此应用程序的一次成功运行。

![](img/3d365b72b289213a91ade7eb366b8f35_1496_0.png)

**图 39.6**

此时，你需要在服务器中实现服务功能。程序已经在运行，现在你需要确保服务器程序在系统启动时自动启动，且无需任何人登录系统。你可以通过创建服务程序来实现这一点，接下来将讨论这方面内容。

## Windows 服务程序

使用“新建项目”对话框中的 C# Windows 服务模板，你现在可以创建一个 Windows 服务程序。对于新服务，请使用名称 QuoteService。

单击“确定”按钮创建 Windows 服务程序后，设计器图面会出现，但你不能插入任何 UI 组件，因为应用程序无法直接在屏幕上显示任何内容。本章稍后将使用设计器图面添加安装对象、性能计数器和事件日志记录等组件。

打开此服务的属性，会打开“属性”对话框，你可以在其中配置以下值：

- `AutoLog` — 指定服务启动和停止的事件自动写入事件日志。
- `CanPauseAndContinue`、`CanShutdown` 和 `CanStop` — 指定暂停、继续、关闭和停止请求。
- `ServiceName` — 写入注册表并用于控制服务的服务名称。
- `CanHandleSessionChangeEvent` — 定义服务是否可以处理终端服务器会话中的更改事件。
- `CanHandlePowerEvent` — 对于在笔记本电脑或移动设备上运行的服务，这是一个非常有用的选项。如果启用此选项，服务可以响应低电量事件并相应地改变服务行为。电源事件的示例包括电池电量低、电源状态更改（由于在交流电源和电池之间切换）以及切换到挂起状态。

> **注意** *默认服务名是 `Service1`，无论项目叫什么名称。你只能安装一个 `Service1` 服务。如果在测试过程中遇到安装错误，可能已经安装了一个 `Service1` 服务。因此，请确保在服务开发初期就在“属性”对话框中将服务名称改为更合适的名称。*

在“属性”对话框中更改这些属性，会在 `InitializeComponent` 方法中设置 `ServiceBase` 派生类的值。你已经从 Windows Forms 应用程序中了解了此方法。服务中的使用方式与此类似。

向导会生成代码，但会将文件名改为 `QuoteService.cs`，将命名空间改为 `Wrox.ProCSharp.WinServices`，并将类名改为 `QuoteService`。稍后将详细讨论服务代码。

## ServiceBase 类

`ServiceBase` 类是所有使用 .NET Framework 开发的 Windows 服务的基类。`QuoteService` 类派生自 `ServiceBase`；该类使用一个未公开的辅助类 `System.ServiceProcess.NativeMethods` 与 SCM 通信，而后者只是 Windows API 调用的一个包装类。`NativeMethods` 类是内部类，因此不能在代码中使用。

图 39.7 中的序列图显示了 SCM、`QuoteService` 类以及 `System.ServiceProcess` 命名空间中的类之间的交互。你可以看到对象的生命线是垂直的，而通信是水平进行的。通信按时间顺序从上到下进行。

![](img/3d365b72b289213a91ade7eb366b8f35_1498_0.png)

**图 39.7**

SCM 启动应启动的服务的进程。启动时，会调用 Main 方法。在示例服务的 Main 方法中，会调用基类 ServiceBase 的 Run 方法。Run 使用 NativeMethods.StartServiceCtrlDispatcher 在 SCM 中注册方法 ServiceMainCallback，并向事件日志写入一个条目。

接下来，SCM 在服务程序中调用已注册的方法 ServiceMainCallback。ServiceMainCallback 本身使用 NativeMethods.RegisterServiceCtrlHandler[Ex] 在 SCM 中注册处理程序，并在 SCM 中设置服务状态。然后会调用 OnStart 方法。在 OnStart 中，你需要实现启动代码。如果 OnStart 成功，字符串“Service started successfully”会被写入事件日志。

处理程序是在 ServiceCommandCallback 方法中实现的。当请求服务进行更改时，SCM 会调用此方法。ServiceCommandCallback 方法会将请求进一步路由到 OnPause、OnContinue、OnStop、OnCustomCommand 和 OnPowerEvent。

## 主函数

本节探讨服务进程的由应用程序模板生成的主函数。在主函数中，声明了一个 ServiceBase 类的数组 ServicesToRun。创建 QuoteService 类的一个实例，并作为第一个元素传递给 ServicesToRun 数组。如果此服务进程中应运行多个服务，则必须向该数组添加更多特定服务类的实例。然后，此数组被传递给 ServiceBase 类的静态 Run 方法。通过 ServiceBase 的 Run 方法，你为 SCM 提供了服务入口点的引用。服务进程的主线程现在被阻塞，并等待

