

# 半监督聚类

当学习的有效性通过无标记集中预测的簇/类别标签的准确率来衡量时，该方法尤为重要。

本章其余部分的结构如下：在第 20.2 节，我们讨论了基于特征表示的点对点监督方法的半监督聚类（SSC）以及相关的聚类算法。在第 20.3 节，我们描述了半监督图切和谱聚类。在第 20.4 节，我们引入了 GLP 公式，提出了对现有标签传播方法的统一视角，并阐明了它们与半监督图聚类的关系。在第 20.5 节，我们讨论了半监督流形嵌入和基于嵌入的标签传播方法。我们在第 20.6 节展示了实验结果，并在 20.7 节给出结论。

## 20.2 基于点对点监督的聚类

基于点对点监督的半监督聚类在基于特征的聚类方法中得到了广泛研究。在本节中，我们回顾了文献 [6] 中的一些方法。

### 20.2.1 基于引导的半监督聚类

SSC 的早期思想之一关注于点对点的标签监督，即少量点的簇 ID 是可用。基于引导的 SSC 侧重于基于质心的聚类算法，例如 k-means [2, 11]。在无监督设置下，算法通常从随机初始化开始，并对簇成员和簇原型进行期望最大化（EM）风格的迭代更新。基于引导的 SSC 主要思想是根据可用的簇 ID 改进初始化。特别是，[2] 列出了 k-means 的两种变体：*引导 k-means*（seeded k-means）和*约束 k-means*（constrained k-means）。引导 k-means 使用可用的簇来初始化簇，然后运行 k-means 的迭代更新。在 k-means 中，令 $K$ 为簇的数量，$S = \{x_1, ..., x_n\}, x_i \in \mathbb{R}^d$ 表示数据点集，令 $S = \cup_{j=1}^K S_j$ 表示初始种子。目标函数随着迭代更新的变化而改进。*引导 k-means* 算法总结如下步骤：

- 初始化簇中心 $\mu_h \leftarrow \frac{1}{|S_h|} \sum_{x \in S_h} x$，对于 $h = 1, ..., K$
- 将每个数据点分配到簇 $h^* = \text{argmin}_h |x - \mu_h|^2$
- 估计簇中心 $\mu_h \leftarrow \frac{1}{|S_h|} \sum_{x \in S_h} x$，对于 $h = 1, ..., K$
- 重复最后步骤直到收敛

约束 k-means 同样使用可用的簇 ID 初始化簇，但在迭代更新期间不允许这些标记点的簇分配发生改变。当标签引导不是错误时，*引导 k-means* 更加合适。

基于引导的 SSC 可以推广到 k-means 之外的其他聚类方法，且 [2] 地评估了谱 k-means。引导方法可以看作是概率设置，在其中我们使用 EM 算法学习混合模型 [21]，每个混合分量对应一个簇。特别是，监督信息被用于将标记点的后验概率 $p(z|x_i, \Theta)$ 设置为真实类别（1）或否则（0）。[2] 中的实证结果说明了引导方法的优势，聚类性能在节点数量较少的情况下也会显著提高。该方法也被应用于标记数据仅覆盖部分簇的场景，此时其他簇的质心必须被随机初始化。

### 20.2.2 基于成对约束的半监督聚类

SSC 的流行框架之一是基于成对约束的。给定数据集 $X$，成对监督通常以两种类型约束的形式给出：*必须链接*（must-link）和*不能链接*（cannot-link）约束。如果 $(x_i, x_j) \in M$（必须链接约束集），则鼓励聚类算法将 $(x_i, x_j)$ 保留在同一个簇中；如果 $(x_i, x_j) \in C$（不能链接约束集），则鼓励算法将 $(x_i, x_j)$ 保留在不同的簇。一些方法使用适当的违规惩罚，而另一些方法则认为约束是硬性的 [37, 5, 20, 38]。

带对约束的 SSC 早期方法之一侧重于修改 k-means 算法 [38] 以纳入必须链接和不能链接约束。在算法的每次迭代中，对每个点考虑一个排序后的簇列表。算法移动列表，直到找到一个不违反任何约束的簇分配。如果未找到此类簇，则算法终止。

[38] 中提出的方法相比 k-means 的无监督版本有了显著改进，并允许了半监督知识的引入。然而，从实际角度来看，它的缺点是要求所有约束都必须满足。必须确保相互矛盾的约束得到满足。

其他方法侧重于修改 k-means 目标以考虑成对约束违规 [3]，文献中已有此类方法。特别是，带对约束的 k-means 聚类（PCMeans）目标函数可以写为：

$J_{PC}(M,Y) = \frac{1}{2} \sum_{x_i \in X} ||x_i - \mu_{y_i}||^2 + \sum_{(x_i,x_j) \in M} W_{ij} 1(y_i \neq y_j) + \sum_{(x_i,x_j) \in C} W_{ij} 1(y_i = y_j)$

其中 $W_{ij}$ 是违规的适当惩罚，$M = \{\mu_1, ..., \mu_k\}$ 是簇中心，$Y = \{y_1, ..., y_k\}$，$y_i \in \{1, ..., k\}$ 是数据点的簇 ID。

**局部度量学习：** 聚类背景下的度量学习关注参数化的散度。可以考虑一种监督度量方法，在其中使用 EM 算法学习混合模型 [21]，每个混合分量对应一个簇。
$J_{LML}(M,Y,\mathcal{A}) = \frac{1}{2} \sum_{x_i \in X} (x_i - \mu_{y_i})^T A_i^{-1} (x_i - \mu_{y_i}) + \log(\det(A_i))$ 其中 $A$ 是正定矩阵，每个簇 $h=1, ..., k$ 都有自己的参数 $A_h$。在 [9] 中提出了一种混合方法，能够纳入必须链接和不能链接约束，并调整底层度量。该方法通过结合公式 20.1 和 20.2 中的两个聚类目标来工作。组合目标为：

