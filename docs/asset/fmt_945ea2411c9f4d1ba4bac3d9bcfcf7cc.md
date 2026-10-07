
ASP.NET 在过去的 8 年里（几乎是十年！）增长得巨大，通过将 Web 开发的重复性任务自动化为拖放控件，使 Web 页面变得高效且简单。这种抽象可以提供巨大的帮助，但一些开发者发现他们想要对生成的 HTML 和浏览器脚本拥有控制权，并且能够轻松地测试他们的 Web 页面。

随着语言的成熟和 Web 软件能力的增长，MVC 很快进入了应用程序架构。但 MVC 直到 2004 年 7 月才进入主流视野，当时伊利诺伊州芝加哥 37Signals 公司的一位 24 岁的开发者 David Heinemer Hansson 向世界介绍了他关于 MVC 的新颖思维方式。

David（或者社区中熟知的 DHH）创建了 Ruby on Rails，这是一个 Web 开发框架，它使用 Ruby 语言和 MVC 模式来创建创建特别的东西。

现在让我们进一步深入探讨这个新成员 ASP.NET MVC，并回答这个问题：“为什么不用 Web Forms 了？”

2007 年，微软的 Scott Guthrie 在飞往美国东海岸参加会议的飞机上勾勒出了 ASP.NET MVC 的核心。这是一个简单的应用程序，包含几百行代码，但它为 Web 开发者群体提供的承诺和潜力是巨大的。

## 团队旁白

ScottGu（或者 "The Gu"）以原型酷酷的设计而闻名，如果你在走廊里看到他，他正拿着笔记本电脑并说：“哥们儿！看这个！”他的热情是具有感染力的。

据传说，在 2007 年 10 月于华盛顿州雷德蒙举行的 ALT 会上，ScottGu 向一组开发者展示了他在飞机上写的酷酷的东西，并询问他们是否看到了以及是怎么想的。这太火了。事实上，许多人参与了代号为 "Scalene" 的原始原型，Eilon Lipton 在 2007 年 9 月向团队展示了第一个原型，他和 ScottGu 通过电子邮件往来讨论想法。

## 模型-视图-控制器与 ASP.NET

ASP.NET MVC 依赖于其他 MVC 平台使用的许多核心策略，并提供了编译和托管代码的优势，并在 .NET 3.5 及以上版本中使用 C#3 的 lambda 和匿名类型探索新功能。每个 MVC 框架广泛共享一些基本原则：

- 约定优于配置（Convention over Configuration）
- 不要重复（Don't repeat yourself，也称为 DRY 原则）
- 尽可能可插件（Pluggability whenever possible）
- 尽可能提供帮助，如果必要的话

## 方法，而非文件

Web 服务器最初使用存储在磁盘上的静态文件。动态 Web 页面变得流行，Web 服务器从加载的动态脚本动态生成 HTML。使用 MVC，生成 HTML 有所不同。URL 告诉路由机制渲染哪个视图（如果有）。在 ASP.NET MVC 中，此类类习惯上以 "Controller" 后缀命名。

如果你没有使用 Visual Studio，首要任务是在你的 2008 开发机上安装 MVC 框架。请从 `www.aspnet.mvc` 下载最新版本开始。如果你喜欢挑战，可以在 `codeplex.com/aspnet` 获取 ASP.NET MVC 的未来发布版本。

你正在下载的是一组 Visual 项目模板，这些模板将创建你的 ASP.NET MVC Web 应用程序。你已经用过这些了——每个 ASP.NET 网站和 ASP.NET Web 应用程序都是基于一组模板的。这些模板将安装在 Visual Studio 中，而引用程序集将安装在 `C:\Program Files\Microsoft.ASP.NET`。

在安装完 ASP.NET 和 MVC 之后，你就可以使用 Visual Studio 2008 创建 ASP.NET MVC 应用了。不过，如果你使用的是 Visual Studio 10，则需要按照以下步骤操作：

- 1. 通过选择“文件->新建”打开 Visual Studio 2010。
- 2. 从图 27-1 所示的“新建项目”对话框中，选择 ASP.NET MVC 2 Web Application。

![](img/7040c21013b8e6c23c612d6da3599ff8_1122_0.png)

