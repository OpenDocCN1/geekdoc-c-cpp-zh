
3. 在 `Index` 动作中使用 LINQ `Select` 方法将每个视频转换为 `VideoViewModel` 对象，并将其存储在 `model` 字段中。使用 `Enum.GetName` 方法获取视频类型 ID 对应的类型方法。

# ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

```sharp
public ViewResult Index()
{
    var model = _videos.GetAll().Select(video =>
    new VideoViewModel
    {
        Id = video.Id,
        Title = video.Title,
        Genre = Enum.GetName(typeof(Genres), video.GenreId)
    });
    return View(model);
}
```

- 4. 打开 Index 视图并将 `@model` 指令更改为 `IEnumerable<VideoViewModel>`。

  `@model IEnumerable<AspNetCore.Models.VideoViewModel>`

- 5. 为类型添加一个新的 `<td>` 标签。

  `<td>@@video.Genre</td>`

- 6. 切换到浏览器并刷新应用程序。如你所见，类型类型现在显示在每个视频标题的旁边。

![](img/4b74569a91d8303eca7672688cf7d979_81_0.png)

## 添加详情视图 (Details View)

现在你已经知道如何使用 `VideoViewModel` 将数据发送到 Index 视图，是时候向 Views 文件夹添加一个新视图了。

Details 视图将在浏览器中显示单个视频，这将基于你接下来要添加的 Details action 方法所发送的 `id`。

### ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

- 1. 在 `HomeController` 中添加一个名为 `Details` 的新 public action 方法。它应该有一个名为 `id` 的 int 参数，该参数将匹配 URL 或请求数据中的视频 id。返回类型应该是 `IActionResult`，这使得返回不同类型的数据成为可能。

```csharp
public IActionResult Details(int id)
{
}
```

- 2. 获取与传入 id 匹配的视频，你必须在 `IVideoData` 接口中添加一个名为 `Get` 的新方法。该方法应该有一个名为 `id` 的 int 参数并返回视频对象。

```csharp
Video Get(int id);
```

- 3. 现在你需要在 `MockVideoData` 类中实现该方法，并返回与 `id` 参数值匹配的视频。使用 LINQ 的 `FirstOrDefault` 方法获取视频。

```csharp
public Video Get(int id)
{
    return _videos.FirstOrDefault(v => v.Id.Equals(id));
}
```

- 4. 为 `System.Linq` 命名空间添加语句。

```csharp
using System.Linq;
```

- 5. 在 `HomeController` 类的 Details action 中添加名为 `model` 的变量。使用 `Get` 方法获取与传入 id 匹配的视频并将其赋值给 `model` 变量。

```csharp
var model = _videos.Get(id);
```

- 6. 使用 `ObjectResult` 实例返回 `model` 变量以测试 Get 方法。

```csharp
return new ObjectResult(model);
```

- 7. 保存所有文件并切换到浏览器。导航到 `/Home/Details/2` URL。应该显示与 id 2 匹配的视频。

![](img/4b74569a91d8303eca7672688cf7d979_82_0.png)

### ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

- 8. 将 Details action 中的返回语句更改为返回 `View` 方法，并传递一个填充了 `model` 变量数据的 ViewModel 类实例。

```csharp
return View(new ViewModel)
{
    Id = model.Id,
    Title = model.Title,
    Genre = Enum.GetName(typeof(Genres)), model.GenreId
}
```

- 9. 在解决方案资源器的 `Views/Home` 文件夹中添加名为 `Details.cshtml` 的新 MVC 视图页面文件。

- 10. 删除 Details 视图中的所有内容。

- 11. 在标签页中输入 `html` 为视图添加 HTML 骨架。

- 12. 为视图添加单个 ViewModel 的 `@model` 指令。这使得视图能够显示关于一个视频的信息。

`@model AspNetVideoCore.Models.ViewModel`

- 13. 在 `<item>` 元素中添加文本 Video。

- 14. 在 `<body>` 元素内部为每个属性添加一个 `<div>` 元素。

