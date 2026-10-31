
执行顺序；或使用外部编排组件。在后一种情况下，如果流程是关键的，可以使用状态机来管理与协调组件的对话并检测故障。

TIBCO BusinessEvents 具有内置日志，可在 CDD 文件中进行配置。还可通过推理、查询和流程代理中的规则函数添加额外的日志记录和异常报告。

命名最佳实践将使您的设计更易于理解。规则的名称应表示规则识别的条件。函数的名称应表示其在解决方案中的预期作用。事件的名称应标识事件所宣布存在的情况。

## 事件模式识别

### 目标

TIBCO BusinessEvents® 事件流处理扩展包含用于识别事件模式的功能。本章探讨这些功能。阅读本章后，您将能够描述这些模式是如何定义的以及模式识别是如何部署的。您还将能够描述模式如何用于组件存活监控。

### 事件模式识别的需求

使用规则识别某些事件模式很困难。请考虑以下示例：

- 三个红球
- 其后是两个蓝球
- 其后是一个黄球

当然，您可以设计一个状态机来识别此模式（图 11-1）。这种方法的问题在于，随着模式变得

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_190_0.png)

**图 11-1：** *状态机模式识别器*

越来越复杂，设计状态机变得越来越困难和繁琐——并且验证其识别的模式是否正是您想要识别的模式。

复杂性的另一个维度是引入时间约束。请考虑以下变体：

- 五分钟内三个红球
- 其后在 30 秒内两个蓝球
- 其后在一小时内一个黄球

再次，您可以设计一个状态机来识别此模式（图 11-2），但这样做的复杂性不断增加开始变得明显。

从识别的角度来看，状态机是合适的工具。问题在于机器的构建。计算机科学对这一问题的传统答案是定义一种模式语言，以及一个随附的编译器，可自动生成

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_191_0.png)

**图 11-2：** *带超时的状态机模式识别器*

状态机，以及可在其中应用状态机来识别模式的运行时环境。TIBCO BusinessEvents 事件流处理扩展提供了识别事件模式的这些功能。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_193_0.png)

**图 11-3：** *模式元素*

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_193_1.png)

**图 11-4：** *模式部署*

（类的实例）被创建。每个实例需要两个回调函数，一个在识别到模式时调用，另一个在模式失败时调用。这些回调函数的签名是固定的。实例创建后，可以为模式定义中的任何变量分配值。

模式部署在推理代理中（图 11-4）。模式的处理由专用于模式匹配器的线程池处理。事件可通过预处理器函数或规则操作使用 `Pattern.IO.toPattern()` 函数发送到模式匹配器。模式回调函数可以创建事件并将其发送到通道，但不能与概念交互。模式匹配器线程池的大小可通过 `Pattern.Manager.Advanced.setPoolSize()` 函数设置。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_194_0.png)

- 1) 注册欺诈模式。
  - `Pattern.Manager.register(<pattern>)`
- 2) 创建模式的实例。
  - `Pattern.Manager.instantiate()`
- 3) 绑定完成和失败监听器并设置参数。
  - `Pattern.Manager.setCompletionListener(<instance>, <function>)`
  - `Pattern.Manager.setFailureListener(<instance>, <function>)`
  - `Pattern.Manager.setParameter<parameterType>(<value>)`
- 4) 部署模式。
  - `Pattern.Manager.deploy(<instance>, <deploymentInstanceName>)`
- 5) 向模式发送事件。
  - `Pattern.IO.toPattern(<event>)`

图 11-5：模式生命周期

实际部署过程由在推理代理中运行的代码管理（图 11-5）。该过程始于对 `Pattern.Manager.register(<pattern>)` 的调用，该调用创建表示模式的类。通常，此调用在启动函数中进行，但也可以在任何可以调用目录函数的地方进行。通过调用 `Pattern.Manager.instantiate()` 创建模式的实例。对于应持续运行的模式，此调用在启动函数中进行。对于仅在特定情况下运行的模式，此调用要么在预处理器函数中响应宣布这些情况存在的事件而进行，要么在识别这些情况的规则的操作部分中进行。不论实例化在哪里进行，都必须设置完成监听器和失败监听器以及任何参数的值。一旦这些操作完成，模式即可部署。

### 存活监控

模式的一种应用是存活监控。有时可能需要确定特定组件是否正在运行。一种方法是让组件发送周期性心跳并使用模式识别来

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_195_0.png)

*图 11-6：心跳识别*

确定组件是否仍在运行（图 11-6）。例如，组件可能每三秒发送一次心跳事件。模式可能是十秒滑动时间窗口内至少应有一个心跳。十秒内没有心跳则构成模式失败。

### 摘要

使用规则和手工制作的状态机识别复杂模式可能很困难。因此，TIBCO BusinessEvents 事件流处理器扩展提供了一种模式识别语言，使定义感兴趣的模式变得容易。该语言用于自动创建识别指定模式的状态机。

模式由推理代理部署。事件必须显式地由预处理器或规则的操作部分发送到模式匹配器。当匹配成功时，完成监听器回调函数将被调用；如果模式匹配失败，则失败监听器回调函数将被调用。

模式的生命周期由在推理代理中运行的代码管理。此代码定义模式、创建实例、设置回调函数和变量值，并部署模式。执行这些功能的代码可以位于启动函数、预处理器函数或规则的操作部分中。

模式可用于组件存活监控。如果组件预期定期发送心跳，则可以使用模式识别心跳的缺失并得出组件不再运行的结论。

## 集成

### 目标

提供复杂事件处理能力的组件不能孤立存在。它们所反应的大多数事件源自其他系统，它们所采取的许多操作由其他系统实现。与这些系统的集成至关重要。

集成是一个广泛的主题，其中大部分超出了本书的范围。集成和服务的基础知识在 TIBCO™ Architecture Fundamentals¹ 中有所介绍；更高级的相关主题在 Architecting Composite Applications and Services with TIBCO™ ² 中有所介绍。这些书籍描述了一些与 TIBCO BusinessEvents™、TIBCO ActiveMatrix BusinessWorks™、TIBCO ActiveMatrix® Adapter for Database、TIBCO ActiveMatrix® Adapter for Files 和 TIBCO Enterprise Message Service™ 等一起常用的 TIBCO™ 产品。它们还涵盖涉及这些产品的 SOA 概念和设计模式。

1. Paul C. Brown, TIBCO® Architecture Fundamentals, Boston: Addison-Wesley (2011).
2. Paul C. Brown, Architecting Composite Applications and Services with TIBCO®, Boston: Addison-Wesley (2012).
