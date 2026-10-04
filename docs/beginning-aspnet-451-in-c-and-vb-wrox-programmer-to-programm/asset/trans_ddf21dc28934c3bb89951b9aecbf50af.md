

# 在 LINQ 查询中使用模型绑定 | 531

```xml
<asp:DropDownList ID="PhotoAlbumList" runat="server" AutoPostBack="True"
DataTextField="Name" DataValueField="Id" SelectMethod="PhotoAlbumList_GetData"
OnItemSelectedChanged="PhotoAlbumList_SelectedIndexChanged"
</asp:DropDownList>
```

4. 如必要，请选择代码后面（Code Behind）。在代码顶部，紧接类定义之后，添加以下行代码来实例化一个新的 `PlanetWroxEntities` 实例：

VB.NET
```vb
Partial Class PhotoAlbums_Default
Inherits BasePage
Dim entities As New PlanetWroxEntities()
```

```csharp
public partial class PhotoAlbums_Default : BasePage
{
    PlanetWroxEntities entities = new PlanetWroxEntities();
```

由于该类中的多个方法都需要访问 `Planet-WroxEntities`，因此创建一个类作用范围内的单个实例供所有方法使用，比在每个方法内部都创建一个新实例要合理。

5. 接下来，创建 `PhotoAlbumList_GetData` 方法并按照如下方式实现它：

VB.NET
```vb
Public Function PhotoAlbumList_GetData() As Enumerable(Of PhotoAlbum)
Return p from entities.PhotoAlbums
       Order By p.Id
       Select p
```

```csharp
public IEnumerable<PhotoAlbum> PhotoAlbumList_GetData()
{
    return p from entities.PhotoAlbums
           orderby p.Id
           select p;
}
```

此方法查询所有 `PhotoAlbum` 实例并按 ID 排序返回。该方法的返回类型是 `PhotoAlbum` 的 `Enumerable`，这意味着该集合只能用于枚举。这正是此练习所需要的，因为 `PhotoAlbum` 实例只显示在 `DropDownList` 中。你将在 `SelectedIndexChanged` 处理程序中添加代码。

6. 回到标记视图（Markup View），并紧接 `DropDownList` 下方插入以下用于 `ListView` 控件的代码，让 Visual 为 `SelectMethod` 创建名称并在代码后面中生成相应的代码：

```xml
<asp:ListView ID="ListView" runat="server" DataKeyNames="Id"
ItemTemplate="Picture" SelectMethod="ListView_GetData">
<EmptyDataTemplate>
未找到此相册的图片。
</EmptyDataTemplate>
```

*

# 532 | 第 14 章 LINQ 与 ADO.NET 实体框架

```xml
<ItemTemplate>
<<li>
  <asp:Image ID="Image" runat="server" ImageUrl='<%# Item.ImageUrl %>'
  Tooltip='<%# Item.Tooltip %>' />
  <asp:Label ID="Description" runat="server" Text='<%# Item.Description %>' />
</</li>
</ItemTemplate>
<LayoutTemplate>
<ul class="ItemContainer">
  <li id="itemplaceholder" runat="server" />
</ul>
<!-- 待办：添加 DataPager -- -->
</LayoutTemplate>
</asp:ListView>
```

这创建了一个图片，其 `ImageUrl` 和 `Tooltip` 属性绑定到你将绑定的 `Picture` 对象的对应属性上。当在浏览器中悬停在图片上时，会显示 `Tooltip`。在图片旁边，有一个简单的 `Label` 控件控制图片的描述。

- 7. 对于 `<ul>` 元素，将占位符文本替换为以下用于 `DataPager` 代码。你可以手动输入代码，也可以在标记视图中从工具箱中拖入 `Data` 。
```xml
<div style="clear: both;">
<asp:DataPager ID="DataPager1" runat="server" PageSize="3">
<Fields>
<asp:NextPreviousPageField ButtonType="Button"
ShowFirstPageButton="True" ShowLastPageButton="True" />
</Fields>
</asp:DataPager>
</div>
```

- 8. 将整个代码封装在 `UpdatePanel` 的 `cpMainContent` 块中，以避免在分页图片列表或从列表中选择新相册时出现闪烁。
```xml
<asp:Content ID="Content2" ContentHolderID="cpMainContent" runat="Server">
<asp:UpdatePanel ID="UpdatePanel" runat="server">
<ContentTemplate>

</ContentTemplate>
</asp:UpdatePanel>
</asp:Content>
```

- 9. 切换到代码后面并如下方式实现 `ListView_GetData` 方法：

VB.NET
```vb
Public Function ListView1_GetData() As IQueryable(Of Picture)
  Dim photoAlbumId As Integer = Convert.ToInt32(PhotoAlbumList.SelectedValue)
  Return From p in entities.Pictures
    where p.PhotoAlbumId = photoAlbumId
    Order By p.Id
    select p
End Function
```

