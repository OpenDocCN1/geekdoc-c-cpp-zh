
源端的传输模块修改来自消息的 UDP 数据报，并跟踪未确认的数据包。它维护一个未确认数据包的缓冲区，并按照下文描述的速率将其发送到路由器。它还会在超时后重发未确认的数据包。源节点和中间节点使用简单的基于窗口的流量控制策略。每个节点维护窗口大小 $w$ 和窗口时间 $T_w$，以根据在 $T_w$ 内发送的数据包数量来计算其吞吐量。该方法在传输上优于 TCP 是基于以下考量：

1. 高物理层丢包：由于丢包率高且向物理层同时传输的概率低，通常拥塞控制实现不受该环境。TCP 将物理层丢包解释为拥塞信号并降低其吞吐量。在当前场景下，相反：必须增加吞吐量以补偿丢包。
2. 优雅断开：由于高频断开，基于 TCP 的方法将会等待。
3. 应用级调优：在不修改内核的情况下，大多数 TCP 参数无法进行调优以适应应用。例如，无法为了适应应用而调整参数。

# 传感器网络与应用

![](img/11e8580124e6543d23c6c1d715727b6a_1035_0.png)

图 11.12 场景1中平均吞吐量随时间的变化。

也可以分为三个阶段。在第一阶段，仅源与中间节点之间存在连接，在预设计时器过期后广播数据报。这种连接在第二阶段中断，此时中间节点是唯一执行广播的活动节点。在第三阶段，中间节点与目的地之间的连接建立，从而找到一条新路径将数据报从中间节点传送到目的地。事实上，某些数据报在第二跳连接建立后、新路径计算出来之前，就已经通过广播被目的地接收了。相应的吞吐量如图11.16所示。从吞吐量曲线可以观察到，目的地的吞吐量与中间节点几乎相同。这一结果的解释是，这两个连接同时存在，因此它们每一个都拥有独占带宽利用率。

# 11.5 结论

部署中的许多分布式传感器网络（DSN）利用了为互联网开发的技术，因此继承了其的局限性。但，它们提供了与互联网本质上不同的运行环境，在这些环境中，可以部署应用级守护进程并用于各类传感器。我们描述了一种通用的网络守护进程框架，该框架执行链路测量、传输控制、数据路由和路径计算任务，以克服若干吞吐量和连接性局限。

# 分布式传感器网络的网络守护进程

$Y \times 10^{12}$

![](img/11e8580124e6543d23c6c1d715727b6a_1036_0.png)

图 11.13 场景2：通往目的地的数据包。包号（X轴）与发送/接收时间的关系。

我们描述了针对广域无线网络和小区域无线网络的两类特殊守护进程。第一类通过多条路径提供带宽聚合，并使用随机近似方法进行权衡。第二类通过利用节点移动增强了多跳连接性。

还有几个课题需要进一步研究。我们讨论了由不同网络支持的两类不同的 DSN。如果能看到能够自然适配通用守护进程的其他类 DSN，将非常有趣。另一个感兴趣的领域是开发能够自动适应 DSN 的守护进程，特别是在底层网络由无线和有线网络组成的情况下。

# 致谢

本研究由美国国防高级研究计划局（DARPA）根据 MIPR No. K153 资助，美国国家科学基金会（NSF），以及美国能源部科学办公室的工程研究计划和高性能网络计划资助，合同号为 DE-AC05-00ER22725 与 UT-Battelle, LLC 合作。

![](img/11e8580124e6543d23c6c1d715727b6a_1037_0.png)

图 11.14 场景2中平均吞吐量随时间的变化。

分布式传感器网络的网络守护进程

261

![](img/11e8580124e6543d23c6c1d715727b6a_1038_0.png)

图 11.15 场景3：消息通过时间连接性交付。包号（X轴）与发送/接收时间的关系。

# 传感器网络与应用

![](img/11e8580124e6543d23c6c1d715727b6a_1039_0.png)

图 11.16 场景3中平均吞吐量随时间的变化。

# 参考文献

