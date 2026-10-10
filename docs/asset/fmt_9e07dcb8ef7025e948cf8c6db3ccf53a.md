
为了保持 VS 中的模型与 PS 中的实体之间的一致性和同步性，有必要在一方确保模型与相应实体之间的一致性，在另一方确保同一实体的不同维度模型之间的一致性。

### 6.5 数据融合

车间制造数据具有与大数据相同的特征 [8,24,25]，例如体量巨大、来源多样、异构、多尺度、多维度。通过建立车间生产过程与运营决策制定之间基于大数据的关系，可以分析车间的运行规律，有助于提高生产效率 [25,26] 和产品质量 [27]，降低能耗 [28]，并保持机器处于健康状态 [29]。尽管相关研究已实现了车间部分数据的集成和融合，但在网络物理交互环境下，对所有元素、过程和业务的数据集成和融合尚未完全实现。例如，在制造手机外壳时，不仅需要考虑设计数据，如款式、颜色、用户评价和材料，还需要考虑 PS 中的实时加工数据，如加工温度、压力和表面粗糙度。同时，订单数据如加工质量、交货时间和生产任务也不能被忽视。因此，本节提出了整个元素、过程和业务的网络物理数据融合的科学问题（即数据融合）。

数据融合是指基于车间物理元素融合、模型融合和运行一致性原则，对所有元素、过程和业务的数据进行生成、建模、清洗、关联、聚类、挖掘、迭代、演化和融合。通过数据融合，可以有效地描述和反映车间的各种动态演化过程、演化规律和统计特征。如图 6.4 [1] 所示，数据融合主要涉及以下标准和技术。

![](img/5042607b423be4a5ee3f15dae22cc5bb_138_0.png)

## Figure 6.4 Data fusion in SDTD.

描述和反映。如图 6.4 [1] 所示，数据融合主要涉及以下标准和技术。

#### 1. 数据生成、建模和清洗

这包括 SDTD 中数据的实时生成机制，如复杂的数据分类和建模、不完整信息下的空值估计和特征约简、数据清洗，以及数据准确性、完整性和一致性的验证。

#### 2. 数据关联、聚类和挖掘

这包括关联，如 SDTD 中实时数据与历史数据的比较和整合；数据与操作之间的映射；来自不同层级、时期和空间的数据聚类和融合；数据追溯；特征提取；以及行为模式识别。

#### 3. 数据迭代、演化和融合

这包括 PS、VS 和 SSS 数据的交互迭代和优化，如数据的动态增长规律、数据关联的动态演化、数据演化规律和统计特征分析。

### 6.6 服务融合

融合物理和虚拟数据的 SDTD 不仅可以反映 PS 和 VS 的状态，还可以驱动其运行。DTS 运行期间的实际需求，如能耗管理、精确控制和预测性维护，涉及一系列复杂且动态的智能决策问题。复杂性和动态性源于动态且不确定的环境、物理元素的状态不确定、生产任务的动态变化以及多样化的目标和约束。服务可以建立制造物理空间与虚拟空间之间的重要桥梁，有助于实现智能互联和运行 [30,31]。DTS 中物理元素融合、模型融合和数据融合的最终目标是基于 SDTD，结合现有信息系统（如 MES），为生产提供各种所需服务。这些服务包括生产调度、产品质量管理、协同工艺规划 [32]、生产过程控制、设备健康管理和能源效率优化分析 [33]。因此，通过动态服务调用、调度和组合实现服务的融合与协作，可以实现车间智能生产和管理。上述过程被定义为数据驱动服务融合的科学问题（即服务融合）。车间服务融合和应用主要涉及以下标准和技术 [1]。

#### 1. 数据驱动服务生成

这包括从数据到服务的转换方法；物理元素、虚拟模型、数据和服务之间的多级映射机制；服务的数字描述和封装；以及服务聚合。

#### 2. 服务智能管理与优化

这包括车间服务模型的构建、服务质量（QoS）的综合评估、服务在线监控、供需匹配机制 [34,35]，以及服务优化配置。

#### 3. 服务融合与应用

这包括车间复杂耦合应用的需求分析、动态供需匹配机制、服务动态调度、基于服务组合的服务协作和融合 [36,37]，以及服务协作的可靠性评估和改进策略。

### 6.7 总结

网络物理融合是先进制造战略的共同挑战，也是 DTS 部署需要解决的关键科学问题。目前，DTS 在生产和运营过程中存在以下不足：（1）车间数据采集不完整；（2）虚拟/数字模型难以建立，仿真分析缺乏系统性；（3）物理和虚拟数据的双向动态映射和融合不足；（4）缺乏针对特定需求的动态灵活服务组合。

