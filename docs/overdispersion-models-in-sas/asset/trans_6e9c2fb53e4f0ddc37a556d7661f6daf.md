

## 68 SAS 中的过离散模型

```
run;
ods html close;
```

### Output 3.5: 使用 GENMOD 的椎体骨折示例结果

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_80_0.png)

| 拟合优度评估准则 |
| Criterion | DF | Value | Value/DF |
| Pearson Chi-Square | 51 | 88.2883 | 1.7311 |

| 最大似然参数估计分析 |
| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.0449 | 0.1632 | -0.3647 | 0.2750 | 0.08 | 0.7833 |
| treat | Active | 1 | -0.9000 | 0.2974 | -1.4829 | -0.3170 | 9.16 | 0.0025 |
| treat | Placebo | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | |
| Scale | 0 | 0.3157 | 0.0000 | 0.3157 | 1.3157 | | |

> 尺度参数由 Pearson 卡方值/自由度的平方根估计。

| 对比估计结果 |
| Label | Mean Estimate | Mean | L'Beta Estimate | Standard Error | Alpha | L'Beta | Chi-Square | Pr > ChiSq |
| | | Confidence Limits | | | | Confidence Limits | | |
| Placebo | 0.9561 | 0.6944 | 1.3165 | -0.0449 | 0.1632 | 0.05 | -0.3647 | 0.2750 | 0.08 | 0.7833 |
| Active | 0.3887 | 0.2388 | 0.6329 | -0.9488 | 0.2486 | 0.05 | -1.4322 | -0.4575 | 14.44 | 0.0001 |
| Rate Ratio | 0.4066 | 0.2278 | 0.7283 | -0.0900 | 0.2475 | 0.05 | -1.4829 | -0.3170 | 9.16 | 0.0025 |

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS*. Copyright © 2011, SAS Institute, Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## 第 3 章 拟似然函数 69

估计的安慰剂组每年骨折率为 $e^{-0.0449} = 0.9561$，双膦酸盐组为
$e^{-0.0449-0.9000} = 0.3887$，表明双膦酸盐组与安慰剂相比椎体骨折数量显著降低

（P 值 = 0.0025）。估计的每年骨折数为

```
$$\left(\sum_{j=1}^{n_i} y_{ij} / \sum_{j=1}^{n_i} z_{ij}\right), i = 1, 2.$
```

比率比为

```
$RR = \left(\sum_{j=1}^{n_i} y_{ij} / \sum_{j=1}^{n_i} z_{ij}\right) \cdot \left(\sum_{j=1}^{n_i} y_{2j} / \sum_{j=1}^{n_i} z_{2j}\right)$
```

在本例中结果为 0.4066。这表明与安慰剂组相比，双膦酸盐组估计的每年骨折率大约减少了 41%。比率比的近似 95% 置信区间为 (0.2270, 0.7283)。该置信区间是通过将逆链接函数，即指数函数应用于模型尺度置信区间的边界（$-1.4829, -0.3170$）得到的。由 Pearson 卡方统计量除以其自由度估计的膨胀因子的平方根为 1.3157。最大似然估计得到的所有标准误差均被该因子膨胀。

### 表 3.6：椎体骨折数据 Poisson 额外变异模型的估计值、标准误差、卡方值和 P 值

| Parameter | Estimate | Standard Error | Chi-square | P-value |
|---| Intercept | -0.0449 | 0.1632 | 0.08 | 0.7833 |
| Bisphosphonate | -0.9000 | 0.2974 | 9.16 | 0.0025 |
| Scale ($\sqrt{\}$) | 1.3157 | | | |

### 3.7 Williams’ 拟似然模型

考虑以下具有过离散的 logistic 回归模型

```
$E(T) = \mu_i, \text{Var}(T) = \mu_i\pi_i\{1+(1-\pi_i)\theta\},$ and $\log(\frac{\pi_i}{1-\pi_i}) = x_i\beta.$
```

Williams (1982) 提出了一种迭代加权最小二乘程序，类似于第 2 章方程 (2.23) 中的方法，以便同时估计 $\beta$ 和 $\theta$。在 Williams 的论文中，组内相关性用 $\phi$ 表示。为了避免与尺度（离散）参数混淆

## SAS 中的过离散模型

过离散模型。当适当时，我们将用 $\rho^2$ 表示组内相关性以表示过离散。

Williams 修改了第 2 章方程 (2.23) 中的迭代最小二乘程序，允许权重（膨胀因子）$w_j^{-1} = [1 + (m_j - 1)\theta]$ 与方差函数 $v_j = m_j\pi_j(1 - \pi_j)$ 结合使用。注意 $T_j$ 的方差为 $v_jw_j^{-1}$。对于已知的 $\theta$，$\beta$ 的拟似然估计量可以迭代求解

```
$\hat{\beta}_{(s+1)} = \hat{\beta}_{(s)} +(\mathbf{X}'\mathbf{W}\mathbf{X})^{-1}\mathbf{X}'\mathbf{W}(\mathbf{y}-\boldsymbol{\mu}),\quad$ (3.10)
```

其中 $\mathbf{V} = \text{Diag} [m_1\pi_1(1-\pi_1), m_2\pi_2(1-\pi_2), ..., m_n\pi_n(1-\pi_n)] = (v_1, v_2, ..., v_n)$ 且

