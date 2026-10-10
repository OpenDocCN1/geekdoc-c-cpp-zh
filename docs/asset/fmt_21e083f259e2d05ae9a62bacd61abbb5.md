
[22] W. Zhang, S. Zhang, F. Qi, M. Cai, Self-organized P2P approach to manufacturing service discovery for cross-enterprise collaboration, IEEE Trans. Syst. Man Cybern. Syst. 44 (3) (2014) 263–276.

[23] X. Yang, G. Shi, Z. Zhang, Collaboration of large equipment complete service under cloud manufacturing mode, Int. J. Prod. Res. 52 (2) (2014) 326–336.

[24] F. Tao, J. Cheng, Y. Cheng, S. Gu, T. Zheng, H. Yang, SDMSim: a manufacturing service supply–demand matching simulator under cloud environment, Robot. Comput. Integr. Manuf. 45 (2017) 34–46.

[25] L.M. Camarinha-Matos, H. Afsarmanesh, B. Koelmel, Collaborative networks in support of service-enhanced products, in: Adaptation and Value Creating Collaborative Networks. PRO-VE 2011 (IFIP Advances in Information and Communication Technology), Berlin, Heidelberg, vol. 362, 2011, pp. 95–104.

[26] F. Tao, Q. Qi, New IT driven service-oriented smart manufacturing: framework and characteristics, IEEE Trans. Syst. Man Cybern. Syst. (2017). Available from: `https://doi.org/10.1109/TSMC.2017.2723764`.

[27] L. Zhang, Y.L. Luo, F. Tao, L. Ren, H. Guo, Key technologies for the construction of manufacturing cloud, Comput. Integr. Manuf. Syst. 16 (11) (2010) 2510–2520.

[28] L. Ren, L. Zhang, Y.B. Zhang, F. Tao, Y.L. Luo, Resource virtualization in cloud manufacturing, Comput. Integr. Manuf. Syst. 17 (3) (2011) 511–518.

[29] Y. Cheng, F. Tao, L. Zhang, Y. Zuo, Supply–demand matching of manufacturing service in service-oriented manufacturing systems, Comput. Integr. Manuf. Syst. 21 (7) (2015) 1930–1940.

[30] Q. Qi, F. Tao, Y. Zuo, D. Zhao, Digital twin service towards smart manufacturing, Procedia CIRP 72 (2018) 237–242.

[31] X. Wang, X. Xu, Virtualise manufacturing capabilities in the cloud: requirements, architecture and implementation, Int. J. Manuf. Res. 9 (4) (2014) 348–368.

[32] F. Tao, J. Cheng, Q. Qi, IIHub: an industrial internet-of-things hub toward smart manufacturing based on cyber–physical system, IEEE Trans. Ind. Inform. 14 (5) (2018) 2271–2280.

[33] F. Tao, Q. Qi, A. Liu, A. Kusiak, Data-driven smart manufacturing, J. Manuf. Syst. (2018). Available from: `https://doi.org/10.1016/j.jmsy.2018.01.006`.

[34] R. Sarraj, E. Ballot, S. Pan, B. Montreuil, Analogies between internet network and logistics service networks: challenges involved in the interconnection, J. Intell. Manuf. 25 (6) (2014) 1207–1219.

[35] Q. Qi, F. Tao, Digital twin and big data towards smart manufacturing and industry 4.0: 360 degree comparison, IEEE Access 6 (2018) 3585–3593.

[36] J.S. Gero, U. Kannengieser, The situated function–behaviour–structure framework, Design Stud. 25 (4) (2004) 373–391.

[37] A. Kusiak, Innovation: a data-driven approach, Int. J. Prod. Econ. 122 (1) (2009) 440–448.

[38] J. Madhavan, S.R. Jeffery, S. Cohen, X. Dong, D. Ko, C. Yu, et al., Web-scale data integration: you can only afford to pay as you go, CIDR (2007) 342–350.

[39] F. Tao, F. Sui, A. Liu, Q. Qi, M. Zhang, B. Song, et al., DT-driven product design framework, Int. J. Prod. Res. (2018). Available from: `https://doi.org/10.1080/00207543.2018.1443229`.

[40] R. Rosen, G. Von Wichert, G. Lo, K.D. Bettenhausen, About the importance of autonomy and digital twins for the future of manufacturing, IFAC-PapersOnLine 48 (3) (2015) 567–572.

[41] F. Tao, M. Zhang, Digital twin shop-floor: a new shop-floor paradigm towards smart manufacturing, IEEE Access 5 (2017) 20418–20427.

# CHAPTER 11

### 数字孪生与虚拟现实及增强现实/混合现实

虚拟现实（VR）和增强现实（AR）/混合现实（MR）随着相关技术的发展而日益成熟，例如先进的传感器、计算机图形学、实时配准与跟踪等。VR 和 AR/MR 技术在物理世界与虚拟世界的无缝集成和融合中发挥着重要作用，这对数字孪生（DT）的实现至关重要。本章将 DT 与这些技术相结合。基于 VR 和 AR/MR 在 DT 中的现有和潜在应用，提出了一个通用框架，以将这些技术与 DT 集成，为用户提供更具沉浸感和交互性的服务。根据所提出的框架，随后讨论了一个装配过程。

