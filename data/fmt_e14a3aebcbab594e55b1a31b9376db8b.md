
8. 保存 `Web.config` 的更改，重新打开主页并切换到设计视图。你会发现 VS 现在为你的页面应用了正确的信息。

9. 为站点添加另一个主题，在 `App_Themes` 下创建一个新文件夹并命名为 `DarkGrey`。现在，打开你解压随书下载的代码的文件夹。如果你遵循了书中的说明，你的文件夹位于 `C:\ASPNET\Resources`。如果你没有这些文件，可以在 www.wrox.com/go/aspnet-451 获取。打开第 06 章和主题文件夹，将文件资源管理器中的 `DarkGrey` 文件夹拖入 VS 中的 `DarkGrey` 主题文件夹。如果拖放不起用，请在文件资源管理器中使用 `Ctrl+C` 复制文件，然后在 VS 中使用 `Ctrl+V` 将文件粘贴到项目。你的解决方案资源管理器现在应该显示图 6-15。

你将在稍后的条目中添加 CSS 文件引用的图像。

10. 再次打开 `Web.config` 文件，将 `<pages>` 元素中的其他 `Monochrome` 更改为 `DarkGrey`。再次保存更改并按 `Ctrl+F5`。你看到的将不是蓝色的 Monochrome，而是应用了 DarkGrey 主题的网站，如图 6-16 所示。如果你没有看到占位符、主内容和侧边栏并排，请确保你的浏览器足够宽以显示所有内容。

## 扩展主题

除了 CSS 文件和皮肤（在书末尾讨论），主题还可以包含图像。

## 尝试：向你的主题添加图像

在本次尝试中，你将图像和 CSS 文件添加到主题中以完成它们。你覆盖了 Monochrome 主题中的 `Monochrome.css` 文件，因此如果你做了任何想要保留的自定义更改，请先创建其备份。

5. 在浏览器中右键点击 `Default.aspx` 并选择“在浏览器中查看”。你现在将看到带有 DarkGrey 主题图像的网页（如图 6-18 所示），该页面在 Apple 的 Safari 中显示。

![](img/9e033e3b9560597824f8b22941d6d8bb_260_0.png)

图 6-18

6. 回到 VS，打开 `Web.config` 文件，并将 `<pages>` 元素的两个主题属性从 `DarkGrey` 切换为 `Monochrome`。在浏览器中打开 `Default.aspx`，你将看到带有新主题和图片的页面，如图 6-19 所示，该页面在 Google Chrome 中显示。如果你仍然看到旧页面，按 `Ctrl+F5` 进行强制刷新。如果你发现浏览器中的页面显示了两个主题的组合，回到 VS 打开 `Web.config`，并合并 `<pages>` 元素的 `StyleSheet` 属性。

![](img/9e033e3b9560597824f8b22941d6d8bb_260_1.png)

图 6-19

## 工作原理

从某个角度来看，这个练习中没有发生变化。正如你之前看到的那样，主题的样式表被添加到页面的头部（head）。然而，这次样式指向了位于文件夹中的图像。浏览器读取 CSS 文件，顺着图像链接下载它们，然后根据代码中各种 CSS 选择器的指示，在正确的位置显示它们。

为两个主题添加的 CSS 文件都包含一组注释，因此如果你想知道 CSS 的作用，请查看两个文件夹中的文件。

主题对于让页面开发者快速更改网站的外观甚至布局可能非常有用，但如果你让用户在运行时切换它们，它们将变得更加有用。这样，用户就可以根据自己的喜好自定义网站。下一节将向你展示如何实现。

## 动态切换主题

在运行时切换主题有其优势。例如，你可以通过允许用户选择他们喜欢的颜色和布局的主题来取悦用户。并不是所有人都喜欢黑底白字，因此运行时更改的选项是许多人喜的。然而，你还可以将主题部署给视障用户。通过创建一个具有高对比度颜色方案和大字体大小的主题，你让人们更容易看到他们的网站。Planet Wrox 网站中的主题仅显示颜色和布局等屏幕元素，创建其中一个主题的副本非常容易。

由于主题在运行时应用的方式，你需要在页面的生命周期早期设置主题，准确地说，是在 `PreInit` 事件中。网站的基础页面再次是执行此操作的理想位置，因为网站中的每个页面都继承自此类。

为了让用户更改主题，你可以为他们提供一个下拉菜单，该菜单会自动将活动选项回传到服务器。在列表中从列表中获取选定的主题，将其应用于页面，并将选择存储在 cookie 中，以便在访问网站时可以检索。

Cookies 是存储在用户计算机上的一小段文本。你在 cookie 中存储的数据只会发送到第一个设置它的服务器，因此其他网站无法从你的站点读取 cookie。然而，由于 cookie 以明文形式存储在用户的计算机上，你不应该使用它们来存储任何敏感数据（如密码）。尽管如此，存储无害的首选主题是使用 cookie 的极佳方式。

