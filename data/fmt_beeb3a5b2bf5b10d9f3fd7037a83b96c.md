
# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

![](img/4b74569a91d8303eca7672688cf7d979_333_0.png)

# 视频 1 标题

课程 1 / 2 50 分钟

课程 1

Lorem ipsum dolor sit amet, consect

# 视频 1 标题

课程 1 / 2 50 分钟

课程 1

Lorem ipsum dolor sit amet, consect

## 初学者 ASP.NET Core 2.0 MVC Razor Pages

### 创建一个视频播放器

- 1. 访问 `www.jwplayer.com` 注册账户并登录。
- 2. 选择菜单中 Players 部分的 `Manage` 链接。
- 3. 点击 `Create New Player` 按钮创建你的视频播放器。
- 4. 在文本字段中为播放器命名；你可以称它为任何名称。
- 5. 在 Basic Setup 区域选择 `Responsive` 单选按钮。
- 6. 如果你需要，可以更改其他设置以自定义播放器标记。
- 7. 点击 `Save` 按钮。
- 8. 复制演示视频播放器下方的链接。这就是你将添加到 `*_Layout*` 视图中的链接，以便访问视频播放器。

### 将视频播放器添加到视频视图

- 1. 打开 `*_Layout*` 视图。
- 2. 将从 JWPlayer 网站复制的链接添加到 `<body>` 元素结尾的所有 `<environment>` 元素中。
- 3. 打开 Video 视图。
- 4. 在视图底部添加一个 `Scripts` 区域，在页面加载到 DOM 后立即调用 `jwplayer` 函数。注意 `jwplayer` 函数名必须使用小写字母。

```csharp
@section Scripts {
<script type="text/javascript">
$(function () {
    jwplayer("video").setup({
        file: $("#hiddenUrl").text(),
        image: $("#hiddenImageUrl").text()
    });
});
</script>
}
```
- 5. 保存所有文件。
- 6. 刷新浏览器中的 Video 视图。视频图像应该是可见的，如果你点击它，视频将开始播放。

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

### 为 LessonInfoDTO 类添加属性

有一条信息需要添加到 `LessonInfoDTO` 和 `Membership` 控制器。为了避免用户使用“Coming Up”部分中的“Next”按钮导航到最后一个视频时显示空的图像容器，应该显示当前视频的缩略图。因此，你必须在 `LessonInfoDTO` 类中包含当前视频的缩略图和标题，并将该数据添加到 `Membership` 控制器 `Video` 操作的视图模型中。

- 1. 打开 `LessonInfoDTO` 类。
- 2. 添加两个名为 `CurrentVideoTitle` 和 `CurrentVideoThumbnail` 的字符串属性。

```csharp
public string CurrentVideoTitle { get; set; }
public string CurrentVideoThumbnail { get; set; }
```
- 3. 打开 `Membership` 控制器并找到 `Video` 操作。
- 4. 将视频对象的 `Thumbnail` 和 `Title` 属性赋值给你刚刚添加到 `LessonInfoDTO` 类的属性。

```csharp
CurrentVideoTitle = video.Title;
CurrentThumbnail = video.Thumbnail
```
- 5. 在 `MockReadRepository` 中为第一个课程的第一个模块添加一个视频。第一个模块应该至少有三个视频，这样你在测试 Video 视图的“Coming Up”部分时就可以正确使用“Previous”和“Next”按钮。

完整的 `LessonInfoDTO` 类：

```csharp
public class LessonInfoDTO {
    public int LessonNumber { get; set; }
    public int NumberOfLessons { get; set; }
    public int PreviousVideoId { get; set; }
    public int NextVideoId { get; set; }
    public string NextVideoTitle { get; set; }
    public string NextVideoThumbnail { get; set; }
    public string CurrentVideoTitle { get; set; }
    public string CurrentVideoThumbnail { get; set; }
}
```

## ASP.NET Core 2 MVC & Razor Pages 初学者

### Video 操作中完整的 `LessonInfoDTO` 对象

