
![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_138_0.png)

Figure 6-8: Selecting Shared-All Options
图 6-8：选择共享全部选项

performs the database update. If the box is not checked, the cache agent performs the update. This is referred to as “Write Behind.” Note that the Cache-Aside option is not available for the Berkeley DB.
执行数据库更新。如果未勾选该框，则缓存代理执行更新。这被称为“写后”。请注意，Cache-Aside 选项在 Berkeley DB 中不可用。

### Cache-Aside Behavior
### Cache-Aside 行为

With Cache-Aside, the inference agent performs the database update. This activity is performed in the postprocessing after the RTC cycle has completed. The details of this update are described in Chapter 5.
使用 Cache-Aside 时，推理代理执行数据库更新。此活动在 RTC 周期完成后在后处理中执行。有关此更新的详细信息请参见第 5 章。

A key parameter driving this update is the `Agent.<agentName>.enableParallelOps` property in the CDD file for the agent that will be performing the update. Figure 5-22 shows the behavior when this property is set to `false`, and Figure 5-23 shows the behavior when the property is set to true.
驱动此更新的一个关键参数是执行更新的代理的 CDD 文件中的 `Agent.<agentName>.enableParallelOps` 属性。图 5-22 显示了将此属性设置为 `false` 时的行为，图 5-23 显示了将属性设置为 true 时的行为。

When Cache-Aside is selected, database operations may be batched together and executed as a single transaction for efficiency. With `enableParallelOps = false`, all database updates occur before any cache updates.
选择 Cache-Aside 时，数据库操作可以批量组合并作为单个事务执行以提高效率。当 `enableParallelOps = false` 时，所有数据库更新都在任何缓存更新之前发生。

### Write-Behind Behavior
### Write-Behind 行为

If the Cache Aside box is not checked, the result is Write-Behind behavior (Figure 6-9). In this mode, the inference agent updates the cache, and the cache agent, in turn, updates the database. In this mode, each individual cache object update results in a separate database transaction.
如果未勾选 Cache Aside 框，则结果为 Write-Behind 行为（图 6-9）。在此模式下，推理代理更新缓存，然后缓存代理更新数据库。在此模式下，每个单独的缓存对象更新都会导致一次单独的数据库事务。

reside in working memory and never enter the cache. In Cache-Only mode, objects reside in the cache and must be explicitly brought into working memory when needed. In Cache + Memory mode, objects reside in both working memory and the cache. This mode must be used with caution, as any change to an object may trigger every rule in every agent that uses that object.
驻留在工作内存中且永不进入缓存。在 Cache-Only 模式下，对象驻留在缓存中，需要时必须显式带入工作内存。在 Cache + Memory 模式下，对象同时驻留在工作内存和缓存中。此模式必须谨慎使用，因为对对象的任何更改都可能触发使用该对象的每个代理中的每条规则。

Because objects can be accessed from multiple agents or multiple threads within one agent, a locking mechanism is required. The locks provided by TIBCO BusinessEvents are logical: The objects themselves are not locked, key values are. A convention associates the key being locked with the object, with the common convention being the use of the object's extID as the lock key. Programming discipline is required to ensure the consistent use of locks.
由于对象可以从多个代理或一个代理内的多个线程访问，因此需要锁定机制。TIBCO BusinessEvents 提供的锁是逻辑上的：对象本身并未被锁定，而是键值被锁定。一种约定将锁定的键与对象关联起来，常见约定是使用对象的 extID 作为锁键。需要编程规范以确保锁的一致使用。

The cache provides the ability to replicate objects in memory, with each copy of the object residing in a different cache agent. This guarantees that the object will survive the loss of a cache agent.
缓存提供了在内存中复制对象的能力，每个对象的副本驻留在不同的缓存代理中。这保证了对象在缓存代理丢失时仍然存活。

Objects in cache may be optionally persisted, either in a database (Shared-All option) or in files (Shared-Nothing option). With Shared-All, there are two sub-modes: Cache-Aside and Write-Behind. With Cache-Aside, the inference agent does the database update, while in Write-Behind the cache agent does the database update. In the Shared-Nothing option, each cache agent persists the objects in its memory to a separate file.
缓存中的对象可以可选地持久化，要么在数据库中（共享全部选项），要么在文件中（共享无选项）。在共享全部中，有两种子模式：Cache-Aside 和 Write-Behind。在 Cache-Aside 中，推理代理执行数据库更新，而在 Write-Behind 中，缓存代理执行数据库更新。在共享无选项中，每个缓存代理将内存中的对象持久化到单独的文件中。

## Chapter 7: Query Agents
## 第 7 章：查询代理

