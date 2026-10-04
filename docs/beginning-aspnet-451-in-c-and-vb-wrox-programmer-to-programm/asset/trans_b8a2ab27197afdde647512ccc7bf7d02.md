

# 使用样式格式化控件

```html
<tr style="background-color:#FF3FB;"> ... </tr>
<tr style="background-color:White;"> ... </tr>
```

关闭源文档并点击几次 Grid 的表头。表头会改变颜色，以显示当前排序的列。

# 工作原理

你在第 5 步中创建的不同样式元素被转换为它们相应的 CSS 和 HTML 等效项。例如，`RowStyle` 和 `AlternatingRowStyle` 的 `BackColor` 被设置了不同的背景颜色：

```
<RowStyle BackColor="#FF3FB" />
<AlternatingRowStyle BackColor="White" />
```

当控件渲染其 HTML 时，它会将这些背景应用于项目行和交替项目的的表格行：

```
<tr style="background-color:#FF3FB;"> ... </tr>
<tr style="background-color:White;"> ... </tr>
```

同样的原理也适用于 GridView 中的其他样式。
如果你查看页面源代码，你会发现大量的页面冗余，因为每一行都设置了其属性。这增加了页面大小，特别是当 GridView 中显示较多结果时。为了减少页面大小并提高页面性能，你可以将样式定义移动到页面主题中，然后改用 CSS 和 jQuery。你将看到如何这样做。

# 组合样式、主题和皮肤

第 6 章讨论了如何使用主页（master pages）、主题（themes）和皮肤（skins）创建外观一致的网页。在设置好基础架构后，现在添加一个适用于整个管理（Management）部分的新主题变得简单了。之前你已经了如何创建一个皮肤文件来更改按钮的外观；在下面的练习中，你将看到如何复用这个概念为 GridView 创建一个皮肤文件，从而能够一次性格式化 Management 文件夹中的所有 GridView 控件。

# 尝试创建高级样式解决方案

在本次尝试中，你把 Genres.aspx 页的样式属性移动到单独的皮肤文件中。你还将内联样式信息移动到 CSS 文件。然后使用 jQuery 进一步分离页的数据和外观。

- 1. 在解决方案管理器中，右键点击 `App_Themes` 文件夹，选择添加 > 新文件夹，并输入 `Management` 作为新名称。
- 2. 右键点击此新文件夹并选择添加 > 添加新项。添加一个名为 `GridView.skin` 的皮肤文件。你的解决方案管理器最终应该像图 15-5 一样。

![](img/9e033e3b9560597824f8b22941d6d8bb_582_0.png)

图 15-5

- 3. 在标记视图中打开 Genres.aspx ，删除上一个练习中创建的所有样式，除了 `HeaderStyle`、`PagerStyle`、`SortedAscendingHeaderStyle` 和 `SortedDescendingHeaderStyle`。从剩余的四个样式中删除所有属性，并将其替换为与样式同名且以 `GridView` 为前缀的单个 Css。你应该得到以下样式：

```
<HeaderStyle Css="GridViewHeaderStyle" />
<PagerStyle Css="GridViewPagerStyle" />
<SortedAscendingHeaderStyle Css="GridViewSortedAscendingHeaderStyle" />
<SortedDescendingHeaderStyle Css="GridViewSortedDescendingHeaderStyle" />
```

如果 VS 在 CSS 类名下添加了错误线，请担心。因为 CSS 类尚未定义，你稍后可以找到它们，并将它们添加到 CSS 文件中，此时 VS 仍然找不到它们。

- 4. 在代码编辑器中选择样式并删除所有现有内容（你之前看到的注释文本），然后使用 Ctrl+X 将其剪到剪贴板。打开 `GridView.skin` 文件，并将样式粘贴到皮肤文件中。

- 5. 将样式封装在 `<asp:GridView>` 元素中，并将其 `runat` 设置为 `server` 并作为 `CssClass`。不要添加 `ID` 属性，因为皮肤文件不需要这个。你应该得到这个：

```
<asp:GridView runat="server" CssClass="GridView">
    <% styles go here %>
</asp:GridView>
```

- 6. 在文件资源管理器（Windows 7 中的 Windows 资源管理器）中打开本章的资源文件夹（如果你遵循本书介绍部分的说明，位于 `C:\BegASPNET\Chapter15`），选择 `Images` 文件夹和 `Management.css` 文件，并按 Ctrl+C 复制。切换回 VS，点击 `App_Themes` 下的 `Management` 文件夹，并按 Ctrl+V。与之前的两个一样，管理主题现在有了它自己的样式和 `Images` 文件夹，如图 15-6 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_583_0.png)

图 15-6

- 7. 打开你之前在根目录下的 `Management` 文件夹的 `Web.config` 文件，并将主题设置为 `Management`：

```
<system.web>
    <pages theme="Management" />
</system.web>
```

- 8. 打开根目录下 `Management` 文件夹的 `Management.master` 文件，切换到标记视图，在 `<head>` 标签下方引入 `Scripts` 文件夹中的 `jquery-2.0.3.js`：

```
<head>
<script src="../Scripts/jquery-2.0.3.js"></script>
</head>
```

- 9. 回到 Genres.aspx，在标记视图中，在 GridView 的 `Columns` 元素下删除 Id 列。

# 使用样式格式化控件

将 `ItemStyle` 的宽度设置为 `100px`，并将 `SortOrder` 的宽度设置为 `200px`。你应该得到这个：

```
<asp:GridView runat="server" CssClass="GridView" AllowPaging="True" DataSource="SqlDataSource" GridLines="None" EmptyData="No records to display.">
<Columns>
  <CommandField EditButton="True" ShowSelectButton="False" />
  <BoundField FieldName="Name" HeaderText="Name" />
  <BoundField FieldName="SortOrder" HeaderText="Sort Order" />
</Columns>
</asp:GridView>
```

- 10. 在标记视图中滚动到页面末尾，在关闭 `</Content>` 标签之前添加你写的以下 `<script>`：

```javascript
<script>
$(function() {
  $('.GridView tr:not(.PagerStyle)').addClass('GridViewAlternatingStyle');
});
</script>
```

- 11. 按 Ctrl+Shift+S 保存所有更改并在浏览器中打开 .aspx。点击 Name 或 Sort Order 列头进行排序。注意 GridView 如何显示排序方向。

- 12. 在主菜单中管理评论以打开评论视图。从下拉列表中选择一个类型以显示评论列表。注意图 15-7 中的评论现在应用了你刚刚选择的类型样式，除了交替行样式以及 GridView 的设置（如 GridLines 和 CellPadding）。

| Index Rock | Authorized | Created |
|---|---|---|
| Sort: Youth Democrat live in Roundhouse, London | Yes | 11/04/2007 5:19 PM |
| Sort: Youth Democrat live at Locations, Billings | Yes | 11/04/2007 5:27 PM |
| Age & The Killers - Excellent album, but is it better before? | Yes | 11/04/2008 10:01 PM |
| Us | | |
| The Pain of Being Pure at Heart - One of the new bands | Yes | 2/3/2009 2:45 PM |
| P.J. Harvey & John Paris - A Woman Man Walking | No | 4/1/2009 1:08 PM |
| Battle for the Sun by Placebo - Possibly best of 2009 already | Yes | 6/9/2009 9:01 PM |
| Sort: The Elemental Takes to get used but then... | Yes | 6/10/2009 9:33 PM |
| Farm Dionysac - Winter - Summer | Yes | 6/23/2009 10:36 PM |
| Insert New | Yes | 6/24/2012 9:25 PM |