```html
<div>: @Model.Id</div>
<div>Title: @Model.Title</div>
<div>Genre: @Model.Genre</div>
```

- 15. 保存所有文件并刷新到浏览器。你应该能看到与 URL 中的 id 匹配的视频数据。

![](img/4b74569a91d8303eca7672688cf7d979_83_0.png)

- 16. 更改 URL 中的 id 并确保显示正确的电影。

### ASP.NET Core 2 MVC & Razor Pages 初学者教程

- 17. 更改为一个不存在的 id。浏览器中应该显示错误。

错误的原因是如果视频不存在，Get 方法将返回 null，而视图可以处理模型的空空值。

![](img/4b74569a91d8303eca7672688cf7d979_84_0.png)

- 18. 解决此问题的方法是重定向到另一个 action；在这种情况下，Index action 是合适的。在上一个返回语句之前添加一个 `if` 语句，检查 model 是否为 null；如果是，则重定向到 Index action。实现此操作可以确保 action 不会显示错误，而是显示视频列表。

```csharp
if (model == null)
    return RedirectToAction("Index");
```

- 19. 切换到浏览器并刷新。Index 视图应该显示。

- 20. 在 Details 视图中添加指向 Index 视图的链接，以便导航回根目录。可以使用传统的 `<a>` 标签或 `ActionLink` 方法。第三种方法是使用 Tag Helpers 添加链接：`@Html.ActionLink("Home", "Index")`

- 21. 切换到浏览器并导航到 `/Home/Details/2`。视图应该有一个文本为 Home 的链接。

- 22. 现在打开 Index 视图并视频添加链接。要实现这一点，你必须传递匿名对象作为参数，并向该对象添加 `id` 属性。

```html
<td>@Html.ActionLink(video.Id.ToString(), "Details", new { id })</td>
```

- 23. 切换到浏览器并进入根目录 `/`。点击链接之一查看该视频的详情。

### ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

![](img/4b74569a91d8303eca7672688cf7d979_85_0.png)

Index 视图的完整标记：

```html
@model IEnumerable<AspNetCoreVideoCore.ViewModels.VideoViewModel>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Video</title>
</head>
<body>
<table>
    @foreach (var video in Model)
    {
        <tr>
            <td>@Html.ActionLink(video.Id.ToString(), "Details", new { id = video.Id })</td>
            <td>@video.Title</td>
            <td>@video.Genre</td>
        </tr>
    }
</table>
</body>
</html>
```

Details 视图的完整标记：

```html
@model AspNetVideoCore.ViewModels.VideoViewModel
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Video</title>
</head>
<body>
  <div>Id: @Model.Id</div>
  <div>Title: @Model.Title</div>
  <div>Genre: @Model.Genre</div>
  @Html.ActionLink("Home", "Index") />
</body>
</html>
```

Details action 的完整标记：

```csharp
public IActionResult Details(int id)
{
    var model = _videos.Get(id);

    if (model == null) return RedirectToAction("Index");

    return View(new ViewModel
    {
        Id = model.Id,
        Title = model.Title,
        Genre = Enum.GetName(typeof(Genres), model.GenreId
    });
}
```

## 添加创建视图 (Create View)

使用 Create 视图在数据源创建新记录时，必须实现两个 action 方法。第一个是使用 HTTP GET 在浏览器中渲染 Create 视图，选择需要数据的字段和控件。第二个是 HTTP POST 方法，通过 HTTP POST 请求接收客户端的数据。

从客户端提交可以通过多种方式，例如使用 JavaScript 或表单提交。在本示例中，当用户点击提交 按钮时使用表单提交回调服务器。

HTTP POST action 方法可以从发布数据的多个位置获取数据：标头、查询字符串和请求体。然后将数据与模型对象的属性（action 方法的参数）进行匹配。action 还可以处理 int 和 string 等简单类型，而无需将其封装在模型对象中。

### ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

你需要注意一种命名约定，以便正确将表单数据与模型对象的属性和其他参数匹配。规则规定表单数据中的元素名称必须与要匹配的属性名称匹配。

