

## 4.5.3 对 DataTable 对象的操作

除了 `DataRowExtensions` 类中定义的 `DataRow` 运算符外，在 `DataTableExtensions` 类中还有其他可用于 `DataTable` 类的方法。

扩展方法允许你在无需创建新类型、重新编译或以其他方式修改原始类型的情况下，向现有类型“添加”方法。扩展方法是一种特殊的静态方法，但它们的调用方式就像是在扩展类型上调用实例方法一样。对于用 C# 编写的代码，调用扩展方法与调用在类型中实际定义的方法没有区别。

最常见的扩展方法是 LINQ 标准查询运算符，它们为现有的 `IEnumerable<T>` 类型添加了功能。要使用标准查询运算符，首先通过 `System.Linq` 将其引入作用范围。然后，任何实现 `IEnumerable<T>` 的类型看起来都拥有实例。当你输入 `IEnumerable<T>` 类型（如 `List<T>` 或 `Array`）实例之后输入运算符时，可以在 IntelliSense 补全中看到这些额外方法。

`DataTable` 类中定义的两个扩展方法 `AsEnumerable()` 和 `CopyToDataTable()` 在数据驱动应用程序中得到了实现。由于空间限制，本节我们仅使用第一个方法。

扩展方法 `AsEnumerable()` 的功能是从 `DataTable` 对象转换并返回类型为 `IEnumerable<DataRow>` 的序列。你可能已经注意到，我们在之前章节的许多示例中使用了此方法。例如，在上一节讨论的 `RowField` 和 `DataSetField` 示例方法中，你可以找到该方法及其功能。参考图 4.40 和图 4.41 可以清晰了解如何使用该方法返回 `DataRow` 对象。

接下来让我们来看 LINQ to SQL。

## 4.6 LINQ to SQL

如上一节所述，LINQ to SQL 属于 LINQ to ADO.NET，它是 ADO.NET 的一个子组件。LINQ to SQL 绝对是为 SQL Server 数据库实现的。不同的数据库需要使用不同的 LINQ 模型来执行相关查询，例如 LINQ to MySQL、LINQ to DB2 或 Oracle。

LINQ to SQL 查询是在实现 `IQueryable<T>` 接口的类上执行的；该接口继承自 `IEnumerable<T>` 接口并带有额外的方法，因此，除了标准查询运算符 (SQO) 外，LINQ to SQL 查询还具有额外的查询运算符，因为它使用了 `IQueryable<T>` 接口。

LINQ to SQL 是一个应用程序编程接口 (API)，允许用户通过与 LINQ 标准查询运算符 (SQO) 方便地访问 SQL Server 数据库。要使用此 API，你首先需要将构建在逻辑模型上的关系型数据库表转换为基于对象模型构建实体类。然后，在关系型数据库与一组从实体类实例化的对象之间建立映射关系。LINQ to SQL 或标准查询运算符将与这些实体交互以执行真实的数据操作。之后，每个实体类可以映射或等同于数据库中的物理表，每个实体类的属性可以映射或等同于该表中的列。只有在建立这种映射关系后，才能使用 LINQ to SQL 更新数据库中的数据。

在创建实体类并建立每个物理表与每个实体类之间的映射关系后，需要实体类与真实数据表之间的数据操作转换。DataContext 是负责这一工作的家伙。基本上，

## 语言集成查询 (LINQ) 简介

DataContext 是一个用于建立项目与数据库之间连接的类。除了这种连接角色外，DataContext 还提供了连接功能，将标准查询运算符的操作转换为或解释为可以在关系型数据库中运行的 SQL 语句。

LINQ to SQL 提供的两个工具是 SQL 和对象关系设计器 (O/R Designer)。借助这些工具的帮助，用户可以轻松构建所有实体类，设置关系数据库与 LINQ to SQL 使用的对象模型之间的映射，并创建 DataContext。

SQLModel 和对象关系设计器的区别在于前者是基于控制台的应用程序，而后者是基于窗口的应用程序。这意味着 SQLModel 提供类似 DOS 的模板，通过在黑白窗口中输入单个命令来执行操作。对象关系设计器提供了图形界面 (GUI)，允许用户将由图标表示的表格拖入 GUI。显然，第二种方法或工具比第一种更方便。

由于 Visual Studio 2022 停止了对 SQLModel 的支持，我们将在第 5 章中重点关注如何使用对象关系设计器构建 LINQ to SQL 查询。

## 4.6.1 LINQ TO SQL 的实现

使用 O/R Designer 进行 LINQ to SQL 查询的一些项目将在接下来的章节中开发，项目按以下章节分类：

- LINQ to SQL: 选择查询项目：第 5、8 和 9 章
- LINQ to SQL: 插入查询项目：第 8 和 9 章
- LINQ to SQL: 更新查询项目：第 7、8 和 9 章
- LINQ to SQL: 删除查询项目：第 7、8 和 9 章

参考这些章节以获取这些项目的更详细信息和相关代码开发。

## 4.7 LINQ TO ENTITIES

如 LINQ 简介部分所述，LINQ to Entities 属于 LINQ to ADO.NET，是 ADO.NET 3.5 Entity Framework 的子组件。

LINQ to Entities 查询在 ADO.NET 3.5 Entity Framework (ADO.NET 3.5 EF) 和 ADO.NET 3.5 Entity Framework Tools (ADO.NET 3.5 EF) 的控制下执行。ADO.NET 3.5 EF 允许能够以领域特定对象和属性（如客户和客户地址）的形式处理数据，而无需考虑存储这些数据的底层数据库表和列。

要访问和实现 ADO.NET 3.5 EF，开发者需要理解实体数据模型 (Entity Data Model)，它是 ADO.NET 3.5 EF 的核心。LINQ 允许开发者在应用程序代码中开发基于集合的查询，而无需使用单独的查询语言。通过 Entity Framework 的对象服务基础设施，ADO.NET 在 .NET 环境中将数据的通用概念视图（包括关系数据）暴露为对象。这使得对象层成为 LINQ 支持的理想目标。

这种 LINQ 技术——LINQ to Entities，允许开发者直接从开发环境使用 LINQ 表达式和 LINQ 标准查询运算符针对 Entity Framework 对象上下文创建灵活的、强类型查询。查询是用编程语言表示的，成员名称和数据类型的错误将被编译器在编译时捕获，减少了实体模型与应用程序之间出现类型问题的可能性。

## 150 使用 C# 进行 SQL Server 数据库编程

成员名称和数据类型的错误将被编译器在编译时捕获，减少了实体模型与应用程序之间出现类型问题的可能性。

针对 Entity Framework 的查询由命令树查询表示，这些查询在对象上下文中执行。LINQ to Entities 将语言集成查询 (LINQ) 转换为命令树查询，针对 Entity Framework 执行查询，并返回对象

