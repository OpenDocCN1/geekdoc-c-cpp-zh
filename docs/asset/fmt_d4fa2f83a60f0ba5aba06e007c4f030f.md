
```
var request = (HttpRequest)WebRequest.Create(uri);
request.Headers.Add(HttpHeaders.Encoding, "deflate");
request.AutomaticDecompression = DecompressionMethods.Gzip | DecompressionMethods.Deflate;
```

其他 HTTP 通信对象（如 ASMX Web 服务或 WebClient 对象）也支持 IIS 压缩，但必须手动配置以发送头部并解压缩响应。作为 HTTP-WCF 服务，在 WCF 4 之前，.NET 客户端必须使用不支持 IIS 压缩的程序引用（service reference）或通道工厂。从 WCF 4 开始，自动支持 IIS 压缩，用于发送头部和解压缩响应。

# 第 11 章 Web 应用程序性能

## 压缩化与合并（Minification and Bundling）

在开发应用程序时，您的页面可能会使用多个 JavaScript 和 CSS 文件。当页面有多个指向外部资源的链接时，在浏览器中加载页面将成为一项耗时的操作，用户将需要等待页面及其所有相关脚本被下载并解析。对于外部资源，我们面临着两个问题：

1. 浏览器需要发送并等待响应的请求数量。请求越多，告知服务器所有请求所需的时间越长，因为浏览器受到其对单个服务器并发连接数量的限制（例如，在 IE 9 中，每个服务器的并发请求限制为 6 个）。
2. 响应的大小，这影响了浏览器下载所有响应的总时间。响应越大，浏览器下载响应所需的时间越长。如果达到最大并发请求数，这还可能影响浏览器开始发送新请求的能力。

为了解决这个问题，我们需要一种能够让我们降低响应大小和请求数量（从而减少响应数量）的技术。在 ASP.NET MVC 4 和 ASP.NET 4.5 中，这种技术内置在框架中，允许进行“合并和压缩化（bundling and minification）”。合并指的是在请求时将一组文件合并到一个 URL 中，返回所有合并后的文件作为一个单个脚本；而压缩化是指通过删除空格以及在脚本文件的情况下删除变量和函数来减少样式或脚本文件的大小，从而占用更少的空间。

将压缩化与压缩结合可以显著减少响应的大小。例如，jQuery 1.6 脚本文件在压缩之前的大小为 240 kb。压缩后文件大小约为 68 kb。原始文件的压缩版本为 93 kb，比压缩版本略大；应用压缩化文件后，大小降至 33 kb，约占原始文件大小的 14%。

要创建一个包，首先安装 `Microsoft.Web.Optimization` NuGet 包，并添加对 `System.Optimization` 程序集的引用。添加后，您可以使用 `BundleTable` 静态类为脚本和样式创建新包。合并应该在加载页面之前设置，您应该将包放置在 `global.asax` 的 `Application Start` 方法中。例如，以下代码创建了名为 MyScripts（可从虚拟文件夹访问）的三个脚本文件包，这些文件将被自动压缩化：

```
protected void Application_Start() {
    Bundle MyScripts = new Bundle("/MyScripts").Include(
    ~/Scripts/MyCustomJs.js",
    "~/Scripts/thirdPartyJs.js",
    "~/Scripts/myNewJsTypes.js");
    BundleTable.Bundles.Add(MyScripts);
    BundleTable.EnableOptimizations=true;
}
```

默认情况下，合并和压缩仅在 Web 应用程序编译设置为 Release 时工作。为了在 Debug 模式下启用合并，我们将 `EnableOptimizations` 设置为 true。

要使用创建的包，在页面上添加以下脚本行：

<%= Scripts.Render("/MyScripts") %>

当页面渲染时，该行将被替换为指向包的 `<script>` 标签，例如上面的行可能转换为 HTML：

```
<script src="/bundles/MyScript?xGAE5010_bMlU7DS_Xmgf5dchi8g41" type="javascript"></script>
```

## 内容分发网络（CDN）

合并和压缩框架还支持自定义转换，允许为 JavaScript 文件创建专门的转换。

以类似的方式，我们可以为 CSS 文件创建一个包：

```
MyStylesBundle=new StyleBundle("/bundles/myStyles").Include("~/Styles/defaultstyle.css",
"~/Styles/extensions.css",
"~/Styles/someStyles.js");
BundleTable.Add(MyStylesBundle);
```

并在页面中使用该包：

<%= Styles.Render("/bundles/myStyles") %>

这将渲染一个链接：

<link href="/bundles/MyStyles?v=jj30n1pdg6Y3V3cUJwxtzgGNfZ1zRc1WDbm4YfW-yORI1" type="text/css" />

Web 性能问题之一是通过网络访问资源的延迟。与 Web 服务器位于同一网络的终端用户通常具有良好的响应时间，但一旦您的 Web 应用程序在全球范围内通过互联网收集世界用户，远远的用户（例如来自其他大洲的用户）将由于网络问题遭受更长的延迟和较慢的带宽。

