
现在，按键盘上的F5键运行应用程序。在“Enter a number”文本框中输入一个数字，此处为5；然后在“Enter another number”文本框中输入一个数字，此处为200。在“Range divided by number”文本框中输入用于除第一个和第二个文本框中指定数字范围的数字，此处为12。现在单击“Click Me”按钮，该按钮将仅显示那些可被“Range divided by number”文本框中指定数字整除的数字。应用程序的输出如图27.23所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1400_0.png)

图27.23：显示PLINQQuery应用程序的输出

## 摘要

在本章中，您学习了不同的LINQ查询。您还学习了LINQ中使用的不同标准查询运算符。本章还讨论了LINQ to Objects、LINQ to ADO.NET和LINQ to XML的概念。此外，您还学习了扩展方法、匿名方法和Lambda表达式的概念。您还了解了LINQ中引入的新概念：PLINQ查询。

在下一章中，您将学习C# 2010中的Windows Workflow Foundation。

![](img/e073a4882197be4ab61103cbe0bcb394_1402_0.png)

## 使用Windows Workflow Foundation

| 如果需要立即解决以下问题： | 请参阅页面： |
|---------------------------------------|-----------|
| 创建简单的WF应用程序      | 1370      |
| 使用If活动和变量   | 1372      |
| 创建和恢复书签      | 1375      |

## 深入探讨

Windows Workflow Foundation（WF）是一种用于定义、执行和管理工作流的Microsoft技术。WF中的工作流由一系列连接的步骤组成，每个步骤表示应用程序要执行的一个活动。WF包含顺序工作流和状态机工作流。顺序工作流从头到尾运行，由工作流引擎启动每个步骤；而状态机工作流则表示一组状态、转换和操作。一个状态被指定为开始状态，然后根据外部事件和用户交互，可以转换到另一个状态。状态机可以有一个确定工作流结束的最终状态。工作流使用声明式模型来编写程序，通过将预定义的活动链接在一起，而不是逐行编写命令式编程模型。

WF于2006年随.NET Framework 3.0发布，随后在.NET Framework 3.5中进行了更新。在.NET Framework 4.0中，对WF的支持得到了增强，引入了许多新功能，例如流程图和工作流活动模型。WF包含各种用于创建工作流的模板、用于定义逻辑和控制流的活动，以及用于执行WF应用程序的运行时引擎。工作流项目本身并不是完整的应用程序，但它们构成了应用程序，并且需要宿主来运行工作流。此外，WF提供了编写应用程序逻辑所需的各种服务和功能。它还提供了用于构建应用程序和服务逻辑的声明式框架；从而使您能够处理异步和并行任务以及其他复杂处理。

在本章中，您将了解WF 4.0的各种新功能以及组件。接下来，您将了解用于创建工作流的活动。您还将了解WF 4.0中的各种工作流类型。此外，您将了解内置活动和书签活动。最后，您将学习如何在应用程序中处理错误和承载工作流。

让我们从WF 4.0的新功能开始。

### 列出WF 4.0的新功能

在WF 4.0中，您可以轻松地创建、执行和维护工作流，并在工作流中实现新功能。WF 4.0帮助您用更少的时间和精力创建工作流。WF 4.0中的一些新功能如下：

- 改进的工作流设计器
- 数据流模型的增强
- Flowchart控制流活动
- 工作流活动模型
- 内置活动库的增强

让我们逐一讨论这些功能。

### 改进的工作流设计器

WF 4.0中最明显的改进领域之一是工作流设计器，它基于Windows Presentation Foundation（WPF）构建。工作流设计器现在支持复杂的工作流，并提供了更简单的机制来创建自定义活动。您可以使用可扩展应用程序标记语言（XAML）来定义活动的外观以及活动在可视化设计环境中与用户交互的方式。此外，您可以在应用程序中重新托管工作流设计器，使其他用户能够轻松查看您的工作流并与之交互。重新托管工作流设计器还为工作流设计提供了自定义的用户体验。

### 数据流模型的增强

数据流模型定义给定活动的输入和输出，管理数据，并在运行时提高工作流的性能。WF 4.0提供了两个选项：变量和参数，用于数据存储和数据流。您可以使用变量在活动中存储数据。您还可以使用一些专用参数，例如`InArgument`、`InOutArgument`和`OutArgument`，来确定数据移入和移出活动时的数据方向。

### Flowchart控制流活动

