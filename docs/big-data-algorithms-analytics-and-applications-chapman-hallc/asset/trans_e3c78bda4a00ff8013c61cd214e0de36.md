
调度器的能力。遗传调度器有一个估计阶段，在该阶段会测量每个应用的处理数据速度。调度器确保，一旦某个应用开始执行，在正常条件下该应用将成功结束。Hadoop按需（HOD）[3]虚拟集群使用Torque资源管理器进行节点分配，并自动准备配置文件。然后，它基于虚拟集群内的节点初始化系统。HOD可以以相对独立的方式使用。

为支持多用户场景[14,17]，Hadoop框架集成了若干适合大数据处理的组件（图6.3），因为这些组件通过海量数据提供高可扩展性，并支持访问广泛分布的数据。以下是对这些组件的简要描述：Hadoop Common由支持任何Hadoop模块和任何新扩展的通用工具组成。HDFS提供对应用数据的高吞吐量访问。Hadoop YARN（Apache Hadoop NextGen MapReduce）是一个用于作业调度和集群资源管理的框架，可跨多个平台扩展。Hadoop MapReduce是一个基于YARN的系统，用于大数据集的并行处理。

Facebook的解决方案Corona [18]扩展并改进了Hadoop模型，提供更好的可扩展性和集群利用率、更小作业的更低延迟、无中断升级能力，以及基于实际任务资源需求而非map和reduce任务数量的调度。Corona旨在应对Facebook最重要的挑战：独特的可扩展性（最大集群拥有超过100 PB数据）和处理需求（每天处理超过6万条Hive查询）。Facebook内部数据仓库在2008年至2012年间增长了2500倍，预计到2016年还将以相同倍数增长。

![](img/1643181e79c76dc765d55a7355afb4a4_148_0.png)

图6.3 Hadoop处理与大数据平台。

![](img/1643181e79c76dc765d55a7355afb4a4_151_0.png)

图6.5 资源分配过程。

用于大数据处理的集群中的通用资源管理方法，应对纳入服务级别协议中的策略作出一些假设。例如，交互式任务、分布式与并行应用以及非交互式批处理任务都应得到高性能支持。这一特性很直接，但在某种程度上难以实现。因为任务具有不同属性，在共享环境中它们对调度器的需求可能相互矛盾。例如，需要短时间响应的实时任务偏好空间共享调度；需要高吞吐量的非交互式批处理任务可能偏好时间共享调度[6,29]。为了具备通用性，可能必须作出权衡。该调度方法聚焦于并行任务，同时为其他类型任务提供可接受的性能。

YARN有一个用于动态策略加载的可插拔解决方案，考虑资源分配过程的两个步骤（图6.5）。资源分配由YARN完成，任务调度由应用完成，这使YARN平台成为通用平台，同时仍允许调度策略具有灵活性。YARN中的具体策略面向根据应用提供的调度进行资源拆分。这样，YARN的调度器根据资源可用性和配置的共享策略，决定分配多少资源以及在哪个集群中分配资源。

### 6.6 调度优化技术

大数据平台中的调度是使数据中心更易被应用和用户群体使用的主要构建模块。优化的一个示例是Hadoop中许多任务的多目标多约束调度[30]，或用Hadoop优化短作业[31]。调度优化策略因每种模型和每种应用类型而异。最常用的调度优化技术如下：

- 线性规划使调度器能够基于已定义的约束找到合适资源或资源集群。
- *动态分区*将复杂应用拆分为任务簇，并用特定调度算法调度每个任务簇。
- *组合优化*旨在为有限资源集合找到最优分配方案。这是一种耗时技术，不推荐用于实时处理。
- *演化优化*旨在在特定约束内为特定系统找到最优配置，由特定仿生技术组成，如遗传与免疫算法、蚁群与蜂群计算、粒子群优化等。这些方法通常能为调度问题找到近优解。
- *随机优化*使用出现在优化问题本身公式中的随机变量，尤其用于具有确定性行为的应用，即正态分布（针对周期任务）或泊松分布（针对偶发任务）等。
- *面向任务的优化*考虑任务属性、到达时间（松弛优化）和频率（针对周期任务）。
- *面向资源的优化*在作出最大化资源利用率的决策时考虑完成时间约束。

### 6.7 Hadoop与大数据应用案例研究

