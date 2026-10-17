
In addition, developers have created a number of tools to make working with SQL Azure easier. One of the most useful is the Microsoft Sync Framework Power Pack for SQL Azure, which (besides having one of those horribly long names that Microsoft is becoming known for) allows you to synchronize a database on your network to one running within SQL Azure. This uses the same Sync Framework you saw when working with SQL Server Compact (see Chapter 12), and enables you to select the tables you want to synchronize (see Figure E-8).

![](img/d99870e80390742f93963da7be0b2e61_1205_0.png)

FIGURE E-8

While SQL Azure provides a familiar — and powerful — alternative to the other storage mechanisms, keep in mind that it is billed in addition to the existing services. In addition, you need to register to request a SQL Azure application key separately from the Windows Azure account key.

### Compute Services

In addition to a public interface and data storage, most applications also require some processing. Of course, this processing can be included in the other two components. However, there are times when you need longer-running or asynchronous processing in your application. For example, you might need to perform some analysis of a large block of data, such as sales analysis on a data warehouse, or convert videos into alternative formats.

Alternately, your application might need to poll an external data source at regular intervals. In these cases, it’s not a good idea to include this functionality within your user interface. Instead, you can use the Azure Compute services to perform these operations. This provides highly scalable processing, billed at a rate based on actual usage (that is, per CPU-hour). It’s like having a highly scalable supercomputer available to your application.

As described earlier in the Queues section, you communicate with the worker roles via queues. As Compute services consist entirely of worker roles, you therefore use queues to communicate with your Compute services. You send the data necessary for computation by adding a message to a queue. The worker role running within the Compute services retrieves the first available message from a queue and performs whatever processing is required, then deletes the message to prevent other workers from retrieving it. The worker role can then use the other storage services to save data as needed.

### Windows Azure Tools for Visual Studio

Before you can create solutions using Windows Azure, you must first install the Windows Azure Tools for Visual Studio. You can access this install by clicking File ⇨ New Project (see Figure E-9). Selecting the Enable Windows Azure Tools option will send you to the Microsoft Download Center to download the current version of these tools.

![](img/d99870e80390742f93963da7be0b2e61_1206_0.png)

FIGURE E-9

> 为了运行 Windows Azure 的开发环境，你需要以管理员身份运行 Visual Studio 2010。否则，在尝试运行应用程序时，你会看到图 E-10 中显示的错误消息。要在 Windows Vista 或 Windows 7 中以管理员身份运行 Visual Studio，请右键单击图标并选择“以管理员身份运行”。此时可能需要你输入用户 ID 和密码。

此外，为了将应用程序部署到云中，你需要获得一个开发者密钥。该密钥也用于所有数据请求。目前，你可以通过在`http://go.microsoft.com/fwlink/?LinkID=129453`上提出请求来获取密钥。但是，使用 Visual Studio 的 Windows Azure 工具进行开发并不需要此密钥，只有在将应用程序部署到实时服务器时才需要。

你需要退出 Visual Studio 才能安装工具。运行安装程序后，你将看到创建 Azure 服务的选项（见图 E-11）。

![](img/d99870e80390742f93963da7be0b2e61_1207_0.png)

FIGURE E-10

![](img/d99870e80390742f93963da7be0b2e61_1207_1.png)

FIGURE E-11

### Creating a Windows Azure Project

要探索使用 Windows Azure 创建应用程序时可用的功能，请创建一个名为`CloudToDo`的新项目。

选择该选项后，你将进入“新建云服务项目”对话框（见图 E-12）。此对话框使你能够选择将要创建的初始服务类型。当然，你以后可以向项目中添加其他服务。

![](img/d99870e80390742f93963da7be0b2e61_1207_2.png)

FIGURE E-12

目前，你可以创建五种类型的服务：

- ASP.NET Web role — 这是一个标准的 Web 服务，将在云中托管 ASP.NET 应用程序。你会包含其中一个来为你的云提供可见的用户界面。

