
```csharp
public void Main(Project client)
{
    if (SucceedingRuleHelper.AnyOutcomesSuccessfully(client))
    {
        AllPathTasksFinished(client);
        // 开始自定义代码
        XmlDocument xmlDoc = new XmlDocument();
        xmlDoc.LoadXml(client.ProcessInstance.XmlFields["TestForm"].Value);
        XmlNamespaceManager namespaceManager = new XmlNamespaceManager(xmlDoc);
        namespaceManager.AddNamespace("my", xmlDoc.DocumentElement.NamespaceURI);
        
        xmlDoc.SelectSingleNode("my:fields/my:DataField", namespaceManager).InnerText = client.ActivityInstance.DataFields["Outcome"].ToString();
        client.ProcessInstance.XmlFields["TestForm"].Value = xmlDoc.OuterXml;
        // 结束自定义代码
    }
    else
    {
        InfoPathTasksFinished(client);
        client.SucceedingRule = false;
    }
}
```

如果你使用“Just Once”（仅执行一次）选项，应该注意只有一个带有一个或多个槽（slots）的活动实例。如果你想遍历操作列表，这里有一个可以使用的代码段：

```csharp
for (int i = 0; i < ActivityInstance.WorklistSlots.Count; i++) {
    Console.WriteLine("Action Result: " + ActivityInstance.WorklistSlots[i].DataFields["Action Result"].ToString());
    Console.WriteLine("Destination User: " + ActivityInstance.WorklistSlots[i].User.Name.ToString());
}
```

### 在 K2 blackpearl SharePoint 模板中处理多个

在 K2 blackpearl 中，当你使用 SharePoint 模板时，支持多种功能，例如上传和下载文档（高级模式下的多个文档）、提交（check-in）、签出（check-out）、更新元数据等。

这里的挑战在于，如果你需要对多个文档执行这些操作，该如何做？目前没有内置功能，但这并不意味着无法实现。以下步骤显示了该技术如何适用于 K2 向导中的所有功能，包括上传、下载和更新元数据；签出；提交；签出。

1. 创建文档向导功能。在此示例中仅显示了更改，而不是整个代码段：

```csharp
foreach (XmlNode checkItem in checkItems)
{
    foreach (string docName in ProcessInstance.DataFields["FileName"].Value.ToString().Split('/'))
    {
        if (bool.Parse(checkItem.SelectSingleNode("UsePartOfItems").InnerText))
        {
            // ...
            checkInSet += "<DocumentName>" + docName + "</DocumentName>";
            // ...
        }
        else
        {
            // ...
            checkInSet += "<DocumentName>" + docName + "</DocumentName>";
        }
    }
}
```

### 最佳实践 —— 主机服务器连接

在使用 `Connection` 对象时，有一些提示。该对象是 API 继承的基 API 的（`SmartObjectClientServer`、`SmartObjectManagementServer` 等）。

以下子章节显示了基于通过 API 连接到服务器的三场景示例代码。

#### 场景 1：打开和关闭多个连接

这是使用连接最昂贵的方式，会产生最大的开销。在 `Connection` 对象的每个 `Open` 方法之后，都会在服务器上进行身份验证，这就是产生最大开销的原因。这种场景通常用于无状态环境，即方法调用之间不存在用户上下文，例如无会话 Web 应用程序。

# 附录 A：K2 blackpearl 技巧与窍

## 场景 2：一个连接执行多次操作

这是一种更高效连接方法。你可以在 API 之间共享 Connection 对象，使连接更容易管理。

```csharp
SmartObjectManagementServer _mgmtServer = new SmartObjectManagementServer();
SmartObjectClientServer _clientServer = new SmartObjectClientServer();
```