我们可以认为，在Apache Hadoop或某个Hadoop发行版之上，可以使用生成大数据的大数据套件和调度应用。Hadoop框架适合特定的高价值、高容量工作负载[32]。通过将合适的大数据工作负载放入合适的系统来优化资源和数据管理，YARN与特定调度器（G-Hadoop [33]、MPI Scheduler、Torque等）的集成提供了一种解决方案。IBM、Oracle和Hortonworks Data Platform（HDP）开发了Hadoop的成本效益、可扩展性和精简架构，主要目标是构建一个Hadoop操作系统。Hadoop可通过集成到Hadoop框架中的相关项目用于公共/私有云，试图为以下问题提供最佳答案：为了实现成本感知云调度器[34]，应将何种类型的数据/任务迁移到公共云？

在应用开发和实现中使用并集成Hadoop的不同平台会考虑不同方面。建模是第一个方面。即使在为Hadoop集群提供基础设施的Apache Hadoop中，通过编写复杂代码来构建特定MapReduce应用仍然非常复杂。生成MapReduce代码的Pig Latin和Hive查询语言（HQL）是面向应用开发的优化语言。还支持不同调度算法和策略的集成。应用可以以图形方式建模，并生成所有所需代码。然后，在专用开发环境（Eclipse）中，大数据服务的工具链使用各种专用插件。所有代码的代码生成会自动

### 6.8 结论

过去几年，调度模型和工具经历了根本性的重新架构，以尽可能适应大规模多任务计算环境。现有解决方案的重新设计方式包括将工具拆分为多个组件，并根据每个组件的新角色和位置进行调整。工作负载和工作流序列在应用侧进行调度，然后资源管理器为执行阶段分配资源池。因此，调度对用户和提供者同时变得重要，是任何大数据科学中最优处理的最重要关键。

## 参考文献

- 1. M. D. Assuncao, R. N. Calheiros, S. Bianchi, M. A. Netto, and R. Buyya. 大数据计算与云：挑战、解决方案与未来方向. arXiv preprint arXiv:1312.4722, 2013. 可访问：http://arxiv.org/pdf/1312.4722v2.pdf.
- 2. A. Rasooli, and D. G. Down. COSHH：一种面向异构Hadoop系统的基于分类与优化的调度器. Future Generation Computer Systems, vol. 36, pp. 1–15, 2014.
- 3. M. Tim Jones. Hadoop中的调度. 可插拔调度框架介绍. IBM developerWorks, 技术报告, 2011年12月. 可访问：https://www.ibm.com/developerworks/opensource/library/os-hadoop-scheduling.
- 4. L. Zhang, C. Wu, Z. Li, C. Guo, M. Chen, and F. C. M. Lau. 将大数据迁移到云：一种在线成本最小化方法. Selected Areas in Communications, IEEE Journal on, vol. 31, no. 12, pp. 2710–2721, 2013.
- 5. Cisco Report. Cisco UCS通用平台架构（CPA）上的大数据解决方案. 可访问：http://www.cisco.com/c/en/us/solutions/data-center-virtualization/big-data/index.html, 2014年5月.
- 6. V. Cristea, C. Dobre, C. Stratan, F. Pop, and A. Costan. 大规模分布式计算与应用：模型与趋势. IGI Global, Hershey, PA, pp. 1–276, 2010. doi:10.4018/978-1-61520-703-9.
- 7. D. Pletea, F. Pop, and V. Cristea. 面向Hadoop环境的推测式遗传调度方法. In 2012 14th International Symposium on Symbolic and Numeric Algorithms for Scientific Computing, SYNASC, pp. 281–286, 2012.
- 8. A.-M. Oprescu, T. Kielmann, and H. Leahu. 云中任务包调度的预算估计与控制. Parallel Processing Letters, vol. 21, no. 2, pp. 219–243, 2011.
- 9. M. Mao, J. Li, and M. Humphrey. 带截止时间和预算约束的云自动伸缩. In The 11th ACM/IEEE International Conference on Grid Computing (Grid 2010). Brussels, Belgium, 2010.
- 10. J. Yu, and R. Buyya. 使用遗传算法在截止时间和预算约束下调度科学工作流应用. Scientific Programming Journal, vol. 14, nos. 3–4, pp. 217–230, 2006.
- 11. K. Liu, H. Jin, J. Chen, X. Liu, D. Yuan, and Y. Yang. swindew-c中面向云计算平台上实例密集型成本约束工作流的时间-成本折中调度算法. International Journal of High Performance Computing Applications, vol. 24, no. 4, pp. 445–456, 2010.
- 12. T. White. Hadoop：权威指南. O’Reilly Media, Inc., Yahoo Press, Sebastopol, CA, 2012.
- 13. X. Hua, H. Wu, Z. Li, and S. Ren. 提升面向交互密集型任务的Hadoop分布式文件系统吞吐量. Journal of Parallel and Distributed Computing, vol. 74, no. 8, pp. 2770–2779, 2014. ISSN 0743-7315.

