
`Task<bool> UpdateUser(UserModel user);`

# ASP.NET Core 2.0 MVC & Razor Pages

该方法的第一件事是根据传入参数的 id 获取用户，并将其存储在名为 `dbUser` 的变量中。

```csharp
var dbUser = await _db.Users.FirstOrDefaultAsync(u => u.Equals(user.Id));
```

如果 `dbUser` 为（用户不存在）或传入参数中的电子邮箱为空字符串，则返回 `false`。

```csharp
if (dbUser == null) return false;
if (string.IsNullOrEmpty(user.Email)) return false;
```

将传入用户的地址分配给获取到的 `dbUser`。

```csharp
dbUser.Email = user.Email;
```

使用管理员角色的 id 和传入用户的 id 创建 `IdentityRole<string>` 类的新实例。将该对象存储在名为 `role` 的变量中。你将使用该对象来判断用户是否已经是管理员。

```csharp
var role = new IdentityRole<string>() {
    RoleId = "1",
    UserId = user.Id
};
```

通过在 `UserRoles` 实体上使用 `AnyAsync` 方法查询 `AspNetUserRoles` 表，并传入你之前创建的 `role` 对象，以查找该用户是否为管理员。

```csharp
var isAdmin = await _db.UserRoles.AnyAsync(ur => ur.Equals(role));
```

添加一个 `if/else` 块：如果 UI 中未勾选管理员复选框，或者如果勾选则添加管理员角色。

```csharp
if (isAdmin && !user.IsAdmin)
    _db.UserRoles.Remove(role);
else if (!isAdmin && user.IsAdmin)
    await _db.UserRoles.AddAsync(role);
```

调用 `SaveChangesAsync` 方法来持久化更改并等待结果。如果数据已持久化则返回 `true`，否则返回 `false`。

1. 打开 `IUserService` 接口。
2. 为 `UpdateUser` 方法添加定义，返回 `bool` 并有一个 `UserModel` 参数。
3. 手动或使用快速操作小灯泡将 `UpdateUser` 方法添加到 `UserService` 类中。如果你自动生成了方法，必须删除 `throw` 语句。
4. （逻辑见上文）

调用 `SaveChangesAsync` 方法来持久化更改并等待结果。如果数据已持久化则返回 `true`，否则返回 `false`。

## ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

目前 `IUUserService` 接口的代码如下：

```cs
public interface IUUserService {
    IEnumerable<UserPageModel> GetUsers();
    UserUserModel GetUser(string userId);
    Task<IdentityResult> AddUser(RegisterUserModel user);
    Task<bool> UpdateUser(UserUserModel user);
}
```

`UpdateUser` 方法的完整代码：

```cs
public async Task<bool> UpdateUser(UserUserModel user) {
    var dbUser = await _db.Users.FirstOrDefaultAsync(u => u.Id.Equals(user.Id));
    if (dbUser == null) return false;
    if (string.IsNullOrEmpty(user.Email)) return false;
    dbUser.Email = user.Email;
    var userRole = new IdentityRole<string>() {
        RoleId = "1",
        UserId = user.Id
    };
    var isAdmin = await _db.UserRoles.AnyAsync(ur => ur.Equals(userRole));
    if (isAdmin && !user.IsAdmin) {
        _db.UserRoles.Remove(userRole);
    } else if (!isAdmin && user.IsAdmin) {
        await _db.UserRoles.AddAsync(userRole);
    }
    var result = await _db.SaveChangesAsync();
    return result >= 0;
}
```

### DeleteUser 方法

`DeleteUser` 方法将异步从 `AspNetUsers` 表中删除用户，并根据 `_db` 上下文调用 `SaveChangesAsync` 方法返回的结果返回一个 `bool` 值。该方法应接受一个名为 `userId` 的 `string` 参数来表示该用户。

```cs
Task<bool> DeleteUser(string userId);
```

该方法的第一件事是从 `AspNetUsers` 表中获取与 `userId` 参数值匹配的用户。将该用户存储在名为 `dbUser` 的变量中。

然后，应该检查 `dbUser` 是否为 `null` 以确保用户存在，如果不存在则返回 `false`。

