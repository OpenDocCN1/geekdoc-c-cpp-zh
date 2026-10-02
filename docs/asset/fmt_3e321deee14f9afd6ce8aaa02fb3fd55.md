
最后，持久性（durability）属性确保当你提交事务时，一旦收到数据库的确认，你就可以确保事务已完成并可以被恢复。SQL Server 对持久性的保证取决于你数据库的恢复模型。恢复模型是一个决定数据库可恢复性的数据库设置。支持的选项有 `SIMPLE`、`BULK_LOGGED` 和 `FULL`。如果恢复模型为 `FULL`，它允许 SQL Server 在提交时将更改硬化（harden）到日志文件中。硬化更改意味着将 60-KB 的日志缓冲区（`log buffer`）刷新（flushing）到磁盘上的日志文件。如果你使用的是 `SIMPLE` 或 `BULK_LOGGED` 恢复模型，批量操作将只执行最小日志记录，以在需要时支持回滚操作。因此，当你提交事务时，为了保证持久性，SQL Server 仅刷新日志缓冲区是不够的；它还需要将脏页从缓冲区池中刷新到数据文件中。结果，在 `SIMPLE` 和 `BULK_LOGGED` 恢复模型下，提交可能需要更长时间。

SQL Server 2014 引入了一个名为延迟持久性（delayed durability）的新功能。我将在本节稍后介绍。

SQL Server 不支持嵌套事务。它允许你嵌套一个 `BEGIN TRAN`/`COMMIT TRAN` 语句来命名事务，但实际上最多只有一个事务。`ROLLBACK TRAN <tran_name>` 命令（带有事务名称）仅在引用最外层的事务名称时有效。每执行一次 `BEGIN TRAN` 命令，SQL Server 都会增加计数器，可以通过 `@@trancount` 函数查询。每执行一次 `COMMIT TRAN` 命令，SQL Server 实际上仅在计数器降为 0 时才会执行提交。

假设你打开了一个事务，并在其中调用了一个存储过程。在存储过程中，你发布了 `BEGIN TRAN` 命令，做了一些工作，并发布了 `COMMIT` 命令。当过程结束时，你仍然处于一个开启的事务中。如果发生导致事务回滚的故障，所有的所有更改将被撤销——包括调用过程之前和之后提交的更改，以及由过程本身提交的更改。

由于 SQL Server 不支持嵌套事务，在存储过程内部你没有办法强制执行实际提交。然而，如果你需要在某些条件下撤销过程的工作，可以使用保存点（savepoint）来实现此目的。在存储过程的初，你可以检查是否已经处于 `@@trancount` 内部。将此信息存储在变量中（命名为 `@tranexited`）。如果你不在事务中，发布 `BEGIN TRAN` 来开启一个事务。如果你已经在事务中，发布 `SAVE TRAN <savepoint_name>` 命令来标记一个保存点。如果过程过程中一切顺利，只有在过程确实开启了事务时，你才会发布 `COMMIT` 命令。如果你需要撤销过程的工作，取决于过程是开启了事务还是标记了保存点，你将分别发布 `ROLLBACK TRAN` 命令或 `ROLLBACK TRAN <savepoint_name>` 命令。

以下代码演示了你如何实现这种策略（通常这段代码会位于存储过程中）：

```sql
-- BEGIN TRAN;

DECLARE @tranexited AS INT = 0, @allisgood AS INT = 0;

IF @@trancount = 0
    BEGIN TRAN;
ELSE
BEGIN
    SET @tranexited = 1;
    SAVE TRAN S1;
END;

-- ... 一些工作 ...

-- 仅在内部工作时需要回滚
IF @allisgood = 1
    COMMIT TRAN;
ELSE
    IF @tranexited = 1
    BEGIN
        PRINT 'Rolling back to savepoint.';
        ROLLBACK TRAN S1;
    END;
    ELSE
    BEGIN
        PRINT 'Rolling back transaction.'
        ROLLBACK TRAN;
    END;

-- COMMIT TRAN;
```

你可以使用被注释的 `BEGIN TRAN` 和 `COMMIT TRAN` 命令来测试在存在和不存在现有事务的情况下运行代码。`@allisgood` 标志允许你在情况顺利时测试代码（当标志设置为 1 时，你不想撤销工作）以及在情况不顺时测试代码（当标志设置为 0 时，你想撤销工作）。

