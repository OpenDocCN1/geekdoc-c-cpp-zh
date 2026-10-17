
Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 需更多 SAS 资源，请访问 `support.sas.com/publishing`。

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_234_0)

上一个箱图中箱的底部和顶部边缘表示**四分位距**（intra-quartile range），即第一分位数和第三分位数之间（第 25 百分位和第 75 百分位）之间的值范围。

在 Scale Multinomial 模型下，每个多项响应相关的普通协方差矩阵被单因子 $\hat{\phi}=4.8323$ 放大。这是通过 Pearson 卡方统计量除以其自由度得到的。在 Generalized Scale Multinomial 模型下，每个多项协方差矩阵的不同分量通过因子 $\phi_1=7.9296$ 和 $\phi_2=2.0419$ 进行调整。下面的编程语句用于获取 (7.21) 中残差的箱图。如果单因子普通多项模型适用于镉-锌数据，预计 $Z_j$ 的每个分量都是同分布的。

# SAS 中的 224 过度离散模型

$$V(T) = m\{\text{Diag}(\pi) - \pi\pi^T\mathbf{1}+\rho^2(m-1)}, \quad (7.29)$$

其中 $\pi = (\pi_1, \pi_2, ..., \pi_d)$ 是概率向量，$0 < \pi_i < 1$，$\sum_{i=1}^d \pi_i < 1$，且rho$ 是过度离散参数。注意与伽马相关的概率为：

$$\pi_{d+1} = 1 - \sum_{i=1}^d \pi_i.$$ 由方程 (7.28) 和 (7.29) 给出的矩结构可以通过在通常多项空间内支撑的若干分布来实现。我们将此类分布称为过度离散多项分布（或模型）。我们考虑两种过度离散多项模型的极大似然估计，即狄利克雷-多项分布（Dirichlet-multinomial distribution）以及由本文书作者提出的随机聚类多项分布（Random-clumped Multinomial distribution）。

如果 $t$ 是 $T$ 的实现值，$t = (t_1, t_2, ..., t_d)$ 且 $t_{d+1} = m - \sum_{i=1}^d t_i$，根据 Mosimann (1962)，狄利克雷-多项 (DM) 分布的概率函数为：

$$P_{DM}(t; \pi, \rho) = \frac{m!}{t_1!t_2!...t_d!} \frac{\Gamma(c)}{\Gamma(m+c)} \frac{\prod_{i=1}^{d+1}\Gamma(t_i+c_i)}{\prod_{i=1}^{d+1}\Gamma(c_i)}, \quad (7.30)$$

其中 $c = \rho^2(1-\rho)$，$0 < \rho < 1$，且 $\Gamma(\cdot)$ 表示伽马函数。狄利克雷-多项分布的均值和方差与方程 (7.28) 和 (7.29) 给出的相同。狄利克雷-多项分布是第 4.2 节讨论的 Beta-二项分布的多元扩展。如果 $T|P$ 的条件分布是 Multinomial($P;m$)，且 $P$ 是概率密度为的狄利克雷分布：

$$f_D(P; \pi, \rho) = \frac{\Gamma(c)}{\prod_{i=1}^{d+1}\Gamma(c_i)} \prod_{i=1}^{d+1}P_i^{c_i-1}}, \quad (7.31)$$

那么 $T$ 的无条件分布就是狄利克雷-多项分布。Mosimann (1962) 将此分布称为复合多项分布（Compound Multinomial Distribution）。这把 Beta-二项分布推广到了多元情况。DM 分布具有许多有趣的性质。例如，它们的边缘分布仍然是 DM 分布，特别是一维边缘分布是 Beta-二项分布。正如我们稍后将看到的，这一观察在极大似然估计的计算中证明是非常重要的。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 `support.sas.com/publishing`。

## 7.8 随机聚类多项分布

