

## 使用 Web 表单

Web 表单由 .aspx 文件表示，是 ASP.NET Web Forms 网站的核心。它们是用户访问你的网站时在浏览器中看到的实际页面。

如上一章所学，Web 表单可以包含 HTML、ASP.NET 服务器控件、客户端 JavaScript、CSS 和编程逻辑的混合。为了更轻松地查看所有代码最终在浏览器中的样子，VS 为你的页面提供了多种不同的视图。

## Web 表单的不同视图

VS 使你能够从不同角度查看 Web 表单。当你在文档窗口中打开一个包含标记的文件（如 Web 表单或母版页）时，你会在窗口左下角看到三个按钮。通过这些按钮，如图 2-9 所示，你可以在不同的视图之间切换。该图显示了一个母版页，你将在第 6 章学习它。

![](img/9e033e3b9560597824f8b22941d6d8bb_84_0.png)

图 2-9

Source View 是打开页面时的默认视图。它显示页面的原始 HTML 和其他标记，如果你想调整页面的内容并且对想要更改的内容和位置有很好的了解，这非常有用。如上一章所述，我使用 Markup View 而不是 Source View 来指代 ASP 和 HTML 页面的标记。

Design 按钮使你能够将文档窗口切换到 Design View，从而了解页面最终会是什么样子。在 Design View 中，你可以使用主菜单中的 Visual Aids 和 Formatting Marks 子菜单来控制诸如换行符、边框和空格之类的视觉标记。但子菜单提供了一个名为 Show 的菜单项，使你能够打开或关闭视觉辅助。关闭它们是有用的，如果你想了解页面在浏览器中的最终效果。你应该使用 Design View 来了解页面最终会是什么样子。尽管 VS 具有出色的渲染引擎，可以很好地在 Design View 中显示页面，但你也应该始终在浏览器中检查你的页面，因为你在 VS 中看到的是页面在处理之前的状态。页面上的服务器控件会发出改变浏览器中页面外观的 HTML。因此，建议尽可能在浏览器中查看页面，以便检查它是否会以你想要的方式显示。还建议在你能找到的尽可能多的浏览器中测试你的网站，因为它们在渲染网页的方式上可能存在细微差异。Planet Wrox 网站已针对最近版本的 Microsoft Internet Explorer、Firefox、Google Chrome、Safari 和 Opera 进行了开发和测试。你将在书中的各个地方看到这些浏览器的屏幕截图。在第 18 章，你将介绍 Browser Link，这使得浏览器测试变得更加容易。

Split 使你能够同时查看 Design 和 Markup View，如图 2-10 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_85_0.png)

图 2-10

Split View 在你想查看向页面的 Design View 添加控件时 VS 生成的代码时非常有用。反过来也非常有用：当你在 Markup View 中对页面的标记进行更改时，你可以看到它在 Design View 中的效果。有时 Design View 会与 Markup View 不同步。如果是这种情况，Design View 顶部会出现一条消息。只需单击该消息或保存页面即可更新 Design View。你可以使用 Ctrl+Page Up 和 Ctrl+Page Down 键在三种不同模式之间循环。

如果你希望页面以不同于 Markup View 的视图打开，请选择 Tools Options。然后展开 HTML Designer，并在 General 类别中选择你首选的视图。或者，在 VS 右上角的 Quick launch 框中（可通过按 Ctrl+Q 访问）输入 HTML Designer General，然后单击出现的那一列表中的项目。

> NOTE 最初，Visual Studio 对基于标记的文件有两个编辑器。对于表单（以及你将在本书后面遇到的用户控件），Visual Studio 使用随早期版本 Visual Studio 一起提供的旧编辑器。此编辑器支持 Design View。新的 HTML 编辑器主要关注代码编辑，不支持 Design View。这意味着你可以为 Web 表单切换到 Design View，但不能为常规 HTML 文件。如果还想为 HTML 文件使用 Design View，可以在 Tools Options Text Editor File Extension 下将 .htm 扩展名与 HTML (Web Forms) 编辑器关联。

除了在 Markup View 窗口中看到的 HTML 和其他标记外，Web 表单还可以包含 C# 或 Visual Basic .NET 中的代码。此代码放置的位置取决于你创建的 Web 表单的类型。下一节更详细地解释了你拥有的两种选择。

## 选择代码后置和内联代码页面

