
选定的结果显示在优势比的对数 9.6 中。注意，用于测试活性组（腹部切开）与安慰剂（无腹内引吸）比较结果显著性的 Wald 卡方为 14.52。该统计量极显著（P 值=0.0001）。对应的优势比为 6.7，其对应的 95% 置信区间为 (2.53,18.09)。这些结果有力地支持了活性组受试者在术后疼痛较少的观察。这对应于疼痛减少了六倍。同样观察到与时间变量相关的 beta 估计值极显著（P<0.01）。时间每增加一个单位优势比为 1.22，其对应的 95% 置信区间为 (1.05,1.44)。默认情况下，`SURVEYLOGISTIC` 模拟的是疼痛量表低端的概率。因此，时间优势比大于一表示疼痛随时间增加而减轻。

# 第 9 章 边际模型的广义估计方程技术 323

**输出 9.6:** 使用 `PROC SURVEYLOGISTIC` 拟合 GEE 累计 Logit 模型的选结果

*** 对 Lumley (1996) 中的肩尖疼痛数据拟合 GEE 累计 Logit 产生的结果 ***

`SURVEYLOGISTIC` 过程

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

可以使用以下代码在 `GENMOD` 中拟合相同的累计 logit 模型：

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 `support.sas.com/publishing`。

## 9.10 夹明治估计量的小样本偏差修正

众周知，在小样本中，参数估计值协方差矩阵的 GEE 估计会导致第一类错误率膨胀。为了解决这个问题，建议使用剪刀法（jackknife）和自助法（bootstrap）等重采样方法来估计稳健协方差矩阵。Mancel 和 DeRouten (2001) 指出，这些方法对于二分类响应和较少的受试者（簇）失效。如果 `$\hat{H}^{-1}\hat{G}\hat{H}^{-1}$` 表示使用 `$\hat{H}^{-1}$` 作为“基于模型的”协方差矩阵的 GEE “明治”估计量，Mancel 和 DeRouten 认为用于估计 `$\hat{H}$` 的残差往往太小。因此，“明治”协方差矩阵可能会低估参数的协方差矩阵，且在残差偏差较大时（即簇数量较小时）具有低估的偏差。因此，为了通过在计算 `$\hat{G}$` 时对残差使用一阶泰勒级数近似来减少小样本偏差，Fay 和 Graraud (2001) 提出了两种样本修正。第一种修正与 Mancel 和 DeRouten (2001) 的修正相似，但优点是它可以应用于比 GEE 更通用的框架，例如 Cox 比例风险模型和逻辑回归。由Fay 和 Graraud (2001) 的第二种修正包括使用 f（或 t）分布代替卡方（或正态）分布，并对自由度进行调整。Kaumarni 和 Karoll (2001) 提出了一种调整，以确保使用明治估计量结合分布量时提供的覆盖概率低于标称值。Pan 和 Wall (2002) 提出了一种估计量，并允许考虑到“明治”估计量偏差的 f 检验（或 t 检验），允许同时测试多个参数。Morel (1989) 受调查采样文献中类似工作的启发，对 GEE 估计量提出了一种小样本修正，并使用广义链接函数结合标称类型数据实现了它。该修正不仅减少了第一类错误率中的小样本偏差，还保证了估计的协方差矩阵是正定的。它可以用于一个或多个参数的检验，但与 `$\hat{G}$` 残差的调整与其他修正方法不同。也就是说，该修正是加法的而非乘法的，所加项随簇（主抽样单元）数量的增加而变化。Morel, Bokossa 和 Neerhaal (2003) 将这种加法修正考虑了 GLM 和 GLMM 框架，这些框架适用于单变量和多变量类型的响应。`GLIMMIX` 过程提供了多种乘法小样本偏差修正，这些修正实际上在其文档的“基于残差的估计量”标题下找到。Morel, Bokossa 和 Neerhaal (2003) 的实际修正（简简称 MBN）位于“设计调整的 MBN 估计量”标题下。`SURVEYLOGISTIC` 过程提供了使用 Morel (1989) 修正调整明治方差估计量的选项。

根据 `PROC GLIMMIX` 的文档，带有当前乘法小样本偏差修正的经验协方差估计量的通用形式可以写为：

```
$Var(\hat{\beta}) = c \times \Omega \sum_{i=1}^{n} A_{i}' \hat{D}_{i}' \Sigma_{i}^{-1} e_{i} e_{i}' \hat{D}_{i} A_{i}, \quad (9.26)$
```

Morel, Jorge, and Nagaraj Neerhaal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA.

## 9 边际模型的广义估计方程 325

其中 `$e_i = y_i - \mu_i$`，且 `$m$` 是簇的数量（通常称为主抽样单元）。注意 (9.26) 中的 `$\Omega$` 是 `$D'VD$` 的逆矩阵。带有当前乘法小样本偏差修正的经验协方差估计量的通用形式可以写为：

