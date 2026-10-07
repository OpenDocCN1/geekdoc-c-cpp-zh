
End Sub

```csharp
using System.Xml;
using System.Xml.Schema;
protected void Load(object sender, EventArgs e)
{
    int itemCount = 0;
    XmlReaderSettings settings = new XmlReaderSettings();
    string booksSchema = Server.MapPath("books.xsd");
    settings.ValidationType = ValidationType.Schema;
    settings.ValidationFlags = ValidationFlags.None;
    settings.ValidationEventHandler += ValidationEventHandler;
    string booksFile = Server.MapPath("books.xml");
    using (XmlReader reader = XmlReader.Create(booksFile, settings))
    {
        while (reader.Read())
        {
            if (reader.NodeType == XmlNodeType.Element &&
                reader.LocalName == "book")
            {
                itemCount++;
            }
        }
    }
    Response.Write(String.Format("Found {0} books!", itemCount));
}
private void ValidationEventHandler(object sender, ValidationEventArgs e)
{
    Response.Write(e.Message);
}
```

## 使用 XDocument 验证 Schema

`System.Xml.Linq` 的大部分内容桥接了 `System.Xml`。例如，`XDocument` 有一个扩展方法。

将匿名方法作为 `Validate` 方法的参数。`(param1, param2) >> ( method )` 语法初看看起来有点突兀，因为你可能不习惯看到等大于符号，但它让代码变得整洁得多。

## 包含 NameTable 优化

`XmlReader` 使用 `NameTable`，它列出了该文档中使用的所有已知带命名空间的元素和属性。这个过程被称为原子化（atomization）——字面意思是将 XML 文档拆分为它的原子部分。如果你可以创建一个并存储在表中、且与其他元素名称相同的书本对象引用，那么就不就不需要在内部结构中存储多次字符串。

虽然这是一个内部实现细节，但它是一种受支持且有效的方法，可以显著提高 `XmlReader` 和 `XmlDocument` 等 XML 类的速度。向 `NameTable` 添加你确定存在于文档中的名称元素。列表 10-5 和 10-6 使用字符串将一个大的字面量与 `reader.LocalName` 进行比较。这些比较也可以通过将它们转换为多次对象引用来优化。初始化后，`Xml NameTable` 可以在多个 `System.Xml` 和 `XmlDocument` 实例之间共享。该主题将在稍后介绍。

因为你正在计算书本元素，请创建一个包含该元素（`book`）的 `NameTable`，并且不要再次计算字符串，而是像列表 10-7 那样将对象引用与对象引用进行比较。

### 列表 10-7：使用 NameTable 优化 XmlReader

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
Dim bookCount As Integer = 0
Dim settings As XmlReaderSettings()
Dim nt As NameTable = New NameTable()
Dim book As Object = nt.Add("book")
settings.NameTable = nt
Dim bookSchema As String = Path.Combine(reader.PhysicalApplicationPath, "books.xsd")
settings.Schemas.Add(Nothing, XmlReader.Create(bookSchema))
settings.ValidationType = ValidationType.Schema
settings.ValidationFlags = XmlSchemaValidationFlags.ReportWarnings
AddHandler(settings.EventHandler, 
AddressOf Whitespace_ValidationEventHandler)
settings.IgnoreWhitespace = True
settings.IgnoreComments = True
Dim bookFile As String = Path.Combine(reader.PhysicalApplicationPath, "books.xml")
Using reader As XmlReader.Create(bookFile, settings)
While (reader.Read())
If (reader.NodeType = XmlNodeType.Element) Then
	And book.Equals(reader.LocalName) Then
		"A subtle, but significant change"
		bookCount += 1
	End If
End If
End While
Response.Write(String.Format("Found {0} books!", bookCount))
```

### 列表 10-7（续）

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    int count = 0;
    XmlReaderSettings settings = new XmlReaderSettings();
    NameTable nt = new NameTable();
    object book = nt.Add("book");
    settings.NameTable = nt;
    string booksSchema = Path.Combine(Request.PhysicalApplicationPath,
        "books.xsd");
    settings.Schemas.Add(null, XmlReader.Create(booksSchema));
    settings.ValidationType = ValidationType.Schema;
    settings.ValidationFlags |= XmlSchemaValidationFlags.ReportValidationWarnings;
    settings.ValidationEventHandler += 
        new IgnoreWhitespaceEventHandler(settings.ValidationEventHandler);
    settings.IgnoreWhitespace = true;
    settings.IgnoreComments = true;
    string booksFile = Path.Combine(Request.PhysicalApplicationPath, "books.xml");
    using (XmlReader reader = XmlReader.Create(booksFile, settings))
    {
        while (reader.Read())
        {
            if (reader.NodeType == XmlNodeType.Element &&
                book.Equals(reader.LocalName)) //A subtle, but significant change
            {
                count++;
            }
        }
    }
    Response.Write(String.Format("Found {0} books!", count));
}
```