运行该代码，这代表在执行过程时没有开启的事务，且过程中的情况并不顺利。在这种情况下，代码开启了一个事务并在随后将其回滚。代码产生：

```
Rolling back transaction.
```

取消注释 `BEGIN TRAN` 和 `COMMIT TRAN` 命令并再次运行代码。这代表在执行过程时开启了事务，且过程中的情况并不顺利。代码回滚到保存点。代码产生：

```
Rolling back to savepoint.
```

# 锁与阻塞

SQL Server 支持不同的模型来强制执行你需要的隔离语义。最老的模型——对于基于表的 SQL Server 的默认模型——是基于锁的。在这种模型中，行只有一个版本。你的会话需要获取锁来与数据交互，无论是为了写入还是读取。如果你的会话请求的资源（行、页或表）锁与另一个会话持有的锁发生冲突，则你的会话会被阻塞。这意味着你必须等待另一个会话释放锁或你定义的超时到。

基于表的另一种替代模型是行版本（row-versioning），它是 Microsoft Azure SQL Database（或 "SQL Database"）的默认模型。当你更新或删除行时，SQL Server 将旧版本的行复制到 `tempdb` 中的版本存储器中，SQL Server 可以在这种链列表中维护同一行的多个版本。这种模型是在锁模型之上的补丁。写入者使用锁，读取者不是。当会话需要读取资源时，它不请求锁。如果当前版本不是会话在其当前隔离级别下应拥的版本，SQL Server 将遵循链列表为会话检索较早版本的行。

表 9-2 显示了 SQL Server 使用的一些常用锁的锁矩阵。

## 表格 9-2 锁兼容性

| 请求模式 | IS | S | U | IX | SIX | X |
|---|---|---|---|---|---|---|
| 意向共享 (IS) | 是 | 是 | 是 | 是 | 是 | 否 |
| 共享 (S) | 是 | 是 | 是 | 否 | 否 | 否 |
| 更新 (U) | 是 | 是 | 否 | 否 | 否 | 否 |
| 意向排他 (IX) | 是 | 否 | 否 | 是 | 否 | 否 |
| 意向排他共享 (SIX) | 是 | 否 | 否 | 否 | 否 | 否 |
| 排他 (X) | 否 | 否 | 否 | 否 | 否 | 否 |

更新锁 (U) 是共享锁和排他锁的一种混合。类似于共享锁，更新锁与另一个共享锁兼容。类似于排他锁，更新锁与另一个更新锁不兼容。这意味着一次只有一个会话可以持有某个资源的更新锁。SQL Server 示例在内部使用更新锁来保护索引中搜索需要修改的行的访问路径。你也可以在查询中使用表提示（table hint）显式请求更新锁，例如：

```sql
SELECT ... FromTable WITH (UPDLOCK) ... :
```

这种显式提示的一个经典用例是当事务涉及读取数据、应用计算并在稍后写入数据时。如果你想确保在任何时刻只有一个会话在运行，可以在启动该过程的 `SELECT` 查询中通过一个 `UPDLOCK` 提示。这样，谁先执行查询，谁就先运行该流程。其余的将等待。稍后，我将解释这种方法如何帮助你防止“丢失更新”（lost updates）的现象。

锁兼容性表中剩余的锁是意向锁。包括意向共享锁 (IS)、意向排他锁 (IX) 和意向排他共享锁 (SIX)。意向共享和排他锁会阻塞相同粒度级别上的冲突锁请求，但不会阻塞更低层级的请求。意向排他共享锁类似于排他锁，但带有共享锁的额外限制，会阻塞更低粒度级别上的冲突锁。

SQL Server 示例内部使用意向锁来保护你需要交互的资源之上的层级结构。例如，假设你需要作为事务的一部分更新某行。你的会话需要一个排他锁来更新该行。但你的事务仍然开启着。假设此时另一个会话尝试获取整个张表的共享锁。这里存在一个冲突。但对于 SQL Server 来说，要发现冲突的存在并不简单，因为资源是不同的——一个是行，另一个是表。为了简化冲突检测，你的会话会在较高层级的粒度上获取相同类型的意向锁。例如，为了更新某行，你的会话在请求该行的排他锁之前，必须先获取该表的排他锁。然后，当另一个会话尝试在同一张表或页上获取冲突锁时，SQL Server 就能检测到冲突。

