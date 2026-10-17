
名为 `XmlDataDocument` 的类派生自 `XmlDocument` 类。`XmlDataDocument` 类是专门为处理与 `DataSet` 对象关联的数据而构建的。`XmlDataDocument` 类有一个重载构造函数，该构造函数接受一个 `DataSet` 类型的参数。当你通过向构造函数传递 `DataSet` 类型的参数来创建 `XmlDataDocument` 类的对象时，会根据 `DataSet` 对象创建一个 XML 文档。如果你在创建 `XmlDataDocument` 类的对象时未向构造函数传递任何参数，则该对象包含一个名为 `NewDataSet` 的 `DataSet`，其 `Tables` 集合中没有任何 `DataTable`。

表 30.5 列出了从 `XmlCharacterData` 抽象类（见表 30.4）派生的类：

| 表 30.5：从 XmlCharacterData 类派生的类 |
| 类名 | 描述 |
| `XmlCDataSection` | 表示 XML 文档的字符数据（CDATA）部分。 |
| `XmlComment` | 表示一个 XML 注释对象。 |
| `XmlSignificantWhitespace` | 表示带有空白的节点。在 `XmlSignificantWhitespace` 类中，仅当 `PreserveWhiteSpace` 标志为 true 时才会创建该节点。 |
| `XmlWhitespace` | 表示元素内容中的空白。在 `XmlWhitespace` 类中，仅当 `PreserveWhiteSpace` 标志为 true 时才会创建该节点。 |
| `XmlText` | 表示元素或属性的文本内容。 |

让我们来学习 .NET 中的 XPath 和 XSLT。

## .NET Framework 4.0 中的 XPath 和 XSLT

XPath 是一种 XML 路径语言，提供了一种灵活的方式来寻址（指向）XML 文档的不同部分。此外，它还可用于测试文档中已寻址的节点，以确定它们是否匹配某种模式。要在 .NET Framework 中使用 XPath，可以使用 `System.Xml.XPath` 命名空间，其中包含用于根据元素文本值或属性值选择元素子集的类。

XSLT 代表可扩展样式表语言转换（EXtensible Stylesheet Language Transformation），用于将 XML 文档转换为其他格式，例如可扩展超文本标记语言（XHTML）。要在 .NET Framework 中使用 XSLT，可以使用 `System.Xml.Xsl` 命名空间，其中包含用于将基础文档转换为不同结构或类型文档的类。

### System.Xml.XPath 命名空间

XPath 用于根据给定条件检索元素的子集。在 .NET 中，导入 `System.Xml.XPath` 命名空间即可使用 XPath，这有助于快速处理 XML 文档。`System.Xml.XPath` 命名空间提供 XML 文档的只读视图。此命名空间中的类用于以游标方式对 XML 文档执行快速迭代和选择。

| 表 30.6：System.Xml.XPath 命名空间中的类 |
| 类名 | 描述 |
| `XPathDocument` | 提供整个 XML 文档的只读视图 |
| `XPathNavigator` | 提供对 `XmlDataDocument` 对象的导航功能 |
| `XPathNodeIterator` | 提供对节点集的迭代功能 |
| `XPathExpression` | 表示已编译的 XPath 表达式 |
| `XPathException` | 表示 XPath 异常类 |

现在，我们讨论表 30.6 中列出的 `System.Xml.XPath` 命名空间的重要类。

### XPathDocument 类

可以使用 `XPathDocument` 类来加快 XML 文档的处理速度。`XPathDocument` 类具有重载构造函数，这些构造函数接受 XML 文档的文件名、`TextReader` 对象、`XmlReader` 对象或基于 `Stream` 的对象作为参数。`XPathDocument` 类的使用非常简单，因为它只有一个名为 `CreateNavigator()` 的 XML 相关方法，可用于创建 `XPathNavigator` 类的实例。

### XPathNavigator 类

`XPathNavigator` 类包含用于从 XML 文档移动和选择元素的方法。

| 表 30.7：XPathNavigator 类的常用方法 |
| 方法名 | 描述 |
| `MoveTo()` | 接受一个参数，该参数是 `XPathNavigator` 类的对象。它用于将当前游标位置移动到传入 `XPathNavigator` 对象中的新位置。 |
| `MoveToAttribute()` | 移动到指定的属性。它将属性名称和命名空间作为参数。 |
| `MoveToFirstAttribute()` | 移动到当前元素中的第一个属性。如果执行成功，则返回 true。 |
| `MoveToNextAttribute()` | 移动到当前元素中的下一个属性。如果执行成功，则返回 true。 |
| `MoveToFirst()` | 移动到当前节点中的第一个同级节点。如果执行成功，则返回 true；否则返回 false。 |
| `MoveToLast()` | 移动到当前节点中的最后一个同级节点。如果执行成功，则返回 true。 |
| `MoveToNext()` | 移动到当前节点中的下一个同级节点。如果执行成功，则返回 true。 |
| `MoveToPrevious()` | 移动到当前节点中的上一个同级节点。如果执行成功，则返回 true。 |
| `MoveToFirstChild()` | 移动到当前元素的子节点。如果执行成功，则返回 true。 |
| `MoveToId()` | 移动到具有作为参数提供的 ID 的元素。对于此方法，您应该为文档提供架构，并且元素的数据类型必须是 Id 类型。 |
| `MoveToParent()` | 移动到当前节点的父节点。如果执行成功，则返回 true。 |
| `MoveToRoot()` | 移动到文档的根节点。 |

