

# 使用 C#.NET 插入数据

| RTOInsert | CurrentFaculty() |

```csharp
private void CurrentFaculty()
{
    SqlDataReader sqlReader;
    SqlConnection conn = loginForm.SqlConnection;
    SqlCommand sqlCommand = new SqlCommand("SELECT faculty_name FROM Faculty", conn);
    sqlReader = sqlCommand.ExecuteReader();
    ComboBoxName.Items.Clear();
    while (sqlReader.Read())
{
        ComboBoxName.Items.Add(sqlReader["faculty_name"]);
    }
    ComboBoxName.SelectedIndex = 0;
    sqlReader.Close();
}
```

**图 6.31** CurrentFaculty() 方法的代码。

- 在我们检索所有院系名称并将其添加到组合框 **ComboBoxName** 之前，我们需要清理该组合框以做好就绪。
- 使用 **while** 循环并以 **SqlReader.Read()** 作为条件，扫描并逐个读取所有院系名称，将它们每一个都添加到组合框 **ComboBoxName** 中。一个问题是，可以使用 **SqlReader** 对象的列名或列索引来获取每个院系名称。
- 通过将 **SelectedIndex** 属性设置为0，可以将第一个添加的院系名称选择为默认值并显示在组合框的顶部。
- 最后，使用 **Close()** 方法关闭 **SqlReader**。

现在，让我们为 **Insert** 按钮的 Click 方法编写代码，调用这两个方法来执行验证，并执行数据插入操作。

## 6.5.3 数据插入操作的编码过程

现在，在 Faculty Form 窗口上双击插入按钮，打开其 Click 方法，并将图 6.32 所示的代码输入到方法中。

这段代码的功能非常直观且易于理解。首先，调用用户自定义方法 **initFaculty()** 来设置数组 **Faculty[]** 中每个项目与每个 TextBox 之间的映射关系。然后执行另一个用户自定义方法 **CheckFaculty()** 来检查并确保没有 TextBox 是空的。如果任何一个 TextBox 为空，该方法将返回一个非零值，允许用户重新填写关联 TextBox 单元的任何缺失信息，直到所有单元都非为空。让我们来看这段代码看看它是如何工作的。

- 首先创建两个本地整数变量，**check** 和 **intinsert**。前者用作我们自定义方法 **CheckFaculty** 结果的状态持有者，后者用作执行方法 **ExecuteQuery()**的状态持有者。
- 插入查询声明了八项新的院系信息，插入到示例数据库的 **Faculty** 表中。
- 这里声明了用于执行数据插入的一些数据组件，包括 **DataAdapter** 和 **SqlCommand** 对象。

# RTOInsert C# SQL 数据库编程

```csharp
private void cmdInsert_Click(object sender, EventArgs e)
{
    int check, intInsert;
    string cmdString="INSERT INTO faculty (faculty_id, faculty_name, title, office, college, image) " +
        "VALUES (@faculty_id, @faculty_name, @title, @office, @college, @image)";
    SqlDataAdapter dataAdapter=new SqlDataAdapter();
    SqlCommand sqlCommand=new SqlCommand();
    InitFaculty();
    if (check == 0)
    {
        sqlCommand.Connection=loginForm.Connection;
        sqlCommand.CommandType=CommandType.Text;
        sqlCommand.Text=cmdString;
        InsertParameters(sqlCommand);
        dataAdapter.SqlCommand=sqlCommand;
        intInsert=dataAdapter.ExecuteNonQuery();
        if (intInsert != 0)
        {
            MessageBox.Show("插入失败");
        }
        else
        {
            PhotoBox.Image=null;
            CurrentFaculty();
            ClearFacultyInfo();
            cmdInsert.Enabled=false;
        }
    }
    MessageBox.Show("填写所有院系信息，输入为空");
}
```

6.32 插入按钮完成的代码。

- D. 执行两个用户自定义方法 InitFacultyInfo() 和 CheckFacultyInfo()，以在类级数组 Faculty[] 和 Faculty Form 中的每个 TextBox 之间建立映射关系，并检查 TextBox 是否已填写值。
- E. 如果返回的 check 为 0，意味着所有 TextBox 都已填写值，初始化 Command 对象的属性，如 Connection、CommandType 和 CommandText。需要注意的是，我们不需要创建新连接，而是可以使用 LoginForm 中创建的类级 Connection 对象。
- F. 稍后将调用另一个用户自定义方法 InsertParameters()，将八项院系信息添加到 Command 对象的属性中。
- G. 这两条指令用于通过另一个方法 DataAdapter 执行数据插入。它们都被已注释掉，以与下方的 ExecuteNonQuery() 方法集中。该方法提供了与下方的 ExecuteNonQuery() 方法相同的功能。
- H. 通过调用 ExecuteNonQuery() 方法执行数据插入，将此新记录物理插入示例数据库中的 faculty 表。该方法的执行结果返回并赋值给本地变量 intInsert。
- I. 如果 intInsert 返回值为 0，意味着数据插入失败。显示警告消息以指示这种情况。

# 使用 C#.NET 插入数据

- J. 否则，数据插入成功，执行一些清理工作以清除 Faculty Form 中的所有 TextBox 和 PhotoBox。执行用户自定义方法 CurrentFaculty() 以获取新插入的所有院系名称，并将它们添加到组合框 ComboName，以便用户以后执行检查或确认工作。禁用 Insert 以避免任何重复插入。
- K. 如果整数返回非零值，意味着 TextBox 未填写值，显示警告消息以指示这种情况。

现在，让我们查看 Insert 方法中一些用户自定义方法，包括方法 InsertParameters()、ClearFaculty() 和 getFaculty()。第一个是将所有新插入信息添加到 Command 对象的 Parameters 中以配置 Command 对象，第二个作为清理方法来清除插入到 Faculty 中的所有 TextBox 内容，第三个方法用于获取用户选择的院系图像。

用户自定义方法 InsertParameters() 的详细代码如图 6.33 所示。在 Faculty Form 的打开窗口中，输入这段代码使该方法可用。这段代码的功能很简单，首先生成一个 byte[] image，此数组用于持有用户选择的院系图像并插入数据库中。调用用户自定义方法 getFaculty() 来获取选择的院系图像并将其赋值给数组。对该图像使用 byte[] 格式的原因是 SQL Server 数据库存储图像的要求。

接下来，使用 Add() 方法将存储在 TextBox 每个院系相关信息分配给每个匹配的参数。需要注意的是，每个参数前必须带有 @ 符号，因为这是 SQL Server 数据库操作的规则。

现在，留在打开的代码窗口，输入方法 ClearFaculty()。为了清理 Faculty Form 中的所有 TextBox，生成一个本地数组作为所示 for 循环的计数器。通过将所有 TextBox 分配给该数组创建一个 TextBox array[]。在 for 循环的帮助下，通过为每个属性分配零长度或空字符串来清理数组中存储的每个 TextBox。fbox.length 属性作为 for 循环的上限。

最后，让我们处理 getFaculty() 方法。在 Faculty Form 的打开窗口中，代码如图 6.35 所示，这些是该方法的代码体。

| RTOIntObject | InsertParameters(SqlCommand cmd) |
|---|---|

