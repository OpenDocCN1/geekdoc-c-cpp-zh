
# 高性能并行 I/O (Chapman & Hall／CRC 计算科学系列第 22 )

编辑：

PRABHAT • QUINCEY KOZIOL

丛主编辑

Horst Simon

副主任

劳伦斯·伯克利国家实验室

美国加利福尼亚州伯克利

编辑：

# PRABHAT

劳伦斯·伯克利国家实验室

美国加利福尼亚州

# QUINCEY KOZIOL

HDF Group, Urbana-Champaign

美国伊利诺伊州

Galen Shipman

- 3 国家超级计算应用中心 17

William Kramer, Michelle Butler, Gregory Bauer, Kalyana Chadadava, 和 Celso Mendes

- 4 阿贡纳领导设施 33

William E. Allock 和 Kevin Harms

Richard Hedges 和 Blaine Barney

- 6 洛斯阿拉莫斯国家实验室 65

Gary Grider

7 德克萨斯先进计算中心 (TACC) 79

Karl W. Schulz

Eric Barton and Andreas Dilger

Dean Hildebrand and Frank Schmuck

Walt Lyman 和 Boyd Wilson

Nick Kirsch

+ Mike Folk

+ John Bent

+ Rob Latham

+ Quince Kozi, Russ Mew, Mark Howison, 和 Marc Poito

+ Norbert Podhorszki, Scott Klaky, Qing Liu, Yuan Tian, Manish Parashar, Karsten Schwan, Matthew Wolf, 和 Sriram Lakshminarayan

- 17.4 结论 211

+ Venkatram Vishwanath, Huy Bui, Mark Herrell, 和 Michael E. Papka

+ Sundra Byna, Prabhat, Karim, 和 William Daughi

+ Mark Miller

# 21 Silo: 科学数据库 249

+ Scott Klaky, Gary Liu, Hasan Abbasi, Norbert Podhorszki, Jackie Chen, 和 Hemmanth Kolla

+ Christopher Mitchell, David Bonnieie 和 Jonathan Woodring

- 24.1 引言 279

- 24.2 I/O 基准测试 280

Sameer Shende 和 Allen D. Maloney

David Skinner

Philip Carns

Mark Howison, Prabhat, Surendra Byna

John Shelf

- 29.3 结论 331

Dries Kim 和 Robert Ross

Gary Grider 和 Nathan Deeleben

- 32.5 结论 360

Matthew L. Curry, H. Lee Ward, David Martinez, Jill Gemmill, Gary Grider 和 Anna Maria Bailey

## 前言

在日益强调“大数据”的时代，高性能并行 I/O 主题在文献中本应得到充分的。毕竟，如果不理解如何快速高效地读写所有数据，那么讨论不断增长的数据洪流又有什么意义呢？然而，奇奇的是，在搜索并行 I/O 相关书籍时发现，自从十年前以来，还没有有人尝试过为高性能计算 (HPC) 社区以以书的形式来总结我们高性能并行 I/O 的现状。

Prabhat 和 Quincey 通过编辑这本名为《高性能并行 I/O》的书，取得了巨大的成就。这本书确实非常非凡，因为在过去的十年里，并行 I/O 的技术、软件和工具取得了如此巨大的进步，但对这些进展的文档记录却显著缺失。I/O 往往是实现 HPC 最佳可能性能的瓶颈，但其处理和讨论通常次于对 CPU 性能的讨论。作者们致力于解决这一缺陷，并取得了非常成功。他们的文本为这个快速发展的领域提供了实用的概述，而该领域目前在任何书中都没有得到体现。

本书的一个重要区别是，它是由该领域的从业者编写的。编辑者和章节作者都曾亲自参与并行 I/O 软件的开发，以及在大规模并行 I/O 系统上迁移和优化科学应用。这种实践经验使编辑者在选择书籍的主题时，转向了一组高度实用的主题：目前领先 HPC 中心所实现的并行 I/O 系统概述、当前文件系统和 I/O 库的综述，以及并行 I/O 工具的选择。各章节由该领域的顶级专家贡献。这本书将是应用开发者的得手参考。

并行 I/O 是现代高性能计算 (HPC) 的不可或缺的组成部分。Petascale 级模拟通常产生 TB 到 PB 级的数据集，这些数据需要高效存储。以数据为中心的分析和可视化工具依赖于高效的读取。读和写操作对于促进科学发现至关重要。这本书捕捉了 2013-2014 年并行 I/O 的现状。我们借鉴了从业者、研究人员、软件架构师、开发者和科学家的见解。

