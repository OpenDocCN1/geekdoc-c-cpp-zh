

# 130 NGS数据分析的计算方法

8. Warren RL, Sutton GG, Jones SJ, Holt RA. 使用 SSAKE组装短 DNA 序列。Bioinformatics 2007:23(4):500–501.

9. Dayarian A, Michael T, Sengupta A. SOPRA: 通过统计优化对对读段进行骨架构建。BMC Bioinformatics 2010;11(1):345-.

10. Dixon H, Reinhardt K, Myers EW. 用于 contig 骨架构建的贪婪路径合并算法。J ACM 2002;49(5):603–65.

11. Hopcroft JE, Tarjan RE. 将图分为连通分量。SIAM Comput 1973;2(3):135–158.

12. Di Battista G, Tamassia R. 保证与编程。Berlin: Springer-Verlag; 1990. p. 590–611.

13. Chimani W, Guttinger C, Jung M, Klau GW, Klein M, Putri. 开源图框架 (OGDF)。In: Tamassia R. 图形绘制与可视化手册。CRC Press; 2011, p. 543–569.

14. Lindsay J, Saoloi C, Mändoufal A. 使用整数线性规划进行扩展性骨架构建。ACM生物信息学、计算生物学和生物信息学会议论文，BCB 12。New York: ACM; 2012, p. 377–383.

15. CPLEX II, V. 1: CPLEX 用户手册。In Bus March Corporation 2009;46(53):157.

16. Shchberina O. 离散优化中的非序列动态骨架构建和树分解。In: Waldmann K-H, Stocker UM, editors. 运筹学进展2006。Berlin Heidelberg: Springer-Verlag; 2006. p. 155–160.

17. Mandric I. 使用 Bowtie 2 对短测序读段比对。Nat Proc Bioinformatics 2010; Chapter 11:11-7–11-7-14.

19. Li H, Durbin R. 使用 Burrows-Wheeler 变换快速准确的短比对。Bioinformatics 2009;25(14):175–176.

20. Salin K, Street N, Lundeberg J, Arvest L. 改进骨架算法的间隙大小估计。Bioinformatics 2012;28(17):2215–2222.

21. Salin K, Vezzi F, Nystedt B, Lundeberg J, Arvest L. BESST-大型碎片组装的高效骨架构建。BMC Bioinformatics 2014;15:2481.

22. Pulleyblank W. B-匹配问题中的双重完整性。Heidelberg: Springer-Verlag; 1980.

23. Edmonds J. 树、树与花。In Jan Math 1965;17(3):449–467.

24. Hagberg A, Schult D, Swart P. 网络: 用于网络分析的 Python 。技术报告，数学建模与分析。洛斯阿拉莫国立实验室；2005。访问地址：http://network.lanl.gov。

25. Hunt M, Newbold C, Brimmer M, Otto TD. 组装骨架工具的全面评估。Genome Biol 2014;15(3):R42.

# 骨架构建算法

- 27. Salzberg SL, Phillippy AM, Zimin A, Puiu D, Magoc T, Koren S, Treangen TJ, Schatz MC, Delcher AL, Roberts M. 组装骨架工具的评估。Genome Res 2012;22(3):557–567。

- 28. Vezzi F. 特征评估。PLoS ONE 2012;7:e310

- 29. Simpson JT, Durbin B. 压缩数据的重复序列组装。Genome Res 2012;22(3):549。

- 30. Luo R, Xie Y, Huang W, Yuan J, Chen Y. 基因组组装。GigaScience 2012;1:18。

# 变异检测与基因型确定

##基因变异检测与基因型确定

6.1 引言

高通量测序（HTS）技术的发展和普及在测序和基因型确定方面取得了重大突破，从孤立基因测序和少数预定义标记的基因型确定到几乎全基因组测序和数百万 SNP 的全面基因型确定。由于基因组学研究发现，DNA 分子由腺嘌呤（A）、胞嘧啶（C）、鸟嘌呤（G）和胸腺啶（T）组成。基因变异中最常见的类型是单核苷酸多态性（SNP），正如其名称所示，两个序列之间仅在一个碱基对上的差异。SNP 在进化中非常重要，由于它们在基因组中广泛分布，且可以通过实验室技术进行基因型确定，并已证明它们可能是导致某些疾病的因素。此外，通过全基因组关联分析（GWAS）进行表型与状的关联是可行的。由于连锁不平衡（LD），这些 SNP 变异在表型关联中是正常的。因此，完全理解基因组变异需要识别其他类型的变异。这些变异类型包括插入和缺失（indels）、拷贝数变异（CNVs）、倒位和易位。图 6.1 显示了两个染色体之间的变异示意图。

indels 可定义为仅存在于样本中的 DNA 序列。插入或缺失的确定取决于选择特定的序列作为参考。indels 在基因组中也分布良好，但频率不如 SNP。大型 indels 可能会跨越整个基因，因此可能导致显著的表型变异。小型 indels 可能是中性的，除非跨越了调控或编码区域。CNVs 是（通常是）重复 DNA 序列，位于

img/46aec008551cecb3bf3aac2ee69b926_152_0.png

图 6.1 样本间的变异类型。结构变异包括 indels、拷贝数变异（CNVs）、倒位和易位。(a) 单核苷酸多态性（SNP）和 (b) 重复序列的示例显示在放大区域，在这些区域中序列的拷贝在样本之间发生变化。CNV 的拷贝有时呈相邻排列，但也可以散布在基因组中。最近的一些研究揭示了 CNV 对人类遗传学（10）和医学研究（3, 11）的重要性。重复 DNA 序列较小且以相邻方式重复的情况通常被称为 CNV 或重复序列。重复序列在生物技术历史中非常重要，因为它们相对于 SNP 具有高度多态性，可以使用实验室技术进行基因型确定，并且已经证明它们可能导致主要疾病（13）。最后，根据名称索引，倒位和易位分别是区域。与 indels 情况类似，确定变异 DNA 链的正确位置需要将特定的序列作为参考。注意，翻译意味着两个 indels，而 CNV 通常意味着多次事件。

# 134 NGS数据分析的计算方法

6.2 SNP 和小型 indels 的检测与基因型确定方法

###6.2.1 问题描述

一旦读段比对到参考基因组并对比对按照参考坐标进行排序，将遍历参考基因组的碱基位点，以观察支持不同参考等位基因的碱基调用。

