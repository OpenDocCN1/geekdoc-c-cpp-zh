
当用户点击某个动态超链接时，页面模板通常需要从请求查询字符串中提取列值。这一操作通过 GetColumnValuesFromRoute 方法完成，该方法用于列表页模板；而 GetDataKeyFromRoute 方法则对单项模板执行相同的操作。

```
public virtual string GetDisplayString(object row);
```

当需要表示某行或某个实体的可读字符串时，可以使用 GetDisplayString 方法。ForeignKey 字段和筛选模板正是通过该方法为其 DropDownList 控件中的 ListItem 对象设置 Text 属性。该方法会考虑 MetaTable 的 DisplayColumn，以定位其值将用作显示字符串的列。

```
public string GetPrimaryKeyString(IList<object> primaryKeyValues);
public string GetPrimaryKeyString(object row);
```

如果需要使用某个字符串来唯一标识实体，以便日后从数据库检索该实体，可以使用 GetPrimaryKeyString 的重载之一。ForeignKey 字段和筛选模板正是通过这种方式为其 DropDownList 控件中的 ListItem 对象生成 Value 属性。

## 安全支持

最后但同样重要的是，MetaTable 类包含一组可用于实现表级授权的虚拟方法。这些方法的默认实现返回 true，因此只要表已搭建，所有用户都可以访问所有表。第 14 章将讨论 Dynamic Data 应用程序如何利用这一扩展机制来实现基于角色的 UI 裁剪：

```
public virtual bool CanDelete(IPrincipal principal);
public virtual bool CanInsert(IPrincipal principal);
public virtual bool CanRead(IPrincipal principal);
public virtual bool CanUpdate(IPrincipal principal);
```

## MetaColumn 类

MetaColumn 类描述实体类的单个属性。在 Northwind 数据模型中，Product 实体类表示 Products 数据库表，Dynamic Data 会为 Product 实体类定义的每个属性创建单独的 MetaColumn 类实例，包括基本属性（如 ProductID、ProductName、CategoryID 和 SupplierID）以及导航属性（如 Category 和 Supplier）。

实体类的导航属性由继承自 MetaColumn 类的 MetaForeignKeyColumn 和 MetaChildrenColumn 类表示。这些类将在本章后续部分讨论；本节重点介绍所有元列及其专用派生类的常见属性。

## 属性定义

.NET 属性由其名称、类型以及 getter 和 setter 的可访问性来定义。

```csharp
public string Name { get; }
```

MetaColumn 类的 Name 属性返回实体属性的名称。它是一个原始的内部字符串，可用于标识该列，但可能不适合直接展示给最终用户。

```csharp
public Type ColumnType { get; }
public TypeCode TypeCode { get; }
```

ColumnType 属性返回一个 Type 对象，表示实体属性的 .NET 类型。对于 Product 实体的 ProductName 属性，该值将是 typeof(string)。而 TypeCode 属性则返回 TypeCode 枚举的成员之一，对于 ProductName 列，该值将是 TypeCode.String。

```csharp
public bool IsBinaryData { get; }
public bool IsFloatingPoint { get; }
public bool IsInteger { get; }
public bool IsLongString { get; }
public bool IsString { get; }
```

还提供了一组便捷属性，用于确定属性数据类型的高层级分组。例如，IsFloatingPoint 属性对于 Float、Double 和 Decimal 列返回 true；IsInteger 属性对 Byte、Int16、Int32 和 Int64 列也有类似作用。如果字符串的 MaxLength 超过十亿个字符（确切地说是 1,073,741,819），IsLongString 属性将返回 true。实际上，这意味着 memo 列（Microsoft SQL Server 中的 TEXT 和 NTEXT），并决定默认情况下是否为此列使用 MultiLineText 字段模板。

```csharp
public int MaxLength { get; }
```

对于二进制列和字符串列，MaxLength 属性返回数据模型中列值允许的最大长度。例如，Products 表的 ProductName 列限制为 40 个字符，MaxLength 属性默认将返回 40。

```csharp
using System.ComponentModel.DataAnnotations;

[MetadataType(typeof(Product.Metadata))]
partial class Product
{
    public class Metadata
    {
        [StringLength(32)]
        public object ProductName { get; set; }
    }
}
```

