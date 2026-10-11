
在如果我们有足够的领域知识来定义可能的簇，那么稳定性问题将与监督学习中的稳定性是相同的。因此，我们期望特征选择算法在存在少量扰动时是保持稳定的。然而，如果数据的变化没有随主题的变化而发生变化，我们可能会认为这种选择是不稳定的。

## 未定义簇

与第一情况相反，如果我们对数据的簇并不了解（这在现实世界中是常态），我们通常认为这种情况取决于领域和实践者的意愿。例如，在流数据数据中，我们预期会出现某种数据集偏移或漂移，数据的分布和聚类主题可能会随时间移而演变。因此，我们应该拥有一个自适应演化的特征选择过程，通过调整特征来捕捉数据演化的结构。然而，我们可能在一段时间内需要稳定的选择，而在另一时期需要不稳定的选择。例如，在新闻数据聚类中，当我们没有处理会导致分布转向不同主题的突发新闻时，我们希望获得稳定的选择。

另一方面，子空间和投影聚类可能无法提高稳定性，因为它们搜索所有定义簇的可能特征集。在某些情况下，我们可能希望在某些簇上保持稳定的选择，而在另一些簇上保持不稳定。例如，如果我们对新闻数据执行投影聚类，我们可能希望在不快速演化的簇上保持稳定的选择，而对快速演化的簇则保持不稳定的选择。

## 参考文献

- [1] C.C. Aggrawal, J. Han, J. Wang, and P.S. Yu. A framework for clustering evolving data streams. In Proceedings of the 29th International Conference on Very Large Data Bases—Volume 29, pages 81–92. VLDB Endowment, 2003.

- [2] C.C. Aggrawal, J. Han, J. Wang, and P.S. Yu. A framework for projected clustering of dimensional data streams. In Proceedings of the Thirtieth International Conference on Very Large Data Bases-Volume 30, pages 852–863. VLDB Endowment, 2004.

- [3] C.C. Aggarwal, J.L. Wolf, P.S. Yu, C. Prokopuc, and J.S. Park. Fast algorithms for projected clustering. ACM SIGMOD, 28(2):61–72, 1999.

- [4] T.M. Akhriz, Y. Ma, and J.L. Li. Clustering using frequent contextual term. In 2011 International Conference on Information Management, Innovation Management and Industrial Engineering (ICII), Volume 1, pages 339–342. IEEE, 2011.

- [5] S. Alelyani, W. Wang, and H. Liu. The effect of the characteristics of the dataset on the selection stability. In Proceedings of the 23rd IEEE International Conference on Tools with Artificial Intelligence, 2011.

- [6] F. Beil, M. Ester, and X. Xu. Frequent term-based clustering. In Proceedings of the Eighth ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 436–442. ACM, 2002.

- [7] C. Bousaidis, M.W. Mahoney, and P. Draneas. Unsupervised feature selection for the k-means clustering problem. Advances in Neural Information Processing Systems, 22:153–161, 2009.

- [8] P.S. Bradley and O.L. Mangasarian. Feature selection via concave minimization and support vector machines. pages 82–90. Morgan Kaufmann, 1998.

- [9] D. Cai, C. Chang, and X. He. Unsupervised feature selection for multi-cluster data. In Proceedings of the 16th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 333–340. ACM, 2010.

- [10] A. Carvalho, R.F. Melo, S. Alelyani, H. Liu. Quantifying features using false nearly neighbors: an unsupervised approach. In Proceedings of the 2nd IEEE International Conference on Tools with Artificial Intelligence (ICTAI), pages 994–997. IEEE, 2011.

- [11] G. C. Cvalley, N. L. Talbot, and M. G. Sparse logistic regression. NIPS, 2006.

# 聚类的特征选择：综述

## 聚类：算法与应用

- [12] 聚类：算法与应用
- [13] 聚类：算法与应用
- [14] 聚类：算法与应用
- [15] 聚类：算法与应用
- [16] 聚类：算法与应用
- [17] 聚类：算法与应用
- [18] 聚类：算法与应用
- [19] 聚类：算法与应用
- [20] 聚类：算法与应用
- [21] 聚类：算法与应用
- [22] 聚类：算法与应用
- [23] 聚类：算法与应用
- [24] 聚类：算法与应用
- [25] 聚类：算法与应用
- [26] 聚类：算法与应用
- [27] 聚类：算法与应用
- [28] 聚类：算法与应用
- [29] 聚类：算法与应用
- [30] 聚类：算法与应用
- [31] 聚类：算法与应用
- [32] 聚类：算法与应用
- [33] 聚类：算法与应用
- [34] 聚类：算法与应用
- [35] 聚类：算法与应用

