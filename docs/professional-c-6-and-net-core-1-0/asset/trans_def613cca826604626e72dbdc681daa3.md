
当模型信息从操作方法传递到视图时，可以创建强类型视图。强类型视图使用 model 关键字声明。传递给视图的模型类型必须与 model 指令的声明相匹配。在下面的代码片段中，强类型视图声明的类型 `IEnumerable<Menu>` 与模型类型相匹配。由于 Menu 类定义在命名空间 MVCSampleApp.Models 中，因此使用 using 关键字打开该命名空间。

从 .cshtml 文件创建的视图的基类派生自 RazorPage 基类。有了模型后，基类类型为 `RazorPage<TModel>`；在下面的代码片段中，基类为 `RazorPage<IEnumerable<Menu>>`。这个泛型参数反过来定义了类型为 `IEnumerable<Menu>` 的 Model 属性。在代码片段中，基类的 Model 属性用于通过 @foreach 遍历 Menu 项，并为每个菜单显示一个列表项（代码文件 MVCSampleApp/ViewsDemo/PassingAModel.cshtml）：

```
@using MVCSampleApp.Models
@model IEnumerable<Menu>
@{
    Layout = null;
}

<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>PassingAModel</title>
</head>

<body>
    <div>
        <ul>
            @foreach (var item in Model)
            {
                <li>@item.Text</li>
            }
        </ul>
    </div>
</body>
</html>
```

你可以将任何对象作为模型传递——凡是视图所需的对象都可以。例如，当编辑单个 Menu 对象时，可以使用类型为 Menu 的模型。当显示或编辑列表时，可以使用 `IEnumerable<Menu>`。

运行显示所定义视图的应用程序时，你会在浏览器中看到菜单列表，如图 41.2 所示。

- Schweinsbraten mit Knödel und Sauerkraut
- Erdäpfelgulasch mit Tofu und Gebäck
- Tiroler Bauerngröst'l mit Spiegelei und Krautsalat

**图 41.2**

## 定义布局

通常，Web 应用程序的许多页面都共享部分相同的内容——例如版权信息、徽标和主导航结构。到目前为止，你的所有视图都包含了完整的 HTML 内容，但有一种更简单的方法来管理共享内容。这就是布局页面发挥作用的地方。

要定义布局，需要设置视图的 Layout 属性。要为所有视图定义默认属性，可以创建一个视图起始页。你需要将此文件放在 Views 文件夹中，并且可以使用项模板 MVC View Start Page 来创建它。这会创建文件 _ViewStart.cshtml（代码文件 MVCSampleApp/Views/_ViewStart.cshtml）：

```
@{
    Layout = "_Layout";
}
```

对于不需要布局的所有视图，可以将 Layout 属性设置为 null：

```
@{
    Layout = null;
}
```

## 使用默认布局页面

你可以使用项模板 MVC View Layout Page 创建默认布局页面。可以将此页面创建在 Shared 文件夹中，以便不同控制器的所有视图都可以使用它。项模板 MVC View Layout Page 会生成以下代码：

```
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>@ViewBag.Title</title>
</head>

<body>
    <div>
        @RenderBody()
    </div>
</body>
</html>
```

布局页面包含使用该布局页面的所有页面共有的 HTML 内容（例如页眉、页脚和导航）。你已经了解了视图和控制器如何通过 ViewBag 进行通信。布局页面也可以使用相同的机制。你可以在内容页面中定义 ViewBag.Title 的值；在布局页面中，它会在前面的代码片段的 HTML title 元素中显示。基类 RazorPage 的 RenderBody 方法会渲染内容页面的内容，从而定义内容应放置的位置。

在下面的代码片段中，生成的布局页面被更新为引用样式表，并向每个页面添加页眉、页脚和导航部分。environment、asp-controller 和 asp-action 是创建 HTML 元素的标记帮助程序。标记帮助程序将在本章后面的“帮助程序”部分讨论（代码文件 MVCSampleApp/Views/Shared/_Layout.cshtml）：

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <environment names="Development">
        <link rel="stylesheet" href="~/css/site.css" />
    </environment>
    <environment names="Staging,Production">
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

为 LayoutSample 操作创建了一个视图（代码文件 MVCSampleApp/Views/ViewsDemo/LayoutSample.cshtml）。该视图没有设置 Layout 属性，因此使用默认布局。下面的代码片段设置了 ViewBag.Title，该值在布局的 HTML title 元素中使用：

```
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

渲染主体和使用 ViewBag 并不是在布局和视图之间交换数据的唯一方式。使用节区域，你可以定义命名内容在视图中的放置位置。下面的代码片段使用了一个名为 PageNavigation 的节。默认情况下，这样的节是必需的，如果未定义该节，视图加载将失败。当 required 参数设置为 false 时，该节变为可选（代码文件 MVCSampleApp/Views/Shared/_Layout.cshtml）：

```
<!-- etc. -->
<div>
    @RenderSection("PageNavigation", required: false)
</div>
<div>
@RenderBody()
</div>
<!-- etc. -->
```

在视图页面中，section 关键字定义节。节的放置位置与其他内容完全无关。视图不定义节在页面中的位置；这由布局来定义（代码文件 MVCSampleApp/Views/ViewsDemo/LayoutUsingSections.cshtml）：

```
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
