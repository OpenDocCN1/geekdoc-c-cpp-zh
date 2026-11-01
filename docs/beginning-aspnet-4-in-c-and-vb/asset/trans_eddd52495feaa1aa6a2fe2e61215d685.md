
总而言之，执行转换时需牢记的关键是使用正确的 XML 数据存储。如果不需要编辑功能，可使用 XPathDocument；如果数据来自 ADO.NET，可使用 XmlDataDocument；如果需要编辑数据，则使用 XmlDocument。每种情况下，您处理的都是相同的过程。

## XML 与 ADO.NET

XML 是将 ADO.NET 与外部世界联系起来的粘合剂。ADO.NET 从设计之初就致力于在 XML 环境中工作。XML 用于在数据存储与应用程序或网页之间传输数据。由于 ADO.NET 在远程场景中使用 XML 作为传输介质，因此可以与那些甚至不了解 ADO.NET 的应用程序和系统交换数据。鉴于 XML 在 ADO.NET 中的重要性，ADO.NET 提供了一些强大的功能来读写 XML 文档。System.Xml 命名空间也包含一些可以使用或利用 ADO.NET 关系数据的类。

示例中使用的数据库来自 AdventureWorksLT 示例应用程序。该示例数据库可从 codeplex.com/SQLServerSamples 下载。请注意，AdventureWorks 数据库有多个版本。大多数版本都可以使用，但 LT 版本是简化版，对于本章而言已经绰绰有余。

### 将 ADO.NET 数据转换为 XML

第一个示例使用 ADO.NET、流和 XML 将一些数据从数据库提取到 DataSet 中，使用来自 DataSet 的 XML 加载 XmlDocument 对象，并将 XML 加载到文本框中。要运行接下来的几个示例，需要添加以下 using 语句：

```
using System.Data;
using System.Xml;
using System.Data.SqlClient;
using System.IO;
```

连接字符串定义为模块级变量：

```
string _connectString = "Server=.\\SQLEXPRESS; Database=AdventureWorksLT;Trusted_Connection=Yes";
```

ADO.NET 示例在窗体中添加了一个 DataGrid 对象。由于数据绑定到网格，因此可以在 DataGrid 中查看 ADO.NET DataSet 中的数据，也可以查看加载到文本框中的生成 XML 文档中的数据。下面是第一个示例的代码。示例的第一步是创建标准的 ADO.NET 对象以生成 DataSet 对象。创建数据集后，将其绑定到网格。

```
private void button1_Click(object sender, EventArgs e)
{
    XmlDocument doc = new XmlDocument();
    DataSet ds = new DataSet("XMLProducts");
    SqlConnection conn = new SqlConnection(_connectString);
    SqlDataAdapter da = new SqlDataAdapter("SELECT Name, StandardCost FROM SalesLT.Product", conn);
    // fill the dataset
    da.Fill(ds, "Products");
    // load data into grid
    dataGridView1.DataSource = ds.Tables["Products"];
}
```

创建 ADO.NET 对象并绑定到网格后，您将实例化一个 MemoryStream 对象、一个 StreamReader 对象和一个 StreamWriter 对象。StreamReader 和 StreamWriter 对象将使用 MemoryStream 来移动 XML：

```
MemoryStream memStrm = new MemoryStream();
StreamReader strmRead = new StreamReader(memStrm);
StreamWriter strmWrite = new StreamWriter(memStrm);
```

使用 MemoryStream 可以避免将任何内容写入磁盘；不过，您也可以使用任何基于 Stream 类的对象，例如 FileStream。

下一步是生成 XML。您调用 DataSet 类的 WriteXml() 方法。此方法会生成一个 XML 文档。WriteXml() 有两个重载：一个接受包含文件路径和名称的字符串，另一个增加了一个模式参数。该模式是 XmlWriteMode 枚举，其可能的值如下：

- IgnoreSchema
- WriteSchema
- DiffGram

如果您不希望 WriteXml() 在 XML 文件开头写入内联架构，则使用 IgnoreSchema；如果希望写入，则使用 WriteSchema 参数。DiffGram 显示 DataSet 中编辑前后的数据。

```
// write the xml from the dataset to the memory stream
ds.WriteXml(strmWrite, XmlWriteMode.IgnoreSchema);
memStrm.Seek(0, SeekOrigin.Begin);
// read from the memory stream to an XmlDocument object
doc.Load(strmRead);
// get all of the products elements
XmlNodeList nodeList = doc.SelectNodes("//XMLProducts/Products");
textBox1.Text = "";
foreach (XmlNode node in nodeList)
{
    textBox1.Text += node.InnerXml + "\r\n";
}
```

代码片段 frmADOXML.cs

![](img/d7d2ffa0a76feaab821930e95daace93_989_0.png)

图 33-5

XmlDataDocument 基于 XmlDocument 类，因此具有 XmlDocument 类的所有功能。主要区别之一在于 XmlDataDocument 具有重载的构造函数。注意实例化 XmlDataDocument (doc) 的代码行：

```
doc = new XmlDataDocument(ds);
```

