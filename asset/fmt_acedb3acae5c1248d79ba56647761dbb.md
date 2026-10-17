
```
var next = videos.ElementAtOrDefault(index + 1);

var nextId = next == null ? null : next.Id;

var nextTitle = next == null ? string.Empty : next.Title;

var nextThumb = next == null ? string.Empty : next.Thumbnail;

var videoModel = new VideoViewModel

{

    Video = mappedVideoDTO,

    Instructor = mappedInstructorDTO,

    Course = mappedCourseDTO,

    LessonInfo = new LessonInfo

    {

        LessonNumber = index + 1,

        NumberOfLessons = count,

        NextVideoId = nextId,

        PreviousVideoId = previousId,

        NextVideoTitle = nextTitle,

        NextVideoThumbnail = nextThumb

    }

};

return View(videoModel);

}
```

## 总结

在本章中，你为 AutoMapper 添加了实体和 DTO 类的配置。你配置了 `Startup` 类，并并在 `Membership` 控制器的构造函数中注入了必要的对象。你实现了 `Dashboard`、`Course` 和 `Video` 动作。接下来，你将实现 `Dashboard` 视图并渲染它。

# ASP.NET Core 2.0 MVC & Razor Pages 入学者教程

# 18. Dashboard 视图

## 引言

在本章中，你将在 `Membership` 文件夹中添加 `Dashboard` 视图。它将通过 `Dashboard` 动作进行渲染。

## 概述

在本章中，你将在 `Membership` 文件夹中添加 `Dashboard` 视图。它将通过 `Dashboard` 动作进行渲染。

## 本章使用的技术

- 1. HTML – 用于创建视图
- 2. CSS – 用于样式化视图
- 3. Razor – 用于在视图中使用 C#

## 课程

在本章中，你将在 `Membership` 文件夹中添加 `Dashboard` 视图。它将通过 `Dashboard` 动作进行渲染。

## 课程

在本章中，你将在 `Membership` 文件夹中添加 `Dashboard` 视图。它将通过 `Dashboard` 动作进行渲染。

## 课程

在本章中，你将在 `Membership` 文件夹中添加 `Dashboard` 视图。它将通过 `Dashboard` 动作进行渲染。

# 面初学者 ASP.NET Core 2 MVC & Razor Pages 教程

- 5. 在循环内部添加一个 `<div>`，并使用 Bootstrap 的 `row` 类对其进行装饰。`row` 类将该 `<div>` 样式化为浏览器中的新行。
```html
<div class="row">
</div>
```

- 6. 在 `<div>` 内部添加一个 `foreach` 循环，用于遍历该行的（三门）课程。目前，添加一个 `<h1>` 元素来显示课程标题。
```razor
@foreach (var course in dashboardRow)
{
  <h4>@course.CourseTitle</h4>
}
```

- 7. 切换到浏览器并刷新 Dashboard 视图（`/membership/dashboard`）。课程标题应该显示在视图标题下方。

到目前为止 Dashboard 视图中的标记代码如下：
```razor
@model DashboardViewModel
{
  ViewData["Title"] = "Dashboard";
}
<div class="membership top-margin">
  <h2 class="text-dark">Dashboard</h2>
  <hr class="thick-margin">
  @foreach (var dashboardRow in Model.Courses)
  {
    <div class="row">
      <h4>@course.CourseTitle</h4>
    </div>
  }
</div>
```

## 创建 CoursePanelPartial 部分视图

为了避免让课程标记弄乱 Dashboard 视图，你将创建一个名为 `_CoursePanelPartial` 的部分视图，它将为每门课程进行渲染。将使用 Bootstrap 面板来显示课程信息。

- 1. 右键点击 `Views/Membership` 文件夹并选择“添加视图”（Add-View）。
- 2. 将视图命名为 `_CoursePanelPartial`，并在点击添加按钮之前勾选“创建部分视图”（Create as partial view）复选框。

![](img/4b74569a91d8303eca7672688cf7d979_292_0.png)

- 3. 删除视图中的所有代码。
- 4. 打开 `_ViewImports` 视图并为 `VideoOnDemand.UI.Models.DTOModels` 命名空间添加 `using` 语句。保存文件并关闭。
```razor
using VideoOnDemand.UI.Models.DTOModels
```

