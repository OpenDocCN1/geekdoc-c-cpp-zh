

会议结束。

## 摘要

在会议过程中，团队从客户那里得到一个简短的描述，并将其分解为用户故事。团队随后对这些故事进行了估算并创建了一个优先排序的待办事项列表。他们现在可以开始开发了。

注意对话如何让开发过程的各方都提供了输入：分析、实现和测试。对于每个故事，团队就完成该故事所需的工作量达成了共识。

## 第11章 自适应示例：冲刺1

### 本章你将

- 观察团队的第一次冲刺计划会议。
- 跟随第一个用户故事的实现和演进。
- 观察团队的冲刺演示和回顾。

在本章中，Trey Research 团队实现了其前四个用户故事。这些是团队分配给项目冲刺1的唯一故事。团队已设定以下冲刺目标：

> 演示一个动态的房间列表，能够创建新房间，查看房间中编写的消息，并且至少有两位用户能够在房间中共享消息

通过定义冲刺目标，团队设定了一个具有挑战性但可实现的目标，以便在冲刺内完成。所有工作都应与冲刺目标保持一致，以便团队知道自己是否在正轨上，并且只做客户要求的工作。

### 计划

团队为冲刺安排了一次计划会议，并带去了与冲刺目标相关的故事。对于本次冲刺，团队将要实现的故事是：

- 我想要创建房间来对对话进行分类。
- 我想要查看代表对话的房间列表。
- 我想要查看已发送到房间的消息。
- 我想要向其他房间成员发送纯文本消息。

团队开始讨论。

PETRA：好吧，有四个故事要讨论，但这些是首先要实现的，所以我预计这里有一些关键决策需要做出。

STEVE：也许吧，是的。开始之前我们确实需要考虑一些技术。有人有什么建议吗？

DIANNE：这是一个 Web 应用程序，所以我们最好选择我们都熟悉和舒适的东西。ASP.NET MVC 似乎是显而易见的选择。大家都同意吗？

STEVE：我很满意。

DAVID：嗯。说实话，我认为这是一个完美的 Node.js 应用程序。

TOM：我对 Node 没有任何经验，很不幸。还有别人吗？

STEVE：真的没有。我认为 Dianne 说得对，我们应该坚持我们所知道的。

DIANNE：使用 MVC，我们已经为代码结构做好了大部分准备。看看这个序列图。

Dianne 向团队展示了图 11-1 中的 UML 序列图。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_368_0.png)

图 11-1 Dianne 的序列图概括了应用程序的结构。

STEVE：好的，我明白你在这里做了什么。到目前为止，这看起来不错。

DAVID：看起来与房间或消息没有任何关系。

DIANNE：是的，我会解释。它非常通用。 rather than 为每个用户故事创建一个序列图，我决定将解决方案概括化，以便我们可以知道我们将需要的类——至少在短期内。

DAVID：哦，我明白了。所以 Get data 是 Get room 和 Get messages 的占位符，对吧？

DIANNE：是的，你说对了。

STEVE：那么，服务部分呢？它是事件驱动的消息传递还是某种我们轮询的数据库？

DIANNE：HTTP 是一个断开连接、无状态的协议。我们必须轮询服务器以获取消息。

DAVID：但只有自上次检查以来的消息。我们不想每次都返回所有消息。

STEVE：是的，这样扩展性不好。

DIANNE：说到这个，这真的是一个可扩展的解决方案吗？

PETRA：很好的观点。虽然客户短期内只希望支持 20 个用户，但你可以看出这将会迅速扩展。无法知道上限可能是什么。我们不应该限制应用程序的可扩展性。

STEVE：也许不是。但只要我们从一开始就将适应性构建到代码中，我们应该能够在进展中发现最合适的架构。

TOM：用户界面呢？如果我们下周要演示，至少应该看起来体面。

PETRA：Tom 说得对——功能很棒但美观很差的演示会让客户失去很多信心。

DAVID：嗯，MVC 使用 bootstrap，所以我们可以实现几个 bootstrap 模板。我们需要一个房间列表页面和一个房间消息页面。至少这样看起来会更现代一些，虽然有点极简。

PETRA：别担心极简主义。我认为他们最终可能希望这个应用程序由用户主题化。 在如此早期的阶段，我们在用户界面上花费的任何精力可能都会被浪费。