解决位置问题的解决方案之一是在不同的地理位置部署多个 Web 服务器实例，这样终端用户在地理位置上就会靠近其中一台服务器。当然，当你需要不断更换和同步服务器，并可能需要指示每个终端用户根据其所在位置使用不同的 URL 时，就会产生一个巨大的问题。

这正是内容分发网络（CDN）大显用场。CDN 是分布在世界不同位置的 Web 服务器集合，允许终端用户始终靠近你的 Web 应用内容。使用 CDN，你实际上在全世界可以使用同一个 CDN 地址，但你所在区域的本地 DNS 会将其转换为距离你位置最近的实际 CDN 服务器。微软、亚马逊和 Akamai 等各种互联网公司都有自己的 CDN，你可以支付费用来使用。

以下场景描述了 CDN 的用法：

- 1. 你设置了 CDN 并将其指向原始内容所在地。
- 2. 当终端用户第一次通过 CDN 访问内容时，本地 CDN 服务器连接到你的 Web 服务器，拉取内容，将其缓存在 CDN 服务器中，并将内容返回给终端用户。
- 3. 对于随后的请求，CDN 服务器将在不联系你的 Web 服务器的情况下检索缓存内容，从而实现更快的响应时间，并可能更快的带宽。

> 除了更快地服务终端用户外，使用 CDN 还减少了 Web 服务器需要处理的静态内容请求数，使其能够将大部分资源用于处理动态内容。

要实现第一步，你需要选择你想要使用的 CDN，并按照提供者的说明配置你的 CDN。一旦获得了 CDN 的地址，只需将静态内容（图像、样式、脚本）的链接指向 CDN 即可。例如，如果你将静态内容上传到 Windows Azure 存储并在 Azure CDN 中注册内容，你可以将代码中的 URL 指向 CDN，如下：

```html
<link href="http://az182js3.vo.msecnd.net/static/Content/Site.css" rel="stylesheet" type="text/css" />
```

为了调试，你可以将静态 URL 替换为变量，允许你控制是使用本地地址还是 CDN 地址。例如，Razor 代码通过来自 `web.config` 文件的 `CdnUrl` 配置设置提供的 CDN 地址前缀来构建 URL：

```razor
@using System.Web.Configuration
<script src="WebConfigurationManager.AppSettings["CdnUrl"]/Scripts/jquery-1.6.2.js" type="text/javascript"></script>
```

在调试 Web 应用时，将 `CdnUrl` 更改为空字符串，以从本地 Web 服务器获取内容。

## 扩展 ASP.NET

现在，你通过结合在这里学到的所有知识提升了 Web 应用的性能，甚至应用了一些其他技术来加速，现在你的应用程序运行良好，并达到了尽可能的优化。当你将应用程序投入生产环境时，前几周运行一切正常，但随后额外的用户开始访问网站，每天都有新用户加入，增加了服务器必须处理的请求数量，突然，你的服务器开始出现瓶颈。这可能始于请求时间比平时长，你的工作进程开始使用更多内存和 CPU，最终导致超时，日志文件中出现了 HTTP 500（“内部服务器错误”）。

哪里出错了？你是否应该尝试提高应用程序的性能？会有更多用户加入，你将陷入同样的境地。你是否应该增加机器内存或添加更多 CPU？单台机器可以进行的垂直扩展（scale-up）也是有限的。是时候面对事实了——你需要扩展更多的服务器。

扩展 Web 应用是一个必须在 Web 应用生命周期某个阶段发生的自然过程。一台服务器可以处理几十或数千个并发用户，但它无法长时间承受这种压力。Session 填满服务器内存、线程因为没有更多可用线程而饥饿，以及过于频繁的上下文切换将增加单台服务器的延迟和吞吐量。

## 横向扩展（Scaling Out）

从架构角度来看，扩展不仅仅是增加一或多台服务器。扩展 Web 应用是一个必须在 Web 应用生命周期某个阶段发生的自然过程。一台服务器可以处理几十或数千个并发用户，但它无法长时间承受这种压力。Session 填满服务器内存、线程因为没有更多可用线程而饥饿，以及过于频繁的上下文切换将增加单台服务器的延迟和吞吐量。

# 第 11 章 Web 应用性能

从架构角度来看，扩展不仅仅是增加一或多台服务器。扩展 Web 应用是一个必须在 Web 应用生命周期某个阶段发生的自然过程。一台服务器可以处理几十或数千个并发用户，但它无法长时间承受这种压力。Session 填满服务器内存、线程因为没有更多可用线程而饥饿，以及过于频繁的上下文切换将增加单台服务器的延迟和吞吐量。

以及可以帮助你定位 Web 应用程序瓶颈的分析工具。通过使用监控和分析工具，你可以轻松追踪问题，并显著提高你的 Web 应用程序的性能。从那里，我们回顾了流水线（pipeline），识别了可以进行修改的不同部分，使你的应用程序运行更快、更智能，或提供更小的负载（payload）以便更快提供服务。在学习这一章之后，你现在已经意识到微小的变化（如正确使用客户端缓存）如何帮助减少服务器需要处理的请求数量，解决许多应用程序面临的某些瓶颈问题。