除了表 30.7 中列出的方法之外，`XPathNavigator` 类还有一些用于从 XML 文档中选择元素的方法。这些方法是 `Select()`、`SelectAncestors()` 和 `SelectChildren()`；所有这些方法都返回一个 `XPathNodeIterator` 对象。`Select()` 方法接受一个 XPath 表达式作为参数，而另外两个方法接受 `XPathNodeType` 对象作为参数。

### XPathNodeIterator 类

`XPathNodeIterator` 类对选定的节点集提供迭代器。此类定义的属性如下：

- `Count` — 表示 `XPathNodeIterator` 对象中的节点总数
- `Current` — 表示指向当前节点的 `XPathNavigator` 对象
- `CurrentPosition` — 以整数的形式表示节点的当前位置

以下是 `XPathNodeIterator` 类定义的方法：

- `Clone()` — 创建 `XPathNodeIterator` 对象的新副本
- `MoveNext()` — 移动到与创建 `XPathNodeIterator` 对象的 XPath 表达式匹配的下一个节点

### XPathExpression 类

`XPathExpression` 类封装了已编译的 XPath 查询表达式，其中包含符合 W3C XPath 查询语言规范的语法。因此，您必须在执行代码的查询表达式之前编译 XPath 查询表达式。在调用 `XPathNavigator` 类的 `Select()` 方法时，可以使用 `XPathExpression` 类提供预编译的 XPath 查询表达式。您还可以调用 `XPathNavigator` 类的 `Compile()` 方法来返回 `XPathExpression` 类的对象。

### XPathException 类

`XPathException` 是一个异常类，当在执行 XPath 查询表达式期间发生错误时，会生成异常。`XPathNavigator` 类的 `Select()` 和 `Compile()` 方法可能引发 `XPathException` 异常。

### System.Xml.Xsl 命名空间

`System.Xml.Xsl` 命名空间中包含的类用于在 .NET Framework 中执行 XSL 转换。此命名空间的内容可供实现 `IXPathNavigable` 接口的类使用。在 .NET Framework 中，`XmlDocument`、`XmlDataDocument` 和 `XPathDocument` 类实现了 `IXPathNavigable` 接口。如果要使用一组类创建自定义存储，则需要在类中实现 `IXPathNavigable` 接口。例如，某个类使用文件系统并执行 XSLT 转换。XSLT 使用流式拉取模型将数据拉入应用程序。因此，您可以一起执行多个转换。如果需要，可以在转换之间应用自定义读取器。

## 将 XML 与 ADO.NET 一起使用

XML 是在数据存储和应用程序之间交换数据的媒介。ADO.NET 主要设计用于在 XML 环境中工作。它提供了一些强大的功能，用于读取和写入 XML 文档。`System.Xml` 命名空间中包含的一些类（如 `XmlDataDocument`）也用于处理 ADO.NET 关系数据。

您可以通过首先使用来自 ADO.NET 数据源的数据填充 `DataSet` 对象，然后调用 `DataSet` 对象的 `WriteXml()` 方法来创建包含 ADO.NET 数据源数据的 XML 文件。`WriteXml()` 方法有两种重载形式，一种接受带有文件路径和名称的字符串，另一种接受一个附加参数来指定模式，该模式从 `XmlWriteMode` 枚举中取值。`XmlWriteMode` 枚举具有三个值，如下所示：

- `IgnoreSchema` – 忽略或不提供 XML 文件开头的内联架构。
- `WriteSchema` – 在 XML 文件开头提供内联架构。
- `DiffGram` – 指定包含与编辑前和编辑后会话相关的数据的 XML 文档。`DiffGram` 可能包括对数据所做的任何类型的更改，例如添加和删除某些数据元素。`DiffGram` 对于提交/回滚过程的审计跟踪非常有用。如今，`DiffGram` 已成为大多数数据库管理系统（DBMS）的一项内置功能。

## 使用 XML 进行对象序列化

将对象的数据保存到存储介质中称为对象序列化。在对象序列化中，对象的公共属性和字段会转换为 XML 元素或属性，或两者兼有。您可以序列化的数据可以是原始类型、字段、数组，或 `XmlElement` 和 `XmlAttribute` 对象形式的嵌入式 XML。

在 .NET Framework 中，您可以借助 `System.Xml.Serialization` 命名空间中的 `XmlSerializer` 类来序列化对象。为此，您首先通过指定要序列化的对象类型来创建 `XmlSerializer` 类的对象。接下来，创建一个流/写入器对象，以将文件写入一个流/文档。最后，您通过传递两个参数来调用 `XmlSerializer` 类的 `Serialize()` 方法。其中一个参数是流/写入器对象，另一个是您想要序列化的对象。

