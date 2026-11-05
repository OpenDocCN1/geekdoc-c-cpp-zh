
你确实可以调用通过反射找到的在程序集中定义的类型和成员。下面的清单是动态加载程序集并通过反射调用静态方法的一个示例。

第一条语句定义了框架定义的 System.Windows.Forms.dll 程序集的常量路径。第二条语句使用 Assembly.LoadFrom 方法加载程序集——清单 2-1 提供了另一个示例。第三条检索 MessageBox 类的元数据类型，最后一条语句调用 MessageBox 类中的一个成员。第一个参数是要引用的成员的名称。第三个参数将三个绑定标志进行 OR 操作，表示 Show 是一个需要调用的 Public、Static 方法。第一个 null 参数可以用一个描述如何绑定方法的类来替换，第二个 null 是调用该方法所需类型的实例。例如，如果 Show 是一个非静态方法，那么我们就需要创建 MessageBox 类的一个实例并将其作为此参数值传递。最后一个参数是要传递给被调用方法的参数数组。

Reflection 赋予的强大功能不仅仅是发现程序集包含什么内容。你确实可以调用通过反射找到的在程序集中定义的类型和成员。下面的清单是动态加载程序集并通过反射调用静态方法的一个示例。

第一条语句定义了框架定义的 System.Windows.Forms.dll 程序集的常量路径。第二条语句使用 Assembly.LoadFrom 方法加载程序集——清单 2-1 提供了另一个示例。第三条检索 MessageBox 类的元数据类型，最后一条语句调用 MessageBox 类中的一个成员。第一个参数是要引用的成员的名称。第三个参数将三个绑定标志进行 OR 操作，表示 Show 是一个需要调用的 Public、Static 方法。第一个 null 参数可以用一个描述如何绑定方法的类来替换，第二个 null 是调用该方法所需类型的实例。例如，如果 Show 是一个非静态方法，那么我们就需要创建 MessageBox 类的一个实例并将其作为此参数值传递。最后一个参数是要传递给被调用方法的参数数组。

## Broadcasting Operations
清单 2-1 包含一个声明 Broadcaster.Broadcast。这是我定义的一个方法，用于将内部数据发送到单个位置，允许需要了解正在发生什么的监听者调谐到广播器。例如，我们可以将主窗体指定为监听者并在主窗体上显示任务的状态。AssemblyViewer 正是这样做的；主窗体有一个状态栏，用于显示 AssemblyManager 在加载操作期间的进度。

class that implements IListener and registers with the Broadcaster is capable of accepting string data sent to the Broadcaster. The class and the interface demonstrate a couple of interesting mechanisms, so we will look at each.

### Implementing the Broadcaster
Broadcaster 演示了 Singleton 模式。Singleton 是一个你需要确保只有一个实例的类。通常，此实例用于表示单个资源的存在，例如一台打印机。通过将构造函数设为 sealed 或 private 并仅通过静态成员提供访问，可以创建 Singleton 类。Broadcaster 通过内部、私有的 Instance 属性来实现这一点。

Broadcaster 中的每个公共方法都是静态的。当你在 Broadcaster（或任何 Singleton）中调用公共成员时，该方法引用只读的 Instance 属性。代码会验证 Broadcaster 的单个实例是否已被创建。如果 Singleton 不存在，则会创建一个实例并将其分配给私有字段 instance。然后返回 Singleton 对象。结果是 Broadcaster 包含对自身实例的引用。

如果你将一个 IListener 添加到 listeners 的 ArrayList 中，那么每次调用静态方法 Broadcast 时，所有

正在监听的监听者都将收到字符串消息。此过程可用于显示内部状态信息、写入日志文件、跟踪你的分布式应用程序，或执行这些任务的组合。（建议你使用与 Broadcaster 惯用法相关的 Debug 和 Trace 监听器。）另外，请注意 IEnumerator 用于遍历 listeners 的 ArrayList。

## Defining the Interface
IListener 接口定义了两个方法：Listening 和 Listen。Listening 是一个返回 Boolean 的函数，表示实现 IListener 接口的对象是否希望接收消息。这使得对象可以在不从 Broadcaster 注销的情况下 figuratively 堵住耳朵。Listen 方法是在监听时接收字符串消息的方法。

你可以通过实现 IListener 接口来使用 Broadcaster。FormMain 类实现 IListener 以在状态栏中显示广播消息。在主窗体的情况下，你可以在 Form 的 Load 中将窗体添加到监听者列表中。另一个将控件添加到监听者列表的好地方是在类的构造函数中。考虑实现 IDisposable 和 Dispose，以便在对象被释放时将其从 Broadcaster 的监听者列表中移除。

以下代码片段显示了你在实现 IListener 接口并从 Broadcaster 接收消息的类中可能遇到的部分内容。

## Using RichTextBox References
Using RichTextBox rich Text 是一种标记语言。称为 Rich Text Format，或 RTF，Rich Text 支持描述文本格式的嵌入式标签。RichTextBox 类似于 TextBox，但支持嵌入式 RTF 格式。RichTextBox 的主要作用是显示格式化的文本，然而 RichTextBox 可以显示纯文本，并且具有内置功能，可帮助将文本属性的内容加载和保存到文件中。

Placing Text in the RichTextBox 文本可以是纯文本或 Rich Text。要自动将字符串数据分配给 RichTextBox 控件，分配一个字符串

value of the Text property can be used to open IE, for instance.

Process 类定义在 System.Diagnostics 命名空间中，Start 是一个静态方法。Process 类对于启动、停止、控制和监视应用程序非常有用。在此模型中，http://moniker 指示 Process.Start 启动 Internet Explorer 的另一个实例，给定 URL 与 Internet Explorer 之间的关联。

## Basic Printing And Multithreading
Crystal Reports 是 Seagate Software 的热门产品，现在是 Crystal Decisions。对于高级打印和报告，你可以将基于 Crystal Decisions 的控件合并到你的应用程序中，然而基本打印由 PrintDocument 控件支持。

要实现基本打印，请向你的应用程序添加一个 PrintDocument 控件并调用 Print 方法。当你调用 PrintDocument.Print 时，会触发 PrintPage 事件。PrintPage 会传递一个 PrintPageEventArgs 我们实际更新 Opacity 值的方式是通过调用窗体的 Invoke 方法。Invoke 是线程安全的；Invoke 将委托代码 marshaling 到调用对象所在的同一线程。（再次强调，没有委托，线程安全线程是不可能的。）

Invoke 需要一个 MethodInvoker 委托并执行用于调用委托的方法内部的代码。Increment 方法更新 Opacity 值。done 字段用于指示窗体是否隐藏。我们在更新它时锁定 Done 方法，防止运行 Show 的线程在 Done 值被更新之前检查 Done 值。

最后，Show 使用 try-finally 结构来捕获异常并关闭窗体。例如，如果用户在 Splash 窗体完全不透明之前关闭了应用程序，Show 将引用一个已释放的窗体（这是在清单 2-3 中的第 17 行）并引发异常。异常处理程序响应立即应用程序关闭。

object that contains a Graphics object representing the Device Context (DC) of the
