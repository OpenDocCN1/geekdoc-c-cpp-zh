
Finally, understanding the infrastructure means making difficult choices regarding how to configure and deploy services. For example, choosing to have the IT department run a separate database server, rely on Amazon's RDS, or keep database systems on its application servers is a complex decision with cost, technical expertise, and system sustainability considerations. Likewise, the IT department must decide how to group and isolate IT services on servers and how to manage server configuration and updates as the number of systems grows.

Being familiar with the IaaS platform includes understanding something about the underlying hypervisor that runs the virtualized computing instances. Though an understanding of the underlying hypervisor is not as important as server management, understanding how hypervisors work is an important element of being able to migrate your server image into new cloud environments. At the very least, your IT department should understand the capabilities of the hypervisor and the service's support for downloading server images and volume snapshots. Although it is possible to migrate between incompatible hypervisors, this can be a difficult and somewhat tedious process (Amazon 2012). Still, there are benefits to migration, particularly for organizations seeking to test virtualization systems locally. In certain IaaS environments organizations may choose to run private cloud systems using a common cloud platform or to test exported cloud servers using locally deployed hypervisors.

## Understanding backup and restoration

Perhaps the most stressful element of moving to the cloud is making sure that your IT department has a robust backup plan. Without detailed backup and restoration plans, stress levels are high indeed and the first loss of data is disastrous. A backup plan at the least must include tested and easily replicated processes for restoring individual files/folders, entire applications, or entire servers. In an IaaS environment, backup and restoration processes should include a method to redeploy the application or data on a different availability zone or cloud platform, be appropriately secure, and be redundant as required to ensure service sustainability. It is important to know that the IT 部门依法有义务应执法部门要求恢复或提供所有备份数据的访问权限，因此制定包含备份轮换、特定归档以及恢复理解的自动化备份轮换计划是良好的实践。可以使用多种方法，但这些方法超出了本书的范围。至少，在评估 IaaS 提供商时，组织应考虑包含哪些备份功能，以及它们如何与现有的备份实践集成。某些提供商确实将备份作为服务的一部分，但可能会额外收费，并且可能只提供特定的恢复服务（例如，恢复完整磁盘但无法检索单个文件）。

## 理解服务器管理、服务监控和复制

服务器管理涵盖服务器配置、监控、安全管理、服务复制和系统更新。至少，服务器管理员应了解如何创建和管理用户，如何安装和保护应用程序，如何加固服务器以抵御攻击，如何将防火墙用作额外的安全层，以及如何自动化日志和日志轮换。服务需要以能够抵抗配置退化、抵御功能被破坏的尝试、并且能够轻松恢复或重新配置的方式设计。

测试复制服务器能力的最佳方法是仅使用系统备份从头开始恢复它。在可能的情况下，流程应实现自动化，并且在检测到服务中断时应建立新的流程。在云环境中，故障转移计划必须包括能够在单个云提供商的不同可用区之间移动或迁移到其他云提供商的能力。RightScale 等服务通过支持跨多个提供商复制服务器的机制简化了这一过程。同样，Amazon 提供了通过命令行工具迁移服务的选项。作为这一过程的一部分，了解在可用区中断情况下可用的服务非常重要。

IT 部门中正在获得支持的另一种服务器复制方法是自动配置和服务器部署，而不依赖云提供商。Puppet 和 Chef 等服务器配置工具用易于部署的配置脚本取代了“金蛋”方法。这些脚本记录了服务器创建和配置过程中的每个步骤，直到数据恢复和投入生产为止。使用这种“可操作”的配置文档，IT 部门可以通过快速恢复服务并使用配置脚本监控运行中的服务器来避免停机，从而节省大量时间。自动配置在 IaaS 提供商中变得越来越普遍。Amazon（通过 CloudFormation）、Linode 和 RightScale 都提供内置的脚本化配置服务。虽然这可能不是极大规模 IT 环境的最佳实践，这些环境更喜欢在特定云提供商之外托管其配置服务，但使用内置的服务配置工具在无需学习和管理另一个 IT 管理工具的开销的情况下，极大地提高了服务的耐久性。

与 IaaS 服务合作的另一个重要部分是确定服务器容量需求。这里讨论的所有 IaaS 提供商都提供各种 CPU、RAM 和存储空间选项，但可能有必要在多个平台上测试应用程序安装以找到性能最佳且最经济的配置。例如，Uspal 等人（2011）采用多方面的方法测试 AWS 服务器容量，与同等规模的本地虚拟化和物理服务器进行比较。尽管服务器 CPU 容量和可用内存存在差异，但所有三台服务器均使用运行在约 2 GHz 的 Intel Xeon CPU，并具有 6–8 GB 的 RAM。研究人员在所有三个服务器平台上使用名为 Bonnie++（`www.coker.com.au/bonnie++`）的输入/输出文件测试系统、MySQL 数据库加载例程以及 ImageMagick（`www.imagemagick.org`）对 1000 万张图像进行图像处理例程，以比较服务器性能。他们的测试发现，Amazon 服务器在全部三项测试中均优于本地物理服务器和本地虚拟化服务器，其中与文件输入和输出操作相关的差异最为显著。例如，在 Bonnie++ 测试中，Amazon 服务器的读取操作完成速度为每秒 92K，而物理服务器为每秒 38K，本地虚拟化服务器为每秒 18K。磁盘写入和 ImageMagick 处理显示出类似的结果。

