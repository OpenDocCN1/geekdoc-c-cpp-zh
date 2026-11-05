
- 2. 下一步是实际定义将用于我们数据库的 SQL 语句。在我们的例子中，我们发出一条 insert 语句，该语句将插入 TutorialID=1 且 TutorialName=VB.Net 的记录
- 3. 接下来，我们创建用于对数据库执行 SQL 语句的 command 对象。在 SQL command 中，你必须传递 connection 对象和 SQL 字符串
- 4. 在我们的数据适配器命令中，我们现在将 insert SQL 命令关联到我们的适配器。我们还发出 ExecuteNonQuery 方法，该方法用于对数据库执行 Insert 语句。‘ExecuteNonQuery’ 方法在 C# 中用于向数据库发出任何 DML 语句。所谓 DML 语句，我们指的是 insert、delete 和 update 操作。在 C# 中，如果你想对表发出这些语句中的任何一个，你需要使用 ExecuteNonQuery 方法。
- 5. 我们最后关闭与数据库操作相关的所有对象。记住这始终是一个良好的实践。

当上述代码设置好后，使用 Visual Studio 执行项目时，你将得到下面的输出。表单显示后，点击 Connect 按钮。

### Output

**登录**

连接

点击 连接 按钮

如果你实际进入 SQL Server Express 并查看 demotb 表中的行，你会看到插入的行如下所示

|  | TutorialName | TutorialID |
|---|---|---|
| 1 | C# | 1 |
| 2 | ASP.Net | 2 |
| 3 | VB.Net | 3 |

行已添加

## C# 更新数据库

就像访问数据一样，C# 也有能力更新数据库中已有的记录。为了展示如何更新我们数据库中的记录，让我们使用上面使用过的相同表结构。

| TutorialID | TutorialName |
|---|---|
| 1 | C# |
| 2 | ASP.Net |
| 3 | VB.Net |

让我们更改表单中的代码，以便我们可以更新以下行。旧行的值为 TutorialID 为“3”且 Tutorial Name 为“VB.Net”。我们将把它更新为“VB.Net complete”，而 Tutorial ID 的行值保持不变。

### 旧行

| TutorialID | TutorialName |
|---|---|
| 3 | VB.Net |

### 新行

| TutorialID | TutorialName |
|---|---|
| 3 | VB.Net complete |

所以让我们向我们的程序添加以下代码。下面的代码片段将用于更新数据库中已有的记录。

```csharp
SqlCommand command;
SqlDataAdapter adapter = new SqlDataAdapter();
String sql="";

sql = "Update demotb set TutorialName='"+"VB.Net Complete"+"' where TutorialID=3";

command = new SqlCommand(sql, cnn);

adapter.UpdateCommand = new SqlCommand(sql, cnn);
adapter.UpdateCommand.ExecuteNonQuery();

command.Dispose();
cnn.Close();
```

### 代码说明

- 1. 第一步是创建以下变量
  - a. SQLCommand – 此数据类型用于定义用于对数据库执行 SQL 操作的对象。此对象将保存将对我们的 SQL Server 数据库运行的 SQL 命令。
  - b. dataadapter 对象用于执行特定的 SQL 操作，例如 insert、delete 和 update 命令。
  - c. 然后我们定义一个字符串变量，即 SQL，用于保存我们的 SQL 命令字符串。
- 2. 下一步是实际定义将用于我们数据库的 SQL 语句。在我们的例子中我们发出一条 update 语句，这将把 Tutorial 名称更新为“VB.Net Complete”，而 TutorialID 保持不变为 3。
- 3. 接下来，我们将创建 command 对象，该对象用于对数据库执行 SQL 语句。在 SQL command 中，你已传递了 connection 对象和 SQL 字符串。
- 4. 在我们的数据适配器命令中，我们现在将 insert SQL 命令关联到我们的适配器。我们还发出 ExecuteNonQuery 方法，该方法用于对数据库执行 Update 语句。
- 5. 我们最后关闭与数据库操作相关的所有对象。记住这始终是一个良好的实践。

