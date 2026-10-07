

## 替代聚类分析：综述

[17] Derek Greene and Patrick Cunningham. 一种整合多数据视图的矩阵分解方法。于 *Machine Learning and Knowledge Discovery in Databases, European Conference, ECML PKDD*, pages 423–438, 2009.

[18] L. Hamers, Y. Hemck, G. Herweyer, M. Janssen, H. Keters, R. Rousseau and A. Vanhout. 科学计量学的相似性度量：Jaccard指数与Salton余弦公式。*Information Processing and Management*, 25(3):315–318, 1998.

[19] A. Hinburg and D. Keim. 带噪声的大型数据库高效聚类方法。*International Conference on Knowledge Discovery and Data Mining*, pages 58–65, 1998.

[20] Ming Hua and Jian Pei. 多源聚类——一种互子空间聚类方法。*Neurocomputing*, 92:133–144, 2002.

[21] L. Hubert and Phipps Ariele. 划分比较。*Journal of Classification*, 2(1):193–218, 1985.

[22] Prateek Jain, Raghu Meka and Inder Dhillon. 不同聚类的同步无监督学习。*Statistical Analysis and Data Mining*, 1(3):95–210, 2008.

[23] Bo Long, Philip S. Yu and Zhongfei (Mark) Zhang. 一种用于无监督学习的通用模型。*Proceedings of the SIAM International Conference on Data Mining, SDM*, pages 822–833, 2008.

[24] M. Meila. 聚类——基于信息的距离。*Journal of Multivariate Analytics*, 98(5):873–895, 2007.

[25] Emmanuel Muller, Stefan Gunnemann, Thomas Seidl and Ines Faber. 教程：发现不同视图中的对象分组。*ICDM 2010, SDM2011, ICDE 2012.

[26] H. Nages, S. Goil and A. Chowdhury. Mafia: 针对大数据集的高效可扩展子空间聚类。技术报告 9906-010, Northwestern University, 1999.

[27] Xuan Vinh Nguyen and Julien Eps. min：一种生成替代聚类的新颖理论方法。*10th IEEE International Conference on Data Mining, ICDM 2010*, Sydney, Australia, 14–17 December 2010, pages 521–530, 2010.

[28] Donglin Liu, G. Dy, and Michael I. Jordan. 多非冗余谱聚类。*Machine Learning, Proceedings of the Twenty-Fourth International Conference (ICML-10)*, June 21–24, 2010, Haifa, Israel, pages 831–838, 2010.

[29] 第1届发现、总结和使用多聚类的国际工作会议 (MultiCl)。与第16届 ACM SIGKDD 知识发现与数据挖掘会议 (KDD) 同举行。2010年7月25日。

[30] 第2届发现、总结和使用多聚类的国际工作会议 (MultiCl)。与欧洲机器学习与数据库知识发现原理与实践会议 (ECML PKDD) 同举行。2011年9月5日。

[31] 第3届发现、总结和使用多聚类的国际工作会议 (MultiCl)。与2012年 SIAM 国际数据挖掘会议 (SDM) 同举行。2012年4月26日。

## 数据聚类：算法与应用

- [32] Zije Qi and Ivan Davason. 一种寻找替代聚类的有原则且灵活的框架。*第15届 ACM SIGKDD 知识发现与数据挖掘会议*, Paris, France, 2009年6月28日-7月1日, pages 717–726, 2009.
- [33] W. Rand. 聚类方法评估的目标标准。*Journal of the American Statistical Association*, 66(36):846–850, 1971.
- [34] P. J. Rousseau. 轮廓法：聚类分析解释与验证的图形辅助。*Journal of Computational and Applied Mathematics*, 20:53–65, 1987.
- [35] Grigorios Tzortzis and C. L. Likas. 基于样本混合模型的加权组合的多视图聚类。*IEEE Transactions on Neural Networks*, 21(12):1925–1938, 2010.
- [36] Nguyen Xuan Vinh, Julien Epps, and James Bailey. 用于聚类比较的信息理论量：变体、属性、归一化和随机修正。*Journal of Machine Learning Research*, 9999:2837–2854, 2010.
- [37] 多视图数据、高维、外部知识工作会议：追求统一的聚类方法。与第16届亚太知识发现与数据挖掘会议 (PAKDD 2012) 同举行。2012年5月29日。
- [38] Dengyong Zhou and Christopher J. Burges. 多视图下的谱聚类与直推学习。*Machine Learning, 第24次国际会议 (ICML 2007)*, pages 1159–1166, 2007.

## 第22章 聚类集成：理论与应用

Deep Ghosh, University of Texas at Austin, Austin, TX, gosh@utex.edu
Ayan Acharya, University of Texas at Austin, Austin, TX, acharya@utex.edu

22.1 引言 ... 551
22.2集成问题 ... 554
22.3 衡量聚类间的相似性 ... 555
22.4 聚类优化 ... 558
22.4.1 概率集成方法 ... 558
22.4.1.1 混合模型集成 (MMCE) ... 558
22.4.1.2 贝叶斯集成 (BCE) ... 558
22.4.1.3 非参数贝叶斯集成 (NPCE) ... 559
22.4.2 基于相似性的方法 ... 560
22.4.2.1 配对关系方法 ... 560
22.4.2.2 关联性方法 ... 562
22.4.3 使用标签集成 ... 562
22.4.3.1 图形划分 ... 562
22.4.3.2 投票法 ... 563
22.5 集类的应用 ... 564
22.5.1 基因表达分析 ... 564
22.5.2 图像分割 ... 564
22.6 结语 ... 566
参考文献 ... 566

过去十年，通过装袋（bagging）、提升（boosting）等技术，集成多个分类器，在解决困难分类问题方面取得了显著进展 [54, 36, 62]。相关研究表明，通过集成多个分类器，可以提高预测结果 [51]。该主题的广泛文献表明，通过多样化的分类器形成的集成通常比其单个组件更可靠。聚类集成的成功为研究如何有效地整合聚类解决方案提供了直接动力。本章涵盖了聚类集成的理论、设计与应用，旨在解决整合“基础”聚类的问题。然而，整合多个解决方案面临额外的挑战：首先，不同基础解决方案产生的聚类数量可能不同 [6]。其次，共识中合适的聚类数量是不可预知的，并且取决于数据的尺度。此外，聚类标签是符号化的，因此不同解决方案之间的标签对齐是一个难题。在典型的公式中，用于产生解决方案的原始数据对共识机制可见，后者只能访问聚类标签。在某些方案中，可以控制基础聚类的生成 [21]，而在其他方案中，这是为了允许知识重用。尽管存在这些复杂性，针对多种聚类算法的集成不可避免会引起特定数据集的准确率变异。这表明与分类器集成相比，聚类集成可能实现更大的改进 [24]。

