
在前面的命令中，创建了一个具有指定名称、路径和权限的程序集。在 Visual Studio 2012 中，你可以通过当前项目属性中的 SQLCLR 选项卡设置程序集的权限，如图 20:1 所示：

![](img/17af790174c480761404624aeed9b30b_966_0.png)

图 20:1：Visual Studio 2012 中的 SQLCLR 选项卡

接下来，将学习 `Microsoft.SqlServer.Server` 命名空间。

# 探索 Microsoft.SqlServer.Server 命名空间

`Microsoft.SqlServer.Server` 命名空间提供了各种类，用于在 SQL Server 2008 中集成 .NET Framework 4.5 的 CLR。你可以使用这些类创建存储过程、触发器、UDT 和 UDF。使用 `SqlContext` 类，你可以识别执行的代码是否运行在 SQL Server 数据库引擎进程中。当您使用存储过程、函数或触发触发器时，`SqlContext` 类还会提供调用者的上下文。表 20.1 列出了 `Microsoft.SqlServer.Server` 命名空间提供的类：

表 20.1：`Microsoft.SqlServer.Server` 命名空间提供的类
| 类 | 描述 |
| :--- | :--- |
| `InvalidUdtException` | 当 SQL Server 检测到无效 UDT 时抛出此异常 |
| `SqlContext` | 返回由 `SqlPipe`、`SqlTrigger/Context` 和 `Windowidentity` 类提供的调用者上下文 |
| `SqlDataRecord` | 返回一行数据及其元数据 |
| `SqlFacetAttribute` | 为返回的 UDT 提供注释，并附带可以在 Transact-SQL 中使用的额外信息 |
| `SqlFunctionAttribute` | 指定用户定义聚合的方法定义，并在 SQL Server 中作为函数使用 |
| `SqlMetaData` | 从 `SqlDataRecord` 对象中检索元数据信息 |
| `SqlMethodAttribute` | 指定 UDT 方法或属性的数据访问属性 |
| `SqlPipe` | 通过存储过程向调用者返回结果 |
| `SqlProcedureAttribute` | 指定程序集中的方法定义，该方法在 SQL Server 中充当存储过程作用 |
| `SqlTriggerAttribute` | 指定程序集中的方法定义，该方法在 SQL Server 中充当触发器作用 |
| `SqlTriggerContext` | 返回触发的触发器的上下文信息 |
| `SqlUserDefinedAggregateAttribute` | 表示该类型已注册为用户定义聚合 |
| `SqlUserDefinedTypeAttribute` | 表示程序集作为 SQL Server 中 UDT 的类型定义 |

表 20.2 列出了 `Microsoft.SqlServer.Server` 命名空间提供的接口：

表 20.2：`Microsoft.SqlServer.Server.Namespace` 提供的接口
| 接口 | 描述 |
| :--- | :--- |
| `BinarySerialize` | 帮助 UDT 和用户定义聚合的序列化或反序列化 |

表 20.3 列出了 `Microsoft.SqlServer.Server` 提供的枚举：

表 20.3：`Microsoft.SqlServer.ServerNamespace` 提供的枚举
| 枚举 | 描述 |
| :--- | :--- |
| `DataAccessKind` | 代表用户定义方法可以访问的数据类型 |
| `Format` | 代表 UDT 或聚合的序列化格式 |
| `SystemDataAccessKind` | 代表用户定义方法可以访问的系统数据类型 |
| `TriggerAction` | 表示触发器的动作，与 `SqlTriggerContext` 类一起使用 |

接下来，让我们学习存储过程。

# 第 20 章：.NET 与 SQL Server

## 存储过程

存储过程是存储在数据库上的编译 SQL 命令集。当客户端应用程序将其发送到数据库时，它会被编译并重复使用。SQL Server 2008 中存储过程的一个示例可以在代码列表 20.1 中所示：

代码列表 20.1：在 SQL Server 2008 中创建存储过程

```sql
CREATE PROCEDURE GetProductDetails
@ProductID INT
AS
SELECT ProductID, ProductName,QuantityPer,UnitPrice,UnitsInStock FROM Products
WHERE ProductID=@ProductID
```

