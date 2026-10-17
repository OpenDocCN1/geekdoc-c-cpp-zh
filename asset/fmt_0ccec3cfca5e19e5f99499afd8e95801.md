
## 关联

### 关联：业务边界 (Business boundary)

目的：

根据业务的功能现实情况划分工作上下文。

多重性：

- 对于每个业务事件 (Business Event)，有一个工作上下文 (Work Context)。
- 对于每个工作上下文，可能存在多个业务事件。

### 关联：业务相关性 (Business relevancy)

目的：

确保调查范围、项目目的和利益相关者之间存在相关的业务连接。

多重性：

该三元关联如下：
- 对于每一个工作上下文实例和一个利益相关者实例，存在一个或多个项目目的。
- 对于每一个项目目的实例和一个利益相关者实例，有一个工作上下文。
- 对于每一个项目目的实例和每一个工作上下文实例，可能存在多个利益相关者。

### 关联：业务响应 (Business responding)

目的：

揭示使用哪些用例来响应事件。

多重性：
- 对于每个业务事件，通常有一个用例，但也可能有多个。
- 对于每个用例，只能有一个业务事件。

### 关联：业务追踪 (Business tracing)

目的：

跟踪哪些需求是由哪些用例生成的。注意，这是一个多对多的关联，因为给定的需求可能存在于多个用例中。

多重性：
- 对于每个用例，可能存在多个需求。
- 对于每个需求，可能存在多个用例。

### 关联：实现 (Implementing)

目的：

跟踪哪些用例在实现单元（Implementation Units）中被实现。

多重性：
- 对于每个用例，可能存在多个实现单元。
- 对于每个实现单元，可能存在多个用例。

### 关联：所有 (Owning)

目的：

跟踪哪些利益相关者是哪些需求的源头。“所有权”的概念是识别一个负责责任帮助获取需求答案的人员。

多重性：
- 对于每个需求，有一个利益相关者。
- 对于每个利益相关者，可能存在多个需求。

### 关联：产品划分 (Product partitioning)

目的：

所有用例共同构成了产品的完整范围。产品范围被划分为若干用例。

多重性：
- 对于每个产品用例，有一个产品范围。
- 对于每个产品范围，可能存在多个产品用例。

### 关联：产品追踪 (Product tracing)

目的：

跟踪哪些需求包含在哪些用例中，用于可追溯和处理变更。

多重性：
- 对于每个需求，可能存在多个用例。
- 对于每个用例，可能存在多个需求。

### 关联：支持 (Supporting)

目的：

跟踪哪些架构组件支持哪些实现单元，用于跟踪测试和评估变更影响。

多重性：
- 对于每个系统架构组件，可能存在多个实现单元。
- 对于每个实现单元，可能存在多个系统架构组件。

### 关联：测试 (Testing)

目的：

跟踪哪些测试覆盖了原子需求或与 PUC 相关的原子需求组。

多重性：
- 对于每个测试，可能存在多个原子需求。

## 带有模板章节编号的知识模型

Volere 需求知识模型是一个用于识别和关联需求知识类的正式结构。在图 D.2 所示的视图中，类上的数字提供了指向 Volere 需求规范模板相关章节的交叉引用。

## 使用模板章节编号 509 标注的知识模型

| 工作范围 | * 业务事件 | 产品范围 | 系统架构组件 | 图表 D.2 |
|---|---|---|---|---|
| 6b | 6c | 8a | | Volere 需求规范 |
| | 业务边界 | | | 与 Volere 需求规范模板相关章节有交叉引用的知识模型 |
| 1 | 1 | | | |
| | | 业务响应 | 产品拆分 | * 支持 |
| | * 项目目标 | | * 实现 | |
| | 业务相关性 | 业务用例 | 产品用例 | 实现单元 |
| | | 6d | 8a8b | | |
| * 利益相关者 | * 业务追溯 | 产品追溯 | 测试 | |
| 2 | * | * | | | |
| | | 原子化需求 | 测试 | | |
| | | 3,9-17 | * | | |
| 命名规范与数据类型// | | | | |
| 4,7 | | | | |
| 约束 | | | | |
| 事实/假设 | 功能性需求 | 非功能性需求 | 技术性需求 | |
| 5 | 3 | 9 | 10-17 | |

