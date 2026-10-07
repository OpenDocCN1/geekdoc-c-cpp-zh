

# 222
# 使用 C# 进行 SQL Server 数据库编程

| SelectWizard Project | cmdBack_Click(object sender, EventArgs e) |
|---|---|
| private void cmdBack_Click(object sender, EventArgs e) { \n  this.Hide(); \n } | |

图 5.57 返回按钮的代码。

在这种情况下，需要用户来处理此问题。用户可以继续选择正确的院系名称或退出项目。如果此属性不为 0，则表示填充成功并找到了匹配的院系名称，且我们 Dataset 中的表（Table）已填充。与匹配院系相关的记录将显示在 TextBoxes 和 PictureBox 中。

D. 否则，选择了 LINQ & DataSet 方法，并调用了用户定义的方法 LINQToDataSet()（该方法将在下文中开发），以使用 LINQ 查询方法检索返回信息。

返回按钮 Click 方法的代码非常简单。点击此按钮时，Faculty Form（院系表）将被隐藏。为此使用了 `Hide()` 方法，如图 5.57 所示。

### 5.11.2 开发使用 LINQ 方法查询数据的代码

LINQ 查询技术是最流行的查询方法之一，广泛应用于现代数据库编程应用程序中。使用此技术可以显著地整合和改进查询过程。我们已经在第 4 章中对这项技术进行了非常详细的讨论。请参考该章节以获得该问题的清晰思路。在这一部分，我们将集中于该方法的实现。

如果 Faculty Form 的代码窗口未打开，请打开它，定义一个用户定义方法，并将如图 5.58 所示的代码输入到该方法中。

| SelectWizard Project | LINQToDataSet() |
|---|---|
| A; using System.LINQ; | |
| B { \n  this.facultyTableAdapter.Fill(cse_DeptDataSet.Faculty); \n  var facultyInfo = (from row in cse_DeptDataSet.Faculty \n  where row.Field("faculty_name").Equals(ComboBox.Text) \n  select row); \n  foreach (var row in facultyInfo) { \n  this.facultyID.Text = row.faculty_id; \n  this.facultyName.Text = row.faculty_name; \n  this.title.Text = row.title; \n  this.office.Text = row.office; \n  this.college.Text = row.college; \n  this.email.Text = row.email; \n  this.Photo.Image = Image.FromStream(new MemoryStream(row.Image)); \n}\n} | |

图 5.58 LINQ 方法的详细代码。

## 使用 Visual#.NET 进行数据选择查询

让我们看看这段代码是如何工作的。

- A. 启用了 `System.IO` 命名空间以使用方法 `MemoryStream()` 将 Faculty 表中数据类型为 `byte[]` 的列转换为 `System.Drawing.Image`，以便在表单的 PictureBox 中接受并显示所选院系的图像。
- B. 然后，使用 `facultyTableAdapter` 的默认 `Fill()` 方法将 Faculty 表中的数据加载到 DataSet 中。因为 LINQ 是应用于 DataSet 的，在实现之前，DataSet 必须包含所有表中的有效数据。
- C. 构建并执行了一个典型的 LINQ 查询结构，以检索所选院系的所有信息。`facultyQuery` 是一个隐式类型局部变量，类型为 `var`。C# 将自动将 `var` 转换为任何其他数据类型。事实上，
- D. 使用 `foreach` 循环从所选的数据行 `Row` 中提取每一列，该 `Row` 是从上述 LINQ 查询中获取的。
- E. 将每一列分配给所选的 TextBox，以便在 Faculty Form 窗口中显示它们。
- F. 最后，我们需要调用带参数的系统方法 `MemoryStream()`，该参数是 `MemoryStream` 类的一个新对象，其中嵌入了我们 Faculty 表中的图像，以将后者从 `byte[]` 转换为 `System.Drawing.Image` 类型。后者可以被我们表单中的 PictureBox 接受并显示给所选院系。

至此，我们完成了此表单的代码处理。不要忘记删除图 5.56 所示代码中 LINQ 子句的注释，我们已经完成了该部分的构建。现在我们可以运行并测试我们的项目了。

点击 `Build | Solution` 方法构建我们的项目，并点击 `Start` 按钮运行项目。在 Login 处输入用户名和密码。点击 `Login` 按钮打开 Selection Form，从 ComboBox 中选择院系名称，并点击 `Select`。与所选院系相关的所有信息将显示出来，如图 5.59 所示。你可以选择每个 TableAdapter 或 LINQ DataSet 让不同成员执行不同的查询，以确认我们过程的正确性。此时，我们完成了通过 Faculty Form 对 Faculty 表的查询过程。接，我们将处理 Course Form。

## 5.12 在 COURSE FORM 中绑定数据到关联课程

该表的功能通过以下步骤所示：

- 1) 此表允许用户在点击 `Select` 时，通过 Faculty Name 控件从选择的院系查找课程。所有查询到的课程 (course_id) 都显示在 List 中。
- 2) 通过点击 List 中所需的课程，可以获取每个课程的详细信息（如课程 ID、课程标题、课程安排和人数），并显示在 TextBox 控件中。
- 3) Back 按钮允许用户返回 Selection Form 进行其他选择，或获取与该选择所需的信息。

