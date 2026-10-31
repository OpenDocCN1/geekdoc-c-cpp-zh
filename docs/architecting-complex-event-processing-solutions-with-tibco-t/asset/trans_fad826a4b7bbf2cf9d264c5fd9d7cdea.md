

## 后处理行为

一旦 RTC 周期完成，还需要执行许多后处理活动。根据 CDD 文件中布尔属性 `Agent.<agentName>.enableParallelOps` 的值，这些活动可以单线程执行，也可以并行执行。

图 5-22 显示了单线程选项的行为。如果对选择了 cache-aside 对象管理选项的对象进行了更改，则首先执行所需的数据库更新（详见第 6 章）。接下来执行缓存更新。这种顺序确保了在数据库操作成功完成之前，对象更改不会在缓存中暴露。接下来发送出站事件，然后是待处理的消息确认。最后，释放对象锁（对象锁定在第 6 章中讨论）。

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_119_0.png)

图 5-22：后处理行为——单线程

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_120_0.png)

图 5-23：后处理行为——多线程

图 5-23 显示了多线程处理的行为。所有活动并行运行，其中事件输出和缓存更新活动使用来自 `Agent.threadcount` 线程池的线程，数据库更新（如果需要）使用来自 `Agent.dbthreadcount` 线程池的线程。

## ACEPSTLocalChannel 示例

ACEPSTLocalChannel 示例说明了几个功能，包括：

-   使用两个推理代理配置处理单元
-   本地通道的使用
-   规则操作发布事件
-   预处理器函数创建和消费事件

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_121_0.png)

### 图 5-24：ACEPSTLocalChannel 示例配置

图 5-24 显示了此示例的配置。它包含一个名为 inferenceProcUnit 的处理单元，其中包含两个推理代理：testDriverInference 和 productionInference。这两个推理代理之间配置了一个本地通道。

测试驱动推理代理的存在仅仅是为了向生产推理代理提供交易事件。当示例项目在调试器中运行时，测试数据被直接馈送到测试驱动推理代理的工作内存中。测试数据包含 SourceTransaction 事件，这些事件触发源交易规则（清单 5-3）。规则操作使用传入事件中的数据创建 Transaction 事件，并将该事件发送到其默认目的地，该目的地与本地通道关联。这导致新创建的事件被发送到生产推理代理。

### 清单 5-3：源交易规则

```
rule Rules.SourceTransaction {
    attribute {
        priority = 5;
        forwardChain = true;
    }
    declare {
        Events.SourceTransaction sourceTransaction;
    }
    when {

}
then {
        // Create the real transaction to drive
            the test
        Events.Transaction newTransaction =
            Events.Transaction.Transaction(
                null,
                null,
                sourceTransaction.accountNumber,
                sourceTransaction.
                    transactionAmount,
                sourceTransaction.
                    transactionDateTime);
        Event.sendEvent(newTransaction);
    }
}
```

Transaction 事件到达生产推理代理。与本地通道关联的目的地配置了 newTransaction 规则函数（清单 5-4）作为此事件的预处理器函数。此函数接收传入的交易，并确定其金额是低于 5 美元阈值还是高于 10,000 美元阈值。如果低于 5 美元阈值，则创建并断言 TinyTransaction；如果大于 10,000 美元，则创建并断言 GiantTransaction。在所有情况下，它都会消费原始交易。

### 清单 5-4：*newTransaction* 规则函数

```
void rulefunction RuleFunctions.newTransaction {
    attribute {validity = ACTION;}
    scope {Events.Transaction transaction; }
    body {
        if (transaction.transactionAmount <= 5.00) {
            TinyTransaction tinyTransaction =
                Events.TinyTransaction.TinyTransaction(
                    null,
                    null,
                    transaction.accountNumber,
                    transaction.transactionAmount,
                    transaction.transactionDateTime);
            System.debugOut("Created tiny transaction:
                " + tinyTransaction@id);
            Event.assertEvent(tinyTransaction);
            System.debugOut("Asserted tiny transaction:
                " + tinyTransaction@id);
        }
        else if (transaction.transactionAmount >=
            10000.00) {
            GiantTransaction giantTransaction =
Events.GiantTransaction.
    GiantTransaction(
        null,
        null,
        transaction.accountNumber,
        transaction.transactionAmount,
        transaction.transactionDateTime);
    System.debugOut("Created giant transaction: " + giantTransaction@id);
    Event.assertEvent(giantTransaction);
    System.debugOut("Asserted giant transaction: " + giantTransaction@id);
}
System.debugOut("About to consume transaction: " + transaction@id);
Event.consumeEvent(transaction);
System.debugOut("Consumed transaction: " + transaction@id);
}
```

此预处理器函数做了两件事：它既对交易进行分类，又对交易进行过滤。通过对交易进行分类，它向规则清楚地表明哪些交易低于较低阈值，哪些交易高于较大阈值。它还过滤交易：任何介于两个阈值之间的交易都会被直接消费。

对 tiny 和 giant 交易（配置了 1 小时的生存时间）进行断言会触发新版本的欺诈规则（清单 5-5）。该规则仅比较账户号并确定交易发生的顺序。关于每个交易是低于较低阈值还是高于较高阈值的判断已在预处理器中完成。此外，事件只会存在一个小时，因此无需确定交易的时效。

### 清单 5-5：ACEPSTLocalChannel 欺诈规则

```
rule Rules.Fraud {
    attribute {
        priority = 5;
        forwardChain = true;
    }
    declare {
        Events.GiantTransaction giantTransaction;
        Events.TinyTransaction tinyTransaction;
    }
    when {
        tinyTransaction.accountNumber ==
            giantTransaction.accountNumber;
        giantTransaction.transactionDateTime >
```

转换规则可以具有与常规推理代理规则关联的相同类型的操作。此外，可以指定在进入状态和退出状态时执行的操作。一种可能的操作类型是启动或停止另一个状态机。

## 超时

状态可以具有与之关联的超时。计时器在进入状态时启动。如果在状态退出之前计时器到期，则执行指定操作，并且状态机转换到指定状态。

尽管状态机启动了计时器，但计时器本身不是状态机的一部分。每个计时器都是一个对象，默认情况下以仅缓存模式运行，并保存到后备存储（如果进行了相应配置）。

集群中的一个推理代理（自动确定）运行调度程序。调度程序定期检查计时器以查看哪些已过期，并执行与超时关联的状态机逻辑。请注意，此超时事件不会经过预处理器，但仍然可能需要锁定才能安全地执行逻辑。为了支持这一点，可以注册状态机超时回调，其作用与预处理器函数相同。当超时事件需要锁定（或其他预处理器功能）时，必须定义并注册必要的函数。_TIBCO BusinessEvents 数据建模开发人员指南_ 提供了详细信息。

## 启动和停止状态机

每个概念都可以有一个与之关联的主状态机。默认情况下，此状态机配置为在概念创建时自动启动。作为例外，可以使用目录函数 `startStateMachine()` 启动状态机。

有关状态机的更多信息，请参阅 _TIBCO BusinessEvents 数据建模开发人员指南_。

