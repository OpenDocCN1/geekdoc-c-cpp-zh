
Dim `dr` As `DataRow` = `doc.GetRowFromElement(XmlElement.ParentNode, XmlElement)`

`Response.Write(dr["ContactName"].ToString() + " * is the ")`

`Response.Write(dr["ContactTitle"].ToString())`

```vb
```

```C#
string connStr = "database=Northwind;Data Source=localhost;" *
& " User id=sa;pwd=wrow"

using (SqlConnection conn = new SqlConnection(connStr))
{
    SqlCommand command = new SqlCommand("select * from customers", conn);
    conn.Open();
    DataSet ds = new DataSet();
    ds.DataSetName = "Customers";
    ds.Load(command.ExecuteReader(), LoadOption.OverwriteChanges);
    //Response.ContentType = "text/xml";
    //ds.WriteXml(Response.OutputStream);
    // 在列表 10-15 中添加
    XmlDocument doc = new XmlDocument(ds);
    doc.DataSet.EnforceConstraints = false;
    XmlNode node = doc.SelectSingleNode("//CustomerID[='ANATR']/ContactTitle");
    node.InnerText = "Boss";
    doc.DataSet.EnforceConstraints = true;
    DataRow dr = doc.GetRowFromElement(XmlElement.ParentNode);
    Response.Write(dr["ContactName"].ToString() + " * is the ");
    Response.Write(dr["ContactTitle"].ToString());
}
```

列表 10-15 在 10-14 的基础上扩展，首先注释掉了 `DataSet.WriteXml` 的 HTTP `ContentType`。在从数据库加载 `DataSet` 后，它被解析到 `XmlDocument` 构造函数中。此时，`XmlDataDocument` 和 `DataSet` 指向相同的信息。将 `EnforceConstraints` 设置为 `false` 以允许对 `DataSet` 进行更改。当随后将 `EnforceConstraints` 设置为 `true` 时，如果违反了任何约束规则，将抛出异常。使用 XPath 表达式解析 DOM 方法 `SelectSingleNode`，选择客户的 `ContactTitle`，并将其设置为 `Boss`。通过在 `XmlDataDocument` 上调用 `GetRowFromElement`，上下文从 `XmlDocument` 的世界回到了 `DataSet` 的世界。列名被传递到 `DataRow` 的索引属性中，输出如下所示：

> Ana Trujillo is the Boss

数据从 SQL 服务器加载，然后使用 `XmlDocument` 风格的策略进行处理和编辑；使用底层 `DataSet` 的 `DataRow` 构建字符串。

XML 不仅仅是标签。XML 数据可以来自文件、数据库、像 `DataSet` 对象这样的信息集，而且由于大量数据存储在 XML 格式中，因此 ASP.NET 2.0 添加了一个特定的数据源控件用于检索和处理 XML 数据。

# XmlDataSource 控件

`XmlDataSource` 控件允许你连接到 XML 数据，并与任何 ASP.NET 数据绑定控件配合使用数据。与 `SqlDataSource` 和 `AccessDataSource` 控件一样，`XmlDataSource` 不仅允许你检索数据，还可以插入、删除和更新数据项。

> `XmlDataSource` 的一个注意事项是，它的 `XPath` 属性不支持使用命名空间限定的文件。本章示例使用了 `Books.xml` 文件，其默认命名空间为 `http://examples.books.com`。XML 文件使用多个命名空间（包括默认命名空间）常见。当你用 XPath 查询它时，元素所在的命名空间非常重要。遗憾的现实是，没有办法使用命名空间 XPath 表达式或通过 `XmlNamespaceManager` 类通过前缀/命名空间对列表使用 `XmlDataSource` 控件；Template 控件中使用的函数其第二个参数接收来自 `XmlDataSource` 的查询——只要该控件不包含命名空间限定的 XPath 属性，或者你可以完全省略它。尽管如此，为了让这些示例运行，你必须从 XML 中删除命名空间，并使用不包含命名空间限定的 XPath 查询，如列表 10-16 所示。

你可以使用 `DataList` 或任何感知数据绑定的控件连接到 `<asp:XmlDataSource>` 控件。直接将控件绑定到 `Books.xml` 文件的技术将在列表 10-16 中。

## 列表 10-16：使用 DataList 控件显示 XML 内容

