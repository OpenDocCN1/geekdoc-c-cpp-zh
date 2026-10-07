

## SelectWizard 产品

| | LINQToDataSet() |
|---|---|
| | |

```csharp
private void LINQToDataSet(string facultyID)
{
    this.courseTableAdapter.FillByFacultyID(CSE_DEPTDataSet.Course, facultyID);
    var course = from (c in CSE_DEPTDataSet.Course.AsEnumerable())
                  where c.Field<string>("faculty_id") == facultyID
                  select c;
    foreach (var c in course)
    {
        //this.txtCourseID.Text = c.CourseName;
        this.txtSchedule.Text = c.schedule;
        this.txtClassroom.Text = c.classroom;
        this.txtCredits.Text = c.Credits.ToString();
        this.txtEnroll.Text = c.enrollment.ToString();
    }
}
```

**图 5.65** LINQ to DataSet 方法的代码。

如果课程表单（Course Form）的代码窗口未打开，请打开它，然后创建一个新方法 **LINQToDataSet**，并将图 5.65 所示的代码输入该方法中。
让我们来看看这段代码是如何运行的。

- **A.** 首先需要调用查询方法 *FillByFacultyID()*，该方法将在 5.12 节中构建，用于将课程数据从 Course 表加载到我们 DataSet 中的 Course 中。这一操作对于我们的后续操作是重要且必要的，即从 DataSet 中的 Course 表中检索数据并将其显示在课程列表中。

- **B.** 创建并执行一个典型的 LINQ 查询结构，以检索所选教师的所有相关课程信息。**courseinfo 是一个带有数据类型的 C# 隐式类型变量 var**。C# 2022 在看到它时，能够自动将其转换为任何合适的数据类型（在本例中是一个 DataSet）。这里使用一个迭代变量 *ci* 来遍历来自 Course 表的此查询结果。然后将执行一个带有 **WHERE** 子句的类似 SQL SELECT 的语句。

- **C.** 利用 `foreach` 循环从选定的数据行 *crow* 中提取每一列，该行是从我们通过 LINQ 查询获取的 **courseinfo** 的。

将每一列分配给 TextBox 以便在课程窗口中显示。
在分配过程中存在一个复杂性，即 **foreach** 循环的最后一次运行。当 **foreach** 循环运行时，迭代变量 *crow* 中的课程 ID 和课程名称列（**crow.course_id** 和 **crow.course**）将包含这两个值，即使我们只想第一个 *course_id* 和 *course* 分配给变量。为了避免此错误，前两个赋值不能包含在此循环中。因此，我们应该注释掉前面的赋值，并将这些列分配到课程窗口中的课程 ID 和课程文本框中？这项工作可以由 BindingSource 处理，因为你可以点击并自动从 **CourseList** 框中选择 **course_id**。

到此时，我们已经完成了课程项目的所有代码。在测试之前，不要忘记删除图 5.64 中 **LINQToDataSet()** 方法中的注释符号，使该方法生效。
现在点击 **Start**（启动）按钮运行我们的项目。在登录表单中输入 **ybai** 和 **come** 作为用户名和密码，然后从选择表单中选择 **Course Information**（课程信息），点击 **OK** 按钮打开我们的课程表单，如图 5.66 所示。

## 使用 Visual C#.NET 进行数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_259_0.png)

图 5.66 课程的运行状态。

在打开的课程表单窗口中，选择默认姓名 Ying Bai 并点击 Select（选择），以便该教师的所有课程 (course_id) 加载并填充到我们 DataSet 中的表中，作为此表单中的 Course ListBox（课程列表框）。

填充后的 course_id 显示在 Course ListBox 中，如图 5.66 所示。
现在让我们更进一步，从 Course ListBox 中点击一个 course_id。立即，所选课程的详细信息（包括课程 ID、课程名称、时间表、教室、学分和选课人数）将显示在文本框中。这是合理的，因为这些文本框已绑定到我们 DataSet 中 Course 表的六列。当你从 Course ListBox 中点击一个 course_id 时，你实际上是从 Course 表中选择并提取了一门课程。记住，当我们在 5.12 节中使用 BindingSource 执行数据绑定时，ListBox 绑定到了我们 DataSet 中的 Course 表。对于所选的课程，六列记录已绑定到表单中的六个文本框，因此数据也将反映在这些六个文本框上。这些关系可以通过图 5.67 中的连接来表示和说明。

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

