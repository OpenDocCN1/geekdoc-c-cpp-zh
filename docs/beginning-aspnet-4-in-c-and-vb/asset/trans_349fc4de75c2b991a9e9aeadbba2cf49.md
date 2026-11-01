
（续）

| 事务类成员 | 描述 |
|---|---|
| DependentClone() | 使用 DependentClone() 方法，您可以创建一个依赖于当前事务的事务。 |
| TransactionCompleted | TransactionCompleted 是一个事件，当事务完成（无论成功还是失败）时会触发该事件。通过类型为 TransactionCompletedEventHandler 的事件处理程序对象，您可以访问 Transaction 对象并读取其状态。 |

为了演示 System.Transactions 的特性，独立程序集中的 Utilities 类提供了一些静态方法。AbortTx() 方法根据用户的输入返回 true 或 false。DisplayTransactionInformation() 方法接受一个 TransactionInformation 对象作为参数，并显示事务中的所有信息：创建时间、状态、本地标识符和分布式标识符：

```
public static class Utilities
{
    public static bool AbortTx()
    {
        Console.Write("Abort the Transaction (y/n)?");
        return Console.ReadLine() == "y";
    }

    public static void DisplayTransactionInformation(string title,
        TransactionInformation ti)
    {
        if (ti != null)
        {
            Console.WriteLine(title);
            Console.WriteLine("Creation Time: {0}", ti.CreationTime);
            Console.WriteLine("Status: {0}", ti.Status);
            Console.WriteLine("Local ID: {0}", ti.LocalIdentifier);
            Console.WriteLine("Distributed ID: {0}", ti.DistributedIdentifier);
            Console.WriteLine();
        }
    }
}
```

代码片段 Utilities/Utilities.cs

## 可提交事务

Transaction 类无法通过编程方式提交；它没有提交事务的方法。基类 Transaction 仅支持中止事务。唯一支持提交的事务类是 CommittableTransaction 类。

使用 ADO.NET，可以将事务登记到连接中。为此，在 StudentData 类中添加了一个 AddStudent() 方法，该方法接受一个 System.Transactions.Transaction 对象作为第二个参数。通过调用 SqlConnection 类的 EnlistTransaction 方法，将对象 tx 登记到连接中。这样，ADO.NET 连接就与事务关联起来：

```
public void AddStudent(Student student, Transaction tx)
{
    var connection = new SqlConnection(
        Properties.Settings.Default.CourseManagementConnectionString);
    connection.Open();
    try
    {
        if (tx != null)
            connection.EnlistTransaction(tx);
        SqlCommand command = connection.CreateCommand();
        command.CommandText = 'INSERT INTO Students (FirstName, ' +
            'LastName, Company)' +
            'VALUES (@FirstName, @LastName, @Company)';
        command.Parameters.AddWithValue("@FirstName", student.FirstName);
        command.Parameters.AddWithValue("@LastName", student.LastName);
        command.Parameters.AddWithValue("@Company", student.Company);
        command.ExecuteNonQuery();
    }
    finally
    {
        connection.Close();
    }
}
```

代码片段 DataLib/StudentData.cs

在控制台应用程序 TransactionSamples 的 CommittableTransaction() 方法中，首先创建一个 CommittableTransaction 类型的事务，并在控制台上显示信息。然后创建一个 Student 对象，并通过 AddStudent() 方法将该对象写入数据库。如果在事务外部验证数据库中的记录，那么在事务完成之前，您无法看到已添加的学生。如果事务失败，则会进行回滚，并且该学生不会写入数据库。

调用 AddStudent() 方法后，调用辅助方法 Utilities.AbortTx() 来询问是否应中止事务。如果用户中止，则抛出 ApplicationException 类型的异常，并在 catch 块中通过调用 Transaction 类的 Rollback() 方法进行回滚。记录不会写入数据库。如果用户不中止，则 Commit() 方法提交事务，事务的最终状态为已提交：