在WF 4.0中，引入了一个新的控制流活动`Flowchart`，用于在工作流中实现循环和条件分支。`Flowchart`控制活动允许您创建灵活的工作流，您可以在其中导航回以前的步骤，也可以根据工作流中的条件跳过步骤。您可以通过代码或使用工作流设计器将`Flowchart`活动添加到工作流中。您可以在一个工作流中创建多个`Flowchart`活动，但一次只能执行一个活动。

### 工作流活动模型

在WF 4.0中，活动是创建工作流的基本单元，通过使用`Activity`类在工作流中实现。工作流活动模型使您能够将工作流的复杂业务流程分解为更小的流程。这确保了具有自动异常处理的可靠流控制。您可以使用`CodeActivity`类为活动添加基本的自定义功能。

### 内置活动库的增强

WF 4.0活动库包含一组可在工作流中使用的预定义活动。这些活动并不打算通过继承来创建新功能。添加到内置活动库中的一些新活动如下：

- 新的流控制活动，如`DoWhile`、`Pick`、`TryCatch`、`ForEach`、`Switch`和`ParallelForEach`
- 用于操作数据的活动，如`Assign`
- 集合活动，如`AddToCollection`
- 用于控制事务的活动，如`TransactionScope`和`Compensate`
- 消息传递活动，如`SendContent`和`ReceiveReply`

现在让我们了解WF 4.0的组件。

## 描述WF 4.0的组件

WF由多个协同工作的组件组成，以创建所需的工作流。例如，自定义活动是WF的一个组件，允许您定义要在工作流中执行的自己的活动。借助此组件，您可以根据需要轻松创建基于工作流的应用程序。WF的所有组件如下：

- 工作流和活动
- 宿主进程
- 活动数据模型
- 基础活动库
- 自定义活动
- 运行时引擎
- 运行时服务

## 工作流和活动

工作流是表示流程模型的操作集合。每个操作表示一个活动。这些活动存储为描述现实世界流程的模型。工作流提供了一种描述长时间运行过程执行顺序的方法。在Visual Studio 2010中，工作流实例由进程内运行时引擎创建和维护。

## Host Process

主机进程是一个可执行程序，用于承载工作流。它可能是一个 Windows 应用程序、Web 应用程序或 Web 服务应用程序。主机进程通过使用 `WorkflowInvoker` 类与工作流进行交互，并将工作流作为方法调用。工作流在主机进程中被承载并运行。您可以在主机进程中使用 Web 服务或远程处理，以使其他应用程序能够与工作流通信。

## Activity Data Model

在 WF 4 中，活动通过使用以下元素存储和维护数据：

- `Variable`: 在活动中存储数据
- `Argument`: 将数据在活动和工作流之间移入移出
- `Expression`: 表示返回在参数中使用的值的活动

## Base Activity Library

基础活动库是一组标准操作集合，称为活动，用于创建工作流。活动实现的操作可以是简单的操作，例如延迟，也可以是包含多个子活动的复合活动。基础活动库中包含的活动为控制流、状态管理、事件处理以及与应用程序和服务通信提供功能。每个活动都有一个活动执行上下文，表示活动的执行环境。

## Custom Activities

除了基础活动库中提供的标准活动之外，您还可以创建新的活动以满足特定的业务需求。创建自定义活动可能需要支持您想要与 WF 集成的特定应用程序。自定义活动通常通过属性和继承创建。您可以创建两种类型的自定义活动，基础和复合。要创建基本的自定义活动，您需要继承 `Activity` 类；而要创建自定义复合活动，您需要继承 `CompositeActivity` 类或其派生类型。

## Runtime Engine

WF 的运行时引擎提供执行和管理工作流生命周期所需的基本功能。它与主机进程交互，并负责执行每个工作流实例。一个主机进程可以同时与多个运行时引擎交互，其中每个引擎执行多个工作流实例。主机进程通过使用以下任一类与运行时引擎交互：

- `WorkflowInvoker` — 将工作流作为方法调用
- `WorkflowApplication` — 显式控制单个工作流实例的执行
- `WorkflowServiceHost` — 允许工作流的多个实例之间进行基于消息的交互

## Runtime Services

运行时服务提供用于自定义工作流运行时行为的功能。WF 4.0 中可用的一些运行时服务如下：

- Persistence service — 使您能够将工作流的状态保存到或从持久介质中恢复。由于工作流可能需要很长时间才能完成；因此，同时运行的多个工作流会使用大量内存。持久性服务使工作流能够保存以供以后使用。
- Tracking services — 使您能够监控工作流的状态。当同时有多个工作流处于活动状态时，这尤其有用（例如，在购物车应用程序中）。跟踪服务使您能够创建应用程序来监控您的工作流。
- Timer service — 管理 `DelayActivity` 活动所需的时间。
- Transactions service — 提供数据完整性所需的事物支持。
- Threading services — 管理用于执行工作流实例的物理线程。

