

下一阶段是创建 **UpdateDataSet** 方法将用于更新数据库中目标表的命令。代码声明三个合适的 SQL 语句，然后构建命令并向其添加所需的参数。请注意，每个参数可能应用于目标表中的多行，因此实际值必须根据当前正在将其更新应用到目标表的 **DataSet** 行的内容动态设置。

这意味着，除了参数名称和数据类型外，您还必须指定 **DataSet** 中行的名称和版本（**Current** 或 **Original**），以从中获取值。对于 **INSERT** 命令，您需要包含新值的行的当前版本。对于 **DELETE** 命令，您需要 ID 的原始值以定位表中将被删除的行。对于 **UPDATE** 命令，您需要 ID 的原始值以定位表中将被更新的行，以及用于更新目标表行中其余列的值的当前版本。

```vb
Dim addSQL As String
    = "INSERT INTO Products (Name, Description) VALUES (@name, @description);"
Dim updateSQL As String = "UPDATE Products SET Name = @name, "
    & "Description = @description WHERE Id = @id"
Dim deleteSQL As String = "DELETE FROM Products WHERE Id = @id"

' Create the commands to update the original table in the database
Dim insertCommand As DbCommand = defaultDB.GetSqlStringCommand(addSQL)
defaultDB.AddInParameter(insertCommand, "name", DbType.String, "Name", _
    DataRowVersion.Current)
defaultDB.AddInParameter(insertCommand, "description", DbType.String, _
    "Description", DataRowVersion.Current)

Dim updateCommand As DbCommand = defaultDB.GetSqlStringCommand(updateSQL)
defaultDB.AddInParameter(updateCommand, "name", DbType.String, "Name", _
    DataRowVersion.Current)
defaultDB.AddInParameter(updateCommand, "description", DbType.String, _
    "Description", DataRowVersion.Current)
defaultDB.AddInParameter(updateCommand, "id", DbType.String, "Id", _
    DataRowVersion.Original)

Dim deleteCommand As DbCommand = defaultDB.GetSqlStringCommand(deleteSQL)
defaultDB.AddInParameter(deleteCommand, "id", DbType.Int32, "Id", _
    DataRowVersion.Current)
```

最后，您可以通过调用 **UpdateDataSet** 方法来应用更改，如下所示。

```vb
' Apply the updates in the DataSet to the original table in the database.
Dim rowsAffected As Integer = defaultDB.UpdateDataSet(loaddbDS, "Products", _
InsertCommand, updateCommand, deleteCommand, _
UpdateBehavior.Standard)
Console.WriteLine("Updated a total of {0} rows in the database.", rowsAffected)
```

已在数据库中更新总共 3 行。

## 管理连接

多年来，开发者一直为如何在数据访问代码中以理想方式管理连接而烦恼。连接资源稀缺，在资源使用方面成本高昂，如果管理不当，还会造成巨大的性能损失。显然，在访问数据之前必须打开连接，并且在使用完毕后应确保将其关闭。但是，如果操作系统每次都实际创建一个新连接，然后关闭并销毁它，那么应用程序的执行将会像糖浆一样缓慢。

相反，ADO.NET 维护一个打开的连接池，并将其分配给需要它们的应用程序。数据访问代码仍然需要调用创建、打开和关闭连接的方法，但 ADO.NET 在可能时会自动从连接池中检索连接，并决定何时以及是否实际关闭底层连接并将其释放。主要问题在于您需要决定代码何时以及如何调用 Close 方法。数据访问块通过尽可能自动管理连接来帮助解决这些问题。

使用数据访问块检索 DataSet 时，ExecuteDataSet 方法会自动打开和关闭到数据库的连接。如果发生错误，它将确保连接已关闭。如果您想保持连接打开（例如，要通过该连接执行多个操作），可以访问 DbCommand 对象的 Active Connection 属性，并在调用 ExecuteDataSet 方法之前将其打开。ExecuteDataSet 方法在完成时会保持连接打开，因此您必须确保代码之后将其关闭。