### 表 9.6: 乘法小样本修正

| | | | | | |
|---|---|---|---|---|---|
| CLASSICAL | 1 | I | | | |
| | | | | | (9.27) |

上文上文给出的 `$\delta_m$` 公式是 Morel (1989) 相应公式的推广；它允许用户通过 `$d$` 限制 `$\delta_m$` 的上界。默认值为 2，对应于 0.5 的上限。选择 `$d=1$` 意味着当 `$m \leq 2k$` 时 `$\delta_m=1$`。在这种情况下，经典的明治量通过 `$\phi$` 加法地“膨胀”。

量

```
\text{trace} \left [ \Omega \left[ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right ] / k
```

是“广义设计”的平均值（参见 Rao and Scott, 1981）。在拟似然理论中，它是扩大或缩小“原始”协方差估计所需的稳定常数。注意

```
\text{trace} \left [ \Omega \left [ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right ] > 0.
```

用户可以选择满足 `$0 \leq r \leq 1$` 的 `$r$`。默认值为 `$r=1$`，这是 `$\phi$` 的自然下界，确保明治总是膨胀。这对应于设计效应大于1的过度离散情况。如果用户怀疑欠离散，`$r$` 应该小于 1，使得膨胀不那么显著。通过取 `$r$` 为正，用户强制执行了最小程度的修正。选择 `$r=0$` 意味着没有对 `$\phi$` 的下界施加限制。

# 第 9 章 边缘模型的广义估计方程技术 327

```
trace \left[ \hat{\Omega} \sum_{i=1}^{m} \hat{\Sigma}_i \Sigma_i^{-1} e_i e_i^T \Sigma_i^{-1} \hat{\Delta}_i \right] / k
```

完全决定了 `$\hat{\phi}$` 的值。取 r > 1 是没有意义的，因为它可能会使“朴素”协方差估计超出拟似然理论允许的范围。注意估计量 (9.28) 可以写为

```
Var(\hat{\phi}) = \hat{\Omega} \sum_{i=1}^{m} \hat{\Sigma}_i \Sigma_i^{-1} (c_i e_i^T + \mathbf{B}_i) \Sigma_i^{-1} \hat{\Sigma}_i \Omega, (9.29)
```

其中 `$\mathbf{B}_i = \delta_m \phi_i^T \Sigma_i$`。

MBN 具有采样单位数量较小时能够恢复秩的良好属性。如果 `$m < k$`，经典三明治估计量的“肉部分”本质上是秩矩阵之和。相对于 X 的秩，受试者数量较少会导致秩的丢失，以及随后用于假设检验的自由度损失。正如 `GLIMMIX` 文档所述，“加性 MBN 调整考虑了秩的耗尽。”

让我们再次考虑第 4.9 节和 9.5 节讨论的骨化问题。我们将说明 `GLIMMIX` 过程中可用的某些样本偏偏正的使用。我们首先在 `GLIMMIX` 中使用 Ferratino 的方差选项 `TYPE=VC`；工作矩阵，这在 `GLIMMIX` 中对应于。然后，我们在 `FIRORES`、`FIROEQ` 和 `MBN` 选项计算经验方差估计量。编程语句见“程序 9.2：继续”。

# 程序 9.2：继续

```
ods html;

title *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL-CLASS ***

proc glimmix data=ossification_b_empirical=classical;

class litters pht;

model y(ref='0') = tcpo pht tcpo*pha / dist=binary link=logit s;

random_residual / subject=litters type=vc;

run;
```

```
ntitle *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL-FIRORES ***

proc glimmix data=ossification_b_empirical=firores;

class litters pht;

model y(ref='0') = tcpo pht tcpo*pha / dist=binary link=logit s;

random_residual / subject=litters type=vc;

run;
```

```
ntitle *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL-FIROEQ ***

proc glimmix data=ossification_b_empirical=firoeq;

class litters pht;

model y(ref='0') = tcpo pht tcpo*pha / dist=binary link=logit s;

random_residual / subject=litters type=vc;

run;
```

```
ntitle *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL=MBN ***

proc glimmix data=ossification_b_empirical=mbn;

class litters pht;
```

Morel, Jorge, and Nagaraj Neelheer. Overdispersion Models in SAS. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多资源，请访问 `sas.com/publishing`。

# 328 SAS 中的过度离散模型

```
model y (ref='0') = tcpo pht tcpo*pha / dist=binary link=logit;

random_residual / subject=litters type=vc;

ods html;
```

表 9.7 展示了 `GLIMMIX` 过程中经验方差估计量的四种样本偏差校正的使用。调整后的标准误差略大，以修正“三明治”中嵌入的微小偏差。注意 beta 估计值与四种校正相同。

