
LINQ to DataSet 实际上是三个独立的技术，允许你与关系型数据库进行交互。图 16.8 显示了 LINQ to DataSet 如何相互关联，以及 C# 数据源。

![](img/d08df1b94a49a49b95ebbdc5e982bda6_370_0.png)

图 16.8 LINQ to DataSet

## 使用 LINQ to DataSet

LINQ to DataSet 构建在现有的 ADO.NET 架构之上，让你能够轻松查询 `DataSet`。它并不是为了取代 ADO.NET，而是为了让你编写查询。

要使用 LINQ to DataSet，你必须先填充 `DataSet`。数据加载后，你可以使用学习 LINQ to XML 时学的技术进行查询。列表 16.2 在功能上等同于列表 16.1 所示的查询。然而，通过对 `DataTable` 使用 `AsEnumerable` 方法，你可以对数据执行标准的 LINQ 查询。

### 列表 16.2 一个简单的 LINQ to DataSet 查询

```csharp
string connectionString = "Integrated Security=SSPI;database=AdventureWorksLT2012;server=(local)\SQLLEXPRESS";
```

```csharp
string selectSQL = @"SELECT * FROM [AdventureWorksLT2012].[SalesLT].[Customer]";

DataAdapter adapter = new SqlDataAdapter(selectSQL, connectionString);
DataSet ds = new DataSet();
adapter.Fill(ds);
foreach (var customer in ds.Tables[0].AsEnumerable()
    Where(row => row.Field<string>("CompanyName") == "A Bike Store"))
{
    Console.WriteLine("{0} {1}", customer.Field<string>("Title"), customer.Field<string>("FirstName"));
}
```

## LINQ to SQL

### 使用

### 使用 LINQ to SQL

LINQ to SQL 允许你使用与内存集合或其他任何 LINQ 数据源相同的查询语法直接对 SQL 数据库进行查询。尽管 ADO.NET 将数据库映射到概念数据模型（由 `DataSet` 表示），但 LINQ to SQL 直接映射到你应用程序代码中的对象模型。当你的执行执行时，LINQ 语法查询会被 LINQ to SQL 翻译成 SQL 语言查询，然后发送到。

要执行的数据库。当结果返回时，LINQ to SQL 将它们转换回数据模型对象。

要使用 LINQ to SQL，你必须首先创建一个表示数据库的对象模型。有两种方法可以实现这一点，如下所示：

- 对象关系设计器（O/R Designer），它是 Visual Studio 2012 的一部分，提供了一个丰富的用户界面，用于从现有数据库创建对象模型。O/R Designer 仅支持 SQL Server Express 或 SQL Server 2000（及版本）数据库。

- `SQLMetal` 命令行工具，应适用于大型数据库，或 O/R Designer 不支持的数据库。

当你决定了如何生成对象模型时，你需要决定想要生成的代码类型。使用 O/R Designer，你可以生成提供基于特性的映射的 C# 源代码。如果你使用 `SQLMetal` 命令行工具，你还可以生成一个包含映射元数据的外部 XML 文件。

### 注意

### 创建对象模型

实际上有创建对象模型的第三种方法，即你使用代码编辑器手动编写对象模型。这种方法是不推荐的，因为很容易出错，特别是在创建表示现有数据库的对象模型时。

你可以使用代码编辑器来修改或精炼由对象关系设计器或 `SQLMetal` 命令行工具生成的代码。

当你创建好对象模型后，就可以通过编写 LINQ 查询在应用程序中使用它。列表 16.3 中的代码显示了定义 `DataContext` 到执行查询并观察结果的完整示例，并产生与列表 16.1 和 16.2 中代码相同的结果。

# 列表 16.3 简单的 LINQ to SQL 查询

```
DataContext context = new DataContext("Integrated Security=SSPI;database=AdventureWorksLT2012;server=(local)\SQLPRESS");
```

```
Table<Customer> customers = dataContext.GetTable<Customer>();
IQueryable<Customer> query =
  from customer in customers
where customer.CompanyName == "A Bike Store"
select customer;
```

```
foreach(Customer customer in query)
{
    Console.WriteLine("{0} {1} {2}",
    customer.Title,
    customer.FirstName,
    customer.LastName);
}
```

### 注意

### 必要的命名空间

要使用 LINQ to SQL，你需要包含 `System.Linq` 和 `System.Data.Linq` 命名空间。

你必须首先通过 `DataContext` 在你的对象模型和数据库之间建立连接。然后你创建一个 `Table<T>` 类，作为你可以查询的表。虽然实际上并非如此，但你可以将 `DataContext` 认为类似于 `DBConnection`，将 `Table<T>` 类似于 `DataTable`。然后你定义并随后执行你的查询。

### 试一试

### 使用 LINQ to SQL

通过遵循这些步骤，你可以使用 O/R Designer 和 LINQ to SQL 插入记录并查询表：

1. 创建一个新的控制台应用程序。

2. 使用指令包含 `System.Data.Linq` 命名空间。

