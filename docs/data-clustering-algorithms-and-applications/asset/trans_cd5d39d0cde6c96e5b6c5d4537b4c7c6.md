

# 数据聚类：算法与应用

而不是标准的 NMF 如 $\phi(X) \approx FG^T$，后者是很难实现的，因为 $F,G$ 将显式地取决于映射函数 $\phi(\cdot)$。很容易看出最小化目标：

```
$|\phi(X)-\phi(X)WG^T||_F^2 = \text{Tr}[\phi(X)^T\phi(X)-2G^T\phi(X)^T\phi(X)W+W^T\phi(X)XWG^T G], \quad (7.25)$
```

该目标仅取决于核矩阵 $K = \phi(X)$。这种 NMF 的核扩展类似于核-PCA 和核-means。

- **10. 多层 NMF：** 在多层 NMF 中，基础因子矩阵被一组使用顺序分解的矩阵取代 [22, 32, 23]。给定一个输入矩阵 $X$，首先将其分解为 $F_{(1)}G_{(1)}^T$。在第二步中，将 $G_{(1)}$ 进一步分解为 $F_{(2)}G_{(2)}^T$，并重复此过程若干次。多层 NMF 模型可以表示如下：

```
$X \approx F_{(1)}F_{(2)}\dots F_{(L)}G_{(L)}^T = FG^T. \quad (7.26)$
```

已经证明，多层 NMF 可以提高大多数 NMF 算法的性能，并解决由于分布式、多阶段性质以及具有不同初始条件的顺序分解导致的局部极值问题 [24]。

- **11. 二值 NMF：** 当输入数据 $X$ 是二值矩阵时，二值 NMF 将 $X$ 分解为两个矩阵，从而保留了 $X$ 最重要的属性 [141, 140, 71]。二值 NMF 模型可以写为：

```
Binary NMF: $X_0^{-1} \approx F_0G_0^{-1}. \quad (7.27)$
```

二值 NMF 的一个特例是布尔因子分解

```
$X_0^{-1} \approx W_0 \oplus H_0^{-1}. \quad (7.28)$
```

- **12. 加权特征子集 NMF：** 在加权 NMF 中，引入权重来表示对应行和列的重要性。如果只考虑重要性，会导致加权子集 NMF (FS-NMF)：

```
$$\min_{W \ge 0, G \ge 0} ||X-FG^T||_W^2, \sum_j W_j^a = 1, \quad (7.28)$$
```

其中 $W \in \mathbb{R}^{m \times m}$ 是一个指示 $X$ 中行（或特征）权重的对角矩阵，$\alpha$ 是一个参数 [116, 117]。通常，我们可以为不同的样本分配权重。这导致了加权 FS-NMF：

```
$$\min_{W \ge 0, G \ge 0} ||X-FG^T||_W^2$$
```

其中我们设置 $W_{ij} = a_{ij}b_j$。

```
$$\min_{W \ge 0, G \ge 0} (X-FG^T)_{ij}^2 a_{ij}b_j, s.t. \sum_i a_{ij}^a = 1, \sum_j b_j^b = 1, \quad (7.29)$$
```

其中 $\alpha, \beta$ 是两个满足 $0 < \alpha < 1, \beta < 1$ 的参数。

- **13. 鲁棒 NMF：** 最近 [63] 提出了一种使用 $L_{2,1}$范数损失函数的鲁棒 NMF。误差函数为：

```
$||X-FG^T||_{2,1} = \sqrt{\sum\sum (X-FG^T)_{ij}^2}, \quad (7.30)$
```

提出的方法比标准 NMF 能更好地处理离群值和噪声。

# 用于聚类的非负矩阵分解：综述

总之，各种提出的 NMF 格式汇总如下：

- SVD: $X_{\pm} \approx U_{\pm}V_{\pm}^T$
- NMF: $X_{\pm} \approx F_{\pm}G_{\pm}^T$
- Regularized NMF: $\min \{\|X - FG^T\|^2 + \alpha J_1(F) + \beta J_2(G)\}$
- Projective NMF: $X \approx FF^T$
- Semi-NMF: $X_{\pm} \approx F_{\pm}G_{\pm}^T$
- Convex-NMF: $X \approx CG^T, \text{ where } c_i \in \text{conv}(X)$
- Cluster-NMF: $X \approx XG_i^^T$
- Kernel-NMF: $\Phi(X_{\pm}) \approx (X_{\pm})W_{\pm}^T$
- Tri-Factorization: $X_i \approx F_i S_i^T$
- Symmetric-NMF: $W_1 \approx H_1^T$
- Multi-layer NMF: $X \approx F_{(1)}\dots F_{(t)}G_{(t)}^T$
- Binary NMF: $X_{0}^{-1} \approx F_{0}^{-1}G_{0}^{-1}$
- Weighted Subset NMF: $\min \|X - FG^T\|_W^2$
- Robust NMF: $\min \|X - FG^T\|_R^2$

