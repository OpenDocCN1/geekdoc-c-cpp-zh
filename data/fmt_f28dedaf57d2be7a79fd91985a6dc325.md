
```csharp
internal sealed class DNRequestTrackingBehavior: IServiceBehavior
{
    public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
        ServiceBase serviceBase)
    {
        var workflowService = serviceBase as WorkflowServiceHost;
        if (workflowService == null) return;
        var tracker = new DNRequestTrackingParticipant();
        workflowService.WorkflowExtensions.Add(tracker);
    }

    public void AddBindingParameters(ServiceDescription serviceDescription,
        ServiceBase serviceBase,
        Collection<Endpoint> endpoints,
        BindingParameterCollection bindingParameters)
    {
    }

    public void Validate(ServiceDescription serviceDescription,
        ServiceBase serviceBase)
    {
    }
}
```

*DNRequestTrackingParticipant.cs 可可在 Wrox.com 下载。*

该类实现了 `System.ServiceModel.Description` 命名空间的 `IServiceBehavior` 接口。此接口可以在 `System.ServiceModel.dll` 程序集中找到，因此它是 WCF 的一部分。此行为仅使用 `ApplyDispatchBehavior` 方法，该方法显式地将 `DNRequestTrackingParticipant` 添加到服务主机的 `WorkflowExtensions` 集合中。这将实体注入任何新的工作流实例。

## 运行应用程序

应用程序已就绪。启动后，你可以添加请求。审批过程大约需要 10 秒，新请求大约在 10 秒后变为已批准或拒绝。图 11-28 显示了应用程序的运行情况。

你可以尝试发送多个请求。当你查询 `DNRequestTracking` 表时，你会发现每个审批工作流占用一个独立的工作流实例，并且工作流处理重叠请求也是并行的。

![](img/b5597c749e848b27b0d305153ae1610_602_0.png)

图 11-28：运行中的应用程序

## 总结 (SUMMARY)

WF 4.0 不仅仅是 WF 3.5 的简单增强。它经过了完全的重新设计和编写。它现在使用 XAML 工作流，并提供了一个基于 WPF 的设计器，可以处理比以前版本更大的工作流。

WF 4.0 使用了一种全新的架构，工作流和活动具有共同的根对象 (`System.Activities.Activity`)。通过这种模型，你可以描述顺序和流程图的工作流，甚至可以将它们混合。.NET Framework 4.0 附的活动库包含约 40 个新活动，你也可以轻松地开发自己的自定义活动。

WF 4.0 为补偿事务模型提供了强大的支持，并允许你在几分钟内创建工作流服务。工作流模型是可扩展的。你可以为工作流跟踪创建扩展，还可以注入自己的自定义扩展。

第 12 章重点关注 .NET Data Framework 的增强，包括语言集成查询 (`LINQ`)、实体框架和实体数据源控制。

除了当 `LINQ` 作为 ORM 工具使用时具有的优势外，`LINQ` 还可以用于任何对数组或集合进行内存中的操作，用以对记录进行搜索、过滤和排序。

> 注意，任何针对公共语言运行时 (`CLR`) 的语言都对 `LINQ` 有内置支持。因此，你可以使用 C#、F 和 Visual Basic (`VB`) 9 来编写你的 `LINQ` 查询。

# LINQ 运算符

*运算符*（operator）是作用于*操作数*（operand）以执行特定操作的符号。`LINQ` 中有很多运算符来方便操作。

`System.Query` 命名空间下的 `System.Sequence` 静态类由一组静态方法组成。这些方法通常被称为*标准查询运算符*，分为以下类型：

- 用于 `IEnumerable(T)` 的标准查询运算符作用于实现了 `IEnumerable(T)` 接口的对象

- 用于 `IQueryable(T)` 的标准查询运算符作用于实现了 `IQueryable(T)` 接口的对象

表 12-1 显示了 `LINQ` 运算符及其分类。

