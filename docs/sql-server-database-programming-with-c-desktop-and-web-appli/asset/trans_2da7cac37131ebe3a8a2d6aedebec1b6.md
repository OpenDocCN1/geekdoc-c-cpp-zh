

# 使用 C# 进行 SQL Server 数据库编程

RTOSelectProject 是我们在上一节中构建的，用于减少我们的工作负载。执行以下操作以完成此解决方案项目的复制粘贴和修改过程：

- 1. 打开 Windows 资源管理器窗口并浏览我们的解决方案文件夹 RTOSelect Solution。可以在该网站 Students 文件夹下的 CRC Press 提示文件夹 `Class DB Projects\Chapter 5` 中找到此文件夹和项目。
 2. 右键点击该文件夹并选择“复制项目项”以复制该文件夹，然后进入您的本地机器并验证所需的文件夹，右键点击该文件夹并选择“粘贴项”将其粘贴到您的本地文件夹中。
 3. 展开已复制的解决方案文件夹，分别将名称更改为 PSelect Solution，并将项目名称更改为 PSelect Project。
 4. 通过记事本打开重命名后的项目 PSelect Project 文件夹下的执行文件。
 5. 在打开的文件中，找到 <RootNamespace>（第 9 行）和 <AssemblyName> 标签，分别将 RootNamespace 更改为 PSelect_Project，将 AssemblyName 更改为 PSelect Project。
 6. 在同一个文件中，找到 <StartObject> 标签（第 36 行），并将其名称更改为 PSelect_Project.Program。
 7. 转到“文件 | 保存”菜单以编辑保存的文件并关闭。
 8. 在 Windows 资源管理器窗口中，将保存的文件重命名为 PSelect_Project.csproj。
 9. 双击重命名后的文件 PSelect.Project.csproj 以打开此项目。
 10. 转到解决方案管理器窗口，在窗口处右键点击 Login，点击 Login.cs 并选择“查看代码”项以打开其代码。将其命名空间更改为 PSelect_Project。
 11. 在解决方案管理器中，展开 Login.cs 文件夹并双击 Login.designer.cs。将其顶部的名称更改为 PSelect_Project。
 12. 对所有其他文件 Course.cs、Faculty.cs、Selection.cs 和 Student.cs 重复步骤 10 和 11，将它们的名称更改为 PSelect_Project。
 13. 在解决方案管理器中，双击 C# Program.cs 文件以打开它，并将其命名空间更改为 PSelect_Project。
 14. 现在转到“生成 | 生成解决方案”项以生成我们的项目，完成此复制粘贴过程。

接下来让我们开始 Student Form 窗口的编码过程。首先，为此 Student 类的构造函数编写代码。
进入解决方案管理器，右键点击 Student.cs 文件夹并选择“查看代码”项以打开其代码。将图 5.95 所示的代码输入到构造函数中。让我们仔细查看这段代码，看看它是如何工作的。

- A. 首先添加 System.Data.SqlClient 成员，因为在本节中，我们需要使用该命名空间下一依赖 SQL Data Provider 的一组数据组件。
- B. 声明一个新的 InfoObject login，生成此新对象的目的是建立到我们的示例数据库的有效连接，以获取我们需要的连接对象，以便查询 Student 表中的数据。
- C. 将所有五个学生成员添加到 Student Name 组合框中，使用户可以选择其中一个来对所选定的学生执行数据查询。SelectedIndex = 0 将 Student Name 组合框中的第一个学生设为默认。
- D. 在 Query Method 组合框中添加了两个查询方法：DataAdapter Method 和 DataReader Method，使用户可以选择其中一个来执行相关数据查询。同样，通过设置 SelectedIndex 属性将第一个查询方法选为默认方法。

# 使用 Visual#.NET 进行数据选择查询

| SPSelect Project | StudentForm() |
| :--- | :--- |
| A | `using System.Data; using System.Data.SqlClient; using System.Data.OleDb; using System.Drawing; using System.Linq; using System.Text; using System.Windows.Forms; namespace SPSelect_Project { public partial class StudentForm : Form { LoginForm logInForm = new LogForm(); public StudentForm() { InitializeComponent(); ComboName.Items.Add("Tom Erica"); ComboName.Items.Add("Ashly Jade"); ComboName.Items.Add("Holes Smith"); ComboName.Items.Add("Andrew Woods"); ComboName.Items.Add("Blue Valley"); ComboName.SelectedIndex = 0; ComboName.Items.Add("DataAdapter Method"); ComboName.Items.Add("DataReader Method"); ComboName.SelectedIndex = 0; } } }` |
| B C D | |

