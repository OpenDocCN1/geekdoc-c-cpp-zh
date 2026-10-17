
如果课程表单（Course Form）的代码窗口未打开，请打开它，然后创建一个新方法 `LINQToDataSet`，并将图 5.65 所示的代码输入该方法中。

让我们来看看这段代码是如何运行的。

- **A.** 首先需要调用查询方法 `FillByFacultyID()`，该方法将在 5.12 节中构建，用于将课程数据从 Course 表加载到我们 DataSet 中的 Course 中。这一操作对于我们的后续操作是重要且必要的，即从 DataSet 中的 Course 表中检索数据并将其显示在课程列表中。

- **B.** 创建并执行一个典型的 LINQ 查询结构，以检索所选教师的所有相关课程信息。`courseinfo` 是一个带有数据类型的 C# 隐式类型变量 `var`。C# 2022 在看到它时，能够自动将其转换为任何合适的数据类型（在本例中是一个 DataSet）。这里使用一个迭代变量 `ci` 来遍历来自 Course 表的此查询结果。然后将执行一个带有 `WHERE` 子句的类似 SQL SELECT 的语句。

- **C.** 利用 `foreach` 循环从选定的数据行 `crow` 中提取每一列，该行是从我们通过 LINQ 查询获取的 `courseinfo` 的。

将每一列分配给 TextBox 以便在课程窗口中显示。

在分配过程中存在一个复杂性，即 `foreach` 循环的最后一次运行。当 `foreach` 循环运行时，迭代变量 `crow` 中的课程 ID 和课程名称列（`crow.course_id` 和 `crow.course`）将包含这两个值，即使我们只想第一个 `course_id` 和 `course` 分配给变量。为了避免此错误，前两个赋值不能包含在此循环中。因此，我们应该注释掉前面的赋值，并将这些列分配到课程窗口中的课程 ID 和课程文本框中？这项工作可以由 `BindingSource` 处理，因为你可以点击并自动从 `CourseList` 框中选择 `course_id`。

到此时，我们已经完成了课程项目的所有代码。在测试之前，不要忘记删除图 5.64 中 `LINQToDataSet()` 方法中的注释符号，使该方法生效。

现在点击 `Start`（启动）按钮运行我们的项目。在登录表单中输入 `ybai` 和 `come` 作为用户名和密码，然后从选择表单中选择 `Course Information`（课程信息），点击 `OK` 按钮打开我们的课程表单，如图 5.66 所示。

## 使用 Visual C#.NET 进行数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_259_0.png)

图 5.66 课程的运行状态。

在打开的课程表单窗口中，选择默认姓名 Ying Bai 并点击 Select（选择），以便该教师的所有课程 (`course_id`) 加载并填充到我们 DataSet 中的表中，作为此表单中的 Course ListBox（课程列表框）。

填充后的 `course_id` 显示在 Course ListBox 中，如图 5.66 所示。

现在让我们更进一步，从 Course ListBox 中点击一个 `course_id`。立即，所选课程的详细信息（包括课程 ID、课程名称、时间表、教室、学分和选课人数）将显示在文本框中。这是合理的，因为这些文本框已绑定到我们 DataSet 中 Course 表的六列。当你从 Course ListBox 中点击一个 `course_id` 时，你实际上是从 Course 表中选择并提取了一门课程。记住，当我们在 5.12 节中使用 `BindingSource` 执行数据绑定时，ListBox 绑定到了我们 DataSet 中的 Course 表。对于所选的课程，六列记录已绑定到表单中的六个文本框，因此数据也将反映在这些六个文本框上。这些关系可以通过图 5.67 中的连接来表示和说明。

你可以选择 LINQ to DataSet 方法来执行此查询，查询结果相同且没有问题。

这非常有趣，不是吗？

是的！这就是 Visual Studio 2022 提供的力量。通过使用这些设计工具和向导，在 Visual C# 2022 环境下开发数据库编程非常容易，并且在 Windows 应用程序的模板中开发数据库编程变得非常简单。

我们还有最后一个表单，即学生表单（Student Form），但我们想把这项作业留给学生，让他们自己完成学生表单与学生表以及 StudentCourse 表之间数据连接和查询的。

