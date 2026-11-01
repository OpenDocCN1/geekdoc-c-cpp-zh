
```
<mass>18.998404</mass>
<density>1.696 g/cm3</density>
</specification>
</element>
<element Type="Noble Gas">
<name>Neon</name>
<symbol>Ne</symbol>
<number>10</number>
<specification>
<mass>20.1797</mass>
<density>0.901 g/cm3</density>
</specification>
</element>
</elements>
```

将 XML 文件保存为 Elements.xml。请记住在以下代码中更改文件的路径。此示例是一个小型查询工具，您可以使用它在代码提供的 XML 上测试不同的查询。

按照以下步骤创建具有查询功能的 WPF 应用程序：

+   1. 创建一个新的 WPF 应用程序并将其命名为 XPath Query。
+   2. 创建图 19-8 所示的对话框。按图所示命名控件，除了按钮应命名为 buttonExecute。将 TextBlock 包装在 ScrollViewer 控件中，并将其 VerticalScrollBarVisibility 属性设置为 Auto。
+   3. 转到代码视图并包含 using 指令。
+   4. 添加一个私有字段来保存文档，并在构造函数中初始化它：
+   5. 您需要一些辅助方法来在 textBlockResult TextBlock 中显示查询结果：

```
private XmlDocument document;

public MainWindow()
{
    InitializeComponent();
    document = new XmlDocument();
    document.Load(@"C:\BegVCSharp\Chapter19\XML and Schema\Elements.xml");
}
```

```
private void Update(XmlNodeList nodes)
{
    if (nodes == null || nodes.Count == 0)
    {
        textBlockResult.Text = "The query yielded no results";
        return;
    }
    string text = "";
    foreach (XmlNode node in nodes)
    {
        text = FormatText(node, text, "") + "\r\n";
    }
    textBlockResult.Text = text;
}
```

6. 更新构造函数以在应用程序启动时显示 XML 文件的全部内容：

```csharp
public MainWindow()
{
    InitializeComponent();
    document = new XmlDocument();
    document.Load(@"C:\BegVCSharp\Chapter19\XML and Schema\Elements.xml");
    Update(document.DocumentElement.SelectNodes("."));
}
```

7. 将之前的 Try It Out 部分中的两个方法 FormatText 和 AddAttributes 复制并粘贴到新项目中。

8. 最后，插入执行用户在文本框中输入内容的代码：

```csharp
private void buttonExecute_Click(object sender, RoutedEventArgs e)
{
    try
    {
        XmlNodeList nodes = document.DocumentElement.SelectNodes(textBoxQuery.Text);
        Update(nodes);
    }
    catch (Exception err)
    {
        textBlockResult.Text = err.Message;
    }
}
```

9. 运行应用程序并在 textBoxQuery 文本框中输入以下查询，以选择包含文本为 Hydrogen 的节点的元素节点：

```
element [name='Hydrogen']
```

![](img/cf72ea860016d2d680fc085fc06f265a_641_0.png)

图 19-8

## 工作原理

buttonExecute_Click 方法执行查询。由于您无法提前知道输入到 textBoxQuery 中的查询是否会产生单个节点或多个节点，因此您必须使用

`SelectNodes` 方法。这将返回一个 `XmlNodeList` 对象，或者如果使用的查询不合法，则抛出关于 XPath 的异常之一。

`Update` 方法负责遍历由 `SelectNodes` 选择的 `XmlNodeList` 的内容。它使用每个节点调用来自早期示例的 `FormatText`，而 `FormatText` 负责递归遍历节点树并创建可在 `textBoxResult` 控件中使用的可读文本。

在本章末尾的练习中，您将找到许多其他 XPath 查询可供尝试。在将它们输入 XPathQuery 应用程序以查看结果之前，请先自行确定查询的结果。

## 练习

19.1 将“创建节点”Try It Out 部分中的 Insert 示例更改为在 book 节点上插入名为 `Pages` 且值为 1000+ 的属性。

19.2 确定以下 XPath 查询的结果，然后通过将查询输入“选择节点”Try It Out 中的 XPathQuery 应用程序来验证您的结果。请记住，所有查询都在 `DocumentElement` 上执行，即 elements 节点。

```
//elements
element
element[@Type='Noble Gas']
//mass
//mass/..
element/specification[mass='20.1797']
element/name[text()='Neon']
Solution:
```