让我们在 WF 的上下文中探索活动。

## Exploring Activities

在 WF 中，工作单元以活动的形式包含。这些活动提供流程控制、异常处理、数据持久性、加载或卸载工作流、跟踪和事务流的设施。您可以使用以下类型实现这些活动：

- `Activity` – 将预先存在的活动组合起来，以在 WF 环境中创建执行工作流的工作单元
- `CodeActivity` – 通过使用 `CodeActivityContext` 类在托管代码中处理执行逻辑
- `AsyncCodeActivity` – 处理执行逻辑以在工作流中实现异步任务
- `NativeActivity` – 通过使用 `NativeActivityContext` 类提供对运行时功能的访问，例如创建书签和调用异步任务

现在，让我们探索 WF 4.0 中的工作流类型。

## Describing Types of Workflows

工作流是一系列要按顺序执行的活动的集合。在 WF 4.0 中，有两种类型的工作流 Flowchart 和 Procedural。流程图工作流帮助您使用常见的流程图元素创建工作流。流程图是设计程序的通用标准。在 WF 中，`Flowchart` 活动通常用于实现非顺序工作流，有时在流程图中未使用 `FlowDecision` 节点时实现顺序工作流。`Flowchart` 活动包含继承自 `FlowNode` 类的流节点集合。流程图可以包含以下类型的节点或元素：

- `FlowStep` – 按顺序执行流程图的活动
- `FlowDecision` – 根据布尔条件显示执行。它类似于 If 构造。
- `FlowSwitch` – 根据排他性开关显示执行。它类似于 Switch 构造。

另一方面，过程式工作流帮助您使用基本和顺序执行标准创建工作流。在 WF 中，过程式工作流使用 While、Switch、ForEach 和 If 等流程控制构造来执行活动。这些流程控制构造类似于在过程式语言中发现的构造。过程式工作流还可以包含其他流程控制活动，例如 `Flowchart` 和 `Sequence`。

现在，让我们简要了解内置活动。

## Exploring Built-in Activities

在 WF 4.0 中，有某些内置活动可帮助您定义应用程序的工作流。您可以在所有工作流应用程序中使用内置活动。这些活动分为以下类别：

- Control Flow – 控制工作流中的执行流程
- Flowchart – 控制流程图中的执行和分支
- Messaging – 允许工作流发送和接收 Windows Communication Foundation (WCF) 消息
- Runtime – 在工作流应用程序中实现数据持久性和工作流终止过程
- Primitives – 管理变量并安排工作流执行
- Transaction – 执行数据事务、补偿和取消
- Collection – 允许您在工作流中处理集合对象，例如向集合添加和删除项目或清除集合
- Error Handling – 实现错误处理和恢复
- Migration – 将工作流从 WF 的早期版本迁移到当前版本

表 28.1 描述了控制流活动：

## Table 28.1: Control Flow Activities

| Activity | Description |
|---|---|
| DoWhile | 至少执行一次工作流元素，即使条件不为真 |
| ForEach | 对 Values 集合中给出的每个值至少执行一次操作 |
| If | 根据 If-Then-Else 条件执行工作流 |
| Parallel | 同时且异步执行子活动 |
| ParallelForEach | 对集合中存在的每个元素并行执行嵌入语句 |
| Pick | 根据基于事件的控制流执行工作流 |
| PickBranch | 显示 Pick 活动中的替代执行路径 |
| Sequence | 按顺序执行其他活动 |
| Switch | 根据表达式的值从多个语句中选择一个语句执行 |
| While | 当条件评估为真时执行工作流元素 |

表 28.2 描述了流程图活动

## Table 28.2: Flowchart Activities

| Activity | Description |
|---|---|
| Flowchart | 使用流程图的通用模型执行包含的活动 |
| FlowDecision | 表示充当条件节点的 FlowNode 元素 |
| FlowSwitch <T> | 表示实现具有活动类型的一个表达式的开关构造的 FlowNode 元素，并为每个匹配提供单独的结果 |

表 28.3 描述了消息活动

## Table 28.3: Messaging Activities

| Activity | Description |
|---|---|
| Send | 表示发送消息的活动 |
| SendReply | 表示发送对接收消息的响应的活动 |
| Receive | 表示接收消息的活动 |
| ReceiveReply | 表示接收回复的活动 |

表 28.4 描述了运行时活动

## Table 28.4: Runtime Activities