## 术语表

**参与者 (Actor)** 与产品用例交互的人员或自动化系统。参与者也称为*用户*（个人、组织、计算机系统）以及终端用户。

**相邻系统 (Adjacent system)** 一系列专注于需求建模的原则，它向你正在研究的工作提供信息或从其接收信息。

**敏捷开发 (Agile development)** 使用迭代开发来开发软件的方法。存在多种敏捷技术，包括极端编程（Extreme Programming）、Scrum 和水晶（Crystal）。我们使用*迭代*一词来指任何敏捷或迭代技术。

**敏捷宣言 (Agile Manifesto)** 一组原则，专注于向客户交付可运行的软件、协作工作实践以及快速响应变化的能力。

**原子化需求 (Atomic requirement)** 一种可测试且不需要进一步拆解的需求。参见功能性需求、非功能性需求、约束、雪花卡（Snow card）。

**属性 (Attribute)** 描述（并已分配给）类的数据元素。也指*原子化*需求的组成部分。

**启动 (Blastoff)** 一种通过建立“范围-利益相关者-目标”三位一体并验证项目可行性，为需求活动建立基础的技术。

**棕牛模型 (Brown Cow Model)** 一种通过不同系统视角来讨论和建模工作的技术。这些视角是现在、未来、如何以及什么是的组合。

**业务分析师 (Business analyst)** 负责在项目利益相关者之间发现和沟通需求的角色。也称为需求分析师、需求工程师和系统分析师。

**业务数据模型 (Business data model)** 业务数据核心类及其之间关联的模型，这些关联对于支持工作范围内的功能性需求是必要的。

**业务事件 (Business event)** 发生在业务中的某事情（通常被称为“工作”），使其产生响应。例如：“客户支付发票”、“卡车报告所有道路均已经过处理”、“读取电表的时间到到”、“冲浪者想搜索网站”。

**业务流程模型 (Business process model)** 业务中流程的模型；通常用于理解当前流程以便进行改进。此类模型可以使用多种表示法。

**业务用例 (Business use case, BUC)** 工作对业务事件的响应。它包含了满足业务中隐含请求所需的流程和存储数据。参见*产品用例*。

**类 (Class)** 研究语境中的物理或抽象实体，具有一个或多个存储数据的属性。

**客户 (Client)** 为产品开发支付费用的人，或对项目有组织责任的人。也称为*赞助者 (sponsor)*。

**约束 (Constraint)** 一种限制你生产产品方式的组织或技术需求。它可能是对产品设计方式的管理限制——“它必须在 4G 移动手机上运行”——或者是限制产品范围的预算，或者是限制可能解决方案的当前特征。

**上下文 (Context)** 影响产品需求的主题、人员和组织。研究语境（或工作语境）识别了正在研究的业务以及与该工作交互的相邻系统。产品上下文识别了产品自身的上下文。

**上下文图 (Context diagram)** 显示产品及其与相邻系统交互的图表。

**商业现货产品 (Commercial off-the-shelf, COTS products)** 由外部组织开发的产品（通常是软件）。

**客户 (Customer)** 购买产品的人。

**数据字典 (Data dictionary)** 需求中使用的术语规范。

**数据元素 (Data element)** 数据的元素部分。参见*属性 (attribute)*。

**数据流 (Data flow)** 从一个过程移动到另一个过程的数据。

**数据模型 (Data model)** 显示类和关联的模型。参见*业务数据模型*。

**设计 (Design)** 制定解决方案的行为。

