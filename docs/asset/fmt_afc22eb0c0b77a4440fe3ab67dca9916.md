
```csharp
_db.Set<TEntity>().Add(updatedItem);

return await _db.SaveChangesAsync() >= 0;
}
catch
{
    return false;
}
}
```

## 总结

在本章中，你创建了一个用于向数据库写入数据的服务。该服务将从 **Admin** 项目中使用以获取数据。

接下来，你将添加一个用户服务，该服务将从 **Admin** 项目中使用以管理 **AspNetUsers** 表中的用户以及 **AspNetUserRoles** 表中的角色。

## 29. 用户服务 (User Service)

### 引言

在本章中，你将在 **Admin** 项目中创建一个名为 **UserService** 的服务。该服务将用于管理 **AspNetUsers** 表中的用户以及 **AspNetUserRoles** 表中的角色。由于这是一个通过依赖注入注入的服务，因此你需要为它创建一个接口。

### 本章使用的技术

1. **C#** – 用于创建服务。
2. **Entity framework** – 用于与数据库中的表交互。
3. **LINQ** – 用于查询数据库表。

### 概述

你的目标是创建一个数据服务，对 **AspNetUsers** 和 **AspNetUserRoles** 数据库表执行添加、更新和删除操作。

### 添加 UserService 服务

你需要在 Admin 项目中名为 `Services` 的文件夹下添加名为 `IUserService` 的接口。然后，你需要在名为 **UserService** 的类中实现该接口，并编写访问数据库的代码。

这些方法不会实现为泛型方法，因为它们仅用于 **AspNetUsers** 和 **AspNetUserRoles** 数据库表。

### UserPageModel 类

该类将把从数据库获取的数据传输到 **User** CRUD Razor Pages。它将包含三个属性：第一个是 **Id (string)**，表示用户 ID。它应该用 **[Required]** 和 **[Display]** 特性修饰；第一个属性要求输入 ID，第二个属性将标签文本更改为 *User Id*。第二个属性是 **Email (string)**。它应该用 **[Required]** 和 **[EmailAddress]** 特性修饰；第一个属性要求输入地址，第二个属性将对输入的数据进行检查以确保其为有效的电子邮件地址。第三个属性是 IsAdmin(bool)，它将具有与 Id 属性相同的特性。它将以复选框的形式显示，显示用户是否已被分配 Admin 角色。

#### 添加 User 类

1. 在 Admin 项目中创建一个名为 Models 的新文件夹（如果它不存在）。
2. 在 Models 文件夹中添加一个名为 UserPageModel 的类。
3. 添加一个名为 Id (string) 的属性。
4. 添加 [Required] 和 [Display] 特性。[Display] 特性应将文本更改为 User id。
   `[Required]`
   `[Display(Name = "User Id")]`
   `public string Id { get; set; }`
5. 添加一个名为 Email (string) 的属性。
6. 添加 [Required] 和 [EmailAddress] 特性。
7. 添加一个名为 IsAdmin(bool) 的属性。
8. 添加 [Required] 和 [Display] 特性。[Display] 特性应将文本更改为 Is Admin。
9. 保存类。

UserPageModel类的完整代码：

```csharp
public class UserPageModel
{
    [Required]
    [Display(Name = "User Id")]
    public string Id { get; set; }

    [Required]
    [EmailAddress]
    public string Email { get; set; }

    [Required]
    [Display(Name = "Is Admin")]
    public bool IsAdmin { get; set; }
}
```

#### 添加服务接口和类

1. 打开 VideoOnDemand.Admin 项目。
2. 添加一个名为 Services 的新文件夹。
3. 向文件夹添加一个名为 IUserService 的接口。
4. 向 Services 文件夹添加一个名为 UserService 的类。
5. 实现 UserService 的构造函数以注入 DbContext 和 UserManager。
6. 在 UserService 类中实现 GetUsers 方法。
7. 在 UserService 类中实现 GetUser 方法。
8. 在 Startup.cs 文件中注册服务。
9. 保存文件。

到目前为止 IUserService 接口的代码：

```csharp
public interface IUserService
{
    IEnumerable<UserPage> GetUsers();
    UserPage GetUser(string userId);
}
```

到目前为止 UserService 类的代码：

```csharp
public class UserService : IUserService
{
    private readonly MyDbContext _db;
    private readonly UserManager<Identity> _userManager;
    public UserService(MyDbContext db, UserManager<Identity> userManager)
    {
        _db = db;
        _userManager = userManager;
    }
    public IEnumerable<UserPage> GetUsers()
    {
        return from user in _db.Users
            orderby user.Email
            select new UserPage
            {
                Id = user.Id,
                Email = user.Email,
                IsAdmin = _db.UserRoles.Any(ur =>
                    ur.UserId.Equals(user.Id) &&
                    ur.RoleId.Equals(1.ToString()))
            };
    }
    public UserPage GetUser(string userId)
    {
        var user = _db.Users.Find(userId);
        if (user == null) return null;
        return new UserPage
        {
            Id = user.Id,
            Email = user.Email,
            IsAdmin = _db.UserRoles.Any(ur =>
                ur.UserId.Equals(user.Id) &&
                ur.RoleId.Equals(1.ToString()))
        };
    }
}
```

### 初学者 ASP.NET Core 2.0 MVC Razor Pages

4. 返回将传入的 user id 转换为 `UserUserModel` 对象的用户。在 `AspNetUserUserRoles` 上使用 `Any` LINQ 方法判断该用户是否为管理员。

```csharp
return (from user in db.Users
where user.Id.Equals(userId)
select new UserPageModel
{
    Id = user.Id,
    Email = user.Email,
    IsAdmin = _db.UserRoles.Any(ur =>
        ur.RoleId.Equals(user.Id) &&
        ur.RoleId.Equals(1.ToString())
}).FirstOrDefault();
```

