
注意该类和方法是静态的，`this`关键字指向被扩展的类，在此例中为`XmlSerializer`。创建XML并返回`XmlWriter`。`XmlSerializer`将对象序列化到此`XmlWriter`。然后当处理根元素时存在细微差别。

（注：此处原文似乎存在部分文本乱码或重复，翻译已根据上下文逻辑进行了平滑处理）

当从`XmlDocument`移除元素时，可以使用以下。

## XmlReader 和 XmlWriter 的改进

`XmlReader`和`XmlWriter`的改进方法：

- `Read`：`XmlReader`读取当前节点。
- `NextSiblings`：`XmlReader`提供后续兄弟节点。
- `Dispose`：`XmlReader`实现了`IDisposable`，这意味着它可以释放资源。

## XML 中的 XPath

在.NET中，使用`XPathDocument`有三种方式。`XPathDocument`是只读的，类似于`XmlDocument`。`XPathDocument`允许使用URL、文件或流。`XPathDocument`允许加载XML。

## XPath、XPathDocument 和 XmlDocument

`XPathDocument`非常好用，因为它是在内存中使用XPath的有效方式。`XPathDocument`实现了`IPathigable`接口，允许通过`XPathNavigator`遍历XML。`XPathNavigator`类与`XmlReader`不同，它不是只读的，提供了随机访问。

你通常希望使用`XPathDocument`在文档中向前和向后移动。`XPathDocument`是只读的，而`XmlDocument`允许写入。

`XmlDocument`包含内存验证；只有通过流或文件才能验证XML。`XmlDocument`还可以订阅如`NodeChanged`、`Inserting`等事件。

XPath是通过示例学习的。你必须学会如何使用`XPathDocument`。在`Books.xml`文件中有一些有效的XPath查询。XPath本身是一门丰富的语言，拥有数十种函数。因此，完全使用XPath超出了本书的范畴，表10-1让你了解了可能性。

### 表 10-1

| XPath 查询 | 结果 |
|---|---|
| `//book[@genre="novel"]/title` | 递归从根节点获取所有属性为 novel 的书籍的标题 |
| `//bookstore/book[author-last-name="Melville"]` | 获取书商店中作者姓为 Melville 的书籍 |
| `//bookstore/book[last-name="Melville"]` | 获取书籍节点下姓为 Melville 的所有作者 |
| `//book[title="The Gorgias" or title="The Confidence Man"]` | 递归从根节点获取标题为 The Gorgias 或 The Confidence Man 的书籍 |
| `//title[contains(., "The")]` | 获取所有包含 "The" 的标题 |
| `//book[not(price > 10.00)]` | 获取价格不大于 10.00 的书籍 |

列表10-12查询了`XPathDocument`中价格低于$10.00的书籍并输出其价格。为了说明如何使用内置的XPath函数，此示例使用了“大于”符号而不是“小于”符号。它通过使用`not()`方法反转了结果。XPath包含了许多用于字符串拼接、算术运算等的函数。`XPathDocument`通过调用`CreateNavigator`返回一个`XPathNavigator`。使用XPath的`Select`方法对`XPathNavigator`进行查询会返回一个`XPathNodeIterator`。该`XPathNodeIterator`通过`IEnumerable`进行`foreach`遍历。列表10-12使用了只读的`XPathDocument`，它不会更新内存中的数据。

### 列表 10-12：使用 XPathDocument 和 XPathNodeIterator 查询 xml

```vbnet
' document
dim booksFile = Server.MapPath("books.xml")
dim doc As New XPathDocument(booksFile)
dim nav As XPathNavigator = document.CreateNavigator()
```

```vbnet
// 一个可以在 XPath 表达式中使用的命名空间缀
dim namespaceMgr = new XmlNamespaceManager(nav.NameTable)
namespaceMgr.AddNamespace("b", "http://example.books.com")
// 所有价格不大于 10.00 的书籍
For Each node As XPathNavigator in nav.Select("/b:book[not(b:price > 10.00)]/b:price", namespaceMgr)
    dim price As Decimal =
    CType(node.ValueAs(GetType(Decimal)), Decimal)
    Response.Write(String.Format("Price is {0}<BR>", price))
```

