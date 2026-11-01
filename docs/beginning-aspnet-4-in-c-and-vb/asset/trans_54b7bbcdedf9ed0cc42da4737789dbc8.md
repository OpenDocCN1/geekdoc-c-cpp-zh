
此控件绑定到 Retry 活动的 Body 属性，而 HintText 定义了在未向控件添加子活动时显示的帮助文本。XAML 中还包含了一些用于显示设计器展开或收缩版本的样式——这确保了该活动的工作方式与内置活动相同。此示例的所有代码和 XAML 都可在 04_CustomActivities 解决方案中找到。

## 工作流

到目前为止，本章主要集中在活动上，但尚未讨论工作流。工作流只是一系列活动的列表，事实上工作流本身也只是一种活动类型。使用这种模型简化了运行时引擎，因为引擎只需要知道如何执行一种类型的对象——即派生自 Activity 类的任何对象。

你已经见过 WorkflowExecutor 类，它可用于执行工作流，但如当时所述，这只是执行工作流的方式之一。执行工作流有三种不同的选项，每种选项的功能各不相同。在深入了解执行工作流的其他方法之前，我们必须先探讨参数和变量。

## 参数和变量

工作流可以被视为一个程序，而任何编程语言的一个方面都是能够创建变量，并将参数传入和传出该程序。自然地，Workflow 4 支持这两种结构，在本节中我们将向你展示如何定义参数和变量。

首先，假设工作流正在处理一份保险单，因此传递给工作流的一个可能参数是保单 ID。要为工作流定义参数，你需要进入 Designer 并点击左下角的 Arguments 按钮。这会列出为工作流定义的参数，如图 44-12 所示，你也可以在此添加自己的参数。

![](img/d7d2ffa0a76feaab821930e95daace93_1383_0.png)

图 44-12

要定义一个参数，你需要指定 Name、Direction（可以是 In、Out 或 InOut）以及该参数的数据类型。你可以 optionally 指定默认值，如果未提供参数则会使用该值。

参数的方向用于定义参数是作为工作流的输入、作为工作流的输出，还是在 InOut 方向的情况下作为输入和输出。

在本章的第一部分，我们描述了使用 WorkflowInvoker 类来执行工作流。Invoke 方法有几个重载可用于将参数传递给工作流。它们以名称/值对的字典形式传递，其中名称必须与参数的名称完全匹配——此匹配区分大小写。下面代码用于将 PolicyId 值传递给工作流——此示例的代码可在 05_ArgsAndVars 解决方案中找到。

```
Dictionary<string, object> parms = new Dictionary<string, object>();
parms.Add("PolicyId", 123);

WorkflowInvoker.Invoke(new PolicyFlow(), parms);
```

因此，当工作流处于休眠状态时，最好将其从内存中卸载，并在事件触发工作流继续时再重新加载。为此，我们需要在 WorkflowApplication 中添加一个 InstanceStore 对象，并对前面的代码进行一些其他小的修改。框架中抽象 InstanceStore 类有一个实现——SqlWorkflowInstanceStore。要使用此类，首先需要一个数据库，其脚本默认可在 C:\Windows\Microsoft.NET\Framework\v4.0.21006\Sql\en 目录中找到。请注意版本号可能会更改。

在此目录中你会找到多个 SQL 文件，但你需要的是 SqlWorkflowInstanceStoreSchema.sql 和 SqlWorkflowInstanceStoreLogic.sql。你可以将其运行在现有数据库上，也可以根据需要创建全新的数据库，并且可以使用完整的 SQL Server 安装或 SQL Express 安装。

一旦拥有数据库，就需要对托管代码进行一些修改。首先，需要构造一个 SqlWorkflowInstanceStore 实例，然后将其添加到工作流应用程序中：

