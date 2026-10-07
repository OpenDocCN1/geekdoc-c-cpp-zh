
`Dim xs As XmlSerializer = factory.CreateSerializer(GetType(Author))`

`Dim a As Author = (Author)xs.Deserialize(reader.ReadSubtree())`

`Response.Write(String.Format("Author: {1}, ({0})<BR/>", a.FirstName, a.LastName))`

`End If`

`End While`

```
```

```csharp
// 尽早创建工厂

XmlSerializerFactory factory = new XmlSerializerFactory();

using (reader = XmlReader.Create(booksFile, settings))

while (reader.Read())
{
    if (reader.NodeType == NodeType.Element &&
    author.Equals(reader.LocalName))
    {
        // 使用工厂来创建并缓存序列化器
        XmlSerializer xs = factory.CreateSerializer(typeof(Author));
        Author a = (Author)xs.Deserialize(reader.ReadSubtree());
        Response.Write(String.Format("Author: {1}, ({0})<BR/>", a.FirstName, a.LastName));
    }
}
```

另一种代码选项，正如你所看到的，作者原子（在 `Equals` 语句中使用）被添加到 `NameTable` 中，就像书籍和价格那样，通过 `Dim Author Object = nt.Add("author")` 实现。

当你为特定类型创建 `XmlSerializer` 实例时，反射使用反射创建一个临时程序集来处理序列化和反序列化。.NET Framework 2.0 引入了一个新的 `XmlSerializerFactory`，它会自动处理这些临时程序集的缓存。这个小型的工厂提供了一个重要的抽象层，允许你以方便的方式组织代码，而无需担心提前创建 `XmlSerializer` 实例。

## 使用 LINQ to XML 创建 CLR 对象

尽管 `XmlSerializer` 和 `System.Xml.Linq` 之间没有直接桥接，但确实存在一种通过 LINQ to XML 语法创建 CLR 对象的非常简洁的方法。这种语法比传统的 `XmlSerializer` 稍微灵活且更具容错，如列表 10-1q 所示。

### 列表 10-10q：读取 Author 实例

```vb
Dim booksXML = XDocument.Load(Server.Map("books.xml"))
```

```vb
Dim authors = From book In booksXML.<books:book> Select New Author \
With (.FirstName = book.books:author.<first-name>.Value, \
  .LastName = book.books:author.<last-name>.Value)
```

```vb
For Each a As In Author \
Response.Write(String.Format("{0}, {1}<BR/>", a.FirstName, a.LastName))
```

```csharp
Document booksXML = XDocument.Load(Server.Map("books.xml"));
XNamespace ns = "http://example.books.com";
var authors = from book in booksXML.Descendants(ns + "author") \
  select new {
    FirstName = book.Element(ns + "first-name").Value,
    LastName = book.Element(ns + "last-name").Value
  };
foreach (Author a in authors) {
  Response.Write(String.Format("{0}, {1}<BR/>", a.FirstName, a.LastName));
}
```

再次，注意 VB 示例中独特的语法，使用的是 `is` 而不是 "descendants"。在 C# 端，请注意如何使用 `select` 语法清晰地创建新的 `Author` 对象，以及新 `Author` 对象从 XML 元素中复制值的花括号。VB 示例假设了与之前在本章节列表 10-6q 中所示的相同语句。

## 使用 XmlWriter 创建 XML

`XmlWriter` 的工作方式与 `XmlReader` 完全相反。使用字符串拼接创建 XML 文档或片段是很诱人的人的，但你应该抵抗这种冲动。记住，XML 的核心在于 `InfoSet` 的表示，而不是角括号。如果你使用 `StringBuilder` 拼接字面量来创建 XML，你就会降到了 `InfoSet` 实现细节的级别。大多数人发现（作为一种可视化工具）VB 在生成代码缩进方面比 C# 激进得多。除非 `Indenting` 设置为 `Block` 或 `None`，否则不允许这种人工缩进。`XmlWriter` 显然也有 `XmlWriterSettings` 类，该类具有缩进、换行和编码的选项。列表 10-11 使用 `XmlWriter` 创建了一个书店并直接输出到 `Response.OutputStream`。ASPX 页面中的所有 HTML 标签必须为 XML 文档移除。轻松输出 XML 的另一种方法是使用 `StreamWriter`。列表 10-11 中不寻常的缩进在使用 `XmlWriter` 时显著且常见的。

# 列表 10-1iq：使用 XElement 树写入书商店

`Imports System.Xml`
`Imports System.Xml.Linq`

```vb
VB Partial Class _Default
Inherits System.Web.UI.Page
```

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs)
    Me.Load
    Dim price As Double = 49.99
    Dim publication As New DateTime(2005, 1, 1)
    Dim isbn As String = "1-057-610-0"
    Dim a As New Author()
    a.FirstName = "Scott"
    a.LastName = "Hanselman"
