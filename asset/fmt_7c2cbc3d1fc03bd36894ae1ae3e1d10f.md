
`Response.Redirect(Request.Url.ToString());`

这是必要的，否则主题将不会应用。最后一步是将用户重定向到相同的页面：这样主题就被设置了。最后，你可以使用它的值来设置正确主题。如前，主题需要在 `PreInit` 事件中设置，该事件发生在页面生命周期的早期。在此事件中，你可以检查是否存在所选主题的 Cookie。如果是，你就可以使用它的值来设置正确主题。如前，主题需要在 `PreInit` 事件中设置，该事件发生在页面生命周期的早期。在此事件中，你可以检查是否存在所选主题的 Cookie。如果是，你就可以使用它的值来设置正确主题。

# 230 | 第 6 章 创建外观一致的网站

## 尝试一下应用用户选择的主题

在此练习中，你修改母页并为 `PreInit` 事件添加代码以设置用户主题。

1. 从 `App_Code` 文件夹打开母页文件，并添加在 `PreInit` 事件期间设置主题的代码。你可以将此代码添加到检查页面标题的方法之前或之后。

```vbnet
Private Sub Page_PreInit(sender As Object, e As EventArgs) Handles Me.PreInit
  Dim preferredTheme As HttpCookie = Request.Cookies.Get("PreferredTheme")
  If preferredTheme IsNot Nothing Then
    Dim folder As String = Server.MapPath("~/Themes/" & preferredTheme.Value)
    If System.IO.Directory.Exists(folder) Then
      Page.Theme = preferredTheme.Value
  End If
End Sub
```

```csharp
private void Page_PreInit(object sender, EventArgs e)
{
  HttpCookie preferredTheme = Request.Cookies.Get("PreferredTheme");
  if (preferredTheme != null)
  {
    string folder = Server.MapPath("~/App_Themes/" + preferredTheme.Value);
    if (System.IO.Directory.Exists(folder))
    {
      Page.Theme = preferredTheme.Value;
    }
  }
}
```

对于 C# 示例，你需要在文件顶部包含一条语句将 `Request` 类引入作用域，如下：
`using System.Web;`

2. 如果你使用的是 C#，你还需要在类的构造函数中为 `PreInit` 事件设置事件处理程序，就像你在之前的练习中为 `PreRender` 事件处理程序做的那样。这告诉 ASP.NET 运行方法将处理 `PreInit` 事件：

```csharp
public BasePage()
{
  this.PreRender += Page_PreRender;
  this.PreInit += Page_PreInit;
}
```

## 主题 | 231

### 4. 从列表中选择一个新项目。页面应该重新加载并现在显示另一个主题。

如果你发现浏览器中的页面显示了两个主题的组合，请返回 VS，打开 `Web.config`，从 `<pages>` 元素中删除 `setTheme` 属性，但保留该属性在原处，因为它作为新访问者的默认设置。如果你没有看到主题被应用，请确保你在代码后置（Code Behind）中继承了 `BasePage` 类。

## 工作原理

在已经实现了获取用户最喜爱的主题并将其存储在 cookie 中的困难之后，现在应用主题变得非常简单。`PreInit` 事件处理程序中的代码首先验证是否存在一个名为 `PreferredTheme` 的 cookie。这是通过将 `Get` 方法的返回值与 `Nothing`（C# 中的 `null`）比较来实现的。

```VB.NET
Dim preferredTheme As HttpCookie = Request.Cookies.Get("PreferredTheme")
If preferredTheme IsNot Nothing
```

```c#
HttpCookie preferredTheme = Request.Cookies.Get("PreferredTheme")
if (preferredTheme == null)
```

这段代码使用 `Request.Cookies` 读取用户浏览器随请求一起发送的 cookie。如果 cookie 存在，则使用其 `Value` 属性设置正确的主题：

```VB.NET
Page.Theme = preferredTheme.Value
```

```c#
Page.Theme = preferredTheme.Value;
```

由于主题是在页面生命周期早期设置的，因此此设置将应用于整个页面，有效地为页面赋予了其中定义的视图和感受。为了确保代码不会尝试应用一个（不再）存在的主题，它使用了 `Directory.Exists`，该方法根据磁盘上是否存在文件夹返回 `true` 或 `false`。要获取磁盘上主题文件夹的完整路径，它使用 `Server.MapPath` 将虚拟路径翻译为相应的物理路径。你将在下一章学习更多关于虚拟路径的知识，第 9 章将讨论 `Server.MapPath`。

