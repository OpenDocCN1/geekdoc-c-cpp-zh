

![](img/3d365b72b289213a91ade7eb366b8f35_1673_0.png)

**图43.5**

## 分组连接

通常，你并不想在所有客户端之间通信，而是希望在一组客户端之间通信。SignalR 对这种场景提供了开箱即用的支持。

在本节中，你将添加另一个具有分组功能的聊天中心，并了解使用 SignalR 中心的其他可行选项。WPF 客户端应用程序将扩展为进入组并向选定的组发送消息。

### 使用分组扩展中心

为了支持群聊，你需要创建 `GroupChatHub` 类。在前面的中心中，你已经看到了如何使用 `dynamic` 关键字定义发送给客户端的消息。除了使用动态类型，你还可以创建一个自定义接口，如下面的代码片段所示。该接口被用作基类 `Hub` 的泛型参数（代码文件 ChatServer/GroupChatHub.cs）：

```
public interface IGroupClient
{
    void MessageToGroup(string groupName, string name, string message);
}
```

```
public class GroupChatHub: Hub<IGroupClient>
{
    // etc.
}
```

`AddGroup` 和 `LeaveGroup` 是定义为由客户端调用的方法。注册组时，客户端使用 `AddGroup` 方法发送一个组名。`Hub` 类定义了一个 `Groups` 属性，可以在其中注册到组的连接。`Hub` 类的 `Groups` 属性返回 `IGroupManager`。此接口定义了两个方法：`Add` 和 `Remove`。这两个方法都需要一个组名和一个连接标识符，以向组中添加或移除指定连接。连接标识符是与客户端连接关联的唯一标识符。客户端连接标识符——以及有关客户端的其他信息——可以通过 `Hub` 类的 `Context` 属性访问。下面的代码片段调用 `IGroupManager` 的 `Add` 方法来使用连接注册组，并调用 `Remove` 方法来注销组（代码文件 ChatServer/GroupChatHub.cs）：

```
public Task AddGroup(string groupName) =>
    Groups.Add(Context.ConnectionId, groupName);

public Task LeaveGroup(string groupName) =>
    Groups.Remove(Context.ConnectionId, groupName);
```

> 注意 `Hub` 类的 `Context` 属性返回一个 `HubCallerContext` 类型的对象。通过该类，你不仅可以访问与连接关联的连接标识符，还可以访问有关客户端的其他信息，例如 HTTP 请求中的标头、查询字符串和 Cookie 信息，以及有关用户的信息。这些信息可用于用户身份验证。

调用 `Send` 方法——这次带有包括组在内的三个参数——将信息发送到与该组关联的所有连接。现在使用 `Clients` 属性来调用 `Group` 方法。`Group` 方法接受一个组字符串，将 `MessageToGroup` 消息发送到与该组名关联的所有连接。通过 `Group` 方法的一个重载，你可以添加应排除的连接 ID。因为 `Hub` 实现了 `IGroupClient` 接口，所以 `Groups` 方法返回 `IGroupClient`。这样，就可以在编译时支持下调用 `MessageToGroup` 方法（代码文件 ChatServer/GroupChatHub.cs）：

```
public void Send(string group, string name, string message)
{
    Clients.Group(group).MessageToGroup(group, name, message);
}
```

还定义了一些其他扩展方法，用于向客户端连接列表发送信息。你已经看到了 `Group` 方法，它用于向由组名指定的一组连接发送消息。通过此方法，你可以排除客户端连接。例如，发送消息的客户端可能不需要接收它。`Groups` 方法接受一个组名列表，消息会发送到这些组。你已经看到了 `All` 属性，它用于向所有已连接的客户端发送消息。排除向调用者发送消息的方法是 `OthersInGroup` 和 `OthersInGroups`。这些方法会向一个特定组（排除调用者）发送消息，或者向一组组（排除调用者）发送消息。