| 运算符类型 | 运算符 |
| --- | --- |
| 聚合 | Aggregate, Average, Count, LongCount, Max, Min, Sum |
| 转换 | Cast, OfType, ToArray, ToDictionary, ToList, ToLookup, ToSequence |
| 运算符类型 | 运算符 |
|---|---|---|
| 元素 | DefaultIsEmpty<br>ElementAt<br>ElementAtOrDefault<br>First<br>FirstOrDefault<br>Last<br>LastOrDefault<br>Single<br>SingleOrDefault |
| 等等 | EqualAll |
| 生成 | Empty<br>Range<br>Repeat |
| 分组 | GroupBy<br>GroupJoin |
| 链接 | Join |
| 排序 | OrderBy<br>ThenBy<br>OrderByDescending<br>ThenByDescending<br>Reverse |
| 分区 | Skip<br>SkipWhile<br>Take<br>TakeWhile |
| 量化 | All<br>Any<br>Contains |
| 限制 | Where |
| 选择 | Select<br>SelectMany |

# 表 12.1（续）

| 运算符类型 | 运算符 |
| --- | --- |
|  | Concat<br>Distinct<br>Except<br>Intersect<br>Union |

使用 `LINQ`，你可以轻松地查询和组织列表中的项目，过滤特定的列表项目或项目，甚至将对象转换为其他对象。以下示例展示了这些概念中的：

```csharp
String[] cities = {"London", "New York", "New Delhi", "Tokyo", "Paris"};
// 按名称排序项目
var sortedResults = from x in cities
    orderby x
    select x;
// 查找以 New 开头的城市
var newCities = from x in cities
    where x.StartsWith("New")
    select x;
```

```csharp
// 输出结果
Console.WriteLine("Sorted")
foreach (var city in sortedResults)
    Console.WriteLine(city);
Console.WriteLine("Filtered")
foreach (var city in newCities)
    Console.WriteLine(city);
```

从这些示例中你可以看到，`LINQ` 查询的基本结构以 `from` 开始。你定义了一个别名来表示所查询集合中的项。在这些示例中，使用 `x` 来表示单个城市。对于 `LINQ` 查询的其余部分，Visual Studio 为查询对象可用的属性和方法提供了完整的 IntelliSense 支持。示例查询的后续部分是限制性的 `where` 子句，或者是用于重新排序列表的 `orderby` 子句。

这只是 `LINQ` 力量的一角，以及它在处理内存中的对象时如何简化操作。

# LINQ 实现

`LINQ` 已实现用于多种数据源和对象源。最常见的实现包括：

- `LINQ to Objects`

- `LINQ to XML`

- `LINQ to DataSet`

- `LINQ to SQL`

- `LINQ to Entities`

# LINQ to Objects

`LINQ to Objects` 是 `LINQ` 的一种实现，可用于查询内存中的对象或内存对象集合。注意，此类对象或此类对象的集合应该是类型 `T:System.Collections.IEnumerable` 或 `T:System.Collections.Generic`。

让我们来看看如何使用 `LINQ to Objects` 来查询内存中的对象集合。考虑以下类：

```csharp
public class Product
{
    public int ProductID { get; set; }
    public string ProductName { get; set; }
    public string ProductType { get; set; }
    public int Quantity { get; set; }
}
```

以下代码段说明了如何填充一个 `Product` 类型的 `List` 并返回它：

```csharp
static List<Product> PopulateData()
{
    List<Product> products = new List<Product>();
    products.Add(new Product { ProductID = 1, ProductName = "Laptop", ProductType = "Laptop", Quantity = 100 });
    products.Add(new Product { ProductID = 2, ProductName = "Compa", ProductType = "Laptop", Quantity = 150 });
    products.Add(new Product { ProductID = 3, ProductName = "Dell", ProductType = "Laptop", Quantity = 200 });
    products.Add(new Product { ProductID = 4, ProductName = "HCL", ProductType = "Laptop", Quantity = 150 });
    products.Add(new Product { ProductID = 5, ProductName = "Acer", ProductType = "Laptop", Quantity = 200 });
    return products;
}
```

你可以使用 `LINQ to Objects` 根据产品名称对此列表进行排序并输出列表进行审查：