接下来，你需要在删除 `AspNetUserRoles` 表中与该用户关联的角色。使用 `UserRoles` 实体上的 `Where` LINQ 方法获取角色，并通过调用 `UserRoles` 实体上的 `RemoveRange` 方法删除该用户现有的任何角色。

然后，通过调用 `User` 实体上的 `Remove` 方法从 `AspNetUsers` 表中删除用户。

然后 `await` 来自 `SaveChangesAsync` 方法的结果，如果更改已持久化到数据库则返回 `true`，否则返回 `false`。

1. 打开 `IUserService` 接口。
2. 为 `DeleteUser` 方法添加方法定义，其返回 `bool` 并带有一个名为 `userId` 的 `string` 参数。
   `Task<bool> DeleteUser(string userId);`
3. 向 `UserService` 类中添加 `DeleteUser` 方法，可以手动添加，也可以使用 `Quick Actions`（快速操作）小按钮。如果你使用 `Quick Actions` 生成方法，必须记住加上 `throw` 语句。
4. 添加一个 try-catch 块，其中 catch 块返回 `false`。
5. 在 try 块中根据传入的 `userId` 参数获取与用户 匹配的用户。
   `var dbUser = await _db.Users.FirstOrDefault(d => d.Equals(userId));`
6. 如果 `dbUser` 为 `null`（用户不存在），则返回 `false`。
   `if (dbUser == null) return false;`
7. 获取与用户 ID 关联的角色并从 `AspNetUserRoles` 表中删除它们。
   `var userRoles = _db.UserRoles.Where(ur => ur.UserId.Equals(dbUser.Id));`
   `_db.UserRoles.RemoveRange(userRoles);`
8. 从 `AspNetUsers` 表中删除用户。
   `_db.Users.Remove(dbUser);`
9. 调用 `SaveChanges` 将更改持久化到数据库并等待结果。如果数据已持久化，则返回 true，否则返回 false。
   `var result = await _db.SaveChangesAsync();`
   `return result >= 0;`
10. 保存所有文件。

`IUserService` 接口的完整代码：

```cs
public interface IUserService {
    IEnumerable<UserPageModel> GetUsers();
    UserModel GetUser(string userId);
    Task<Identity> AddUser(RegisterPageModel user);
    Task<bool> Update(UserPageModel user);
    Task<bool> DeleteUser(string userId);
}
```

`DeleteUser` 方法的完整代码：

```cs
public async Task<bool> DeleteUser(string userId) {
    try {
        var dbUser = await _db.Users.FirstOrDefaultAsync(d => d.Id.Equals(userId));
        if (dbUser == null) return false;
        var userRoles = _db.UserRoles.Where(ur => ur.UserId.Equals(dbUser.Id));
        _db.UserRoles.RemoveRange(userRoles);
        _db.Users.Remove(dbUser);
        var result = await _db.SaveChangesAsync();
        if (result < 0) return false;
    }
    catch {
      return false;
    }
    return true;
}
```

#### 总结

在本章中，你创建了一个处理用户和角色的服务。你使用了 `DeleteUser` 方法从 `AspNetUsers` 表中删除用户。接下来，你将在下一章中学习如何显示状态消息。

### TempData 属性

`[TempData]` 属性是 ASP.NET Core 2.0 中的新功能，可以与控制器中的属性一起用于存储数据直到被读取。它在重定向时特别有用，当数据需要跨多个请求使用时。可以使用 `Keep` 和 `Peek` 方法在不删除的情况下检查数据。

后台代码（code-behind）的工作方式类似于控制器和模型的结合。如果需要，你可以使用控制器处理不需要 Razor Page 的请求，例如注销用户。

##### 本章使用的技术

- `C#` – 用于编写代码
- `HTML` – 用于显示内容
- `Entity Framework` – 执行 CRUD 操作

##### 概述

在本章中，你创建了一个处理用户和角色的服务。你使用了 `DeleteUser` 方法从 `AspNetUsers` 表中删除用户。接下来，你将在下一章中学习如何显示状态消息。