C#
```csharp
public IQueryable<Picture> ListView1_GetData()
{
    int photoAlbumId = Convert.ToInt32(PhotoAlbumList.SelectedValue);
    return from p in entities.Pictures
        where p.PhotoAlbumId == photoAlbumId
        orderby p.Id
        select p;
}
```

10. 仍然在代码后面，向 Visual Studio 在第 3 步中添加的 `PhotoAlbumList_SelectedIndexChanged` 方法中添加以下高亮行：

VB.NET
```vb
Public Sub PhotoAlbumList_SelectedIndexChanged(sender As Object, e As EventArgs)
    Handles PhotoAlbumList.SelectedIndexChanged
    ListView1.DataBind()
End Sub
```

C#
```csharp
protected void PhotoAlbumList_SelectedIndexChanged(object sender, EventArgs e)
{
    ListView1.DataBind();
}
```

11. 打开该网站的 `web.s` 文件，并在 Reviews 和 About 部分之间为 Gig Pics 部分添加主菜单和两个子菜单项：
```xml
<siteMapNode url="/PhotoAlbum/" title="Gig Pics" description="All Gig Pics">
    <siteMapNode url="/PhotoAlbum/Default/" title="Gig Pics" description="All Gig Pics" />
    <siteMapNode url="/NewPhoto/" title="New Album" description="create a New Album with Gig Pics" />
</siteMapNode>
<siteMapNode url="/About/Default/" title="About" description="About this site" />
```

12. 因为你添加了另一个菜单项，需要更改 Monochrome 中每个项的宽度。要执行此操作，打开 `Monochrome.css` 并将 `.MainMenu li` 的宽度从 200 像素更改为 160 像素：
```css
.MainMenu li {
    width: 160px;
}
```

13. 保存所有更改并从 `PhotoAlbums` 文件夹请求 `Default.aspx`。从列表中选择一个相册，页面将重新加载并显示相关的图片。

# 常见错误

如果从下拉列表中选择新项时没有发生任何，请回到 VS 并确保你将 `DropDownList` 控件上的 `AutoPostBack` 设置为 `True`。

如果你在相册中没有任何图片，或者不想填满整个页面，请从 Gig Pics 菜单创建 `New Album`，创建一个新相册，并为其添加至少四张图片。然后点击 Gig Pics 项并从列表中选择你的相册。注意，现在有一个分页界面，允许使用屏幕底部的 `First`、`Previous` 和 `Last` 按钮在图片列表中前后移动。由于你添加了 AJAX 面板，选择和分页操作现在是无闪烁地进行的。

注意：你的前几个相册将会损坏的。这是因为你在创建它们时没有提供图片。如果你想清理一下，可以从数据库中删除相册（及其关联图片）。在第 16 章中，你将开发从 `Default.aspx` 页面删除图片的功能。

![](img/9e033eb9560597824f8b22941d6dbb571_0.png)

图 14-1

# 工作原理

创建了一个图片，其 `ImageUrl` 和 `Tooltip` 属性绑定到你将绑定的 `Picture` 对象的对应属性上。当在浏览器中悬停在图片上时，会显示 `Tooltip`。在图片旁边，有一个简单的 `Label` 控件控制图片的描述。

- 7. 对于 `<ul>` 元素，将占位符文本替换为以下用于 `DataPager` 代码。你可以手动输入代码，也可以在标记视图中从工具箱中拖入 `Data` 。
```xml
<div style="clear: both;">
<asp:DataPager ID="DataPager1" runat="server" PageSize="3">
<Fields>
<asp:NextPreviousPageField ButtonType="Button"
ShowFirstPageButton="True" ShowLastPageButton="True" />
</Fields>
</asp:DataPager>
</div>
```

- 8. 将整个代码封装在 `UpdatePanel` 的 `cpMainContent` 块中，以避免在分页图片列表或从列表中选择新相册时出现闪烁。
```xml
<asp:Content ID="Content2" ContentHolderID="cpMainContent" runat="Server">
<asp:UpdatePanel ID="UpdatePanel" runat="server">
<ContentTemplate>

</ContentTemplate>
</asp:UpdatePanel>
</asp:Content>
```

- 9. 切换到代码后面并如下方式实现 `ListView_GetData` 方法：

VB.NET
```vb
Public Function ListView1_GetData() As IQueryable(Of Picture)
  Dim photoAlbumId As Integer = Convert.ToInt32(PhotoAlbumList.SelectedValue)
  Return From p in entities.Pictures
    where p.PhotoAlbumId = photoAlbumId
    Order By p.Id
    select p
End Function
```

C#
```csharp
public IQueryable<Picture> ListView1_GetData()
{
    int photoAlbumId = Convert.ToInt32(PhotoAlbumList.SelectedValue);
    return from p in entities.Pictures
        where p.PhotoAlbumId == photoAlbumId
        orderby p.Id
        select p;
}
```