- 3. 选择你的项目名称以及它在磁盘上的位置，并点击确定。出现图 27-2 所示的“创建单元测试项目”对话框。
- 4. 默认情况下，测试框架下拉列表包含“Visual Studio Test”选项。选择“是”以创建一个包含 ASP.NET MVC 项目和额外的 MSTTest 单元测试项目的解决方案。如果你安装了像 MSTUnit 或 NUnit 等第三方单元测试框架，对话框中会显示额外选项。

![](img/7040c21013b8e6c23c612d6da3599ff8_1122_1.png)

- 5. 点击确定，将生成一个与图 27-3 所示的项目解决方案。请注意，尽管这是一个带有标准类库的 ASP.NET 应用，但它具有一些你以前从未见过的额外功能。

事实上，该应用程序的目录比你预想的要多；ASP.NET MVC 设计像其他 MVC 框架一样，严重依赖于这样观点：通过依靠应用程序中的某些结构规则来减少工作和代码。Ruby on Rails 非常简洁地呈现了这一强大思想：*约定优于配置*（Convention over Configuration）。

## 约定优于配置

“约定优于配置”的概念几年前由 Ruby on Rails 普及，它本质上意味着：我们现在已经知道如何构建 Web 应用程序。将这些经验融入框架中，这样我们就不需要配置任何东西。

你可以通过查看应用程序的三个核心目录看到这一概念在 ASP.NET MVC 中的应用：

Controllers（控制器）
- Models（模型）
- Views（视图）

你不需要在 `web.config` 文件中设置这些名称——按照约定，它们是预期的。

这为你节省了编辑 XML 文件（例如 *web.config* 文件）的工作，无需显式告诉 MVC 引擎“你可以在 Controllers 目录中找到控制器”。它已经知道了。这是约定。

这个功能并不是为了变得魔法。事实上，它确实是；它并不是 ASP.NET MVC 项目经理 Phil Haag 所说的“黑魔法”——它是那种可以让你获得预期输出（而且实际上可以运行你的应用程序）的魔法。

ASP.NET MVC 的约定非常直观。这是对你应用程序结构的预期：

- 它有一个 Controllers 目录，用于存放你的控制器。
每个 Controller 的类名都以 "Controller" 结尾——例如 `ProductController`、`HomeController` 等——并存在于 Controllers 目录。
- 它有一个 Views 目录，用于存放应用程序的所有视图。
- 控制器所在的视图位于 Views 目录的子目录中，并根据控制名称（去掉 "Controller"）命名。例如，之前讨论的 `ProductController` 的视图将位于 `/Views/Product` 中。

所有可重用的 UI 元素都位于类似的结构中，但在根目录下有一个“shared”（共享）目录。

如果你深入观察图 27-4 所示的示例应用程序的初始结构，你可以看到这些约定的应用。两个控制器 `HomeController` 和 `AccountController` 位于 Controllers 目录中，许多视图位于 Views 目录中。接下来的讨论集中在 `/Views/Home` 下名为 About 和 Index 的视图。

![](img/7040c21013b8e6c23c612d6da3599ff8_1123_0.png)

![](img/7040c21013b8e6c23c612d6da3599ff8_1123_1.png)

图 27-3

图 27-4

虽然对你如何命名视图没有硬性约定，但你可以学习 ASP.NET MVC 的约定，即让你的视图与你的操作（action）具有相同的名称。使用这种约定也让其他开发者更容易审查和理解你的应用程序。

你可以从模板创建 Index 和 About 视图的方式看到这一约定的应用。这些也是你创建的控制器名称，渲染这些视图的代码非常简单：

- 1. 回到 `HomeController.cs`，并将渲染这些视图的代码更改：

```csharp
public ActionResult Foo()
{
    View["Title"] = "Foo Page";
    return View();
}
```

- 2. 启动应用程序，再次在 `/Home/Foo` 查看视图。Index 视图被渲染，Title 字符串出现在你浏览器的标题中。
- 3. 回到 Visual Studio，在返回 View 结果的行上设置断点。刷新浏览器，确认你仍处于 `/Home/Foo`，并进行深入研究。

*(注：由于原始 OCR 文本在第 1124-1125 页略有碎片，此处根据实际内容重新对齐了文本流。)*

### 模型-视图-控制器与 ASP.NET | 2067

