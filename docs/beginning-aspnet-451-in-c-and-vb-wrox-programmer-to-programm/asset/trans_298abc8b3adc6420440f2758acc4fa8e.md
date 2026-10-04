

9. 切换回设计视图并为向导打开属性网格，确保其 ActiveStepIndex 设置为 0。设计器会记住你上次设计的步骤，并在标记视图中将该值存储在向导的 ActiveStepIndex 中。为了确保向导从第一页开始，你在查看更改并运行页面之前，应始终将 ActiveStepIndex 重新设置为 0（或在设计视图中单击向导控件中的第一步）。

10. 保存所有更改，关闭所有窗口，然后按 Ctrl+F5 在浏览器中打开页面。选中复选框使面板可见并输入你的编程语言。注意有一个 Previous 按钮，允许你返回向导的步骤以更改你的姓名。检查 Next 和 Previous 按钮，你还可以单击浏览器中信息左侧的链接。当你单击 Finish 按钮时，你会看到在向导中输入的信息的结果（图 4-15）。

![](img/9e033e3b9560597824f8b22941d6d8bb_157_0.png)

FIGURE 4-15

## How It Works

向导为你处理了大部分繁重的工作。它处理导航，确定何时显示正确的按钮（Next、Previous 和 Finish），并确保在结果页面中，你在向导步骤中添加的控件的值仍然可用，以便你可以用标签显示它们。你通过一种称为 View 的概念来实现这一点，你将在本章末尾了解更多相关信息。

你需要做的只是定义步骤并设置它们的 StepType。你将第一个步骤的 StepType 设置为 Auto。有了此设置，向导会计算出显示哪些按钮。因为它是向导中的第一步，没有可返回的上一步，所以它排除了 Previous（相当于手动将 StepType 设置为 Start）。你将第二个步骤的 StepType 设置为 Finish，这告诉向导绘制一个 Previous 按钮和一个 Finish。当你单击 Finish 按钮时，向导到达最后一个步骤，其 StepType 为 Complete。在此步骤中，导航按钮被隐藏，你看到的只是标签上的结果，该结果由页面代码隐藏中的代码分配。在第 5 章中，你将了解更多关于使此成为可能 的控件的信息。

除了前面各节中看到的控件外，还有一些其他控件值得检查。并非所有这些控件都将在此处详细讨论，因为它们在本书中不再使用。有关这些控件的良好信息来源是位于 http://msdn.microsoft.com 的 Microsoft Developer Network（MSDN）站点。要在此站点上查找有关控件的信息，请使用

你喜欢的搜索引擎，然后搜索 ControlName Control MSD。例如，要查找有关向导控件的更多信息，你可以搜索 Wizard Control MSD。通常，MSDN 站点位于搜索结果的顶部。

## Other Standard Controls

本节简要讨论工具箱标准类别中剩余的控件。你将在本书其余部分的示例应用程序中看到其中许多控件。

### LinkButton and ImageButton

LinkButton 和 ImageButton 控件与普通的 Button 控件类似。它们在被单击时都会导致向服务器的回发。LinkButton 将自己呈现为简单的 <a> 元素，使用 JavaScript 回发而不是请求新页面。ImageButton 也是如此，但显示用户可以单击以触发回发的图像。

### Image and ImageMap

这些控件在浏览器中显示图像方面非常相似。ImageMap 使你能够在图像上定义热点，单击时会导致向服务器回发或导航到不同页面。

### Calendar

Calendar 控件提供了一个丰富的界面，使用户能够选择日期。你将在本章末尾讨论 ASP.NET 状态引擎时看到更多相关内容。

### FileUpload

FileUpload 控件使用户能够上传可以存储在服务器上的文件。你将在第 14 章看到更多关于此控件的内容。

### Literal, Localize, and Substitute

这三个控件看起来都像 Label 控件，因为它们可以显示任何静态文本或 HTML。Literal 最大的优势在于它不呈现任何额外标签；它只显示你分配给其 Text 属性的内容，非常有用，可用于显示你在代码隐藏中构建的 HTML 或 JavaScript，或从数据库中检索的 HTML 或 JavaScript。

Localize 控件用于多语言网站，能够从翻译的资源文件中检索其内容。Substitute 控件用于高级缓存场景，使你能够仅更新否则完全缓存的页面的部分内容。这两个控件都超出了本书的范围，但如果你想对其进行深入讨论，可以考虑购买 Wrox 的 Professional ASP.NET 4.5 in C# and VB（ISBN：978-1-118-33182-0）。

### AdRotator

AdRotator 控件使你能够在网站上显示随机广告。广告来自你在服务器上创建的 XML 文件。由于它缺乏点击跟踪和日志记录等高级功能，而这些功能在除最简单场景之外的所有场景中都是必需的，因此该控件在当今网站中并不常用。

### HiddenField

HiddenField 控件使你能够在页面中存储随每次请求提交的数据。如果希望页面记住特定数据而不让用户在页面上看到它，这很有用。由于该字段会在页面的 HTML 源代码中显示，因此最终用户可以访问它，因此你不应在其中存储任何敏感数据。

### XML

XML 控件使你能够将数据从 XML 格式转换为另一种格式（HTML）以在页面上显示。请查看 Professional ASP.NET 4.5 以获取详细说明。

### Table

<asp:Table> 控件在许多方面与 HTML <table> 相对应。然而，由于该控件位于服务器端，你可以对其进行编程，动态创建新列和行并向其动态添加数据。

这结束了对标准类别中控件的讨论。在大多数 Web 情况下，你将至少使用其中几个控件。本节的其余部分讨论工具箱的其他类别。由于它们中的大多数在本书其余部分以某种形式使用，本章仅描述其用途，以便你对它们的使用有一个大致的了解。你将找到交叉引用到其他章节，在那里你可以找到更多关于它们的信息。

## HTML Controls

工具箱的 HTML 类别包含许多 HTML 控件，其外观与标准类别中的控件相似。例如，使用 Input（Button）看起来像 <asp:Button>。同样，还有一个 Select 控件，其对应控件为 <asp:DropDownList> 和 <asp:ListBox>。

与 ASP.NET 服务器控件不同，HTML 控件是客户端控件，并直接出现在 HTML 浏览器中。通过添加 runat="server" 属性。这使你能够从 Web 窗体的代码隐藏中进行编程，影响诸如其可见性之类的事情。

HTML 控件的功能比标准类别中的控件少。例如，Select 控件缺乏使用 ListItem Collection Editor 添加新项目到列表的设计支持。这迫使你手动在 VS 的标记视图中编写项目。

标准和 HTML 类别中的控件看起来非常相似，下一个部分讨论它们之间的差异，并让你对何时更倾向于一个类别而不是另一个类别有一个大致的了解。

## How to Choose Between Standard and HTML Controls

工具箱的标准和 HTML 类别中的控件似乎存在重叠。你应该选择哪一个以及为什么？通常，服务器控件为你提供了更多功能，包括 VS 中的设计支持和它们在运行时可以执行的操作。但这种功能是有代价的。由于其功能增强

