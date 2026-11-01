
```
writer.WriteElementString("title", "Case of the Missing Cookie");
writer.WriteStartElement("author");
writer.WriteElementString("name", "Cookie Monster");
writer.WriteEndElement();
writer.WriteElementString("price", "9.99");
writer.WriteEndElement();
writer.WriteEndDocument();
//clean up
writer.Flush();
writer.Close();
}
```

代码下载 XMLReaderSample.sln

在这里，你正在向名为 newbook.xml 的新 XML 文件写入数据，添加一本新书的数据。请注意，XmlWriter 会用新文件覆盖已存在的文件。你将在本章后面了解如何在现有文档中插入新的元素或节点。你是通过使用 Create 静态方法来实例化 XmlWriter 对象的。在此示例中，一个表示文件名的字符串作为参数传递，同时还传递了一个 XmlWriterSettings 类的实例。

XmlWriterSettings 类具有控制 XML 生成方式的属性。CheckedCharacters 属性是一个 Boolean 值，如果 XML 中的字符不符合 W3C XML 1.0 建议，则会引发异常。Encoding 类设置生成 XML 时使用的编码；默认值为 Encoding.UTF8。Indent 属性是一个布尔值，用于确定元素是否应缩进。IndentChars 属性设置为用于缩进的字符字符串。默认值为两个空格。NewLine 属性用于确定换行符的字符。在前面的示例中，NewLineOnAttribute 设置为 true。这会将每个属性放在单独的行中，从而使生成的 XML 更易于阅读。

WriteStartDocument() 添加文档声明。现在开始写入数据。首先是 book 元素；接下来，你添加 genre、publicationdate 和 ISBN 属性。然后写入 title、author 和 price 元素。请注意，author 元素有一个子元素 name。

当你单击按钮时，会生成 booknew.xml 文件，其内容如下：

```
<?xml version="1.0" encoding="utf-8"?>
<book
  genre="Mystery"
  publicationdate="2001"
  ISBN="123456789">
  <title>Case of the Missing Cookie</title>
  <author>
    <name>Cookie Monster</name>
  </author>
  <price>9.99</price>
</book>
```

元素的嵌套是通过注意何时开始和结束写入元素和属性来控制的。当你向 author 元素添加 name 子元素时就可以看到这一点。请注意 WriteStartElement() 和 WriteEndElement() 方法调用的排列方式，以及这种排列如何产生输出文件中的嵌套元素。

除了 WriteElementString() 和 WriteAttributeString() 方法外，还有几个专门的写入方法。WriteCDATA() 输出一个 CDATA 部分（<![CDATA[ ]]>），并写入其作为参数接收的文本。WriteComment() 以正确的 XML 格式写入注释。WriteChars() 写入 char 缓冲区的内容。这与你之前查看的 ReadChars() 方法的工作方式类似；它们都使用相同类型的参数。WriteChars() 需要一个缓冲区（字符数组）、写入的起始位置（整数）以及要写入的字符数（整数）。

使用基于 XmlReader 和 XmlWriter 的类读取和写入 XML 令人惊讶地灵活且简单。接下来，你将学习 DOM 如何通过 XmlDocument 和 XmlNode 类在 System.Xml 命名空间中实现。

## 在 .NET 中使用 DOM

.NET 中的 DOM 实现支持 W3C DOM Level 1 和 Core DOM Level 2 规范。DOM 通过 XmlNode 类实现，该类是一个抽象类，表示 XML 文档的节点。

还有一个 XmlNodeList 类，它是有序的节点列表。这是一个实时节点列表，任何节点的变化都会立即反映在列表中。XmlNodeList 支持索引访问或迭代访问。

XmlNode 和 XmlNodeList 类构成了 .NET Framework 中 DOM 实现的核心。下表列出了基于 XmlNode 的一些类。

