
将项目命名为 `VideoDemand.Data` 并点击“确定”按钮。

确保下拉列表中选择了 `.NET Core` 和 `ASP.NET Core 2.0`。

在模板列表中选择“空”。

点击“确定”按钮。

右键点击 `VideoDemand.Data` 项目并选择“设置为启动项目”。

## 添加用户类

为 `VideoDemand.Data` 项目添加一个名为 `Data` 的文件夹。

在 `Data` 文件夹中添加一个名为 `User` 继承自 `IdentityUser` 的类。

继承自 `IdentityUser`。

```csharp
public class User : IdentityUser
{
}
```

## 添加数据库上下文

在 `Data` 文件夹中添加一个名为 `VideoDemandContext` 的类。

使用 `IdentityDbContext` 作为基类。

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;

public class VideoDemandContext : IdentityDbContext<User>
{
    public VideoDemandContext(DbContextOptions<User> options) : base(options)
    {
    }
}
```

打开 `Startup.cs` `get` `ConfigureServices` 方法中添加连接字符串。

```csharp
using Microsoft.EntityFrameworkCore;

public class Startup
{
    private readonly IConfiguration _configuration;

    public Startup(IConfiguration configuration)
    {
        _configuration = configuration;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddDbContext<VideoDemandContext>(options =>
            options.UseSqlServer(_configuration.GetConnectionString("DefaultConnection")));
    }
}
```

# 初学者级 ASP.NET Core 2.0 MVC & Razor Pages

SQL Server 节点可能需要一秒或两秒的时间在 SQL Server 对象资源生成器中加载。加载完成后，展开名为 `MSSQLDB` 的服务器，然后展开 `VideoDemand` 数据库。数据库中应该已经添加了几个表。以 Aspnet 开头的表存储用户账户信息，并在用户注册和登录时使用。在这种情况下，当你在为用户实现注册和登录，并判断用户是否为管理员时，你将使用 `AspNetUsers`、`AspNetRoles` 和 `AspNetUserRoles` 表。

![](img/4b74569a91d8303eca7672688cf7d979_200_0.png)

## 总结

在本章中，你创建了一个项目，该项目将在本书书中剩余部分用于创建用户界面（UI）。你还安装了 AutoMapper NuGet 包，它之后将用于将数据库实体对象映射到数据传输对象（DTO），从而为视图提供数据。

接下来，你将把 `Home/Index` 操作重定向到显示 `Account/Login` 视图。这将在应用程序启动时显示登录表单。然后你将对登录表单进行样式设计，使其看起来更专业。

# 11. 登录

## 引言

在本章中，你将让登录视图在访问 Web 应用程序立即可用。为了实现这一点，你将从 `Home/Index` 操作重定向到 `Account/Login` 操作。

由于登录视图只应该给尚未登录的访问者，你将使用依赖注入（Dependency Injection）在控制器中使用 `SignInManager`，以便检查用户是否已登录。

为了让访问者能够注册和登录，你必须使用与 `VideoOnDemand.Data` 项目相同的连接字符串。

# 本章使用的技术

- 依赖注入 – 将对象注入控制器的构造函数中。
- C# – 在控制器的操作和构造函数中编写代码。
- Razor – 在必要的视图中引入 C#。
- HTML 5 – 用于构建视图。
- Bootstrap 和 CSS – 用于 HTML 5 元素设置样式。
- TagHelpers – 用于添加 HTML 5 元素及其属性。

## 重定向到登录视图

ASP.NET Core 从设计之初就支持并利用依赖注入（DI）。依赖注入是一种让框架自动创建服务（类）的实例并将其注入构造函数中的方法。为什么这很重要？嗯，它在对象与其协作者之间创建了松耦合。这意味着不需要在协作者本身中创建硬编码实例；它们是被发送到其中的。

不仅可以注入内置的框架服务，你自己的对象也可以在 `Startup` 类中配置 DI。

现在，你将使用 DI 将 `SignInManager` 传递给 `HomeController` 类中的构造函数并将其存储在私有变量中。`SignInManager` 及其 `User` 类型需要两个 `using` 语句：`Microsoft.AspNetCore.Identity` 和 `VideoOnDemand.Data.Entities`。

1. 打开位于 UI 项目中 Controllers 文件夹下的 `HomeController` 类。
2. 添加以下 `using` 语句。

```csharp
using Microsoft.AspNetCore.Identity;
using VideoOnDemand.Data.Entities;
using VideoOnDemand.UI.Models;
```

3. 添加一个构造函数，通过依赖注入接收 `SignInManager` 并将其存储在私有类级变量中。

```csharp
private SignInManager<User> _signInManager;