## 11.1 INTRODUCTION

虚拟现实（VR）的历史始于 1962 年，当时一种名为 Sensorama Simulator 的设备被发明并获得专利，用于创建虚拟环境，可为用户提供声音、气味、风、振动等方面的多感官体验 [1]。然而，Sensorama Simulator 提供的环境并非交互式 [2]。为解决这一问题，Sutherland 在几年后开发了第一个头戴式显示器（HMD）系统，该系统可根据用户头部位置感知生成交互式视图 [3]。Krueger 还创建了一个 VR 交互环境，其中计算机可以感知参与者的动作并实时以视觉和听觉显示做出响应 [4]。在 1980 年代，Virtual Programming Languages（VPL）公司生产了流行的 DataGlove 和 Eyephone HMD，它们是首批商用 VR 设备 [2]。1992 年，CAVE 自动虚拟环境出现 [2]。它不使用 HMD，而是将立体图像投射到房间的墙壁上，从而增强了用户的沉浸感。1995 年，Silicon Graphics 开发了 VR 建模语言，使人们能够方便、快速地创建和交互各种虚拟模型 [5]。在 21 世纪，VR 已应用于不同领域，包括娱乐 [6]、教育 [7]、医疗保健 [8]、制造 [9] 等。

增强现实（AR）可以被视为 VR 的一种变体 [5]。与创建完全虚拟环境的 VR 相比，AR 将虚拟信息叠加在真实世界之上，以增强现实而不是取代它。增强现实这一术语由 Caudell 和 Mizell 于 1990 年提出 [10]。1993 年，Rosenberg 发明了第一个功能性 AR 系统，即虚拟夹具，它可以将计算机生成的感知叠加在真实工作空间上以增强人类性能 [11]。Feiner 等人开发了一个系统，为佩戴实验性头戴式透视显示器的用户生成维护和维修说明 [12]。该系统使用户能够与真实环境和虚拟信息进行交互，也可被视为 AR 的早期原型之一。1998 年，Raskar 等人引入了空间增强现实（SAR），虚拟对象可直接集成到物理空间中 [13]。1999 年，Kato 开发了 ARToolKit，为 AR 系统构建提供了一种高效、快速的方法 [10]。Thomas 等人发明了 ARQuake，这是首次将传统的桌面第一人称视角应用转换为室外/室内移动 AR 应用 [11]。2008 年，Wikitude AR 旅行指南为 Android 手机推出，它将导航数据添加到实时街景中 [5]。近年来，随着相关硬件和软件技术的发展，AR 已成为规划、指导和培训等活动中的有效工具。

混合现实（MR）是 AR 的另一种形式。1994 年，Milgram 和 Kishino [14] 首先提出了“虚拟性连续体”的概念，并指出 MR 可以提供一个混合且连续的空间，该空间从完全真实的环境延伸到完全虚拟的环境。MR 本质上与 AR 相同，两者都侧重于物理和虚拟元素的融合。然而，AR 是相关研究中更常用的术语，而 MR 比 AR 提及较少。因此，在本章的其余部分，AR 用于简写表示 AR/MR。

近年来，VR 和 AR 已紧密耦合并相互补充。由于它们显示出物理和虚拟空间无缝集成和融合的潜力，因此对其发展给予了高度重视。本章将 VR 和 AR 与数字孪生（DT）相结合，以增强 DT 的两个空间并进一步增强融合，从而帮助 DT 实现更高效的应用。在以下各节中，回顾了 VR 和 AR 在设计、制造和服务中的应用，并从不同方面进行了比较。基于这些技术在 DT 中的现有和潜在应用，提出了一个通用应用框架，并以装配过程为例进行讨论。

## 11.2 VR IN DESIGN, MANUFACTURING, AND SERVICE

VR 可以提供一种沉浸式、交互式的计算机介导体验，其中一个人通过人机交互设备（如计算机、HMD、耳机和数据手套）感知人工环境 [1,15]。VR 的相关技术包括人机交互、计算机图形学、触觉反馈、动态环境建模、立体视觉等。由于 VR 以沉浸感、临场感、交互性和导航为特征 [16]，许多研究人员已探索 VR 在设计、制造和服务领域的应用。

### 11.2.1 VR in Design

VR 为设计师提供了一个完全虚拟的环境，用于开发原型、与产品模型交互、评估替代设计等。它可以改善产品的可视化，提供直观的模型操作，并实现协同设计。以下是关于工厂布局设计和产品设计的相關研究介绍。

在工厂布局设计中，Iqbal 和 Hashmi [17] 讨论了如何通过 VR 在三维虚拟环境中设计和分析工厂布局，并开发了一种新的通道系统以减少物料搬运距离。Menck 等人 [18] 提出了一个基于 VR 的协同平台，用于工厂布局设计。不同地点的用户可以在同一沉浸式系统中实时协作、探索和分析。Gebhardt 等人 [19] 提出了一个整体的 VR 应用，称为工厂布局规划助手，它不仅可作为逼真的虚拟漫游模拟平台，还可为决策提供见解。Ebner 等人 [20] 开发了一款基于 VR 的多点触控桌，使用户可以从对象库中选择必要项目并用手指触摸将其放置在布局上。错误或信息可以实时评估并在桌上显示。

