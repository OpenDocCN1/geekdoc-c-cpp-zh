
开发人员只是接受 CLR 的默认策略。也就是说，当应用程序遇到未处理异常时，Windows 会向系统的事件日志写入一个条目。你可以通过打开“事件查看器”应用程序，然后在树中的 Windows 日志 > 应用程序节点下查看，如图 20-1 所示。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_481_0.png)

**图 20-1** Windows 事件日志显示了一个因未处理异常而终止的应用程序。

但是，你可以使用 Windows 操作中心小程序获取有关该问题的更有趣的详细信息。要启动操作中心，请单击系统托盘中的旗标图标，选择“打开操作中心”，展开“维护”框，然后选择“查看可靠性历史记录”链接。在这里，你可以在底部窗格中看到因未处理异常而终止的应用程序，如图 20-2 所示。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_482_0.png)

**图 20-2** 可靠性监视器显示了一个因未处理异常而终止的应用程序。

要查看有关已终止应用程序的更多详细信息，请在可靠性监视器中双击某个已终止的应用程序。详细信息将类似于图 20-3，问题签名的含义在表 20-2 中描述。托管应用程序产生的所有未处理异常都放在 CLR20r3 桶中。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_482_1.png)

**图 20-3** 可靠性监视器显示了有关失败应用程序的更多详细信息。

**表 20-2 问题签名**

| 问题签名 | 描述* |
|---|---|
| 01 | EXE 文件名（32 字符限制） |
| 02 | EXE 文件的程序集版本号 |
| 03 | EXE 文件的时间戳 |
| 04 | EXE 文件的完整程序集名称（64 字符限制） |
| 05 | 出错程序集的版本 |
| 06 | 出错程序集的时间戳 |
| 07 | 出错程序集的类型和方法。此值是 MethodDef 元数据标记（去掉 0x06 高字节后），用于标识引发异常的方法。根据此值，你可以使用 ILDasm.exe 确定有问题的类型和方法。 |
| 08 | 出错方法的 IL 指令。此值是引发异常的 IL 指令在出错方法内的偏移量。根据此值，你可以使用 ILDasm.exe 确定有问题的指令。 |
| 09 | 引发的异常类型（32 字符限制） |

\* 如果字符串超出允许限制，则会执行一些智能截断，例如从异常类型中删除“Exception”，或从文件名中删除“.dll”。如果结果字符串仍然太长，则 CLR 会通过对字符串进行哈希或 base-64 编码来创建一个值。

记录有关失败应用程序的信息后，Windows 会显示一个消息框，允许最终用户将有关失败应用程序的信息发送到 Microsoft 服务器。¹⁷ 这称为 *Windows 错误报告*，有关它的更多信息可在 Windows 质量网站（*http://WinQual.Microsoft.com*）上找到。

公司可以选择向 Microsoft 注册，以查看有关其自己的应用程序和组件的信息。注册是免费的，但要求你的程序集使用 VeriSign ID（也称为用于 Authenticode 的软件发行者数字 ID）进行签名。

当然，你也可以开发自己的系统来将未处理异常信息返回给你，以便修复代码中的 bug。当应用程序初始化时，你可以告知 CLR：你有一个方法，希望在应用程序中的任何线程遇到未处理异常时调用它。

不幸的是，Microsoft 生成的每种应用程序模型都有自己接入未处理异常的方式。你需要在 FCL 文档中查找的成员包括：

- 对于任何应用程序，请查看 `System.AppDomain’s UnhandledException` 事件。Silverlight 应用程序执行时的安全级别不足以注册此事件。
- 对于 Windows Forms 应用程序，请查看 System.Windows.Forms.NativeWindow 的 OnThreadException 虚方法、System.Windows.Forms.Application 的 OnThreadException 虚方法，以及 System.Windows.Forms.Application 的 ThreadException 事件。
- 对于 Windows Presentation Foundation (WPF) 应用程序，请查看 System.Windows.Application 的 DispatcherUnhandledException 事件，以及 System.Threading.Dispatcher 的 UnhandledException 和 UnhandledExceptionFilter 事件。
- 对于 Silverlight，请查看 System.Windows.Application 的 UnhandledException 事件。
- 对于 ASP.NET Web Form 应用程序，请查看 System.Web.UI.TemplateControl 的 Error 事件。TemplateControl 是 System.Web.UI.Page 和 System.Web.UI.UserControl 类的基类。此外，你还应查看 System.Web.HttpApplication 的 Error 事件。
- 对于 Windows Communication Foundation 应用程序，请查看 System.ServiceModel.Dispatcher.ChannelDispatcher 的 ErrorHandlers 属性。

