

| 类名 | 说明 |
|---|---|
| XPathDocument | 提供整个 XML 文档的视图。只读。 |
| XPathNavigator | 为 XPathDocument 提供导航功能。 |
| XPathNodeIterator | 为节点集提供迭代功能。 |
| XPathExpression | 表示已编译的 XPath 表达式。由 SelectNodes、SelectSingleNode、Evaluate 和 Matches 使用。 |
| XPathException | XPath 异常类。 |

## XPathDocument

XPathDocument 不提供 XmlDocument 类的任何功能。它的唯一用途是创建 XPathNavigator。事实上，这也是 XPathDocument 类上唯一可用的方法（除了 Object 所提供的方法之外）。

可以通过多种不同的方式创建 XPathDocument。你可以将 XmlReader、XML 文档的文件名或基于 Stream 的对象传递给构造函数。这提供了很大的灵活性。例如，你可以使用 XmlValidatingReader 验证 XML，然后使用同一个对象创建 XPathDocument。

## XPathNavigator

XPathNavigator 包含移动和选择元素所需的全部方法。下表列出了该类中定义的一些“移动”方法。

| 方法名 | 说明 |
|---|---|
| MoveTo() | 接受 XPathNavigator 作为参数。将当前位置移动到与传入的 XPathNavigator 相同的位置。 |
| MoveToAttribute() | 移动到指定的属性。接受属性名称和命名空间作为参数。 |
| MoveToFirstAttribute() | 移动到当前元素中的第一个属性。如果成功，则返回 true。 |
| MoveToNextAttribute() | 移动到当前元素中的下一个属性。如果成功，则返回 true。 |
| MoveToFirst() | 移动到当前节点中的第一个同级节点。如果成功，则返回 true。 |
| MoveToLast() | 移动到当前节点中的最后一个同级节点。如果成功，则返回 true。 |
| MoveToNext() | 移动到当前节点中的下一个同级节点。如果成功，则返回 true。 |
| MoveToPrevious() | 移动到当前节点中的上一个同级节点。如果成功，则返回 true。 |
| MoveToFirstChild() | 移动到当前元素的第一个子节点。如果成功，则返回 true。 |
| MoveToId() | 移动到具有作为参数提供的 ID 的元素。文档需要有架构，并且该元素的数据类型必须是 ID 类型。 |
| MoveToParent() | 移动到当前节点的父节点。如果成功，则返回 true。 |
| MoveToRoot() | 移动到文档的根节点。 |

若要选择文档的子集，可以使用下表列出的 Select 方法之一。

| 方法名 | 说明 |
|---|---|
| Select() | 使用 XPath 表达式选择节点集。 |
| SelectAncestors() | 基于 XPath 表达式选择当前节点的所有祖先节点。 |
| SelectChildren() | 基于 XPath 表达式选择当前节点的所有子节点。 |
| SelectDescendants() | 基于 XPath 表达式选择当前节点的所有后代节点。 |
| SelectSingleNode() | 基于 XPath 表达式选择一个节点。 |

如果 XPathNavigator 是从 XPathDocument 创建的，则它是只读的。如果是从 XmlDocument 创建的，则可以使用 XPathNavigator 编辑文档。这可以通过检查 CanEdit 属性来确认。如果该属性为 true，则可以使用某个 Insert 方法。InsertBefore 和 InsertAfter 将在当前节点之前或之后创建一个新节点。新节点的来源可以是 XmlReader 或字符串。或者，可以返回一个 XmlWriter，并使用它来编写新节点信息。

可以使用 ValueAs 属性从节点读取强类型值。请注意，这与 XmlReader 不同，XmlReader 使用 ReadValue 方法。

## XPathNodeIterator

可以将 XPathNodeIterator 视为 XPath 中 NodeList 或 NodeSet 的等价物。此对象具有两个属性和三个方法：

- Clone() — 创建自身的新副本
- Count — XPathNodeIterator 对象中的节点数
- Current — 返回指向当前节点的 XPathNavigator
- CurrentPosition() — 返回包含当前位置的整数
- MoveNext() — 移动到与创建 XPathNodeIterator 的 XPath 表达式匹配的下一个节点

