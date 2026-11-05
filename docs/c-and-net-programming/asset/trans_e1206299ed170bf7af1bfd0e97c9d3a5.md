
不应抛出任何异常的代码块。不要捕获无法处理的异常，并避免不必要地重新抛出异常，因为这样做的开销很大。

## 防止不必要的数据库访问

ADO.NET 所有特性中最有用的特性之一是，可以将消息附加到 `DataSet` 对象中每一行数据上。如果某个特定数据库操作未成功完成，`SqlDataAdapter` 类会将错误消息附加到 `DataSet` 的行上。然后，可以使用 `DataSet` 实例的 `HasErrors` 属性，在将 `DataSet` 发送去更新数据库之前检查其中是否有任何错误。如果使用得当，这可以防止不必要的数据库访问。请参考下面的代码片段，

```
DataSet newDataSet = previousDataSet.GetChanges(DataRowState.Modified);
if (newDataSet.HasErrors)
{
    // If there are errors take appropriate action
}
else
{
    // Necessary code to update the database
}
```

## 16.8 ADO.NET 中的事务

事务是一个单一工作单元，意味着要么全部完成，要么全部不完成。如果事务成功，所有数据操作都会被提交（保存），并成为数据库中持久的一部分。如果事务遇到错误/异常而必须取消或回滚，则需要移除所有数据修改/操作。

数据库事务将数据库从一个一致状态带到另一个一致状态。在事务结束时，如果事务失败，系统必须处于先前状态；如果事务成功完成，则系统状态应反映成功完成的结果。

### 16.8.1 事务的属性

### 原子性

一个事务由许多步骤组成。当事务中的所有步骤都完成时，它将在数据库中体现；或者如果任何步骤失败，则所有事务都会回滚。

### 一致性

如果事务成功，数据库将从一个一致状态转移到另一个一致状态；如果事务失败，则数据库保持原始状态。

### 隔离性

每个事务在运行时都应像系统中唯一的事务一样。

### 持久性

一旦事务成功完成，更新后的行/记录必须永久可供所有其他事务使用。

## 16.8.2 事务命令

事务命令仅用于 SQL DML（数据操作语言）中，DML 包含 INSERT、UPDATE 和 DELETE 等操作。也就是说，它们会更改数据。DDL（数据定义语言）或 DCL（数据控制语言）用于创建结构和 SQL 安全性。

事务命令如下，

- **COMMIT**
  此命令用于保存事务调用的更改。
- **ROLLBACK**
  此命令用于撤销事务所做的更改。
- **SAVEPOINT**
  借助此命令，可以将事务回滚到某个点，而无需回滚整个事务。
- **SET TRANSACTION**
  此命令用于指定事务的特性。例如，可以将事务指定为只读或读写。它还有助于设置事务名称。

## 16.8.3 使用 ADO.NET 的事务

//用于说明 ADO.NET 中使用的 SQL 事务的示例。
示例

```csharp
string strConnString = "connectionstring"; // can be taken from Web.config file
SqlTransaction objTrans = null;
using (SqlConnection objConn = new SqlConnection(strConnString))
{
    objConn.Open();
    objTrans = objConn.BeginTransaction();
    SqlCommand objCmd1 = new SqlCommand("insert into tblAuthor values(12, 'Ravi')", objConn);
    SqlCommand objCmd2 = new SqlCommand("insert into tblTechMember(MemberID, TaskID) values(5, 15)", objConn);
    try
    {
        objCmd1.ExecuteNonQuery();
        objCmd2.ExecuteNonQuery(); // Throws exception due to foreign key constraint

        objTrans.Commit();
    }
    catch (Exception)
    {
        objTrans.Rollback();
    }
    finally
    {
        objConn.Close();
    }
}
```