你的会话请求的锁与同一资源上已有的锁不兼容，这种情况被称为“阻塞”（blocking）。默认情况下，等待时间没有限制。如果你想设置限制，可以在会话或客户端进行设置。在你的会话中，你可以设置一个名为 `LOCK_TIMEOUT` 的选项为某些毫秒。默认值为 -1，意味着无限期等待。如果设置了此选项，一旦超时过期，你就会收到错误 1222。

在客户端，你可以设置一个命令，使客户端在超时过期后立即终止请求。但这样你并不一定知道查询为什么没有按时完成。可能是因为阻塞，但也可能是由于其他原因，例如系统运行非常慢。

在依赖锁模型的系统中，短期阻塞是正常的。然而，如果阻塞持续很长时间，它就会变成一个问题。如果用户经常经历长时间等待，你需要评估所使用的模型。

在此视图的列中，你将找到 `most_recent_sql_handle` 列。该列存储你提供给表函数 `sys.dm_exec_sql_text` 的二进制句柄，用于获取该连接执行的最后一个 SQL 批处理文本。使用 `APPLY` 操作符将该函数应用于涉及的每个连接，如下所示：

```sql
SELECT C.session_id, ST.text
FROM sys.dm_exec_connections AS C
CROSS APPLY sys.dm_exec_sql_text(most_recent_sql_handle) AS ST
WHERE C.session_id IN(53, 54);
```

我在系统上得到了如下输出：

```
session_id      text
53              BEGIN TRAN;
                UPDATE dbo.T1 SET col2 = 'Version 2' WHERE keycol = 2;
54              SELECT keycol, col1 FROM dbo.T1;
```

会话 53 是阻塞会话。在我们的情况下，该会话包含了导致阻塞情况的语句。在实践中，情况并非如此，因为会话可能会继续工作。会话 54 是被阻塞的会话。显然，它最后执行的是被阻塞的语句。这在故障排除过程中是一条关键信息。

要获取与会话相关的信息，请查询视图 `sys.dm_exec_sessions`：

```sql
SELECT * FROM sys.dm_exec_sessions
WHERE session_id IN(53, 54);
```

在这里，你将找到有关涉及会话的有用信息，如主机、程序、登录名称、NT 用户名、性能指标、set选项的状态以及隔离级别。

要获取被阻塞请求的信息，请查询 `sys.dm_exec_requests` 视图，如下：

```sql
SELECT * FROM sys.dm_exec_requests
WHERE blocking_session_id > 0;
```

你也可以在 `sys.dm_os_waiting_tasks` 视图中找到被阻塞请求的信息：

```sql
SELECT * FROM sys.dm_os_waiting_tasks
WHERE blocking_session_id > 0;
```

请注意，在这两种情况下，你都过滤了被阻塞的请求。

许多人喜欢通过查询这些视图来开始故障排除。视图为你提供了阻塞会话 ID（在我们的案例中为 53，等待为 `LCK_M_S`，意味着共享锁）、等待时间等信息。每个视图都有一些独特的元素。例如，`sys.dm_exec_requests` 视图提供了请求的隔离级别、计划句柄和 SQL 文本。`sys.dm_os_waiting_tasks` 视图对于 `resource_description` 列中发生冲突的资源提供了更详细的信息。

我在这里描述的所有工具都是 SQL Server 的内置工具。Adam Machanic 创建了自己的工具来排查阻塞，其形式为存储过程 `sp_WhoIsActive`。许多人发现它非常有用，并将其作为系统中的标准工具。你可以在 Adam 的博客中找到该存储过程、用法说明以及许可条款：http://tinyurl.com/WholesActive。

回到我们的故障排除过程；到此时，你已经知道会话 53 是阻塞会话，它的事务处于打开状态，并将一直持续到有人终止它为止。要终止与会话 53 相关的用户进程及其打开事务，请使用 `KILL` 命令：

```sql
KILL 53;
```

会话 53 中事务应用的更改被撤销了。回到连接 2，会话 54 成功获得了它一直在等待的共享锁并完成了查询。查询生成了如下输出：

