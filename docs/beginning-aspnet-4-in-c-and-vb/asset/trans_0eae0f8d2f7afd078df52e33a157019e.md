
该架构包含了 DataSet 中的这两个 DataTable。此外，数据也包含了这两个表中的所有数据。为简洁起见，此处仅显示了第一条 Products 和 ProductCategory 记录。和之前一样，你可以通过传入正确的 XmlWriteMode 参数，仅保存架构或仅保存数据。

## 将 XML 转换为 ADO.NET 数据

假设你有一个 XML 文档，希望将其导入 ADO.NET DataSet。你可能希望这样做，以便将 XML 加载到数据库中，或者将数据绑定到诸如 DataGrid 之类的 .NET 数据控件上。这样，你实际上可以将 XML 文档用作数据存储，并完全消除数据库的开销。如果你的数据量相当小，这是一个很有吸引力的选择。下面是一些入门代码：

```
private void button_Click(object sender, EventArgs e)
{
    //create the DataSet
    DataSet ds = new DataSet("XMLProducts");
    //read in the xml document
    ds.ReadXml("Products.xml");
    //load data into grid
    dataGridView1.DataSource = ds.Tables[0];
    textBox1.Text = "";
    foreach (DataTable dt in ds.Tables)
    {
        textBox1.Text += dt.TableName + "\r\n";
        foreach (DataColumn col in dt.Columns)
        {
            textBox1.Text += "\t" + col.ColumnName + " - " + col.DataType.FullName + "\r\n";
        }
    }
}
```

代码片段 frmADOXML.cs

就这么简单。在本例中，你实例化一个新的 DataSet 对象。然后，调用 ReadXml() 方法，你就可以在 DataSet 的 DataTable 中得到 XML。与 WriteXml() 方法一样，ReadXml() 有一个 `XmlReadMode` 参数。ReadXml() 在 `XmlReadMode` 中有更多选项，如下表所示。

| 值 | 描述 |
|---|---|
| Auto | 将 `XmlReadMode` 设置为最合适的选项。如果数据为 DiffGram 格式，则选择 DiffGram。如果已读取架构，或检测到内联架构，则选择 ReadSchema。如果尚未为 DataSet 分配架构，且未检测到内联架构，则选择 IgnoreSchema。 |
| DiffGram | 读取 DiffGram 并将更改应用到 DataSet。 |
| Fragment | 读取包含 XDR 架构片段的文档，例如 SQL Server 创建的类型。 |
| IgnoreSchema | 忽略可能找到的任何内联架构。将数据读入当前 DataSet 架构。如果数据与 DataSet 架构不匹配，则丢弃该数据。 |
| InferSchema | 忽略任何内联架构。根据 XML 文档中的数据创建架构。如果 DataSet 中已存在架构，则使用该架构，并在需要时使用其他列和表进行扩展。如果列已存在但数据类型不同，则会引发异常。 |
| ReadSchema | 读取内联架构并加载数据。不会覆盖 DataSet 中的架构，但如果内联架构中的表已存在于 DataSet 中，则会引发异常。 |

还有 `ReadXmlSchema()` 方法。该方法读取独立的架构，并创建表、列和关系。当你的架构与数据不是内联时，可以使用此方法。`ReadXmlSchema()` 具有相同的四个重载：带有文件名和路径名的字符串、基于 `Stream` 的对象、基于 `TextReader` 的对象以及基于 `XmlReader` 的对象。

为了证明数据表被正确创建，我们遍历表和列，并在文本框中显示名称。你可以将其与数据库进行比较，确认一切正常。最后的 `foreach` 循环执行此任务。图 33-6 显示了输出。

![](img/d7d2ffa0a76feaab821930e95daace93_994_0.png)

图 33-6

查看列表框，你可以检查所创建的数据表中的所有列是否具有正确的名称和数据类型。

另外你可能想注意的是，由于前面两个示例没有在数据库之间传输任何数据，因此没有定义 SqlDataAdapter 或 SqlConnection。这显示了 System.Xml 命名空间和 ADO.NET 的真正灵活性：你可以以多种格式查看相同的数据。如果你需要进行转换并以 HTML 格式显示数据，或者需要将数据绑定到网格，你可以获取相同的数据，只需一次方法调用即可将其转换为所需格式。

## 在 XML 中序列化对象

序列化是将对象持久化到磁盘的过程。应用程序的另一部分，甚至一个单独的应用程序，都可以反序列化该对象，并且它将处于与序列化之前相同的状态。.NET Framework 提供了几种方法来实现这一点。