```csharp
LessonInfo = new LessonInfoDTO
{
  LessonNumber = index + 1,
  NumberOfLessons = count,
  NextVideoId = nextId,
  PreviousVideoId = previousId,
  NextVideoTitle = next,
  NextVideoThumbnail = nextThumb,
  CurrentVideoTitle = video.Title,
  CurrentVideoThumbnail = video.Thumbnail
}
```

### 添加 _VideoComingUpPartial 部分视图

此部分视图将显示包含下一个视频缩略图、其标题以及“Previous”和“Next”按钮的面板。当显示第一个视频的信息时，“Previous”按钮应被禁用。当显示最后一个视频的信息时，“Next”按钮应被禁用。如果没有视频，则不应显示“Coming Up”面板。

# ASP.NET Core 2.0 MVC & Razor Pages 初学者教程

```html
<div class="panel-body">
  @if (Model.NextVideoId == 0)
  {
    <p>课程完成</p>
    <h<h5>@CurrentVideoTitle</h5>
  } else
  {
    <p>即将播放</p>
    <h<h5>@NextVideoTitle</h5>
  }
  <div class="btn-group" role="group">
    @if (Model.PreviousVideoId == 0)
    {
      <a class="btn btn-default" disabled href="#">
        上一个
      </a>
    } else
    {
      <a class="btn btn-default" href="~/Membership/Video/@Model.PreviousVideoId">
        上一个
      </a>
    }
    @if (Model.NextVideoId == 0)
    {
      <a class="btn btn-default" disabled href="#">
        下一个
      </a>
    } else
    {
      <a class="btn btn-default" href="~/Membership/Video/@Model.NextVideoId">
        下一个
      </a>
    }
  </div>
</div>
```

323

# ASP.NET Core 2. MVC & Razor Pages 初学者教程

## 为 _VideoComingUpPartial 局部视图设置样式

打开 `video.css` 样式表，使按钮组尽可能宽。

```css
.coming-up .btn-group {
  width: 100%;
}
```

让每个按钮占据按钮组宽度的 50%。

```css
.coming-up .btn-group .btn {
  width: 50%;
}
```

## 添加 _InstructorBioPartial 局部视图

你将在 Video（视频）视图中添加的最后一个部分是 `_InstructorBioPartial` 局部视图，它用于显示讲师的信息。

![](img/4b74569a91d8303eca7672688cf7d979_341_0.png)

- 1. 打开 Video 视图。
- 2. 在带有 `col-sm-3` Bootstrap 类的装饰 `<div>` 内部，在上一个 `if` 块下方调用 `PartialAsync` 方法来渲染 `_InstructorBioPartial` 局部视图。

# ASP.NET Core 2.0 MVC Razor Pages 初学者教程

从视图模型（view model）将讲师对象传递到局部视图。用一个 `if` 块包裹该方法调用，检查视图模型和讲师对象是否不空。

```razor
@if (Model != null && Model.Instructor != null)
{
    @await Html.PartialAsync("_InstructorBioPartial",
    Model.Instructor)
}
```
- 3. 保存文件并在浏览器中刷新 Video 视图。`InstructorBioPartial` 局部视图应显示在 `_VideoComingUpPart` 局部视图下方。

Video 视图的完整代码：

```razor
@model ViewModel
{
ViewData["Title"] = "Video";
<div class="membership top-margin navigation-bar">
    <div class="row">
        <div class="col-sm-12">
            <a class="btn btn-primary" href="~/Membership/Course/@Model.Course.CourseId">
                <span class="glyphicon glyphicon-menu-left"></span>
                返回课程 @Model.Course.CourseTitle
            </a>
        </div>
    </div>
</div>
<div class="row">
    <div class="col-sm-9">
        @if (Model != null && Model.Video != null &&
            Model.LessonInfo != null && Model.Course != null)
        {
            @await Html.PartialAsync("_VideoPlayerPartial", Model)
        }
    </div>
}
```

# ASP.NET Core 2. MVC & Razor Pages 初学者教程

## 总结

在本章中，你添加了 Video 视图及其局部视图。你还添加了 JWPlayer以便在视图中播放视频内容。