在产品设计中，Ryken 和 Vance [21] 将 VR 与有限元分析、灵敏度分析、碰撞检测等相结合，创建了一个交互环境，设计师可以在其中修改零件形状、评估应力并检查新零件的干涉。Bruno 等人 [22] 使用进程间通信库将 VR 环境与数值模拟环境连接起来。这样，产品行为可以利用数值模拟软件进行模拟和预测，然后在 VR 环境中可视化。Sung 等人 [23] 提出了一个基于 VR 的线束设计系统，该系统可以自动捕获嵌入在日志文件中的设计知识，并在设计任务期间将知识传递给用户。

### 11.2.2 VR in Manufacturing

VR 可应用于制造中的工艺规划、仿真、检验、验证等，有助于操作员更好地理解制造过程并提高最终产品的可制造性、耐用性和盈利能力。主要介绍 VR 在计算机数控（CNC）、虚拟装配和机器人中的应用。

在 CNC 仿真中，Luo 等人 [24] 提出了一种基于 VR 的数控行为仿真层次结构并开发了一个原型系统。Lin 和 Fu [25] 提出了一种虚拟建模方法，以响应用户在功能和结构方面的要求生成机床结构。开发了一台虚拟机床，用于在虚拟环境中进行设计、测试、优化、控制和加工。Kao 等人 [26] 基于 VR 软件和 Microsoft Visual Basic 编程环境构建了 CNC 铣床的虚拟控制器。虚拟控制器可以解析用户的数控代码、模拟刀具路径并根据刀具路径驱动虚拟 CNC。

在装配验证中，Seth 等人 [27] 开发了一个低成本的 VR 应用，可在虚拟环境中执行碰撞检测和行为仿真。该应用可在许多类型的 VR 系统（例如桌面、Cave、Power wall 等）和操作系统（Linux、Windows、Irix testbed 等）上运行。在 Virtuelle Werkstatt 项目中，Biermann 等人 [28] 设计了一种基于知识的方法来在 VR 环境中装配基于 CAD 的零件，并提出了一种使用手势和语音进行的多模态交互以进行

人机交互以一种直观自然的方式进行。Wang 等人 [29] 使用 Visual C++ 和 Open Inventor 开发了一个用于机床的虚拟装配与加工系统，该系统可以模拟装配和加工过程以及关键参数。该系统在上海一家工厂生产的 CK6430 机床上进行了验证。De Sa 和 Zachmann [30] 提出了几种用于虚拟装配和维护的交互范式，使缺乏经验的用户能够高效地使用虚拟原型进行工作。

在机器人路径规划方面，Chen 等人 [31] 构建了一个由 PHANToM 设备驱动的基于力反馈的虚拟机械臂，并提出了一种基于机器人运动学分析的工作空间映射方法。该虚拟机械臂既可用于自由路径规划，也可用于约束条件下的路径规划。Yap 等人 [32] 开发了一套基于 VR 的机器人工作单元布局规划与编程支持系统。在其工作中，构建了 VR 机器人工作单元布局（VR-RoWL）和基于 VR 的机器人教学系统（VR-RoT），分别用于完成机器人的布局规划和克服编程中的安全问题。Liu 等人 [33] 提出了一种特征映射算法，用于将工件的设计特征转换为焊缝的加工特征，该算法支持焊接机器人在虚拟环境中的运动导航。

### 11.2.3 VR 在服务中的应用

在 VR 的帮助下，服务可以在实际执行前在沉浸式虚拟环境中进行模拟和优化，避免对操作人员以及设备造成潜在风险。同时，VR 可以增强操作人员的能力，从而提高相关活动的质量。以下部分介绍了 VR 在维护、物流和培训方面的一些研究工作。

在维护仿真方面，Lecakes 等人 [34] 开发了一套 VR 系统，用于可视化火箭发动机健康管理的多传感器测量数据。该系统可以为操作人员显示与图形耦合的各种形式的数据。Liu 和 Hao [35] 提出了一种基于虚拟维护仿真的可维护性分析框架，该框架包括虚拟维护原型模块、维护仿真模块、可维护性分析模块和系统管理模块。Peng 等人 [36] 构建了一种基于桌面 VR 的复杂产品可维护性设计与验证方法。该方法的效率已在移动机器人系统上得到验证。

在物流规划方面，Reif 和 Walch [37] 将 VR 视为规划物流系统的一种创新方式。利用数据手套和跑步机，可以构建一个用于拣货规划的沉浸式工作空间，使工人在虚拟仓库中能够从存储位置抓取货物并行走。Xu [38] 通过构建空间距离计算模型并基于 VR 技术模拟仓库布局，对物流仓储空间进行了分配。