在列表 20.1 中，创建了一个名为 `GetProductDetails` 的存储过程，它包含一个整数类型的参数。该存储过程提供了 `Products` 表中某物品的详细信息，包括 `ProductID`、`ProductName`、`QuantityPer`、`UnitPrice` 和 `UnitsStock`。你可以使用以下命令执行 `GetProductDetails`：

```sql
EXEC GetProductDetails
```

> 注意：你可以通过提供任何其他 ID（如 2）来执行 `GetProductDetails` 存储过程。

## 探索触发器

触发器是存储过程的一种，当使用一个或多个数据操作（`UPDATE`、`INSERT` 或 `DELETE`）修改数据库数据时触发。注意，触发器永远不会被手动调用，但当关联表中的数据被修改时，它会自动触发。列表 20.2 显示了在 SQL Server 2008 中创建触发器的示例：

代码列表 20.2：为 INSERT 操作创建触发器

```sql
CREATE TRIGGER TestTrigger1
ON MyTable
AFTER INSERT
AS
INSERT INTO TestTable(Col) SELECT ...
```

在列表 20.2 中，在 `MyTable` 上创建了一个名为 `TestTrigger1` 的触发器。每当在 `MyTable` 上执行 `INSERT` 操作时，`TestTrigger1` 就会触发并在另一个表中插入一个值。作为存储过程，触发器包含过程逻辑，该逻辑存储在数据库级别。

## 用户定义聚合函数

触发器是存储过程的一种类型，当使用一个或多个数据操作修改数据库数据时会被触发。注意，触发器永远不会被调用，但当关联表中的数据被修改时，它会自动触发。列表 20.2 显示了在 SQL Server 2008 中创建触发器的示例：

代码列表 20.2：为 INSERT 操作创建触发器

```sql
CREATE TRIGGER TestTrigger1
ON MyTable
AFTER INSERT
AS
INSERT INTO TestTable(Col) SELECT ...
```

在列表 20.2 中，在 `MyTable` 上创建了一个名为 `TestTrigger1` 的触发器。每当在 `MyTable` 上执行 `INSERT` 操作时，`TestTrigger1` 就会触发并在另一个表中插入一个值。作为存储过程，触发器包含过程逻辑，该逻辑存储在数据库级别。

## 探索用户定义聚合

触发器是存储过程的一种类型，当使用一个或多个数据操作修改数据库数据时会被触发。注意，触发器永远不会被调用，但当关联表中的数据被修改时，它会自动触发。

聚合函数

代码列表 20.3：使用聚合函数

```sql
USE Northwind;
SELECT EmployeeID, SUM(Freight) AS TotalFreight
FROM Orders
GROUP BY EmployeeID
```

在列表 20.3 中，使用 `SUM` 聚合函数计算 `Orders` 表。表 20.4：内置聚合函数
| 函数 | 描述 |
| :--- | :--- |
| `AVG` | 返回平均值 |
| `COUNT` | 返回计数 |
| `COUNT DISTINCT` | 返回去重计数 |
| `MAX` | 返回最大值 |
| `MIN` | 返回最小值 |
| `SUM` | 返回和 |

SQL Server 2008 中集成 .NET Framework 4.5 的 CLR 提供了各种类。你可以使用这些类创建存储过程、触发器、UDT 和 UDF。使用 `SqlContext` 类，你可以识别执行的代码是否运行在 SQL Server 数据库引擎进程中。`SqlContext` 类在当使用存储过程、函数或触发触发器时，还提供调用者的上下文。表 20.1 列出了 `Microsoft.SqlServer.Server` 命名空间提供的类：

