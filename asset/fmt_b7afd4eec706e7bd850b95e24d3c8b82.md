
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

## 常见错误

如果从下拉列表中选择新项时没有发生任何，请回到 VS 并确保你将 `DropDownList` 控件上的 `AutoPostBack` 设置为 `True`。

如果你在相册中没有任何图片，或者不想填满整个页面，请从 Gig Pics 菜单创建 `New Album`，创建一个新相册，并为其添加至少四张图片。然后点击 Gig Pics 项并从列表中选择你的相册。注意，现在有一个分页界面，允许使用屏幕底部的 `First`、`Previous` 和 `Last` 按钮在图片列表中前后移动。由于你添加了 AJAX 面板，选择和分页操作现在是无闪烁地进行的。

注意：你的前几个相册将会损坏的。这是因为你在创建它们时没有提供图片。如果你想清理一下，可以从数据库中删除相册（及其关联图片）。在第 16 章中，你将开发从 `Default.aspx` 页面删除图片的功能。

![](img/9e033eb9560597824f8b22941d6dbb571_0.png)

图 14-1

## 工作原理

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

## 常见错误

如果从下拉列表中选择新项时没有发生任何，请回到 VS 并确保你将 `DropDownList` 控件上的 `AutoPostBack` 设置为 `True`。

如果你在相册中没有任何图片，或者不想填满整个页面，请从 Gig Pics 菜单创建 `New Album`，创建一个新相册，并为其添加至少四张图片。然后点击 Gig Pics 项并从列表中选择你的相册。注意，现在有一个分页界面，允许使用屏幕底部的 `First`、`Previous` 和 `Last` 按钮在图片列表中前后移动。由于你添加了 AJAX 面板，选择和分页操作现在是无闪烁地进行的。

注意：你的前几个相册将会损坏的。这是因为你在创建它们时没有提供图片。如果你想清理一下，可以从数据库中删除相册（及其关联图片）。在第 16 章中，你将开发从 `Default.aspx` 页面删除图片的功能。

![](img/9e033eb9560597824f8b22941d6dbb571_0.png)

图 14-1

## 工作原理

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

