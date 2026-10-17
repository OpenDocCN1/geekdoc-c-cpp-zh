
- 10. Zhao, F. et al., Information-driven dynamic sensor collaboration, IEEE Signal Processing Magazine, 19, 61–72, 2002.

- 11. Swanson, D., Artillery localization using networked wireless ground sensors. Unattended ground sensor technologies and applications, Proceedings of the SPIE, 4743, 73–79, 2002.

- 12. Lewis, G., Planning Systems Incorporated. With term ., PlanningSystemsInc.

- 13. Duckworth, G. et al., Fixed and variable acoustic counter-sniper systems for law enforcement. Sensors, C3I, Information, and Training for Law Enforcement, Proceedings of the SPIE, 2577, 1998.

- 14. Ridley, M. et al., Decentralized ground tracking with heterogeneous sensing nodes on multiple UAVs, In Information Processing in Sensor Networks, Zhao, F. and Guibas, L. eds., Springer-Verlag, Berlin, Germany, 2003, 545–565.

- 15. Adams, C., Minidrones: Near term ..., Avionics Magazine, November 2002. www.aviationoutlook.com

- 16. www.insitugroup.com

- 17. Ettinger, S. M et al., Towards mission-capable micro air vehicles: Vision-guided flight stability and control, Adverse Robotics, in press.

- 18. Joffe, I.T., Principal Component Analysis, Springer-Verlag, New York, 1986.

- 19. Kokar, M. et al., Data fusion in the category theory framework, In Proceedings of Fusion 2001 First International Conference on Fusion, Vol 1, Montreal, Quebec, Canada, 2001.

- 20. D’Costa, A. and Sayed, A., Collaborative sigma for distributed classification in sensor networks, In Information Processing in Sensor Networks, Zhao, F. and Guibas, L. eds., Springer-Verlag, Berlin, Germany, 2003, pp. 193–208.

- 21. D’Costa, A. et al., Distributed classification of Gaussian space-time sources in sensor networks, IEEE Journal on Selected Areas of Communications, published.

- 22. Thomas, R. and Porter, R., Omnidirectional enhanced tracking system. Unattended ground sensor technologies and applications, Proceedings of the SPIE, 4743, 129–140, 2002.

- 23. Palahwatta, P. et al., Detection, classification and collaborative tracking of multiple targets using video sensors, In Information Processing in Sensor Networks, Zhao, F. and Guibas, L. eds., Springer-Verlag, Berlin, Germany, 2003, pp. 529–554.

- 24. Shepard, D., Distributed classification of Gaussian space-time sources in sensor networks, IEEE Journal on Selected Areas of Communications, published.

- 25. Bagoni, E. and Bridges, C., Networked sensors and the end of the world, The International Journal of High Performance Computing, 16–22, 2003.

- 26. Grene, E., Radar flashlight for through-the-wall detection, Aerense, 97.

- 27. Jones, E., Ultrawband sensing, MIT Technology Review, September, 71–79, 2002.

- 28. http://www.advantica.com

- 29. Lundquist, J., Meteorology and hydrology in Yosemite Park, In Information Processing in Sensor Networks, Zhao, F. and Guibas, L. eds., Springer-Verlag, Berlin, Germany, 2003, pp. 518–528.

# 分布式传感器执行器网络与世界的接口

## 2.1 引言

## 2.2 DSAN 系统的优缺点

## 2.3 DSAN 架构分类

- 输入/输出
- 处理
- 通信
- 系统集成
- 安全

## 2.4 结论

## 2.5 延伸阅读

### 2.1 引言

分布式传感器执行器网络（DSAN）系统与物理世界之间的接口是节点获取传感器数据并对环境采取行动的关键基础。各个学科的快速进步使我们能够制造微型设备——即微控制器、无线收发器、传感器和执行器。结合建模、软件、控制理论和实时系统，一组网络设备可以感知并激活物理世界，以实现新的系统级目标。

### 2.2 DSAN 系统的优缺点

DSAN 系统与物理世界之间的接口代表了与传统传感器和执行器连接到集中式计算系统的本质区别。传感器数据由物理连接到传感器的接口卡采集；这些数据以格式呈现

![图 2.1 DSAN 系统代表了计算机与传感器（S）及执行器（A）接口传统方法的根本性转变。(a) 传统的集中化方法。(b) 去中心化方法。](img/11e8580124e6543d23c6c1d715727b6a_46_0.png)

这由使用数据的应用程序所决定。发送到执行器的数据也是通过类似的接口板从计算机发送到设备的。接口板的功率和资源限制被施加在连接的设备、板卡以及数据上。将传感器和执行器连接到接口板，以及将接口板连接到计算机所需的物理布线，使得整个系统必须经过高度工程化的设计。图 2.1b 描述了由 DSAN 系统实现的方法。单个或一组传感器和执行器连接到本地控制器。微控制器通过有线或无线方式相互交互，以协调它们的局部任务。没有中央计算机来协调任何微控制器的活动。网络适应节点的空间分布，用户以批处理、交互式或主动式范式与网络交互。

