
`drop` `_all`

`use` `residuals`

`bsample`

`merge` `1:1` `_n` `using` `mus212bootstrapdata`

`regress` `docvis` `chronic`

`predict` `xb`

`generate` `ystar = xb + uhat`

`regress` `ystar` `chronic`

```
我们通过使用 `bootstrapresidual` 命令并自助 400 次来检查该程序。

+   * 参数的残差自助
* simulate _b, seed(10101) reps(400) nodots: bootstrapresidual

Command: bootstrapresidual

.summarize

| Variable | Obs | Mean | Std. dev. | Min | Max |
| --- | --- | --- | --- | --- | --- |
| _b_chronic | 400 | 4.802995 | 2.296399 | -.9681436 | 12.29839 |
| _b_cons | 400 | 2.766325 | 1.20739 | -.2407045 | 6.493056 |
```

输出报告了 400 次斜系数估计的平均值（4.803），接近原始样本 OLS 斜系数估计值（未报告，4.694）。自助标准误估计（2.30）接近原始样本 OLS 默认估计，而非 2.39。这是预期的，因为残差自助假设误差是 i.i.d.。。

### 12.8.4 野自助重抽样方案

野自助在 12.6 节中介绍，并使用社区提供的 `boottest` 命令实现。这里我们提供一个没有渐近精化的简单示例。

对于独立观测值的线性回归，野自助适应了更真实的假设，即误差独立但非同分布，允许异方差。它将 $x_i$ 固定在样本值上，并将 $y_i^*$ 替换为 $x_i^*\beta + \hat{u}_i^*$，我们使用 Mammen 权重使得 $\hat{u}_i^* = a_i\hat{u}_i$，其中 $a_i = (1-\sqrt{5})/2 \approx -0.618$ 的概率为 $(1+\sqrt{5})/2 \approx 0.723$，$a_i = 1-(1-\sqrt{5})/2$ 的概率为 $1-(1+\sqrt{5})/2$。如果所有 $N$ 个 $\hat{u}_i$ 值不同，则有 $2^N$ 种可能。

之前的残差程序通过将 `bsample` 替换为代码，从 $\hat{u}_i$ 随机抽取 $\hat{u}_i^*$，然后形成 $y_i^* = x_i\beta + \hat{u}_i^*$ 来适配。

Stata 代码与 12.8.1 节中的相同，但自助程序中的 `bsample` 命令需要被替换为

从 $\hat{u}_i$ 中随机抽取 $\hat{u}_i^*$，然后形成 $y_i^* = \mathbf{x}_i'\hat{\beta} + \hat{u}_i^*$ 的代码。

- *针对 i.i.d. 误差的LSLS 野性自助法*
```stata
use mus212bootstrapdata, clear

program biotwild

version 17

drop _all

use mus212bootstrapdata

regress docsis chronic

predict xb

predict u, resid

gen ustar = -0.618034*u

replace ustar = 1.618034*u if uniform() > 0.723607

gen yster = xb + uster

regress yster chronic
```

我们通过执行 `biotwild` 命令并进行 400 次自助来检查该程序。

- *参数的野性自助法*
```stata
.simulate _b, seed(10101) reps(400) notots: biotwild
```

命令：`biotwild`

汇总

| Variable | Obs | Mean | Std. dev. | Min | Max |
|---|---|---|---|---|---|
| _b_chronic | 400 | 4.779422 | 2.986341 | -2.205521 | 11.53673 |
| _b_cons | 400 | 2.807026 | .957078 | 1.123328 | 5.709338 |

野性自助允许异方差误差，并产生标准误差的自助估计（2.99），该值与原始样本 OLS 异方差稳健估计（未给出）的 3.06 接近。这些标准误差远高于使用残差自助得到的误差，而后者在本例中显然是不合适的，因为计数数据具有内在异方差性。

带有野性自助的百分位数-$t$ 方法为具有异方差误差或聚类误差的线性模型中的 Wald 检验和置信区间提供了渐近改进；参见第 12.6 节。

## 12.8.5 子抽样 (Subsampling)

自助法在某些情况下会失效，例如非平滑估计器。此时，理论上更稳健的重采样方法是子抽样，它抽取比原始样本小得多的样本。Politis、Romano 和 Wolf (1999) 提供了该方法的介绍。

该方法可以使用 `bsample` 命令轻松实现。例如，要执行重采样观测量为原始样本三分分之一的子抽样，将自助对中的 `bsample` 命令替换为 `bsample int(_N/3)`，其中 `int()` 函数向零截断为整数。

然而，我们警告不要使用这种方法，因为在实践中它对所选择的子抽样大小非常敏感。

## 12.9 刀法 (The jackknife)

删除一个刀法 (delete-one jackknife) 是一种重采样方案，它通过顺序删除每个观测值并在每个样本中估计 $\theta$，形成 $N$ 个大小为 $(N - 1)$ 的重样本。

