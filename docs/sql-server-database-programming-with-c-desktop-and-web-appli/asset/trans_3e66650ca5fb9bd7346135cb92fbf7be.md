

# 在 ASP.NET 中访问数据

| WebLINQSQL Project | cmdBack_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdBack_Click(object sender, EventArgs e) { cse_dept.Connection.Close(); cse_dept.Dispose(); Response.Redirect("Selection.aspx"); } |

**图 8.84** DataContext 实例 cse_dept 使用的代码应该通过执行另一个方法 Dispose() 来释放。

- B. 通过执行另一个方法 **Dispose()** 释放我们构建的所有资源。
- C. 最后，程序控制权传回 **Selection** 页面，使用户根据该页面执行任何其他首选的数据查询。

到此时，我们已经完成了通过 LINQ to SQL 方法课程记录查询和实现的全部开发工作。
现在让我们测试构建的代码，以确认通过 LINQ to SQL 方法实现的删除和**Back**（返回）点击方法的功能。

点击 **IIS** 按钮运行我们的项目。完成登录过程并打开课程组合框（Course Combo）。在 **Opened** 页面上，从 **Faculty Name** 下拉框中选择所需的教员，例如 *Ying Bai*，并点击 **Select** 以获取该教员教授的所有课程 (*course_id*)。

然后通过点击 **Courselist** 框中的 *course_id* 来选择，该课程的详细信息将在六个文本框中显示。保持所选教员名称不变并选择 *course_id*、**CSE-668**，点击 **Delete** 按钮从我们示例数据库的 **Course** 表中删除此记录。

为了确认并验证此删除操作，保持所选教员名称不变，点击 **Select** 按钮以检索该教员教授的所有课程 (*course_id*)。可以发现 **CSE-668** 已从 **Courselist** 框中消失或被移除。这意味着我们的数据删除操作是成功的。

由于 **CSE-668** 是在第 8.8.2 节中新插入或添加到数据库的 **Course** 表中的；因此，子表 **Student** 中没有相关的记录需要删除。然而，如果生成了作为我们示例数据库的原始记录，表中的某些相关记录（如 **StudentCourse**）也将被删除。

现在点击 **Back** 按钮，然后从 **Selection** 页面点击 **Exit** 按钮终止我们的项目。

完整的 Web 应用程序项目 **WebLINQSQL Project** 可以在 CRC 文件网站 **Student** 文件夹下的 Class **DB Projects;Chapter 8:WebLINQSQL Solution** 文件夹中找到（请参考第 1 章中的图 1.2）。

# 8.9 使用存储过程方法查询表格的 WEB 应用程序

在第 5 章第 5.16 节中，我们讨论了如何使用存储过程方法对示例数据库中的 **Student** 表进行查询。生成了五个存储过程：**dbo.StudentInfo**、**dbo.StudentCourseInto**、**dbo.StudentAndCourse** 和 **dbo.StudentInfo**，以便我们能够从 C# Windows 项目中调用它们来执行相关查询。
在本节中，我们尝试在 Web 应用程序项目中使用这些存储过程，通过 LINQ to SQL 技术执行类似的查询。

# 492 使用 C# 进行 SQL Server 数据库编程

我们不需要创建任何新的 Web 应用程序项目来对 Student 表执行任何查询；相反，我们可以修改之前的 Web 应用程序项目之一 WebLNSQL Project，将其变为我们的新项目 WebSP_Student Project。执行以下操作以完成此修改并准备我们的新 Web 应用程序项目：

- 1. 打开 Windows 资源管理器或文件资源管理器，并在本地机器 (C:\Chapter 8) 上找到 Web 应用程序解决方案 WebLNSQL Solution。
- 2. 右键点击该解决方案并选择“复制”以复制该解决方案及其项目，然后将该文件夹粘贴到机器上的相同位置，例如 C:\Chapter 8。
- 3. 分别将两个文件夹重命名为 WebSP_Student Solution 和 WebSP_Student Project。
- 4. 展开新的解决方案文件夹 WebSP_Student Solution，并点击新项目文件夹 WebSP_Student Project 以在资源管理器中打开它。
- 5. 将以下两个名称 WebLNSQL Project.csproj 和 WebLNSQL Project.csproj.user 更改为 csproj WebSP_Student Project.csproj 和 WebSP_Student Project.csproj.user。
- 6. 现在双击新项目 WebSP_Student Project.csproj 以在 Visual Studio 2022 中打开它。