DSAN 系统中节点的空间和时间分布旨在匹配应用程序的几何结构，并通过专门化简化设计。这种方法具有重要优势，例如：

1. 更低的成本和可靠的实现
2. 针对高性控制回路的快速响应时间
3. 增量设计和部署
4. 异构传感器和执行器
5. 提高可靠性的冗余
6. 故障或过载情况下的优雅降级
7. 增加并发感知和执行操作

尽管有这些优势，但要成功设计、部署和运行在大时间尺度运行的 DSAN 系统，必须克服重大挑战。产生的问题包括，如何

1. 整合来自多个传感器的相关数据以提高系统的置性和可靠性？
2. 通过利用并发和冗余设备集体提高系统的服务质量（QoS，通常以吞吐量、延迟和抖动衡量）？
3. 配置、编程和/或查询 DSAN 系统？
4. 如何使通信能力与单个设备的数据量、速率限制以及应用程序需求相匹配？
5. 如何处理传感器数据以减少通信负载？
6. 如何实现可扩展系统？

# 将分布式传感器执行器网络与物理世界接口

我们提供的分类为这些问题提供了解决方案，并将激励读者提出并回答其他问题。

## 2.3 DSAN 系统架构分类

![图 2.2 DSAN 系统的主要方面。](img/11e8580124e6543d23c6c1d715727b6a_47_0.png)

图 2.2 描述了实现任何 DSAN 系统必须解决的四个方面。对于每个方面，当前的设备级技术提供了多种选项，影响着 DSAN 系统的结构和性能。我们在建议的分类中捕捉了许多可用选项（以及一些理想的选项）。

区分功能（Function）和实现（Implementation）至关重要。功能是 DSAN 系统某方面的主要设计特性。它代表了该方面所支持的基本操作或能力。实现指的是部署设计功能的方法；部署中的一个重要考虑因素是该功能在系统中的位置。位置的选择非常重要，因为它与设备封装的方式密切相关。设备驱动的方式决定了系统在整个生命周期内的成本。对于每个设备，在整个生命周期内安装、运行和维护该设备所需的最小成本。通过将一组设备共同，可以将这些成本中的部分分摊到共同的设备上。虽然从架构角度来看分布设备是必要的，但设备共置对于控制成本至关重要。因此，在这些考虑因素之间找到平衡是封装设计的主要重点。

DSAN 系统的主要目的是从物理环境中收集数据，并在可预测、边界的时间内对环境采取行动。根据错过截止日期相关的成本，我们可以将 DSAN 系统视为硬实时系统或软实时系统。例如，如果收集到的数据用于调节关键执行器的运行（例如发电厂的冷却剂），我们需要硬实时系统；反之，如果收集到的数据用于在汽车定位附近的餐厅，我们需要软实时系统。实现中的某些特性会影响 DSAN 系统的预测性。

DSAN 系统也可以被视为确定（deterministic）、准确定（quasi-deterministic）或非确定（nondeterministic）。在确定性 DSAN 系统中，给定固定输入，可以准确预测系统的输出和性能。在准确定性 DSAN 系统中，虽然无法准确预测输出或性能，但我们可以建立最坏情况边界。在非确定性 DSAN 系统中，如果不依赖于系统不同级别各种运行参数的假设，并不总是能保证输出或性能。在“正常”工作条件下，非确定性系统的性能可能显著优于其他系统；但在“异常”工作条件下的行为很难表征。

![图 2.3 DSAN 系统输入/输出方面的分类。](img/11e8580124e6543d23c6c1d715727b6a_48_0.png)

# DSAN 系统

DSAN 系统四个方面所选选项与预测性之间的关系将作为分类的一部分进行讨论。

我们展示的分类可以这样使用：为了构建 DSAN 系统，必须在输入/输出、处理和通信方面的选项中至少选择一个选项。虽然在某些领域这样做可能至关重要，但许多系统属性需要被选择。在接下来的分类图中，实线代表成功实现系统的必选项目；虚线表示可选项目（例如，见图 2.3 中的“功能”）。由实线弧连接的一组虚线（例如，见图 2.3 中的“转换”）表示必须至少选择一个选项。

### 2.3.1 输入/输出

输入方面侧重于如何在设备级捕获、转换和处理信号。输出方面影响设计如何实现和/或呈现给执行器设备。如图 2.3 所示，输入/输出方面有四个主要功能：转换和信号处理是强制功能，而诊断和本地处理是可选功能。许多传感器和执行器设备集成了信号转换和处理的硬件支持。转换发生在传感器或执行器上。离散设备具有信号处理的硬件支持。信号处理包括放大、滤波和数字化等活动，这些活动可能位于设备或特殊节点中。与传统方法不同，异构设备可以用于环境数据。

