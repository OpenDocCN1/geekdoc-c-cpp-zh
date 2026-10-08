
# 表 11-9: 集合处理活动

| 活动 | 描述 |
| --- | --- |
| AddCollection<T> | 向指定的集合中添加项。 |
| ClearCollection<T> | 清空指定集合中的所有项。 |
| ExistsInCollection<T> | 指明给定项是否存在于给集合中。如果项在集合中，则 Result 属性为 true；否则为 false。 |
| RemoveFromCollection<T> | 从指定的集合中移除项。如果该项已从集合中移除（其曾存在于集合中），则 Result 属性为 true；否则为 false。 |

## 消息活动

工作流涉及不同的人和系统在工作流中具有定义良好的角色。通常，整个工作流（一个业务流程）在技术上被分为若干更小的工作流以组成整个过程。例如，从你的角度来看，从网上商店订书的过程是一个业务工作流，在你收到书籍时完成。从网上商店的角度来看，这个过程必须被划分为更小的工作流（下单、发货调度、收款、交付等），并且通常还会涉及第三方服务提供商。

当你创建分布式工作流（无论是简单的还是复杂的）时，这些工作流必须进行通信。在许多情况下，工作流构建在异构的后端系统（ERP、CRM、库存、企业目录等）之上，这些系统为业务流程提供服务。WF 4.0 比 WF 3.5 提供了更复杂的工作流间通信和访问外部服务的模型。它与 Windows Communication Foundation (WCF) 无缝集成，并提供了比 WF 3.5 更多的活动。

表 11-10 总结了 WF 4.0 的内置消息活动。

# 表 11-10: 消息活动

| 活动 | 描述 |
| --- | --- |
| Send | 此活动向服务发送消息。它有大约十个属性用于设置消息，包括 Content、EndpointAddress、OperationName 等许多属性。 |
| Receive | 此活动接收消息。当消息到达时，可以通过 Content 属性进行访问。 |

# 表 11-10（续）

| 活动 | 描述 |
|---|---|
| SendReply | 此活动作为服务端请求/响应消息交换模式的一部分发送消息。 |
| ReceiveReply | 此活动作为请求/响应消息交换模式的一部分接收消息。 |
| CorrelationScope | 此活动为子消息活动执行隐式的关联管理服务。通过相关的 CorrelationHandle 实例，可以将此类请求和相关的响应进行关联。例如，当 CorrelationScope 包含一个 Send 和一个 ReceiveReply 活动时，工作流将响应消息与正确的工作流实例进行关联。 |
| InitializeCorrelation | 此活动在不发送或接收消息的情况下初始化关联。通常情况下，关联是通过发送或接收消息来初始化的。如果必须在发送或接收消息之前初始化关联，则可以使用此活动来初始化关联。 |
| TransactedReceiveScope | 此活动允许你将事务流入工作流或进入调度器-服务器端的事务。这在 WF 3.5 中是不可能的。你可以在客户端拥有事务，在服务器端拥有事务，但它们无法协作。通过 TransactedReceiveScope 活动，WF 4.0 提供了一个极大的解决方案。 |

> 在工作流中使用消息需要对消息模式和 WCF 有深入理解。深入探讨这个主题绝对超出了本书的范围。在本章中，你将看到一个演示 WorkflowServiceHost 类的示例，其中将使用一些消息活动。微软发布了许多示例来演示 WF 4.0 中的消息。你可以从此处下载这些示例：http://www.microsoft.com/downloads/details.aspx?FamilyID=35ec8682-d5fd-4bc3-a51a-d8ad11a8792&language=en，或者可以在 MSDN 上搜索 "WCF WF Samples .NET 4"。

虽然大多数处理活动现在包含在 System.Activities 和 System.Activities.Statements 命名空间中，但消息活动是在 System.ServiceModel.Activities 命名空间定义的。

## 使用补偿事务模型

尽管表 11-8 总结了与事务处理相关的活动，但很难想象补偿事务模式在实践中是如何工作的。因为它是 WF 4.0 的核心组成部分，理解其背后的概念有助于你开发更健壮的工作流。

让我们创建一个示例，帮助你理解这种模式在 WF 4.0 中是如何工作的。此示例通过 TryCatch 活动演示了错误处理概念。

## ConferenceWorkflow 示例

此示例将演示一个非常简化的会议注册案例，期间你还要安排旅行并预订酒店。

创建一个新的 Workflow Console Application，并将其命名为 ConferenceWorkflow。将一个 TryCatch 活动拖入 Workflow 的设计表面，然后将一个 Sequence 活动拖入 Try 块中。将其 DisplayName 设置为 Conference Preparations。在 Conference Preparations 中添加一个 WriteLine 活动，并将其 Text 属性设置为 "Conference preparations completed"。点击 Finally 块中的 "Add an activity"，并拖入一个带有 "Conference preparations completed" 的 WriteLine 活动。点击 Try 块中的 Conference Preparations 链接。

图 11-16 显示了你创建的工作流。

正如你预期的，当你按下 Ctrl+F5 运行此工作流时，它会生成以下输出：

> Conference preparations started
Conference preparations completed

在 Conference Preparations 的 WriteLine 下添加一个 Parallel 活动，并将其 DisplayName 设置为 "Registration and Travelling"。在 Parallel 活动中添加一个 Sequence 活动，并将其 DisplayName 设置为 "Registration"。在 Registration 中添加一个 WriteLine 活动，将其 Text 属性设置为 "Registration completed"。在 Travelling 中添加一个 WriteLine 活动，将其 Text 属性设置为 "Travelling completed"。在 Try 块中添加一个 Parallel 活动，并将其 DisplayName 设置为 "Registration and Travelling"。

（注：原文后续部分存在大量重复和 OCR 错误，此处已根据核心逻辑完成翻译清理。）
