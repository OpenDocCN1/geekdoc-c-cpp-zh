
在您的页面中使用它们。Visual Studio 还为 ASP.NET AJAX 提供了强大的支持，使您不仅可以为服务器端控件获得 IntelliSense，还可以为您编写的、用来与客户端页面及服务器上运行的代码进行交互的客户端 JavaScript 获得 IntelliSense。

## 创建无闪烁页面

为了避免 ASPX 页面中的完整回发，只更新页面的部分内容，可以使用 UpdatePanel 服务器控件。要使该控件正常运行，还需要一个 ScriptManager 控件。如果你要在许多 ASPX 页面中使用 Ajax 功能，可以将 ScriptManager 放在母版页中，这样它就可以用于所有基于该母版页的页面。每个页面只能有一个 ScriptManager，所以如果你在母版页中添加了一个，就不能在内容页中再添加另一个。要从内容页访问母版页中定义的 ScriptManager 控件，可以使用 ScriptManagerProxy 控件，稍后会介绍。你可以在工具箱的“AJAX 扩展”类别中找到这些控件以及其他与 Ajax 相关的服务器控件，如图 10-2 所示。

![](img/eadab2ccd79b253c01a3fdff2321202d_397_0.png)

接下来的两节将向你介绍 UpdatePanel 和 ScriptManager 控件。介绍完之后，你将看到如何在 Planet Wrox 网站的页面中使用这些控件。后面的章节将向你介绍 UpdateProgress、Timer 和 ScriptManagerProxy 控件。

### UpdatePanel 控件

UpdatePanel 控件是创建无闪烁页面的关键组件。在其最基本的应用中，只需将需要更新的内容用该控件包起来，然后向页面添加一个 ScriptManager，就完成了。只要 UpdatePanel 内的某个控件导致向服务器回发，就只会刷新该 UpdatePanel 中的内容。

### 试一试：向页面添加 UpdatePanel

在本练习中，你要向页面添加一个 Label 和一个 Button 控件。当你在浏览器中单击按钮时，Label 的 Text 属性会更新为服务器上的当前日期和时间。为了避免通常伴随回发出现的页面闪烁，接下来你将控件包装在 UpdatePanel 中，以了解该控件如何影响此行为。

- 1. 在 Visual Studio 中打开 Planet Wrox 网站。
- 2. 在 Demo 文件夹中，使用你的自定义模板创建一个名为 UpdatePanel.aspx 的新 Web 窗体。给页面指定标题 UpdatePanel Demo。
- 3. 将新页面切换到设计视图，然后从工具箱中将一个 Label 控件和一个 Button 控件拖到 cpMainContent 占位符中。如果 ContentPlaceHolder 突然变得和 Label 一样小，只需将 Button 拖放到 Label 上。此时 Button 会放在 Label 之前，但如果你再将 Label 拖到 Button 上，两个控件就会交换位置。

通过单击按钮添加的内容并不属于 HTML 源码，因为它们是由 ASP.NET AJAX 框架动态添加到浏览器内部 HTML 中的。

### 工作原理

通过将内容包装在 UpdatePanel 中，你就在页面中定义了一个要刷新的区域，而不会影响整个页面。在示例中，UpdatePanel 内的 Button 控件引起了一次回发，因此只刷新了定义该控件的区域。页面不会整体替换，只有包装在 UpdatePanel 中的部分会被刷新，从而实现了无闪烁的页面重载。

如果你分析从服务器发送到浏览器的数据（使用类似 Fiddler 的网络分析工具，可从 www.fiddler2.com/fiddler2/ 下载），你会看到只有有限的数据被发送到客户端。发送的并不是整个页面（约 12KB），而只有以下数据：

```
1|#|4|232|updatePanel|cpMainContent_ctl00
<span id="cpMainContent_Label1">4/9/2012 11:56:09 AM</span>
<input type="submit" name="ctl00$cpMainContent$Button1" value="Button" id="cpMainContent_Button1" class="MyButton" style="background-color:#7A70A4;" />
|0|hiddenField__|__EVENTTARGET||0|hiddenField__|__EVENTARGUMENT||0|hiddenField__|__LASTFOCUS||1624|hiddenField|__VIEWSTATE|1|Ac... 
...
Demo|184|scriptBlock|ScriptResource.axd?d=... 
...
```

