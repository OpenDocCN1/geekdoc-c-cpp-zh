
```csharp
public class RepositoryRoomViewModelService : IRoomViewModelReader, IRoomViewModelWriter
{
    private readonly IRoomRepository roomRepository;
    private readonly IMessageRepository messageRepository;
    private readonly IViewModelMapper mapper;

    public RepositoryRoomViewModelService(IRoomRepository roomRepository,
        IMessageRepository messageRepository, IViewModelMapper mapper)
    {
        Contract.Requires<ArgumentNullException>(roomRepository != null);
        Contract.Requires<ArgumentNullException>(messageRepository != null);
        Contract.Requires<ArgumentNullException>(mapper != null);

        this.roomRepository = roomRepository;
        this.messageRepository = messageRepository;
        this.mapper = mapper;
    }

    public IEnumerable<MessageViewModel> GetRoomMessages(int roomID)
    {
        var roomMessages = new List<MessageViewModel>();
        var roomMessageRecords = messageRepository.GetMessagesForRoomID(roomID);

        foreach (var messageRecord in roomMessageRecords)
        {
            roomMessages.Add(mapper.MapMessageRecordToMessageViewModel(messageRecord));
        }

        return roomMessages;
    }
}
```

**DAVID:** 我觉得这样很好。

David 和 Dianne 继续实现存储库方法 `IMessageRepository.GetMessagesForRoomID()`，该方法从 Microsoft SQL Server 数据库加载消息。实现此方法后，他们继续下一个用户故事。

#### “我想向其他房间成员发送纯文本消息。”

David 转而与 Dianne 一起实现冲刺的最后一个故事。

**DAVID:** 现在我们有了读写数据的模式，这应该很容易。

**DIANNE:** 或许吧。但请记住，这个故事的一个要求是请求将以异步方式发出。

**DAVID:** 哦。所以它不会是整页的回发？

**DIANNE:** 不，用户界面将通过 AJAX 请求发送数据。

> **Note**
>
> 一些定义：AJAX 代表 Asynchronous JavaScript and XML。XML 代表 Extensible Markup Language。AJAJ 代表 Asynchronous JavaScript and JSON。JSON 代表 JavaScript Object Notation。

**DAVID:** 等等。你是说 AJAJ，对吧？

**DIANNE:** 我想确实是！

**DAVID:** 那么这个控制器操作有什么不同呢？

**DIANNE:** 其实有两点。当 `ModelState.IsValid` 属性为 true 时，我们应该使用 `IRoomViewModelWriter` 保存消息。但我们应该然后以 `JsonResult` 的形式返回视图模型。

**DAVID:** 当模型状态无效时我们该怎么办？

**DIANNE:** 在这种情况下，返回一个带有 HTTP 400 错误的 `HttpStatusCodeResult`。

**DAVID:** 那是客户端错误响应代码，对吧？

**DIANNE:** 是的。具体来说，它是 Bad Request 响应。

David 向 Dianne 展示了第 11-14 节中的代码。

#### LISTING 11-14 The AddMessage method on the RoomController class.

```csharp
[HttpPost]
public ActionResult AddMessage(MessageViewModel messageViewModel)
{
    ActionResult result;

    if (ModelState.IsValid)
    {
        writer.AddMessage(messageViewModel);

        result = Json(messageViewModel);
    }
    else
    {
        result = new HttpStatusCodeResult(400);
    }

    return result;
}
```

**DAVID:** `IRoomViewModelWriter` 上的 `AddMessage` 方法呢？

**DIANNE:** 我认为我们可以使用之前的相同模式。这部分代码不关心它是同步还是异步调用，因此不会改变我们迄今为止建立的模式。

David 继续遵循 `IRoomViewModelWriter.CreateRoom` 方法使用的相同模式，这导致了第 11-15 节所示的 `AddMessage` 方法。

#### LISTING 11-15 The AddMessage method on the RoomViewModelWriter class.

```csharp
public void AddMessage(MessageViewModel messageViewModel)
{
    var messageRecord = mapper.MapMessageViewModelToMessageRecord(messageViewModel);
    messageRepository.AddMessageToRoom(messageRecord.RoomID,
        messageRecord.AuthorName,
        messageRecord.Text);
}
```

