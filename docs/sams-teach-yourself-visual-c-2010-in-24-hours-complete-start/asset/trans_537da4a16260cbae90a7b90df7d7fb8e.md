

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

尽管 LINQ to XML 类会自动处理命名空间声明，但有时可能需要通过提供命名空间前缀来控制命名空间在 XML 数据中的表示方式。可以通过显式定义用于命名空间的前缀来实现，方法包括一个 **xmlns** 属性，如清单 14.7 所示。

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

例如，清单 14.6 中 title 元素的扩展名是 `{http://www.w3.org/1999/xhtml}` title。

### 原子化

XNamespace 对象是**原子化**的，这意味着如果两个对象具有完全相同的 URI，它们将共享同一个实例。虽然在创建 XElement 或 XAttribute 实例时使用扩展名是可能的，但这会有潜在的性能影响。每次遇到包含扩展名的字符串时，都必须解析该字符串以找到原子化的命名空间和名称。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_339_0.png)

### 动手试一试

#### 处理 XML 命名空间

要修改你在上一个练习中编写的代码以处理 XML 命名空间，请遵循以下步骤。如果你已关闭 Visual Studio，请先重复上一个练习。请确保在结束本练习时保持 Visual Studio 处于打开状态，因为你稍后将使用此应用程序。

- 1. 添加一条新的语句，声明一个 XNamespace 实例，定义一个 `http://www.w3.org/TR/html4` 的命名空间。
- 2. 修改你之前编写的语句，将刚刚声明的命名空间包含进来，并使用前缀为 `ns` 的命名空间，并将命名空间作为元素名称的一部分包含进去。
- 3. 使用 Ctrl+F5 运行应用程序。输出应如图 14.4 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_339_1.png)

### 选择和查询 XML

当拥有通过 XElement 实例在内存中表示的 XML 文档时，你几乎总是需要选择或查询信息。所有派生自 XNode 的类都提供了用于直接导航到 XML 树中特定节点的方法和属性。

FirstNode 和 LastNode 属性分别返回第一个和最后一个子节点，而 NextNode 和 PreviousNode 属性使你能够向前和向后遍历节点集合。Parent 属性使你能够直接导航到父节点。

清单 14.9 展示了如何使用清单 14.1 中简化版的 XML 来使用这些导航属性的示例。

## 清单 14.9 使用 XElement 的导航属性

```
XElement document = new XElement("book",
    new XElement("title", "Sams Teach Yourself Visual C# 2010 in 24 Hours"),
    new XElement("isbn-10", "0-672-33101-2"),
    new XElement("author", "Dorman"),
    new XElement("price", new XAttribute("currency", "US"), 39.99M));

Console.WriteLine(document.LastNode);
Console.WriteLine(document.FirstNode);
Console.WriteLine(document.LastNode.Parent);
Console.WriteLine(document.LastNode.PreviousNode);
Console.WriteLine(document.FirstNode.NextNode);
```

XElement 还提供了 FirstAttribute 和 LastAttribute 属性，它们返回与调用它们的 XElement 关联的第一个和最后一个属性。如果元素不包含任何属性，这两个属性都将返回 null；如果元素只包含一个属性，它们都返回相同的值。当检索到第一个或最后一个属性后，你可以使用 NextAttribute 和 PreviousAttribute 属性在属性集合中向前和向后移动。

虽然这些属性很方便，但它们提供的灵活性有限。如果你将 XML 树中的每个节点视为一个节点序列，那么就可以使用你在第 12 小时“理解查询表达式”中使用的相同 LINQ 查询。这是完全可能的，因为每个节点集合都是一个 IEnumerable<> 实例。

清单 14.10 展示了如何对从清单 14.2 创建的 XElement 执行简单的 LINQ 查询。

## 清单 14.10 对 XElement 的 LINQ 查询

```
foreach (var o in document.Elements()
    .Where(e => (string)e.Element("author") == "Dorman"))
{
    Console.WriteLine(o);
}
```

清单 14.10 中显示的代码使用了 Elements 方法来返回当前 XElement 的所有子元素的 IEnumerable<> 序列。

在这种情况下，所有子元素都返回；但是，如果提供一个名称作为参数，则只会返回具有相同名称的那些子元素。

### LINQ to XML 和 XPath 查询

当使用 `System.XML` 中提供的传统 XML DOM 类时，你必须使用 XPath 查询来选择节点集合或单个节点。在 LINQ to XML 中，这不再必要，但通过 `System.Xml.XPath` 命名空间提供的一组扩展方法得到支持。

这些扩展方法是：

- **`CreateNavigator`** — 为 `XNode` 创建一个 `XPathNavigator`。
- **`XPathEvaluate`** — 评估一个 XPath 表达式，返回包含表达式结果的对象。
- **`XPathSelectElement`** — 使用 XPath 表达式选择一个 `XElement`。
- **`XPathSelectElements`** — 使用 XPath 表达式选择一个元素集合。

提供给 Where 方法的 lambda 表达式将结果序列限制为包含作者元素且其值等于字符串 “Dorman” 的序列。Element 方法用于返回名称与提供的名称相对应的第一个 XElement。

通过 Attributes 和 Attribute 方法选择属性同样简单。Attribute 方法返回名称与提供的名称相对应的单个属性，如果找不到匹配的属性则返回 null。Attributes 方法返回当前 XElement 的 `IEnumerable<XAttribute>` 属性序列。虽然 Attributes 方法可以接受名称作为参数，但如果找不到匹配的属性，它总是返回一个空集合，或者返回包含一个元素的集合，因为属性在每个元素内必须具有唯一名称。

### 动手试一试

#### 选择 XML

通过遵循这些步骤，你可以了解如何使用 LINQ to XML 选择特定元素。如果你已关闭 Visual Studio，请先重复上一个练习。请确保在结束本练习时保持 Visual Studio 处于打开状态，因为你稍后将使用此应用程序。

- 1. 用清单 14.10 中显示的代码替换上一个练习中打印 XElement 实例内容的语句。确保更改你要查询的元素名称以包含 XNamespace。
- 2. 使用 Ctrl+F5 运行应用程序。输出应如图 14.5 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_341_0.png)

