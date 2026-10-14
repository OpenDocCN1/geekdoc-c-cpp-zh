

DAVID：不，当然！我认为这足以很好地展示他们想要的功能。测试怎么样？

DIANNE：哦，当然。这里就是。

RoomControllerTests 类中的两个单元测试显示在清单 12-4 中。

## LISTING 12-4 为房间名称和消息文本上的验证规则添加单元测试。

Click here to view code image

```csharp
[Test]
[TestCase("Callooh! Callay! O frabjous day!")]
[TestCase("The frumious Bandersnatch!")]
[TestCase("A heffalump or woozle is very confused...")]
public void PostCreateNewRoomWithBlockedWordsCausesValidationError(string roomName)
{
    var controller = CreateController();

    var viewModel = new RoomViewModel { Name = roomName };
    var context = new ValidationContext(viewModel, serviceProvider: null, items: null);
    var results = new List<ValidationResult>();

    var isValid = Validator.TryValidateObject(viewModel, context, results, true);

    Assert.That(isValid, Is.False);
}
//...
[Test]
[TestCase("Callooh! Callay! O frabjous day!")]
[TestCase("The frumious Bandersnatch!")]
[TestCase("A heffalump or woozle is very confused...")]
public void PostAddMessageWithBlockedWordsCausesValidationError(string text)
{
    var controller = CreateController();

    var viewModel = new MessageViewModel { AuthorName = "David", Text = text };
    var context = new ValidationContext(viewModel, serviceProvider: null, items: null);
    var results = new List<ValidationResult>();

    var isValid = Validator.TryValidateObject(viewModel, context, results, true);

    Assert.That(isValid, Is.False);
}
```

DAVID：视图模型上的两个属性都标记了 ContentFiltered 属性，这些测试将会很顺利地通过。

DIANNE：绝对如此。尽管如此，目前我对这个设计还是有些不满意的地方。

DAVID：什么？

DIANNE：显然是被阻止词列表的硬编码。我认为这可以算作审慎的技术债务，但我仍然希望从提供者接口请求被阻止词列表。这样，我就可以创建一个实现类来返回静态的硬编码列表，并在未来提供更数据驱动的实现。

DAVID：是的，这样就能很好地将被阻止词列表的数据与验证属性的算法分离开来。你能使用依赖注入吗？

DIANNE：不幸的是不能。这些自定义属性不够灵活，不会通过控制器或 MVC 暴露的任何其他扩展点进行构造。

DAVID：真遗憾。那服务定位器模式怎么样？

DIANNE：我通常把服务定位器称为反模式，但在这种情况下，它可能是我们可用的最佳选择。

DAVID：我们现在就这样保留吧，接受这个属性存在一些技术债务？这样我们就能取得进展，如果有必要的话再回头修改这段代码。

DIANNE：我同意。我认为这在未来很可能会发生很大变化，所以现在猜测它会朝哪个方向发展毫无意义。

## “我想同时为数百名用户提供服务。”

冲刺的最后一个故事涉及 Dianne 和 Steve 提高应用程序的可扩展性。客户要求应用程序能够水平扩展，而不是垂直扩展。水平扩展意味着应用程序应能够通过添加额外的机器来支持更多并发用户。相比之下，垂直扩展是通过向单台机器添加额外资源来支持更多并发用户的能力。

Dianne 和 Steve 理解，水平扩展的限制因素是架构中存在关系数据库管理系统 RDBMS，例如 Microsoft SQL Server。与专为水平扩展而设计的专用分布式存储解决方案相比，很难向机器集群中添加新的 SQL Server 实例。

因此，Dianne 调查了团队用文档存储替换 SQL Server 数据库的选项。她向团队介绍了 MongoDB 作为一个可靠且流行的替代方案，它将允许团队通过向集群添加新机器来扩展应用程序。唯一的问题是应用程序目前依赖 SQL Server 来存储和检索房间和消息数据。

幸运的是，团队已经通过面向接口编程为这种情况做好了准备。

DIANNE：我们只需要为存储库接口创建新的实现：IRoomRepository 和 IMessageRepository。

STEVE：我们当然可以这样做，但我认为我们可以省去从记录数据到视图模型数据的映射，而是直接对视图模型进行序列化和反序列化。

DIANNE：听起来很有趣！这样我们只需要创建 IRoomViewModelReader 和 IRoomViewModelWriter 接口的新实现，让它们委派给 MongoDB 即可。

STEVE：没错。

这对开始着手实现 MongoRoomViewModelStorage 类，如清单 12-5 所示。

## LISTING 12-5 MongoDB 数据持久层 的实现。

Click here to view code image

```csharp
public class MongoRoomViewModelStorage : IRoomViewModelReader,
IRoomViewModelWriter
{
    public MongoRoomViewModelStorage(IApplicationSettings applicationSettings)
    {
        this.applicationSettings = applicationSettings;
    }

    public IEnumerable<RoomViewModel> GetAllRooms()
    {
        var roomsCollection = GetRoomsCollection();
        return roomsCollection.FindAll();
    }

    public void CreateRoom(RoomViewModel roomViewModel)
    {
        var roomsCollection = GetRoomsCollection();
        roomsCollection.Save(roomViewModel);
    }

    public IEnumerable<MessageViewModel> GetRoomMessages(int roomID)
    {
        var messageQuery = Query<MessageViewModel>
            .EQ(viewModel => viewModel.RoomID, roomID);
        var messagesCollection = GetMessagesCollection();
        return messagesCollection.Find(messageQuery);
    }

    public void AddMessage(MessageViewModel messageViewModel)
    {
        var messagesCollection = GetMessagesCollection();
        messagesCollection.Save(messageViewModel);
    }

    private MongoCollection<MessageViewModel> GetMessagesCollection()
    {
        var database = GetDatabase();
        var messagesCollection = database.
            GetCollection<MessageViewModel>(MessagesCollection);
        return messagesCollection;
    }

    private MongoCollection<RoomViewModel> GetRoomsCollection()
    {
        var database = GetDatabase();
        var roomsCollection = database.GetCollection<RoomViewModel>(RoomsCollection);
        return roomsCollection;
    }

    private MongoDatabase GetDatabase()
    {
        var connectionString = applicationSettings.GetValue(MongoConnectionString);
        var client = new MongoClient(connectionString);
        var server = client.GetServer();
        return server.GetDatabase(ProsewareDatabase);
    }

    private readonly IApplicationSettings applicationSettings;
    private static string MongoConnectionString = "MongoConnectionString";
    private static string ProsewareDatabase = "Proseware";
    private static string MessagesCollection = "messages";
    private static string RoomsCollection = "rooms";
}
```

有了这个实现，团队能够释放 Proseware 应用程序水平可扩展性的潜力，并为客户服务。

## Sprint demo

在第二个冲刺结束时，团队准备向客户进行另一次演示。本冲刺完成的全部故事都被汇总并展示其功能。第一轮冲刺回顾会议中的一个关键行动是改进演示的准备工作。团队对此进行了认真的跟进，在客户到场前提前开会，演练每个故事的功能。这有助于减轻由于开发环境和演示环境不同而导致的问题。彩排顺利进行，因此团队已准备好向客户展示其进展。
