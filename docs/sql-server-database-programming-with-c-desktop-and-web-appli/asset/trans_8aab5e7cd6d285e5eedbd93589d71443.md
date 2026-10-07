

## 使用 Visual#.NET 进行数据选择查询

| SPSSelect 项目 | SelectionForm() |

```csharp
public partial class SelectionForm : Form
{
    FacultyForm facultyForm = new FacultyForm();
    CourseForm courseForm = new CourseForm();
    StudentForm studentForm = new StudentForm();
    SPForm spForm = new SPForm();
    public SelectionForm()
    {
        InitializeComponent();
        this.ComboSelection.Items.Add("Faculty Information");
        this.ComboSelection.Items.Add("Course Information");
        this.ComboSelection.Items.Add("Student Information");
        this.ComboSelection.Items.Add("SP Information");
        this.ComboSelection.SelectedIndex = 0;
    }
    private void cmdOK_Click(object sender, EventArgs args)
    {
        if(this.ComboSelection.Text == "Faculty Information")
            facultyForm.Show();
        else if(this.ComboSelection.Text == "Course Information")
            courseForm.Show();
        else if (this.ComboSelection.Text == "Student Information")
            studentForm.Show();
        else
            spForm.Show();
    }
    private void cmdExit_Click(object sender, EventArgs e)
    {
        courseForm.Close();
        facultyForm.Close();
        studentForm.Close();
        spForm.Close();
        Application.Exit();
    }
}
```

FIGURE 5.106 修改后的 SelectionForm 类代码。

## 5.16.6 使用嵌套存储过程查询数据

所谓的嵌套存储过程与子程序或子查询非常相似，这意味着主存储过程可以被视为父过程，而子存储过程可以被视为子存储过程。在本节中，我们创建了两个存储过程，一个是主存储过程，另一个是子存储过程。主存储过程命名为 `StudentAndCourse`，用于根据 `student_id` 从 `StudentCourse` 表中获取所选学生修的所有课程；名为 `StudentInfo` 的子存储过程则用于根据输入的学生姓名从 `Student` 表中获取 `student_id`。

现在打开 Server 窗口并连接到我们的数据库 `CSE_DEPT`。在连接到数据库后，右键点击“Stored Procedures”（存储过程）文件夹并选择“Add New Item”（添加新项）以添加存储过程。

首先，让我们创建主存储过程 —— `dbo.StudentAndCourse`。将图 5.108 所示的代码输入到我们的主存储过程中。

## 278 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_306_0.png)

**图 5.107** 调用我们存储过程的运行状态。

![](img/d59a47501d0a20fc0460a49c469c6fb7_306_1.png)

**图 5.108** 主存储过程。

每行代码的功能：

- **A.** 首先声明我们的存储过程名称为 `dbo.StudentAndCourse`。此名称必须与稍后 Visual C# 项目中使用的存储过程名称完全一致。
- **B.** 在此处声明输入参数 `@StudentName`。
- **C.** 本地变量 `@StudentID` 用作子存储过程的输出参数，该子过程会将此参数 `student_id` 返回给我们的主过程。
- **D.** 使用 `EXEC` 命令调用并执行子存储过程。此调用向子存储过程传递了两个参数：子过程的输入参数 `@StudentName` 和输出 `@StudentID`。后者必须用关键字 `OUTPUT` 指明。在稍后的子存储过程中，你必须使用 `OUTPUT` 关键字将此参数声明为输出参数，以匹配主存储过程中的定义。
- **E.** 子存储过程执行完毕后，它会返回 `student_id`。现在我们可以执行主查询，根据子存储过程返回的 `student_id` 从 `StudentCourse` 表中获取所选学生修的所有课程。
- **F.** 获取的课程将返回给在 Visual C# 项目中开发的子过程。

现在点击左上角的 **Update**（更新）项（如图 5.108 所示）以保存此存储过程。在打开的 **Preview Database**（预览数据库）更新中点击 **Update Database**（更新数据库）按钮完成保存。

其次，创建我们的子存储过程。在已连接的示例数据库 **CSE_DEPT** 的服务器资源管理器窗口中，右键点击 **Stored Procedures** 文件夹，从弹出菜单中选择 **Add New Stored Procedure**（新建存储过程）项。在打开的向导中，将图 5.109 中的代码输入此子存储过程。

每行代码的功能概述如下：

- **A.** 首先声明我们的子存储过程名称，即：`dbo.StudentInfo`。此名称必须与主存储过程调用此过程时使用的名称完全一致。
- **B.** 在此处声明两个参数；第一个 `@sName` 是输入，第二个 `@sid` 是输出参数。参数的默认类型为 `INPUT`，因此由于第二个参数是输出且将返回给主存储过程，必须为其加上 `OUTPUT` 关键字。
- **C.** 执行 SQL 语句，根据输入的名称从表中获取所需的 `student_id`。
- **D.** 将输出 `@sid` 返回给主存储过程。

现在点击左上角的 **Update**（更新）项以保存此存储过程。在打开的 **Preview Database** 中点击 **Update Database** 完成保存。

## 使用 Visual#.NET 进行数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_307_0.png)

**图 5.109** 子存储过程。

![](img/d59a47501d0a20fc0460a49c469c6fb7_308_0.png)

**图 5.110** 嵌套存储过程的结果。

输入一个姓名（如 Tom），并点击 OK 按钮运行存储过程。结果如图 5.110 所示。我们的嵌套存储过程运行良好！为了调用此存储过程，我们需要开发一个 Visual C# 项目。为了节省时间和空间，可以使用上一节为 SP Form 开发的代码。所有代码都相同，唯一的修改在于 `cmd()` 方法中的存储过程名称以及传递存储过程的输入参数。将存储过程名称从 `dbo.StudentCourseINTO` 修改为 `dbo.StudentAndCourse`（参见 A 行），并将参数名从 `@StudentName` 修改为 `@StudentName`（参见 D 行）。