在书的下半部分，你将使用 Entity Framework 迁移（migrations）向 SQL Server 数据库添加实体类。你还将添加一个新的数据存储仓库（repository）来与数据库交互。当仓库就绪后，你将为管理员创建一个用户界面。

## 21. 创建数据库表

### 引言

在本章中，你将创建用于存储视频数据的数据库表；你已经在之前的章节中创建了用户数据的表。虽然你可以有多个数据库上下文（contexts）来与数据库交互，但你将继续使用已经创建的那个。

在创建表之后，你还将为数据库填充初始数据。这会让你在创建各种视图时更容易跟上进度，因为这些视图将已经包含你熟悉的数据。

在创建并填充表后，你将创建一个名为 `SqlRepository` 的新数据存储仓库，并使用你在添加 `MockReadRepository` 类时使用的相同 `IRepository` 接口。一旦实现，你将在 `Startup` 类的 `ConfigureServices` 方法中，用 `SqlReadRepository` 类替换 `IRead-Repository` 服务。这将使应用程序使用来自数据库的数据而不是模拟数据。

### 本章使用的技术

- 1. C# – 在填充数据库和创建仓库时使用。
- 2. Entity framework – 用于从仓库创建并与新表交互。
- 3. LINQ – 用于查询数据库表。

### 概述

你的第一个目标是在数据库中创建存储视频相关数据的表，并填充数据。第二个目标是创建一个可以与数据库表通信的数据存储仓库。

ASP.NET Core 2 MVC Razor Pages 初学者

## 创建表

你的第一个目标是在数据库中创建存储视频相关数据的表，并填充数据。第二个目标是创建一个可以与数据库表通信的数据存储仓库。在实现这些步骤后，应用程序将使用实时数据。

ASP.NET Core 2 MVC Razor Pages 初学者

### 添加表

为了与数据库交互，你需要将实体类作为 `DbSet` 属性添加到 `VODContext` 中。你可以将 `VODContext` 注入到 `SqlRepository` 类的构造函数中以对表执行 CRUD（增删改查）操作。在 `Startup` 类中用 `SqlReadRepository` 类替换 `MockReadRepository`，将使用实时数据而不是模拟数据。

### 在 VODContext 中添加实体类

- 打开 `VideoOnDemand.Data` 项目。
- 打开 `VODContext` 类。
- 将所有实体作为 `DbSet` 属性添加到类中。

```csharp
public DbSet<Course> { get; set; }
public DbSet<Download> { get; set; }
public DbSet<Instructor> { get; set; }
public DbSet<Module> { get; set; }
public DbSet<UserCourse> { get; set; }
public DbSet<Video> { get; set; }
```
- 因为 `UserCourse` 表具有复合键（UserId 和 CourseId），你需要在 `OnCreating` 方法中指定它。在 ASP.NET Core 的早期版本中，可以通过 Lambda 表达式传递给 `HasKey` 方法。

```csharp
builder.Entity<UserCourse>().HasKey(uc => new { uc.UserId, uc.CourseId });
```
删除父记录时避免级联删除，可以在 `OnCreating` 方法中添加删除行为。级联删除将删除相关的记录；例如，如果你删除一个订单，它的行也会被删除。

```csharp
foreach (var relationship in builder.Model.GetEntityTypes()
    .SelectMany(e => e.ForeignKeys()))
{
    relationship.DeleteBehavior = DeleteBehavior.Restrict;
}
```

ASP.NET Core 2.0 Razor Pages 初学者

## VODContext 的完整代码

```csharp
public class VODContext : IdentityDbContext<User>
{
    public DbSet<Course> Courses { get; set; }
    public DbSet<Download> Downloads { get; set; }
    public DbSet<Instructor> Instructors { get; set; }
    public DbSet<Module> Modules { get; set; }
    public DbSet<UserCourse> UserCourses { get; set; }
    public DbSet<Video> Videos { get; set; }
}
```

```csharp
public VODContext(DbContext<VODContext> options)
: base(options) { }
```

```csharp
protected override void OnCreating(ModelBuilder builder)
{
    base.OnModelCreating(builder);
    // 复合键
    Entity<UserCourse>().HasKey(uc => new { uc.UserId, uc.CourseId });
    // 限制级联删除
```