- MVC 2 Web role — 这是一个 Web 服务，将托管使用 ASP.NET MVC 框架构建的应用程序。

- WCF Web role — 这是一个包含一个或多个 WCF 服务的 Web 服务。你会包含其中一个来在应用程序中提供 Web 服务。

- Worker role — 这是一个不可见的应用程序，将在你的云中运行。通常，这些是 Web 应用程序所需的后台任务，或计算服务。例如，你可能有一个 worker role 来将订单传输到履行服务，或一个处理数据以确定趋势的 worker role。

- CGI Web role — 这是一个设计用于运行用 PHP、Python、Ruby 或其他非 ASP.NET 语言编写的 Web 应用程序的 Web 服务。

现在，先向应用程序添加一个名为`ToDoWeb`的单个 Web role。添加 Web role 后，通过单击铅笔图标设置名称。这将是应用程序的用户界面。

Web role 看起来并工作起来与 ASP.NET 应用程序完全一样：你会得到一个初始的`default.aspx`页面，并且它包含一个`web.config`文件和 jQuery 脚本库。唯一的区别是添加了`WebRole.vb`文件。该文件包含两个方法：

- `OnStart` — 此方法重写基类`RoleEntryPoint`中的方法。当角色在 Azure 结构中初始化时调用它，可以将其视为类似于构造函数。你可以在此时执行任何必要的初始化。该方法应返回`true`，如果角色准备好参与 Azure 环境，或返回`false`，如果有任何因素阻止它这样做。例如，你可以在此处连接到数据源。如果由于某种原因它们不可用，你可以将`OnStart`设置为`false`以防止 Web role 初始化。

- `RoleEnvironmentChanging` — 这是 Azure 环境可能在对正在运行的实例的配置进行某些更改时调用的事件。这使你的应用程序能够重新加载配置设置并相应地采取行动。

经过硬盘的短暂忙碌后，你应该在“解决方案资源管理器”中看到类似图 E-13 的内容。除了 ASP.NET 应用程序之外，你还有由你添加的单个 Web role 组成的 Windows Azure 项目，以及两个配置文件。

这两个配置文件标识 Web role 将监听的端口，以及将运行的大小和实例数量。你可以手动编辑这些文件，但使用 Visual Studio 编辑它们要容易得多。右键单击“角色”文件夹中的`ToDoWeb`并选择“属性”以配置你的 Web 应用程序。从“配置”选项卡（见图 E-14）你可以设置以下内容：

- 应用程序的信任级别 — 完全信任允许所有访问（直接访问计算机的明显例外除外）。Windows Azure 部分信任基本上与 ASP.NET 中的中等信任（见第 34 章）类似。然而，它更具限制性，特别是在访问环境变量或文件 IO 方面。

- 应用程序将运行的实例数量 — 这可以稍后从 Windows Azure 管理屏幕中更改。

- 将运行你的应用程序的虚拟机的“大小” — 这些是 CPU 数量、内存大小和磁盘空间的基本组合。随着底层计算机变得更强大，它们会发生变化，截至本文撰写时，可用大小映射到以下容量：

![](img/d99870e80390742f93963da7be0b2e61_1208_0.png)

| VM SIZE | CPU CORES | MEMORY | DISK SPACE |
|---|---|---|---|
| Small | 1 | 1.7 GB | 250 GB |
| Medium | 2 | 3.5 GB | 500 GB |
| Large | 4 | 7 GB | 1 TB |
| ExtraLarge | 8 | 15 GB | 2 TB |

Web role 是否使用 HTTP、HTTPS 或两者结合 — 如果你的应用程序从用户接收任何安全信息，你应该使用 HTTPS。否则，HTTP 对于大多数用途来说应该足够了。

