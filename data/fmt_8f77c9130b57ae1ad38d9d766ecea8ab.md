
| `<>` | 不等于 |

SQL 中的等于和不等于运算符与 C# 中的不同。等于运算符是一个符号，而不是两个等号。不等于运算符是 `<>`。

让我们再看几个 `Select` 语句的示例。以下语句可以用于检索价格为 $28.95 的所有商品的编号和价格：

```
Select Product_Number, Price From Product Where Price = 28.95
```

## 数据库

以下 `Select` 语句从检索描述为 "Denim Jeans" 的行的所有列。

```
Select * From Product Where Description = 'Denim Jeans'
```

如果你仔细观察上一个语句，你会发现 SQL 语法和 C# 语法之间的另一个区别。在 SQL 中，字符串字面量包含在单引号中，而不是双引号。

> 提示：如果你需要将单引号作为字符串的一部分，只需在该位置写两个单引号即可。例如，假设你想在 `Product` 表中搜索 `Katy's Wool Cap`。你可以使用以下语句：

```
Select * From Product Where Description = 'Katy''s Wool Cap'
```

SQL 中的字符串比较是区分大小写的。如果你对 `Product` 表运行该语句，你将得不到任何结果：

```
Select * From Product Where Description = 'denim jeans'
```

然而，你可以使用 `Lower()` 函数将字符串转换为小写。这里有一个示例：

```
Select * From Product Where Lower(Description) = 'denim jeans'
```

该语句在执行比较之前会将 `Description` 列转换为全小写。结果，无论大小写如何，它都会返回所有 `Description` 等于 "denim jeans" 的行。你可以使用 `Upper` 函数（将字符串转换为大写）来实现相同的结果：

```
Select * From Product Where Upper(Description) = 'DENIM JEANS'
```

### 使用 LIKE 运算符

有时，搜索精确字符串可能得不到想要的结果。例如，假设 `Product` 表包含图 67 所示的行，而你想要所有衬衫的列表。

以下语句将不起。你能看出为什么吗？

```
Select * From Product Where Description = 'Shirt'
```

图 67 `ProductDB.mdf` 数据库中的 `Product` 表

| 产品编号 | 描述 | 库存 | 价格 |
|---|---|---|---|
| 10-01 | Oxford Cloth Shirt | 100 | 39.950 |
| 10-02 | Poplin Shirt | 150 | 38.500 |
| 10-03 | Plaid Flannel Shirt | 80 | 34.750 |
| 10-04 | Canvas Shirt | 200 | 32.950 |
| 10-05 | Cotton Short | 200 | 28.950 |
| 20-01 | Chino Classic Fit Pants | 100 | 28.950 |
| 20-02 | Relaxed Fit Pants | 100 | 28.950 |
| 20-03 | Denim Jeans | 275 | 32.950 |
| 20-04 | Wool Trousers | 75 | 28.950 |
| 30-01 | Warm-Up Jacket | 125 | 59.950 |
| 30-02 | Fleece Pullover | 130 | 29.950 |
| 30-03 | Parks | 75 | 19.950 |

## 数据库

图 68 解决方案管理器中的 Schema 定义条目

![](img/9467d25da5679b16515c9401daaae36c_708_0.png)

图 69 正在编辑的 `ProductDataSet.xsd`

![](img/9467d25da5679b16515c9401daaae36c_708_1.png)

右键点击显示 `Fill`、`GetData()` 的区域，如图 70 所示，从弹出菜单中选择 `Configure`（配置）。这将显示图 71 所示的表适配器配置窗口。注意表适配器配置中出现的 SQL 查询语句。数据集由此 `Select` 语句返回的行填充。如果你更改了此 `Select` 语句（例如添加一个 `Where` 子句），然后点击 `Finish`（完成）按钮，则 `DataGridView` 控件中最初显示的数据将发生相应变化。检查完该窗口后，点击 `Cancel`（取消）按钮关闭它。

图 70 从弹出菜单中选择 Configure

![](img/9467d25da5679b16515c9401daaae36c_708_2.png)