```xml
<%@ Language="VB" AutoEventWireups="false" %>
CodeFile="Default.aspx.vb" Inherits="Default_aspx" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
<title>XmlDataSource</title>
</head>
<body>
<form id="form1" runat="server">
<asp:DataList id="DataList1" runat="server">
<ItemTemplate>
<p><# Eval("title") %></p>
<p><# Eval("lastName") %></p>
<p><# Eval("firstName") %></p>
</ItemTemplate>
</asp:DataList>
<asp:XmlDataSource id="XmlDataSource" runat="server" DataFile="Books.xml" SelectExpression="//book" />
</form>
</body>
</html>
```
*(注：由于原文示例代码块存在明显的乱码或截断错误，翻译时已根据逻辑修正了 HTML 标签结构以保持可读性)*

## 第 10 章：使用 XML 和 LINQ to XML

```xml
<AlternatingItemTemplate>
  <tr bgcolor="LightGrey">
    <td><%# XPath("title") %></td>
    <td><br />
    <td><%# XPath("pubDate") %></td>
    <br />
    <td><%# XPath("description") %></td>
    </td>
  </tr>
</AlternatingItemTemplate>
</FooterTemplate>
</table>
</FooterTemplate>
<asp:DataList>
  <asp:XmlDataSource Id="XmlDataSource" Runat="server" DataFile="http://www.hanselman.com/blog/feed" XPath="/rss/item">
</asp:XmlDataSource>
</form>
</body>
</html>
```

查看程序清单-10 中的代码，你可以看到 `DataList` 指向一个获取 XML 的 URL。`XPath` 属性过滤并返回 RSS 馈中所有的 `<item>` 元素。`DataList` 创建了一个 HTML 表格，并从 RSS 馈中提取数据元素，例如 `<title>`、`<pubDate>` 和 `<description>` 元素。

在浏览器中运行此页面，你将得到与图 10-6 显示的结果类似的内容。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_576_0.png)

516

www.e-books.info

这种方法也适用于 XML Web 服务，甚至是那些可以使用 HTTP-GET 传递参数的服务。你只需要在下面的值中设置 `DataFile` 属性：

```xml
DataFile="http://www.myserver.com/GetWeather.asmx/zipWeather?zipcode=63301"
```

查找和使用 XML 的地方无处不在：文件、数据库、网站和服务。有时你可能通过查询或编程方式来操作 XML，有时你可能想获取 XML “树”并将其转换为另一种形式的树结构。

## XSLT

XSLT 是一种同样用 XML 语法编写的转换语言。它是声明式语言和程序化语言的奇特混合体，一些程序员会认为它根本不是一种语言。而其他使用许多 XSLT 脚本扩展的人则认为它是一种非常强大的语言。无论争议如何争议，XSLT 转换对于快速方便地更改 XML 文件的结构非常有用，并且通常使用非常声明式的语法。

熟悉 XSLT 的最佳方法是看一个示例。记住，本章使用的 `Books.xml` 文件是书籍和作者的列表。程序清单 10-18 中的 XSLT 获取了该文档，并将其转换为一个作者列表的文档。

### 程序清单 10-18：Books.xslt

```xml
<xml version="1.0" encoding="utf-8" ?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:template name="Authors">
    <xsl:apply-templates select="//book"/>
  </xsl:template>
  <xsl:template name="book">
    <xsl:element name="Author">
      <xsl:value-of select="first-name"/> <xsl:text> </xsl:text>
      <xsl:value-of select="last-name"/>
    </xsl:element>
  </xsl:template>
</xsl:stylesheet>
```

XSL 本身就是一套 XML 词汇，因此它有自己的命名空间和前缀是有意义的。XSLT 通常结构化为一组与源文档中的元素匹配的模板。XSLT 文档并不描述结果的样貌，而是声明了为了转换成功必须执行的步骤。记住，如果你的目标是创建一个包含作者列表的 XML 文件，你将匹配 `Books.xml` 的根节点，并为生成的文档输出一个名为 `<Authors>` 的根元素。然后，`<xsl:apply-templates select="//book"/>` 指示处理器应该继续寻找模板，在这种例中，匹配 XPath 表达式 `//book`。第一个模板下方是第二个模板，它处理所有书籍匹配项。它输出一个新元素 `<Author>`。

XSLT 非常关注上下文，这就像想象一个光标位于源文档的特定元素上一样，通常是有帮助的。在输出 `<author>` 元素之后，处理器正处于对 `<book>` 元素模板匹配的中间。该元素中所有的 XPath 表达式都是相对于 `book` 元素的。当 `<xsl:value-of select="author/first-name">` 指令相对于 `book` 元素搜索作者姓名时。`<xsl:text></xsl:text>` 指令值得注意，因为它是显式的，并提醒人们有意义空白和无意义空白之间存在差异。例如，在作者的姓和名之间放置空格是重要的，因此必须显式调用。

