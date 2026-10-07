

# ADO.NET 简介

## 3.4.7 DataTable 组件

DataTable 可以被设计为一个容器，它持有一个 Rows 和 Columns 集合，而 Rows 和 Columns 集合包含了数据库表中的一组行（或 `DataRow` 对象）和一组列（或 `DataColumn` 对象）。DataTable 直接映射到数据库中的真实数据表，或者将其数据存储在映射区域、或与数据库中的数据或你的项目运行数据关联的某块内存空间中。正如我们在前面的节中提到的，DataTable 对象可以用两种方式使用。一种方法是在 DataObjects 组中，每个 DataTable 对象都映射到真实数据库中的表，但可以集成到 DataSet 对象中。所有这些 DataTable 对象都可以通过执行 DataAdapter 的 `Fill()` 方法来填充（参见第 3.4.6.4 节）。`Fill()` 方法的参数不是 DataTable，而是 DataSet，因为所有 DataTable 对象都嵌入在该 DataSet 中。另一种方法是使用通过独立数据表对象创建每个 DataTable，并可以通过执行 Command 对象的 `ExecuteReader()` 或 `SqlCommand()` 方法进行填充或操作。

DataTable 类位于 `System.Data` 命名空间中，它是一个不依赖于提供程序（Provider-independent）的组件，这意味着无论你在应用程序中使用哪种提供程序，只存在一个 DataSet 对象。

DataTable 是 ADO.NET 库中的核心对象。其他使用 DataTable 的对象包括 DataSet 和 DataAdapter。

在访问 DataTable 对象时，注意它们是条件区分大小敏感的。例如，如果一个 DataTable 命名为“factory”，另一个命名为“Factory”，那么搜索其中一个的字符串被视为区分大小敏感的。然而，如果“factory”存在而“Factory”不存在，则搜索被视为不区分大小敏感的。一个 DataSet 可以包含两个 `TableName` 值相同但 `Namespace` 属性不同的 DataTable。

如果你通过程序创建 DataTable，你必须先通过添加 `Column` 对象来定义它的架构（schema）。要向表中添加行，你必须先使用 `NewRow()` 方法返回一个 `DataRow` 对象。该 `DataRow` 由表的 `DataColumnCollection` 定义。DataTable 可以存储的最大行数是 16,777,216 行。

DataTable 还包含一个约束（Constraint）集合，该集合可以确保数据的完整性。DataTable 类是 .NET Framework 中 `System.Data` 的成员。你可以独立地创建和使用 DataTable，也可以将其作为 DataSet 的成员，DataTable 对象还可以与其他 .NET Framework 对象（包括 `View`）结合使用。如上一节所述，你通过 DataSet 对象的 `Tables` 属性访问表集合。

除了架构外，DataTable 还必须具有行数据和顺序数据。`DataRow` 及其属性和方法用于检索、评估和操作表中的数据。当你访问并更改行内的数据时，`DataRow` 对象会同时维护其当前状态和原始状态。

## 3.4.7.1 DataTable 构造函数

DataTable 有四个重载的构造函数，图 3.33 列出了三个最常用的构造函数。

你可以使用 DataTable 构造函数来创建一个 DataTable 对象。你可以使用 `Add` 方法将其添加到 DataTable 集合中，从而将其添加到 DataSet。

你可以通过使用 DataAdapter 对象的 `Fill()` 或 `FillSchema()` 方法在 DataSet 内部创建 DataTable 对象，或者通过 DataSet 的 `ReadXmlSchema()` 或 `InferSchema()` 方法从预定义的或推断的 XML 架构创建 DataTable。请注意，如果你已经将一个 DataTable 作为某个 DataSet 的 `Tables` 集合的成员添加，则你不能将其添加到任何其他 DataSet 的表集合中。

# 使用 C# 进行 SQL Server 数据库编程

| 构造函数 | 描述 |
| :--- | :--- |
| DataTable() | 初始化一个无参数的 DataTable 类新实例。 |
| DataTable(String) | 使用指定的表名初始化 DataTable 类新实例。 |
| DataTable(String, String) | 使用指定的表名和命名空间初始化 DataTable 类新实例。 |

