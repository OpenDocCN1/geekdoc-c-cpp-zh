

# 274 使用 C# 进行 SQL Server 数据库编程

现在让我们为 SP_Student 表编写代码，需要四个代码部分：

- 1. 该类构造函数的代码编写。
- 2. 在 SP_Student 表类中添加 LogLoginForm 类的一个新对象，`LogLoginForm loginForm = new LogLoginForm();`。
- 3. 为 **Select（选择）**和 **Back（返回）**点击方法编写代码。
- 4. 为选择表类编写代码以添加此 SP_Student 表。

打开 Student Form 类的构造函数，复制构造函数内部的所有代码并将其粘贴到 SP_Student Form 类的构造函数中。接下来让我们构建**Select按钮（选择按钮）**点击方法的代码。首先，我们需要在 SP_Student Form 代码窗口的命名空间声明部分添加 SQL Server 相关的命名空间 `using System.Data.SqlClient;`。打开 **Select** 按钮点击方法，并输入图 5.104 所示的代码。

让我们逐步讨论这段代码，看看它是如何工作的。

- A. 我们的存储过程名称 `dbo.StudentCourseINTO` 必须首先声明，且该名称必须与我们在服务器资源管理器环境中创建存储过程时使用的名称完全一致。
- B. 所有数据组件，包括 Command、Adapter、DataTable 和 DataReader 对象在这里定义，因为我们需要使用它们执行此查询。
- C. 通过用户定义方法 `BuildCommand()` 为 Command 初始化适当的属性。CommandType 属性必须为 `StoredProcedure`，以指示该查询是要执行一个存储过程。CommandText 属性必须等于我们的存储过程名称 `dbo.StudentCourseINTO`，它存储在字符串变量 `strStudentCourse` 中。
- D. 存储过程的输入参数是学生姓名，从 **Student Name（学生姓名）** 组合框获取。它应该被添加到 Command 对象的 Parameters 集合中。你需要注意，名名 `@stdName` 必须与我们存储过程 `dbo.StudentCourseINTO` 中定义的输入参数名完全一致。实际参数是在项目运行时由用户输入的。完成后的 Command 被分配给 DataAdapter 的 `SelectCommand` 属性，稍后将从 `Student` 表中获取 `course_id`。
- E. 如果用户选择 **DataAdapter Method（适配器方法）**，则调用 `Fill()` 方法向 StudentCourse 表填充所需的 `course_id`。
- F. 如果属性大于 0，则意味着填充成功。调用用户定义方法 `FillCourse()` 将 `course_id` 获取到 CourseList listBox 中。否则，将显示错误消息以指示此情况。
- G. 如果用户选择 **DataReader Method（读取器方法）**，则执行 `ExecuteReader()` 方法调用 DataReader 来调用我们的存储过程。
- H. 如果成功，查询结果应存储在 DataReader 的某些行中。在这种情况下，执行用户定义方法 `FillCourseReader()` 将 `course_id` 返回到 CourseList Box 中。如果调用失败，则显示错误消息。
- I. 执行任务以释放此数据查询中使用的所有对象。

所有用户定义方法，如 `BuildCommand()`、`FillCourseList()` 和 `FillCourseReader()` 都与 Student Form 中的那些方法相同，无需任何修改。只是所有这些方法

## 使用 Visual#.NET 进行数据选择查询

| SPSelect 项目 | cmdSelect_Click() |
| :--- | :--- |

```csharp
using System.Data;
using System.Data.SqlClient;

namespace SPSelect_Project
{
    public partial class SpForm : Form
    {
        public LoginForm loginForm = new LoginForm();
        public SpForm()
        {
            InitializeComponent();
            ComboName.Items.Add("Tom Erica");
            ComboName.Items.Add("Ashly Jade");
            ComboName.Items.Add("Holes Smith");
            ComboName.Items.Add("Andrew Woods");
            ComboName.Items.Add("Blue Valley");
            ComboMethod.Items.Add("DataAdapter Method");
            ComboMethod.Items.Add("DataReader Method");
            ComboMethod.SelectedIndex = 0;
        }

        private void cmdSelect_Click(object sender, EventArgs e)
        {
            string sqlStudentCourse = "dboStudentCourseINTO";
            SqlDataAdapter studentCourseDataAdapter = new SqlDataAdapter(sqlStudentCourse);
            SqlCommand cmdSelectStudentCourse = new SqlCommand(sqlStudentCourse);
            DataTable studentCourseTable = new DataTable();
            SqlDataReader studentCourseReader = 

            BuildCommand(ref cmdSelectStudentCourse, studentStudentCourse);
            cmdSelectStudentCourse.Parameters.Add("@studentname", SqlDbType.Char).Value = ComboName.Text;
            studentCourseDataAdapter.SelectCommand = cmdSelectStudentCourse;
            if (ComboMethod.Text == "DataAdapter Method")
            {
                studentCourseDataAdapter.Fill(studentCourseTable);
                if (studentCourseTable.Rows.Count > 0)
                    FillList(studentCourseTable);
                else
                    MessageBox.Show("No course_id found!");
            }
            else //选择了 DataReader
            {
                studentCourseReader = cmdSelectStudentCourse.ExecuteReader();
                if (studentCourseReader.HasRows == true)
                    FillDataReader(studentCourseReader);
                else
                    MessageBox.Show("No course_id found!");
                studentCourseReader.Close();
            }
            studentCourseTable.Dispose();
            studentCourseDataAdapter.Dispose();
            cmdSelectStudentCourse.Dispose();
        }
    }
}
```

图 5.104 select 按钮点击方法的代码。

# 276 使用 C# 进行 SQL Server 数据库编程

| SPSelect | FillCourseList(DataTable StudentCourseTable) |
| :--- | :--- |

```csharp
private void FillCourseList(DataTable StudentCourseTable)
{
    CourseList.Items.Clear();
    foreach (DataRow row in StudentCourse.Rows)
    {
        CourseList.Items.Add(row[0]); //第一列是 course_id - strStudentCourse
    }
}
private void FillCourseReader(DataReader StudentCourseReader)
{
    int pos;
    CourseList.Items.Clear();
    for (pos = 0; pos <= StudentCourseReader.FieldCount - 1; pos++)
    {
        CourseList.Items.Add(StudentCourseReader.GetValue(pos).ToString());
    }
}
```

**图 5.105** 两个方法的代码。

