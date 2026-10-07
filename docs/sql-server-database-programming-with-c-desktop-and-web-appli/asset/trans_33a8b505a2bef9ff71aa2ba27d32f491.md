

I. 通过检查 DataReader 的 `HasRows` 属性，我们确定本次读取是否成功。如果读取成功（HasRows=True），则调用用户定义的方法 `FillCourseReader()`（其详细细节将在后文中讨论），将返回的 `course_id` 分配给我们返回对象 `GetSQLResult` 中的每个关联成员数据。

J. 否则，如果读取失败，则将一个警告消息赋值给返回对象中的成员数据 `SqlError`，并由 `ReportError()` 报告。

K. 执行清理作业以释放此 Web 方法中的所有数据对象。
- 将包含所有 `course_ids` 的返回对象返回给调用过程。

我们的用户定义方法 `FillCourseReader()` 的详细代码所示如图 9.57。这段代码的功能非常直观，没有任何技巧。使用 `while()` 循环来继续从 `Course` 表中选取列索引为 0 的每个 `course_id`，将其转换为字符串并赋值给每个类 `SQLInsertRecord` 中的 `CourseID` 字符串数组。

现在，让我们通过运行此项目来测试这个 Web 方法。点击 IIS Express 按钮来运行我们的项目，将显示内置 Web 界面，如图 9.58 所示。点击 Web 方法 `GetInsert()`，并在下一个内置 Web 界面的 `FacultyName` 框中输入教师姓名 Yin Bai，然后点击 `Invoke` 按钮执行该方法。该方法的结果如图 9.60 所示。

可以看出，所有的课程（确切是所有的 `course_ids`），包括由选教师 Yin Bai 授的插入课程 CSE-556，都以 XML 格式插入了。

| WebServiceInsert Project | FillCourseReader() |
| :--- | :--- |
| protected void FillCourseReader(ref SQLInsertRecord sResult, SqlDataReader sReader) { |
| int pos = 0; |
| while (sReader.Read()) { |
| sResult.CourseID[pos] = System.Convert.ToString(sReader.GetSqlString()); // 第 1 列是 course_id |
| pos++; |
| } | |

图 9.57 FillCourseReader() 方法的代码。

![](img/d59a47501d0a20fc0460a49c469c6fb7_598_0.png)

图 9.58 我们 Web 服务项目的运行状态。

# ASP.NET Web Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_599_0.png)

**图 9.59** Web 方法 `SQLGetInsert()` 的输入参数宽度。

![](img/d59a47501d0a20fc0460a49c469c6fb7_599_1.png)

**图 9.60** 我们 Web 方法 `GetInsert()` 的运行结果。

我们的第二个 Web 方法执行成功。点击此页面右上角的 **Close** 按钮终止我们的 Web 服务项目。转到 **File | Save All** 保存我们开发的所有方法。

接下来，让我们来构建第三个方法 **InsertDataSet()**，使用 DataSet 方法向 **Course** 表插入数据。

## 9.4.2.4 开发第三个 Web 方法 InsertDataSet()

该方法的功能与第一个 Web 方法类似，即根据所选教师向 **Course** 表插入新的课程记录。区别在于，该 Web 方法使用多查询来向 Course 表插入新的课程记录，并使用 DataSet 作为返回对象。此外，返回的 DataSet 包含了更新后的 Course 表，该表包含了已插入的课程记录。使用 DataSet 作为返回对象的优势包括：

- 1) 与成对出现的方法 1 和 2 不同（它们是一对方法，第一个用于向数据库插入数据，第二个用于从数据库中检索新插入的数据以确认插入成功），方法 3 包含了数据插入和检索功能。稍后当开发客户端项目来使用此 Web 服务时，必须从该客户端项目同时调用方法 1 和 2 来执行数据插入和验证工作。方法 3 具有数据插入和验证功能，因此可以被独立调用。
- 2) 因为返回的是 DataSet，所以我们不需要为自定义类创建任何新实例作为返回对象。为了报告或记录项目运行期间遇到的任何异常，我们仍然需要创建并使用自定义类的实例来处理这些错误处理问题。

创建并添加 Web 方法 `InsertDataSet()`，并将图 9.61 所示的代码输入到该方法中。让我们此方法中的 DataSet，看看它是如何运作的。

