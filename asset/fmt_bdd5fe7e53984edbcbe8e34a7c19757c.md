
```csharp
namespace RTOInsertSP_Project
{
    public partial class CourseForm : Form
    {
        string[] CourseInfo = new string[6];
        LogInForm loginForm = new LogLoginForm();

        public CourseForm()
        {
            InitializeComponent();
            ComboName.Items.Add("Ying Bai");
            ComboName.Items.Add("David Blair");
            ComboName.Items.Add("Black Anderson");
            ComboName.Items.Add("Steve Johnson");
            ComboName.Items.Add("Jenney King");
            ComboName.Items.Add("Alice Brown");
            ComboName.Items.Add("Delay Angel");
            ComboName.Items.Add("Jeff Henry");
            ComboName.SelectedIndex = 0;
            ComboMethod.Items.Add("DataAdapter Method");
            ComboMethod.Items.Add("Stored Procedure");
            ComboMethod.SelectedIndex = 0;
        }

        private void InitCourseInfo()
        {
            CourseInfo[0] = txtCourseID.Text;
            CourseInfo[1] = txtName.Text;
            CourseInfo[2] = txtSchedule.Text;
            CourseInfo[3] = txtClassRoom.Text;
            CourseInfo[4] = txtCredits.Text;
            CourseInfo[5] = txtEnroll.Text;
        }

        private int CheckCourseInfo()
        {
            int pos = 0, check = 0;
            for (pos = 1; pos <= 6; pos++)
            {
                if (CourseInfo[pos] == String.Empty)
                {
                    check++;
                }
            }
            return check;
        }

        private void ClearCourse()
        {
            int index;
            TextBox[] cBox = {txtCourseID, txtName, txtSchedule, txtClassRoom, txtCredits, txtEnroll};
            for (index = 0; index < cBox.Length; index++)
                cBox[index].Text = "";
        }
    }
}
```

![](img/d59a47501d0a20fc0460a49c469c6fb7_382_0.png)

图 6.43 用于数据插入前检查的代码。

**F.** 调用对象在插入后被进行清理。

**G.** 调用 `ExecuteNonQuery()` 方法的返回值等于成功插入数据库的行数或记录数。零表示没有行或记录被插入数据库，且此次数据插入失败。在这种情况下，将显示一条警告消息。

# 使用 Visual C#.NET 插入数据

| RTOInsert 项目 | `cmdInsert_Click(object sender, EventArgs e)` |
|---|---|

