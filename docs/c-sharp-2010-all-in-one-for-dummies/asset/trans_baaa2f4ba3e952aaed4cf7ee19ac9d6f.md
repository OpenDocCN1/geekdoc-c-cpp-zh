
这种方法会格式化信息，以便更好地管理与服务器之间的通信。一次回发（PostBack）看起来像这样：

```
POST /admin/Pages/Add_entry.aspx?id=37aab-1292-4c75-95f5-5f9a5d3089a HTTP/1.1
Accept: application/*-xml,application/xhtml+xml, image/gif, image/jpeg, application/x-ms-xbap, application/vnd.ms-excel, application/vnd.ms-powerpoint, application/msword, application/x-shockwave-flash, */*
Referer: http://www.sempf.net/admin/Pages/Add_entry.aspx?id=e387ccb8-1292-4c75-985f-5f8e5db3089a
Accept-Language: en-US
User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET CLR 1.1.4322; InfoPath.2; OfficeLiveConnector.1.3; OfficeLivePatch.0.0)
Content-Type: multipart/form-data; boundary=-----------------------------7d922c32b0016
Accept-Encoding: gzip, deflate
Host: www.sempf.net
Content-Length: 9399
Connection: Keep-Alive
Pragma: no-cache

-----------------------------7d922c32b0016
Content-Disposition: form-data; name="__LASTFOCUS"

-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$txtTitle"

C# 4.0 at CONDG
-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$ddlAuthor"

Admin
-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$txtDate"

2009-09-08 22:21
-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$txtContent$TinyMCE$txtContent"

<p>I was very pleased to be able to give my C# 4.0 talk at the <a href="http://www.condg.org/">Central Ohio .NET Developers Group</a> last month.</p>
-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$txtUploadImage"; filename=""
Content-Type: application/octet-stream

-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$txtUploadFile"; filename=""
Content-Type: application/octet-stream

-----------------------------7d922c32b0016
Content-Disposition: form-data; name="ctl00$cpAdmin$txtSlug"

C-4.0-at-CONDG
-----------------------------7d922c32b0016
```

注意到数据的布局很规整，表单字段名、数据以及所有内容都清晰易读了吗？幸运的是，你完全不必操心这些。ASP.NET 会替你处理。

当你为某个对象（例如按钮）创建事件处理程序时，就会使用回发（PostBack）来完成这种通信。ASP.NET 就是这样改变你与服务器和客户端之间的交互方式的。至少就事件而言，它让 Web 编程看起来像 Windows 编程。

### 这关乎状态

Web 服务器使用中的另一个主要难题是状态。不，我指的不是 Address 数据库里的那个字段。我指的是服务器应当随时知道应用程序的状态。

由于 Web 浏览器的一个问题——通信不一致——Web 服务器在记住状态方面做得并不好。因为服务器不知道你下一分钟是否会发送任何内容，所以它们不能依赖一定会收到。

出于这个原因，服务器会尝试把一些值放入表单，以便以后使用，从而记住关于你会话的某些信息。服务器为此使用 ViewState 值。ViewState 是一个加密字符串，服务器可以用它在每次 POST 之间记住你是谁。

即使有了这些值，维护会话状态仍有其问题。例如，在安全应用中，你可能需要为某个数据库功能维护事务。这在 Web 应用程序中几乎不可能，因为你无法确定会收到返回确认。因此，几乎所有数据处理都发生在服务器上——我会在第 5 章更详细地介绍这一点。

## 第 2 章：构建 Web 应用程序

### 本章内容

- 在 Visual Studio 中工作
- 以风格开发
- 为视图控制器建模

Web 开发涉及的内容很多。过去人们常问我用什么语言编程。我告诉他们我是 Web 开发者。

> “不，说真的，你用什么语言编程？”他们会问。
> “Web。它是七种语言。我必须知道的七种语言。天哪，真的是七种吗？”

当时确实是七种。我需要懂 SQL、VBScript、XML、Visual Basic、HTML、CSS 和 JavaScript。至少现在情况好一点了。你可以不用 C++，而它曾经是必需的。哦，C# 可以替代 Visual Basic。其余的……

有了 Visual Studio 的加入，事情比过去稍微容易一些。当你选择 Visual Studio 作为构建 Web 应用程序的首选工具时，有两点需要考虑。第一是工具本身。第二是你将要使用该工具的方式，也就是你的方法学。

