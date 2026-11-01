
姓氏和年龄字段，因为我们将需要这些信息用于其他操作。我们只需要创建如下所示的readCommand，使其也包含id_number：

```
OleDbCommand readCommand = new OleDbCommand("SELECT
    name_field, surname_field, age_field FROM Table1",
    myConn);
```

代码 15.14

另外，在while循环中使用下面的Add()方法添加数据库条目，以同时添加id_number：

```
displayListBox.Items.Add(reader["id_number"] + "-" +
    reader["name_field"].ToString() + "-" +
    reader["surname_field"] + "-" +
    reader["age_field"]);
```

代码 15.15

经过这些小幅修改后，我们的listButton_Click()方法如下所示：

```csharp
private void listButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();
    OleDbCommand readCommand = new OleDbCommand("SELECT id_number, name_field, surname_field, age_field FROM Table1", myConn);
    OleDbDataReader reader = readCommand.ExecuteReader();
    displayListBox.Items.Clear();
    while (reader.Read())
    {
        displayListBox.Items.Add(reader["id_number"] + "-" + reader["name_field"].ToString() + "-" + reader["surname_field"] + "-" + reader["age_field"])
    }
    myConn.Close();
}
```

代码 15.16

10. 让我们生成并运行项目，看看我们的List entries按钮是否正常工作。当点击List entries按钮时，条目应该连同id_number一起列在ListBox中：

![](img/41d82527c4e41cdb7e56259564306ddc_368_0.png)

图15.22. 数据条目列在ListBox中

如果你看不到数据，或者程序报错，请在继续之前仔细检查前面的步骤。

11. 现在让我们为Delete按钮开发代码。用户将在ListBox中选择一行，然后点击此按钮以从数据库中删除所选条目。首先，双击Delete按钮以创建其事件处理方法deleteButton_Click(...)。

12. 首先，我们将打开连接：

```
string path = Environment.CurrentDirectory;
string databasePath = path + "\\firstDatabase.accdb";
OleDbConnection myConn = new
OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
myConn.Open();
```

代码 15.17

13. 然后我们将获取ListBox中选中的条目，并通过以下代码行取得其id_number：

```csharp
string selectedEntry = displayListBox.SelectedItem
    .ToString();
int selectedEntry_id_number = int.Parse(selectedEntry
    .Split('-')[0]);
MessageBox.Show("The entry with id_number: " + 
    selectedEntry_id_number + " will now be deleted.");
```

代码 15.18

在第一行中，我们获取ListBox中所选行的完整文本。然后解析该文本，以获取连字符前的第一部分，也就是id_number。我们显示一个消息框，告知用户将要删除的条目。

14. 然后我们将构建执行删除所需的查询，如下所示：

```csharp
OleDbCommand cmd = new OleDbCommand("DELETE FROM Table1
    WHERE id_number=?", myConn);
cmd.Parameters.AddWithValue("?", selectedEntry_id_number);
```

代码 15.19

我们用查询行（"DELETE FROM Table1 WHERE id_number=?"，该查询将作用于myConn）构造一个全新的OleDbCommand对象。我们传入之前获取的id_number。我们使用“?”符号，通过将其作为参数添加到查询中来传递id_number。

15. 最后，我们按如下方式执行cmd对象：

```csharp
int cmdResult = cmd.ExecuteNonQuery();
MessageBox.Show("Number of deleted entries: " + 
    cmdResult.ToString());
myConn.Close();
```

代码 15.20

ExecuteNonQuery()是实际运行查询的方法。它返回受查询影响的条目数。我们将此结果存储在名为cmdResult的变量中。然后显示受影响条目数的信息，并关闭连接。完整起见，下面也给出了完整的deleteButton_Click(...)：

```
private void deleteButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new
        OleDbConnection("Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();

    string selectedEntry =
        displayListBox.SelectedItem.ToString();
    int selectedEntry_id_number =
        int.Parse(selectedEntry.Split('-'));

    MessageBox.Show("The entry with id number: " +
        selectedEntry_id_number + " will now be deleted.");

    OleDbCommand cmd = new OleDbCommand("DELETE FROM Table1
        WHERE id_number=?", myConn);
    cmd.Parameters.AddWithValue("?",
        selectedEntry_id_number);

    int cmdResult = cmd.ExecuteNonQuery();
    MessageBox.Show("Number of deleted entries: " +
        cmdResult.ToString());
    myConn.Close();
}
```

代码 15.21

16. 生成并运行项目，看看目前一切是否正常。首先点击List entries按钮，将数据库条目显示在ListBox中：

![](img/41d82527c4e41cdb7e56259564306ddc_370_0.png)

图15.23. 数据库条目列在ListBox中

点击选择ListBox中的一个条目。我选择了第二个：

![](img/41d82527c4e41cdb7e56259564306ddc_371_0.png)

图15.24. 第二个条目被选中

现在，点击Delete selected按钮。程序将弹出关于要删除条目的id_number的消息，如图15.25所示。然后该条目将从数据库中删除，随后将显示受影响条目数的信息，如图15.26所示。

![](img/41d82527c4e41cdb7e56259564306ddc_371_1.png)

图15.25. 显示删除信息的消息框

## 第15章 使用ADO.NET进行数据库连接

![](img/41d82527c4e41cdb7e56259564306ddc_372_0.png)

图15.26. 显示已删除条目数的消息框

点击List entries按钮，查看所选条目是否真的从数据库中删除。它被成功删除，证明我们的Delete按钮按预期工作，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_372_1.png)

图15.27. 删除第二个条目后显示的数据库条目

17. 我们现在准备实现插入操作。当点击Insert按钮时，我们将获取Name、Surname和Age输入，并将它们作为新条目插入数据库。双击Insert按钮以创建其Click事件处理方法insertButton_Click()。

我们将编写insertButton_Click()方法的代码。首先，复制并粘贴我们之前实现的标准数据库连接部分：

```csharp
string path = Environment.CurrentDirectory;
string databasePath = path + "\\firstDatabase.accdb";
OleDbConnection myConn = new
OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
myConn.Open();
```
代码 15.22

现在，创建一个OleDbCommand对象，它将保存插入查询，如下所示：

```csharp
OleDbCommand cmd = new OleDbCommand("INSERT INTO Table1(name_field,surname_field,age_field) VALUES (?,?,?)", myConn);
```
代码 15.23

我们将利用“?”参数，从insertNameTextBox、insertSurnameTextBox和insertAgeTextBox传递name_field、surname_field和age_field字符串：

```csharp
cmd.Parameters.AddWithValue("?", insertNameTextBox.Text);
cmd.Parameters.AddWithValue("?", insertSurnameTextBox.Text);
cmd.Parameters.AddWithValue("?", insertAgeTextBox.Text);
```
代码 15.24

最后，像我们在Delete按钮中所做的那样，使用ExecuteNonQuery()方法执行查询命令：

```csharp
int cmdResult = cmd.ExecuteNonQuery();
MessageBox.Show("Number of inserted entries: " + cmdResult.ToString());
myConn.Close();
```
代码 15.25

