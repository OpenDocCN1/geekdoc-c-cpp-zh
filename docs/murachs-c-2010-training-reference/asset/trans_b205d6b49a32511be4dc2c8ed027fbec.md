

# 查询生成器

查询生成器

| 列 | 别名 | 输出 | 排序类型 | 排序 | 过滤 | 或... |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| CustomerID | Customers | | 升序 | | | |
| Name | | | | | | |

设计窗格

网格窗格

SQL窗格

```sql
SELECT
FROM
ORDER BY Name
CustomerID, Name, Address, City, State, ZipCode
```

结果窗格

![](img/3148667e42d4db35b3d08576aaa1fa01_594_0.png)

# 描述

- 要显示主查询的查询生成器，请选择包含查询的表适配器，然后点击省略号...，在属性窗口中选择 SelectCommand 对象的 CommandText。
- 默认情况下，当前表显示在设计窗格中。要向此窗格添加相关表，请在窗格中点击鼠标右键，选择“添加表”，并从对话框显示的列表中选择该表。然后，查询将添加一个连接。
- 要将列包含在查询中，点击其左侧的框。然后，该列将添加到网格窗格中。或者，通过勾选 *（所有列）项目选择所有列。
- 要创建计算列，请在“列”中输入表达式，然后在“别名”列中输入您想要使用的名称。
- 要按一个或多个列对返回的进行排序，请按照您所需的顺序从这些列的“排序类型”中选择升序或降序。您还可以使用“排序”来设置排序序列。
- 要指定选择标准（例如列必须包含特定值才能被选中），请在“过滤”列中输入。
- 要使用某列进行排序或指定标准但不将其包含在查询结果中，请取消“输出”列中的勾选。
- 当您选择列并指定排序和选择标准时，查询生成器会构建 SQL 语句并显示在 SQL 窗格中。
- 要要在结果窗格中显示查询结果，请点击执行查询按钮。
- 当您接受一个查询时，如果需要更新根据主查询生成的插入、更新和删除查询，将显示一个对话框。

图 18-17 如何使用查询生成器

# 如何预览查询的数据

在创建查询后，您可以使用数据集设计器预览其检索的数据。要执行此操作，您需要使用如图 18-18 所示的预览数据对话框。在这里，正在预览为 Customers 表适配器的 Fill 查询返回的数据。

要预览查询的数据，只需点击预览按钮。点击后，数据将显示在结果网格中，且查询返回的列数和行数将显示在网格正下方。在此示例中，查询检索了 6 列和 697 行。

在接下来的章节中，您将学习如何创建使用参数的查询。对于这些查询，您必须在参数网格的“值”列中为每个参数输入一个值，然后才能预览其数据。例如，假设您想检索具有特定客户 ID 的客户数据。那么，您必须在参数网格中输入该客户 ID，以检索该客户的数据。

# 预览数据对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_596_0.png)

# 描述

- 要显示查询的预览数据对话框，请在数据集设计器中右键点击查询并选择“预览数据”命令，或者选择查询然后使用 数据→预览数据命令。
- 要预览数据，点击预览按钮。点击后，数据将显示在结果网格中，且查询返回的列数和行数将显示在结果网格下方。
- 如果查询需要参数，您必须在参数网格的“值”列中为每个参数输入值。有关查询参数的更多信息，请参阅第 19 章。

图 18-18 如何预览查询的数据

# 如何解释生成的 SQL 语句

表适配器的 Fill 方法使用存储在 SelectCommand 对象中的 SQL Select 语句执行适配器的 Fill 查询，以便从数据库中检索数据。同样，UpdateAll 管理器使用存储在适配器的 InsertCommand、UpdateCommand 和 DeleteCommand 对象中的 SQL Insert、Update 和 Delete 语句来对数据库中执行添加、更新和删除操作。

为了帮助您理解这些语句是如何构成的，图 18-19 展示了客户维护窗的 Select 语句以及从该语句生成的 Insert、Update 和 Delete 语句。尽管这些语句看起来很复杂，但此处提供的信息将让您直观了解它们的工作原理。

首先，请注意 Insert 语句是由一个 Select 语句构成的，该语句检索了刚刚添加到数据库的行。在数据库为新行生成某些数据的情况下，这可能是必要的。例如，当向数据库添加客户客户行时，数据库会生成 CustomerID 列的值。此时，图中的 Select 语句使用 SQL Server 的 SCOPE_IDENTITY 函数检索具有此 ID 的行。然而，如果数据库没有生成或计算任何列值，则此 Select 语句以及 Update 语句之后的语句将不需要。

此外，请注意 Update 和 Delete 语句使用了乐观并发。因此，这些语句的 Where 子句中添加了代码，以检查任何列值是否自从数据库检索以来已发生了变化。此代码将数据库中每个列的当前值与存储在数据集中的列的原始值进行比较。如果没有值发生变化，则执行该操作。

最后，请注意图中的大多数语句都使用一个或多个参数。参数用于 Insert 语句的 Values 子句和数据集的 Set 子句中，以引用数据集中列的当前值。参数还用于 Update 和 Delete 语句的 Where 子句中，以引用数据列的原始值。Update 语句之后的 Select 语句的 Where 子句中使用了一个参数来引用当前行。向会在为表适配器创建命令对象时插入这些参数。然后，在执行每个语句之前，Visual Studio 会为每个变量替换适当的值。

这应该让您对使用 ADO.NET 时如何刷新数据集以及如何提供乐观并发更有视角。由于离线数据架构，这些功能无法由数据库管理系统或 ADO.NET 提供。相反，它们是由数据源配置向导生成的 SQL 语句提供的。

# 检索客户行的 SQL

```sql
SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
```

# 插入客户行并刷新数据集的 SQL

```sql
INSERT INTO Customers
(Name, Address, City, State, ZipCode)
VALUES (@Name, @Address, @City, @State, @ZipCode);

SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
WHERE (CustomerID = SCOPE_IDENTITY())
```

# 更新客户行并刷新数据集的 SQL

```sql
UPDATE Customers
SET Name = @Name,
    Address = @Address,
    City = @City,
    State = @State,
    ZipCode = @ZipCode
WHERE (CustomerID = @Original_CustomerID) AND
  (Name = @Original_Name) AND
  (City = @Original_City) AND
  (State = @Original_State) AND
  (ZipCode = @Original_ZipCode);

SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
WHERE (CustomerID = @CustomerID)
```

# 删除客户行的 SQL

```sql
DELETE FROM Customers
WHERE (CustomerID = @Original_CustomerID) AND
  (Name = @Original_Name) AND
  (City = @Original_City) AND
  (State = @Original_State) AND
  (ZipCode = @Original_ZipCode);
```

