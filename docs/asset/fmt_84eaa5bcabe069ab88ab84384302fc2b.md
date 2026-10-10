
从制造发展视角来看，制造的物理空间与虚拟空间之间的融合过程正在随时间演进。首先，在信息技术出现之前，制造仅涉及物理空间。具体而言，所有制造活动均由人类和/或机器完成。信息缺乏限制了制造效率和生产能力。第二阶段，虚拟空间出现。各种制造相关软件产品被开发并应用于生产。然而，由于技术限制，虚拟空间的优势和潜在应用尚未得到充分发挥。第三阶段，物理空间和虚拟空间开始相互作用。虚拟空间加强了对制造过程的管理，优化了物流、资金流和信息流。然而，在此阶段，制造的物理空间和虚拟空间并未同步。当前，随着新一代信息技术（新 IT）的持续发展，物理空间与虚拟空间之间的实时交互和进一步集成正成为智能制造不可避免的趋势 [16]。

根据对各种制造战略的水平分析和对制造发展的垂直分析，制造的 cyber–physical 融合变得越来越重要。为此，数字孪生（DT）已成为首选技术。DT 以数字方式为物理对象创建虚拟模型以模拟其行为，作为物理空间与虚拟空间之间的桥梁 [1]。通过 cyber–physical 闭环，DT 可促进所有制造过程的智能化 [16]。

智能制造是多主体参与的价值创造过程。根据智能制造中数据的不同规模以及智能应用的不同时间敏感性，DT 可分为三个不同层级，即单元级、系统级和系统-of-系统（SoS）级 [2]。每个层级都有一个数据闭环，包括状态感知、数据分析、决策和执行。然而，由于各层级具有不同的角色和基础设施，如何构建面向智能制造的各层级 DT 成为一个核心问题 [16]。

边缘计算、雾计算和云计算可能为上述问题提供解决方案。云计算能够按需实现对共享资源池的无处不在、便捷的网络访问 [3]。由于按需资源共享、高计算和存储能力以及低成本，云计算是 SoS 级 DT 的完美技术手段。雾计算将云的计算、存储和网络能力转移到边缘网络 [4]。通过直接在网络上处理数据（例如网络路由器、各种信息系统等），雾计算可以帮助实现系统级 DT。边缘计算允许在更接近数据源的位置进行数据处理 [5]。边缘可定义为同时具有数据生产者和数据消费者的端点。对于单元级 DT，边缘计算将非常有益 [16]。

在本章中，边缘计算、雾计算和云计算分别被引入用于实现面向智能制造的单元级、系统级和 SoS 级 DT。首先描述制造中的三级 DT，然后简要回顾边缘计算、雾计算和云计算。最后，讨论了基于这些技术的三级 DT 框架。

## 8.2 THREE-LEVEL DIGITAL TWINS IN MANUFACTURING

通过构建集成来自不同对象、活动和过程数据的 DT 系统，可以有效增强产品设计、生产计划和实施的创新性和效率。DT 是智能制造的重要支撑技术。为了更好地理解 DT，应建立系统化和分层的视角。对于智能制造，既可以把诸如一台设备或一条生产线这样的小对象，也可以把诸如一个车间或整个工厂这样的大对象视为 DT。因此，DT 需要根据不同粒度的对象划分为不同层级，包括单元级、系统级和 SoS 级 [6]。每个层级的 DT 都是一个系统模型，由前一层级或多个层级组成。系统级 DT 可被视为多个相互协作的单元级 DT 的集成。多个单元级 DT 或多个系统级 DT 构成 SoS 级 DT，即包含复杂关系、关联和组合的复杂系统。如图 8.1 所示，单元级 DT 主要服务于单个对象（例如一台设备），它是参与制造活动的最小单元。通过对设备的调整可以实现制造的优化。关于系统级 DT，由机床、机械臂、自动导引车（AGVs）等组成的智能生产线可被视为具有特定生产能力的系统。对于单元级和系统级 DT，虚拟模型是通过从几何形状、功能和运行状态角度对设备和生产线进行数字描述而实现的超高保真映射。基本属性、实时状态和其他数据被传输到虚拟模型以驱动仿真和预测。同时，虚拟模型的参数被反馈以优化物理实体。通过闭环交互过程，物理实体和虚拟模型同步演进。对于 SoS 级（例如车间），准确的车间管理和可靠的运行，与服务密不可分，尤其至关重要。如图 8.1 所示，（1）物理实体是一组具有特定功能的对象实体，根据输入和输出完成制造任务；（2）虚拟模型是物理实体的数字映像，能够完整真实地反映物理对应物的生命周期；（3）服务整合控制、优化和预测等各种功能，根据需求提供应用服务；（4）数据是 DT 的核心驱动，包括来自物理实体、虚拟模型、服务的以及它们的融合数据；以及（5）它们之间的连接将上述四个部分配对，确保实时交互和迭代优化。基于 DT 的五维结构，数字孪生车间（DTS）为实践智能制造提供了一种新方式 [6]。

