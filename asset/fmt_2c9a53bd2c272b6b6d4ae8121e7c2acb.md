
```csharp
var queryableDS = PopulateData().AsEnumerable();
var result = from record in queryableDS
where record["ProductType"] == "Laptop"
```

```csharp
select record;
foreach (var product in result)
    Console.WriteLine(product["ProductName"]);
```

查询 `DataTable`/`DataSet` 的过程略有不同，它需要调用 `AsEnumerable()` 来获取可以被 LINQ 系统交互的帧结果。在之前的示例中，第一行被拆分出来是为了更准确地说明这一概念。然而，在 LINQ 语句第一行的 `in` 之后调用 `PopulateData().AsEnumerable()` 是完全有效的。

对于 LINQ 语句的剩余部分，语法应该类似于你使用标准数组访问器获取单个字段的方法——首先通过 `where` 子句选择类型，然后通过 `select` 返回实体。

## LINQ to SQL

LINQ to SQL 以前被称为 DLIN，它是 LINQ 的一种实现，可用于查询 SQL Server 数据库的数据。它与任何其他用于从 SQL Server 数据库检索数据的 ORM 工具一样。

要使用 LINQ to SQL，你必须创建一个 `DataContext`。`DataContext` 实际上是 LINQ to SQL 查询的网关。它接受 LINQ 查询作为输入，然后处理这些查询以生成相应的语句。

在 LINQ to SQL 中创建 `DataContext`，请遵循以下步骤：

1. 在解决方案管理器（Solution Explorer）中右键点击项目，并选择“添加新项”。

2. 从显示的模板列表中，选择“LINQ to SQL Classes”，如图 12-1 所示。

![](img/b5597c749e848b27b0d305153ae16106_611_0.png)

图 12-1：创建新的 LINQ 数据上下文

3. 为 `DataContext` 提供一个名称并点击确定。

4. 拖放你需要的表（在本示例中，它是 AdventureWorks 数据库的 `Product` 表，如图 12-2 所示）。

![](img/b5597c749e848b27b0d305153ae16106_612_0.png)

图 12：服务器资源管理器

一旦创建了 `DataContext`，你就可以使用 LINQ 查询数据，如下代码段所示：

```csharp
WroxDataContext dataContext = new WroxDataContext();
var result = from p in dataContext.select p;
foreach (var v in result)
    Console.WriteLine(v.Name);
```

在 SQL 中处理 LINQ 非常简单，因为生成的数据上下文是强类型的，就像你处理手动创建的对象一样。因此，所有查询函数都可以完成，就像数据库中的每一列都存在对应的公共属性一样。

一个需要注意的重要点是，LINQ to SQL 特有的特点是查询在开始枚举结果之前是不会执行的。因此，如果你有一个 LINQ 语句，在处理结果之前有十行代码，那么查询的执行将延迟到查询执行时刻。此外，鉴于这种行为，结果的每次迭代都会导致执行一个新的数据库查询。

在下面的示例中，`Products` 表的全部内容被返回两次，对应每个 `foreach` 语句：

```csharp
WroxDataContext dataContext = new WroxDataContext();
var result = from p in dataContext.Products select p;
foreach (var v in result)
    Console.WriteLine(v.Name);
foreach (var v in result)
    Console.WriteLine(v.Name);
```

你可以通过将结果转换为列表或数组来消除这一局限性。这将执行查询并将结果放入内存中。下面的示例执行了一次查询：

```csharp
WroxDataContext dataContext = new WroxDataContext();
var result = from p in dataContext.Products select p;
var list = result.ToList();
foreach (var v in list)
    Console.WriteLine(v.Name);
foreach (var v in list)
    Console.WriteLine(v.Name);
```

这里最后需要注意的是，由于 LINQ to SQL 的延迟执行模型，它的用处在于执行复杂的条件查询，并确保实际执行时包含正确的数据。

例如，考虑以下情况：

```csharp
var result = from p in dataContext.products select p;
if(orderByProduct) //变量在别处声明
    result = from r in result order by r;
foreach (var item in result)
    Console.WriteLine(item.Name);
```

## 并行 LINQ (PLINQ)

并行 LINQ (PLINQ) 是 LINQ 的扩展，允许并行执行查询。这对于大型数据集特别有用，因为处理可以分布在多个 CPU 核心上。

要使用 PLINQ，你只需要在 LINQ 查询上调用 `AsParallel()` 方法。例如：

```csharp
var result = from p in dataContext.Products.AsParallel() select p;
```

列表 12-1 显示了典型 EDM 在其 XML 视图中的模式。请注意，EDM 示例已删除了所有额外属性。

### 列表 12-1：XML 中的 EDM

```xml
<xml version="1.0" encoding="utf-8"?>
<edmx Version="2.0" xmlns="http://schemas.microsoft.com/ado/
2008/10/edmx">
  <!-- EF Runtime -->
  <edmx>
    <!-- SSL content -->
    <edmx:StorageModel>
      <Schema Namespaces="WroxModel.Store" Alias=
        "Self" Provider="System.Data.SqlClient" xmlns=
        ManifestToken="2008" xmlns="http://schemas.microsoft.com/ado/2007/12/edm"
        SchemaGenerator="http://schemas.microsoft.com/
ado/2009/02/">
      <EntityContainer Name="WroxStoreContainer">
        <EntityTypeSet Name="Product" EntityType=
        "WroxModel.Store.Product" store:type=
        "Tables" Schema="Production" />
      </EntityTypeSet>
      <EntityType Name="Product">
        <Key>
          <Property Name="ProductID" />
        </Key>
        <Property Name="ProductID" Type="int" Nullable="false"
        StoreGenerated="Identity" />
        <Property Name="ModifiedDate" Type="datetime" Nullable="false" />
      </EntityType>
      </Schema>
    </edmx:StorageModel>
    <!-- Conceptual Models -->
    <edmx:ConceptualModels>
      <Schema Name="WroxModel" Alias="self"
        xmlns="http://schemas.microsoft.com/ado/2009/02/edm"
        xmlns:annotation="http://schemas.microsoft.com/ado/2008/09/edm">
      <EntityContainer Name="WroxEntities" annotation:LazyLoadingEnabled="true">
        <EntityTypeSet Name="Products" EntityType="WroxModel.Product" />
      </EntityContainer>
      <EntityType Name="Product">
        <Key>
          <PropertyRef Name="ProductID" />
        </Key>
        <Property Name="ProductID" Type="Int32" Nullable="false"
        annotation:StoreGenerated="Identity" />
      </EntityType>
      </Schema>
    </edmx:ConceptualModels>
  <!-- C-S mapping -->
  <edmx:Mappings>
```