**开发者 (Developer)** 构建产品的人。也称为程序员、架构师。

**领域分析 (Domain analysis)** 调查、捕获和规范需求的活动。

**核心视角 (Essential viewpoint)** 关注需求的视角。

**外部事件 (External event)** 由外部世界触发的事件。另参见*业务事件*。

**适配性 (Fit)** 衡量交付的产品是否满足需求的指标。

**功能点 (Function point)** 功能性的衡量标准。功能点最初由国际用户小组提出。

**功能性需求 (Functional requirement)** 产品必须执行的事情。

**创新 (Innovation)** 对问题进行新颖的思考或以不同的方式思考。

**迭代开发 (Iterative development)** 促进重复和持续交付的策略。

**命名规范 (Naming conventions)** 利益相关者在讨论工作时使用的术语（包括缩写和首字母）。

**非功能性需求 (Non-functional requirement)** 产品必须具备的属性或质量，如外观、速度、安全性或准确性。

**人物画像 (Persona)** 为了帮助你发现需求的虚拟人物，代表典型用户。

**产品 (Product)** 你正在为其编写需求的东西。在书中，“产品”通常指软件产品，但需求也可以针对硬件、消费品或其他事物。

**产品用例 (Product use case, PUC)** 你决定自动化的业务用例部分。你为该用例编写需求。参见业务用例。

**项目启动 (Project blastoff)** 参见启动 (Blastoff)。

**项目目标 (Project goal)** 执行项目的原因。目标必须包含预期收益的量化。

**原型 (Prototype)** 使用软件原型工具、低保真白板或纸质模型进行的仿真。也称为*草图 (sketch)*。

**质量门关 (Quality Gateway)** 在需求成为需求规范的一部分之前，应用一组测试（相关性、歧义、易用性、适配性等）来确保需求的质量。

**理由 (Rationale)** 需求的依据。它用于帮助理解需求，并通常揭示需求产生。

**需求 (Requirement)** 产品必须执行的事情，或利益相关者需要或想要的产品属性。

**需求分析师 (Requirements analyst)** 负责编制需求规范的人员。分析师不一定完成所有的需求获取，但负责协调需求工作。根据组织对角色的定义，该人员可能被称为*业务分析师*、系统分析师或需求工程师。

**需求蔓延 (Requirements creep)** 在需求被认为完成后，向产品不受控制地增加新需求。

**需求知识模型 (Requirements knowledge model)** 一种概念性的文件系统——通常实现为数据模型——用于建立沟通需求的通用语言。（示例见附录 D。）

**需求模式 (Requirements pattern)** 一组凝聚的需求集合，执行某些可识别的、可能重复的功能。

**需求规范 (Requirements specification)** 针对特定项目的需求知识完整集合。规范定义了产品，并可以作为构建产品的合同。

- 需求规格文档（Requirements specification document）：一份包含全部或部分需求规格知识的文档，取决于传递对象以及为什么要传递这些知识。
- 需求规格模板（Requirements specification template）：收集和组织需求知识的指南。（附录 A 中有一个示例。）
- 需求工具（Requirements tool）：一种能够维护全部或部分需求规格的软件工具。
- 回顾（Retrospective）：一种旨在总结经验并为改进需求过程提供投入的评审。也称为“教训”。
- 场景（Scenario）：将业务用例或用例分解为一系列利益相关者可以识别的集合。场景用于发现和沟通工作。
- 草图（Sketch）：对某项工作或提议产品的快速粗略的模型或原型。草图可以在任何媒介上（纸张、电子设备、白板）创建，目的是更容易让利益相关者理解和讨论他们的需求。
- 雪花卡（Snow card）：一种显示原子需求属性的纸片。大多数需求使用电子版本的雪花卡。
- 解决方案（Solution）：实现需求的方式。也称为产品。
- 赞助者（Sponsor）：参见客户（Client）。
- 利益相关者（Stakeholder）：任何对产品有兴趣并对其有需求的人，例如客户、用户以及构建产品的人。某些利益相关者是远端的，例如审计员、安全检查员和公司律师。
- 系统（System）：在本书的语境下，指业务或工作系统，而不仅仅是计算机或软件系统。
- 系统性思维（Systemic thinking）：理解事物如何在整体内部影响其他事物的技术。
- 系统分析（Systems analysis）：对系统功能和数据进行建模的技术。系统分析可以通过多种方式进行：根据 DeMarco 定义的数据流建模；根据 McMenamien 和 Palmer 的事件响应建模；根据 Jacobson 的用例分析；或者使用许多面向对象的方法中的任何一种，其中大多数方法都使用统一建模语言（UML）表示法。
- 技术需求（Technological requirement）：仅因为所选技术而才存在的需求；它并不是为了满足业务需求。

