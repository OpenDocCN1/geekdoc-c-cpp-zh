

# 第 2 章 广义线性模型 17

为找到使 (2.4) 最小的 $\beta$，需要求出 (2.4) 对 $\beta$ 的一阶导数向量，并令其等于零，

```
$\frac{\partial S(\beta)}{\partial\beta} = -2X'y+2X'X\beta = 0.$\quad (2.5)
```

(2.5) 的解是熟知的最小二乘估计量

```
$\hat{\beta} = (X'X)^{-1}X'y.$\quad (2.6)
```

显然，在这种简化方法中，矩阵 $X'X$ 是满秩的。

可以证明，$\hat{\beta}$，$\beta$ 的最小二乘估计量，是无偏的。其协方差矩阵为

```
$Var(\hat{\beta}) = \sigma^2(X'X)^{-1}.$
```

估计量 $\hat{\beta}$ 在最小方差无偏估计量（BLUE）意义下是最优的，即在所有估计量为观测值的线性函数时，它是无偏估计量，具有最小方差，也就是形如 $\hat{\beta}=Ry$ 的估计量，其中 $R$ 是一个 knx 的实数矩阵。残差平方和的最小值，$(y_j-\hat{y}_j)^2$，提供了 $\sigma^2$ 的自然估计量。可以证明估计量

```
$\hat{\sigma}^2 = \frac{\sum_{j=1}^n(y_j-\hat{y}_j)^2}{n-k}.$\quad (2.7)
```

对 $\sigma^2$ 是无偏的。

读者可能已经注意到，OLS 方法并不要求式 (2.1) 中的 $\varepsilon_j$ 服从正态分布。只要它们满足 $E(\varepsilon_j) = 0$ 且 $Var(\varepsilon_j) = \sigma^2$ 且相关，BLUE 性质就成立。$\theta = (\beta', \sigma^2)$ 的最大似然估计量（MLE），记为 $\hat{\theta} = (\hat{\beta}', \hat{\sigma}^2)$，可以在 $\varepsilon_j$ 独立同分布于
Normal$(0, \sigma^2)$ 时求得。为此，需要似然函数 $\prod_{i=1}^n f(\epsilon_i; \sigma)$，其中

```
$f(\epsilon_i; 0) = \frac{1}{2\pi\sigma^2}} \exp\left(\frac{(y_i - x_i\beta)^2}{2\sigma^2}\right)$
```

MLE $\hat{\theta} = (\hat{\beta}, \hat{\sigma}^2)$ 通过最大化似然函数的对数得到，即先对 $\beta$ 和 $\sigma^2$ 求对数似然的偏导数，然后令这些导数等于零，从而分别求得 $\beta$ 和 $\sigma^2$ 的解。对数似然的导数被称为 **score function**。可以证明 $\hat{\beta}$ 的 MLE 为

```
$$\hat{\beta} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$ (2.8)
```

这正是式 (2.6) 中的 OLS 估计量 $\hat{\beta}$。$\sigma^2$ 的 MLE  turns out to be

```
$$\hat{\sigma}^2 = \frac{\sum_{i=1}^n (y_i - x_i\beta)^2}{n}$ (2.9)
```

注意 $\hat{\sigma}^2 = \frac{n-k}{n}\sigma^2$，因此 $\hat{\sigma}^2$ 是渐近无偏的（相合的）。也就是说，$\hat{\sigma}^2$是有偏的，但其偏差随着 $n$ 的增大趋于零。

评估线性模型质量的一种方法是检查估计残差 $\hat{\epsilon}_i = y_i - \sum_{j=1}^k x_{ij}\hat{\beta}_j$。残差的一个良好性质是它们与预测值（线性预测值）$\hat{\y}_i = \sum_{j=1}^k x_{ij}\hat{\beta}_j$ 不相关。因此，估计残差 $\hat{\epsilon}_i$ 与线性预测值 $\hat{\y}_i$ 的散点图（诊断图）应随机散布而不呈现任何模式。诊断图中的持续模式表明模型存在不足或 **Lack-of-Fit (LOF)**。残差的正态性可通过 **Normal Probability Plot** 直观评估。正态图是一种图形技术，用于评估残差，进而评估数据是否近似正态分布。在正态概率图上，

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

经验累积分布函数与标准正态分布累积分布函数的相应分位数一起作图。另一种常见图是分位数-分位数图（Q-Q Plot），它是残差的观测值与来自标准正态分布的随机样本的顺序统计量的期望值的图。在任何一种情况下，绘图点应基本沿一条直线排列。偏离直线表明数据存在偏态。诊断图对于识别数据集中可能的异常值和有影响的观测值也非常有用。关于此主题有许多优秀书籍可供参考——我们建议读者参考 Montgomery, Peck, and Vining (2007) 以获得 gentle introduction。

## 第 2 章 广义线性模型 19

### 2.3 一个简单线性回归示例

考虑表 2.1 中的数据，包含 15 只高蛋白饮食的雌性大鼠从 24 到 84 天龄的初始体重和体重增加（克）。这些数据取自 Snedecor and Cochran (1980, 7th Ed., pp. 156–157)。