- 5. 为部分视图添加针对 `CourseDTO` 的 `@model` 指令。
```razor
@model CourseDTO
```

- 6. 添加一个 `<div>` 元素并使用 Bootstrap 的 `col-sm` 类对其进行装饰，使其占据 1/3 的行空间。`col-sm` 类在行中的总和必须为 12，由于每行添加了 3 门课程，因此满足了要求。
```html
<div class="col-sm-4">
</div>
```

- 7. 在之前的 `<div>` 内部添加一个 `<div>`，并使用 Bootstrap 面板类进行装饰，使其作为一个面板（即课程信息的外部容器）。同时添加一个名为 `course-listing` 的 CSS 类。它将作为一个主选择器，以提高特殊性，并将样式与其他样式分离。
```html
<div class="panel course-listing">
</div>
```

- 8. 在上一个 `<div>` 中添加一个带有 CSS 类 `thumb` 的 `<img>` 元素。该类将用于对图像进行样式化。在视图模型中添加 `@CourseImageUrl` 属性作为图像源。
```html
<img class="thumb" src="@Model.CourseImageUrl">
```

- 9. 添加一个 `<div>` 元素包含图像，并使用 Bootstrap 的 `panel-body` 类进行装饰。这是显示视频信息的区域。
```html
<div class="panel-body">
</div>
```

- 10. 在上一个 `<div>` 内部添加一个 `<h3>` 元素，并使用名为 `text-dark` 的 CSS 类进行装饰。向其添加视图模型中的 `@CourseTitle` 属性。
```html
<h3 class="text-dark">@Model.CourseTitle</h3>
```

- 11. 在上一个 `<div>` 内部添加一个 `<p>` 元素。

- 12. 在该元素中添加视图模型中的 `@CourseDescription` 属性。添加一个 `<a>` 元素。
```html
<a class="btn-primary" href="~/membership/details/@Model.CourseId">查看详情</a>
```

- 13. 打开 Dashboard。

- 14. 使用 `PartialAsync` 方法为每门课程渲染 `_CoursePanelPartial`。

- 15. 使用 `foreach` 循环替换之前的硬编码标记。
```razor
@foreach (var dashboardRow in Model.Courses)
{
    @await Html.PartialAsync("_CoursePanelPartial", dashboardRow)
}
```

- 16. 保存文件并刷新 Dashboard。

CoursePanelPartial 视图的完整标记如下：
```razor
@model CourseDTO
<div class="col-sm-4">
  <div class="panel course-listing">
    <img class="thumb" src="@Model.CourseImageUrl">
    <div class="panel-body">
      <h3 class="text-dark">@Model.CourseTitle</h3>
      <p>@Model.CourseDescription</p>
      <a class="btn-primary" href="~/membership/details/@Model.CourseId">查看详情</a>
    </div>
  </div>
</div>
```

## 对 Dashboard 和 _CoursePartial 进行样式化

现在，你将对 Dashboard 和 `_CoursePartial` 进行样式化。为了实现这一点，你将为 Dashboard 和 `_CoursePartial` 创建 CSS 文件。

- 1. 在 `content/css` 文件夹中创建一个 `dashboard.css` 文件。
- 2. 在 Layout 视图中引用该 CSS 文件。
- 3. 为容器和标题添加样式。
- 4. 为分割线和响应式行添加样式。

- 1. 在 `content/css` 文件夹中创建一个 `_coursepartial.css` 文件。
- 2. 在 `CoursePanelPartial` 视图中引用该 CSS 文件。
- 3. 为面板、缩略图和主体添加样式。
- 4. 为标题、描述和按钮添加样式。

- 1. 在 `dashboard.css` 中添加媒体查询以实现响应式。
- 2. 针对小屏幕调整样式。

- 1. 为应用程序添加 Google 字体链接。
- 2. 在 Layout 视图中添加字体链接。
- 3. 在 `membership.css` 文件中添加字体族。
- 4. 为 `body` 添加背景颜色。

- 1. 为容器和标题添加样式。
- 2. 为分割线和响应式行添加样式。

