
以下代码创建一个 DataTable，它对应于图 30-6 中所示的架构（但未涵盖列的可空性）：

```csharp
public static void ManufactureProductDataTable(DataSet ds)
{
    DataTable products = new DataTable("Products");
    products.Columns.Add(new DataColumn("ProductID", typeof(int)));
    products.Columns.Add(new DataColumn("ProductName", typeof(string)));
    products.Columns.Add(new DataColumn("SupplierID", typeof(int)));
    products.Columns.Add(new DataColumn("CategoryID", typeof(int)));
    products.Columns.Add(new DataColumn("QuantityPerUnit", typeof(string)));
    products.Columns.Add(new DataColumn("UnitPrice", typeof(decimal)));
    products.Columns.Add(new DataColumn("UnitsInStock", typeof(short)));
    products.Columns.Add(new DataColumn("UnitsOnOrder", typeof(short)));
    products.Columns.Add(new DataColumn("ReorderLevel", typeof(short)));
    products.Columns.Add(new DataColumn("Discontinued", typeof(bool)));
    ds.Tables.Add(products);
}
```

[代码下载 ManufacturedDataSet.cs](ManufacturedDataSet.cs)

你可以修改 DataRow 示例中的代码，以使用这个新生成的表定义，如下所示：

```csharp
string source = "server=(local); " + "integrated security=sspi;" + "database=Northwind";
string select = "SELECT * FROM Products";
SqlConnection conn = new SqlConnection(source);
SqlDataAdapter cmd = new SqlDataAdapter(select, conn);
DataSet ds = new DataSet();
ManufactureProductDataTable(ds);
cmd.Fill(ds, "Products");
foreach(DataRow row in ds.Tables["Products"].Rows)
{
    Console.WriteLine("{0} from {1}", row[0], row[1]);
}
```

ManufactureProductDataTable 方法创建一个新的 DataTable，依次添加每个列，最后将其追加到 DataSet 中的表列表中。DataSet 有一个索引器，它接受表的名称并将该 DataTable 返回给调用方。

前面的示例仍然不是真正类型安全的，因为在列上使用了索引器来检索数据。更好的做法是从 DataSet、DataTable 和 DataRow 派生一个类（或一组类），为表、行和列定义类型安全的访问器。你可以自己生成这些代码；这并不特别繁琐，而且最终会得到真正类型安全的数据访问类。

如果你不喜欢自己生成这些类型安全的类，现成的帮助就在手边。.NET Framework 支持本节开头列出的第三种方法：使用 XML 架构来定义 DataSet 类、DataTable 类以及我们在此描述的其他类。（有关此方法的更多详细信息，请参阅本章后面的“XML 架构：使用 XSD 生成代码”一节。）

## 数据关系

编写应用程序时，通常需要获取并缓存各种信息表。DataSet 类就是这些信息的容器。使用常规 OLE DB 时，必须提供一种奇怪的 SQL 方言来强制实现分层数据关系，而且该提供程序本身也并非没有自身的微妙怪癖。

然而，DataSet 类从一开始就被设计为可以轻松地在数据表之间建立关系。本节中的代码演示了如何手动生成数据并填充两个表。因此，即使你无法访问 SQL Server 或 Northwind 数据库，也仍然可以运行此示例：

可以使用两个具有各种重载的方法来检索父行：GetParentRows()（返回零个或多个行的数组）和 GetParentRow()（在给定关系的情况下检索单个父行）。

## 数据约束

更改客户端创建的列的数据类型并非 DataTable 的唯一用途。ADO.NET 允许你在一个或多个列上创建一组约束，然后用这些约束来强制实施数据内的规则。

下表列出了运行时当前支持的约束类型，它们以 System.Data 命名空间中的类体现。

| 约束 | 描述 |
|---|---|
| ForeignKeyConstraint | 在 DataSet 中的两个 DataTable 之间强制建立链接。 |
| UniqueConstraint | 确保给定列中的条目是唯一的。 |