当上述代码设置好后，使用 Visual Studio 执行项目时，你将得到下面的输出。表单显示后，点击 Connect 按钮。

### Output

![](img/8115a2172ef67838d7fe1933fc517c4d_135_0.png)

如果你实际进入 SQL Server Express 并查看 demotb 表中的行，你会看到行已成功更新如下所示。

![](img/8115a2172ef67838d7fe1933fc517c4d_135_1.png)

## 删除记录

就像访问数据一样，C# 也有能力从数据库中删除已有的记录。为了展示如何删除我们数据库中的记录，让我们使用上面使用过的相同表结构。

| TutorialID | TutorialName |
|---|---|
| 1 | C# |
| 2 | ASP.Net |
| 3 | VB.Net complete |

让我们更改表单中的代码，以便我们可以删除以下行

| TutorialID | TutorialName |
|---|---|
| 3 | VB.Net complete |

所以让我们向我们的程序添加以下代码。下面的代码片段将用于删除数据库中已有的记录。

```csharp
SqlCommand command;
SqlDataAdapter adapter = new SqlDataAdapter();
String sql="";

sql = "Delete demotb where TutorialID=3";

command = new SqlCommand(sql, cnn);

adapter.DeleteCommand = new SqlCommand(sql, cnn);
adapter.DeleteCommand.ExecuteNonQuery();

command.Dispose();
cnn.Close();
}
```

### 代码说明

- 1. 此代码的关键区别在于我们现在发出 delete SQL 语句。delete 语句用于删除 demotb 表中 TutorialID 值为 3 的行。
- 2. 在我们的数据适配器命令中，我们现在将 insert SQL 命令关联到我们的适配器。我们还发出 ExecuteNonQuery 方法，该方法用于对数据库执行 Delete 语句。

当上述代码设置好后，使用 Visual Studio 执行项目时，你将得到下面的输出。表单显示后，点击 Connect 按钮。

### Output

![](img/8115a2172ef67838d7fe1933fc517c4d_137_0.png)

如果你实际进入 SQL Server Express 并查看 demotb 表中的行，你会看到行已成功删除如下所示。

![](img/8115a2172ef67838d7fe1933fc517c4d_137_1.png)

## 将控件连接到数据

在之前的章节中，我们已经看到如何使用 C# 命令如 SQLCommand 和 SQLReader 从数据库获取数据。我们还看到了如何读取表的每一行并使用 messagebox 将表的内容显示给用户。

但显然，用户不想通过 message box 查看数据，而是希望有更好的控件来显示数据。让我们看下面表中的数据结构

| TutorialID | TutorialName |
|---|---|
| 1 | C# |
| 2 | ASP.Net |
| 3 | VB.Net complete |

从上述数据结构来看，用户理想情况下希望在 textbox 中看到 TutorialID 和 Tutorial Name。其次，他们可能希望有某种按钮控件，可以让他们在表中移动到下一条记录或上一条记录。这需要开发人员做一些额外的编码。

好消息是 C# 通过允许控件与数据绑定来减少额外的编码工作。这意味着 C# 可以根据表的特定字段自动填充 textbox 的值。

因此，你可以在 windows form 中有 2 个 textbox。然后你可以将一个 text box 链接到 TutorialID 字段，另一个 textbox 链接到 TutorialName 字段。这种链接是在 Visual Studio 设计器中完成的，你不需要为此编写额外的代码。

Visual Studio 将确保它实际上为你编写代码以确保链接正常工作。然后当你运行应用程序时，textbox 控件将自动连接到数据库，获取数据并在 textbox 控件中显示。开发人员无需编码即可实现这一点。

让我们看一个代码示例，了解如何实现控件绑定。

在我们的示例中，我们将在 windows form 上创建 2 个 textbox。它们将分别代表 Tutorial ID 和 Tutorial Name。它们将相应地绑定到数据库的 Tutorial ID 和 TutorialName 字段。

让我们按照下面提到的步骤来实现这一点。
