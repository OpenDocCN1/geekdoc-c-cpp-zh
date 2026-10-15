

如第 9 章所示，你使用共享的 Create 方法创建 XmlReader。该方法有多个重载版本。在本例中，使用 URL 的字符串版本来创建 XmlReader。代码随后遍历生成的 XML，直到找到 Latitude 元素的起始元素。正如你所知，这两个值彼此相邻；代码可以访问它们然后停止读取。图 12-26 显示了 SQL Server Management Studio 中这个新函数。

![](img/d99870e80390742f93963da7be0b2e61_494_0.png)

图 12-26

## 使用用户定义函数

即使 fnGetLocation 函数是用 Visual Basic 编写的，你仍然可以从 T-SQL 中使用此函数。这意味着对于给定的 SQL Server 对象，你可以使用 Visual Basic 或 T-SQL，视场景而定。以下代码显示了用于插入新商店的存储过程。该过程是用 T-SQL 编写的，但它调用了用 Visual Basic 编写的函数。或者，你也可以创建一个插入触发器来调用该函数以确定商店的位置。

```
CREATE PROCEDURE dbo.procInsertStore
(
    @name nvarchar(50),
    @street nvarchar(512),
    @city nvarchar(50),
    @state char(2),
    @zip varchar(50)
)
AS
    /* need to populate location */
    DECLARE @loc AS Location;
    SET @loc = dbo.fnGetLocation(@street, @city, @state, @zip);
    INSERT INTO Stores (Name, Street, City, State, Zip, GeoLocation)
        OUTPUT INSERTED.id
    VALUES (@name, @street, @city, @state, @zip, @loc);
    RETURN @@IDENTITY
```

来自 FooStore 的代码片段

存储过程使用函数和用户定义类型，就像使用用 T-SQL 编写的相同对象一样。在存储商店数据之前，它调用 Web 服务以确定位置的纬度和经度，然后将数据存储到表中。

我们现在准备向三个表添加数据。使用存储过程添加一些商店（见图 12-27）。实际数据并不重要，但拥有多个相对接近的商店在以后会很有用。

![](img/d99870e80390742f93963da7be0b2e61_495_0.png)

图 12-27

同样，向 Products 表添加一些项目（见图 12-28）。同样，数据本身并不重要，只要你有多种可供选择的商品即可。

![](img/d99870e80390742f93963da7be0b2e61_495_1.png)

图 12-28

最后，向 Stock 表添加数据（见图 12-29）。对每个商店和产品的组合使用一个条目。确保你有多种数量的库存以供测试。

![](img/d99870e80390742f93963da7be0b2e61_495_2.png)

图 12-29

现在我们有了一些数据可供使用，并且有一个用于确定任何地址的纬度和经度的函数，我们准备研究如何创建 Visual Basic 存储过程来查找距离客户最近且有库存的商店。

## 创建存储过程

与用户定义类型和函数一样，你使用属性将方法标识为存储过程。对于存储过程而言，这是 Microsoft.SqlServer.Server.SqlProcedureAttribute。该属性基本上是一个标记属性；没有额外的参数会对代码的行为产生显著影响。

在 Visual Basic 中创建存储过程时，你应牢记几点考虑。首先，也是最重要的一点，是上下文。你的代码不再作为独立应用程序运行，而是在 SQL Server 内部运行。需要长时间处理的任务意味着你使用的任何资源都将无法供其他代码使用，这可能导致数据库响应变慢，从而导致更多延迟。因此，始终要意识到你使用的资源以及锁定它们的时间。

在 Visual Basic 中创建存储过程时的第二个主要考虑因素是与数据的连接。在编写访问数据的独立 Visual Basic 代码时，你需要创建一个实现 IDbConnection 的类的连接，通常是 SqlConnection 或 OleDbConnection。然后使用的连接字符串标识数据库、用户 ID 等。然而，在存储过程中，你在 SQL Server 本身的上下文中运行，因此其中大部分信息是多余的，这使得连接到数据源变得更容易。

```
Using connection As New SqlConnection("context connection=true")
...work with the data here
End Using
```

连接字符串现在简化为相当于“代码正在运行的位置”。用户 ID、数据库和其他参数由代码运行的上下文隐含。

一旦你连接到数据库，其余代码基本上与你使用其他 ADO.NET 代码执行的操作相同。这意味着将访问 SQL Server 的代码迁移到作为存储过程运行是相当容易的：更改用于连接到数据库的连接字符串，并添加 SqlProcedure 属性。

## 从存储过程返回数据

一旦你执行了获取数据的必要操作，显然需要将其发送回用户。使用普通的 ADO.NET，你会创建一个 DataSet 或 SqlDataReader，并使用类的方法和属性来提取数据。然而，在存储过程中运行的数据访问代码在 SQL Server 的上下文中运行，并且存储过程必须像其他存储过程一样表现。此外，你的存储过程可能实际上是从 T-SQL 调用的，而 T-SQL 对 DataSet 或 IDataReader 数据类型一无所知。因此，你必须稍微更改代码以实现此行为。