我们在这里考虑的第二个过度离散多项模型是由 Morel 和 Nagaraj (1993) 以及 Neerchal 和 Morel (1998) 提出的。它是第 4.3 节涵盖的随机聚类多项分布的多元推广。该模型可以推导如下。

设 $Y, Y_1^0, \dots, Y_m^0$ 是独立同分布的多项随机变量，参数为 $(\boldsymbol{\pi}; 1)$。所有这些多项随机向量中已经移除了 $(d+1)$ 类别。设 $U_1, U_2, \dots, U_m$ 是独立同分布的均匀(0,1) 随机变量，$\rho$ 是任意随机变量，$0 < \rho < 1$。如第 4.3 节所示，定义：

$$Y_i = Y_i^0(U_i \le \rho) + Y_i^0(U_i > \rho), \quad i=1,2,\dots,m$$

其中 $I(\cdot)$ 表示指示函数。

现在考虑随机变量：

$$\mathbf{T} = \sum_{i=1}^m Y_i$$

$\mathbf{T}$ 的均值和协方差矩阵如方程 (7.28) 和 (7.29) 所示。作为第 4 章随机聚类二项分布的单变量版本，随机向量 $\mathbf{T}$ 可以表示为：

$$\mathbf{T} = (\mathbf{YN}) + (\mathbf{X|N}), \quad \quad (7.32)$$

其中 $N \sim \text{Binomial}(\rho; m)$，当 $N < m$ 时 $(\mathbf{X|N}) \sim \text{Multinomial}((1-\rho)\boldsymbol{\pi}; m)$。随机聚类多项 $T$ 的聚类机制解释已在第 4.3 节讨论。Sutrachdar (2001) 为描述聚类机制的若干场景提供了图形表示。

可以证明随机聚类多项分布 (7.32) 的概率函数为：

$$P_{\text{RCM}}(\mathbf{T}=\mathbf{t}) = \sum_{i=1}^{d+1} \dots P(\mathbf{X}_i=t_i), \quad (7.33)$$

其中 $\mathbf{X}_i$ 服从为 Multinomial($(1-\rho)\boldsymbol{\pi}; m)$，对于 $i=1,2,\dots,d$。随机聚类多项 $T$ 的聚类机制解释已在第 4.3 节讨论。Sutrachdar (2001) 为描述聚类机制的若干场景提供了图形表示。

输出 7.3：Dirichlet-multinomial 模型和随机聚集 Multinomial 模型下的 MLE 结果——住房满意度数据

# 住房满意度，Brier(1980)，农村地区

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_240_0.png)

## 7.10 一个森林花粉计数问题

