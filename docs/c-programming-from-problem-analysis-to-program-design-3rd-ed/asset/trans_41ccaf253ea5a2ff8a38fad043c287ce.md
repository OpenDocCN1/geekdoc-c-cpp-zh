
```
{
    return phoneNumber;
}
}

public override string ToString( )
{
    return firstName + " " + lastName;
}
}
}
```

最后一点要添加到访问数据库的类的程序语句中：你应该在退出应用程序之前始终关闭连接。

## 关闭连接

这是最容易做到的事情之一，但常常被忽视。你需要关闭读取器对象和连接对象。通过这样做，你可以解锁数据库，以便其他应用程序可以访问它。示例14–12包含了调用`Close( )`方法以关闭之前示例中实例化的连接和数据读取器对象。

### 示例14–12

```csharp
dbReader.Close( );
dbConn.Close( );
```

当你尝试关闭连接以及尝试访问数据时，都可能会抛出异常。你也可以将关闭连接的语句放在`try...catch`块中，以便在出现问题时提醒用户，从而采取纠正措施。

![](img/e33ae760e23d89eac66541252ad65de8_878_0.png)

可以添加一个特殊的`using`语句来包围访问数据库的整个代码块。添加该语句后，就不再需要调用`Close( )`方法了。当`using`块（由花括号包围）中包含的语句超出作用域时，所有对象都会被释放。

示例14–13汇集了示例14–1、14–3、14–11和14–12中的语句，并将它们封装在一个`try...catch`块中。为简洁起见，列表中没有包含部分Windows窗体设计器生成的代码。该应用程序包含一个用于数据展示的`Listbox`对象和一个用于显示错误信息的`Label`对象。该标签最初设置为`null`值。

### 示例14-13

```csharp
// DBExample.cs
// A Windows application is used as the
// front end to display records retrieved
// from an Access database.
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.Data.OleDb;

namespace DBExample
{
    public class DbGUI : System.Windows.Forms.Form
    {
        private System.Windows.Forms.ListBox listBox1;
        private System.Windows.Forms.Label label2;
        private System.Windows.Forms.Label lblErrorMsg;
        private System.Windows.Forms.Button btnLoad;
        private System.ComponentModel.Container components = null;
        private OleDbConnection dbConn;   // Connection object
        private OleDbCommand dbCmd;       // Command object
        private OleDbDataReader dbReader; // Data Reader object
        private Member aMember;
        private string sConnection;
        private string sql;

        public DbGUI()
        {
            InitializeComponent();
        }

        // Dispose( ) method removed from listing

        #region Windows Forms Designer generated code
        // Note: Windows Generated Code
        // removed - Due to space constraints
        #endregion

        static void Main()
        {
            Application.Run(new DbGUI());
        }

private void btnLoad_Click(object sender,
                         System.EventArgs e)
{
    try
    {
        // Construct an object of the OleDbConnection
        // class to store the connection string
        // representing the type of data provider
        // (database) and the source (actual db).
        sConnection =
            "Provider=Microsoft.ACE.OLEDB.12.0;" +
            "Data Source=member.accdb";
        dbConn = new OleDbConnection(sConnection);
        dbConn.Open();

        // Construct an object of the OleDbCommand
        // class to hold the SQL query. Tie the
        // OleDbCommand object to the OleDbConnection
        // object.
        sql = "SELECT * FROM memberTable ORDER " +
              "BY LastName ASC, FirstName ASC";
        dbCmd = new OleDbCommand();
        dbCmd.CommandText = sql;
        dbCmd.Connection = dbConn;

        // Create a dbReader object.
        dbReader = dbCmd.ExecuteReader();

        while (dbReader.Read())
        {
            aMember = new Member
                      (dbReader["FirstName"].ToString(),
                       dbReader["LastName"].ToString());
            this.listBox1.Items.Add(aMember);
        }
        dbReader.Close();
        dbConn.Close();
    }
    catch (System.Exception exc)
    {
        this.lblErrorMsg.Text = exc.Message;
    }
}
```

