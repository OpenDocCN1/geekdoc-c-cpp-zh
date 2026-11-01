

因为它不会在视图状态中维护其状态。本练习的第二部分随后向您展示如何实现能够维护其状态的 `NavigateUrl` 属性。

- 1. 打开 `AboutUs.aspx` 的代码隐藏文件，并将以下粗体代码添加到 `Page_Load` 事件处理程序中。如果该处理程序尚不存在，请切换到设计视图，并双击页面灰色区域的任意位置。

```vb.net
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    If Not Page.IsPostBack Then
        Banner2.DisplayDirection = Direction.Vertical
    End If
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (!Page.IsPostBack)
    {
        Banner2.DisplayDirection = Direction.Vertical;
    }
}
```

验证页面的标记视图中的 Banner 用户控件是否具有 `ID` `Banner2`，或者相应地更新你的代码。

- 2. 切换到设计视图，将工具箱的“标准”类别中的 Button 控件拖到页面内的 `Banner.ascx` 控件上（而不是母版页中定义的控件）。无需为 Button 控件的 `Click` 事件编写任何代码。

- 3. 保存页面并在浏览器中打开。由于 `Page_Load` 中的代码，页面首次加载时，屏幕底部的横幅显示垂直横幅。现在单击按钮，页面将重新加载。这一次，页面显示水平图片。因为 Banner 控件的 `DisplayDirection` 仅在 `Page.IsPostBack` 为 `False` 时在 `Page_Load` 中设置，所以当你回发时该设置会丢失，导致横幅恢复为默认设置 `Horizontal`。

- 4. 为了避免 `NavigateUrl` 出现此问题，你需要将其实现为视图状态属性，使用 `ViewState` 集合作为后备存储来存储底层值。这样，该值会随每个请求发送到浏览器并返回服务器。要实现该属性，请将以下代码添加到 `Banner.ascx` 用户控件的代码隐藏中，就在你之前创建的 `DisplayDirection` 属性下方。

请记住，你不必手动输入所有这些代码，因为本书附带的下载内容包含所有显示的代码。

```vb.net
Public Property NavigateUrl() As String
    Get
        Dim _navigateUrl As Object = ViewState("NavigateUrl")
```

## 工作原理

在前三个步骤中，你了解了非视图状态属性的行为。你首先在 `Page_Load` 事件处理程序中编写了一些代码，以编程方式设置 `DisplayDirection`：

```vb.net
If Not Page.IsPostBack Then
    Banner2.DisplayDirection = Direction.Vertical
End If
```

```csharp
if (!Page.IsPostBack)
{
    Banner2.DisplayDirection = Direction.Vertical;
}
```

由于对 `Page.IsPostBack` 的检查，此代码仅在页面首次加载时触发。当页面因回发而重新加载时，它不会触发。当它触发时，它会设置 Banner 控件的 `DisplayDirection` 属性，以便横幅显示正确的图像。但是，一旦页面被回发，该值就会丢失，控件将恢复为其默认方向 `Horizontal`。克服此问题的一种方法是确保代码在首次加载和随后的回发时都触发。删除对 `Page.IsPostBack` 的检查就足以实现这一点。然而，这并不总是理想的解决方案。假设你从数据库获取正确的显示方向。因为从数据库获取数据是一项代价高昂的操作，你希望尽量减少访问数据库的次数。在这种情况下，开发人员可能只在页面首次加载时获取数据，并期望在随后的回发中该数据仍然存在。这正是 `NavigateUrl` 属性所做的。你设置它的值一次，它就一直可用，即使你将页面回发到服务器。这是通过视图状态属性实现的。

要了解其工作原理，请先看一下该属性的 `setter`：

```vb.net
Public Property NavigateUrl() As String
...
    Set(Value As String)
        ViewState("NavigateUrl") = Value
    End Set
End Property
```

```csharp
public string NavigateUrl
{
    ...
    set
    {
        ViewState["NavigateUrl"] = value;
    }
}
```