```csharp
string _conString = "Integrated=True;IsPrimaryKey=True;Authenticate=True;EncryptedPassword=False;Host=blackpearl;Port=5555;";

SCConnectionStringBuilder _connBuilder = new SCConnectionStringBuilder(_conString);

_mgmtServer.CreateConnection();
_clientServer.Connection = _mgmtServer.Connection;

_mgmtServer.Connection.Open(_connBuilder.ToString());
SmartObjectExplorer smoExplorer = _mgmtServer.GetObjects(SmartObjectInfo.System);
SmartObject smo = _clientServer.GetObject(smoExplorer.Objects["*USER"].Guid);
smo.ListMethods[smo.MethodToExecute = "*Users*"];
smo.ListMethods[smo.MethodToExecute].Parameters["*Name"].Value = "*K2*";
SmartObjectList userList = _clientServer.ExecuteList(smo);

_mgmtServer.Connection.Close();
```

## 场景 3：使用会

如果调用的客户端具有状态并可以管理会，这就是与 Connection 对象配合使用的方法。可以设置服务器上的会超时时间。但是，它适用于整个服务器，这意味着托管在该服务器上的所有服务器。默认时间为 20 分钟。如果会超时且你在未进行身份验证（Authenticate=true）的情况下进行 API 调用，将得到异常。

这种方法是处理具有会状态（session state）连接的最有效方式。

```csharp
SmartObjectManagementServer _mgmtServer = new SmartObjectManagementServer();
SmartObjectClientServer _clientServer = new SmartObjectClientServer();
```

```csharp
string _conString = "Integrated=True;IsPrimaryKey=True;Authenticate=True;EncryptedPassword=False;Host=blackpearl;Port=5555;";

SCConnectionStringBuilder _connBuilder = new SCConnectionStringBuilder(_conString);

_mgmtServer.CreateConnection();
```

```csharp
_clientServer.Connection = _mgmtServer.Connection;

_mgmtServer.Connection.Open(_connBuilder.ToString());
string sessionID = _mgmtServer.Connection.GetResumableSessionCookie();

SmartObjectExplorer smo = _mgmtServer.GetSmartObjects(SmartInfoType.System);
_mgmtServer.Connection.Close();
```

```csharp
//Time elapse = ...
SmartObject smo = null;
try {
    _connBuilder.Authenticate = false;
    _clientServer.Connection.Open(_connBuilder.ToString());
    _clientServer.Connection.ResumeSession(sessionID);
    smo = _clientServer.GetSmartObject((smoExplorer.SmartObjects["UMUser"].Guid);
    _clientServer.Connection.Close();
} catch (Exception ex) {
    Console.WriteLine(ex.Message);
}
```

```csharp
// Some more time elapse...
if (smo != null) {
    SmartObjectList userList;
    try {
        smo.MethodToExecute = "Get_Users";
        smo.ListMethods[smo.MethodToExecute].Parameters["Label Name"].Value = "k2";
        _clientServer.Connection.Open(_connBuilder.ToString());
        userList = _clientServer.ExecuteList(smo);
        _clientServer.Connection.EndSession(sessionID);
        _clientServer.Connection.Close();
    } catch (Exception ex) {
    Console.WriteLine(ex.Message);
    }
}
```

## 升级中的默认结果

作者：David Loomis，K2 顾问

这里是一种为升级（escalation）设置默认结果的简单方法，这样当升级触发时，工作流将转到你选择的活动。我见过许多实现此功能的方法，但我认为这种方法是最简单的。

假设你有一个客户端事件（此技术可以适用于服务器事件或 IPC 事件），其中用户有两个选择：批准或拒绝。如果用户在经过一段时间时间后没有采取行动，你希望自动执行拒绝。

- 1. 打开 K2 设计并转到活动（activity）选项卡。
- 2. 展开活动并找到该事件（event）。
- 3. 右键点击事件并选择属性（properties）。
- 4. 在升级字段中，输入如图 A-19 所示的结果。
- 5. 在活动中，设置如图 A-20 所示的结果。

## 附录 A：K2 blackpearl 技巧与窍

![](img/20dd98d522a8a8d52ab6ce56d548ca5_79.png)

为了通知工作流事件已完成，必须向外部系统提供一个关键信息：异步服务器事件的活动序列号。序列号与消息队列中使用的关联 ID（correlation ID）类似。此序列号允许你使用 K2 API 打开正确的服务器项，并使用 ServerItem 的 `Finish` 方法完成事件。

## 向进程中添加事件

作者：Harvinder Dhami，K2 用户