```csharp
// document
string booksFile = Server.MapPath("books.xml");
XPathDocument document = new XPathDocument(booksFile);
XPathNavigator nav = document.CreateNavigator();
// 一个可以在 XPath 表达式中使用的命名空间缀
XmlNamespaceManager namespaceMgr = new XmlNamespaceManager(nav.NameTable);
namespaceMgr.AddNamespace("b", "http://example.books.com")
// 所有价格不大于 10.00 的书籍
foreach (XPathNavigator node in
nav.Select("/b:book[not(b:price > 10.00)]/b:price", namespaceMgr))
{
    decimal price = (decimal)node.ValueAs(typeof(decimal));
    Response.Write(String.Format("Price is {0}<BR>", price));
}
```

如果你想以`XPathNavigator`的形式更新底层的XML节点，你应该使用`XmlDocument`而不是`XPathDocument`。你的XPath评估可能会减慢速度，但你获得了编辑的能力。请注意这种性能上的权衡。通常情况下，你会想要使用只读的`XPathDocument`，此更改展示了这种变化，新增或更改的部分已**加粗**显示。此外，由于现在文档是可编辑的，价格增加了20%。

### 432 | 第 10 章 配合 XML 和 LINQ TO XML

### 列表 10：使用 XmlDocument 和 XPathNavigator 查询和编辑 XML

```vbnet
// Load document
Dim booksFile As String = Server.MapPath("books.xml")
Dim document As XmlDocument
document.Load(booksFile)
Dim nav As XPathNavigator = document.CreateNavigator()
```

```vbnet
// 一个可以在 XPath 表达式中使用的命名空间缀
namespaceMgr = new XmlNamespaceManager(nav, document.NameTable)
namespaceMgr.AddNamespace("b", "http://example.books.com")
// 所有价格不大于 10.00 的书籍
For Each node As XPathNavigator in nav.Select("//b:book[not(b:price > 10.00)]/b:price", namespaceMgr)
    Dim price As Decimal = CType(node.ValueAs.GetType(Decimal), Decimal)
```

```vbnet
node.SetTypeValue(price)
Response.Write(String.Format("Price is {0}<BR>", price))
```

```csharp
// document
string booksFile = Server.MapPath("books.xml");
XmlDocument document = new XmlDocument();
document.Load(booksFile);
XPathNavigator nav = document.CreateNavigator();
```

```csharp
// 一个可以在 XPath 表达式中使用的命名空间缀
XmlNamespaceManager namespaceMgr = new XmlNamespaceManager(nav, document.NameTable);
namespaceMgr.AddNamespace("b", "http://example.books.com");
// 所有价格不大于 10.00 的书籍
foreach (XPathNavigator node in
nav.Select("//b:book[not(b:price > 10.00)]/b:price", namespaceMgr))
{
    decimal price = (decimal)node.ValueAs(typeof(decimal));
    Response.Write(String.Format("Price is {0}<BR>", price));
}
```

## 数据集 (DATASETS)

`System.Data`命名空间和`System.Xml`命名空间已经开始融合它们的功能。`DataSet`是关系型数据和XML数据在混合类库中汇的极佳示例。在COM和XML的黄金时代，ADO 2.5重新发现了作为XML进行久久化的能力。在一个完全专注于处理关系型数据的类中戏剧性地包含XML功能，这对开发者的生产力来说是一个巨大的福音。可以从SQL Server中提取XML并对其进行操作。

### 将 DataSet 持久化为 XML

`System.Data`内部类在多处使用了`StreamWriter`和`XmlReader`。现在你已经更熟悉`System.Xml`概念了，请务必注意`System.Data`中的类所提供的方法重载。例如，`DataSet.WriteXml`方法有四个重载，其中一个接受`StreamWriter`。大多数带有`System.Data`的方法与`System.Xml`的类紧密耦合。列表10-14显示了另一种方法，通过使用来自SQL命令的`DataSet`从关系型数据中检索XML，并使用`DataSet.WriteXml`通过`Response`的`OutputStream`属性将其直接写入浏览器。