注意还有其他 NMF 格式未包含在讨论中，例如用于非负矩阵的卷积 NMF [24] 以及基于贝叶斯方法的 NMF [14, 45]。

# 用于聚类的 NMF：扩展

我们已经证明 NMF 为无监督学习提供了一个通用框架，可以处理广泛的数据分布并进行硬聚类和软聚类。事实上，许多其他聚类问题如协同聚类、共识聚类、监督聚类和图聚类可以重构为 NMF 问题。

## 7.6.1 协同聚类 (Co-clustering)

在现实应用中，聚类通常涉及多种类型的数据点以及输入类型。在文档分析中，存在词和文档。在 DNA 微列数据中，行代表基因，列代表样本。协同聚类算法通过利用词-文档矩阵和基因-样本矩阵同时聚类不同类型的数据 [30, 136, 20, 83]。

为了同时对输入数据的行和列进行聚类，针对非负矩阵提出了三元分解 [41]，其目标是：

```
$\|X - FSG^T\|^2, \text{ s.t. } F^T F = \mathbf{I}, G^T G = \mathbf{I}$.
```

这在 $F$ 和 $G$ 作为对称矩阵增长时提供了额外的自由度。三元分解提供了一个良好的指标框架。

## 7.6.2 监督聚类 (Supervised Clustering)

在许多使用聚类发现新模式的情况下，对于问题存在一些先验的、不完整的知识。我们希望将知识纳入聚类算法中。监督聚类是指带有链路约束（两个点可能聚类到同一类中）和非链路约束（两个数据点不能聚类到同一类中）的聚类情况 [5, 8, 4, 115, 129, 61]。

上述约束公式如下 [115]

1. 链路约束 (Must-link constraints)：$A=\{(i_1, j_1), \dots, (i_a, j_a)\}; |A|$ 包含点对，其中 $x_i, x_j$ 被认为是相似的必须聚类到同一类中。
2. 非链路约束 (Cannot-link constraints)：$B=\{(i_1, j_1), \dots, (i_b, j_b)\}; |B|$，每对点都是不相似且不能聚类到同一类中。

$A, B$ 也可以视为包含 $\{0, 1\}$ 的对称矩阵。使用聚类指示矩阵 $H$，链路约束 $(i_1, j_1)$ 意味着 $x_i, x_j$ 在同一簇 $k$ 上应有非零后验概率；重叠 $\sum_{(i,j) \in A}h_{ik}h_{jk} = (HH^T)_{ij}$ 应最大化。因此，链路条件是 $\max_H \sum_{(i,j) \in A}(HH^T)_{ij} = Tr[A(HH^T)] = Tr[AH^TH]$。同样，非链路约束可以表述为惩罚 $\lambda Tr[BH^TB]$。但监督聚类问题可以表述为以下优化问题：

```
$\max_{H H^T \ge 0} Tr[AH^TH] + \alpha Tr[BH^TB]; \quad (7.32)$
```

```
$\min_{H H^T \ge 0} ||(W^* - HH^T)||^2; \quad (7.33)$
```

因此，监督聚类问题等同于半 NMF 问题 [37, 72]。Chen 等利用非负三元分解通过实例级约束制定了监督聚类 [17]；Zhu 等 [143] 注意到链路约束和非链路约束在聚类中起不同作用，并提出了一种约束 NMF 方法，其中链路约束用于控制压缩格式下数据的距离，而非链路约束用于控制编码因子。

还有一些将（部分）类别标签信息引入矩阵分解框架的研究。Lee 等 [69] 提出了监督 NMF (SSNMF)，它将数据和（部分）类别标签共同纳入 NMF 中。Liu 和 Wu [81] 提出了一种约束 NMF 形式，要求共享相同标签的数据点在新表示空间具有相同的坐标。

## 7.6.3 监督协同聚类 (Supervised Co-Clustering)

在聚类两类对象时，我们对 x 类对象有部分先验知识，对 y 类对象也有部分先验知识。监督聚类旨在控制