# 使用 SQL Server 数据库编程

img/d59a4750d0a20fc0449fb7252.png
59 运行状态，使用 C# 的 SQL Server

该表的功能通过以下步骤说明：

- 1) 此表允许用户在点击 `Select` 时，通过 Faculty Name 控件从选择的院系查找课程。所有查询到的课程 (course_id) 都显示在 List 中。
- 2) 通过点击 List 中所需的课程，可以获取每个课程的详细信息（如课程 ID、课程标题、课程安排和人数），并显示在 TextBox 控件中。
- 3) Back 按钮允许用户返回 Selection Form 进行其他选择，或获取与该选择所需的信息。

在本节中我们将讨论 `Insert`、`Update` 和 `Delete` 按钮。为了找到所选院系的课程，我们需要使用 LINQ 查询方法。在实现此之前，DataSet 必须包含所有表中的有效数据，因为 LINQ 是应用于 DataSet 的。为了检索所选院系的所有信息，我们构建并执行了一个典型的 LINQ 查询结构。`facultyQuery` 是一个隐式类型局部变量，类型为 `var`。C# 将自动将 `var` 转换为任何其他数据类型。事实上，

- D. 使用 `foreach` 循环从所选的数据行 `Row` 中提取每一列，该 `Row` 是从 `facultyinfo` 中通过上述 LINQ 查询获取的。
- E. 将每一列分配给所选的 TextBox，以便在 Faculty Form 窗口中显示它们。
- F. 最后，我们需要调用带参数的系统方法 `MemoryStream()`，该参数是 `MemoryStream` 类的一个新对象，其中嵌入了我们 Faculty 表中的图像，以将后者从 `byte[]` 转换为 `System.Drawing.Image` 类型。后者可以被我们表单中的 PictureBox 接受并显示给所选院系。

至此，我们完成了此表单的代码处理。不要忘记删除图 5.56 所示代码中 LINQ 子句的注释，我们已经完成了该部分的构建。现在我们可以运行并测试我们的项目了。

点击 `Build | Solution` 方法构建我们的项目，并点击 `Start` 按钮运行项目。在 Login 处输入用户名和密码。点击 `Login` 按钮打开 Selection Form，从 ComboBox 中选择院系名称，并点击 `Select`。与所选院系相关的所有信息将显示出来，如图 5.59 所示。你可以选择每个 TableAdapter 或 LINQ DataSet 让不同成员执行不同的查询，以确认我们过程的正确性。此时，我们完成了通过 Faculty Form 对 Faculty 表的查询过程。接，我们将处理 Course Form。

## 5.12 在 COURSE FORM 中绑定数据到关联课程

该表的功能通过以下步骤所示：

- 1) 此表允许用户在点击 `Select` 时，通过 Faculty Name 控件从选择的院系查找课程。所有查询到的课程 (course_id) 都显示在 List 中。
- 2) 通过点击 List 中所需的课程，可以获取每个课程的详细信息（如课程 ID、课程标题、课程安排和人数），并显示在 TextBox 控件中。
- 3) Back 按钮允许用户返回 Selection Form 进行其他选择，或获取与该选择所需的信息。

# 使用 SQL Server 数据库编程

为了找到所选院系的课程，我们需要使用 LINQ 查询方法。在实现此之前，DataSet 必须包含所有表中的有效数据。让我们构建第二个查询来找到所选院系的课程。打开 DataSet Designer 以创建我们所需的查询并修改 `facultyTableAdapter` 的 `(Fill)` 方法。通过点击 `View | Other Windows | Data Sources` 菜单打开数据源。然后右键点击该窗口中的任何项并选择 `Edit DataSet with Designer` 以打开 DataSet Designer。右键点击 Course 表的最后一行并选择 `Add Query` 打开 TableAdapter 查询配置向导。保持默认选择 `SELECT` 语句并点击 `Next`。同样保持顶部的 `SELECT` 返回下一个窗口中的行并点击 `Next`。然后点击 `Query Builder` 按钮打开图 5.61 中的向导。

保持此图形化查询的默认选择。我们只需要 `course_id` 列，稍后将解释为什么我们需要保留这些默认项。在 `faculty_id` 行的 Filter 列上输入一个问号 `?` 并按下回车键。这等同于设置根据 `faculty_name` 过滤所选院系。

- 4) 在输出面板中取消勾选 `faculty_name` 列的复选框，因为我们不想将其作为输出。相反，我们需要使用它作为查询条件。

img/d59a4750d0a20fc0449fb7253.png
图 5.60 关于 `faculty_id` 的完成查询

- 5) 在第二个面板中，右键点击 `Group By` 列并从弹出菜单中选择 `Edit Item` 以删除此分组依据。
- 6) 在 `faculty_name` 的 Filter 列上输入字符 `?` 并按下回车键。你完成的 Query Builder 应该与图 5.60 所示的匹配。

```
SELECT faculty_id FROM Faculty WHERE (faculty_name = @Param1)
```

点击 `OK` 按钮和 `Next` 按钮进入下一个窗口继续。在框中输入 `FacultyIdByName` 作为你的函数名，然后点击 `Next` 和 `Finish` 按钮完成此查询的构建。