Mosimann (1962) 分析了一个对四种树木类森林花粉（松树、橡树和赤木）的问题。这是文献中首次将 Dirichlet-multinomial 分布用于建模过离散性的例子。数据见表 7.4，由 n = 73 组组成，每组代表在岩芯特定深度处四种化石花粉出现频率的计数。花粉计数一直直到总数达到 $m_j = 100$ 粒为止。与 Mosimann 的分析一样，我们将不同组的数据视为相互独立的。对于第 $j$ 组（$j = 1, 2, ..., 73$），$t_j = (t_{j1}, t_{j2}, t_{j3})$ 是“松树”、“冷杉”和“橡树”类型的观测计数向量，满足常规约束 $t_{j1} + t_{j2} + t_{j3} \le 100$。假设 $t_j$ 是 $T_j$ 的一个实现值。当 $T_j$ 被建模为 Dirichlet-multinomial($pi,r;m_j$) 或 Random-clumped Multinomial($pi,r;m_j$) 时，我们将找到 $\theta = (\pi, r')$ 的 MLE。注意 $\pi = (\pi_1,\pi_2,\pi_3)$，其中 $\pi_1, \pi_2$ 和 $\pi_3$ 分别代表在特定时间内落入岩芯的松树、冷杉和橡树花粉的比例。同样注意 $\pi_1+\pi_2+\pi_3 < 1$，且赤木花粉的比例为 $\pi_4 = 1-(\pi_1+\pi_2+\pi_3)$。

### 表 7.4：森林花粉计数数据

| t1 | t2 | t3 | t1 | t2 | t3 | t1 | t2 | t3 | t1 | t2 | t3 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 94 | 0 | 5 | 85 | 1 | 84 | 1 | 12 | 88 | 0 | 0 | 9 |
| 75 | 2 | 1 | 91 | 1 | 4 | 97 | 0 | 3 | 94 | 0 | 4 |
| 81 | 2 | 3 | 99 | 1 | 0 | 83 | 0 | 13 | 69 | 7 | 18 |
| 95 | 2 | 3 | 90 | 2 | 8 | 81 | 1 | 15 | 90 | 0 | 8 |
| 89 | 3 | 1 | 91 | 0 | 8 | 81 | 1 | 16 | 86 | 1 | 8 |
| 84 | 5 | 1 | 79 | 1 | 19 | 76 | 2 | 18 | 90 | 0 | 7 |
| 81 | 3 | 10 | 89 | 0 | 7 | 87 | 3 | 7 | 74 | 5 | 16 |
| 97 | 0 | 2 | 95 | 2 | 1 | 91 | 1 | 5 | 82 | 2 | 11 |
| 86 | 1 | 8 | 90 | 3 | 5 | 94 | 0 | 5 | 87 | 3 | 9 |
| 86 | 2 | 1 | 93 | 1 | 6 | 88 | 1 | 11 | 68 | 3 | 26 |
| 82 | 2 | 1 | 90 | 2 | 7 | 93 | 4 | 2 | 77 | 3 | 11 |
| 72 | 1 | 6 | 89 | 2 | 9 | 84 | 0 | 8 | 86 | 2 | 7 |
| 89 | 0 | 8 | 88 | 1 | 9 | 87 | 1 | 12 | 79 | 1 | 11 |
| 93 | 4 | 2 | 99 | 0 | 1 | 89 | 1 | 6 | 87 | 0 | 11 |
| 87 | 1 | 1 | 86 | 1 | 10 | 73 | 0 | 13 | 79 | 1 | 17 |
| 85 | 0 | 12 | 88 | 0 | 7 | 73 | 3 | 8 | 74 | 0 | 19 |
| 91 | 0 | 7 | 91 | 0 | 7 | 94 | 1 | 3 | 80 | 0 | 14 |
| 95 | 1 | 3 | 84 | 0 | 14 | 81 | 2 | 9 | 85 | 3 | 9 |
| 94 | 3 | 3 | | | | | | | | | |

$t_1, t_2$ 和 $t_3$ 分别是松树、冷杉和橡树的花粉计数。程序 7.4 读取森林花粉数据并拟合 Dirichlet-multinomial 和 Random-clumped Multinomial 的语句。在上例中，调用了 "`DirMult`" 模块。极大似然结果见表 7.5。

### 程序 7.4：对森林花粉数据拟合 Dirichlet-multinomial 和 Random-clumped Multinomial 模型

```sas
/*
Forest Pollen Count, Mosimann (1962)
*/
data pollen_count;
  input t1 t2 t3;
  t4 = 100 - t1 - t2;
datalines;
94 0 5 85 1 84 1 12 88 0 0 9
75 2 1 91 1 4 97 0 3 94 0 4
81 2 3 99 1 0 83 0 13 69 7 18
95 2 3 90 2 8 81 1 15 90 0 8
89 3 1 91 0 8 81 1 16 86 1 8
84 5 1 79 1 19 76 2 18 90 0 7
81 3 10 89 0 7 87 3 7 74 5 16
97 0 2 95 2 1 91 1 5 82 2 11
86 1 8 90 3 5 94 0 5 87 3 9
86 2 1 93 1 6 88 1 11 68 3 26
82 2 1 90 2 7 93 4 2 77 3 11
72 1 6 89 2 9 84 0 8 86 2 7
89 0 8 88 1 9 87 1 12 79 1 11
93 4 2 99 0 1 89 1 6 87 0 11
87 1 1 86 1 10 73 0 13 79 1 17
85 0 12 88 0 7 73 3 8 74 0 19
91 0 7 91 0 7 94 1 3 80 0 14
95 1 3 84 0 14 81 2 9 85 3 9
94 3 3
;
ods html;
%DirMult(pollen_count, "Forest Poll Count, Mosimann (1962)");
ods close;
```

### 表 7.5：Dirichlet-multinomial 和 Random-clumped Multinomial 模型下森林花粉计数数据的极大似然估计

| 参数 | Dirichlet-multinomial 估计 | Dirichlet-multinomial 标准误 | Random-clumped Multinomial 估计 | Random-clumped Multinomial 标准误 |
| :--- | :--- | :--- | :--- | :--- |
| $\pi_1$ | 0.08621 | 0.00653 | 0.08636 | 0.00482 |
| $\pi_2$ | 0.01643 | 0.00224 | 0.01514 | 0.00153 |
| $\pi_3$ | 0.00880 | 0.00531 | 0.08626 | 0.00395 |
| $\rho$ | 0.12783 | 0.01094 | 0.08972 | 0.01390 |
| 对数似然值 | -507.82206 | | -534.27114 | |

$\pi_1, \pi_2$ 和 $\pi_3$ 分分别是冷杉、松树和橡树花粉的概率。

在这个例子中，样本量相对较大（n = 73），两种模型下的 $\pi = (\pi_1, \pi_2, \pi_3)$ 估计值彼此接近。Dirichlet-multinomial 下 $\rho$ 的估计值结果略大一些。然而，两组 MLE 之间的差异似乎出现在估计的标准误上：在本例中，Random-clumped Multinomial 的误差比 Dirichlet-multinomial 的误差要小。这是 Random-clumped Multinomial 分布在 $m_j$ 较大时的一个固有性质。该性质将在下一章进行讨论。

## 7.11 多项响应的广义线性离散模型——重新审视出生研究

与多项分布类似，DM 和 RCM 也可以结合协变量使用，以获得多项概率向量的 GLM。我们限制在使用最常用的连接函数：累积 logit 和 logit。

# 第 7 章 过离散多项响应的似然模型 233

| 0 | 0 | -1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 1 | -1 | 0 | 0 | 0 | 0 | 0 |
| 带 C= | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 |

因此，用于检验 (7.37) 的 Wald 统计量为：

```
$$X^2 = (C\hat{\theta})^T C \hat{V}(\hat{\theta}) C^{-1} (C\hat{\theta}) \quad (7.38)$$
```

在原假设下，该统计量渐近服从自由度为五的卡方统计分布。在本例中，矩阵 $\hat{V}(\hat{\theta})$ 是满秩的。因此，自由度由矩阵 $C$ 的秩决定，即五。

程序 7.5 包含了使用链接函数 (7.35) 将狄利克雷-多项（Dirichlet-multinomial）和随机聚类多项（Random-clumped Multinomial）模型拟合表 7.2 缺陷研究数据的编程语句。我们跳过了与数据读取相关的语句，这些可以在程序 7.2 中找到。在本例中，我们使用了 `NLMIXED` 过程。`NLMIXED` 中的 `CONSTRAINT` 语句提供了经过自由度归一化的 (7.38) Wald 。这可以用 F 分布近似。由于我们的模型（DM 和 RCM）是基于似然的，我们还可以计算似然比检验以及与 (7.38) 中 Wald 检验对应的得分检验。注意，在 ODS 语句中，已经列出了特定的表格来计算用于检验平行假设的 Wald 检验和似然比检验。涉及累积对数（cumulative logits）的参数初始估计是通过 `LOGISTIC` 过程链接的（此处未显示）。编程语句由 Sandia 国家实验室的 John New 博士感谢提供。