它将您创建的 DataSet 对象 ds 作为参数传入。这会根据 DataSet 创建 XML 文档，因此您不必使用 Load() 方法。实际上，如果您在实例化新的 XmlDataDocument 对象时没有传入 DataSet 作为参数，那么它将包含一个名为 NewDataSet 的 DataSet，其 tables 集合中没有 DataTables。此外，还有一个 DataSet 属性，您可以在创建基于 XmlDataDocument 的对象后对其进行设置。

假设您在调用 DataSet.Fill() 之后添加以下代码行：

```
ds.WriteXml("c:\\test\\sample.xml", XmlWriteMode.WriteSchema);
```

在这种情况下，将在 c:\test 文件夹中生成以下 XML 文件 sample.xml：

```
<?xml version="1.0" standalone="yes"?>
<XMLProducts>
  <xs:schema id="XMLProducts" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">
    <xs:element name="XMLProducts" msdata:IsDataSet="true" msdata:UseCurrentLocale="true">
      <xs:complexType>
        <xs:choice minOccurs="0" maxOccurs="unbounded">
          <xs:element name="Products">
            <xs:complexType>
              <xs:sequence>
                <xs:element name="Name" type="xs:string" minOccurs="0" />
                <xs:element name="StandardCost" type="xs:decimal" minOccurs="0" />
              </xs:sequence>
            </xs:complexType>
          </xs:element>
        </xs:choice>
      </xs:complexType>
    </xs:element>
  </xs:schema>
  <Products>
    <Name>Hill Road Frame-Black, 58</Name>
    <StandardCost>1059.3100</StandardCost>
  </Products>
  <Products>
    <Name>Hill Road Frame-Red, 58</Name>
    <StandardCost>1059.3100</StandardCost>
  </Products>
  <Products>
    <Name>Sport-100 Helmet, Red</Name>
    <StandardCost>13.0863</StandardCost>
  </Products>
</XMLProducts>
```

这里只显示了前几个 Products 元素。实际的 XML 文件将包含 Northwind 数据库 Products 表中的所有产品。

### 转换关系数据

对于单个表来说，这看起来非常简单，但如果是关系数据呢？例如 DataSet 中有多个 DataTable 和 Relation。这些仍然以相同的方式工作。下面是一个使用两个相关表的示例：

```
private void button5_Click(object sender, EventArgs e)
{
    XmlDocument doc = new XmlDocument();
    DataSet ds = new DataSet("XMLProducts");
    SqlConnection conn = new SqlConnection(_connectString);

    SqlDataAdapter daProduct = new SqlDataAdapter
        ("SELECT Name, StandardCost, ProductCategoryID FROM SalesLT.Product", conn);
    SqlDataAdapter daCategory = new SqlDataAdapter
        ("SELECT ProductCategoryID, Name FROM SalesLT.ProductCategory", conn);

    // Fill DataSet from both SqlAdapters
    daProduct.Fill(ds, "Products");
    daCategory.Fill(ds, "Categories");

    // Add the relation
    ds.Relations.Add(ds.Tables["Categories"].Columns["ProductCategoryID"],
                     ds.Tables["Products"].Columns["ProductCategoryID"]);

    // Write the Xml to a file so we can look at it later
    ds.WriteXml("Products.xml", XmlWriteMode.WriteSchema);

    // load data into grid
    dataGridView1.DataSource = ds.Tables[0];

    // create the XmlDataDocument
    doc = new XmlDataDocument(ds);

    // Select the product name elements and load them in the grid
    XmlNodeList nodeList = doc.SelectNodes("//XMLProducts/Products");
    textBox1.Text = "";
    foreach (XmlNode node in nodeList)
    {
        textBox1.Text += node.InnerXml + "\r\n";
    }
}
```

代码片段 frmADOXML.cs

在您创建的示例中，XMLProducts DataSet 中有两个 DataTable：Products 和 Categories。您在这两个表的 ProductCategoryID 列上创建了一个新关系。

通过使用与上一个示例相同的 WriteXml() 方法调用，您将获得以下 XML 文件（SuppProd.xml）：

```
<?xml version="1.0" standalone="yes"?>
<XMLProducts xmlns="" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">
  <xs:schema id="XMLProducts" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" msdata:IsDataSet="true" msdata:UseCurrentLocale="true">
    <xs:complexType name="XMLProducts">
      <xs:choice minOccurs="0" maxOccurs="unbounded">
        <xs:element name="Products">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="Name" type="xs:string" minOccurs="0" />
              <xs:element name="StandardCost" type="xs:decimal" minOccurs="0" />
              <xs:element name="ProductCategoryID" type="xs:int" minOccurs="0" />
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="Categories">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="ProductCategoryID" type="xs:int" minOccurs="0" />
              <xs:element name="Name" type="xs:string" minOccurs="0" />
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:choice>
    </xs:complexType>
    <xs:unique name="Constraint1">
      <xs:selector xpath=".//Categories" />
    </xs:unique>
  </xs:schema>
</XMLProducts>
```
