
```
<div onclick="controls">
  <source src="file.mp4" type="video/mp4">
  <source src="file.webm" type="video/webm">
</div>
```
- T1 声音带有... `Ctrl+K`, `S`
- 剪切 `Ctrl+X`
- 复制 `Ctrl+C`
- 粘贴 `Ctrl+V`
- 删除 `Del`
- 在浏览器中查看 (Internet Explorer)
- 在页面检查器中查看 `Ctrl+Shift+I`
- 运行到光标 `Ctrl+F10`
- 单步运行到光标 `Ctrl+F11`
- 展开控件
- 折叠标签

# C#.NET 基础

图 1.16：选择提取为用户控件选项

另存为对话框出现（图 1.17）。在文件名框中输入文件名；在我们的中输入了 `VideoControl.ascx`，如图 1.17 所示。

![](img/17af790174c480761404624aeed9b30b_68_0.png)

图 1.17：显示另存为对话框

点击确定按钮以创建用户控件。新创建的用户控件标签替换了选中的文本，如图 1.18 所示：

```html
<div>
  <u:VideoControl runat="server" Id="VideoControl" />
</div>
```

图 1.18：显示用户控件标签

- 属性中代码片段的 IntelliSense - 为 HTML 属性中的代码片段提供智能提示；这让程序员的生活变得轻松了一些，因为他们不需要记住复杂标签和属性的名称；只需输入几个字母即可获取与输入字母开头的所需项目列表。之前的 Visual Studio 版本仅对服务器端代码片段提供 IntelliSense，而不提供 HTML 属性。然而，在 Visual Studio 2012 中，对服务器端代码片段和 HTML 属性都提供了 IntelliSense。图 1.19 显示了 `<input>` 元素的 `value` 属性的 IntelliSense：

# 第 1 章

```xml
<asp:Repeater runat="server">
  <ItemTemplate>
    <Input value="##validationStatus.Text" />
  </ItemTemplate>
</asp:Repeater>
```

图 1.19：显示 HTML 属性的 IntelliSense

- 标签自动重命名 - 指一种在源视图中帮助你的功能，当你尝试更改任何标签名称时，它会自动重命名标签。例如，你将 HTML `<div>` 标签重命名为 `<header>` 标签，相应的标签也会同时自动更改。此功能非常有用，因为如果你忘记重命名匹配或起始标签，它可以减少文档中的工作量。图 1.20 显示了 `<div>` 标签重命名为 `<header>`：

```html
<header>
  <!-- 代码 --
</header>
```

图 1.20：显示标签的实时重命名

- 事件处理器 - 当你生成事件处理程序时，必须选择`<创建新事件>`选项。按下它时会生成事件处理程序，然后在事件名称后给出等号 `=`，显示的事件处理器的 IntelliSense 包含 `<创建新事件>` 选项，如图 1.21 所示：

```xml
<asp:Button runat="server" ID="btnSave" OnClick="
  <Create New Event />
```

图 1.21：显示事件处理器的 IntelliSense

要生成事件处理程序，必须选择`<创建新事件>`选项。事件处理程序将在 Web 页面上带有正确的签名生成。此外，事件处理程序的方法是通过使用控件 ID 的名称派生的，如图 1.22 所示：

```xml
<asp:Button runat="server" ID="btnSave" OnClick="btnSave_Click" />
```

图 1.22：显示按钮标签

如图 1.22 所示，ID 是 `btnSave`，事件是 `Click`。因此，通过在 `btnSave` 单词后附加 `Click` 单词，在 C# 的 `.cs` 文件和 Visual Basic 的 `.vb` 文件生成了相应的事件处理器方法 `btnSave_Click`。图 1.23 显示了 C# 中的事件处理器方法：

```csharp
protected void btnSave_Click(object sender, EventArgs e)
{
}
```

图 1.23：显示 C# 中的事件处理器方法

- 智能缩进 - 在空 HTML 元素内按回车键后，插入点将位于正确的位置。假设插入点在 `<header>` 元素内部，如图 1.24 所示：