### Objectives
### 目标

Query agents are part of the TIBCO BusinessEvents® Event Stream Processing product, an add-on to the core TIBCO BusinessEvents® product (Chapter 4).
查询代理是 TIBCO BusinessEvents® Event Stream Processing 产品的一部分，该产品是核心 TIBCO BusinessEvents® 产品（第 4 章）的附加组件。

After reading this chapter you will be able to describe the capabilities and appropriate uses for query agents and how snapshot and continuous queries work.
阅读本章后，您将能够描述查询代理的功能和适当用途，以及快照查询和连续查询的工作方式。

### Snapshot Queries
### 快照查询

A snapshot query is a query of the cache contents that is executed on-demand. The demand comes in the form of an event sent to a channel on the query agent (Figure 7-1).
快照查询是对缓存内容执行的按需查询。需求以发送到查询代理通道上的事件的形式出现（图 7-1）。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_142_0.png)

Figure 7-1: Query Agent Snapshot Configuration
图 7-1：查询代理快照配置

### Snapshot Query Execution
### 快照查询执行

The processing associated with the query execution is split between the cache agent and the query agent (Figure 7-2). The cache agent performs filtering operations involving concepts in a manner similar to the inference agent’s Rete network filters. Any objects that satisfy the filter conditions are forwarded to the query agent where joins are performed.
与查询执行相关的处理在缓存代理和查询代理之间拆分（图 7-2）。缓存代理以类似于推理代理 Rete 网络过滤器的方式执行涉及概念的过滤操作。满足过滤条件的任何对象都会转发到查询代理，在那里执行连接。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_142_1.png)

Figure 7-2: Snapshot Query Execution
图 7-2：快照查询执行

Objects that pass all conditions are added to the query results.
通过所有条件的对象将被添加到查询结果中。

An example query is shown in Listing 7-1. There is one where clause in the query, accountNumber = $acctNo. This is a filter condition: the accountNumber is compared against a variable whose value is fixed at the time the query is executed. The filter condition is passed to the cache agent, and the cache agent will return all accounts whose accountNumber matches the condition (hopefully only one!).
示例查询如清单 7-1 所示。查询中有一个 where 子句，accountNumber = $acctNo。这是一个过滤条件：accountNumber 与在查询执行时值固定的变量进行比较。过滤条件传递给缓存代理，缓存代理将返回 accountNumber 与条件匹配的所有账户（希望只有一个！）。

Listing 7-1: Snapshot Query Example
清单 7-1：快照查询示例

```
select account
from /Concepts/Account account
where accountNumber = $acctNo
```

The query agent can query all of the contents of the cache. In addition to concepts, this may include events and scorecards present in the cache, even though they are otherwise inaccessible to other agents.
查询代理可以查询缓存的所有内容。除了概念之外，这可能还包括缓存中存在的事件和评分卡，即使它们对其他代理而言通常无法访问。

### Snapshot Query Life Cycle
### 快照查询生命周期

The configuration and execution of a snapshot query is done by executing code (Figure 7-3). The first step in the process is to create (define) the query using the Query.create() function. The function parameters are the name you choose for the query and a string containing the query definition (Listing 7-1 is an example of such a string). The query definition is parsed, and the function will throw an exception if there is an error in the query definition.
快照查询的配置和执行是通过执行代码完成的（图 7-3）。过程中的第一步是使用 Query.create() 函数创建（定义）查询。函数参数是您为查询选择的名称和包含查询定义的字符串（清单 7-1 是此类字符串的示例）。查询定义将被解析，如果查询定义中存在错误，函数将抛出异常。

There are two places you might put the query creation code: in a rule function that is designated as a start-up function or in the preprocessor function that will eventually execute the query. If the query definition will not change, the start-up function is a good choice: The process of parsing the query definition will occur only once. But if the query definition depends upon the current context, it will have to go in the preprocessor function.
您可能将查询创建代码放在两个位置之一：在被指定为启动函数的规则函数中，或在最终执行查询的预处理器函数中。如果查询定义不会更改，启动函数是很好的选择：解析查询定义的过程只会发生一次。但如果查询定义取决于当前上下文，则必须放在预处理器函数中。

Once the query has been created, the next step is to create an instance of the query using the Query.Statement.open() function. Creating instances of the query allows multiple queries of the same type to be executed concurrently. If there are variables in the query (e.g., $acctNo in Listing 7-1), the third step is to set the values of these variables using the Query.Statement.setVar() function.
一旦查询被创建，下一步就是使用 Query.Statement.open() 函数创建查询的实例。创建查询实例允许并发执行同一类型的多个查询。如果查询中有变量（例如清单 7-1 中的 $acctNo），第三步是使用 Query.Statement.setVar() 函数设置这些变量的值。

