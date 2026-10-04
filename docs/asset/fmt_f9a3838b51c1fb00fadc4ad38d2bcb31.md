
# 临时排序路由算法（TORA）

临时排序路由算法（TORA）是一种源自触发的分布式路由方案，具有与自旋模型的某些属性。它建立了一个相对于数据汇点具有高度度比指标的无环图，并且对拓扑扰动有局部反应 [Royer 99]。

我们自旋玻璃模型中的动力因子以及蚁群费素模型中蚂蚁产生的频率，为系统提供了在各种条件下控制行为的灵活性。自旋玻璃模型的路由维护开销中等。

多重分形方法作为一种概率空间填充曲线，具有非常轻的计算和通信负载，并在路由发现和维护中节省了开销。这是以增加数据汇点距离为代价的。由于参与每个路径的节点数量减少，费素的路由维护开销很低。由于多重分形模型力求使用尽可能少的单元来覆盖区域，稀疏路由树节省了能量。使用多重分形无法找到到数据汇点的最短路径。

另一方面，自旋玻璃模型对任何可能扩散整个网络的内部错误都更敏感。多重分形和蚁群费素模型对内部错误非常有抵抗力。蚁群费素算法收敛到所需状态的时间比其他两种适应长得多。对于需要短数据路径的应用，首选自旋模型。对于需要快速部署且开销敏感的应用，多重分形模型是更好的选择。如果错误恢复和低开销是主要需求，那么蚁群费素模型是合适的。混合方法或在不同阶段切换方法可能是有效的。

## 致谢与免责声明

本研究由国防高级研究计划署（DARPA）资助，由陆军研究办公室根据紧急监控项目 MURI 资助号 DAAD19-01-1-0504 进行管理。它还由空军研究实验室、美国空军材料司令部、美国空军（USAF）根据协议 F306 资助。本研究涉及的任何观点、发现或结论不代表资助机构的官方立场或认可。

# 参考文献