# 数据聚类：算法与应用

[37] H. Liu 和 R. Setion. 特征选择的概率方法——一种过滤解决方案。第13次国际机器学习会议论文集 (ICML '96) 1996, 319–327, 意大利巴里。

[38] H. Liu 和 L. Yu. 迈向分类与聚类的特征选择算法集成。IEEE Transactions on Knowledge and Data Engineering, 17(4):49–502, 2005年4月。

[39] B. Long, Z.M. Zhang, 和 P. Yu. 关系聚类的概率框架。第13次 ACM SIGKDD 国际知识发现与数据挖掘会议论文集, 第 470–479 页, ACM, 2007。

[40] B. Long, Z.M. Zhang, X. Wu, 和 P. Yu. 针对多类型关系数据的谱聚类。在第23次国际机器学习会议论文集中, 第 585–592 页。ACM, 2006。

[41] H.P. Luhn. 文学信息机械化编码与检索的统计方法。IBM Journal of Research and Development, 1(4):309–317, 1957。

[42] U. Luxburg. 谱聚类教程。Statistics and Computing, 17(4):395–416, 2007。

[43] S.A. Macscassky 和 F. Provost. 网络数据分类：一种工具箱与单变量案例研究。Journal of Machine Learning Research, 8:935–983, 2007。

[44] P. Mitra, C. A. Murphy, 和 S. K. Pal. 基于特征相似性的无监督特征选择。IEEE Transactions on Pattern Analysis and Machine Intelligence, 24:301–312, 2002。

[45] F. Model, P. Adorjan, A. Ok, 和 C. Pierbrock. 基于 DNA 甲基化的癌症分类特征选择。Bioinformatics, 1  Suppl:S157–S164, 2001。

[46] D.S. Modha 和 W.S. Spangler. k-means 聚类中的特征加权。Machine Learning, 52(3):217–237, 2003。

[47] K. Morik, A. Kaspuri, M. Wurst, 和 M. Skrzynski. 多目标频繁变换聚类。Knowledge and Information Systems, 30(3):175–738, 2012。

[48] M. Mugunhadhee, P. Munitha, 和 M. Punithavali. 文档聚类中的特征选择综述。International Journal, 3, 2011。

[49] M. E. Newman 和 M. Girvan. 关于特征选择：以指数级无关特征作为训练样本进行学习。在第15次国际机器学习会议论文集中, 第 404–412 页。Morgan Kaufmann, 1998。

[51] K. Nigam, A. McCallum, S. Thrun, 和 T. Mitchell. 使用 EM 算法从标记和未标记文档中进行文本分类。在. Machine Learning, 39(2–3):103–134, 1999。

[52] I.S. Oh, J.S. Lee, 和 B.R. Moon. 用于特征选择的混合遗传算法。IEEE Transactions on Pattern Analysis and Machine Intelligence, 26(11):1424–1437, 2004。

[53] J. R. Quin. C4.5: 机器学习程序。Morgan Kaufmann, 1993。

[54] V. Roth 和 T. Lange. 聚类方法中的特征选择。Advances in Neural Information Processing Systems, 16, 2003。

[55] V. Rui 和 T. S. Huang. 图像检索：当前技术、前景方向和问题。Journal of Visual Communication and Image Representation, 10:39–62, 1999。

# 聚类的特征选择：综述

[56] Y. Saeis, I. Inza, 和 P. Larranaga. 生物信息学中特征选择技术的综述。Bioinformatics, 23(19):2507–2517, 2007年10月。

[57] P. Sen, G. Mata, M. Biliga, L. Getoor, B. Galligher, 和 T. Eliaassi-Rad. 网络数据中的集体分类。AI Magazine, 29(3):93, 2008。

[58] W. Siedlecki 和 J. Klansky. 关于自动特征选择。在模式识别与视觉手册中, 63–87, 1993。

[59] M. R. Rikonja 和 I. Kononenko. Relief 和 ReliefF 的理论与实证分析。Machine Learning, 53:23–69, 2003。

[60] L. Song, A. Smola, K. Gottwang, 和 J. Beda. 通过依赖估计进行监督特征选择。在国际机器学习会议, 2007。

[61] C. Su, Q. Chen, X. Wang, 和 X. Meng. 基于最大查询项的文本聚类方法。在 2000。

[62] V. Roth. 聚类方法中的特征选择。2009。

[63] J. Tang 和 H. Liu. 基于最大查询项的文本聚类。2009。

[64] L. Tang 和 H. Liu. 关联数据的特征选择。在第15次 ACM SIGKDD 知识发现与数据挖掘会议论文集中, 第 817–826 页。ACM, 2009。

[65] J. Tang 和 H. Liu. 关联媒体的无监督特征选择。在 KDD。

[66] B. Taskar, P. Abbeel, M.F. Wong, 和 D. Keller. 关系数据的标签预测。在 IJCAI 会议。

[77] R. Tibiani, G. Walther, 和 T. Hastie. 使用间隙法估计聚类数量。Journal of the Statistical Association, 105(490):713–726。

[78] C.Y. Tsai 和 C. Chiu. 通过谱分析开发的特征选择机制。Computational Statistics & Data Analysis, 23(5):379–388。

[79] J. Weston, E. Eliss, 和 M. King. 判别半监督特征选择。Journal of Machine Learning Research (JMLR), 5:1439–1461, 2003。

[80] D. Whiteson. 聚类的概率模型。Artificial Intelligence, 11:273。

[81] R. Tibiani, G. Walther, 和 T. Hastie. 实用机器学习：工具与技术。Morgan Kaufmann, 2005。

[82] Z. Zhao 和 H. Liu. 数据挖掘特征选择。Chapman & Hall/CRC Data Mining, Boca Raton, FL, 2011。

# 62 数据聚类：算法与应用

最可能属于同一分布的数据点（或对象）可以很容易定义为聚类。

在本章中，我们介绍了几种概率聚类的基本模型和算法，包括混合模型 [45, 48, 25]、EM算法 [23, 46, 53, 16] 以及概率主题模型 [35, 14]。对于每个概率模型，我们将介绍其通用的建模框架、概率解释、学习该模型的标准算法及其应用。混合模型是概率模型，越来越多地用于寻找单变量和多变量数据的聚类。因此，我们从第 3.2 节开始讨论混合模型，在该节中，离散隐变量的值可以解释为数据点对混合中特定成分（即聚类）的分配。为了在混合模型中进行极大似然估计，第 3 节介绍了一种通用且优雅的技巧——期望最大化（EM）算法。首先，通过高斯混合以非正式的方式引入 EM 算法的动机，然后给出 EM 算法提供一个更通用的视角，它是许多概率模型的标准学习方法。在第 3.4 节中，我们介绍了两个流行的主题模型，即概率隐语义分析（PLSA） [35] 和狄利克雷分配（LDA）。注意，某些方法（例如 EM/混合模型）可能更适用于定量数据，而其他方法如主题模型、PLSI 和 LDA 通常用于文本数据。最后，我们在第 3.3 节给出结论和总结。

### 3.2 混合模型

聚类分析的混合模型 [75, 45, 28, 27] 已经通过多种方式解决。其基本假设是待聚类的观测值来自若干成分中的一个，问题是估计每个成分的参数以拟合数据。推断这些成分的参数并识别哪个成分产生了每个观测值，从而对观测集进行聚类。在本节中，我们首先给出混合建模的概述，然后介绍两种常见的混合模型——高斯混合模型和伯努利混合模型，最后讨论关于模型选择的几个问题。

#### 3.2.1 概述

假设我们有一组数据点 `X={x_1,...,x_N}`，由 `N` 个维变量的观测值组成。随机变量 `x_i` 假设按照 `K` 个成分的混合分布分布。每个成分（即聚类）在数学上由一个度量分布表示。然后使用单个分布来对特定聚类建模，通常被称为成分分布。整个数据集随后通过这些分布的混合进行建模。形式上，`x_i` 的混合密度（或概率密度函数）可以写为：

```
p(x_i) = \sum_{k=1}^{K} \pi_k p(x_i|\theta_k)
```

其中 `π_1,...,\pi_K` 是混合概率（即混合系数或权重），每个 `θ_k` 是指定第 `k` 个成分的参数集，`p(x_i|\theta_k)` 是成分分布。为了使其成为有效模型，混合概率 `{π_k}` 必须满足

```
0 \leq \pi_k \leq 1 (k=1,...,K), \text{ and } \sum_{k=1}^{K} \pi_k = 1.
```

# 用于聚类的概率模型

![](img/b94d85a2e934001944bcc21abd9a9943_89_0.png)

**图 3.1：** 混合模型的图形表示。圆表示随机变量，黑色和阴影形状表示观测变量和隐（即未观测）变量。