```html
<header>k</header>
```

图 1.24：显示 `<header>` 元素内部的插入点

当你按下回车键时，插入点缩进到它的正确位置，如图 1.25 所示：

```html
<header>
  | 
</header>
```

图 1.25：显示插入点的智能缩进

# C#.NET 基础

智能缩进将使文档更具可读性且美观。

自动减少语句完成 – 在 IntelliSense 中仅显示与字母匹配的相关的选项列表，与标题匹配的单个单词也会显示在 IntelliSense 中。自动减少语句完成功能的优势是它让已知元素的语句完成更快。

## JavaScript 编辑器

智能缩进将使文档更具可读性且美观。

自动减少语句完成 – 在 IntelliSense 中仅显示与字母匹配的相关的选项列表，与标题匹配的单个单词也会显示在 IntelliSense 中。自动减少语句完成功能的优势是它让已知元素的语句完成更快。

## CSS 编辑器

智能缩进将使文档更具可读性且美观。

自动减少语句完成 – 在 IntelliSense 中仅显示与字母匹配的相关的选项列表，与标题匹配的单个单词也会显示在 IntelliSense 中。自动减少语句完成功能的优势是它让已知元素的语句完成更快。

## JavaScript

智能缩进将使文档更具可读性且美观。

自动减少语句完成 – 在 IntelliSense 中仅显示与字母匹配的相关的选项列表，与标题匹配的单个单词也会显示在 IntelliSense 中。自动减少语句完成功能的优势是它让已知元素的语句完成更快。

## C.NET 基础

```css
#menu {
  list-style-type: upper-margin;
}
*:first-child + html #menu li {
  margin: 0;
  float: right;
}
```

图 1.31：显示选择器技巧（Selector Hack）

厂商特定架构——支持在 IntelliSense 中使用特定浏览器的 CSS 属性。不同的浏览器由不同的厂商创建，并有自己的厂商特定语法。由于这种情况，开发者必须根据厂商的特定语法为浏览器编写代码。CSS3 通过提供特定浏览器的 CSS 属性解决了这一问题，例如 Mozilla (`-moz`)、Microsoft Internet Explorer (`-ms`)、Opera (`-o`) 和 Webkit (`-webkit`)。在 IntelliSense 中通过输入连字符（`-`）后跟特定浏览器的首字母，即可显示这些浏览器特定属性，如图 1.32 所示：

```css
body {
  -ms-wrap-margin
  -ms-wrap-through
  -ms-indenting-width
  -ms-column-width
  -webkit-animation
  -webkit-animation-delay
  -webkit-animation-duration
  -webkit-animation-fill-mode
}
```

图 1.32：显示浏览器特定属性的 IntelliSense

注释和取消注释支持——支持对 CSS 规则进行注释和取消注释。要进行注释，选择文本并按下快捷键（`Ctrl+K`, `C`）；若要取消选中文本的注释，按下快捷键（`Ctrl+K`, `U`）。相同的快捷键也可用于 Code 编辑器中文本的注释和取消注释。图 1.34 显示了在 css 文件中使用快捷键对选中文本进行的注释：

```css
body {
  /*color:#ff00ff;
  background-color:#f00;
}
```

图 1.33：显示注释

颜色选择器——当在 CSS 属性中输入值时，会提供颜色选择器。Visual Studio 之前的版本提供了颜色值的 IntelliSense，但是以下拉列表的形式呈现的。Visual Studio 2012 以颜色选择器的形式提供了颜色的 IntelliSense，该选择器会自动显示，并列出可以使用键盘或鼠标选择的颜色列表。对于键盘选择，按向下箭头键访问颜色选择器，按向右或向左箭头键在选择器中导航，按 Enter 键选择颜色值。图 1.34 显示了收起状态的颜色选择器：

```css
body {
  background-color:;
}
```

