
`System.Diagnostics.Trace` 是 .NET Framework 的核心追踪库。与 `System.Diagnostics.Debug` 一起，该类为任何应用程序提供了灵活、非侵入的追踪和调试输出。然而，如前，丰富的追踪功能内置在 `System.Web` 命名空间中。作为开发者，你会发现自己正在使用 ASP.NET 的追踪功能。你可能需要将 ASP.NET 特有的追踪转发到基类的 `System.Diagnostics.Trace`，或者更有可能的是，你希望你的非 Web 感知组件将追踪信息输出到 ASP.NET，以便利用 `trace.and` 和其他 ASP.NET 特有的功能。

此外，`Trace.Write` 和 `Debug.Write` 函数之间存在一些困惑。查看 `Debug.Write` 的源码，你会看到类似下面的内容：

```csharp
[Conditional("DEBUG")]
public static void Write(string message)
{
    TraceInternal.Write(message);
}
```

注意 `Debug.Write` 调用了名为 `TraceInternal.Write` 的函数，该函数有一个条件属性，指示 `Debug.Write` 只有在设置了调试预处理器时才会被编译。换句话说，你可以在应用程序中尽可能多调用 `Debug.Write`，而不会在编译 Release 模式时影响性能。这允许你在开发的调试阶段尽情使用。

`TraceInternal` 会循环遍历所有附加的追踪监听器（trace listeners），即所有派自 `Trace` 基类并根据配置文件配置的类。默认的 `TraceListener` 位于名为 `DefaultTraceListener` 中，并调用 Win32 API `OutputDebugString`。`OutputDebugString` 将你的字符串发送到深渊，如果有调试器正在监听，它就会被显示。如果没有调试器在监听，`OutputDebugString` 则什么都不做。大家都知道调试器会监听 `OutputDebugString`，这可以是你应用程序调试版本中监听的一种非常有效的方法。

> 要进行快速且无干预的调试，请尝试使用来自 http://technet.microsoft.com/en-us/sysinternals/bb896647.aspx 的 SysInternals DebugView。DebugView 不需要安装，与你对 `Debug.Write` 的所有调用配合得很好，并具有许多酷的功能，如高亮和记录到文件。

现在，如果你查看 `Trace.Write` 的源码（注意**不是** DEBUG），你会看到类似的内容：

```csharp
[Conditional("TRACE")]
public static void Write(string message)
{
    TraceInternal.Write(message);
}
```

`Debug.Write` 和 `Trace.Write` 之间的区别在于这两个源代码片段带有指示预处理器指令 `TRACE` 的条件属性。你可以根据条件选择地编译你的程序集，以包含追踪语句、调试语句、两者都包含，或两者都不包含。大多数人在发布版本中保持 `TRACE` 的定义，并使用配置文件来开启或关闭追踪。极有可能，你通过为用户提供追踪功能所获得的收益大于可能出现的任何性能问题。

由于 `Trace.Write` 像 `Debug.Write` 一样调用 `DefaultTraceListener`，你可以使用任何调试器来接入追踪信息。那么，区别在哪里呢？

在设计应用程序时，考虑你的部署模型。你是要发布调试版本还是发布版本？你是否希望最终用户或系统工程师能够使用日志文件或事件查看器来调试你的应用程序？是否存在某些你只希望让开发者看到的内容？

# 第 23 章 调试与错误处理

通常，对于任何可能在生产环境中调试应用程序有用的正式信息，你都会使用追踪和 `Trace.Write`。`Trace.Write` 为你提供了 `Debug.Write` 的所有功能，但它使用了 `Trace` 预处理器，且不受调试或发布构建的影响。

这意味着你的构建有四种可能性：Debug On、Trace On、Both On 或 Neither On。由你选择适合自己的。通常，在调试时使用 Debug On，在生产环境中使用 Trace On。你可以在编译器的属性页或命令行命令行中指定这些条件属性，也可以使用 `#define` 关键字或 Visual Basic 指定。

## 追踪转发 (Trace Forwarding)

你经常会发现某些高度仪器化并大量使用 ASP.NET `Trace` 类的 ASP.NET 应用程序。ASP.NET 在 `web.config` 的 `<trace>` 元素中包含追踪，允许你通过 ASP.NET 将消息路由到 `System.Diagnostics.Trace.WriteToDiagnostics`。

```xml
<trace writeToDiagnostics="true" pageOutput="true" />
```