本书分为六部分。第一部分旨在让读者了解如何配置和运行系统，特别强调 I/O 选择、中间件和应用。来自国家能源计算中心 (NERSC)、阿根纳领导计算设施 (ALCF)、利物浦计算中心和德克萨斯先进中心 (TACC) 的专家在书中分享了观点。

随后，本书遍历了 I/O 栈。第二部分处理文件系统层。领先的设计师和架构师分享了关于主流文件系统 Lustre、GPFS、OrangeFS 和 OneFS 的设计、架构和应用。在第三部分，我们回顾了中间件（如 MPI 和 PLFS）以及面向用户的库（如 Parallel-NetCDF、HDF5、ADIOS 和 GLEAN）。这些章节提供了库开发者的决策、库功能和应用的见解。

第四部分处理利用 I/O 基础设施的真实科学应用。应用和库开发者提供了粒子场、随机、有限体积和直接数值模拟的案例研究。仔细的性能分析和优化对于获得峰值（及持续）并行 I/O 性能至关重要。第五部分介绍了领域从业者使用的性能分析和基准工具。最后，HPC 世界处于变动之中。第六部分讨论了 HPC 当前趋势对百亿级时代并行 I/O 的影响。

# 致谢

感谢 Mary Hester 在校对和编辑文本方面付出的卓越工作。她模范般的耐心勤奋极大提升了书籍的质量。Wes Bethel 和 Mike Folk 鼓励我们承担这个项目。Taylor and Francis 的 Randi Cohen 对我们的努力提供了很大支持，并对我们的问题非常有耐心。我们都在伯克利国家实验室的计算研究部门以及 HDF Group 拥有良好的支持环境，我们要感谢我们的同事。最后，我们要感谢家人提供的支持和爱。

Prabhat, Quincey Koziol

伯克利实验室，2014年9月

# 致谢

编辑们感谢劳伦斯·伯克利国家实验室（Lawrence Berkeley National Laboratory）和 HDF Group 提供的支持。本工作由美国能源部科学办公室、先进科学计算研究办公室的主主任支持，合同号为 DE-AC02-05CH11231。

## 第 1 章—高性能计算（HPC）设施中的并行 I/O

本工作由美国能源部科学办公室、先进科学计算研究计划赞助，并在橡克里奇国家实验室（Oak Ridge National Laboratory, ORL）完成。该实验室由 UT-Battelle, LLC 为美国能源部管理，合同号为 DEAC0500OR22725。

## 第 2 章—国家能源研究科学计算中心

本工作由美国能源部科学办公室、先进科学计算研究办公室的主主任支持，合同号为 DE-AC02-05CH11231。本研究使用了国家能源研究科学计算中心（NERSC）的资源。

## 第 3 章—国家超级计算应用中心

本研究是 Blue Waters 持续 peta亿级项目（sustained-petascale project）的一部分，该项目由国家科学基金会（奖励编号 OCI 07-25070）和伊利诺伊州支持。Blue Waters 是伊利诺伊大学厄巴纳-香槟分校及其国家超级计算应用中心的合作成果。

## 第 4 章—阿根领先计算设施

本研究使用了位于阿根国家实验室的阿根领先计算设施（Argonne Leadership Computing Facility）的资源，该设施由美国能源部科学办公室通过合同 DE-AC02-06CH11357 支持。

# 致谢

## 第 5 章—利弗莫尔计算中心

作者感谢整个利弗莫尔计算组织（Livermore Computing organization），他们在过去的至少十年里一直支持这项工作。此外，我们感谢由 Mark Gary、Chris Morrone 和 Mark Stearns 的 Lustre 团队，以及三位个人在准备和审查本文稿期间提供的帮助。

本工作是在美国能源部的支持下，由劳伦斯·利弗莫尔国家实验室（Lawrence Livermore National Laboratory）根据合同 DE-AC52-07NA27344 完成。本章是一份 LLNL 文档：LLNNL-BOOK-641234。

## 第 6 章—洛斯阿莫斯国家实验室

作者感谢整个洛斯阿莫斯高性能计算部门（Los Alamos High Performance Computing Division），他们已支持该工作数十年。洛斯阿莫斯国家实验室（LANL）由洛斯阿莫斯安全公司（Los Alamos National Security）根据美国能源部合同 DE-AC52-06NA25396 运营。

## 第 7 章—德克萨斯先进计算中心

本工作部分由美国国家科学基金会第 1134872 号奖励支持。

## 第 8 章—Lustre
