

# ASP.NET Web Services

| WebServiceUpDtP | SQLUpdateSP() |
| --- | --- |
| A | using System.Configuration;using System.Data;using System.Data.SqlClient;using System.Web.Services; | |
| B | public SQLBase SQLUpdateSP(string stringName, float GPA, int Credits, string Major, string SchoolYear, string byte[], string image, string StudentID) | |

```csharp
[WebMethod]
public SQLBase SQLUpdateSP(string stringName, float GPA, int Credits, string Major, string SchoolYear, byte[] byte[], string image, string StudentID)
{
    string cmd = "dbo.WebUpdateDataSet";
    SqlConnection connection = new SqlConnection();
    SQLBase Result = new SQLBase();
    SqlCommand command = new SqlCommand(cmd);
    int intUpdate;
    Result.SQLOK = true;
    connection.Open();
    if (connection == null)
    {
        Result.Error = "Database connection is failed";
        ReportError(Result);
        return null;
    }
    command.Connection = connection;
    command.CommandType = CommandType.StoredProcedure;
    command.CommandText = cmd;
    command.Parameters.Add("@Name", SqlDbType.VarChar).Value = stringName;
    command.Parameters.Add("@GPA", SqlDbType.Char).Value = GPA;
    command.Parameters.Add("@Major", SqlDbType.Text).Value = Major;
    command.Parameters.Add("@SchoolYear", SqlDbType.Text).Value = SchoolYear;
    command.Parameters.Add("@Credits", SqlDbType.Int).Value = Credits;
    command.Parameters.Add("@Email", SqlDbType.Text).Value = Email;
    command.Parameters.Add("@image", SqlDbType.Image).Value = image;
    command.Parameters.Add("@StudentID", SqlDbType.Text).Value = StudentID;
    intUpdate = command.ExecuteNonQuery();
    command.Dispose();
    connection.Close();
    if (intUpdate == 0)
    {
        Result.Error = "Data updating is failed";
        ReportError(Result);
    }
    return Result;
}
```

图 9.97 传递给 SQLUpdateSP() 方法的参数类型的代码。

唯一的修改是将传递给此方法的参数的类型更改为 `SQLBase`，因为我们只需要检查此数据更新操作的状态，并将基类的成员数据更改为 `SQLOK`。

转到“文件 | 保存所有”项目以保存这些修改。接下来，让我们使用我们的方法 `SQLDeleteSP()` 来调用存储过程以删除学生记录。

# 9.5.4 创建一个 Web 方法来调用存储过程删除学生记录

如第 7 章第 7.1.1 节所述，要从关系型数据库中删除记录，需要按照下面列出的操作步骤进行操作：

- 1) 从子表中通过外键删除与主表相关的记录。
- 2) 从主表中删除定义为主键的记录。

# 使用 C# 进行 SQL Server 数据库编程

| WebServerUpDt Project | SQLConn() |
| --- | --- |

```csharp
protected SqlConnection SQLConn()
{
    string cmdString = ConfigurationManager.ConnectionString["sql_conn"].ConnectionString;
    SqlConnection conn = new SqlConnection();
    conn.ConnectionString = cmdString;
    conn.Open();
    if (conn.State != System.Data.ConnectionState.Open)
    {
        conn = null;
    }
    return conn;
}

protected void ReportError(SQLBase ErrSource)
{
    ErrSource.SQLOK = false;
}
```

**图 9.98** 两个删除方法的详细代码。

换句话说，要从主表中删除一条记录，必须删除与外键相关且位于不同子表的所有记录。要从主表中删除一条记录，需要通过外键从子表中删除与主表相关的记录，然后从主表中删除定义为主键的记录。要从主表中删除一条记录，是将传递给此方法的参数类型更改为 `SQLBase`，因为我们只需要检查此数据更新操作的状态，并将基类的成员数据更改为 `SQLOK`。转到“文件 | 保存所有”项目以保存这些修改。接下来，让我们使用我们的方法 `SQLDeleteSP()` 来调用存储过程以删除学生记录。

图 9.98 传递给 SQLDelete 方法的参数类型代码。

换句话说，要从主表中删除一条记录，必须删除与外键相关且位于不同子表的所有记录。要从主表中删除一条记录，需要通过外键从子表中删除与主表相关的记录，然后从主表中删除定义为主键的记录。唯一的修改是将传递给此方法的参数的类型更改为 `SQLBase`，因为我们只需要检查此数据更新操作的状态，并将基类的成员数据更改为 `SQLOK`。转到“文件 | 保存所有”项目以保存这些修改。接下来，让我们使用我们的方法 `SQLDeleteSP()` 来调用存储过程以删除学生记录。

# ASP.NET Web Services

| WebServiceDt | SQLDelete() |
| --- | --- |

```csharp
[Method]
public void SQLDelete(string sName)
{
    string cmdString = "WebDelete";
    SqlConnection connection = new SqlConnection();
    SqlBase Result = new SqlBase();
    int intDelete;

    Result.SQLOK = true;
    connection.Open();
    if (connection == null)
    {
        Result.SQLOK = false;
        Result.Error = "Database connection is failed";
        ReportError(Result);
        return;
    }
    SqlCommand command = new SqlCommand(cmdString, connection);
    command.CommandType = CommandType.StoredProcedure;
    command.Parameters.Add("@sName", SqlDbType.VarChar).Value = sName;
    intDelete = command.ExecuteNonQuery();
    if (intDelete == 0)
    {
        Result.Error = "Data deleting failed";
        ReportError(Result);
    }
    connection.Close();
    command.Dispose();
    return;
}
```

图 9.99 SQLDelete 方法的代码。

- A. 首先，我们预先将方法的良好状态指示设置为成员数据 `SQLOK`，以指示我们的方法目前运行正常。
- B. 如果在数据库连接过程中遇到任何错误，会将错误信息存储在成员数据 `SQLException` 中并使用自定义方法 `ReportError()` 进行报告。
- C. 使用包含两个参数的构造函数创建 `SqlCommand` 对象。然后初始化对象的关联数据对象和属性。重点是 `CommandType` 属性必须设置为 `StoredProcedure` 的值，因为此命令对象将调用存储过程来执行此数据删除操作。
- D. 动态参数 `@sName` 被分配了实际的 `sName` 作为此方法的输入参数。
- E. 执行 `ExecuteNonQuery` 方法来调用我们的存储过程以执行此数据删除操作。此方法返回一个整数表示该方法的状态，并将该返回值赋值给本地整数变量 `intDelete`。
- F. `ExecuteNonQuery` 返回的值等于从学生表中成功删除的行数。如果此返回值为 0，意味着没有从学生表中删除任何行，则将显示并使用自定义方法 `ReportError()` 报告错误信息。
- G. 执行清理工作以释放此方法中使用的所有对象。
- H. 最后，将包含方法运行状态的实例返回给调用过程。
- I. 这里的 `cmdString` 等于 `WebDelete`。
- J. 存储过程的 `intDelete` 变量已经声明。
- K. 这种方法 `intDelete` 对应的存储过程。
- L. 这种方法 `intDelete` 对应的方法。
- M. 这种方法 `intDelete` 用于存储该方法的返回值。
- N. 声明一个本地整数变量 `intDelete` 用于存储该方法的返回值。