**图 34** DataTable 类的构造函数

```csharp
DataSet dataSet = new DataSet();
DataTable dataTable = new DataTable("Factory");
dataSet.Tables.Add(dataTable);
```

**图 35** 向 DataSet 添加 DataTable 的示例。

当你通过程序创建 DataTable 时，你必须先通过添加 `Column` 对象来定义它的架构。要向表中添加行，你必须先使用 `NewRow()` 方法返回一个 `DataRow` 对象。该 `DataRow` 由表的 `DataColumnCollection` 定义。访问 DataTable 对象时，注意它们是条件区分大小敏感的。例如，如果一个 DataTable 命名为“factory”，另一个命名为“Factory”，那么搜索其中一个的字符串被视为区分大小敏感的。然而，如果“factory”存在而“Factory”不存在，则搜索被视为不区分大小敏感的。一个 DataSet 可以包含两个 `TableName` 值相同但 `Namespace` 属性不同的 DataTable。

如果你通过程序创建 DataTable，你必须先通过添加 `Column` 对象来定义它的架构。要向表中添加行，你必须先使用 `NewRow()` 方法返回一个 `DataRow` 对象。该 `DataRow` 由表的 `DataColumnCollection` 定义。DataTable 可以存储的最大行数是 16,777,216 行。

DataTable 还包含一个约束（Constraint）集合，该集合可以确保数据的完整性。DataTable 类是 .NET Framework 中 `System.Data` 的成员。你可以独立地创建和使用 DataTable，也可以将其作为 DataSet 的成员，DataTable 对象还可以与其他 .NET Framework 对象（包括 `View`）结合使用。如上一节所述，你通过 DataSet 对象的 `Tables` 属性访问表集合。

除了架构外，DataTable 还必须具有行数据和顺序数据。`DataRow` 及其属性和方法用于检索、评估和操作表中的数据。当你访问并更改行内的数据时，`DataRow` 对象会同时维护其当前状态和原始状态。

DataTable 有四个重载的构造函数，图 3.33 列出了三个最常用的构造函数。

你可以使用 DataTable 构造函数来创建一个 DataTable 对象。你可以使用 `Add` 方法将其添加到 DataTable 集合中，从而将其添加到 DataSet。

你可以通过使用 DataAdapter 对象的 `Fill()` 或 `FillSchema()` 方法在 DataSet 内部创建 DataTable 对象，或者通过 DataSet 的 `ReadXmlSchema()` 或 `InferSchema()` 方法从预定义的或推断的 XML 架构创建 DataTable。请注意，如果你已经将一个 DataTable 作为某个 DataSet 的 `Tables` 集合的成员添加，则你不能将其添加到任何其他 DataSet 的表集合中。

## 3.4.7.2 DataTable 属性

访问 DataTable 对象时，注意它们是条件区分大小敏感的。例如，如果一个 DataTable 命名为“factory”，另一个命名为“Factory”，那么搜索其中一个的字符串被视为区分大小敏感的。然而，如果“factory”存在而“Factory”不存在，则搜索被视为不区分大小敏感的。一个 DataSet 可以包含两个 `TableName` 值相同但 `Namespace` 属性不同的 DataTable。

如果你通过程序创建 DataTable，你必须先通过添加 `Column` 对象来定义它的架构。要向表中添加行，你必须先使用 `NewRow()` 方法返回一个 `DataRow` 对象。该 `DataRow` 由表的 `DataColumnCollection` 定义。DataTable 可以存储的最大行数是 16,777,216 行。

DataTable 还包含一个约束（Constraint）集合，该集合可以确保数据的完整性。DataTable 类是 .NET Framework 中 `System.Data` 的成员。你可以独立地创建和使用 DataTable，也可以将其作为 DataSet 的成员，DataTable 对象还可以与其他 .NET Framework 对象（包括 `View`）结合使用。如上一节所述，你通过 DataSet 对象的 `Tables` 属性访问表集合。

除了架构外，DataTable 还必须具有行数据和顺序数据。`DataRow` 及其属性和方法用于检索、评估和操作表中的数据。当你访问并更改行内的数据时，`DataRow` 对象会同时维护其当前状态和原始状态。