你也可以向不基于内置分组功能的自定义组发送消息。此时，你可以重写 `OnConnected`、`OnDisconnected` 和 `OnReconnected` 方法。每次客户端连接时都会调用 `OnConnected` 方法；客户端断开连接时会调用 `OnDisconnected` 方法。在这些方法中，你可以访问 `Hub` 类的 `Context` 属性，以获取客户端信息以及客户端关联的连接 ID。在这里，你可以将连接信息写入共享状态，以便通过访问同一共享状态的多个实例来使服务器可扩展。你也可以基于自己的业务逻辑选择客户端，或者在发送消息时实现优先级，以优待特定客户端。

```
public override Task OnConnected()
{
    return base.OnConnected();
}

public override Task OnDisconnected(bool stopCalled)
{
    return base.OnDisconnected(stopCalled);
}
```

### 使用分组扩展 WPF 客户端

在中心的分组功能准备好之后，你可以扩展 WPF 客户端应用程序。对于分组功能，定义了另一个与 `GroupChatViewModel` 类关联的 XAML 页面。

与之前定义的 `ChatViewModel` 相比，`GroupChatViewModel` 类定义了一些额外的属性和命令。`NewGroup` 属性定义了用户要注册的组。`SelectedGroup` 属性定义了用于后续通信（例如向组发送消息或离开组）的组。`SelectedGroup` 属性需要进行更改通知，以便在更改该属性时更新用户界面；这就是为什么 `GroupChatViewModel` 类实现了 `INotifyPropertyChanged` 接口，并且 `SelectedGroup` 属性的 set 访问器会触发通知。加入和离开组的命令也一并定义了：`EnterGroupCommand` 和 `LeaveGroupCommand` 属性（代码文件 WPFChatClient/ViewModels/GroupChatViewModel.cs）：

```
public sealed class GroupChatViewModel: IDisposable,
INotifyPropertyChanged
{
    private readonly IMessagingService _messagingService;
    public GroupChatViewModel(IMessagingService messagingService)
    {
        _messagingService = messagingService;

        ConnectCommand = new DelegateCommand(OnConnect);
        SendCommand = new DelegateCommand(OnSendMessage);
        EnterGroupCommand = new DelegateCommand(OnEnterGroup);
        LeaveGroupCommand = new DelegateCommand(OnLeaveGroup);
    }

private const string ServerURI
="http://localhost:45269/signalr";

public event PropertyChangedEventHandler PropertyChanged;

public string Name { get; set; }
public string Message { get; set; }
public string NewGroup { get; set; }

private string _selectedGroup;
public string SelectedGroup
{
    get { return _selectedGroup; }
    set
    {
        _selectedGroup = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(
            nameof(SelectedGroup)));
    }
}

public ObservableCollection<string> Messages { get; } =
    new ObservableCollection<string>();
public ObservableCollection<string> Groups { get; } =
    new ObservableCollection<string>();

public DelegateCommand SendCommand { get; }
public DelegateCommand ConnectCommand { get; }
public DelegateCommand EnterGroupCommand { get; }
public DelegateCommand LeaveGroupCommand { get; }
// etc.
}
```

下面的代码片段展示了 `EnterGroupCommand` 和 `LeaveGroupCommand` 命令的处理程序方法。在这里，`AddGroup` 和 `RemoveGroup` 方法会在组中心内被调用（代码文件 WPFChatClient/ViewModels/GroupChatViewModel.cs）：

```
public async void OnEnterGroup()
{
    try
    {
        await _hubProxy.Invoke("AddGroup", NewGroup);
        Groups.Add(NewGroup);
        SelectedGroup = NewGroup;
    }
    catch (Exception ex)
    {
        _messagingService.ShowMessage(ex.Message);
    }
}

public async void OnLeaveGroup()
{
    try
    {
        await _hubProxy.Invoke("RemoveGroup", SelectedGroup);
        Groups.Remove(SelectedGroup);
    }
    catch (Exception ex)
```

