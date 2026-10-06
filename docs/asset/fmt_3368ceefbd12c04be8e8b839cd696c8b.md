
<div class="row">
<div class="col-md-4 col-md-offset-4">
<h2>@ViewData["Title"] @Model.StatusMessage</h2>
<page-button path="/Videos/Index" glyph="inline-sign" description="Back to List"></page-button>
<page-button path="Index" Bootstrap-style="warning" glyph="list-alt" description="Dashboard"></page-button>
</div>
</div>

```html
<span class="form-control" />
<span asp-validation-for="Input.Duration">
<span class="text-danger"></span>
</div>
<div class="form-group">
<label asp-for="Input.Thumbnail">
<span class="control-label"></span>
</label>
<input asp-for="Input.Thumbnail" class="form-control" />
<span asp-validation-for="Input.Thumbnail">
<span class="text-danger"></span>
</div>
<div class="form-group">
<label asp-for="Input.Url" class="control-label">
</label>
<input asp-for="Input.Url" class="form-control" />
<span asp-validation-for="Input.Url">
<span class="text-danger"></span>
</div></div></div>
<div class="form-group">
<label asp-for="Input.Position">
<span class="control-label"></span>
</label>
<input asp-for="Input.Position" class="form-control" />
<span asp-validation-for="Input.Position">
<span class="text-danger"></span>
</div></div></div>
<div class="form-group">
<label asp-for="Input.ModuleId">
<span class="control-label"></span>
</label>
<select asp-for="Input.ModuleId" class="form-control" asp-items="ViewBag.Modules"></select>
</div>
<button type="submit" class="btn btn-success">创建</button>
</form>
</div>
</div>
}
@section Scripts {
@{await Html.RenderPartialAsync("_ValidationScriptsPartial");}
}
```

# ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

# ASP.NET Core MVC & Razor Pages 初学者教程

## EditModel 类

1. 删除 `Videos` 文件夹中的两个 Edit Razor 页面（`.cshtml` 和 `.cshtml.cs`）。
2. 复制 `Videos` 文件夹中的两个 Create Razor 页面文件，并将粘贴到 `Videos` 文件夹中。将文件重命名为 `Edit.cshtml` 和 `Edit.cshtml.cs`。
3. 打开 `Videos` 文件夹中的 `Edit.cshtml` 文件，并将类和构造函数重命名为 `EditModel`。
4. 在 `OnGet` 方法中添加一个名为 `id` 的 `int` 参数。
5. 使用读取服务中的 `Get` 方法获取与你添加的参数 `id` 匹配的 `Video` 实体。将视频保存到 `Input` 属性中。

```csharp
public void OnGet(int id)
{
ViewData["Modules"] = _dbReadService.GetSelectList<Module>("Id", "Title");
Input = _dbReadService.Get<Video>(id, true);
}
```

6. 因为更新 `Video` 实体时 `Input` 对象中不需要课程对象，你应该将其赋值为 `null`。将以下代码放在分配课程 id 的之后。
`Input.Course = null;`
7. 将写入服务中的异步 `Add` 方法替换为对同一存储中 `Update` 方法的调用。将返回值存储在名为 `success` 的变量中。
`var success = await _dbWriteService.Update(Input);`
8. 将 `SuccessMessage` 属性中的文本替换为 `Updated Video:` ，后接视频标题。
`StatusMessage = "Updated Video: {Input.Title}";`
9. 保存所有文件。

EditModel 类的完整代码：

```csharp
[Authorize(Roles = "Admin")]
public class EditModel : PageModel
{
private IDbWriteService _dbWriteService;
private IDbReadService _dbReadService;
[BindProperty] public Video Input { get; set; } = new Video();
[TempData] public string StatusMessage { get; set; }
```

# ASP.NET Core MVC & Razor Pages 初学者教程

1. 打开 `Videos` 文件夹中的 Edit Razor 页面（`.cshtml` 文件）。
2. 修改 `@model` 指令以使用 `EditModel` 类。
3. 将 `ViewData` title 更改为 Edit Video。
4. 在第一个 `form-group <div>` 之上的 `Input.Id` 属性值上添加一个隐藏的 `<input>` 元素。该隐藏元素用于跟踪正在编辑的实体的 id。
`<input type="hidden" asp-for="Input.Id" />`

