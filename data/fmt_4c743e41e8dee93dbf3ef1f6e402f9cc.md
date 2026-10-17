
### 6.1
给出了 OLS 和 FGLS 估计量的默认、异方差稳健和聚类稳健 VCE 的公式。FGLS 估计量的异方差稳健 VCE 要求 $\hat{\Omega}$ 为对角且 $N \to \infty$。FGLS 估计量的聚类稳健 VCE 要求 $\hat{\Omega} = \text{Diag}(\hat{\Omega}_g)$ 为块对角且 $G \to \infty$。

**表 6.1.** OLS 和 FGLS 估计量及其估计方差

| 估计量 | 估计量定义及估计的渐近方差 |
| :--- | :--- |
| OLS | $\hat{\beta} = (\mathbf{X}'\mathbf{X})^{-1}\mathbf{X}'\mathbf{y}$<br>$hat{V}_{\text{default}}(\hat{\beta}) = s^2(\mathbf{X}'\mathbf{X})^{-1}$<br>$hat{V}_{\text{het}}(\hat{\beta}) = (\mathbf{X}'\mathbf{X})^{-1}(b \times \sum_i \hat{u}_i^2\mathbf{x}_i\mathbf{x}_i')(\mathbf{X}'\mathbf{X})^{-1}$<br>$hat{V}_{\text{cluster}}(\hat{\beta}) = (\mathbf{X}'\mathbf{X})^{-1}(c \times \sum_g \mathbf{X}'_g\hat{\Omega}_g\mathbf{X}_g)(\mathbf{X}'\mathbf{X})^{-1}$ |
| FGLS | $\hat{\beta} = (\mathbf{X}'\hat{\Omega}\mathbf{X})^{-1}\mathbf{X}'\mathbf{y}$<br>$hat{V}_{\text{default}}(\hat{\beta}) = (\mathbf{X}'\hat{\Omega}\mathbf{X})^{-1}$<br>$hat{V}_{\text{het}}(\hat{\beta}) = (\mathbf{X}'\hat{\Omega}\mathbf{X})^{-1}(b \times \sum_i \hat{u}_i^2\mathbf{x}_i\mathbf{x}_i'/\hat{\Omega}_{gg})(\mathbf{X}'\hat{\Omega}\mathbf{X})^{-1}$<br>$hat{V}_{\text{cluster}}(\hat{\beta}) = (\mathbf{X}'\hat{\Omega}\mathbf{X})^{-1}(c \times \sum_g \mathbf{X}'_g\hat{\Omega}_g\hat{\mathbf{u}}_g\hat{\mathbf{u}}'_g\mathbf{X}_g)(\mathbf{X}'\hat{\Omega}\mathbf{X})^{-1}$ |

注：FGLS 的聚类稳健估计假设 $\hat{\Omega} = \text{Diag}(\Omega_g)$，其中 $g = 1, \dots, G$ 定义了聚类。自由度修正为 $b = N/(N-K)/\{G/(G-1\}$，其中 $K$ 是回归参数的数量，$G$ 是聚类的数量。$\hat{\Omega}_{gg}$ 表示 $\Omega_g$ 中的第 $g$ 个对角元素。

考虑聚类误差的情况。给定 $y = \mathbf{X}\beta + \mathbf{u}$， OLS 估计量可以表示为 $\hat{\beta} = \beta + (\mathbf{X}'\mathbf{X})^{-1}\mathbf{X}'\mathbf{u}$。因此，在给定 $\mathbf{E}(\mathbf{u}\mathbf{u}') = \mathbf{0}$ 时，OLS 估计量的渐近方差为 $(\mathbf{X}'\mathbf{X})^{-1}\mathbf{E}(\mathbf{u}\mathbf{u}')(\mathbf{X}'\mathbf{X})^{-1}$。对于第 $g$ 个聚类 $\mathbf{y}_g = \mathbf{X}_g\beta + \mathbf{u}_g$，给定 $\mathbf{E}(\mathbf{u}_g\mathbf{u}'_g) \dots$，其渐近方差为 $(\mathbf{X}'\mathbf{X})^{-1}\dots$

$y_{ji} = \mathbf{x}'_{ji}\beta_j + u_{ji}, j = 1,\dotsdots,m$，其中误差 $u_{ji}$ 在给定 $i$ 的情况下对于 $j$ 相关，但在 $i$ 上不相关。那么广义最小二法（GLS）估计是指对所有 $m$ 个回归进行有效的联合估计。三阶段最小二法估计器是方程组情况的扩展。

## 6.3 异方差数据的建模

异方差误差在微观计量经济学中无处不在。标准回归模型中同方差假设的失效会导致普通最小二乘法（OLS）估计量是不有效的，尽管它仍然是一个一致的估计量。对于异方差误差，有两种主流方法。

第一种方法在第 `[3.4.5/]` 节中介绍，是在不对异方差的函数形式做假设的情况下，获得回归系数标准误的稳健估计。在这种选项下，对于那些只想报告正确标准误、$t$ 统计量和 $p$ 值的研究者来说，异方差的形式并不重要。这种方法在 Stata 中很容易实现，使用 `vce(robust)` 选项，并且是目前经济学研究应用中最常用的方法。

第二种方法试图对异方差进行建模并获得更有效的 FGLS，从而对参数和边际效应进行更精确的估计以及对条件均值进行更的预测。在实践中，这种效率的提高通常很小，通常使用 OLS。

与 FGLS 的其他标准设置不同，给定异方差误差的情况下，没有直接的 Stata 命令用于 FGLS 估计。然而，手动获得 FGLS 估计量是非常简单的，如下所示。

### 6.3.1 模拟数据集

我们使用一个模拟数据集，其中 $y$ 的条件均值取决于回归变量 $x_2$ 和 $x_3$，而条件方差仅取决于 $x_2$。具体的数据生成过程（DGP）为：

```
$y = 1 + 1 \times x_2 + 1 \times x_3 + u; \quad x_2, x_3 \sim N(0, 25)$
$u = \sqrt{\exp(-1 + 0.2 \times x_2)} \times \varepsilon; \quad \varepsilon \sim N(0, 25)$
```

然后误差 $u$ 是异方差的，其条件方差为 25 * exp(-1 + 0.2 * x2)，根据 $x_2$ 的取值随观测值变化。

我们从 DGP 生成生成包含 500 个样本的样本：

* 异方差示例的生成数据

```
set seed 10101
qui set obs 500
generate double x2 = 5*normal(0)
generate double x3 = 5*normal(0)
generate double e = 5*normal(0)
generate double u = sqrt(exp(-1+0.2*x2))*e
generate double y = 1 + 1*x2 + 1*x3 + u
summarize
```

| 变量 | 观测值 | 平均值 | 标准差 | 最小值 | 最大值 |
|---|---|---|---|---|---|
| x2 | 500 | -.0117399 | 5.073625 | -16.30832 | 15.46858 |
| x3 | 500 | .0534507 | 5.061389 | -20.95962 | 12.92513 |
| e | 500 | .2355246 | 5.131809 | -15.90812 | 12.4746 |
| u | 500 | .1644912 | 4.234811 | -22.13982 | 24.04547 |
| y | 500 | 1.206202 | 8.475936 | -24.92206 | 41.67478 |

生成的独立同分布（i.i.d.）正态变量 $x_2$、$x_3$ 以及在较小程度上的 $e$ 的其均值符合预期的 0，标准差为 5。

### 6.3.2 OLS 估计

带有默认标准误的 OLS 回归产生

* 带有默认标准误的 OLS 回归

```
regress y x2 x3
```

| 来源 | df | MS | 观测值 = | |
||---|---|---|---|
| 模型 | 26914.9701 | 2 | 13457.485 | F(2, 497) = 748.65 |
| 残差 | | 8933.93 | | Prob > F = 0.0000 |
| | | | | R 方 = 0.75 |
| 总计 | | 35848.026 | 499 | 均方误差 = 4.2398 |
| 变量 | 系数 | 标准误 | t | P | [95% 置信区间] |
|---|---|---|---|---|
| x2 | 1.033346 | .037413 | 27.62 | 0.000 | [0.9598 1.1068] |
| x3 | 0.991959 | .037508 | 26.45 | 0.000 | [0.9182 1.0656] |
| 常数项 | 1.165312 | .189619 | 6.15 | 0.000 | [0.7925 1.5378] |

生成的独立同分布（i.i.d.）正态变量 $x_2$、$x_3$ 以及在较小程度上的 $e$ 的均值约为 0，标准差为 5，符合预期。

与 FGLS 的其他标准设置不同，给定异方差误差的情况下，没有直接的 Stata 命令用于 FGLS 估计。然而，手动获得 FGLS 估计量是非常简单的，正如我们现在演示的样。

### 6.3.3 检测异方差

我们使用模拟数据集，其中 $y$ 的条件均值取决于回归变量 $x_2$ 和 $x_3$，而条件方差仅取决于 $x_2$。具体的数据生成过程（DGP）为：

然而，请使用误差服从正态分布的统计检验版本。为了将此假设放宽为独立同同分布的误差，我们需要使用 `iid` 选项（见第 3.7.4 节）并进行单独检验。这样做会导致检验统计量（未报告）的值比上述获得的值低，且无异方差的零假设在 $x_2$ 上被拒绝，而在 $x_3$ 上未被拒绝。

为了获得效率上的潜在提升，我们可以使用第 6.2.2 节介绍的两步 FGLS 估计法来估计模型参数。对于异方差，这很容易：从公式 (6.2) 出发，我们需要 1) 估计 $\sigma^2_i$ 以及 2) 对 $x_i/\sigma_i$ 进行 $y_i/\sigma_i$ 进行 OLS 回归。

在第一步，我们通过 OLS 估计线性回归，保存残差 $u = y - x'\beta_{OLS}$，通过将 $u^2$ 对 $\sigma^2(z_i, \gamma)$ 回归来估计异方差函数 $\sigma^2(z_i, \gamma)$，并获得预测值 $\sigma^2(z_i, \gamma)$。这里的检验表明，异方差函数应仅包含 $x_2$。我们指定异方差函数 $\sigma^2(z) = \exp(\gamma_1 + \gamma_2x_2)$，因为取指数可以确保方差为正。这是一个非线性模型，需要通过非线性最小二乘法进行估计。我们使用 `nl` 命令，该命令在第 13.3.6 节中有解释。

FGLS 的第一步产生：

* FGLS: 第一步获取异方差函数的估计

```
drop uhat
qui regress y2 x3 // 获取 bols
predict uhat, resid // 获取残差平方
generate double uhatsq = uhat^2
nl (uhatsq = exp(xb:x2}+{b0}), nolog // 对 uhatsq 对 exp(z'a) 进行非线性最小二乘法
```

| Source | SS | df | Number of obs |
| :--- | :--- | :--- | :--- |
| Model | 890038.92 | 2 | 440519.48 | R-squared = 0.5975 |
| Residual | 599505.8 | 498 | 1203.8333 | Adj R-squared = 0.5969 |
| | | | Root MSE = 34.6963 |
| Total | 149854.8 | 500 | 2979.0653 | Res. dev. = 4963.568 |
| Coefficient | Std. err. | t | P|t| | [95% conf. interval] |
| :--- | :--- | :--- | :--- | :--- |
| /xb,x2 | 0.3002613 | 0.012050 | 24.951 | 0.000 | .2765743 - .3239482 |
| /b0 | 1.586178 | 0.1561775 | 10.16 | 0.000 | 1.27933 - 1.893026 |

```
predict double varu, yhat // 获取 sigmath^2
```

注意，$x_2$ 解释了很大一部分异方差（$R^2 = 0.60$）且在统计上高度显著。对于我们的数据数据生成过程（DGP），

$\sigma^2(z) = 25 \exp(-1+0.2x_2) = \exp(\ln 25-1+0.2x_2) = \exp(2.22+0.2x_2)$，估计值为 1.59 和 0.30。

在第二步，预测值 $\hat{\sigma}^2(z)$ 定义了用于获取 FGLS 估计量的权重。具体而言，我们将 $y_i/\hat{\sigma}_i$ 对 $x_i/\hat{\sigma}_i$ 进行回归，其中 $\hat{\sigma}_i^2=\exp(\hat{\gamma}_1+\hat{\gamma}_2x_{2i})$。这种加权可以通过在估计中使用权重自动完成。如果权重为 $w_i$，则 OLS 回归是对 $\sqrt{w_i}y_i$ 对 $\sqrt{w_i}x_i$ 进行。这里希望权重为 $1/\hat{\sigma}^2$，即 $1/varu$。

* FGLS: 第二步获取异方差函数的估计

```
regress y x2 x3 [weight=1/var]
(sum of w= 338.057522101863)
```

| Source | SS | df | MS | Number of obs = |
| :--- | :--- | :--- | :--- | :--- |
| Model | 17266.210 | 2 | 8633.10525 | F(2, 497) = 2530.65 |
| Residual | 1695.47363 | 497 | 3.41411576 | Prob > F = 0.0000 |
| | | | | R-squared = 0.9106 |
| Total | 18961.6841 | 499 | 37.999367 | Adj R-squared = 0.9102 |
| | | | | Root MSE = 1.847 |
| Coefficient | Std. err. | t | P|t| | [95% conf. interval] |
| :--- | :--- | :--- | :--- | :--- |
| x2 | 1.037914 | .017689 | 60.450 | 0.000 | 1.004811 - 1.071644 |
| x3 | 1.012177 | .017454 | 58.000 | 0.000 | 0.977808 - 1.046464 |
| _cons | 1.348954 | .1548488 | 8.710 | 0.000 | 1.044715 - 1.653165 |

$x_2$ 解释了大量的异方差（$R^2 = 0.60$）且在统计上非常显著。对于我们的 DGP，$\sigma^2(z) = 25 \exp(-1+0.2x_2) = \exp(\ln 25-1+0.2x_2) = \exp(2.22+0.2x_2)$，估计值为 1.59 和 0.30。

在第二步，预测值 $\hat{\sigma}^2(z)$ 定义了用于获取 FGLS 估计量的权重。具体而言，我们将 $y_i/\hat{\sigma}_i$ 对 $x_i/\hat{\sigma}_i$ 进行回归，其中 $\hat{\sigma}_i^2=\exp(\hat{\gamma}_1+\hat{\gamma}_2x_{2i})$。这种加权可以通过在估计中使用权重自动完成。如果权重为 $w_i$，则 OLS 回归是对 $\sqrt{w_i}y_i$ 对 $\sqrt{w_i}x_i$ 进行。这里我们希望权重为 $1/\hat{\sigma}^2$，即 $1/varu$。

* FGLS: 第二步获取异方差函数的估计

```
regress y x2 x3 [weight=1/var]
(sum of w= 338.057522101863)
```

| Source | SS | df | MS | Number of obs = |
| :--- | :--- | :--- | :--- | :--- |
| Model | 17266.210 | 2 | 8633.10525 | F(2, 497) = 2530.65 |
| Residual | 1695.47363 | 497 | 3.41411576 | Prob > F = 0.0000 |
| | | | | R-squared = 0.9106 |
| Total | 18961.6841 | 499 | 37.999367 | Adj R-squared = 0.9102 |
| | | | | Root MSE = 1.847 |