3. 使用 O/R Designer 创建对象模型。要执行此操作，通过选择 LINQ to SQL 类 向你的项目添加新项，如图 16.9 所示。将文件命名为 `AdventureWorksLT`。

4. 在生成的编辑器中（部分内容如图 16.10 所示），点击“数据库资源管理器”链接以显示 Visual Studio 数据库资源管理器窗口。

5. 展开 `AdventureWorksLT2012` 连接以查看可用表，选择 `Customer` 表并将其拖到 `AdventureWorksLT.dbml` 编辑器窗口，如图 16.11 所示。这将创建表示 `Customer` 表的实体类。

## 理解 LINQ to ADO.NET

![](img/d08df1b94a49a49b95ebbdc5e982da6_374_0.png)

图 16.9

新建项对话框。

![](img/d08df1b94a49a49b95ebbdc5e982da6_374_1.png)

图 16.10

对象关系设计器。

![](img/d08df1b94a49a49b95ebbdc5e982da6_374_2.png)

图 16.11

显示表的对象关系设计器。

### 将数据库文件复制到项目

如果你看到类似于图 16.12 所示的对话框，提示连接使用的是本地文件并询问你是否将文件复制到项目，请确保说“否”。

![](img/d08df1b94a49a49b95ebbdc5e982da6_375_0.png)

图 16.12

复制文件到项目的对话框。

6. 在 `Program.cs` 文件的 `Main` 方法中实现列表 16.3 所示的代码。

7. 使用 `Ctrl+F5` 运行应用程序。输出应该像图 16.13 所示。

# 理解 LINQ to ADO.NET 359

```csharp
customer.CompanyName == "A Bike Store"
select customer;
```

```csharp
foreach (Customer customer in query)
{
    Console.WriteLine("{0} {1} {2}",
    customer.Title,
    customer.FirstName,
    customer.LastName);
}
```

### 使用 LINQ to Entities

早些时候，你学习了 ADO.NET 以及如何使用 LINQ to SQL 开发与数据库交互的应用程序。Entity Framework（实体框架）扩展了 ADO.NET 的基本功能，以支持开发以数据为中心的应用。

传统上，在开发以数据为中心的应用时，你不仅必须对数据库表、关系和业务逻辑进行建模，还必须直接操作数据库以存储和检索数据。尽管 LINQ to SQL 帮助解决了其中的一些问题，但 Entity Framework 允许你通过创建一个定义实体和被建模关系的领域模型，从而在更高层次的抽象上进行工作。

随后，Entity Framework 会将此领域模型（通常称为概念模型）转换为特定数据源的命令。这种方法允许你在开发应用程序时，无需担心对特定数据源的依赖。

当领域模型定义完成后，Entity Framework 会将关系表、类和外键约束映射到逻辑模型中的类。这种方法为定义和优化逻辑模型提供了极大的灵活性。生成的类是部分类（partial classes），允许你轻松扩展它们。

要通过 Entity Framework 访问或修改数据，你可以对概念模型执行查询，并通过以下方法之一返回对象：

- LINQ to Entities 为直接针对概念模型进行查询提供了 LINQ 支持。随后，Entity Framework 和 LINQ 都可以使用 LINQ to Entities 查询返回的对象。

- Entity SQL 是一种数据源无关的 SQL 版本，可以直接与概念模型工作。

- 查询生成器方法（Query builder methods）允许你使用与 LINQ 扩展方法相似的语法创建 Entity SQL 查询。

为了让创建实体模型更容易，Visual Studio 2012 包含了实体数据模型设计器（Entity Data Model Designer），如图 16.14 所示。

![](img/d08df1b94a49a49b95ebbdc5e982bda6_379_0.png)

**图 16.14**

实体数据模型设计器（图像不供详细阅读）。

注意

### EntityClient 数据提供程序

由于 Entity Framework 是构建在传统的 ADO.NET 服务之上的，它包含了 `EntityClient` 数据提供程序，该程序负责将实体查询转换为其特定数据源的版本，并将实体数据转换为对应的对象。

你也可以像使用任何其他 ADO.NET 数据提供程序一样使用 `EntityClient Provider`，允许你使用数据读取器（data reader）执行返回数据的 Entity SQL 查询。

此设计器允许你视觉创建并修改模型的实体、映射、关联和继承。

它由以下组件组成：

- 可视化设计表面

- 映射详细窗口，允许你查看和编辑映射

- 模型浏览器窗口，以树形视图显示概念模型和逻辑模型

# 总结 361

使用 Entity Framework 的简单方法是向项目添加一个新的 ADO.Net 实体数据模型项。这会启动实体数据模型向导，允许你从现有数据库或通过创建空数据模型来生成实体数据模型。

创建数据模型后，你就可以使用 LINQ to Entities 轻松地对数据上下文（data context）执行查询，如列表 16.8 所示。该查询从 `Products` 表选择前 10 条记录并显示产品名称。实体数据模型向导创建了 `AdventureWorksLT2012_DataEntities` 和 `Product` 类。

### 列表 16.8 一个自定义DataContext

