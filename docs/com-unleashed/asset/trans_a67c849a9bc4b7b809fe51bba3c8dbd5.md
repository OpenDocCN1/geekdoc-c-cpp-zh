

### 清单 25.14（续）

```cpp
if ( OUTKEY == dwKey )
{
    wprintf(L"Got quit message thread %x\n", GetCurrentThreadId());
    ExitThread(0);
}

// Display message
ShippingRequest * psr = (ShippingRequest *) wcsBody;
wprintf(L"Received message on thread %x\n", GetCurrentThreadId());
wprintf(L"Label: %s\n", wcsLabel);
wprintf(L"Account: %ld, Product ID: %ld, Quantity: %ld\n",
        psr->Account, psr->Product, psr->Quantity);

// Try to ship order
if ( !ExecuteSlowUnstableLinkShippingRequest(
        psr->Account, psr->Product, psr->Quantity ) )
{
    wprintf(L"Shipping failed thread %x\n", GetCurrentThreadId());
    // We should retry the shipping operation or requeue here
    continue;
}

// Release the transaction and display success
wprintf(L"Order shipped on thread %x\n", GetCurrentThreadId());
}

// Exit with error
wprintf(L"Abort on thread %x\n", GetCurrentThreadId());
return 1;
}

bool ExecuteSlowUnstableLinkShippingRequest( long, long, long )
{
    Sleep(4000);
    return ( rand() % 4 ) > 0;
}
```

关于此应用程序，需要注意的一个重要点是：你不得不放弃事务。事务只能与同步调用一起工作。此应用程序中的线程在大多数情况下彼此独立运行。不过，同步关闭过程很重要。退出主线程会隐式调用 `ExitProcess()`，并会终止发货线程。因此，你创建了特殊的 `quitKey`，对于每个需要关闭的线程，它都会排队到 IOCP 一次。完成此操作后，主线程会等待发货线程清理完毕，然后退出。另外，请看 `MQReceiveMessage` 调用中的另外两处更改。第一处是超时值 `INFINITE`。这一点很重要，因为你不希望挂起的 I/O 操作超时。否则会导致 `GetQueuedCompletionStatus()` 调用返回错误。最后一个问题是，Receive 调用会修改一些大小属性，以反映实际检索到的数据。在循环中重置这些属性非常重要，这样 MSMQ 就不会认为你的缓冲区正在缩小。过小的缓冲区会返回错误，但错误来自 `GetQueuedCompletionStatus()`！这就有问题，因为你希望看到的错误代码是由 `MQReceiveMessage()` 传递的错误代码，而不是 `GetQueuedCompletionStatus()` 的。请注意，原始 I/O 错误消息可以在重叠结构的内部字段中找到。

## 队列安全

MSMQ ActiveX 组件提供对安全上下文信息的支持，这些信息可通过 MSMQMessage 和 MSMQQueueInfo 类的属性和方法获得。基本的 MSMQ 队列安全功能是在通过 MSMQQueueInfo 对象设置创建队列时配置的。可以通过 Authenticate 属性将队列配置为仅接受经过身份验证的消息。在调用 MSMQQueueInfo::Create() 期间，可以将队列设置为全局可读，使任何应用程序都能从队列接收消息，而不仅仅是所有者。QueueInfo 对象还提供一个 Privacy Level 属性，允许队列接受已加密、未加密或两者皆可的消息。

你看到的示例创建的是具有默认安全设置的队列。以这种方式创建队列会将创建进程的用户和组设置为队列的用户和组。自由访问控制列表已初始化，为创建者提供完全控制，并为其他人提供属性读取、安全读取和发送访问权限。没有提供用于审核的系统访问控制列表。

MSMQ 队列是管理员可见的企业对象，使用标准 NT 安全描述符加以保护。正如我在第 20 章“组件负载平衡”中所讨论的，可以通过 MSMQ Explorer 管理安全功能。也可以通过 MSMQ API 调用接口管理队列安全。管理队列安全需要了解第 18 章“COM+ 安全”中讨论的 Windows/COM+ 安全服务。有几个例程提供 MSMQ 安全支持：