1.34 显示了默认的颜色选择器。如果你已经使用了一些颜色，颜色选择器还会显示之前使用过的颜色，并用竖线分隔，然后是默认调色板。颜色选择器最右侧还有一个小的双向下箭头按钮，点击它可以以展开形式显示颜色选择器，如图 1.35 所示：

# 第 1 章

![](img/17af790174c480761404624aeed9b30b_73_0.png)

图 1.35：显示展开形式的颜色选择器

你也可以通过在键盘上按两次向下箭头来显示颜色选择器的展开形式。此展开形式包含一个不透明滑块、左下角用于选择颜色的颜色选择器按钮、一个包含颜色的条以及颜色查看器。可以移动不透明滑块来控制 Alpha 通道，从而将所选颜色转换为 RGBA 格式，如图 1.36 所示。

![](img/17af790174c480761404624aeed9b30b_73_1.png)

图 1.36：使用不透明滑块显示颜色选择器

- 代码段（Snippets）——支持以代码段形式使用特定浏览器的 CSS 属性。代码段帮助开发者快速创建跨浏览器样式。Visual Studio 2012 以代码段形式提供了颜色的 IntelliSense。你可以输入 `@` 符号来生成代码段，如图 1.37 所示：

![](img/17af790174c480761404624aeed9b30b_73_2.png)

图 1.37：使用 `@` 符号

你可以在 IntelliSense 中选择任意元素，然后按 Tab 键生成相应的代码段，如图 1.38 所示：

C.NET 基础

```css
@keyframes name {
  from {
    background: red;
  }
to {
    background: yellow;
  }
}
```

图 1.38：插入代码段

自定义区域（Custom regions）——帮助分组可以展开或折叠的代码。自定义区域功能在 Code 编辑器中已经存在。现在，Visual Studio 2012 在 CSS 编辑器中也引入了自定义区域功能。当区域折叠时，它会显示名称并用省略号表示有更多内容，如图 1.39 所示：

图 1.39：在编辑器中显示自定义区域

页面查看器（Page Viewer）

Visual Studio 2012 的页面查看器可以在 Visual Studio IDE 中渲染网页，并允许你查看源码和结果。此外，页面查看器是一个强大的调试工具。图 1.40 显示了页面查看器：

![](img/17af790174c480761404624aeed9b30b_74_0.png)

图 1.40：显示页面查看器

第 1 章

![](img/17af790174c480761404624aeed9b30b_75_0.png)

图 1.41：带有标准工具栏的页面查看器

![](img/17af790174c480761404624aeed9b30b_75_1.png)

图 1.42：显示页面查看器

# 第1章

- 允许你离线工作

- 允许你对从文本模板生成的代码进行调试

## 自动化与调试构建

Visual Studio 2012 在自动化和调试构建方面的增强如下：

- 允许你使用改进后的接口执行、跟踪和管理构建

- 允许使用 Team Foundation Service 执行自动化构建

- 允许你定义支持多次提交的门禁检查（gated check-in）过程

- 允许在构建过程中执行原生和第三方框架的单元测试

- 允许你更轻松地调试构建过程

## Microsoft Test Manager

Visual Studio 2012 中的 Microsoft Test Manager 功能允许你完成以下任务：

- 允许你进行手动测试以识别 Windows Store 应用中的错误

- 允许你对测试集或预定步骤进行探索性测试

- 允许你在 Microsoft Test Manager 中以报告形式检索测试状态

- 允许通过克隆测试并行处理更多测试

## Visual Studio 2012 的一些杂功能

以下是 Visual Studio 2012 引入的一些杂功能和增强：

- LightSwitch – 此功能允许你完成以下任务：

- 将 LightSwitch 应用连接到任何开放数据协议（ODATA）数据源

- 将应用数据暴露为 OData 数据源

- 为安全组分配角色和权限

- 限制服务器返回的数据

- 使用新控件改进屏幕外观

- 自定义数字和日期的格式

- 将 URL 和排列组合视为数据类型

- 数据应用开发 – 此功能允许你完成以下任务：

- 在 SQL Server 对象管理器中处理数据库对象 

- 在新的表设计器中定义表

