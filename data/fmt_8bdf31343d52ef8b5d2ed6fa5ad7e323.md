
此事件处理程序接收到的第二个参数具有你可以 way来显示错误信息的属性。你最常用的是 `Exception` 属性，它提供了对由于错误而抛出的异常对象的访问。与任何其他异常对象一样，该对象具有一个 `Message` 属性，用于提供错误的描述。你还可以使用第二个参数的 `RowIndex` 和 `ColumnIndex` 属性来识别导致数据错误的行和列。

# DataGridView 控件的事件

| 事件 | 说明 |
| --- | --- |
| `DataError` | 当 `DataGridView` 控件检测到值格式不正确或在无效的地方出现空值导致的数据错误时触发。 |

# DataGridViewDataErrorEventArgs 类的三个属性

| 属性 | 说明 |
| --- | --- |
| `Exception` | 由于错误而抛出的异常。你可以使用此对象的 `Message` 属性获取有关异常的附加信息。 |
| `RowIndex` | 发生错误的行的索引。 |
| `ColumnIndex` | 发生错误的列的索引。 |

# 处理 DataGridView 控件数据错误的代码

```
private void productsDataGridView_DataError(
    object sender, DataGridViewDataErrorEventArgs e)
{
    int row = e.RowIndex + 1;
    string errorMessage = "A data error occurred.\n" +
    "Row: " + row + "\n" +
    "Error: " + e.Exception.Message;
    MessageBox.Show(errorMessage, "Data Error");
}
```

- 你可以 `DataGridView` 控件的 `DataError` 事件编写事件处理程序，以处理在使用 `DataGridView` 控件时发生的任何数据错误。
- 你可以使用事件处理程序的第二个参数的 `Exception`、`RowIndex` 和 `ColumnIndex` 属性来显示意义的错误信息。

图 18-15 如何处理 `DataGridView` 控件的数据错误

# 如何使用数据集设计器

# 数据集设计器允许你使用图形界面与数据集架构工作。在接下来的主题中，你将学习一些使用数据集设计器的基本技能。

# 如何查看数据集的架构

要了解更多关于数据集的信息，可以在数据集设计器中显示其架构。例如，在图 18-16 中，你可以看到 Customer Maintenance 应用程序使用的 MMABooks 数据集的架构。对于这个简单的应用程序，数据集仅包含 `Customers` 表，因为这是应用程序使用的唯一表。该表中的键图标表示 `CustomerID` 列是该表的主键。

对于每个表，数据集架构还包含一个表适配器，它列出了可以与该表配合使用的查询。每个表适配器至少包含一个名为 `Fill` 的主查询，它决定了当你从“数据源”窗口拖动表时使用哪些列。该查询还用于生成该表的 `Insert`、`Update` 和 `Delete` 语句。此外，表适配器还包含你为表定义的任何其他查询。你将在下一章中学习更多关于定义额外查询的内容。

如果你在数据集设计器中点击表适配器，你会发现它的“属性”窗口中的属性包含了该表适配器定义的 ADO.NET 对象。这包括一个 `Connection` 对象，以及 `SelectCommand`、`InsertCommand`、`UpdateCommand` 和 `DeleteCommand`。如果你展开这些命令对象之一，可以查看定义其执行执行的 SQL 语句的 `CommandText` 属性。例如，你可以看到用于 Customers 表表适配器 `Fill` 查询的 `SelectCommand` 对象的 `Select` 语句的开头。如果你点击此属性的省略号按钮，可以使用后续所示的查询生成器（Query Builder）处理该查询。

注意，数据集设计器还便于设置数据表中列的属性。要执行此操作，只需选择一个列并打开“属性”窗口即可。例如，你可以使用这种技术设置数据集中某个列的 `DefaultValue` 属性，这是你经常需要的操作。

# 在数据集设计器中显示的架构

![](img/3148667e42d4db35b3d08576aaa1fa01_592_0.png)

## Description

