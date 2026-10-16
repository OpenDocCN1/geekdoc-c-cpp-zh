

{
  "author": {
    "first-name":"Herman",
    "last-name":"Melville"
  },
  "price": 11.99
},
"book": {
  "genre":"philosophy",
  "publicationdate": 1991,
  "ISBN":"1-861001-57-6",
  "title":"The Georgias",
  "author": {
    "name":"Plato",
  },
  "price": 9.99
}
```

在 .NET 中，JSON 被用于许多不同的地方。当你创建新的 DNX 项目时，可以看到 JSON 被用作项目配置文件。它与 Web 项目一起使用，用于通过 ASP.NET Web API 将数据从客户端序列化并序列化到客户端（参见第 42 章“ASP.NET Web API。”），并用于诸如与 Microsoft Azure 提供的 NoSQL 数据库 DocumentDB 之类的数据存储。

在使用 JSON 与 .NET 时，你有多种选择。其中一种 JSON 序列化器是 DataContractJsonSerializer。该类型派生自基类 XmlObjectSerializer，虽然它与 XML 并没有真正的关联。当数据契约序列化技术被发明时（这是在 .NET 3.0 中发生的），想法是今后所有序列化都是 XML（XML 的二进制格式也可用）。随着时间的推移，这一假设不再成立。JSON 被广泛使用。事实上，JSON 已被添加到层次结构中以支持数据契约序列化。然而，一个更快、更灵活的实现赢得了市场，现在由 Microsoft 支持并与许多 .NET 应用程序一起使用：Json.NET。因为这个库是与 .NET 应用程序一起使用最多的，所以本章对其进行了介绍。

除了核心 JSON 标准之外，JSON 也在不断发展。XML 中已知的功能被添加到 JSON 中。让我们进入 JSON 改进的示例，并将其与 XML 功能进行比较。XML 架构定义（XSD）描述 XML 词汇表；截至本文撰写时，具有类似功能的 JSON Schema 仍在进行中。使用 WCF，XML 可以使用自定义二进制格式进行压缩。你也可以以比文本格式更紧凑的二进制形式序列化 JSON。JSON 的二进制版本由 BSON（Binary JSON）描述：http://bsonspec.org。跨网络发送 SOAP（一种 XML 格式）使用 Web 服务描述语言（WSDL）来描述服务。对于提供 JSON 数据的 REST 服务，也提供描述：Swagger（http://swagger.io）。

**NOTE** *第 42 章介绍了 ASP.NET Web API 和 Swagger。*

现在是时候进入 .NET Framework 类的具体使用。

# 读取和写入流式 XML

`XmlReader` 和 `XmlWriter` 类提供了一种快速读取和写入大型 XML 文档的方法。基于 `XmlReader` 的类提供了一个非常快速的、只向前、只读的光标，用于流式传输 XML 数据以供处理。因为它是一个流式模型，所以内存需求并不高。然而，你不具备 DOM 基于模型所提供的导航灵活性和读取或写入能力。基于 `XmlWriter` 的类生成符合 W3C XML 1.0（第 4 版）的 XML 文档。

使用 `XmlReader` 和 `XmlWriter` 的示例代码使用了以下依赖项和命名空间：

# 依赖项

```
NETStandard.Library

System.Xml.ReaderWriter
```

# 命名空间

```
System.Xml