通过此更改，以及创建另一个存储库方法以通过 ADO.NET 将消息记录保留在 Microsoft SQL Server 中，该故事已完成。

David 和 Dianne 现在已完成分配给冲刺的故事，正好赶上冲刺演示。

### Sprint demo

一周结束时，团队安排与客户会面并展示迄今为止的进展。要完成的任务被汇总，并展示每个任务的功能。客户受邀提供反馈并改变产品的方向。

冲刺演示有很多好处。首先，它允许团队确保始终与客户当前的需求和期望保持一致。演示还能激励团队成员始终拿出最佳成果，因为他们必须确信自己能够向客户展示产品的当前状态。客户也因此受益，因为他们能够在早期阶段看到产品的切实进展，并在整个开发过程中定期看到。如果客户想对软件的运作方式做出任何更改，产品演示正是绝佳时机。用户故事待办列表可以据此调整并重新排列优先级，软件也会立即改变方向以满足客户的需求。

### Proseware 的首次演示

演示当天，团队与客户公司的一位代表在会议室集合。团队简要讨论了冲刺的进展情况，并准备展示软件的当前状态。

不幸的是，在这样一个关键时刻，人们发现会议室里的投影仪无法正常工作。这使演示推迟了几分钟，直到找到一位能解决问题技术人员。投影仪恢复正常后，团队发现屏幕的分辨率远低于开发用机器的分辨率。这降低了用户界面的外观效果，使客户更难理解页面上各个部分的位置。

团队表示了歉意，客户似乎也表示理解，不过看到应用程序并不像他所在公司所期望的那样，客户略感失望。调整了一些显示设置后，应用程序开始看起来好一些，但仍然无法与开发环境中的显示完全一致。

团队逐一演示了冲刺期间实现的四个用户故事，然后询问客户是否有任何问题或评论。总体反馈是有利的：虽然应用程序目前能做的不多，但很明显，一些核心功能在非常早期的阶段就已经到位了。

Petra 建议他们的下一项任务将包括格式化发送到房间的消息。她还提到了 David 关于内容过滤器的想法。客户似乎对这个想法非常认可，并要求团队在即将到来的冲刺中将其列为高优先级事项。

会议结束时，客户离开，团队留下召开冲刺回顾会议。

### 冲刺回顾

在冲刺结束时，团队召开会议，讨论这一周取得的进展。所有团队成员都到场，并回答了以下问题：

- 哪些方面进展顺利？
- 哪些方面进展不佳？
- 流程中有没有哪些部分需要改变？
- 冲刺中是否有任何新的做法需要保留？
- 冲刺过程中是否有任何意外发现？

目标是要列出一份可执行的行动项清单，以便确定优先级并继续推进。像往常一样，这次会议的目的不是在没有切实行动的情况下进行大量讨论。

#### 哪些方面进展顺利？

团队成员在一个合适的会议空间集合，逐一讨论问题清单。他们先从冲刺中进展顺利的方面开始。

STEVE：那么，大家认为第一次冲刺中哪些方面进展顺利？

PETRA：我觉得演示很不错。虽然可能不完全符合客户的期望，但我认为是很积极的。

TOM：完全同意，我也这么认为。我觉得他们足够现实，知道这还不是一个成品，甚至连首个版本都算不上，但我们在很短的时间内所产出的东西确实具有切实的价值。

DIANNE：他们出席了，提供了建设性的反馈，而且即使在这么早的阶段，就改变了我们的方向。

PETRA：是的，我觉得这件事值得单独记一条。David，你的内容过滤器想法反响很好，他们已经提高了它的优先级，所以我们将在下一个冲刺中着手处理这个问题。

DAVID：我很高兴他们对我们所做的事情如此明显充满热情。我们只需要稍微管理一下他们的期望：我不希望他们过度吹嘘我们目前的工作。

STEVE：还有什么进展顺利的？

DIANNE：我觉得代码状况良好。虽然代码量不大，但现有的代码肯定能为未来的工作奠定良好的基础。

DAVID：谢谢——我认为 Dianne、Steve 和我之间的协作对此帮助很大。如果不是他们在整个过程中给予指导，代码可能已经积累了相当多的技术债务。

