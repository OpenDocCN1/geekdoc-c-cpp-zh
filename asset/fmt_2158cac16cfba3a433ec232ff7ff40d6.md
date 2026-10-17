
# ASP.NET MVC 布局与视图

## 布局页面

```html
<link rel="stylesheet" href="~/css/site.min.css" asp-append-version="true" />

</environment>

<title>@ViewBag.Title - My ASP.NET Application</title>

</head>

<body>

    <div class="container">

        <header>

            <h1>ASP.NET MVC Sample App</h1>

        </header>

        <nav>

            <ul>

                <li><a asp-controller="ViewsDemo" asp-action="LayoutSample">Layout Sample</a></li>

                <li><a asp-controller="ViewsDemo" asp-action="LayoutUsingSections">Layout Using Sections</a></li>

            </ul>

        </nav>

        <div>

            @RenderBody()

        </div>

        <hr />

        <footer>

            <p>

                <div>Sample Code for Professional C#</div>

                &copy; @DateTime.Now.Year - My ASP.NET Application

            </p>

        </footer>

    </div>

</body>

</html>
```

为 `LayoutSample` 操作创建了一个视图（代码文件 `MVCSampleApp/Views/ViewsDemo/LayoutSample.cshtml`）。该视图没有设置 `Layout` 属性，因此使用默认布局。下面的代码片段设置了 `ViewBag.Title`，该值在布局的 HTML `title` 元素中使用：

```csharp
@{

    ViewBag.Title ="Layout Sample";

}

<h2>LayoutSample</h2>

<p>

    This content is merged with the layout page

</p>
```

现在运行应用程序时，布局和视图的内容会合并，如图 41.3 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1581_0.png)

**图 41.3**

## 使用节

渲染主体和使用 `ViewBag` 并不是在布局和视图之间交换数据的唯一方式。使用节区域，你可以定义命名内容在视图中的放置位置。下面的代码片段使用了一个名为 `PageNavigation` 的节。默认情况下，这样的节是必需的，如果未定义该节，视图加载将失败。当 `required` 参数设置为 `false` 时，该节变为可选（代码文件 `MVCSampleApp/Views/Shared/_Layout.cshtml`）：

```html
<!-- etc. -->

<div>

    @RenderSection("PageNavigation", required: false)

</div>

<div>

@RenderBody()

</div>

<!-- etc. -->
```

在视图页面中，`section` 关键字定义节。节的放置位置与其他内容完全无关。视图不定义节在页面中的位置；这由布局来定义（代码文件 `MVCSampleApp/Views/ViewsDemo/LayoutUsingSections.cshtml`）：

```csharp
@{

    ViewBag.Title = "Layout Using Sections";

}

<h2>Layout Using Sections</h2>

Main content here

@section PageNavigation

{

    <div>Navigation defined from the view</div>

    <ul>

        <li>Nav1</li>

        <li>Nav2</li>

    </ul>

}
```

运行应用程序时，视图和布局的内容会根据布局定义的位置合并，如图 41.4 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1582_0.png)

**图 41.4**

> **注意** 节不仅用于在 HTML 页面主体中放置某些内容；它们还可用于让视图在头部放置某些内容——例如来自页面的元数据。

## 使用分部视图定义内容

布局为 Web 应用程序中的多个页面提供整体定义，而分部视图可用于定义视图内的内容。分部视图没有布局。

除此之外，分部视图与普通视图类似。分部视图使用与普通视图相同的基类，并且它们有一个模型。

下面是一个分部视图的示例。这里从一个模型开始，该模型包含独立集合、事件和菜单的属性，如 `EventsAndMenusContext` 类所定义（代码文件 `MVCSampleApp/Models/EventsAndMenusContext.cs`）：

```csharp
public class EventsAndMenusContext

{

    private IEnumerable<Event> events = null;

    public IEnumerable<Event> Events

    {

        get

        {

            return events ?? (events = new List<Event>()

            {

                new Event

                {

                    Id=1,

                    Text="Formula 1 G.P. Australia, Melbourne",

                    Day=new DateTime(2016, 4, 3)

                },

                new Event

                {

                    Id=2,

                    Text="Formula 1 G.P. China, Shanghai",

                    Day = new DateTime(2016, 4, 10)

                },

                new Event

                {

                    Id=3,

                    Text="Formula 1 G.P. Bahrain, Sakhir",

                    Day = new DateTime(2016, 4, 24)

                },

                new Event

                {

                    Id=4,

                    Text="Formula 1 G.P. Russia, Sochi",

                    Day = new DateTime(2016, 5, 1)

                }

            });

        }

    }

    private List<Menu> menus = null;

    public IEnumerable<Menu> Menus

    {

```

（代码文件 `MVCSampleApp/Controllers/ViewsDemoController.cs`）：

```csharp
public IActionResult UseAPartialView1() => View(_context);
```

视图页面被定义为使用类型为 `EventsAndMenusContext` 的模型。你可以通过使用 HTML Helper 方法 `Html.PartialAsync` 来显示一个分部视图。此方法返回一个 `Task<HtmlString>`。在下面的示例代码中，该字符串使用 Razor 语法写入 `div` 元素的内容中。`PartialAsync` 方法的第一个参数接受分部视图的名称。通过第二个参数，`PartialAsync` 方法可以传递一个模型。如果没有传递模型，分部视图可以访问与视图相同的模型。此处，视图使用类型为 `EventsAndMenusContext` 的模型，而分部视图仅使用其中类型为 `IEnumerable<Event>` 的一部分（代码文件 `MVCSampleApp/Views/ViewsDemo/UseAPartialView1.cshtml`）：

