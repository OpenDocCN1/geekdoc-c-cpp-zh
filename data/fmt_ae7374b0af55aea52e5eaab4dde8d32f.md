
Transact-SQL functionality not available in Entity SQL — Specifies that the transact functionalities are not supported in Entity SQL. The functionalities of SQL that are not supported in Entity SQL are as follows:

- Data Manipulation Language (DML) — Entity SQL does not provide support for DML statements such as `INSERT`, `UPDATE`, and `DELETE`
- Data Definition Language (DDL) — Entity SQL does not provide support for DDL statements such as `CREATE`, `GRANT`, and `REVOKE`
- Imperative programming — Entity SQL supports functional programming languages rather than supporting imperative programming.
- Grouping functions — Entity SQL does not provide support for grouping functions such as `CUBE`, `ROLLUP`, and `GROUPING_SET`.
- Analytic functions — Entity SQL does not provide support for analytic functions.

Built-in functions and operators — Specifies that Entity SQL provides support for subsets of Transact-SQL built-in functions and operators that are supported by database providers. Entity Framework also provides the capability of declaring built-in and user-defined existing database functions.

Paging — Specifies that Entity SQL supports physical paging by using the `SKIP` and `LIMIT` sub-clauses in the `ORDER BY` clause. We cannot use the `SKIP` and `LIMIT` sub-clauses together.

By using `SKIP`, the result set includes rows that start from the next row immediately after the `SKIP` expression. Suppose a table has 10 rows. Now, if we use `SKIP 6` here, it returns the result from the seventh row.

The use of the `LIMIT` subclause restricts the resulting number of rows in a result set returned by the `LIMIT` expression. For example, `LIMIT 4` restricts the result set to 4 instances or rows.

## NOTE

> Entity SQL does not support any mechanisms for query hints.

Now, let's take a look into the operators supported by Entity SQL.

## Operators for Entity SQL

Entity SQL supports many operators to specify an action performed on one or more expressions. Table 22.3 lists the noteworthy operators for Entity SQL:

| Type of Operators | Description |
|---|---|
| Arithmetic Operators | Describes the Entity SQL arithmetic operators. These perform mathematical operations on two expressions of one or more numeric data types, such as addition. |
| Comparison Operators | Describes the Entity SQL comparison operators. These test whether two expressions are the same, such as `=`. |
| Logical Operators | Describes the Entity SQL logical operators such as `AND`. |
| Member Access Operator | Describes the Entity SQL member access operator such as the dot operator (`.`). |
| String Concatenation Operator | Describes the Entity SQL string concatenation operator such as plus (`+`). |

Now, let's learn about the EntityClient provider in more detail.

## Understanding the `EntityClient` Provider

The `EntityClient` provider is an ADO.NET-managed provider that supports retrieving data described in an EDM. Entities are combined together with other related entities that can have different types of relationships among them. The `EntityClient` provider allows a user to query data described in a conceptual model. It is capable of returning results such as scalar results, result sets, and object graphs. The `EntityClient` provider is located within the `System.Data.EntityClient` namespace. Table 22.4 lists the noteworthy classes of the `System.Data.EntityClient` namespace:

### Table 22.4: Noteworthy Classes of the `System.Data.EntityClient` Namespace

| Class | Description |
|---|---|
| `EntityCommand` | Represents a command to be executed against an EDM. |
| `EntityConnection` | Represents a connection to an underlying data store. This class cannot be inherited. |
| `EntityConnectionStringBuilder` | Represents a simple way to create and manage the contents of connection strings used by the `EntityClient` class. |
| `EntityParameter` | Represents a parameter in an `EntityCommand` class. This class cannot be inherited. |
| `EntityParameterCollection` | Represents a collection of parameters associated with the `EntityCommand` class. |
| `EntityProviderFactory` | Represents a set of methods for creating instances of a provider's implementation of the data source classes. |
| `EntityTransaction` | Specifies the transaction for an `EntityCommand` class. |

The `EntityClient` provider uses standard ADO.NET providers, such as .NET Framework Data Provider (`SqlClient`), to communicate with databases, such as SQL Server. Table 22.5 lists EDM type facets to corresponding provider type names in the table:

### Table 22.5: EDM Type Facets to Corresponding Provider Type Names

| Provider Type Name | EDM Type Name | Facet Name | Attribute Name | Value |
|---|---|---|---|---|
| `bit`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Boolean` | Not applicable | | |
| `tinyint`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Byte` | Not applicable | | |
| `smallint`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Int16` | Not applicable | | |
| `int`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Int32` | Not applicable | | |
| `float`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Double` | Not applicable | | |
| `real`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Single` | Not applicable | | |
| `decimal`: Supports the `Equal Comparable` and `Order Comparable` attributes when set to `True` | `Decimal` | `Precision` | `Minimum` | `1` |
| | | | `Maximum` | `29` |
| | | | `Default` | `18` |
| | | | `Constant` | `False` |
| | | `Scale` | `Minimum` | `0` |
| | | | `Maximum` | `29` |
| | | | `Default` | `0` |
| | | | `Constant` | `False` |

### 表 22.5：EDM 类型方面到对应提供程序类型名称

| 提供程序类型名称 | EDM 类型名称 | 方面名称 | 属性名称 | 值 |
|---|---|---|---|---|
| `image`：在设置为 `False` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `Binary` | `MaxLength` | `Default` | `2147483647` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `timestamp`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `Binary` | `MaxLength` | `Default` | `8` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `True` |
| | | | `Constant` | `True` |
| `rowversion`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `Binary` | `MaxLength` | `Default` | `8` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `True` |
| | | | `Constant` | `True` |
| `smalldatetime`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `DateTime` | `PreserveSeconds` | `Default` | `False` |
| | | | `Constant` | `True` |
| | | `DateTimeKind` | `Default` | `Unspecified` |
| | | | `Constant` | `True` |
| `datetime`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `DateTime` | `PreserveSeconds` | `Default` | `True` |
| | | | `Constant` | `True` |
| | | `DateTimeKind` | `Default` | `Unspecified` |
| | | | `Constant` | `True` |
| `nvarchar`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Minimum` | `1` |
| | | | `Maximum` | `4000` |
| | | | `Default` | `4000` |
| | | | `Constant` | `False` |
| | | `Unicode` | `Default` | `True` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `varchar`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Minimum` | `1` |
| | | | `Maximum` | `4000` |
| | | | `Default` | `4000` |
| | | | `Constant` | `False` |
| | | `Unicode` | `Default` | `False` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `char`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Minimum` | `1` |
| | | | `Maximum` | `8000` |
| | | | `Default` | `8000` |
| | | | `Constant` | `False` |
| | | `Unicode` | `Default` | `False` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `True` |
| | | | `Constant` | `True` |
| `nchar`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Minimum` | `1` |
| | | | `Maximum` | `4000` |
| | | | `Default` | `4000` |
| | | | `Constant` | `False` |
| | | `Unicode` | `Default` | `True` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `True` |
| | | | `Constant` | `True` |
| `varchar(max)`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Default` | `2147483647` |
| | | | `Constant` | `True` |
| | | `Unicode` | `Default` | `False` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `nvarchar(max)`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Default` | `1073741823` |
| | | | `Constant` | `True` |
| | | `Unicode` | `Default` | `True` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `ntext`：在设置为 `False` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Default` | `1073741823` |
| | | | `Constant` | `True` |
| | | `Unicode` | `Default` | `False` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `text`：在设置为 `False` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Default` | `2147483647` |
| | | | `Constant` | `True` |
| | | `Unicode` | `Default` | `False` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |
| `Unique identifier`：在设置为 `True` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `Guid` | n/a | | |
| `XML`：在设置为 `False` 时支持 `Equal Comparable` 和 `Order Comparable` 属性 | `String` | `MaxLength` | `Default` | `1073741823` |
| | | | `Constant` | `True` |
| | | `Unicode` | `Default` | `True` |
| | | | `Constant` | `True` |
| | | `FixedLength` | `Default` | `False` |
| | | | `Constant` | `True` |

在下一节，让我们了解 ADO.NET 元数据。

## ADO.NET 元数据