![](img/5042607b423be4a5ee3f15dae22cc5bb_174_0.png)

图 8.1 制造中单元级、系统级和 SoS 级 DT [6]。

## 8.3 FROM CLOUD COMPUTING TO FOG COMPUTING AND EDGE COMPUTING

作为互补技术，雾计算和边缘计算在终端 devices and traditional cloud computing [4], offer bright prospects for expanding smart manufacturing applications [16].

### 8.3.1 云计算

美国国家标准与技术研究院（NIST）将云计算定义为“一种使能够实现无处不在、便捷、按需通过网络访问共享的、可配置的计算资源池（例如网络、服务器、存储、应用程序和服务）的模型，这些资源能够在最少的管理工作或服务提供商交互的情况下快速配置和释放” [3]。由于具有无处不在、便捷、按需资源共享、高计算和存储能力以及低成本等显著优势，云计算对许多大型公司（例如 Amazon、Google、Facebook 等）极具吸引力，这些公司通过互联网提供服务以获得经济和技术效益 [7]。从用户角度来看，云通过基础设施即服务（IaaS）、平台即服务（PaaS）和软件即服务（SaaS）隐藏了底层复杂性和异构性 [8]。用户可以将任务外包给服务提供商，而无需为小任务购买昂贵的设备。云计算的兴起改变了行业和企业做生意的方式，并为其创造了全新的机会。然而，网络不可用、带宽过载和延迟等问题使得云计算无法解决所有问题 [9]。

### 8.3.2 雾计算

新一代智能设备能够在本地处理数据而不是将其发送到云端，从而实现一种新的分布式计算范式，即雾计算 [9]。雾计算最初由 Cisco 提出，Cisco 是全球领先的网络解决方案提供商之一。雾计算被视为将云计算扩展到边缘网络的延伸，在靠近用户边缘设备的附近提供服务（例如计算、存储等），而不是将数据发送到云端 [9–11]。通过直接在网络上处理数据，例如网络路由器，雾计算范式可以提高效率，减少需要传输的数据量并增强安全性 [8]。雾计算可由位置感知、低延迟、边缘位置、实时交互、互操作性、支持与云在线交互等特征表征 [4,12]。这些特征使得应用服务部署更加便捷。因此，雾计算将在众多面向智能制造的延迟敏感型应用中发挥关键作用。

### 8.3.3 边缘计算

边缘计算是一种分散的架构，其驱动因素是智能终端的增加、物联网中海量网络设备以及计算机组件成本的降低 [13]。由于其广阔的应用前景，许多公司已致力于边缘计算，例如 Intel、ARM 和华为，它们是信息和通信技术（ICT）设备的主要提供商 [14]。与雾计算类似，边缘计算也允许在网络边缘执行计算，但更接近数据源。因此，边缘可以被定义为更靠近终端侧的资源，这些资源不仅是数据消费者，也是数据生产者 [5]。通过在边缘设备中进行数据分析和处理，边缘计算可以实现底层对象与对象之间的感知、交互和控制。在制造中，边缘计算可以满足制造现场敏捷连接、实时优化等关键需求以及其他应用。

## 8.4 基于边缘计算、雾计算和云计算的三级数字孪生

鉴于新一代信息技术在制造中的广泛应用，制造商面临着数据爆炸式增长 [15]。数字孪生的本质是通过传感器从物理实体和环境中获取数据，然后在虚拟空间中计算和分析，从而控制物理实体和环境。由此建立数据闭环，形成物理空间与虚拟空间之间的交互和融合。制造中不同层级的数字孪生对数据处理和数据流通有不同的要求，例如延迟、带宽、安全等。具有互补属性的边缘计算、雾计算和云计算为单元级、系统级和体系结构级数字孪生的实现提供了新思路和新方法。从资源高效利用的角度来看，基于边缘计算部署的单元级数字孪生、基于雾计算的系统级数字孪生以及基于云计算的体系结构级数字孪生可以实现资产控制、管理、优化和业务优化 [16]。

### 8.4.1 基于边缘计算的单元级数字孪生

