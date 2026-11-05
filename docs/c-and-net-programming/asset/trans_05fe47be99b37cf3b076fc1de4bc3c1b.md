
要仅获取男性姓名（选择具有特定 XML 属性的所有节点）请使用 XPath 表达式 /Names/Name[@type='M']。

代码 -

```
XmlDocument xml = new XmlDocument();
xml.LoadXml(str); // suppose that str string contains "<Names>...</Names>"

XmlNodeList xnList = xml.SelectNodes("/Names/Name[@type='M']");
foreach (XmlNode xn in xnList)
{
    Console.WriteLine(xn.InnerText);
}
```

## 输出

Ravindra
Prakash

- 使用 XPath 选择顶部的 XML 节点

要从 XML 中选择节点，请使用方法 XmlNode.SelectNodes。将 XPath 表达式作为参数传递，方法将返回所选节点列表。

请考虑下面的 XML 文件，

```
[XML]
<Names>
    <Name>Ravi</Name>
    <Name>Shyam</Name>
    <Name>Avi</Name>
    <Name>Lucky</Name>
    <Name>Sandy</Name>
    <Name>Sam</Name>
    <Name>Niru</Name>
</Names>
```

要获取所有 <Name> 节点，请使用 XPath 表达式 /Names/Name。

如果不是选择所有节点，而只是前 5 个节点，请使用 XPath 表达式，/Names/Name[position() <= 5]。

## 示例

```
XmlDocument xml = new XmlDocument();
xml.LoadXml(str); // suppose that str string contains "<Names>...</Names>"

XmlNodeList xnList = xml.SelectNodes("/Names/Name[position() <= 5]");
foreach (XmlNode xn in xnList)
{
    Console.WriteLine(xn.InnerText);
}
```

| 输出 |
|---|
| Ravi |
| Shyam |
| Avi |
| Lucky |
| Sandy |

## 17.8 使用 XML 和 ADO.NET 处理数据

处理 XML 和 ADO 有两种方法，即，一是使用 ADO.NET 访问 XML 文档，二是使用 XML 和 ADO.NET 访问 XML。此外，关系数据库也可以使用 ADO.NET 和 XML.NET 访问。

- 使用 DataSet 读取 XML

DataSet 类可用于访问数据。该类实现了用于处理 XML 文档的方法和属性。

### ReadXml 方法

ReadXml 是一个重载方法；用于读取数据流、TextReader、XmlReader 或 XML 文件并存储到 DataSet 对象中，后者稍后可用于以表格格式显示数据。ReadXml 方法有八种不同的重载形式。它可以读取文本、string、stream、TextReader、XmlReader 及其组合格式。在使用 DataSet 和其他通用数据组件之前，请记住添加对 System.Data 和 System.Data.Common 命名空间的引用。

### 示例

```
```csharp
//1. Create a DataSet object
DataSet ds = new DataSet();
// 2. Fill with the data with file
ds.ReadXml("media.xml");
```
```

### ReadXmlSchema 方法

ReadXmlSchema 方法在 DataSet 对象中读取 XML 架构（具有四种重载形式），可使用 Text Reader、string、stream 和 XmlReader

### 示例

```
```csharp
//illustrates how to use a file as direct input and call the ReadXmlSchema method to read the file
DataSet ds = new DataSet();
ds.ReadXmlSchema(@"c:\media.xml");
```
```

### 示例

```
//illustration of reading the file XmlReader and use XmlTextReader as the input of
/ReadXmlSchema

//Create a dataset object
DataSet ds = new DataSet("New DataSet");
// Read xml in an XmlTextReader
XmlTextReader myXmlReader = new XmlTextReader(@"c:\media.Xml");
// Call ReadXmlSchema
ds.ReadXmlSchema(myXmlReader);
myXmlReader.Close();
```

- 使用 DataSet 写入 XML

DataSet 类包含从 DataSet 对象写入 XML 文件并将数据填充到文件中的方法。

### WriteXml 方法

WriteXml 方法将 DataSet 对象的当前数据（架构和数据）写入 XML 文件。这是一个重载方法。通过使用此方法，可以将数据写入文件、流、TextWriter 或 XmlWriter。

### 示例

```
//illustration writing the data to an XML file using DataSet
using System;
using System.IO;
using System.Xml;
using System.Data;
namespace XmlandADO
{
    class XmlAndDataSetDemo
    {
    public static void Main()
    {
    try
    {
    // Create a DataSet, namespace and Media table
    // with Name and Type columns
    DataSet ds = new DataSet("DS");
    ds.Namespace = "StdNamespace";
    DataTable mdTable = new DataTable("Media");
    DataColumn col1 = new DataColumn("Name");
    DataColumn col2 = new DataColumn("Type");
    mdTable.Columns.Add(col1);
    mdTable.Columns.Add(col2);
    ds.Tables.Add(mdTable);
    //Add media Data to the table
```

