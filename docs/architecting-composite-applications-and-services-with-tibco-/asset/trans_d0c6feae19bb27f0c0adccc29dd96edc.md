
## EMS 基于文件的同站点故障转移模式

使用基于文件消息存储的内置故障转移方法（图 16-9），主服务器实例和辅助服务器实例会定期交换心跳——这些消息表明主服务器处于活动状态。这些消息默认每三秒发送一次。当辅助服务器在一段时间内未收到心跳，默认十秒后，它会尝试成为主服务器。

故障转移期间发生的过程如图 16-10 所示。在正常情况下，主服务器会在其使用的消息存储文件上获取文件锁。当发生故障时（主服务器进程终止），这些锁应由文件系统释放。辅助服务器注意到主服务器的心跳缺失，获取文件锁，检索未交付的消息集，并开始为 EMS 客户端提供服务。

此设计模式需要共享文件系统，以便让两个服务器都能访问消息存储文件。这种方法的问题在于，最常见的共享文件系统 NFS 并不能可靠地释放文件锁。3 如果锁未成功释放，故障转移本身就会失败。请参阅 TIBCO® Enterprise Message Service™ 用户指南中关于容错的章节，以了解共享文件系统用作共享消息存储时必须满足的标准。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_418_0.png)

图 16-9：企业消息服务基于文件的同站点故障转移

3. 尽管 NFS V4 有能力可靠地处理文件锁，但操作系统必须正确配置以使用这些功能——大多数操作系统默认并未配置为这样做。在 Linux 上，至少磁盘挂载必须使用 nfs4 和 tcp 协议，并带 “hard” 选项（无限期重试失败的 NFS 操作），并且 nfs 和 nfslock 必须作为服务运行，并在重启后自动启动。

## EMS 基于数据库的同站点故障转移模式

一种替代方法是使用数据库而不是共享文件系统来存储未交付的消息（图 16-11）。在此模式中不存在文件锁定问题。然而，与文件系统相比，在数据库中存储和检索消息通常较慢。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_419_0.png)

图 16-11：企业消息服务基于数据库的故障转移

然后可以启动 EMS 服务器实例。根据环境不同，这可能需要几分钟。

### 持久化消息读取时间

如果存在持久化消息，辅助服务器必须在开始提供服务之前读取它们。在此过程中，从文件系统读取始终比从数据库读取更快。基于文件的读取时间可以通过将消息存储拆分到多个文件中进一步减少，这些文件将并发读取。

### 文件锁定可靠性

从 RTO 角度来看，获胜策略似乎是基于文件的故障转移——但前提是有可靠文件锁定的共享文件系统可用。不要陷入试图让 NFS V2 或 V3 工作的做法（许多团队都尝试过并失败了），如果你考虑 NFS V4，则需要确保操作系统已配置为正确使用锁定（默认情况下不会）。不可靠的文件锁定机制意味着不可靠的故障转移模式。

### 管理复杂性

从管理复杂性的角度来看，通用故障转移方法无疑是赢家。只有一个服务器配置，它既可用于数据中心内部的故障转移，也可用于数据中心之间的故障转移。客户端配置也保持不变。此外，不同类型组件之间的一致性也有好处：使用集群式故障转移的所有组件的故障转移过程管理方式相同。

## ActiveMatrix BusinessWorks 故障转移

有三种主要模式可用于实现 ActiveMatrix BusinessWorks 引擎的高可用性。这些模式无论 BusinessWorks 以独立引擎运行还是嵌入在 ActiveMatrix 节点中都可用：

- 1. ActiveMatrix BusinessWorks 延迟 JMS 确认模式
- 2. ActiveMatrix BusinessWorks 内置同站点故障转移模式
- 3. ActiveMatrix BusinessWorks 集群故障转移模式

### ActiveMatrix BusinessWorks 延迟 JMS 确认模式

当 ActiveMatrix BusinessWorks 作业通过接收 JMS 消息启动时，BusinessWorks 提供了将作业对 JMS 消息接收的确认作为作业中的显式活动选项。这使得 BusinessWorks 能够实现延迟 JMS 确认模式。

接收 JMS 消息的作业启动器必须配置为使用此模式。这是通过作业启动器的 Acknowledge Mode 参数完成的，可选择 Client、Transactional、Local Transactional 或 TIBCO EMS Explicit Client Acknowledge 模式。第 15 章中的图 15-15 详细说明了 Client、Transactional 和 Local Transactional 模式下的引擎行为，同一章中的图 15-16 详细说明了 TIBCO EMS Explicit Client Acknowledge 模式下的引擎行为。这些模式在图 16-12 中进行了汇总。

这些延迟确认模式结合 JMS 消息重递的逻辑，可用于避免工作丢失。当使用这些模式并且 ActiveMatrix BusinessWorks 引擎在作业中间因任何原因终止时，与 EMS 服务器的连接会丢失，并且该消息将立即有资格重递。如果您使用 JMS 队列在多个 BusinessWorks 引擎之间分配负载（图 11-2），则该消息将

![](img/b8d8132a583ad73d511c4c1bb92e2df7_422_0.png)

图 16-12：ActiveMatrix BusinessWorks 延迟 JMS 确认模式汇总

![](img/b8d8132a583ad73d511c4c1bb92e2df7_425_0.png)

**Figure 16-14:** *ActiveMatrix BusinessWorks 集群故障转移——故障转移前*

ActiveMatrix BusinessWorks 引擎检索其检查点文件并恢复这些作业的执行（图 16-15）。

与内置方法相比，使用集群式故障转移具有一些优势：

- 与使用数据库存储检查点相比，使用文件系统存储检查点更快。
- 所有进程启动器将继续正常工作，因为 ActiveMatrix BusinessWorks 的备份实例在同一虚拟环境中运行。
- 同一模式可用于同站点和异站点故障转移。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_425_1.png)

**Figure 16-15:** *ActiveMatrix BusinessWorks 集群故障转移——故障转移后*

## ActiveMatrix Service Bus 故障转移

有四种故障转移模式可与 ActiveMatrix 节点一起使用，所有这些模式都已描述过：

- 1. 延迟 JMS 确认模式
- 2. ActiveMatrix BusinessWorks 内置同站点故障转移模式
- 3. 同站点集群故障转移模式
- 4. 具有相同主机标识的异站点故障转移模式

### 使用延迟 JMS 确认模式

默认情况下，ActiveMatrix 节点使用延迟 JMS 确认模式。节点仅在 JMS Binding 工作线程释放时才确认 JMS 消息的接收。因此，使用该线程执行的任何活动都将在消息被确认之前完成。

然而，利用此功能需要理解 ActiveMatrix 节点的线程模型，因为 JMS Binding 工作线程可能会将工作移交给其他线程。请参阅第 15 章中的线程模型描述以了解详情。

### 使用 ActiveMatrix BusinessWorks 内置同站点故障转移模式

ActiveMatrix 节点没有 ActiveMatrix BusinessWorks 检查点的通用等价物：没有内置机制可以保存整个节点的执行状态。因此，没有通用能力可以恢复正在进行工作的任意 ActiveMatrix 节点的状态。

然而，这并不妨碍节点中的组件显式保存和恢复状态信息。例如，ActiveMatrix BusinessWorks 组件仍可使用 ActiveMatrix