- `MQCreateQueue()`
- `MQGetQueueSecurity()`
- `MQSetQueueSecurity()`
- `MQFreeSecurityContext()`
- `MQGetSecurityContext()`

可以使用前三个例程创建、检索和修改队列安全功能。队列既维护标准权限，也维护队列特定权限，例如查看消息、接收消息、发送消息和接收日志。队列还支持对队列权限和属性的读写访问。安全上下文设置用于通过证书管理消息身份验证。模拟其他用户的服务器必须利用 MSMQ 安全上下文系统，在模拟上下文中发送消息。

## 消息安全

消息本身有若干安全措施。消息可以使用各种哈希算法进行数字签名，并使用各种加密技术进行加密。

消息的 Authentication Level 属性指定消息是否要求接收队列使用其数字签名对消息进行身份验证。启用了身份验证的消息可以设置其 Hash Algorithm 属性，以指定非默认签名方法。MSMQ 通过 MSMQ_CALG 枚举提供多种签名选择。消息还提供 Sender Certificate 属性，使应用程序能够提供自己的证书和身份验证管理。

消息的 Privacy Level 属性指示消息是否应加密。Encrypt Algorithm 属性指定要用于消息的加密类型。如果未设置此属性，MSMQ 使用默认值。目前，通过底层 RSA 提供程序实现的公钥安全支持 RC2 和 RC4 算法。

## 总结

在本章中，你详尽地研究了 MSMQ 的高级功能。你学习了如何使用基于消息的、内部的、DTC 和 MTS 管理的事务来构建事务性 MSMQ 应用程序。你还研究了用于管理 MSMQ 队列的互斥异步技术。Ping/Pong 和 OrderEntry 示例应用程序为探索游标以及消息和队列提供的各种属性提供了一个简单基础。如果你读到了这里，那你肯定是在努力成为 MSMQ 大师。

## 第26章：松散耦合事件

### 本章内容

- 一些基本术语的定义  696
- 比较发布-订阅的选项  697
- COM+ 事件服务  701
- 事件服务演示  705
- COM+ 事件服务的高级问题  711
- 事件筛选  717

任何基于组件的系统的常见需求是：使一个组件能够通知其他组件它们关心的事件已经发生。例如，一个股票行情组件需要在给定股票价格变化时得到更新，或者一个缺货订单履行组件需要知道某些零件何时已入库。

事实上，这是一个如此常见的编程任务，以至于《设计模式》的作者明确命名了该任务，并提供了一种以编程方式解决它的通用方法。该模式称为观察者模式，它定义了一种机制，组件可以通过该机制发布它拥有可能对其他组件重要的知识这一事实。然后，其他组件可以订阅它们关心的事件。因此，许多人经常将这种模式称为发布/订阅模式。

在本章中，你将学习 COM+ 如何通过 COM+ 事件服务解决此问题，从而使你为实现这个常见问题的解决方案所需的编程要求降至最低。本章首先解释可用于处理事件通知的不同技术，以及为什么松散耦合事件（特别是 COM+ 事件服务）能很好地解决此问题。接下来，你将了解发布者和订阅者组件在事件服务体系结构中的角色。之后，你将看到如何编写一个触发事件的简单应用程序，以及另一个接收该事件触发通知的应用程序。在你学习了处理松散耦合事件的基础知识后，本章将深入讨论处理 IEventSubscription 接口以及使用 COM+ 事件服务管理接口注册和注销临时订阅的高级问题。最后，本章以一节关于如何以编程方式筛选订阅者传入事件的内容作为结尾。

### 一些基本术语的定义

在继续之前，我将花一点时间澄清一些关于松散耦合事件、COM+ 事件服务以及本章的基本术语：

- 设计模式
- 发布者
- 订阅者
- COM+ 事件服务

#### 设计模式

设计模式被定义为针对反复出现的问题的文档化解决方案。1995年，Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 发表了一本广受关注的

