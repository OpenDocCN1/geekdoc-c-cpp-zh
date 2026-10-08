
- **数据源 (Data Source)** 如其名，数据源是应用程序可以的数据源。通常是数据库，也可以是 Excel 表格、XML 数据、文本文件或 Web 服务。

- **表适配器 (Table Adapter)** 表适配器连接到数据源并从数据源中的表检索数据。它还可以更新数据源中的表。

- **数据集 (Dataset)** 数据集获取内存中的副本。当你与表适配器交互时，应用程序与数据集交互，修改行、删除行、添加新行等。然后，数据集指示适配器将更改写回数据库。

- **绑定源 (Binding Source)** 绑定源是一种可以将用户界面控件连接到数据集的组件。

幸运的是，Visual Studio 提供了向导，可以轻松创建和配置必要的组件。在教程 1 中，你将启动一个新的 C# 项目并使用 Visual Studio 执行以下操作：

- 创建 SQL Server 数据库
- 在数据库中设计表
- 向表中添加数据

### 教程 1：启动电话录应用程序并创建 Phonelist.mdf 数据库

在接下来的教程中，你将创建一个使用数据库存储姓名和电话号码列表的应用程序。在本教程中，你将通过创建数据库来启动应用程序。在下一次教程中，你把应用程序连接到数据库、数据集，并在表单上添加一个允许用户与数据库交互的控件。

- 第 1 步：启动 Visual Studio（或 Visual C Express）。创建一个名为 Phone Book 的新 Windows Forms 项目。
- 第 2 步：将 Form 的 Text 属性更改为 Phone Book。
- 第 3 步：接下来你创建一个新数据库并将其添加到项目中。点击 Visual Studio 菜单栏上的 Project（项目）并选择 Add New Item...（新建项...）。
- 第 4 步：出现 Add New Item 窗口。滚动列表并选择 Service-based Database（基于服务的数据库），如图 5 所示。你还需要在窗口底部 Name 文本框中指定数据库的名称。会出现一个默认名称，例如 Database.mdf。将其更改为 `Phonelist.mdf`。确保保留项 `.mdf` 文件扩展名。

图 5 Add New Item 窗口

| Add New Item - Phone Book | Sort by: Default | Search Installed Templates |
|---|---|---|
| Installed Templates | | |
| Visual CP Items | | |
| Code | Local Database | Visual CP Items |
| Data | General | 用于服务数据访问的空 SQL Server 数据库 |
| Web | Local Data Cache | |
| Windows Forms | MDI Parent Form | Visual CP Items |
| WFP | Preprocessed Template | Visual CP Items |
| Reporting | Report | Visual CP Items |
| Workflow | Report Wizard | Visual CP Items |
| Online Templates | Resources File | Visual CP Items |
| Select Service-based Database | RuleSet | Visual CP Items |
| Change the name to Phonelist.mdf | Service-based Database | Visual CP Items |
| | Settings File | Visual CP Items |
| | Style Sheet | |
| Name: Phonelist.mdf | | Add | Cancel |

第 5 步：点击 Add New Item 窗口中的 Add 按钮。这向项目中添加了一个名为 `Phonelist.mdf` 的空 SQL Server 数据库。

第 6 步：接下来出现图 6 所示的 Data Source Configuration Wizard（数据源配置向导）窗口。点击 Cancel 按钮。此处你取消过程，因为你刚刚创建的数据库是空的。在创建数据库之前，你无法配置数据源。

## 图 6 在数据源配置向导中点击 Cancel

![](img/9467d25da5679b16515c9401daaae36c_667_0.png)

**步骤 7**：查看图 7 所示的 Solution Explorer（解决方案管理器），注意它现在包含一个 `Phonelist.mdf` 数据库条目。双击 `Phonelist.mdf` 数据库条目。注意 Toolbox 所在区域现在打开了一个名为 Server Explorer（服务器管理器）的新窗口。在 Visual Studio 中，该窗口名为 Server Explorer。如果你使用的是 Visual C# Express，该窗口名为 Database Explorer。Server Explorer 如图 8 所示。

> 注意：对于我们的目的而言，使用 Visual Studio 中的 Server Explorer 还是 Visual C# Express 中的 Database Explorer 并不重要。它们的功能相同。Server Explorer 提供了跨网络定位数据库的额外功能。

**图 7** `Phonelist.mdf` 数据库的 Solution Explorer 条目

![](img/9467d25da5679b16515c9401daaae36c_667_1.png)

## 数据库

## 图 8 Server Explorer

![](img/9467d25da5679b16515c9401daaae36c_668_0.png)

**步骤 8**：现在你向 `Phonelist.mdf` 数据库添加一个表。在 Server Explorer (Database Explorer) 中，确保 `Phonelist.mdf` 条目已展开，如图 8 所示。右键点击 *Tables*（表），如图 9 所示，点击菜单上的 *Add New Table*（添加新表）。

