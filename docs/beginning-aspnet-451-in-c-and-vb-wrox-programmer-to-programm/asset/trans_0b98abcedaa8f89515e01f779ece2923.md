

+ 3. 给定以下 Person 类，创建一个包含名为 `StudentId` 的字符串属性的新 Student 类代码应该是什么样的？利用继承来创建此新类。

# VB.NET

```
Public Class Person
    Public Property Name As String
End Class
```

# C#

```csharp
public class Person
{
    public string Name {get; set;}
}
```

你可以在附录 A 中找到练习的答案。

# 本章学习内容

| 术语 |  |
| --- | --- |
| 类 (Class) | 编程语言中对象的蓝图 |
| 集合 (Collection) | 一种能够同时存放多个特殊数据类型 |
| 构造函数 (Constructor) | 一种创建对象实例的特殊方法 |
| 封装 (Encapsulation) | 向外部隐藏类的内部机制和数据，以便更好地管理和保护这些数据 |
| 实例化 (Instantiating) | 根据类型定义在内存中创建新对象的过程 |
| 方法 (Method) | 对象上的操作，例如 Car 类的 Brake() 方法 |
| 命名空间 (Namespace) | 以层级方式组织类和其他类型的方法 |
| 面向对象 (Object Orientation) | 一种流行的编程风格，将软件建模为一组相互作用的对象 |
| 重写 (Overriding) | 在子类中重新定义在父类中定义的成员成员的行为 |
| 属性 (Property) | 对象的特征，例如人的名字 |

# 6 创建外观一致的网站

你将在本章学到：

- 如何使用主页（Master Pages）和内容页（Content Pages），让你能够定义网页的全局外观和效果
- 如何使用中心化的基页（Base Page），让你能够为站点中的所有页面定义通用行为
- 如何创建主题（Themes）来定义网站的视觉效果，并允许用户在运行时选择主题
- 如何创建皮肤（Skins）进行全站范围更改以控制布局
- ASP.NET 页面生命周期是什么以及为什么它很重要

WROX.COM 本章代码下载

你可以在 www.wrox.com/go/beaspnet451 的 Download Code 选项卡找到本章的 wrox.com 代码下载。代码位于 Chapter 6 文件夹中。

在构建网站时，你应该努力使布局和行为尽可能一致。一致性为你的网站提供了专业的外，并帮助访问者在站点中导航。幸运的是，ASP.NET 4.5.1 和 Visual Studio 2013 提供了许多强大的功能和工具来实现一致的设计，帮助你快速创建精美的页面。

在之前的章节中，你学习了如何使用 VS、HTML5、CSS 和服务器控件在视觉上控制你的网页。第 5 章向你介绍了 ASP.NET 编程。本章是第一个结合这些概念的章节，向你展示了——在许多方面——如何使用编程代码更改网站的外。

第一部分介绍了如何创建一个定义页面通用外观和效果的主页。你站点中的 ASPX 页面可以使用此主页，而无需重复通用布局。本章的其余部分在此主页的基础上构建。

# 使用主页实现一致的页面布局

对于大多数网站，当你从一个页面跳转到另一个页面时，只有部分内容会发生。不变的部分通常包括公共区域，如页眉、菜单和页脚。为了创建具有一致布局的页面，你需要一种在单个模板文件中定义这些静态区域的方法。2.0 之前的 ASP.NET 没有模板解决方案，因此你被迫在网站的每个页面上复制页面布局，或者依靠重新排列控件。坦率地说，由于主页的存在，情况已不再如此。主页最大的处处是它让你在一个位置定义站点中所有页面的外观和效果。这意味着如果你想更改网站的布局——例如，想将菜单从左侧移动到右侧——你只需要修改主页，基于此主页的页面会自动获取更改。

当主页在 ASP.NET 2.0 中引入时，它们迅速被开发者社区接受为 ASP.NET 页面的模板解决方案。此外，VS 提供了强大的设计时支持，因为它让你能够在设计时非常方便地使用和查看页面，而不仅仅是在运行时在浏览器中查看。

在某种程度上，主页看起来像一个普通的 ASPX 页面。它包含静态 HTML，如 `<html>`、`<head>` 和 `<body>` 元素，还可以包含其他 HTML 和 ASP.Net 服务器控件。在主页中，你设置了希望在每个页面重复的标记，例如页面的通用结构和菜单。

然而，主页并不是真正的 ASPX 页面，不能直接在浏览器中请求；它只作为模板，真实的网页（称为内容页）基于此模板。

与其使用你在第 4 章中看到的 @Page 指令，主页使用 @Master 指令来标识该页面为主主页：

# VB.NET

```vb
<@ Master Language="VB" %>
```

# C#

```csharp
<@ Master Language="C#" %>
```

就像普通的 ASPX 页面一样，主页可以有一个后置代码（Code Behind）文件，通过其 CodeFile 和 Inherits 属性标识：

# VB.NET

```vb
<@ Master Language="VB" CodeFile="Frontend.vb" Inherits="Default" %>
```

# C#

```csharp
<@ Master Language="C#" CodeFile="Frontend.cs" Inherits="Default" %>
```

为了创建内容可以填充的区域，你在主页中定义了 ContentHolder 控件：

```html
<asp:ContentHolder ID="ContentHolder1" runat="server" />
```

你可以创建多个 ContentHolder，尽管你通常只需要几个。页面特定的内容放在 Content 控件中，它指向主页：

# VB.NET

```vb
<@ Page Language="VB" MasterPage="~/MasterPages/Frontend.master" Inherits="Default" %>
```

# C#

```csharp
<@ Page Language="C#" MasterPage="~/MasterPages/Frontend.master" Inherits="Default" %>
```

注意 控件的 ContentHolderID 属性指向主页中定义的 ContentHolder。现在它指向默认的 ContentHolder，但在后面的练习中你会看到如何更改它。

在运行时，当请求页面时，主页的标记和内容页的标记合并并发送到浏览器。图 6-1 显示了只有一个 ContentHolder 的主页图。

为了看到这一过程，下面的章节将引导你创建主页和内容页。

# 主页

| 页眉 | 内容页 |
| --- | --- |
| 菜单 | ContentHolder |

![](img/9e033e3b9560597824f8b22941d6bb_235_0.png)

图 6-1

# 创建主页

可以使用添加对话框向站点添加主页。你可以将它们放在站点的任何自定义文件夹中，包括根文件夹，但从组织角度来看，将它们存储在单独的文件夹更为方便。与普通 ASPX 页面一样，它们支持内联代码模型以及后置代码模型。Planet Wrox 项目使用的主页专门使用后置代码模型。在接下来的练习中，你将学习创建一个简单的主页并在其中添加一些 HTML 来定义网站页面的通用结构。

> 尝试一下创建一个主页

+ 1. 在 Visual Studio 中打开 W Wrox 项目如果尚未打开）。
2. 在第 2 章中，你创建了一个名为 MasterPages 的文件夹来存放主页，并在该文件夹中添加了一个简单的主页。如果你没有执行练习，现在添加主页。方法是：在站点根目录下创建 MasterPages 文件夹，右键点击新文件夹，选择添加项，选择主页项。确保主页使用 Code Behind 并且使用的是你为站点选择的编程语言。将主页命名为 Frontend.master，最后点击。
3. 在主页的 <form> 标签之间添加以下高亮代码，替换 VS 创建主页时为你添加的 <div> 标签和 ContentPlaceholder。

