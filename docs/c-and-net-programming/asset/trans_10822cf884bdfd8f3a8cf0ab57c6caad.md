

## DataReader 方法

| 方法 | 描述 |
|---|---|
| Close | 关闭 DataReader 对象。 |
| Read | 读取数据读取器中的下一条记录。 |
| NextResult | 在批量事务期间将数据读取器推进到下一个结果。 |
| Getxxx | 有几十个 Getxxx 方法。这些方法从列中读取特定数据类型的值。例如，GetChar 将列值作为字符返回，GetString 作为字符串返回。 |

## 创建 SqlDataReader 对象

实例化 SqlDataReader 与实例化其他 ADO.NET 对象不同。

首先，在命令对象上调用 ExecuteReader：

```csharp
SqlDataReader sqldr = sqlcmd.ExecuteReader();
```

SqlCommand 对象 sqlcmd 的 ExecuteReader 方法返回一个 SqlDataReader 实例。使用 new 运算符创建 SqlDataReader 不足以完成任何操作，因为 SqlCommand 对象引用连接，并且 SQL 语句是 SqlDataReader 获取数据所必需的。

## 读取数据

SqlDataReader 通过顺序流返回数据。要读取这些数据，需从表中逐行获取数据。一旦读取了一行，上一行就不再可用。要再次读取该行，必须创建 SqlDataReader 的新实例并再次读取数据流。

从 SqlDataReader 返回的数据流中读取的典型方法是使用 while 循环遍历每一行。

```csharp
while (sqldr.Read())
{
    // get the results of each column
    string contact = (string)sqldr["AuthorContactName"];
    string publication = (string)sqldr["AuthorPublicationName"];
    string city = (string)sqldr["AuthorCity"];

    // print results
    Console.Write("{0,35}", contact);
    Console.Write("{0,30}", city);
    Console.Write("{0,35}", publication);
}
```

*Read* 的返回值是 bool 类型，只要还有更多记录可读就返回 true。读取完数据流中的最后一条记录后，*Read* 返回 false。

可以使用数字索引器从行中提取每一列。也可以使用字符串索引器代替数字索引器，其中字符串是 SQL 查询中的列名（如果使用星号 \*，则使用表列名）。字符串索引器可读性高得多，使代码更易于维护。

无论索引器参数的类型如何，SqlDataReader 索引器都将返回 object 类型。

### 关闭连接

使用完 SqlDataReader 后，请关闭 SqlConnection。

```csharp
try
{
    // data access code
}
finally
{
    // 3. close the reader
    if (sqldr != null)
    {
        sqldr.Close();
    }

    // close the connection too
}
```