| Activity | Description |
|---|---|
| Persist | 表示请求工作流持久性的活动 |
| TerminateWorkflow | 表示终止当前正在运行的工作流实例的活动 |

表 28.5 描述了原语活动

## Table 28.5: Primitives Activities

| Activity | Description |
|---|---|
| Assign | 表示将值分配给工作流中声明的变量的活动 |
| Delay | 表示在特定时间段后执行工作流的活动 |

| 表 28.5：原语活动 |
|---|---|
| 活动 | 描述 |
| InvokeMethod | 表示执行 Common Language Runtime (CLR) 对象的方法的活动 |
| WriteLine | 表示向 TextWriter 对象写入文本的活动 |

表 28.6 描述了事务活动

| 表 28.6：事务活动 |
|---|---|
| 活动 | 描述 |
| CancellationScope | 将取消逻辑与执行的主路径关联 |
| CompensableActivity | 支持其子活动的补偿 |
| Compensate | 调用 CompensableActivity 类的补偿处理程序 |
| Confirm | 调用 CompensableActivity 类的确认处理程序 |
| TransactionScope | 定义事务边界 |
| TransactedReceiveScope | 定义由接收到的消息启动的事务的作用域（生命周期） |

表 28.7 描述了集合活动

| 表 28.7：集合活动 |
|---|---|
| 活动 | 描述 |
| AddToCollection | 向集合添加一项 |
| ClearCollection | 清除集合中的所有项 |
| ExistsInCollection | 检查集合中的一项并在该项存在于集合中时返回 true |
| RemoveFromCollection | 从集合中删除一项，并在成功删除该项时返回 true |

表 28.8 描述了错误处理活动

| 表 28.8：错误处理活动 |
|---|---|
| 活动 | 描述 |
| Rethrow | 表示重新抛出上次从 TryCatch 活动抛出的异常的活动 |
| Throw | 表示抛出异常的活动 |
| TryCatch | 表示执行异常处理的活动 |

让我们探索 WF 4.0 中的书签活动。

## 了解书签活动

在 WF 4.0 中，书签是一种使活动能够在不中断工作流线程的情况下等待输入的机制。当活动发出信号表示它正在等待来自用户的输入时，它可以创建一个书签。书签是通过使用 `BookmarkOptions` 类创建的。该类提供了以下书签类型：

- None — 指预期仅恢复一次的书签。这是默认的书签类型。
- MultipleResume — 指可以恢复多次的书签。
- NonBlocking — 指可能永远不会被恢复的书签。

书签可以通过在工作流外部编写代码并使用 `ResumeBookmark` 类的方法来恢复。

让我们学习如何在 WF 4.0 中处理运行时错误。

## 处理运行时错误

到目前为止，您已经了解了工作流以及用于创建工作流的活动。假设您创建了一个工作流，并且在执行工作流时它抛出错误。此错误可以很容易地在小型工作流中处理和纠正，另一方面，如果您的工作流复杂且包含许多各种活动，则查找和纠正该错误可能很困难。因此，WF 4.0 提供了各种机制来处理运行时错误。这些机制如下所示：

- Exceptions – 使您能够使用 `TryCatch` 活动来处理在工作流执行期间引发的异常。您还可以使用 `Rethrow` 活动重新抛出异常。在执行 Try 和 Catch 部分中包含的活动之后，将执行 Finally 部分的活动。
- Transactions – 提供 `TransactionScope` 活动以在工作流中使用事务。
- Compensation – 提供补偿活动，例如 `CompensableActivity`、`Compensate` 和 `Confirm`，以补偿先前完成的任务或后续失败。
- Cancellation of Workflows – 提供 `CancellationScope` 活动、`CompensableActivity` 活动或提供取消逻辑的自定义活动。

让我们现在学习如何在 WF 4.0 中托管工作流。

## 托管工作流

托管是将您的工作流与其他用户共享的过程，以便他们可以在其应用程序中使用您的工作流。您可以将您的工作流托管在主机应用程序中，如果您的工作流符合用户的需求，他们可以从主机应用程序中使用您的工作流。WF 4.0 提供了三个类来托管工作流。这些类如下所示：

- `WorkflowInvoker` – 将工作流作为其方法调用
- `WorkflowApplication` – 包含控制流活动、书签恢复和持久性
- `WorkflowServiceHost` – 托管工作流并允许在各种工作流实例之间发送和接收消息

让我们在以下各节中探索这些类。

## WorkflowInvoker 类

`WorkflowInvoker` 类属于 `System.Activities` 命名空间。`WorkflowInvoker` 类的类层次结构如下所示：

```