| private void `cmdInsert_Click(object sender, EventArgs e)` { |

| A | { int check, insert;

string `cmdString` = "dbo.FacultyCourse";

`SqlCommand` `sqlCommand` = new `SqlCommand`();

`InitCheckInfo`();

check = `CheckCourseInfo`();

if (check == 0) {

`sqlCommand.Connection` = `loginForm.Connection`;

`sqlCommand.CommandType` = `CommandType.StoredProcedure`;

`sqlCommand.CommandText` = `cmdString`;

`sqlCommand.Parameters.Add(ref sqlCommand)`;

insert = `sqlCommand.ExecuteNonQuery()`;

`sqlCommand.Dispose()`;

if (insert == 0) {

`MessageBox.Show("The data insertion is failed")`;

} else {

`ClearCourse()`;

`cmdInsert.Enabled` = false; // 清理所有课程信息

}

} | |

| I | else {

`MessageBox.Show("请填写所有课程信息框，空白列输入 NULL")`;

} | |

图 6.44 插入按钮点击方法的代码。

- **H.** 否则，此数据插入成功。所有 `TextBoxes` 中存储的信息将被清理，以便户户对该次数据插入进行检查或验证。此外，禁用了插入按钮，以避免向数据库重复插入相同数据。

- **I.** 如果返回的检查值不为零（意味着 `TextBoxes` 为空），则会显示一条警告消息，提醒用户立即填写。

用户定义的 `InsertParameters()` 的详细代码如图 6.45 所示。此代码的功能非常直观，不需要进一步解释。

现在我们已经完成了此数据插入操作的代码工作。

让我们运行项目，以使用存储过程方法测试新数据的插入。点击 `Start` 运行项目，用户名和密码均输入 `henry`，然后

| RTOInsertSP 项目 | `InsertParameters(ref SqlCommand cmd)` |
|---|---|

| private void `InsertParameters(ref SqlCommand cmd)` { |

| { `cmd.Parameters.Add("FullName", SqlDbType.Char).Value` = `ComboName.Text`;

`cmd.Parameters.Add("CourseID", SqlDbType.Char).Value` = `txtCourseID.Text`;

`cmd.Parameters.Add("Course", SqlDbType.Char).Value` = `txtCourseName.Text`;

`cmd.Parameters.Add("Schedule", SqlDbType.Char).Value` = `txtSchedule.Text`;

`cmd.Parameters.Add("Classroom", SqlDbType.Char).Value` = `txtClassRoom.Text`;

`cmd.Parameters.Add("Credit", SqlDbType.Char).Value` = `txtCredits.Text`;

`cmd.Parameters.Add("Enroll", SqlDbType.Char).Value` = `txtEnroll.Text`;

} } |

图 6.45 `InsertParameters()` 方法的代码。

# 356 使用 C# 进行 SQL Server 数据库编程

以完成登录过程。从选择表（Selection Form）中选择课程信息项以打开课程表窗口。

在关联的 `TextBox` 中输入以下数据作为新的课程记录：

| 教师名称 | Ying Bai |
|---|---|

| 课程 ID | CSE-668 |
| 课程名称 | Modern Controls |
| 时间 | M-W-F: 9:00 – 9:50 AM |
| 教室 | MTC-309 |
| 学分 | 3 |
| 注册人数 | 30 |

在教师名称下拉框中保留默认名称 `Ying Bai` 不作更改，并点击插入按钮以调用过程将此新课程记录插入数据库。数据插入后，插入按钮立即被禁用。数据插入成功了吗？为了回答这个问题，我们需要在下一节进行数据验证。

# 6.6.2.3 课程插入后的数据插入验证

为了确认或验证插入，我们使用 `Select` 按钮，即通过 `Select` 的 `Click` 方法来检索所有课程，包括所选教师教授的插入课程。要进行检查，只需点击 `Select` 按钮检索该教师所教的所有课程并显示在课程窗口。如图 6.46 所示，这是使用存储过程数据插入成功的证据。

img/d59a47501d0a20fc0460a49c469c6fb7_384_0.png

图 6.46 数据验证过程。

# 使用 C#.NET 插入数据

357

img/d59a47501d0a20fc0460a49c469c6fb7_385_0.png

图 6.47

另一种确认此数据插入的方法是从服务器管理器打开课程表。在打开的表中，可以发现我们插入的课程 `CSE-668`位于底部，如图 6.47 所示。

包含使用存储过程方法数据插入的完整 `RTOInsertSP` 项目可以在 `DB Projects> Chapter 6 RTOInsert Solution` 中找到（请参见第 1 章图 1.2）。

# 6.7 章节总结

本章讨论并分析了针对我们的 `SQL Server 2019` 数据库的四种流行数据插入方法：

- 1) 使用 `TableAdapter.Insert()` 方法插入。
- 2) 使用 `TableAdapter.Update()` 方法插入 `DataTable` 中的新记录。
- 3) 使用 `Command` 对象的 `ExecuteNonQuery()` 方法。
- 4) 使用存储过程。

使用 C# 的 SQL Server 数据库编程

该方法可以执行以将 `DataSet` 中的整个表更新到数据库中的关联表。

方法 3 是一种运行时对象方法，它更加灵活和方便，因为它允许用户向具有不同功能的多个数据表中插入数据。

方法 4 使用存储过程来代替通用查询函数。这种方法为用户在数据插入方面注定了更强的可控性和灵活性，特别是对于涉及对多个表进行多次查询的数据插入操作。

本章分为两个部分。第一部分详细讨论并分析了如何使用 `Visual Studio.NET` 工具和向导向 SQL 数据库插入数据。使用这些工具和向导开发数据插入项目非常简单容易。使用这些工具和向导的缺点是数据只能插入到有限的目标地，例如某个特定的数据表。第二部分介绍了运行时对象方法和存储过程，以提高数据插入的效率，并在数据插入中提供更多的灵活性。

本章提供了三个真实项目，以便读者在 C#.NET 环境下开发数据插入应用有一个清晰直观的认识。

# 课作业

# I. 判断题

