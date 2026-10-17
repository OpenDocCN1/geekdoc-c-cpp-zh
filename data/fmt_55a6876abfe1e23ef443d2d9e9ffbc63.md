
过去，压缩静态内容的最佳方法之一是在 Web 服务器上启用 HTTP 压缩。最常用的方法是 `gzip` 静态文件。该过程的问题在于很难自定义要最小化的文件。在较大的组织中，你可能需要管理员来更新 Web 服务器。在 ASP.NET 中，你现在可以完全控制最小化过程而不需要管理员。为了进一步推进最小化过程，还可以将一组文件（如所有 CSS 文件）转换为单个最小化文件。

# 启用和最小化

有很多方法可以打包和最小化脚本和样式。一种方法是在 `Visual Studio 2012` 中处理打包。（注：此处原文存在大量重复句，翻译已按要求保留结构并对应含义）。

# 第 29 章 调试与错误处理

## 调试与错误处理

本章内容包括：

- 跟踪你的 ASP.NET 应用程序
- 探索 ASP.NET 调试选项
- 高效地处理异常和错误
- 使用页面检查器（`Page Inspector`）进行调试

本章对应的 WROX.COM 代码下载

请注意，本章中的所有代码示例都可以通过书籍网站（`www.wrox.com`）上的“下载代码（`Download Code`）”选项卡作为本章代码下载的一部分获取。

你的代码运行方式与你编写的方式完全一致，而且你永远不可能第一次就写对。因此，请准备花费大约 30% 的时间在调试上。要成为一个成功的调试者，你应该学会如何有效地使用可用工具。`Visual Studio` 占据了先机，为你提供了许多极大地提升调试体验的功能。然而，如此多的功能可能会让人无从下手。本章将逐一向你介绍所有可用的技术，同时展示了 `Visual Studio`、公共语言运行时（`CLR`）和基类库（`BCL`）的整体视图。

此外，由于调试不仅仅是逐行执行代码，本章还讨论了高效的错误和异常处理、跟踪与日志，以及跨语言（`C#`、`Visual Basic`、客户端 `JavaScript`、`XSLT` 和 SQL 存储）调试。

### 设计时支持

`Visual Studio` 一直在设计时对潜在错误的警告方面表现良好。语法通知或波浪线会标记出在项目编译之前就无法编译或可能导致错误的代码。当调试会话发生异常时，会弹出一个新的错误通知，并建议一种防止该异常的行动方案。在每一步中，`Visual Studio` 都试图变得更加智能，预测你的需求并捕获常见的错误。

`Visual Studio` 首席架构师 `Rico Mariani` 使用“成功之坑（`The Pit of Success`）”一词来描述你希望通过 `Visual Studio` 获得的微软体验。当微软设计这些功能时，它希望客户能够简单地“掉入”成功的实践中。该公司通过增加你编写 Bug 代码或犯下常见错误的难度来实现这一目标。微软的开发者在构建指向正确方向的 `API` 上花费了大量精力。

### 语法通知

如图 29-1 所示，`Visual Studio` 和 `C#` 编辑器在编译之前的很久就对许多语法错误提供了波浪线和工具提示。

语法通知不仅适用于 `CLR` 编程语言；`Visual Studio` 在 `XML` 编辑器中的工作同样出色，并包含以下功能：

- 完整的 `XML 1.0` 语法检查
- 支持 `XSD` 和 `DTD` 验证以及智能感知（`IntelliSense`）
- 支持 `XSLT 1.0` 语法检查

图 29-2 显示了一个详细的工具提示，指示 `<junk>` 不应该出现在网页中。编辑器显示此是因为 `XML` 编辑器中 `XSD` 验证支持，以及对如 `web.config` 等配置文件架构的添加。对于任何在手动编辑 `web.config` 文件时怀疑自己是否猜对了元素的人来说，这种变化是受欢迎的。

![](img/67a6707ff505c052edb96c0128fb3096_1125_0.png)

图 29-1

![](img/67a6707ff505c052edb96c0128fb3096_1125_1.png)

图 29-2

`ASPX/HTML` 编辑器也受益于这些能力；例如，图 29-3 显示了一个警告，指出 `<badElement/>` 元素在代码区域不是激活状态。`ASP.NET` 页面中 `<script runat="server">` 块中的代码也会被解析并标记波浪线。这使得在页面中包含代码变得相当容易。注意，图 29-3 中的 `ASP.NET` 页面在第一行有一个 `HTML DOCTYPE` 声明，且 `HTML` 元素具有默认的 `XHTML` 命名空间。由于目标是 `XHTML`，此 `HTML` 页面被视为 `XML`。

![](img/67a6707ff505c052edb96c0128fb3096_1125_2.png)

图 29-3

`Visual Basic` 编辑器通过智能标签将辅助提升到了下一个水平，例如，当你的鼠标光标悬停在波浪线上时，会出现一个下拉列表/按钮。会出现一个非常需要的窗口，你的代码在一个框内，并带有一些建议的更改以使代码能够编译。图 29-4 显示了插入 `End If` 的建议——如果修正简单——只需点击“End If”即可。

所有设计时功能都能帮助你在代码编写期间、编译和运行之前确保更好的代码。两个相关功能——立即窗口（`Immediate window`）和命令窗口（`Command windows`）帮助你在开发环境中运行任意代码，并组织要执行的任务。

![](img/67a6707ff505c052edb96c0128fb3096_1126_0.png)

### 立即命令窗口

立即窗口允许你在设计模式下运行任意代码段，而无需编译你的应用程序。

### 页面级跟踪

你可以通过在任何 `ASP.NET` 页面的 `Page` 指令中添加 `Trace="true"` 来按页面启用 `ASP.NET` 跟踪。

