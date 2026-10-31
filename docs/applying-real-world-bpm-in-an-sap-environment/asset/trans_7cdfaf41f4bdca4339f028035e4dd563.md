
The solution for achieving consistency in an SOA landscape with subsequent service calls is to introduce a compensation service. A compensation service is designed to roll back all changes (even partial changes) made by a service call in the corresponding system. This means the service and the compensation service always form a pair.

实现 SOA 架构中后续服务调用的一致性的解决方案是引入补偿服务。补偿服务旨在回滚服务调用在对应系统中所做的所有更改（即使是部分更改）。这意味着服务和补偿服务始终构成一对。

In real process modeling, this would mean error handling always calls the compensation service if the original service call fails. So far, this is not a very complex infrastructure, because it only involves manual modeling for the process designer.

在实际流程建模中，这意味着如果原始服务调用失败，错误处理始终会调用补偿服务。迄今为止，这并不是一个非常复杂的架构，因为它仅涉及流程设计人员的手动建模。

It becomes a little bit more difficult, however, if there are subsequent service calls that belong together to achieve a consistent state in the connected systems. If one of the calls fails, all changes have to be rolled back. As a result, service call A, which happened before service call B and which failed, has to be rolled back too. In this case, the compensation services for B and A therefore have to be invoked, because otherwise the state in System A is not consistent with the state in System B. The modeling for a pattern of this kind looks like Figure 14.20.

然而，如果存在属于一起以实现连接系统中的一致状态的后续服务调用，则会变得稍微复杂一些。如果其中一个调用失败，所有更改都必须回滚。因此，在服务调用 B 之前发生的服务调用 A 且失败的，也必须回滚。在这种情况下，必须调用 B 和 A 的补偿服务，否则系统 A 中的状态与系统 B 中的状态不一致。此类模式的建模如 图 14.20 所示。

![](img/30a88f75957f887ca511028d178ca5c7_469_0.png)

## Error Resolution: Retry

## 错误解决：重试

Because composite applications are applications that call services at different back-end systems in a probably loosely coupled way, a requirement is that service calls may need to be re-launched if the initial call fails. Usually in SOA, HTTP is used as the protocol, and within this protocol the failure can occur at the delivery of the information packages. The retry of a service is accompanied by a retry policy. If the condition of the policy evaluates true, a retry is triggered; otherwise other measures such as compensation patterns may take effect.

由于复合应用程序是以松散耦合的方式调用不同后端系统服务的应用程序，因此要求如果初始调用失败，服务调用可能需要重新启动。通常在 SOA 中，使用 HTTP 作为协议，而在此协议中，故障可能发生在信息包的传递过程中。服务的重试伴随着重试策略。如果策略的条件评估为真，则会触发重试；否则，其他措施（如补偿模式）可能会生效。

There are two kinds of failures for which the service consumer cannot be sure that the request has been processed properly:

服务消费者无法确定请求是否已正确处理的失败有两种类型：

- 1. **Undelivered request**
  The message is sent but does not reach the provider (see Figure 14.21).

- 1. **未送达请求**
  消息已发送但未到达提供方（参见 图 14.21）。

![](img/30a88f75957f887ca511028d178ca5c7_470_0.png)

**Figure 14.21** Undelivered Request

**图 14.21** 未送达请求

- 2. **Undelivered response**
  The message is sent and the response is sent, but the response does not reach the consumer (see Figure 14.22).

- 2. **未送达响应**
  消息已发送且响应已发送，但响应未到达消费者（参见 图 14.22）。

The retry pattern describes the infrastructure rather than a particular behavior of one of the involved components. Thus, it is not a matter of how customers using services can resolve the issue, but rather the solution of the issue affects all communicating and mediating components.

重试模式描述的是基础设施，而不是所涉及组件中的某个特定行为。因此，这不是服务使用者如何解决问题的事，而是问题的解决方案影响所有通信和中介组件。

Nonetheless, evaluation of the conditions of retry policies can be handled in a process model; no particular requirements of the infrastructure need to be taken into account. At the end of this chapter a process model we depict a sample that demonstrates the usage of retry policies.

尽管如此，重试策略条件的评估可以在流程模型中处理；无需考虑基础设施的特殊要求。本章末尾我们描绘了一个流程模型示例，演示了重试策略的使用。