- 1. 为面板、缩略图和主体添加样式。
- 2. 为标题、描述和按钮添加样式。

- 1. 在 `dashboard.css` 中添加媒体查询以实现响应式。
- 2. 针对小屏幕调整样式。

## 总结

在本章中，你添加了 Dashboard 视图和 `_CoursePanelPartial` 部分，并使用 CSS 和 Bootstrap 对它们进行了样式化。

接下来，你将添加 Course 视图以及作为该视图部分的 `_ModuleVideosPartial` 和 `_InstructorBio-Partial` 部分视图。然后你将使用 CSS 和 Bootstrap 对它们进行样式化。

# 19. 课程视图 (Course View)

## 介绍

在本章中，你将添加课程视图以及三个部分视图，分别称为 `_ModuleVideosPartial`、`_ModuleDownloadsPartial` 和 `_InstructorBioPartial`，它们都是课程视图的一部分。当你查看部分视图内容时，你将使用 CSS 和 Bootstrap 对其进行样式设置。当用户点击仪表板（Dashboard）视图的课程面板按钮时，将显示课程视图。该视图包含所选课程的信息，并包含该课程所有视频的模块列表。讲师简介将显示在模块列表旁边。你将在视图顶部添加一个按钮，使用户返回仪表板视图。

## 本章使用的技术

- 1. HTML – 用于创建视图布局。
- 2. CSS – 用于视图的样式设置。
- 3. Razor – 在视图中使用 C#。

## 概述

你的任务是在 `Course` 中中使用视图模型，并渲染一个视图，该视图将在视图顶部“返回仪表板”按钮下方以单独的一行显示跑灯效果（marquee）、课程图像、标题和描述。在这一行下方，应显示一个分为两列的第二行。在左列中为课程的每个模块添加行，并列出每个模块的视频。在右列中显示讲师简介。

## ASP.NET 2.0 MVC & Razor Pages 初学者

![](img/4b74569a91d8303eca7672688cf7d979_299_0.png)

## 课程 1

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco nisi ut ut aliquip ex ea commodo consequat.

模块 1

| 视频 1 | |
| --- | --- |
| 视频 1 | 10分钟 <br>Lorem dolor sit amet, consect. |
| 视频 2 | 10分钟 <br>Lorem dolor sit amet, consect. |

下载

- ADD NET 1 (PDF)
- ADD NET 2 (PDF)

模块 2

| 视频 3 | |
| --- | --- |
| 视频 3 | 10分钟 <br>Lorem dolor sit amet, consect. |

## 添加课程视图

首先，你将导航到 `Views/Membership` 文件夹并添加课程视图。

然后，你将添加一个导航到仪表板的按钮、一个带有课程图像、课程信息、讲师简介以及带有视频和下载模块的跑灯。你需要创建三个部分视图：一个名为 `_InstructorBioPartial` 用于讲师简介，一个名为 `_ModuleVideosPartial` 用于视频，一个名为 `_ModuleDownloadsPartial` 用于下载。然后，这三个区域将使用 Bootstrap 和 CSS 进行样式设置。

## ASP.NET Core MVC & Razor Pages 初学者

- 1. 打开 Membership 控制器。
- 2. 右键点击 `Course` 操作并选择“Add-View”（添加视图）。
- 3. 确保取消勾选“Create as partial view”（创建部分视图）复选框。
- 4. 点击“Add”（添加）按钮创建视图。

![](img/4b74569a91d8303eca7672688cf7d979_300_0.png)

- 5. 关闭并重新打开 Course 视图消除消除错误。
- 6. 在视图开头为 `CourseViewModel` 类添加 `@model` 指令。
- 7. 保存文件。
- 8. 在不调试的情况下启动应用程序（Ctrl+F5）并导航到 `Membership/Dashboard`。点击面板按钮之一打开一个课程，或导航到 `Membership/Course/1` URL。如果 Course 视图渲染正确，浏览器中应显示文本“Course”。

@model CourseViewModel

目前 Course 视图中的标记内容如下：
```
@model CourseViewModel
@{
    ViewData["Title"] = "Course";
}
```

## ASP.NET Core 2.0 MVC & Razor Pages 初学者

```
<h2>Course</h2>
```
