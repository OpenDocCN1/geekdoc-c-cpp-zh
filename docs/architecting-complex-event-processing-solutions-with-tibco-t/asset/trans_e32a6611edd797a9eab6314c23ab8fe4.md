

TIBCO BusinessEvents® 当然可以通过其通道，使用受支持的传输方式与任何组件进行交互。此外，该产品还具备其他集成能力。本章将探讨这些额外的集成能力。阅读本章后，您将能够描述 TIBCO BusinessEvents® 如何与以下组件交互：

- TIBCO ActiveMatrix BusinessWorks™
- Web 服务
- 数据库

## 与 TIBCO ActiveMatrix BusinessWorks™ 交互

TIBCO ActiveMatrix BusinessWorks™ 提供了一个插件，用于简化与 TIBCO BusinessEvents® 的交互。使用该插件可使 ActiveMatrix BusinessWorks 定义 RuleServiceProvider 配置。每个配置都包含指向您要交互的 TIBCO BusinessEvents 项目中的 EAR 和 CDD 文件的指针。该配置还会标识 CDD 文件中定义的处理单元。当 ActiveMatrix BusinessWorks 引擎运行时，它将在与 ActiveMatrix BusinessWorks 引擎相同的 JVM 中运行该处理单元的一个实例。³

³ 类似这种在同一个 JVM 中运行 TIBCO ActiveMatrix BusinessWorks 实例与处理单元的集成方式，自 TIBCO BusinessEvents 5.x 版本起已弃用。

该插件提供了四个可在 ActiveMatrix BusinessWorks 进程中使用的活动：(1) 发送事件，(2) 接收事件，(3) 等待事件，以及 (4) 调用规则函数。

### TIBCO ActiveMatrix BusinessWorks™ 发送事件

发送事件活动使 ActiveMatrix BusinessWorks 能够将事件发送到处理单元中的特定目的地（图 12-1）。此活动的配置会显示事件数据结构，以便将值直接映射到事件属性。执行该活动会将事件发送到指定的目的地。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_199_0.png)

**图 12-1：** *TIBCO ActiveMatrix BusinessWorks™ 发送事件*

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_199_1.png)

**图 12-2：** *TIBCO ActiveMatrix BusinessWorks™ 等待事件*

### TIBCO ActiveMatrix BusinessWorks™ 等待事件

等待事件活动是 ActiveMatrix BusinessWorks 进程中的阻塞活动（图 12-2）。当进程执行该活动时，它会等待 TIBCO BusinessEvents 发送事件。该事件的属性可供 ActiveMatrix BusinessWorks 进程使用。

等待事件活动可以与发送事件活动结合使用，以实现 ActiveMatrix BusinessWorks 与 TIBCO BusinessEvents 之间的同步请求-应答交互。

### TIBCO ActiveMatrix BusinessWorks™ 接收事件

TIBCO ActiveMatrix BusinessWorks 接收事件活动是一个 ActiveMatrix BusinessWorks 进程启动器（图 12-3）。当 TIBCO BusinessEvents 发送指定类型的事件时，ActiveMatrix BusinessWorks 进程启动器接收该事件，并创建一个使用该事件作为进程启动器的进程实例。该事件的属性可在进程中使用。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_201_0.png)

(a) 同步交互

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_201_1.png)

(b) 异步交互

图 12-5：TIBCO BusinessEvents® 作为服务提供方

socket 连接。通常使用推理代理作为服务提供方，但流程代理甚至查询代理也可以扮演此角色。

在大多数情况下，当代理扮演服务提供方的角色时，请求的接收是生成结果所需的全部处理的触发事件。收到请求后，处理会持续进行，直到产生结果。

在某些情况下，当代理扮演异步提供方的角色时，请求的接收并不会触发所有工作：部分剩余工作是响应另一个事件而执行的。在某些情况下，该事件与请求直接相关——例如计时器到期或来自某个后端系统的异步响应。在其他情况下，另一个事件可能是对缓存概念的更新，而该概念的变化会触发响应的生成（参见第 10 章中的“参考数据变更协调”模式）。

## TIBCO BusinessEvents® 作为异步服务消费方

使用 TIBCO BusinessEvents 进行异步交互的服务消费是相当直接的。然而，异步交互通常需要保留处理响应所需的上下文信息。有三种设计模式可用于维护此上下文：

- 概念维护异步上下文
- 状态机维护异步上下文
- 流程维护异步上下文

### 概念维护异步上下文

使用此方法时，推理代理在规则的操作部分或预处理函数中发送请求（图 12-6）。同时，还会创建或更新一个概念，用于保存处理应答所需的任何上下文信息。

当返回应答时，应答事件的预处理函数会从缓存中检索该概念（假设使用了仅缓存模式）。为了使检索成为可能，必须将概念的标识符（通常是 extID）包含在请求中，并在应答中返回。服务提供方还必须设计为在应答中返回请求中的标识符。如果使用 JMS 作为传输方式，并将概念的 extID 用作请求的 JMSCorrelationID，则 JMS 规范要求服务提供方在应答的 JMSCorrelationID 中返回相同的值。随后，应答将在预处理函数中或由应答事件到达所触发的规则中进行处理。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_202_0.png)

图 12-6：概念维护异步上下文

在发送请求时，如果用于保存上下文的 概念已存在，则必须在规则的操作部分发送请求，因为预处理函数不能修改现有概念——它只能创建新概念。

### 状态机维护异步状态

TIBCO BusinessEvents® 数据建模扩展为概念增加了状态机功能。这使得一种使用状态机来维护异步状态并管理整个交互的模式成为可能。图 12-7 展示了这种状态机的草图。

回想一下，状态机由概念拥有（第 5 章）。当状态机启动时，它发送的请求包含一个数据元素，即拥有该状态机的概念的 extID。这个 extID 预期会在应答中返回，并将用于将该应答与此特定状态机实例相关联。然后状态机进入等待应答的状态。当收到带有匹配 extID 的应答时，状态机进行另一次转换。

至于收到应答后要采取的操作，有两种可能的方法。一种是将操作作为状态机结构的一部分，在状态转换时或进入/退出状态时执行。另一种方法是将操作放在规则的 action 部分，该规则在状态机发生变化时触发。从规则的角度来看，这是对拥有状态机的概念的一种更改。

这种方法的一个优点是状态机具有计时器基础设施，可用于识别在指定时间段内未收到应答的情况。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_203_0.png)

图 12-7：状态机维护异步状态

## HTTP 发送请求调用

此模式使用目录 HTTP 函数 `sendRequest()`。它既可用于传统的 HTTP 请求-应答交互，也可用于 SOAP 交互（图 12-9）。在使用此模式时应谨慎，因为发起调用的线程在等待应答期间会被占用。当有大量线程可用时（例如在执行预处理函数时），被阻塞的线程可能只是在决定线程池大小时需要考虑的一个条件。但是，当该函数在规则的操作部分执行，且 RTC 配置为单线程时，所有 RTC 处理都将被阻塞，直到请求完成。

## TIBCO BusinessEvents® 流程编排

### Web 服务调用

TIBCO BusinessEvents 流程编排扩展包含一个 Web 服务任务，用于同步服务调用（图 12-10）。回想一下，所有任务都由线程池执行：

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_205_0.png)

图 12-9：HTTP 发送请求调用

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_205_1.png)

图 12-10：TIBCO BusinessEvents® 流程编排 Web 服务调用

