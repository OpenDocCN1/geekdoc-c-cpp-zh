
最后，如果既未引发 `Approved` 事件也未引发 `Rejected` 事件，`DelayActivity` 最终会在其延迟到期后完成，然后费用报告可能会被路由到另一位经理——可能在 Active Directory 中查找该人员。在示例中，当执行 `RequestApproval` 活动时，会向用户显示一个对话框，因此如果延迟执行，则还需关闭该对话框，这正是图 57-6 中名为 `HideDialog` 的活动的用途。

此示例的代码可在 `02 Listen` 目录中找到。示例中使用的一些概念尚未介绍——例如如何识别工作流实例，以及如何将事件重新发送到工作流运行时并最终传递给正确的工作流实例。这些概念在标题为“Workflows”的章节中介绍。

## 活动执行模型

到目前为止，本章仅讨论了运行时通过调用 `Execute` 方法来执行活动。然而，活动在执行过程中可能会经历多个状态——这些状态在图 57-7 中呈现。

![](img/d7d2ffa0a76feaab821930e95daace93_1822_0.png)

FIGURE 57-7

活动首先由 `WorkflowRuntime` 初始化，当运行时调用活动的 `Initialize` 方法时。 该方法会传入一个 `IServiceProvider` 实例，该实例映射到运行时中可用的服务。 这些服务将在本章后面的“Workflow Services”部分讨论。大多数活动在此方法中不执行任何操作，但该方法可供您进行必要的设置。

运行时随后调用 `Execute` 方法，活动可以返回 `ActivityExecutionStatus` 枚举中的任意一个值。通常，您会从 `Execute` 方法返回 `Closed`，这表示您的活动已完成处理；然而，如果您返回其他状态值之一，运行时将据此确定活动的当前状态。

您可从此方法返回 `Executing` 以告知运行时您还有额外工作要做——典型的例子是当您有一个需要执行其子活动的复合活动时。在这种情况下，您的活动可以为每个子活动安排执行，然后在所有子活动完成后才通知运行时活动已完成。

## 自定义活动

到目前为止，您使用的是在 `System.Workflow.Activities` 命名空间中定义的活动。在本节中，您将学习如何创建自定义活动并扩展这些活动，以在设计时和运行时都提供良好的用户体验。

首先，您创建一个 `WriteLineActivity`，可用于向控制台输出一行文本。虽然这是一个简单的示例，但它将被扩展以展示自定义

在此方法中，首先验证传入的参数，然后调用基类的 Validate 方法以获取 ValidationErrorCollection。虽然这里并非严格必要，但如果您是从具有多个也需要验证的属性的活动派生而来，调用基类方法将确保这些属性也被检查。

然后代码将传入的 obj 参数强制转换为 WriteLineActivity 实例，并检查活动是否具有父级。此测试是必要的，因为 Validate 函数在活动编译期间被调用（如果活动位于工作流项目或活动库中），此时尚未定义父活动。没有此检查，您实际上无法构建包含活动和验证器的程序集。如果项目类型为类库，则不需要此额外步骤。

最后一步是检查 Message 属性是否已设置为非空字符串的值。这使用了 ValidationError 类的静态方法，该方法构造一个错误，指定该属性未定义。

要为您的 WriteLineActivity 添加验证支持，最后一步是将 ActivityValidation 属性添加到活动中，如以下代码段所示：

```
```csharp
[ActivityValidator(typeof(WriteLineValidator))]
public class WriteLineActivity: Activity
{
}
```
```

如果您编译应用程序然后将 WriteLineActivity 拖放到工作流上，您应该会看到验证错误，如图 57-9 所示；单击此错误将带您进入属性网格中的该属性。

如果您为 Message 属性输入一些文本，验证错误将被移除，然后您可以编译并运行应用程序。

现在您已完成活动验证，下一步是更改活动的渲染行为以添加填充颜色。为此，您需要同时定义 ActivityDesigner 类和 ActivityDesignerTheme 类，如下一节所述。

![](img/d7d2ffa0a76feaab821930e95daace93_1825_0.png)

## 主题和设计器

活动的屏幕渲染是通过使用 ActivityDesigner 类完成的，并且也可以使用 ActivityDesignerTheme。

主题类用于在 Workflow Designer 中对活动的渲染行为进行简单更改：

```
```csharp
public class WriteLineTheme: ActivityDesignerTheme
{
    /// <summary>
    /// Construct the theme and set some defaults
    /// </summary>
    /// <param name="theme">...</param>
    public WriteLineTheme(WorkflowTheme theme)
        : base(theme)
    {
        this.BackColorStart = Color.Yellow;
        this.BackColorEnd = Color.Orange;
        this.BackgroundStyle = LinearGradientMode.ForwardDiagonal;
    }
}
```
```

主题派生自 ActivityDesignerTheme，后者具有一个接收 WorkflowTheme 参数的构造函数。在构造函数内部，设置活动的起始和结束颜色，然后定义一个线性渐变画刷，该画刷在绘制背景时使用。

一旦您添加了图像文件并将其生成操作设置为 Embedded Resource，您就可以按以下代码段所示为活动添加属性：

```
[ActivityValidator(typeof(WriteLineValidator))]
[Designer(typeof(WriteLineDesigner))]
[ToolboxBitmap(typeof(WriteLineActivity), "Resources.WriteLine.png")]
public class WriteLineActivity: Activity
{
  .
}
```

ToolboxBitmap 属性定义了多个构造函数，这里使用的是一个接受活动程序集中定义的类型的构造函数以及资源名称。当您将资源添加到文件夹时，其名称由程序集的命名空间和图像所在文件夹的名称构造而成——因此此处资源的完全限定名称为 CustomActivities.Resources.WriteLine.png。 与 ToolboxBitmap 属性一起使用的构造函数会将类型参数所在的命名空间附加到作为第二个参数传递的字符串上，因此在 Visual Studio 加载时它将解析为适当的资源。

您需要创建的最后一个类派生自 ActivityToolboxItem。当活动加载到 Visual Studio 工具箱时使用此类。此类的典型用途是更改工具箱上活动的显示名称——所有内置活动的名称都已更改，以从类型中移除“Activity”一词。在您的类中，您可以通过将 DisplayName 属性设置为“WriteLine”来实现同样的效果。

```
[Serializable]
public class WriteLineToolboxItem: ActivityToolboxItem
{
    /// <summary>
    /// Set the display name to WriteLine - i.e. trim off
    /// the 'Activity' string
    /// </summary>
    /// <param name="t"></param>
    public WriteLineToolboxItem(Type t)
        : base(t)
    {
        base.DisplayName = "WriteLine";
    }

    /// <summary>
    /// Necessary for the Visual Studio design time environment
    /// </summary>
    /// <param name="info"></param>
    /// <param name="context"></param>
    private WriteLineToolboxItem(SerializationInfo info,
        StreamingContext context)
    {
        this.Deserialize(info, context);
    }
}
```

该类派生自 ActivityToolboxItem 并重写构造函数以更改显示名称；它还提供了一个序列化构造函数，当项目加载到工具箱时工具箱会使用它。如果没有此构造函数，您在尝试将活动添加到工具箱时将收到错误。请注意，该类也标记为 [Serializable]。

工具箱项是通过使用 ToolboxItem 属性添加到活动中的，如下所示：

```
[ActivityValidator(typeof(WriteLineValidator))]
[Designer(typeof(WriteLineDesigner))]
[ToolboxBitmap(typeof(WriteLineActivity), "Resources.WriteLine.png")]
[ToolboxItem(typeof(WriteLineToolboxItem))]
public class WriteLineActivity: Activity
{
  .
}
```
