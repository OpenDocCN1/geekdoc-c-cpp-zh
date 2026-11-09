
你的代码可能试图捕获它并从中恢复，但你甚至不知道自己正在调用类型构造函数。因此，CLR 将 DivideByZeroException 转换为 TypeInitializationException，以便你清楚地知道异常是由于类型构造函数失败而发生的；问题并不出在你的代码中。

另一方面，这里有一个使用该技术的糟糕示例：当你通过反射调用方法时，CLR 会包装该方法抛出的每个异常，并将其转换为 TargetInvocationException。这非常烦人，因为你现在必须捕获 TargetInvocationException 对象，并查看其 InnerException 属性，才能辨别失败的真正原因。事实上，在使用反射时，经常会看到类似下面这样的代码。

```csharp
private static void Reflection(Object o) {
    try {
        // Invoke a DoSomething method on this object
        var mi = o.GetType().GetMethod("DoSomething");
        mi.Invoke(o, null); // The DoSomething method might throw an exception
    }
    catch (System.Reflection.TargetInvocationException e) {
        // The CLR converts reflection-produced exceptions to TargetInvocationException
        throw e.InnerException; // Re-throw what was originally thrown
    }
}
```

不过我有个好消息：如果你使用 C# 的 dynamic 基元类型（在第 5 章“基元类型、引用类型和值类型”中讨论）来调用成员，编译器生成的代码不会捕获任何异常并抛出 TargetInvocationException 对象；原始抛出的异常对象只会沿调用栈向上传播。对许多开发者来说，这是更倾向于使用 C# 的 dynamic 基元类型而不是反射的一个很好的理由。

## 未处理异常

当抛出异常时，CLR 会沿调用栈向上查找与所抛异常对象类型匹配的 catch 块。如果没有 catch 块与抛出的异常类型匹配，就会发生未处理异常。当 CLR 检测到进程中的任何线程发生了未处理异常时，CLR 会终止该进程。未处理异常表示应用程序未预料到的情况，被视为应用程序中的真正 bug。此时，应将该 bug 报告给发布该应用程序的公司。希望发布者会修复该 bug 并分发应用程序的新版本。

类库开发者甚至不应该考虑未处理异常。只有应用程序开发者需要关注未处理异常，并且应用程序应该制定处理未处理异常的策略。Microsoft 实际上建议应用程序开发者直接接受 CLR 的默认策略。也就是说，当应用程序发生未处理异常时，Windows 会向系统事件日志写入一个条目。你可以打开事件查看器应用程序，然后在树中的“Windows 日志 ➞ 应用程序”节点下查看该条目，如图 20-1 所示。

![](img/857bdf6cef9e242b53a37f88df9a1287_511_0.png)

**图 20-1** Windows 事件日志显示一个因未处理异常而终止的应用程序。

不过，你可以使用 Windows 可靠性监视器小程序获取有关该问题的更有趣的详细信息。要启动可靠性监视器，请打开 Windows 控制面板并搜索“可靠性历史记录”。在这里，你可以在底部窗格中看到因未处理异常而终止的应用程序，如图 20-2 所示。

![](img/857bdf6cef9e242b53a37f88df9a1287_511_1.png)

**图 20-2** 可靠性监视器显示一个因未处理异常而终止的应用程序。

要查看有关已终止应用程序的更多详细信息，请在可靠性监视器中双击已终止的应用程序。详细信息将类似于图 20-3，问题签名的含义在表 20-2 中描述。托管应用程序产生的所有未处理异常都放在 CLR20r3 存储桶中。

![](img/857bdf6cef9e242b53a37f88df9a1287_512_0.png)

**图 20-3** 可靠性监视器显示有关失败应用程序的更多详细信息。

### 表 20-2 问题签名

| 问题签名 | 描述* |
|---|---|
| 01 | EXE 文件的名称（32 个字符限制） |
| 02 | EXE 文件的程序集版本号 |
| 03 | EXE 文件的时间戳 |
| 04 | EXE 文件的完整程序集名称（64 个字符限制） |
| 05 | 出错程序集的版本 |
| 06 | 出错程序集的时间戳 |
| 07 | 出错程序集的类型和方法。该值是一个 MethodDef 元数据标记（去掉 0x06 高字节后），用于标识抛出异常的方法。通过该值，你可以使用 ILDasm.exe 确定有问题的类型和方法。 |
| 08 | 出错方法的 IL 指令。该值是抛出异常的 IL 指令在出错方法内的偏移量。通过该值，你可以使用 ILDasm.exe 确定有问题的指令。 |
| 09 | 抛出的异常类型（32 个字符限制） |

* 如果字符串超出允许限制，则会执行一些智能截断，例如从异常类型中删除“Exception”或从文件名中删除“.dll”。如果结果字符串仍然过长，则 CLR 会通过哈希或 base-64 编码该字符串来创建一个值。

记录有关失败应用程序的信息后，Windows 会显示一个消息框，允许最终用户将有关失败应用程序的信息发送到 Microsoft 服务器。⁷ 这称为 *Windows 错误报告*，有关它的更多信息可在 Windows Quality 网站（http://WinQual.Microsoft.com）上找到。

公司可以选择与 Microsoft 签约，以查看有关其自身应用程序和组件的此信息。注册是免费的，但它确实要求你的程序集使用 VeriSign ID（也称为用于 Authenticode 的软件发布者数字 ID）进行签名。

当然，你也可以开发自己的系统，将未处理异常信息反馈给你，以便你修复代码中的 bug。当应用程序初始化时，你可以通知 CLR：你有一个方法，希望在应用程序中的任何线程发生未处理异常时调用它。

不幸的是，Microsoft 产生的每种应用程序模型都有自己接入未处理异常的方式。你需要在 FCL 文档中查找的成员包括：

- 对于许多应用程序，请查看 `System.AppDomain` 的 `UnhandledException` 事件。Windows 应用商店应用程序和 Microsoft Silverlight 应用程序无法访问此事件。
- 对于 Windows 应用商店应用，请查看 `Windows.UI.Xaml.Application` 的 `UnhandledException` 事件。
- 对于 Windows Forms 应用程序，请查看 `System.Windows.Forms.NativeWindow` 的 `OnThreadException` 虚方法、`System.Windows.Forms.Application` 的 `OnThreadException` 虚方法，以及 `System.Windows.Forms.Application` 的 `ThreadException` 事件。
- 对于 Windows Presentation Foundation (WPF) 应用程序，请查看 `System.Windows.Application` 的 `DispatcherUnhandledException` 事件，以及 `System.Windows.Threading.Dispatcher` 的 `UnhandledException` 和 `UnhandledExceptionFilter` 事件。
- 对于 Silverlight，请查看 `System.Windows.Application` 的 `UnhandledException` 事件。
- 对于 ASP.NET Web Form 应用程序，请查看 `System.Web.UI.TemplateControl` 的 `Error` 事件。`TemplateControl` 是 `System.Web.UI.Page` 和 `System.Web.UI.UserControl` 类的基类。此外，还应查看 `System.Web.HttpApplication` 的 `Error` 事件。
- 对于 Windows Communication Foundation 应用程序，请查看 `System.ServiceModel.Dispatcher.ChannelDispatcher` 的 `ErrorHandlers` 属性。

在结束本节之前，我想谈一谈分布式应用程序（如网站或 Web 服务）中可能发生的未处理异常。在理想情况下，遇到未处理异常的服务器应用程序应记录该异常，并向……

⁷ 实际上，你可以通过使用 P/Invoke 调用 Win32 的 `SetErrorMode` 函数，并传入 `SEM_NOGPFAULTERRORBOX` 来禁用此消息框。