在章节后半部分，我们意识到单服务器无法处理所有客户端的请求，因此提前为扩展做计划并应用可扩展的解决方案（例如分布式缓存和进程外状态管理），将让你在达到一台服务器不再够用的点时能够更轻松地进行扩展。最后，在本章中，我们只探索了改进 Web 应用程序服务端的不同技术，而将另一侧留给你去探索——客户端。

这是本书的最后一章。在整个十一章中，你已经了解了如何衡量和改进应用程序性能、如何将 .NET 代码并行化并在 GPU 上运行算法、如何应对 .NET 类型系统和垃圾回收器的复杂性、如何明智地选择集合以及何时实现自己的集合，甚至如何使用最新强大的处理器功能为你的 CPU 密集型软件榨取额外性能。感谢你跟随我们完成这段旅程，祝你改进应用程序性能时好运！

# 索引

## A

- 聚合 (Aggregation), 193–194
- 算法优化 (Algorithm optimization)
  - c 近似算法 (c-approximation algorithm), 269–270
  - 最大切 (maximum cut), 271, 270–271
  - 旅行推员问题 (traveling salesman), 273
  - 间压缩 (gap compression)
  - 索引压缩 (index compression), 273–274
  - 引言 (introduction), 259
  - 记忆化与编程 (memorization and programming)
  - 全对最短路径 (all-pairs-shortest-paths), 267–269
  - 计算 (calculation), 265–266
  - 动态规划 (dynamic programming), 266
  - 编辑距离 (edit distance), 266–267
  - 斐波那契数字 (Fibonacci numbers), 265
  - 递归 (recursion), 265
  - 内存与字符串字典 (memory and string dictionary), 274
  - 概率算法 (probabilistic algorithms)
    - 费马质数性测试 (fermat primality test), 272
    - 最大切 (maximum cut), 271
  - 分类复杂度 (taxonomy complexity)
    - 大 O 表示法 (Big-notation), 259–260
    - 复杂度类与图机 (complexity classes and TM), 261–265
    - 主定理 (master theorem), 260–261
  - 变长编码 (variable length encoding), 272–273
- 分配器 (Allocators)
  - CLR 性能分析器 (CLR profiler)
    - 构建分配图 (allocation graph built), 40–41
    - 堆转储 (heap dumps), 43–44
    - 直方图按钮 (histogram buttons), 40
    - 主报告视图 (main report view), 39
    - 对象 (objects), 41–42
    - 时间线底部 (time line bottom), 42–43
    - Visual (Visual), 43–44
  - 内存相关统计数据 (memory-related statistics), 32
  - Visual 性能分析器 (Visual profiler)
    - 分配视图 (allocation view), 36, 38
    - 函数详情视图 (function details view), 36–37
    - JCompiler.exe, 35–36
    - 对象生命周期视图 (object lifetime view), 38–39
    - 摘要视图 (summary view), 36
- 全对最短路径 (All-pairs-shortest-paths)
  - Floyd-Warshall 算法 (Floyd-Warshall algorithm), 268
  - 观察 (observation), 269
  - 现实场景 (real-life scenarios), 267–268
  - 最短路径 (SP), 268
- ANTS 内存性能分析器 (ANTS memory profiler)
  - 比较 (comparison), 45–46
  - 目录 (directories), 44–45
  - 单个字符串 (individual string), 45, 47
  - 字符串 (strings), 45–46
- ASNET 应用程序 (ASNET applications)
  - 特性 (features), 305
  - 机制 (mechanisms), 331–332
  - 概述 (overview), 330–331
  - 编译 (per-compiling), 317–318
  - 陷阱 (pitfalls), 322
  - 进程模型 (process model), 318–319
  - 服务端应用程序 (server applications), 331
  - 服务端输出 (server-side output), 316–317
  - 跟踪与调试 (tracing and debugging), 313–315
  - 状态 (view state), 315–316
  - 异步课程 (asynchronous courses), 225

## B

- 基类库 (Base class library (BCL)), 118–119
- 大 O 表示法算法 (Big-notation algorithm), 259–260
- 内置 Windows 工具 (Built-in Windows tools)
  - 分类 (categories), 12–13
  - Windows 事件跟踪 (Event Tracing for Windows (ETW))
    - 自定义 ETW 提供者 (custom ETW providers), 24–26
    - 内内核提供者 (kernel providers), 3
    - 部分列表 (partial list), 13–14
    - PerMonitor (PerMonitor), 19–21
    - PerView (PerView), 22–24
  - 内置 Windows 工具 (Built-in Windows tools cont.)
    - 采样 (sampling), 13
    - Windows 性能工具包 (Windows Toolkit), 14–19
  - 性能计数器 (performance counters), 8
    - 配置性能 (configuring performance), 11
    - 日志与警报 (logs and alerts), 10
    - 监控内存 (monitoring memory), 9–10
    - 点 (points), 8
    - 步骤 (steps), 11
    - 工具 (tools), 8–9

![](img/d3ea56ae375e1d9f44bff55d84_333_0.png)