$J_{P}(M,Y,\mathcal{A}) = \sum_{\mathbf{x}_i \in \mathcal{X}} \{(\mathbf{x}_i - \boldsymbol{\mu}_{y_i})^T A_i(\mathbf{x}_i - \boldsymbol{\mu}_{y_i}) + \log(\det(A_i))\} + \sum_{\mathbf{x}_i,\mathbf{x}_j \in M} w_{ij}f_m(\mathbf{x}_i,\mathbf{x}_j)[y_i \neq y_j] + \sum w_{ij}f_c(\mathbf{x}_i,\mathbf{x}_j)[y_i = y_j]$ 其中 $f_m$ 和 $f_c$ 是关于 $(\mathbf{x}_i, \mathbf{x}_j)$ 的函数。$f_m$ 的定义使得远端点违反必须链接约束的惩罚更高。由于远端点需要必须链接，所使用的度量需要重大更新来实现这一点，惩罚以以下两种方式定义：

$f_M(\mathbf{x}_i,\mathbf{x}_j) = \frac{1}{2}(\mathbf{x}_i - \boldsymbol{\mu}_{y_i})^T A_i(\mathbf{x}_i - \boldsymbol{\mu}_{y_i}) + \frac{1}{2}(\mathbf{x}_j - \boldsymbol{\mu}_{y_j})^T A_j(\mathbf{x}_j - \boldsymbol{\mu}_{y_j})$

在不能链接违规的情况下，附近点的惩罚应该更高。考虑以下惩罚项：

$f_C(\mathbf{x}_i,\mathbf{x}_j) = \frac{1}{2}(\mathbf{x}_i - \boldsymbol{\mu}_{y_i})^T A_i(\mathbf{x}_i - \boldsymbol{\mu}_{y_i}) - \frac{1}{2}(\mathbf{x}_j - \boldsymbol{\mu}_{y_j})^T A_j(\mathbf{x}_j - \boldsymbol{\mu}_{y_j})$ 其中 $(\mathbf{x}_i, \mathbf{x}_j)$ 是根据 $A_l$ 在数据中最大分离的点集。引入这些权重函数是为了产生与约束相关的结果。目标函数通过 EM 算法优化，该算法在更新簇分配与更新簇均 $\mu_0$ 和 $A_0$ 之间切换，直到收敛。为了扩展性和稳定性，[9] 建议在高维问题中使用结构更简单的度量，如对角矩阵。

**全局度量学习：** 文献 [9, 5, 4] 了 PCMeans 设置的推广，其中衡量簇内失真的距离度量是全局的，参数作为 SSC 的一部分进行学习。特别是，如果 $A$ 是正定矩阵，考虑以下公式：

$J_{GL}(M,Y,\mathcal{A}) = \frac{1}{2}\sum_{\mathbf{x}_i \in \mathcal{X}} (\mathbf{x}_i - \boldsymbol{\mu}_{y_i})^T A_i(\mathbf{x}_i - \boldsymbol{\mu}_{y_i}) + \sum_{\mathbf{x}_i,\mathbf{x}_j \in M} w_{ij}[y_i \neq y_j] + \sum_{\mathbf{x}_i,\mathbf{x}_j \in \mathcal{X}} w_{ij}[y_i = y_j]$

尽管上述内容关注 K-means 聚类，但该公式可以推广到其他几种设置，如信息论聚类和球面聚类。每个设置中的两个主要选择是 (i) 参数化距离 $d_l(\mathbf{x}_i, \boldsymbol{\mu}_{y_i})$，它衡量每个数据点与其对应簇均值的散度；(ii) 适当的惩罚函数 $f_L(i,j)$ 和 $f_C(i,j)$，它们衡量违反必须链接和不能链接约束的代价。在公式 20.6 中，我们有 $d_l(\mathbf{x}_i, \boldsymbol{\mu}_{y_i}) = (\mathbf{x}_i - \boldsymbol{\mu}_{y_i})^T A_i(\mathbf{x}_i - \boldsymbol{\mu}_{y_i})$，且 $f_L(i,j) = 1, f_C(i,j) = 1$

参数化散度函数：可以考虑更通用的散度函数，包括参数化散度和方向性散度。特别是，信息论聚类使用以下散度 [22, 4]：$d_l(\mathbf{x}_i,\boldsymbol{\mu}_{y_i}) = \sum_{k=1}^d x_{ik} \log \frac{x_{ik}}{\mu_{y_i,k}}$，其中 $\mu_{y_i}$ 为正。参数化的 I 散度使用对角矩阵 $A = diag(a_j)$ 以及对应每个维度 $j$ 的非负权重 $a_j$，使得 $d_{L,A}(\mathbf{x}_i,\boldsymbol{\mu}_{y_i}) = \sum_{j=1}^d a_{ij} x_{ij} \log \frac{x_{ij}}{\mu_{y_i,j}} - \sum_{j=1}^d a_{ij}(x_{ij} - \mu_{y_i,j})$。同样可以定义一种基于余弦相似性的参数化方向性散度 $d_A(\mathbf{x}_i,\boldsymbol{\mu}_{y_i}) = 1 - \frac{\mathbf{x}_i^T\boldsymbol{\mu}_{y_i}}{\|\mathbf{x}_i\|\|\boldsymbol{\mu}_{y_i}\|}$，其中 $\|\mathbf{x}_i\| = \sqrt{\mathbf{x}_i^T\mathbf{x}_i}$。