```cshtml
@model MVCSampleApp.Models.EventsAndMenusContext

@{

    ViewBag.Title = "Use a Partial View";

    ViewBag.EventsTitle = "Live Events";

}

<h2>Use a Partial View</h2>

<div>this is the main view</div>

<div>

    @await Html.PartialAsync("ShowEvents", Model.Events)

</div>
```

与使用异步方法不同，你可以使用同步变体 `Html.Partial`。这是一个返回 `HtmlString` 的扩展方法。

在视图中呈现分部视图的另一种方式是使用 HTML Helper 方法 `Html.RenderPartialAsync`，它被定义为返回一个 `Task`。此方法直接将分部视图内容写入响应流。这样，你可以在 Razor 代码块中使用 `RenderPartialAsync`。

创建分部视图的方式与创建普通视图类似。你可以访问模型，也可以访问通过 `ViewBag` 属性访问的字典。分部视图接收字典的副本，以便使用相同的字典数据（代码文件 `MVCSampleApp/Views/ViewsDemo/ShowEvents.cshtml`）：

```cshtml
@using MVCSampleApp.Models

@model IEnumerable<Event>

<h2>

    @ViewBag.EventsTitle

</h2>

<table>

    @foreach (var item in Model)

    {

        <tr>

            <td>@item.Day.ToShortDateString()</td>

            <td>@item.Text</td>

        </tr>

    }

</table>
```

运行应用程序时，视图、分部视图和布局都会被呈现，如图 41.5 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1586_0.png)

**图 41.5**

## 从控制器返回分部视图

到目前为止，分部视图都是在没有与控制器交互的情况下直接加载的，但你也可以使用控制器来返回分部视图。

在下面的代码片段中，`ViewsDemoController` 类中定义了两个操作方法。第一个操作方法 `UseAPartialView2` 返回一个普通视图；第二个操作方法 `ShowEvents` 使用基类方法 `PartialView` 返回一个分部视图。分部视图 `ShowEvents` 已经在前面创建并使用过，这里也使用了它。通过 `PartialView` 方法，一个包含事件列表的模型被传递给分部视图（代码文件 `MVCSampleApp/Controllers/ViewsDemoController.cs`）：

```csharp
public ActionResult UseAPartialView2() => View();

public ActionResult ShowEvents()

{

    ViewBag.EventsTitle = "Live Events";

    return PartialView(_context.Events);

}
```

当分部视图由控制器提供时，可以从客户端代码直接调用分部视图。下面的代码片段使用了 jQuery：一个事件处理程序被绑定到按钮的点击事件。在事件处理程序内部，通过 jQuery 的 `load` 函数向服务器发出 GET 请求，以请求 `/ViewsDemo/ShowEvents`。该请求返回一个分部视图，分部视图的结果被放置在名为 `events` 的 `div` 元素中（代码文件 `MVCSampleApp/Views/ViewsDemo/UseAPartialView2.cshtml`）：

```html
@model MVCSampleApp.Models.EventsAndMenusContext

@{

    ViewBag.Title = "Use a Partial View";

}

<script src="~/lib/jquery/dist/jquery.js"></script>

<script>

$(function () {

    $("#getEvents").click(function () {

        $("#events").load("/ViewsDemo/ShowEvents");

    });

});

</script>

<h2>Use a Partial View</h2>

<div>this is the main view</div>

<button id="getEvents">Get Events</button>

<div id="events">

</div>
```

## 使用视图组件

ASP.NET MVC 6 为分部视图提供了一种新的替代方案：视图组件。视图组件与分部视图非常相似；主要区别在于视图组件与控制器没有关联。这使得它们很容易在多个控制器中使用。视图组件真正有用的示例包括菜单的动态导航、登录面板或博客中的侧边栏内容。这些场景都是独立于单个控制器的，非常有用。

与控制器和视图一样，视图组件有两个部分。对于视图组件，控制器功能由派生自 `ViewComponent` 的类（或带有 `ViewComponent` 特性的 POCO 类）接管。用户界面的定义方式与视图类似，但调用视图组件的方法不同。

下面的代码片段定义了一个派生自基类 `ViewComponent` 的视图组件。该类使用了之前在 `Startup` 类中注册的 `EventsAndMenusContext` 类型，以便通过依赖注入使用。这与控制器中使用构造函数注入的方式类似。`InvokeAsync` 方法被定义为从显示视图组件的视图中调用。这个方法可以有任意数量和类型的参数，因为 `IViewComponentHelper` 接口定义的方法使用 `params` 关键字来接受灵活数量的参数。除了使用异步方法实现之外，你也可以同步实现此方法，返回 `IViewComponentResult` 而不是 `Task<IViewComponentResult>`。然而，通常异步变体是最好的选择——例如，用于访问数据库。视图组件需要存储在 `ViewComponents` 目录中。该目录本身可以放在项目中的任何位置（代码文件 `MVCSampleApp/ViewComponents/EventListViewComponent.cs`）：

```csharp
public class EventListViewComponent : ViewComponent

{

    private readonly EventsAndMenusContext _context;

    public EventListViewComponent(EventsAndMenusContext context)

    {

        _context = context;

    }

    public Task<IViewComponentResult> InvokeAsync(DateTime from,

DateTime to)

    {

        return Task.FromResult<IViewComponentResult>(

            View(EventsByDateRange(from, to)));

    }

    private IEnumerable<Event> EventsByDateRange(DateTime from,

DateTime to)

    {

        return _context.Events.Where(e => e.Day >= from && e.Day <= to);

    }

}
