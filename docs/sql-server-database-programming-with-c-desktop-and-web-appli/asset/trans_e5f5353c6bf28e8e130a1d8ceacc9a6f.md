

# 384 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_412_0.png)

图 7.19 更新后的教职工信息。

为了保持我们的示例数据库一致，强烈建议将更新后的教职工记录恢复到原始记录。为了实现这一点，可以执行另一个更新操作以获取原始教职工记录 Ying Bai（所示），并用它替换原来的记录：

| 教员姓名 | Ying Bai |
| :--- | :--- |
| 职称 | 副教授 |
| 办公室 | MTC-211 |
| 电话 | 750-378-1148 |
| 学院 | 佛罗里达大立大学 |
| 邮箱 | ybai@college.edu |
| 教员头像 | Bai.jpg |

接下来测试删除功能。为了避免复杂的数据恢复，我们倾向于不删除任何原始教职工记录。所谓的原始教职工记录是指我们在第 2 章构建示例数据库时创建的记录，因为这些教职工与 Course、Login 和 StudentCourse 表等其他表通过主键和外键存在某些复杂的关系。请参阅第 7.2 第 6 节获取有关这些关系的更多细节。

现在进入教员姓名（Faculty Name）下拉框选择教员 James David，他不是原始教职工记录，而是在第 6 章第 6.8 节插入的。点击删除（Delete）按钮，从 Faculty 表中删除该教员。然后在消息框中点击是（Yes），TextBox 中显示的所有信息都将消失。这就是我们的数据删除吗？为了回答这个问题，使用教员姓名（Faculty Name）下拉框，发现找不到被删除的教员 James David。这意味着选定的教员及其所有信息已成功从 Faculty 表中删除，是的，这就是我们的数据删除。

然而，如果删除了像 Ying Bai 这样的原始教职工记录，由于存在复杂的关系，不仅该教职工记录会从 Faculty 表中删除，相关表中的某些其他数据记录也会被删除。请参考图 7.20 以清晰了解这些关系。

为了恢复被删除的教职工，必须记住以下几点并遵循以下步骤：

- 1) 回想我们在构建数据库 CSE_DEPT 时，正是在设置表之间的关系时，在 Faculty 和 Login、Faculty 和 Course 以及 Course 和 Student 表之间的 INSERT 和 UPDATE 指定字段中，将 Update 和 Delete 规则都设置为级联（Cascade）模式。这意味着对于删除操作，Faculty 是 Login 和 Course 的父表，它们是子表。同样，Course 是 StudentCourse 表的父表，StudentCourse 是 Course 表的子表。级联更新和删除意味着当父表中的记录被更新或删除时，子表中的所有记录也会被更新或删除。图 7.20 显示了级联更新和删除的示例。该示例选择了 faculty_id=B78880 的教员 Ying Bai 进行更新和删除操作。

- 2) 如图 7.20 所示，当 faculty_id=B78880 的教员（它是 Faculty 表的主键，也是 Login 和 Course 表的外键）从 Faculty 表中被更新或删除时，子表 Login 和 Course 中具有相同 faculty_id 的相关记录也将随关联列一起更新或删除。位于 Login 表中的两个列 user_name 和 pass_word，以及位于 Course 表中的四个关联列 course_id 也将被更新或删除。

- 3) 一个导入问题是恢复这些被删除的记录。你必须先恢复父表记录（Faculty 和 Course 表），然后恢复子表中的记录。按照图 7.20 中的表顺序并参考第 2 章的 2.9.4.1-2.9.4.5 节以及图 7.21-7.24 来恢复这些记录。

完整的项目 RTOUpdateDeleteProject可以在 CRC fps 网站 Students 文件夹下的 Class DB Projects\Chapter 7\RTOUpdateDelete Solution 找到，参考第 1 章的图 1.2。

![](img/d59a47501d0a20fc0460a49c469c6fb7_413_0.png)

# 386 使用 C# 进行 SQL Server 编程

| faculty_id | faculty_name | title | office | phone | college | email | fimage |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| B78880 | Ying Bai | Associate Professor | LTC-271 | 750-378-1148 | Florida Atlantic University | ybai@college.edu | NULL |

**图 7.21** Faculty 表中应包含的数据。

| user_name | pass_word | faculty_id | student_id |
| :--- | :--- | :--- | :--- |
| ybai | come | B78880 | NULL |

**图 7.22** Login 表中应包含的数据。

| course_id | course | credit | classroom | schedule | enrollment | faculty_id |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| CSC-132B | Introduction to Programming | 3 | MTC-302 | T-H:1:00-2:25 PM | 21 | B78880 |
| CSC-234A | Data Structure & Algorithms | 3 | MTC-302 | M-W:9:00-9:55 AM | 25 | B78880 |
| CSC-434 | Advanced Electronics Systems | 3 | MTC-213 | M-W:1:00-1:55 PM | 26 | B78880 |
| CSC-438 | Advanced Logic & Microprocessor | 3 | MTC-213 | M-W:11:00-11:55 AM | 35 | B78880 |