**图 5.95** 学生窗口构造函数的代码。

- 0. 需要注意的是，尽管为用户提供了两种查询方法，但两种方法都需要调用我们的存储过程来对示例数据库中的 *Student* 表执行相关查询。

现在，通过解决方案管理器打开 Student Form，右键点击 *Student.cs* 并选择 **Designer**（设计器）项。
然后通过双击 Student Form 上的 **Select**（选择）按钮打开 **Select** Click 方法，并将图 5.96 所示的代码输入到此方法。
让我们仔细查看这段代码，看看它是如何工作的。

- A. 将两个存储过程名称赋值给两个字符串变量 strStudent 和 strStudentCourse。名称必须与我们在两个存储过程中创建的名称相同：`dbo.StoredInfo` 和 `dbo.StoredCourseInfo`。
- B. 在后续部分声明并创建了所有数据组件，包括两个 TableAdapters、两个 DataTypes、两个 Command 对象和一个 Data。
- C. 用户定义方法 `SqlCommand` 用于使用正确的 Connection、CommandType 属性初始化第一个 Command 对象。为了执行我们的存储过程，这些属性应设置如下：
* `Connection = login.sql`
* `CommandType = CommandType.StoredProcedure`
* `CommandText = "dbo.StoredInfo"`
CommandText 的内容必须等于开发的存储过程名称。

[content]
# SQL Server Database Programming with C#

# SPSelectProject

```c
private void Select_Click(object sender, EventArgs e)
{
    string strStudent = "StudentInfo";
    string strCourse = "CourseInfo";
    SqlDataAdapter dataAdapter = new SqlDataAdapter();
    SqlDataAdapter studentCourseDataAdapter = new SqlDataAdapter();
    SqlCommand cmdStudent = new SqlCommand();
    SqlCommand cmdCourse = new SqlCommand();
    DataTable studentTable = new DataTable();
    DataTable courseTable = new DataTable();

    BuildCommand(cmdStudent, strStudent);
    cmdStudent.Parameters.Add("@StudentName", SqlDbType.Char).Value = ComboName.Text;
    cmdStudent.CommandText = "Select * from StudentTable";
    dataAdapter.Fill(studentTable);
    if (studentTable.Rows.Count > 0)
    {
        FillStudentTextBox(studentTable);
    }
    else
    {
        MessageBox("No matched student found!");
        BuildCommand(cmdCourse, strCourse);
        cmdCourse.Parameters.Add("@StudentID", SqlDbType.Char).Value = txtStudentID.Text;
        cmdCourse.CommandText = "Select * from CourseTable";
        studentCourseDataAdapter.Fill(courseTable);
        if (courseTable.Rows.Count > 0)
        {
            FillCourseList(courseTable);
        }
        else
        {
            MessageBox("No matched course_id found!");
        }
    }
    cmdStudent.Dispose();
}

// DataReader Method
SqlCommand cmdStudent = new SqlCommand();
SqlDataReader studentReader = cmdStudent.ExecuteReader();
if (studentReader.HasRows == true)
{
    MessageBox("No matched student found!");
    studentReader.Close();
    BuildCommand(cmdCourse, dr, strCourse);
    cmdCourse.Parameters.Add("@StudentID", SqlDbType.Char).Value = txtStudentID.Text;
    SqlDataReader courseReader = cmdCourse.ExecuteReader();
    if (courseReader.HasRows == true)
    {
        FillStudentReader(courseReader);
    }
    else
    {
        MessageBox("No matched course_id found!");
    }
    studentReader.Close();
    cmdCourse_dr.Dispose();
    courseReader.Close();
}

studentTable.Dispose();
courseTable.Dispose();
studentDataAdapter.Dispose();
studentCourseDataAdapter.Dispose();
cmdStudent.Dispose();
cmdCourse.Dispose();
}
```