### 图 71 表适配器配置向导

![](img/9467d25da5679b16515c9401daaae36c_709_0.png)

> 注意：注意 `Select` 语句中的表名前带有带有 `dbo.` 前缀。`dbo` 代表数据库所有者（database owner），是 SQL Server 命名规范的一部分。在我们的示例程序中，`dbo` 前缀是可选的。

### 添加新的表适配器查询

你可以将你的 SQL 查询语句添加到表适配器中，并在 C# 代码中调用它们。教程 6 为表适配器添加了几个查询，然后在应用程序的表单上创建按钮来执行这些查询。

教程 6：

*创建 Prodeut 查询应用程序*

在本教程中，你将创建一个应用程序，该程序将在 `DataGridView` 控件中显示来自 `ProductDB.mdf` 数据库的 `Product` 表。你还向表适配器添加了两个 SQL 查询语句。这些查询执行以下操作：

- 按价格升序排序返回所有行
- 仅返回库存单位超过 100 的行

然后，你在应用程序表单上创建执行这些查询的按钮。

第 1 步：启动 Visual Studio（或 Visual C#）。创建一个名为 `Product Queries` 的 Windows Forms 项目。

第 2 步：将 `Form1` 的 `Text` 属性更改 `Product Queries`。

## 数据库

第 3 步：执行以下步骤连接应用程序到 `ProductDB.mdf` 数据库并为数据集选择 `Product` 表：

- 从 `Data`（数据）选择 `Add New Data Source...`（添加新数据源...）。
- 选择 `Database`（数据库）并点击 `Next`（下一步）。
- 选择 `Dataset`（数据集）并点击 `Next`。
- 点击 `New Connection...`（新建连接...）。
- 在 `Connection` 窗口中，确保选的数据源是 `Microsoft SQL Server Database (Sql)`。
- 在 `Connection` 窗口中，点击 `Browse`（浏览）并进入 `Student Sample Programs` 中的 `Chap11` 文件夹。选择 `ProductDB.mdf` 文件。点击 `OK`。
- 点击 `Next >`，当询问是否要将文件复制到项目时，选择 `Yes`（是）。
- 点击 `Next`。
- 选择 `Product` 表作为数据库对象，并将数据集名称更改为 `ProductDataSet`。点击 `Finish`（完成）。

> 注意：这是你在教程 3 第 3-11 步中执行的相同过程。如果你需要更详细的指导，请返回教程查看实际界面。

第 4 步：打开 `Data Sources`（数据源）窗口并将 `DataGridView` 控件拖到表单上，并绑定到 `Product` 表。创建 `DataGridView` 控件后，如图 72 所示调整表单和控件的大小。

图 72 应用程序的表单

![](img/9467d25da5679b16515c9401daaae36c_710_0.png)

第 5 步：现在添加第一个查询，该查询按价格对数据集中的数据进行排序。在解决方案管理器中，双击 `ProductDataSet.xsd` 条目。这将打开数据集的架构描述。右键点击显示 `ProductTableAdapter` 的区域。如图 73 所示，选择 `Add`（添加），然后点击 `Query...`（查询...）。

> 注意：你可能会在弹出菜单上看到 `Add Query...`（添加查询...）而不是 `Add`。如果是如此，只需点击 `Add Query...` 即可。

## 数据库

图 73 向表适配器添加查询

![](img/9467d25da5679b16515c9401daaae36c_711_0.png)

**第 6 步：** 接下来出现表适配器配置向导，如图 74 所示。确保选择了 `SQL Statements`（SQL 语句），然后点击 `Next`。

图 74 表适配器配置向导——选择命令类型

![](img/9467d25da5679b16515c9401daaae36c_711_1.png)

**第 7 步：** 向导现在提示你选择查询类型，如图 75 所示。确保选中了返回行的 `SELECT`（返回 rows），然后点击 `Next`。

## 数据库

图 75 表适配器配置向导——选择查询类型

![](img/9467d25da5679b16515c9401daaae36c_712_0.png)