`[TempData]` 属性构建在会话状态（session state）之上，因此它可以在 Razor Pages 之间共享。当你从一个 Razor Page 向另一个 Razor Page 发消息时，可以利用这一点，并使用将在下一章实现的 `<status-message>` Tag Helper 来显示它。

### Users/Index Razor 页面

`Users` 文件夹下的 `Index` Razor 页面可以被视为用户仪表板，以表格形式列出用户，并包含有关用户的数据以及删除每个用户的按钮。它在 HTML 表格上方还有一个“创建新”按钮，用于在 `AspNetUsers` 数据库中创建新用户。

### 初学者 ASP.NET Core 2 MVC & Razor Pages

当你添加完所有页面后，`Users` 文件夹中将会有四个 Razor Pages：`Index`（索引）、`Create`（创建）、`Edit`（编辑）和 `Delete`（删除）。

为了添加、读取和修改用户数据，需要将 `IService` 服务注入到 Razor 页后端代码 `IndexModel` 类的构造函数中，并存储在名为 `_userService` 的私有字段中。

#### 修改 IndexModel 类

你想要的第一件事是使用 `[Authorize]` 特性将使用权限限制为管理员。

然后，你需要将 `UserService` 注入到你添加到类的构造函数中。将服务实例存储在名为 `_userService` 的私有类级变量中。

接着在 `OnGet` 方法中通过 `_userService` 对象的 `GetUsers` 方法获取所有用户，并将它们存储在名为 `Users` 的 `IEnumerable<PageModel>` 集合中；该集合将是 HTML Razor 页模型的一部分。

添加一个名为 `StatusMessage` 的 `string` 属性，并用 `[TempData]` 特性对其进行装饰。当获得成功结果（例如添加新用户）时，该属性将从其他 Razor 页获取值。

- 1. 在 `Pages` 文件夹中创建一个名为 `Users` 的文件夹。
- 2. 添加一个 Razor Page，使用同名的模板，并命名为 `Index`。
- 3. 展开解决方案管理器中的 `Index` 节点并打开 `Index.cshtml.cs` 文件。
- 4. 为类添加 `[Authorize]` 特性，并指定从浏览器访问该页面需要 `Admin` 角色。
```csharp
[Authorize](Roles = "Admin")
public class IndexModel : PageModel
```
- 5. 将 `IUserService` 注入构造函数并将注入的对象保存到类级变量 `_userService` 中。该变量将允许你从类中的任何方法访问该服务。
```csharp
private IUserService _userService;
public IndexModel(IUserService userService)
{
  _userService = userService;
}
```
- 6. 添加一个名为 `Users` 的 `IEnumerable<PageModel>` 类列表变量。
```csharp
public IEnumerable<PageModel> Users = new List<PageModel>();
```
- 7. 在 `OnGet` 方法中调用 `_userService` 对象的 `GetUsers` 方法，并将结果存储在你刚刚添加的 `Users` 属性中。
```csharp
public void OnGet()
{
  Users = _userService.GetUsers();
}
```
- 8. 添加一个名为 `ErrorMessage` 的公共属性并用 `[TempData]` 特性进行装饰。当获得成功结果（例如添加新用户）时，该属性将从其他 Razor 页获取值。
```csharp
[TempData]
public string StatusMessage { get; set; }
```
- 9. 保存所有文件。

`Index` 后端文件中的完整代码：

```csharp
[Authorize](Roles = "Admin")
public class IndexModel : PageModel
{
  private IUserService _userService;
  public IEnumerable<PageModel> Users = new List<PageModel>();
  [TempData]
  public string StatusMessage { get; set; }
  public IndexModel(IUserService userService)
  {
    _userService = userService;
  }
  public void OnGet()
  {
    Users = _userService.GetUsers();
  }
}
```

#### 修改 Index Razor 页

首先向 Identity 和 Entities 命名空间添加 using 语句，并注入 `SignInManager` 以确保用户拥有正确的凭据。

使用 `ViewData` 对象添加一个文本为 `Users` 的 `Title`（标题）属性。此值将显示在浏览器的标签页上。

添加一个 if 块来检查用户已登录并属于 `Admin` 角色。其余代码应放在该 if 块内，以便只有管理员可见。