## 图 9 向 `Phonelist.mdf` 数据库添加表

![](img/9467d25da5679b16515c9401daaae36c_668_1.png)

这将显示 Table Designer（表设计器）和 Column Properties（列属性）窗口，如图 10 所示。你使用 *Table Designer* 来指定表列的名称和数据类型，*Column properties* 窗口允许你为每列设置各种属性。

**步骤 9**：你添加到表中的第一列是 *PersonID* 列。*PersonID* 是一个标识列（DBMS 自动为其生成唯一的整数值），它将是表的主键。

在 *Table Designer* 中，在 *Column Name*（列名）下输入 *PersonID*，然后按 *Tab*。在 *Data Type*（数据类型）下，取消 Allow Nulls（允许为空）下的勾选标记。*Table Designer* 应该如图 11 所示。

## 图 10 Table Designer 和 Column Properties 窗口

![](img/9467d25da5679b16515c9401daaae36c_669_0.png)

## 图 11 在 Table Designer 中创建的 PersonID 列

| Column Name | Data Type | Allow Nulls |
| --- | --- | --- |
| PersonID | int | |

第 10 步：现在你必须设置 PersonID 列的属性以将其指定为标识列。在 Column Properties 窗口中，向下滚动直到看到 Identity Specification（标识规格）。双击 Identity Specification，你将在下方看到 (Is Identity)、Identity Increment（标识增量）和 Identity Seed（标识种子）属性，如图 12 所示。

## 图 12 显示的列的 Identity Specification 属性

| Column Properties | |
| --- | --- |
| Has Non-SQL Server Subscriber | No |
| Identity Specification | |
| (Is Identity) | No |
| Identity Increment | | |
| Identity Seed | |
| Identity Specification | Yes |

第 11 步：将 (Is Identity) 属性更改为 Yes。这该列指定为标识列。结果是该列包含唯一的自动生成的值。注意 Identity Increment 和 Identity Seed 属性都设置为 1，如图 13 所示。保持这些值不变。

图 13 设置为值的 Identity Specification 属性

![](img/9467d25da5679b16515c9401daaae36c_670.png)

第 12 步：现在你将 PersonID 列指定为标识列。在 Server Explorer (Database Explorer) 中，确保 `Phonelist.mdf` 条目已展开，如图 8 所示。右键点击 *Tables*，如图 9 所示，点击菜单上的 *Add New Table*。

图 14 作为主键的 PersonID 列

![](img/9467d25da5679b16515c9401daaae36c_671.png)

图 15 作为主键的 PersonID 列

![](img/9467d25da5679b16515c9401daaae36c_672.png)

# 数据库

## 数据库文件的位置

当你使用 Visual Studio 创建数据库时（如你在教程 1 中执行的那样），数据库文件将在项目文件夹中创建。例如，图 21 显示了 `Phonelist.mdf` 数据库文件是如何在电话簿（Phone Book）项目文件夹中生成的。

> 注意：当你创建一个 SQL Server 数据库时，你还会看到一个以 '_LDF' 扩展结尾的文件。例如，在图 21 中，你会看到一个名为 `Phonelist_log.LDF` 的文件。这是一个事务日志文件。SQL Server DBMS 使用它来保存你对数据库执行的所有操作。

**图 21** `Phonelist.mdf` 数据库文件的位置

![](img/img/9467d25da5679b16515c9401daaae36c_673_0.png)

### 检查点

- 9 按照层级顺序列出允许应用程序连接并与数据库交互的 .NET 组件。列表从应用程序作为最顶层开始。
- 10 表格适配器（table adapter）和数据源（data source）组件之间是什么关系？
- 11 使用什么组件将界面控件连接到数据集（dataset）？

# DataGridView 控件

**概念：** `DataGridView` 控件可以在可滚网格中显示数据库表。

数据绑定控件（data-bound control）是一种连接到数据源的用户界面控件。例如，一个数据绑定控件可以连接到数据库表中的某列。数据绑定控件会自动显示来自数据源的数据，并可用于更改它们所绑定的数据。最简单且最强大的数据绑定控件之一就是 `DataGridView` 控件。`DataGridView` 控件可以在你的应用程序表单上的可滚网格中显示整个数据库表。

在教程 2 中，你将继续开发在教程 1 中开始的电话簿应用程序。你将应用程序表单连接到 `Phonelist.mdf` 数据库，并添加一个 `DataGridView` 控件，用于查看和更新 Person 表格。

# 教程 2：完成电话簿应用程序

在本教程中，你将完成电话簿应用程序。你将 `Phonelist.mdf` 数据库作为数据源添加到项目中，创建一个连接到 Person 表格的数据集，并添加一个允许用户与数据库交互的 `DataGridView` 控件。