相比之下，当检索 DataReader 或 XmlReader 时，ExecuteReader 方法（对于 XmlReader 则是 ExecuteXmlReader 方法）必须保持连接打开，以便您可以读取数据。ExecuteReader 方法将读取器的 CommandBehavior 属性设置为 CloseConnection，以便在释放读取器时关闭连接。通常，您将使用 Using 构造来确保释放读取器，如下所示：

```vb
Using reader As IDataReader = db.ExecuteReader(cmd)
' use the reader here
End Using
```

此代码以及本节后面的代码假设您已创建名为 db 的数据访问块 Database 实例和名为 cmd 的 DbCommand 实例。

通常，使用 ExecuteXmlReader 方法时，您会在释放读取器后显式关闭连接。这是因为底层 XmlReader 类不公开 CommandBehavior 属性。但是，您仍应使用与 DataReader 相同的方法（Using 语句）来确保 XmlReader 正确关闭和释放。

```vb
Using reader As XmlReader = db.ExecuteXmlReader(cmd)
 ' use the reader here
End Using
```

最后，如果您想能够访问代码正在使用的连接（例如，要在代码中创建基于连接的事务），可以使用数据访问块方法为数据访问方法显式创建一个连接。这意味着您必须自己管理连接，通常通过下面所示的 Using 语句，该语句会自动关闭和释放连接：

```vb
Using con As DbConnection = defaultDB.CreateConnection()
con.Open()
Try
 ' perform data access here
Catch
 ' handle any errors here
End Try
End Using
```

## 使用基于连接的事务

许多应用程序的常见需求是以这种方式对数据执行多个更新：要么全部成功，要么全部撤销（回滚），以使数据库处于与原始内容一致的有效状态。传统示例是银行执行货币交易，需要从一个账户扣除一笔付款，并将相同金额添加到另一个账户（或者稍微少一点，佣金进入银行自己的账户）。

事务应遵循四个 ACID 原则。这些原则是：原子性（事务的所有任务要么全部执行，要么都不执行）、一致性（数据库在事务前后都保持一致状态）、隔离性（其他操作在事务期间无法访问或查看中间状态的数据）、持久性（成功事务的结果会被持久化，并能够经受住系统故障）。

当所有更新都在单个数据库中发生时，可以通过使用数据库系统的功能（例如在存储过程中包含 BEGIN TRANSACTION 和 ROLLBACK TRANSACTION 等相关命令）来执行事务。ADO.NET 还提供功能，允许您在单个连接上执行基于连接的事务。这使您可以对同一数据库中的不同表执行多个操作，并在数据访问代码中管理提交或回滚。

数据访问块中所有检索或更新数据的方法都有重载，接受对现有事务的引用作为 DbTransaction 类型。作为其用法示例，以下代码在连接上显式创建一个事务。它假设您已创建名为 db 的数据访问块 Database 实例和两个名为 cmdA 和 cmdB 的 DbCommand 实例。

```vb
Using conn As DbConnection = db.CreateConnection()
conn.Open()
Dim trans As DbTransaction = conn.BeginTransaction()
Try
    ' execute commands, passing in the current transaction to each one
    db.ExecuteNonQuery(cmdA, trans)
    db.ExecuteNonQuery(cmdB, trans)
    trans.Commit() ' commit the transaction
Catch
    trans.Rollback() ' rollback the transaction
End Try
End Using
```

本章的示例包括一个名为“使用基于连接的事务”的示例，演示了上述方法。它首先显示 Products 表中两行的值，然后在基于连接的事务上下文中两次使用 ExecuteNonQuery 方法来更新数据库中两行的 Description 列。在此过程中，它会显示这些行的新描述。最后，它回滚事务，恢复原始值，然后显示这些值以证明其有效。

更新前的行内容：

```text
Id = 53
Name = Half-Finger Gloves, L
Description = Full padding, improved finger flex, durable palm, adjustable closure.

Id = 84
Name = Hitch Rack - 4-Bike
Description = Carries 4 bikes securely; steel construction, fits 2" receiver hitch.
--------------------------------------------------------------------------------
Updated row with ID = 53 to 'Third and little fingers tend to get cold.'.
Updated row with ID = 84 to 'Bikes tend to fall off after a few miles.'.
--------------------------------------------------------------------------------
```