ADO.NET Entity Framework 使用 ADO.NET 元数据，该元数据提供基础设施和类型层次结构以展示 `System.Data.Metadata.Edm` 命名空间，用于管理 Entity Framework 的元数据服务。表 22.6 列出了 `System.Data.Metadata.Edm` 命名空间的 noteworthy 类：

### 表 22.6：`System.Data.Metadata.Edm` 命名空间的 noteworthy 类

| 类 | 描述 |
| --- | --- |
| `AssociationEndMember` | 表示 EDM 中关联的末端。 |
| `AssociationSet` | 表示 EDM 中的关联集。 |
| `AssociationSetEnd` | 表示 EDM 中关联集的末端。 |
| `RowType` | 描述一行，例如查询的结果。此类派生自 `StructuralType` 类。行类型的结构取决于查询中投影的数据库列。我们不能在 EDM 架构中显式定义 `RowType`。 |
| `SimpleType` | 表示描述 EDM 中基本类型的基类。 |
| `StructuralType` | 表示 EDM 中具有成员的所有类型的基类型。 |
| `TypeUsage` | 描述一个类型及其该类型的方面集。 |

表 22.7 列出了 `System.Data.Metadata.Edm` 命名空间的 noteworthy 枚举：

### 表 22.7：`System.Data.Metadata.Edm` 命名空间的 noteworthy 枚举

| 枚举 | 描述 |
|---|---|
| `BuiltInTypeKind` | 表示指定 EDM 中所有内置类型的枚举。 |
| `ConcurrencyMode` | 表示 EDM 中属性的并发选项。 |
| `DataSpace` | 表示 Entity Framework 中模型的默认名称。 |
| `OperationAction` | 表示当删除表示概念模型中关系基类的 `RelationshipType` 属性的父末端时执行可能的操作列表。 |
| `ParameterMode` | 表示参数的方向。 |
| `ParameterTypeSemantics` | 表示用于解析函数重载的类型语义。每个存储提供程序必须在提供程序清单文件中为每个函数定义使用这些枚举标志。 |
| `PrimitiveTypeKind` | 表示 EDM 定义的所有基本类型的种类。 |
| `PropertyKind` | 表示 EDM 中项属性的种类。 |
| `RelationshipMultiplicity` | 表示关系类型末端的多重性信息。 |
| `StoreGeneratedPattern` | 表示一个枚举，用于检查 SSDL 中的列在插入和更新操作期间是否需要值。 |

现在，让我们详细了解 `EdmGen.exe` 工具。

## EDM 生成器工具

Entity Framework 不支持在 ASP.NET 网站项目中对 EDM 文件进行编译时验证。ASP.NET 网站项目不支持预构建事件；在预构建事件中验证实体可能是一项非常耗时的任务。ADO.NET 运行时在我们运行或调试应用程序时验证文件。`EdmGen.exe` 工具安装在 .NET Framework 目录中，位于 `C:\Windows\Microsoft.NET\Framework\v4.0.30319`。我们也可以通过执行以下步骤从 Visual Studio 命令提示符访问 `EdmGen.exe` 工具：

1. 单击 开始 → 所有程序 → Microsoft Visual Studio 2010 → Visual Studio 工具 → Visual Studio 命令提示符 (2010)。
   Visual Studio 2010 命令提示符打开，默认路径为，例如 `C:\Program Files\Microsoft Visual Studio 10.0\VC>`。EDM 生成器工具的一般语法如下：
   `EdmGen /mode:choice [options]`

2. 现在，要在 Visual Studio 命令提示符 (2010) 上查看所有 `EdmGen` 选项，请输入 `EdmGen/help` 在命令提示符下。EDM 生成器工具可用的所有选项都将显示在命令提示符下，如图 22.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1124_0.png)

**图 22.3**：使用 `EdmGen.exe` 工具

3. 要查看 `EDMGen` 选项，请向下滚动屏幕（图 22.3）。图 22.4 中显示的示例（由椭圆圈出）展示了如何使用 `EdmGen.exe` 工具通过 `Northwind` 数据库生成和验证 EDM：

![](img/e073a4882197be4ab61103cbe0bcb394_1124_1.png)

**图 22.4**：显示从 `Northwind` 数据库生成实体模型的选项

验证实体模型的语法为：
