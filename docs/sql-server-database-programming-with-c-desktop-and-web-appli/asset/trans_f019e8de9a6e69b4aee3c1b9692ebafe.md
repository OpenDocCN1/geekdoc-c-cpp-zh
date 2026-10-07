
E. 存储过程 `dbo.Student` 需要一个输入参数 `StudentName`，因此在项目运行时，将从 `Name` 组合框获取的实际参数添加到 `Parameters` 集合中，该集合是 `Command` 对象的属性。初始化的 `Command` 对象被赋值给 `DataAdapter` 的 `Select-Command` 属性，并在稍后使用。

F. 执行 `Fill` 方法来调用存储过程并填充表。如果调用成功，返回的数据列将可用；否则将显示错误消息。

在接下来的部分，我们需要创建一个新的 Visual C# Select 项目，并使用表单（Form）创建两个存储过程，以对示例数据库中的表执行数据查询。首先，让我们在 Visual Studio NET 2022 的服务器管理器（Server Explorer）中创建这两个新的存储过程。

## 5.16.3 使用存储过程为 Student Form 查询数据

首先，为这个 Student Form 创建两个存储过程。第一个存储过程用于根据选定的学生姓名从句表中获取 `student_id`，第二个存储过程用于根据 `student_id`获取所选学生的的课程。我们需要使用两个查询的原因是：我们想根据学生的姓名而不是 `student_id` 从 `StudentCourse` 表中查询所选学生的所有课程。但 `StudentCourse` 表中只有 `student_id` 列，没有学生姓名。学生姓名可以从 `Student` 表获取。因此，我们需要根据学生姓名对 `Student` 表进行查询，并根据第一个查询获取的 `student_id` 对 `StudentCourse` 表进行第二次查询，以获取所有课程（所有 course_id）。

第一个存储过程命名为 `dbo.Students`，我们将使用 Visual Studio NET IDE 中的服务器管理器创建此存储过程。

打开 Visual Studio 2022，点击“视图 (View) | 服务器管理器 (Server Explorer)” 菜单项打开服务器管理器。要找到我们的示例数据库 `CSE_DEPT`，只需展开“数据连接 (Data Connections)”文件夹，可以发现我们的示例数据库 `CSE_DEPT` 已初始连接并添加到此管理器中，如图 5.89a 所示。

![](img/d59a47501d0a20fc0460a49c469c6fb7_288_0.png)

图 5.89 完成后的服务器管理器窗口和打开的存储过程向导。如正文中 a) 和 b) 所示。

## Visual#.NET 中的数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_289_0.png)

图 5.90 第一个存储过程 – dbo.StudentInfo。

为了使此连接生效，右键点击我们的示例数据库并刷新。我们展开示例数据库，右键点击“存储过程 (Stored Procedures)”文件夹，选择“添加新建存储过程 (Add New Stored Procedure)”以打开新的存储过程向导，如图 5.9b 所示。

新存储过程的默认名称为 `dbo.Procedure`，位于参数列表紧之后。顶部的默认代码行用于创建参数或参数列表。`AS` 关键字下方用于创建 SQL 语句。我们创建第一个存储过程，将图 5.90 所示的代码输入到此过程中。`@UserName` 是此存储过程的唯一输入参数，此存储过程将根据输入的学生姓名返回与所选数据库相关的每个信息。不要忘记将存储过程的名称修改为 `[dbo].[StudentInfo]`。点击左上角的“更新项 (Update Item)”，如图 5.90 所示，以保存此存储过程。点击底部的“更新数据库 (Update Database)”按钮完成此保存过程。

如果一切正常，将显示“更新成功 (Update completed successfully)”。现在，如果你重新打开服务器管理器窗口，展开数据库连接文件夹和存储过程文件夹，将不会显示我们的新存储过程。只需右键点击“存储过程”文件夹并选择“刷新 (Refresh)`,你就能找到我们新的存储过程 `StudentInfo` 在那里了。

同样，我们可以创建第二个存储过程 `dbo.StudentCourseInfo`，如图 5.91 所示。

![](img/d59a47501d0a20fc0460a49c469c6fb7_289_1.png)

图 5.91 第二个存储过程 – dbo.StudentCourseInfo。

## 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_290_0.png)

**图 5.92** 弹出菜单和 EXECUTE 向导。（如描述文本中的 a 和 b 所示）。

此存储过程的唯一输入参数是 `@StudentID`，此存储过程将根据输入参数 `student_id` 返回所选学生所修的所有课程（**course_id**）。点击左上角的“**更新 (Update)**”项，如图 5.90 所示（此处原文可能误为5.90，指代更新操作）。点击底部的“**更新数据库 (Update Database)**”按钮完成此保存过程。

如果一切正常，将显示“更新成功 (Update completed successfully)”。现在如果你重新打开服务器管理器窗口，展开数据库连接文件夹和存储过程文件夹，我们的新存储过程将不再显示。