```csharp
using (AdventureWorksLT2012_DataEntities context =
    new AdventureWorksLT2012_DataEntities())
{
    IQueryable<Product> productsQuery = (from product in context.Products
    select product).Take(10);

    Console.WriteLine("Product Names:");
    foreach (var prod in productsQuery)
    {
        Console.WriteLine(prod.Name);
    }
}
```

运行此查询的结果如图 16.15 所示。

![](img/d08df1b94a49a49b95ebbdc5e982bda6_380_0.png)

图 16.15

选择前 10 个产品。

## 总结

在这个小时内，你学习了 ADO.NET 和 LINQ to ADO.NET 技术如何使与数据库工作变得简单。你学习了使用 ADO.NET 的基础知识，并在此基础上了解了 LINQ to DataSets 如何允许你对 DataSet 中的数据添加复杂查询。

你学习了 LINQ to SQL 如何允许你创建一个表示数据库的对象模型，使你能够轻松地从数据库中查询、添加、更新和删除数据。最后，你看到了为用于 LINQ to SQL 创建自定义数据上下文是多么简单。

## 问答

- 问：**什么是关系型数据库？**

  答：关系型数据库简单来说组织成表、行和记录的数据仓库。

- 问：**什么是 ADO.NET？**

  答：`ADO.NET` 库是一个丰富的框架，允许你轻松地构建可以检索和更新信息的应用程序。

- 问：**ADO.NET 需要持续连接吗？**

  答：大多数 `ADO.NET` 类的设计都使得它们不需要持续连接。

- 问：**LINQ to ADO.NET 是什么？**

  答：LINQ to ADO.NET 实际上是三个独立的技术：LINQ to DataSet、LINQ to SQL 和 Entities。

- 问：**什么是 LINQ to SQL 对象模型？**

  答：LINQ to SQL 对象模型直接表示（或映射）数据库中的对象（表）。

- 问：**LINQ to SQL 可以更新数据吗？**

  答：是的，LINQ to SQL 可以用于更新数据。

## 测验

1. .NET 框架随附哪些 ADO.NET 提供程序？

1. .NET 框架目前提供了五个数据提供程序，支持 SQL Server、Oracle、任何 OLE DB 兼容的数据库、任何 ODBC 兼容的数据库以及 Entity（它是框架的一部分）。

2. 使用 LINQ to DataSet 需要哪些？

2. LINQ to DataSet 需要以下程序集：

   - `System.Core`

   - `System.Data`

   - `System.Data.DataSetExtensions`

   - `System.Data.Common`

   - `System.Data.SqlClient`

3. 使用 LINQ to SQL 需要哪些？

3. LINQ to SQL 需要以下程序集：

   - `System.Core`

   - `System.Data.Linq`

4. 创建自定义 DataContext 的好处是什么？

4. 创建自定义 `DataContext` 有助于通过提供的公共成员 `Table<T>` 集合访问由定义的表。

## 练习

本小时没有练习。

# 第 17 小时 构建 Windows 应用程序在本小时将学到：

- 理解 WPF

- 创建 WPF 应用程序

- 样式设置

在完成本书的前三个部分后，你应该已经熟悉 .NET Framework 和 C# 语言。你学习了引用类型和值类型的基本区别，包括如何创建自己的类型。你学习了语言特性，如扩展方法、自动属性、lambda、事件和异常。你现在知道如何查询数据集以及处理文件系统、XML 和数据库中的文件和目录。简而言之，你现在已经拥有了创建复杂应用程序的所有语言技能，这些应用程序可以利用 .NET Framework 提供的用户界面库。

Windows Foundation (WPF) 提供了一个统一的编程模型，允许你构建包含用户界面元素、媒体和文档的 Windows 应用程序。然而，WPF 不仅仅限于用户界面。它是一个下一代演示系统，允许你创建各种视觉丰富的独立和浏览器托管应用程序。WPF 的核心是一个与分辨率无关的基于矢量的渲染引擎，设计用于

为了利用现代图形硬件。WPF 是 .NET Framework 的一部分，你需要的大多数类型位于 `System.Windows` 命名空间中。

## 使用标记和后置代码

如果你之前开发过 ASP.NET 应用程序，那么标记和后置代码（code-behind）的概念应该已经熟悉了。在 WPF 应用程序中，你使用标记语言来实现应用程序的外观；而你使用编程语言（如 C#）在标记的“后面”实现行为。这实现了外观与行为的整洁分离，提供了以下益处：

-   降低了开发和维护成本。

-   开发效率更高，允许其他开发者在实现应用程序行为的同时，创建应用程序的外观。

-   多个设计工具可以创建并共享标记。

### 介绍可扩展应用程序标记语言

WPF 使用可扩展应用程序标记语言（XAML），这是一种基于 XML 的组合式标记用语言。由于 XAML 是基于 XML 的，你用它构建的用户界面（UI）是在元素树中组装的，这是一个由嵌套元素的层次结构。元素树提供了一种创建和管理用户界面的逻辑方式。