要创建一个 cookie 并将其存储在用户的计算机上，你使用响应对象上的 `Cookies` 集合。这样，cookie 就会随响应发送到浏览器。这是一个简单的示例：

### VB.NET

```
Dim myCookie As HttpCookie = New HttpCookie("6")

myCookie.Expires = DateTime.Now.AddMonths(3)

myCookie.Value = "Cookie value"

Response.Cookies.Add(myCookie)
```

### C#

此代码将 cookie 发送到浏览器，它将一直存储直到过期，在本示例中，过期是在设置 cookie 的三个月后。对页面的每次请求，浏览器都会将此 cookie 发回服务器，你可以使用请求 对象的 `Cookies` 集合再次读取它，如下：

### VB.NET

```
Dim myCookie As HttpCookie = Request.Cookies.Get("CookieName")

If myCookie Is Not Nothing Then
    Label1.Text = myCookie.Value ' 将显示 "Cookie value"
End If
```

### C#

```csharp
HttpCookie myCookie = Request.Cookies.Get("CookieName");
If (myCookie != null)
{
    Label1.Text = myCookie.Value // 将显示 "Cookie value"
}
```

在接下来的两个练习中，我们将看到如何使用主页让用户选择主题。第一个练习将引导你修改主页，获取用户选择的主题名称并将其存储在 cookie 中。第二个练习将向你展示如何在运行时将该主题应用于继承自 `BasePage` 的每个页面。

> 注意 关于 cookie 以及它们是否会损害你的隐私存在很多争论。通常情况下，cookie 是安全的，因为它们只存储服务器已经拥有的数据。如果你没有将这些数据提供给你的服务器，它们就无法用于从你的计算机中窃取敏感数据。在大多数情况下，cookie 通过记住一小段数据来提高用户的浏览体验，而不是在每次访问页面时都询问。遗憾的是，像广告公司这样的大公司使用唯一的 cookie 来跟踪你在互联网上的行踪，从而获得关于你访问过的网站的全局信息。为了确保访问你网站的游客了解你关于他们的哪些信息，在网站上添加隐私声明通常是一个好主意，说明 cookie 的意图、用途以及你可能保留的任何个人数据。请注意，在欧洲，你必须遵守“cookie 法”，该法律不允许在未获得用户同意的情况下创建 cookie。

# 第 6 章创建外观一致的网站

## 尝试：让用户选择主题

在这个练习中，你向主页添加一个 `DropDownList` 控件。该控件包含你可以选择的所有可用主题。用户的选择被存储在 cookie 中，以便以后再次使用。最后一步是当用户重新访问页面时，在下拉列表中预选正确的主题。

- 1. 在标记视图（Markup View）中打开主页并找到 `<aside>` 元素。从工具箱中拖入 `DropDownList` 替换静态文本。将 ID 从 `DropDown1` 更改为 `ThemeList`。在下拉列表前添加一行 `<br>`（例如：选择主题）以阐明该文本的目的。
- 2. 打开控件的智能任务面板（在设计视图或标记视图中），启用 `AutoPostBack`。
- 3. 在同一个智能任务面板中，点击 `Items` 列表插入两个项目：一个为 `Monochrome`，另一个为 `DarkGrey`。
- 4. 在设计视图中双击下拉列表以为 `SelectedIndex` 事件设置事件处理程序。除了双击，你也可以选择 `DropList`，按 `F4` 打开其属性网，点击带有闪电图标的按钮选择事件，双击 `SelectedIndex`。图 6-20 显示了事件模式下的属性网。

![](/img/9e033e3b9560597824f8b22941d6d8bb_263_0.png)

图 6-20

如你所知，你也可以直接在标记视图的控件声明中添加此事件处理程序。

当用户在客户端下拉列表中做出选择时，你在 `SelectedIndex` 处理程序中编写的代码将在服务器端触发。在处理器块中，添加以下代码，从存储器检索主题并存储在 cookie 中：

VB.NET

```
Protected Sub ThemeList_SelectedIndex(sender As Object, 
                                e As EventArgs) Handles ThemeList.SelectedIndex
Dim preferredTheme As HttpCookie = New HttpCookie("*PreferredTheme*")
preferredTheme.Expires = DateTime.Now.AddMonths(3)
preferredTheme.Value = ThemeList.SelectedIndexValue
Response.Cookies.Add(preferredTheme)
Response.Redirect(Request.Url.ToString())
End Sub
```

C#

```csharp
protected void ThemeList_SelectedIndexChanged(object sender, EventArgs e)
{
    HttpCookie preferredTheme = new HttpCookie("*PreferredTheme*");
    preferredTheme.Expires = DateTime.Now.AddMonths(3);
    preferredTheme.Value = ThemeList.SelectedIndexValue;
    Response.Cookies.Add(preferredTheme);
    Response.Redirect(Request.Url.ToString());
}
```

