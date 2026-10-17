
```csharp
XmlDocument document = new XmlDocument();

XmlElement booksElement = document.CreateElement("books");
XmlElement bookElement = document.CreateElement("book");
XmlElement titleElement = document.CreateElement("title");
titleElement.InnerText = "Sams Teach Yourself Visual C# 2010 in 24 Hours";
XmlElement isbn10Element = document.CreateElement("isbn-10");
isbn10Element.InnerText = "0-672-33101-2";
XmlElement authorElement = document.CreateElement("author");
authorElement.InnerText = "Dorman";
XmlElement priceElement = document.CreateElement("price");
priceElement.InnerText = "39.99";
XmlAttribute currencyAttribute = document.CreateAttribute("currency");
currencyAttribute.Value = "US";
priceElement.Attributes.Append(currencyAttribute);

XmlElement publisherElement = document.CreateElement("publisher");
XmlElement publisherNameElement = document.CreateElement("name");
publisherNameElement.InnerText = "Sams Publishing";
XmlElement publisherStateElement = document.CreateElement("state");
publisherStateElement.InnerText = "IN";

booksElement.AppendChild(bookElement);
bookElement.AppendChild(titleElement);
bookElement.AppendChild(isbn10Element);
bookElement.AppendChild(authorElement);
bookElement.AppendChild(priceElement);
bookElement.AppendChild(publisherElement);

publisherElement.AppendChild(publisherNameElement);
publisherElement.AppendChild(publisherStateElement);

document.AppendChild(booksElement);
```

可以看到，列表 14.3 中的代码长度几乎是列表 14.2 的三倍，并且更难阅读和理解。此外，如果你查看列表 14.2 中 `price` 元素的声明，你可以直接将值设置为十进制数，而在列表 14.3 中的相同代码必须将值设置为字符串。这种差异在检索值时变得非常重要。`XElement` 和 `XAttribute` 类都允许你通过使用到所需类型的直接转换来读取其内容。如果直接转换指定的转换失败，它将抛出 `FormatException`。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_335_0.png)

## SetElementValue 和 SetAttributeValue

使用列表 14.2 中显示的构造函数语法并不是创建 XML 的唯一方法。你也可以使用 `XElement` 类提供的 `SetElementValue` 和 `SetAttributeValue` 方法。

这些方法使得维护名称-值对列表作为子元素或属性集合变得容易，允许你添加、修改或删除这些对。如果提供的名称尚未作为子元素或属性存在，它将为你创建；否则，其值将被更改为你指定的值。如果值为 `null`，则该元素或属性被移除。在修改或删除子元素或属性时，第一个具有指定名称的元素或属性将被修改或移除。

下面的代码展示了如何创建与列表 14.2 中生成的相同 XML，但使用了 `SetElementValue` 和 `SetAttributeValue` 方法：

```csharp
XElement document = new XElement("books",  
        new XElement("book",  
        new XElement("publisher")));

XElement bookElement = document.Element("book");
XElement publisherElement = document.Element("publisher");

bookElement.SetElementValue("title",  
    "Sams Teach Yourself Visual C# 2010 in 24 Hours");
bookElement.SetElementValue("isbn-10", "0-672-33301-2");
bookElement.SetElementValue("author", "Dorman");
bookElement.SetElementValue("price", 39.99M);
bookElement.Element("price").  
    SetAttributeValue("currency", "US");

publisherElement.SetElementValue("name", "Sams Publishing");
publisherElement.SetElementValue("state", "IN");
```

列表 14.4 展示了检索 `price` 元素值的两种方法。

## 列表 14.4 使用直接转换检索 XElement 的值

```csharp
decimal price = (Decimal)(document.Element("book").Element("price"));
price = (Decimal)document.XPathSelectElement("//price");
```

### 顺便说一下

**XML 字符编码**

`XElement` 和 `XAttribute` 类自动处理包含无效 XML 字符的文本的编码和解码。给定以下语句

```csharp
XElement comments = new XElement("comments",
"This line contains special characters <node> & </node>");
```

结果会自动编码为：

```xml
<comments>This line contains special characters &lt;node&gt; &amp;
&lt;/node&gt;</comments>
```

当检索值时，它会被自动解码。

## 动手试一试

## 创建 XML 文档

通过遵循这些步骤，你将了解如何使用 LINQ to XML 类来创建 XML 文档。请在此练习结束时保持 Visual Studio 打开，因为你稍后还会使用这个应用程序。

1. 创建一个新的控制台应用程序。
2. 在 `Program.cs` 文件的 `Main` 方法中，实现列表 14.2 中的代码。
3. 编写一条语句，用于打印步骤 2 中创建的 `XElement` 的内容。
4. 使用 `Ctrl+F5` 运行应用程序。输出应该看起来像图 14.3。

### 图 14.3 创建 XML 文档

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_336_0.png)

## XName 和 XNamespace

XML 名称表示 XML 文档中元素或属性的名称，由两部分组成：XML 命名空间和本地名称。XML 命名空间使你能够唯一地限定元素和属性的名称，有助于避免 XML 文档不同部分之间的冲突。当你声明了一个 XML 命名空间后，你可以选择一个仅在该命名空间内唯一的本地名称。

在使用 XML 命名空间时，你会利用 XML 前缀，允许你为 XML 命名空间创建一个快捷方式。虽然 XML 前缀可以使 XML 文档更可读，但增加了复杂性，因为它们的意义依赖于其上下文。.NET Framework 提供了 `XNamespace` 类来表示 XML 命名空间。

`XName` 类表示本地名称。在 LINQ to XML 中，任何需要 XML 名称的地方都使用 `XName`。幸运的是，`XName` 包含从 `string` 的隐式转换，因此你很少直接处理 `XName`。每个 `XName` 都包含一个 `XNamespace`。如果元素不在命名空间中，则 `XNamespace` 为 `XNamespace.None`。