请注意，我删除了中间的一大块内容，包括页面的大部分视图状态（用三个点表示），以节省本书的篇幅。如果你查看这个响应，你会认出更新后的 Label 和 Button 的 HTML；这两个控件定义在 UpdatePanel 控件的 <ContentTemplate> 中。其余文本由 ASP.NET AJAX 框架用于维护页面状态（使用 __VIEWSTATE 字段），并用于确定将响应放置在页面中的什么位置。尽管仍然有大量数据通过网络传输，但远比原始完整页面（约 12KB）少。这带来了更快的响应速度和更好的用户体验。

当你在步骤 10 中查看浏览器中页面的源代码时，你可能已经注意到，页面仍然包含原始源代码，而不是由 ASP.NET AJAX 框架修改后的源代码。这有时会使构建、测试和调试 Ajax 应用程序变得困难，因为你无法真正看到发送到浏览器的数据。幸运的是，有许多工具可以帮助解决这个问题。除了前面提到的 Fiddler 工具，建议你了解一下 Microsoft Internet Explorer 开发人员工具栏。它随 Internet Explorer 8 及更高版本一起提供，可以通过“工具 ▸ 开发人员工具”菜单选项访问。

另一个出色的调试工具是 Firebug，它与 Firefox 浏览器集成得很好。你可以在 http://getfirebug.com 获取该工具。Google Chrome 也有类似的工具，你可以单击扳手图标，然后选择“工具 ▸ 开发人员工具”来打开它。

在本练习中，你使用了两个重要的 AJAX 扩展控件。`ScriptManager`——你在此练习中直接放在 `UpdatePanel.aspx` 中——是大多数 Ajax 功能在 ASPX 页面中正常运行的必要条件。它充当客户端页面与 Microsoft ASP.NET AJAX 框架之间的桥梁，并负责处理诸如注册浏览器中使用的正确 JavaScript 文件等事宜。然后使用 `UpdatePanel` 来定义你希望更新但无需重新加载整个页面的区域。在接下来的几节中，你将更详细地了解这两个控件。

### 深入了解 UpdatePanel

`UpdatePanel` 及其内容是当你单击按钮时页面中唯一更新的部分（如上一练习所讨论）。这是 `UpdatePanel` 的默认行为，其中只有内部内容会被 `<ContentTemplate>` 元素中定义的其他服务器控件刷新。然而，正如你在下一节中所看到的，`UpdatePanel` 的功能远不止于此。

### UpdatePanel 常用属性

| 属性 | 描述 |
|---|---|
| ChildrenAsTriggers | 此属性决定 UpdatePanel 内的控件是否可以引起 UpdatePanel 的刷新。默认值为 True，正如你在上一练习中看到的那样。当你将此值设置为 False 时，必须将 UpdateMode 设置为 Conditional。请注意，当此属性设置为 False 时，UpdatePanel 内定义的控件仍然会导致向服务器回发；只是它们不再自动更新面板。 |
| Triggers | Triggers 集合包含 PostBackTrigger 和 AsyncPostBackTrigger 元素。前者在你想要强制完全刷新页面时很有用，而后者在你想要使用面板外部定义的控件更新 UpdatePanel 时很有用。 |
| RenderMode | 你可以将此属性设置为 Block（默认值）或 Inline，以指示 UpdatePanel 是作为 <div> 还是 <span> 元素呈现。 |
| UpdateMode | 此属性决定控件是始终刷新（UpdateMode 设置为 Always），还是仅在特定条件下刷新，例如，当 <Triggers> 元素中定义的某个控件引起回发时（UpdateMode 设置为 Conditional）。此设置的默认值为 Always。 |
| ContentTemplate | 虽然在 UpdatePanel 的属性网格中看不到 <ContentTemplate>，但它是 UpdatePanel 的一个重要属性。它是你将控件作为 UpdatePanel 的子级放置的容器。如果你忘记了这个必需的 ContentTemplate，VS 会给你一个警告。 |
