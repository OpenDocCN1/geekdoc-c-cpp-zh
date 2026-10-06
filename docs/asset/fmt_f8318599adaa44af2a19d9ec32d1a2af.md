
## 总结

在本章中，你添加了 Admin 菜单并针对了将在书中添加的 Index Razor Pages。在下一章中，你将创建一个标记助手（Tag Helper）。

# ASP.NET Core 2.0 MVC & Razor Pages 入门教程

## 引言

你的任务是为按钮创建一个自定义标记助手。你将首先使用字符串传递值的静态方法，然后实现一种更动态的属性读取方法。标记助手将通过继承自 `TagHelper` 的类来实现 `Process` 方法。

## 本章使用的技术

- `C#` – 用于创建标记助手。
- `HTML` – 用于创建 Razor Pages。

## 概述

任务是为按钮创建一个自定义标记助手。你将首先使用字符串传递值的静态方法，然后实现一种更动态的属性读取方法。标记助手将通过继承自 `TagHelper` 的类来实现 `Process` 方法。

## 自定义标记助手

你的任务是为按钮创建一个自定义标记助手。你将首先使用字符串传递值的静态方法，然后实现一种更动态的属性读取方法。标记助手将通过继承自 `TagHelper` 的类来实现 `Process` 方法。

## 静态方法

任务是为按钮创建一个自定义标记助手。你将首先使用字符串传递值的静态方法，然后实现一种更动态的属性读取方法。标记助手将通过继承自 `TagHelper` 的类来实现 `Process` 方法。

## 动态方法

任务是为按钮创建一个自定义标记助手。你将首先使用字符串传递值的静态方法，然后实现一种更动态的属性读取方法。标记助手将通过继承自 `TagHelper` 的类来实现 `Process` 方法。

## 实现

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

```html
<page-button path="Videos/Create" Bootstrap-style="primary" description="Create New"></page-button>
```

## 实现 Page-Button Tag Helper

Tag Helper（标签助手）应该在一个名为 `PageButtonTagHelper` 的类中，该类位于项目节点直接下方的 `TagHelpers` 文件夹中。使用“新建项”对话框中的 Razor Tag Helper 模板。

你可以使用 `HtmlTargetElement` 将 Tag Helper 的范围限制到特定的 HTML 元素类型。

```csharp
[HtmlTargetElement("my-tag-helper")]
public class MyTagTagHelper : TagHelper
```

Tag Helper 将生成一个 Bootstrap 风格 `<element>` 元素。

为了在 Razor Pages 中可以使用 Tag Helper，你需要在项目程序集中添加 `@addTagHelper` 指令以包含项目程序集中的所有 Tag Helper，或者在 `_Imports` 视图中添加。

```razor
@addTagHelper *, VideoOnDemand.Admin
```

将 Tag Helper 添加到视图时，使用闭合标签非常重要，否则 Tag Helper 将无法工作。

```html
<page-button></page-button>
```

## 创建 Tag Helper

- 1. 在 `_Imports` 视图中添加一个包含项目程序集中所有 Tag Helper 的 `@addTagHelper` 指令。`VideoOnDemand.Admin`。
- 2. 向项目中添加一个名为 `TagHelpers` 的文件夹。
- 3. 向文件夹中添加一个名为 `PageButtonTagHelper` 的 Razor Tag Helper 类。右键点击文件夹并选择“添加新项”。选择 Razor Tag Helper 模板，对其命名并点击“添加”按钮。

```csharp
[HtmlTargetElement("tag-name")]
public class PageButtonTagHelper : TagHelper
{
    public override void Process(TagHelperContext context, TagHelperOutput output) { }
}
```

- 4. 将 `HtmlTargetElement` 属性更改为 `page-button`。这将是 Tag Helper “元素”名称。它不是一个真实的 HTML 元素，但它看起来像是一个，以便绑定到 HTML 标记中。然而，在渲染时它将生成一个真实的 HTML 元素。

```csharp
[HtmlTargetElement("page-button")]
```

