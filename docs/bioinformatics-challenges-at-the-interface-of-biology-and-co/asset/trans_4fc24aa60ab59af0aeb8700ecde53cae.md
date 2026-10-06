

## 2.3 全基因组的获取

20世纪 80 年代和 90 年年代初是一个丰饶的年代，催生了大量新分子结构和序列的出现，以及用于存储这些数据的新数据库。回顾这段活跃的时期，令人难以置信的是当时有两项重大进展尚未发生：这两项进展共同出现不仅将拯救生物数据的爆炸式增长，还将促进它们的全球传播——它们就是 Web 的诞生和高通量 DNA 测序的到来。

高通量技术发展的意义在于，它使全基因组测序首次成为现实。抓住这一机会，随后出现了前所未有的测序热潮，相继产出了：1995年的流感嗜杆菌（Haemophilus influenzae）和生殖支原体（Mycoplasma genitalium）（Fleisch et al., 1995; Fraser et al., 1995），1996年的产甲烷结球菌（Methanaldococcus jannaschii）和酿酒母（Saccharomyces cerevisiae）（Bul et al., 1996），1998年的秀隐线虫（Caenorhabditis elegans）（Cels sequencing consortium, 1998; Goffau et al., 1996），2000年的黑果蝇（Drosophila melanogaster）（Adams et al., 2000），以及终极奖——2001年的人（Homo sapiens）（Lander et al.; V et al., 2001; International Human Genome Sequencing Consortium, 2004; Gregory et al., 2006）。自这一丰收的黎明以来，已有数千个基因组被测序——表 2.7 提供了一些主要里程碑的概述。

与之发展的是许多特定物种数据库，用于存储新兴的基因组数据：FlyBase（Ashburner and Drysdale, 1994）、ACeDB（Eckman and Zurbin, 1995）、SGD（Cherry et al., 1998）、TAIR（Huala et al., 2001）、Ensembl（Hubbard et al., 2002）等。对于某些人来说，这场基因组“淘金热”的价值并不显而易见：由于积累的大量数据似乎无法表征，且其中大部分是非编码的，在某些评论者看来，我们开始追求的宝藏似乎像大规模蝴蝶收藏一样令人兴奋（Strasser, 2008），而另一些人则认为分子生物学进入了相当的“高科技集邮”真空期（Hunter, 2006）。有趣的是，这些论点被一些首批公共资助核苷酸序列数据库的反对者所使用，并描述了几年后对人类基因组计划（HGP）的大部分性抵抗（Strasser, 2008）。

## 表 2.7
基因组测序中的里程碑事件（改编自 Higgs and Atwood, 2005）。

| 年份 | 物种 | 里程碑 |
| :--- | :--- | :--- |
| 1995 | 流感嗜杆菌 | 首个细菌基因组 |
| 1996 | 产甲烷结球菌 | 首个古菌基因组 |
| 1997 | 酿酒酵母 | 首个单细胞真菌 |
| 1998 | 秀隐线虫 | 首个多细胞真菌 |
| 2000 | 拟南芥 | 首个植物基因组 |
| 2001 | 人类 | 人类基因组首次草案 |
| 2004 | 人类 | 人类基因组“完成版”草案 |

## 第 2 章 生物背景

无论今天是否还持有此类观点，基因组测序的冲击仍在持续，并未减弱。来自全球测序项目的数据收集规模令人惊叹，迫使我们从更多方面思考如何管理、存档和存储这些信息，以便未来的研究人员能够更高效、更有效地进行探索。这种情况为本书中的计算机科学章节提供了许多背景，并为下一章奠定了基础，在下一章中，我们将介绍多年来创建的一些数据库，用于捕捉和管理大量的积累生物数据。

## 2.4 总结

本章介绍了了一些为生物信息学提供基础的基本生物概念和数据类型。具体而言，我们看到：