`NameTable` 被添加到 `XmlSettings` 对象中，返回存储在 `NameTable` 中的名为 `book` 的添加节点引用。`book` 引用随后用于与 `reader.LocalName` 属性进行比较。我们特别选择使用所有对象上的 `Equals` 方法来执行身份检查。这两个对象是相同的。在列表 10-7 中，当 `reader` 处理 `Books.xml` 中的元素时使用 `NameTable`，对于较少量的书籍将产生明显的收益。然而，对于接近 10MB 大小的较大 XML 文档，可能会看到大量的性能提升——特别是涉及计算和 `XmlReader` 操作时。此外，由于 `NameTable` 缓存在 `XmlReaderSettings` 对象中，会产生额外的性能提升。

## 从 XML 获取强类型

如果你正在使用对象，从 `XmlReader` 获取数据应该感觉很熟悉。以前，一个名为 `XmlConvert` 的辅助类获取强类型，如下所示：

```vb
//在 .NET Framework 中获取 double
Double price = XmlConvert.ToDouble(reader.ReadString());
//.NET Framework 2.0 替换并改进
Double price = reader.ReadElementAs();
```

移除不必要的方法调用可以让代码更整洁、易读。列表 10-8 不仅增加了对书籍的计数，还使用 `ReadElementAs` 获取所有书籍的总和。注意，为了简洁，如果 `reader` 没有任何架构信息，它将直接以字符串形式返回。

### 列表 10-8：使用 XmlReader.ReadElementAs

```vb
Dim count As Integer = 0
Dim total As Decimal = 0
Dim settings As New XmlReaderSettings()
Dim nt As New NameTable()
Dim book As Object = nt.Add("book")
Dim price As Object = nt.Add("price")
settings.NameTable = nt
Dim booksFile As String = Path.Combine(Request.PhysicalApplicationPath, "books.xml")
Using reader As XmlReader.Create(booksFile, settings)
    While reader.Read()
        If reader.NodeType = XmlNodeType.Element
            And book.Equals(reader.LocalName) Then
                count += 1
        End If
        If reader.NodeType = XmlNodeType.Element
            And price.Equals(reader.LocalName) Then
                total += reader.ReadElementAsDecimal()
        End If
    End While
Response.Write(String.Format("Found {0} books that total {1:C}:", count, total))
```

```vb
Dim count As Integer = 0
decimal total = 0
Dim settings As New XmlReaderSettings()
NameTable nt = New NameTable()
object book = nt.Add("book")
object price = nt.Add("price")
settings.NameTable = nt
string booksFile = Path.Combine(Request.PhysicalApplicationPath, "books.xml")
using (XmlReader reader = XmlReader.Create(booksFile, settings))
{
    while (reader.Read())
    {
        if (reader.NodeType == XmlNodeType.Element &&
            book.Equals(reader.LocalName)) //A subtle, but significant change
        {
            count++;
        }
    }
}
```

### 列表 10-8（续）

```csharp
if (reader.NodeType == XmlNodeType.Element &&
    price.Equals(reader.LocalName))
{
    booktotal +=
        reader.ReadElementAsDecimal();
}
Response.Write(String.Format("Found {0} books that total {1:C}!",
count,booktotal));
```

列表 10-8 中的 `booktotal` 变量被强类型为 `decimal`，因此在 `String.Format` 调用中，它可以使用格式字符串 `{1:C}` 格式化为货币。这导致浏览器的输出如下：

Found 3 books that total $30.97!

## ReadSubtree 和 XmlSerialization

`XmlReader` 不仅帮助你从 XML 获取样本，还可以使用 XML 序列化和 `ReadSubtree` 获取更复杂的类型。

XML 序列化允许你向现有类添加属性，告诉 XML 序列化如何将对象表示为 XML。XML 序列化只持久对象的属性，而不是私有属性。

当你创建一个 `XmlSerializer` 时，会将一个 `Type` 传递给构造函数，`XmlSerializer` 使用反射检查对象并创建一个知道如何以 XML 格式读写入特定对象的临时程序集。`XmlSerializer` 在内部使用 `XmlReader` 的具体实现来序列化这些对象。

### 列表 10-9：带有 XML 序列化属性的 Author 类

```vb
Imports System.Xml.Serialization
<XmlRoot(Namespace = "http://example.books.com/")>
Public Class Author
    <XmlElement(ElementName = "first-name")>
    Public FirstName As String
    <XmlElement(ElementName = "last-name")>
    Public LastName As String
End Class
```

```csharp
using System.Xml.Serialization;
[XmlRoot(Namespace = "http://example.books.com/")]
public class Author
{
    [XmlElement(ElementName = "first-name")]
    public string FirstName;
    [XmlElement(ElementName = "last-name")]
    public string LastName;
}
```

接下来，此 `Author` 类配合 `XmlReader.ReadTree` 和 `XmlSerializer` 使用，以输出每本书作者的名称。列表 10-10 显示了仅添加到 `While` 循环中的额外语句。

## 列表 10-10：使用 XmlSerialization 从 XmlReader 读取 Author 实例

```vb
'尽早创建工厂
Dim factory As XmlSerializerFactory
Using reader As XmlReader = XmlReader.Create(booksFile, settings)
While (reader.Read())
    If (reader.NodeType == NodeType.Element
    And, Author.Equals(reader.LocalName))
        '使用工厂来创建并缓存序列化器