当你将 `WriteToDiagnostics` 设置为 `true` 时，对 `System.Web.UI.Page.Write`（ASP.NET TraceContext）的所有调用也会进入 `System.Diagnostics.Trace.Write`，让你能够使用基类库范围内涵盖的所有标准 `TraceListeners` 和追踪选项。这个简单的 `WriteToDiagnostics` 设置将 ASP.NET 的追踪功能与基类库的其他部分连接起来。当我深度调试页面时会使用此功能，并通过此配置开关轻松关闭。我相信信息越多比越少好，但你可能会发现具体的页面事件信息过于冗长。尝试形成你自己的观点。

## 追踪监听器 (TraceListeners)

`System.Diagnostics.Trace` 方法的输出可以通过 `TraceListener` 路由到文本文件、通过 ASP.NET 路由到外部监控系统或到数据库。这一强大功能对于许多 ASP.NET 开发者来说是一个极少被使用的工具。在 ASP.NET 早期，开发者知道假设 `HttpContext` 始终可用是危险的。首先，将你的组件与 `HttpContext` 绑定会让单元测试变得困难。其次，如果 `HttpContext` 为 `null`，你的应用程序将会崩溃。

访问资源（如文件、事件日志或数据库）的 `TraceListeners`（如 `TextWriterListener`）需要 ASP.NET 进程以足够权限的用户运行。例如，要写入 `c:\example.log`，ASP.NET 进程需要对该文件的访问控制列表 (ACL) 写入权限。

然而，假设 `HttpContext` 始终可用是危险的。首先，将你的组件与 `HttpContext` 绑定会让单元测试变得困难。其次，如果 `HttpContext` 为 `null`，你的应用程序将会崩溃。

你可以使用任何调试器来接入追踪信息。那么，区别在哪里呢？

在设计应用程序时，考虑你的部署模型。你是要发布调试版本还是发布版本？你是否希望最终用户或系统工程师能够使用日志文件或事件查看器来调试你的应用程序？是否存在某些你只希望让开发者看到的内容？

访问资源（如文件、事件日志或数据库）的 `TraceListeners`（如 `TextWriterListener`）需要 ASP.NET 进程以足够权限的用户运行。例如，要写入 `c:\example.log`，ASP.NET 进程需要对该文件的访问控制列表 (ACL) 写入权限。

### 列表 23-2：配置 TraceListeners

VB

```vb
Dim myTextListener As New TextWriterListener(File.Create("c:\example.log"))
Trace.Listeners.Add(myTextListener)
```

C#

```csharp
TextWriterListener myTextListener = new TextWriterListener(File.Create("c:\example.log"));
Trace.Listeners.Add(myTextListener);
```

你可以在 `web.config` 文件中声明式地执行：

```xml
<configuration>
  <system.diagnostics>
    <trace autoflush="false" indentize="4">
      <listeners>
      <add name="myListener"
        type="System.Diagnostics.TextWriterListener"
        initializeData="c:\example.log" />
      <remove name="Default" />
      </listeners>
    </trace>
  </system.diagnostics>
</configuration>
```

## 使用 ASP.NET WebPageTraceListener

ASP.NET `WebPageTraceListener` 派自 `System.Diagnostics.TraceListener`，并将任何组件的追踪信息自动转发到 `System.Diagnostics.Trace`。这允许你使用通用的追踪提供程序编写组件，并在 ASP.NET 应用程序的文中查看其追踪输出。

如下例所示，将 `WebPageTraceListener` 添加到 `web.config` 文件中。注意我们使用了 `System.Web` 的完全限定程序集名称。

```xml
<configuration>
  <system.diagnostics>
    <trace autoflush="false" indentize="4">
      <listeners>
      <add name="webpagelistener"
        type="System.Web.WebPageTraceListener,System.Web,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b0f5f7f1ld50a3" />
      </listeners>
    </trace>
  <system.web>
    <trace enabled="true" pageOutput="false" localOnly="true" />
  </system.web>
</configuration>
```

图 23-8 显示了从引用库调用 `System.Diagnostics.Trace.Write`。它出现在 ASP.NET 追踪文中。引用监听器生成的行在图中被圈出。

# 906 | 第23 章 调试与错误处理

![](img/7040c21013b8e6c23c612d6da3599ff8_965_0.png)

图 23-8

### EventLogTraceListener

跟踪信息也可以通过 EventLogTraceListener 发送到事件日志中。这样做可能比较复杂，因为 ASP.NET 需要对事件日志进行显式访问：

```xml
<configuration>
  <system.diagnostic>
    <trace autoflush="false" indentsize="4">
      <listeners>
        <add name="EventLogTraceListener"
          type="System.Diagnostics.EventLogTraceListener"
          initializeData="Wrox" />
      </listeners>
    </trace>
  </system.diagnostic>
</configuration>
```

