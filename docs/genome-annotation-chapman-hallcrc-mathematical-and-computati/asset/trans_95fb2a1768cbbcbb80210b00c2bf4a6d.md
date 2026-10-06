

# 196 基因组注释

来自 Solexa 和 SOLID 机器。这些短读段（short reads）每个提供的信息很少，导致组装困难，特别是在处理那些来自基因组内重复区域的 reads 时。为了弥补这一缺陷，NGS 测序读取相对于待组装基因组的大小需要高覆盖度，这导致任何特定基因组产生的 reads 数量剧增。现在单次机器运行即可产生 5 亿条单独的序列 reads！

已知某些新技术会产生一些特征性的系统性错误，例如难以估计同质聚物区域（即单碱基重复）的长度，以及向 reads 的 3' 端碱基识别错误率增加。所有上述测序技术都包含每个碱基识别的置信度估计值作为质量值。这些 NGS 数据的特征可以总结为：组装过程中歧义性的增加，以及下游处理信息总量的指数级增长，这为 NGS 数据分析流水线带来了计算挑战。需要更具计算密集型的算法来应对这种歧义性，同时还需要更多的计算能力和充足的存储空间来容纳序列和其他类型的基因组数据。最近对 NGS 分析的计算挑战进行了回顾（Li et al., 2011; Pop, 2009）。

## 11.2 基因组重组

大多数 NGS 数据分析工作流的首要任务是从短的个体 reads 开始重组出尽可能完整的基因组序列，而这些 reads 本身几乎没有意义。当已知测序 reads 来自哪个物种时，如果存在同种或极近缘物种的参考基因组，可以将它们比对到先先测序并注释的参考基因组。比对过程的目标是确定每个 read 在参考基因组序列中可能的可能的来源位置。比对方法仅适用于对特定物种内的近缘物种进行重测序（resequencing）或遗传图谱比较。例如，通过 NGS reads 比对已进行了一项关于拟南芥（Arabidopsis thaliana）菌株间遗传变异的研究（Ossowski et al., 2008）。

当被测序的物种与任何现有测序基因组都不相似时，必须从 reads 集合从头（de novo）重组其基因组序列。虽然这在计算上并不可逾越，但在算法复杂性和计算资源方面，从头基因组组装比比对的要求高得多。由于这种困难，短 reads 的从头组装主要应用于细菌基因组重组（Butler et al., 2008; Chaisson and Pevner, 2008）或哺乳动物人工染色体（Zerbino and Birney, 2008）。还需要注意的是，比对和组装方法并不总是以互斥的方式使用的。如果新基因组的某些区域无法比对到参考基因组的任何地方，则这些区域需要从头组装。

### 11.2.1 比对到参考基因组

尽管早期的比对工具如 BLAST（Altschul et al., 1990）、Clustal（Chenna et al., 2003）和 T-Coffee（Notredame et al., 2000）多年来一直很流行且仍在广泛使用，但它们的主要目的是在大型数据库中搜索较小的同源序列，或者对给定的序列集进行比对以研究其演化关系。相比之下，NGS 数据的短 reads 比对需要将这些 reads 映射到同种或极近缘物种的参考基因组，目标是检测结构变异或引导基因组重组。因此，与经典比对算法不同，大多数短 reads 比对算法假设非匹配碱基源于特定序列内的变异而非演化突变。这种底层假设上细微但重要的差异允许为 NGS reads 实现较快的比对算法，因为通常情况下允许的错配较少，且参考序列中的初始候选位置可以迅速缩小到可处理的数量。

大多数短 reads 比对力求在处理速度和比对准确性之间取得平衡。结果，这些算法通常采用两步策略：第一步通过采用简单的启发式方法（例如在 read 开头预设数量的碱基中进行精确匹配）在参考基因组中寻找数量较少的潜在位置以映射每个 read。一旦确定了候选映射位置，就会在第二步中将更准确但较慢的比对算法（例如 Smith–Waterman 算法的变体，Smith and Waterman, 1981）应用于序列集。第一步中采用的启发式方法的严格性通常可以由用户通过一组参数进行控制，例如匹配的碱基数量和这些碱基中允许的错配数量。

最近，出现了许多用于 NGS 短 reads 比对的新软件工具。这一波发展的动力主要是传统比对算法无法高效处理海量短 reads，以及所开展测序项目的基因组尺寸不断增大。上一代工具大多设计用于处理较少量的 reads。一些最常用的 NGS 比对工具包括 Bowtie（Langmead et al., 2009）、SOAP（Lin et al., 2009）、BWA（Li and Durbin, 2009）、SHRiMP（Rumble et al., 2009）、mrFAST（Alkan et al., 2009）、mrfFAST（Hach et al., 2010）、ZOOM（Lin et al., 2008）、SSAHA2（https://www.sager.uk/resources/software/ssaha2）（（Ning et al., 2001）以及 Mosaik（http://bioinformatics.bc.edu/Mosaik）。最近对这些算法中的几种进行了性能比较，标准是基于正确映射和错误映射 reads 以及未映射 reads 数量的准确性（Ruff et al., 2011）。

### 11.2.2 从头组装

从短 reads 重组基因组序列最大的挑战之一是在没有参考基因组的情况下处理重复序列，特别是当 reads 短于重复长度时。增加 reads 的覆盖度是解决这一困难的主要策略，NGS 组装算法利用了这一点。例如，对于 454、Illumina 和 SOLID 技术，覆盖度分布是不均匀的（Sheendure et al., 2009）。由于这些覆盖度模式取决于特定的测序技术，对多种技术进行组装的研究已经进行并得到了结果（Aury et al., 2008; Reinhardt et al., 2009）。NGS 组装算法使用计算策略来应对大量 reads 的复杂度。在穷尽重比较的情况下，每个 read 都需要与其他所有 reads 进行比较，导致组合爆炸。为了效率，大多数从头组装算法在某种程度上利用了 k-mer 的概念。与其寻找 reads之间的重叠，不如寻找具有相同 k-mer 的 reads 并对其进行比较。然而，k 值必须仔细选择，以防漏掉真实的重叠并减少假阳性重叠。此外，大多数组装算法还使用紧凑图作为 reads、contigs 及其关系的表示。

在过去几年中发布了许多从头组装工具。第一类组装工具被称为贪心算法，其中通过添加得分最高的重叠来扩展给定的 read，这种基本操作用于连接 contigs。这一类的工具包括 SSAKE（Warren et al., 2007）、SHARCGS（Dohm et al., 2007）和 VKACE（Jeck et al., 2007）。下一种主要的组装策略是布局-共识（OLC），它包含三个步骤：(1) 计算所有 reads 之间的重叠；(2) 将它们布局在图中，连接重叠的节点；(3) 最后通过分析图生成共识序列。例如，Newbler（Margulies et al., 2005）、Celera Assembly（Myers et al., 2000）及其针对 454 数据的扩展 CABOG（Miller et al., 2008）、ARACHNE（Batzoglou et al., 2002）和 Edena（Hernandez et al., 2008）都是基于德布罗因图（DBGs）的组装工具，其中 reads 首先被切割成 k-mer，使用这些 k-mer 构建 DBG，然后从 DBG 中推导出基因组序列。组装软件如 EULER-USR（Chaisson et al., 2009）、Velvet（Zerardino and Binney, 2008）、AByss（Simpson et al., 2009）、ALLPATHS-LG（Gnerrea et al., 2011）和 SOAPdenovo（Li et al., 2010）属于最后一类。关于组装算法和工具的几篇回顾已经发表（Flicek and Binney, 2009；Li et al., 2011; Miller et al., 2010; Sheendure and Ji, 2008）。

