

## 数据包处理架构

Intel Xeon Phi 协处理器为 HFT 和上述描述的行情处理系统等大量 * embarrassingly parallel * 应用提供了一种通用解决方案。它提供了一个功能强大、通用的计算平台，包括：

- 大量缓存一致的核心和线程，可最优地处理许多独立的 *streams* 工作
- 通过 512 位宽向量而非更窄的 MMX、SSE 或 AVX2 能力实现的独特宽 SIMD 能力
- 对执行倒数、平方根和指数运算的指令提供高性能支持，为蒙特卡洛相关应用提供了理想环境。
- 大量的可用内存带宽。
- 主机与系统上所有附属协处理器之间高效的、从带宽和延迟角度来看都高效的通信管道，即 PCIe 总线。

该问题可分解为如图 7.2 所示的 *packet processing* 问题。一个或多个主机线程通过套接字连接从外部源接收数据包，例如

![](img/16cb41208935c5f22dd1044f03f2e31b_143_0.png)

## 图 7.2

利用协处理器的通用数据包处理应用。

市场数据，通过标准网络接口（NIC）。主机线程将数据包，全部或仅相关部分，排队到单独的 FIFO 中以供进一步处理。在图中，FIFO 位于协处理器上的 GDDR 内存中，这一选择将在本章后面解释。协处理器侧的亲和线程在核心上运行，按接收顺序处理其 FIFO 上接收到的每个数据包，并将数据包通过行情处理算法。算法的结果随后被复制回 FIFO，如图 7.2 中所示位于主机上，以供进一步处理。该架构的衡量指标涉及平均和最坏情况下的延迟，以每个数据包 p 的往返时间（RTT）衡量。在行情处理器的情况下，最坏情况的延迟预计出现在交易日开始时交易所开盘时，以及交易日结束时临近收盘时。虽然预计由一连串数据包组成、背靠背且几乎没有或没有数据包间间隔的突发会导致备份从而增加 RTT，但对这种系统的期望是，最坏情况 RTT 是有良好界限的（无抖动），并且最好接近平均 RTT。本章的其余部分重点介绍几种满足该要求的优化技术。

示例代码提供了一个简单的数据包处理应用，包含客户端和服务器（packet_processing/scif_connect_rbuf.cpp 和 packet_processing/scif_accept_rbuf.cpp）。本章后面描述的优化已用于优化数据包处理示例应用。

## 对称通信接口

Intel® 多核平台软件栈（Intel® MPSS）的高级架构如图 7.3 所示，其中包括对称通信接口（SCIF）驱动程序和库，应用程序链接这些库以获得其服务。SCIF 在两个对等进程之间提供高效的节点间通信。在此定义中，节点是 Intel Xeon 处理器或 Intel Xeon Phi 协处理器。

SCIF 抽象了 PCIe 总线上通信的细节，并提供了一个与 Berkeley Sockets API 非常相似的接口。在此模型中，应用程序相互连接（对等端点）并使用 SCIF API 执行数据传输操作。SCIF 的一个重要属性，如其名称所示，是对称性；SCIF 驱动程序和库在 PCIe 总线两侧呈现相同的接口。建立连接的过程与套接字 API 非常相似，其中一侧监听（scif_listen()）并接受（scif_accept()）传入连接，而另一侧连接到（scif_connects()）远程进程。

作为入门，图 7.4 和 7.5 提供了使用 SCIF 的简单客户端/服务器应用示例，演示了连接建立过程。

最后，SCIF 提供了几类 API 用于：

- 连接管理
- 消息传递
- 内存注册
- 远程内存访问（用于批量传输和低延迟访问）

SCIF API 集相当小，大多数应用程序会使用整个集合。本章的重点是用于主机和协处理器之间低延迟数据传输的有用 API。

![](img/16cb41208935c5f22dd1044f03f2e31b_145_0.png)

## 图 7.3

Intel® 多核平台软件栈（Intel® MPSS）显示 SCIF 驱动程序和用户模式库。

## 内存注册

每个进程都有一个虚拟地址空间（VAS）。该空间中的虚拟地址（VAs）在线程对该进程进行读或写访问时由操作系统通过物理页支持。SCIF 引入了注册地址空间（RAS）的概念。该地址空间是稀疏的，只有通过 scif_register() 由应用程序注册的特定范围，称为注册窗口或窗口，在建立连接后才能被进程的远程对等方访问。图 7.6 显示了进程的物理、虚拟和 RAS 之间的关系。一组物理页（P）支持由 RAS 中的窗口偏移（W）引用的虚拟范围（V）。值得注意的是，主机处理器和所有协处理器上的物理和 VAS 只能由本地运行的进程访问。然而，RAS 允许进程在远程进程的上下文中访问支持它的物理内存。

换句话说，使用 scif_register() 标记一段内存区域可供远程访问。它接受一个页对齐的 VA 和长度参数（以及一些标志）并返回一个表示进程 RAS 中窗口的偏移量。可选地，偏移量可以由应用程序选择并作为输入提供给 scif_register()，方法是指定 SCIF_MAP_FIXED 标志。物理页

```
/* open end point */
if ((epd = scif_open()) == SCIF_OPEN_FAILED) {
        printf("scif_open failed with error %d\n", errno);
        exit(1);
}

/* bind end point to available port, generated
 * dynamically
 */
if ((conn_port = scif_bind(epd, 0)) < 0) {
        printf("scif_bind failed with error %d\n", errno);
        exit(1);
}
printf("bind success to port %d\n", conn_port);

/* initiate a connection to remote node, when
 * successful returns the peer portID. Re-tries
 * for 20 seconds and exits with error message
 */
__retry:
    if (scif_connect(epd, &portID) < 0) {
        if ((errno == ECONNREFUSED) && (tries > 0)) {
                printf("connection to node %d failed : trial %d\n", portID.node, tries);
                tries--;
                sleep(1);
                goto __retry;
        }
        printf("scif_connect failed with error %d\n", errno);
        exit(1);
    }
    printf("connect success\n");
```

**图 7.4**  
SCIF 连接的客户端侧（在 connection/scif_connect_register.c 中）显示了连接建立的基本 SCIF API。

```
/* open end pt */
if ((epd = scif_open()) == SCIF_OPEN_FAILED) {
        printf("scif_open failed with err %d\n", errno);
        exit(1);
}

/* bind end pt to specified port */
if ((conn_port = scif_bind(epd, PORT_NO)) < 0) {
        printf("scif_bind failed with error %d\n", errno);
        exit(1);
}
printf("bind success to port %d\n", conn_port);

/* marks an end pt as listening end pt and queues
 * up a maximum of BACKLOG no: of incoming connection
 * requests
 */
if (scif_listen(epd, BACKLOG) != 0) {
        printf("scif_listen failed with error %d\n", errno);
        exit(1);
}

/* accepts a conn request by creating a new end pt
 * that connects to peer
 */
if (scif_accept(epd, &portID, &newepd,
SCIF_ACCEPT_SYNC) != 0) {
        printf("scif_accept failed with error %d\n", errno);
        exit(1);
}
printf("accept success\n");
```

## 图 7.5

SCIF 连接的服务器侧（在 connection/scif_accept_register.c 中）显示了连接建立的基本 SCIF API。