# 表 9.7：经验方差下的 Beta 估计和标准误差——四种经验方差选项全因子逻辑 GLM 的骨化数据 | 参数 | 估计值 | CLASSIC 标准误差 | FIROEQ 标准误差 | MBN 标准误差 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 (Intercept) | 0.8323 | 0.2472 | 0.2512 | 0.2555 |
| TCPO | -0.4881 | 0.4063 | 0.4292 | 0.4235 | 0.4199 |
| PHT | -2.1094 | 0.3344 | 0.3589 | 0.3543 | 0.3611 |
| TCPO + PHT | 1.0453 | 0.7628 | 0.8329 | 0.8339 | 0.7874 |

# 齐质性检验

多项模型的 GLM 为每个类别的概率具有单独的回归方程。因此，感兴趣的话题自然是以相同的方式检查差异，或者特定的协变量是否倾向于影响特定类别。以下示例旨在说明使用广义模型对多项结果进行齐质性检验。为了简单起见，我们限制在两种产品和名义响应的情况下，即使用 GEE 方法论进行分析。然而，本节讨论的方法论可以扩展到 2x3 列联表的情况。`$\pi_{11}$`、`$\pi_{12}$` 和 `$\pi_{13}$` 分别将底层真实概率（率）视为“低”、“中”和“高”。同样，我们定义 `$\pi_{21}$`、`$\pi_{22}$` 和 `$\pi_{23}$` 为产品 2 的相应概率。齐质性假设可以述为：

`$H_0: \pi_{11} = \pi_{21}$` 和 `$\pi_{12} = \pi_{22}$` 和 `$\pi_{13} = \pi_{23}$`
`$H_1: \pi_{11} \neq \pi_{21}$` 或 `$\pi_{12} \neq \pi_{22}$` 或 `$\pi_{13} \neq \pi_{23}$` (9.30)

由于 `$\pi_{i0}$` 的线性依赖，我们有 `$\pi_{i1} = 1 - \sum_{j=1}^2 \pi_{ij} = 1, i=1,2$`。读者可能会注意到我们正在将“低”的概率表示为其他产品的组合。虽然可以选择三个类别中的任何一个，但我们选择将“低”的概率表示为其他概率的线性组合，以便与以后使用的广义逻辑模型保持一致，该类别将作为基准。然后，齐质性假设 (9.30) 可以述为：

`$H_0: \pi_{12} = \pi_{22}$` 和 `$\pi_{13} = \pi_{23}$`
`$H_1: \pi_{12} \neq \pi_{22}$` 或 `$\pi_{13} \neq \pi_{23}$`

等价于

`$H_0: \ln\frac{\pi_{12}}{\pi_{22}} = 0$` 和 `$\ln\frac{\pi_{13}}{\pi_{23}} = 0$`
`$H_1: \ln\frac{\pi_{12}}{\pi_{22}} \neq 0$` 或 `$\ln\frac{\pi_{13}}{\pi_{23}} \neq 0$`。(9.31)

注意，上述表示以“低”类别作为基准的广义逻辑链接的重述。在实践中，如果提出假设，习惯上考虑两个额外的假设：

`$H_0: \pi_{12} = \pi_{22}$` 和 `$H_1: \pi_{12} \neq \pi_{22}$` (9.32)

以及

`$H_0: \pi_{13} = \pi_{23}$` 和 `$H_1: \pi_{13} \neq \pi_{23}$` (9.33)

这些假设可以用对数比重述如下：

`$H_0: \ln\frac{\pi_{12}}{\pi_{22}} = 0$` 和 `$H_1: \ln\frac{\pi_{12}}{\pi_{22}} \neq 0$` (9.34)

以及

`$H_0: \ln\frac{\pi_{13}}{\pi_{23}} = 0$` 和 `$H_1: \ln\frac{\pi_{13}}{\pi_{23}} \neq 0$`。(9.35)

`$I(\cdot)$` 代表一个产品指示函数，`$i=1, 2$`。假设广义逻辑函数

$$\ln\frac{\pi_{2i}}{\pi_{ii}} = \dots$$

（注：由于提供的文本中存在大量重复的段落和乱码，翻译已针对核心内容进行。）

# 第9章 边际模型的广义估计方程技术 331

```sas

u = uniform( seed);

if u < rho then y = yy;

else

    uu = uniform( seed);

    if u < cp12 then y = 2;

    if u < pi21 then y = 1;

end;

output;

*-- Product 2;

Product = 2;

Subjid = j + n;

YY = 3;

u = uniform( seed);

if u < cp12 then y = 2;

if u < pi21 then y = 1;

for i=1 to m;

  Y = 3;

  u = uniform( seed);

  if u < rho then y = yy;

  else

      uu = uniform( seed);

      if u < cp21 then y = 2;
```