- A. Web 方法名为 `InsertDataSet()`。七个参数作为新插入记录传递到此方法，返回的数据类型为 `DataSet`。
- B. 数据插入查询所示此处。前两个查询用于执行数据插入，第三个用于从数据库中检索新插入的数据以验证插入情况。对于数据插入，我们首先需要对 `Faculty` 表进行查询，根据输入的名称获取匹配的 `faculty_id`，因为 `Course` 表中没有可用列名。其次，我们可以根据从第一个查询获得的 `faculty_id` 执行另一个查询，向 `Course` 表插入新的课程记录。在此声明的第二个查询是第二个查询字符串。
- C. 此 Web 方法使用的所有对象均在此声明，包括 `Connection`、`Command`、`DataAdapter` 以及我们类 `SQLite` 的实例。整数变量 `result` 用于保存调用 `ExecuteNonQuery()` 的返回值。字符串变量 `facultyID` 用于保留从第一个查询获取的 `faculty_id`。
- D. 成员变量 `sqlConn01` 初始化为普通情况。
- E. 成员变量 `sqlConn01` 初始化为普通情况。
- F. 成员变量 `sqlConn01` 初始化为普通情况。
- G. 成员变量 `sqlConn01` 初始化为普通情况。
- H. 成员变量 `sqlConn01` 初始化为普通情况。
- I. 成员变量 `sqlConn01` 初始化为普通情况。

```csharp
public DataSet InsertDataSet(string FacultyName, string CourseID, string Course, string Schedule, int Credit, int enroll)
{
    string cmdString = "INSERT INTO COURSE (@course_id, @course, @schedule, @classroom, @credit, @enrollment, @faculty_id)";
    SqlConnection connection = new SqlConnection();
    SqlInsertBase base = new SqlInsertBase();
    SqlCommand command = new SqlCommand(cmdString, connection);
    SqlDataAdapter adapter = new SqlDataAdapter(adapter);
    DataSet ds = new DataSet();
    int result = 0;
    string facultyID;
    base.SqlInsert(true);
    connection.Open();
    if (connection.State == null)
    {
        resultSet.SqlInsertError = "Database connection failed";
        ReportError(resultSet);
        return null;
    }
    command.CommandText = "SELECT * FROM Faculty WHERE faculty_name = @Name";
    command.Parameters.Add("@Name", SqlDbType.VarChar).Value = FacultyName;
    facultyID = (string)command.ExecuteScalar();
    command.CommandText = cmdString;
    command.Parameters.Add("@course_id", SqlDbType.VarChar).Value = CourseID;
    command.Parameters.Add("@course", SqlDbType.VarChar).Value = Course;
    command.Parameters.Add("@schedule", SqlDbType.Char).Value = Schedule;
    command.Parameters.Add("@classroom", SqlDbType.Text).Value = Classroom;
    command.Parameters.Add("@credit", SqlDbType.Int).Value = Credit;
    command.Parameters.Add("@enrollment", SqlDbType.Int).Value = enroll;
    command.Parameters.Add("@faculty_id", SqlDbType.Int).Value = facultyID;
    adapter.InsertCommand = command;
    result = command.ExecuteNonQuery();
    if (result == 0)
    {
        resultSet.SqlInsertError = "No matched course found";
        ReportError(resultSet);
    }
    command.CommandText = "SELECT * FROM Course WHERE faculty_id = @FacultyID";
    command.Parameters.Add("@faculty_id", SqlDbType.VarChar).Value = facultyID;
    adapter.SelectCommand = command;
    adapter.Fill(ds, "Course");
    connection.Close();
    command.Dispose();
    return ds;
}
```
*(注：由于原文代码块中存在一些逻辑/变量定义错误，如 `Classroom` 未定义、`command` 赋值冲突等，根据指令“代码块不需要翻译”原则，此处保持了原始代码逻辑结构，仅对不必要的重复进行了微调以确保可读性，或严格遵循不翻译代码原则)*

图 9.61 FillCourseReader() 方法的代码。

- J. 第二个查询字符串赋值给 `CommandText` 以执行第二个查询 - 向 Course 表插入课程记录。
- K. 将初始化对象赋值给 `adapter` 的 `InsertCommand` 属性。
- L. 成员变量 `sqlConn01` 初始化为普通情况。