¹⁷ 实际上，你可以通过使用 P/Invoke 调用 Win32 的 `SetErrorMode` 函数并传入 `SEM_NOGPFAULTERRORBOX` 来禁用此消息框。

在结束本节之前，我想谈谈可能在分布式应用程序（如网站或 Web 服务）中发生的未处理异常。在理想情况下，遇到未处理异常的服务器应用程序应记录该异常，向客户端发送某种通知，表明请求的操作无法完成，然后服务器应终止。不幸的是，我们并非生活在理想世界中，因此可能无法向客户端发送失败通知。对于某些无状态服务器（如 Microsoft SQL Server），终止服务器并启动一个全新实例可能并不实际。

对于服务器应用程序，不应将有关未处理异常的信息返回给客户端，因为客户端对此几乎无能为力，尤其是在客户端由其他公司实现时。此外，服务器应尽可能少地向客户端泄露有关自身的信息，以降低服务器被黑客攻击的可能性。

**注意** CLR 将本机代码引发的一些异常视为损坏状态异常（CSE），因为它们通常是 CLR 本身或某些本机代码中的 bug 导致的结果，而托管开发人员无法控制这些本机代码。默认情况下，CLR 不允许托管代码捕获这些异常，并且 finally 块不会执行。以下是被视为 CSE 的本机 Win32 异常列表：

```
EXCEPTION_ACCESS_VIOLATION          EXCEPTION_STACK_OVERFLOW
EXCEPTION_ILLEGAL_INSTRUCTION       EXCEPTION_IN_PAGE_ERROR
EXCEPTION_INVALID_DISPOSITION       EXCEPTION_NONCONTINUABLE_EXCEPTION
EXCEPTION_PRIV_INSTRUCTION          STATUS_UNWIND_CONSOLIDATE
```

单个托管方法可以通过将 System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute 应用于该方法，来重写默认行为并捕获这些异常。此外，该方法还必须应用 System.Security.SecurityCriticalAttribute。你还可以通过将应用程序的可扩展标记语言 (XML) 配置文件中的 `legacyCorruptedStateExceptionPolicy` 元素设置为 true，来重写整个进程的默认行为。CLR 会将其中大多数异常转换为 `System.Runtime.InteropServices.SEHException` 对象，但 `EXCEPTION_ACCESS_VIOLATION` 会转换为 `System.AccessViolationException` 对象，而 `EXCEPTION_STACK_OVERFLOW` 会转换为 `System.StackOverflowException` 对象。

**注意** 在调用方法之前，你可以通过调用 `RuntimeHelpers.EnsureSufficientExecutionStack` 方法来检查是否有充足的堆栈空间。此方法检查调用线程是否有足够的可用堆栈空间来执行普通方法（该术语并未明确定义）。如果堆栈空间不足，此方法会抛出 `InsufficientExecutionStackException`，你可以捕获它。`EnsureSufficientExecutionStack` 方法不接受参数并返回 void。此方法通常由递归方法使用。

### 调试异常

Visual Studio 调试器为异常提供特殊支持。打开解决方案后，从“调试”菜单中选择“异常”，你将看到如图 20-4 所示的对话框。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_485_0.png)

**图 20-4** “异常”对话框，显示了不同类型的异常。

此对话框显示了 Visual Studio 已知的不同类型的异常。对于公共语言运行时异常，在对话框中展开相应分支（如图 20-5 所示），会显示 Visual Studio 调试器已知的命名空间集。
