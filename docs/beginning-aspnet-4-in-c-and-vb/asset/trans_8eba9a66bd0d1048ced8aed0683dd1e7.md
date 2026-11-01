

- 一个 `WebPartManager` 控件（没有可视化组件）。
- 三个 `WebPartZone` 控件。
- 三个 Web 部件（日期、事件和用户信息），分别位于每个 `WebPartZone` 中。其中两个 Web 部件通过静态连接相连——如果你在“日期”中更改日期，“事件”中显示的日期也会随之更新。
- 一个用于更改显示模式的下拉列表。该列表并不包含所有可能的显示模式，只包含可用的模式。可用模式是从 `WebPartManager` 控件中获取的，稍后你会看到。列出的模式包括：
    - 浏览——这是默认模式，允许你查看和使用 Web 部件。在此模式下，每个 Web 部件都可以通过其右上角的下拉菜单进行最小化或关闭。
    - 设计——在此模式下，你可以重新定位 Web 部件。
    - 编辑——在此模式下，你可以编辑 Web 部件属性。每个 Web 部件的下拉菜单中会多出一个可用项：编辑。
    - 目录——在此模式下，你可以向页面添加新的 Web 部件。
- 一个将 Web 部件布局重置为默认布局的链接（仅对当前用户有效）。
- 一个 `EditorZone` 控件（仅在编辑模式下可见）。
- 一个 `CatalogZone` 控件（仅在目录模式下可见）。
- 目录中还有一个可以添加到页面上的额外 Web 部件。

每个 Web 部件都在一个用户控件中定义。

## Web 部件实际操作

为了说明布局可以如何更改，请使用下拉列表将显示模式更改为“设计”。你会注意到每个 `WebPartZone` 都会带上一个 ID 值（分别为 `LeftZone`、`CenterZone` 和 `RightZone`）。你还可以通过直接拖动其标题来移动 Web 部件——拖动时甚至能看到视觉反馈。如图 41-9 所示，图中正在移动“日期”Web 部件。

![](img/d7d2ffa0a76feaab821930e95daace93_1274_0.png)

图 41-9

接下来，尝试从目录中添加一个新的 Web 部件。将显示模式更改为“目录”，你会注意到 `CatalogZone` 控件在页面底部变得可见。单击“声明性目录”链接，你就可以向页面添加一个“链接”控件，如图 41-10 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1275_0.png)

图 41-10

注意这里还有一个“页面目录”链接。如果你通过某个部件的下拉菜单关闭了该 Web 部件，你会在这里找到它——它并没有被完全删除，只是被隐藏了。

接下来，将显示模式更改为“编辑”，并从某个 Web 部件的下拉菜单中选择“编辑”项，如图 41-11 所示。

当你选择此菜单选项时，将打开 `EditorZone` 控件。在示例中，该控件包含一个 `AppearanceEditorPart` 控件，如图 41-12 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1276_0.png)

图 41-11

![](img/d7d2ffa0a76feaab821930e95daace93_1276_1.png)

图 41-12

你可以使用此界面编辑并应用 Web 部件的属性值。

做出更改后，请通过注销并以另一个用户身份登录，然后再切换回第一个用户，来确认这些更改已为该用户保存。

```
<div class="zoneDiv">
<asp:WebPartZone ID="RightZone" runat="server">
<ZoneTemplate>
<uc4:UserInfo ID="UserInfo1" runat="server" Title="User Info" />
</ZoneTemplate>
</asp:WebPartZone>
</div>
```

最后是 `EditorZone` 和 `CatalogZone` 控件，分别包含一个 `AppearanceEditor` 控件，以及 `PageCatalogPart` 和 `DeclarativeCatalogPart` 控件：

```
<asp:PlaceHolder runat="server" ID="editorPH" Visible="false">
<div class="footerDiv">
<asp:EditorZone ID="EditorZone1" runat="server">
<ZoneTemplate>
<asp:AppearanceEditorPart ID="AppearanceEditorPart1" runat="server" />
</ZoneTemplate>
</asp:EditorZone>
<asp:CatalogZone ID="CatalogZone1" runat="server">
<ZoneTemplate>
<asp:PageCatalogPart ID="PageCatalogPart1" runat="server" />
<asp:DeclarativeCatalogPart ID="DeclarativeCatalogPart1" runat="server">
<WebPartsTemplate>
<uc3:LinksControl ID="LinksControl1" runat="server" Title="Links" />
</WebPartsTemplate>
</asp:DeclarativeCatalogPart>
</ZoneTemplate>
</asp:CatalogZone>
</div>
</asp:PlaceHolder>
</div>
</form>
```

`DeclarativeCatalogPart` 控件包含第四个用户控件，即用户可以添加到页面的“链接”控件。

## Web 部件代码

Web 部件的代码同样简单。例如，“链接”Web 部件仅包含以下代码：

```
<%@ Control Language="C#" AutoEventWireup="true"
CodeFile="LinksControl.ascx.cs"
Inherits="LinksControl" %>
<a href="http://www.msn.com/">MSN</a>
<br />
<a href="http://www.microsoft.com/">Microsoft</a>
<br />
<a href="http://www.wrox.com/">Wrox Press</a>

code snippet PCSWebParts/LinksControl.ascx
```

将用户控件用作 Web 部件不需要任何额外标记。这里唯一需要注意的是，用户控件（如 Default.aspx 中所使用的）的 `LinksControl` 元素带有一个 title 属性——尽管该用户控件本身没有 title 属性。`DeclarativeCatalogPart` 控件会使用该属性来推断要显示的 Web 部件标题（你可以在运行时通过 `AppearanceEditorPart` 对其进行编辑）。

