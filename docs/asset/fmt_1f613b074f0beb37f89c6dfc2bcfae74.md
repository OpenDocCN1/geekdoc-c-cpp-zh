
ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

ASP.NET Identity 是一个框架，你可以用它来实现应用程序中的注册和登录。你将从零开始添加身份验证，以学习所有组件是如何组合在一起的。

ASP.NET Identity 框架。ASP.NET Identity。

# 初学者 ASP.NET Core 2.0 MVC Razor Pages

2. 打开 `VideoDbContext` 并将其改为 `IdentityDbContext` 类，而不是 EF 默认的 `DbContext`。你可以指定它应该存储的用户类型，在此例中，即你刚刚添加的 `User` 实体类。

`IdentityDbContext` 类位于

```csharp
Microsoft.AspNetCore.Identity.EntityFrameworkCore 命名空间。
public class VideoDbContext : IdentityDbContext<User>
{
    ...
}
```

3. 打开 `Startup` 类并添加 `using` 语句以访问 `User` 和 `Identity` 命名空间，然后找到 `ConfigureServices` 方法。

```csharp
using AspNetCore.Entities;
using Microsoft.AspNetCore.Identity;
```

4. 通过调用 `AddIdentity` 方法将 Identity 服务添加到服务集合中。该方法接受两个泛型参数：第一个是你想要使用的用户，即你刚刚添加的 `User` 实体类，第二个是你想要使用的 Identity 角色，内置的 `IdentityRole` 类。如果你想实现自己的身份角色行为，可以让另一个类继承 `IdentityRole` 类。将该服务添加到 `AddMvc` 方法调用上方。

```csharp
services.AddIdentity<User, IdentityRole>();
```

5. 你还必须安装 Entity Framework Stores 服务来处理针对数据库的用户创建和验证。你需要向它提供 `VideoDbContext`，以便它知道与数据库通信时使用哪个上下文。你可以使用 Fluent API 在 `AddIdentity` 方法上调用 `AddEntityFrameworkStores`。

```csharp
.AddEntityFrameworkStores<User, IdentityRole, VideoDbContext>();
```

6. 接下来，你需要在 `Configure` 方法中安装中间件组件。中间件的位置非常重要。如果你将其放在管道中太靠后的位置，它将永远不会执行。将其放在 MVC 中间件上方，以便 MVC 框架可以使用。

```csharp
app.UseAuthentication();
```

7. 使用 `Ctrl+Shift+B` 构建应用程序，以确保其构建正确。

# 初学者 ASP.NET Core 2. MVC & Razor Pages

完整的 `User` 类：

```csharp
public class User : IdentityUser
{
}
```

`IdentityUser` 类中的属性：

```csharp
public class IdentityUser<TKey> where TKey : IEquatable<TKey>
{
    public IdentityUser();
    public virtual IdentityUser(string username);
    public virtual DateTimeOffset Lockout { get; set; }
    public virtual bool TwoFactorEnabled { get; set; }
    public virtual bool PhoneNumberConfirmed { get; set; }
    public virtual string PhoneNumber { get; set; }
    public virtual string CurrencyStamp { get; set; }
    public virtual string SecurityStamp { get; set; }
    public virtual string PasswordHash { get; set; }
    public virtual bool EmailConfirmed { get; set; }
    public virtual string Email { get; set; }
    public virtual string NormalizedEmail { get; set; }
    public virtual string UserName { get; set; }
    public virtual TKey Id { get; set; }
    public virtual bool LockEnabled { get; set; }
    public virtual int AccessFailedCount { get; set; }
    public override string ToString();
}
```

# 创建 AspNet Identity 数据库表

现在配置已经完成，是时候创建一个新的迁移 `migration`，以将必要的 AspNet identity 表添加到数据库中了。

- 打开包管理器控制台 `Package Manager Console` 并执行以下命令来创建必要的迁移文件：`add-migration IdentityTables`
- 执行以下命令在数据库中创建身份表：`update-database`
- 打开 SQL Server 对象资源管理器 `SQL Server Object Explorer`，并展开你的 `VideoDB` 数据库中的表。

# 初学者 ASP.NET Core MVC & Razor Pages

![](img/4b74569a91d8303eca7672688cf7d979_147_0.png)

## 用户注册

现在所有配置和数据库表创建都已完成，是时候关注用户如何注册该网站了。

如果你按照目前的状态运行应用程序，Identity 中间件将重定向到 `/Account/Login` URL，该 URL 尚不存在。相反，下一个中间件将处理该请求，浏览器将显示消息 *Hello from configuration*。

要显示登录视图 `Login view`，你必须添加一个带有 `Login` 动作的 `AccountController` 类。为了登录，用户需要注册。因此，你必须在 `AccountController` 类中实现一个 `Register` 动作。

- 1. 在 `Controllers` 文件夹中添加名为 **AccountController** 的类，并继承位于 `Microsoft.AspNetCore.Mvc` 命名空间中的 `Controller` 类。

```csharp
public class AccountController : Controller
{
}
```

# 初学者 ASP.NET Core 2 MVC & Razor Pages

- 2. 为该类添加一个 HTTP GET 动作。视图不需要接收带有数据的模型，因为用户将在视图中提供所有信息。

```csharp
[HttpGet]
public IActionResult Register()
{
    return View();
}
```

- 3. 在 `Views` 文件夹中添加一个名为 `RegisterViewModel` 的类。这将将是 Register 视图的模型。

- 4. 添加对 `System.ComponentModel.DataAnnotations` 的 `using` 语句以获取必要的属性。

