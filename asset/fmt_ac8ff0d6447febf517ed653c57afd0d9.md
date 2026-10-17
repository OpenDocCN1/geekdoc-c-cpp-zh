
运行此示例将产生图 32-7 中的结果。

# 1226 | 第 32 章 构建全球化应用程序

![](img/7040c21013b8e6c23c612d6da3599ff8_1286_0.png)

图 32-6

从这个示例可以看到，`en-US` 文化使用逗号作为千位分隔符，使用句号作为数字之后可能出现的任何小数的开头。当与其他文化一起工作时，这个数字看起来非常不同。列表 32-9 为我们展示了在其他文化中表示数字的示例。

![](img/7040c21013b8e6c23c612d6da3599ff8_1283_0.png)

图 32-2

从你所可以看到，表示数字的构造之间，文化本身不同的符号更多的是使用分隔来处理千、百万或更多金额。例如在美国英语 `en-US` 中，我们使用以下表示数字：`$1,223,456.00`

`en-US` 文化使用美元符号 `($)` 紧跟数字，而符号文化使用不同的符号，`$1,223,456.00`

`en-US` 文化在美元符号 `($)` 之前使用美元符号 `($)`：`$1,223,456.00`

如你所见，表示日期/时间值的格式之间彼此截然不同——而且其中一种文化，泰语文化 `th-TH`，甚至使用了一种完全不同的历法，其年份标记为 2553 年。

## 理解数字和货币的差异

除了日期/时间值外，数字在不同文化之间的构造方式也不同。数字在不同文化中是如何表示的？嗯，这与数字本身的关系较小，更多的是与如何使用数字分隔符处理小数或显示千、百万等更多金额有关。例如，在美国英语 `en-US` 中，我们使用以下方式表示数字：

`5,123,456.00`

从这个示例中看到，`en-US` 文化使用逗号作为千位分隔符，使用句号作为数字之后可能出现的任何小数的开头。当与其他文化一起工作时，这个数字看起来非常不同。列表 32-9 为我们展示了在其他文化中表示数字的示例。

### 列表 32-9：在不同文化中处理数字

```vbsharp
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
    Dim myNumber As Double = 5123456.00
    System.Threading.Thread.CurrentCulture = new CultureInfo("en-US")
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
    System.Threading.Thread.CurrentCulture = new CultureInfo("vi-VN")
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
    System.Threading.Thread.CurrentCulture = new CultureInfo("fi-FI")
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
    System.Threading.Thread.CurrentCulture = new CultureInfo("fr-CH")
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    double myNumber = 5123456.00;
    System.Threading.Thread.CurrentCulture = new CultureInfo("en-US");
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
    System.Threading.Thread.CurrentCulture = new CultureInfo("vi-VN");
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
    System.Threading.Thread.CurrentCulture = new CultureInfo("fi-FI");
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
    System.Threading.Thread.CurrentCulture = new CultureInfo("fr-CH");
    Response.Write("<br>" + myNumber + "<br>")
    Response.Write(myNumber.ToString("n") + "<br>")
}
```

运行此示例将产生图 32-7 中的结果。

# 1228 | 第 32 章 构建全球化应用程序

相应的欧元数值以及货币的文化规范。因此，如果你在 ASP.NET 页面上使用自动文化设置且没有进行货币转换，那么你执行的操作与列表 32-11 中用于货币值显示的操作类似。

### 列表 32-11：在显示货币时恢复到特定文化

```vb
VB myNumber As Double = 5123456.0
Dim usCurr As CultureInfo = New CultureInfo("en-US")
Response.Write(myNumber.ToString("c", usCurr));
```

## 理解字符串排序的差异

在对进行全球化时，你已经学习了如何翻译值以及标头、日期/时间值等内容的构造。你还应该注意将文化设置应用到为应用程序建立的某些程序化行为中。一种可以根据所应用的文化设置而改变的操作是 `.NET` 字符串排序。你可能认为所有文化的排序方式都是相同的，但有时排序方式会存在差异。为了向你说明，列表 32-12 显示了在 `en-US` 文化下进行的排序操作。

