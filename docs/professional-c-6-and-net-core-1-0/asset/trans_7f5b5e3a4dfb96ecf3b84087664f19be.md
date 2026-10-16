
```html
<input data-val="true"
    data-val-length="The field Text must be a string with a maximum length of 50."
    data-val-length-max="50"
    data-val-required="The Text field is required."
    id="FileName_Text" name="Text"
    type="text"
    value="Schweinsbraten mit Kn&ouml;del und Sauerkraut" />
```

## 使用编辑器扩展

不必为每个属性都使用至少一个辅助方法，`EditorExtensions`类中的辅助方法可以为某个类型的所有属性提供一个编辑器。

使用与之前相同的`Menu`模型，通过`Html.EditorFor(m => m)`方法即可构建编辑菜单所需的完整用户界面（UI）。该方法调用的结果如图41.9所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1599_0.png)

**图41.9**

不用`Html.EditorFor(m => m)`，你可以使用`Html.EditorForModel`。`EditorForModel`方法直接使用视图的模型，无需显式指定。`EditorFor`在使用其他数据源（例如模型提供的属性）时更灵活，而`EditorForModel`需要添加的参数更少。

## 实现模板

扩展HTML Helper输出的一种好方法是使用模板。*模板*是HTML Helper方法隐式或显式使用的一个简单视图。模板存储在特殊的文件夹中。显示模板存储在视图文件夹（例如`Views/HelperMethods`）中的`DisplayTemplates`文件夹内，或者存储在共享文件夹（`Shared/DisplayTemplates`）中。共享文件夹可被所有视图使用；特定视图文件夹仅供该文件夹内的视图使用。编辑器模板存储在`EditorTemplates`文件夹中。

现在来看一个例子。在`Menu`类型中，`Date`属性带有`DataType`注解，其值为`DataType.Date`。指定此特性后，`DateTime`类型默认不显示为日期和时间，而只显示短日期格式（代码文件`MVCSampleApp/Models/Menu.cs`）：

```csharp
public class Menu
{
    public int Id { get; set; }
    [Required, StringLength(50)]
    public string Text { get; set; }
    [Display(Name = "Price"), DisplayFormat(DataFormatString = "{0:c}")]
    public double Price { get; set; }
    [DataType(DataType.Date)]
    public DateTime Date { get; set; }
    [StringLength(10)]
    public string Category { get; set; }
}
```

现在创建日期的模板。使用此模板时，`Model`以长日期字符串格式`D`返回，并嵌入到带有CSS类`markRed`的`div`标签中（代码文件`MVCSampleApp/Views/HTMLHelpers/DisplayTemplates/Date.cshtml`）：

```cshtml
<div class="markRed">
    @string.Format("{0:D}", Model)
</div>
```

`markRed` CSS类在样式表中定义，用于将颜色设置为红色（代码文件`MVCSampleApp/wwwroot/styles/Site.css`）：

```css
.markRed {
    color: #f00;
}
```

现在，可以使用`DisplayForModel`等显示HTML Helper来利用已定义的模板。模型是`Menu`类型，因此`DisplayForModel`方法会显示`Menu`类型的所有属性。对于`Date`，它会找到`Date.cshtml`模板，并使用该模板以长日期格式和CSS样式显示日期（代码文件`MVCSampleApp/Views/HTMLHelpers/Display.cshtml`）：

```cshtml
@model MVCSampleApp.Models.Menu
@{
    ViewBag.Title = "Display";
}
<h2>@ViewBag.Title</h2>
@Html.DisplayForModel()
```

如果某个类型在同一个视图中需要不同的呈现方式，可以为模板文件使用其他名称。然后可以使用`UIHint`特性指定模板名称，或者使用辅助方法的模板参数来指定模板。

## 了解标签助手

ASP.NET MVC 6提供了一种可替代HTML Helper的新技术：标签助手（Tag Helpers）。使用标签助手时，你不必编写混有HTML的C#代码，而是使用在服务器上解析的HTML属性和元素。如今，许多JavaScript库通过自定义属性扩展HTML（如Angular），因此能够将自定义HTML属性与服务器端技术结合使用非常方便。ASP.NET MVC的许多标签助手都有`asp-`前缀，因此你可以轻松分辨哪些内容会在服务器端解析。这些属性不会发送到客户端，而是在服务器端解析以生成HTML代码。

### 激活标签助手

要使用ASP.NET MVC标签助手，你需要通过调用`addTagHelper`来激活这些标签助手。第一个参数定义要使用的类型（`*`会打开程序集中的所有标签助手）；第二个参数定义标签助手的程序集。使用`removeTagHelper`可以再次停用标签助手。停用标签助手可能很重要——例如，为了避免与脚本库产生命名冲突。使用带有`asp-`前缀的内置标签助手时，你很可能不会遇到冲突，但其他标签助手很容易产生冲突，因为它们可能与其他标签助手或脚本库使用的HTML属性同名。