```

```vb
    Response.ContentType = "text/xml"
Dim books = "<bookstore xmlns=""http://examples.books.com"">
  <book publicationdate=""{publication}"" ISBN=""{isbn}"">
    <title>ASP.NET 2.0</title>
    <price>={price}</price>
    <author>
      <first-name>={a.FirstName}</first-name>
      <last-name>={a.LastName}</last-name>
    </author>
  </book>
</bookstore>"
    Response.Write(books)
```

```vb
End Sub
End Class
```

```csharp
using System;
using System.Xml.Linq;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
```

```csharp
    double price = 49.99;
    DateTime publicationDate = new DateTime(2005, 1, 1);
    string isbn = "1-057-610-0";
    Author a = new Author();
    a.FirstName = "Scott";
    a.LastName = "Hanselman";
```

```csharp
    Response.ContentType = "text/xml";
    XNamespace ns = "http://example.books.com";
    XDocument document = new XDocument(
        new XElement(ns + "bookstore",
            new XElement(ns + "book",
                new XAttribute("publicationdate", publicationDate),
                new XAttribute("isbn", isbn),
                new XElement(ns + "title", "ASP.NET 2.0 Book"),
                new XElement(ns + "price", price),
                new XElement(ns + "author",
                    new XElement(ns + "first-name", a.FirstName),
                    new XElement(ns + "last-name", a.LastName))))
            ));
    document.Save(Response.Output);
```

## 428 | 第 10 章 使用 XML 和 LINQ to XML

列表 10-11q (续)

```csharp
new XElement(ns + "first-name", a.FirstName);
new XElement(ns + "last-name", a.LastName);
});
Response.Write(books);
```

尽管 C# 示例跨多行显示，但它也可以写在一行中，因为它是一个单一的表达式。`XElement` 和 `XDocument` 的构造函数接受任意长度的参数数组，允许你以具声明性的方式创建 XML 文档结构。如果你将其与列表 10-11 进行比较，你会发现 `XmlWriter` 示例中的缩进使样本更具可读性，但并没有影响文档结构。使用 `XDocument`/`XElement` 声明时，结构是通过节点粘贴到对方的每个构造函数的方式表达的。

> 曾经有一个“将 XML 粘贴为 true”的功能，它没有进入发布的产品，而是作为示例分发的。该插件为你的 Visual Studio 编辑器添加了一个菜单项，它可以从剪贴板获取 XML 并将其作为 `XElement` 粘贴到编辑器中。你可以在 Visual Studio 内部通过 Help > Samples > C# Samples 文件夹找到它。该示例名为 PasteXmlAsLinq，可以编译并复制到任何 Visual Studio 加载项文件夹。

## 桥接 XmlSerializer 和 LINQ to XML

`XmlSerialization` 和 LINQ 类之间没有直接的桥接；`XDocument` 和 `XElement` 都包含一个返回 `XmlWriter` 的 `CreateWriter` 方法。当返回的 XML 转换为 `XElements` 并添加到父级 `XDocument` 或 `XElement` 中时。这允许你在单个表达式中混合使用 `XElements` 和 `XmlSerialization` 技术。尽管这可能被视为特殊情况，但 `XmlSerialization` 经常发生，意识到新旧技术如何良好地协同工作是有用的。BCL 随着新的 .NET Framework 版本而扩展，但并没有随着 LINQ 2.0。

此 C# 示例与列表 10-11 相同，它创建了一个扩展来为 `XmlSerializer` 添加一个 `SerializeAsElement` 方法，该方法返回一个包含序列化结果的 `XElement`。
首先是：

```csharp
static class XmlSerializerExtension
{
    public static XElement SerializeAsElement(this XmlSerializer serializer, object o)
    {
        XDocument d = new XDocument();
        using (XmlWriter w = d.CreateWriter())
        {
            serializer.Serialize(w, o);
        }
        XElement e = d.Root;
        e.Remove();
        return e;
    }
}
```

## XmlDocument 和 XPathDocument

注意该类和方法是静态的，`this` 关键字指向被扩展的类，在此例中为 `XmlSerializer`。创建 XML 并返回 `XmlWriter`。`XmlSerializer` 将对象序列化到此 `XmlWriter`。然后当处理根元素时存在细微差别。

```csharp
XmlSerializer xs = new XmlSerializer(typeof(Author));
XmlDocument document = new XmlDocument();
    new XElement(ns + "bookstore",
        new XElement(ns + "book",
            new XAttribute("publicationdate", publicationDate),
            new XAttribute("isbn", isbn),
            new XElement(ns + "title", "ASP.NET 2.0 Book"),
            new XElement(ns + "price", price),
            new XElement(ns + "author",
                new XElement(ns + "first-name", a.FirstName),
                new XElement(ns + "last-name", a.LastName))))
            ));
    document.Save(Response.Output);
```
