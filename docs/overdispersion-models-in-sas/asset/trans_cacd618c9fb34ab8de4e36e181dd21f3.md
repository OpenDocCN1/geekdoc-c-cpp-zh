

# 第 9 章 边际模型的广义估计方程技术 323

**输出 9.6:** 使用 PROC SURVEYLOGISTIC 拟合 GEE 累计 Logit 模型的选结果

*** 对 Lumley (1996) 中的肩尖疼痛数据拟合 GEE 累计 Logit 产生的结果 ***

SURVEYLOGISTIC 过程

| 效应类型 3 分析 | | | |
| 效应 | DF | Wald 卡方检验 | Pr > ChiSq |
| --- | --- | --- | --- |
| trt | 1 | 14.5228 | 0.0001 |
| gender | 1 | 0.0575 | 0.8105 |
| age | 1 | 3.5987 | 0.0578 |
| time | 1 | 6.6168 | 0.0101 |

| 优势比估计值 | | | |
| 效应 | 点估计值 | 95% Wald 置信区间 |
| --- | --- | --- | --- |
| trt 活动组 vs 安慰剂 | 6.766 | 2.531 | 18.086 |
| gender 女性 vs 男性 | 1.130 | 0.415 | 3.079 |
| age | 1.027 | 0.999 | 1.055 |
| time | 1.217 | 1.048 | 1.414 |

可以使用以下代码在 GENMOD 中拟合相同的累计 logit 模型：

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

## 9.10 夹明治估计量的小样本偏差修正

众周知，在小样本中，参数估计值协方差矩阵的 GEE 估计会导致第一类错误率膨胀。为了解决这个问题，建议使用剪刀法（jackknife）和自助法（bootstrap）等重采样方法来估计稳健协方差矩阵。Mancel 和 DeRouten (2001) 指出，这些方法对于二分类响应和较少的受试者（簇）失效。如果 $\hat{H}^{-1}\hat{G}\hat{H}^{-1}$ 表示使用 $\hat{H}^{-1}$ 作为“基于模型的”协方差矩阵的 GEE “明治”估计量，Mancel 和 DeRouten 认为用于估计 $\hat{H}$ 的残差往往太小。因此，“明治”协方差矩阵可能会低估参数的协方差矩阵，且在残差偏差较大时（即簇数量较小时）具有低估的偏差。因此，为了通过在计算 $\hat{G}$ 时对残差使用一阶泰勒级数近似来减少小样本偏差，Fay 和 Graraud (2001) 提出了两种样本修正。第一种修正与 Mancel 和 DeRouten (2001) 的修正相似，但优点是它可以应用于比 GEE 更通用的框架，例如 Cox 比例风险模型和逻辑回归。由Fay 和 Graraud (2001) 的第二种修正包括使用 f（或 t）分布代替卡方（或正态）分布，并对自由度进行调整。Kaumarni 和 Karoll (2001) 提出了一种调整，以确保使用明治估计量结合分布量时提供的覆盖概率低于标称值。Pan 和 Wall (2002) 提出了一种估计量，并允许考虑到“明治”估计量偏差的 f 检验（或 t 检验），允许同时测试多个参数。Morel (1989) 受调查采样文献中类似工作的启发，对 GEE 估计量提出了一种小样本修正，并使用广义链接函数结合标称类型数据实现了它。该修正不仅减少了第一类错误率中的小样本偏差，还保证了估计的协方差矩阵是正定的。它可以用于一个或多个参数的检验，但与 $\hat{G}$ 残差的调整与其他修正方法不同。也就是说，该修正是加法的而非乘法的，所加项随簇（主抽样单元）数量的增加而变化。Morel, Bokossa 和 Neerhaal (2003) 将这种加法修正考虑了 GLM 和 GLMM 框架，这些框架适用于单变量和多变量类型的响应。GLIMMIX 过程提供了多种乘法小样本偏差修正，这些修正实际上在其文档的“基于残差的估计量”标题下找到。Morel, Bokossa 和 Neerhaal (2003) 的实际修正（简简称 MBN）位于“设计调整的 MBN 估计量”标题下。SURVEYLOGISTIC 过程提供了使用 Morel (1989) 修正调整明治方差估计量的选项。

根据 PROC GLIMMIX 的文档，带有当前乘法小样本偏差修正的经验协方差估计量的通用形式可以写为：

```
$Var(\hat{\beta}) = c \times \Omega \sum_{i=1}^{n} A_{i}' \hat{D}_{i}' \Sigma_{i}^{-1} e_{i} e_{i}' \hat{D}_{i} A_{i}, \quad (9.26)
```

Morel, Jorge, and Nagaraj Neerhaal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA.

## 9 边际模型的广义估计方程 325

其中 $e_i = y_i - \mu_i$，且 $m$ 是簇的数量（通常称为主抽样单元）。注意 (9.26) 中的 $\Omega$ 是 $D'VD$ 的逆矩阵。带有当前乘法小样本偏差修正的经验协方差估计量的通用形式可以写为：

### 表 9.6: 乘法小样本修正

| | | | | | |
|---|---|---|---|---|---|
| CLASSICAL | 1 | I | | | |
| | | | | | (9.27) |

上文上文给出的 $\delta_m$ 公式是 Morel (1989) 相应公式的推广；它允许用户通过 $d$ 限制 $\delta_m$ 的上界。默认值为 2，对应于 0.5 的上限。选择 $d=1$ 意味着当 $m \leq 2k$ 时 $\delta_m=1$。在这种情况下，经典的明治量通过 $\phi$ 加法地“膨胀”。

量

```
\text{trace} \left [ \Omega \left[ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right ] / k
```

是“广义设计”的平均值（参见 Rao and Scott, 1981）。在拟似然理论中，它是扩大或缩小“原始”协方差估计所需的稳定常数。注意

```
\text{trace} \left [ \Omega \left [ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right ] > 0.
```

用户可以选择满足 $0 \leq r \leq 1$ 的 $r$。默认值为 $r=1$，这是 $\phi$ 的自然下界，确保明治总是膨胀。这对应于设计效应大于1的过度离散情况。如果用户怀疑欠离散，$r$ 应该小于 1，使得膨胀不那么显著。通过取 $r$ 为正，用户强制执行了最小程度的修正。选择 $r=0$ 意味着没有对 $\phi$ 的下界施加限制。

