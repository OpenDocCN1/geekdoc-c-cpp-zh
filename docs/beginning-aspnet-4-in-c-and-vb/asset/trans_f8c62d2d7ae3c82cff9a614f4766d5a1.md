
下表列出了处理 XML 的一些其他有用的类。

| 类名 | 描述 |
|---|---|
| XmlNode | 一个表示 XML 文档中单个节点的抽象类。XML 命名空间中多个类的基类。 |
| XmlDocument | 继承自 XmlNode。这是 W3C DOM 实现。它在内存中提供 XML 文档的树表示，支持导航和编辑。 |
| XmlDataDocument | 继承自 XmlDocument。这是一个可以从 XML 数据或 ADO.NET DataSet 中的关系数据加载的文档。允许在同一视图中混合 XML 和关系数据。 |
| XmlResolver | 一个用于解析外部基于 XML 的资源（如 DTD 和模式引用）的抽象类。也用于处理 <xsl:include> 和 <xsl:import> 元素。 |
| XmlNodeList | 可以迭代的 XmlNodes 列表。 |
| XmlUrlResolver | 继承自 XmlResolver。解析由统一资源标识符 (URI) 命名的外部资源。 |

System.Xml 命名空间中的许多类提供了管理 XML 文档和流的方法，而其他类（如 XmlDataDocument 类）则在 XML 数据存储和存储在 DataSet 中的关系数据之间提供桥梁。

![](img/d7d2ffa0a76feaab821930e95daace93_966_0.png)

## 使用 System.Xml 类

以下示例使用 books.xml 作为数据源。你可以从 Wrox 网站 (www.wrox.com) 下载此文件和本章的其他代码示例，但它也包含在 .NET SDK 的多个示例中。books.xml 文件是一个虚构书店的图书目录。它包含诸如类型、作者姓名、价格和 ISBN 号码等图书信息。

这就是 books.xml 文件的样貌：

```xml
<?xml version="1.0"?>
<!--This file represents a fragment of a book store inventory database-->
<bookstore>
  <book genre="autobiography" publicationdate="1991" ISBN="1-861003-11-0">
    <title>The Autobiography of Benjamin Franklin</title>
    <author>
      <first-name>Benjamin</first-name>
      <last-name>Franklin</last-name>
    </author>
    <price>$8.99</price>
  </book>
  <book genre="novel" publicationdate="1967" ISBN="0-201-63361-2">
    <title>The Confidence Man</title>
    <author>
      <first-name>Herman</first-name>
      <last-name>Melville</last-name>
    </author>
    <price>$11.99</price>
  </book>
  <book genre="philosophy" publicationdate="1991" ISBN="1-861001-57-6">
    <title>The Gorgias</title>
<author>
    <name>Plato</name>
</author>
<price>$9.99</price>
</book>
</bookstore>
```

*代码片段 books.xml*

## 流式读取和写入 XML

如果曾使用过 SAX，XmlReader 和 XmlWriter 类会让你感到熟悉。基于 XmlReader 的类提供了一个非常快速的、只向前、只读的光标，用于流式传输 XML 数据进行处理。由于它是一种流模型，内存需求并不高。然而，你没有基于 DOM 模型可用的导航灵活性和读写能力。基于 XmlWriter 的类生成符合 W3C XML 1.0 命名空间建议的 XML 文档。

XmlReader 和 XmlWriter 都是抽象类。以下类派生自 XmlReader：

- XmlNodeReader
- XmlTextReader
- XmlValidatingReader

以下类派生自 XmlWriter：

- XmlTextWriter
- XmlQueryOutput

XmlTextReader 和 XmlTextWriter 可以与来自 System.IO 命名空间的基于流的对象或 TextReader/TextWriter 对象一起工作。XmlNodeReader 使用 XmlNode 作为其源而不是流。XmlValidatingReader 添加了 DTD 和模式验证，因此提供了数据验证。你将在本章后面更详细地了解这些内容。

### 使用 XmlReader 类

XmlReader 在 MSXML SDK 中与 SAX 很相似。然而，最大的区别之一是 SAX 是一种推送模型（即它将数据推送到应用程序，开发人员必须准备好接收它），而 XmlReader 是一种拉取模型，数据被拉入请求它的应用程序。这提供了一个更简单、更直观的编程模型。另一个优点是拉取模型可以选择发送到应用程序的数据：如果不需要所有数据，就无需处理它。在推送模型中，所有 XML 数据都必须由应用程序处理，无论是否需要。

以下是一个非常简单的读取 XML 数据的示例，稍后你将更详细地了解 XmlReader 类。你可以在 XmlReaderSample 文件夹中找到代码。以下是读取 books.xml 文档的代码。读取每个节点时，会检查 NodeType 属性。如果节点是文本节点，则将其值附加到文本框：

```csharp
using System.Xml;

private void button3_Click(object sender, EventArgs e)
{
    richTextBox1.Clear();
    XmlReader rdr = XmlReader.Create("books.xml");
    while (rdr.Read())
    {
        if (rdr.NodeType == XmlNodeType.Text)
richTextBox1.AppendText(rdr.Value + "\r\n");
}
}
```