### 表 2.1：15 只大鼠的初始体重和体重增加（克）

| Rat Number | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Initial Weight, X | 50 | 64 | 76 | 64 | 74 | 60 | 69 | 68 | 56 | 48 | 57 | 59 | 46 | 45 | 65 |
| Gains, Y | 128 | 158 | 159 | 118 | 133 | 112 | 96 | 126 | 132 | 118 | 107 | 106 | 82 | 103 | 104 |

这些数据收集的目的是调查体重增加是否与初始体重相关。如果相关，则在比较不同饮食时，可以通过考虑大鼠的初始体重来使雌性大鼠的喂养实验更准确，这通常在协方差分析中进行。我们使用 GLIMMIX 过程获得 OLS 和 MLE 结果。编程语句在程序 2.1 中提供。

## 程序 2.1：体重增加——使用 OLS 和 MLE 方法的简单线性回归

```
/*
Snedecor and Cochran 1980, 7th Ed. Pages 156-157
Gains in Weight Example
*/
data gains_in_weight;
  do Rat=1 to 15;
    input x @@
    output;
  end;
datalines;
  50 64 76 64 74 60 69 68 57 48 57 49 46 65
  128 158 159 119 133 112 96 126 132 118 107 106 82 103 104
;

proc sort data=gains_in_weight;
  by rat;
run;
proc transpose data=gains_in_weight out=gains_in_weight
  (rename=(COL1=Initial_Weight COL2=Gains));
  by rat;
  var x;
run;
ods html;
  graphics on;
  title """ MLE Results -- Gains in Weight Data ****"
proc glimmix data=gains_in_weight plots=residualpanel;
  model Gains = Initial_Weight / solution;
run;
  title """ MLE Results -- Gains in Weight Data ****"
proc glimmix data=gains_in_weight noreml;
  model Gains = Initial_Weight / solution;
run;
ods graphics off;
ods html close;
```

对于模型 (2.1)，GLIMMIX 过程不使用任何迭代拟合。然而，尺度参数 $\sigma^2$ 通过残差平方和除以残差自由度 $(n-k=13)$ 估计得到 $\hat{\sigma}^2$，而不是除以大鼠总数 $(n=15)$，后者对应于 $\tilde{\sigma}^2$。后者是最大似然估计量，而前者是无偏估计量且是众所周知的方法。与 PROC GLM 和 REG 不同，GLIMMIX 过程提供了 $\tilde{\sigma}^2$ 标准误差的估计。要获得尺度参数 $\sigma^2$ 的 $\hat{\sigma}^2$，应在 PROC GLIMMIX 语句中包含 NOREML 选项。程序 2.1 的主要结果在输出 2.1 中报告。

## 输出 2.1：程序 2.1 的选定结果

| *** OLS Results -- Gains in Weight Data *** |
|---|
| The GLIMMIX Procedure | |
| Parameter Estimates | |
| Effect | Estimate | Standard Error | DF | t Value | Pr > [t] |
| Intercept | 54.9502 | 31.9768 | 13 | 1.72 | 0.1094 |
| Initial_Weight | 1.0641 | 0.5259 | 13 | 2.02 | 0.0641 |
| Scale | 371.91 | 145.88 | . | . | . |

| *** MLE Results -- Gains in Weight Data *** |
|---|
| The GLIMMIX Procedure | |
| Parameter Estimates | |
| Effect | Estimate | Standard Error | DF | t Value | Pr > [t] |
| Intercept | 54.9502 | 29.7687 | 13 | 1.85 | 0.0878 |
| Initial_Weight | 1.0641 | 0.4895 | 13 | 2.17 | 0.0488 |
| Scale | 322.33 | 117.70 | . | . | . |

如预期，两方法下的 beta 估计值相同：$\hat{\beta}_1 = 1.0641$。$\sigma^2$ 的 OLS 估计量为 $\hat{\sigma}^2 = 371.91$，而 MLE $\hat{\sigma}^2 = 322.33$。注意 $\hat{\sigma}^2 = \frac{15-2}{15}\hat{\sigma}^2$。在 MLE 方法下，检验斜率显著性的 t 统计量为 2.02。这可视为在零假设真实斜率为零下自由度为 13 的 t 分布的 realization。P 值为 0.0641。该结果在 5% 水平上不显著。另一方面，MLE 方法给出 t 值 2.17，P 值为 0.0488。有人可能会得出该结果在 5% 水平上显著的结论。此示例说明了在某些情况下 OLS 和 MLE 估计可能会产生不同的推断——如果严格执行 5% 水平。这里，如果有足够证据相信误差分布为正态，使用 MLE 方法是有用的。PROC GLIMMIX 语句中的 `plots=residuals` 选项生成了图 2.1 所示的诊断图。上图中，Residual Predictor 对应于 $\hat{\epsilon}_i$，相对于 $y_i$。这些图表明线性回归拟合是充分的，正态性假设是合理的。我们可以据此进行基于 MLE 的推断。

