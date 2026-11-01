

```
创建时间：7:56:24 PM
状态：活动
本地 ID：0d2f5ada-32aa-40eb-b9d7-cc6aa9a2a554:1
分布式 ID：501bad91-e512-47f3-95d5-0e48874293d

中止事务 (y/n)？
```

事务提升要求 DTC 已启动。如果事务提升在你的系统上失败，请确认 DTC 服务已启动。启动“组件服务”MMC 管理单元后，可以查看系统上运行的所有 DTC 事务的实际状态。

在树视图中选择“事务列表”，可以查看所有活动事务。在图 23-3 中，可以看到有一个事务处于活动状态，其分布式标识符与前面控制台输出中显示的标识符相同。如果在你的系统上验证输出，请确保事务设置了超时，并且在达到超时时中止。超时后，你将无法再在事务列表中看到该事务。还可以使用同一工具验证事务统计信息。“事务统计信息”显示已提交和已中止事务的数量。

![](img/d7d2ffa0a76feaab821930e95daace93_677_0.png)

图 23-3

## 依赖事务

借助依赖事务，可以从多个线程影响一个事务。依赖事务依赖于另一个事务，并影响该事务的结果。

示例应用程序 DependentTransactions 会为新线程创建一个依赖事务。方法 TxThread() 是新线程的方法，其中将 DependentTransaction 对象作为参数传入。依赖事务的信息通过辅助方法 DisplayTransactionInformation() 显示。在线程退出之前，会调用依赖事务的 Complete() 方法来定义事务结果。依赖事务可以通过调用 Complete() 或 Rollback() 方法来定义事务结果。Complete() 方法会设置成功位。如果根事务完成，并且所有依赖事务都将成功位设置为 true，则事务会提交。如果任何依赖事务通过调用 Rollback() 方法设置中止位，则整个事务会中止：

```
static void TxThread(object obj)
{
    DependentTransaction tx = obj as DependentTransaction;
    Utilities.DisplayTransactionInformation("Dependent Transaction",
        tx.TransactionInformation);

    Thread.Sleep(3000);
    tx.Complete();

    Utilities.DisplayTransactionInformation("Dependent TX Complete",
        tx.TransactionInformation);
}
```

代码片段 TransactionSamples/Program.cs

通过 DependentTransaction() 方法，首先实例化 CommittableTransaction 类来创建一个根事务，并显示事务信息。接下来，方法 tx.DependentClone() 会创建一个依赖事务。此依赖事务会传递给方法 TxThread()，该方法被定义为新线程的入口点。

方法 DependentClone() 需要一个 DependentCloneOption 类型的参数。该类型是一个枚举，其值包括 BlockCommitUntilComplete 和 RollbackIfNotComplete。如果根事务在依赖事务之前完成，此选项就非常重要。将选项设置为 RollbackIfNotComplete 时，如果依赖事务在根事务的 Commit() 方法调用之前没有调用 Complete() 方法，则事务会中止。将选项设置为 BlockCommitUntilComplete 时，Commit() 方法会一直等待，直到所有依赖事务定义了结果。

接下来，如果用户没有中止事务，则会调用 CommittableTransaction 类的 Commit() 方法。

![](img/d7d2ffa0a76feaab821930e95daace93_678_0.png)

```
static void DependentTransaction()
{
    var tx = new CommittableTransaction();
    Utilities.DisplayTransactionInformation("Root TX created",
        tx.TransactionInformation);

    try
    {
        new Thread(TxThread).Start(tx.DependentClone(
            DependentCloneOption.BlockCommitUntilComplete));

        if (Utilities.AbortTx())
        {
            throw new ApplicationException("transaction abort");
        }

        tx.Commit();
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
        tx.Rollback();
    }

    Utilities.DisplayTransactionInformation("TX finished",
        tx.TransactionInformation);
}
```

代码片段 TransactionSamples/Program.cs

通过应用程序的输出，可以看到带有其标识符的根事务。由于使用了选项 DependentCloneOption.BlockCommitUntilComplete，根事务会在 Commit() 方法中等待，直到依赖事务的结果被定义。依赖事务完成后，事务会立即提交：