如前所述，XmlReader 是一个抽象类。因此，为了直接使用 XmlReader 类，添加了一个 Create 静态方法。Create 方法返回一个 XmlReader 对象。Create 方法的重载列表包含九个条目。在前面的示例中，一个表示 XmlDocument 文件名的字符串作为参数传入。基于流的对象和基于 TextReader 的对象也可以传入。

也可以使用 XmlReaderSettings 对象。XmlReaderSettings 指定了读取器的功能。例如，可以使用模式来验证流。将 Schemas 属性设置为有效的 XmlSchemaSet 对象，后者是 XSD 模式的缓存。然后可以将 XmlReaderSettings 对象上的 ValidationType 属性设置为 true。

你可以使用多个 Ignore 属性来控制读取器处理某些节点和值的方式。这些属性包括 IgnoreComments、IgnoreIdentityConstraints、IgnoreInlineSchema、IgnoreProcessingInstructions、IgnoreSchemaLocation 和 IgnoreWhitespace。这些属性可用于从文档中删除某些项目。

### 读取方法

有多种方式遍历文档。如前例所示，Read() 将你带到下一个节点。然后你可以验证节点是否有值（HasValue()），或者，如你将很快看到的，节点是否有任何属性（HasAttributes()）。你也可以使用 ReadStartElement() 方法，它验证当前节点是否为起始元素，然后将你定位到下一个节点。如果不在起始元素上，将引发 XmlException。调用此方法等同于先调用 IsStartElement() 方法然后调用 Read() 方法。

ReadElementString() 与 ReadString() 类似，不同之处在于你可以选择性地传入元素的名称。如果下一个内容节点不是开始标签，或者 Name 参数与当前节点 Name 不匹配，将引发异常。

以下是 ReadElementString() 的使用示例。请注意，此示例使用 FileStreams，因此你需要确保通过 using 语句包含 System.IO 命名空间：

```csharp
private void button6_Click(object sender, EventArgs e)
{
    richTextBox1.Clear();
    XmlReader rdr = XmlReader.Create("books.xml");
    while (!rdr.EOF)
    {
        // if we hit an element type, try and load it in the listbox
        if ((rdr.MoveToContent() == XmlNodeType.Element && rdr.Name == "title"))
        {
            richTextBox1.AppendText(rdr.ReadElementString() + "\r\n");
        }
        else
        {
            //otherwise move on
            rdr.Read();
        }
    }
}
```

在 while 循环中，你使用 MoveToContent() 查找类型为 XmlNodeType.Element 且名称为 title 的每个节点。你使用 XmlTextReader 的 EOF 属性作为循环条件。如果节点不是 Element 类型或名称不是 title，else 子句将发出 Read() 方法以移动到下一个节点。当你找到符合条件的节点时，将 ReadElementString() 的结果添加到列表框中。这应该只在列表框中留下图书标题。请注意，在成功的 ReadElementString() 之后无需发出 Read() 调用，因为 ReadElementString() 会消耗整个元素并将你定位到下一个节点。

如果从 if 子句中删除 && rdr.Name=="title"，你将需要在抛出时捕获 XmlException。如果查看数据文件，你会发现 MoveToContent() 找到的第一个元素是 <bookstore> 元素。因为它是一个元素，它会通过 if 语句中的检查。然而，因为它不包含简单的文本类型，它会导致 ReadElementString() 引发 XmlException。一种解决方法是将 ReadElementString() 调用放在自己的函数中。然后，如果 ReadElementString() 调用在此函数内部失败，你可以处理错误并返回到调用函数。

继续这样做；调用这个新方法 LoadTextBox() 并将 XmlTextReader 作为参数传入。进行这些更改后，LoadTextBox() 方法如下所示：

```csharp
private void LoadTextBox(XmlReader reader)
{
    try
    {
        richTextBox1.AppendText(reader.ReadElementString() + "\r\n");
    }
    // if an XmlException is raised, ignore it.
    catch(XmlException er){}
}
```

上一个示例中的这一部分：

```
if (tr.MoveToContent() == XmlNodeType.Element && tr.Name == "title")
{
    richTextBox1.AppendText(tr.ReadElementString() + "\r\n");
}
else
{
    //otherwise move on
    tr.Read();
}
```

必须更改为以下内容：

```
if (tr.MoveToContent() == XmlNodeType.Element)
{
    LoadTextBox(tr);
}
else
{
    //otherwise move on
    tr.Read();
}
```

运行此示例后，结果应与之前相同。你看到的是有多种方法可以实现相同的目标。这就是 System.Xml 命名空间中类的灵活性开始显现的地方。

XmlReader 也可以读取强类型数据。有多个 ReadElementContentAs 方法，例如 ReadElementContentAsDouble、ReadElementContentAsBoolean 等。以下示例展示了如何将值作为十进制读取并对其进行数学运算。在这种情况下，price 元素的值增加了 25%：