基于对 DTS 的概念、组成、运行机制、特征和关键技术的

不同维度下，模型可以在结构和功能上进行集成和融合，形成对 PS 的全面镜像，具有统一的三维表示。

#### 4. 多维模型一致性的理论与方法

为了保持 VS 中的模型与 PS 中的实体之间的一致性和同步性，有必要在一方确保模型与相应实体之间的一致性，在另一方确保同一实体的不同维度模型之间的一致性。

### 6.5 DATA FUSION

Shop-floor manufacturing data have the same features as big data [8,24,25] such as massive volume, multiple sources, heterogeneity, multiple scales, and multiple dimensions. Through establishing relationships between the production process and operational decision making on the shop-floor with big data, the operation rules of the shop-floor can be analyzed, which contributes to improving production efficiency [25,26] and product quality [27], reducing energy consumption [28], and keeping machines in healthy condition [29]. Although relevant studies have achieved integration and fusion of part data on the shop-floor, the integration and fusion of data from all of the elements, processes, and businesses under the cyber-physical interaction environment have not been fully realized. For example, when a mobile phone casing is manufactured, it is required to consider not only the design data, such as style, color, user evaluation, and material, but also the real-time processing data in the PS such as processing temperature, pressure, and surface roughness. Meanwhile, the order data such as processing quality, delivery time, and production tasks also cannot be neglected. Therefore, this section puts forward the scientific problem of fusion of cyber-physical data from entire elements, processes, and businesses (i.e., data fusion).

Data fusion refers to the generation, modeling, cleaning, correlation, clustering, mining, iteration, evolution, and fusion of data from all of the elements, processes, and businesses based on the physical elements fusion, models fusion, and running consistency principles of the shop-floor. Through data fusion, various dynamic evolution processes, evolution rules, and statistical characteristics of the shop-floor can be effectively

![](img/5042607b423be4a5ee3f15dae22cc5bb_138_0.png)

## Figure 6.4 Data fusion in SDTD.

described and reflected. As shown in Fig. 6.4 [1], data fusion mainly involves the following criteria and technologies.

#### 1. Data Generation, Modeling, and Cleaning

This includes real-time generation mechanisms of data in SDTD, such as complicated data classification and modeling, empty value estimation and feature reduction for incomplete information, data cleaning, and verification of data accuracy, integrity, and consistency.

#### 2. Data Correlation, Clustering, and Mining

This includes correlation, such as comparison and integration of the real-time data and the historical data in SDTD; mapping between the data and operations; clustering and fusion of the data from different levels, periods, and spaces; data tracing; feature extraction; and behavior pattern recognition.

#### 3. Data Iteration, Evolution, and Fusion

This includes interactive iteration and optimization of the data from PS, VS, and SSS, such as dynamic growth rules of the data, dynamic evolution of data correlation, data evolution rules, and statistical characteristics analysis.

### 6.6 SERVICES FUSION

The SDTD that fuses the physical and virtual data not only can reflect the states of the PS and the VS, but also drive their operations. The actual demands during the operation of the DTS, such as energy consumption management, precise control, and predictive maintenance, involve a series of complex and dynamic smart decision-making problems. The complexity and dynamism are due to the dynamic and uncertain environment, uncertain states of physical elements, dynamic changes of production tasks, and diverse objectives and constraints. Services can be used to build an important bridge between the manufacturing physical space and the virtual space, which helps to realize smart interconnections and operations [30,31]. The ultimate goal of the physical elements fusion, models fusion, and data fusion in the DTS is to provide various services required in the production based on the SDTD in combination with the existing information systems (e.g., MES). The services herein include production scheduling, product quality management, collaborative process planning [32], production process control, equipment health management, and energy efficiency optimization analysis [33]. Accordingly, smart production and management on the shop-floor can be achieved through fusion and collaboration of the services through dynamic service invocation, scheduling, and combination. The above process is defined as the scientific problem of data-driven services fusion (i.e., services fusion). The shop-floor service fusion and application mainly involve the following criteria and technologies [1].

#### 1. Data-Driven Service Generation

This includes conversion methods from data to services; multilevel mapping mechanisms among physical elements, virtual models, data, and services; digital description and encapsulation for services; and services aggregation.

#### 2. Service Smart Management and Optimization

This includes construction of shop-floor service models, comprehensive assessment of quality of service (QoS), service online monitoring, supply–demand matching mechanisms [34,35], as well as service optimization configurations.

#### 3. Service Fusion and Application

This includes demand analysis for shop-floor complex coupling application, dynamic supply-demand matching mechanisms, service dynamic scheduling, service collaboration and fusion based on service combinations [36,37], and reliability assessments and improvement strategies for service collaboration.

### 6.7 SUMMARY
