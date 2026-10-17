
```
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                textBox1.Text = openFileDialog1.FileName;
            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                byte[] bufferwrite;
                FileStream fsSource;
                FileStream fsDest;
                GZipStream gzDecompressed;
                fsSource = new FileStream(textBox1.Text, FileMode.Open, FileAccess.Read, FileShare.Read);
                gzDecompressed = new GZipStream(fsSource, CompressionMode.Decompress, true);
                bufferwrite = new byte[4];
                fsSource.Position = (int)fsSource.Length - 4;
                fsSource.Read(bufferwrite, 0, 4);
                fsSource.Position = 0;
                int bufferLength = BitConverter.ToInt32(bufferwrite, 0);
                byte[] buffer = new byte[bufferLength + 100];
                int readoffset = 0;
                int totalBytes = 0;
                while (true)
                {
                    int bytesRead = gzDecompressed.Read(buffer, readoffset, 100);
                    if (bytesRead == 0)
                        break;
                    readoffset += bytesRead;
                    totalBytes += bytesRead;
                }
                fsDest = new FileStream(saveFileDialog1.FileName, FileMode.Create);
                fsDest.Write(buffer, 0, totalBytes);
                fsSource.Close();
                gzDecompressed.Close();
                fsDest.Close();
            }
        }
    }
}
```

4. 按 F5 键运行应用程序并单击 Browse 按钮以打开打开对话框。

5. 从打开对话框中选择压缩文件并单击打开按钮，如图 29.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1457_0.png)

图 29.35：显示打开对话框

6. 现在，单击 `Form1` 表单上的 Decompress File 按钮，其结果是另存为对话框出现，如图 29.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1457_1.png)

图 29.36：显示另存为对话框

7. 在另存为对话框的文件名组合框中指定文件的名称，以便您可以在指定位置轻松找到文件的解压缩形式。在本例中，我们指定了 `DecompressedFile`（图 29.36）。

8. 单击保存按钮以将文件以 `DecompressedFile` 的名称保存在所需位置。现在，让我们总结本章讨论的主要主题。

## 摘要

在本章中，您学习了 `System.IO` 命名空间及其类。接下来，您学习了如何处理目录和文件。此外，您还学习了如何检查目录是否存在、创建、重命名和删除目录。您还了解到文件 I/O 操作涉及检查文件属性；并执行其他操作，例如创建、读取、写入、重命名和复制文件。最后，您学习了如何压缩和解压缩文件。

在下一章中，您将学习如何使用可扩展标记语言（XML）和 .NET。

# 30 使用 XML 和 .NET 工作

![](img/e073a4882197be4ab61103cbe0bcb394_1458_0.png)

| 如果您需要立即解决以下问题： | 请参见页码： |
|---|---|
| 使用流式 XML | 1425 |
| 在 .NET 中实现 DOM | 1432 |
| 导航和转换数据 | 1435 |
| 转换 ADO.NET 和 XML 数据 | 1438 |
| 使用 XML 实现对象序列化 | 1442 |

## In Depth

Extensible Markup Language (XML) 是一种简单且灵活的文本格式，广泛用于在 Web 上交换不同类型的数据。XML 对于 .NET Framework 具有非常重要的作用，因为它提供了一个命名空间 `System.Xml`，其中包含处理 XML 所需的类。你可以导入此命名空间在 .NET 应用程序中使用 XML。XML 还存储 .NET 应用程序中使用的数据。ActiveX Data Objects (ADO) .NET 是在 .NET Framework 4.0 支持的许多编程语言中用于数据访问和数据操作的主要工具。ADO.NET 使用 XML 作为在应用程序之间传输数据的媒介，并提供读取和写入 XML 文档的强大功能。

Document Object Model (DOM) 是一种平台和语言无关的接口，允许程序和脚本动态地访问和更新文档的内容和结构。你可以使用 `XmlDocument` 类实现 DOM。此外，你可以使用 `System.Xml.Serialization` 命名空间对对象进行序列化和反序列化。

在本章中，你将了解 .NET Framework 4.0 提供的对 XML 的支持。你将了解 `System.Xml` 命名空间，以及如何处理流式 XML。此外，你将学习如何在 .NET 中实现 DOM。你还将了解如何在 .NET Framework 4.0 中使用 XPath 和 XSLT。最后，你将学习如何将 XML 与 ADO.NET 结合使用，以及如何在 XML 中进行对象序列化。