## 3.4.7.3 DataTable 方法

DataTable 有四个重载的构造函数，图 3.33 列出了三个最常用的构造函数。

你可以使用 DataTable 构造函数来创建一个 DataTable 对象。你可以使用 `Add` 方法将其添加到 DataTable 集合中，从而将其添加到 DataSet。

你可以通过使用 DataAdapter 对象的 `Fill()` 或 `FillSchema()` 方法在 DataSet 内部创建 DataTable 对象，或者通过 DataSet 的 `ReadXmlSchema()` 或 `InferSchema()` 方法从预定义的或推断的 XML 架构创建 DataTable。请注意，如果你已经将一个 DataTable 作为某个 DataSet 的 `Tables` 集合的成员添加，则你不能将其添加到任何其他 DataSet 的表集合中。

DataTable 是 ADO.NET 库中的核心对象。其他使用 DataTable 的对象包括 DataSet 和 DataAdapter。

（此处省略重复的说明说明）

# 使用 C# 进行 SQL Server 数据库编程

| 构造函数 | 描述 |
| :--- | :--- |
| `DataTable()` | 初始化一个无参数的 DataTable 类新实例。 |
| `DataTable(String)` | 使用指定的表名初始化 DataTable 类新实例。 |
| `DataTable(String, String)` | 使用指定的表名和命名空间初始化 DataTable 类新实例。 |

**图 34** DataTable 类的构造函数

```csharp
DataSet dataSet = new DataSet();
DataTable dataTable = new DataTable("Factory");
dataSet.Tables.Add(dataTable);
```

**图 35** 向 DataSet 添加 DataTable 的示例。

（此处省略重复的说明说明）

# ADO.NET 简介

| 属性 | 描述 |
| :--- | :--- |
| `Columns` | `Columns` 属性的类型为 `DataColumnCollection`，它包含一组 `DataColumn` 对象。 |
| `DataSet` | 所属的 DataSet。 |
| `Initialized` | 表示 DataTable 是否已初始化的值。 |
| `Namespace` | 用于 XML 表示的设置的命名空间。 |
| `PrimaryKey` | 获取或设置作为主键的列数组。 |
| `Rows` | `Rows` 属性的类型为 `DataRowCollection`，它包含一组 `DataRow` 对象。 |
| `TableName` | 获取或设置 DataTable 的名称。 |

**图 36** DataTable 类的属性

| 方法 | 描述 |
| :--- | :--- |
| `Clear` | 清空 DataTable 的所有数据。 |
| `Copy` | 复制结构和数据。 |
| `Dispose` | 释放使用的资源。 |
| `GetChanges` | 获取自上次加载或调用 `AcceptChanges` 以来所有更改的副本。 |
| `GetType` | 获取实例的类型。 |
| `ImportRow` | 将行复制到 DataTable，保留任何属性设置的原始和当前值。 |
| `Load` | 使用提供的 `IDataReader` 填充 DataTable。如果 DataTable 已包含行，则来自数据源的数据与现有行合并。 |
| `LoadDataRow` | 查找并更新。如果没有找到匹配项，则使用给定值创建一个新行。 |
| `Merge` | 将指定的 DataTable 与当前 DataTable合并。 |
| `NewRow` | 创建与表架构相同的新行。 |
| `ReadXML` | 读取 XML 架构和数据到 DataTable。 |
| `RejectChanges` | 回滚自加载或上一次调用 `AcceptChanges` 以来对表进行的所有更改。 |
| `Reset` | 重置 DataTable 为原始状态。 |
| `Select` | 获取 `DataRow` 对象数组。 |
| `ToString` | 获取 `TableName` 和 `DisplayExpression`（如果有）的连接字符串。 |
| `WriteXML` | 将 DataTable 的当前内容写入 XML。 |

**图 37** DataTable 的方法

该条件用于指示是否对表进行更新。如果找到了匹配行，则使用给定值创建一个新行。

## 3.4.7.4 DataTable 事件

最常用的事件是 `ColumnChanged`、`Initialized`、`RowChanged` 和 `RowDeleted`。通过使用这些事件，可以跟踪和监控 DataTable 中发生的真实情况。

