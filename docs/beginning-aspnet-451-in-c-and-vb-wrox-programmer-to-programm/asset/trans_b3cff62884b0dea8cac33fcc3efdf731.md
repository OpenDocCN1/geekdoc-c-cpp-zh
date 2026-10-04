

# 使用样式格式化控件 | 51

是免费的。在下一节中，你将看到如何将这些样式应用于页面上的单个控件。接下来的章节将向你展示如何将样式移动到主题中，以便你所在区域的所有控件都能更容易地复用这些样式。你已经在第 7 章中看到了一些样式的应用，当时你使用它们来对 Menu 和 TreeView 控件进行样式设置。然而，由于样式广泛用于数据绑定控件，它们应该有一个专门的章节。

## 样式简介

许多数据绑定和导航控件具有许多样式属性，允许你修改控件的外观。例如，GridView 具有 `RowStyle` 和 `AlternatingRowStyle` 属性，允许你自定义网格中单行的颜色。以下是一个带有样式元素的 GridView 示例，它使用不同的背景颜色渲染奇偶行：

```
<asp:GridView Id="GridView" runat="server">
<AlternatingRowStyle BackColor="White" />
<RowStyle BackColor="#FFF3FB" />
</asp:GridView>
```

同样，DetailsView 拥有 `CommandBorderStyle`，用于控制包含插入（Insert）、删除（Delete）、取消（Cancel）等命令的命令行的的外观。

最终，每个样式属性都继承自 `System.UI.WebControls` 命名空间中的 `Style` 类。图 15-3 显示了该类最常见可见属性的过滤视图。

从名称可以看出，`Style` 类的属性用于更改应用到该类的对象上的样式相关信息。这些属性中的每一个最终都会转换为 CSS 属性或 HTML 属性，例如 `background-color`、`border` 等。其他样式（如 GridView 控件的样式）还添加了布局相关的属性，作为控制对齐的不同选项。下表列出了可用的各种 `Style` 派生类最重要的属性。请注意，并非每个属性适用于适用于样式。IntelliSense 会确切显示你可以在特定样式中使用哪些属性。

![](img/9e033e3b9560597824f8b22941d6d8bb_578_0.png)

| 属性 | 说明 |
|---|---|
| BackColor | 这些属性允许你更改元素的背景颜色和文本颜色。它们分别映射到 CSS 属性 `background-color` 和 `color`。 |
| ForeColor | |
| BorderColor | 这些属性允许你更改应用样式的边框。它们直接映射到对应的 CSS 属性 `border-color`、`border-style` 和 `border-width`。 |
| BorderStyle | |
| BorderWidth | | |

| 属性 | 说明 |
| --- | --- |
| CssClass | 这允许你分配 CSS 类而不是内联样式信息。你应该优先使用 `CssClass` 属性而不是单个样式属性，因为它们可以减少页面膨胀。你将在稍后的练习中看到如何使用 `CssClass`。 |
| Font | 这允许你通过各种子属性（如 `Font-Names`、`Font-Size` 和 `Font-Bold`）设置元素的字体。这些属性最终变为各种 CSS 字体属性，如 `font-family`、`font-size` 和 `font-weight`。 |
| HorizontalAlign | 这些最终变为应用到其 HTML 上的 `align` 和 `valign` 属性，并允许你控制元素内容的对齐。例如，你使用 `HorizontalAlign` 来左对齐或右对齐 `GridSearch` 列标题的文本。注意：这些属性输出的属性在 HTML5 中已过时。大多数浏览器仍会按预期渲染它们，但如果 HTML5 兼容性很重要，你不应该使用这些属性，而应该使用通过 `CssClass` 属性分配自定义 CSS 类。 |
| Wrap | 设置为 False 时，它将变为 `white-space: nowrap;` CSS 声明，决定一段文本是否允许换行。Height 允许你控制应用到其上的元素的高度和宽度，并直接映射到对应的 CSS `height` 和 `width` 属性。 |

查看 MSDN 文档（位于 http://bit.ly/Lb3Zd）以获取 `Style` 类的完整说明。

不同的数据绑定控件具有不同的样式集，尽管它们共享一些常用样式。下表列出了 `GridSearch` 可用的样式及其用途。其他数据绑定控件的样式略有不同，但通过它们你应该能够看出它们的作用并确定它们的用途。学习更多可用样式的另一种良好方法是使用 Visual Studio 的“自动格式”（Auto Format）功能，它会插入许多样式。你稍后将看到如何使用和改进由自动格式功能生成的样式。

| 样式 | 说明 |
| --- | --- |
| RowStyle | 这些控制单行的外观。默认情况下，`RowStyle` 影响所有行。设置 `AlternatingRowStyle` 时，它仅用于偶数行。 |
| SelectedRowStyle | 这可以应用于选中的行，让你有机会在视觉上将选中行与未选中行区分。 |

## EditRowStyle

这可以应用于当前处于编辑模式的行。例如，当你点击 Management 部分中 Genres 页面上 GridView 某行的编辑链接时，该行将切换到编辑模式并应用此 `EditRowStyle`。

## EmptyDataRowStyle

这允许你定义当网格绑定到空数据源时显示的行的外观。

## HeaderStyle

这些控制页头的外观。

## FooterStyle

这些控制页脚的外观。

## PagerStyle

这允许你定义分页器的外观。

## SortedAscendingCellStyle

## SortedAscendingHeaderStyle

## SortedDescendingCellStyle

## SortedDescendingHeaderStyle

这些样式共同允许你更改页头和页脚。

## 尝试应用样式

在本次尝试中，你将使用 VS 的内置功能来更改 GridView。

- 打开 Management 文件夹下的 Genres.aspx。
- 切换到设计视图并打开 GridView 的智能任务面板。
- 在面板顶部，点击“自动格式”链接。
- 从左侧的方案列表中选择 Classic。右侧的预览已更新，现在看起来像图 15-4。

![](img/9e033e3b9560597824f8b22941d6d8bb_581_0.png)

图 15-4

- 点击确定让 VS 生成必要的模板。设计视图中的 GridView立即更新，显示所选方案。
- 回到标记视图并检查生成的各种样式。你应该看到以下样式，某些在 `<Columns>` 元素之前，某些在之后：

```
<AlternatingRowStyle="#2461BF" />
```

```
<FooterStyle BackColor="#507DC1" Font-Bold="True" ForeColor="White" />
```

为了留白，此处未显示某些样式

```
<SortedDescendingHeaderStyle="#4870BE" />
```

