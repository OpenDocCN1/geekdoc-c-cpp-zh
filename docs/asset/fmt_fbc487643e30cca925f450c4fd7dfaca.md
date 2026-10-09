
```csharp
settings.IgnoreComments = true;

string booksFile = Server.MapPath("books.xml");

using (XmlReader reader = XmlReader.Create(booksFile, settings))
{
    while (reader.NodeType == XmlNodeType.Element &&
        "book" == reader.LocalName)
    {
        bookcount++;
    }
}
Response.Write(String.Format("Found {0} books!", bookcount));
}
}
```

注意列表 10-5 中的 `XmlReader.Create` 方法。你可能习惯于创建 `XmlReader` 的具体实现，但如果你尝试这种技术，你会发现它要灵活得多，因为你在其他 `XmlReader` 实例中可以使用 `XmlReaderSettings` 对象。`XmlReader` 实现了 `IDisposable`，因此在 VB 和 C# 中使用 `Using` 关键字都是正确的。

在列表 10-5 中，`Books.xml` 文件与 ASPX 页面位于同一目录，调用 `Server.MapPath` 会获取完整路径，然后将其传递给 `XmlReader.Create`，以及几行之前定义的 `XmlReaderSettings` 实例。

如果节点被成功读取，`Read` 方法可以返回 `true`。当没有更多节点可以读取时，它将返回 `false`。从 `XmlReader` 的角度来看，一切都是节点，包括空白区域、注释、属性和元素。如果列表 10-5 运行循环并在每次 `reader.LocalName` 读取时都增加 `bookcount` 变量，那么 `bookcount` 的最终值将是六。你会统计到起始标签和结束 book标签。因此，你必须更显式一些，确保修改语句不仅检查 `LocalName`，还检查 `NodeType`。

> `Reader.LocalName` 属性包含该节点的非命名空间名称。`Reader.Name` 属性则不同，它包含包含命名空间的完全限定名。在列表 10-5 的示例中使用 `Reader.LocalName` 属性是为了简单方便。你将在本章后面的部分了解到关于命名空间的内容。

## 使用 XDocument 而非 XmlReader

`System.Linq` 引入了一个新的 `XDocument` 类，它比 `XmlDocument` 提供了更加友好的界面，同时仍允许与 `XmlReader` 和 `XmlWriter` 互操作。列表 10-5 使用 `XDocument` 实现了与之前列表 10-5 相同的功能。`XDocument` 的加载方式与 `XmlDocument` 相同，但检索元素的语法显著不同。

该查询的语法非常简洁，但与你使用 T-SQL 时的逻辑相反。我们没有使用 `select..`，而是使用 LINQ 的 `from...select`。我们向 `booksxml` `XDocument` 请求其所有的后代节点，并将它们选择到 `book count` 范围内。所有 `book` 元素的值被选择到 `books` 变量中。

VB 参考了 C# 的优点，包含了一些“语法糖”，这使得处理 Visual Basic 和 XML 的体验更加集成化。注意使用 `Imports` 来声明 XML 命名空间，以及使用 `<...>` 来表示对 `Descendants` 方法的调用，使用 `<.>` 表示 `Elements`。编译器与 XML 这种高水平的集成使得在 VB 中处理 XML 变成了一种乐事——而且这看起来是 C# 级别的。

### 列表 10-5：使用 XDocument 处理 XML

```vb
Imports System.IO
Imports System.Xml
Imports System.Linq
Imports System.Xml.Linq
Imports <xmlns:b="http://example.books.com">
Partial Class _Default
    Inherits System.Web.UI.Page
    Protected Sub Page_Load(ByVal sender As Object
```

```csharp
using System;
using System.IO;
using System.Linq;
using System.Web.UI;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        XDocument booksXML = XDocument.Load(Server.MapPath("books.xml"));
        var books = from book in
            booksXML.Descendants("http://example.books.com/book")
            select book.Element("http://example.books.com/title").Value;
        Response.Write(String.Format("Found {0} books!", books.Count()));
    }
}
```

在 C# 和 VB 示例中，我们通过在调用 `XDocument.Descendants` 时不返回类型，利用了隐式类型。在 VB 中，我们使用 `Dim books` 和 `var books`。在这个示例中，我们使用 `from...select` 语法从 XML 对象中查询书籍，变量 `books` 的类型是 `System.Linq.Enumerable.Iterator`，其 `Count` 方法是由 LINQ 作为扩展方法添加的，允许我们检索框的数量。注意在调用 `XDocument.Descendants` 时不返回类型。在 VB 中处理 XML 命名空间。

# 第 10 章：使用 XML 和 LINQ to XML

### 列表 10-6q：使用 LINQ XDocument 结合 XML Schema 验证 XML

```VB
Imports System
Imports System.Xml
Imports System.Linq
Imports System.Xml.Linq
Imports System.Xml.Schema
```

```VB
Partial Class _Default
Inherits System.Web.UI.Page
Protected Sub Page_Load(ByVal sender As Object
```

```VB
Dim books = From book In booksXML...<b>
Select book.<title></b>.Value
```

```VB
Response.Write(String.Format("Found {0} books!", books.Count()))
End Sub
```

```VB
Sub ValidationEventHandler(ByVal sender As Object,
ByVal e As System.Xml.Schema.ValidationEventArgs)
Response.Write(e.Message)
End Sub
End Class
```