> 列表 10-14：使用 System.Data.DataSet 从 SQL Server 提取 XML

```vb
Dim connStr As String = "Data Source=.\SQLPRESS;
Initial Catalog=Northwind;
Integrated Security=SSPI;"
Using conn As New SqlConnection(connStr)
    Dim command As New SqlCommand("select * from customers", conn)
    conn.Open()
    Dim ds As New DataSet()
    ds.DataSetName = "Customers"
    ds.Load(command.ExecuteReader(), LoadOption.OverwriteChanges, "Customer")
    Response.ContentType = "text/xml"
    ds.WriteXml(Response.OutputStream)
End Using
```

`DataSet`具有固定格式，如图所示。文档的根节点是`Customers`，对应于`DataSetName`属性。`DataSet`一个或多个`DataTable`对象，这些`DataTable`的名称定义了包装元素——在这种情况下是`Customer`。`DataTable`的名称被传递给`DataSet`的`load`方法。在使用`DataSet`时，`DataSet`的名称、`DataTable`的名称与生成的XML之间的关联并不明显。生成的XML显示在图10-4的浏览器中。

![](img/7040c21013b8e6c23c612d6da3599ff8_494_0.png)

图 10-4

`DataSet`代表了一种数据模型，这与XML或DOM的数据思维方式非常不同。许多XML风格的思维围绕着InfoSet或DOM展开，而`DataSet`是基于行和列的。`XmlDataDocument`尝试在一个相对统一的模型中呈现这两种思维方式。

## XmlDataDocument

尽管`DataSet`在使用XML时有其自身相对不灵活的格式，但`XmlDocument`类并没有弥补这一差距。通过一种不寻常的混合，`XmlDataDocument`被引入了。此对象维护了所有XML结构的完整保真，并允许你通过`XmlDocument`API访问XML，而不会丢失关系型API的灵活性。一个`XmlDataDocument`包含它的`DataSet`，被称为“DataSet 感知（DataSet-aware）”。其内部`DataSet`提供了XML数据的关系视图。XML数据文档中任何未映射到关系视图的数据都不会丢失，而是可以被`DataSet`的API访问。

`XmlDataDocument`是一个接受`DataSet`作为参数的构造函数。对`XmlDataDocument`的任何更改都会反映在`DataSet`中，反之亦然。

现在取列表10-14中加载的`DataSet`，并使用你熟悉的`XmlDataDocument`和DOM API操作数据。接着，回到System世界，你会发现`DataSet`底层的`DataRows`已用新数据更新，如列表10-15所示。

### 列表 10-15：通过 XmlDataDocument 使用 DOM API 修改 DataSet

```vb
Dim connStr As String = "Data Source=.\SQLPRESS;
Initial Catalog=Northwind;
Integrated Security=SSPI;"
Using conn As New SqlConnection(connStr)
    Dim command As New SqlCommand("select * from customers", conn)
    conn.Open()
    Dim ds As New DataSet(null)
    ds.DataSetName = "Customers"
    ds.Load(command.ExecuteReader(), LoadOption.OverwriteChanges, "Customer")
//Response.ContentType = "text/xml"
//ds.WriteXml(Response.OutputStream)
// Added in Listing 10-13
    Dim doc As New XmlDataDocument(ds)
    doc.DataSet.EnforceConstraints = false
    XmlNode node = doc.SelectSingleNode("//Customer[CustomerID = 'ANATR']/ContactTitle")
    node.InnerText = "Boss"
    doc.DataSet.EnforceConstraints = true
    Dim dr As DataRow = doc.GetDataRow.GetRowFromElement(CType(node.ParentNode, HTMLElement))
    Response.Write(dr("ContactName").ToString() & " is the ")
    Response.Write(dr("ContactTitle").ToString())
End Using
```