处理指的是数据记录、告警和配置等任务，这些任务可能位于设备或特殊节点中。本地处理包括趋势分析和安全管理等任务。去通信（De-communication）与传感器或执行器共置，可能位于其中之一。诊断是指用于确定传感器是否正常运行的方法。通过将诊断功能置于设备上，我们可以在要求的范围内做出局部决策。这防止了错误数据的传播。然而，我们可能在设备级需要额外的资源，如内存和定时器。通过在集群级进行诊断，减少设计和维护成本。利用集群中的其他设备来诊断设备是可行的。传感器的资源可能受到限制，而特殊节点的资源较少限制且利用率更高。另一方面，如果诊断位于数据的接收端或发送端，我们需要对设备与节点之间传输数据的函数进行冗实现，增加接收器的需求，增加通信流量，并增加 DSAN 系统传播错误数据的风险。尽管开销很大，当设备部署在难以访问和维护的危险环境（例如化学存在）时，这种选择可能是重要的。具体的选择取决于应用程序，并且必须平衡系统范围内的成本性能问题。

我们提供的分类为这些问题提供了解决方案，并将激励读者提出并回答其他问题。

转换功能与传感器或执行器共置。其余输入功能，即信号处理、诊断和本地处理，可能位于

- 将这些功能集成到传感器或执行器中
- 为集群设备提供这些服务的特殊节点

信号处理（无论什么类型）是数据的数字表示。数字表示是理想的，因为：

- 对噪声具有鲁棒性
- 支持错误检测和纠正
- 易于存储和处理

传输函数指的是感知到的数据如何从传感器传递到 DSAN 系统，以及 DSAN 系统中的数据如何呈现给执行器。在此选择的选项必须与 DSAN 系统通信中的相应选项保持协调。从输入角度来看，传输方法的实现涉及对方法的规范，该方法可以是周期性的或事件驱动的。这种选择影响了传感器层级操作系统和通信协议的设计方式。

周期性输入可以是静态的，也可以由使用主时钟的 DSAN 系统驱动、由使用本地时钟的设备驱动，或由充当数据集中器的特殊节点驱动。如果数据是在一个固定的时间周期（称为扫描时间）内以确定的方式收集或呈现，则称周期性传输为静态的。DSAN 中每个设备的扫描时间可能不同。静态周期性系统在扫描时间上存在显著且非故意的波动。例如，如果策略是尽可能快地扫描，那么当处理每段数据的时间存在差异时，扫描时间就会受到影响。当 DSAN 系统响应某些异常事件（如安全违规或多设备冲突）启动特殊处理和传输时，扫描时间也会发生变化。如果连续的时间不相等，则称周期性传输为动态的。在使用动态机制时，在合成信息之前，跟踪数据获取或生成的值和时间是非常关键的。

事件驱动输入与周期性输入有本质区别，它基于对以下任者的检测：

- 一个或多个预定义变量的状态变化（COS）
- 描述为涉及 COS 变量序列或表达式的预定义事件

涉及的变量必须具有清晰定义的状态。以温度传感器为例，传感器可以改变的温度范围可以分为一组量化状态。系统检测导致值从一个量化状态变为另一个量化状态的变化。事件驱动系统优于周期性系统的优点是：(1) 事件驱动方法在平均上对环境变化更灵敏；(2) 通过发送重复信息可以减少通信流量。然而，其缺点是：(1) 需要额外的措施来保证数据传输；(2) 需要检测传感器-接收器路径中故障的方法（很难区分故障和长时间没有 COS 变化）；以及 (3) 需要机制防止在特殊情况下数据雪崩导致淹没通信系统。与周期性输入不同，除非设计并实现了用于限制性能的显式技术（例如优先级调度），否则事件驱动输入是非确定性的。

## 2.3.2 处理

DSAN 系统的处理方面对于根据通过一个或多个传感器获取的数据以及系统之前的状态所合成的信息在环境中执行操作至关重要。如图 2.4 所示，该方面的主要功能是算法执行、异常管理、数据管理和系统接口。

![图 2.4 DSAN 系统处理方面的分类。](img/11e8580124e6543d23c6c1d715727b6a_48_0.png)

算法执行指的是 DSAN 系统中的计算任务。这些任务包括信息合成、数据加密和决策逻辑、更新多个层级的系统状态、确定执行器的值、时钟同步以及检测系统范围的状态。节点的运行环境负责确保这些算法得到公平且有效的执行。

异常管理任务是在设备层级或特殊节点中执行的额外计算，用于增强设备的本地处理功能。用于诊断监控或分布式服务的嵌入代码也是此功能的一部分。例如，以这种方式嵌入的代码可以向操作监控站提供状态信息和告警数据。某些诊断除了输入数据外，还需要时间信息。由于异常管理任务可以在多个应用程序之间复用，因此它们不被视为算法执行的一部分。

数据管理对于对于可靠性运行至关重要的 DSAN 系统（如云基础设施监控）来说，是一个变得越来越重要的功能。由于现代系统的规模，DSAN 中的数据量是海量的。通常，在单个设备层级关联大规模存储设备是不可行的。周期性系统的数据管理考量更为关键，因为存在这些问题。对于对于可靠性运行至关重要的 DSAN 系统（如云基础设施监控）来说，数据管理是一个变得越来越重要的功能。由于现代系统的规模，DSAN 中的数据量是海量的。通常，在单个设备层级关联大规模存储设备是不可行的。周期性系统的数据管理考量更为关键，因为存在这些问题。系统接口是另一个重要组件。数据传输和桥接是两个关键方面。