Web 表单有两种形式：要么是带有代码后置的 .aspx 文件（文件名为 Web 表单名加上 .vb 或 .cs 扩展名），要么是代码嵌入其中的 .aspx 文件，称为带内联代码的 Web 表单。虽然你直到第 5 章才看到太多代码，但了解这些类型的 Web 表单之间的区别很重要。首先，带内联代码的 Web 表单更容易理解。因为用于编程网站的代码与同一个 Web 表单，因此你可以清楚地看到代码与文件的关系。但是，如果你的页面变大并且需要更多功能，通常将代码放在单独的文件中会更容易。这样，它就完全与标记分离，使你能够专注于手头的任务。

在下一个练习中，你将使用两个文件来演示代码后置和内联代码之间的区别。

## TRY IT OUT 向你的网站添加带代码的 Web 表单

你在本次练习中使用的文件不是最终应用程序所必需的。为了避免项目混乱，你应该将它们放在单独的 Demos 文件夹中。

- 1. 在 Solution Explorer 中，右键单击你的网站并选择 Add -> New Folder。将文件夹命名为 Demos 并按 Enter。
- 2. 右键单击 Demos 文件夹并选择 Add -> New Item。在出现的对话框中，在左侧选择你的编程语言，单击 Web Form 模板，并将文件命名为 CodeBehind.aspx。确保选中 Place Code in Separate File 复选框。最后，单击 Add 按钮。页面应以 Markup View 打开，以便你可以看到页面的 HTML。
- 3. 在文档窗口底部，单击 Design 按钮以从 Markup 切换到 Design View。你看到的页面背景为白色，顶部有一个小虚线矩形。虚线矩形代表你在 Markup View 中看到的 div 元素。
- 4. 从 Toolbox 拖动 Label 从 Standard 并将其放置在页面的虚线区域中。记住，如果 Toolbox 未打开，你可以使用快捷键 Ctrl+Alt+X。 在 Design View 中，你的屏幕现在应如下图 2-11 所示。

```
CodeBehind.aspx * x
codebehind.aspx.cs
[Label]
```

| Design | Split | Source | <html><body><form id="Form1"><div><asp:Label ID="Label1" /> |

图 2-11

- 5. 双击 <div> 元素虚线 *下方* 的白色区域中的某个位置。VS 从 Design View 切换到文件的代码后置，并添加在浏览器中加载页面时触发的代码：

### VB.NET

```
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load

End Sub
```

### C#

```
protected void Page_Load(object sender, EventArgs e)
{
}
```

尽管这段代码现在看起来可能有点吓人，但现在不要太担心。在大多数情况下，VS 会自动为你添加它，就像你刚才看到的那样。在后面的章节中，你将看到这段代码的确切工作原理，但现在重要的是要意识到，你将放置在以 Protected 开头并以 End Sub 结尾的行之间（在 Visual Basic 中）以及花括号之间（在 C# 中）的代码将在浏览器中请求页面时执行。

从现在开始你看到的所有示例都包括 Visual Basic (VB.NET) 和 C# 版本，因此始终选择与你的编程语言匹配的版本。

- 6. 将光标放在 VS 创建并添加的空行中以标记标签的代码，该代码将今天的日期和时间分配给标签，最终将在浏览器中显示：

### VB.NET

```
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
Label1.Text = "Hello World; the time is now " + DateTime.Now.ToString()

End Sub
```

### C#

```
protected void Page_Load(object sender, EventArgs e)
{
Label1.Text = "Hello World; the time is now " + DateTime.Now.ToString();
```

请注意，当你输入 L 表示 Label 时，你会得到一个选项列表可供选择。这是 Visual Studio IntelliSense 的一部分，这是一个很棒的工具，可以帮助你编写代码而不是输入。不是输入单词 Label，你只需输入字母或字母 La，然后从列表中选择适当的项目，如图 2-12 所示。

要完成所选单词，你可以按 Enter 或 Tab 甚至句点。在后一种情况下，你会立即得到另一个列表，使你能够通过简单地输入前几个字母来选择单词。此功能是一个真正的生产力工具，因为你可以用更少的击键编写代码。IntelliSense 也适用于许多其他文件类型，包括 ASPX、HTML、CSS、JavaScript 和 XML。在许多情况下，只要开始输入，选项列表就会自动弹出。如果没有，请按 Ctrl+Spacebar 调出它。如果列表覆盖了窗口中的部分代码，请按住 Ctrl 键使窗口透明。

