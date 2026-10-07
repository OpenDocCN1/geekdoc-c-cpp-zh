

## 5.15.6.2 为用户定义方法构建代码

在课程表单已打开的代码窗口中，将图 5.84 所示的代码输入此代码窗口。让我们仔细观察几段代码，看看它们是如何运行的。

- A. 对于第一个方法 `FullCourseTextBox()`，首先声明了一些局部变量和对象，包括一个作为循环计数器的本地整数变量 `pos`，以及一个作为数据持有器的 `TextBox` 数组 `cTextBox[]`，用于存储要在六个 `TextBox` 中显示的所有课程信息。
- B. 为了检查并获取匹配的列，使用了两个 `foreach` 循环。外层循环用于选择选定的行，内层循环用于每一列。实际上，外层循环只运行一次，而内层循环共有 6 列，代表 6 份课程信息需要被检查和收集。
- D. 每个选定的列都通过 `TextBox cTextBox[]` 分配给课程表单中相关的 `TextBox`，并通过 `Text` 属性显示每一项。需要注意的是，所选的列 `row[column]` 是一个对象，必须通过 `ToString()` 转换为字符串，然后分配给该属性。
- E. 外层循环 `pos` 每次循环都会更新，以便为 `TextBox` 设置正确的位置来存放检索和收集的列。
- F. 对于第二个方法 `FillCourseReader()`，首先声明了一些局部变量和对象，包括一个作为循环计数器的本地整数变量 `intIndex`，以及一个作为数据持有器的 `TextBox` 数组 `cTextBox[]`，用于存储要在六个 `TextBox` 中显示的所有查询信息。
- G. 使用 `while()` 循环，循环条件为 `DataReader` 的 `Read()` 方法。这意味着只要 `Read()` 方法返回 true，`while()` 循环就会继续，这意味着已从 `DataReader` 中检索到有效列。

| RTOSelectProject | FillCourseTextBox(DataTable CourseTable) |
|---|---|
| private void FillCourseTextBox(DataTable CourseTable) { int pos = 0; TextBox[] cTextBox = {txtCourseID, txtCourseName, txtCredits, txtClass, txtSchedule, txtEnroll}; foreach (DataRow row in CourseTable.Rows) { foreach (DataColumn column in CourseTable.Columns) { cTextBox[pos].Text = row[column].ToString(); pos++; } } } private void FillCourseReader(SqlDataReader CourseReader) { intIndex = 0; TextBox[] cTextBox = {txtCourseID, txtCourseName, txtCredits, txtClass, txtSchedule, txtEnroll}; while (CourseReader.Read()) { for (int intIndex = 0; intIndex < CourseReader.FieldCount - 1; intIndex++) cTextBox[intIndex].Text = CourseReader.GetValue(intIndex).ToString(); } } |

FIGURE 5.84 两个用户定义方法的详细代码。

## 使用 Visual#.NET 进行数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_285_0.png)

**图 5.85** 课程的运行状态。

- H. 在 **while** 循环内部，利用 **for** 循环选取每一列并将其分配给课程表单窗口中相关的 `TextBox` 以显示。需要注意的是，此循环的上限是 **FieldCount - 1**，列的顺序从 0 开始。

我们现在已经完成了课程表单的所有编码工作，可以开始运行为 `CourseForm` 类开发的测试。点击顶部的 Start（开始）按钮运行我们的项目。通过输入用户名和密码完成登录过程，然后输入 **jheny** 和 **test**。然后选择 Course Information（课程信息）项目，并点击选择表单上的 OK（确定）按钮打开课程表。点击默认的教师名称和查询方法，然后点击 Select（选择）为选定的方法查询所需的课程 (**course_id**）。结果如图 5.85 所示。

现在你可以通过点击 CourseList 中的其中一个来选择 **course_id**。立即，你会发现该课程（**course_id**）的详细信息显示在右侧的 `TextBox` 中。

你也可以尝试从 Query Method（查询方法）组合框框中选择 **DataReader** 方法，以测试项目对我们示例数据库中的表执行每次查询。

一个完成的项目 **RTSelectProject** 可以在 CRC fit 网站的 **Class DB Projects\RTSelectSolution** 文件夹找到，该文件夹位于网站的 **Students** 文件夹下（参见第 1 章中的图 1.2）。

接下来讨论如何通过存储过程查询数据。

## 5.16 使用存储过程查询数据

存储过程不仅仅是应用于任何用编程语言开发的项目中的函数或过程。这意味着存储过程可以被视为函数或子程序，它们可以带有任何参数被轻松调用，并返回特定类型的任何数据。你可以将多个 SQL 语句集成到单个存储过程中，以便一次执行多次查询，而这些语句将由 SQL Server 预编译以形成一个集成的主体。通过这种方式，预编译的主体与你在 Visual C# 环境中开发的代码隔离开。你可以在项目运行时从你的 Visual C# 2022 项目中轻松调用存储过程。使用存储过程的结果是数据驱动应用程序的性能可以大大提高，数据查询速度可以显著加快。此外，当开发一个存储过程时，数据库服务器会自动根据该过程创建执行计划，每当数据库服务器进行任何修改时，开发的计划也会自动更新。

通常，存储过程有三种类型：系统存储过程、扩展存储过程和自定义存储过程。系统存储过程是为管理、维护、配置和监控 SQL Server 而开发的。扩展存储过程以动态链接库 (dll) 格式开发和应用。这种存储过程可以动态链接到你的项目中，从而提高运行速度并节省运行空间。自定义存储过程是由用户为其应用程序开发和实现的。

### 5.16.1 创建存储过程

通常，有五种可能的方法创建存储过程。

- 1) 使用 SQL Server Enterprise Manager
- 2) 使用 Query Analyzer
- 3) 使用 ASP 代码
- 4) 使用 Visual Studio.NET - 实时编码方法
- 5) 使用 Visual Studio.NET - Server Explorer

