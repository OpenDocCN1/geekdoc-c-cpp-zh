
# 初学者 ASP.NET Core MVC & Razor Pages

```csharp
[HttpGet]
public IActionResult Edit(int id)
{
  ...
}
```

- 9. 将模型变量重命名为 `video`。
- 10. 将返回语句替换为返回 `video` 对象的视图。
`return View(video);`
- 11. 添加一个 HTTP POST 操作，包含一个 `int` 类型的 `id` 参数和一个名为 `model` 的 `VideoEditViewModel` 参数。为该操作添加 `HttpPost` 特性。

```csharp
[HttpPost]
public IActionResult Edit(int id, VideoEditViewModel model)
{
  ...
}
```

- 12. 获取与传入的 `id` 匹配的视频并将其存储在名为 `video` 的变量中。
`var video = __videos.Get(id);`
- 13. 添加一个 `if` 语句来检查模型状态是否无效或 `video` 对象是否为空。如果其中任一个为真，则返回带模型的视图。
`if (video == null || !ModelState.IsValid)`
`return View(model);`
- 14. 将模型中的 `Title` 和 `Genre` 值分配给你获取的 `video` 对象。Entity Framework 将跟踪 `video` 对象的更改。
`video.Title = model.Title;`
`video.Genre = model.Genre;`
- 15. 调用 `_Video` 上的上的 `Commit` 方法。该方法目前尚不存在，但你很快就会将其添加到 `IData` 服务类中。在你重构了 `IVideo` 服务后，该方法将能够工作并将任何更改保存到数据库中。由于 Entity Framework 会跟踪 `DbContext` 的任何更改，你不需要将 `video` 对象发送给 `Commit` 方法。
`_videos.Commit();`
- 16. 添加一个重定向到 `Details` 视图。
`return RedirectToAction("Details", new { id = video.Id });`

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

## HTTP GET Edit 操作的完整代码

```csharp
[HttpGet]
public IActionResult Edit(int id)
{
    var video = _videos.Get(id);

    if (video == null) return RedirectToAction("Index");

    return View(video);
}
```

## HTTP POST Edit 操作的完整代码

```csharp
[HttpPost]
public IActionResult Edit(int id, VideoEditViewModel model)
{
    var video = _videos.Get(id);

    if (video == null || !ModelState.IsValid) return View(model);

    video.Title = model.Title;
    video.Genre = model.Genre;

    _videos.Commit();

    return RedirectToAction("Details", new { id = video.Id });
}
```

## 重构 IVideoData 服务

其思想是，你应该能够在将更改提交到数据库之前进行多次更改并添加新视频。为了实现这一点，你必须将 `SaveChanges` 方法移动到名为 `Commit` 的独立方法。每当需要将更改持久化数据库时，必须调用 `Commit` 方法。

- 1. 打开 `IVideoData` 接口。
- 2. 定义一个名为 `Commit` 的方法，返回一个 `int`。在某些情况下，该 `int` 值反映了受提交影响的记录数。
`int Commit();`
- 3. 打开 `MockVideoData` 类并添加一个返回 `0` 的 `Commit` 方法。即使对于模拟数据来说没有必要，你也必须添加该方法。
模拟数据在内存中会即时保存。接口要求实现 `Commit` 方法。

```csharp
public int Commit()
{
    return 0;
}
```

- 4. 打开 `SqlVideoData` 类并添加一个 `Commit` 方法，返回调用 `SaveChanges` 方法的结果。

```csharp
public int Commit()
{
    return _db.SaveChanges();
}
```

- 5. 从 `Add` 方法中移除 `SaveChanges` 方法的调用。

```csharp
public void Add(Video video)
{
    _db.Add(video);
}
```

- 6. 打开 `HomeController`，验证 `Commit` 方法没有红色波浪线且运行正常。
- 7. 在 `Create` 操作中、`Add` 方法下方调用 `Commit` 方法。这是必要的，因为你已经重构了 `SqlVideoData` 服务中 `Add` 方法对 `SaveChanges` 方法的调用。
- 8. 保存所有文件并导航到根 URL。新的 `Edit` 链接应该出现在视频列表右侧，位于 `Details` 链接旁边。

![](img/4b74569a91d8303eca7672688cf7d979_131_0.png)

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

- 9. 点击其中一个视频的 `Edit` 链接打开新的 `Edit` 视图。
- 10. 对视频进行一些更改并点击 `Edit` 按钮。

![](img/4b74569a91d8303eca7672688cf7d979_132_0.png)

- 11. 显示视频的 `Details` 视图。点击 `Home` 链接返回 `Index` 视图中的视频列表。

![](img/4b74569a91d8303eca7672688cf7d979_132_1.png)

## 初学者 ASP.NET Core MVC & Razor Pages

- 12. 显示视频的 `Details` 视图。点击 `Home` 链接返回 `Index` 视图中的视频列表。

![](img/4b74569a91d8303eca7672688cf7d979_132_1.png)

## ASP.NET Core MVC & Razor Pages 初学者

- 12. 显示视频的 `Details` 视图。点击 `Home` 链接返回 `Index` 视图中的视频列表。

![](img/4b74569a91d8303eca7672688cf7d979_133_0.png)

### IVideoData 接口的代码

```csharp
interface IVideoData {
    IEnumerable<Video> GetAll();
    Video Get(int id);
    void Add(Video video);
    int Commit();
}
```