为了使标签助手在所有视图中可用，请将`addTagHelper`语句添加到共享文件_ViewImports.cshtml中（代码文件`MVCSampleApp/Views/_ViewImports.cshtml`）：

```cshtml
@addTagHelper *, Microsoft.AspNet.Mvc.TagHelpers
```

### 使用锚点标签助手

让我们从扩展锚点a元素的标签助手开始。标签助手的示例控制器是`TagHelpersController`。`Index`操作方法返回一个用于展示锚点标签助手的视图（代码文件`MVCSampleApp/Controllers/TagHelpersController.cs`）：

```csharp
public class TagHelpersController : Controller
{
    public IActionResult Index() => View();
    // etc.
}
```

锚点标签助手定义了`asp-controller`和`asp-action`属性。通过这些属性，控制器和操作方法用于构建锚点元素的URL。在第二个和第三个示例中，不需要指定控制器，因为视图来自同一个控制器（代码文件`MVCSampleApp/Views/TagHelpers/Index.cshtml`）：

```html
<a asp-controller="Home" asp-action="Index">Home</a>
<br />
<a asp-action="LabelHelper">Label Tag Helper</a>
<br />
<a asp-action="InputTypeHelper">Input Type Tag Helper</a>
```

以下片段显示了生成的HTML代码。`asp-controller`和`asp-action`属性为`a`元素生成了`href`属性。在第一个示例中，访问Home控制器中的`Index`操作方法，由于两者都是路由定义的默认值，结果中只需一个指向`/`的`href`。当你指定`asp-action`为`LabelHelper`时，`href`指向`/TagHelpers/LabelHelper`，即当前控制器中的`LabelHelper`操作方法：

```html
<a href="/">Home</a>
<br />
<a href="/TagHelpers/LabelHelper">Label Tag Helper</a>
<br />
<a href="/TagHelpers/InputTypeHelper">Input Type Tag Helper</a>
```

### 使用Label标签助手

在下面的代码片段中，我们演示了`label`标签助手的功能。`LabelHelper`操作方法将一个`Menu`对象传递给视图（代码文件`MVCSampleApp/Controllers/TagHelpersController.cs`）：

```csharp
    public IActionResult LabelHelper() => View(GetSampleMenu());

    private Menu GetSampleMenu() =>
        new Menu
        {
            Id = 1,
            Text = "Schweinsbraten mit Kn&ouml;del und Sauerkraut",
            Price = 6.9,
            Date = new DateTime(2016, 10, 5),
            Category = "Main"
        };
}
```

`Menu`类应用了一些数据注解来影响标签助手的输出。请看`Text`属性的`Display`特性。它将`Display`特性的`Name`属性设置为`"Menu"`（代码文件`MVCSampleApp/Models/Menu.cs`）：

```csharp
public class Menu
{
    public int Id { get; set; }

    [Required, StringLength(50)]
    [Display(Name = "Menu")]
    public string Text { get; set; }

    [Display(Name = "Price"), DisplayFormat(DataFormatString = "{0:C}")]
    public double Price { get; set; }

    [DataType(DataType.Date)]
    public DateTime Date { get; set; }

    [StringLength(10)]
    public string Category { get; set; }
}
```

视图使用了应用于`label`控件的`asp-for`属性。此属性使用的值是视图模型的一个属性。使用Visual Studio 2015时，你可以借助IntelliSense访问`Text`、`Price`和`Date`属性（代码文件`MVCSampleApp/Views/TagHelpers/LabelHelper.cshtml`）：

```cshtml
@model MVCSampleApp.Models.Menu
@{
    ViewBag.Title = "Label Tag Helper";
}
<h2>@ViewBag.Title</h2>

<label asp-for="Text"></label>
<br/>
<label asp-for="Price"></label>
<br />
<label asp-for="Date"></label>
```

在生成的HTML代码中，你可以看到`for`属性，它引用了与属性名称同名的元素，其内容可以是属性名称或`Display`特性的值。你还可以使用此属性来本地化值：

```html
<label for="Text">Menu</label>
<br/>
<label for="Price">Price</label>
<br />
<label for="Date">Date</label>
```

### 使用Input标签助手

HTML的`label`元素通常与`input`元素关联。以下代码片段展示了使用带有标签助手的`input`元素所生成的内容：

```html
<label asp-for="Text"></label>
<input asp-for="Text" />
<br/>
<label asp-for="Price"></label>
<input asp-for="Price" />
<br />
<label asp-for="Date"></label>
<input asp-for="Date" />
```
