
## @Assembly

`@Assembly` 指令将程序集（.NET 的构建模块）附加到它编译的 ASP.NET 页面或用户控件上，使程序集的所有类和接口对页面可用。该指令支持两个属性，如表 3-8 所示。

### 表 3-8

| 属性 | 说明 |
| :--- | :--- |
| Name | 允许指定用于附加到页面文件的程序集名称。程序集的名称应包含文件名，而不仅仅是文件扩展。例如，如果文件是 `MyAssembly.vb`，则 name 的值应为 `MyAssembly`。 |
| Src | 允许指定编译时使用的程序集文件源。 |

以下提供了如何使用 `@Assembly` 指令的一些示例：

```xml
<%@ Assembly Name="MyAssembly" %>
<%@ Assembly Src="MyAssembly.vb" %>
```

## @PreviousPageType

此指令用于指定任何跨页面提交（cross-page postings）的源页面。ASP.NET 页面之间的跨页面提交将在稍后的“跨页面提交”章节中解释。

`@PreviousPageType` 与 ASP.NET 4.5 提供的跨页面提交功能配合。该指令包含两个属性，如表 3-9 所示。

### 表 3-9

| 属性 | 说明 |
| :--- | :--- |
| TypeName | 设置发生回传（postback）的派生类名称 |
| VirtualPath | 设置发生回传提交页面位置 |

## @MasterType

`@MasterType` 指令将类名与 ASP.NET 页面关联，以便从指定的母页获取某些强类型引用或成员。该指令支持两个属性，如表 3-10 所示。

### 表 3-10

| 属性 | 说明 |
| :--- | :--- |
| TypeName | 设置用于获取强类型引用或成员的派生类名称 |
| VirtualPath | 设置从这些强类型引用和成员获取的页面位置 |

如何使用 `@MasterType` 指令的详情见第 16 章。以下是其用法示例：

```aspx
<%@ MasterType VirtualPath="/Wrox.master" %>
```

## @OutputCache

`@OutputCache` 指令控制 ASP.NET 页面或用户控件的缓存策略。它支持表 3-11 所示的属性。

### 表 3-11

| 属性 | 说明 |
| :--- | :--- |
| CacheProfile | 允许以集中方式管理应用程序的缓存配置文件。使用 `CacheProfile` 属性指定 `web.config` 文件中详细定义的配置文件。 |
| Duration | ASP.NET 页面或用户控件缓存的持续时间（秒）。 |
| Location | 位置枚举。默认值是 `Any`。这仅适用于 `.aspx` 页面，不适用于控件（`.ascx`）。其他可能的值包括 `Client`、`Downstream`、`None`。 |
| SqlDependency | 允许为缓存指定 SQL 依赖。 |
| VaryByContent | 指定缓存是否根据内容变化。 |
| VaryByControl | 指定缓存是否根据控件变化。 |
| VaryByEncodings | 指定缓存是否根据编码变化。 |
| VaryByHeader | 指定缓存是否根据标头变化。 |
| VaryByParam | 指定缓存是否根据参数变化。 |

下面是如何使用 `@OutputCache` 指令的示例：

```aspx
<%@ OutputCache Duration="180" VaryByParam="None" %>
```

## @Register

`@Register` 指令将别名与命名空间和类名关联，以便在自定义服务器控制语法中表示。当你将用户控件拖放到任何一个 `.aspx` 页面上时，就可以看到 `@Register` 指令。将用户控件拖动到 `.aspx` 页面会使 Visual Studio 2012 在页面顶部创建一个 `@Register` 指令。这在页面上注册了你的用户控件，以便通过特定名称在 `.aspx` 页面上访问该控件。

## 页面生命周期事件

如果你创建一个 ASP.NET 4.5 页面并开启跟踪（tracing），你可以看到主页面事件启动的顺序。它们按照图 3-7 所示的顺序触发。

通过增加这些选项，你现在可以在页面编译过程的许多点对页面以及页面上的控件进行操作。你可以在全书的代码示例中看到这些实用的页面事件。

![图 3-7](img/67a6707ff505c052edb96c0128fb3096_122_0.png)