# ASP.NET Core MVC Razor Pages 初学者教程

5. 在包含下拉列表的 `form-group <div>` 之上，添加带有 label 和用于 `Input.Course` 中课程标题的只读 `<input>` 元素的 `form-group <div>`。
```html
<div class="form-group">
<label class="control-label">课程</label>
<input asp-for="Input.Course.Title" readonly class="form-control" />
</div>
```
6. 将提交按钮更改为保存。
`<button type="submit" class="btn btn-success">保存</button>`
7. 保存所有文件。

Edit Razor 页面的完整代码：

```html
@page
@using Microsoft.AspNetCore.Identity
@using Video.Data.Entities
@inject UserManager User
@model EditModel
@{
ViewData["Title"] = "Edit Video";
}
@if (User.IsAuthenticated && User.IsInRole("Admin")) {
<div class="row">
<div class="col-md-4 col-offset-4">
<h2>@ViewData["Title"]</h2>
<a asp-page="Index" class="btn btn-primary">返回列表</a>
<a asp-page="Index" class="btn btn-warning">仪表盘</a>
</div>
<form method="post">
<div asp-validation-summary="ModelOnly" class="text-danger"></div>
<input type="hidden" asp-for="Input.Id" />
<div class="form-group">
<label asp-for="Input.Title" class="control-label"></label>
<input asp-for="Input.Title" class="form-control" />
<span asp-validation-for="Input.Title"></span>
</div>
<div class="form-group">
<label asp-for="Input.Description" class="control-label"></label>
<input asp-for="Input.Description" class="form-control" />
<span asp-validation-for="Input.Description"></span>
</div>
<div class="form-group">
<label asp-for="Input.Duration" class="control-label"></label>
<input asp-for="Input.Duration" class="form-control" />
<span asp-validation-for="Input.Duration"></span>
</div>
<div class="form-group">
<label asp-for="Input.Thumbnail" class="control-label"></label>
<input asp-for="Input.Thumbnail" class="form-control" />
<span asp-validation-for="Input.Thumbnail"></span>
</div>
<div class="form-group">
<label asp-for="Input.Url" class="control-label"></label>
<input asp-for="Input.Url" class="form-control" />
<span asp-validation-for="Input.Url"></span>
</div>
<div class="form-group">
<label asp-for="Input.Position" class="control-label"></label>
<input asp-for="Input.Position" class="form-control" />
<span asp-validation-for="Input.Position"></span>
</div>
<div class="form-group">
<label asp-for="Input.ModuleId" class="control-label"></label>
<select asp-for="Input.ModuleId" class="form-control" asp-items="ViewBag.Modules"></select>
</div>
<button type="submit" class="btn btn-success">保存</button>
</form>
</div>
}
```

## DeleteModel 类

1. 删除 `Videos` 文件夹中的两个 Edit Razor 页面（`.cshtml` 和 `.cshtml.cs`）。
2. 复制 `Videos` 文件夹中的两个 Create Razor 页面文件，并将粘贴到 `Videos` 文件夹中。将文件重命名为 `Delete.cshtml` 和 `Delete.cshtml.cs`。
3. 打开 `Videos` 文件夹中的 `Delete.cshtml` 文件，并将类和构造函数重命名为 `DeleteModel`。
4. 在 `OnGet` 方法中添加一个名为 `id` 的 `int` 参数。
5. 使用读取服务中的 `Get` 方法获取与你添加的参数 `id` 匹配的 `Video` 实体。将视频保存到 `Input` 属性中。
6. 因为更新 `Video` 实体时 `Input` 对象中不需要课程对象，你应该将其赋值为 `null`。将以下代码放在分配课程 id 的之后。
`Input.Course = null;`
7. 将写入服务中的异步 `Add` 方法替换为对同一存储中 `Delete` 方法的调用。将返回值存储在名为 `success` 的变量中。
`var success = await _dbWriteService.Delete(Input);`
8. 将 `SuccessMessage` 属性中的文本替换为 `Deleted Video:` ，后接视频标题。
`StatusMessage = "Deleted Video: {Input.Title}";`
9. 保存所有文件。

# ASP.NET Core 2.0 MVC Razor Pages 初学者教程

DeleteModel 类的完整代码：