凭借通过程序设置主题的能力，你为用户提供了一种快速方便的方法来将页面更改为他们喜欢的样式。主题会影响整个网站每个页面的颜色和布局。结合主页（master pages），这为你提供了一种影响整个页面外观和感受的灵活方法。如果你能够更改页面上的某些控件，这可能也会有用。例如，你可能需要为网站中的每个按钮提供相同的外观。这就是 ASP.NET 皮肤（skins）发挥作用的地方。

## 皮肤 (SKINS)

皮肤是简单的文本文件，包含标记，允许你从中心位置定义一个或多个控件的外观和感受。它们放置在主题文件夹中，是 ASP.NET 主题功能的不可或缺的一部分。皮肤文件（带有 `.skin` 扩展名）包含控件的服务器端显示元素。这些设置随后应用到所有应用该皮肤的控件上。要查看这是如何工作的，请考虑以下示例，它定义了一个皮肤——Button 控件的外观：

```asp
<asp:Button BackColor="#cccccc" ForeColor="#308462" runat="server" />
```

通过这种区分，你网站中的按钮将获得 `#cccccc` 的 `BackColor` 和 `#308462` 的 `ForeColor`。你只需要在定义其他内容时创建一个皮肤文件，将此内容添加到标记中即可。从那时起，所有的按钮都将被自动处理。正如你早直接直接在控件上设置属性（如 `BackColor` 和 `ForeColor`）一样，这些属性会被转换为客户端 HTML 和 CSS。

注意，皮肤类似于按钮的标记。首先，皮肤文件中的控件不能有 `ID` 属性。ID 是为了唯一标识页面中的控件，因为皮肤应用到所有控件，所以给它设置 ID 没有意义。另一个区别是可以在标记中可以设置的属性数量。控件并不是所有属性都可以被皮肤化。例如，你可以通过皮肤设置 Button 的 `Enabled` 属性。微软的 MSDN 文档说明了每个属性是否可以皮肤化。发现是否可以设置特定属性的另一种方法是尝试：在皮肤中设置该属性，如果不允许，你将在运行时收到错误。

通常情况下，影响外观的属性（`BackColor`、`ForeColor`、`BorderRadius` 等）是可以皮肤化的，而影响行为的属性（`Enabled`、`EnableViewState` 等）则不能。

当你使用“添加新项”对话框创建新皮肤文件时，你会得到一组封装在服务器端控件块中的文本。你可以安全地删除这些控件，因为它们只是为你提供了一个关于皮肤如何工作的简短示例。你可以在单个皮肤文件中定义多个控件。然而，从维护的角度来看，根据每个皮肤文件所代表的控件来重命名每个皮肤文件更容易。例如，你将拥有一个名为 `Button.skin` 的文件用于按钮，`Label.skin` 用于标签，依此类推。

与其直接将格式元素应用到皮肤中的控件，不如使用 `CssClass` 属性指向你某个 CSS 文件中的 CSS 类。这样，网站更改会变得更加容易，并避免导致最终 HTML 臃肿。根据之前的示例，一个具有以下皮肤定义的文件和主题 CSS 文件中的一个类将产生相同的效果：

```asp
<asp:Button CssClass="MyButton" runat="server" />
```

```css
.MyButton {
  color: #308462;
  background-color: #cccccc;
}
```

## 创建皮肤文件

皮肤文件必须在主题文件夹中创建。要查看这是如何工作的，你应该：

1. 打开主题文件夹。
2. 打开皮肤文件。
3. 在编辑器中输入以下内容：
```asp
<asp:Button CssClass="MyButton" runat="server" />
```
4. 保存文件。
5. 刷新页面。

你将看到按钮现在具有了你定义的样式。要更改外观，请修改 CSS 文件：

```css
.MyButton {
  color: #308462;
  background-color: #cccccc;
}
```

## 尝试为 Button 创建皮肤

要查看这是如何工作的，你应该：

1. 右键点击主题文件夹并选择“添加 > 皮肤”。
2. 命名为 `Button.skin`。
3. 在编辑器中输入：
```asp
<asp:Button BackColor="#cccccc" ForeColor="#308462" runat="server" />
```
4. 保存文件。
5. 刷新页面。

按钮具有你定义的样式。

## 第 6 章 创建一致的网站

要在保持外观一致的同时有效地使用皮肤，你应该：

1. 创建一个新的 Web Form 并命名为 `SkinsDemo`。
2. 从工具箱将一个按钮拖到 MainContent 区域。
3. 输入以下：
```asp
<asp:Content ID="Content2" PlaceholderID="MainContent" runat="Server">
  <asp:Button ID="Button1" runat="Server" Text="Button" />
</asp:Content>
```
4. 保存文件并在浏览器中打开。按钮应该是默认外观。
5. 要更改外观，请创建一个 CSS 文件并添加以下选择器：
```css
.MyButton {
  color: #308462;
  background-color: #cccccc;
}
```
6. 在皮肤文件中，将类添加到按钮上：
```asp
<asp:Button CssClass="MyButton" runat="server" />
```
7. 刷新页面。按钮现在具有了你定义的样式。