static System.Console
```

该应用程序使你能够为所有不同的示例用例指定多个命令行参数，这些用例定义为 `const` 值，并且还指定要读取和写入的文件名（代码文件 `XmlReaderAndWriterSample/Program.cs`）：

```
class Program
{
    private const string BooksFileName ="books.xml";
    private const string NewBooksFileName ="newbooks.xml";
    private const string ReadTextOption ="-r";
    private const string ReadElementContentOption ="-c";
    private const string ReadElementContentOption2 ="-c2";
    private const string ReadDecimalOption ="-d";
    private const string ReadAttributesOption ="-a";
    private const string WriteOption ="-w";
    // etc
}
```

`Main` 方法根据传递的命令行调用特定的示例方法：

```
static void Main(string[] args)
{
    if (args.Length != 1)
    {
        ShowUsage();
        return;
    }
}
```

```
switch (args[0])
{
    case ReadTextOption:
        ReadTextNodes();
        break;
    case ReadElementContentOption:
        ReadElementContent();
        break;
    case ReadElementContentOption2:
        ReadElementContent2();
        break;
    case ReadDecimalOption:
        ReadDecimal();
        break;
    case ReadAttributesOption:
        ReadAttributes();
        break;
    default:
        ShowUsage();
        break;
}
}
```

# 使用 XmlReader 读取 XML

XmlReader 使你能够读取大型 XML 流。它被实现为一个拉模型解析器，以将数据拉入请求它的应用程序。

以下是读取 XML 数据的非常简单的示例；稍后你将更详细地查看 XmlReader 类。因为 XmlReader 是一个抽象类，所以它不能直接实例化。相反，会调用工厂方法 Create 来返回派生自基类 XmlReader 的实例。Create 方法提供了几个重载，其中第一个参数可以提供文件名、TextReader 或 Stream。示例代码直接将文件名传递给 Books.xml 文件。创建读取器后，可以使用 Read 方法读取节点。一旦没有节点可用，Read 方法返回 false。你可以通过 while 循环进行调试，查看从 books.xml 文件返回的所有节点类型。只有对于类型为 XmlNodeType.Text 的节点，其值才会被写入控制台（代码文件 XMLReaderAndWriterSample/Program.cs）：

```
public static void ReadTextNodes()
{
    using (XmlReader reader = XmlReader.Create(BooksFileName))
    {
        while (reader.Read())
        {
            if (reader.NodeType == XmlNodeType.Text)
            {
                WriteLine(reader.Value);
            }
        }
    }
}
```

使用 -r 选项运行应用程序会显示所有文本

# 节点的值：

The Autobiography of Benjamin Franklin
Benjamin
Franklin
8.99
The Confidence Man
Herman
Melville
11.99
The Gorgias
Plato
9.99

# 使用读取方法

有几种方法可以遍历文档。如前例所示，Read 会带你到下一个节点。然后你可以验证节点是否有值（HasValue）或，如你稍后看到的，节点是否有任何属性（HasAttributes）。你也可以使用 ReadStartElement 方法，它会验证当前节点是否为开始元素，然后将你定位到下一个节点。如果不在开始元素上，则会引发 XmlException。调用此方法等同于调用 IsStartElement 方法然后调用 Read 方法。

ReadElementString 与 ReadString 类似，只是你可以选择性地传入元素的名称。如果下一个内容节点不是开始标签，或者 Name 参数与当前节点 Name 不匹配，则会引发异常。

下面是一个使用 ReadElementString 的示例。请注意它使用了 FileStreams，因此你需要确保导入 System.IO 命名空间（代码文件 XMLReaderAndWriterSample/Program.cs）：

```
public static void ReadElementContent()
{
    using (XmlReader reader = XmlReader.Create(BooksFileName))
    {
        while (!reader.EOF)
        {
            if (reader.MoveToContent() == XmlNodeType.Element &&
                reader.Name =="title")
            {
                WriteLine(reader.ReadElementContentAsString());
            }
            else
            {
                // move on
                reader.Read();
            }
        }
    }
}
```

在 while 循环中，MoveToContent 方法用于查找每个类型为 XmlNodeType.Element 且名称为 title 的节点。XmlTextReader 的 EOF 属性检查循环结束条件。如果节点

不是 Element 类型或名称不是 title，则 else 子句会发出 Read 方法以移动到下一个节点。当找到符合条件的节点时，结果会写入控制台。这应该只会将书籍标题写入控制台。请注意，在成功调用 ReadElementString 后，你不需要发出 Read 调用，因为 ReadElementString 会消耗整个元素并将你定位到下一个节点。

如果你从 if 子句中删除 && rdr.Name=="title"，则在抛出 XmlException 时必须捕获它。查看 XML 数据文件，MoveToContent 找到的第一个元素是 <bookstore> 元素。因为它是一个元素，所以通过了 if 语句中的检查。然而，因为它不包含简单的文本类型，所以会导致 ReadElementString 引发 XmlException。一种解决方法是在异常处理程序中捕获异常并调用 Read 方法（代码文件 XmlReaderAndWriterSample/Program.cs）：

```
public static void ReadElementContent2()
{
    using (XmlReader reader = XmlReader.Create(BooksFileName))
    {
        while (!reader.EOF)
        {
            if (reader.MoveToContent() == XmlNodeType.Element)
            {
                try
                {
                    WriteLine(reader.ReadElementContentAsString());
                }
                catch (XmlException ex)
                {
                    reader.Read();
                }
            }
            else
            {
                // move on
                reader.Read();
            }
        }
    }
}
```

运行此示例后，结果应与之前相同。XmlReader 还可以读取强类型数据。有几个 ReadElementContentAs 方法，例如 ReadElementContentAsDouble、ReadElementContentAsBoolean 等。以下示例展示了如何将值读入十进制并对值进行一些数学运算。在这种情况下，price 元素的值增加了 25%（代码文件 XmlReaderAndWriterSample/Program.cs）：

```
public static void ReadDecimal()
{
    using (XmlReader reader = XmlReader.Create(BooksFileName))
    {
        while (reader.Read())
        {
            if (reader.NodeType == XmlNodeType.Element)
```

