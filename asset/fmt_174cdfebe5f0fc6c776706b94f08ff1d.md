
<span asp-validation-for="Input.IsAdmin" class="text-danger"></span>
</div>
```
- 5. 将第二个 form-group 的元素改为 `Input.IsAdmin` 属性。
- 6. 移除第三个 form-group 及其内容。
- 7. 将提交按钮的文本改为 Save。

Edit Razor Page 的完整代码：

```html
@page
@using Microsoft.AspNetCore.Identity
@using VideoDemand.Data.Entities
@inject SignInManager<User> SignInManager
@model EditModel
@{
    ViewData["Title"] = "Edit User";
}
@if (SignInManager.IsSignedIn(User) && User.IsInRole("Admin"))
<div class="row">
  <div class="col-md-4 col-md-offset-4">
    <h2>@ViewData["Title"]</h2>
    <page-button path="Users/Index" Bootstrap-style="primary" glyph="info-sign" description="返回列表"></page-button>
    <page-button path="Index" Bootstrap-style="warning" glyph="list-alt" description="仪表板"></page-button>
    <p></p>
    <form method="post">
      <div asp-validation-summary="All" class="text-danger"></div>
      <input type="hidden" asp-for="Input.Id" />
      <div class="form-group">
        <label asp-for="Input.Email"></label>
        <input asp-for="Input.Email" class="form-control" />
        <span asp-validation-for="Input.Email" class="text-danger"></span>
      </div>
      <div class="form-group">
        <label asp-for="Input.IsAdmin"></label>
        <input asp-for="Input.IsAdmin" class="form-control" />
        <span asp-validation-for="Input.IsAdmin" class="text-danger"></span>
      </div>
      <button type="submit" class="btn btn-success">Save</button>
    </form>
  </div>
</div>
@section Scripts {
  await Html.PartialAsync("_ValidationScriptsPartial")
}
```

# Users/Delete Razor Page

此 Razor Page 将显示用户信息以及删除用户的按钮。你将复制 Edit 页面并进行修改。

![](img/4b74569a91d8303eca7672688cf7d979_475_0.png)

### 修改 DeleteModel 类及其后代码文件

- 1. 将 Edit 复制到相同文件夹，重命名为 Delete。
- 2. 打开 `.cshtml` 文件。
- 3. 将类和构造函数改为 `DeleteModel`。
- 4. 在 `OnPostAsync` 方法中，将对 Update 方法的调用替换为对 DeleteUser 方法的调用。将 Input id 值传递给 DeleteUser 方法以指定要删除的用户。
`var result = await _userService.DeleteUser(Input.Id);`
- 5. 将赋值给 `StatusMessage` 的文本改为：
`StatusMessage = $"Input.Email} was deleted.";`

DeleteModel 类的完整代码：

```csharp
public class DeleteModel : PageModel
{
    private IUserService _userService;
    [BindProperty]
    public UserPageModel Input { get; set; } = new UserPageModel();
    [TempData]
    public string StatusMessage { get; set; }
    public DeleteModel(IUserService userService)
    {
        _userService = userService;
    }
    public void OnGet(string userId)
    {
        Input = _userService.Get(userId);
        StatusMessage = string.Empty;
    }
    public async Task<IActionResult> OnPostAsync()
    {
        if (Model.IsValid)
        {
            var result = await _userService.DeleteUser(Input.Id);
            if (result)
            {
                StatusMessage = $"Input.Email} was deleted.";
                return RedirectToPage("Index");
            }
        }
        return Page();
    }
}
```

### 修改 Delete Razor Page

- 1. 打开 `Delete.cshtml` 文件。
- 2. 将模型类名为 `DeleteModel`。
- 3. 将 `ViewData` 对象的 `Title` 属性改为 Delete User。
- 4. 表单需要稍微宽一点，因为用户 id 在此页面显示。将第二个 `<div>` 的 Bootstrap 列类改为：

```html
<div class="col-6 col-md-3">
```

- 5. 将 `<p>` 元素替换为水平线。
`<hr />`
- 6. 在 `<form>` 元素上方水平线下方添加一个列表（而不是表格）。为 `Input` 对象中的 `Id`、`Email` 和 `IsAdmin` 属性添加 `<dt>` 和 `<dd>` 元素。`<dt>` 元素包含标签，`<dd>` 元素包含数据。`DisplayFor` 获取属性名称或 `[Display]` 特性中的名称。`DisplayFor` 获取存储在属性中的值。

```html
<dl class="dl-horizontal">
    <dt>@Html.DisplayNameFor(model.Input.Id)</dt>
    <dd>@Html.DisplayNameFor(model.Input.Id)</dd>
    <dt>@Html.DisplayNameFor(model.Input.Email)</dt>
    <dd>@Html.DisplayNameFor(model.Input.Email)</dd>
    <dt>@Html.DisplayNameFor(model.Input.IsAdmin)</dt>
    <dd>@Html.DisplayNameFor(model.Input.IsAdmin)</dd>
