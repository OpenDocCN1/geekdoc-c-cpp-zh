
FIGURE 10-1 The Hype Cycle can help explain attitudes toward new techniques and technologies.

The x-axis of the graph represents advancing time, and the y-axis represents expectations. Initially there is a trigger, which could be a new technological discovery or a helpful new technique or procedure. Soon thereafter, expectations rise rapidly until they hit the “peak of inflated expectations.” At this point, the technology or technique begins to be viewed as less all-powerful than was initially believed. This causes expectations to plummet rapidly to the “trough of disillusionment.” All is not lost, however, because the “slope of enlightenment” gradually leads to a “plateau of productivity.” At this point, the technology or technique is established and has more realistic expectations attached to it.

The expectations of developers are often located somewhere on this graph with respect to one or more programming technologies or techniques. For example, at Trey Research, David is nearing the peak of inflated expectations with respect to design patterns, the SOLID principles, unit testing, and refactoring. Dianne is just crawling out of the trough of disillusionment. In the sprint meetings detailed throughout this chapter, pay close attention to their questions and responses and consider how they are shaped by their relative positions on the Hype Cycle.

For completeness, it is worth noting that Steve’s experience has moved him along the graph sufficient for him to be on the plateau of productivity. Not only that, but Steve is no longer as susceptible to the Hype Cycle as he once was. He is cautious when approaching new techniques and technologies that are purported to increase productivity, quality, efficiency—or any other metric. As a result, his expectations do not oscillate as wildly when he is presented with a new technique or technology.

### Test analyst

Tom is the team’s test analyst. His focus is on test automation. He has always had an ability to find a software product’s weaknesses and improve the overall user experience through an increased robustness. He likes to treat features as black boxes and is less concerned with how something is implemented than in whether it works to specification—and beyond.

Tom feels like he is overworked in the team because he is constantly rejecting work that has been implemented. This means that he has to test and retest a story at least twice before it works to his exacting standards. It is a point of pride for Tom that defects are rarely deployed to a client’s machine and are instead caught early by his automated tests.

### The product

Trey Research has been hired by a client to develop a new online chat application called Proseware. This is a web-based application that will allow people to chat from around the world. During first discussions with the client, Petra was able to determine that the client has a lot of ideas for the project but would like to put something small together so that they are better able to decide the direction of the application. Trey Research is well suited to this product because of its incremental development style and its ability to balance this against potentially rapid changes in requirements.

Petra spoke to the client before the project started so that she could prepare the team with some information about what they will develop. The client wants Proseware to be hosted by Trey Research, thus the team is free to choose whichever platforms and tools the team members think are best for the project. Petra was sure to ask the client what their requirements were with regard to Proseware’s capacity for users. She agreed with the client that the application needs to only support 20 concurrent users at a time, and this has become a key nonfunctional requirement of Proseware.

Before the team sets to work on writing any code, Petra calls a team meeting so that the team members can discuss the project and try to create an initial backlog of user stories. With these stories in place, the team can set to work on creating something demonstrable within a single sprint.

### Initial backlog

The client provided Petra and the team with a list of features for Proseware. This was provided as a prose description, and the team’s goal for the meeting is to turn this into one or more user stories.

We view Proseware as the primary site for people to chat. However, we realize that Rome was not built in a day, so we have limited our mission statement somewhat so that something can be delivered in the fastest possible timeframe.

Although we do want to allow users to be able to send each other images or files, the key functionality will be centered around textual communication. Anyone who is in a room should receive all the messages that are sent from anyone else.

Because the textual side of chat is so important, we need the members of a room to be able to send each other formatted text—something like HTML. Of course, they shouldn’t be able to spam the chat with lots of meaningless images or videos!

Some of the conversations in Proseware should not be editable by some users, and some users should only be allowed to read, but not contribute.

Petra brings this short description to the meeting, and the team sets to work trying to find the user stories.

### Finding stories in prose

Sometimes clients write prose descriptions of their expectations, as in the previous section. From this, the team must extract and negotiate the user stories to be implemented. The Trey Research team arranges a meeting to find the user stories in the description of Proseware that was supplied by the client.