19.3 在许多 Windows 系统中，XML 的默认查看器是 Web 浏览器。如果您使用的是 Internet Explorer，将 `Elements.xml` 文件加载到其中时，您会看到 XML 的漂亮格式视图。为什么在文本框而不是浏览器控件中显示我们查询的 XML 不是理想的选择？

19.4 还使用 Newtonsoft 库将 JSON 转换为 XML 按钮（与本章所示示例相反）。

练习的答案可在附录 A 中找到。

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| XML 基础 | XML 文档由 XML 声明、XML 命名空间、XML 元素和属性创建。XML 声明定义 XML 版本。XML 命名空间用于定义词汇表，而 XML 元素和属性用于定义 XML 文档内容。 |
| JSON 基础 | JSON 是一种在传输 JavaScript 和 Web 服务时使用的数据语言。JSON 比 XML 更紧凑但更难阅读。 |
| XML 模式 | XML 模式用于定义 XML 文档的结构。当您需要与第三方交换信息时，模式尤其有用。通过就交换的数据达成一致的模式，您和第三方将能够检查文档是否有效。 |
| XML DOM | 文档对象模型（XML DOM）是 .NET Framework 为创建和操作 XML 提供的类的基础。 |
| JSON 包 | 您可以使用 Newtonsoft 等 JSON 包将 XML 转换为 JSON，反之亦然，并对 JSON 执行与 .NET XML 类类似的其他操作。 |
| XPath | XPath 是查询 XML 文档数据的方式之一。要使用 XPath，您必须熟悉 XML 文档的结构，以便能够从中选择单个元素。虽然 XPath 可用于任何格式良好的 XML 文档，但创建查询时必须了解文档结构这一事实意味着确保文档有效也确保了查询在文档之间有效，只要文档符合相同的模式。 |

## 20

## LINQ

## 本章将学习的内容

- LINQ to XML
- LINQ providers
- LINQ query syntax
- LINQ method syntax
- Lambda expressions
- Ordering query results
- Aggregates (Count, Sum, Min, Max, Average)
- SelectDistinctQuery
- Group queries
- Joins

## WROX.COM 本章代码下载

您可以在“下载代码”选项卡上找到本章的 wrox.com 代码下载，网址为 www.wrox.com/go/beginning visual#2015programming。代码位于第 20 章下载中，并根据整章中的名称单独命名。

本章介绍语言集成查询（LINQ）。LINQ 是 C# 语言的扩展，它将数据查询直接集成到编程语言本身中。

在 LINQ 之前，这类工作需要编写大量循环代码，而诸如对找到的对象进行排序或分组之类的额外处理则需要更多代码，具体取决于数据源而有所不同。LINQ 提供了查询、排序和分组许多不同类型数据（XML、JSON、SQL 数据库、对象集合、Web 服务、企业目录等）的便携且一致的方式。

```
new XElement("customers",
    new XElement("customer",
        new XAttribute("ID", "A"),
        new XAttribute("City", "New York"),
        new XAttribute("Region", "North America"),
        new XElement("order",
            new XAttribute("Item", "Widget"),
            new XAttribute("Price", 100)
        ),
        new XElement("order",
            new XAttribute("Item", "Tire"),
            new XAttribute("Price", 200)
        )
    ),
    new XElement("customer",
        new XAttribute("ID", "B"),
        new XAttribute("City", "Mumbai"),
        new XAttribute("Region", "Asia"),
        new XElement("order",
            new XAttribute("Item", "Oven"),
            new XAttribute("Price", 501)
        )
    )
);
WriteLine(xdoc);
Write("Program finished, press Enter/Return to continue:");
ReadLine();
}
```

5. 编译并执行程序（您只需按 F5 开始调试）。您将看到此处显示的输出：

```
<customers>
  <customer ID="A" City="New York" Region="North America">
    <order Item="Widget" Price="100" />
    <order Item="Tire" Price="200" />
  </customer>
  <customer ID="B" City="Mumbai" Region="Asia">
    <order Item="Oven" Price="501" />
  </customer>
</customers>
Program finished, press Enter/Return to continue:
```

输出屏幕上显示的 XML 文档包含一组非常简化的客户/订单数据。请注意，XML 文档的根元素是 <customers>，它包含两个嵌套的 <customer> 元素。这些元素又包含多个嵌套的 <order> 元素。<customer> 元素有两个属性 City 和 Region，而 <order> 元素具有 Item 和 Price 属性。

按 Enter/Return 退出程序并使控制台屏幕消失。如果您使用的是 Ctrl+F5（不调试启动），可能需要按两次 Enter/Return。