## 连接控件

“日期”和“事件”控件之间的连接是通过将接口引用从 `DateSelectorControl` 传递给 `EventListControl`（这两个 Web 部件使用的两个用户控件类）实现的：

```csharp
public interface IDateProvider
{
    SelectedDatesCollection SelectedDates
    {
        get;
    }
}
```

*代码片段 PCSWebParts/App_Code/IDateProvider.cs*

`DateSelectorControl` 支持此接口，因此可以通过 `this` 传递 `IDateProvider` 的实例。该引用通过 `DateSelectorControl` 中的一个端点方法传递，该方法带有 `ConnectionProvider` 特性：

```csharp
[ConnectionProvider("Date Provider", "DateProvider")]
public IDateProvider ProvideDate()
{
    return this;
}
```

*代码片段 PCSWebParts/DateSelectorControl.ascx.cs*

这就是将 Web 部件标记为提供程序控件所需的全部内容。然后你可以通过其端点 ID（此处为 `DateProvider`）来引用该提供程序。

要使用提供程序，你需要使用 `ConnectionConsumer` 特性来修饰 `EventListControl` 中的一个消费方法：

```csharp
[ConnectionConsumer("Date Consumer", "DateConsumer")]
public void GetDate(IDateProvider provider)
{
    this.provider = provider;
    IsConnected = true;
    SetDateLabel();
}
```

*代码片段 PCSWebParts/EventListControl.ascx.cs*

此方法存储传入的 `IDateProvider` 接口引用，设置一个标志，并更改控件中的标签文本。

这个示例中需要查看的内容并不多。还有一些次要的外观修饰代码，以及 `Page_Load()` 中的事件处理程序细节，但这些都不是你真正需要在这里查看的。你可以通过查看本章的可下载代码来做进一步研究。

不过，Web 部件的内容远不止这些。Web 部件框架极其强大且功能丰富，有整本整本的书籍专门讨论这一主题。但希望通过本节内容，你已经对 Web 部件有所了解，并对其部分功能不再感到神秘。

## ASP.NET AJAX

Web 应用程序编程正处于不断变化和改进之中。如果你经常上网，可能会注意到，较新的网站在可用性方面明显优于较旧的网站。如今许多优秀的网站都提供了丰富的用户界面，其响应速度几乎可以媲美 Windows 应用程序。它们通过客户端处理来实现这一点，主要借助 JavaScript 代码，并且越来越多地使用一种名为 Ajax 的技术。

Ajax 并不是一项新技术。更确切地说，它是多种标准的组合，使得当前 Web 浏览器的丰富潜在功能得以实现。

支持 Ajax 的 Web 应用程序的一个关键定义性特征是，Web 浏览器能够通过带外操作与 Web 服务器通信；这被称为异步回发，或部分页面回发。在实践中，这意味着用户可以与服务器端功能和数据进行交互，而无需完全刷新页面。例如，当点击链接翻到表格中数据的第二页时，Ajax 使得只刷新表格内容而非整个网页成为可能。这意味着通过互联网传输的流量减少，从而使 Web 应用程序的响应速度更快。

你将在代码中使用微软对 Ajax 的实现，称为 ASP.NET AJAX。该实现将 Ajax 模型应用于 ASP.NET 框架。ASP.NET AJAX 提供了许多专门针对 ASP.NET 开发人员的服务器控件和客户端技术，使你能够以令人惊讶的少量工作量向 Web 应用程序添加 Ajax 功能。

本节将向你介绍：

- Ajax 以及使 Ajax 成为可能的相关技术。
- ASP.NET AJAX 及其组成部分，以及 ASP.NET AJAX 所提供的功能。
- 如何通过服务器端和客户端代码在你的 Web 应用程序中使用 ASP.NET AJAX。

这部分内容构成了本节的主体。

### 什么是 Ajax？

Ajax 允许你通过异步回发和动态的客户端网页操作来增强 Web 应用程序的用户界面。Ajax 一词由 Jesse James Garrett 发明，是 Asynchronous JavaScript and XML（异步 JavaScript 和 XML）的缩写。

> 注意，Ajax 并非首字母缩写词，因此不写作全大写的 AJAX。不过，在微软对 Ajax 的实现产品名称 ASP.NET AJAX 中，它使用了全大写拼写，你将在本章下一节中看到。

从定义上讲，Ajax 涉及 JavaScript 和 XML。然而，Ajax 编程还需要使用其他技术，如下表所述。

| 技术 | 说明 |
|---|---|
| HTML/XHTML | HTML（超文本标记语言）是 Web 浏览器用来在图形用户界面中呈现信息的表示和布局语言。你已经了解了 HTML 如何实现这种功能，以及 ASP.NET 如何生成 HTML 代码。可扩展超文本标记语言（XHTML）是使用 XML 结构的更严格的 HTML 定义。 |
| CSS | CSS（层叠样式表）是一种根据独立样式表中定义的规则来为 HTML 元素设置样式的手段。这使你能够同时将样式应用于多个 HTML 元素，并可以通过更换样式来改变网页的外观，而无需修改 HTML。CSS 既包含布局信息也包含样式信息，因此你还可以使用 CSS 在页面上定位 HTML 元素。 |
| DOM | DOM（文档对象模型）是一种以分层结构表示和操作 (X)HTML 代码的方式。这使得你可以访问网页中的“表 x 的第三行第二列”等内容，而无需使用更原始的文本处理方法来定位该元素。 |

