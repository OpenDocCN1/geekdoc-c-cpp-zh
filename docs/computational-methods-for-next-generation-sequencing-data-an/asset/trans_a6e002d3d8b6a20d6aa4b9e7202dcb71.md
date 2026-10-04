

# 转录组定量化与差异表达

325

![](img/46aec008551cecb3bbf3aac2ee69b926_337_0.png)

**图 14.7** IsoDE-All（每个条件运行 20 次自助采样法）、edgeR 和 GFOLD 在 Illumina MCF-7 数据上的表现，涉及不同重复次数和最小倍数变化 1.5 时的敏感性、PPV（阳性预测值）、F 分和准确率。

![](img/46aec008551cecb3bbf3aac2ee69b926_337_1.png)

**图 14.8** IsoDE-All（每个条件运行 20 次自助采样法）、edgeR 和 GFOLD 在 Illumina MCF-7 数据上的表现，涉及不同重复次数和最小倍数变化 2时的敏感性、PPV（阳性预测值）、F 分和准确率。

# NGS 数据分析的计算方法

与高表达基因相比（在中间重复次数和更高的倍数阈值下也获得了相似的结果）。相比之下，GFOLD 在低位数基因与高位数基因之间，在所有准确率指标上均显示出显著差异。edgeR 对低表达水平基因的敏感性也较低；但其 PPV 在不同表达水平上保持相对稳定。

# 致谢

这项工作部分来自 Life Technologies 的两项合作研究资助、美国科学基金会（NSF）的 IIS-0916401 和 IIS-0916948 奖，以及美国农业部 USDA 国家食品与农业倡议的竞争性资助（号 201176016-30331）。

# 参考文献

- 1. Caciula A, Glebova O, Artyomenko A, Mangul S, Lindsay J, Mändoiu II, Zelikosky A. 用于转录组定量的模拟回归算法。Bioinformatics Research and Applications: 10th International Symposium, ISBRA 2014, p. 406; (b) Caciula A, Glebova O, Artyomenko A, Mangul S, Lindsay J, Mändoiu II, Zelikosky A 用于转录组频率估计的确定性回归算法。2014 IEEE 4th International Conference on Computational Advances in Bio and Medical Sciences (ICABS), IEEE; 2014, p. 1–1.
- 2. Fujujita A, Semairo P, Kojima K, Sato JR, Patriota AG, Miyano S. 通过 Granger 因果关系时间基因表达数据的功能聚类。BMC Syst Biol 2012(6):137.
- 3. Mortazavi A, Williams BA, McCue K, Schaeffer L, Wolf B. 通过 RNA-Seq 映射和定量化动物转录本。Nat Methods 2008;5):621–628.
- 4. Morozov O, Hirsch M, Snyder MA. 新测序技术在转录分析中的应用。Annu Rev Genet 2009;10:135–151.
- 5. Wang Z, Ferguson D. RNA-Seq：转录组学的革命性工具。Nat Genet 2009;10(1):57–63.
- 6. Bullard J, Purdom E, Hansen K, Dudoit S. mRNA-Seq 实验中归一化和差异表达统计方法的评估。BMC Bioinformatics 2010;11(1):94.
- 7. Robinson MD, McCarthy DY, Smith GY. edgeR: 用于数字基因表达数据差异分析的工具。Bioinformatics 2010;26(1):139–140.
- 8. Anders S, Huber W. 序列计数数据的差异表达分析。Genome Biol 2010;11(10):106.
- 9. Trainpell C, Hernandez DG, Sauvageau M, Goff L, Rinn J, Pachter L. 基于 RNA-Seq 的转录本分辨率的基因表达差异分析。Nat Biotechnol 2012;31(1):46–53.
- 10. Bi Y, Davavluri RV. NPEBseq: 基于非参数贝叶斯的 RNA-Seq 数据差异表达分析方法。BMC Bioinformatics 2013;14(1):262.
- 11. Barrett, T, Troup D, Wilhite S, Ledoux P, Evangelista C, Kim IF, Tomashesky M, Marshall KA, Phillippi KH, Sherman PM et al. NCBI GEO: 功能基因组学数据集存档 - 10 年。Nucleic Acids Res 2011:39 Suppl 1:1005–1010.
- 12. Feng J, Meyer CA, Wang Q, Li JS, LS X, Zhang Y. GFOLD: 用于 RNA-Seq 数据中快速表达基因的通用折叠数。Bioinformatics 2012(28):2782–2788.
- 13. Scholtz D, von Heydeck A. 差异基因表达研究分析。In: Tleman R, Carey V, Hubert W, Irizary R, Dudoit S, Using R and Bioconductor 的生物信息学与计算生物。纽约:Springer-Verlag; 2005, p. 229–248.
- 14. Alwine JC, Kemp DJ, Stark GR. 琼脂凝胶转移到重苯甲甲基聚合物杂交并使用 DNA 探针检测 RNA 方法。Proc Natl Acad Sci U 1977;74(12):5350–5354.
- 15. Schema M, Shalon D, Brown BW. 微阵列基因表达模式的定量分析。Science 1995;270(52):467–470.
- 16. Wang AM, Doyle MV, Mark DF. 通过聚合酶链反应定量化 mRNA。Proc Natl Sci U 1989;86(4):9717–9721.
- 18. Steiger A, Prit JF, Engel PG, Kokocinski F, RGASP TJ. Guig R, Bertone P. 用于 RNA-Seq 转录本重构方法的分析。Nat Methods 2013;10:777–184.
- 19. Kent JW, Puget C, Fure TF, Roskin KM, Zahler AM. UCSC 的人类基因组。Genome Res 2002;12(6):996–1000.
- 20. Nicolae M, Mangolii II, Zeliskovsky A. 来自 RNA-Seq 数据的剪接异构体分析。Algorithms Mol Biol 2011;6(9).
- 21. Li B, Dewey C. RMSE: 无参考基因组的 RNA-Seq 数据准确定量化。Bioinformatics 2011;12(1):323.
- 22. Li W, Jiang T. 来自偏偏 RNA-seq 数据的转录组组装和异构体水平估计。Bioinformatics 2012;28(22):2914–2921.
- 23. Lin YY, Dao P, Hach F, Bachvili M, Mo F, Lapuk A, Collins C, Sahinal SC. CLIQ: 群群中表达异构体的准确定量和检测。第 12 次生物信息学算法工作会议；2012.
- 24. Mangul S, Cacic A, Seii S, Brinza D, Kanadia R. 从成对 RNA-Seq Reads 中重构新转录本的整数方法。ACM 计算生物学与生物学会议论文集。2012;纽约:ACM. p. 369–376.
- 25. Tomescu AI, Kuosmen A, Rizzi R, Mäkinen V. 一种用于 RNA-Seq 的新型最小折叠法方法。
- 26. Li W, Feng J, Liang Y, Isolasso A. 基于 LASSO 的转录组组装。Genome Biol 2011;10:1693–1770.
- 27. Tomescu AI, Kuosmen A, Mäkinen V. 用于 RNA-Seq 的新型最小折叠法方法。Bioinformatics 2013;14:5.
- 28. Anders S, Huber W. 序列计数数据的差异表达分析。Genome Biol 2010;11(10):106.
- 29. 29 328

