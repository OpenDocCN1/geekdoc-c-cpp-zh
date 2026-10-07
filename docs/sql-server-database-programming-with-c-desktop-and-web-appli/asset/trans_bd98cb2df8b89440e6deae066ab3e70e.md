

# 使用 C# 进行 SQL Server 数据库编程

此错误。另一个自定义方法 ReportError() 的代码稍后将，将被调用以报告此错误。

-   I. 必须将属性值 CommandType.StoredProcedure 赋值给 Command 对象的 CommandType 属性，以告诉项目在执行此命令时应调用存储过程。
-   J. 将输入参数分配给 `Parameters` 集合，以作为要插入到 `Course` 表的新课程。需要注意的一点是，这些输入参数的名称必须与第 6 章 6.6.1 节开发的存储过程 `dbo.InsertFactory(Course)` 中定义的名称完全一致。参考本节以获取该存储过程中定义的参数名称的详细说明。
-   K. 执行 `ExecuteNonQuery` 方法来调用存储过程执行此数据插入。该方法返回一个存储在我们本地变量 `insert` 中的整数值。
-   L. 一个清理方法，用于去分配并释放在此方法中使用的数据对象。
-   M. 调用 `ExecuteNonQuery()` 的返回值（存储在变量 `insert` 中）等于成功插入到 `Course` 表的行数。如果此值为 0，则意味着没有向我们的数据库插入新行且数据插入失败，一个警告消息被赋值给成员数据 `SqlInsertError`，并将由我们的自定义方法 `ReportError()` 报告。
-   N. 最后，我们的基类 `SqlInsertResult` 被返回给调用过程，以指示此方法的运行结果。

接下来处理该项目中使用的两个自定义方法的编码工作。

## 9.4.2.2 开发自定义方法的代码

该项目包含两个自定义方法：`SqlCommit()` 和 `ReportError()`。请参考第 9.3.7.3 节的图 9.19 和第 9.3.7.4 节的图 9.22 以获取有关这些自定义方法的更多详细信息。为了方便起见，这两个方法的详细代码如图 9.52 所示。

此时我们已经完成了此 Web 方法的编码开发和修改。我们现在可以运行此 Web 服务，通过该服务向示例数据库插入一条新的课程记录。点击 IIS Express 按钮运行项目。内置的 Web 界面如图 9.53 所示。

点击方法 `SqlInsertSP` 以打开另一个内置的 Web 接口来显示参数窗口，如图 9.54 所示。

在此 Web 方法中输入以下课程记录：

| FacultyName: Yin Bai |
| CourseID: CSE-556 |
| Course: Advanced Fuzzy Systems |
| Schedule: M-W-F: 1:00-1:55 PM |
| Classroom: LTC-315 |
| Credit: 3 |
| Enroll: 28 |

点击 `Invoke` 按钮运行此 Web 方法，以调用存储过程执行此数据插入。运行结果显示在内置的 Web 界面中，如图 9.55 所示。

根据返回的数据 `SqlInsertOK = True`，表明我们的数据插入成功。为了确认这一点，首先点击位于右上角的 `Close` 按钮。

# ASP.NET Web Services

| WebServiceInsertProject | SQLConn() |

```csharp
using System.Configuration;
protected SQLConnection SQLConn()
{
    string cmd = ConfigurationManager.Connections("sql-conn").ConnectionString;
    SQLConnection conn = new SQLConnection();
    conn.ConnectionString = cmd;
    conn.Open();
    if (conn.State != System.Data.ConnectionState.Open)
        conn = null;
    return conn;
}
protected void ReportError(SQLInsertBase Error)
```

**图 9.52** 两个用户方法的详细代码。

![](img/d59a47501d0a20fc0460a49c469c6fb7_595_0.png)

**图 9.53** 内置 web 界面的运行状态。

此 Web 界面终止我们的 Web 服务项目。使用 Server Explorer 或 Microsoft SQL Management Studio 打开示例数据库 `CSE_DEPT` 中的 `Course` 以检查此插入的课程。

可以发现 `course_id = CSE-556` 的新插入课程已插入到 `Course` 表的最后一行，其 `faculty_id = B78880`。这证实了我们的数据插入成功了。

## 9.4.2.3 开发第二个方法 GetInsert

该方法的功能根据输入的教师名称从 `Course` 表中检索所有 `course_id`，包括原始和新插入的 `course_id`。此方法将由客户端项目负责人调用或消费，以便在客户端项目的 ListBox 控件中获取并显示所有 `course_id`。

回想第5章第5.1.6节，我们开发了一个连接表查询，根据教师名称对所有 `course_id` 执行数据查询。之所以 `Course` 表中没有教师名称列，是因为每个课程或 `course_id` 都与所选教师名称关联的 `faculty_id` 相关，必须先从教师表中进行查询以获取它。在这种情况下，查询是执行此功能的理想方法。

我们将使用相同的策略在本节中执行此数据查询。

# 568 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_595_0.png)

**图 9.54** 输入参数。

![](img/d59a47501d0a20fc0460a49c469c6fb7_596_0.png)

**图 9.55** 运行结果。

![](img/d59a47501d0a20fc0460a49c469c6fb7_596_1.png)

**图 9.56** 我们第二个方法的代码。

# ASP.NET Services

| WebServiceInsertProject | GetInsert(string fullName) |