### 示例

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ADONetDemos
{
    class ReadersDemo
    {
        static void Main()
        {
            ReadersDemo rsd = new ReadersDemo();
            rsd.DataRead();
        }

        public void DataRead()
        {
            // declare the SqlDataReader
            SqlDataReader sqldr = null;

            // create a connection object
            SqlConnection sqlconn = new SqlConnection(
                "Data Source=(local);Initial Catalog=Northwind;Integrated Security=SSPI");

            // create a command object
            SqlCommand sqlcmd = new SqlCommand(
                "select * from Books", sqlconn);

            try
            {
                // open the connection
                sqlconn.Open();

                // 1. get an instance of the SqlDataReader
                sqldr = sqlcmd.ExecuteReader();

                // print column headers
                Console.WriteLine("Author Contact Name  Author City  Publication Name");

                // 2. print necessary columns of each record
                while (sqldr.Read())
                {
                    // get the results of each column
                    string contact = (string)sqldr["AuthorContactName"];
                    string publication = (string)sqldr["Publication"];
                    string city = (string)sqldr["AuthorCity"];

                    // print results
                    Console.Write("{0,-35}", contact);
                    Console.Write("{0,-30}", city);
                    Console.Write("{0,-35}", publication);
                }
            }
            finally
            {
                // 3. close the reader
                if (sqldr != null)
                {
                    sqldr.Close();
                }

                // close the connection
                if (sqlconn != null)
                {
                    sqlconn.Close();
                }
            }
        }
    }
}
```

## 5. 使用 SqlDataAdapter

- DataSet 是内存中的数据存储，可容纳许多表。DataSet 只保存数据，不与数据源交互。SqlDataAdapter 管理与数据源的连接，并提供断开连接的行为。SqlDataAdapter 仅在需要时打开连接，并在完成任务后立即关闭连接。

- SqlDataAdapter 在用数据填充 DataSet 时执行以下任务：
    1. 打开连接
    2. 将数据检索到 DataSet
    3. 关闭连接

  当 DataSet 更改后更新数据源时，它执行以下操作：
    1. 打开连接
    2. 将 DataSet 中的更改写入数据源
    3. 关闭连接

在 Fill 和 Update 操作之间，数据源连接是关闭的。可以使用 DataSet 读取和写入数据。由于应用程序仅在必要时保持连接，因此应用程序的可伸缩性更高。

### 创建 DataSet 对象

```csharp
DataSet dsBooks = new DataSet();
```

现在，DataSet 为空，需要一个 SqlDataAdapter 来加载它。

### 创建 SqlDataAdapter

1. SqlDataAdapter 保存用于读取和写入数据的 SQL 命令和连接对象。它使用 SQL select 语句和连接对象进行初始化：

    ```csharp
    SqlDataAdapter daBooks = new SqlDataAdapter("select BookID,Author from Books", sqlconn);
    ```

2. 上面的代码创建了一个新的 SqlDataAdapter，名为 daBooks。SQL select 语句指定将哪些数据读入 DataSet。连接对象 sqlconn 应该已经实例化，但尚未打开。SqlDataAdapter 负责在调用 Fill 和 Update 方法期间打开和关闭连接。

3. SqlDataAdapter 包含与数据源交互所需的所有命令。有两种方法可以添加插入、更新和删除命令：通过 SqlDataAdapter 属性或使用 SqlCommandBuilder。

    ```csharp
    // Using SqlCommandBuilder
    SqlCommandBuilder cmdBldr = new SqlCommandBuilder(daBooks);
    ```

4. SqlCommandBuilder 使用 SqlDataAdapter 实例 daBooks 的单个构造函数参数进行实例化。这告诉 SqlCommandBuilder 要向哪个 SqlDataAdapter 添加命令。SqlCommandBuilder 将读取 SQL select 语句（在实例化 SqlDataAdapter 时指定），推断插入、更新和删除命令，并将新命令分别分配给 SqlDataAdapter 的 Insert、Update 和 Delete 属性。

请注意，SqlCommandBuilder 适用于单个表，而不适用于多表联接。

## 填充 DataSet

```csharp
daBooks.Fill(dsBooks, "Books");
```

上面代码中的 Fill 方法接受两个参数：一个 DataSet 和一个表名。在尝试用数据填充 DataSet 之前，必须先将其实例化。第二个参数是将在 DataSet 中创建的表的名称。

Fill 方法有一个重载，仅接受一个 DataSet 参数。在这种情况下，创建的第一个表默认名称为 "table1"。对于添加到 DataSet 中且未在 Fill 方法中指定表名的每个表，编号将递增（table2、table3、...、tableN）。

## 使用 DataSet

DataSet 可同时绑定到 ASP.NET 和 Windows Forms DataGrid。

```csharp
// Illustration of a DataSet assigned to a Windows Forms DataGrid
dgBooks.DataSource = dsBooks;
dgBooks.DataMember = "Books";
```

DataSet 被分配给 DataGrid 的 DataSource 属性。

要准确指定要使用哪个表，请将 DataGrid 的 DataMember 属性设置为该表的名称。

## 更新更改

对数据做出修改后，如果要将其更新到实际数据库，则使用 SqlDataAdapter 的 Update 方法将修改应用到数据库。

```csharp
daBooks.Update(dsBooks, "Books");
```

上面的 Update 方法是在最初填充 dsBooks DataSet 的 SqlDataAdapter 实例上调用的。Update 方法的第二个参数指定哪个表，来自