对于图像，整个图像仍然被下载，仅显示为较小的缩略图。更好的做法是在服务器端创建真正的缩略图，并将其发送到浏览器。我的书籍《ASP.NET 2.0 Instant Results》(ISBN: 978-0-471-74951-6）中名为“Greeting Cards”的章节有许多在服务器上调整图像大小的示例。

# 实用的 LINQ 和 ADO.NET Entity Framework 技巧

这里是一些实用的 LINQ 和 ADO.NET Entity Framework 技巧：

- 在本章中，你展示了如何创建匿名类型来构建你想要从查询中返回的数据。编译器和 IntelliSense 是确定你可以返回什么以及可以使用哪些属性的宝贵工具。花些时间玩玩匿名类型，查看 IntelliSense 提供的不同选项。

- 就像其他数据访问方法一样，使用 `SqlDataSource` 来尽可能地控制你的数据。如果你只需要爵士乐（Jazz）流派评论，请明确并在代码中包含 `Where` 子句，在数据库级别限制评论列表。这可以加速你的查询和数据检索，提高应用程序的整体速度。

- 利用匿名类型来减少 LINQ 查询的内存消耗。例如，与其检索整个 `Review` 对象，不如使用 `New`（C# 中为 `new`）关键字动态创建一个新的匿名类型。因为此对象只包含你需要的属性，所以可以节省引入完整对象的开销。

## 总结

LINQ 是一项随 .NET 提供的强大且令人兴奋的技术。LINQ 是许多数据访问场景中重要的基础技术，包括在 ways ADO.NET Entity Framework 的 ASP.NET Web应用程序中访问数据库。

由于 LINQ 非常重要，它已经集成到 .NET 的许多地方。LINQ 适用于对象，允许你查询内存中的集合。此外，LINQ 还适用于 XML、ADO.NET 和 DataSets，每个类型提供了对不同数据存储的访问，但使用相同的统一查询语言。LINQ 也被用作 ADO.NET Entity Framework 的查询语言。

在 ASP.NET Web 应用程序中使用 EF，你有几种不同的选择。首先，你可以在页面的后台代码（Code Behind）中编写查询，并使用控件的 `DataSource` 属性和 `DataBind` 方法将结果绑定到数据控件。或者，你可以使用数据绑定控件的模型绑定（Model Binding）从 EF 获取数据。结合 `ListView` 和 `DataPager` 控件，这让你能够创建功能完全 CRUD 页面。

到目前为止，你看到的数据库驱动页面看起来相当单调。你还没有应用大量的样式，也没有提供任何条件格式（根据数据值以不同的方式呈现数据）。你可以通过控件样式以及数据绑定控件和数据源控件的许多事件来实现。下一章将向你展示如何利用这些样式和事件。

## 练习

- 1. 假设你在 `Reviews` 文件夹中有一个 `MostRecent.aspx` 页面。该页面应该显示最近添加的 10 条评论。如果你只想显示评论的 `Title` 属性和它所属的流派，你的 LINQ 查询应该是什么样？你应该使用 `Take` 方法将结果限制为 10 个。如果你在编写获取最后评论的代码遇到困难，请查看标题为“First, FirstOrDefault, Last, and LastOrDefault”的章节，它将了如何获取数据库中的最后一条评论。

- 2. `ListView` 控件相比 `GridView` 和 `Repeater` 等其他数据控件的主要优势是什么？

- 3. 目前，来自 `PhotoAlbums` 文件夹的 `Default.aspx` 页面仅显示图片的缩略图。你需要做什么才能使用 LINQ 查询在单独的页面上显示全尺寸图片？

- 4. 当你从 Photo Album 页面上的 `ListView` 删除图片时，只删除了数据库行，但磁盘上的图像保持不变。使用静态的 `System.IO.File.Delete` 方法在图片被删除时从磁盘删除该项。

- 5. 目前，`AllByGenre.aspx` 页面显示流派标题，无论是否有关联评论。如何隐藏没有评论的流派？利用 `Reviews` 集合上的 `Count` 方法来解决这个问题。

你可以在附录 A 中找到这些练习的答案。

## 本章学习内容

| Ado.Net 数据模型文件 | 包含将你的对象模型映射到数据库表所需信息的文件 |

| :--- | :--- |

| 匿名类型 | 动态创建而无需显式定义的类型 |

| Entity Framework | 一种创建强类型对象模型的技术，并有底层数据库，允许你与数据库中的数据进行交互 |

| Entity set | 实体模型中的对象集合；例如，一个 `PhotoAlbum` 实例有一个包含相册中图片的 `Pictures` set |

| 延迟加载 | 一种技术，在运行时访问数据之前，不会从数据库加载数据 |

| LINQ | 语言集成查询；.NET Framework 编程语言的一部分，提供对各种类型数据集合（包括对象、XML 和数据库）的查询支持 |

| 模型绑定 | ASP.NET 通过来自各种来源的数据为你填充对象的机制。从数据绑定控件中可以调用的各种方法大量使用了此过程 |

| 范围变量 | 在 LINQ 查询中定义的变量，随后在 `Select` 和 `where` 部分被使用 |

| 强类型 | 一种编程概念，在声明变量时显式定义变量的类型 |

| 类型推断 | 编译器根据变量的使用确定变量类型的技术 |

# 使用样式控制控件

使用 ASP.NET 样式和数据绑定控件的许多事件，可以轻松将图 15-1 中外观单调的 `GridView` 变为图 15-2 所示更酷的版本。

本章学习内容：

- 如何使用 CSS 为数据绑定控件设置样式

- 如何处理数据绑定控件触发的各种事件

- 如何使用条件格式显示数据

- 如何为控件实现自定义主题和皮肤

# 使用样式格式化控件 | 51
