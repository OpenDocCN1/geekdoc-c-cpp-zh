

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_254_0.png)

**图 5.61** 完成后的查询生成器。

此 SQL SELECT 语句的动态参数。完成的 SQL 语句显示在文本窗中，如图 5.61 所示，该语句的内容为：

```
SELECT course_id, course, credit, classroom, schedule, enrollment,
faculty_id
FROM Course
WHERE (faculty_id = @Param1)
```

动态参数 @Param1 是一个临时参数，在项目运行时将被真实参数 faculty_id 替换。

点击 OK（确定）和 Next（下一）按钮，返回 TableAdapter 配置向导，将 `AttachFacultyId` 方法添加到 `Fill` 方法的末尾，以获取修改后的方法：`FillByFacultyId()`。如果此查询不需要该方法，请取消勾选 Refresh DataTable 复选框。

下一步是绑定 `CourseForm` 中的文本控件，以关联 DataSet 中表中的相关数据。从解决方案管理器中选择 `Course.cs` 并点击 View Designer（视图设计器）按钮打开 `CourseForm` 的图形界面。

首先，我们需要将 `CourseList` 绑定到 DataSet 表中的 `course_id` 列。回想一下我们在第 2 章构建示例数据库时，该表中有多个具有相同 `faculty_id` 的 `course_id`。这些具有相同 `faculty_id` 的多条记录通过教师所授的不同课程来区分。要将 ListBox 绑定到具有相同 `faculty_id` 的多条记录，我们不能继续使用之前在节中用于文本控件的绑定方法。这是 ListBox 控件绑定的特殊之处。

特殊之处在于 ListBox 与表中数据列之间的关系是一一对多的，这意味着 ListBox 可以包含多个项目。在这种情况下，`CourseList`

# 使用 Visual C#.NET 进行数据选择查询

| 无 | 无 | 无 |
|---|---|---|
| 其他数据源 | course_id | courseBindingSource |
| 项目数据源 | course | course_id |
| CSE_DEPTDataSet | credit | course |
| Course | classroom | schedule |
| Faculty | schedule | enrollment |
| Logic | enrollment | faculty_id |
| Student | faculty_id | |
| StudentCourse | | |

添加项目数据源...
选择项目数据源会在表单上创建一个并绑定到 th...

添加项目数据源...
选择一个 BindingSource 进行绑定。

**图 5.62** 展开的数据绑定源。文中描述了 (a-c)。

可以包含许多 `course_id`。因此，ListBox 控件的绑定实际上是将 ListBox 绑定到 DataSet 中的一个表，在本应用程序中即为 `Course` 表。

要执行此操作，从 `Course Form` 中点击 `CourseList`，然后进入属性窗口找到 `DataSource` 属性，并点击下拉箭头展开 Other Data Sources | Project Data Sources | CSE_DEPTDataSet 直到绑定到 `Course`。通过点击它进行选择。图 5.62a 显示了这种情况。

继续此操作，展开 `DisplayMember` 属性以找到 `course_id` 列，并点击此项进行选择，如图 5.6b 所示。

通过这种方式，我们在 `Course Form` 中的 ListBox 和 DataSet 中的 `Course` 数据之间建立了绑定关系。

现在，我们需要将 `Course Form` 中的六个文本控件绑定到 DataSet 中 `Course` 数据的六列。执行以下操作步骤以完成这些绑定：

- 1) 保持 `Course Form` 开启，并从 Course 信息分组框中选择 Course ID TextBox。
- 2) 进入 `DataBindings` 属性并展开该项目中的 `courseBindingSource` 对象。然后你将发现一个由于上述绑定操作导致的 `Course listing`（课程列表）而产生的下拉箭头。
- 3) 展开此 `courseBindingSource` 直到找到 `course_id` 列（如图 5.62c 所示），并通过点击 `course_id` 列进行选择。在表单中的 Course ID TextBox 与 DataSet 中 `Course` 表的 `course_id` 列之间建立了绑定。
- 4) 以同样的方式，完成其他五个 TextBox 控件的绑定：Course、Schedule、Classroom 和 Enrollment。

需要注意的是执行这些绑定的顺序。你必须**首先**对 `CourseList` 控件进行绑定，然后对六个 TextBox 进行绑定。

# 使用 C# 进行 SQL Server 数据库编程

现在我们可以回答为什么在使用查询生成器时需要在图形面板上保持默认选择的原因（参考图 5.60）。这是因为我们需要控件为我们的六个 TextBox 控件执行数据绑定。这样，`Course Form` 中的每个 TextBox 都与 DataSet 中 `Course` 表中的相关数据绑定。设置此类绑定后，每当执行 `FillFacultyID()` 方法时，DataSet 中 `Course` 表中的所有列都由真实数据库中 `Course` 表的数据列更新。同时，所有六个 TextBox 的内容也将更新，因为这些 TextBox 控件已绑定到 DataSet `Course` 表中的这些数据列。

好了，是时候为此表单编写代码了。

# 5.13 开发用于为 COURSE FORM 查询数据的代码

根据我们上面对 `Course Form` 功能的分析，当用户选择教师姓名并点击 Select（选择）按钮时，该教师教授的 `course_id` 将列在 `CourseList` 中。要检查每个课程的详细信息，点击 `CourseList` 将显示该课程的详细信息。代码分为两个部分：第一部分使用 TableAdapter 方法查询，第二部分使用 LINQ 方法查询。

# 使用 TableAdapter 方法从表查询数据

通过在解决方案管理器中右键点击 `Course Form` 并选择 Designer 项打开 `Course Form`。双击 Select 按钮进入其 Click 方法，如下所示：

- A. 在命名空间中创建了一个 TableAdapter 对象。
- B. 声明了一个本地字符串 `facultyid` 用于存储返回的结果。
- C. 如果返回的 `facultyid` 不为空，意味着已获取 `facultyid`，我们可以根据此继续查询。
- D. 如果用户选择了 TableAdapter 方法，将调用 DataSet 中的 `FillFacultyID()`，动态参数 `@Param` 被替换。
- E. 通过检查查询表的属性来确认查询是否成功。如果没有找到匹配且未返回记录，则使用消息框提示此情况。
- F. 否则，调用用户定义的 `LINToDataSet()` 方法。该参数是从上面的查询中获取的 `facultyid`。
- G. 如果返回的 `facultyid` 为空字符串，则未从表中找到有效的 `facultyid`。

在解决方案管理器中右键点击并选择 Designer 项，双击进入 Load 方法并输入以下代码：

```c
private void Course_Load(object sender, EventArgs args)
{
    this.ComboName.Add("

```

*(注：此处原文文本似乎有中断，根据上下文推断后续为填充组合框数据项的代码)*

# 使用 Visual C#.NET 进行数据选择查询

| 选择 | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| private void cmdSelect_Click(object sender, EventArgs e) { CSE_DEPTDataSet.FacultyTableAdapter = new CSE_DEPTDataSet.FacultyTableAdapter(); string facultyID = FacultyTableAdapter.FindIDByName(ComboName.Text); ... } | 

**图 5.64** 选择按钮的详细代码。

# 5.13.2 使用 LINQ 方法从表查询数据

在最后一节的代码中（参考图 5.64），如果用户在组合框中选择了 LINQ & DataSet 方法，程序将重定向到 `LINQToDataSet` 方法。关于 LINQ 和 DataSet 之间数据查询的详细讨论，请参考第 4 章。在本部分，我们将开发代码以使用此方法对 DataSet 中的 `Course` 表执行数据查询。