使用 ADO.NET 返回数据时，你通常有几个选项。第一个选项取决于你需要返回单个值还是多行数据。

### 返回单个值

如果要从存储过程返回单个值，则将存储过程创建为子程序。你返回的数据应为子程序的 ByRef 参数。最后，你需要使用 System.Runtime.InteropServices.Out 属性将此参数标记为 out 参数。例如，如果你尝试创建一个返回所选商店所有可用商品总值的存储过程，则会创建类似于以下过程的内容：

```
Imports System
Imports System.Data
Imports System.Data.SqlClient
Imports System.Data.SqlTypes
Imports Microsoft.SqlServer.Server
Imports System.Runtime.InteropServices
Partial Public Class StoredProcedures
    <Microsoft.SqlServer.Server.SqlProcedure()>
    Public Shared Sub procGetStoreInventoryValue(ByVal storeID As Int32,
        <Out()> ByRef totalValue As SqlMoney)
        Dim query As String =
            "SELECT SUM(Products.Price * Stock.Quantity) as total " &
            "FROM Products INNER JOIN Stock ON " &
            "Products.id = Stock.ProductID " &
            "WHERE Stock.StoreID = @storeID"
        Using conn As New SqlConnection("context connection = true")
            Using cmd As New SqlCommand(query, conn)
                cmd.Parameters.Add("@storeID", SqlDbType.Int).Value = storeID
                totalValue = CType(cmd.ExecuteScalar(), SqlMoney)
            End Using
        End Using
    End Sub
End Class
```

> 由于此存储过程实际上不对数据进行任何处理或数学计算，因此最好使用 T-SQL 创建它。

该过程相当基础：它使用当前连接执行一段 SQL 并返回该 SQL 的值。如前所述，SqlConnection 和 SqlCommand 值是使用新的 Using 语句创建的。这确保了在代码块完成后它们会被释放，从而释放所使用的内存。

与在其他代码中处理 ByRef 参数时一样，在过程中对变量所做的任何更改都会反映在方法外部。Out 属性扩展了这一点，以标识参数为需要从应用程序中封送出来的值。它是改变 ByRef 变量行为所必需的。通常，ByRef 变量是 In/Out 值。你必须至少在调用时使其可用。通过使用 Out 属性标记它，你将其标记为不需要此要求。

### 返回多个值

如果要返回一行或多行数据，事情会变得稍微复杂一些。从某种意义上说，你的代码需要复制在 SQL Server 中执行存储过程时通常发生的数据传输。数据必须以某种方式传输到 TDS（Tabular Data Stream）。如何创建此 TDS？幸运的是，SQL Server 为你提供了一种方法，通过 SqlPipe 类。SqlContext 类通过其 Pipe 属性提供对 SqlPipe 类的访问。如表 12-7 所示，SqlPipe 类有几个方法可用于将数据返回给调用存储过程的代码：

**表 12-7：用于返回数据的 SqlPipe 类方法**

| 方法 | 描述 |
| --- | --- |
| ExecuteAndSend | 接受 SqlCommand，执行它并返回结果。这是返回数据时可使用的最高效方法，因为它不需要生成任何内存结构。 |
| Send(SqlDataReader) | 接受 SqlDataReader 并将结果数据流式传输到客户端。这比前一种方法稍慢，但在需要对数据进行处理后再返回时推荐使用。 |
| Send(SqlDataRecord) | 向客户端返回一行数据。如果你在生成数据并且只需要发送一行时，此方法很有用。 |
| Send(String) | 向客户端返回一条消息。这与标量字符串值不同。然而，这旨在向客户端发送信息性消息。发送回的信息可使用 SqlConnection 的 InfoMessage 事件检索。 |
| SendResultsStart | 用于标记多行数据块的开始。此方法接受一个 SqlDataRecord，用于标识随后续 SendResultsRow 调用一起发送的列。此方法在必须在返回给客户端之前构造多行数据时最有用。 |
| SendResultsRow | 用于将 SqlDataRecord 发送回客户端。你必须先使用匹配的 SqlDataRecord 调用 SendResultsStart；否则，将发生异常。 |
| SendResultsEnd | 标记多行数据块传输的结束。这只能在先调用 SendResultsStart 并且可能调用一个或多个 SendResultsRow 之后调用。如果你未能调用此方法，则任何其他尝试使用 SqlPipe 的操作都会导致异常。 |

如果你只想执行一段 SQL 并返回结果数据，则使用 ExecuteAndSend 方法。实际上，在这种情况下，你最好使用 T-SQL，但可能存在证明在 Visual Basic 中执行此操作的理由。此方法避免了创建任何