- 第 1 步：确保 Visual Studio（或 Visual C# Express）中打开了上一个教程中的电话簿项目。
- 第 2 步：点击 Visual Studio 菜单上的“数据 (Data)”，然后点击“添加新数据源...”。你应该看到“数据源配置向导”，如图 22 所示。

图 22 数据源配置向导——选择数据源类型

![](img/img/9467d25da5679b16515c9401daaae36c_674_0.png)

- 第 3 步：你正在添加的数据源是数据库，因此确保选中了“数据库”（Database），然后点击“下一步”。现在出现了窗口，如图 23 所示。
- 第 4 步：确保选中了“数据集”（Dataset），并点击“下一步”。现在出现了窗口，如图 24 所示。

图 23 数据源配置向导——选择数据库模型

![](img/img/9467d25da5679b16515c9401daaae36c_675_0.png)

图 24 数据源配置向导——选择你的数据连接

![](img/img/9467d25da5679b16515c9401daaae36c_675_1.png)

**第 5 步：** 在此窗口中，你被要求选择数据连接，`Phonelist .mdf` 数据库应该会被自动选中，如图 24 所示。只需点击“下一步”。现在出现了窗口，如图 25 所示。

图 25 数据源配置向导——保存连接字符串

![](img/img/9467d25da5679b16515c9401daaae36c_676_0.png)

**第 6 步：** 在此窗口中，你被询问是否保存连接字符串。勾选“是 (Yes)”并点击“下一步”。

第 7 步：在弹出的窗口中，你被要求选择要包含在数据集中的数据库对象。展开“表格 (Tables)”，选中 Person 表格，如图 26 所示。在窗口底部，你可以为数据集命名。这里是你所操作的总结：

- 你将 `Phonelist.mdf` 数据库作为数据源添加到项目。
- 你创建了一个连接到 Person 表格的数据集。

第 8 步：在 Visual Studio 菜单上点击“数据 (Data)”，然后点击“显示数据源 (Show Data Sources)”。现在出现了窗口，如图 27 所示。

图 26 选择你的数据库对象

![](img/img/9467d25da5679b16515c9401daaae36c_677_0.png)

图 27 数据源窗口

![](img/img/9467d25da5679b16515c9401daaae36c_677_1.png)

第 9 步：在此窗口中，你被要求选择数据连接，`Phonelist .mdf` 数据库应该会被自动选中，如图 24 所示。只需点击“下一步”。现在出现了窗口，如图 28 所示。

图 28 表格格数据绑定控件

![](img/img/9467d25da5679b16515c9401daaae36c_678_0.png)

第 10 步：你将 `DataGridView` 控件拖动到表单上，如图 29 所示。

图 29 拖动表格到表单

![](img/img/9467d25da5679b16515c9401daaae36c_679_0.png)

图 30 表单上的 DataGridView 控件

![](img/img/9467d25da5679b16515c9401daaae36c_678_1.png)

注意设计器底部的灰色区域现在包含了几个项。这些是你在表单上放置 `DataGridView` 控件时自动生成的：

- `personTableAdapter`（表格适配器）：这是适配器，它直接从数据源获取数据。
- `tableAdapterManager`（表格适配器管理器）：在许多应用程序中，数据库有多个我们需要从中获取数据的表格。适配器管理多个表格。
- `personDataSet`（数据集）：这是数据集，它持有适配器的副本并将其保内存中。应用程序与数据集交互而不是数据库。
- `personBindings`（绑定源）：这是导航栏。

第 11 步：保存并运行应用程序。表单将与图 31 类似，Person 表的行显示在 `DataGridView` 中。你可以通过以下方式使用 `DataGridView` 控件：

- 要更改单元格的值，用鼠标点击单元格并进行更改。
- 要选择一行，点击控件左侧出现的按钮。
- 要删除一行，选择导航栏上的删除按钮 (X) 或按键盘上的 Delete 键。
- 要添加新行，滚动到网格底部，你会看到一个空行。在空行中输入新数据。
- 你所的影响仅影响留在内存中的表格副本。要保存到数据库，点击导航栏上的保存按钮 (💾)。
- 要根据列值对行进行排序，点击列标题。

图 31 运行中的电话簿应用程序

![](img/img/9467d25da5679b16515c9401daaae36c_680_0.png)

第 12 步：使用 `DataGridView` 控件对数据集进行若干更改。例如，更改现有行的值、添加新行并删除现有行。务必点击导航栏上的保存按钮 (💾) 以保存你的更改。

第 13 步：关闭应用程序并重新运行，以验证你的更改已保存。完成后，关闭应用程序。

# 数据库

# 自动生成的代码

当您将数据绑定控件（例如 `DataGridView`）放置在表单上时，Visual Studio 会在后台执行大量工作来管理控件功能。事实上，在教程 2 中，您甚至没有写一行代码就完成了应用程序的开发！但是，如果您在代码编辑器中打开表单，您将会看到 Visual Studio 生成了一些代码，如程序 1 所示。

电话簿应用程序中的程序 1 代码
