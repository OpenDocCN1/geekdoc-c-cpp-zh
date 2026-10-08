

```cs
{
  Dispatcher.BeginInvoke(new Action(
    {
      for (var i = 0; i < Requests.Count; i++)
      {
        if (Requests[i].RequestsID != requestID) continue;
        var request = Requests[i];
        request.Status = status;
        Requests[i] = request;
        RequestList.SelectedIndex = i;
        RequestList.Focus();
        break;
      }
    }));
  } //
}
```

`Window_Loaded` 事件处理方法将 `RequestClientProxy` 的 `AppInstance` 属性设置为应用程序创建的窗口实例。使用 `Dispatcher.BeginInvoke` 更新 UI，是因为 `AddDNRequestToList` 和 `UpdatedDNRequest` 方法是从工作流实例的线程调用的，而不是 UI 线程。

## 挂起工作流实例

工作流最令人兴奋的部分是它的执行会被挂起，直到适当的用户对请求的领域做出决策。在简单的应用程序中，你可以将其实现为阻塞调用，直到用户指定所需的输入。但在工作流的世界，这并不是一个恰当的解决方案。

该请求简单地挂起工作流实例，将其从内存中移除，并释放该实例持有的资源，当然，还会将工作流持久化以便稍后恢复。这一步在工作流中使用 `WaitForApproval` 自定义活动进行定义：

```
WaitForApproval
{
  BookmarkName = "ApproveRequest";
  Status = new OutArgument<string>(ctx => status.Get(ctx))
}
```

挂起和恢复工作流实例是通过一个名为“书签”（bookmark）的概念完成的。书签是工作流中需要记住的一个点。`WaitForApproval` 活动允许工作流开发者设置此书签的名称（`Bookmark` 属性）。不过，也可以将其硬编码到活动中。当用户提供输入且工作流恢复时，`Status` 输出参数将检索预期的用户输入。

列表 11-14 显示了 `WaitForApproval` 的定义。

## 列表 11-14：WaitForApproval.cs

```cs
using System.IdleActivities;

namespace RequestClient.Activities
{
    public class WaitForApproval: NativeActivity
    {
        public string BookmarkName { get; set; }
        public OutArgument<string> Status { get; set; }

        protected override void Execute(NativeActivityContext context)
        {
            context.CreateBookmark(BookmarkName, ctx, bookmark, obj) => Status.Set(ctx, obj.ToString());
        }

        protected override bool CanInduceIdle { get { return true; } }
    }
}
```

[WaitForApproval.cs] 代码文件可在 Wrox.com 下载。

这个简单的定义在幕后执行了大量工作。`CanInduceIdle` 属性被设置为 `true`。此设置非常重要，因为它允许工作流扩展空闲状态以等待书签恢复。

`Execute` 方法调用了 `CreateBookmark` 方法，传递了书签名称以及在书签恢复时调用的委托。该委托（在此处使用 Lambda 表达式实现）接受三个参数。第一个参数 `ctx` 是一个 `NativeExecutionContext`。`Bookmark` 是一个 `Bookmark` 对象（在此处未使用），`obj` 是一个表示用户输入的对象。当工作流恢复时，输入对象会被传递给用户，并在此处通过 `obj` 接收委托接收。如你所见，此对象被简单存储在该活动的参数中。

## 配置 SqlWorkflowInstanceStore

执行 `WaitForApproval` 方法会导致工作流实例不仅被挂起，而且被持久化。这是通过 `SqlWorkflowInstanceStore` 对象实现的，它是一个特殊的内置工作流扩展（你可以将其看作工作流的插件组件）。如果工作流中安装了扩展，活动就可以运行，你可以使用扩展的服务。

`SqlWorkflowInstanceStore` 派自 `System.Runtime.DurableInstancing` 命名空间中的 `InstanceStore`。你可以从 `InstanceStore` 派生自己的持久化机制，将工作流状态保存到另一个持久存储中（例如保存到 XML 文件）。

以下来自 `MainWindow.xaml` 的片段显示了如何准备、配置和使用 `InstanceStore`：

```cs
public partial class MainWindow
{
    public ObservableCollection<DNRequest> Requests { get; set; }
    private string PersistenceConnStr;
    private InstanceStore InstanceStore { get; set; }
}
```

```cs
public MainWindow()
{
    InitializeComponent();
}
```

```cs
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    var config = ConfigurationManager;
    OpenExeConfiguration(ConfigurationUserLevel.None);
    _PersistenceConnStr = ((ConnectionStringsSection)config.
    GetConnectionString("connectionStrings")).ConnectionString;
    ConnectionStrings("Persistence").ConnectionString;
    InstanceStore = new SqlInstanceStore(_PersistenceConnStr);
}
```

```cs
var view = InstanceStore.Execute(InstanceStore.CreateInstanceHandler(),
new WorkflowOwnerCommand(
TimeSpan.FromSeconds(30));
InstanceStore.DefaultInstanceOwner = view.InstanceOwner;
// ...
RequestClientProxy.AppInstance = this;
// ...
```

```cs
private void OnRequestButtonClick(object sender, RoutedEventArgs e)
{
    var parameters = new Dictionary<string, object>
    {
        {"DomainName", DomainNameBox.Text}
    };
    var wkf = new WorkflowApplication(new ProcessDomainRequest(
parameters));
    ConfigureWorkflow(wf);
    wkf.Run();
}
```

```cs
private void ConfigureWorkflow(WorkflowApplication wf)
{
    wf.InstanceStore = InstanceStore;
    wf.PersistableIdle = e => PersistableAction.Unload();
}
// ...
```

`Window_Loaded` 方法负责准备供所有工作流实例使用的 `SqlWorkflowInstanceStore` 对象。`Window_Loaded` 首先查询应用程序配置文件获取连接字符串，并将其传递给新创建的 SQL Store 实例，该实例被立即存储在 `InstanceStore` 字段中。后续语句将应用程序注册为工作流主机，作为持久化数据库的锁者。

`OnButtonClick` 事件处理器创建一个新的工作流实例并传递工作流参数。在调用同步执行工作流的 `Run` 方法之前，它调用 `ConfigureWorkflow` 方法将准备好的 `InstanceStore` 扩展传递给该工作流实例：

```cs
wf.InstanceStore = InstanceStore;
wf.PersistableIdle = e => PersistableAction.Unload;
```

`PersistableIdle` 事件属性在工作流即将持久化时被调用。你可以在这里添加任何自定义的持久化操作。默认返回 `PersistableAction.Unload`。它会导致工作流在状态保存后从内存中卸载（并释放资源）。