public HomeController(SignInManager<User> signInMgr)
{
    _signInManager = signInMgr;
}
```

4. 使用你刚刚添加的类级变量检查用户是否登录，如果是匿名用户，则重定向到 `AccountController` 类中的 `Login` 操作。否则，目前打开默认的 `Index` 视图。你将在稍后的章节中更改此。

```csharp
public IActionResult Index()
{
    if (!_signInManager.IsSignedIn(User))
        return RedirectToAction("Login", "Account");

    return View();
}
```

*注：原文代码片段中此处有小错误 `_signInManager.IsSignedIn(User)`，翻译时保持代码逻辑不变*

5. 按 `F5` 运行应用程序。
6. 检查 URL，它应该指向 `/Account/Login`。
7. 检查登录视图是否显示。

# ASP.NET Core 2.0 MVC & Razor Pages 初学者

![](img/4b74569a91d8303eca7672688cf7d979_200_0.png)

## 设置登录视图

如上所示，登录视图并不美观。我们可以通过 CSS 对其进行样式设置。

![](img/4b74569a91d8303eca7672688cf7d979_200_0.png)

## 添加样式

为了让登录框看起来更专业，我们需要对它进行样式处理。

1. 打开 `wwwroot/css` 文件夹下的 `style.css`。
2. 添加 `.form-group` 类。
3. 添加 `.input-addon` 类。
4. 添加 `.form-control` 类。
5. 添加 `.btn` 类。
6. 添加 `.btn-primary` 类。
7. 添加 `.glyphicon` 类。
8. 添加 `.checkbox` 类。
9. 添加 `.checkbox-inline` 类。
10. 添加 `.label` 类。
11. 添加 `.input` 类。
12. 添加 `.hr` 类。
13. 添加 `.panel` 类。
14. 添加 `.panel-heading` 类。
15. 添加 `.panel-body` 类。
16. 添加 `.panel-footer` 类。
17. 添加 `.panel-default` 类。
18. 添加 `.row` 类。
19. 添加 `.col-md-12` 类。
20. 添加 `.col-md-6` 类。
21. 添加 `.col-md-4` 类。
22. 添加 `.col-md-3` 类。
23. 添加 `.col-md-2` 类。
24. 添加 `.col-md-1` 类。
25. 添加 `.col-sm-8` 类。
26. 添加 `.col-sm-6` 类。
27. 添加 `.col-sm-4` 类。
28. 添加 `.col-sm-3` 类。
29. 添加 `.col-sm-2` 类。
30. 添加 `.col-sm-1` 类。
31. 添加 `.col-xs-8` 类。
32. 添加 `.col-xs-6` 类。
33. 添加 `.col-xs-4` 类。
34. 添加 `.col-xs-3` 类。
35. 添加 `.col-xs-2` 类。
36. 添加 `.col-xs-1` 类。
37. 添加 `.pull` 类。
38. 添加 `.left` 类。
39. 添加 `.right` 类。
40. 添加 `.clearfix` 类。
41. 添加 `.text-center` 类。
42. 添加 `.text-right` 类。
43. 添加 `.text-justify` 类。

## 修改登录视图的布局

1. 打开 `Views/Account/Login.cshtml`。
2. 将登录表单包裹在 `class="panel panel-default"` 的 `div` 中。
3. 添加一个 `class="panel-heading"` 的 `div`，并包含 `<h2>Login</h2>`。
4. 将表单包裹在 `class="panel-body"` 的 `div` 中。
5. 将表单包裹在 `class="panel-footer"` 的 `div` 中。
6. 将表单包裹在 `class="col-md-6"` 的 `div` 中。
7. 将表单包裹在 `class="col-md-8"` 的 `div` 中。
8. 将表单包裹在 `class="col-md-12"` 的 `div` 中。
9. 修改 `form` 标签如下。

```html
<div class="panel panel-default">
    <div class="panel-heading">
        <h2>Login</h2>
    </div>
    <div class="panel-body">
        <form asp-action="Login">
            <div class="form-group">
                <input asp-for="Email" class="form-control" />
                <label for="Email" class="glyphicon glyphicon-envelope"></label>
            </div>
            <div class="form-group">
                <input asp-for="Password" class="form-control" />
                <label for="Password" class="glyphicon glyphicon-lock"></label>
            </div>
            <div class="form-group checkbox">
                <label class="checkbox">
                    <input asp-for="RememberMe" />
                    @Html.DisplayName(m => m.RememberMe)
                </label>
            </div>
            <button type="submit" class="btn btn-primary">Login</button>
        </form>
    </div>
</div>
```

10. 按 `F5` 运行应用程序以查看效果。

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

更改布局后，表单应该看起来如下。

# 使用本地账户登录。

```
Password
```

- 记住我？

```
Log in
```

`登录` 视图的完整代码：