## 使用 C# 进行 SQL 编程

![](img/d59a47501d0a20fc0460a49c46c6fb7_260_0.png)

图 5.67 ListBox 与 TextBox 之间的关系。

## 第二部分使用运行时对象的查询

与我们在第一部分开发的数据驱动应用程序 SelectWizard 项目相比，后者使用了 Visual Studio 提供的许多工具和向导（例如 DataSet、BindingSource、BindingNavigator 和 Adapter）来帮助读者方便地开发数据驱动应用程序，而本部分与这些工具和向导无关。这意味着我们通过直接编写 C# 代码来创建 ADO.NET 对象。所有对象都在运行时创建。

使用 Visual Studio 工具和向导创建连接的缺点是，生成的连接与向导绑定并嵌入程序中，一旦程序中的连接信息编译，无法修改。也就是说，你的程序无法在其他平台上发布和运行。

与设计工具和向导相比，使用运行时对象简化数据操作的优势在于：

1. 它为程序员创建连接对象对象和 ADO.NET 数据操作对象提供了更大的灵活性。

2. 它允许读者使用不同的方法访问和处理数据源以及数据库。

# 使用 Visual C#.NET 进行数据查询

## 5.14 运行时对象简介

运行时对象（Runtime objects）可以定义为：在数据驱动应用中，用于数据连接和操作的对象或实例是在项目运行期间创建并实现的；换句话说，对象是动态创建并利用的。为了理解数据驱动应用中哪些类型的对象是通常用的，让我们详细讨论一下 ADO.NET 提供的最实用的类。

根据第 3 章节，ADO.NET 架构可以分为三个部分：数据提供程序（Data Provider）、DataSet 和 DataTable。这三个组件与不同的类直接相关，如图 5.68 所示。

数据提供程序提供了四种组件：

- 1) 数据连接 (`Data Connection`)
- 2) 数据命令 (`Data Command`)
- 3) 数据读取 (`DataReader`)
- 4) 表格适配器 (`DataAdapter`)

数据提供程序内部的所有组件都是依赖于数据提供程序的组件，这意味着包括连接、命令、适配器（`DataAdapter`）和读取在内的所有组件都是根据实际的数据提供程序或数据库进行识别和命名的。例如，用于 SQL Server 数据库的数据提供程序必须以 Sql 为缀进行识别和命名，例如：

- 数据连接组件：`SqlConnection`
- 数据命令组件：`SqlCommand`
- 数据适配器 (`TableAdapter`)：`SqlDataAdapter` (`SqlTable`)
- 数据读取组件：`SqlDataReader`

所有其他数据提供程序也适用相同的定义。这四类数据提供程序的所有类、方法、属性和常量位于四个不同的命名空间中：`System.Data.OleDb`、`System.Data.SqlClient`、`System.Data.Odbc` 和 `System.Data.OracleClient`。

如图 5.68 所示，在 Visual C# 数据库编程中经常使用四种数据对象。用户必须使用特定的前缀根据实际数据库创建连接对象。

| 参数 | 连接 | 连接命令 SELECT INSERT UPDATE DELETE 命令 ExecuteReader ExecuteNoneQuery DataReader INSERT UPDATE DELETE SELECT |
| :--- | :--- | :--- | :--- | :--- |
| 数据提供程序 | OLEDB | SQL Server | ODBC | ORACLE |
| OleDb 连接 | `SqlConnection` | `OdbcConnection` | `Oracle Connection` |
| OleDb 命令 | `SqlCommand` | `OdbcCommand` | `Oracle Command` |
| 数据适配器 | OleDb | Sql | Odbc | Oracle |
| DataSet | | | | |
| DataTable | | | | |

图 5.68 ADO.NET 提供的类。

# 使用 C# 进行 SQL Server 数据库编程

然而，ADO.NET 中的两个组件是不依赖于数据提供程序的：`DataSet` 和 `DataTable`。这两个组件位于 `System.Data` 命名空间下。在应用程序中使用这两个组件时，不需要使用任何前缀。`DataSet` 和 `DataTable` 都可以使用 `DataAdapter` 或适配器组件进行填充。