10. 仍然在代码后面，向 Visual Studio 在第 3 步中添加的 `PhotoAlbumList_SelectedIndexChanged` 方法中添加以下高亮行：

VB.NET
```vb
Public Sub PhotoAlbumList_SelectedIndexChanged(sender As Object, e As EventArgs)
    Handles PhotoAlbumList.SelectedIndexChanged
    ListView1.DataBind()
End Sub
```

C#
```csharp
protected void PhotoAlbumList_SelectedIndexChanged(object sender, EventArgs e)
{
    ListView1.DataBind();
}
```

11. 打开该网站的 `web.s` 文件，并在 Reviews 和 About 部分之间为 Gig Pics 部分添加主菜单和两个子菜单项：
```xml
<siteMapNode url="/PhotoAlbum/" title="Gig Pics" description="All Gig Pics">
    <siteMapNode url="/PhotoAlbum/Default/" title="Gig Pics" description="All Gig Pics" />
    <siteMapNode url="/NewPhoto/" title="New Album" description="create a New Album with Gig Pics" />
</siteMapNode>
<siteMapNode url="/About/Default/" title="About" description="About this site" />
```

12. 因为你添加了另一个菜单项，需要更改 Monochrome 中每个项的宽度。要执行此操作，打开 `Monochrome.css` 并将 `.MainMenu li` 的宽度从 200 像素更改为 160 像素：
```css
.MainMenu li {
    width: 160px;
}
```

13. 保存所有更改并从 `PhotoAlbums` 文件夹请求 `Default.aspx`。从列表中选择一个相册，页面将重新加载并显示相关的图片。

# 常见错误

如果从下拉列表中选择新项时没有发生任何，请回到 VS 并确保你将 `DropDownList` 控件上的 `AutoPostBack` 设置为 `True`。

如果你在相册中没有任何图片，或者不想填满整个页面，请从 Gig Pics 菜单创建 `New Album`，创建一个新相册，并为其添加至少四张图片。然后点击 Gig Pics 项并从列表中选择你的相册。注意，现在有一个分页界面，允许使用屏幕底部的 `First`、`Previous` 和 `Last` 按钮在图片列表中前后移动。由于你添加了 AJAX 面板，选择和分页操作现在是无闪烁地进行的。

注意：你的前几个相册将会损坏的。这是因为你在创建它们时没有提供图片。如果你想清理一下，可以从数据库中删除相册（及其关联图片）。在第 16 章中，你将开发从 `Default.aspx` 页面删除图片的功能。

![](img/9e033eb9560597824f8b22941d6dbb571_0.png)

图 14-1

# 工作原理

创建了一个图片，其 `ImageUrl` 和 `Tooltip` 属性绑定到你将绑定的 `Picture` 对象的对应属性上。当在浏览器中悬停在图片上时，会显示 `Tooltip`。在图片旁边，有一个简单的 `Label` 控件控制图片的描述。

- 7. 对于 `<ul>` 元素，将占位符文本替换为以下用于 `DataPager` 代码。你可以手动输入代码，也可以在标记视图中从工具箱中拖入 `Data` 。
```xml
<div style="clear: both;">
<asp:DataPager ID="DataPager1" runat="server" PageSize="3">
<Fields>
<asp:NextPreviousPageField ButtonType="Button"
ShowFirstPageButton="True" ShowLastPageButton="True" />
</Fields>
</asp:DataPager>
</div>
```

- 8. 将整个代码封装在 `UpdatePanel` 的 `cpMainContent` 块中，以避免在分页图片列表或从列表中选择新相册时出现闪烁。
```xml
<asp:Content ID="Content2" ContentHolderID="cpMainContent" runat="Server">
<asp:UpdatePanel ID="UpdatePanel" runat="server">
<ContentTemplate>

</ContentTemplate>
</asp:UpdatePanel>
</asp:Content>
```

- 9. 切换到代码后面并如下方式实现 `ListView_GetData` 方法：

VB.NET
```vb
Public Function ListView1_GetData() As IQueryable(Of Picture)
  Dim photoAlbumId As Integer = Convert.ToInt32(PhotoAlbumList.SelectedValue)
  Return From p in entities.Pictures
    where p.PhotoAlbumId = photoAlbumId
    Order By p.Id
    select p
End Function
```

C#
```csharp
public IQueryable<Picture> ListView1_GetData()
{
    int photoAlbumId = Convert.ToInt32(PhotoAlbumList.SelectedValue);
    return from p in entities.Pictures
        where p.PhotoAlbumId == photoAlbumId
        orderby p.Id
        select p;
}
```

# 关于性能的说明

之前的练习有一个已知的性能问题，你应该注意。虽然 `ListView` 的 `ItemTemplate` 在浏览器中通过拉伸宽度将图片缩调整为 180 像素，但实际图片保持未修改。这意味着如果你上传了大的