本节介绍 System.Xml.Serialization 命名空间，该命名空间包含用于将对象序列化为 XML 文档或流的类。这意味着对象的公共属性和公共字段会转换为 XML 元素、属性或两者。

System.Xml.Serialization 命名空间中最重要的类是 XmlSerializer。要序列化对象，首先需要实例化一个 XmlSerializer 对象，指定要序列化的对象的类型。然后，需要实例化一个流/编写器对象，将文件写入流/文档。最后一步是在 XmlSerializer 上调用 Serialize() 方法，将流/编写器对象和要序列化的对象传递给它。

可序列化的数据可以是基元类型、字段、数组以及 XmlElement 和 XmlAttribute 对象形式的嵌入式 XML。

要从 XML 文档中反序列化对象，可以反转前面示例中的过程。创建一个流/读取器和一个 XmlSerializer 对象，然后将流/读取器传递给 Deserialize() 方法。此方法返回反序列化后的对象，但需要将其转换为正确的类型。

> > XML 序列化程序无法转换私有数据，只能转换公共数据，并且无法序列化对象图。但是，这些不应该成为严重的限制；通过仔细设计类，你应该能够轻松避免这些问题。如果确实需要序列化公共和私有数据以及包含许多嵌套对象的对象图，则需要使用 System.Runtime.Serialization.Formatters.Binary 命名空间。

使用 System.Xml.Serialization 类可以完成的其他一些任务包括：
- 确定数据应为属性还是元素
- 指定命名空间
- 更改属性或元素名称

对象与 XML 文档之间的链接是用于标注类的自定义 C# 属性。这些属性用于告知序列化程序如何写出数据。.NET Framework 附带的 xsd.exe 工具可以帮助你创建这些属性。xsd.exe 可以执行以下操作：
- 从 XDR 架构文件生成 XML 架构
- 从 XML 文件生成 XML 架构
- 从 XSD 架构文件生成 DataSet 类
- 生成具有 XmlSerialization 自定义属性的运行时类
- 从已开发的类生成 XSD 文件
- 限制在代码中创建哪些元素
- 确定生成代码应使用的编程语言（C#、Visual Basic .NET 或 JScript .NET）
- 从编译的程序集中的类型创建架构

有关 xsd.exe 命令行选项的详细信息，请参阅 Framework 文档。

尽管 xsd.exe 具有这些功能，但你不必使用它来创建用于序列化的类。这个过程非常简单。下面是一个序列化类的简单应用程序。在示例的开头，有一段非常简单的代码，用于创建新的 Product 对象 pd，并向其中填充一些数据：

```
private void button1_Click(object sender, EventArgs e)
{
    //new products object
    Product pd = new Product();
    //set some properties
    pd.ProductID = 200;
    pd.CategoryID = 100;
    pd.Discontinued = false;
    pd.ProductName = "Serialize Objects";
    pd.QuantityPerUnit = "6*";
    pd.ReorderLevel = 1;
    pd.SupplierID = 1;
    pd.UnitPrice = 100;
    pd.UnitsInStock = 10;
    pd.UnitsOnOrder = 0;
}
```

XmlSerializer 类的 Serialize() 方法实际执行序列化，它有九个重载。需要的参数之一是用于写入数据的流。它可以是 Stream、TextWriter 或 XmlWriter 参数。在示例中，你创建了一个基于 TextWriter 的对象 tr。接下来要创建基于 XmlSerializer 的对象 sr。XmlSerializer 需要知道它正在序列化的对象的类型信息，因此你使用 typeof 关键字指定要序列化的类型。创建 sr 对象后，调用 Serialize() 方法，传入 tr（基于流的对象）和要序列化的对象，此处为 pd。使用完流后，请务必将其关闭：

```
//new TextWriter and XmlSerializer
TextWriter tr = new StreamWriter("serialprod.xml");
XmlSerializer sr = new XmlSerializer(typeof(Product));
//serialize object
sr.Serialize(tr, pd);
tr.Close();
webBrowser1.Navigate(AppDomain.CurrentDomain.BaseDirectory + "serialprod.xml");
```

接下来是 Product 类，即要序列化的类。它与你可能编写的任何其他类之间的唯一区别是添加了 C# 属性。这些属性中的 XmlRootAttribute 和 XmlElementAttribute 类继承自 System.Attribute 类。不要将这些属性与 XML 文档中的属性混淆。C# 属性只是一些声明性信息。
