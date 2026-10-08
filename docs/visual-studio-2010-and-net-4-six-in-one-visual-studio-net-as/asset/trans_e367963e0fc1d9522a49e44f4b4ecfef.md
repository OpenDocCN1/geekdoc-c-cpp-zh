

# 列表 11-5：Program.cs (CodedHelloWorkflow)

```csharp
new WriteLine { Text = "The workflow has finished",
new Assign<string>
{
    To = new Argument<string>(ctx) => Result.Get(ctx),
    Value = new InArgument<string>(ctx) => temp.Get(ctx)
}
};
```

代码文件 [Program.cs] 可以在 Wrox.com 下载。

当你运行此应用程序时，你会发现它产生的输出与 HelloWorkflow 相似。当你查看 `Main` 方法时，你可以看到在这里通过 `Invoke` 方法实例化了一个名为 `HelloWorkflow` 的内部工作流类。输入参数被传递，而输出参数的提取方式与图形化设计的工作流完全相同。

这可能会让你感到意外，但工作流本身就是一个活动——也就是说 `HelloWorkflow` 继承自 `Activity` 类：

```csharp
internal class HelloWorkflow : Activity
{
    // ...
}
```

假设要执行的活动是以声明式定义的。查看该类的构造函数：

```csharp
public HelloWorkflow()
{
    var temp = new Variable<string>("temp");
    Implementation = () =>
        new Sequence
        // ...
}
```

`Implementation` 属性的类型为 `Func<Activity>`，在这里使用的 Lambda 表达式声明了包含所有嵌套活动的 `Sequence` 活动。因为它仅仅是一个声明，所以创建此 Lambda 表达式是一个低开销的操作。当工作流即将执行时，将调用 `Implementation` 后面的 Lambda 表达式表示的方法。

# 声明工作流参数

工作流参数被声明为简单的读写属性：

```csharp
public InArgument<String> Message { get; set; }
OutArgument<String> Result { get; set; }
```

显然，泛型类型 `InArgument<>` 和 `OutArgument<>` 分别定义了输入和输出参数。类型参数告诉我们参数的类型——在这种情况下，两者都是字符串。当你运行工作流时，`HelloWorkflow` 类被实例化，并通过传递给 `Invoke` 方法的字典中的名称将参数匹配到相应的属性。

> 尝试在 `Main` 方法中传递错误的参数名称——例如使用 `Msg` 而不是 `Message`。你将收到一个 `System.ArgumentException` 异常，错误信息为：“The values for the root activity's arguments do not satisfy the root activity's requirements.”

# 声明变量

`HelloWorkflow` 构造函数定义了作为工作流变量使用的局部变量 `temp`：

```csharp
var temp = new Variable<string>("temp");
```

尽管它包含了数据，但它并没有声明为原生字符串变量，而是 `Variable<string>`。这里使用的 "temp" 参数是变量名称。你可能会好奇为什么不使用原生变量。原因是工作流实例在空闲时（例如，等待输入）可以被持久化到存储器中。在这种情况下，它们的状态由变量表示。不详细说明，这种持久化要求工作流变量必须是可以引用的。`Variable` 泛型类型提供了这一需求。.NET 反射没有提供检索方法本地变量信息的方法，因此传递给参数的 "temp" 名称有助于工作流运行时管理变量的区分。

# 构建活动

`Sequence` 活动的定义如下：

```csharp
new Sequence
{
    DisplayName = "Hello Workflow",
    Variables = { temp },
    Activities = {
        // ...
    }
}
```

`DisplayName` 属性是在使用工作流设计器时可以在属性窗口中设置的。`Variables` 容器包含了 `Variable<>` 实例，这些实例被视为工作流实例的状态。`Activities` 容器列出了 `Sequence` 的嵌套活动，并按照列出的顺序执行。

# 使用表达式

`WriteLine` 和 `Assign` 的属性是表达式中使用参数和变量的很好的表示。你可以看到使用工作流参数和变量的 `Get` 方法的如下奇怪构造：

```csharp
To = new OutArgument<String>(temp)
//...
Value = new InArgument<string>(ctx) => "Message: " + Message.Get(ctx)
//...
Text = new InArgument<string>(ctx) => temp.Get(ctx)
```

要从 `Variable` 实例获取实际数据，必须使用 `Get` 方法。工作流本身不存储任何数据元素；你必须从具体工作流实例的上下获取数据。这就是为什么早期片段中的 Lambda 表达式是有意义的 `ctx` 表达式参数是 `ActivityContext` 类的实例。你必须将上下文传递给变量的 `Get` 方法以提取其值。

`Activity` 类的属性实际上是工作流参数，可以用 `InArgument<T>` 或 `OutArgument<T>` 实例表示。`WriteLine` 的 `Text` 属性和 `Assign` 的 `Value` 属性是输入参数，而 `Assign` 的 `To` 属性是输出参数。

确保将整个表达式放入 `InArgument` 或 `OutArgument` 的构造函数中。如果你写成：

```csharp
Value = "Message: " + new InArgument<string>(ctx) => Message.Get(ctx)
```

而不是

```csharp
Value = new InArgument<string>(ctx) => "Message: " + Message.Get(ctx)
```

输出将是：

```text
Message: System.Activities.InArgument`1[System.String]
```

而不是

```text
Message: Hello from WF 4.0
```

# 工作流架构

到此时，你已经看到了使用工作流设计器创建工作流的几个示例，并且学习了你可以定义仅代码的工作流。还提到了几个概念，例如工作流实例、活动、变量等。本节提供了工作流架构的概述，以便你理解这些概念是如何运作。

![11-13: Overview of workflow](https://example.com/1113.png)

# 工作流实例与主机

`System.Activity` 命名空间中的类是工作流架构的核心元素。WorkflowApplication 被实例化、设置并启动工作流实例。WorkflowApplication 负责在工作流处于空闲时从内存中卸载并恢复它。

在工作流的生命周期期间，主机可以：

字体 向工作流传递输入参数，并从工作流检索输出参数。早期的示例展示了这一点。
- 主机可以访问工作流的扩展（你稍后将学习该概念）。
- 工作流产生事件（例如，当启动、空闲或完成时）。主机可以响应这些事件。例如，当工作流完成时，它可以通知用户或清理资源。
- 工作流在等待用户时进入空闲状态（例如，用户必须做决定）。当预期的交互完成后（例如，用户做了决定），主机可以恢复工作流。这种机制通过书签来指定恢复点并传递数据（例如，用户的决策到工作流）。
- 工作流有机会访问主机服务。

尽管可能有多个工作流实例同时执行（例如，每个请求一个实例），但它们之间不相互交互。工作流内部没有与其他实例通信的机制，实例也不知道其他实例的存在。

