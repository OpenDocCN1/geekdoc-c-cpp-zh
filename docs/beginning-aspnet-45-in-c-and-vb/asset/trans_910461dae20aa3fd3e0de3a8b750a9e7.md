
![](img/eadab2ccd79b253c01a3fdff2321202d_590_0.png)

图 14-20

6. 在设计视图中选择新的 EntityDataSource 控件（名为 EntityDataSource2），打开其属性网格，并单击 Where 属性旁的省略号按钮以打开表达式编辑器。勾选对话框顶部自动生成的 Where 子句复选框。单击添加参数按钮并输入 PhotoAlbumId 作为参数名称。然后在参数源下拉属性中选择 Control，并在 ControlID 中选择 DropDownList1。最后，单击显示高级属性链接并将参数的类型更改为 Int32。您的表达式编辑器应如下图 14-21 所示。单击确定关闭对话框。

7. 在 ListView 控件的智能任务面板上，单击配置 ListView（如果看不到该选项，请先单击刷新架构并重新打开智能任务面板）。选择项目符号列表作为布局，并在选项区域中选择启用分页。其下的下拉列表应默认选择为上一页/下一页分页器，这对本练习来说是可以的。

8. 单击确定，VS 会为您创建几个模板。

9. 切换到标记视图并为 ListView 添加一个 ItemType 属性，其值设为 PlanetWroxModel.Picture。您的 ListView 应如下所示：

```
<asp:ListView ID="ListView1" runat="server" DataKeyNames="Id"
DataSourceID="EntityDataSource2" ItemType="PlanetWroxModel.Picture">
```

![](img/eadab2ccd79b253c01a3fdff2321202d_591_0.png)

## 图 14-21

10. 接下来，删除以下模板及其包含的代码：

- `<AlternatingItemTemplate>`
- `<EditItemTemplate>`
- `<InsertItemTemplate>`
- `<ItemSeparatorTemplate>`
- `<SelectedItemTemplate>`

11. 从 LayoutTemplate 中的 <ul> 中删除 ID、runat 和 style 属性，并添加一个 class 属性并将其设为 ItemContainer。找到 LayoutTemplate 中的 DataPager 并添加一个 PageSize 属性设为 3。最后，将 clear: both; 添加到空的 style 属性中：

```
<LayoutTemplate>
  <ul class="ItemContainer">
    <li id="ItemPlaceholder" runat="server" />
  </ul>
  <div style="clear: both;">
    <asp:DataPager ID="DataPager1" runat="server" PageSize="3">
      <Fields>
        <asp:NextPreviousPagerField ButtonType="Button" ShowFirstPageButton="True" ShowLastPageButton="True" />
      </Fields>
    </asp:DataPager>
  </div>
</LayoutTemplate>
```

```
</Fields>
</asp:DataPager>
</div>
</LayoutTemplate>
```

12. 修改 ItemTemplate 中的代码，使其如下所示：

```
<ItemTemplate>
<li>
<asp:Image ID="Image1" runat="server" ImageUrl='<%# Item.ImageUrl %>'
ToolTip='<%# Item.ToolTip %>' />
<asp:Label ID="DescriptionLabel" runat="server"
Text='<%# Item.Description %>' />
</li>
</ItemTemplate>
```

这会创建一个 Image 控件，其 ImageUrl 和 ToolTip 属性绑定到您正在绑定的 Picture 对象的相应属性。在浏览器中将鼠标悬停在图像上时会出现 ToolTip。在图像下方，一个简单的 Label 控件显示图像的描述。对于本练习，您不需要模板中最初定义的其他属性。

13. 接下来，将 cpMainContent 内容块中的整个代码用带有 ContentTemplate 元素的 UpdatePanel 包裹起来，以避免在分页图片列表或从列表中选择新的相册时出现页面闪烁。

```
<asp:Content ID="Content2" ContentPlaceHolderID="cpMainContent" runat="Server">
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
<asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="True"
DataSourceID="EntityDataSource1" DataTextField="Name" DataValueField="Id">
...
</ContentTemplate>
</asp:UpdatePanel>
</asp:Content>
```

14. 打开站点的 Web.sitemap 文件，并在 Reviews 和 About 部分之间为 Gig Pics 部分添加一个主菜单和两个子菜单项：

```
<siteMapNode
<siteMapNode url="~/PhotoAlbums/" title="Gig Pics" description="All Gig Pics">
<siteMapNode url="~/PhotoAlbums/Default.aspx" title="Gig Pics"
description="All Gig Pics" />
<siteMapNode url="~/NewPhotoAlbum.aspx" title="New Album"
description="Create a new Photo Album with Gig Pics" />
</siteMapNode>
<siteMapNode url="~/About/Default.aspx" title="About"
description="About this site">
```