```csharp
SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore
(ConfigurationManager.ConnectionStrings["db"].ConnectionString);

AutoResetEvent finished = new AutoResetEvent(false);

WorkflowApplication app = new WorkflowApplication(new Workflow1());
app.Completed = (e) => { finished.Set(); };
app.PersistableIdle = (e) => { return PersistableIdleAction.Unload; };
app.InstanceStore = store;

app.Run();

finished.WaitOne();
```

代码下载 06_WorkflowApplication

加粗的行是相对于前一个示例新增的内容。你还会注意到，我们已在工作流应用程序上添加了 PersistableIdle 委托的事件处理程序。当工作流执行时，它会运行尽可能多的活动，直到没有更多工作可做为止。此时，它会转换到 Idle 状态，而空闲的工作流是持久化的候选对象。PersistableIdle 委托用于确定空闲工作流应发生什么。默认行为是无操作；然而，你也可以指定 PersistableIdleAction.Persist，这将复制工作流并将其存储在数据库中，但仍保留在内存中，或者你可以指定 PersistableIdleAction.Unload，这将持久化后卸载工作流。

还可以使用 Persist 活动请求工作流的持久化，事实上作为自定义活动编写者，如果你派生自 NativeActivity，也可以通过调用 NativeActivityContext 的 RequestPersist 方法来请求持久化。

我们现在遇到一个问题——我们有能力将工作流从内存中卸载并存储在持久化存储中，但迄今为止我们尚未描述如何从存储中检索它并使其再次执行。

## 书签

书签的传统用途是在书中标记一页，以便你可以从同一位置继续阅读。在工作流的上下文中，书签指定了你希望恢复运行该工作流的位置，书签通常在等待外部输入时使用。

在指定时间内到达。此工作流然后有多个执行周期，以及其他休眠且可从内存中卸载的时间。在被卸载之前，然而，有必要在工作流中定义一个可以恢复处理的位置，这就是书签的使用之处。

要定义书签，你需要一个派生自 NativeActivity 的自定义活动。然后你可以在 Execute 方法中创建书签，当书签被恢复时你的代码将继续执行。下面示例活动定义了一个简单的 Task 活动，该活动创建了一个书签，并在该书签点恢复时活动完成。

```csharp
public class Task : NativeActivity<Boolean>
{
    [RequiredArgument]
    public InArgument<string> TaskName { get; set; }

    protected override bool CanInduceIdle
    {
        get { return true; }
    }

    protected override void Execute(NativeActivityContext context)
    {
        context.CreateBookmark(TaskName.Get(context),
            new BookmarkCallback(OnTaskComplete));
    }

    private void OnTaskComplete(NativeActivityContext context,
        Bookmark bookmark, object state)
    {
        bool taskOK = Convert.ToBoolean(state);
        this.Result.Set(context, taskOK);
    }
}
```

代码下载 06_WorkflowApplication

对 CreateBookmark 的调用传递了书签的名称以及一个回调函数。当书签被恢复时，此回调将被执行。回调本身会传递一个任意对象，在本例中为 Boolean，因为我们决定每个任务都应报告成功或失败，然后我们可以使用它来决定工作流的下一步——它也可以是一个具有多个字段的复杂类型。

这就是活动的编写——我们现在需要修改托管代码以便在书签处恢复。但还有另一个问题——托管代码如何知道工作流创建了书签？如果恢复书签是主机的责任，它需要知道书签是否存在。

我们上面创建的 Task 真的需要做更多工作——通知外部世界任务已被创建。在生产系统中，这通常会导致在队列表中存储一个条目，并且该队列将作为任务列表呈现给呼叫中心员工。

与主机通信是下一节“扩展”的主题。

## 扩展

扩展只是一个添加到工作流应用程序运行时上下文中的类或接口。在 Workflow 3.x 中它们被称为 Services，然而这与 WCF Services 冲突，因此在 Workflow 4 中它们被重命名为扩展。

你通常会为扩展定义一个接口，然后提供该接口的运行时实现。你的活动只需调用该接口，这允许实现根据需要更改。一个很好的扩展示例是发送电子邮件。你可以创建一个 SendEmail