### 12.9.1 刀法方法

令 $\hat{\theta}$ 表示从删除第 $i$ 个观测值的样本中得到的参数估计，$i = 1, \dots, N$，令 $\hat{\theta}$ 为原始样本对 $\theta$ 的估计，$\bar{\theta} = \sum_{i=1}^N \hat{\theta}_i$ 表示 $N$ 个刀法估计的平均值。

刀法有几种用途。$\theta$ 的 bc 刀法估计等于 $N\bar{\theta} - (N-1)\hat{\theta}^* = (1/N)\sum_{i=1}^N\{\hat{\theta} - (N-1)\hat{\theta}_i\}$。$N$ 个伪变量 $\hat{\theta}_i^* = N\bar{\theta} - (N-1)\hat{\theta}_i$ 的方差可用于估计 $\text{Var}(\hat{\theta})$。作为渐近改进的自助 Bca 方法也使用了刀法。

VCE（方方差矩阵）的刀法估计有两种变体。Stata 的默认值为：

```math
$$\widehat{V}_{Jack}(\theta) = \left\{\frac{1}{N(N-1)}\sum_{i=1}^N\(\hat{\theta}_i^* - \bar{\theta}\right)\left(\hat{\theta}_i - \bar{\theta}\right)'\right\}$$
```

而 `mse` 选项给出的是：

```math
$$\widehat{V}_{Jack}(\theta) = \left\{\frac{N-1}{N}\sum_{i=1}^N\left(\hat{\theta}_i - \bar{\theta}\right)\left(\hat{\theta}_i - \bar{\theta}\right)'\right\}$$
```

该方法涉及 $N$ 个重样本，当 $N$ 很大时需要大量的计算。重样本不是随机抽取，因此使用刀法估计 VCE 已在很大程度上被自助法取代了。在最近的研究中，Cattaneo、Jansson 和 Ma (2019) 发现刀法可以减少第一步包含许多协变量的两步估计器中的偏误，并提出基于刀法基础估计的百分位数-$t$ 自助进行后续推断。

### 12.9.2 vce(jackknife) 选项与刀法

对于许多估计命令，可以使用 `vce(jackknife)` 选项来获得刀法估计。例如：

```stata
* 刀法估计

* use mus212bootstrapdata, replace

* poisson docsis chronic
```

| Variable | Obs | Mean | Std. dev. | Min | Max |
|---|---|---|---|---|---|
| _b_chronic | 400 | 4.779422 | 2.986341 | -2.205521 | 11.53673 |
| _b_cons | 400 | 2.807026 | .957078 | 1.123328 | 5.709338 |

野性自助允许异方差误差，并产生标准误差的自助估计（2.99），该值与原始样本 OLS 异方差稳健估计（未给出）的 3.06 接近。这些标准误差远高于使用残差自助得到的误差，而后者显然是不合适的，因为计数数据具有内在异方差性。

带有野性自助的百分位数-$t$ 方法为具有异方差误差或聚类误差的线性模型中的 Wald 检验和置信区间提供了渐近改进；参见第 12.6 节。

## 12.10 附加资源

对于许多目的，`vce(bootstrap)` 选项足够了。对于更高级的分析，可以使用自助前缀和 `bsample` 命令。参考文献 Efron 和 Tibshirani (1993)、Davidson 和 MacKinnon (1997)、Horowitz (2001)、Cameron 和 Trivedi (2005) 以及 Hansen (2022)。关于渐近改进的自助，请参见第 12.6。

## 12.11 练习

1. 使用与 12.3.3 节相同的数据，但保留前 100 个观测值以及 `educ`, `age` 变量。对 `docvis` 进行 回 回归，默认标准误差、稳健标准误差以及基于 100 次自助且种子为 10101的标准误差。

2. 对于练习 1 中的 Poisson 回归，获得以下 95% 置信区间：基于正态的、百分位数的和 BCa 的。这些中哪种最好？

3. 获得估计标准差的自助估计。

4. 继续练习 1 中的回归，获得 $\hat{\beta}_{educ}$ 稳健标准误差的标准差自助估计。

5. 继续练习 1 中的回归，使用百分位数-$t$ 方法对 $H_0: \beta = 0$ 与 $H_a: \beta \neq 0$ 进行 Wald 检验（显著性水平为 0.05），并获得百分位数-$t$ 95% 置信区间。

6. 使用 12.3.3 中的 50 个观测值。使用 `percentile.dta` 中的数据获得变量系数的：1) 自助标准误差；2) 偏误自助估计；3) 基于正态的95% 置信区间；4) 百分位数-$t$ 95% 置信区间。对于后者，使用 `centile` 命令。将你的结果与带有 `vce(bootstrap)` 选项的 Poisson 回归后得到的结果进行比较。

```stata
bootstrap bstar=_b[chromic], reps(999) seed(10101) nodots ///
saving(percentile, replace): poisson docvis chronic

use percentile, clear
```
