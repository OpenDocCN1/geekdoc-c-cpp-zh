

点击确定关闭对话框并将更改应用到标题。你最终得到以下带有内联样式的 <h1> 元素在 Markup View 中：

```
<h1 style="padding: 0; margin: 0 0 10px 0">
</h1>
```

Hi visitor and welcome to Flanet Wrox

+   5. 接下来，在 Design View 中，通过点击选择第一个段落。会出现一个小图标以指示你已选择一个 <p> 元素。文档窗口底部的 Tag Selector 高亮显示 <p> 元素，如图 3-18 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_128_0.png)

+   6. 在段落被选中的情况下，从主菜单中选择 Format New Style。这次，不要创建内联样式，在 Selector 框中输入 .Introduction。不要忘记选择器菜单中的点号（.）。

+   7. 在屏幕顶部，选中 Apply New Style to Document Selection 复选框。有了此设置，你即将创建的新类将被应用到你已选择的 <p> 元素上。

+   8. 从样式下拉列表中选择 italic。

+   9. 点击确定关闭对话框。注意整个段落现在都以斜体字体显示。

+   10. 在 <p> 元素被选中的情况下，通过选择 ▼ CSS Properties 打开 CSS Properties Grid（图 3-19）。这可以让你概览 CSS 属性以及当前页面中哪些属性处于活动状态。

此网格在窗口顶部按出现顺序显示已应用规则的列表。窗口底部部分用于显示这些规则的 CSS 属性。在图 3-19 中，你可以看到适用于 .Introduction 选择器的规则。

+   11. 在 CSS Properties Grid 中找到 color 并将其设置为深蓝色，如 #003399。要实现这一点，打开属性值的下拉列表并从颜色选择器中选择一种颜色。你要找的颜色不可用，点击 More Colors 以调出扩展的颜色选择器，如图 3-20 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_128_1.png)

![](img/9e033e3b9560597824f8b22941d6d8bb_128_2.png)

*

除了使用颜色选择器，你也可以直接在 Properties Grid 中取值。这就是 CSS Properties Grid 中许多属性的工作方式：它们允许你直接输入值，或通过使用属性值框末尾的下拉列表或带省略号的框来更改值。图 3-21 显示了 font-style 属性在方便的下拉列表中的不同选项。

![](img/9e033e3b9560597824f8b22941d6d8bb_129_0.png)

请特别注意窗口顶部的三个按钮，因为它们使用了某些功能。前两个按钮可让你在分类模式和字母顺序模式之间切换，从而更轻松地找到正确的属性。第三个按钮可让你在列表顶部显示已应用的属性，或在列表中的默认位置显示它们。

+   12. 保存所有更改并在浏览器中打开 Default.aspx（你会看到第一个段落以蓝色和斜体字体显示，文本中的链接为红色或绿色，具体取决于你是否之前访问过该链接。此外，如果你遵循了上一章的所有说明，文本“paying a visit”将为红色，由嵌入的 CSS 类设置。

![](img/9e033e3b9560597824f8b22941d6d8bb_129_1.png)

FIGURE 3-22

+   13. 切回 VS 并在 Markup View 中查看你的页面。在页面的 <head> 部分，你应该看到以下嵌入式样式表：

## How It Works

VS 提供的众多工具使为你的网站编写 CSS 变得容易。你不需要手工编码任何内容，也不需要记住 CSS 标准支持的所有不同属性。相反，你可以

## Working with CSS in Visual Studio

只需从 CSS Properties Grid 的不同列表中选择它们。此网格允许你手动输入值，但提供了方便的工具来选择颜色、从下拉列表中选择项目等。

你在 Properties Grid 中所做的所有更改都会应用于相关的样式表，无论你使用的是内联、嵌入式还是外部样式表。与此同时，Design View 会更新以反映你所设置的新 CSS 选项。

当你查看 <h1> 元素时，你可以看到 VS 创建了一个内联样式，将 padding 设置为 0 以同时影响四个边，将 margin 设置为 0 0 10px 以单独控制四个边。

一旦你创建了一堆有用且可重用的样式，你需要一种方法将现有样式应用到其他页面或 HTML 元素。你接下来会看到这是如何工作的。

## Applying Styles