XPathNodeIterator 由 XPathNavigator 的 Select 方法返回。你可以使用它来遍历 XPathNavigator 的 Select 方法返回的节点集。使用 XPathNodeIterator 的 MoveNext 方法不会更改创建它的 XPathNavigator 的位置。

## 使用 XPath 命名空间中的类

了解这些类用法的最佳方式是查看一些遍历 books.xml 文档的代码。这将使你能够了解导航的工作原理。为了使用这些示例，你首先需要添加对 System.Xml.Xsl 和 System.Xml.XPath 命名空间的引用：

using System.Xml.XPath;
using System.Xml.Xsl;

对于此示例，你使用文件 bookxpath.xml。它与你一直在使用的 books.xml 文件类似，只是额外添加了几本书。以下是表单代码，属于 XmlSample 项目的一部分：

```
private void button1_Click(object sender, EventArgs e)
{
    //modify to match your path structure
    XPathDocument doc = new XPathDocument("books.xml");
    //create the XPath navigator
    XPathNavigator nav = ((IXPathNavigable)doc).CreateNavigator();
    //create the XPathNodeIterator of book nodes
    //that have genre attribute value of novel
    XPathNodeIterator iter = nav.Select("/bookstore/book[@genre='novel']");
    textBox1.Text = "";
    while (iter.MoveNext())
    {
        XPathNodeIterator newIter =
            iter.Current.SelectDescendants(XPathNodeType.Element, false);
        while (newIter.MoveNext())
        {
            textBox1.Text += newIter.Current.Name + ": " +
                newIter.Current.Value + "\r\n";
        }
    }
}
```

在 button1_Click() 方法中，你要做的第一件事是创建 XPathDocument（名为 doc），并传入你想要打开的文档的文件和路径字符串。下一行是创建 XPathNavigator 的位置：

```
XPathNavigator nav = doc.CreateNavigator();
```

在示例中，你可以看到使用 Select() 方法检索所有将 genre 属性值设置为 novel 的节点集。然后使用 MoveNext() 方法遍历图书列表中的所有小说。

要将数据加载到列表框中，可以使用 XPathNodeIterator.Current 属性。这将基于 XPathNodeIterator 当前指向的节点创建一个新的 XPathNavigator 对象。在本例中，你正在为文档中的一个图书节点创建 XPathNavigator。

下一个循环获取此 XPathNavigator，并通过发出另一种类型的 select 方法 SelectDescendants() 来创建另一个 XPathNodeIterator。这会为你提供一个 XPathNodeIterator，其中包含图书节点的所有子节点以及子节点的子节点。

然后，你在此 XPathNodeIterator 上执行另一个 MoveNext() 循环，并将元素名称和元素值加载到文本框中。

图 33-2 显示了运行代码后的屏幕外观。请注意，现在列出的图书只有小说。

![](img/d7d2ffa0a76feaab821930e95daace93_981_0.png)

图 33-2

如果你想要累加这些图书的成本怎么办？XPathNavigator 包含 Evaluate() 方法正是出于这个原因。Evaluate() 有三个重载。第一个包含一个字符串，即 XPath 函数调用。第二个重载使用 XPathExpression 对象作为参数，第三个使用 XPathExpression 和 XPathNodeIterator 作为参数。以下代码与前面的示例类似，只不过这次遍历了文档中的所有节点。最后的 Evaluate 方法调用会累加所有图书的成本：

```
private void button2_Click(object sender, EventArgs e)
{
    //modify to match your path structure
    XPathDocument doc = new XPathDocument("books.xml");
    //create the XPath navigator
    XPathNavigator nav = ((IXPathNavigable)doc).CreateNavigator();
    //create the XPathNodeIterator of book nodes
    XPathNodeIterator iter = nav.Select("/bookstore/book");
    textBox1.Text = "";
    while (iter.MoveNext())
    {
        XPathNodeIterator newIter =
            iter.Current.SelectDescendants(XPathNodeType.Element, false);
        while (newIter.MoveNext())
        {
            textBox1.Text += newIter.Current.Name + ": " + newIter.Current.Value +
                "\r\n";
        }
    }
    textBox1.Text += "=================" + "\r\n";
    textBox1.Text += "Total Cost = " +
        nav.Evaluate("sum(/bookstore/book/price)");
}
```