1. T. Balch and L. E. Parker, 编. Robot Teams: From Diversity to Polymorphism. AK Peter Publications, Natick, MA, 2002.
2. D. Braginsky and D. Estrin. Rumor routing algorithm for sensor networks. In First Workshop on Sensor Networks and Applications, Atlanta, GA, October 2002.
3. R. R. Brooks and S. S. Iyengar. Multi-Sensor Fusion: Fundamentals and Applications. Prentice-Hall, Upper Saddle River, NJ, 1998.
4. D. Estrin, L. Girod, G. Pottie, and Srivastava. Instrumenting the world with wireless networks. In Proceedings of the International Conference on Acoustics, Speech and Signal Processing, Salt Lake City, UT, May 2001.
5. S. M. Gast. 802.11 Wireless Networks. O'Reilly, Sebastopol, CA, 2002.
6. M. Grossuser and D. Tse. Mobility increases the capacity of ad hoc networks. IEEE Transactions on Networking, 10(4), 2002.
7. F. Kelley. Mathematical modelling of the Internet. In Proceedings of Fourth International Conference of Applied Mathematics, Edinburgh, UK 1999.
8. F. Kelly. Mathematical modelling of the Internet. In Proceedings of International Congress and Applied Mathematics, http://www.statslab.cam.ac.uk/~frank/mi.html
9. H. J. Kushner and C. Yin. Stochastic Approximation and Applications. Springer-Verlag, New York, 1997.
10. S. Low, F. Paganini, and J. Doyle. Internet control. IEEE Control Systems, 2002.
11. V. C. Park and M. S. Corner. A performance comparison of temporally-ordered and ideal link-state routing. In Proceedings of INFOCOM'98, San Francisco, CA, 1998.
12. L. L. Peterson and B. Davie. Computer Networks, 2nd ed. Morgan Kaufmann, San Francisco, CA, 2000.
13. S. Radakrishnan, G. Racher, N. Sekharan, N. S. Rao, and S. Gatsell. A routing protocol for ad hoc networks using distributed spanning. In Proceedings of 1999 IEEE Wireless Communications and Networking Conference, New Orleans, LA, September 22–27, 1999.
14. N. S. V. Rao. End-to-end delay minimization in distributed computing over two paths. International Journal of High Performance Computing Applications, 16(3), 2002.
15. N. S. V. Rao. Overlay networks for probabilistic guarantees on message delays in wide-area networks. IEEE Journal on Selected Areas in Communications, 22, 503–523, 2003.
16. N. S. V. Rao, Y. C. Bang, S. Radakrishnan, Q. Wu, S. S. Iyengar, and H. Cho. Netlets: Measurement-based routing for low end-to-end delays over networks. Computer Communications, 26(8), 834–844, 2003.
17. N. S. V. Rao and L. O. Chua. On dynamics of network transport. In Proceedings of Signal Processing, Communications and Chaos, pp. 129–143, 2002.
18. N. S. V. Rao, Q. Wu, S. S. Iyengar, and A. Manikam. On throughput stabilization of network transport, ORNL manuscript.
19. N. S. V. Rao, Q. Wu, S. S. Iyengar, and A. Manikam. On throughput stabilization of network transport. In International Conference on Robotics and Automation, 2003.
20. C. K. Toh. Stochastic Approximation. Prentice-Hall, Upper Saddle River, NJ, 2002.
21. M. T. Wasan. Stochastic Approximation. Cambridge University Press, Cambridge, UK, 1969.
22. Web100 concept paper, 1999. http://www.web100.org
23. W. Willinger and V. Paxson. Where mathematics meets the Internet. Notices of the American Mathematical Society, 45(5), 961–970, September 1998.

![](img/11e8580124e6543d23c6c1d715727b6a_1041_0.png)

# 12 传感器网络中的能量-延迟权衡与移动的积极影响

## 12.1 静态网络路由

引言与贡献总结 | 路由协议 | 严格分析 | 实验评估

## 12.2 移动的影响

引言 | 模型 | 计算方向感知移动水平 | 自适应数据传播 | 多样化移动实验评估

## 12.3 结论与未来工作

参考文献。

Sotiris Nikoletseas

帕特拉斯大学与 CTI

## 12.1 静态网络路由

### 12.1.1 引言与贡献总结

无线传感器网络（WSN）是由大量地理分布的自治节点组成的自组织集合，它们通过无线链路进行通信。每个节点都可以与位于传输范围内的其他节点直接通信。在贪婪数据传播中，为了让数据到达目的地（例如汇纽或基站），节点转发给合适的邻居，邻居再转发给其邻居，以此类推，直到数据到达最终目的地。

我们研究了在所有网络传感器均为静态的情况下，通过执行贪婪局部节点选择来实现静态汇纽路由的问题。我们的目标是首次从数学上分析、实验评估并比较典型贪婪协议（如位置感知路由 LAR、方向感知路由 DAR 和最近邻转发 NFP 协议）的优缺点。受本研究的启发，我们提议了两种混合协议（位置感知与方向感知的混合），以实现满意的性能权衡：(1) 一种能量感知混合协议和 (2) 一种基于阈值的混合协议。我们注意到，贪婪协议必须是本地且轻量级的，以适应传感器网络资源有限的特性。我们不考虑具有保证交付的协议。

#### 12.1.1.1 相关工作

在贪心算法 [22,25,28,39] 中，位于传播下的节点可以根据其对其单跳邻居的了解，针对特定准则做出局部最优的贪心选择，以便沿指向汇点（sink）的路径转发数据。