> **注意**：回传使用 HTTP POST 操作而不是 HTTP GET。HTTP POST 在 HTTP 请求的消息正文中发送表单数据。HTTP GET 则在 HTTP 请求的 URL 中发送表单数据。

## 处理回传

当你处理 ASP.NET 页面时，请务必理解所列出的页面事件。这些事件非常重要，因为你将大量的页面行为放置在页面生命周期特定时间点的事件中。

在 Active Server Pages 3.0 中，开发者可以将页面提交到应用程序内的其他页面。ASP.NET 页面通常会回传到自身（post back）以处理事件（例如按钮点击事件）。

出于这个原因，你必须区分用户首次加载页面时的提交和普通的回传。回传其实就是如此——提交到同一个页面。回传包含了初始页面上收集的所有表单信息，以便在需要时进行处理。

由于 ASP.NET 页面可能会发生所有的回传，你想要知道请求是特定页面的首次实例，还是来自同一页面的回传。你可以通过 `Page` 类的 `IsPostBack` 属性进行此项检查，如下例所示：

### VB

```vb
If Not Page.IsPostBack Then
    ' Do processing
End If
```

### C#

```csharp
if (!Page.IsPostBack) {
    // Do processing
}
```

## 跨页面提交

ASP 3.0 中在 ASP.NET 早期版本中难以实现的常用功能之一是跨页面提交的能力。跨页面提交允许你提交一个表单（例如 `Page1.aspx`），并让此表单及所有控件的值自行提交到另一个页面（`Page2.aspx`）。

传统上，在 ASP.NET 1.0/1.1 中创建的任何页面都提交到自身，并在该页面实例中处理控件值。你可以使用 `Page.IsPostBack` 属性来区分页面的首次请求和回传，如本章开头所示。

有了这种功能，许多开发者希望能够提交到另一个页面，并在该页面上处理第一个页面的控件值。这在 ASP.NET 4.5 中是可以实现的，而且过程非常简单。

例如，名为 `Page1.aspx` 的页面包含一个简单的表单。列表 3-7 显示了该页面；你可以在该章节的代码下载包中的列表 03-07 (`Page1.aspx`) 中找到此列表的代码。

### 列表 3-7：Page1.aspx

#### VB

```vb
<%@ Page Language="vb" %>
<!DOCTYPE html>
<script runat="server">
    Protected Sub Button1_Click(sender As Object, e As EventArgs)
        Label1.Text = "Hello " + TextBox1.Text & "<br />" & "Date Selected: " + Calendar1.SelectedDate.ToShortDateString()
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>First Page</title>
</head>
<body>
    <form id="form1" runat="server">
        Enter your name <br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <p>
            When do you want to fly? <br />
            <asp:Calendar ID="Calendar1" runat="server"></asp:Calendar>
        </p>
        <br />
        <asp:Button ID="Button1" runat="server" Text="Submit page to itself" OnClick="Button1_Click"></asp:Button>
        <asp:Button ID="Button2" runat="server" Text="Submit page to Page2.aspx" PostBackUrl="Page2.aspx"></asp:Button>
        <p>
            <asp:Label ID="Label1" runat="server"></asp:Label>
        </p>
    </form>
</body>
</html>
```

#### C#

```csharp
<%@ Page Language="C#" %>
<!DOCTYPE html>
<script runat="server">
    protected void Button1_Click(object sender, EventArgs e)
    {
        Label1.Text = "Hello " + TextBox1.Text + "<br />" + "Date Selected: " + Calendar1.SelectedDate.ToShortDateString();
    }
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>First Page</title>
</head>
<body>
    <form id="form1" runat="server">
        Enter your name <br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <p>
            When do you want to fly? <br />
            <asp:Calendar ID="Calendar1" runat="server"></asp:Calendar>
        </p>
        <br />
        <asp:Button ID="Button1" runat="server" Text="Submit page to itself" OnClick="Button1_Click"></asp:Button>
        <asp:Button ID="Button2" runat="server" Text="Submit page to Page2.aspx" PostBackUrl="Page2.aspx"></asp:Button>
        <p>
            <asp:Label ID="Label1" runat="server"></asp:Label>
        </p>
    </form>
</body>
</html>
```