### SqlVideoData 完整代码

```csharp
public class SqlVideoData : IVideoData {
    private MyDbContext _db;
    // 类的其余部分
}
```

- 5. 从 `Add` 方法中移除 `SaveChanges` 方法的调用。

```csharp
public void Add(Video video)
{
    _db.Add(video);
}
```

- 6. 打开 `HomeController`，验证 `Commit` 方法没有红色波浪线且运行正常。
- 7. 在 `Create` 操作中、`Add` 方法下方调用 `Commit` 方法。这是必要的，因为你已经重构了 `SqlVideoData` 服务中 `Add` 方法对 `SaveChanges` 方法的调用。
- 8. 保存所有文件并导航到根 URL。新的 `Edit` 链接应该出现在视频列表右侧，位于 `Details` 链接旁边。

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

- 9. 点击其中一个视频的 `Edit` 链接打开新的 `Edit` 视图。
- 10. 对视频进行一些更改并点击 `Edit` 按钮。

# ASP.NET Core 2.0 MVC Razor Pages 初学者

## 视图组件 (View Components)

视图组件（View Component）几乎是一个完整的抽象。它是一个拥有自己的模型的部分视图，该模型是从类似控制器的类中名为 `Invoke` 的方法获取的。视图组件的模型与当前视图的模型是独立的。你不应该在 `_Layout view_` 视图模型中使用带有模型的普通视图，因为它没有模型，且很难向其引入模型。你应该使用视图组件在 `_Layout view_` 视图中渲染部分内容。

在之前的 MVC 版本中，你使用 `@Html.ActionHelper` 来执行子操作。在这一版本的 MVC 中，它已被视图组件取代。

你可以将视图组件看作是一个从不路由的控制器。

视图组件始终放置在 `Views` 文件夹下的 `Components` 文件夹中。如果你将该文件夹放在 `Views/Shared` 文件夹中，则可以在任何视图中使用它。每个视图组件在 `Components` 文件夹中都有一个与组件同名的子文件夹。

## 为 IMessageService 添加视图组件

让我们实现一个使用 `IMessageService` 在每个视图中显示配置信息的视图组件。

- 1. 在项目节点下创建一个名为 `Components` 的新文件夹。此文件夹将存放视图组件运行所需的文件。
- 2. 向文件夹中添加一个名为 `Message` 的类并继承 `ViewComponent` 类。为 `Microsoft.AspNetCore.Mvc` 命名空间添加 `using` 语句以访问 `ViewComponent` 类。
`public class Message : ViewComponent { }`
- 3. 添加一个构造函数并注入 `IMessageService` 接口，参数命名为 `message`，并将其存储在名为 `_message` 的类变量中。为 `Services` 命名空间添加 `using` 语句以访问 `IMessageService` 类。
`private IMessageService _message;`
`public Message(IMessageService message)`
`{    _message = message; }`
- 4. 添加一个名为 `Invoke` 的公共方法，返回 `IViewComponentResult`。
`public IViewComponentResult Invoke()`
`}`
- 5. 在 `Invoke` 方法中添加一个名为 `model` 的变量，用于存储调用 `_message.GetMessage` 方法的结果。
`var model = _message.GetMessage();`
- 6. 使用 `View` 方法返回该模型。由于模型是一个字符串，`View` 方法会产生混义并认为它是要渲染的视图名称。为了修复此问题，将视图名称作为第一个参数，并将模型对象作为第二个参数。
`return View("Default", model);`
- 7. 在 `Views/Shared` 文件夹内部创建一个新的 `Components` 文件夹。
- 8. 在 `Components` 文件夹内部添加名为 `Message` 的文件夹。
- 9. 在 `Message` 文件夹中添加名为 `Default` 的 MVC 页面。
- 10. 删除视图中的所有代码。
- 11. 添加类型为 `string` 的 `@model` 指令。
- 12. 添加一个 `<section>` 元素并在内部包含 `<small>` 元素。将 `@Model` 值添加到 `<small>` 元素中。
`<section>`
`<small>@Model</small>`
`</section>`
- 14. 保存所有文件。
- 15. 逐一访问所有视图，验证配置文件中的消息（Hello from configuration）是否显示在每个视图的页脚中。

# ASP.NET Core 2.0 MVC & Razor Pages 初学者

### Message 视图组件的完整代码

```
public class Message : ViewComponent
{
    private IMessageService _message;

    public Message(IMessageService message)
    {
        _message = message;
    }

    public IViewResult Invoke()
    {
        var model = _message.GetMessage();
        return View("Default", model);
    }
}
```

### Default 视图的完整标记代码

```
@model string

<section>
    <small>@Model</small>
</section>
```

### Layout 视图的完整代码

```html
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>@ViewBag.Title</title>
</head>
<body>
    <div>
        @Body
    </div>
    <footer>
        @RenderSection("footer", false)
        @await Component.InvokeAsync("Message")
    </footer>
</body>
</html>
```

## 总结

在本章中，你学习了布局视图和部分视图。你还使用了新功能，如标签辅助程序（Tag Helpers）、视图组件以及 `_ViewStart` 和 `_ViewImport` 视图。

使用这些功能允许你复用代码并将一个大视图分解为更小、更易维护的部分。它们赋予了你编写可维护和可复用代码的能力。

# 7. 表单身份验证 (Forms Authentication)

在本章中，你将学习 ASP.NET Identity 以及如何使用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。