此外，您还可以使用应用程序的另一部分或单独一个应用程序来反序列化对象。反序列化后，对象将恢复到序列化之前的状态。要反序列化对象，您首先创建两个对象——一个 `XmlSerializer` 对象和一个流/读取器对象。之后，您通过传递流/读取器对象作为参数来调用 `XmlSerializer` 类的 `Deserialize()` 方法。`Deserialize()` 方法返回一个反序列化对象，该对象需要转换为正确的类型。

您想要序列化的对象和 XML 文档借助自定义的 C# 特性建立联系。C# 特性是一种声明性信息，可在运行时由公共语言运行时 (`CLR`) 检索。此外，它描述了对象应如何被序列化。可以使用名为 `xsd.exe` 的工具来创建它，该工具包含在 .NET Framework 4.0 中。`xsd.exe` 的特性如下：

- 从 XML 文件生成 XML 架构
- 从外部数据表示 (XDR) 架构文件生成 XML 架构
- 从 XSD 架构文件生成 `DataSet` 对象
- 从您已开发的类生成 XSD 文件
- 从运行时程序集文件中定义的类型生成架构
- 生成包含用于 XmlSerialization 的自定义特性的运行时类

## 即时解决方案

### 使用流式 XML

在本节中，您将学习如何读取、验证和写入 XML 文档中的数据。我们先创建一个 XML 文件 `authors.xml`（也可在 CD 上找到）。请注意，`authors.xml` 文件在后续的其他应用程序中也会用到。清单 30.1 显示了 `authors.xml` 文件的代码：

#### 清单 30.1：展示 authors.xml 文件的代码

```
<?xml version="1.0"?>
<authorslist>
  <authors au_id="409-56-7008">
    <au_lname>Tom</au_lname>
    <au_fname>Abraham</au_fname>
  </authors>
  <authors au_id="648-92-1872">
    <au_lname>Blotchet-Halls</au_lname>
    <au_fname>Reginald</au_fname>
  </authors>
  <authors au_id="238-95-7766">
    <au_lname>Carson</au_lname>
    <au_fname>Cheryl</au_fname>
  </authors>
  <authors au_id="722-51-5454">
    <au_lname>DeFrance</au_lname>
    <au_fname>Michel</au_fname>
  </authors>
  <authors au_id="427-17-2319">
    <au_lname>Dull</au_lname>
    <au_fname>Ann</au_fname>
  </authors>
  <authors au_id="213-46-8915">
    <au_lname>Green</au_lname>
    <au_fname>Marjorie</au_fname>
  </authors>
  <authors au_id="527-72-3246">
    <au_lname>Greene</au_lname>
    <au_fname>Morningstar</au_fname>
  </authors>
  <authors au_id="472-27-2349">
    <au_lname>Gringlesby</au_lname>
    <au_fname>Burt</au_fname>
  </authors>
  <authors au_id="846-92-7186">
    <au_lname>Hunter</au_lname>
    <au_fname>Sheryl</au_fname>
  </authors>
  <authors au_id="756-30-7391">
    <au_lname>Karsen</au_lname>
    <au_fname>Livia</au_fname>
  </authors>
</authorslist>
```

让我们从 XML 文件中读取数据开始。

### 读取数据

您可以从 XML 文件中读取所有元素数据和属性值。此外，您还可以通过指定元素名称来读取单个元素的数据。让我们创建一个名为 `ReadingXMLData` 的应用程序（也可在 CD 上找到）来读取 XML 数据。

执行以下步骤来创建 `ReadingXMLData` 应用程序：

- 1. 创建一个名为 `ReadingXMLData` 的 Windows 窗体应用程序。
- 2. 将 `authors.xml` 文件添加到 `ReadingXMLData` 应用程序的 `bin\Debug` 文件夹中。
- 3. 在 `Form1.cs` 文件中添加以下命名空间：

  `using System.Xml;`
- 4. 从工具箱中向 `Form1` 添加一个列表框和三个按钮控件。
- 5. 将按钮的 `Text` 属性分别设置为“显示所有元素”“显示姓氏”和“显示所有属性”。
- 6. 双击“显示所有元素”按钮，并添加以下代码片段：

```
private void button1_Click(object sender, EventArgs e)
{
    listBox1.Items.Clear();
    XmlReader xr = XmlReader.Create("authors.xml");
    while (xr.Read())
    {
        if (xr.NodeType == XmlNodeType.Text)
            listBox1.Items.Add(xr.Value);
    }
}
```

在上述代码片段中，我们创建了一个空白的列表框，并通过调用 `XmlReader` 类的 `Create()` 方法并向其传递 XML 文件（`authors.xml`）的名称作为参数，创建了一个 `XmlReader` 对象。然后，我们在 while 循环中使用 `XmlReader` 对象的 `Read()` 方法遍历了 XML 文档的节点。在循环内部，我们将每个节点的 `NodeType` 与 `XmlNodeType` 枚举中的值进行比较。如果它是一个文本节点，我们就把文本值添加到列表框中。

- 7. 双击“显示姓氏”按钮，并添加以下代码片段：