ADO.NET 提供了不同的类，允许用户使用不同的方法开发数据驱动应用。其中，本章将详细讨论两种流行的方法。

第一种方法是使用所谓的 DataSetDataAdapter 方法来构建数据驱动应用。在实际应用中，当 `DataSet` 和 `DataTable` 类被嵌入 `DataSet` 时，具有不同的角色，每个表都可以使用 `DataAdapter` 提供的不同查询方法（作为 `SelectCommand`、`InsertCommand`、`UpdateCommand` 或 `DeleteCommand`）进行填充、插入、更新和删除。如图 5.68 所示，当你使用这种方法时，命令对象和参数对象被嵌入或附加到 `DataAdapter`（由阴影块表示），而 `DataTable` 被嵌入 `DataSet` 中（由另一个阴影块表示）。这种方法相对简单，因为你不需要调用某些特定对象（如 `DataReader` 或 `ExecuteNonQuery`）来完成此数据查询。你只需要调用表的关联命令即可完成此操作。但这种简单性给你的应用带来了一些局限性。例如，你无法通过这个指定的 `DataAdapter` 分别访问数据表以执行多个特定操作。

第二种方法是单独使用每个对象，这意味着你不需要使用 `DataAdapter` 或将 `DataTable` 嵌入 `DataSet` 中。这提供了更大的灵活性。在这种方法中，不需要 `DataAdapter` 或 `DataSet`，你可以使用新连接创建一个新的命令对象，然后构建查询语句并为该查询附加一些实用的参数供 `DataReader` 对象；你还可以通过调用 `ExecuteReader()` 方法执行任何数据操作，或通过调用 `ExecuteNonQuery()` 执行任何数据操作来修改 `DataTable`。

除了这两种方法外，本章后面还将讨论微软在 Visual Studio 2008 中引入的 LINQ 方法。

在本节中，我们将提供四个示例项目来涵盖这两种流行方法以及 LINQ 方法：`RTSelect` 项目、`SPSelect` 项目、`LINQSelect` 和 `LINQSPProject`，它们分别与四种查询方法相关：运行时对象方法、存储过程方法、LINQ 方法和 LINQ to SQL Server 方法。

为了更好地了解 LINQ 方法，请参阅第 4 章节。为了更好地理解这两种流行方法，我们需要清晰了解如何使用 ADO.NET 的相关类和方法开发数据驱动应用。

## 5.14.1 使用运行时对象构建数据驱动应用的步骤

首先，我们将关注传统的运行时对象查询方法，LINQ 和存储过程方法将在本章稍后讨论。

回想一下我们在第 3 章节中讨论的 ADO.NET 架构和重要类。为了 Visual C# 项目连接并实现数据库，我们需要按照以下列出的顺序：

- 1) 创建具有正确参数的新连接字符串（`Connection String`）。
- 2) 使用第 1 步构建的合适连接字符串创建一个新的连接对象。
- 3) 使用 Try-Catch 块调用 `Open()` 方法打开数据库连接。
- 4) 创建新的表格适配器 (`DataAdapter`) 对象。
- 5) 创建可以填充数据的 `DataTable` 对象。
# 使用 Visual C#.NET 进行数据查询
- 6) 使用 `SelectCommand`（或 `Fill()`）或 `DataReader` 调用合适的命令/对象进行数据查询。
- 7) 将数据填充到 Visual C# 表单窗口上的绑定控件中。
- 8) 释放已使用的 `OleDataAdapter`、`Command`、`DataTable` 和 `DataReader` 对象。
- 9) 如果不需要数据库操作，则关闭数据库连接对象。

现在让我们开发一个示例项目，通过 Faculty Form 使用运行时对象访问 SQL Server 2019 Expression 数据库的数据。

## 5.15 使用运行时对象进行 SQL Server 数据库查询

