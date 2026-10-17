
For libraries seeking to use SaaS solutions to fill these gaps, there are an increasingly large number of case studies that explore SaaS alternatives to traditional library solutions. For example, Wilson (2011) explores the use of `Drupal`, `Basecamp` (`http://basecamphq.com`), and `MIRA` (`http://atlassian.com/software/jira`) as an alternative platform for electronic resource management systems. Wilson explores the challenges associated with adapting these platforms to serve a very specific function, as opposed to the implications of using an SaaS platform for this service, but the reported success of all three services point to an opportunity for these types of tools to have a dramatic impact on library IT decisions.

Perhaps the largest challenge in this adoption environment is managing the budgetary, license, identity management, and functional interoperability of these systems. Although many providers feature some form of integration through web-based plug-ins, back-end indexing, or automated data loading, making these services work together can be challenging, particularly for libraries interested in offloading as much technical work as possible. Unfortunately, these challenges may not emerge until a specific system is implemented or need found, and it can be difficult for libraries without in-house IT staff to identify potential solutions.

These data and interoperability problems do not have easy one-size-fits-all solutions, but there are potentially useful options. For example, Peter Murray (personal communication, March 2012) observed that `Lyrasis` tunes its hosting services based on library need and worked with outside consultants to bring data migration services to the table for libraries adopting its hosted IT services. In addition, there are IaaS providers whose primary purpose is to enable interoperability in an SaaS environment. Two examples are `SnapLogic` (`http://snaplogic.com`) and `Jitterbit` (`http://jitterbit.com`). These providers support data connections using a range of data sources (e.g., `XML`, `CSV`, `ODBC`), include a data migration design interface, and support HTTP endpoint services in which data queries and publishing actions can be activated by REST-based HTTP requests. These services require detailed data analysis skills; still, they may enable libraries to avoid implementing expensive IT infrastructure for otherwise lightweight data conversion services.

这四种方法强调了云解决方案中不同的优势和劣势，可以作为图书馆转向云计算的起点。第一种方法强调使用单一云提供商的简单性和控制力，但也认识到通过广泛使用提供商API而被锁定的风险。第二种方法试图通过使用多个提供商并利用SaaS解决方案来监控、管理和审计这些提供商，从而减轻部分风险。这种方法展示了跟踪云基础设施和支出的好处，并表明SaaS解决方案是提供基础设施管理支持的一种方式。第三种方法侧重于从IaaS提供商抽象系统设计和实现的服务，并展示了轻松使用多个云平台的好处；尽管如此，它很复杂，可能需要超出第一和第二种方法的IT和资金资源。第四种方法认识到图书馆很可能转向完全基于SaaS的解决方案来满足技术需求。在这种情况下，运营、管理和服务质量问题比技术问题更为重要。

在现实世界中，图书馆很可能会采用不止一种方法。事实上，大多数图书馆已经在某种程度上依赖SaaS提供商或外包信息服务。在决定是否扩大这些角色，或在将新服务迁移到云端时考虑其他方法时，本地资源、专业知识、IT支持能力、组织政策和服务需求等问题是有用的因素，可以使一种方法比另一种方法更可行。无论选择哪种方法，容量规划、服务质量监控、服务集成和资源利用监控等IT服务要素都是可持续IT基础设施的重要组成部分。本章其余部分将探讨这些问题，并为开始使用云计算提供建议。

## 准备采用云计算

图书馆IT部门的发展是为了响应特定的图书馆需求，如客户支持、ILS支持和DAMS支持。仍然常见的是，IT图书馆员拥有IT学科以外的背景，但也有一个趋势在图书馆会议和文献中被记录，即采用行业标准的IT软件开发和服务管理方法（Chang 2010; Dougherty 2009）。这些文章讨论了图书馆正在采用IT服务模型，包括正式的模型，如信息技术基础设施库（ITIL）（`www.itil-officialsite.com`）和较非正式的模型，如ITSM（`www.itsm.info/ITSM.htm`）。即使对于尚未使用此类模型的图书馆，也存在服务管理门户的使用（McHale 2010），并且对社区驱动软件开发责任的认识日益增强（Reese 2012）。

正如我们对云方法的探索所强调的，需要正式的IT管理实践。对于主要转向SaaS解决方案的图书馆，IT管理的重点应放在维护服务提供商和支持信息的内部网上。对于更多转向PaaS和IaaS解决方案的图书馆，更正式的支持策略有助于使解决方案的实施和管理可持续。有多种模型可供选择，包括`ITIL`、系统开发生命周期（Department of Justice 2003）、信息及相关技术控制目标（ISACA 2011）和微软操作框架（Microsoft 2011）。这些模型帮助IT组织以系统的方式处理IT服务的系统选择、开发、实施、管理和退役，对任何类型的图书馆都有帮助。尽管每个模型都有其独特的特点，但已经尝试在这些模型中寻找相似的过程和共同点（Pollard et al. 2009; Susanto et al. 2011）。这些模型的批评者指出，IT服务模型的采用并未证明IT服务的改进，并断言它们创造了行政开销，并可能导致武断边界的创建（Addy 2007, 4）。

服务管理是一个广泛的概念，定义为“一组专门的组织能力，以服务的形式为客户提供价值”（ITIL 2011, 11）。`ITIL`服务生命周期描述了开发、交付和管理服务的过程，并特别关注知识管理、SLA和标准化。服务管理模型可以提供标准化的成功衡量标准，包括解决时间、未结与已结事件的比例、支持的服务数量以及IT人员的时间投入。