- 5. 添加一个名为 `Username` 的字符串，它是必填的且最大长度为 255 个字符。长度由 Identity 表可以存储的用户名的最大字符数决定。

```csharp
[Required, MaxLength(255)]
public string Username { get; set; }
```

- 6. 添加一个名为 `Password` 的字符串属性，它是必填的且具有 `Password` 类型。

```csharp
[Required, DataType(Password)]
public string Password { get; set; }
```

- 7. 添加一个名为 `ConfirmPassword` 的字符串属性，它是必填的且具有 `Compare` 属性。使用 `nameof(Password)` 将其与其进行比较。

```csharp
[Required, Compare(nameof(Password))]
public string ConfirmPassword { get; set; }
```

- 8. 在 `Views` 文件夹中添加一个 `Account` 文件夹。

- 9. 在 `Account` 文件夹中添加一个 `Register` 视图。

- 10. 在视图中添加内容。

- 11. 添加 `@model RegisterViewModel` 指令。

```razor
@model RegisterViewModel
```

- 12. 使用 `ViewBag` 设置 Register 标题。

```razor
@{ ViewBag.Title = "Register"; }
```

# ASP.NET Core 2.0 MVC Razor Pages

- 13. 添加一个 `<h1>` 标题。

- 14. 添加一个 `<form>` 表单。

```razor
<form asp-action="Register" method="post">
```

- 15. 添加一个 `<div>` 用于显示验证摘要 `validation summary`。

```razor
<div asp-validation-summary="Model"></div>
```

- 16. 添加一个 `<label>` 标签。

```razor
<label asp-for="Username"></label>
```

- 17. 添加一个 `<input>` 输入框。

```razor
<input asp-for="Username" />
```

- 18. 添加一个 `<label>` 标签。

```razor
<label asp-for="Password"></label>
```

- 19. 添加一个 `<input>` 输入框。

```razor
<input asp-for="Password" />
```

- 20. 添加一个 `<label>` 标签。

```razor
<label asp-for="ConfirmPassword"></label>
```

- 21. 添加一个 `<input>` 输入框。

```razor
<input asp-for="ConfirmPassword" />
```

- 22. 添加一个提交按钮。

```razor
<button type="submit">Register</button>
```

# ASP.NET Core 2.0 MVC & Razor Pages

- 23. 添加 `Entities` 和 `Identity` 命名空间的 `using` 语句以访问 `User`、`UserManager` 和 `SignInManager` 类。

- 24. 在 `if` 语句下方创建一个 `User` 类的实例，并将传递的 `model` 赋值给属性。

```csharp
var user = new User { Username = model.Username };
```

- 25. 为了处理用户实体，你需要通过构造函数引入 `UserManager`。为控制器添加构造函数并注入上述两个类。

```csharp
private UserManager<User> _userManager;
private SignInManager<User> _signInManager;

public AccountController(UserManager<User> userManager, SignInManager<User> signInManager)
{
    _userManager = userManager;
    _signInManager = signInManager;
}
```

- 26. 接下来你想在 HTTP POST Register 动作中使用 `UserManager` 创建新用户。将结果保存在名为 `result` 的变量中。

```csharp
var result = await _userManager.CreateAsync(user, model.Password);
```

- 27. 如果用户创建成功，你想自动登录该用户。使用 `result` 变量上的 `Created` 属性检查用户是否创建成功，并使用 `SignInAsync` 方法登录用户。方法的第二个参数决定 Cookie 是否持久会话。

```csharp
if (result.Created)
{
    await _signInManager.SignInAsync(user, false);
    return RedirectToAction("Index", "Home");
}
```

- 28. 如果用户未创建成功，你想将错误添加到 `ModelState` 对象中，以便作为模型错误发送到客户端并在验证摘要中显示。

```csharp
else
{
    foreach (var error in result.Errors)
        ModelState.AddModelError("", error.Description);
}
```

# 初初学者 ASP.NET Core MVC & Razor Pages

29. 在 `else` 块下方返回视图。

```csharp
return View();
```

30. 保存所有文件并导航到 `/Account/Register` URL。应该显示 Register 视图。用三个字母的密码填写表单，并点击 Register 按钮。验证摘要应该显示在 `Register` 动作中循环到 `ModelState` 对象的错误。

![](img/4b74569a91d8303eca7672688cf7d979_151_0.png)

- 密码长度至少为 6 个字符。
- 密码至少包含一个非字母数字字符 `'a'-'z'`。
- 密码至少包含一个小写字母 `'a'-'z'`。
- 密码至少包含一个大写字母 `'A'-'Z'`。

用户名 Jonas

密码

确认密码

注册

来自配置的问

31. 填写表单 `这次使用正确信息`。你应该通过 `Register` 动作中的 `RedirectToAction` 方法重定向到 Index 视图。

32. 在 SQL Server 对象资源管理器中查看 `AspNetUsers` 表中的数据，以验证用户已注册。

| dbo.AspNetUsers [Data] | Id | PasswordHash | UserName |
| :--- | :--- | :--- | :--- |
| 9d1cc0a0-5a8-... | AQAAAAAEA... | Jonas |
| NULL | NULL | NULL |

# 初初学者 ASP.NET Core 2. MVC & Razor Pages

`RegisterViewModel` 类的完整代码：

```csharp
public class RegisterViewModel
{
    [Required, MaxLength(255)]
    public string Username { get; set; }
    [Required, DataType(DataType.Password)]
    public string Password { get; set; }
    [Required, DataType(DataType.Password), Compare(nameof(Password))]
    public string ConfirmPassword { get; set; }
}
```

`AccountController` 类的完整代码：