```C#
using System;
using System.Xml;
using System.Xml.Linq;
using System.Linq;
using System.Xml.Schema;
```

```C#
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string booksSchema = Server.MapPath("books.xsd");
        string booksFile = Server.MapPath("books.xml");
```

```C#
XmlSchemaSet schemas = new XmlSchemaSet();
schemas.Add(null, XmlReader.Create(booksSchema));
XDocument booksXML = XDocument.Load(booksFile);
booksXML.Validate(schemas, (senderParam, e) => {
    Response.Write(e.Message);
});
```

# 第 10 章：使用 XML 和 LINQ to XML

```C#
XNamespace ns = "http://example.books.com";
var books = from booksXML.Descendants(ns + "book")
    select book.Element(ns + "title").Value;
Response.Write(String.Format("Found {0} books!", books.Count));
```

注意列表 10-q 中 C# 示例中匿名事件处理程序的独特有语法。C# 3.0 程序不再需要创建一个单独的方法并将其传递给 Validate，而是可以匿名地将该方法作为 Validate 方法的参数。`(param1, param2) => { method }` 语法起初可能有些突兀，但它让代码变得整洁得多。

## 包含 NameTable 优化

`XmlReader` 内部使用 `NameTable`，它列出了该文档中使用的所有带命名空间的元素和属性。这一过程被称为原子化（atomization）——字面意思是将 XML 文档拆分为它的原子部分。如果你创建了 book 对象引用，并将其存储在包含其他元素名称的表中，那么就不需要在内部结构中存储多次一次 `"book"` 字符串。

虽然这是一个内部实现细节，但它是一种受支持且有效的方法，可以提高你对 XML 类（如 `XmlReader` 和 `XmlDocument`）的使用。你向 `NameTable` 中添加文档中将存在的元素。列表 10-5 和 10-6 使用字符串与 `reader.LocalName` 进行比较。这些比较可以通过将其转换为对象引用比较来优化，而后者的速度要快很多倍。此外，`NameTable` 可以在多个 `System.Xml` 类的实例之间共享，甚至在 `XmlReaders` 和 `XmlDocuments` 之间共享。这个主题很快就会被介绍。

由于你正在计算 book 元素，请创建一个包含此元素（book）的 `NameTable`，并且像列表 10-7 所示，与其比较字符串，不如比较对象引用和对象引用。

### 列表 10-7：使用 NameTable 优化 XmlReader

```VB
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) \
    Handles Me.Load
Dim bookcount As Integer = 0
Dim nt As Object New NameTable()
Dim book As Object = nt.Add("book")
settings.NameTable = nt
Dim booksSchemaFile As String =
    Path.Combine(Request.PhysicalApplicationPath, "books.xsd")
settings.Schemas.Add(Nothing, XmlReader.Create(booksSchemaFile))
settings.ValidationType = ValidationType.Schema
settings.ValidationFlags = ReportValidationWarnings
AddEventHandler settings.ValidationEventHandler, _
AddressOf settings_ValidationEventHandler
settings.IgnoreWhitespace = True
settings.IgnoreComments = True
```

```VB
Dim booksFile As String = 
Path.Combine(Request.PhysicalApplicationPath, "books.xml")
using reader XmlReader = XmlReader.Create(booksFile, settings)
If (reader.NodeType = XmlNodeType.Element
    and book.Equals(reader.LocalName)) Then
    "a subtle, but significant change"
    bookcount += 1
End If
End While
End Using
Response.Write(String.Format("Found {0} books!", bookcount))
```

# C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    int bookcount = 0;
    XmlReaderSettings settings = new XmlReaderSettings();
    NameTable nt = new NameTable();
    object book = nt.Add("book");
    settings.Namespace = nt;
    string booksSchemaFile = Path.Combine(Request.PhysicalApplicationPath,
    "books.xml.xsd")
    settings.Schemas.Add(null, XmlReader.Create(booksSchemaFile));
    settings.ValidationType = ValidationType.Schema;
    settings.ValidationFlags = XmlSchemaValidationFlags.ReportValidationWarnings;
    settings.ValidationEventHandler +=
    new ValidationEventHandler(settings_ValidationEventHandler);
    settings.IgnoreWhitespace = true;
    settings.IgnoreComments = true;
    string booksFile = Path.Combine(Request.PhysicalApplicationPath, "books.xml");
    using (XmlReader reader = XmlReader.Create(booksFile, settings))
    {
        while (reader.Read())
        {
            if (reader.NodeType == XmlNodeType.Element
                book.Equals(reader.LocalName)) //a subtle, but significant change
            {
                bookcount++;
            }
        }
        Response.Write(String.Format("Found {0} books!", bookcount));
    }
}
```

# 第10 章：使用 XML 和 LINQ to XML

```vbsharp
Path.Combine(Request.PhysicalApplicationPath, "books.xml")
Using reader As XmlReader = XmlReader.Create(booksFile, settings)
While (reader.Read()) {
    If (reader.NodeType = NodeType.Element
    And book.Equals(reader.LocalName)) Then
        bookcount += 1
    End
    If (reader.NodeType = NodeType.Element
    And price.Equals(reader.LocalName)) Then
        booktotal += reader.ReadElementContentAsDecimal()
    End
}
End While
End Using
```
