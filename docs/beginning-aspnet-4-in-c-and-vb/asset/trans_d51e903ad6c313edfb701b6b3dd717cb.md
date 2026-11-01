
SelectNodes() 返回一个 NodeList，或 XmlNodes 的集合。该列表仅包含作为参数 SelectNodes 传入的 XPath 语句匹配的节点。在本例中，你只想看到 title 节点。如果你调用了 SelectSingleNode，那么你将收到一个单个节点对象，其中包含与 XPath 条件匹配的 XmlDocument 中的第一个节点。

关于 SelectSingleNode() 方法的简要说明：这是 XmlDocument 类中的 XPath 实现。SelectSingleNode() 和 SelectNodes() 方法都定义在 XmlNode 中，而 XmlDocument 基于 XmlNode。SelectSingleNode() 返回一个 XmlNode，而 SelectNodes() 返回一个 XmlNodeList。然而，System.Xml.XPath 命名空间包含更丰富的 XPath 实现，你将在后面的章节中查看。

## 插入节点

之前，你看过一个使用 XmlTextWriter 创建新文档的示例。其局限性在于它无法向当前文档插入节点。使用 XmlDocument 类，你就可以做到这一点。将上一个示例中的 button1_Click() 事件处理程序改为如下所示：

```
private void button4_Click(object sender, System.EventArgs e)
{
    //change path to match your structure
    _doc.Load("books.xml");
    //create a new 'book' element
    XmlElement newBook = _doc.CreateElement("book");
    //set some attributes
    newBook.SetAttribute("genre", "Mystery");
    newBook.SetAttribute("publicationDate", "2001");
    newBook.SetAttribute("ISBN", "123456789");
    //create a new 'title' element
    XmlElement newTitle = _doc.CreateElement("title");
    newTitle.InnerText = "Case of the Missing Cookie";
    newBook.AppendChild(newTitle);
    //create new author element
    XmlElement newAuthor = _doc.CreateElement("author");
    newBook.AppendChild(newAuthor);
    //create new name element
    XmlElement newName = _doc.CreateElement("name");
    newName.InnerText = "Cookie Monster";
    newAuthor.AppendChild(newName);
    //create new price element
    XmlElement newPrice = _doc.CreateElement("price");
    newPrice.InnerText = "9.95";
    newBook.AppendChild(newPrice);
    //add to the current document
    _doc.DocumentElement.AppendChild(newBook);
    //write out the doc to disk
    XmlTextWriter tr = new XmlTextWriter("booksEdit.xml", null);
    tr.Formatting = Formatting.Indented;
    _doc.WriteContentTo(tr);
    tr.Close();
    //load listBox1 with all of the titles, including new one
    XmlNodeList nodeList = _doc.GetElementsByTagName("title");
    textBox1.Text = "*";
    foreach (XmlNode node in nodeList)
    {
        textBox1.Text += node.OuterXml + "\r\n";
    }
}
```

执行此代码后，你将获得与上一个示例相同的功能，但文本框中多了一本书《The Case of the Missing Cookie》（一部即将成为经典的作品）。仔细查看代码，你会发现这实际上是一个相当简单的过程。首先要做的是创建一个新的 book 元素：

```
XmlElement newBook = doc.CreateElement("book");
```

CreateElement() 有三个重载，允许你指定以下内容：

-   元素名称
-   名称和命名空间 URI
-   前缀、本地名称和命名空间

元素创建后，你需要添加属性：

```
newBook.SetAttribute("genre", "Mystery");
newBook.SetAttribute("publicationdate", "2001");
newBook.SetAttribute("ISBN", "123456789");
```

创建属性后，你需要添加书的其他元素：

```
XmlElement newTitle = doc.CreateElement("title");
newTitle.InnerText = "The Case of the Missing Cookie";
newBook.AppendChild(newTitle);
```

再次，你创建一个基于 XmlElement 的新对象（newTitle）。然后将 InnerText 属性设置为我们新经典作品的标题，并将该元素作为子元素追加到 book 元素。你对该 book 元素中的其余元素重复此操作。请注意，你将 name 元素作为 author 元素的子元素添加。这将给出适当的嵌套关系，如其他 book 元素中所示。

