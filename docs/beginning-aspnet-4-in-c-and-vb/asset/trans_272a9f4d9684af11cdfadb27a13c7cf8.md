
```
Transaction.Current.TransactionInformation);
scope.Complete();
}
catch (TransactionAbortedException ex)
{
    Console.WriteLine("ThreadMethod - transaction was aborted, {0}",
        ex.Message);
}
finally
{
    if (dTx != null)
    {
        dTx.Complete();
    }
}
static void TransactionCompleted(object sender, TransactionEventArgs e)
{
    Utilities.DisplayTransactionInformation("TX completed",
        e.Transaction.TransactionInformation);
}
```

运行应用程序后，您可以看到主线程和新创建的线程正在使用并影响同一个事务。线程列出的事务具有相同的标识符。如果在某个线程中未通过调用 Complete() 方法设置成功位，则整个事务会中止：

```
Main thread TX
Creation Time: 23:00:57
Status: Active
Local ID: 2fblb54d-6f5-4d4e-a55e-fda9e04778be:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Thread TX
Creation Time: 23:00:57
Status: Active
Local ID: 2fblb54d-6f5-4d4e-a55e-fda9e04778be:1
Distributed ID: 00000000-0000-0000-0000-000000000000

TX completed
Creation Time: 23:00:57
Status: Committed
Local ID: 2fblb54d-6f5-4d4e-a55e-fda9e04778be:1
Distributed ID: 00000000-0000-0000-0000-000000000000

TX completed
Creation Time: 23:00:57
Status: Committed
Local ID: 2fblb54d-6f5-4d4e-a55e-fda9e04778be:1
Distributed ID: 00000000-0000-0000-0000-000000000000
```

## 隔离级别

本章开头，您可以看到用于描述事务的 ACID 属性。ACID 中的字母 I（隔离）并非总是完全必需的。出于性能原因，您可能会降低隔离要求，但必须意识到更改隔离级别时将会遇到的问题。

如果不完全隔离事务外部的范围，您可能会遇到的问题可以分为三类：

-   **脏读** — 另一个事务可以读取在事务中被更改的记录。因为事务中更改的数据可能会回滚到原始状态，所以从另一个事务读取这种中间状态被认为是“脏”的——数据尚未提交。您可以通过锁定要更改的记录来避免这种情况。
-   **不可重复读** — 当在事务内部读取数据时，而事务正在运行时，另一个事务更改了相同的记录。如果在事务内部再次读取该记录，结果会不同——不可重复。您可以通过锁定已读取的记录来避免这种情况。
-   **幻读** — 当读取一段数据时，例如使用 WHERE 子句。另一个事务可以添加一条属于事务内读取范围的新记录。使用相同 WHERE 子句的新的读取会返回不同的行数。幻读在对一批行执行 UPDATE 时可能是一个特定问题。例如，UPDATE Addresses SET Zip=4711 WHERE (Zip=2315) 会将所有记录的邮政编码从 2315 更新为 4711。执行更新后，如果在更新运行期间另一用户添加了邮政编码为 2315 的新记录，则仍可能存在邮政编码为 2315 的记录。您可以通过执行范围锁定来避免这种情况。

在定义隔离要求时，您可以设置隔离级别。这是通过在创建事务时配置的 IsolationLevel 枚举来设置的（使用 CommitableTransaction 类的构造函数或 TransactionScope 类的构造函数）。IsolationLevel 定义了锁定行为。下表列出了 IsolationLevel 枚举的值。

| 隔离级别 | 描述 |
|---|---|
| 读未提交 | 使用 读未提交 时，事务之间不会相互隔离。在此级别下，不会等待来自其他事务的锁定记录。这样，未提交的数据可以从其他事务中读取——脏读。此级别通常仅用于读取记录的情况，即使读取中间更改也无关紧要（例如，报表）。 |
| 读已提交 | ReadCommitted 会等待来自其他事务的写锁记录。这样，脏读就不会发生。此级别为当前读取的记录设置读锁，并为正在写入的记录设置写锁，直到事务完成。读取一系列记录时，每读取一条新记录，先前的记录就会被解锁。这就是为什么可能发生不可重复读的原因。 |
| 可重复读 | RepeatableRead 会在事务完成之前保持对已读取记录的锁定。这样就避免了不可重复读的问题。幻读仍可能发生。 |
| 可序列化 | Serializable 持有范围锁。在事务运行时，不可能添加属于从中读取数据的相同范围的新记录。 |
| 快照 | 隔离级别 快照 仅在 SQL Server 2005 及更高版本中可用。此级别通过复制已修改的行来减少锁。这样，其他事务仍可以读取旧数据而无需等待解锁。 |
| 未指定 | 级别 Unspecified 表示提供程序使用与 IsolationLevel 枚举定义的值不同的隔离级别值。 |
| 混沌 | 级别 Chaos 与 ReadUncommitted 类似，但除了执行 ReadUncommitted 值操作外，Chaos 不会锁定已更新的记录。 |