STEVE：好的，我会把这两点都记下来。还有别的吗？

房间里沉默下来，于是 Steve 在白板上写下以下几点，然后继续下一个问题。

- 演示效果不错，即使现阶段可展示的内容不多。
- 客户出席了演示，并给出了高质量的反馈。
- 代码似乎状态良好。

#### 哪些方面进展不佳？

团队要回答的下一个问题是冲刺期间哪些方面进展不佳。

STEVE：这里要诚实但现实一点：冲刺期间哪些方面进展不佳？

TOM：我认为这次冲刺中我没有得到充分利用。我意识到在这么早的阶段，我能做的事情不多，但需要测试的内容很少，而且仅有的那些测试工作也是一波一波来的。

PETRA：好的——这非常有价值。根本原因是什么？

STEVE：我想这是因为 David 是唯一一个实际在开发用户故事的开发人员，而 Dianne 和我在为另一个项目准备一些架构设计。

PETRA：这会是一个持续的问题，还是我们可以解决？

DIANNE：这一点更应该归入“需要改变的事项”部分，但 Steve 和我从今往后在 Proseware 项目上会从“鸡”变成“猪”。

TOM：请再提醒我一下那是什么意思。

STEVE：基本上，我们一直在为 Proseware 做贡献，但还没有完全投入资源。由于另一个项目进入了维护模式，我们被调到了那边。

DIANNE：确实如此。我们可以在接下来的冲刺中编写用户故事，这样你就能有持续不断的新功能可供测试，而不是一两阵零散的活动。

TOM：我觉得不错。

STEVE：还有其他进展不佳的吗？

PETRA：显然，演示开始时投影仪出的问题不太好。

DAVID：是的，我真的不知道那是怎么回事！当时很尴尬，但我觉得我们后来处理得很好。

DIANNE：完全同意，我们处理得好。但我们需要防止这种情况再次发生。

STEVE：我觉得问题纯粹是准备时间不足。就像在其他所有环境中一样，我们需要尽早并经常集成！将来，我们应该在演示前花半个小时，在会议室里用投影仪预演一遍要展示的内容。客户会原谅一次这种失误，但如果再犯，就会显得很不专业。

Steve 在白板上记下以下几点：

- QA 在整个冲刺期间未得到充分利用。
- 演示因环境问题几乎变成一场灾难。

STEVE：还有别的吗？

所有团队成员都摇了摇头表示没有，Steve 便继续往下进行。

#### 需要改变的事项？

敏捷流程具有很强的可塑性，团队应当抓住机会反思流程是在帮助他们，还是在阻碍他们。从流程、工作环境或其他实践中提炼出需要改变的事项，并将其转化为可执行行动项，是改进团队工作方式的一种极佳途径。

STEVE：好，我们已经从进展不佳的事项中得出了一些改变。首先，Dianne 和我必须在本冲刺中对项目投入更多时间。第二，我们需要额外花半个小时在会议室里准备演示。还有别的吗？

房间里一片安静。

STEVE：好的——每日站会还有效吗？

TOM：其实没有——这次冲刺中我缺席了两次，因为路上遇到堵车，没能赶到，记得吗？

DIANNE：当然——我完全忘了这件事。

STEVE：那改到上午 9:30 会不会更好？

TOM：我想是的。我实在难以保证自己能早上9点到这里。

PETRA：Tom，我会告知管理层，我们应该研究一下弹性工作时间。

TOM：谢谢——那太好了。

DAVID：我认为我们需要减少演示的频率。客户表示很惊讶，他们必须每周都来，而且我们展示的功能很少。为什么不改为每两周演示一次，同时解决这两个问题呢？

STEVE：这是个好主意——绝对值得研究。不过，我认为演示对交付是很好的激励。我想保留每周演示，但你觉得把给客户的演示限制在隔周一次，中间穿插内部演示怎么样？我们不需要管理层参与，只需要这个团队。

PETRA：我觉得可行。这样我们既能完善演示流程，又能同时向客户展示更多的功能。

David 看起来很满意，Steve 在白板上写下了以下内容：