表 20.1：`Microsoft.SqlServer.Server` 命名空间提供的类
| 类 | 描述 |
| :--- | :--- |
| `InvalidUdtException` | 当 SQL Server 检测到无效 UDT 时抛出此异常 |
| `SqlContext` | 返回由 `SqlPipe`、`SqlTrigger/Context` 和 `Windowidentity` 类提供的调用者上下文 |
| `SqlDataRecord` | 返回一行数据及其元数据 |
| `SqlFacetAttribute` | 为返回的 UDT 提供注释，并附带可以在 Transact-SQL 中使用的额外信息 |
| `SqlFunctionAttribute` | 指定用户定义聚合的方法定义，并在 SQL Server 中作为函数使用 |
| `SqlMetaData` | 从 `SqlDataRecord` 对象中检索元数据信息 |
| `SqlMethodAttribute` | 指定 UDT 方法或属性的数据访问属性 |
| `SqlPipe` | 通过存储过程向调用者返回结果 |
| `SqlProcedureAttribute` | 指定程序集中的方法定义，该方法在 SQL Server 中充当存储过程作用 |
| `SqlTriggerAttribute` | 指定程序集中的方法定义，该方法在 SQL Server 中充当触发器作用 |
| `SqlTriggerContext` | 返回触发的触发器的上下文信息 |
| `SqlUserDefinedAggregateAttribute` | 表示该类型已注册为用户定义聚合 |
| `SqlUserDefinedTypeAttribute` | 表示程序集作为 SQL Server 中 UDT 的类型定义 |

表 20.2 列出了 `Microsoft.SqlServer.Server` 命名空间提供的接口：

表 20.2：`Microsoft.SqlServer.Server.Namespace` 提供的接口
| 接口 | 描述 |
| :--- | :--- |
| `BinarySerialize` | 帮助 UDT 和用户定义聚合的序列化或反序列化 |

表 20.3 列出了 `Microsoft.SqlServer.Server.` 提供的枚举：

表 20.3：`Microsoft.SqlServer.ServerNamespace` 提供的枚举
| 枚举 | 描述 |
| :--- | :--- |
| `DataAccessKind` | 代表用户定义方法可以访问的数据类型 |
| `Format` | 代表 UDT 或聚合的序列化格式 |
| `SystemDataAccessKind` | 代表用户定义方法可以访问的系统数据类型 |
| `TriggerAction` | 表示触发器的动作，与 `SqlTriggerContext` 类一起使用 |

接下来，让我们学习存储过程。

## 存储过程

存储过程是存储在数据库上的编译 SQL 命令集。当客户端应用程序将其发送到数据库时，它会被编译并重复使用。SQL Server 2008 中存储过程的一个示例可以在代码列表 20.1 中所示：

代码列表 20.1：在 SQL Server 2008 中创建存储过程

```sql
CREATE PROCEDURE GetProductDetails
@ProductID INT
AS
SELECT ProductID, ProductName,QuantityPer,UnitPrice,UnitsInStock FROM Products
WHERE ProductID=@ProductID
```

在列表 20.1 中，创建了一个名为 `GetProductDetails` 的存储过程，它包含一个整数类型的参数。该存储过程提供了 `Products` 表中某物品的详细信息，包括 `ProductID`、`ProductName`、`QuantityPer`、`UnitPrice` 和 `UnitsStock`。你可以使用以下命令执行 `GetProductDetails`：

```sql
EXEC GetProductDetails
```

> 注意：你可以通过提供任何其他 ID（如 2）来执行 `GetProductDetails` 存储过程。

## 探索触发器

触发器是存储过程的一种，当使用一个或多个数据操作（`UPDATE`、`INSERT` 或 `DELETE`）修改数据库数据时会被触发。注意，触发器永远不会被手动调用，但当关联表中的数据被修改时，它会自动触发。列表 20.2 显示了在 SQL Server 2008 中创建触发器的示例：

代码列表 20.2：为 INSERT 操作创建触发器

```sql
CREATE TRIGGER TestTrigger1
ON MyTable
AFTER INSERT
AS
INSERT INTO TestTable(Col) SELECT ...
```

在列表 20.2 中，在 `MyTable` 上创建了一个名为 `TestTrigger1` 的触发器。每当在 `MyTable` 上执行 `INSERT` 操作时，`TestTrigger1` 就会触发并在另一个表中插入一个值。作为存储过程，触发器包含过程逻辑，该逻辑存储在数据库级别。

## 探索用户定义聚合

触发器是存储过程的一种类型，当使用一个或多个数据操作修改数据库数据时会被触发。注意，触发器永远不会被调用，但当关联表中的数据被修改时，它会自动触发。

聚合函数

代码列表 20.3：使用聚合函数

```sql
USE Northwind;
SELECT EmployeeID, SUM(Freight) AS TotalFreight
FROM Orders
GROUP BY EmployeeID
```