| 类名 | 描述 |
|---|---|
| XmlLinkedNode | 返回当前节点之前或之后的节点。向 XmlNode 添加 NextSibling 和 PreviousSibling 属性。 |
| XmlDocument | 表示整个文档。实现 DOM Level 1 和 Level 2 规范。 |
| XmlDocumentFragment | 表示文档树的片段。 |
| XmlAttribute | 表示 XmlElement 对象的属性对象。 |
| XmlEntity | 表示已解析或未解析的实体节点。 |
| XmlNotation | 包含在 DTD 或模式中声明的记法。 |

下表列出了扩展 XmlCharacterData 的类。

| 类名 | 描述 |
|---|---|
| XmlCDataSection | 表示文档的 CDATA 部分。 |
| XmlComment | 表示 XML 注释对象。 |
| XmlSignificantWhitespace | 表示包含空白的节点。仅当 PreserveWhiteSpace 标志为 true 时才会创建节点。 |
| XmlWhitespace | 表示元素内容中的空白。仅当 PreserveWhiteSpace 标志为 true 时才会创建节点。 |
| XmlText | 表示元素或属性的文本内容。 |

下表列出了扩展 XmlLinkedNode 的类。

| 类名 | 描述 |
|---|---|
| XmlDeclaration | 表示声明节点（<?xml version="1.0" ?>）。 |
| XmlDocumentType | 表示与文档类型声明相关的数据。 |
| XmlElement | 表示 XML 元素对象。 |
| XmlEntityReferenceNode | 表示实体引用节点。 |
| XmlProcessingInstruction | 包含 XML 处理指令。 |

正如你所见，.NET 提供了适合你可能遇到的几乎任何 XML 类型的类。因此，你最终拥有一个非常灵活且功能强大的工具集。本节不会详细讨论每个类，但你将看到几个示例，以了解你可以完成的工作。

## 使用 XmlDocument 类

XmlDocument 及其派生类 XmlDataDocument（本章后面讨论）是你将在 .NET 中用于表示 DOM 的类。与 XmlReader 和 XmlWriter 不同，XmlDocument 提供了读写功能以及对 DOM 树的随机访问。XmlDocument 类似于 MSXML 中的 DOM 实现。如果你有使用 MSXML 编程的经验，你会感到使用 XmlDocument 很舒适。

本节介绍一个示例，该示例创建 XmlDocument 对象，从磁盘加载文档，并使用 title 元素的数据填充文本框。这与“使用 XmlReader 类”部分中构建的一个示例类似。这里的区别在于，你将选择要操作的节点，而不是像基于 XmlReader 的示例那样遍历整个文档。

以下是创建 XmlDocument 对象的代码。与 XmlReader 示例相比，请注意它看起来有多简单：

```csharp
private void button1_Click(object sender, System.EventArgs e)
{
    //doc is declared at the module level
    //change path to match your path structure
    _doc.Load("books.xml");
    //get only the nodes that we want.
    XmlNodeList nodeList = _doc.GetElementsByTagName("title");
    //iterate through the XmlNodeList
    textBox1.Text = "";
    foreach (XmlNode node in nodeList)
    {
        textBox1.Text += node.OuterXml + "\r\n";
    }
}
```

请注意，对于本节中的示例，你还需要在模块级别添加以下声明：

```csharp
private XmlDocument doc=new XmlDocument();
```

如果这就是你想要做的全部，使用 XmlReader 将是加载文本框的更有效方法，因为你只需遍历一次文档，然后就完成了。这正是 XmlReader 设计用于的工作类型。然而，如果你想重新访问某个节点，使用 XmlDocument 是更好的方法。

以下是使用 XPath 语法从文档中检索一组节点的示例：

```csharp
private void button2_Click(object sender, EventArgs e)
{
    //doc is declared at the module level
    //change path to match your path structure
    doc.Load("books.xml");
    //get only the nodes that we want.
    XmlNodeList nodeList = _doc.SelectNodes("/bookstore/book/title");
    textBox1.Text = "";
    //iterate through the XmlNodeList
    foreach (XmlNode node in nodeList)
    {
        textBox1.Text += node.OuterXml + "\r\n";
    }
}
```
