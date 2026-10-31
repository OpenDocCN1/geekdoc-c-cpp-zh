
![](img/b8d8132a583ad73d511c4c1bb92e2df7_73_0.png)

Figure 2-19: 增强与内容转换中介模式

![](img/b8d8132a583ad73d511c4c1bb92e2df7_73_1.png)

Figure 2-20: 路由中介模式

## 外部系统访问模式

该模式族专注于托管在 ActiveMatrix Service Bus 中的组件与外部组件之间的交互。这些交互分为三类：

- 1. 通过 ActiveMatrix Service Bus 支持的协议进行交互
- 2. 通过 TIBCO 适配器或 ActiveMatrix 适配器进行交互
- 3. 通过 ActiveMatrix Service Bus 不支持的协议进行交互

### 通过受支持的协议进行交互

ActiveMatrix Service Bus 直接支持多种协议，包括 SOAP over HTTP 和 JMS、XML over JMS 以及 EJB 交互。直接交互模式有两种变体，取决于哪一方发起交互。图 2-21 显示了外部系统（通常是前端系统）发起交互的情况。这是当 ActiveMatrix 组合向外部组件公开 Web 服务时所使用的模式。

图 2-22 显示了 ActiveMatrix 组合发起交互的情况。这是当外部系统（通常是后端系统）公开一个被 ActiveMatrix 组合引用的 Web 服务时所使用的模式。

## 协调模式

协调模式决定了多方工作执行的协调方式。共有六种常见的协调模式（以及许多变体）：

- 1. 发射后不管
- 2. 请求-回复
- 3. 委派
- 4. 带确认的委派
- 5. 两阶段提交的分布式事务
- 6. 使用补偿事务的流程协调器

发射后不管协调模式（图 2-27）是最简单的协调模式，但它不提供任何一方检测流程中断的机会。

为了简化在更复杂流程中识别协调模式，我们引入了发起方活动的颜色编码。在此模式中，交互是异步的；即发送方不会等待接收方的响应。

请求-回复协调模式（图 2-28）为服务消费者提供了检测流程中断的机会，但前提是建立了响应时间的服务等级协议。它还在工作执行期间占用服务消费者的资源。这里展示的是该模式的同步变体。

图 2-29 显示了该模式的异步变体。这里服务消费者不会等待响应（并且很可能在执行其他活动）。当服务提供者完成工作后，它会异步发送回复。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_76_0.png)

Figure 2-27: 发射后不管协调模式

![](img/b8d8132a583ad73d511c4c1bb92e2df7_77_0.png)

Figure 2-28: 同步请求-回复协调模式

![](img/b8d8132a583ad73d511c4c1bb92e2df7_77_1.png)

Figure 2-29: 异步请求-回复协调模式

委派模式（图 2-30）涉及与服务提供者进行初始请求-回复交互，但回复仅表示将在稍后某个时间执行工作的承诺。当此模式出现时，通常工作结果会发送给第三方。该模式确保了责任的成功移交，但无法检测后续服务执行中的中断。

在带确认的委派（图 2-31）中，与服务消费者进行的额外异步交互会通知消费者服务是否（或未）已执行。为了使其有用，必须为预期此响应的时间范围建立服务等级协议。重要的是要清楚地认识到此确认的含义。在所示示例中，它表示工作已执行且服务结果已生成。然而，由于服务结果是使用发射后不管模式发送的，因此确认并未说明该结果成功交付给第三方的任何信息。

两阶段提交的分布式事务（图 2-32）提供了协调多方工作的能力。然而，如果任何一方不可用，应用程序将无法继续。此类事务也涉及相当多的开销。请注意，应用程序程序使用同步请求-回复与事务管理器进行交互。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_79_0.png)

Figure 2-32: 两阶段提交分布式事务协调模式

![](img/b8d8132a583ad73d511c4c1bb92e2df7_80_0.png)

Figure 2-33: 流程协调器

引入流程协调器（图 2-33）明确指定了管理整体流程的责任。流程协调器随后使用较低级别的协调模式来启动参与方的工作并确认其成功。

流程协调器常用的工具是补偿事务。补偿事务是一种撤销先前操作净效应的操作。图 2-34 说明了补偿事务的使用。

## ActiveMatrix Service Bus 策略

ActiveMatrix Service Bus 提供了在 ActiveMatrix 节点内强制执行的策略框架。这些策略提供了与传输无关的机制，用于

- 身份验证
- 授权
- 隐私（加密）
- 数据完整性（数字签名）
- 调优（线程管理策略）
- 事务

## 摘要

*TIBCO® Architecture Fundamentals* 为本书内容提供了基础。本章对该材料进行了简要回顾。

本书中的解决方案使用了 *TIBCO® Architecture Fundamentals* 中描述的若干产品。这些包括 Enterprise Message Service、ActiveMatrix Service Bus、ActiveMatrix Service Grid、ActiveMatrix BusinessWorks，以及 TIBCO 和 ActiveMatrix 适配器组合。

基于 ActiveMatrix Service Bus 的设计可以灵活地以多种方式部署。组件、服务和引用可独立部署，如果需要可放置在不同的节点上。部署在不同节点上的元素之间的通信通过部署环境私有的 Enterprise Message Service 实例进行。

*TIBCO® Architecture Fundamentals* 涵盖了若干设计模式，这些模式构成了本书中描述的模式的构建块。这些包括组件对之间的基本交互、事件驱动交互模式、中介模式、外部系统访问模式和协调模式。它还提供了 ActiveMatrix Service Bus 提供的策略框架概述。

- TIBCO® Adapter for Files z/OS (MVS)
- TIBCO® Adapter for Files (IBM i)
- TIBCO ActiveMatrix BusinessWorks™ Plug-in for Data Conversion
- TIBCO BusinessConnect™
- TIBCO Collaborative Information Manager™

阅读本章后，您应能够描述每种产品的适当用途。

## Hawk®

### 概述

Hawk 包含一组用于监控组件（正在执行的程序）及其上运行的服务状态的组件。对于需要监控组件的每个非大型机环境（物理或虚拟），运行两个 Hawk 可执行文件：Hawk Agent 和 Hawk Microagent Adapter（HMA）。在大型机上，TIBCO Mainframe Service Tracker 执行。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_84_0.png)

### Hawk Agent

Hawk Agent 是主力工作者。在规则库的指导下，它监控其环境中的组件（正在执行的程序），通过组件提供的应用程序微代理接口（AMI）与这些组件交互。大多数 TIBCO 产品提供 AMI 接口，并且有一个工具包可用于向其他组件添加 AMI 接口。Hawk Agent 使用 TIBCO 传输与 AMI 接口通信，即 Enterprise Message Service 或 TIBCO Rendezvous®。

Hawk Agent 还通过其自身的 AMI 接口提供功能。其中包括，代理能够通过 Rendezvous® 和 Enterprise Message Service 发送和接收任何消息。

### Hawk 规则

通常您使用 Rulebase Editor（图 3-2）创建 Hawk 规则，尽管规则库只是一个可以直接编辑的 XML 文件。规则名称（高亮的字符串）指定了规则将操作的数据来源。数据源指定了 Microagent，

![](img/b8d8132a583ad73d511c4c1bb92e2df7_85_0.png)

Figure 3-2: Hawk 规则库编辑器中的三个规则