- [AC299] 自适应模型，交付给 DARPA 的技术报告，1999。
- [Adam 98] 混沌，Springer，纽约，1998。
- [Allgood 96] 分布式概率数据分布，《动力学系统引言》，1996。
- [Akyildiz 01] 匿名传播：改进无线网络的可靠性，分布式计算国际会议，美国，2001。
- [Bonabeau 97] 涌现行为，圣费基学院工作论文，1997。
- [Brooks 91] 现代控制，Prentice Hall，纽约，1991。
- [Brooks 98] 分布式传感器网络，IEEE Network，124(1),28–35,1998。
- [Brooks 00] 分布式传感网络，IEEE 系统系统。
- [Brooks 2000a] 分布式传感器的自组织性，宾法立大学，2000。
- [Brooks 2000b] 分布式传感器的动态链接，智能 研讨会，2000。
- [Brooks 2000c] 分布式传感网络，宾法立大学，2000。
- [Camazine 01] 涌现，《生物系统》，普林斯顿大学，2001。
- [Cebrowski 98] 网络中心战：起源与未来，《IEEE Network》，1998。
- [Chandra 01] 匿名传播，第21届分布式计算会议，美国，275–84，2001。
- [Chang 86] 分布式传感器网络的联合概率数据分布，《自动控制汇》，AC-31,889–897,1986。
- [Chang 99] 多单元组织的中心化与去中心化：零售链的多智能体模型，圣费基学院工作论文，1999。
- [Di Cao 96] G. Di Cao and M. Dorigo, AntNet: A mobile agents approach to adaptive routing, Technical Report IDRIA/9712, Université de Bruxelles, Brussels, Belgium, 1997.
- [Dorigo 1996] M. Dorigo, V. Manizzo, and A. Coloni. The ant system: Optimization by a colony of cooperating agents, IEEE Transactions on Systems, and Cybernetics-Part B, 26(1), 29–41, 1996.
- [Eigen 1982] M. Eigens, Ursprung und Evolution des Lebens auf molekularer Ebene, in *Evolution of Order and Chaos*, H. Haken (ed.), pp. 6–23. Springer-Verlag, Berlin, Germany, 1982.
- [Fitzpatrick 2002] R. Fitzpatrick, Lecture notes of Introduction to Computational Physics, 2002.
- [Gaylord 96] R. J. Gaylord and K. Nishitate, Modeling Natural Cellular Automata with Mathematica, Springer-Verlag, New York, 1996.
- [Gottasch 2000] T. Gottasch and D. Davis, Hotspot Project, Center for Advanced Computing Research at Caltech, Pasadena, 2000.
- [Grosshauser 1999] M. Grosshauser and J.-C. Bolot, On the relevance of range-dependent metric in network traffic, IEEE Transactions on Networking, 7(5), 629–640, 1999.
- [Haas 02] Z. Haas, J. Halpern, and L. Li, Gissip-based on hot routing, Proceedings of the IEEE INFOCOM, New York, 2002.
- [Haberman 1998] R. Haberman, Mathematical Models: Population Dynamics, and Traffic Flow, SIAM, Philadelphia, PA, 1998.
- [Hagen 1990] H. Haken, Application of synergetics to pattern formation and pattern recognition, *Self-Organization, Emerging Properties and Learning*. NATO Series B: Vol. 260, p. 21–30, Plenum Press, New York, 1991.
- [Haken 1987] H. Haken, Synergetics: An Introduction, Springer-Verlag, Berlin, 1978.
- [Haken 1983] H. Haken, Synergetics, Springer Verlag, Berlin, Germany, 1983.
- [Holroyd 02] H. Brochmann, Introduction to fractal geometry, http://www.saltbrug.com/brochmann/math/Fractals-fractal.html
- [Hopcroft 1979] J. Hopcroft and J. D. Ullman, Introduction to Automata Theory, Languages, and Computation, Addison-Wesley, Reading, MA, 1979.
- [Jensen 98] J. Jensen, Self-Organized Criticality, Cambridge University Press, Cambridge, U.K., 1998.
- [Karp 00] B. Karp and H. T. K. Ung, Greedy parameter stateless routing for wireless networks, Proceedings of the Sixth ACM/IEEE International Conference on Mobile Computing and Networking, Boston, MA, August 6–11, 2000.
- [Kaussmann 1993] S. Kaufmann, Origins of Order, Oxford University Press, New York, 1993.
- [Kemp 01] D. Kemp, M. Klein, and A. J. Demers, Spanish gossip and resource location protocols, Proceedings of 33rd Annual ACM Symposium on Theory of Computing, 162–172, 2001.
- [Kott 99] A. Kott and B. B. Krug, Toward a catalog of pathological behaviors in complex enterprise systems, Proceedings from November 1999 DARPA-JFACC Symposium on Advances in Enterprise San Diego, CA, pp. 1–6, November 15–16, 1999, http://www.darpa.mil/iso/jfacc/symposium/sess-2.
- [Kuros 03] J. E. Kuros and K. W. Ross, Networking: a top-down approach featuring the Internet, AI Higher Education Group, division of Pearson Education, 2003.
- [Leland 94] Y. E. Leland, M. S. Taququ, and D. V. Wilson, On the self-similar nature of Ethernet traffic (extended version), IEEE/ACM Transactions on Networking, 2(1), 1–15, 1994.
- [Li 93] Y. Li and W. M. Wonham, Control of vector discrete event systems–The base model, IEEE Transactions on Automatic Control, 38(8), 1224–1227, 1993.
- [Li 94] Y. Li and W. M. Wonham, Control of vector discrete event systems I–Controller systems, IEEE Transactions on Automatic Control, 39(3), 512–531, 1994.
- [Major 01] J. A. Major and Y. Lantsman, Part 1 Actuarial application of multifractal modelling, 2001.
- [Nicolas 77] G. Nicolis and I. Prigotine, Self-Organization in Non-Equilibrium Systems, Wiley, New York, 1977.
- [Pandaya 1996] A. Pandya, Rough sets for Intelligence, CRC Press, Boca Raton, 1996.
- [Parunak 99] H. Parunak and S. Bruecker, Synthetic pheromones for distributed control, JFACC Symposium on Advances in Enterprise San Diego, CA, November 1999.
- [PBS 96] Online Newshour, July 3, 1996, http://www.pbs.org/newshour/blackout-7-3
- [Phoa 1999] S. Phoa, R. Horn, A constructivist theory for complex dynamics, Symposium on Enterprise, San Diego, CA, November 1999.
- [Phoa 2000a] S. Phoa, N. Gautam, Tactical intelligence for agile operations, Second Symposium on Enterprise, Minneapolis, MN, July 2000.
- [Phoa 2000b] S. Phoa, E. Peluso, and R. L. Culver, A high fidelity AOSN for networked assets, invited paper, special issue of the IEEE Journal of Ocean Engineering, 26(4), 646, 2000.
- [Portugoli 2000] J. Portugoli, Self-Organization and the City, Springer-Verlag, Berlin, 2000.
- [Preston 84] K. Preston, and J. M. Buff, Modern Automata Theory and Applications, Plenum Press, New York, 1984.
- [Rai 1990] S. Rai and D. P. Agrawal, edges in Distributed System Reliability, IEEE Computer Society, Los Alamitos, CA, 1990.
- [Royer 99] E. Royer, A review of routing protocols, IEEE Communication, 6(2), 46–55, 1999.
- [Rudie 1992] R. Rudie, Decentralized control, IEEE Automatic Control, 37(1), 1692–1708, 1992.
- [Sarkar 2000] P. Sarkar, Energy distribution, IEEE Surveys, 2000.
- [Siewk 1982] D. Siewk, Robust design, Digital Press, 1982.
- [Smulders 1991] S. Smulders, Traffic of, CWI, Amsterdam, 1991.
- [Swanson 2000] D. Swanson, Intelligence discovery, San Francisco, CA, 2000.
- [Tsapsintos 1997] D. Tsapsintos, Rough sets for, Intelligence, 8(1), 203–223, 1997.
- [Tsumoto 1998] S. Tsumoto, Discovery of, International Conference on, Anchorage, AK, pp. 1296–1301, 1998.
- [Tymbal 1998] A. Tymbal, Collective intelligence for, Symposium on, San Diego, CA, pp. 50–54, 1998.