![](img/e33ae760e23d89eac66541252ad65de8_880_0.png)

特别提示：如果你不在Member类中重写ToString( )方法，那么当你将该类的对象添加到列表框中时，你将会得到一个充满成员类型名称的列表框。

示例14-13程序清单（使用了`Member`类，见示例14-11）生成的输出如图14-2所示。请记住，该数据库此前已在图14-1中显示。

![](img/e33ae760e23d89eac66541252ad65de8_881_0.png)

图14-2  使用数据库读取器对象访问member.accdb数据库

数据读取器类支持对数据库的只读访问。有些情况需要你更改或更新数据库中的数据。这可以通过多种方式完成。你可以编写包含INSERT、DELETE和UPDATE语句的SQL语句，然后通过调用OleDbCommand.ExecuteNonQuery()方法来执行这些查询。另一种更简单的方法是实例化数据集和数据适配器类的对象。你可以使用数据适配器对象来填充数据集对象。数据适配器类具有Fill()和Update()等方法，可以省去编写SQL更新语句的需要。接下来的章节将解释如何实现这一点。

## 更新数据库数据

ADO.NET并不要求你始终保持与数据库的持续实时连接，并一次处理一条检索到的记录。还有其他类可用，使你能够连接到数据库足够长的时间，将记录检索到内存中。然后可以更改数据，并重新连接到数据库以更新数据。这可以提高应用程序的性能，并允许其他应用程序在你以断开模式工作时访问数据库。当你这样做时，你会在内存中创建从数据库检索到的记录的临时副本，然后处理临时数据，而不是数据库中存储的实时数据。在.NET中，这是通过数据集实现的。数据集是从某个数据源检索到的记录的缓存，可能包含来自该数据源的多个表。数据集与实际数据库之间的交互通过数据适配器进行控制。

## 使用数据集处理数据库记录

与数据读取器对象一样，根据你所访问的数据库类型，你会在每个不同的数据提供程序命名空间中使用不同的数据集和数据适配器类。对于Access数据库提供程序类，你仍然需要添加：`using System.Data.OleDb;`

直到处理从SQL查询检索到的数据为止，你都需要包含与使用数据库读取器对象时相同的程序语句。你仍然需要使用OleDb数据提供程序的连接字符串来实例化连接对象，并且仍然指定数据库名称。你将在本章后面的章节中了解这一点，但当你使用数据适配器对象时，无需使用连接对象调用Open( )方法。这会自动为你处理。

你仍然通过执行SQL SELECT语句从数据库中选择记录（和字段）。正如你在示例14–13中看到的，SQL语句被打包在数据命令对象中。因此，你仍然需要实例化OleDbCommand类的对象，并将该类的CommandText属性设置为该SQL字符串。示例14–13中的这些语句在示例14–14中为你重复。到目前为止，使用数据库读取器类与使用数据集和数据适配器类之间的唯一区别是省略了dbConn.Open( )。连接对象和命令对象是必需的。

### 示例14-14

```csharp
private OleDbConnection  dbConn;
private OleDbCommand      dbCmd;
private string     sConnection;
private string     sql;
                 :    // Colon indicates items missing
// Construct an object of the OleDbConnection
// class to store the connection string
// representing the type of data provider
// (database) and the source (actual db).
sConnection =
        "Provider=Microsoft.ACE.OLEDB.12.0;" +
        "Data Source=member.accdb";
dbConn = new OleDbConnection(sConnection);

// Construct an object of the OleDbCommand
// class to hold the SQL query. Tie the
// OleDbCommand object to the OleDbConnection
// object.
sql = "SELECT * FROM memberTable ORDER " +
      "BY LastName ASC, FirstName ASC;";
dbCmd = new OleDbCommand();
dbCmd.CommandText = sql;
dbCmd.Connection = dbConn;
```