```xml
<Mapping Space="C-S" xmlns=
http://schemas.microsoft.com/ado/2008/09/mapping/cs">
<EntityContainerMapping Name="WroxStoreContainer
EntityContainer="WroxEntities">
<EntitySetMapping Name="Products"><EntityTypeMapping TypeName=
nWroxModel.Product"><MappingFragment StoreEntitySet="Product">
<ScalarProperty Name="ProductID" ColumnName="ProductID" />
</MappingFragment></EntityTypeMapping></EntitySetMapping>
</EntityContainerMapping>
</Mapping>
<edmx:
<edmx:Runtime>
<!-- Designer content (不要在此手动编辑) -->
<Designer xmlns="http://schemas.microsoft.com/ado/2008/10/edmx">
<Connection>
<DesignerInfoProperty>
<DesignerProperty Name="MetadataArtifactProcessing" Value=
EmbeddedOutputAssembly" />
</DesignerInfoProperty>
<Options>
<DesignerInfoPropertyGroup>
<DesignerProperty Name="ValidateOnBuild" Value="true" />
<DesignerProperty Name="EnablePluralization" Value="true" />
<DesignerProperty Name="IncludeForeignKeyKeysInModel" Value="True" />
</DesignerInfoPropertyGroup>
</Options>
<Diagram>
<!-- Diagram (形状和连接器位置) -->
<Diagram Name="WroxModel" ZoomLevel="73">
<EntityTypeShape Type="WroxModel.Product" Width=
2.625 PointX="0.75" PointY="0.75" Height=
5.043600260416656 IsExpanded=
true" /></Diagram></Diagram>
</Designer>
</edmx:
```

## LINQ to Entities

LINQ to Entities 实现 LINQ 是一种 API，你可以以强类型的方式查询 EDM 暴露的数据。

以下代码段是 LINQ to Entities 查询的示例：

```csharp
WroxModel.WroxEntities context = new WroxModel.WroxEntities();
var result = from product in context.Products
select product;
foreach (var p in result)
Console.WriteLine(p.ProductName);
```

从这里可以看出，EDM 被创建了，允许查询像其他类型的 LINQ 查询一样查询实体。

## Entity Client

Entity Client 是一种提供程序，充当 Entity Framework 中实体级查询的网关。你可以使用此提供程序使用 Entity SQL 编写查询，对 EDM 暴露的数据执行 CRUD（创建、读取、更新、删除）操作。

## Entity SQL

像 T-SQL 一样，Entity SQL 是一种独立于数据存储的查询语言，你可以用它对 EDM 暴露的数据执行 CRUD 操作。它不像 LINQ 那样是强类型的，你可以用它来组合或构建你的动态查询并执行它们。

以下代码段说明了如何使用 Entity SQL：

```csharp
using (EntityConnection entityConnection = new EntityConnection("Name=WroxEntities"))
{
    try
    {
        EntityCommand entityCommand = entityConnection.CreateCommand();
        entityCommand.CommandText = "WroxEntities.AddNew";
        entityCommand.CommandType = CommandType.StoredProcedure;
        entityCommand.Parameters.AddWithValue("ProductID", 2);
        entityCommand.Parameters.AddWithValue("ProductName", "DELL");
        entityCommand.Parameters.AddWithValue("Quantity", 150);
        entityCommand.ExecuteNonQuery();
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error: " + ex.ToString());
    }
}
```

## Object Services

Object Services 是一种 API，允许你作为内存对象处理 EDM 暴露的内容。此外，Object Services 提供了以下功能：

- 跟踪

- 延迟加载

- 继承

- 乐观并发

你还可以使用 Object Services 通过 Entity SQL 或 LINQ to Entities 查询。

以下代码段显示了如何使用 Object Services：

```csharp
using (ObjectContext context = new ObjectContext("Name=WroxEntities"))
{
    var result = from p in context.CreateQuery<WroxModel.Product>("WroxEntities") select p;
    foreach (WroxModel.Product product in result)
    {
        Console.WriteLine(product.ProductName);
    }
}
```

## ENTITY DATA SOURCE CONTROL

Entity Data Source 控制是 Visual Studio 2008 Beta 1 中引入的新数据源控件。它现在是 Visual Studio 2010的一部分，用于检索 EDM 暴露的数据。

以下是 Entity Data Source 控制在标记中的示例：

```asp
<asp:EntityDataSource Id="EntityDataSource" runat="server" ConnectionString="name=WroxEntities" DefaultContainerName="WroxEntities" EntityName="WroxEntities.Product" />
```

### 总结

本章提供了 .NET 数据框架的概述。讨论了两种 ORM 技术——LINQ to SQL 和 Entity Framework，并为各自提供了相应的适用场景。对 LINQ 提供了更广泛的概述以及多个示例。