![](img/30a88f75957f887ca511028d178ca5c7_471_0.png)

Figure 14.22 Undelivered Response

图 14.22 未送达响应

In general, the infrastructure issue can be described as follows:

总体而言，基础设施问题可以描述如下：

- 1. The service call is routed over an ESB or messaging mediators to the service provider or an alternative provider.
- 1. 服务调用通过 ESB 或消息中介路由到服务提供方或替代提供方。
- 2. The consumers and service providers communicate via ESB or mediators that intercede between consumer and provider.
- 2. 消费者和服务提供方通过 ESB 或在消费者和提供方之间介入的中介进行通信。
- 3. An ESB acts as an intermediate service requestor.
- 3. ESB 充当中间服务请求方。
- 4. The ESB intercepts the request messages, evaluates the provider's retry policy, and may even determine alternative providers.
- 4. ESB 拦截请求消息，评估提供方的重试策略，甚至可能确定替代提供方。

Reliable messaging, as specified for instance by the WS-RM standard, is an example of such mediated communication:

可靠消息传递，例如由 WS-RM 标准指定，是此类中介通信的一个示例：

- 1. The service is idempotent, and another call with the same payload and ID will not cause additional state changes in the corresponding backend system.
- 1. 服务是幂等的，使用相同负载和 ID 的另一次调用不会导致对应后端系统中产生额外的状态更改。
- 2. A service call/message will be identified by a unique ID (e.g., UUID) attached to the message.
- 2. 服务调用/消息将由附加到消息的唯一 ID（例如 UUID）标识。

There are two fault scenarios:

存在两种故障场景：

- The service provider receives the message and caches or persists the ID and sends the response the first time the request arrives at the provider. However, the consumer does not obtain the message, due to transmission errors.
- 服务提供方接收到消息并缓存或持久化 ID，并在请求首次到达提供方时发送响应。然而，由于传输错误，消费者未获得该消息。
- The service provider does not receive the message, due to transmission errors.
- 由于传输错误，服务提供方未接收到消息。

The fault situations can be handled in this way:

故障情况可以按以下方式处理：

- 1. If the consumer does not receive the response, it will retry the request with the same message ID.
- 1. 如果消费者未收到响应，它将使用相同的消息 ID 重试请求。
- 2. The consumer evaluates the retry policy and retries its response accordingly.
- 2. 消费者评估重试策略并据此重试其响应。
- 3. The service provider provides the response message for the given ID. The payload for the response is evaluated from scratch, or it may be retrieved from cached data if the provider successfully received the request in a previous call.
- 3. 服务提供方为给定 ID 提供响应消息。响应的负载从头开始评估，或者如果提供方在之前的调用中成功接收到请求，则可以从缓存数据中检索。
- 4. The service is not idempotent but will provide an operation by which the service consumer may poll or request again the response for the initially sent request.
- 4. 服务不是幂等的，但会提供一种操作，通过该操作服务消费者可以轮询或再次请求初始发送请求的响应。

This pattern is very similar to the one for idempotent calls. The only difference is that a service provider has to keep track of already obtained messages/IDs, and the cache has to be in sync. This pattern is similar to the previous pattern, but instead of the request being sent again, a lightweight repetition request is sent.

该模式与幂等调用的模式非常相似。唯一的区别是服务提供方必须跟踪已获取的消息/ID，并且缓存必须保持同步。该模式与前一种模式类似，但不是再次发送请求，而是发送轻量级重复请求。

The lightweight request contains the previous message ID. The provider sends either the response or a notification that the request for the message ID has not arrived at the service provider. In the latter case the consumer needs to send another request containing the initial payload.

轻量级请求包含之前的消息 ID。提供方发送响应或通知，表明该消息 ID 的请求未到达服务提供方。在后一种情况下，消费者需要发送包含初始负载的另一个请求。

As in the previous pattern, additional infrastructure on both the provider and consumer side is required.

与前一种模式一样，提供方和消费者双方都需要额外的基础设施。

Apart from these infrastructure considerations, a retry policy may be evaluated in a dedicated evaluation activity in a process model. The activity precedes the service consumption. If the policy condition evaluates true and the service will be consumed successfully, the normal flow will be followed. Otherwise a compensation flow will be chosen, for instance. Figure 14.23 depicts an example of this pattern where a timer determines the timeout for the request-response time.