![](img/7040c21013b8e6c23c612d6da3599ff8_1126_0.png)

图 27-7

花一点时间观察 Visual Studio（或者如果你喜欢，看这张图），并尝试确定它在告诉你什么。你是如何来到这里的？你在哪里？

你在浏览器中访问了 `/Home/Foo`，现在你奇迹地停在了 `Foo` 方法的一个断点处。调用堆栈（Call stack）窗口包含了这些信息，但它并没有告诉你。你是如何来到这里的？右键点击调用堆栈的空白区域，选择“显示外部代码”（Show External Code）。你也可以提取调用堆栈工具窗口并“脱离” Visual Studio，以便更好地分析即将显示的崩溃信息。如果你有多个显示器，请记住 Visual Studio 2010 支持该功能，如果你喜欢，可以让一个显示器充满调用堆栈工具窗口。

调用堆栈窗口包含的信息太多了，事实上，作者们亲自从上到下强调了其中的一些重要部分，其中底部是你开始的地方，顶部是你当前正在调试的行。在这个调用堆栈中，某些部分比其他部分更重要。

![](img/7040c21013b8e6c23c612d6da3599ff8_1126_1.png)

图 27-8

从底部开始，你可以看到选择了执行线程，`HttpWebRequest` 正在被 ASP.NET 分发并处理——通过 `System.Web.Runtime`。这是 ASP.NET 的“开始”，即这是 `System.Web`，而你正处于 `System.Web.dll` 内部——还没有发生任何 MVC 操作。如果你已经熟悉 Web Forms，你会发现记住 ASP.NET 的正统部分在何处结束以及 ASP.NET MVC 是什么是很有用的。

（从下到上读取）第一个发生的重大事件是在图 27-8 所示的底部。从这个堆栈中你可以学习到什么？ASP.NET MVC 是构建在带有 `HttpHandlers` 和 `HttpModules` 的 ASP.NET 之上的。这就是 MVC 获得其钩子的方式。

ASP.NET MVC 被实现为 `HttpHandler` 这一事实让你感到安心，因为你知道团队在编写它时是“遵循规则”的。ASP.NET MVC 的设计中不存在任何内部知识或秘密。它使用的是所有开发者均可使用的公共构造结构和 API。

> 发现 ASP.NET MVC 的设计中没有秘密让我们感到宽慰。ASP.NET MVC 中的“魔法”越少，我们就越容易理解它。如果 ASP.NET MVC 是一个 `HttpHandler`，而你又写过很多这样的程序，那么它比你想象的要没那么魔法！看到 ASP.NET 本身足够灵活并足以允许像 ASP.NET MVC 这样的东西创建，也是很好的。

从这些发现中你可以学习到的另一点是，ASP.NET MVC 使用 `HttpHandlers`（以及 `HttpModules`）来工作，MVC 是构建在 ASP.NET 之上的。对于某些人来说这似乎是一个显而易见的结论，但一个非常常见的问题是“ASP.NET MVC 是一种新方法吗？”从图 27-8 可以看出它并不是。它运行在你多年使用的相同基础设施——“核心”ASP.NET 之上。

回看 27-8 并查看该调用。记住你现在正停在 `HomeController` 内部 `Foo` 方法的断点处。是谁创建了 `HomeController`？必须有人对它进行了 `new`。是谁调用了 `Foo`？朋友们，请查看调用栈。

在控制器的 Handler 的 `ProcessRequest` 方法内部，控制器是由 `DefaultControllerFactory` 创建的。ASP.NET MVC 创建了 `HomeController` 的实例，然后调用了控制器的 `Execute` 方法。该方法在控制器 action 的上下文中（通过默认的 `ControllerActionoker`）运行，以实际调用该方法。

记住你打开了浏览器并请求了 `/Home/Foo`。ASP.NET MVC 将请求路由到 `MVCHandler`。它创建了 `HomeController` 的实例并调用了 `Foo` 方法。ASP.NET MVC 已经为你处理了激活和调用。

`/Home/Foo` URL 被 `RoutingModule` 拦截了。该模块负责通过解析 URL 并发送某些路由数据，以确保正确的 URL 进入正确的控制器。MVC 管道线分别使用 `ControllerFactory` 和 `Controlleroker` 来创建你的控制器并调用其方法。

