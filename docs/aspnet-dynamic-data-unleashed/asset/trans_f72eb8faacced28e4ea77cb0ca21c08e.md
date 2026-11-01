
你可以使用 MetaTable 类的 Columns 属性访问表列的列表：

```
public ReadOnlyCollection<MetaColumn> Columns { get; }
public MetaColumn GetColumn(string columnName);
public bool TryGetColumn(string columnName, out MetaColumn column);
```

Columns 属性返回一个只读 MetaColumn 对象的集合，这些对象将在本章后面详细讨论。当你需要在运行时获取特定的表列时，最有效的方法是调用 GetColumn 或 TryGetColumn 方法，这些方法利用了 MetaTable 类维护的列内部字典。这比典型的 foreach 循环快得多，在 CPU 是宝贵资源的 Web 应用程序中，这总是件好事。正如你所期望的，如果找不到指定名称的列，GetColumn 方法会抛出异常，而 TryGetColumn 方法则返回 false 且不抛出异常：

```
public TableProvider Provider { get; }
```

各个列对象由 MetaTable 使用表提供程序返回的定义创建，后者从底层数据访问框架中提取信息。虽然通常你应该能够直接通过 MetaTable 和 MetaColumn 对象获取所需的一切，但你也可以选择通过 MetaTable 类的 Provider 属性访问用于创建和配置表的原始提供程序：

```
public Type EntityType { get; }
```

MetaTable 类的 EntityType 属性返回一个 Type 对象，该对象描述实体类，例如 Product。Type 类提供了对描述实体类的 .NET 运行时元数据的访问，包括其属性、方法、事件等。与 MetaTable 类本身相比，通过 Type 类可用的信息非常底层，在 Dynamic Data 应用程序中你很少需要使用它：

```
public Type RootEntityType { get; }
```

另一方面，RootEntityType 属性返回一个 Type 对象，该对象描述实体的根基类。在 NorthwindEntities 数据模型中没有此示例，深入探讨该主题将超出本书范围，但你可以想象一个 CRM 系统，其中实体类 Prospect 和 Customer 从名为 Contact 的公共基类派生。在此场景中，描述 Customer 实体的 MetaTable 将返回 typeof(Customer) 作为 EntityType，并返回 typeof(Contact) 作为 RootEntityType。

> **NOTE**
>
> 在使用派生实体类时，请记住数据模型生成的上下文类没有用于查询 Customers 的单独属性，也没有用于查询 Prospects 的另一个属性。这改变了 Dynamic Data 确定描述这些实体的 MetaTable 实例名称的方式。对于 Contact 这样的基类，MetaTable 名称将是 Contacts，复数形式。然而，对于 Prospect 这样的派生类，MetaTable 名称将是 Prospect，单数形式。

## 数据注释

Entity Framework 和 LINQ to SQL 使用的实体类可以用多种不同的 .NET 属性进行装饰。其中一些属性对 Dynamic Data 有特殊含义，并在 MetaTable 类中表示为不同的属性：

```
public virtual bool Scaffold { get; }
```

MetaTable 类的 Scaffold 属性决定表是否会在 Dynamic Data 生成的页面中可见（或被脚手架化）。这不仅包括仅显示所有表列表的默认主页面，还包括可能包含指向特定表的超链接的页面。例如，如果 Suppliers 表未被脚手架化，你将无法从 Product 详细信息页面导航到它：

```
using System.ComponentModel.DataAnnotations;

[ScaffoldTable(false)]
partial class Supplier { }
```

默认情况下，Scaffold 属性的值由用于注册上下文的 ContextConfiguration 对象的 ScaffoldAllTables 属性的值决定。然而，它也可以通过将 ScaffoldTableAttribute 应用于特定实体类（如上所示）来修改：

```
public virtual bool IsReadOnly { get; }
```

MetaTable 类的 IsReadOnly 属性决定用户是否允许修改它。Visual Studio 中 Dynamic Data 项目创建的页面模板使用此属性隐藏通常允许用户插入、修改和删除表行的链接：

```
using System.ComponentModel;

[ReadOnly(true)]
partial class Supplier { }
```

默认情况下，对于没有主键的表，IsReadOnly 属性返回 true，如果 MetaTable 表示为数据库视图创建的实体类，则可能出现这种情况，对于该视图，Entity Framework 和 LINQ to SQL 无法自动确定主键列。你也可以将 ReadOnlyAttribute 应用于实体类（如上所示），以根据需要显式指定值：