生成的文档如图 10-7 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_578_0.png)

这个示例仅触及 XSLT 力量的表面。对 XSLT 的全面探索超出了本书的范围，Wrox Press 的其他作品更全面地涵盖了该主题。记住，.NET Framework 实现了 XML 的 1.0 版本。在本文写作时，XSLT 2.0 是 W3C 标准，更多细节可以参考 XMLTeam 博客：http://blogs.msdn.com/xmlteam/archive/2007/01/29/xslt-2-0.aspx。

你可以通过多种方式应用 XSLT 转换，声明式和程序化的均有。这些将在后续章节中描述。

## XslCompiledTransform

`XslTransform` 在 .NET Framework 1.x 中用于 XSLT。在 .NET Framework 2.0 中，`XslCompiledTransform` 是新的 XSLT 处理器。`XslTransform` 已经过时并标记了 `[Obsolete]` 特性。这种编译技术还包含了来自 Visual Studio 的完整调试支持，这将在书中稍后介绍。

`XslCompiledTransform` 有两个方法：`Load` 和 `Transform`。尽管只有两个方法，但 `Transform` 有 14 个重载，`Load` 有 6 个重载。初看看起来可能令人令畏，但有一个简单的解释。

`Load` 方法可以处理来自字符串、`XmlReader` 或任何实现 `IXPathigable` 的类的样式表。可以在上述三个重载中的任何一个传递 `XslSettings` 对象，你有 6 种选择。通过 `EnableDocumentFunction` 启用 XSLT 特有函数 `document()`，或通过 `XslSettings.EnableScript` 启用嵌入的脚本块。这些高级选项出于安全考虑是被禁用的。或者，你可以通过静态属性 `XslSettings.TrustedXsl` 获取一个预填充的 `XslSettings` 对象，它已经启用了这些设置。

根据团队的数据，XSLT 在 .NET Framework 2.0 中快了 400%。在程序清单 10-19 中，`Response.Output` 属性消除了不必要的字符串分配。在示例中，`Response.Output` 被封装在 `XmlTextWriter` 中并直接传递给 `Execute` 方法。`XPathDocument` 针对 XSLT 转换进行了绝对优化，应该用它替代 `XmlDocument` 以为转换带来 15% 到 30% 的性能提升。

## 第10 章：与 XML 和 LINQ to XML 工作

```cs
string xsltFile = Server.Path("books.xslt");
string xmlFile = Server.Path("books.xml");
```

```cs
XslCompiledTransform xslt = new XslCompiledTransform();
xslt.Load(xsltFile);
```

```cs
XPathDocument doc = new XPathDocument(xmlFile);
xslt.Transform(doc, new XmlWriter(Response.Output));
```

如果样式表参数允许，可以将命名参数传递给 `XslTransform` 或 `XslCompiledTransform`。以下代码段说明了 `XslArgumentList` 的用法：

```cs
XslTransform transformer = new XslTransform();
transformer.Load("foo.xslt");
```

```cs
XslArgumentList args = new XslArgumentList();
args.Add("ID", "SOMEVALUE");
```

```cs
transformer.Transform("foo.xml", args, Response.OutputStream);
```

XSLT 生成的 XML 可以使用本章讨论过的 system.XML API 进行操纵。XSLT 的一个常见用途是将分级文档（有时是关系型文档）展平为更有于输出为 HTML 的格式。这些转换到 HTML 的结果可以内联在 ASPX 页面中。

## 新的 XSLT.exe 命令行编译器

与运行时编译的样式表相比，编译后的样式表虽然会有微小的性能损失，但非常值得；.NET Framework 3.5 引入了 `XSLT.exe`，这是一个命令行 XSLT 编译器。

用法非常简单——你可以传递任意数量的源 XSLT 文件并输出程序集。对于 Visual Studio 2008 项目，使用以下命令：

```bash
xslt /c:Wook.CompiledStylesheet books.xslt /out:Books.dll
```

现在，在列表 10-19 的项目中添加对新 `Books.dll` 的引用，并更改一行代码：

```cs
XslCompiledTransform xslt = new XslCompiledTransform();
xslt.Load(typeof(Wook.MyCompiledStylesheet));
```