例如，`ITIL`服务模型讨论了服务的三个阶段：开发、转产和运营支持。这些过程中的每一个都涉及各种离散的服务组件，包括定义服务水平需求、评估IT支持容量、定义安全需求和记录用户期望。Addy (2007, 50) 提供了需要定义的领域的完整列表，包括用户、用户需求、预期交付物、用户提供的信息或数据、服务交付方法、角色和责任、合同要求、成功衡量标准、服务可用性定义、服务容量衡量标准、安全标准和成本要求/履行。虽然处于纳入正式IT服务管理方法阶段的读者最好更深入地探讨这些领域，但当您的组织探索云解决方案时，即使是非正式地意识到这些问题也很重要。

这里提到的每个IT服务模型在云环境中都能很好地工作，但有些正在探索特定于云采用的问题。例如，微软操作框架（2011）探讨了SaaS、PaaS和IaaS环境中哪些系统元素（如网络、存储、数据、应用程序）是本地管理还是远程管理。将通用IT服务指南应用于云环境的最佳实践建议包括对沟通、服务和问题解决的改变。例如，微软指南建议在服务目录中添加元素级云服务，以确保用户了解可用的核心云服务及其实施成本和参数。拥有关于组织已使用的云平台的文档，有助于指导围绕IT服务采用的讨论和决策，并可能防止以脱节的方式使用多个云服务提供商。微软的指南还建议尽可能自动化服务并利用云平台的自助服务功能。

对于从事IT服务重新评估、探索向云资源转移，或仅仅有兴趣寻找重新设计IT服务方法途径的图书馆，了解IT服务模型和标准有助于指导组织变革。这可能导致集中式的图书馆IT，特别是在转向PaaS或IaaS解决方案的组织中，也可能导致更分散的IT环境。在这两种情况下，使用某种形式的服务目录、知识管理系统和服务工单系统，可以帮助图书馆跟踪IT发展，并就其IT服务变更做出明智的决策。尽管有设计完美系统的动机，系统管理员应注意过度承诺复杂系统配置和管理实践的风险。事实上，通过使用云环境来托管服务目录、知识管理和工单管理系统，图书馆IT部门既可以利用SaaS解决方案的效率优势，也可以表明他们愿意“吃自己的狗粮”。将这些内部服务迁移到云端或首先在云端部署它们的做法，也可以成为图书馆环境中采用云服务影响的良好试验场。

虽然很难量化IT服务部门的服务容量，但作为IT服务模型一部分的度量标准和框架可以帮助衡量应用程序和资源的使用情况。同样，如果明智地应用，这些IT服务模型可以扩展IT部门的优势，使少量IT人员能够更轻松地管理大量请求。也许这些服务模型最重要的原则是，IT服务提供商设定了对客户和服务提供商都有效的界限和期望。虽然这通常在SLA中正式化，但这些协议不一定需要复杂，至少可以帮助避免误解和客户期望的错位。

### 为新服务腾出空间

对于探索云端的组织，一个重要的问题是云计算如何帮助图书馆支持新的或不同的服务。这里需要考虑几个重要的IT和组织问题，包括服务需求、用户期望、IT平台选项、成本考虑以及法律/组织政策。了解约束和剩余在哪里，可能有助于引导讨论，并帮助组织了解其精力应最好地分配在何处。例如，人员限制和缺乏专业知识可能意味着图书馆倾向于转向SaaS解决方案。正如前一节所指出的，使用SaaS解决方案并不能消除对IT服务管理任务的需求。相反，随着图书馆转向更多的SaaS解决方案，对跨部门服务目录和知识/工单管理系统的需求增加了。在SaaS服务的许可、管理和部署分布在多个部门的组织中，这种需求甚至更大。

对于发现需要定制化或本地化服务意味着使用PaaS或IaaS的组织，识别常见或非差异化服务（这些服务资源利用率高但影响低）并将其转移到SaaS解决方案可能会很有用。这可能包括系统和services that were once the bread and butter of library IT departments, ILSs, and electronic resource management systems. Likewise, new library services such as large-scale discovery, resource recommendation, and resource sharing depend on network-based services to such an extent that they work only as an SaaS solution.

## Build Support for the Migration

Some of the major internal limitations of moving to cloud computing include local policy, staff expertise, lack of cooperation with organizational IT, lack of funding, and lack of satisfaction with provider terms. Many of these issues require administrative-level work with providers; nevertheless, understanding and addressing the limitations of current staff expertise through new recruitment or training can dramatically improve an organization’s ability to adopt cloud solutions. It is not necessarily easy, but building internal capacity for software programming, IT service, and server administration increases the number of options in IT adoption and facilitates management of SaaS as well as PaaS and IaaS solutions.

Organizational resistance to cloud migration can be difficult to overcome. Marketing the shift as an opportunity to redefine service relations between libraries and organizational IT or to enable new collaborations can help resistant departments see how cloud adoption can benefit them. Libraries moving to the cloud are likely to depend on some key services from their organization’s IT, including `DNS` resolution, firewall support (for both incoming and outgoing ports as needed), and advice on IT issues. It makes sense for libraries to be well informed about legal and policy issues before heading to IT departments and to be prepared to take on the liability of service uptime and capacity planning in a formal document. Often, IT organizations are guided by a need to define and understand service boundaries. By recognizing these boundaries and taking appropriate responsibility, libraries can often be successful in renegotiating a relationship with organizational IT management that is beneficial for both parties.

## Leverage Vendor-Provided Tools

One of the key advantages of adopting cloud services is the built-in service infrastructure that comes with even the most basic services. For example, Amazon has a site dedicated to informing cloud customers about value-added applications (`http://aws.amazon.com/customerapps/`). These services include mobile AWS management tools such as `iAWSManager` and value-added services such as