```
public virtual string DisplayName { get; }
```

MetaTable 类的 DisplayName 属性决定当动态生成的网页需要表的可读名称时，Dynamic Data 页面模板显示的文本。默认情况下，DisplayName 属性返回与 Name 属性相同的值。然而，如果表名不友好，例如 Northwind 数据库中的 `Order_Details` 表，可以通过将 DisplayNameAttribute 应用于实体类（如此处所示）来更改它：

```
using System.ComponentModel;

[DisplayName("Order Items")]
partial class Order_Detail { }
```

最后，MetaTable 类有一组三个属性，用于确定从数据库表中检索的实际数据应如何由 Dynamic Data 生成的用户界面元素显示：

```
public virtual MetaColumn DisplayColumn { get; }
public virtual MetaColumn SortColumn { get; }
public virtual bool SortDescending { get; }
```

DisplayColumn 属性返回一个 MetaColumn 对象，该对象表示允许用户识别特定实体实例或表行的属性的值。在 Northwind 数据库场景中，对于 Supplier 实体类，这通常是 CompanyName 属性；对于 Product 实体类，则是 ProductName。只读 ForeignKey 字段模板使用 DisplayColumn 为其生成的超链接提供文本，以便在 Product 详细信息页面上显示 Supplier 的联系人名称。

SortColumn 属性返回一个应默认用于对从数据库检索的项目进行排序的 MetaColumn，而 SortDescending 属性指示行应按 SortColumn 值的升序还是降序排序。ForeignKey_Edit 字段模板使用这些属性对生成的下拉列表控件中的项目进行排序，使 Suppliers 按其 CompanyName 的顺序出现：

```
using System.ComponentModel.DataAnnotations;

[DisplayColumn("CompanyName", "CompanyName", false)]
partial class Supplier { }
```

默认情况下，MetaTable 使用启发式算法来猜测正确的显示列。这三个属性 DisplayColumn、SortColumn 和 SortDescending 也可以通过将 DisplayColumnAttribute 应用于实体类（如上所示）来显式指定。其构造函数接受显示列的名称、排序列的名称以及一个布尔值，该值指示是否应按降序执行默认排序。

## 数据访问支持

除了元数据信息之外，MetaTable 类在实现 Dynamic Data Web 应用程序中的数据访问逻辑方面也发挥着重要作用：

```
public Type DataContextType { get; }
public string DataContextPropertyName { get; }
```

MetaTable 类的 DataContextType 属性返回一个 Type 对象，该对象表示数据模型生成的数据上下文类。该类通常派生自 Entity Framework 中的 ObjectContext 基类和 LINQ to SQL 中的 DataContext 类。DataContextPropertyName 属性返回用于查询表行的属性的名称，例如 NorthwindEntities 对象上下文中的 Products 属性。在运行时，此信息由页面模板中的 DynamicDataManager 控件使用，以配置负责检索实体数据并将更改保存到数据库的 EntityDataSource 和 LinqDataSource 控件。

> **NOTE**
>
> DataContextType 是 MetaTable 类的属性而不是 MetaModel 属性这一点很重要。单个 MetaModel 实例可以通过对 RegisterContext 方法的单独调用注册来自不同数据上下文的表。如果不同上下文具有同名的表，你的代码需要通过将上下文类型传递给 MetaModel 类的 GetTable 方法，连同表名一起，来区分它们。

正如我们讨论 MetaModel 类的 RegisterContext 方法时可能回忆到的，如果对象上下文需要额外的初始化任务，你可以在注册时提供一个工厂方法，而不是简单地提供其类型：

```
public virtual object CreateContext();
```

MetaTable 类的 CreateContext 方法负责创建上下文对象，要么通过创建已注册类型的实例，要么通过调用上下文工厂方法，如果上下文就是这样与 MetaModel 注册的：

```
public IQueryable GetQuery();
public virtual IQueryable GetQuery(object context);
```

MetaTable 类还提供了两个重载的 GetQuery 方法，可用于动态查询任何表。这就是 ForeignKey_Edit 字段模板填充其下拉列表控件的方式。这些方法返回一个 LINQ IQueryable 对象，你可以使用它从数据库中检索行。第 14 章“Implementing Security”讨论了如何重写 GetQuery 方法来实现行级安全性。