```
```csharp
DataRow newRow; newRow = mdTable.NewRow();
newRow["Name"] = "C# Guide";
newRow["Type"] = "Book";
mdTable.Rows.Add(newRow);
newRow = mdTable.NewRow();
newRow["Name"] = "XML";
newRow["Type"] = "CD";
mdTable.Rows.Add(newRow);
newRow = mdTable.NewRow();
    ds.AcceptChanges();
// Create a new StreamWriter
    System.IO.StreamWriter mdStreamWriter = new
    System.IO.StreamWriter(@"c:\media\Data.xml");

// Write data to DataSet which actually creates the file
ds.WriteXml(mdStreamWriter);
mdStreamWriter.Close();
}
catch (Exception e)
{
    Console.WriteLine("Exception: {0}", e.ToString());
}
return;
}
}
}
```
```

### 上述代码片段的输出

```
```xml
<?xml version="1.0" ?>
<DS xmlns="StdNamespace">
  <Media>
    <Name>C# Guide</Name>
    <Type>Book</Type>
  </Media>
  <Media>
    <Name>XML</Name>
    <Type>CD</Type>
  </Media>
</DS>
```
```

## 17.9 使用 SAX 和 DOM 操作 XML

- XML 解析器是一种软件库或包，为客户端应用程序提供与 XML 文档交互的接口。XML 解析器旨在读取 XML 并为程序使用 XML 创建一种方式。XML 解析器验证文档并检查文档是否格式良好。**XML 解析器可以分为两种主要类型 DOM 解析器或 SAX 解析器。**

### 17.9.1 DOM 方法

- DOM 文档是一个对象，其中包含 XML 文档的所有信息。它像树结构一样组成。DOM 解析器实现 DOM API。此 API 非常简单易用。

### 17.9.1.1 DOM 解析器的特性

- DOM 解析器在内存中创建一个内部结构，即 DOM 文档对象，客户端应用程序通过在此文档对象上调用方法来获取原始 XML 文档的信息。
- DOM 解析器具有基于树的结构。

### 优点

- 1) 它支持读写操作，并且 API 非常简单易用。
- 2) 当需要随机访问文档中 widely separated 的部分时首选。

### 缺点

- 1) 它内存效率低下。（消耗更多内存，因为整个 XML 文档需要加载到内存中）。
- 2) 与其他解析器相比速度较慢。

操作 XML 文档的内容包括遍历文档中的节点列表、设置和查询属性值，以及通过创建和插入新节点来操作树本身。本节讨论使用 Document Object Model（DOM）操作 XML 文档，该模型由 System.Xml 命名空间中的 XmlDocument 类建模。DOM 是递归的，这意味着每个节点都具有与文档中每个其他节点相同的属性和方法。

### 17.9.1.2 重要的基本 XML 相关概念

- 1. **XSL** - Extensible Stylesheet Language，旨在为 XML 文档表达样式表。XSL 之于 XML 如 CSS 之于 HTML。
- 2. **XML Transformation** - 是用户定义的算法，将给定的 XML 文档转换为另一种格式，例如 XML、HTML、XHTML。算法由 XSL 描述。

3. **XSLT** - 旨在作为 XSL 的一部分使用，将 XML 文档转换为另一个 XML 文档，或浏览器识别的另一种类型文档，如 HTML 或 XHTML。XSLT 使用 XPath。

4. **XPath** - 是定义 XML 文档部分的一组语法规则。

### 17.9.1.3 XMLNode 类

XMLNode 类用于在 DOM 中操作节点。XML 节点是 DOM 模型文档中最基本的抽象单元。

### 常用 XmlNode 属性

- Attributes - 节点的属性 (XmlAttributeCollection)。
- ChildNodes - 当前节点的子节点列表 (XmlNodeList)。
- FirstChild - 返回 XML 节点的第一个子节点（第一个为文档顺序中的第一个）。
- HasChildNodes - 一个布尔值，指示节点是否有子节点。
- InnerText - 获取或设置节点内部的文本。
- InnerXml - 获取或设置节点内的 XML。
- LastChild - 返回节点的最后一个子节点（相对于文档顺序）。
- Name - 节点的名称。
- NodeType - 指示节点的类型。这可以是多种类型，包括但不限于：Document、DocumentFragment、Element、EndElement、Entity、Notation、Text、Whitespace 或 XmlDeclaration。
- OuterXml - 表示当前节点及其所有子节点的 XML。
- OwnerDocument - 当前节点所属的文档。
- ParentNode - 当前节点的父节点（如果有）。
- PreviousSibling - 获取文档顺序中紧邻当前节点之前的节点。
- Value - 获取或设置当前节点的值。

### 常用 XmlNode 方法

- AppendChild - 将子节点添加到当前子节点列表的末尾。
- Clone - 创建节点的副本。
- CreateNavigator - 为此节点创建 XPathNavigator。
- InsertAfter - 将给定节点插入当前节点之后。
- InsertBefore - 将给定节点插入当前节点之前。
- PrependChild - 在子节点列表开头添加给定的子节点。