```
keycol col1 col2
------ ------ ----
1       101    A
2       102    Version 1
3       103    C
4       101    C
```

如所述，你使用 `LOCK_TIMEOUT` 会话选项来设置毫秒为单位的锁超时。要在你的示例中尝试，请再次执行连接 1 中的代码（你首先需要重新连接）。然后在连接 2 中执行以下代码以设置五秒的锁超时并运行查询：

```sql
SET LOCK_TIMEOUT 5000;
SELECT keycol, col1, col2 FROM dbo.T1;
```

五秒后，你将收到一个关于锁过期的错误：

```
Msg 1222, Level 16, State 51, Line 2
Lock request time out period exceeded.
```

要获取与会话相关的信息，查询视图 `sys.dm_exec_sessions`：...（注：提供的文本后续继续了故障排除逻辑和 SQL 命令）。

为了演示此功能及其对性能的影响，我将使用一个名为 `testddd` 的数据库，其中包含一个名为 `T1` 的表。运行以下代码创建数据库和表，并将数据库的 `DELAYED_DURABILITY` 选项设置为 `Allowed`：

```sql
SET NOCOUNT ON;
USE master;
GO
IF DB_ID('testddd') IS NOT NULL DROP DATABASE testddd;
GO
CREATE DATABASE testddd;
ALTER DATABASE testddd SET DELAYED_DURABILITY = Allowed;
GO
USE testddd;
CREATE TABLE dbo.T1(col1 INT NULL);
```

在运行每个测试之前，截空表以确保它是空的：

```sql
TRUNCATE TABLE dbo.T1;
```

运行以下代码，在自动提交模式下，通过执行 100,000 个完全持久化的事务，向 T1 插入 100,000 行数据：

```sql
DECLARE @i INT;
WHILE @i <= 100000
BEGIN
    INSERT INTO dbo.T1(col1) VALUES(@i);
    SET @i += 1;
END;
```

这段代码在我的系统上耗了 33 秒完成。

在运行下一个测试之前，截空表：

```sql
TRUNCATE TABLE dbo.T1;
```

运行以下代码，在 100,000 个延迟持久化事务中向 T1 插入 100,000 行数据：

```sql
DECLARE @i AS INT = 1;
WHILE @i <= 100000
BEGIN
    BEGIN TRAN;
    INSERT INTO dbo.T1(col1) VALUES(@i);
    COMMIT WITH (DELAYED_DURABILITY = ON);
    SET @i += 1;
END;
```

这段代码在我的系统上仅用了两秒就完成了。

再次，在运行下一个测试之前，截空表：

```sql
TRUNCATE TABLE dbo.T1;
```

运行以下代码，在一个大型完全持久化事务中向 T1 插入 100,000 行数据：

```sql
BEGIN TRAN;
DECLARE @i AS INT = 1;
WHILE @i <= 100000
BEGIN
    INSERT INTO dbo.T1(col1) VALUES(@i);
    SET @i += 1;
END;
COMMIT TRAN;
```

这段代码在我的系统上耗了几秒钟完成。

在最后一个测试之前，清除表：

```sql
TRUNCATE TABLE T1;
```

运行以下代码，在一个大型延迟持久化事务中向 T1 插入 100,000 行数据：

```sql
BEGIN TRAN;
DECLARE @i AS INT = 1;
WHILE @i <= 100000
BEGIN
    INSERT INTO dbo.T1(col1) VALUES(@i);
    SET @i += 1;
END;
COMMIT TRAN WITH (DELAYED_DURABILITY = ON);
```

对于这种类型的负载，这段代码用一秒就完成了。

这些测试证实了，从延迟持久化功能中主要受益的负载类型是包含许多小事务的负载。

## 隔离级别

你使用隔离级别来控制“一致数据”对你来说意味着什么。在与数据库中的数据交互时，可能会遇到许多经典现象；每种现象是否可能发生取决于你所运行的隔离级别。这些现象包括：

- **脏读（Dirty reads）**：对未提交数据的读取。一个事务更改了数据，但在另一个事务读取相同数据之前没有提交。第二个事务最终读取到了不一致的数据状态。

- **丢失的更新（Lost updates）**：两个事务并行运行以下流程：读取数据、进行某些计算、并更新数据。在这样的流程下，一个事务可能会覆盖另一个事务的更新。