## 工作原理

要查看这是如何工作的，你应该查看 HTML。Button 控件已转换为：

```html
<input type="submit" name="ctl100MainContentButton1" value="Button" id="cpMainContent_Button1" class="MyButton" style="background-color:#50EE7;" />
```

## 命名皮肤

命名皮肤与普通皮肤相同，唯一的区别是：它们有一个 `SkinID`，允许你通过名称引用该皮肤。在 ASP 页面中，控件可以使用 `SkinID` 来应用特定的皮肤。下一个练习展示了这是如何工作的。

## 尝试创建一个命名皮肤

创建命名皮肤最简单的方法是复制现有皮肤的代码并添加 `SkinID` 属性。请注意，如果你复制并粘贴皮肤，VS 会自动添加 `ID` 属性（即，如果你将皮肤文件连接到控件编辑器）。

1. 打开 `Button.skin`，复制代码并将其粘贴进去以帮助现有的标记。
2. 如果 VS 添加了 ID 属性，请将其同它的值一起删除（即删除 `ID="Button1"`）。
3. 移除 `CssClass` 属性及其取值，将按钮的 `BackColor`（背景颜色）改为红色（Red），并将 `ForeColor`（前景色）设置为黑色（Black）。
4. 添加一个名为 `RedButton` 的 `SkinID`。你最终将得到这段代码：

```asp
<asp:Button CssClass="MyButton" BackColor="#509EE7" runat="server" />
<asp:Button BackColor="Red" ForeColor="Black" SkinID="RedButton" runat="server" />
```

5. 保存并关闭该 skin 文件。
6. 打开 `SkinsDemo.aspx` 并添加第二个按钮。将此按钮的 `SkinID` 设置为 `RedButton`。注意 IntelliSense（智能感知）如何帮助选择正确的 `SkinID`。现在两个按钮的代码应该看起来像：

```asp
<asp:Button ID="Button1" runat="server" Text="Button" />
<asp:Button runat="server" Text="Button" SkinID="RedButton" />
```

7. 在浏览器中打开 `SkinsDemo.aspx`。你现在应该看到两个按钮：你之前添加的那个以及新建的红底黑字按钮。如果你没有看到不同的颜色，请确保你已经在浏览器中选择了“单色（Monochrome）”主题。

## 工作原理

具名的 skin（Named skins）工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 `SkinsDemo.aspx` 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 `SkinID` 设置为 `RedButton` 的 skin 中获取设置。如果你为控件分配了一个不存在的 `SkinID`，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

## 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```asp
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```

当 `EnableTheming` 设置为 False 时，skin 将不会应用到控件。尽管如此，主题 CSS 文件中的 CSS 设置仍然会被应用。

# 创建一致性页面的实用技巧

以下列表提供了一些关于创建一致性页面的实用技巧：

当你创建一个新网站时，始终从添加一个主页（master page）开始，并以此作为所有其他页面的基础。即使你认为网站只有几个页面，主页也能帮助你确保整个网站外观的一致性。在网站开发的后期阶段添加主页意味着要对现有页面进行大量的手动更改。

一旦你发现自己在为复杂的控件（如 `TreeView` 和 `Menu`，将在下一章讨论）或数据控件（如 `GridView`）添加样式，请考虑为它们创建一个 skin。事实上，你能够从单一位置控制所有控件的布局，这使得更新网站变得更加容易。如果你想覆盖少数控件的布局，可以始终使用带有 `SkinID` 的具名 skin，或者通过将 `EnableTheming` 设置为 False 来禁用 skin。

在创建 skin 或直接在控件上设置属性时，考虑使用 `CssClass` 属性，并将所有与样式相关的属性移动到网站或主题的 CSS 中。这可以减小页面尺寸，并使之后更改布局变得更加容易。

Visual Studio 的导出模板（Export Template）功能是一个非常实用的工具。你不仅可以用它为 ASPX 页面及其后台代码（Code Behind）创建模板，还可以用于其他文件，如类和 CSS 文件，甚至是整个完整的网站。这让你能够快速开始创建新文件。

## 工作

具名的 skin 工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 `SkinsDemo.aspx` 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 `SkinID` 设置为 `RedButton` 的 skin 中获取设置。如果你为控件分配了一个不存在的 `SkinID`，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

## 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```asp
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```