# NGS 数据分析的计算方法

- 30. Benjamini Y, Hochberg T, Willner D, Hugenholtz P, Tyson GW. 控制错误发现率：多重检验的实用且强大的方法。J R Stat Soc, Ser B 1995;57(1):289–300.
- 31. Li J, Jiang H, Wong W, Pop M, Salzberg A. 人类基因组短序列的不均匀性建模。Genome Biol 2010;11(5):25.
- 32. Hansen KD, Dudoit S, Saitais B. 通过随机引物进行全对量转录组测序。Nucleic Acids Res 2010;38(12):e131.
- 33. Roberts A, Tran C, Donaghey J, Rinna J, Pacchter L. 修正片段偏好的 RNA-Seq 估计。Genome Biol 2011;12:3.
- 34. Liu Y, Zhou J, White KP. RNA-Seq 差异研究：更多是重复？Bioinformatics 2014;30(3):301–304.
- 35. Li B, Dewey CN. RSEM: 无参考基因组的 RNA-Seq 数据准确定量化。Bioinformatics 2011;12(1):323.
- 36. MAQC Consortium. 微阵列质量控制 (MAQC) 项目及平台间的测量重复性。Nat Biotechnol 2006;24(9):1151–1161. DOI: 10.1038/nb1239.
- 37. Langneed W-P, Stromberg C, Pop M, Salzberg A, Stewart C, Garrison EP, Marth G. MOSAIK: 短序列到人类基因组的高速内存内存对。Genome Biol 2009;10(3):25. DOI:10.1186/gb-2009-10-25.
- 38. Lee W-P, Stromberg MP, Ward A, Packer SE. 用于精确下一代测序映射的哈希算法。PLoS 2014;9(3):90581.
- 39. Reid LH. 测试和选择 ercc 外部 RNA 质的建议方法。BMC Genomics 2005;6(1):1–18.
- 41. Angly FE, Willner D, Rohwer F, Hugenholtz P, Tyson GW. Nucleic Acids Res 2012;40(12):94. DOI: 10.1093/gks251.
- 42. Kulkarni MM, Willner D, Rohwer F, Hugenholtz P, Tyson GW. 使用 NanoString nCounter 系统进行数字多路基因表达分析。Curr Prot Mol Biol 2011;94:25B:10.1-25B.10.17.

