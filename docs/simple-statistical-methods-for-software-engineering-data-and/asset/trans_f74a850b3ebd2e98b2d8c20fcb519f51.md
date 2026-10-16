

![](img/2f042205c6c0e14747f198ed8f9c9f40_117_0.png)

## 图6.3 跟踪项目进度。

在挣值管理（EVM）术语中，这被称为*工作预算费用*。从项目计划中可以看出项目价值如何随时间增加。随着工作的完成，项目就被称为“挣得价值”。为了衡量进度，我们定义以下度量指标。

计划价值 = 计划工作的预算费用（BCWS）
挣值 = 已完工作的预算费用（BCWP）

图6.3展示了使用这两个度量指标跟踪项目进度的示例。

一眼就能看出挣值落后于计划价值，从而以图形方式说明项目进度。这被称为*挣值图*。

## 跟踪项目成本

完成所报告工作而实际支出的费用，以已完工作实际费用（ACWP）来衡量。成本信息可以包含在挣值图中，如图6.4所示。

除了挣值图，我们还可以计算项目偏差和绩效指数等绩效指标。我们还可以使用线性外推法预测完成项目所需的时间和成本。这些度量指标列于数据6.1中。

挣值报告通常包含所有挣值度量指标，并以图形和表格形式展示项目进度和项目未来。

![](img/2f042205c6c0e14747f198ed8f9c9f40_118_0.png)

## 图6.4 跟踪项目成本。

## 数据6.1 挣值度量指标

核心度量指标

- 计划工作的预算费用（BCWS）（也称计划价值[PV]）
- 已完工作的预算费用（BCWP）（也称挣值[EV]）
- 已完工作实际费用（ACWP）（也称实际成本[AC]）

绩效度量指标

- 成本偏差 = PV – AC
- 进度偏差 = EV – PV
- 成本绩效指数（CPI）= EV/AC
- 进度绩效指数（SPI）= EV/PV
- 项目绩效指数（PPI）= SPI × CPI
- 完工尚需进度绩效指数（TCSPI）

预测度量指标

- 完工预算 = BAC
- 完工尚需估算（ETC）= BAC – EV
- 完工估算（EAC）
  - EAC = AC + (BAC – EV) 乐观
  - EAC = AC + (BAC – EV)/CPI 最可能
  - EAC = BAC/CPI 最可能*简单（广泛使用）
  - EAC = BAC/PPI 悲观
- 完工成本偏差（VAC）= BAC – EAC

项目管理知识体系（PMBOK）将挣值度量指标视为项目经理的关键信息。有多种标准和指南可用于描述EVM的工作原理。例如，美国能源部（DOE）发布的EVMS标准将EVMS信息用作有效的项目管理系统，以确保项目成功执行。

## 框6.4 为什么缺少规模度量？

我们测量所构建对象的规模。如果建造房屋，我们会测量建筑面积。如果制造卡车，我们会测量其长、高、宽等参数。规模测量是工程学的标志。

在构建软件时，我们却不愿测量规模。有些人根本不测量规模。这令人失望，因为我们未能坚持软件工程。仔细想想，测量规模其实相当容易。如果我们觉得IFPUG功能点或FFP耗时且繁琐，尤其是对于大型模块，我们还有其他选择。例如，我们可以使用以下任何一种成熟度量指标：

- Albrecht功能点
- Mark II FP
- 对象点
- 测试用例点
- 用例点
- PROBE
- 特征点

Doug Hubbard的著作*《如何测量任何事物》*[10]有助于克服测量那些被认为无法测量的事物时的心理障碍。他指出，认为测量不可能是一种错觉，源于对测量的概念、测量对象和测量方法的不理解。

你可以构建自己的专有规模度量。有些人将工程规模单位作为度量指标，另一些人则发明了需求规模单位。自研的复杂度度量指标也在流传。拥有一个近似的规模度量指标，远比没有要好得多。

## 复习题

