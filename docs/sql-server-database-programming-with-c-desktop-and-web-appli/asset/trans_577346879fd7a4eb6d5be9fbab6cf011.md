
[content]

# 在 ASP.NET 中访问数据

![](img/d59a47501d0a20fc0460a49c469c6fb7_529_0.png)

图 8.94 插入新学生的运行结果。

在从示例数据库的 Student 表中更新和删除学生记录时，有几个重要的要点：

- 1. 当对数据库中的相关表进行更新或删除操作时，按照正确的顺序更新或删除数据非常重要，以减少违反引用完整性约束的概率。
- 2. 更新数据库中的现有记录时，没有必要更新每条记录的主键。由于操作复杂，向数据库中插入一条带有主键的新记录通常比更新现有记录的主键更好。在本节中，我们重点讨论通过修改所有数据列（不包括主键列）来更新现有的记录。
- 3. 从关系型数据库中删除记录时，必须遵循标准的操作顺序。例如，要删除应用程序中 Student 表中的某条记录，必须先删除 Student 表中与要删除的数据相关的记录（如 Login 和 StudentCourse 表），然后才能删除 Student 表中的记录。删除顺序的原因是 `student_id` 是 Login 和 StudentCourse 表中的外键，但在 Student 表中主键。必须先删除带有外键的数据，然后再从数据库中删除具有主键的数据。

记住这三点，现在让我们开始构建我们的项目。首先，让我们专注于构建我们的两个存储过程：`updateStudentSP()` 和 `deleteStudentSP()`。此外，我们还需要这两个存储过程添加到我们的 `DataContext` 类中。

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_530_0.png)

```sql
CREATE PROCEDURE [dbo].[updateStudentSP]
@studentName VARCHAR(20),
@GPA float,
@Credits smallint,
@Major text,
@SchoolYear text,
@Email text,
@Image Image,
@StudentID VARCHAR(20)

UPDATE student
SET sName=@studentName, major=@Major, schoolYear=@SchoolYear,
credits=@Credits, Gpa=@GPA, email=@Email, simage=@image
WHERE student_id=@StudentID

RETURN 0
```

图 8.95 正确的存储过程 `updateStudentSP()` 详情。

## 8.9.3.1 构建两个更新和删除学生记录的存储过程

打开 Visual Studio 2022 和 Server explorer，连接并打开我们的示例数据库，展开 Stored Procedures 文件夹。执行以下操作生成第一个存储过程 `updateStudentSP()`。

- 1. 右键点击存储过程，并选择 Add New Stored Procedure（添加新存储过程）项以打开默认过程向导。
- 2. 将图 8.95 所示的代码输入此向导作为该存储过程的主体。
- 3. 点击图 8.95 所示的 Update（更新）图标，将此存储过程保存到数据库中。
- 4. 然后点击 Update Database（更新数据库）按钮完成此保存操作。

存储过程的代码非常直观易懂。首先，前七项输入信息被生成为要在 Student 表中更新的学生记录。然后执行 `UPDATE` 命令，以 `student_id` 为查询标准更新数据库中的记录。唯一需要注意的是学生图像的数据类型，它应该是 `Image, Binary`。
参考章节 8.9.1.2 将此过程添加到我们的 `DataContext` 中，以便使其识别并使用它。接下来，让我们构建第二个存储过程 `deleteStudentSP()`。同样，我们按照上述方法操作：打开 Visual Studio 2022 和 Server explorer，连接并打开我们的示例数据库，展开 Stored Procedures 文件夹。执行以下操作生成第二个存储过程 `deleteStudentSP()`。

- 1. 右键点击 Stored Procedures 文件夹，并选择 Add New Stored Procedure 项以打开默认的新过程向导。
- 2. 将图 8.96 所示的代码输入此向导作为该存储过程的主体。
- 3. 点击图 8.96 所示的 Update 图标，将此存储过程保存到数据库中。
- 4. 然后点击 Update Database 按钮完成此保存操作。

# 在 ASP.NET 中访问数据

![](img/d59a47501d0a20fc0460a49c469c6fb7_531_0.png)

**图 8.96** 存储过程 `deleteStudent()` 的代码。

这些存储过程的代码直观易懂。首先声明了第一个输入参数 **sName**（用户选择的学生姓名）。然后生成了一个本地变量 **sID**，因为我们需要根据 **student_id** 而不是 **student_name** 来删除学生记录。执行内部查询以根据学生姓名获取匹配的 **student_id**。最后，从 **Student** 表中删除该学生记录。

参考 8.9.1 将这两个存储过程添加到我们的 `DataContext` 类中，以便使其识别并使用它们。接下来，让我们编写调用存储过程的代码来执行数据更新和删除操作。

## 8.9.2 数据更新查询的代码

打开我们的项目 **WebSP_Student Project**，在页面的设计视图（Design View）中双击 **Update** 按钮以打开其点击方法，并在该方法中输入图 8.97 所示的代码。

让我们来看看这段代码看看它是如何工作的。首先声明数组，因为我们需要通过此数据更新操作更新学生图像。

| WebSP_Student Project | cmdUpdate_Click(object sender, EventArgs) |
| :--- | :--- |
| A | protected void cmdUpdate_Click(object sender, EventArgs) { |
| B | byte[] bImage; |
| | if (FileUploadImage.HasFile) |
| | Response.Write("<script>alert('An updating image using FileUpload!')</script>"); |
| | else { |
| C | bImage = getStudentImage(); |
| D | csep_updateStudentSP(txtStudentName.Text, Convert.ToDouble(txtGPA.Text), |
| | Convert.ToInt16(txtCredits.Text), txtMajor.Text, txtSchool.Text, txtEmail.Text, bImage, |
| | txtStudentID.Text); |
| E | CurrentStudent(); |
| F | ClearStudent(); |
| | } |

**图 8.97** Update 按钮点击的代码。

# 使用 C# 进行 SQL Server 数据库编程

B. 在执行此数据更新操作之前，我们需要通过 `HasFile` 属性检查是否上传了文件。如果上传了文件，则显示“正在使用 FileUpload 更新图像”的警告框。
C. 否则，更新数据库。以 `student_id` 为查询标准执行 `UPDATE` 命令来更新数据库中的记录。唯一需要注意的是学生图像的数据类型，它应该是 `Image, Binary`。
参考章节 8.9.1.2 将此过程添加到我们的 `DataContext` 中，以便使其识别并使用它。接下来，让我们构建第二个存储过程 `deleteStudentSP()`。同样，我们按照上述方法操作：打开 Visual Studio 2022 和 Server explorer，连接并打开我们的示例数据库，展开 Stored Procedures 文件夹。执行以下操作生成第二个存储过程 `deleteStudentSP()`。

D. 然后点击 Update Database 按钮完成此保存操作。
E. `CurrentStudent()`。
F. `ClearStudent()`。

记住这三点，现在让我们开始构建我们的项目。首先，让我们专注于构建我们的两个存储过程：`updateStudentSP()` 和 `deleteStudentSP()`。此外，我们还需要这两个存储过程添加到我们的 `DataContext` 类中。

[/content]