如列表 3-7 所示的 `Page1.aspx` 代码非常有趣。页面上显示了两个按钮。两个按钮都提交表单，但它们提交到不同的位置。第一个按钮提交到自身。这是 ASP.NET 1.0/1.1 的默认行为。

第二个按钮 `Button2` 的工作方式不同。它使用 `PostBackUrl` 属性将表单发送到另一个页面。这就是跨页面提交的能力。

### 列表 3-8：Page2.aspx (使用 FindControl)

#### VB

```vb
<%@ Page Language="vb" %>
<!DOCTYPE html>
<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs)
        Dim txtName As TextBox = CType(PreviousPage.FindControl("TextBox1"), TextBox)
        Dim calDate As Calendar = CType(PreviousPage.FindControl("Calendar1"), Calendar)
        Label1.Text = "Hello " & txtName.Text & "<br />" & "Date Selected: " & calDate.SelectedDate.ToShortDateString()
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Second Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <p>
            <asp:Label ID="Label1" runat="server"></asp:Label>
        </p>
    </form>
</body>
</html>
```

#### C#

```csharp
<%@ Page Language="C#" %>
<!DOCTYPE html>
<script runat="server">
    protected void Page_Load(object sender, EventArgs e)
    {
        TextBox txtName = (TextBox)PreviousPage.FindControl("TextBox1");
        Calendar calDate = (Calendar)PreviousPage.FindControl("Calendar1");
        Label1.Text = "Hello " + txtName.Text + "<br />" + "Date Selected: " + calDate.SelectedDate.ToShortDateString();
    }
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Second Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <p>
            <asp:Label ID="Label1" runat="server"></asp:Label>
        </p>
    </form>
</body>
</html>
```

你有几种方法可以获取从上一个页面暴露的控件值。第一种方法显示在列表 3-8 中。从上一个页面获取特定控件，你需要创建该控件的实例并使用 `PreviousPage` 属性的 `FindControl()` 方法。赋值给 `FindControl()` 的字符串是 ID。赋值后，你就可以像它源自当前页面一样操作服务器控件。

另一种暴露第一个页面（`Page1.aspx`）控件值的方法是为控件创建一个属性，如列表 3-9 所示。

### 列表 3-9：暴露控件属性

#### VB (Page1.aspx)

```vb
<%@ Page Language="vb" %>
<script runat="server">
    Public ReadOnly Property pp_TextBox1() As TextBox
        Get
            Return TextBox1
        End Get
    End Property

    Public ReadOnly Property pp_Calendar1() As Calendar
        Get
            Return Calendar1
        End Get
    End Property
</script>
```

#### C# (Page1.aspx)

```csharp
<%@ Page Language="C#" %>
<!DOCTYPE html>
<script runat="server">
    public TextBox pp_TextBox1 { get { return TextBox1; } }
    public Calendar pp_Calendar1 { get { return Calendar1; } }
</script>
```

现在这些属性在提交页面上暴露了，第二个页面（`Page2.aspx`）就可以轻松地处理从第一个页面暴露的服务器控件属性。列表 3-10 显示了 `Page2.aspx` 如何使用这些暴露的属性。

### 列表 3-10：使用第一个页面暴露的属性

#### VB (Page2.aspx)

```vb
<%@ Page Language="vb" %>
<%@ PreviousPageType VirtualPath="Page1.aspx" %>
<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs)
        Label1.Text = "Hello " & PreviousPage.pp_TextBox1.Text & "<br />" & _
                      "Date Selected: " & _
                      PreviousPage.pp_Calendar1.SelectedDate.ToShortDateString()
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Second Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <p>
            <asp:Label ID="Label1" runat="server"></asp:Label>
        </p>
    </form>
</body>
</html>
```

#### C# (Page2.aspx)

```csharp
<%@ Page Language="C#" %>
<%@ PreviousPageType VirtualPath="Page1.aspx" %>
<script runat="server">
    protected void Page_Load(object sender, EventArgs e)
    {
        Label1.Text = "Hello " + PreviousPage.pp_TextBox1.Text + "<br />" +
                      "Date Selected: " +
                      PreviousPage.pp_Calendar1.SelectedDate.ToShortDateString();
    }
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Second Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <p>
            <asp:Label ID="Label1" runat="server"></asp:Label>
        </p>
    </form>
</body>
</html>
```