- 在 SQL Server Express LocalDB 中开发和测试数据库应用

- 图形工具 – 此功能允许你完成以下任务：

- 更轻松地添加、编辑和组合高级着色语言（HLSL）着色器

- 高效地查看和修改图像资产

- 处理三维模型

- 创建高级像素着色器

- 并行计算 – 此功能允许你完成以下任务：

- 使用 C++ 加速大规模并行 (AMP) 让你的代码运行更快

- 调试用于检查并行性能的并行应用

- 有效地自定义你使用的数据

- 使用任务并行库 (TPL) 数据流使你的并发型应用更健壮

- SharePoint 开发 – 此功能允许你完成以下任务：

# C#.NET 基础

- 为 SharePoint 站点创建站点列

- 为你的 SharePoint 项目添加 Silverlight Web 部

- 将 SharePoint 解决方案发布到远程 SharePoint 站点

- 使用分析工具提高 SharePoint 性能

- 创建沙箱视觉 Web 部

- 更轻松地调试 JavaScript

- 使用精简的项目模板轻松地开发 SharePoint 项目

- 使用 Microsoft Fakes 框架测试你的代码

- **Office 文档** – 此功能允许你完成以下任务：

- 为 Office 创建应用。你可以使用 Web 技术和代码创建 Office 文档、会议请求、预约和电子邮件

- 为 Office 2013 开发解决方案

- 通过下载并安装适用于 Visual Studio 2012 的 Microsoft Office 开发工具，使用 .NET Framework 4.5 开发解决方案

- **NET Framework 4.5** – 此功能允许你完成以下任务：

- 构建可在多个 .NET Framework 平台上运行托管程序集

- 在安装 .NET Framework 时减少系统重启

- 使用异步操作提高输入/输出性能

- 提高多核处理器上的启动性能

- 更轻松地开发和维护 Windows 配置基础 (WCF) 应用

- 提高 WCF 应用的可扩展性

- 更轻松地管理工作流

- 创建状态工作流

- 为你的 Windows Presentation Foundation (WPF) 应用添加丝带

- 在 WPF 应用中更快地显示大组分组数据

- 使用新的编程接口更高效地创建现代超文本传输 (HTTP) 应用

在解释完 Visual Studio 2012 IDE 的新功能后，让我们讨论市场上提供的各种版本的 Visual Studio 2012。

## Visual Studio 2012 版本

Visual Studio 2012 以不同的版本引入市场。每个版本针对不同的用户都有其自己的一套功能。以下讨论了 Visual Studio 2012 的各种版本：

- **Visual Studio 2012 Ultimate** – 提供了一个集成的工具和服务器环境，简化了整个应用过程。此版本的 Visual Studio 2012 通过高效、可预测、可定制的过程产生结果。它增加了整个 Web 生命周期中的透明度和可追溯性。它让你能够针对各种平台和技术进行开发，包括云计算和 Windows Phone。

- **Visual Studio 2012 Premium** – 提供了一个简化应用开发的版本。它包含高级工具来解决最困难的问题。在此版本中，有高级代码分析工具可以帮助你避免在应用的编码阶段产生任何错误。此外，此版本提供的高级测试和调试工具可以快速发现并删除任何运行时错误。此版本可以有效地管理应用的测试环境。此外，你能够跟踪业务和开发团队中的每个任务和角色。

- Visual Studio 2012 Professional— 简化了创建、调试和部署应用的基本任务。它通过强大的设计表面增强创造力，并针对许多平台，如 Silverlight、SharePoint 和云应用。它还提供了以设计为中心的工具，如 CSS3 和 HTML5。

- Visual Studio 2012 Test Professional— 通过在开发过程中集成测试人员、产品经理和利益相关者，简化复杂应用的开发。它管理并执行测试用例，定义需求，检索客户反馈，并跟踪直到最终部署。

- Visual Studio Team Foundation— 为团队之间提供良好的通信和应用生命周期工具，确保应用构建快速准确。现在，让我们学习如何安装 Visual Studio 2012。