如果你有 Microsoft Word 的使用经验，你可能熟悉 Styles 对话框，它列出所有可用的样式并允许你为文本的某些部分选择它们。你可以快速将相同的格式应用到文本块。在 VS 中也是如此。通过 Apply Styles 窗口——可通过从主菜单中选择 Apply Styles 访问——你可以轻松地将样式规则应用到页面中的元素。

> TRY IT OUT Using the Apply Styles

在此练习中，你将使用 .Introduction 类并将其应用到页面的第二个段落。这样，两个段落看起来都一样。

+   1. 在 Default.aspx 中，确保你在 Design View 中并通过点击选择页面的第二个段落。确保文档窗口底部的 Tag Selector 显示 <p> 元素已被选中，而不是 <p> 内的其他元素，如 <strong>。如果你的文本只有一段，请创建一个新段落（在 Design View 中在第一个段落后按 Enter），输入一些文本，然后选择该段落。

+   通过选择 Apply Styles 打开 Apply Styles。确保窗口未停靠在 Document Window 中，而是浮动或放置在 Document Window 侧边。此窗口显示当前页面和任何附加样式表中的所有选择器。如果看不到图 3-23 中显示的所有样式，请点击 Options 按钮并选择 Choose All Styles。

+   3. 在 CSS Styles 列表中点击 Introduction 类。VS 会向 <p> 标签添加一个 class 属性：

```
<p class="Introduction">
Feel free to add a <a href="Default.aspx">around</a>; there are lots of interesting <strong>reviews and concert pictures</strong> to be found here.
</p>
```

![](img/9e033e3b9560597824f8b22941d6d8bb_130_0.png)

FIGURE 3-23

## CHAPTER 3 DESIGNING YOUR WEB PAGES

如果你想应用多个类，请按住 Ctrl 键同时点击列表中的其他类。这会将由空格分隔的类列表应用到元素的 class 属性。你也可以按照相同的步骤在 Markup View 中应用所选样式。

4. 使用 Clear 按钮，你可以快速从标签中移除现有的类和内联样式。考虑你在上一章使用 Foreground Color 按钮时看到的 HTML 片段，你最终得到了工具栏来格式化页面中的文本。

```
We&#39;re glad you&#39;re <span class="auto-style*">paying a visit;</span>
```

要移除 class 属性，请在 Tag Selector 中选择 <span> 标签，或直接在 Markup View 中点击 <span> 标签，然后点击 Apply Styles 窗口中的 Clear，该窗口可在图 3-23 中的工具栏下方看到。你将得到以下结果：

```
We&#39;re glad you&#39;re <span>-around paying a visit
```

由于空标签没有用处，VS 也会为你移除它。此外，VS 还会移除 auto-style 规则，因为它不再被页面上的任何代码使用。如果你在 Markup View 中点击 <span> 时 Apply Styles 窗口为空，你可能需要先切换到 Design View 以填充对话框。

从 HTML 元素中移除样式的方式相同。

## How It Works

再次，VS 能够保持所有相关窗口同步：Design View、Markup View 和你的 CSS 设计工具。当你从 Apply Styles 窗口应用一个类时，VS 会在 Markup View 中将请求的类添加到所选的 HTML 元素中。它还会更新 Design View。同样，当你在 Design View 中从嵌入样式中移除选择器或声明时，Design View 和 CSS 工具都会更新。

本章中你需要查看的最后一个 CSS 功能位于 Manage Styles 和 Apply Styles 窗口上。除了帮助你将 CSS 文件附加到文档外，这些窗口还使你能够轻松管理样式。

## Managing Styles

由于添加新的内联和嵌入样式很容易，你的页面可能会很快变得混乱，样式散布各处。为了实现可重用性，你应该将尽可能多的内联和嵌入样式移至外部样式表。这正是 Apply Styles 和 Manage Styles 窗口所能实现的功能。

> TRY OUT Managing the Manage Styles and Apply Styles Windows

本章前面，你修改了 <h1> 元素并将 padding 和 margin 应用到标题上。然而，default.aspx 并不是唯一可以从此标题样式中受益的页面，因此将其移至 Styles.css 文件是有意义的。Introduction 类似乎足够可重用，可以包含在 Styles.css 文件中，以便其他页面可以访问它。此 Try It 向你展示了如何移动站点中的样式。