不过，也可以通过代码中向实体属性应用 StringLengthAttribute 来更改 MaxLength 属性，如上所示。

```csharp
public virtual bool IsReadOnly { get; }
```

如果实体属性值无法由用户设置，MetaColumn 类的 IsReadOnly 属性返回 true。如果属性的 setter 不可访问或不存在，则该属性可能是只读的。后一种情况不适用于由 Entity Framework 和 LINQ to SQL 生成的实体类，这些类中的属性必须具有 setter，框架才能根据从数据库检索到的信息设置其值。然而，这两种框架都支持较低可见性（protected 或 internal）的属性 setter。

除了更改模型中实体属性的定义外，还可以通过应用 System.ComponentModel.DataAnnotations 命名空间中定义的 EditableAttribute 来使其成为只读。

```csharp
using System.ComponentModel.DataAnnotations;
```

```csharp
[MetadataType(typeof(Product.Metadata))]
partial class Product
{
    public class Metadata
    {
        [Editable(false)]
        public object ProductName { get; set; }
    }
}
```

您还可以通过应用 System.ComponentModel 命名空间中定义的 ReadOnlyAttribute 来达到相同的效果，并使属性对于 Dynamic Data 而言为只读。不过，EditableAttribute 还允许提供额外的元数据信息，以便在插入和更新模式下分别允许编辑。

```csharp
public PropertyInfo EntityTypeProperty { get; }
```

MetaColumn 类的 EntityTypeProperty 返回 System.Reflection 命名空间中定义的 PropertyInfo 类的实例。PropertyInfo 包含描述该属性的低级 .NET 元数据。它还允许您通过调用 PropertyInfo 类的 GetValue 和 SetValue 方法动态获取或设置实体属性的值。

```csharp
public ColumnProvider Provider { get; }
```

MetaColumn 类的 Provider 属性返回原始的 ColumnProvider，该提供程序用于根据元数据提供程序从数据模型中提取的信息创建当前 MetaColumn 实例。虽然您通常不需要直接访问底层列提供程序，但可以通过此属性访问它。

## 属性种类

除了实体属性的名称和类型之外，Dynamic Data 还需要知道它是什么种类的属性，也就是说，该属性是否在实体类中扮演特殊角色。

```csharp
public bool IsPrimaryKey { get; }
```

对于属于实体主键一部分的实体属性，MetaColumn 类的 IsPrimaryKey 属性返回 true。如今数据库设计中广泛使用代理主键，因此大多数实体类的主键只有一个属性。不过，也支持复合主键。可以使用 MetaTable 类的 PrimaryKeyColumns 属性快速访问主键列。

> **注意**
> 实体类必须具有主键，Entity Framework 和 LINQ to SQL 才能更新其数据库表中的行。在将现有数据库反向工程为数据模型时，Visual Studio 可以自动确定表的主键，但无法确定视图的主键。如果您的数据模型必须包含视图，则可能需要手动编辑模型以提供有关主键的缺失信息。

```csharp
public bool IsForeignKeyComponent { get; }
```

对于属于一个或多个导航外键属性组成部分的基本属性，MetaColumn 类的 IsForeignKeyComponent 属性返回 true。例如，Product 实体的 SupplierID 属性是 Supplier 导航属性所表示的外键的组成部分，描述 SupplierID 属性的 MetaColumn 对象的 IsForeignKeyComponent 属性返回 true。

外键组件属性在 Dynamic Data 应用程序中具有特殊含义，因为在正常情况下它们不应呈现给用户。提供一个用于以原始整数形式输入 SupplierID 值的 TextBox 并没有多大帮助。相反，导航属性（此处为 Supplier）会以 DropDownList 或其他适当的控件呈现，用户可以通过它们选择供应商，而不必输入其 ID。

```csharp
public bool IsGenerated { get; }
```

MetaColumn 类的 IsGenerated 属性对于其值由数据库服务器自动生成的属性返回 true。对于 Microsoft SQL Server，这包括 IDENTITY 列，服务器会为每一