## 设置主键

与关系数据库中的表一样，你可以提供主键，该主键可以基于 DataTable 中的一个或多个列。

以下代码为 Products 表创建一个主键，该表的架构是前面手动构建的。请注意，表上的主键只是约束的一种形式。当向 DataTable 添加主键时，运行时还会在键列上生成一个唯一约束）。这是因为实际上并不存在名为 PrimaryKey 的约束类型——主键只是对一个或多个列的唯一约束。

```csharp
public static void ManufacturePrimaryKey(DataTable dt)
{
    DataColumn[] pk = new DataColumn[1];
    pk[0] = dt.Columns["ProductID"];
    dt.PrimaryKey = pk;
}
```

由于主键可以包含多个列，因此它的类型是 DataColumn 数组。只需将列数组赋值给该属性，即可将表的主键设置为这些列。

## 设置外键

除了唯一约束之外，DataTable 类还可以包含外键约束。这些约束主要用于强制实现主/从关系，但也可以用于在

> 只有当 DataSet 的 EnforceConstraints 属性为 true 时，约束才会在 DataSet 类内部强制执行。

本节介绍了构成 DataSet 类各部分的主要类，并展示了如何在代码中手动生成这些类。你还可以使用 XML 架构文件和 .NET 附带的 XSD 工具来定义 DataTable、DataRow、DataColumn、DataRelation 和 Constraint。下一节将介绍如何设置一个简单的架构并生成用于访问数据的类型安全类。

## XML 架构：使用 XSD 生成代码

XML 在 ADO.NET 中根深蒂固——实际上，在对象之间传递数据的远程处理格式现在就是 XML。借助 .NET 运行时，可以在 XML 架构定义文件 (XSD) 中描述 DataTable 类。此外，你还可以定义整个 DataSet 类，其中包含多个 DataTable 类以及这些表之间的一组关系，并且可以包含各种其他细节来完整描述数据。

定义好 XSD 文件后，运行时中有一个工具可以将此架构转换为相应的数据类，例如前面显示的类型安全的产品 DataTable 类。让我们从一个简单的 XSD 文件（Products.xsd）开始，该文件描述了与前面讨论的 Products 示例相同的信息，然后对其进行扩展以包含一些额外功能：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema id="Products" targetNamespace="http://tempuri.org/XMLSchema1.xsd"
    xmlns="http://tempuri.org/XMLSchema1.xsd"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">
  <xs:element name="Product">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="ProductID" msdata:ReadOnly="true"
          msdata:AutoIncrement="true" type="xs:int" />
        <xs:element name="ProductName" type="xs:string" />
        <xs:element name="SupplierID" type="xs:int" minOccurs="0" />
        <xs:element name="CategoryID" type="xs:int" minOccurs="0" />
        <xs:element name="QuantityPerUnit" type="xs:string" minOccurs="0" />
        <xs:element name="UnitPrice" type="xs:decimal" minOccurs="0" />
        <xs:element name="UnitsInStock" type="xs:short" minOccurs="0" />
        <xs:element name="UnitsOnOrder" type="xs:short" minOccurs="0" />
        <xs:element name="ReorderLevel" type="xs:short" minOccurs="0" />
        <xs:element name="Discontinued" type="xs:boolean" minOccurs="0" />
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

[代码下载 Products.xsd](Products.xsd)

这些选项将在第 33 章中详细讨论；目前，该文件基本上定义了一个 id 属性设置为 Products 的架构。其中定义了一个名为 Product 的复杂类型，它包含许多元素，每个元素对应于 Products 表中的一个字段。

这些项映射到数据类的方式如下。Products 架构映射到从 DataSet 派生的类。Product 复杂类型映射到从 DataTable 派生的类。每个子元素映射到从 DataColumn 派生的类。所有列的集合映射到从 DataRow 派生的类。