- Dianne 和 Steve 承诺投入 Proseware 项目，专注于故事交付。
- 每两周向客户演示一次。
- 期间仅向团队演示。
- 在演示前额外留出半小时，用来过一遍议程并确认一切正常。

#### 值得保留的事情？

有时候，最好的做法是不采取行动——换句话说，把团队做过的、但尚未成为习惯的积极事项记录下来。这就是“值得保留的事情”这一问题的主题。

STEVE：那“值得保留的事情”呢？我们主动做过什么应该继续保持的事情吗？

所有人都保持沉默。

STEVE：好吧，如果会议结束后有人想到什么，请告诉我，我们会创建一个行动项。

#### 意外之事？

几乎每个冲刺都会暴露出一些意外。团队可能发现过时的流程需要更新、某个需求没有被正确捕获，或者某个软件突然停止工作。冲刺回顾中的“意外之事”部分旨在捕获所有这些项目，以免未来再次被归为意外。

STEVE：那“意外之事”呢？

DAVID：我很惊讶他们喜欢我的内容过滤想法！

DIANNE：说实话，我觉得这很有意义。他们正将 Proseware 瞄准某一特定人群，这可能对他们代表很大价值。

PETRA：我同意，这是个好主意。也许这正是我们应该继续做的：不断想出新点子。

Steve 在白板的相应列中把它记了下来。

TOM：让我感到意外的是，Steve 和 Dianne 并没有全职投入这个项目。

PETRA：好的，还有其他人吗？

DIANNE：我也很意外。我原本以为我会全职参与 Proseware，但 Steve 和我需要去处理另一个项目的紧急问题。

STEVE：我们应该与管理层达成某种协议，让其他人而不是我们在下一个冲刺接手这项工作。

DIANNE：好计划。

Steve 把这个记在了白板上。

STEVE：好的，谢谢大家。总的来说，这是一个不错的冲刺，也是这个项目的良好开端。我们继续努力。

PETRA：我同意。让我们落实这次回顾中商定的更改，并确保下周继续沿着同样的道路前进。

会议结束，团队离开。

### 总结

第一个冲刺对团队来说算是基本成功。虽然并非一切都按计划进行，但团队在短时间内收集了一些宝贵的反馈。这是任何敏捷流程中的关键部分：用于采取纠正措施的建设性批评总是近在咫尺。

在下一章中，团队将继续进行第二个冲刺的工作，并推进那些尚未实现的用户故事。

## 第12章 自适应示例：冲刺2

### 在本章中，你将

- 观察团队的第二次冲刺规划会议。
- 跟进下一批用户故事的实现与演变。
- 观察团队的第二次冲刺演示与回顾。

在本章中，Trey Research 团队继续为 Proseware 项目实现用户故事。由于在第一次冲刺的演示中收到了客户的反馈，项目方向略有改变。团队设定了以下冲刺目标：

> 在对话中添加可选的 markdown 格式文本，过滤消息内容以使其适当，并确保能够同时服务 300 个用户

这个冲刺目标包含了团队承诺在冲刺期间完成的所有用户故事。像往常一样，团队将以向客户演示来结束冲刺——以获取反馈并告知客户进展——并进行冲刺回顾，团队将在回顾中讨论冲刺出现的任何问题，并肯定团队在冲刺期间所做的出色工作。

不过，首先，团队以规划会议开始冲刺。

### 规划

项目的第二次规划会议让团队成员能够讨论他们在冲刺目标中承诺的用户故事。第二个冲刺包含以下用户故事：

- 我希望发送能够正确格式化的 markdown 消息。
- 我希望过滤消息内容以使其适当。
- 我希望能够同时服务数百个用户。

全体团队成员聚集在会议室中，讨论开始：

PETRA：由于上个冲刺演示时收到的反馈，我们的待办事项中新增了一个用户故事。

STEVE：客户希望我们优先实现内容过滤，而不是实现只读对话。

DIANNE：那么我们现在应该估算这个故事。

STEVE：是的，如果我们能对这个故事进行估算，就能了解这个冲刺我们有多少容量。

DIANNE：好的，数到三，我们一起亮出估算。

每个人都翻动各自的纸牌，然后亮出结果。