- 要查看数据源的数据集的架构，请在解决方案管理器中双击数据集的架构文件 (`.xsd`)，或者选择架构文件并点击解决方案管理器顶部的“查看设计器”按钮。架构将显示在数据集设计器中。
- 在“属性”窗口中查看表适配器的属性，请在数据集设计器中选择表适配器。这些属性包括用于连接数据库的 `Connection` 对象，以及用于处理数据库中数据的 `SelectCommand`、`InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 对象。
- 要查看查询的属性，请在数据集设计器中选择查询。*主查询*定义了当你从“数据源”窗口将表拖到表单时使用的列。该表的 `Insert`、`Update` 和 `Delete` 语句也基于此查询。
- 要处理查询，在数据集设计器中选择查询。*主查询*定义了当你从“数据源”窗口将表拖到表单时使用的列。该表的 `Insert`、`Update` 和 `Delete` 语句也基于此查询。数据集设计器还便于设置数据表中列的属性。要执行此操作，只需选择一个列并打开“属性”窗口。例如，你可以使用这种技术设置数据集中某个列的 `DefaultValue` 属性，这是你经常需要的操作。

图 18-16 如何查看数据集的架构

# 第 4 节数据库

# 如何使用查询生成器

正如你在本章之前看到的，查询生成器提供了一个图形界面，你可以在不知道正确 SQL 语句的情况下修改查询。例如，你可以使用图 18-17 所示的查询生成器进行修改。当查询生成器打开时，显示了当前表。例如，在图中，显示了 `Customers` 表。如果你需要包含相关表，可以通过“添加表”对话框来实现。当你添加表时，查询生成器包含一个显示表之间关系的连接图标。

在网格面板中，你可以看到将包含在查询中的列。要将列添加到此面板中，只需勾选图表中列出的列名。一旦列被添加到网格面板，你可以使用 `Sort` 列来识别哪些列应对返回的行进行排序，并使用 `Sort Order` 列在多个列时指定排序优先级。在这里，行将按 `Name` 列升序排序。

同样，你可以使用 `Filter` 列来建立选择查询检索的行的准则。例如，为了检索特定 ID 的客户，你可以在 `CustomerID` 的 `Filter` 列中指定 `@CustomerID`。你将在下一章中学习更多关于此类查询的代码。

在你创建查询时，SQL 面板显示生成的 `Select` 语句。你还可以随时运行此查询，将选中的行显示在结果面板中。这样，你可以确保查询按照你的要求工作。点击“执行查询”按钮。

当你得到所需的查询，可以点击“确定”按钮保存查询。这样做，Visual Studio 将显示一个对话框，询问你是否根据新的命令语法重新生成命令。也就是说，你希望修改 `Insert`、`Update` 和 `Delete` 语句以与 `Select` 语句匹配。根据你所做的更改，你可能可能不想这样做。例如，如果你只是更改了排序顺序，则没有必要更新 `Insert`、`Update` 和 `Delete` 语句。另一方面，如果你从原始表中添加或删除了一个或多个列，你希望更新 `Insert`、`Update` 和 `Delete` 语句。

# 查询生成器

查询生成器

| 列 | 别名 | 输出 | 排序类型 | 排序 | 过滤 | 或... |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `CustomerID` | `Customers` | | 升序 | | | |
| `Name` | | | | | | |

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

## 描述

- 要显示主查询的查询生成器，请选择包含查询的表适配器，然后点击省略号...，在属性窗口中选择 `SelectCommand` 对象的 `CommandText`。
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

在创建查询后，您可以使用数据集设计器预览其检索的数据。要执行此操作，您需要使用如图 18-18 所示的预览数据对话框。在这里，正在预览为 `Customers` 表适配器的 `Fill` 查询返回的数据。

要预览查询的数据，只需点击预览按钮。点击后，数据将显示在结果网格中，且查询返回的列数和行数将显示在网格正下方。在此示例中，查询检索了 6 列和 697 行。

在接下来的章节中，您将学习如何创建使用参数的查询。对于这些查询，您必须在参数网格的“值”列中为每个参数输入一个值，然后才能预览其数据。例如，假设您想检索具有特定客户 ID 的客户数据。那么，您必须在参数网格中输入该客户 ID，以检索该客户的数据。

# 预览数据对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_596_0.png)

## 描述

- 要显示查询的预览数据对话框，请在数据集设计器中右键点击查询并选择“预览数据”命令，或者选择查询然后使用 数据→预览数据命令。
- 要预览数据，点击预览按钮。点击后，数据将显示在结果网格中，且查询返回的列数和行数将显示在结果网格下方。
- 如果查询需要参数，您必须在参数网格的“值”列中为每个参数输入值。有关查询参数的更多信息，请参阅第 19 章。

图 18-18 如何预览查询的数据

# 如何解释生成的 SQL 语句

表适配器的 `Fill` 方法使用存储在 `SelectCommand` 对象中的 SQL `Select` 语句执行适配器的 `Fill` 查询，以便从数据库中检索数据。同样，`UpdateAll` 管理器使用存储在适配器的 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 对象中的 SQL `Insert`、`Update` 和 `Delete` 语句来对数据库中执行添加、更新和删除操作。

为了帮助您理解这些语句是如何构成的，图 18-19 展示了客户维护窗的 `Select` 语句以及从该语句生成的 `Insert`、`Update` 和 `Delete` 语句。尽管这些语句看起来很复杂，但此处提供的信息将让您直观了解它们的工作原理。

首先，请注意 `Insert` 语句是由一个 `Select` 语句构成的，该语句检索了刚刚添加到数据库的行。在数据库为新行生成某些数据的情况下，这可能是必要的。例如，当向数据库添加客户客户行时，数据库会生成 `CustomerID` 列的值。此时，图中的 `Select` 语句使用 SQL Server 的 `SCOPE_IDENTITY` 函数检索具有此 ID 的行。然而，如果数据库没有生成或计算任何列值，则此 `Select` 语句以及 `Update` 语句之后的语句将不需要。

此外，请注意 `Update` 和 `Delete` 语句使用了乐观并发。因此，这些语句的 `Where` 子句中添加了代码，以检查任何列值是否自从数据库检索以来已发生了变化。此代码将数据库中每个列的当前值与存储在数据集中的列的原始值进行比较。如果没有值发生变化，则执行该操作。

最后，请注意图中的大多数语句都使用一个或多个参数。参数用于 `Insert` 语句的 `Values` 子句和数据集的 `Set` 子句中，以引用数据集中列的当前值。参数还用于 `Update` 和 `Delete` 语句的 `Where` 子句中，以引用数据列的原始值。`Update` 语句之后的 `Select` 语句的 `Where` 子句中使用了一个参数来引用当前行。向会在为表适配器创建命令对象时插入这些参数。然后，在执行每个语句之前，Visual Studio 会为每个变量替换适当的值。

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

## 观点

现在你已经完成了本章，你应该能够使用数据源创建简单的应用程序，以便你能够在数据库的单个数据表中查看和维护数据。这应该让你对使用数据源功能创建应用程序是多么快速和简便有一个直观的认识。在下一章中，你将学习如何使用数据源构建更复杂的应用程序。

## 术语

- 数据源 (`data source`)
- 模式 (`schema`)
- 有类型数据集 (`typed dataset`)
- 无类型数据集 (`untyped dataset`)
- 绑定控件 (`binding a control`)
- 未绑定控件 (`unbound control`)
- 复杂数据绑定 (`complex data binding`)
- 简单数据绑定 (`simple data binding`)
- 参数化查询 (`parameterized query`)
- 数据提供程序错误 (`data provider error`)
- ADO.NET 错误 (`ADO.NET error`)
- 数据集设计器 (`Dataset Designer`)
- 主查询 (`main query`)

## 练习之前...

在进行本节的任何练习之前，请确保安装 SQL Server Express 并按照附录 A 中的说明创建 MMABooks 数据库。

## 练习 18-1 构建一个 DataGridView 应用程序

在练习中，你将构建图 18-9 所示的商品维护（Product Maintenance）应用程序。这将向你展示如何使用数据源、数据集和 `DataGridView` 控件构建简单的应用程序。

### 构建表单并使用有效数据测试

- 1. 在 `C:\C# 2010\Chapter 18` 目录下启动新应用程序 `ProductMaintenance`，并使用图 18-1 到 18-8 中的技术创建数据源将其拖到表单上。然后，根据需要调整表单和 `DataGridView` 控件的大小，但不要更改其他任何内容。
- 2. 分阶段使用有效数据测试应用程序。首先，点击列标题对行进行排序，并通过拖动分隔符调整其中一列的大小。其次，更改行中某列的数据，并移动到另一行查看数据集中的数据是否已更改。最后，添加一行所有列均有有效数据的行，并移动到另一行查看该行已添加。此时，更改仅应用于数据集，尚未更改到数据库。现在，点击工具栏上的保存按钮将更改保存到数据库中。

### 使用无效数据测试表单并提供异常处理