当你向 `NavigateUrl` 属性赋值时，其值存储在 `ViewState` 集合中。你可以将 `ViewState` 集合视为一个袋子，它允许你存储数据，以便在回发后再次检索。你使用唯一键标识视图状态中的值。在示例中，键等于属性的名称，因此很容易看出它们属于同一项。一旦你向视图状态属性赋值，它就会存储在页面的隐藏 `__VIEWSTATE` 字段中，你在第 4 章中已经了解了该字段。这意味着当页面加载时它会发送到浏览器，当页面再次回发时它会发送回服务器。

当回发发生时，用户控件中的 `Page_Load` 代码再次触发。与初始请求一样，代码在 `Select Case`/`switch` 块中访问 `NavigateUrl` 属性：

```vb.net
Case Direction.Horizontal
    ...
    HorizontalLink.HRef = NavigateUrl
    ...
```

```csharp
case Direction.Horizontal:
    ...
    HorizontalLink.HRef = NavigateUrl;
    ...
```

`NavigateUrl` 的值由属性的 `getter` 返回：

```vb.net
Public Property NavigateUrl() As String
    Get
        Dim _navigateUrl As Object = ViewState("NavigateUrl")
        If _navigateUrl IsNot Nothing Then
            Return CType(_navigateUrl, String)
        Else
            Return "http://p2p.wrox.com"  ' Return a default value
        End If
    End Get
    ...
End Property
```

```csharp
public string NavigateUrl
{
    get
    {
        object _navigateUrl = ViewState["NavigateUrl"];
        if ( _navigateUrl != null)
        {
            return (string)_navigateUrl;
        }
        else
        {
            return "http://p2p.wrox.com";  // Return a default value
        }
    }
    ...
}
```

此代码首先尝试使用 VB.NET 中的 `ViewState("NavigateUrl")` 或 C# 中的 `ViewState["NavigateUrl"]` 从 View State 中获取值，后者使用方括号访问集合中的项。如果返回的值为 `Nothing` 或 `null`，则 `getter` 返回该属性的默认值：`http://p2p.wrox.com`。

但是，如果该值不是 `Nothing`，则使用 VB.NET 中的 `CType` 和 C# 中的 `(string)` 将其转换为字符串，并最终返回给调用代码。最后，从视图状态属性返回的 `NavigateUrl` 再次分配给 `anchor` 标签的 `href` 属性，该属性随后用作单击图像时用户被带到的 URL。

## 视图状态注意事项

尽管 View State 旨在克服前面练习中概述的维护状态问题，但你应该仔细考虑是否使用它。你存储在 View State 中的值会随着每个请求发送到浏览器并返回服务器。当你将许多或大的值存储在 View State 中时，这会增加页面的大小，从而对性能产生负面影响。切勿将大型对象（如数据库记录）存储在 View State 中；如果需要存储的数据量很大，通常每次请求从数据库重新获取数据比在隐藏的 View State 字段中传递数据更快。此外，由于 View State 存储在页面内并因此在网络上传输，你不应使用它来存储敏感值，如密码。

## 关于用户控件的实用技巧

以下列表提供了一些使用用户控件的实用技巧：

- 不要过度使用用户控件。用户控件非常适合封装重复的内容，但它们也会使你的站点管理变得稍困难，因为代码和逻辑包含在多个文件中。如果你不确定某些内容是否会在站点的其他部分被重用，可以先将它直接嵌入页面中。如果以后需要，你随时可以将其移动到单独的用户控件中。
- 保持用户控件专注于单一任务。不要创建一个能够显示五种不同类型不相关内容且通过一个属性决定显示什么的用户控件。这会使控件难以维护和使用。相反，创建五个轻量级控件并适当地使用它们。
- 当你创建包含样式化标记的用户控件时，不要硬编码诸如 `CssClass` 之类的样式信息，例如用户控件中包含的服务器控件的 `CssClass`。相反，考虑在用户控件上创建单独的 `CssClass` 属性，然后用这些属性来设置服务器控件的 `CssClass`。这提高了用户控件的可重用性，使其更容易融入不同的设计中。