除了这些基础设施方面的考虑之外，重试策略可以在流程模型中的专用评估活动中进行评估。该活动先于服务消费。如果策略条件评估为真且服务将成功被消费，则将遵循正常流程。否则，例如将选择补偿流程。图 14.23 描述了该模式的一个示例，其中计时器确定请求-响应时间的超时。

There are more variants of the pattern. For instance, it might be crucial that both the consumer and provider need to commit their state changes. In this case some sort of two-phase commit patterns may be additionally applied.

该模式还有更多变体。例如，可能至关重要的是消费者和提供方都需要提交其状态更改。在这种情况下，可能还会额外应用某种两阶段提交模式。

## 14.2 Highlights of the Innovation Provided by SAP NetWeaver BPM and BRM

## 14.2 SAP NetWeaver BPM 和 BRM 提供的创新亮点

The second released version of SAP NetWeaver Business Process Management provides several innovations to customers and partners who want to extend the value of their SAP applications.

SAP NetWeaver Business Process Management 的第二个发布版本为希望扩展其 SAP 应用程序价值的客户和合作伙伴提供了多项创新。

These innovations address the needs of business process analysts and experts, process developers, and process participants. Additionally, interoperability with SAP applications and other task user interfaces has been improved.

这些创新满足了业务流程分析师和专家、流程开发人员以及流程参与者的需求。此外，与 SAP 应用程序和其他任务用户界面的互操作性已得到改进。

SAP NetWeaver BPM provides a comprehensive business process management system, unifying human and system automation processing steps, where a business process is more than just several orchestrated services. This BPM system supports the composition of event-driven processes through a seamless combination of service, event, and human task with business rules through a tight integration with SAP NetWeaver Business Rules Management (BRM). SAP NetWeaver BPM includes a business-friendly graphical modeler based on the standard Business Process Modeling Notation (BPMN) that is used to define and drive the business process execution by the process server. People starting or participating within processes interact with SAP NetWeaver BPM via the process desk.

SAP NetWeaver BPM 提供了一个全面的业务流程管理系统，统一了人工和系统自动化处理步骤，其中业务流程不仅仅是几个编排的服务。该 BPM 系统通过服务、事件和人工任务与业务规则的无缝组合，支持事件驱动流程的组合，通过与 SAP NetWeaver Business Rules Management (BRM) 的紧密集成实现。SAP NetWeaver BPM 包含一个基于标准业务流程建模符号（BPMN）的业务友好型图形建模器，用于由流程服务器定义和驱动业务流程执行。启动或参与流程的人员通过流程桌面与 SAP NetWeaver BPM 交互。

SAP NetWeaver BPM benefits from the fact that it ships as part of an integrated composition environment, SAP NetWeaver Composition Environment, which supports model-driven development via an integrated toolset including out-of-the-box Enterprise Service Repository (ESR) integration and consistent lifecycle management for all composite design artifacts. Next we will present some of the highlights of the innovation provided by SAP NetWeaver BPM and BRM 7.2.

SAP NetWeaver BPM 的优势在于它作为集成组合环境 SAP NetWeaver Composition Environment 的一部分发布，该环境通过集成工具集支持模型驱动开发，包括开箱即用的企业服务存储库（ESR）集成以及对所有复合设计工件的一致生命周期管理。接下来我们将介绍 SAP NetWeaver BPM 和 BRM 7.2 提供的创新亮点。

### 14.2.1 Business Analyst Experience

### 14.2.1 业务分析师体验

In SAP NetWeaver BPM 7.2, the business-friendly modeling has been enabled through various capabilities. A new, dedicated process modeling perspective for process sketching has been introduced (see Figure 14.24).

在 SAP NetWeaver BPM 7.2 中，通过各种功能启用了业务友好型建模。引入了一个新的、专用的流程建模视角用于流程草图（参见 图 14.24）。

This business-friendly perspective focuses on the nontechnical aspects of the process model and the hand-over to the process development perspective that developers use to complete an initial process model resulting from that process sketching effort with implementation details.

这种业务友好型视角专注于流程模型的非技术方面以及向流程开发视角的交接，开发人员使用该视角在流程草图工作产生的初始流程模型中添加实现细节。