大多数 K2 开发者都熟悉异步事件，但较少的人熟悉异步服务器事件。虽然名称听起来相似，但这两个事件非常不同。异步事件允许你独立于工作流启动一个子进程。

## 异步服务器事件

作者：David Loomis，K2 顾问

想象一下一个工作流移交给一个外部系统，而该系统需要未知的时间（几天或几周）才能完成。与其持续轮询外部系统的答案，工作流只需等待通知。假设一家汽车经销商开发了一个处理定制汽车的 K2 流程。经销商工作流收集客户请求、获取批准，然后通过 Web 服务与订单系统通信。汽车的实际交付日期取决于工厂进度、待处理请求数量以及零件的可用性。当车辆完成后，工厂订单系统将调用 Web 服务通知经销商

## 将事件异步化

异步服务器事件是你处理这种情况所需的工具。异步服务器事件与普通的同步代码有何区别？当工作流遇到同步服务器事件时，它执行事件并继续工作流。在异步事件中，工作流执行事件并停止。当你将服务器事件拖到工作流设计画布时，默认是同步的。通过如图 A-21 所示在事件中添加一行代码，可以将服务器事件从同步改为异步。

![](img/20dd98d522a8a8d52ab6ce56d548ca5_880.png)

## 完成服务器事件

为了通知工作流事件已完成，必须向外部系统提供一个关键信息：异步服务器事件的活动序列号。序列号与消息队列中使用的关联 ID 类似。此序列号允许你使用 K2 API 打开正确的服务器项，并使用 ServerItem 的 `Finish` 方法完成事件。

你还可以使用 ServerItem 类设置进程和活动字段，以便将信息传回工作流。此代码可以从 .NET 程序集、Web 服务或任何符合你情况的方法调用。

# 附录 A：K2 黑色赌场技巧与技巧

```cs
public static void Completelistitem(string k2server, string sbn)
{
    if (string.IsNullOrEmpty(sbn)) return;

    SourceCode.Workflow.Client.Connection k2conn = null;
    try {
        SourceCode.Workflow.Client.ConnectionSetup k2setup = new ConnectionSetup();
        k2setup.ConnectionString = k2server;

        k2conn = new Connection();
        k2conn.Open(k2setup);
```

图 A-22

用于连接 K2 服务器的身份需要在管理控制台中为该进程分配正确的服务器服务器事件（参见图 A-23）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_881_0.png)

图 A-23

## 使用异步服务器事件

工作流的一个常见设计场景是：需要能够响应主工作流中的操作，随时取消异步进程。这种场景通常发生在发起者决定取消某个请求时，而该请求已经启动了几个独立的子进程来执行部分工作。

我们将使用一个异步服务器代码事件和其他一些组件来实现其中一种可能的解决方案。基本思想是：每当启动异步 IPC 事件时，它都会向 SmartObject 写入关于自己的信息。当子进程结束时，它会删除该条目。如果主进程需要结束，它只需扫描 SmartObject 中所有属于它的当前正在运行的子进程，并告诉它们完成。异步服务器事件将在子进程中使用，用于等待来自主进程的信号。

## 示例项目

本附录此节讨论的独立示例名为“CancelSubTask”，可以在 www.wrix.com 的书书籍代码下载中获取。客户端事件（Client Events）没有网页；请使用 K2 Worklist 触发它们。该示例包含两个项目：一个 K2 项目和一个 .NET 类库。K2 项目包含两个简单的工作流（MainProcess 和 SubProcess）以及一个 SmartObject —— ActiveSubProcesses。MainProcess 调用 SubProcess 使用异步 IPC 事件执行模拟工作，并传递进程 ID。主进程将执行一个由单个客户端事件构成的模拟工作。当 MainProcess 完成时，它会发出信号让所有仍在运行的子进程完成。

该类实现了一个调用之前讨论过的 CompleteDeleteItem 的 DLL。代码包含了完整代码，以便你根据需求进行修改。此程序集已作为项目引用添加到工作流中，你也可以构建一个类似的工作流例程通用库，并将其部署到全局程序集缓存（GAC）。另一个选项是将此代码放置在 Web 服务中。

## SmartObject