现在，让我们通过描述 .NET Framework 4.0 提供的对 XML 的支持来开始我们的讨论。

## Support for XML in .NET Framework 4.0

XML 是一种数据描述语言 (DDL)，由 World Wide Web Consortium (W3C) 开发。它被 ADO.NET 用作存储和传输数据的格式。W3C 已为 XML 开发了一些标准。.NET Framework 4.0 支持的 W3C 标准集如下：

- XML 1.0 (www.w3.org/TR/1998/REC-xml-19980210) 支持 Document Type Definition (DTD)
- XML Namespaces (www.w3.org/TR/REC-xml-names) 用于流级和 DOM
- XML Schemas (www.w3.org/2001/XMLSchema)
- XPath expressions (www.w3.org/TR/xpath)
- XSLT transformations (www.w3.org/TR/xslt)
- DOM Level 1 Core (www.w3.org/TR/REC-DOM-Level-1/)
- SOAP 1.1 (www.w3.org/TR/SOAP)

在探索了 W3C 开发的各种标准之后，让我们现在来看一下在 .NET Framework 4.0 中支持 XML 的命名空间。

## The `System.Xml` Namespace

.NET Framework 提供了一个名为 `System.Xml` 的命名空间，其中包含处理 XML 的类。表 30.1 描述了 `System.Xml` 命名空间中包含的一些重要类：

**Table 30.1: Important Classes in the `System.Xml` Namespace**

| Class Name | Description |
|---|---|
| `XmlReader` | 指定一个抽象读取器类，提供快速且只向前、无缓存的 XML 数据。 |
| `XmlWriter` | 指定一个抽象写入器类，提供快速无缓存的 XML 数据，形式为流或文件格式。 |
| `XmlTextReader` | 扩展 `XmlReader` 类并提供对 XML 数据的快速且只向前的流访问。 |
| `XmlTextWriter` | 扩展 `XmlWriter` 类并提供快速且只向前的 XML 流生成。 |
| `XmlNode` | 指定一个表示 XML 文档中单个节点的抽象类。它是 XML 命名空间中许多类的基类。 |
| `XmlDocument` | 扩展 `XmlNode` 类并实现 DOM。它在内存中提供 XML 文档的树结构，并使用户能够导航和编辑 XML 文档。 |
| `XmlResolver` | 指定一个解析外部基于 XML 的资源（如 DTD 和模式引用）的抽象类。它还用于处理 `<xml:include>` 和 `<xml:import>` 元素。 |
| `XmlUrlResolver` | 扩展 `XmlResolver` 类并解析由统一资源标识符 (URI) 命名的资源 |

## Working with Streamed XML

在引入 DOM 之前，Simple Application Programming Interface (API) for XML (SAX) 用于访问存储在 XML 文档中的信息。在 SAX 模型中，你只有 `XmlReader` 和 `XmlWriter` 类来处理 XML 数据。基于 `XmlReader` 的类用于以快速向前且只读的方式流式传输 XML 数据以供处理。基于 `XmlWriter` 的类用于生成 XML 文档。`XmlReader` 和 `XmlWriter` 是抽象类，因此你需要在应用程序中工作时使用这些类的派生类。从 `XmlReader` 抽象类派生的类如下：

- `XmlTextReader` — 使用基于流的对象或 `TextReader/TextWriter` 对象工作
- `XmlNodeReader` — 使用 `XmlNode` 类作为源来读取 XML 数据
- `XmlValidatingReader` — 添加 Document Type Definition (DTD) 和模式验证；并提供数据验证

`XmlTextWriter` 是从 `XmlWriter` 抽象类派生的类。与 `XmlTextReader` 类类似，此类也使用基于流的对象或来自 `System.IO` 命名空间的 `TextReader/TextWriter` 对象。

## The `XmlReader` Class

`XmlReader` 类用于以快速、只向前且无缓存的方式读取 XML 数据。它是一个只读游标，其工作方式类似于 SAX 模型。`XmlReader` 类可以读取 XML 文档或流。它使用户能够提取数据，并可以跳过应用程序中不需要的记录。然而，SAX 模型使用推送模型来读取 XML 数据，其中解析器将事件推送到应用程序。这些事件在每次读取到新记录（数据或节点）时通知应用程序。