- 5. 向类添加用于存储 `<page-button>` 元素属性值的属性。

  - `Path` (`string`): 包含目标页面的文件夹以及要打开的页面名称。元素元素的有效值示例：`Videos/Edit`。
    `public string Path { get; set; } = string.Empty;`

  - `Description` (`string`): 在按钮上显示的文本；如果你希望显示一个没有描述的按钮，则不要向元素添加此属性。默认值应为空字符串。
    `public string Description { get; set; } = string.Empty;`

  - `Glyph` (`string`): 显示在按钮上的 Glyphicon 图标。你可以跳过 `glyphicon-` 前缀；如果你希望显示一个没有 Glyphicon 的按钮，则不要向元素添加此属性。默认值应为空字符串。显示相同图标的两个元素有效值示例：`pencil` 或 `glyphicon-pencil`。
    `public string Glyph { get; set; } = string.Empty;`

  - `BootstrapStyle` (`string`): 添加到按钮上的 Bootstrap 样式名称。决定按钮的颜色；如果你希望自定义按钮样式，则不要向元素添加此属性。默认值应为字符串 `btn-default`。你可以从样式中省略 `btn-` 前缀。示例：`success` 或 `btn-success`。
    `public string BootstrapStyle { get; set; } = "btn-default";`

  - `BootstrapSize` (`string`): 用于显示按钮的 Bootstrap 尺寸。决定按钮的大小；如果你希望使用小型按钮，则不要向元素添加此属性。默认值应为字符串 `btn-sm`。你可以从尺寸中省略 `btn-` 前缀。显示相同大小按钮的两个有效值示例：`lg` 或 `btn-lg`。
    `public string BootstrapSize { get; set; } = "btn-sm";`

- 6. 在 `Process` 中添加：如果任何参数为空，则抛出异常。在基类中 `if` 语句下方调用 `Process` 方法。
```csharp
if (context == null)
    throw new ArgumentNullException(nameof(context));
if (output == null)
    throw new ArgumentNullException(nameof(output));
base.Process(context, output);
```

- 7. 为完成的 URL 添加一个有效的命名名 `href`，它将被添加到 `<a>` 元素的 `href` 属性中。
`var href = "";`

- 8. 添加一个 `if` 块检查 `Path` 属性是否有内容。
```csharp
if (Path.Trim().Length > 0)
```

- 9. 在 `if` 块内部使用 `Path` 属性构建 `href`。如果 `Path` 属性以斜杠 (`/`) 开头，则直接添加到 `href` 字符串，否则添加斜杠和 `Path` 属性。
```csharp
if (Path.Trim().StartsWith('/'))
    href = Path.Trim();
else
    href = "/" + Path.Trim();
```

- 10. 在 `if` 块内部通过调用 `output` 对象的 `AppendHtml` 将 `href` 变量添加到 `<a>` 元素中。将 `Description` 属性添加到 `<a>` 元素。
`output.Content.AppendHtml("<a href='" + href + "'>" + Description + "</a>");`

- 11. 在 `Pages` 文件夹中插入 `Index` 页面并添加。`VideoOnDemand.Admin`。

- 12. 运行程序。

- 13. 检查 Tag Helper 属性。

- 14. 停止程序。

## 初学者 ASP.NET Core 2.0 MVC Razor Pages

```csharp
if (Description.Length > 0) Description = "{Description}";
```

- 在 `<a>` 元素的 Description 属性之前，向 `<span>` 标签中添加 `glyphClasses` 变量的值。
`output.Content.AppendHtml("$@<a href` + `<span class=\"{glyphClasses}\">{Description}</span></a>");`

- 打开 Pages 文件夹中的 Index 页面，并在 Tag Helper 的 glyph 属性中添加一个 Glyphicon 类名。
`<page-button path="Videos/Edit" description="Edit" id="1" videoId="2" glyph="pencil"></page-button>`

- 运行应用程序并导航到 Pages 文件夹中的 Index 页面（仪表），），验证铅图标是否可见。

目前 Process 方法中的代码如下：

```csharp
public override void Process(TagHelperContext context, TagHelperOutput output)
{
    if (context == null)
        throw new ArgumentNullException(nameof(context));
    if (output == null)
        throw new ArgumentNullException(nameof(output));
    base.Process(context, output);
    var href = "";Trim();
    if (Path.Trim().Length > 0)
    {
        // 组装 href 参数的值
        if (Path.Trim().StartsWith("/")) href = "$@href='/{Path.Trim()}'";
        else href = "$@href='/{Path.Trim()}'";
    }
    var ids = context.AllAttributes.Where(c => 
        c.Name.StartsWith("id"));
    // 生成 Id 参数
    var param = "";
    foreach (var id in ids)
    {
        var name = id.Name;
        if (name.Contains("-"))
            name = name.Substring(name.IndexOf('-') + 1);
```

## 初学者 ASP.NET Core 2.0 MVC Razor Pages

```csharp
param += "${name}={id.Value}";
if (param.StartsWith("&")) param = param.Substring(1);
if (param.Length > 0)
    href = href.Insert(href.Length, 1, "${param}");
// 显示 Glyph 图标
var glyphClasses = string.Empty;
Glyph = Glyph.Trim();
if (Glyph.StartsWith("glyphicon-"))
    Glyph = Glyph.Substring(Glyph.IndexOfOf('-') + 1);
if (Glyph.Length > 0)
{
    glyphClasses = "class='glyphicon glyphicon-{Glyph}'";
    if (Description.Length > 0)
        Description = "${Description}";
}
output.Content.AppendHtml(@@"<a href=""""><span{glyphClasses}></span>{Description}</a>");
```
