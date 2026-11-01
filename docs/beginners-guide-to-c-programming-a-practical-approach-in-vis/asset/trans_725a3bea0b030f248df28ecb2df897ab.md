

请单击 Save 按钮。现在，我们已经创建了示例数据库，并直接在 Access 中向其中添加了一些数据。接下来，我们将从自己的 C# 程序连接到此数据库。

## 15.2. 从 C# 程序读取数据库条目

我们的程序可以通过 Access Database Engine 连接到 Access 数据库。如果你的计算机安装的是 2007 年之后发布的 Office 套件，则 Access Database Engine 已经安装在计算机上。否则，你可以从 https://www.microsoft.com/en-us/download/details.aspx?id=13255 下载此工具（或者直接在 Google 中搜索“Access Database Engine”），然后将其安装到计算机上。

C# .NET 程序通过数据库命令访问数据库。首先，打开与数据库的连接。然后，使用数据库命令对数据库表执行读写操作。完成数据库操作后，关闭连接。

我们可以使用以下对象访问和操作 Access 数据库：

- **OleDbConnection**：用于打开或关闭与数据库的连接。其构造函数接受文件路径以及与数据库类型相关的连接字符串。
- **OleDbCommand**：用于向数据库发送查询，以选择和操作数据。
- **DataReader**：用于从数据库读取数据。它与 OleDbCommand 对象结合使用。
- **OleDbDataAdapter**：将数据传输到 DataSet 对象。
- **DataSet**：临时存储数据，以便进行显示和操作。

下面通过一个典型示例，看看如何使用这些对象连接到 firstDatabase.accdb。

1. 创建一个新的 C# 项目。
2. 在窗体上添加两个 Button 和一个 ListBox。
3. 按以下顺序，将两个 Button 的 Name 和 Text 分别设置为 **connectDisconnectButton**、**viewEntriesButton**、**Connect-disconnect** 和 **View Entries**。
4. 将 ListBox 的 Name 设置为 **displayListBox**。窗体布局如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_359_0.png)

图 15.14。窗体布局

5. 双击 Connect-disconnect Button，创建其 Click 事件处理程序 `connectDisconnectButton_Click(...)`。在此方法中，我们将打开和关闭数据库连接，以便进行测试。首先，将以下命名空间引用代码行添加到 Form1.cs 顶部：

```csharp
using System.Data;
using System.Data.OleDb;
```

代码 15.1

我们将在 `connectDisconnectButton_Click(...)` 方法中创建一个 OleDbConnection 对象。OleDbConnection 对象使用以下构造函数模板创建：

```csharp
OleDbConnection myConn = new OleDbConnection(@connection string; Data Source= full path of the database file);
```

代码 15.2

临时存储在通过此 `readCommand` 对象创建的 OleDbDataReader 对象中：

```csharp
OleDbDataReader reader = readCommand.ExecuteReader();
```

代码 15.9

我们将在 ListBox 中显示读取到的数据。首先清空 ListBox：

```csharp
displayListBox.Items.Clear();
```

代码 15.10

然后使用 while 循环将读取到的数据插入 ListBox：

```csharp
while (reader.Read())
{
    displayListBox.Items.Add(reader["name_field"].ToString() + " - " + reader["surname_field"] + " - " + reader["age_field"]);
}
```

代码 15.11

只要 `reader` 对象中还有数据，while 循环就会继续运行，因此 Table1 中的所有数据都会显示在 ListBox 中。最后，不要忘记关闭连接：

```csharp
myConn.Close();
```

代码 15.12

下面给出了完整的 `viewEntriesButton_Click()` 方法：

```csharp
private void viewEntriesButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();
    OleDbCommand readCommand = new OleDbCommand("SELECT name_field, surname_field, age_field FROM Table1", myConn);
    OleDbDataReader reader = readCommand.ExecuteReader();
    displayListBox.Items.Clear();
    while (reader.Read())
    {
        displayListBox.Items.Add(reader["name_field"].ToString() + " - " + reader["surname_field"] + " - " + reader["age_field"]);
    }
    myConn.Close();
}
```

代码 15.13（续）

7. 生成并运行项目。此时将出现以下程序窗口：

![](img/41d82527c4e41cdb7e56259564306ddc_363_0.png)

图 15.15。程序窗口

首先，单击 Connect-disconnect Button。程序将显示与这些操作相关的消息框。如果程序出现错误，请仔细检查连接字符串，并确保数据库文件与可执行文件位于同一文件夹中。

![](img/41d82527c4e41cdb7e56259564306ddc_363_1.png)

图 15.16。打开数据库连接的消息

![](img/41d82527c4e41cdb7e56259564306ddc_364_0.png)

图 15.17。关闭数据库连接的消息

这些消息表明我们的连接对象已正确创建，即连接字符串正确，并且数据库文件位于正确的位置。现在，单击 View entries Button，从数据库中读取数据。ListBox 将显示我们在 firstDatabase.accdb 文件中输入的数据：

![](img/41d82527c4e41cdb7e56259564306ddc_364_1.png)

图 15.18。ListBox 中显示的数据库读取数据

我们可以在 Access 中更新、添加或删除数据库条目，然后再次单击 View entries Button，以显示更新后的数据。我向 Table1 中输入了新数据，并在 ListBox 中显示了更新后的数据，如图 15.19 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_365_0.png)

图 15.19。ListBox 中显示的更新后数据

## 15.3. 从 C# 程序添加、更新和删除数据库条目

我们已经在 Access 中操作了数据库中的数据，并在程序中显示了更新后的数据。问题在于，用户的计算机上可能没有安装 Access；或者，我们可能需要在程序中以系统化的方式操作数据库条目。使用 OleDbCommand 对象的相应命令，我们可以在自己的程序中添加新数据、删除条目或更新数据。下面开始开发示例项目，学习如何操作数据库条目。

1. 创建一个新的 C# 项目。
2. 按照图 15.20 所示的布局，在窗体上添加六个 TextBox、六个 Label、四个 Button 和一个 ListBox。
3. 从上到下，将 TextBox 的 Name 分别设置为 insertNameTextBox、insertSurnameTextBox、insertAgeTextBox、updateNameTextBox、updateSurnameTextBox 和 updateAgeTextBox（我知道，这些名称有点令人困惑！）。
4. 按顺序将 Button 的 Name 设置为 insertButton、updateButton、listButton 和 deleteButton。
5. 将 Button 的 Text 分别设置为 Insert、Update、List entries 和 Delete selected。
6. 将 Label 的 Text 分别设置为 Name:、Surname:、Age:、Name:、Surname: 和 Age:。
7. 最后，将 ListBox 的 Name 设置为 displayListBox。完成这些修改后，窗体将如图 15.21 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_366_0.png)

图 15.20。窗体布局

![](img/41d82527c4e41cdb7e56259564306ddc_366_1.png)

图 15.21。设置 Text 属性后的窗体

8. 将示例 Access 数据库文件 firstDatabase.accdb 复制到项目文件夹下的 `/bin/debug` 文件夹中。
9. 由于我们已经编写了在 ListBox 中显示数据的代码，因此可以借用前面示例中的代码来实现 List entries Button 的事件处理程序方法。双击 List entries Button，创建其事件处理程序方法。将代码 15.13 复制并粘贴到 `listButton_Click()` 中，以便在 ListBox 中显示数据库条目。不过，这里需要进行一处小修改。这次，除了 name 之外，我们还将显示 id_number，