```csharp
List<Product> products = PopulateData();
var sortedResults = from x in products
                    orderby x.ProductName
                    select x;
foreach (var p in sortedResults)
{
    Console.WriteLine(p.ProductName);
}
```

如你所看到的，这是对之前使用字符串数组示例的简单扩展。这允许你们所有人访问类的单个属性，然后可以对其进行过滤、排序或其他处理。

# LINQ to XML

以前被称为 `LINQ to XML` 的 `LINQ to XML` 是一个可以用于查询 XML 数据源的 API。它可以将你的 `LINQ` 查询映射到数据源。以下片段显示了一个名为 `Products.xml` 的 XML 文档：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Products>
  <Product>
    <ProductID>1</ProductID>
    <ProductName>Lenovo</ProductName>
    <ProductType>Laptop</ProductType>
    <Quantity>100</Quantity>
  </Product>
  <Product>
    <ProductID>2</ProductID>
    <ProductName>Compa</ProductName>
    <ProductType>Laptop</ProductType>
    <Quantity>150</Quantity>
  </Product>
  <Product>
    <ProductID>3</ProductID>
    <ProductName>DELL</ProductName>
    <ProductType>Laptop</ProductType>
    <Quantity>200</Quantity>
  </Product>
  <Product>
    <ProductID>4</ProductID>
    <ProductName>HCL</ProductName>
    <ProductType>Laptop</ProductType>
    <Quantity>150</Quantity>
  </Product>
  <Product>
    <ProductID>5</ProductID>
    <ProductName>Acer</ProductName>
    <ProductType>Laptop</ProductType>
    <Quantity>200</Quantity>
  </Product>
</Products>
```

使用 `LINQ to XML`，你可以像处理任何其他对象一样加载和查询此文档。它为处理工作提供了一个简单的接口。以下片段显示了如何在不需要 XPath 的情况下获取数量大于 150 的项：

```csharp
XDocument productDocument = XDocument.Load("myfile.xml");
var result = from x in productDocument.Descendants("Product")
             where (int)x.Element("Quantity") > 150
             select (string)x.Element("ProductType") + " " +
             (string)x.Element("ProductName");
foreach(string element in result)
    Console.WriteLine(element);
```

这个示例看起来很复杂，但如果你查看组件，它应该是很容易理解的。第一行代码加载了 `myfile`。`XDocument` 对象允许 `LINQ` 查询操作 "Products" 域。第三行代码使用 `Element` 方法进行查询以获取 `Quantity` 元素。第四行代码定义了查询结果，它是 `ProductType`，后面跟着空格，然后使用 `ProductName`。这产生了字符串数组，指示匹配的元素。最后几行代码用于输出结果。

在处理包含属性的文档时，可以使用 `Attribute` 方法获取特定属性，如之前的示例所示。如果你需要在复杂的文档结构中向上或向下移动，可以链用 `Element` 方法。考虑：

```csharp
x.Element("MyElement").Element("MyChild")
```

这将获取 `MyElement` 节点中的 `Child`节点。

# LINQ to DataSet

`LINQ to DataSet` 是一种实现，用于查询 `DataSet` 或 `DataTable` 实例的数据。例如，假设你有以下加载到 `DataTable` 的代码：

```csharp
static DataTable PopulateData() {
    DataTable products = new DataTable();
    products.Columns.Add("ProductID", typeof(Int32));
    products.Columns.Add("ProductName", typeof(String));
    products.Columns.Add("ProductType", typeof(String));
    products.Columns.Add("Quantity", typeof(Int32));
    products.Rows.Add(1, "Dell", "Laptop", 100);
    products.Rows.Add(1, "Compaq", "Laptop", 150);
    products.Rows.Add(1, "DEL", "Laptop", 200);
    products.Rows.Add(1, "HCL", "Laptop", 150);
    products.Rows.Add(1, "Acer", "Laptop", 200);
    products.Rows.Add(1, "Test", "TV", 200);
    return products;
}
```

通过使用 `LINQ to DataSet`，你可以使用以下片段查询此 `DataTable` 并返回笔记本电脑：