> **顺便说一下**
>
> **XML 命名空间**
>
> XML 命名空间声明与 XML 属性具有相同的语法，因此人们通常将它们视为属性，尽管它们并不是。LINQ to XML 在 XML 树中将命名空间表示为属性，以简化编程接口。如果你需要确定一个属性是否实际上是命名空间声明，可以使用 `IsNamespaceDeclaration` 属性。

列表 14.5 中的代码展示了使用命名空间创建列表 14.2 中相同 XML 的过程。

## 列表 14.5 使用 LINQ to XML 和命名空间创建 XML

```csharp
XNamespace ns = "http://www.w3.org/1999/xhtml";
XElement document = new XElement(ns + "books",
    new XElement(ns + "book",
        new XElement(ns + "title",
            "Sams Teach Yourself Visual C# 2010 in 24 Hours"),
        new XElement(ns + "isbn-10", "0-672-33101-2"),
        new XElement(ns + "author", "Dorman"),
        new XElement(ns + "price", new XAttribute("currency", "US"), 39.99M),
        new XElement(ns + "publisher",
            new XElement(ns + "name", "Sams Publishing"),
            new XElement(ns + "state", "IN")))));
```

这产生了列表 14.6 中所示的 XML。

## 清单 14.6 XML 数据

```
<books xmlns="http://www.w3.org/1999/xhtml">
    <book>
        <title>Sams Teach Yourself Visual C# 2010 in 24 Hours</title>
        <isbn-10>0-672-33101-2</isbn-10>
        <author>Dorman</author>
        <price currency="US">39.99</price>
        <publisher>
            <name>Sams Publishing</name>
            <state>IN</state>
        </publisher>
    </book>
</books>
```

尽管 LINQ to XML 类会自动处理命名空间声明，但有时可能需要通过提供命名空间前缀来控制命名空间在 XML 数据中的表示方式。可以通过显式定义用于命名空间的前缀来实现，方法包括一个 `xmlns` 属性，如清单 14.7 所示。

## 清单 14.7 使用 LINQ to XML 创建带有命名空间前缀的 XML

```
XNamespace ns = "http://www.w3.org/1999/xhtml";
XElement document = new XElement(ns + "books",
    new XAttribute(XNamespace.Xmlns + "ns", ns),
    new XElement(ns + "book",
        new XElement(ns + "title",
            "Sams Teach Yourself Visual C# 2010 in 24 Hours"),
        new XElement(ns + "isbn-10", "0-672-33101-2"),
        new XElement(ns + "author", "Dorman"),
        new XElement(ns + "price", new XAttribute("currency", "US"), 39.99M),
        new XElement(ns + "publisher",
            new XElement(ns + "name", "Sams Publishing"),
            new XElement(ns + "state", "IN")))));
```

这生成了清单 14.8 中所示的 XML。

## 清单 14.8 带有命名空间前缀的 XML 数据

```
<ns:books xmlns:ns="http://www.w3.org/1999/xhtml">
    <ns:book>
        <ns:title>Sams Teach Yourself Visual C# 2010 in 24 Hours</ns:title>
        <ns:isbn-10>0-672-33101-2</ns:isbn-10>
        <ns:author>Dorman</ns:author>
        <ns:price currency="US">39.99</ns:price>
        <ns:publisher>
            <ns:name>Sams Publishing</ns:name>
            <ns:state>IN</ns:state>
        </ns:publisher>
    </ns:book>
</ns:books>
```

当处理使用命名空间的文档时，通常通过 URI 而不是命名空间前缀来访问命名空间。这允许你使用全限定名，也称为**扩展名**，其形式为 `{namespace:name}` 名称。

例如，清单 14.6 中 `title` 元素的扩展名是 `{http://www.w3.org/1999/xhtml}` `title`。

### 原子化

`XNamespace` 对象是**原子化**的，这意味着如果两个对象具有完全相同的 URI，它们将共享同一个实例。虽然在创建 `XElement` 或 `XAttribute` 实例时使用扩展名是可能的，但这会有潜在的性能影响。每次遇到包含扩展名的字符串时，都必须解析该字符串以找到原子化的命名空间和名称。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_339_0.png)

### 动手试一试

#### 处理 XML 命名空间

要修改你在上一个练习中编写的代码以处理 XML 命名空间，请遵循以下步骤。如果你已关闭 Visual Studio，请先重复上一个练习。请确保在结束本练习时保持 Visual Studio 处于打开状态，因为你稍后将使用此应用程序。

- 1. 添加一条新的语句，声明一个 `XNamespace` 实例，定义一个 `http://www.w3.org/TR/html4` 的命名空间。
- 2. 修改你之前编写的语句，将刚刚声明的命名空间包含进来，并使用前缀为 `ns` 的命名空间，并将命名空间作为元素名称的一部分包含进去。
- 3. 使用 `Ctrl+F5` 运行应用程序。输出应如图 14.4 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_339_1.png)

### 选择和查询 XML

当拥有通过 `XElement` 实例在内存中表示的 XML 文档时，你几乎总是需要选择或查询信息。所有派生自 `XNode` 的类都提供了用于直接导航到 XML 树中特定节点的方法和属性。

`FirstNode` 和 `LastNode` 属性分别返回第一个和最后一个子节点，而 `NextNode` 和 `PreviousNode` 属性使你能够向前和向后遍历节点集合。`Parent` 属性使你能够直接导航到父节点。

清单 14.9 展示了如何使用清单 14.1 中简化版的 XML 来使用这些导航属性的示例。

## 清单 14.9 使用 XElement 的导航属性