The query is actually executed with the Query.Statement.execute() function. An argument to this function is the identifier that you want to assign to the ResultsSet data structure that will be returned. Once the query has executed, you can use the Query.ResultsSet.xxx functions to examine the contents of the results set. Optionally, you can close the statement and delete the query if desired.
查询实际使用 Query.Statement.execute() 函数执行。此函数的参数是您希望分配给将返回的 ResultsSet 数据结构的标识符。查询执行后，您可以使用 Query.ResultsSet.xxx 函数检查结果集的内容。可选地，如果需要，您可以关闭语句并删除查询。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_144_0.png)

Figure 7-3: Snapshot Query Life Cycle
图 7-3：快照查询生命周期

### ACEPSTSnapshotQuery Example
### ACEPSTSnapshotQuery 示例

Figure 7-4 shows the configuration of this example.
图 7-4 显示了此示例的配置。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_145_0.png)

Figure 7-4: ACEPSTSnapshotQuery Configuration
图 7-4：ACEPSTSnapshotQuery 配置

When the InferenceQueryPU is started, it executes the start-up function in Listing 7-2. This start-up function creates the FraudQuery.
当 InferenceQueryPU 启动时，它执行清单 7-2 中的启动函数。此启动函数创建 FraudQuery。

Listing 7-2: ACEPSTSnapshotQuery Query Agent Start-up Function
清单 7-2：ACEPSTSnapshotQuery 查询代理启动函数

```
void rulefunction RuleFunctions.queryStartup {
    attribute {
        validity = ACTION;
    }
    scope {
    }
    body {
        Query.create("FraudQuery","select account from /Concepts/Account account where accountNumber = $acctNo");
    }
}
```

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_145_1.png)

Figure 7-5: Concepts Used in ACEPSTSnapshotQuery
图 7-5：ACEPSTSnapshotQuery 中使用的概念

The Account concept and associated tinyTransaction Transaction concept used in the example in Listing 7-2 are shown in Figure 7-5.
清单 7-2 中示例使用的 Account 概念和关联的 tinyTransaction Transaction 概念如图所示 7-5 所示。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_146_0.png)

Figure 7-6: ACEPSTSnapshotQuery Behavior
图 7-6：ACEPSTSnapshotQuery 行为

An overview of this example's behavior is shown in Figure 7-6. The TestDriverInference agent is used as the insertion point for test data. A rule in this agent generates a Transaction event, which is sent to the ProductionInference inference agent.
图 7-6 显示了此示例行为的概述。TestDriverInference 代理用作测试数据的插入点。该代理中的一条规则生成 Transaction 事件，该事件发送到 ProductionInference 推理代理。

The ProductionInference agent has a preprocessor function associated with this event. The function first checks to see whether the amount exceeds the small threshold. If it does, it forwards the transaction to the query agent. If it does not, it attempts to retrieve the Account concept from the cache, and if one is not found, it creates it. Next, it appends a Transaction concept as the Account. tinyTransaction, consumes the event, and allows the cache to be updated.
ProductionInference 代理具有与此事件关联的预处理器函数。该函数首先检查金额是否超过小阈值。如果超过，则将交易转发给查询代理。如果未超过，则尝试从缓存中检索 Account 概念，如果未找到则创建它。接下来，它将 Transaction 概念附加为 Account.tinyTransaction，消费事件，并允许缓存更新。

The preprocessor in the SnapshotQueryAgent checks the transaction to see whether it exceeds the large threshold. If it does, it queries the cache to see if there has been a tiny transaction within the past hour. If one is found, it announces the fraud.
SnapshotQueryAgent 中的预处理器检查交易是否超过大阈值。如果超过，则查询缓存以查看过去一小时内是否发生过微小交易。如果找到，则宣布欺诈。

The preprocessor function for the SnapshotQueryAgent is shown in Listing 7-3. It synthesizes unique identifiers for both the statement and the result set. It opens the statement (i.e., creates an instance of the query) and sets the value of the acctNo variable. It executes the query and examines the results to see if there is an account with a tiny transaction that occurred within the past hour. If one is found, it makes an announcement both with a System.debugOut() statement and the sending of a fraudEvent.
SnapshotQueryAgent 的预处理器函数如清单 7-3 所示。它为语句和结果集合成唯一标识符。它打开语句（即创建查询的实例）并设置 acctNo 变量的值。它执行查询并检查结果，以查看是否存在过去一小时内发生的微小交易的账户。如果找到，则通过 System.debugOut() 语句和发送 fraudEvent 两种方式进行公告。