构建单元级数字孪生需要满足的基本要求包括（1）状态感知，（2）数据的计算和处理，以及（3）对物理实体的控制。作为一种将计算、网络和存储能力从云端扩展到边缘的架构，边缘计算通过在边缘节点中对数据进行分析和处理，实现对物体的感知、计算和控制。如图 8.2 所示，具有物理设备（例如机体、主轴、工具等）和网络部件（例如嵌入式系统、传感设备等）的制造资源（例如机器、机器人、部件、AGV 等）构成单元级数字孪生。网络部件可以通过执行器监控和感知物理设备的信息，并通过能够接收控制指令的执行器对物理设备施加控制。由于具有感知、数据分析和控制能力，边缘计算可以部署在单元级数字孪生上，可被视为一个边缘节点。由于数据在单元设备上循环，边缘计算可以实现更小型的应用，从而提供更好的实时响应。边缘计算在单元级提供的实时应用包括传感数据的实时处理和分析、数据缓冲、高性能实时控制、执行器监控、故障诊断、健康特征提取、周期计数累积、故障

![](img/5042607b423be4a5ee3f15dae22cc5bb_177_0.png)

Figure 8.2 Three-level DTs in manufacturing based on edge computing, fog computing, and cloud computing [16].

处理和安全关机。例如，在机床或机械臂上，使用传感器检测某些故障是否可能带来安全隐患。在这种情况下，延迟是不可容忍的。如果数据发送到云端，响应时间可能过长。然而，有了边缘计算，时延得以降低，允许实时做出决策，因为数据离数据源不远。边缘计算架构不依赖于互联网连接，这有利于单元级数字孪生 [16]。

### 8.4.2 基于雾计算的系统级数字孪生

如图所示 8.2，多個单元级数字孪生通过网络接口和信息管理系统连接，例如企业资源规划（ERP）、制造执行系统（MES）、供应链管理（SCM）和客户关系管理（CRM）。系统级数字孪生集成了多种异构的单元级数字孪生。此外，通过人机界面（HMI），每个单元级数字孪生都可以被访问和控制，以监控和诊断相应系统的状态和健康状况。系统级数字孪生强调其组成元素之间的互联和互操作性。在此基础上，它侧重于不同元素的实时和动态协同控制，以实现物理空间与虚拟空间的协调和统一。一般而言，系统级数字孪生在地理上集中（主要在制造企业内部），非常适合雾计算模型。系统级数字孪生的数据（即企业内部数据）可以直接由雾计算处理以提高效率，而无需传播到云端再返回。考虑到延迟、网络流量、成本等因素，雾计算在网络边缘提供服务，促进实时交互、可扩展性和互操作性。雾计算环境可以由网络组件（例如路由器、代理服务器、基站等）构成。这些组件可以提供不同的计算、存储和网络能力，以支持智能制造应用的实现。单元级数字孪生使用传感器收集每个设备上的运行数据并进行分析。雾计算环境汇总所有单元级数字孪生的数据，并为智能制造提供可操作的信息（例如相互协作完成任务）。

system-level DT in fog computing provides applications that have lower real-time requirements but stronger computation requirements, such as model adaptation, model training, spectrum computing, wavelet transform, alarm priority processing, remote monitoring, accident recording, remote maintenance, performance assessment, and asset visibility. For example, in the actual production process, the robot places materials or parts on the conveyor belt or AGV for transportation, and then machine tools transform them into desired products. In this way, the combination of real-time edge computing and fog computing with interoperability and scalability will provide the best performance for the system-level DT [16].

### 8.4.3 System of Systems–Level Digital Twin Based on Cloud Computing

The collaborative optimization between multiple system-level DTs can be achieved by developing a smart service platform. As a result, multiple system-level DTs constitute a SoS-level DT. For example, multiple production lines or factories collaborate with each other through a smart cloud service platform, achieving the enterprise-wide system integration during the entire product lifecycle. The SoS-level DT involves various participants and resources, which may be geographically dispersed. The data of the SoS-level DT is more abundant and diverse. Therefore, the requirements that need to be met in the SoS-level DT include (1) providing distributed data storage and processing and (2) providing data and smart services for enterprise collaboration. As shown in Fig. 8.2, the cloud computing architecture is conducive to the organization and management of a large number of connected devices, as well as the combination and integration of enterprise’s internal and external data. In the cloud computing architecture, a variety of different types of storage devices can work together through the application software, to jointly provide data storage and business access for enterprises. Besides, massive data mining must be supported by the distributed processing and virtualization technologies, which are the typical characteristics of cloud computing. Therefore, cloud computing is the ideal technology for long-term and massive data storage and analysis of the SoS-level DT. In addition, services with the characteristics of interoperability pave the way for collaboration among the system-level DTs. In virtue of the cloud architecture, various unit-level DTs, or system-level DTs can be encapsulated into services, so as to become plug-and-play components and be shared by other participants [17]. In this way, manufacturers not only can conveniently provide their services to their collaborative stakeholders, but also use various resources in a pay-as-you-go manner [18]. In summary, the cloud computing architecture provides more architectural flexibility, and higher utilization of external data for product innovation and value creation. For example, supply chain application and product customization can benefit from understanding the aggregate data view [16].

## 8.5 SUMMARY