注意，“Wrox" 是作为字符串传递给正在添加的 TraceListener 的 `initializeData` 属性的。字符串 "Wrox" 显示为此事件的应用程序或源。当你调试应用程序时，这是有效的；调试器很可能具有适当的权限。但是，当你的应用程序部署时，它可能会在权限较低的帐户下运行，因此你必须对注册表键授予显式访问，例如 `HKLM\MACHINE\System\CurrentControlSet\Services\EventLog\Wrox`，其中 "Wrox" 与传递给 `initializeData` 的名称相同。记住，注册表键和文件一样拥有 ACL（访问控制列表）。使用 RegEdit.exe，通过右键点击键并选择“属性”，像设置文件一样设置 ACL 来更改注册表键的权限。

使用 EventLogTraceListener 要小心，如果你有一个特别频繁的应用程序，事件日志可能会很快填满。图 23-9 显示了与图 23-8 相同的跟踪输出，但位于事件日志中。事件查看器显示的是 Windows，你需要创建一个简单的自定义视图（Custom View）来仅显示“Wrox”事件。

## 跟踪 907

![](img/7040c21013b8e6c23c612d6da3599ff8_966_0.png)

## 其他有用的监听器

.NET Framework 4 除了 WebPageTraceListener 之外，还包含了两个额外的 TraceListeners：

- `XmlWriterTraceListener`：继承自 `TextWriterTraceListener` 并写出强类型的 XML 文件。
- `DelimitedListTraceListener`：同样继承自 `TextWriterTraceListener`；写入逗号分隔的值 (CSV) 文件。

关于 `XmlWriterTraceListener` 创建的 XML，值得注意的有趣点之一是它不是良好的 XML！具体来说，它没有根节点；它是同级节点的集合，如下所示代码所示。这可能与人们被告知的关于 XML 的许多观点不符，但每个事件都是一个事件。每个事件都是独立的并且可以被消费。它们恰好排在同一个文件中。自动关闭标签的缺失规避了良好性问题，并允许轻松追加到文件中。

```xml
<E2TraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2TraceEvent">
<E2TraceEvent xmlns="http://schemas.microsoft.com/2004/06/windows/eventlog/system">
<Type>3</Type>
<SubType Name="Information">0</SubType>
<TimeCreatedSystemTime>2009-11-05T12:43:44.2234234*Z</TimeCreatedSystemTime>
<Source Name="WroChart23.exe"</Source>
<Correlation ActivityID="00000000-0000-0000-0000-000000000000">
<Execution ProcessName="WroChart23.exe" ProcessID="4234" ThreadID="1"/>
<Channel></Channel>
<Computer>SCOTPC/Computer</Computer>
<System>
<ApplicationData>Your Text Here</ApplicationData>
</System>
</E2TraceEvent>
<E2TraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2TraceEvent">
```

```xml
<System xmlns="http://schemas.microsoft.com/2004/06/windows/eventlog/system">
  <EventID>0</EventID>
  <Type>3</Type>
  <!-- XML 继续 -->
```

E2TraceEvent 中的 "E2E" 代表端到端（end-to-end）。注意它包含了如你的计算机名称和“关联 ID”等信息。

自 .NET Framework 3.5 以来，列表中增加了一个额外的 TraceListener，`ITraceListener`。正如使用 WebTraceListener 将 Diagnostics 与 ASP.NET 跟踪桥接一样，`ITraceListener` 将 ASP.NET 的跟踪机制与 IIS 7.0 桥接。这允许向 IIS 7.0 基础设施引发事件。

## 诊断开关

仅仅为了更改跟踪特性就重新编译是不方便的。有时你可能想更改配置文件以添加和删除 TraceListeners。在其他时候，你可能想更改配置参数或“拨动开关”来调整跟踪的细节。Switch 出现的地方是一个抽象基类。

## SourceSwitch

自 .NET Framework 3.5 以来，列表中增加了一个额外的 TraceListener，`ITraceListener`。正如使用 WebTraceListener 将 Diagnostics 与 ASP.NET 跟踪桥接一样，`ITraceListener` 将 ASP.NET 的跟踪机制与 IIS 7.0 桥接。这允许向 IIS 7.0 基础设施引发事件。

## 诊断开关

仅仅为了更改跟踪特性就重新编译是不方便的。有时你可能想更改配置文件以添加和删除 TraceListeners。在其他时候，你可能想更改配置参数或“拨动开关”来调整跟踪的细节。Switch 出现的地方是一个抽象基类。

随后，在示例 `Page_Load` 中，你将此事件发布到管理子系统：