如果你一直在使用本书中的示例，那么在 Visual Studio 中工作会感到非常熟悉。用户界面有一个设计视图。代码视图的工作方式与所有其他环境中的代码视图完全一样。唯一需要注意的是，你偶尔会在 Web 应用程序中看到一些不寻常的文件类型。你会习惯它们的。我就习惯了。

方法学之争——也就是哪种方法学更好——更难让人适应，因为它是一场宗教战争。人们会出于各种原因告诉你使用这一种或那一种。我在这里也会这样做。你完全可以忽略我。只是不要仅仅因为某个东西又新又闪亮就使用它。做研究，尝试各种方法，并构建能用的软件。在本章中，你将看到如何用一种方法学构建应用程序，并以 Visual Studio 作为工具。

### 在 Visual Studio 中工作

你已经了解在 C# 中使用 Visual Studio 的基础知识；我们一直都在 Visual Studio 中工作。在 Web 领域使用 Visual Studio 会略有不同，但差别不大。使用 Visual Studio 构建 Web 应用程序实际上很像 WPF，因为 Web 应用程序的设计视图有一个代码元素——ASPX 文件中的 HTML 文档。然后还有一个代码元素，位于 ASPX.CS 文件中。

还有很多其他文件也让网页正常工作。包括图像、样式表和脚本文件。它们在 Visual Studio 中都有编辑器。不过，它们与 C# 一点关系都没有，所以我不会在这里过多讨论它们。关于这些文件的更多内容，请参见即将到来的“识别其他文件类型”一节，或参阅 Ken Cox 的 ASP.NET 3.5 For Dummies。

让我们在 Visual Studio 中建立一个简单的网站。你将用它来了解 Visual Studio 所有很酷的 Web 功能。然后就可以开始研究更复杂的网站了。建立简单网站只需完成以下操作：

1. 打开 Visual Studio，单击“项目”，然后单击“新建项目”。
2. 在“新建项目”对话框中，在左侧树视图中选择 Visual C#，然后选择 Web，并在右侧窗口中选择 ASP.NET Web 应用程序。
   我将自己的项目命名为 AspNetFirstSample。
3. 单击“确定”。
   Visual Studio 会创建一个项目。

嘿，就这么简单。它的运行方式很像你完成过的所有其他项目，会生成让 Web 项目正常工作所需的所有文件。要运行项目，请按 <F5>。这样做时，Visual Studio 会启动 Cassini，也就是 Visual Studio 自带的 Web 服务器。你的 Web 浏览器会启动，项目也会启动。

现在让我们把它复杂化。Web 应用程序有许多可移动部件，可能难以管理。在我 17 年 Web 开发经历中接触过的工具里，Visual Studio 让管理 Web 应用程序变得和任何工具一样轻松。

### 处理设计器

Visual Studio 会在设计器中启动 Web 项目。唯一的问题是，设计器显示的是某种代码视图。这不会马上帮助我们构建这个应用程序，对吧？

### 技术细节

过去，可视化界面是使用黑盒架构开发的。黑盒架构是一种设计组件的方式，让用户完全不知道它如何工作。你使用可视化设计器在页面上放置对象，位置等信息会以自定义二进制格式存储。没有设计器，关于“文档”（即表单本身）的任何内容都无法真正编辑。HTML，以及现在的 XAML，改变了这一切。现在，表单至少是使用基于标准、易于理解的标记语言来布局的。

要查看表单设计器，请单击“设计”选项卡。你会看到一个空白视图。目前这没关系。你将添加一些内容。

单击最左侧的“工具箱”选项卡。你已经使用过用于 Windows Forms 和其他应用程序的工具箱。现在它包含用于 Web 应用程序的控件。展开“标准”树视图。

“标准”树视图包含主要的 HTML 控件，这些控件是标准库的一部分，并带有 ASP.NET 的特色。将一个 Label 控件和一个 Button 控件拖到 Web 表单上。它应该看起来像图 2-1。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_668_0.png)

图 2-1：入门很简单。

你在这里做了什么？嗯，你添加了一个 Label 控件，它会变成一个包含一些文本的 <SPAN> 标签；还添加了一个 Button 控件，完成后它实际上会成为一个 <INPUT> 标签。