# 618 传感器网络与应用

## 自组织化

## 28.1.2 信息的素

一种让昆虫在各种任务中表现良好的重要集体行为机制被称为信息素。信息素是一种通过环境进行的间接通信形式。信息素有以下形式：

- 第一种形式：环境的物理特征可能是执行某些任务相关操作的结果，例如蚂蚁挖掘洞，或者白蚁在正在生长的结构上添加一个泥球。对变化环境的后续感知可能会导致下一只蚂蚁放大洞，或者导致白蚁将它的泥球沉积在之前的结构上。这种影响被称为符号信息（sematectic）[Bonneau'94]。
- 第二种形式：通过堆留某些东西来改变环境，这些东西对任务没有直接贡献，但仅用于影响行为，这是一种基于信息的信息素，在蚂蚁和其他社会性昆虫中高度发育。蚂蚁使用一种名为费洛蒙（pheromone）的特殊激素来提供一种复杂的信号系统。

## 28.1.3 蚂蚁追踪

如前所述，蚂蚁在寻找食物或返回巢穴时具有留下费洛蒙足迹的奇特性。蚂蚁根据足迹的强度被费洛蒙沉积物吸引。费洛蒙是一种激素，会挥发并扩散到大气中。在任何时刻，另一只蚂蚁遇到的足迹强度都是原始足迹强度和自足迹铺设以来时间的函数。

图 28.1 显示了巢穴和食物源之间多种可能的路线。最初，到达汇路口的蚂蚁做出随机决定，选择其中一条路线相对于另一条路线的概率为 0.5。现在让我们假设这对蚂蚁选择了不同的路线。

一段时间后，选择较短路径的蚂蚁首先到达目的地，情如图 28.2 所示。我们看到，较短路径上的费洛蒙浓度高于长路径。下一个到达汇路口的蚂蚁将选择较短路线的到达目的地的概率更高。

![](img/11e8580124e6543d23c6c1d715727b6a_1399_0.png)

图 28.1 蚂蚁必须做出决定。

![](img/11e8580124e6543d23c6c1d715727b6a_1399_1.png)

图 28.2 蚂蚁铺设费洛蒙足迹。

这一过程增强了较短路线上的费洛蒙浓度，导致更多蚂蚁通过较短路线。随着通过较短路径的蚂蚁减少，且现有的费洛蒙缓慢挥发，长路径上的足迹会变弱并最终消失。

在寻找最优路径的过程中存在一种强化学习。过度训练会引起两个问题：

- 阻塞问题（Blocking problem）：当蚂蚁之前发现的路线不再可用时发生这种情况。蚂蚁需要时间来寻找新路线，因为通往阻塞路线的足迹有时非常强。