对于 Visual C# 开发者来说，更倾向于使用 Visual Studio.NET 中的 Explorer。创建存储过程的一种更复杂但灵活的方法是使用 Visual Studio.NET 的实时编码方法。在本节中，我们将集中在上述列出的第五种方法上。创建存储过程的原型或语法如图 5.86 所示。
对于 SQL Server 数据库，存储过程名称始终带有关键字 dbo 作为前缀。示例存储过程如图 5.87 所示。

```sql
CREATE PROCEDURE Stored Procedure's name
{
@Param1's name Param1's data type Input/Output,
@Param2's name Param2's data type Input/Output
}
AS
(DECLARE Your local variables.... If you have)
(Your SQL Statements)
RETURN
```

FIGURE 5.86 SQL 存储过程 dbo.StudentInfo 的原型

```sql
CREATE PROCEDURE Student
{
@StudentName VARCHAR(50)
}
ASSELECT student_id FROM Student
WHERE name = @StudentName
RETURN
```

FIGURE 5.87 示例 SQL Server 存储过程。

## 使用 Visual C#.NET 进行数据选择查询

在大括号内声明的参数是用于此存储过程的输入或输出参数。在 SQL Server 数据库中，参数前必须加有 @ 符号。从调用过程发送到此存储过程的任何参数都应在此声明。使用 DECLARE 关键字创建的其他变量是局部变量，只能在此存储过程中使用。RETURN 关键字用于返回查询数据列。

## 5.16.2 调用存储过程

当存储过程创建后，它就准备好被你的 Visual C# 2022 项目调用。你可以使用 DataAdapter 中定义的任何 `Fill()` 方法来填充数据表，或者使用 `ExecuteReader()` 方法将结果返回给 DataReader。上述方法用于单表查询，这意味着存储过程中定义的 SQL 语句仅针对一个数据表执行。如果你想开发一个对表进行多次查询的存储过程，你需要使用系统方法 `SqlCommand()`。

通过 DataAdapter 的 `Fill()` 方法从 Visual C# 项目调用存储过程，需要遵循以下语法：

- 1) 创建 Connection 对象并打开。
- 2) 创建 Command 对象并初始化。
- 3) 如果有，创建任何 Parameter 对象并添加到 Command 对象。
- 4) 使用 TableAdapter 类中的 Fill() 方法执行存储过程。

图 5.88 显示了示例代码，说明了如何调用名为 dbo.StudentInfo 的存储过程（假设 Connection 对象已创建）：

- A. 此处声明了一些常用的数据组件，如 DataAdapter、Command 和 DataTable。
- B. 通过分配关联组件初始化 Command 对象。第一个组件是 Connection 对象。
- C. 为了执行存储过程，必须在此使用关键字 StoredProcedure 并将其分配给 Command 对象的 CommandType 属性，表示执行此 Command 对象将调用存储过程。
- D. 存储过程的名称必须分配给 Command 对象的 CommandText 属性。该名称与创建存储过程时使用的名称完全相同。

```csharp
SqlDataAdapter DataAdapter = new SqlDataAdapter();
SqlCommand SqlCommand = new SqlCommand();
DataTable sqlType = new DataTable();
SqlCommand.Connection = Connection;
SqlCommand.CommandType = CommandType.StoredProcedure;
SqlCommand.CommandText = "dbo.StudentInfo";
SqlCommand.Parameters.Add("StudentName", SqlDbType.Char).Value = StudentName.Text;
StudentDataAdapter.Fill(sqlTable);
if (sqlTable.Rows.Count > 0)
    收集检索到的数据列.....
else
    MessageBox.Show("未找到匹配的学生!");
```

FIGURE 5.88 调用存储过程的示例。