5. 在母页的代码后台（Code Behind）中，你需要再次添加一些代码，在页面加载时重新预选列表中的正确项。此操作的最佳位置 Page 类的 `Load` 事件中。如果你使用 C#，`Page_Load` 句程序应该已经存在了。如果你使用 Visual Basic，可以通过两种方式添加：要么在设计视图（Design View）中双击页面的任意位置（这在 C# 中同样有效），或者在代码后台的文档窗口上方的下拉列表中选择（Page Events，页面事件）（见图 6-21），然后从第二个下拉列表中选择 `Load`。这是为其他控件（如 Button 和 DropDownList）添加处理程序的一种很好的方法。

![](img/9e033e3b9560597824f8b22941d6d8bb_264_0.png)

图 6-21

在 VS 为你添加的处理程序内部，添加以下代码：

### VB.NET

```vbnet
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    If Not Page.IsPostBack Then
        Dim selectedTheme As String = Page.Theme
        Dim preferredTheme As HttpCookie = Request.Cookies.Get("PreferredTheme")
        If preferredTheme IsNot Nothing Then
            selectedTheme = preferredTheme.Value
        End If
        If Not String.IsNullOrEmpty(selectedTheme) Then
            Dim item As ListItem = ThemeList.Items.FindByValue(selectedTheme)
            If item IsNot Nothing Then
                item.Selected = True
            End If
        End If
    End If
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs args)
{
    if (!Page.IsPostBack)
    {
        string selectedTheme = Page.Theme;
        HttpCookie preferredTheme = Request.Cookies.Get("PreferredTheme");
        if (preferredTheme != null)
        {
            selectedTheme = preferredTheme.Value;
        }
        if (!string.IsNullOrEmpty(selectedTheme))
        {
            ListItem item = ThemeList.Items.FindByValue(selectedTheme);
            if (item != null)
            {
                item.Selected = true;
            }
        }
    }
}
```

# 第 6 章 创建外观一致的网站

6. 保存所有更改并在浏览器中请求 `Default.aspx`。侧边栏中的下拉列表应该显示列表中的第一个项。从列表中选择其他选项，页面将刷新。下拉列表中你最后选择的项现在应该是被预选的。关闭浏览器然后访问 `Default.aspx`。下拉列表中你选择的主题仍然应该是选中的。注意，你在编写任何代码的情况下应用了所选主题。

> 常见错误
> 如果遇到错误，请确保代码中没有拼写错误。如果什么都没有发生（例如页面没有回传），请检查是否在 `DropDownList` 上使用了 `AutoPostBack` 属性来控制它。此外，检查 `PreferredTheme` 名称的拼写。最后，如果在回传或刷新后正确项未预选，检查你的浏览器或计算机设置。你可能配置了浏览器完全阻止了 Cookie。如果无法运行，请尝试另一个浏览器以排除代码问题。

## 工作原理

你对母页进行了三个更改。首先，你在 `PreInit` 事件中添加了下拉列表并将 `PostBack` 设置为 `True`。这导致当你选择新项时，页面会立即提交回服务器。当发生这种情况时，`SelectedIndexChanged` 处理程序触发。此代码创建了一个存储在用户计算机上的 Cookie。在浏览器会话之间，你需要设置 `Expires` 属性。在示例中，Cookie 设置为三个月后过期，这意味着浏览器之后将其丢弃。每当用户选择新主题时，日期都会延长，将其设置为三个月：

### VB.NET

```vbnet
Dim preferredTheme As HttpCookie = New HttpCookie("PreferredTheme")
preferredTheme.Expires = DateTime.Now.AddMonths(3)
```

### C#

```csharp
Cookie preferredTheme = new HttpCookie("PreferredTheme");
preferredTheme.Expires = DateTime.Now.AddMonths(3);
```

创建 Cookie 后，你可以设置它的 `Value` 属性。在示例中，DropDown 的 `SelectedValue`（包含主题）存储在 Cookie 中。使用 `Response.Cookies.Add` 将 Cookie 添加到 Cookies 集合中：

### VB.NET

```vbnet
preferredTheme.Value = ThemeList.SelectedValue
Response.Cookies.Add(preferredTheme)
```

### C#

```csharp
preferredTheme.Value = ThemeList.SelectedValue;
Response.Cookies.Add(preferredTheme);
```

注意，Cookie 被添加到与用户响应相关的 `Response` 对象的 Cookies 集合中。你可以查看如何从用户请求页面的 `Request` 对象的 Cookies 集合中重定向此 Cookie。

最后一步是将用户重定向到相同的页面：

### VB.NET

```vbnet
Response.Redirect(Request.Url.ToString())
```

### C#