PETRA: Okay, has everyone read the description? [Everyone nods, displaying a range of enthusiasm.]

STEVE: There’s a lot here!

DAVID: Not really—we could probably get through this in a single sprint. [Steve smiles broadly.]

PETRA: Can someone please show me how this is going to give us a list of user stories?

DIANNE: First thing we can do is pick out the verbs and nouns: send, receive, format, spam...room, conversation, users, members, chat...

STEVE: True, that’s a lot right there.

PETRA: As a user, I want to... So that...

DIANNE: Are they just users?

STEVE: Sounds like there’s more than one role here.

DAVID: They call them users, and then they call them members.

TOM: Aren’t you a participant in a conversation, though?

STEVE: Perhaps, but we should use their ubiquitous language. There are some roles around conversations being read-only or not, surely?

DIANNE: Yeah, that sounds like it’s hinting toward some kind of permissions system.

PETRA: Can someone pick out a story, please?

PETRA：但他们要求的是格式化文本啊？

STEVE：别担心，那是另一个故事——它会在纯文本交付之后才出现。

PETRA：好的。作为房间成员，我想向其他房间成员发送格式化文本消息。

STEVE：这是第二个了。还有吗？

DAVID：我想创建房间？

DIANNE：是的。我觉得这肯定会让那个人成为房主，对吧？作为房主，我想创建房间来对会话进行分类？

STEVE：很好。

TOM：他们说他们还想要发送图片和文件。

PETRA：是的，那是另一个故事。

STEVE：还有一个：我想创建只读会话。

DIANNE：最后一句也涵盖了。我想我们已经完成了。

### 故事点估算

到目前为止，团队成员一致认为他们已经从客户的需求中找到了用户故事。

他们根据以下每一条要点创建了用户故事卡片：

- 我想向其他房间成员发送纯文本消息。

- 我想创建房间来对会话进行分类。

- 我想向其他房间成员发送格式化文本。

- 我想发送图片和/或文件。

- 我想创建只读会话。

团队将卡片摆放在桌子上，准备分配故事点。由于只有五个故事，团队决定使用计划扑克来估算所需工作量。

PETRA：发送纯文本消息应该不会太难吧？

DAVID：我只需一个小时就能搞定！[史蒂夫和黛安挑了挑眉毛。汤姆翻了个白眼。]

STEVE：嗯，这件事其实没法先做。没有房间，就没有参与者。

DIANNE：没错，这里存在依赖关系，但这不会改变工作量的大小。[史蒂夫点头表示同意。]

PETRA：大家都准备好了吗？

经过最后的洗牌，团队成员亮出了他们的卡片：

| PETRA | TOM | STEVE | DIANNE | DAVID |

| --- | --- | --- | --- | --- |

| 3 | 3 | 5 | 5 | 1 |

PETRA：嗯，这有点参差不齐。大卫，为什么是一？

DAVID：这里几乎没什么可做的：只是接收一些输入，然后把它显示到屏幕上。

DIANNE：不完全是，大卫。事情没那么简单。我们需要把文本保存到某个地方，并且能够读回来。其他房间成员也需要能够读取它。

STEVE：确实，黛安说得对。我们需要考虑这里的架构。

DAVID：哦，是啊。我之前以为只是把它输出到浏览器窗口而已。但是，当然，那样只会被写它的人看到——无法共享。哇，那就难多了！

PETRA：好的，我们要重新估算吗？

团队成员从三倒数，然后再次亮出卡片：

| PETRA | TOM | STEVE | DIANNE | DAVID |

| --- | --- | --- | --- | --- |

| 5 | 5 | 5 | 5 | 5 |

STEVE：我们能不能把这个故事拆分成“读取”和“写入”两个部分？

DIANNE：抱歉——我不太明白你的意思。

TOM：我觉得他的意思是，我们可以有一个故事是查看已发送到房间的消息，另一个故事是向该房间发送消息。对吗，史蒂夫？

STEVE：是的。我只是觉得从非常小的粒度开始会有所帮助。我知道估算为五并不算特别大，但在开发的早期阶段，这个数字已经很有分量了。