第 8 步：向导现在提示你选择查询类型。已显示一个返回 `Product` 表中所有行的语句。如图 76 所示，在语句末尾添加 `Where` 子句。点击 `Next`。

图 76 表适配器配置——指定 SQL 语句

![](img/9467d25da5679b16515c9401daaae36c_712_1.png)

第 9 步：向导现在提示选择方法。进行以下选择：

- 勾选 `Fill a DataTable`。
- 在 `Fill a DataTable` 下输入 `FillPrice` 作为方法名。这将是执行 SQL 语句的方法。不要勾选 `Return a DataTable`。

图 77 表适配器配置——选择方法

![](img/9467d25da5679b16515c9401daaae36c_713_0.png)

## 数据库

> 注意：可能会可能会弹出菜单上看到 `Add Query...`（添加查询...）而不是 `Add`。如果是如此，只需点击 `Add Query...` 即可。

第 10 步：向导现在向你显示结果。点击 `Finish`（完成）按钮。数据集由此 `Select` 语句返回的行填充。如果你更改了此 `Select` 语句（例如添加一个 `Where` 子句），然后点击 `Finish` 按钮，则 `DataGridView` 控件中最初显示的数据将发生相应变化。检查完该窗口后，点击 `Cancel`（取消）按钮关闭它。

图 78 表适配器配置——结果

![](img/9467d25da5679b16515c9401daaae36c_714_0.png)

第 11 步：你添加第二个查询，返回库存超过 100 的行。右键点击显示 `Fill`、`GetData()` 的区域，如图 70 所示，从弹出菜单中选择 `Configure`（配置）。这将显示图 71 所示的表适配器配置窗口。

图 79 表适配器配置——选择查询类型

![](img/9467d25da5679b16515c9401daaae36c_714_1.png)

| `ProductDataSet.xsd` | `ProductAdapter` |
|---|---|
| `Product_Number, Description, Units_On_Hand, Price` | `FillPrice()` |

图 80 表适配器配置——指定 SQL 语句

![](img/9467d25da5679b16515c9401daaae36c_715_0.png)

图 81 表适配器配置——选择生成生成

![](img/9467d25da5679b16515c9401daaae36c_715_1.png)

## 数据库

架构定义文件 (`ProductDataSet.xsd`) 现在应该如图 82 所示。注意，你创建的两个方法 `FillByPrice()` 和 `FillByUnits()` 现在出现在图底部的区域。

**图 82** 架构定义文件中的 `FillByPrice()` 和 `FillByUnits()` 方法

![](img/9467d25da5679b16515c9401daaae36c_716_0.png)

**步骤 12 ：** 现在向应用程序表单中添加按钮控件以执行 SQL 查询。在设计器中打开 `Form1`，添加图 83 所示的两个按钮控件。

**图 83** 添加到表单中的按钮控件

![](img/9467d25da5679b16515c9401daaae36c_716_1.png)

**步骤 13 ：** 双击 `sortByPriceButton.control`。通过在程序 4 第 36 行输入代码来完成 `sortByPriceButton_click` 事件处理器。此语句调用了表适配器的 `FillByPrice` 方法。

**步骤 14 ：** 回到设计器的 `Form1` 视图，双击 `unitsGreater100Button.control`。通过在程序 4 第 41 行输入代码来完成 `unitsGreater100Button_click` 事件处理器。此语句调用了表适配器的 `FillByUnits` 方法。

**步骤 15 ：** 保存项目并运行应用程序。当它出现时，它应该在 `DataGridView` 控件中显示 `Product` 表的所有行。当你点击“按价格排序”按钮时，数据应该按价格排序。当你点击“数量超过 100 的产品”按钮时，你只会看到 `Units_On_Hand` 大于 100 的行。完成后，可以退出应用程序表单。如果你计划立即继续下一个教程，请在 Visual Studio 中保持项目打开状态。你将在下一个教程中继续开发此应用程序。

# 程序 4：Product 查询应用程序中完成的 Form1 代码