```
$\mathbf{W} = \text{Diag} [\frac{1}{1+(m_1-1)\theta}, \frac{1}{1+(m_2-1)\theta}, ..., \frac{1}{1+(m_n-1)\theta}] = \text{Diag}(w_1, w_2, ..., w_n).$ The case $\theta=0$ makes $\mathbf{W} = \mathbf{I}$, the identity matrix. Then, the above iterative procedure becomes the one for finding the MLE of $\beta$.
```

当 $w_j$ 与第 $j$ 个受试者（簇）相关联时，通常的 Pearson 平方统计量

```
$\chi^2 = \sum_{j=1}^n \frac{w_j(t_j-m_j\hat{\pi}_j)^2}{m_j\hat{\pi}_j(1-\hat{\pi}_j)},\quad$ (3.11)
```

Williams 对 $E(X^2)$ 进行泰勒级数展开以推导矩估计量

```
$\hat{\theta} = \frac{\sum_{j=1}^n w_j(1-w_jv_j)}{\sum_{j=1}^n w_j(m_j-1)(1-w_jv_j)},\quad$ (3.12)
```

其中 $h_j$ 是线性预测变量 $\hat{\eta}_j = \mathbf{x}'\boldsymbol{\beta}$ 的方差。

Williams 提出的同时估计 $\beta$ 和 $\theta$ 的算法如下。

- Step 1: 假设 $\theta=0$ ($w_j=1$) 并获得 $\hat{\beta}$，$\beta$ 的 MLE，使用第 2 章方程 (2.23) 中的算法。利用方程 (3.11) 评估 Pearson 卡方统计量 $X^2$。

## 第 3 章 拟似然函数 71

Step 2: 将 X$^2$ 的值与自由度为 (n–k) 的卡方分布进行比较。如果统计量 X$^2$ 不可接受地大，则得出组内相关性大于零，（$\theta > 0$）并获得 $\hat{\theta}$ 为

```
$$\hat{\theta} = \frac{X^2 - (n-k)}{\sum(m_j-1)(1-v_j^2)}$$
```

Step 3: 使用新的权重 $w_j = [1+(m_j-1)\hat{\theta}^2]^{-1}$，利用 (3.10) 中的迭代程序估计 $\hat{\beta}$。使用方程 (3.11) 重新计算 Pearson 卡方统计量 X^2$。

Step 4: 如果 X$^2$ 接近 (n – k)，则得出 $\hat{\theta}$ 令人满意并停止该程序，使用方程 (3.12) 重新估计 $\hat{\theta}$，并返回 Step 3。

与 Williams (1982) 一样，我们重新审视 Crowder (1978) 的示例以说明该方法。Crowder 的示例由 2x2 析因实验组成，包含两种种子类型（O. aegyptiaca 75 和 73）和两种根提取物类型（豆类和黄瓜）。结果为 “t”，即 “m” 粒种子中发芽的种子数量。数据报告在表 3.7 中。

### 表 3.7：两种种子类型（O. aegyptiaca 75 和 73）和两种根提取物类型（豆类和黄瓜）的种子发芽情况

| Type of Seed | Root Extract | $t_j$ | $m_j$ |
|---|---|---|---|
| O. aegyptiaca 75 | Bean | 10 | 39 |
| | | 23 | 62 |
| | | 23 | 81 |
| | | 26 | 51 |
| | | 17 | 39 |
| | Cucumber | 5 | 6 |
| | | 53 | 74 |
| | | 55 | 72 |
| | | 32 | 51 |
| | | 46 | 79 |
| | | 10 | 13 |
| O. aegyptiaca 73 | Bean | 8 | 16 |
| | | 10 | 30 |
| | | 8 | 28 |
| | | 23 | 45 |
| | | 0 | 4 |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## SAS 中的过离散模型

| Cucumber | 3 | 12 |
| | 22 | 41 |
| | 15 | 30 |
| | 32 | 51 |
| | 3 | 7 |

我们将使用 LOGISTIC 过程，因为它具有处理 Williams 拟似然模型的能力。我们还使用 SCALE=NONE 选项拟合无过离散的模型。编程语句在程序 3.6 中提供。

### 程序 3.6：对表 3.5 的种子发芽数据拟合 Williams (1982) 拟似然模型

> Williams (1982) 使用 Crowder (1978) 中的种子发芽数据分析

type_seed = 0 对应于 O. aegyptiaca 75
type_seed = 1 对应于 O. aegyptiaca 73
root_extract = 0 对应于豆类
root_extract = 1 对应于黄瓜

```
data seeds;
input type_seed root_extract t m;
datalines;
0 0 10 39
0 0 23 62
0 0 23 81
0 0 26 51
0 0 17 39
0 1 53 74
0 1 55 72
0 1 46 79
1 0 10 13
1 0 8 16
1 0 10 30
1 0 8 28
1 1 23 45
1 1 0 4
1 1 3 12
1 1 22 41
1 1 15 30
1 1 32 51
1 1 3 7;
```

```
ods html;
proc logistic data=seeds;
model/m = type_seed root_extract type_seed*root_extract / scale=none;
out output=out-out predicted=pi_hat;
title "Full Model With SCALE=NONE";
```

```
proc logistic data=seeds;
model/m = type_seed root_extract type_seed*root_extract / scale=williams;
out output=out-out predicted=pi_hat;
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