IT 服务监控是高效服务管理的另一个关键方面。监控越来越多地成为 IaaS 系统的内置功能，但通常侧重于服务器监控而非应用程序监控。服务器资源监控（例如 CPU 负载、硬盘使用率、输入/输出）很重要，但应用程序监控也很重要，因为它使 IT 部门能够在应用程序崩溃前采取行动。大型 IT 部门可能拥有复杂的监控系统，但即使是小型部门也需要确保服务正常运行的监控解决方案。对于寻求大量控制的组织，Nagios（`http://nagios.org`）等系统可提供对应用程序、磁盘利用率、CPU 利用率以及其他各种资源的监控。Nagios 也有 SaaS 替代方案，包括 New Relic（`http://newrelic.com`）和 LogicMonitor（`http://logicmonitor.com`），它们提供类似规模的监控服务。Nagios 适用于复杂监控，但本章介绍的每个 IaaS 提供商都提供不同形式的监控。例如，Amazon 在不同层级监控服务器和基础设施状态，并提供多种通信方式。Monitor.Us（`http://monitor.us`）等 SaaS 服务提供易于使用的基于 Web 的服务监控。

## 能够谨慎预算

与 SaaS 和 PaaS 系统相比，IaaS 系统的预算编制要难以预测得多。例如，组织必须能够预测服务的带宽、存储利用率和 CPU 需求，并随时间推移预测容量需求。包括 Amazon 在内的 IaaS 提供商为愿意承诺特定期限的组织提供更低的成本，因此能够在一年到三年内预测资源利用率可以带来可观的成本节约。这对组织来说是好事，但要求系统管理员知道组织何时需要续订其预留实例条款。在到期日前未提前续订会导致服务器运行成本大幅意外增加。尽管预算编制通常是行政职能，但 IaaS 基础设施的众多变动部分意味着 IT 人员更有可能被要求确定运行 IT 服务的成本。

## 服务复杂性、可持续性和耐久性

IaaS 平台的主要缺点之一是其复杂性。图书馆经常发现 IaaS 服务比传统服务器平台更复杂，并且通常没有足够的 IT 资源来确保可持续的服务。避免不必要复杂服务的关键包括使用单一服务器平台和应用程序环境、使用单一方法管理所有服务，以及避免不增加显著改进的复杂服务调优。例如，在传统 IT 环境中，优选使用逻辑卷管理（LVM）方法，该方法允许卷跨多个磁盘。借助 LVM，IT 部门可以在不中断服务或复杂重建磁盘空间的情况下动态添加卷空间。这种方法的主要缺点是 LVM 需要配置文件和静态磁盘集。在云环境中，镜像、增加、分离和重新附加卷要容易得多。这在一定程度上削弱了 LVM 提供的优势，并具有额外的好处，即能够在无需跟踪 LVM 配置文件和卷关联的情况下轻松镜像、复制和恢复磁盘映像。

发现自己管理 IaaS 环境但超出舒适区的图书馆可以转向高级支持服务，或通过使用单一系统配置并转向自动化来简化服务部署 management tools. Automated backups, automatic configuration, and regular monitoring and notification services go a long way in helping library IT feel more comfortable with IaaS management responsibilities and can lead overall to a more efficient IT organization. Another approach to simplifying an IaaS environment is to identify services, such as database servers, monitoring services, server builds, or e-mail services, that can be outsourced to a PaaS or SaaS platform. By taking these base-level services out of the mix, organizations can focus on running customized services for only the applications that require them.

## Service Cost

IaaS services often cost less than their SaaS and PaaS counterparts, primarily because the latter include value-added services such as IT management, data management, and premium service levels. At the very least, a service cost comparison should include the hard costs of server run-time, storage space, bandwidth, backup, and related infrastructure (e.g., monitoring, documentation, software licensing). A full cost consideration also needs to include hidden or soft costs including those for personnel time, infrastructure management, replication and redundancy plans, and data management. Though planning for and incorporating such soft costs is difficult, even a basic attempt can help organizations fully understand the long-term costs of cloud computing. There are SaaS services such as Cloudability (`http://cloudability.com`) whose primary focus is on monitoring the use of common SaaS, PaaS, and IaaS services and triggering notifications when services are likely to expire or exceed limits.

## Service Portability and Interoperability

Although interoperability between applications in an IaaS environment is less of an issue than in SaaS or PaaS environments, given the control an IT department has over the infrastructure, ensuring IT system portability and interoperability with other systems is a more complex issue. Operations such as firewall administration, user account management, and service management enable application interoperability and data transfer. The larger issue with IaaS platforms is the challenge of moving the entire service to a new platform. This capability has seen increasing support in recent years, and now many IaaS systems support some form of system migration. In addition, services such as RightScale offer configuration management services that help replicate cloud platforms and data across multiple providers. At the very least, a cloud computing plan should include short-term replication and long-term migration planning elements. This may include documenting the server image and data download and redeployment process, server configuration process, and DNS reassignment process.

## Comparing Costs across Providers