如第 3 章节所述，需要使用不同的数据提供程序来访问不同的数据库，ADO.NET 为三种不同的数据提供程序提供了不同的命名空间：用于 OLEDB 的 `System.Data.OleDb`，用于 SQL Server 的 `System.Data.SqlClient` 以及用于 Oracle 的 `OracleClient`。我们将其分为两个部分：1) 使用运行时对象进行数据查询；2) 使用运行时对象通过 LINQ 方法进行数据查询。LINQ to SQL 是一种由 Visual Studio 2008 提供的良好技术，处理 SQL Server 数据库的接口。我们将首先对 SQL Server 数据库的通用查询方法进行详细讨论，然后关注 LINQ 项目。我们之所以将其分为两个部分，是因为使用运行时对象的 SQL Server 2019 Expression 数据库允许连接一个数据库，这意味着它不允许两个或多个用户同时访问和使用同一个 SQL Server 2019 实例。我们将开发的第一个项目是 `RSelectFactory`，它使用通用运行时对象和 SQL 命令对象连接到我们的示例数据库文件 `CSE_DEPT`。我们将开发的第二个项目是 `LINQSelfFactory`，它使用 LINQ to SQL 技术和 `DataContext` 连接到数据库执行类似的操作。正如我们在第 4 章节中讨论的，`DataContext` 是一个特殊的类，提供数据库连接并将查询运算符转换为标准 SQL 语句以访问我们的数据库。

### 5.15.1 连接 SQL SERVER 2019 EXPRESS 数据库

基本上，使用类似的运行时对象和结构来开发访问不同数据库的数据驱动项目。例如，三种数据提供程序都需要使用连接、命令、适配器和读取对象对 `DataSet` 或 `DataTable` 执行数据查询。`DataSet` 和 `DataTable` 组件是不依赖于数据提供程序的，但前四个对象是依赖于数据提供程序的。这意味着必须使用前缀来指定为某些数据库使用了哪种数据提供程序。如果使用了 SQL Server 数据库，可以使用前缀，例如 `SqlConnection`、`SqlCommand`、`SqlDataAdapter` 和 `SqlDataReader`。

# 使用 C# 进行 SQL Server 数据库编程

连接字符串通常由五个部分组成：

- 提供程序 (`Provider`)
- 数据源 (`Data Source`)
- 数据库 (`Database`)
- 用户 ID (`User ID`)
- 密码 (`Password`)

使用通用连接字符串的典型数据连接实例可以用以下代码表示

```
Connection = new xxxConnection("Provider=MyProvider"; +
    "Data Source=MyServer"; +
    "Database=MyDatabase"; +
    "User ID=MyUserID"; +
    "Password=MyPassword");
```

在实际应用中，`xxx` 应该替换为所选的数据驱动程序，例如 `OleDb`、`Sql` 或 `Oracle`。你需要使用应用程序中实现的实际参数值来替换实际应用中的 `MyServer`、`MyDatabase`、`MyUserID` 和 `MyPassword` 等名义值。

`Provider` 参数指示你选择的驱动程序。如果你在计算机上安装了作为 SQL Server 2019 Express 的本地 SQL Server 和客户端，那么计算机名称应该是 `localhost`。如果你正在使用远程 SQL Server 实例，在你的计算机上，你需要使用远程服务器的网络名称。使用 `\SQLEX` 作为你 `provider` 参数的值。Oracle 服务器数据库也可以使用类似的值。

`Data Source` 参数指示安装或运行你的 SQL Server 实例的连接名称。`Database` 参数指示你的数据库名称。`User ID` 和 `Password` 参数用于你数据库的安全性。在大多数情况下，使用的是默认的 Windows 安全身份验证。

你也可以使用 OleDB 作为 SQL Server 数据库驱动程序。使用 OleDB 驱动连接 SQL Server 数据库的示例连接字符串可以表示：

```
Connection = new OleDbConnection("Provider=OLEDB"; +
    "Data Source=MyServer"; +
    "Database=CSE_DEPT"; +
    "User ID=MyUserID"; +
    "Password=MyPassword");
```

你需要使用应用程序中实现的实际参数值来替换此连接对象的 `MyServer`、`MyUserID` 和 `MyPassword` 等名义值。

当使用 Windows 验证模式通过 `SqlClient` 连接到 SQL Server 数据库时，连接字符串与上述字符串略有不同。`Provider` 参数应该替换为 `Server` 参数，`User ID` 和 `Password` 参数应该被替换为 `Integrated Security` 参数。使用 `SqlClient` 连接 SQL Server 数据库的示例连接字符串如下：