5. 保存所有文件。

目前 `IUserService` 接口的代码为：

```csharp
public interface IUserService
{
    IEnumerable<UserPageModel> GetUsers();
    UserPageModel GetUser(string userId);
}
```

`GetUser` 方法的完整代码：

```csharp
return (from user in db.Users
where user.Id.Equals(userId)
select new UserPageModel
{
    Id = user.Id,
    Email = user.Email,
    IsAdmin = _db.UserRoles.Any(ur =>
        ur.RoleId.Equals(user.Id) &&
        ur.RoleId.Equals(1.ToString())
}).FirstOrDefault();
```

### 初学者 ASP.NET Core 2.0 MVC & Razor Pages

#### RegisterUserModelPage 类

`RegisterUserModel` 类用于为 `AspnetUsers` 表创建 Razor 页面。该类应包含名为 `Email`、`Password` 和 `ConfirmPassword` 的字符串属性。这些属性应该使用有助于客户端验证的特性进行标记。

`Email` 和 `Password` 属性应该标记为 `[Required]` 属性。

`Email` 属性还应该标记为 `[EmailAddress]` 属性。

`Password` 属性应该格式化为密码，并且最大长度为 100 个字符。

`ConfirmPassword` 属性应该格式化为密码，并使用 `[Compare]` 属性与 `Password` 属性的内容进行比较。

1. 在 Models 文件夹中添加名为 `RegisterUserModel` 的类。
2. 添加一个带有 `[Required]` 和 `[EmailAddress]` 标记的 `Email` (string) 属性。
```csharp
[Required]
[EmailAddress]
public string Email { get; set; }
```
3. 添加一个带有 `[Required]`、`[StringLength]` 和 `[DataType]` 特性的 `Password` (string) 属性。
```csharp
[Required]
[StringLength(100, ErrorMessage = "The {0} 必须至少为 {2} 个字符，最多为 {1} 个字符。", MinimumLength = 6)]
[DataType(DataType.Password)]
public string Password { get; set; }
```
4. 添加一个带有 `[Display]`、`[Compare]` 和 `[DataType]` 特性的 `ConfirmPassword` (string) 属性。
```csharp
[DataType(DataType.Password)]
[Display(Name = "Confirm password")]
[Compare("Password", ErrorMessage = "The password and confirmation password do not match.")]
public string ConfirmPassword { get; set; }
```
5. 保存所有文件。

### 初学者 ASP.NET Core 2 MVC & Razor Pages

`RegisterUserPageModel` 类的完整代码：

```csharp
public class RegisterUserPageModel
{
    [Required]
    [EmailAddress]
    [Display(Name = "Email")]
    public string Email { get; set; }

    [Required]
    [StringLength(100, ErrorMessage = "The {0} 必须至少为 {2} 个字符，最多为 {1} 个字符。", MinimumLength = 6)]
    [DataType(DataType.Password)]
    [Display(Name = "Password")]
    public string Password { get; set; }

    [DataType(DataType.Password)]
    [DisplayName(Name = "Confirm password")]
    [Compare("Password", "The password and confirmation password do not match.")]
    public string ConfirmPassword { get; set; }
}
```

### AddUser 方法

`AddUser` 方法将异步在 `AspNet` 表中添加新用户，并返回从 `UserManager` 对象的 `Create` 方法返回的 `IdentityResult` 对象。该方法应接受一个名为 `user` 的 `RegisterUserPageModel` 实例作为参数。

```csharp
Task<IdentityResult> AddUser(RegisterUserPageModel user);
```

1. 打开 `IUserService` 接口。
2. 为 `AddUser` 方法添加定义，返回 `Task<IdentityResult>` 并有一个 `user` (RegisterUserPageModel) 参数。
3. 手动或使用快速操作小灯泡将 `AddUser` 方法添加到 `UserService` 类中。如果你生成了方法，必须删除 `throw` 语句。
4. 创建 `User` 类的实例，并将传入的用户对象的电子邮箱分配给新创建的 `User` 对象。同时，将 `EmailConfirmed` 属性赋值为 `true`，以表示已收到电子邮件确认。虽然在此场景中不是严格的，但如果你以后选择实现电子邮件验证，这可能是关重要的。

```csharp
var dbUser = new User { Username = user.Email, Email = user.Email, EmailConfirmed = true };
```

5. 调用 `_userManager` 实例上的 `CreateAsync` 方法来添加新用户。将结果存储在名为 `result` 的变量中。由于这是一个异步方法，你必须使用 `await` 关键字调用该方法。

```csharp
var result = await _userManager.CreateAsync(dbUser, user.Password);
```

6. 从方法返回 `result` 变量中的结果。

```csharp
return result;
```

7. 保存所有文件。

`IUserService` 接口的代码为：

```csharp
public interface IUserService
{
    IEnumerable<UserPageModel> GetUsers();
    UserPageModel GetUser(string userId);
    Task<IdentityResult> AddUser(RegisterUserUserModel user);
}
```

`AddUser` 方法的完整代码：

```csharp
public async Task<IdentityResult> AddUser(RegisterUserUserModel user)
{
    var dbUser = new User { Username = user.Email, Email = user.Email, EmailConfirmed = true };
    var result = await _userManager.CreateAsync(dbUser, user.Password);
    return result;
}
```

### UpdateUser 方法

`UpdateUser` 方法将在 `AspNet` 表中更新用户，并根据对上下文的 `SaveChanges` 调用返回一个 `bool`。该方法应接受一个名为 `user` 的 `UserModel` 参数。