- 1. 请说明你在软件开发中选择的一种产品度量指标。
- 2. 请说明你在软件开发中选择的一种过程度量指标。
- 3. 请说明你在软件开发中选择的一种项目度量指标。
- 4. 请说明你选择的一种用于建立子过程度量指标的过程。识别并列出你所选过程的子过程度量指标。
- 5. 为什么功能点能取得成功？

## 推荐阅读

Aczel, A. D. 和 J. Sundara Pandian，*《完整商业统计》*，McGraw-Hill，伦敦，2008年。

*《将挣值分析应用于你的项目》*。可访问 http://office.microsoft.com/en-in/project-help/applying-earned-value-analysis-to-your-project-HA001021179.aspx。

Astels, D. *《测试驱动开发：实用指南》*，Prentice Hall PTR，Upper Saddle River，新泽西州，2003年。

Cem, K. *《重新思考软件度量》*，STQE，2000年3/4月。

*《估算功能点》*。可访问 http://www.functionpoints.org/, http://www.functionpoints.org/resources.html, http://csse.usc.edu/csse/event/1998/COCOMO/18_Stensrud%20Estimating.pdf。

*《功能点估算》*。可访问 http://webcourse.cs.technion.ac.il/234270/Spring2013/ho/WCFiles/function%20points%20estimation.pdf。

Garmus, D. *《功能点计数简介》*。可访问 http://www.compaid.com/caiinternet/ezine/garmus-functionpointintro.pdf。

Hunt, R. P.、P. J. Solomon 和 D. Galorath，*《将挣值管理应用于软件密集型项目》*。可访问 http://www.galorath.com/DirectContent/applying_earned_value_management_to_software_intensive_programs.pdf。

International Function Point Users Group，*《IT测量：来自专家的实用建议》*，Addison-Wesley，2002年。

Kitchenham, B. *《软件度量——软件过程改进的测量》*，NCC Blackwell，英国，1996年。

Kulik, P. *《软件度量：2000年最新技术》*，KLCI，2000年。

Kusters, R.、A. Cowderoy、F. Heemstra 和 E. van Veenendaal 编，*《软件质量的项目控制》*，Shaker Publishing，1999年。

McBreen, P. *《软件工艺：新的当务之急》*，Addison-Wesley Professional，2002年。

McCarthy, J. *《软件开发动力学》*，Microsoft Press，1995年。

McConnell, S. *《专业软件开发》*，Addison-Wesley，2004年。

Meli, R. 和 L. Santillo，*《功能点估算方法：比较综述》*。可访问 http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.33.6479&rep=rep1&type=pdf。

Norman, F. E. 和 M. Neil，*《软件度量：路线图》*，CSD QM&WC，伦敦，2000年8月。

Parthasarathy, M. A. *《实用软件估算》*，Addison-Wesley，2007年。

Platt, D. S. *《为什么软件很糟糕——以及你能做些什么》*，Addison-Wesley Professional，2007年。

Putnam, L. H. 和 W. Myers，*《专家度量观点》*，Cutter Information Group，2000年。

Wiegers, K. E. *《实用项目启动：工具手册》*，Microsoft Press，2007年。

Woodings, T. L. *《软件度量分类法》*，Software Process Improvement Network (SPIN)，珀斯，1995年。

## 第7章

## 维护度量

## 软件维护中的框架融合

软件维护融合了三种管理风格：项目管理、运营管理和服务管理。维护度量设计正是这种融合的体现。大型维护工作受益于项目管理框架，小型任务受益于运营管理，而所有维护任务都必然遵循服务管理框架。项目方法使这一切协调一致。

> 运营让灯光保持明亮，战略提供隧道尽头的亮光，而项目管理则是推动组织前进的火车引擎。
> 
> Joy Gumz

维护工程基于多种原则。一方面，我们有增强任务（适应性维护），即改变软件功能的小型项目[1]。项目管理知识体系（PMBOK）中的知识领域常被用作基本原则。另一方面，我们有快速修复缺陷的工作（纠正性维护），这更像是服务任务。管理这些任务使用运营管理、ITIL、ISO 20000和CMMi SM概念作为基本原则。这两类不同维护的度量指标在范围、性质和意图上因此有所不同。度量指标的解释反映了各自的基本原则。