15. 由于您添加了另一个菜单项，因此需要更改 Monochrome 主题中菜单中每个项目的宽度。为此，打开 Monochrome.css 并将 .MainMenu ul li 选择器的宽度从 200 改为 160 像素：

```
.MainMenu ul li
{
width: 160px;
}
```

16. 保存所有更改，然后在浏览器中请求 `PhotoAlbums` 文件夹中的 `Default.aspx`。从下拉列表中选择一个相册，页面重新加载，显示该相册中的相关图片。

> **COMMON MISTAKES** 如果从下拉列表中选择新项目时没有任何反应，请返回 VS 并确保将 `DropDownList` 控件上的 `autoPostBack` 设为 True。
>
> 如果相册中没有任何图片，或图片不足以填满一整页，请从 Gig Pics 菜单中选择 New Album，创建一个新的相册并至少添加四张图片。然后单击 Gig Pics 菜单项并从下拉列表中选择您的新相册。请注意，现在有一个分页用户界面，可让您使用屏幕底部图 14-22 中可见的 First、Previous、Next 和 Last 按钮在相册的图片列表中向前和向后移动。由于您添加的 AJAX 面板，选择和分页操作现在完全无闪烁。

> **NOTE** 您最初创建的前几个相册最终会损坏。这是因为您在创建它们时没有提供图片。如果您想清理一下，可以从数据库中删除相册（及其关联的图片行）。在第 16 章中，您将开发从 `PhotoAlbums` 文件夹中的 `Default.aspx` 页面删除图片的功能。

![](img/eadab2ccd79b253c01a3fdff2321202d_593_0.png)

图 14-22

## 工作原理

本练习中您所看到的大部分内容应该都很熟悉。您使用的方法与上一章中创建 Genres 下拉列表时使用的方法类似，将 DropDownList 连接到 EntityDataSource。ListView 及其关联的 EntityDataSource 也与本章前面讨论的内容类似。然而，与查看查询字符串的 Where 参数不同，代码现在使用查看 DropDownList 的 Where 参数：

```
<WhereParameters>
<asp:ControlParameter ControlID="DropDownList1" Name="PhotoAlbumId" PropertyName="SelectedValue" Type="Int32" />
</WhereParameters>
```

由于您在 EntityDataSource 控件上将 AutoGenerateWhereClause 设为 True，因此会根据这些参数即时创建一个 Where 子句。这与早期显式定义 Where 子句的示例形成对比。对于像前述练习这样简单的场景，依赖自动生成的 Where 子句效果很好。对于更详细的场景，了解您也可以显式分配一个 Where 子句是很有用的。

当 EntityDataSource 即将从数据库获取数据时，它会查看下拉列表的 SelectedValue 属性，然后仅检索与请求的 PhotoAlbumId 匹配的图片。

与之前示例相比最大的不同是添加了 DataPager。正如本练习所示，分页会自动为您处理。您需要做的就是在 ListView 的 LayoutTemplate 中的某个位置嵌入一个 DataPager 控件，其余部分会自动处理。如果您将 DataPager 放在 ListView 外部，请不要忘记通过设置 PagedControlID 属性将其连接到 ListView。如果您更喜欢链接或图像而不是按钮，可以将 NextPreviousPagerField 元素的 ButtonType 属性分别设为 Link 或 Image。如果您更喜欢数字分页器，请用 NumericPagerField 替换 NextPreviousPagerField 项：

```
<asp:NumericPagerField NextPageText="..." PreviousPageText="..." />
```

在本练习中，您将 PageSize 设为 3，以便更容易填满多个页面并查看分页器的运行情况。在实际应用中，PageSize 通常会高一些，例如 10 或 20。由于布局在 Monochrome 主题中使用三列布局，在 DarkGrey 主题中使用两列布局，您可能希望选择一个同时能被两者整除的值，例如 18。

## 关于性能的几点说明

前述练习有两个已知的性能问题，您应该注意。第一，虽然 ListView 的 ItemTemplate 通过 CSS 设置宽度将图像调整为浏览器中的 180 像素，但实际图像保持不变。这意味着如果您上传大图像，整个图像仍会被下载，只是显示为小缩略图。最好在服务器上创建一个真正的缩略图图像，然后将其发送到浏览器。我的书 ASP.NET 2.0 Instant Results（ISBN：978-0-471-74951-6）中题为“Greeting Cards”的章节提供了许多关于在服务器上调整图像大小的示例。