- 1. 三种常用的数据插入方法是 `TableAdapter.Insert()`、`TableAdapter.Update()` 和 `Command` 类的 `ExecuteNonQuery()` 方法。
- 2. 与 `Fill()` 方法不同，在向数据库插入新数据之前，必须设置一个有效的数据库连接。
- 3. 人可以使用 `TableAdapter.Update` 通过单步向数据库插入新数据或记录。
- 4. 在执行 `INSERT` 查询时，`VALUES` 列表中输入参数的顺序可以与数据库中列的顺序不同。
- 5. 要向 SQL Server 数据库插入图像，该图像的数据类型应为 `Image`。
- 6. 除了使用 `Command` 类的 `ExecuteNonQuery()` 方法插入新记录外，还可以使用 Data 类的 `SqlCommand.ExecuteNonQuery()` 方法执行数据插入。
- 7. 在执行数据插入时，可以多次向数据库插入相同的数据。
- 8. 要使用 `TableAdapter.Update()` 方法向数据库插入数据，应先将新数据插入 `DataSet` 中的表。然后执行 `Update()` 方法将该数据更新到数据库。
- 9. 要使用存储过程向 SQL Server 数据库插入数据，可以在服务器资源管理器（Server Explorer）窗口中创建并测试新的存储过程。
- 10. 调用存储过程向数据库插入数据时，参数名称必须与存储过程中定义的输入参数名称完全一致。

# II. 单选题

- 1. 要使用 `TableAdapter.Insert()` 方法向数据库插入数据，需要使用 ________ 来构建：

a. 数据源（Data Source）、查询生成器

b. `TableAdapter` 查询配置向导、插入查询

c. 运行时对象、插入查询

d. 服务器资源管理器（Server Explorer）、数据源

# 使用 Visual C#.NET 插入数据

- 2. 要使用 `TableAdapter.Update()` 方法向数据库插入数据，首先需要向 ________ 添加新数据，然后将该数据更新到数据库。

a. 数据表（Data table）

b. 数据库中的数据表

c. `DataSet`

d. `DataSet` 中的数据表

- 3. 要使用 `TableAdapter.Update()` 方法向数据库插入数据，可以更新：

a. 一行数据

b. 多行数据

c. 整个数据表

d. 以上任一均可

- 4. 因为 ADO.NET 为数据库提供了断开模式，为了向数据库插入新记录，必须建立一个有效的 ________。

a. `DataSet`

b. `TableAdapter`

c. 连接（Connection）

d. `Command`

- 5. 在 SQL Server 数据库数据查询的 WHERE 子句中，应使用 ________ 运算符作为动态参数的赋值运算符。

a. =

b. LIKE

c. =

d. @

- 6. 为了确认在 SQL Server 数据库服务器资源管理器窗口中构建的存储过程是否运行，可以 ________ 该存储过程。

a. 构建（Build）

b. 执行（Execute）

c. 调试（Debug）

d. 编译（Compile）

- 7. 为 SQL Server 数据库在服务器资源管理器窗口中创建新的存储过程，可以 ________ 该存储过程并进行测试。

a. 构建（Build）

b. 执行（Execute）

c. 调试（Debug）

d. 编译（Compile）

- 8. 使用 `INSERT` 查询向 SQL Server 数据库插入数据记录，参数的数据类型必须是 ________。

a. `OleDbType`

b. `SqlDbType`

c. `OracleDbType`

d. `OracleType`

- 9. 要调用存储过程向数据库插入记录，`Command` 对象的 `CommandType` 属性必须等于 ________。

a. `CommandType.InsertCommand`

b. `CommandType.StoredProcedure`

c. `CommandType.Text`

d. `CommandType.Insert`

- 10. 使用存储过程插入数据时，`Command` 对象的 `CommandText` 属性必须等于 ___

a. `CommandType.InsertCommand` 的内容

b. `CommandType.Text` 的内容

c. 插入命令的名称

d. 存储过程的名称

# III. 练习题

1. 下文是 SQL Server 数据库中的一个存储过程。在 Visual C#.NET 中编写一段代码调用此存储过程向数据库插入新数据。

```
CREATE OR REPLACE PROCEDURE dbo.InsertStudent
@Name VARCHAR(20),
@Major text,
@SchoolYear int,
@Credits float,
@Email text
AS
INSERT Student VALUES (@Name, @Major, @SchoolYear, @Credits, @Email)
RETURN
```

2. 下文是 Visual C#.NET 中的代码段，该代码用于调用 SQL Server 数据库中的存储过程向数据库插入新记录。请通过服务器资源管理器窗口创建关联的存储过程（已设置有效的数据库连接）。
