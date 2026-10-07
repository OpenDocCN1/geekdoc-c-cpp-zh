

# 使用 C# 进行 SQL Server 数据库编程

如果你想删除 Faculty（教师）表中的一条记录，必须先删除 Login、Course、StudentCourse 和 Student 表中的相关记录，然后才能从 Faculty 表中删除所需的记录。这是因为这五张表之间存在特定的关系。

例如，如果想从 Faculty 表中删除一条记录，必须执行以下删除操作：

- Faculty_id 是 Faculty 表的主键，也是 Login 表和 Course 表中的外键。因此，Faculty 表是父表，而 Login 和 Course 是子表。在删除 Faculty 表中的记录之前，必须先删除子表中所有以 `faculty_id` 作为外键的记录。换句话说，必须先删除 Login 和 Course 表中所有使用 `faculty_id` 作为外键的记录。
- 在删除 Course 表中以 `faculty_id` 作为外键的记录时，相关的 `course_id`（它是 Course 表中的主键）也会被删除。现在 Course 变成了一个父表，因为 `course_id` 是该表的主键。然而，如所述，要删除父表中的任何记录，必须先删除子表中的相关记录。现在 StudentCourse 表是 Course 表的子表；应该先删除 StudentCourse 表中使用 `course_id` 作为外键的记录。
- 在删除了子表中的这些相关记录后，最后就可以从父表 Faculty 表中删除该教师。

## 8.6.2.2 数据删除顺序

总结来说，要删除 Faculty 表中的记录，需要按照所示的顺序执行以下删除任务：

1) 删除 StudentCourse 表中所有使用 `course_id` 作为外键的记录。
2) 删除 Login 表中所有使用 `faculty_id` 作为外键的记录。
3) 删除 Course 表中所有使用 `faculty_id` 作为外键的记录。
4) 从 Faculty 表中删除指定的教师成员。

通过这个示例，你可以看到在关系型数据库中删除一条记录的操作过程是多么的复杂。

## 8.6.2.3 使用级联删除（Cascade Deleting）选项简化数据删除操作

为了简化数据操作，我们可以使用 Microsoft SQL Server Management Studio 18 提供的级联删除（Cascade Deleting）选项。

回想我们创建并建立了这五张表之间的关系，这五种关系是在这些表之间建立的：

1) Login 表和 Faculty 表之间的关系通过 `faculty_id` 作为外键 `FK_Login_Faculty` 在 Login 表中建立。
2) Login 表和 Student 表之间的关系通过 `student_id` 作为外键 `FK_Student_Login` 在 Login 表中建立。
3) Course 表和 Faculty 表之间的关系通过 `faculty_id` 作为外键 `FK_Course_Faculty` 在 Course 表中建立。
4) StudentCourse 表和 Course 表之间的关系通过 `course_id` 作为外键 `FK_StudentCourse_Course` 在 Course 表中建立。
5) StudentCourse 表和 Student 表之间的关系通过 `student_id` 作为外键 `FK_StudentCourse_Student` 在 StudentCourse 表中建立。

# 在 ASP.NET 中访问数据

459

根据上一节列出的数据删除顺序（1–4），为了删除 Faculty 表中的记录，需要按照该顺序执行四次删除操作。与这四次删除操作相比，第一种是最困难的，原因如下：

要执行第一次删除操作，必须先从 Course 表中找到使用 `faculty_id` 作为外键的 `course_id`，并根据这些 `course_id`，删除 StudentCourse 表中所有使用这些 `course_ids` 作为外键的记录。执行顺序 3 和 4 的删除操作非常简单，每个删除操作只需要一次查询。此讨论的结论是：我们如何找到一种更简单的方法来完成顺序中的操作？

解决此问题的一种巧妙方法是使用我们在第 2 章中用过的级联（Cascade）选项，以级联模式执行数据删除。当为上述关系 4 和 5 选择了级联时，SQL Server 数据库就可以自动执行顺序 1 中的删除。

现在，让我们用一个真实的例子来说说明如何使用此级联选项来简化数据删除操作，特别是针对顺序 1 中的第一次删除。
在 SQL Server Management Studio 18 中执行以下操作：

1) 转到 开始 | 所有程序 | Microsoft SQL Server Tools 18 | SQL Server Management Studio 18。
2) 在打开的窗口中，选择 SQL Server 身份验证模式，通过输入用户名 SMART 和密码 Hot2022 完成登录，并点击 Connect 按钮连接我们的数据库。
3) 展开 Databases 文件夹、我们的示例数据库 CSE DEPT，以及 Tables 文件夹以展开所有五张表。由于我们对关系 4 和 5 感兴趣，只需展开 dbo.StudentCourse 表和 Keys 文件夹，找到我们在第 2 章 2.9.4 节中建立的所有键。双击键 FK_StudentCourse_Course 打开它，如图 8.47 所示。

在打开 Foreign Key Relationships 窗口中，保持左侧面板选中我们所需的键 FK_StudentCourse_Course，然后点击 INSERT AND UPDATE Specification 项前的小图标，你会发现 Delete Rule（删除规则）和 Update Rule（更新规则）项都设置了级联模式，如图 8.47 所示。

![图 8.47 外键窗口。](img/d9a4750)

# 使用 C# 进行 SQL Server 数据库编程

460

设置好此级联选项后，每当你想删除 Student 表中所有使用 `course_id` 或 `student_id` 作为外键的记录时，SQL Server 将按照级联顺序自动执行这些删除。因此，你可以看到执行顺序1 有有多简单。点击按钮关闭向导。

## 8.6.2.4 编写代码执行数据删除操作

打开 Studio.NET 和我们的 Web 应用程序 SQLUpdateDeleteProject。打开 Delete 按钮。然后输入图 8.48 所示的代码。让我们来看看这段代码看看它是如何工作的。

| SQLWebDeleteProject | cmdDelete_Click(object sender, EventArgs e) |
|---|---|
| A | private void cmdDelete_Click(object sender, EventArgs e) { |
| B | TextBox fBox[] = new TextBox(txtID, txtName, txtBody, txtPhone, txtCollege, txtEmail);
SqlCommand sqlCommand = new SqlCommand();
intDelete; |
| C | string cmdText = "DELETE FROM Faculty WHERE faculty_name = @facultyName";
sqlCommand.Connection = sqlConnection;
sqlCommand.CommandType = CommandType.Text; |
| D | 
sqlCommand.Parameters.Add("@facultyName", SqlDbType.Char).Value = ComboName.Text;
intDelete = sqlCommand.ExecuteNonQuery(); |
| E | sqlCommand.Dispose(); |
| F | if (intDelete == 0)
Response.Write("<script>alert('The data deleting failed!');</script>"); |
| G | for (int intDelete = 0; intDelete < intDelete; intDelete++)
fBox[intDelete].Text = string.Empty; |
| I | PhotoBox.Image = null; |
| J | CurrentFaculty(); } |

图 8.48 删除按钮点击方法的代码。

