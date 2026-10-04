

## 第 1 步
云配置

## 第 2 步
云处理

预配置

- 同源基因计算
- 实例化
- HDFS
- S3
- 任务流执行
- 全对全 blast (All-v-All)

**图 1.10** 在 EC2 上使用 MapReduce 框架进行 RSD 的工作流 (38)。来源：Wall, http://bmcinformatics.biomedcentral.com/articles/10.1186/1471-2105-259。根据 CC BY 2.0 协议使用 http://creativecommons.org/licenses/by/2.0。

CloudBurst，Schatz (39) 设计了一种名为 CloudBurst 的并行算法，这是一种基于流行的读段比对程序 RMAP (35) 在 Hadoop 平台上的“种子-扩展”读段映射算法。根据 MapReduce 模型，CloudBurst 修改了 RMAP 以在多台机器上并行运行。CloudBurst 的工作流包含两个阶段：Map 阶段和 Reduce 阶段，如图 1.11 所示。mapper 生成的键值对具有以下格式：<reads> 和 <references>，即读段和参考序列的 k-mers，它们在共享 k-mers 的读段与参考序列之间执行端到端对齐。最终结果被转换为与 RMAP 标准格式相同的文件，因此 CloudBurst 可以在流水线中替代 RMAP。CloudBurst 的运行时间随处理器数量的增加而线性扩展。在具有 24 个处理器核心的配置下，在相同输入集的情况下，CloudBurst 的速度比在单核上执行的 RMAP 快了多达 30 倍 (39)。

Nguyen 等人 (41) 开发了 CloudAligner，这是一种基于 MapReduce 的用于处理长读段映射的应用程序。它利用 Map 阶段在参考序列上定位读段。工作流如图 1.12 所示。CloudAligner 接受两种输入类型：读段和参考序列，将读段分成多个块并分发到多个 mapper。CloudAligner 能够处理多种类型，包括比对、亚硫酸盐比对和双端比对，并将读段比对到参考序列。实验结果表明，通过 CloudAligner 使用 MapReduce 模型显著提高了效率。

## 洗牌 (Shuffle)

![](460851ce3bbf26940.png)

**图 1.11** CloudBurst 的工作流。来源：Schatz (39)。

![](460851ce3bbf26940.png)

**图 1.12** CloudAligner 的工作流。来源：Nguyen, http://bmcinformatics.biomedcentral.com/articles/10.1186/1471-2105-259。根据 CC BY 2.0 协议使用 http://creativecommons.org/licenses/by/2.0。

## 单核苷酸多态性 (SNP) 检测
单核苷酸多态性 (SNP) 是基因组中单个碱基的变异。在云计算中，SNP 检测高度依赖于数据，特别是对于基因组分析，这至关重要。为了实现 SNP 检测的解决方案，CloudBurst 提出了一种基于 Hadoop 的工具，即 Bowtie。它包含三个阶段：Map 阶段、排序阶段和 Reduce 阶段。在 Map 阶段，mapper 将短读段比对到参考序列。在排序阶段，Hadoop 平台根据键值对这些比对进行分组。在 Reduce 阶段，reducer 简单地调用 SNP。实验显示，CloudBurst 使用 32 个核心仅花费 3 小时即可完成检测。

## 数据即服务 (DaaS)
DaaS 旨在以各种格式从多个来源提供数据服务，用户可以通过互联网访问。DaaS 允许按需访问数据，而无需使用本地文件系统。此外，数据的共享加速了与其他研究者的合作。DaaS 的一个例子是 AWS，它提供了一个公共数据中心，包括 GenBank、Ensembl、1000 Genomes、模式物种百科、UniGene 和流感病毒。AWS 还包含许多数据，例如天文学、化学。

## 1.5 结论与展望
在本章中，我们首先讨论了 NGS 技术在存储、传输和分析方面带来的挑战。阐述了两类编程模型：MapReduce 和任务模型，以说明并行思想。然而，并非所有数据密集型算法都能轻松迁移到云平台。因此，需要合适的并行策略和更强大的云平台。常用的并行策略有三种：

- 直接并行：许多生物信息学任务（如 BLAST）是显式数据独立的。只需较小修改即可在云平台上运行。这种类型的加速与集群的计算呈近线性关系。
- 迭代并行：多次运行 MapReduce 或执行程序是复杂任务（如 RSD）的另一种解决方案。还可以考虑如何存储、分配和收集中间数据。如何设计高效的方法是一个根本性挑战，因为临时数据在执行过程中可能太大。
- 数据转换并行：对于某些复杂问题，需要对数据和算法本身进行转换以利用云优势。例如参考文献 60 中的。虽然我们在本章中没有介绍，但值得注意的是我们可以智能地改变输入格式以促进云解决方案的发展。

对于生物信息学，不仅限于 NGS 数据分析，云计算处于早期阶段。更强大、更易用的云平台和编程模型有望问世并投入，以解决复杂的科学问题。最终，所有科学家将从各个领域的新计算能力中获益。

