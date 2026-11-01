
克隆以发挥作用。执行并返回某种结果的活动应派生自 `ActivityWithResult` 类——注意，此处最好使用泛型 `Activity<TResult>` 类，因为它提供了强类型的 `Result` 属性。

在构造自定义活动时，决定派生自哪个基类往往是主要难题，本章将展示一些示例，帮助您选择合适的基类。

为了让活动执行某些操作，它通常需要重写 `Execute()` 方法，该方法根据所选择的基类有若干不同的签名。这些签名如下表所示。

| 基类 | 执行方法 |
|---|---|
| `AsyncCodeActivity` | `IAsyncResult BeginExecute(AsyncCodeActivityContext, AsyncCallback, object)`<br>`void EndExecute(AsyncCodeActivityContext, IAsyncResult)` |
| `CodeActivity` | `void Execute (CodeActivityContext)` |
| `NativeActivity` | `void Execute (NativeActivityContext)` |
| `AsyncCodeActivity<TResult>` | `IAsyncResult BeginExecute(AsyncCodeActivityContext, AsyncCallback, object)`<br>`TResult EndExecute(AsyncCodeActivityContext, IAsyncResult)` |
| `CodeActivity<TResult>` | `TResult Execute (CodeActivityContext)` |
| `NativeActivity<TResult>` | `void Execute (NativeActivityContext)` |

在这里您可能会注意到，传入 Execute 方法的参数有所不同，因为使用了特定于类型的执行上下文参数。在 Workflow 3.x 中，只使用一个类（`ActivityExecutionContext`）；而在 Workflow 4 中，我们针对不同类别的活动使用不同的上下文。

主要区别在于，`CodeActivityContext`（以及由其派生的 `AsyncCodeActivityContext`）与 `NativeActivityContext` 相比，功能集有限。这意味着从 `CodeActivity` 和 `AsyncCodeActivity` 派生的活动对其容器的操作能力要弱得多。例如，前面介绍的 `WriteLine` 活动只需要向控制台写入内容，因此它不需要访问其运行时环境。更复杂的活动可能需要调度其他子活动或与其他系统通信，在这种情况下，您需要从 `NativeActivity` 派生才能访问完整的运行时。在您创建自己的自定义活动时，我们会再次讨论这个主题。

WF 提供了许多标准活动，以下各节将给出其中一些活动的示例以及您可能使用这些活动的场景。Workflow 4 使用三个主要程序集：`System.Activities.dll`、`System.Activities.Core.Presentation.dll` 和 `System.Activities.Presentation.dll`。

## If 活动

顾名思义，此活动类似于 C# 中的 If-Else 语句。

当您将 If 活动拖放到设计表面上时，会看到一个活动，如图 44-4 所示。If 是一个复合活动，包含两个子活动，它们分别放置在屏幕的 Then 和 Else 部分中。

![](img/d7d2ffa0a76feaab821930e95daace93_1373_0.png)

在工作流中这样做，因为它可以定义任意数量的分支，每个分支都可以等待一个触发操作发生后再运行。一旦触发被激活，该分支内的其他活动便会执行。

作为一个具体示例，请考虑上一节中概述的费用报销流程。这里我们将有一个 Pick 活动，包含三个分支——一个用于处理已批准的报销，一个用于处理被拒绝的报销，第三个用于处理超时。

该示例可在下载中的 03_PickDemo 代码中找到。其中包含一个示例工作流，由 Pick 活动和三个分支组成。运行时，系统会提示您接受或拒绝报销。如果经过 10 秒或更长时间，它将关闭此提示并改为运行延迟分支。

在示例中，DisplayPrompt 活动用作工作流中的第一个活动。它调用接口上定义的方法，该方法会提示经理进行批准或拒绝。由于此功能定义为接口，因此提示可以是电子邮件、即时消息或任何其他通知经理有待处理的费用报销的方式。然后工作流执行 Pick，它等待来自此外部接口的输入（批准或拒绝），同时也等待一个延迟。

当 Pick 执行时，它实际上会在每个分支的第一个活动上排队等待，当一个事件被触发时，它会取消所有其他等待事件，然后处理引发事件的分支的其余部分。因此，在费用报告被批准的情况下，WaitForAccept 活动完成，下一个操作是写出确认消息。然而，如果您的经理拒绝报销，WaitForReject 活动完成，在示例中它会输出一条拒绝消息。

最后，如果 WaitForAccept 和 WaitForReject 活动都没有完成，WaitForTimeout 会在其延迟到期后最终完成，然后费用报告可以路由给另一位经理——可能会在 Active Directory 中查找该人。在示例中，当 DisplayPrompt 活动执行时，会向用户显示一个对话框，因此如果延迟执行，您还需要关闭该对话框，这就是图 44-7 中名为 ClosePrompt 的活动的作用。

![](img/d7d2ffa0a76feaab821930e95daace93_1376_0.png)

## 图 44-7

该示例中使用的一些概念尚未涵盖——例如如何编写自定义活动或等待外部事件；不过，我们将在本章后面讨论这些主题。

## 自定义活动

到目前为止，您使用的都是 System.Activities 命名空间中定义的活动。在本节中，您将学习如何创建自定义活动并扩展这些活动，以在设计时和运行时都提供良好的用户体验。

首先，您将创建一个 DebugWrite 活动，该活动可用于在调试版本中向控制台输出一行文本。虽然这是一个简单的示例，但它将扩展以展示自定义活动可用的全部选项。在创建自定义活动时，您可以直接在工作流项目中构造一个类；但是，最好将自定义活动构造在单独的程序集中，因为 Visual Studio 设计时环境（尤其是工作流项目）会从您的程序集中加载活动，并且可能会锁定您正在尝试更新的程序集。因此，您应该创建一个简单的类库项目来在其中构造自定义活动。此示例的代码可在 04_CustomActivities 项目中获得。

像 DebugWrite 这样的简单活动将直接从 CodeActivity 基类派生。以下代码显示了一个构造的活动类，并定义了一个在活动执行时显示的 Message 属性：

```csharp
using System;
using System.Activities;
using System.Diagnostics;

namespace Activities
{
    public class DebugWrite : CodeActivity
    {
        [Description("The message output to the debug stream")]
        public InArgument<string> Message { get; set; }

        protected override void Execute(CodeActivityContext context)
        {
            Debug.WriteLine(Message.Get(context));
        }
    }
}
```

代码下载 04_CustomActivities

当 CodeActivity 被调度执行时，会调用其 Execute 方法——这是活动实际需要执行某些操作的地方。

在示例中，我们定义了 Message 属性，它看起来像一个普通的 .NET 属性；然而，它在 Execute 方法内的用法可能不熟悉。Workflow 4 所做的众多更改之一是状态数据的存储位置。在 Workflow 3.x 中，通常使用标准的 .NET 属性并将活动数据存储在活动本身内部。这种方法的问题在于，这种存储对工作流运行时引擎实际上是不透明的，因此为了持久化工作流，有必要对所有构造的活动执行二进制持久化，以忠实地恢复其数据。

在 Workflow 4 中，所有数据都存储在单个活动之外——因此这里的模型是，要获取参数的值，您需要向上下文请求该值；要设置参数的值，您需要向上下文提供新值。这样，工作流引擎可以在工作流执行时跟踪状态变化，并且可能只存储持久化点之间的变化，而不是整个工作流数据。