此外，你使用配置的“终结点”选项卡来配置终结点（见图 E-15）。此选项卡使你能够定义 Web role 使用的端口，以及用于 HTTPS 的证书。

![](img/d99870e80390742f93963da7be0b2e61_1209_0.png)

![](img/d99870e80390742f93963da7be0b2e61_1209_1.png)

你使用“设置”选项卡为项目定义任何其他设置，就像为其他项目一样做。然而，在开发环境中工作时，最好将应用程序设置为使用适合开发环境的连接字符串，而不是尝试访问部署到云中的服务。单击“添加设置”按钮，并将新设置命名为`DataConnectionString`，类型为`ConnectionString`。单击值属性上的省略号以显示“存储连接字符串”对话框（见图 E-16）。

![](img/d99870e80390742f93963da7be0b2e61_1209_2.png)

现在，选择第一个选项“使用开发存储”。正如你可能猜到的那样，当将此应用程序部署到云中时，你需要输入你的凭据以访问服务。保存设置后，“设置”选项卡应如下图 E-17 所示。

![](img/d99870e80390742f93963da7be0b2e61_1209_3.png)

你像处理任何其他 ASP.NET 站点一样处理 Web role。在本例中，应用程序将是一个简单的待办事项列表。

### Using Table Storage

应用程序必须保存待办事项，以及它们是否已完成。通常，这将存储在 SQL Server 数据库中，但在本文中我们将使用 Azure 表存储来保存该信息。

要使用表存储，你需要定义一个代表要保存的数据的类。该类需要为你的数据的属性提供属性，以及`TimeStamp`、`PartitionKey`和`RowKey`属性。`PartitionKey`和`RowKey`属性用于唯一标识存储中的每个项目，而`TimeStamp`属性标识项目最后更改的时间。此外，你需要在类上添加`<DataServiceKey("PartitionKey", "RowKey")>`属性。这用于将键字段标识给 Data Services 基础结构。

为了避免所有这些工作，你可以改为让你的类继承提供的`TableServiceEntity`类。这提供了上面列出的所有更改。项目中使用的`Task`类被有意保持简单：

```
Imports Microsoft.WindowsAzure.StorageClient

Public Class Task
    Inherits TableServiceEntity

    Public Property Name As String
    Public Property IsComplete As Boolean

    Public Sub New()
        'need to set the PartitionKey and RowKey
        'for each instance
        'normally, you would want to have multiple partitions
        'to spread the data out across servers
        PartitionKey = DateTime.Now.ToString("u")
        'rowkey must be unique within each partition
        'data is sorted based on RowKey
        RowKey = String.Format("{0}-{1}",
                            DateTime.Now.Ticks,
                            Guid.NewGuid.ToString())
    End Sub

End Class
```

如你所见，`Task`类将跟踪任务的名称，并且布尔标志标记任务是否已完成。`PartitionKey`和`RowKey`属性在类的构造函数中分配。在这里，所有任务都根据创建日期分配分区。你应该选择`PartitionKey`，以便你的条目分布在多个存储节点上。例如，你可以根据条目日期（正如这里所做的）、文件名的首字母，或组织照片集合的相册来分配`PartitionKey`。

`RowKey`就像每个分区的唯一索引一样，因此你应该选择一个保证唯一的值。此外，项目在每个分区内根据`RowKey`进行排序。在前面的示例中，`RowKey`是根据对象创建时的系统时间（以 ticks 为单位）分配的，并在末尾添加 GUID 以确保唯一性，即使同时添加多个条目也是如此。

```vb
CloudStorageAccount.SetConfigurationSettingPublisher(
    AddressOf ConfigurationSettingPublisher)

'loads the account from settings

Dim account As CloudStorageAccount =
    CloudStorageAccount.FromConfigurationSetting("DataConnectionString")

'creates the tables in table storage

CloudTableClient.CreateTablesFromModel(GetType(TaskContext),
                                      account.TableEndpoint.AbsoluteUri,
```