需要注意的一个关键点是，我们更改了解决方案和项目的名称，但命名空间（namespace）保持不变，因为如果将命名空间从 SQLSelect_Project 更改为 WebSP_Student_Project，过程将非常复杂。
让我们开始为从 SQL Server 示例数据库中的 Student 和 StudentCourse 表执行数据查询。

## 8.9.1 开发从 Student 表查询学生记录的代码**

在本节中，我们需要将编码过程分为以下几个部分：

- 1. 创建 DataContext 类的一个新对象并进行一些初始化编码。
- 2. 开发 Select 按钮 Click 方法的代码，通过 LINQ to SQL 调用相关的存储过程以检索回选定的学生信息。
- 3. 开发 Select 按钮的方法代码，通过 LINQ to SQL 调用相关的存储过程以获取所选学生参加的所有课程。
- 4. 开发 Back Click 方法的代码以返回 Selection 页面。

首先处理 Page_Load() 的编码过程。

### 8.9.1.1 创建 DataContext 类的新对象

打开 Student Web 页的窗口和 Page_Load() 方法，并输入图 8.84 所示的代码直到此处。
让我们仔细查看这些代码，看看它是如何工作的。

| WebSP_Student Project | Page_Load(object sender, EventArgs e) |
|---|---|
```csharp
using System;
using System.Linq;
namespace SQLWebSelect_Project
{
    public partial class Student : System.Web.UI.Page
    {
        WebLINSQL_Project.CSE_DEPTDataContext cse_dep = new WebLINSQL_Project.CSE_DEPTDataContext();
        protected void Page_Load(object sender, EventArgs e)
        {
            if (IsPostBack)
            {
                CurrentStudent();
                ComboName.SelectedIndex = 0;
            }
            void CurrentStudent()
            {
                ComboName.Items.Clear();
                var student = (from s in cse_dep.Students
                               let fields = "student_name"
                               select s);
                foreach (var s in student)
                {
                    ComboName.Items.Add(s.student_name);
                }
            }
        }
    }
}
```

**图 8.85** 学生 Web 页的初始化代码。

- A. 首先创建 DataContext 类的一个新字段级对象 c_des，因为我们需要使用它将我们的示例数据库连接到此 Web 项目以执行数据操作。一点是，WebLNSQL_Project 的名称必须作为项目在生成的类的前缀。
- B. 执行用户定义方法 CurrentStudent()，从我们的示例数据库中检索所有当前学生的名称，并将它们显示在 ComboName 下拉框控件中，以便用户以后选择所需的学生。为了避免重复显示检索到的成员，采用了 if 选择结构，以确保只在 Web 页面首次加载时在下拉框中显示这些当前学生，而不会在服务器向客户端发送刷新后的 Student 页面每次都显示它们。
- D. 在用户定义方法内部，在通过添加当前学生名称更新下拉框 ComboName 之前，执行了清理工作以避免多次添加和显示。
- E. 创建并初始化了一个 LINQ 查询，包含 from、let 和 select 三个语句。范围变量从我们示例数据库中的 Student 实体中选择。所有当前学生 (student_name) 都将使用 let 子句读取并分配给查询变量 student。
- F. 执行 LINQ 查询以选取所有查询的学生名称，并将其添加到 Student 页面中的 ComboName 下拉框控件中。我们仍然使用 LINQ to SQL 方法执行此查询是因为它的代码结构简单。我们可以使用不同的方法来完成此查询工作。后续操作将保存我们的新项目和解决方案：

- 1) **转到文件 | 保存所有** 保存我们的新项目和解决方案。在打开的资源管理器中，点击保存和**覆盖** 按钮，然后再次点击保存按钮。
- 2) 然后打开 Windows 资源管理器或文件，点击我们的解决方案文件夹 WebSP_Student Solution，删除原始解决方案文件 WebLINSQL.sl，因为我们不再需要该文件。
- 3) 进入**生成 | 重新生成 WebSP_Student Project** 菜单重新生成我们的项目。

接下来是 Select 按钮点击方法的编码。然而，在执行该过程之前，我们需要将存储过程添加到我们的 DataContext 类中。