控制器的存在是为了“处理各种事情”。具体要做什么由你决定。你与 `Model` 通信，进行计算，等等。然而，它们不渲染 HTML，也不与数据库通信。这就是关注点分离。控制器的关注点在于控制。

## 理解路由和 URL

软件开发者以关注细节而闻名，特别是在涉及到源代码的质量和结构时。他们经常为了代码缩进样式和大括号应该放在哪里而进行激烈的战斗。因此，当你使用 ASP.NET 的网站方法并遇到如下的 URL 时，会感到有些意外：

`http://example.com/products/list.aspx?id=17313&catid=33723&page=3`

对于所有关注代码的开发者来说，为什么不对 URL 投入同样的关注呢？它看起来可能并不重要，但 URL 是一个合法的且广泛使用的 Web 用户界面。

可用性专家 Jakob Nielsen (`www.useit.com`) 敦促开发者关注 URL：

- 域名易于记忆
- 短且易于输入的 URL
- 不改变的持久性 URL
- 高质量 URL
- 可黑客的（hackable）URL
- 易于拼写的 URL
- 易于记忆的 URL
- 易于输入的 URL

在创建 ASP.NET MVC 项目后，快速查看 `Global.asax.cs` 中的代码。你会发现 `ApplicationStart` 方法包含了对 `RegisterRoutes` 方法的调用。该方法是注册应用程序路由的地方。

## 定义路由

每个 ASP.NET MVC 至少都需要一个路由来定义它的工作。在本节中，你将学习如何定义路由。

## 设置路由

在创建 ASP.NET MVC 项目后，快速查看 `Global.asax.cs` 中的代码。你会发现 `ApplicationStart` 方法包含了对 `RegisterRoutes` 方法的调用。该方法是注册应用程序路由的地方。

现在清除文件中的路由，并将其替换为此简单路由：

```csharp
routes.MapRoute("Default", "{first}/{second}/{third}");
```

`MapRoute` 方法的最简单形式接收路由名称和路由 URL 模式。名称将在本章后面讨论。现在，关注 URL 模式。

注意路由 URL 由多个段组成（段是斜杠之间的所有内容，不包括斜杠），每个段包含一个使用大括号定义的占位符。这些占位符被称为 URL 参数。

这种结构是一个模式匹配规则，用于确定此路由是否适用于传入的请求。在这种情况下，此路由将匹配任何具有三个段的 URL，因为 URL 参数默认匹配任何非值。当它匹配具有三个段的 URL 时，URL 的第一段文本对应 `{first}` URL 参数，第二段的值对应 `{second}` URL 参数，而第三段的值对应 `{third}` 参数。

在这种情况下，你可以为它们命名为任何名称。当请求进入时，路由将请求 URL 处理为字典（特别是通过 `RequestContext` 访问的 `RouteValueDictionary`），使用 URL 参数名称作为键，并将对应位置的 URL 段作为值。在 MVC 应用程序上下文中使用路由时，某些参数名称具有特殊用途。表 27-1 显示了定义的路由如何转换为 `RouteValueDictionary`。

### 表 27-1

| URL | URL 参数值 |
|---|---|
| `/products/display/123` | `(first)` = products<br>`(second)` = display<br>`(third)` = 123 |
| `/foo/bar/baz` | `(first)` = foo<br>`(second)` = bar<br>`(third)` = baz |
| `/a.b/c/d/e-f` | `(first)` = "a.b"<br>`(second)` = "c-d"<br>`(third)` = "e-f" |

## 理解路由和 URL

如果你实际上对上表列出的 URL 发起请求，你可能会发现 ASP.NET MVC 应用程序似乎坏了。尽管你可以使用任何喜欢的参数名称来定义路由，但某些特殊名称会被 ASP.NET MVC 识别以确保其正常运行—— `(controller)` 和 `(action)`。

`(controller)` 参数的值用于实例化控制器类（controller class）来处理请求。按照惯例，MVC 在 `(controller)` 的值后附加 "Controller"，并尝试创建一个与该名称同名的类型（不区分大小写），该类型还继承自 `System.Web.Mvc.IController`。

回到简单的路由，将其更改为

```
routes.MapRoute("simple", "{first}/{second}/{third}");
```