```
Root TX created
Creation Time: 8:35:25 PM
Status: Active
Local ID: 50126e07-cd28-4e0f-a21f-a81a8e14a1a8:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Abort the Transaction (y/n)? n

Dependent Transaction
Creation Time: 8:35:25 PM
Status: Active
Local ID: 50126e07-cd28-4e0f-a21f-a81a8e14a1a8:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Dependent TX Complete
Root TX finished
Creation Time: 8:35:25 PM
Status: Committed
Local ID: 50126e07-cd28-4e0f-a21f-a81a8e14a1a8:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Creation Time: 8:35:25 PM
Status: Committed
Local ID: 50126e07-cd28-4e0f-a21f-a81a8e14a1a8:1
Distributed ID: 00000000-0000-0000-0000-000000000000
```

## 环境事务

System.Transactions 真正重要的优势是环境事务功能。借助环境事务，无需手动将连接登记到事务中；支持环境事务的资源会自动完成此操作。

环境事务与当前线程相关联。可以通过静态属性 Transaction.Current 获取和设置环境事务。支持环境事务的 API 会检查此属性，以获取环境事务并登记到该事务中。ADO.NET 连接支持环境事务。

可以创建一个 CommittableTransaction 对象，并将其分配给 Transaction.Current 属性，从而初始化环境事务。创建环境事务的另一种方式是使用 TransactionScope 类。TransactionScope 的构造函数会创建一个环境事务。

TransactionScope 的重要方法是 Complete() 和 Dispose() 方法。Complete() 方法会为作用域设置成功位，Dispose() 方法会结束作用域；如果该作用域是根作用域，则提交或回滚事务。

由于 TransactionScope 类实现了 IDisposable 接口，因此可以使用 using 语句定义作用域。默认构造函数会创建一个新事务。在创建 TransactionScope 实例后，可以立即通过 Transaction.Current 属性的 get 访问器获取事务，并在控制台中显示事务信息。

若要在事务完成时获取相关信息，可以将 OnTransactionCompleted() 方法设置为环境事务的 TransactionCompleted 事件处理程序。

然后创建一个新的 Student 对象，并通过调用 studentData.AddStudent() 方法将其写入数据库。使用环境事务后，不再需要将 Transaction 对象传递给此方法，因为 SqlConnection 类支持环境事务，并会自动将其登记到连接中。接着，TransactionScope 类的 Complete() 方法会设置成功位。using 语句结束时，TransactionScope 会被释放，并执行提交。如果未调用 Complete() 方法，Dispose() 方法会中止事务。

> 如果不希望 ADO.NET 连接登记到环境事务中，可以在连接字符串中将 Enlist=false 设置为相应的值。

```
static void TransactionScope()
{
    using (var scope = new TransactionScope())
    {
        Transaction.Current.TransactionCompleted +=
            OnTransactionCompleted;

        Utilities.DisplayTransactionInformation("Ambient TX created",
            Transaction.Current.TransactionInformation);

        var s1 = new Student
        {
            FirstName = "Ingo",
            LastName = "Rammer",
            Company = "thinktecture"
        };
        var db = new StudentData();
        db.AddStudent(s1);

        if (!Utilities.AbortTx())
            scope.Complete();
        else
            Console.WriteLine("transaction will be aborted");

    } // scope.Dispose()

    static void OnTransactionCompleted(object sender, TransactionEventArgs e)
    {
        Utilities.DisplayTransactionInformation("TX completed",
            e.Transaction.TransactionInformation);
    }
}
```

代码片段 TransactionSamples/Program.cs

运行应用程序时，可以看到在创建 TransactionScope 类的实例后存在一个活动的环境事务。应用程序的最后一段输出来自 TransactionCompleted 事件处理程序，用于显示已完成事务的状态：

环境事务已创建
创建时间：9:55:40 PM
状态：活动
本地 ID：a0df6fb-7266-435e-b9e0-f024f1d6966e:1
分布式 ID：00000000-0000-0000-0000-000000000000

中止事务 (y/n)? n

事务已完成
创建时间：9:55:40 PM
状态：已提交
本地 ID：a0df6fb-7266-435e-b9e0-f024f1d6966e:1
分布式 ID：00000000-0000-0000-0000-000000000000