**图 7.23** Course 表中应包含的数据。

| course_id | student_id | course_id | credit | major |
| :--- | :--- | :--- | :--- | :--- |
| 1005 | T77896 | CSC-234A | 3 | CS/IS |
| 1009 | A78835 | CSE-434 | 3 | CE |
| 1014 | A78835 | CSC-438 | 3 | CE |
| 1016 | A97850 | CSC-132B | 3 | IS |
| 1017 | A97850 | CSC-234A | 3 | IS |

**图 7.24** StudentCourse 表中应包含的数据。

# 7.4.3 更新 SQL 数据库中的 COURSE 表

在本节中，我们将讨论如何通过上一节构建的 RtUpdateDeleteProject 中的 Course 窗口对示例数据库中的 Course 表进行数据更新。为了更新 Course 表的数据，我们不需要添加任何新表单并将并将 Course 窗口作为界面。我们需要执行以下步骤来完成此数据更新：

- 1) 开发更新课程记录的代码。
- 2) 验证数据更新结果。

首先，我们为数据更新操作开发代码。

在通常情况下，如果需要更新课程记录，不应该更新 **course_id**，因为可以插入新课程，并在需要时删除旧课程。在该项目中，我们更新课程记录除其 course_id 以外的所有信息。更新查询的输入动态参数仅包含一个：course_id。

与更新 Faculty 表中的记录类似，更新课程记录的主要代码工作开发在 Update 按钮的 Click 方法中。现在，让我们开始示例数据库中课程记录的代码过程。

# 使用 Visual C 进行数据更新和删除

| RTOUpdateDelete | cmdUpdate_Click(object sender, EventArgs e) |
| :--- | :--- |
| private void cmdUpdate_Click(object sender, EventArgs e) { string cmdString = "UPDATE SET course = @Cname, credit = @Credit, classroom = @Classroom, " + "schedule = @Schedule, enrollment = @Enroll WHERE (course_id = @cid)"; SqlCommand sqlCommand = new SqlCommand(cmdString, intUpdate; sqlCommand.Connection = Connection; sqlCommand.CommandType = CommandType.Text; sqlCommand.CommandText = cmdString; sqlCommand.Parameters.AddWithValue("@cid", cid); intUpdate = (int)sqlCommand.ExecuteNonQuery(); sqlCommand.Dispose(); } if (intUpdate == 0) { MessageBox.Show("The data is updated!"); } private void UpdateParameters(SqlCommand sqlCommand) { cmdCommand.Parameters.Add("@Cname", SqlDbType.Char).Value = txtCourseName.Text; cmdCommand.Parameters.Add("@Credit", SqlDbType.Char).Value = txtCredits.Text; cmdCommand.Parameters.Add("@Classroom", SqlDbType.Char).Value = txtClassroom.Text; cmdCommand.Parameters.Add("@Schedule", SqlDbType.Char).Value = txtSchedule.Text; cmdCommand.Parameters.Add("@Enroll", SqlDbType.Char).Value = txtEnroll.Text; cmdCommand.Parameters.Add("@cid", SqlDbType.Char).Value = txtCourseID.Text; } |

图 7.25 数据更新操作的代码。

打开 RTOUpdateDelete 项目和 Course 表单，双击 Update 按钮打开其 Click 方法。在此方法中输入图 7.25 所示的代码。让我们看看这段代码，看看它是如何工作的。

- A. 查询字符串首先在方法的开始处定义。Table 表中的所有数据列（course_id）都是输入参数。动态参数 @cid 表示原始的 course_id，它是 Table 表的主键，不会被更新。
- B. 在此处声明所有组件和局部变量，例如 Command 对象和整数变量 intUpdate。后者用于存储调用 ExecuteNonQuery() 方法返回的状态。
- C. 使用 Connection 对象和 Parameter 对象初始化 Command 对象。
- D. 调用用户定义方法 UpdateParameters，其代码在 H 所示，将所有参数添加到 Command 的属性中。参数使用的传递模式是引用传递，这意味着该 Command 对象的有效起始地址被传递到方法，对该 Command 对象的任何修改都存在并可以返回给调用方法。
- E. 执行 Command 类的 ExecuteNonQuery() 方法以更新 Table 中的课程。该方法的运行结果返回并存储在局部变量 intUpdate 中。
- F. 在此数据更新后释放 Command 对象。
- G. 调用 ExecuteNonQuery() 方法的返回值等于 Table 表中更新的行数。零表示没有行被更新，如果这种情况真的发生了，则会显示错误消息来指示。

