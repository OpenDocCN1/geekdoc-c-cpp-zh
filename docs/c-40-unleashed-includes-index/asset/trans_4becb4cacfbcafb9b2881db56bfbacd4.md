
// Code goes here

Debug.WriteLine("Bar - End");
Debug.Unindent();
}
```

调试器输出可以发送给多个侦听器，称为跟踪侦听器，它们只是派生自 System.Diagnostics 中的 TraceListener 类的对象。用于发出调试器输出的代码可以保留在原位，但其底层的跟踪侦听器可以替换为其他侦听器（例如，在预生产环境中）。这样做可以获得一种简单机制，在出现问题时分析代码正在做什么，而无需甚至附加调试器。这可以通过使用配置文件来实现，如下所示；更多信息可在 MSDN 上找到：

```
<configuration>
  <system.diagnostics>
    <trace autoflush="false" indentSize="4">
      <listeners>
        <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
        <remove name="Default" />
      </listeners>
    </trace>
  </system.diagnostics>
</configuration>
```

最后，Debug.Fail 方法与通过调用 Debug.Assert(false) 触发的失败断言基本相同，但它还会向跟踪侦听器打印一条消息——包括失败点的堆栈跟踪。对于所有这些诊断调试器输出日志机制，请记住它们的条件编译特性。如果需要提供在生产环境中可用的诊断信息，其他机制（例如直接使用 Windows 事件日志）会很有帮助。我们将在本章后面的“使用事件日志”部分讨论它们。

## 控制调试器

除了 Debug 类之外，System.Diagnostics 命名空间还有一个 Debugger 类，其静态方法用于控制调试器。可以说，它最有用的方法就是 Break，它会导致代码在调用点在调试器中中断。这种功能通常用于调试程序的启动路径，在这种情况下，事先附加调试器相当不方便。例如，其他某个进程可能会在不给你附加调试器的机会的情况下启动你的程序。

### 映像文件执行选项

事实上，调试启动路径的问题自 Windows 早期的日子就存在了。但这并不是真正的问题。用于在 Windows 上运行可执行文件的加载程序的设计者预见到了这个问题（或很可能自己多次遇到过这种困难）。

为了使此类调试器场景更具吸引力，他们加入了一个名为映像文件执行选项的大型 hack，这是一个基于注册表的设置，可以按程序指定。你可以在注册表的本地计算机配置单元下的 HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options 找到它。每个可执行文件的进程创建应受加载程序应用的调整影响的可执行文件都有一个指定此类选项的子项。例如，影响 notepad.exe 可执行映像进程创建的设置位于名为 notepad.exe 的子项下。

Debugger 设置使你能够使加载程序启动指定的程序而不是原始可执行文件。原始可执行文件的路径作为第一个命令行参数传递给“调试器”可执行文件。这样就可以配置调试器来拦截为给定可执行文件创建的任何进程。

Break 的使用示例如下所示：

```
static void Main()
{
    Debugger.Break();
    // More code goes here...
}
```

代码的行为取决于是否附加了调试器。如果是这样，我们对 Break 的调用只会导致我们在调用所在的行进入调试器。如果尚未附加调试器，则会显示一个对话框，如图 27.6 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1403_0.png)

图 27.6 未附加调试器时调用 Debugger.Break 的结果。

根据机器的配置（即是否已设置调试器），对话框的外观会有所不同。无论如何，你现在可以向触发了 Break 调用的进程附加调试器，这样做会让你直接进入发出 Break 调用的那一行。从那时起，可以分析状态，如果需要，可以恢复执行。

与 Debug 类的方法的一个关键区别在于，Debugger 方法不是条件编译的。换句话说，像 Debugger.Break 这样的东西也会导致“发布”二进制文件在调用点中断。

### 调试器依赖行为的情况

有些人喜欢使用 Debugger.IsAttached 只读属性来检查是否附加了调试器，并使代码基于此条件表现出不同的行为。这种技巧的使用存在于 UI 框架中（例如，在开发期间对用户代码中的跨线程违规更挑剔）。调试器的存在是“开发”的良好指标。

尽管在某些情况下，这种逻辑的条件执行可能是合理的，以便在开发期间更轻松地使用库，但应该很清楚，这也可能是调试库本身时最令人沮丧的来源。（我本人经历过这种情况。）

## 记录堆栈跟踪

从调试开发人员的角度来看，解决问题的最宝贵财富很可能就是堆栈跟踪。拥有这些信息可以回答代码在特定时间点正在做什么的问题。虽然这些信息在调试器中很容易获得，但在代码中记录堆栈跟踪有时也很有用。

这里 System.Diagnostics 中的 StackTrace 类成为当天的英雄。创建此类的新实例会捕获当前线程的堆栈跟踪。有几个构造函数重载可用于从 Exception 对象提取堆栈跟踪、跳过指定数量的帧等等。这里有一个愚蠢的示例：

```
static void Bar()
{
    var trace = new StackTrace();
    Console.WriteLine(trace);
}

static void Main()
{
    Bar();
}
```

StackTrace 对象可以通过其 ToString 方法打印（此处由 WriteLine 的使用隐式调用），或通过使用 GetFrame 和 GetFrames 方法分解为单个堆栈帧。前面的代码片段打印如下内容：

```
at Program.Bar()
at Program.Main()
```

### 看到更大的堆栈跟踪？

尝试运行此示例时，看到更大的堆栈跟踪是可能的，事实上也很可能。这是由于 Visual Studio 主机进程造成的，它用于启用某些调试场景，并且本身是一个托管应用程序，位于调用堆栈的更高位置。

你可以通过存在一个帧来识别这样的调用堆栈，该帧显示对 Microsoft.VisualStudio.HostingProcess.HostProc 中的 RunUsersAssembly 的调用。虽然主机进程具有某些有据可查的优点，但有时它可能被认为是有害的，因为某些全局属性不同。例如，对应用程序域、原生命令行等事物的检查会有所不同。

通过将 true 传递给构造函数，如果找到符号文件（扩展名为 .pdb），也可以获取文件信息。请注意，此过程相当慢，因此最好避免在性能关键的代码路径中使用堆栈跟踪日志记录。还请记住，异常本身就具有堆栈跟踪，因此无需显式代码来捕获此类跟踪。你仍然可以使用 StackTrace 类从代码中更详细地检查堆栈跟踪（例如，在单个帧级别）。

## 使用 StopWatch 测量性能

代码片段的性能测量应使用足够精确的时间，否则毫无价值。仅仅减去 DateTime 值是不够的，因为 DateTime 值的分辨率相对较低。为了证明这一点，输入以下代码片段，该片段多次计算 50 的阶乘：

```
for (int j = 0; j < 10; j++)
{
    var start = DateTime.Now;

    var n = 1L;
    for (int i = 2; i < 50; i++)
        n *= i;

    var end = DateTime.Now;
    Console.WriteLine(end - start);
}
```