使用 enum 的视图的默认行为将其显示为文本字段。在本节中，你删除 Video 类的 Genre 属性，并添加一个类型为 Genres 的新属性 Genre。这使得处理 enum 数据变得更容易，特别是在处理 SQL 数据库实体模型时。

你还将将 enum 作为属性添加到名为 VideoEditModel 的新视图模型中，该模型可以在创建新视频和编辑视频时使用。

### 重构应用程序 (Refactoring the Application)

- 1. 打开 Video 类。

- 2. 删除 Genre 属性。

- 3. 在 Models 命名空间添加使用 语句以使用 Genre 枚举：`using AspNetVideoCore.Models;`

- 4. 添加类型为 Genres 的新属性并命名为 Genre。该属性将持有视频的当前类型。`public Genres Genre { get; set; }`

- 5. 打开 MockVideoData 类。

- 6. 将 Genre 属性替换为 Genre 属性并直接从枚举赋值值：`new Video { Id = 1, Genre = Models.Genres.Comedy, Title = "Shrek" },`

- 7. 打开 HomeController 类。

- 8. 找到 index action 并更改 VideoViewModel 对象中 Genre 字符串的赋值，使用 Video 对象中 Genre 属性存储的值。你可以使用 ToString 方法来获取枚举的名称：`Genre = video.Genre.ToString()`

- 9. 对 Details action 方法重复第 7 步，但使用 model 变量而不是 video 参数。

### ASP.NET Core 2.0 MVC Razor Pages 初学者教程

10. 到浏览器并刷新应用程序。它的外观和工作原理应该与之前完全相同。

修改后的 Video 类完整代码：

```csharp
public class Video {
    public int Id { get; set; }
    public string Title { get; set; }
    public Genres Genre { get; set; }
}
```

修改后的 MockVideoData 类完整代码：

```csharp
public MockVideoData() {
    videos = new List<Video> {
        new Video { Id = 1, Genre = Models.Genres.Animated, Title = "Shrek" },
        new Video { Id = 2, Genre = Models.Genres.Animated, Title = "Despicable Me" },
        new Video { Id = 3, Genre = Models.Genres.Animated, Title = "Megamind" }
    };
}
```

修改后的 HomeController 类完整代码：

```csharp
public class HomeController : Controller {
    private IVideoData _videos;
    public HomeController(IVideoData videos) {
        _videos = videos;
    }

    public ViewResult Index() {
        var model = _videos.GetAll().Select(video => {
            new ViewModel {
                Id = video.Id,
                Title = video.Title,
                Genre = video.Genre.ToString()
            }
        });
    }
}
```

### ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

```csharp
    ));
return View(model);
}
public IActionResult Details(int id)
{
    var model = _videos.Get(id);
    if (model == null) return RedirectToAction("Index");
    return View(new ViewModel)
    {
        Id = model.Id,
        Title = model.Title,
        Genre = model.Genre.ToString();
    }
}
```

### 添加 HTTP GET Create Action 和 Create View

HTTP GET Create Action 方法向浏览器返回 Create 视图，显示用于创建新视图并将表单提交到服务器的必要控件。

1. 打开 HomeController 类。

2. 添加一个名为 Create 的新操作方法，返回类型为 `IActionResult`。返回 `View` 方法。

```csharp
public IActionResult Create()
{
    return View();
}
```

3. 在解决方案资源器的 `Views/Home` 文件夹中添加一个 MVC 视图页面，并命名为 `Create.cshtml`。

4. 删除视图中的所有内容。

5. 为 `Models` 文件夹添加 `@using` 语句，以便访问选择列表的枚举定义。

```razor
using AspNetVideoCore.Models
```

6. 添加 `@model` 指令，并将 `Video` 类作为视图模型。

```razor
@model AspNetVideoCore.Entities.Video
```

7. 为了能够使用 Tag Helpers（标签辅助程序，这是向视图中添加 ASP.NET 特定标记的新方法），你必须在视图或共享文件中添加 `@addTagHelper` 指令。稍后我们将学习更多 Tag Helpers 的知识。