```
static void CommittableTransaction()
{
    var tx = new CommittableTransaction();
    Utilities.DisplayTransactionInformation("TX created",
        tx.TransactionInformation);

    try
    {
        var s1 = new Student
        {
            FirstName = "Jörg",
            LastName = "Neumann",
            Company = "thinktecture"
        };
        var db = new StudentData();
        db.AddStudent(s1, tx);

        if (Utilities.AbortTx())
        {
            throw new ApplicationException("transaction abort");
        }

        tx.Commit();
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
        Console.WriteLine();
        tx.Rollback();
    }
    Utilities.DisplayTransactionInformation("TX completed",
        tx.TransactionInformation);
}
```

代码片段 TransactionSamples/Program.cs

在这里，您可以看到应用程序的输出，其中事务处于活动状态并具有本地标识符。接下来的应用程序输出显示了用户选择中止事务的结果。事务完成后，您可以看到已中止状态：

```
TX created
Creation Time: 7:30:49 PM
Status: Active
Local ID: bdcf1dc-a67e-4ccc-9a5c-cbdf0fe9177:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Abort the Transaction (y/n)? y
Transaction abort

TX completed
Creation Time: 7:30:49 PM
Status: Aborted
Local ID: bdcf1dc-a67e-4ccc-9a5c-cbdf0fe9177:1
Distributed ID: 00000000-0000-0000-0000-000000000000
```

通过您在这里看到的第二个应用程序输出，事务未被用户中止。事务状态为已提交，并且数据已写入数据库：

```
TX Created
Creation Time: 7:33:04 PM
Status: Active
Local ID: 708da71-fa2a-4649-86b4-18b83120f6af:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Abort the Transaction (y/n)? n

TX completed
Creation Time: 7:33:04 PM
Status: Committed
Local ID: 708da71-fa2a-4649-86b4-18b83120f6af:1
Distributed ID: 00000000-0000-0000-0000-000000000000
```

## 事务提升

System.Transactions 支持可提升事务。根据参与事务的资源，要么创建本地事务，要么创建分布式事务。SQL Server 2005 和 2008 支持可提升事务。到目前为止，您只看到了本地事务。在之前的所有示例中，分布式事务 ID 始终设置为 0，并且只分配了本地 ID。对于不支持可提升事务的资源，会创建分布式事务。如果向事务添加多个资源，事务可能会从本地事务开始，并根据需要提升为分布式事务。当向事务添加多个 SQL Server 数据库连接时，就会发生这种提升。事务从本地事务开始，然后提升为分布式事务。

现在对控制台应用程序进行了更改，使用同一个事务对象 tx 添加第二个学生。由于每个 AddStudent() 方法都会打开一个新连接，因此在添加第二个学生后，有两个连接与事务关联：

```
static void TransactionPromotion()
{
    var tx = new CommittableTransaction();
    Utilities.DisplayTransactionInformation("TX created", tx.TransactionInformation);

    try
    {
        var s1 = new Student
        {
            FirstName = "Jörg",
            LastName = "Neumann",
            Company = "thinktecture"
        };
        var db = new StudentData();
        db.AddStudent(s1, tx);

        var s2 = new Student
        {
            FirstName = "Richard",
            LastName = "Blewett",
            Company = "thinktecture"
        };
        db.AddStudent(s2, tx);

        Utilities.DisplayTransactionInformation("2nd connection enlisted", tx.TransactionInformation);

        if (Utilities.AbortTx())
        {
            throw new ApplicationException("transaction abort");
        }

        tx.Commit();
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
        Console.WriteLine();
        tx.Rollback();
    }

    Utilities.DisplayTransactionInformation("TX finished", tx.TransactionInformation);
}
```

代码片段 TransactionSamples/Program.cs

现在运行该应用程序，您可以看到添加第一个学生时分布式标识符为 0，但添加第二个学生时事务被提升，因此一个分布式标识符与事务关联：

```
TX created
Creation Time: 7:56:24 PM
Status: Active
Local ID: 6d2f5ada-32a-40eb-b9d7-cc6aa9a2a554:1
Distributed ID: 00000000-0000-0000-0000-000000000000

2nd connection enlisted
```
