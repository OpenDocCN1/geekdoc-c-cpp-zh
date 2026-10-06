

- 你需要跟踪消息处理的进度。这使得其他工作进程在另一个进程被中断时能够恢复消息处理。
- 你需要关于队列上所有事务活动的服务器端日志信息。

在本节中，我将实现一个简单的队列。示例解决方案 `AzureQueueSample` 除了标准的 Azure 项目外，还包含两个项目。一个是工作器项目，它向队列中插入消息；另一个是消费者项目 `ConsumerProject`，它从队列中获取消息。由于没有 UI 工作，两个 F# 工作角色项目就足够了。我创建了两个项目，并将它们命名为 `WorkerRole` 项目和 `ConsumerRole` 项目。项目创建对话框如图 8-12 所示。

![](img/63aaf94e22830ab98ce16c5946be8ef6_496_0.png)

**图 8-12** 创建 WorkerRole 和 ConsumerRole 项目

创建这些项目后，你可以进入 `AzureQueueSample` 文件夹配置队列连接字符串。右键点击 `WorkerRole` 节点并选择“属性”（Property）以显示配置菜单。队列连接字符串可以在“设置”（Settings）区域进行设置。点击“添加设置”（Add Setting）按钮创建连接。图 8-13 显示了点击此按钮后创建默认字符串。你现在可以将该字符串重命名为 **ConnectionString** 并将其类型设置为“连接字符串”（Connection String）。

![](img/63aaf94e22830ab98ce16c5946be8ef6_496_1.png)

**图 8-13**向项目设置中添加字符串

你可以点击带有省略号 (...) 的按钮来设置连接字符串。你应该先调试程序，而不是初始就针对真实的 Azure 环境。图 8-14 显示了存储账户连接字符串对话框。默认情况下，Azure 项目被设置为使用 Windows Azure 存储模拟器。

![](img/63aaf94e22830ab98ce16c5946be8ef6_497_0.png)

**图 8-14** 存储账户连接字符串对话框

点击“确定”（OK）接受此默认设置，并将连接字符串命名为 *MyConnectionString*。图 8-15 显示了 `WorkerRole` 项目设置。连接字符串被设置为使用开发版存储。该设置存储在 `.csdef` 文件的 XML 格式内容中。虽然这些 XML 文件可以手动修改，但初学者应该使用“设置”对话框。

> 注意：由于工作器和消费者项目都访问队列，因此需要在 `WorkerRole` 和 `ConsumerRole` 项目中都进行此设置。

**图 8-15** WorkerRole 项目的设置

这些是示例中用到的一些 Azure 云队列操作：

- 创建队列

```fsharp
let queueClient = storageAccount.CreateCloudQueueClient()
let queue = queueClient.GetQueueReference("myqueue")
queue.CreateIfNotExists()
```

- 向队列添加消息

```fsharp
let message = CloudQueueMessage("Hello, World")
queue.AddMessage(message)
```

- 预览队列中的消息，并以字符串形式显示消息

```fsharp
let peekedMessage = queue.PeekMessage()
if (peekedMessage <> null) then
    let msg = queue.GetMessage()
    log msg.AsString("Information")
```

- 出队消息

```fsharp
let msg = queue.getMessage()
queue.deleteMessage(msg)
```

为了让这个示例更有趣，我使用了一个变量来指定 `Thread.Sleep` 函数的睡眠时间。睡眠时间是通过队列中当前的消息数量动态设置的。如果消息数量大于 3（意味着客户有大量消息），则睡眠时间将增加 100 毫秒。否则，睡眠时间将减半。`WorkerRole` 代码如列表 8-2 所示。

# 列表 8-2 修改睡眠时间的代码

```fsharp
namespace WorkerRole1

open System.Diagnostics
open System.Net
open System.Threading
open Microsoft.Windows.Azure
open Microsoft.Windows.Azure.Runtime
open Microsoft.Windows.Azure.StorageClient

type WorkerRole() =
    inherit RoleEntryPoint()

    // 这是一个示例工作器实现。请替换为你的逻辑。
    let log messagekind = Trace.WriteLine(message, kind)

    override wr.Run() =
        log "WorkerRole1 entry point called" "Information"
        let connectionName = "MyConnectionString"
        let storageAccount =
            CloudStorageAccount.Parse(CloudConfiguration.GetString(connectionName))
        let queueClient = storageAccount.CreateQueueClient()
        let queue = queueClient.GetQueueReference("myqueue")

        ignore <| queue.CreateIfNotExists()>
        let mutable sleepTime = 1000
        while(true) do
            Thread.Sleep(sleepTime)

            let message = CloudQueueMessage("Hello, World")
            queue.AddMessage(message)
            log "add new message" "Information"

    override wr.OnStart() =
```fsharp
// 设置最大并发连接
ServicePointManager.DefaultConnectionLimit <- 12
```

```fsharp
// 有关处理配置更改的信息
// 请参见 MSDN 主题：http://go.microsoft.com/flink/?LinkId=166357.
base.OnStart()
```

注意：为了防止 `sleepTime` 被设置为 0，使用了 `max` 函数来确保 `sleepTime` 的最小值为 1。项目引用中需要添加 `Microsoft.WindowsAzure.Configuration.dll`。