最后，你将 newBook 元素追加到 doc.DocumentElement 节点。这与所有其他 book 元素处于同一级别。你现在拥有了一个已更新的现有文档，其中包含一个新元素。

要做的最后一件事是将新的 XML 文档写入磁盘。在本例中，你创建一个新的 XmlTextWriter 并将其传递给 WriteContentTo() 方法。WriteContentTo() 和 WriteTo() 都接受 XmlTextWriter 作为参数。WriteContentTo() 将当前节点及其所有子节点保存到 XmlTextWriter，而 WriteTo() 仅保存当前节点。由于 doc 是基于 XmlDocument 的对象，它代表整个文档，因此保存的就是它。你也可以使用 Save() 方法。它总是保存整个文档。

Save() 有四个重载。你可以指定包含文件名和路径的字符串、基于 Stream 的对象、基于 TextWriter 的对象或基于 XmlWriter 的对象。

你还需要在 XmlTextWriter 上调用 Close() 方法以刷新内部缓冲区并关闭文件。

![](img/d7d2ffa0a76feaab821930e95daace93_977_0.png)

图 33-1 显示了运行此示例时得到的结果。请注意列表底部的条目。

## 图 33-1

本章前面，你看到了如何使用 XmlTextWriter 类创建文档。你也可以使用 XmlDocument。为什么要在两者之间选择其一？如果要流式传输到 XML 的数据可用且准备好写入，那么 XmlTextWriter 类是最佳选择。但是，如果你需要一点一点地构建 XML 文档，将节点插入到各个位置，那么使用 XmlDocument 创建文档可能更合适。你可以通过更改以下行来实现：

```
doc.Load("books.xml");
```

改为如下：

```
//create the declaration section
XmlDeclaration newDec = doc.CreateXmlDeclaration("1.0",null,null);
doc.AppendChild(newDec);
//create the new root element
XmlElement newRoot = doc.CreateElement("newBookstore");
doc.AppendChild(newRoot);
```

首先，你创建一个新的 XmlDeclaration。参数为版本（目前始终为 1.0）、编码和 standalone 标志。如果未使用 null，则编码参数应设置为 System.Text.Encoding 类的一部分的字符串（null 默认使用 UTF-8）。standalone 标志可以是 yes、no 或 null。如果为 null，则该属性不使用且不会包含在文档中。

接下来创建的元素将成为 DocumentElement。在本例中，它称为 newBookstore，以便你可以看到区别。其余代码与上一个示例相同，工作方式也相同。

这是 booksEdit.xml，它由以下代码生成：

```
<?xml version="1.0"?>
<newBookstore>
  <book genre="Mystery" publicationDate="2001" ISBN="123456789">
    <title>The Case of the Missing Cookie</title>
    <author>
      <name>C. Monster</name>
    </author>
    <price>9.95</price>
  </book>
</newBookstore>
```

当你想要随机访问文档时，你会想要使用 XmlDocument 类，或者当你想要流式模型时，使用基于 XmlReader 的类。请记住，基于 XmlNode 的 XmlDocument 类的灵活性是有代价的——内存需求更高，使用 XmlReader 读取文档的性能也不如使用 XmlReader。遍历 XML 文档还有另一种方法：XPathNavigator。

## 使用 XPathNavigator

XPathNavigator 用于从 XML 文档中选择、迭代，有时编辑数据。XPathNavigator 可以从 XmlDocument 创建以允许编辑功能，或从 XPathDocument 创建以供只读使用。由于 XPathDocument 是只读的，因此性能非常好。

与 XmlReader 不同，XPathNavigator 不是流式模型，因此可以使用同一文档而无需重新读取和解析。

XPathNavigator 是 System.Xml.XPath 命名空间的一部分。XPath 是一种查询语言，用于从 XML 文档中选择特定节点或元素进行处理。

### System.Xml.XPath 命名空间

System.Xml.XPath 命名空间为速度而构建。它提供 XML 文档的只读视图，因此没有编辑功能。该命名空间中的类旨在对 XML 文档进行快速迭代和选择。

下表列出了 System.Xml.XPath 中的关键类，并简要描述了每个类的用途。