</dl>
```

- 7. 移除所有带有 form-group 装饰的 `<div>` 元素及其内容。由于表单不修改数据，不再需要这些控件。
- 8. 在现有的 `<input>` 下方为 `Input.Email` 和 `Input.IsAdmin` 属性添加隐藏的 `<input>` 元素。

```html
<input type="hidden" asp-for="Input.Id" />
<input type="hidden" asp-for="Input.Email" />
<input type="hidden" asp-for="Input.IsAdmin" />
```

- 9. 将提交按钮的文本改为 Delete，Bootstrap 样式改为 `btn-danger`。
`<button type="submit" class="btn btn-danger">Delete</button>`
- 10. 保存所有文件。

Delete Razor Page 的完整代码：

```html
@page
@using Microsoft.AspNetCore.Identity
@using VideoDemand.Data.Entities
@inject SignInManager<User> SignInManager
```

# ASP.NET Core 2.0 MVC & Razor Pages 初学者

```html
@model DeleteModel
{
    ViewData["Title"] = "Delete User";
}
```

```html
<dl class="dl-horizontal">
    <dt>@Html.DisplayName(model => model.Input.Id)</dt>
    <dd>@Html.DisplayFor(model => model.Input.Id)</dd>
    <dt>@Html.DisplayName(model => model.Input.Email)</dt>
    <dd>@Html.DisplayFor(model => model.Input.Email)</dd>
    <dt>@Html.DisplayName(model => model.Input.IsAdmin)</dt>
    <dd>@Html.DisplayFor(model => model.Input.IsAdmin)</dd>
</dl>
```

```html
<form method="post">
    <div asp-validation-summary="All" class="text-danger"></div>
    <input type="hidden" asp-for="Input.Id" />
    <input type="hidden" asp-for="Input.Email" />
    <input type="hidden" asp-for="Input.IsAdmin" />
    <button type="submit" class="btn btn-danger">Delete</button>
</form>
```

```html
</div>
}
```

## 总结

在本章中，你使用了 `UserService` 服务来处理你添加到 `Users` 文件夹的 Razor Pages 中对应 `AspNetUsers` 和 `AspNetUserRoles` 数据库表中的用户和用户角色。你添加的页面对上述表执行了 CRUD 增删改查操作。

接下来，你将创建一个新的 Tag Helper，用于显示你在 Razor Pages 的后置代码（code-behind）中添加的 `StatusMessage` 属性中的文本。

# ASP.NET Core 2.0 MVC Razor Pages 初学者

# 31. StatusMessage Tag Helper

# 简介

在本章中，你将创建一个 Tag Helper，它用于在数据成功添加、更新或删除时，显示从另一个页面发送的成功消息。该 Tag Helper 将使用属性和属性值来配置最终生成的 HTML 元素，例如消息内容和消息类型。

早些在 Razor Pages 中使用的 `StatusMessage` 属性将用于存储在数据修改时于 `OnPostAsync` 方法中分配的消息。你可以在下方图片的标题下看到警报消息示例。该消息是一个用 Bootstrap 警报类装饰的 `<div>` 标签。

`[TestData]` 属性是 ASP.NET Core 2.0 新引入的特性，可以与控制器和 Razor Pages 中的属性一起使用，在读取时存储数据。它在重定向时特别有用，因为数据可能跨越多个请求。可以使用 `Keep` 和 `Peek` 方法在不删除的情况下检查数据。

由于 `[TestData]` 属性构建于会话状态（session state），因此它可以在 Razor Pages 之间共享。你将用它从一个 Razor Page 发送消息到另一个，并使用你在本章中实现的 `<status-message>` Tag Helper 来显示它。

![](img/4b74569a91d8303eca7672688cf7d973_480_0.png)

463

# ASP.NET Core 2.0 MVC & Razor Pages 初学者

本章使用的技术

- 1 C# – 用于创建 Tag Helper。
- 2 HTML – 用于创建 Tag Helper 并将其添加到 Razor Pages 中。

添加 Tag Helper 类

- 1. 在 TagHelpers 文件夹中添加名为 `StatusMessageTagHelper` 的 Tag Helper。
```csharp
[HtmlTargetElement("tag-name")]
public class StatusMessageTagHelper : TagHelper
{
    public override void Process(TagHelperContext context, TagHelperOutput output) { }
}
```
- 2. 将 `HtmlTargetElement` 属性更改为 `status-message`。这将 Tag Helper 的“元素”名称。它不是真正的 HTML 元素，但看起来像一个，以便与 TagHelper 标记混合。然而，渲染时会生成真实的 HTML 元素。
```csharp
[HtmlTargetElement("status-message")]
```
- 3. 为类添加两个名为 `Message` 和 `MessageType` 的字符串属性，并为 `MessageType` 赋值 `success`。这些属性将成为你配合 `<status-message>` 元素使用的 Tag Helper 属性。
```csharp
public string Message { get; set; }
// 可能的 Bootstrap 类: success, danger, warning, ...
public string MessageType { get; set; } = "success";
```
- 4. 如果 `Message` 属性为空，则从 Process 方法返回。
```csharp
if (string.IsNullOrEmpty(Message)) return;
```
- 5. 如果 `context` 或 `output` 方法参数为空，则抛出 `ArgumentNullException`。如果是，则无法渲染 Tag Helper 元素。
```csharp
if (context == null)
    throw new ArgumentNullException(nameof(context));
if (output == null)
    throw new ArgumentNullException(nameof(output));
```
- 6. 使用两个方法参数调用基类的 `Process` 方法。
```csharp
base.Process(context, output);
```
# ASP.NET Core 2.0 MVC Razor Pages 初学者

7. 告诉 `Process` 方法它应该输出的元素类型。使用 `output` 对象上的 `TagName` 属性来指定 Tag Helper 的主元素容器。
```csharp
output.TagName = "div";
```
8. 添加元素和样式。使用这两个属性来分配要显示的文本，并显示 `<div>` 的背景颜色。只有当 `Message` 属性不为空时才追加消息。你可以在下方图片的标题下看到警报消息示例。该消息是一个用 Bootstrap 警报类装饰的 `<div>`。
```html
<div class="alert {MessageType} alert-dismissible" role="alert">
    {Message}
    <button type="button" class="btn-close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">&times;</span>
    </button>
</div>
```
9. 在输出中追加 `</div>`。
```csharp