### 列表 32-12：处理不同的文化

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    System.Threading.Thread.CurrentThread.Culture = New CultureInfo("en-US")
    Dim myList As List(Of String) = New List(Of String)
    myList.Add("Washington D.C.")
    myList.Add("Helsinki")
    myList.Add("Moscow")
    myList.Add("Warsaw")
    myList.Add("Vienna")
    myList.Add("Tokyo")
    myList.Sort()
    For Each item As String In myList
        Response.Write(item.ToString() + "<br>")
    Next
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    System.Threading.Thread.CurrentThread.Culture = new CultureInfo("en-US");
    List<string> myList = new List<string>();
    myList.Add("Washington D.C.");
    myList.Add("Helsinki");
    myList.Add("Moscow");
    myList.Add("Warsaw");
    myList.Add("Vienna");
    myList.Add("Tokyo");
    myList.Sort();
    foreach (string item in myList)
    {
        Response.Write(item.ToString() + "<br>");
    }
}
```

为了使此示例生效，你需要导入 `System.Collections` 和 `System.Collections.Generic` 命名空间，因为此示例使用了 `List(Of String)` 对象。

在这个示例中，创建了一个包含世界各地首都的随机顺序泛列表。然后调用泛 `List(Of String)` 对象的 `Sort()` 方法。该排序操作根据 ASP.NET 运行的定义文化的排序方式对字符串进行排序。列表 32-1 显示了 `en-US` 文化下的排序结果。图 32-9 显示了该操作的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_1288_0.png)

图 32-9

这完全符合预期。现在，更改之前的列表 32-12 示例，将文化设置为芬兰语，如列表 32-13 所示。

### 列表 32-13：将文化更改为芬兰语

```vb
System.Threading.Thread.CurrentThread.CurrentCulture = New CultureInfo("fi-FI")
```
```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("fi-FI")
```

如果你在芬兰文化设置下运行相同的代码，将得到图 32-10 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_1288_1.png)

图 32-10

如果你检查图 32-10 中进行的芬兰文化排序与图 32-9 中美国英语文化排序之间的差异，你会发现维也纳 `Vienna` 在芬兰语版本中处于不同的位置。在芬兰语中，字母 `V` 和字母 `W` 没有区别。由于没有差异，如果你使用芬兰文化进行排序，那么 `Vi` 会排在 `Wa` 之前，而 `Vienna` 在其他语言的字符串列表中将排最后。

## ASP.NET 资源文件

当你处理 ASP.NET 时，所有资源都由资源文件处理。资源文件是一个基于 XML 且具有 `.resx` 扩展的文件。你可以使用 Visual Studio 2010 来帮助构建此文件。资源文件提供了一组供指定文化使用的项目。在你的 ASP.NET 中，你将资源存储为本地资源或全局资源。以下章节将介绍如何使用每种资源。

## 使用本地资源

你会惊讶于自己可以多么轻松地构建 ASP.NET 页面，使其被其他语言本地化。实际上，你必须做的只是像往常一样构建 ASP.NET 页面，然后使用 Visual Studio 2010 的某些内置功能将页面转换为允许你引入其他语言的格式。

要查看这一点，请按照列表 32-14 所示像常一样构建 ASP.NET 页面。

```vb
@Page Language="VB" %>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        Label2.Text = TextBox1.Text
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Page</title>
</head>
<body>
    <form id="form" runat="server">
    <div>
        <asp:Label ID="Label1" runat="server" Text="What is your name?"></asp:Label>
        <br />
        <br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Submit Name" /></asp:Button>
        <br />
        <br />
        <asp:Label ID="Label2" runat="server"></asp:Label>
    </div>
    </form>
</body>
</html>
```

# 132 | 第 32 章 构建全球化应用程序

在说明中提到，每个服务器控件的几个属性已定义在资源文件中。例如，`Button` 服务器控件的 `Text` 和 `ToolTip` 属性已在该资源文件中公开，而 Visual Studio 的本地化功能会根据你所放置的内容从控件中拉取 `Default` 属性值。仔细查看此文件中 `Button` 服务器控件的构造，你可以发现 `Text` 和 `ToolTip` 属性的名称前都有一个名为 `ButtonResource` 的定义。这个键用于你之前看到的 Button 服务器控件中：

```
<asp:Button ID="Button!"
runat="server" Text="Submit Name"
meta:resourcekey="ButtonResource" />
```

![](img/7040c21013b8e6c23c612d6da3599ff8_1291_0.png)

图 32-12

你可以看到已经添加了 `meta:resourcekey` 属性，在这种情况下，它引用了 `ButtonResource`。资源文件中所有使用此键的属性，例如 `Text` 和 `ToolTip` 属性在运行时都会分配给此 Button 服务器控件。

## 添加另一个语言资源文件

现在 `Default.asresx` 文件已就绪，该文件用于不变区域。 此资源文件没有分配任何区域。要为 `Default.aspx` 页面添加另一个处理完全不同语言的资源文件，你需要将 `Default.asresx` 文件复制并粘贴到相同的 `App_LocalResources` 文件夹中，并重命名复制的文件。如果你使用 `Default.aspx.fi-FI.resx`，你将为以下键赋予相应的值，以创建一个芬兰语资源文件：

| ButtonResource.Text | Lähetä Nimi |
|---|---|
| Label1Resource.Text | Mika sinun nimi on? |
| PageResource.Title | Näytyssivu |

你希望在两个资源文件中都使用 `Label2Answer` 键创建一个自定义资源。`Default.asresx` 文件应包含以下键值：

```
Label2Answer    Hello
```