- 1. 中心法则认为遗传信息的流向方向是从 DNA 到 RNA 再到蛋白质；
- 2. 核酸有四字母字母表：DNA 由碱基 A、T、G 和 C 组成；RNA 由 A、U、G 和 C 组成；
- 3. mRNA 是通过转录过程从 DNA 生成；
- 4. 蛋白质通过翻译过程从 mRNA 生成；
- 5. 在真核 mRNA 剪接之前，非编码区域——内含子会被剪接掉；
- 6. 负责剪接的分子机器被称为剪接体；
- 7. 媒介 mRNA 翻译的分子链是核糖体；
- 8. 蛋白质是由 20 种氨基酸组成的 20 字母表构建的；
- 9. 氨基酸的物理化学性质存在交叉；它们的结构和性质诱导链产生局部和全局折叠模式；
- 10. 蛋白质结构是分级的：一级结构是线性氨基酸序列；二级结构是链内的局部规律；三级结构是整体折叠；
- 11. 大多数蛋白质序列是通过对全基因组测序项目生成的 DNA 序列进行概念翻译产生的；
- 12. 翻译需要使用遗传密码将核酸转换为蛋白质语言；
- 13. DNA 的翻译必须在三个阅读框中进行：三个正向和三个反向；编码区可能出现在正向和反向框中；
- 14. 基因识别和结合需要正确识别起始和终止信号以及内含子边界边界，这是一个很容易出错的过程；
- 15. 全球基因组项目正在产生大规模数据。

## 2.5 参考文献

Adams, M., Celniker, S.E., Holt, R.A. (2000) Drosophila melanogaster 的基因组序列，287, 2185–2195.
Andersson, S.G., Zomorirov, A., Andersson, J.O. (1998) 布氏立热体 Rickettsia prowazii 的基因组序列，396, 133–140.
Arabidopsis Genome Initiative (2000) 植物植物基因组分析，Nature, 408, 796–815.
Ashburn, M. and Drysdale, R. (1994) FlyBase——数据库，Development, 120(7), 2077–2079.
Berg, S.M., Moore, C. and Sharp, P.A. (1977) mRNA 5’ 端的剪接基因，Proceedings of the National Academy of Sciences of the U.S.A., 74(8), 3171–3175.
Bull, C.J., White, O., Olsen, G.J. (1996) 产甲烷菌 Methanococcus jannaschii 的基因组，Science, 273, 1058–1063.
Cels sequencing consortium (2008) 线虫的完整基因组，Science, 282, 2012–2018.
Chain, P.S., Hu, P., Malalti, S.A. (2006) 鼠疫 Yersinia pestis 的完整基因组，Journal of Bacteriology, 188(2), 4453–4463.
Cherry, J.M., Adler, C. (1998) SGD：酿酒酵母，Nucleic Acids Research, 26(1), 73–79.
Chow, L.T., Gelmas, R.E., Bock, J.R. (1993) 腺病毒 5’端的惊序列，Cell, 12(1), 1–8.
Crick, F. (1970) 分子生物学的中心法则，Nature, 227, 561–563.
Eckman, F.D. and Zurbin, R. (1995) ACeDB 和猕猴，Cell Biology, 84, 583–605.
Engelman, D., Staetz, T.A. and Goldman, A. (1986) 膜蛋白氨基酸序列中的非极性转移螺旋酶，Annual Review of Biophysics and Chemistry, 15, 321–353.
Fleischmann, R.D., Adams, M.D., White, O. (1995) 流感嗜杆菌的全基因组测序与组装，Science, 269, 496–512.
Fraser, C.M., Goyne, J.D., White, O. (1995) 生殖支原体的最小基因组，Science, 270, 397–403.
Goffau, A., Barrel, B.G., Bussey, H. (1996) 6000个基因的生命，Science, 274, 546–567.
Hershey, A. and Chase, M. (1992) 蛋白质和核酸在细菌生长中的独立功能，Journal of General Biology, 36(1), 39–56.
Higgs, P. and Arthur, T.K. (2005) 生物信息学与分子进化，Blackwell, Oxford.
Huala, E., Dickerman, A.W., Garcia-Hernandez, M. et al. (2001) 拟南芥信息资源 (TAIR)：模型植物综合数据库和基于网络的信息检索与可视化系统，Nucleic Acids Research, 29(1), 102–105.
Hubbard, T., Barket, D., Birney, E. et al. (2002) Ensembl 数据库项目，Nucleic Acids Research, 30(1), 1–38.
Hurl, D.J. (2006) 基因组学与蛋白质组学：真正的秩序还是堆栈收集？Epidemiology, 17(5), 487–489.
International Human Genome Sequencing Consortium (2004) 人类基因组常染色质序列跟随，Nature, 431, 931–945.
Kaneko, T., Nakamura, Y., Sato, S. et al. (2002) 固氮共生细菌 Bradyrhizobium us 的完整基因组，DNA Res., 9(6), 189–197.
Kyte, J. and Doolittle, R.F. (1982) 分相和预测蛋白质疏水性特征的方法，Journal of Molecular Biology, 157, 105–132.