STEVE：Tom，关于测试呢？这里有什么让你担心的吗？

TOM：没有，我确保冲刺目标仅限于两位用户，这样我就可以将自动负载测试推迟到以后。在这一点上，我们只需手动测试，直到我设置好一些自动化。我可能希望你们三个人进行单元测试，所以如果你们需要帮助，请告诉我。

STEVE：太棒了——我认为我们现在就到这里了。我们可以根据需要进一步详细讨论。

会议结束，团队准备实现其第一个故事。

### “我想要创建房间来对对话进行分类。”

几天后，David 表示他已准备好对房间创建故事进行代码评审。Dianne 来到 David 的办公桌前，两人讨论代码。此次讨论的目标是确定所选实现的积极和消极方面。这样的同行评审为开发人员提供了一个机会，以确定某些内容是否未达到所需标准或缺乏适应性，以便在代码提交到源代码控制之前做出最终更改。

### 控制器

当 David 开始实现控制器时，他请 Dianne 过来征求她的意见。

DAVID：所以，我使用了你建议的 MVC 模式。控制器本身目前没做什么太多——它只是将请求委托给 IRoomRepository 接口，以与我们放置的任何持久存储进行交互。

DIANNE：让我们现在看看控制器代码。

David 向 Dianne 展示了列表 11-1 中的控制器代码。

列表 11-1 RoomController 是 Create 请求的入口点。

Click here to view code image

```csharp
public class RoomController : Controller
{
    private readonly IRoomRepository roomRepository;
    public RoomController(IRoomRepository roomRepository)
    {
        Contract.Requires<ArgumentNullException>(roomRepository != null);

        this.roomRepository = roomRepository;
    }

    [HttpGet]
    public ActionResult List()
    {
        return View();
    }

    [HttpGet]
    public ActionResult Create()
    {
        return View(new CreateRoomViewModel());
    }

    [HttpPost]
    public ActionResult Create(CreateRoomViewModel model)
    {
        ActionResult result;

        if(ModelState.IsValid)
        {
            roomRepository.CreateRoom(model.NewRoomName);

            result = RedirectToAction("List");
        }
        else
        {
            result = View("Create", model);
        }

        return result;
    }
}
```

DIANNE：好的，这看起来不错。我们为 IRoomRepository 提供了依赖注入，这给了我们一些灵活性。而且它是用代码契约强制执行的，这很棒。

DAVID：是的——我也用单元测试确保了前置条件得到满足。如果你愿意，我可以向你展示。

DIANNE：那太好了，但你能解释一下用于处理 POST 请求的 Create 方法吗？具体来说，为什么在委托给存储库的 CreateRoom 方法之后它会重定向？

DAVID：那是 Post-Redirect-Get 模式。基本上，如果我们在此直接返回到 List 视图，用户刷新页面时将导致第二次 POST 请求。这意味着我们会尝试再次创建同名房间，从用户体验角度来看，这感觉不对。

DIANNE：太棒了！到目前为止，这看起来真的很好。

DAVID：有一件事我不太确定，那就是直接实例化一个新的 CreateRoomViewModel。我不应该为此使用工厂吗？

DIANNE：好问题。我会说不——不是这种情况。原因是返回类型不太可能有任何变化。像这样的视图模型是针对特定用途定制的，在这里委托给工厂将是多余的间接。

### 控制器单元测试

David 打开包含单元测试的文件，如列表 11-2 所示，并请 Dianne 对他的工作进行同行评审。

DAVID：这里是 RoomController 构造函数的单元测试。

列表 11-2 通过单元测试验证 RoomController 构造函数。

Click here to view code image

```csharp
[Test]
public void ConstructingWithoutRepositoryThrowsArgumentNullException()
{
    Assert.Throws<ArgumentNullException>(() => new RoomController(null));
}

[Test]
public void ConstructingWithValidParametersDoesNotThrowException()
{
    Assert.DoesNotThrow(() => CreateController());
}
```

DAVID：第一个确保 RoomController 中的 IRoomRepository 字段始终有一个有效的引用。

DIANNE：是的，RoomController 始终具有有效且不为 null 的存储库字段，这是其隐含契约的一部分。

DAVID：接下来的这两个测试断言了用于处理 GET 请求的 Create 方法的行为。