要在应用程序中处理 `XmlReader` 类，你需要导入以下命名空间：

```
System.Xml;
```

你可以使用各种方法从 XML 文档中读取数据，如表 30.2 所述：

**Table 30.2: Methods Used by the `XmlReader` Class for Reading XML Data**

| Method Name | Description |
|---|---|
| `Read()` | 将游标位置移动到下一个节点。 |
| `ReadStartElement()` | 在验证当前节点是否为第一个元素后，将游标位置移动到下一个节点。如果当前节点不是开始元素，则会引发类型为 `XmlException` 的异常。调用此方法的效果与调用 `IsStartElement()` 方法，然后调用 `Read()` 方法的效果相同。 |
| `ReadString()` | 从元素中读取文本数据。此方法返回包含数据的字符串对象。 |
| `ReadElementString()` | 工作方式类似于 `ReadString()` 方法。唯一的区别是你可以选择性地向此方法传递元素的名称。 |

## Validating XML Documents Using the `XmlReader` Class

你可以使用抽象类 `XmlReader` 在读取数据时将 XML 文档与 XML Schema Definition (XSD) 文件进行验证。此类通过首先创建 `XmlReaderSettings` 类的对象来验证 XML 文档是否符合 XSD 模式。然后，你通过设置 `XmlReaderSettings` 类的 `Schemas` 属性将 XSD 模式添加到 `XmlSchemaSet`。你还必须将 `XmlReaderSettings` 类的 `XsdValidate` 属性设置为 true，其默认值是 false。

## The `XmlWriter` Class

`XmlWriter` 类用于将 XML 写入流、文件或 `TextWriter` 对象。此外，它以只向前、无缓存的方式工作。你还可以配置 `XmlWriter` 对象，通过指定一些参数，例如是否缩进 XML 文档的内容，以及 XML 文档是否支持命名空间。

## Implementing DOM in .NET Framework 4.0

DOM 在 .NET Framework 中通过使用 `XmlNode` 抽象类实现。.NET Framework 4.0 中对 DOM 的实现支持 W3C 开发的核心 DOM Level 1 和核心 DOM Level 2 标准。`XmlNode` 抽象类表示 XML 文档的节点。`XmlNodeList` 类是有序的节点列表，支持节点的索引访问。对任何节点的更改都会立即反映在 `XmlNodeList` 类指定的节点列表中。表 30.3 列出了从 `XmlNode` 抽象类派生的类：

**Table 30.3: Classes Derived from the `XmlNode` Abstract Class**

| Class Name | Description |
|---|---|
| `XmlAttribute` | 表示 `XmlElement` 对象的属性对象。 |
| `XmlDocument` | 表示实现 DOM Level 1 和 DOM Level 2 规范的整个 XML 文档。与 `XmlReader` 和 `XmlWriter` 类不同，此类为你提供读写功能以及对 DOM 树的随机访问。 |
| `XmlDocumentFragment` | 表示文档树的片段。 |
| `XmlEntity` | 表示实体节点。 |
| `XmlLinkedNode` | 包含 `NextSibling` 和 `PreviousSibling` 属性，用于检索当前节点之后或之前的节点。它是一个抽象类。 |
| `XmlNotation` | 包含在 DTD 或模式中声明的记法。 |

`XmlLinkedNode` 类（在上表中描述）是一个抽象类，包含派生类。表 30.4 列出了从 `XmlLinkedNode` 类（列于表 30.3）派生的类：

**Table 30.4: Classes Derived from the `XmlLinkedNode` Class**

| Class Name | Description |
|---|---|
| `XmlDeclaration` | 表示声明节点 (`<?xml version='1.0'...?>`) |
| `XmlDocumentType` | 表示与文档类型声明相关的数据 |
| `XmlElement` | 表示 XML 元素对象 |
| `XmlEntityReference` | 表示实体引用节点 |
| `XmlProcessingInstruction` | 包含 XML 处理指令 |
| `XmlCharacterData` | 为其他类提供文本操作方法。它是一个抽象类。 |