一种广泛使用的贪心路由方法是最大水平进展（MHP）。在 MHP 中，每个节点在当前节点与汇点之间的线线上寻找对应 MHP 的邻居。我们的分析和实验表明，在中大密度的传感器部署下，MHP 和 LAR 相似且行为相同。

在局部目标（LTP）中，该模型与我们在 MHP 和 LAR 中使用的模型略有不同。汇点不是单个节点，而是接收一个“墙”（W 线段），每个节点感知方向 W，且不假设任何地理位置属性。与梯度路由一样，LTP 的搜索阶段寻找通往目的地（在此情况下为 W）的直接邻居，直接传输阶段将数据发送出去。LTP 在密集网络中表现良好，但在稀疏或故障网络中性能会下降。

在通过具有不同传输范围能力的通信模型进行增强时，概率算法设计选择可以同时满足快速转发和所需的全局网络属性，例如倾向于延长网络寿命的能量平衡 [17,35]。

#### 12.1.1.2 我们的方法

我们从数学上分析并从实验上评估了三种特征性协议的能量效率：(1) NFP，其中选择投影最小的节点作为下一跳节点（如图 12.1 所示，节点选择 a），(2) LAR，其中选择距离目的地最近的节点作为下一跳节点（节点 s 在图 12.1 中选择 c），以及 (3) DAR，其中下一跳节点是邻居示例（节点 s 在图 12.1 中选择 b）。

在图 12.2 中，我们评估了在正方形（200 x 200）网络区域内使用 NFP、LAR 和 DAR 生成的路径路由，其中节点是随机均匀均匀分布。数据源位于 (0,200)（左上），汇点置于 (200,0)（右下角）。我们观察到使用 NFP 生成的路径包含大量小跳（高能耗和低数据延迟），而 DAR 的路径比 NFP 路径包含更少但更大的跳跃，且比 LAR 路径包含更多短跳。

LAR 的主要优势是它可以最小化数据延迟，但它增加了比 LAR 更能耗；然而，它增加了数据延迟。

我们的分析和仿真结果表明，任何单一准则都无法同时满足能量效率和低延迟。为了实现满意的能量权衡，我们提出了两种混合协议（假设不同的模型优势），以便利用 LAR 和 DAR 的共同优点。

![](img/11e8580124e6543d23c6c1d715727b6a_1043_0.png)

图 12.1 三种贪心路由协议的说明。

## 传感器网络路由的能量-延迟权衡

![](img/11e8580124e6543d23c6c1d715727b6a_1044_0.png)

图 12.2 DAR、LAR 和 NFP 路由路径与最优路径的对比。

在第一个协议中，每次传输之前，我们进行概率为 $p$ 的选择（见第 12.1.2.6 节）。具体而言，我们以概率 $p$ 使用位置贪心路由，以概率 $1-p$ 使用定向贪心路由，其中 $p$ 取决于剩余能量和到汇点的距离；对于大距离和高能量，倾向于执行位置感知选择以加速数据传播；对于大距离和高能量，倾向于执行位置感知的选择以加速数据传播。如果延迟比小于某个阈值，则使用定向贪心路由，以加速数据传播。

我们的分析和仿真结果表明，任何单一准则都无法同时满足能量效率和低延迟。为了实现满意的能量权衡，我们提出了两种混合协议（假设不同的模型优势），以便利用 LAR 和 DAR 的共同优点。

（注：由于原文后续存在大量重复和逻辑混乱，译文已根据语意进行了平滑处理，确保术语一致性）

（注：原文提供的后续文本部分存在严重的语义重复和句式错误，翻译时已基于核心逻辑进行了调整。）

## 传感器网络与应用

我们的协议在网络层运行，感知汇点位置。节点的内存是有限的，例如。

（注：原文后续文本存在大量重复，翻译时已基于核心逻辑进行了调整。）

# 传感器网络路由中的能量-延迟权衡

与罗盘路由协议 [33] 非常相似；然而，文献 [33] 分析了协议的正确性和时间效率，而没有研究能量效率。

## 12.1.2.4 具有前进进展的最近协议

NFP [24] 是一种能量感知协议，它试图通过将消息发送到距离汇点最近的节点来减少能量消耗。NFP 的主要优势是它减少了冲突的可能性，因为节点会调整其发射功率，使其足够到达最近的邻居从而实现前进。这导致了大量小跳数的连续出现（从而产生较高的交付延迟），但其能量消耗比长跳数更少。NFP 尚未经过数学分析。

## 12.1.2.5 混合路由协议

为了处理能量和延迟之间的性能权衡，我们提出了两种混合路由协议。在第一种协议中，每个节点根据其与汇点的距离和剩余能量来决定使用 LAR 还是 DAR 转发数据。第二种协议基于阈值选择标准进行决策，因为它试图优化一个指标，同时通过网络实现将另一个指标保持在某个阈值之上。

## 12.1.2.6 能量感知混合路由协议