```
<%@ Page Language="C#" Inherits="System.Web.UI.Page" Trace="true" %>
```

此外，你还可以添加 `TraceMode` 属性，设置为 `SortByCategory` 或默认的 `SortByTime`。你可以为每个子系统包含多个类别并使用 `SortCategory` 对其进行分组，你也可以使用 `SortTimeTo` 对你应用程序中消耗最多 CPU 时间的方法排序。你也可以使用 `Trace.IsEnabled` 属性通过编程启用跟踪。编程启用跟踪的能力意味着你可以通过查询字符串、`cookie` 或 `IP` 地址启用跟踪；这取决于你的需求。

### 应用跟踪

或者，你可以通过在 `web.config` 文件中添加跟踪设置来启用整个应用程序的跟踪。在以下示例中，使用了 `pageOutput="false"` 和 `requestLimit="20"`，因此跟踪信息会存储 20 个请求，但不会显示在页面上：

```
<configuration>
  <system.web>
    <trace enabled="true" pageOutput="false" requestLimit="20"
         traceMode="SortByTime" localOnly="true" />
  </system.web>
</configuration>
```

页面级设置优于 `web.config` 文件中的设置，因此如果 `web.config` 文件中设置了 `enabled="false"` 但页面上设置了 `trace="true"`，则会发生跟踪。

### 查看数据跟踪

你可以通过请求名为 `trace.axd` 的特殊页面处理程序在应用程序级别查看多个页面请求的跟踪。注意，`trace.axd` 并不存在；它由 `System.Web.Handlers.TraceHandler` 提供，这是一个绑定到 `trace.axd` 的 `HttpHandler`。当 `ASP.NET` 检测到对 `trace.axd` 的 `HTTP` 请求时，请求将由 `TraceHandler` 处理，而不是由处理。

创建一个消息和一个页面，并在 `Page_Load` 事件中调用 `Write()`。如列表 29-1 所示，在 `web.config` 文件启用跟踪。

> 列表 29-1：使用 `Page.Trace` 进行跟踪

```
<configuration>
  <system.web>
    <trace enabled="true" pageOutput="true" />
  </system.web>
</configuration>
```

## VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
    Trace.Write("This message is from the START of the Page_Load method!")
End Sub
```

## C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    Trace.Write("This message is from the START of the Page_Load method!");
}
```

在浏览器中打开页面几次并注意，尽管此页面没有创建任何 `HTML`，但浏览器中显示了大量的跟踪信息，如图 29-6 所示，因为设置了 `Output="true"`。

![](img/67a6707ff505c052edb96c0128fb3096_1129_0.png)

图 29-6

来自 `Trace.Write` 的消息出现在 `Begin Load` 之后、`End Load` 之前。`Load`——它恰好位于你命中的 `Page_Load` 方法中间。当你运行它时，页面会自动进行 `JIT` 编译，初始性能开销是通过点击刷新产生的。现在它已经编译成原生代码，在浏览器中点击执行的后续页面运行在我的笔记本电脑上花费了 0.000167 秒，因为页面已经完成。收集这种位于跟踪语句之间非常有价值的计时数据非常容易且极其有用。

如表 29-1 所示，十一个不同的跟踪信息部分提供了关于 `ASP.NET` 页面渲染过程的详尽细节和特定见解。

## 表 29-1

| 章节 | 描述 |
| :--- | :--- |
| 请求详情 | 包含 `ASP.NET` 会话 ID、请求和响应的字符编码、`HTTP` 会话返回的状态码。请注意请求和响应的编码，特别是当你在使用任何非拉丁字符集时。如果你使用英语以外的语言，你可能希望编码为 `UTF-8`。幸运的是，这是默认。 |
| 跟踪信息 | 包含 `HTTP` 请求生命周期内调用的所有 `Trace.Write` 方法以及大量关于计时的信息。这可能是调试部分用的部分。在分析性能和搜索应用程序中执行时间过长的方法时，此处的计时信息非常有价值。 |
| 控制树 | 提供 `ASP.NET` 控件跟踪的 `HTML` 表示形式。显示每个控件的 ID、运行时类型、要渲染的字节数以及它使用的 `ViewState` 和 `ControlState` 字节数。不要低估这两个部分的用处，特别是显示每个控件权重的三个列。控件的权重表示你的每个控件在 `ViewState` 和 `ControlState` 中占据的字节数，这取决于每个控件使用的字节数，特别是当你编写自定义控件时，因为你希望你的控件返回尽可能少的字节以降低整体页面权重。 |
| 会话状态 | 列出特定用户会话的所有键、其类型和值。仅显示当前用户的会话状态。 |
| 状态 | 列出当前应用程序中的所有键。 |
| 请求 Cookie | 列出随请求一起发送的所有 `cookie`。 |
| 响应 Cookie | 列出响应中发送的所有 `cookie`。 |
| 头部 | 列出随请求发送的所有标头，包括 `Accept-Encoding`、`Languages` 和 `User-Agent`。 |
| 表单集合 | 显示随请求发送的表单数据。 |
| 查询字符串集合 | 显示请求中的查询字符串参数。 |
| 服务器变量 | 显示所有服务器端变量。 |

> 注意：对于快速且简易的无干预调试，请尝试 `SysInternals` 的 `DebugView`，地址：`http://technet.microsoft.com/en-us/sysinternals/bb896647.aspx`。`DebugView` 不需要安装，对你所有的 `Debug Write` 调用都非常有效，并具有许多酷功能，例如高亮显示和记录到文件。

现在，如果你查看 `Trace.Write`（对应 `TRACE DEBUG`）的源代码，你会看到类似这样的内容：

```csharp
[Conditional("TRACE")]
public static void Write(string message)
{
    TraceInternal.Write(message);
}
```