## 术语表 (Glossary)

**线上思考 (Thinking above the line)** 推导出并讨论工作的本质。“思考”指的是对可能性的探索，不受（暂时性）技术现实的限制。“线”是*棕色牛模型（Brown Cow Model）*上的水平线，它将物理现实（来源）与本质策略（内容）隔离开。

**时间触发事件 (Time-triggered event)**：由某些时间相关策略触发的事件。例如：“生成销售报告的时间”、“提醒续期许可的时间”。另见*外部事件（External event）*。

**捕获技术 (Trawling techniques)**：用于发现、引导和创新的需求的技术。

**用例 (Use case)**：描述用户/执行者与自动化系统之间交互的功能块。另见*业务用例（Business use case）*和*产品用例（Product use case）*。

**用户 (User)**：使用产品完成工作的人或系统。也称为*执行者（actor）*或终端用户。

**用户故事 (User story)**：一种通过使用指南“作为一名 [ . . ]，我想要 [ . . ]，以便 [ . . ]”来发现需求的技术，该指南被称为故事卡（story card）。

**Volere**：一套为了改进需求的发现、沟通和管理而开发的原则、过程、模板、工具和技术。（*Volere* 是意大利语中表示“希望”或“想要”的动词）

**工作 (Work)**：你的产品旨在改进的组织业务领域。业务分析师在对执行最佳产品或所有工作做出决定之前会对工作进行研究。

**工作范围 (Work scope)**：调查业务的范围，即其周围的现实世界。它通常使用*上下文图（context diagram）*显示。

## 参考文献 (Bibliography)

- Ackoff, Russell, and Herbert Addison. *Systems Thinking for Curious Managers: With 40 New Management Laws*. Triarchy Press, 2010.
- Alexander, Christopher. *Notes on the Synthesis of Form*. Harvard University Press, 1964.
- Alexander, Christopher, et al. *A Pattern Language*. Oxford University Press, 1977.
- Alexander, Ian, and Ljerka Beus-Dukic. *Discovering Requirements: How to Specify Products and Services*. Wiley, 2009.
- Alexander, Ian, Neil Maiden, et al. *Scenarios, Stories, Use Cases Through the Systems Development Life-Cycle*. John Wiley, 2004.
- Alexander, Ian, and Richard Stevens. *Writing Better Requirements*. Addison-Wesley, 2002.
- Allmeyer, Thomas. *BPMN 2.0. Herstellung und Verlag*: Books on Demand, 2010.
- Beck, Kent, with Cynthia Andres. *Extreme Programming Explained: Embrace Change*, second edition. Addison-Wesley, 2004.
- Beyer, Hugh, and Karen Holtzblatt. *Contextual Design: Defining Customer-Centered Systems*. Morgan Kaufmann, 1998.
- Boehm, Barry. *Software Risk Management*. IEEE Computer Society Press, 1989.
- Boehm, Barry, and Richard Turner. *Balancing Agility and Discipline: A Guide for the Perplexed*. Addison-Wesley, 2004.