如上述程序所示，首先打开与 SQL 数据库的连接，然后实例化 `SqlTransaction` 类的对象。此外，通过调用 SQL Begin Transaction 方法，将 `SqlTransaction` 的引用保留在此事务对象中。在 `try` 块中执行两个 SQL 命令。如果未发生错误，则提交事务；否则 `catch` 块回滚事务。最后，关闭数据库连接。

## 16.8.4 TransactionScope 类

`TransactionScope` 随 .NET 2.0 作为 `System.Transaction` 的一部分引入。它是一个类，提供了一种简单的方法，将一组操作作为事务的一部分，而无需担心背后的复杂性。如果其中任何操作失败，整个事务都会失败并回滚，从而撤销所有已完成的操作。所有这些都由框架处理，以确保数据一致性。

它可以在程序中如下所示使用，

```csharp
try
{
    using (TransactionScope scope = new TransactionScope())
    {
        // Do Operation 1
        // Do Operation 2
        //...

        // if all the operations complete successfully, this would be called
        // and commit the transaction.
        // In case of an exception, it won't be called and transaction is
        // rolled back
        scope.Complete();
    }
}
catch (ThreadAbortException ex)
{
    // Handle exception
}
```

使用 `TransactionScope` 时，它会使代码块进入事务模式。它不能被继承。它位于 `System.Transactions` 命名空间中。

`TransactionScope` 有 3 个主要属性（`IsolationLevel`）。

- **隔离级别**
  它定义在另一个事务中读取数据时的锁定机制。可用选项包括 Read UnCommitted、Read Committed、Repeatable Read、Serializable。默认值为 Serializable。
- **超时**
  事务对象等待完成的时间。`SqlCommand Timeout` 与 `Transaction Timeout` 不同。`SqlCommand Timeout` 定义 `SqlCommand` 对象等待数据库操作完成的时间。可用选项为 10 分钟。默认值为 1 分钟。
- **TransactionScopeOption**
  它是一个枚举。以下是可选项。

| 选项 | 描述 |
|---|---|
| Disable | 此组件不参与事务。这是默认值。 |
| NotSupported | 此组件在事务上下文之外运行。 |
| Required | 它是 TransactionScope 的默认值。如果已经存在事务，则加入该事务；否则创建新事务。 |
| RequiresNew | 选择此选项时，始终会创建新事务。此事务与其外部事务相互独立。 |
| Suppress | 选择此选项时，不会创建任何事务。即使已经存在事务也是如此。 |

### 设置默认值

超时的默认值可以在 web.config 中设置，

```xml
<system.transactions>
<defaultSettings timeout="30"/>
<machineSettings maxTimeout="1200"/>
</system.transactions>
```

### 说明 TransactionScope 类用法的示例

// 创建一个 TransactionScope 类对象，并定义 SQL 查询以向 Author 表、TaskMember 表添加记录。如果没有错误，则调用 Complete() 提交数据。如果引发异常，则回滚到之前的状态。

```csharp
using (var txscope = new TransactionScope(TransactionScopeOption.RequiresNew))
{
    try
    {
        using (SqlConnection objConn = new SqlConnection(strConnString))
        {
            objConn.Open();
            SqlCommand objCmd1 = new SqlCommand("insert into tblAuthor values(12, 'Ravi')", objConn);
            SqlCommand objCmd2 = new SqlCommand("insert into tblTaskMember(MemberID, TaskID) values(12, 18)", objConn);
            objCmd1.ExecuteNonQuery();
            objCmd2.ExecuteNonQuery(); // Throws exception due to foreign key constraint
            //The Transaction will be completed
            txscope.Complete();
        }
    }
    catch(Exception ex)
    {
        // Log error
        txscope.Dispose();
    }
}
```

## 16.8.5 TransactionScope 类与 BeginTransaction() 方法的区别

- TransactionScope 通常是更好的选择，因为它允许嵌套调用其他可能需要事务的方法，而无需传递事务状态。
- 使用 TransactionScope 时，只要作用域存在，它就会处理在线程上向当前 Transaction 注册的所有内容，使代码更清晰、更易维护。