下表为您总结了设置最常用的事务隔离级别时可能出现的问题。

| 隔离级别 | 脏读 | 不可重复读 | 幻读 |
|---|---|---|---|
| 读未提交 | Y | Y | Y |
| 读已提交 | N | Y | Y |
| 可重复读 | N | N | Y |
| 可序列化 | N | N | N |

以下代码段显示了如何使用 TransactionScope 类设置隔离级别。使用 TransactionScope 的构造函数，您可以设置前面讨论过的 TransactionScopeOption 和 TransactionOptions。TransactionOptions 类允许您定义 IsolationLevel 和 Timeout：

```
var options = new TransactionOptions();
options.IsolationLevel = IsolationLevel.ReadUncommitted;
options.Timeout = TimeSpan.FromSeconds(90);
using (TransactionScope scope = 
    new TransactionScope(TransactionScopeOption.Required,
        options))
{
    // Read data without waiting for locks from other transactions.
    // dirty reads are possible.
}
```

## 自定义资源管理器

新事务模型的最大优势之一是相对容易创建参与事务的自定义资源管理器。资源管理器不仅管理持久资源，还可以管理易失性或内存中资源——例如，一个简单的 int 和一个通用列表。

图 23-4 显示了资源管理器与事务类之间的关系。资源管理器实现接口 IEnlistmentNotification，该接口定义了方法 Prepare()、InDoubt()、Commit() 和 Rollback()。资源管理器实现此接口以管理资源的事务。要成为事务的一部分，资源管理器必须向 Transaction 类注册。易失性资源管理器调用方法 EnlistVolatile()；持久性资源管理器调用 EnlistDurable()。根据事务的结果，事务管理器会使用资源管理器调用来自接口 IEnlistmentNotification 的方法。

![](img/d7d2ffa0a76feaab821930e95daace93_687_0.png)

图 23-4

下表解释了您必须与资源管理器一起实现的 IEnlistmentNotification 接口的方法。在查看表格时，请回忆本章前面“事务阶段”部分中解释的活动、准备和提交阶段。

| 注册通知成员 | 描述 |
|---|---|
| Prepare() | 事务管理器为事务准备而调用 Prepare() 方法。资源管理器通过调用传递给 Prepare() 方法的 PreparingEnlistment 参数的 Prepared() 方法来完成准备。如果工作无法成功完成，资源管理器通过调用 ForceRollback() 方法通知事务管理器。持久性资源管理器必须写入日志，以便在准备阶段后成功完成事务。 |
| Commit() | 当所有资源管理器都成功为事务准备好后，事务管理器会调用 Commit() 方法。资源管理器现在可以完成工作以使事务外部可见，并调用 Enlistment 参数的 Done() 方法。 |
| Rollback() | 如果某个资源无法成功为事务准备，事务管理器会使用所有资源管理器调用 Rollback() 方法。状态恢复到事务之前的状态后，资源管理器会调用 Enlistment 参数的 Done() 方法。 |
| InDoubt() | 如果在事务管理器调用 Commit() 方法后出现问题（并且资源没有使用 Done() 方法返回完成信息），事务管理器会调用 InDoubt() 方法。 |

### 事务资源

事务资源必须保留实时值和临时值。实时值在事务外部读取，并在事务回滚时定义有效状态。临时值定义事务提交时的事务有效状态。

为了使非事务类型变为事务，通用示例类 Transactional<T> 包装非通用类型，因此您可以使用它，如下所示：

```csharp
Transactional<int> txInt = new Transactional<int>();
Transactional<string> txString = new Transactional<string>();
```

让我们看看类 Transactional<T> 的实现。托管资源的实时值具有变量 liveValue；与事务关联的临时值存储在 ResourceManager<T> 中。变量 enlistedTransaction 与环境事务关联（如果存在）：

```csharp
using System.Diagnostics;
Insert IconMargin [FILENAME]
using System.Transactions;

namespace Wrox.ProCSharp.Transactions
{
    public partial class Transactional<T>
    {
        private T liveValue;
        private ResourceManager<T> enlistment;
        private Transaction enlistedTransaction;
    }
}
```

代码片段 CustomResource/Transactional.cs

使用 Transactional 构造函数，实时值被设置为变量 liveValue。如果构造函数在环境事务内调用，则会调用 GetEnlistment() 辅助方法。GetEnlistment() 首先检查是否存在环境事务，并在不存在时断言。如果事务尚未注册，则会实例化 ResourceManager<T> 辅助类，并通过调用 EnlistVolatile() 方法将资源管理器与事务注册。此外，变量 enlistedTransaction 被设置为环境事务。
