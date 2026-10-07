
AIC 和 BIC 越小越好，因为似然值越高越好。数值 `2K` 和 `K ln N` 是对模型大小的惩罚。

如果模型实际上是嵌套的，则可以使用等于 `$\Delta(2 \ln L)$` 的 LR 检验统计量。如果 `$\Delta(2 \ln L)$` 增加了 `$\chi^2_{0.05}(\Delta K)$`，则在 0.05 的水平下倾向于较大的模型。相比之下，如果 `$\Delta(2 \ln L)$` 增加了 `2AIC`，则 AIC 倾向于较大的模型，而这是一个较小的值 [例如，如果 AIC = 1，`2 < $\chi^2_{0.05}(1) = 3.84$`]。AIC 的惩罚太小了。BIC 提供了更大的尺寸惩罚，通常更好，特别是当需要较小模型时。

这些数值可以使用 `estat` 命令轻松显示。对于包含截距在内的五个回归变量的松回归，具有：

- 报告信息准则
- `estat ic`

赤池信息准则和贝叶斯信息准则

| Model | N | ll1(null) | ll1(model) | df | AIC | BIC |
|---|---|---|---|---|---|---|
| | 4412 | -22929.9 | -18503.55 | 5 | 37017.1 | 37049.6 |

注：BIC 使用 N = 观测值。参见 [R] BIC note。

信息准则和 LR 检验需要密度函数的正确设定，因此在进行负二项估计时，应在 `nbreg` 命令之后使用它们，因为泊松密度对于这些数据是不适当的。

可以使用 Vuong (1989) 的 LR 检验对两个非嵌套的基于似然的模型进行对比检验。关于 Vuong 检验的通用讨论见 Greene (2018, 751) 以及 Cameron and Trivedi (2005, 280–283)。Shi (2015) 的后续研究表明，Vuong 检验可能会出现尺寸偏误，并提出了一种更好的检验。期刊网站包含了实现这种更好检验的 Stata 代码。

### 13.8.3 残差

残差分析是一个非常有用的诊断工具，如第 3.6 节和 6.3 节中的线性模型所示。

在非线性模型中，可以计算不同的残差。残差的使用和计算方法差随模型和估计量而异。一个自然的起点是原始残差，`$y_i - \hat{y}_i$`。在非线性模型中，这可能是异方差的，导致使用 Pearson森 残差 `$(y_i - \hat{y}_i)/\hat{\sigma}_i$`，其中 `$\hat{\sigma}_i^2$` 是 `$Var(y_i \mid x_i)$` 的估计值。Pearson 统计量是平方 Pearson 残差之和。

对于 13.3.7 中定义的 GLM，通常使用离差残差 `$d_i = sign(y_i - \hat{\mu}_i)\sqrt{2[l(y_i) - l(\hat{\mu}_i)]}$`，其中 `$l(y)$` 是在 `$\mu = y$` 处的对数密度，`$l(\hat{\mu})$` 是在 `$\mu = \hat{\mu}$` 处的对数密度。对于同方差正态误差，这简化为原始残差。离差统计量是平方离差残差之和，是残差和的 GLM推广。

对于用 `glm` 命令拟合的泊松模型，`predict` 后估计命令的不同选项产生不同的残差，`mu` 选项给出预测的条件均值。我们有：

- `glm` 命令后的各种残差
```
qui glm docvis private chronic female income, family(poisson) vce(robust)
predict mu, mu
generate uraw docvis - mu
predict upearson, peearson
predict udeviance, deviance
predict uanscombe, anscombe
summarize uraw upearson deviance uanscombe
```

| Variable | Obs | Mean | Std.dev. | Min | Max |
|---|---|---|---|---|---|
| uraw | 4,412 | -3.34e-08 | 7.408631 | -13.31806 | 125.3078 |
| upearson | 4,412 | -.0102445 | 3.598716 | -3.519644 | 91.16232 |
| udeviance | 4,412 | -.5619154 | 2.462038 | -4.728247 | 24.78259 |
| uanscombe | 4,412 | -.5995917 | 2.545318 | -5.03055 | |

Pearson 残差是平方 Pearson 残差之和。离差统计量是平方离差残差之和，是残差和的 GLM推广。

对于用 `glm` 命令拟合的泊松模型，`predict` 后估计命令的不同选项产生不同的残差，`mu` 选项给出预测的条件均值。我们有：

- `glm` 命令后的各种残差
```
qui glm docvis private female income, family(poisson) vce(robust)
predict mu, mu
generate uraw docvis - mu
predict upearson, peearson
predict udeviance, deviance
predict uanscombe, anscombe
summarize uraw upearson deviance uanscombe
```

| Variable | Obs | Mean | Std.dev. | Min | Max |
|---|---|---|---|---|---|
| uraw | 4,412 | -3.34e-08 | 7.408631 | -13.31806 | 125.3078 |
| upearson | 4,412 | -.0102445 | 3.598716 | -3.519644 | 91.16232 |
| udeviance | 4,412 | -.5619154 | 2.462038 | -4.728247 | 24.78259 |
| uanscombe | 4,412 | -.5995917 | 2.545318 | -5.03055 | |

* 基于 commune 聚类的类稳健标准误的 Poisson 估计
```
. poisson phervis lnhhexp illness, nolog vce(cluster commune)
```

观测值 = 27,753
Wald chi2(2) = 591.84
Prob > chi2 = 0.0000
Pseudo R2 = 0.1769

Poisson 回归
对数伪似然值 = -26217.797

（标准误已针对 commune 中的 194 个聚类调整）

| | 系数 | 稳健标准误 | z | P>|z| | [95% 置信区间] |
|---|---|---|---|---|---|
| lnhhexp | .0175333 | .047699 | 0.37 | 0.711 | -.075114 | .110806 |
| illness | -.686012 | .028681 | 23.73 | 0.000 | .624389 | .736835 |
| _cons | -1.412108 | .1451221 | -9.73 | 0.000 | -1.696542 | -1.127674 |

控制组内相关性会导致更大的标准误、更小的 t 统计量以及更大的 P 值。从给输出来看，变量 `lnhhexp` 和 `illness` 的默认标准误分别为 0.0135 和 0.0053，而异方差稳健标准误为 0.0268 和 0.0264。

## 广义估计方程

如 13.3.1 节所示，Poisson 拟极大似然估计的一致性仅要求条件均值正确设定；分布不需要是 Poisson 分布。这种稳健性被许多常用模型所共享，包括 logit 和 probit，统计学上统称为 GLMs。

对于聚类数据，GLM 框架被扩展到广义估计方程框架。这在给定组内相关性模型的情况下，为非线性模型提供了可行的最小二乘估计，以获得可能更高效的参数估计。只要存在许多聚类，就可以再次获得聚类稳健标准误估计，以防止组内相关性模型设定不当的影响。

组内相关性的自然模型是等相关模型，即对于同一聚类中的个体 i 和 j，满足 `Cor(Uij, Ujg) = ρ`。该假设也被称为可交换性假设。

可以使用 22.4.4 节详细说明的 `xtgee` 命令进行模型拟合。我们有：

+ 基于 commune 聚类的类稳健标准误的广义估计方程估计
```
xtset commune
xtgee phervis lnhhexp illness nog family(poisson) corr(exchangeable) vce(robust)
```

GEE 人群平均模型
分组变量: commune
族: Poisson
链接: Log
相关性: exchangeable

观测值 = 27,753
组数 = 194
每组观测值: 最小 = 51
平均 = 143.1
最大 = 206

Wald chi2(2) = 515.86
Prob chi2 = 0.0000

尺度参数 = 1（标准误已针对 commune 聚类调整）

| phervis | 系数 | 标准误 | z | P|z| | [95% 置信区间] |
|---|---|---|---|---|---|
| lnhhexp | -.0305985 | .078615 | -3.89 | 0.000 | -.046072, -.0151906 |
| illness | .2697244 | .011886 | 22.69 | 0.000 | .246482, .293202 |
| _cons | .9510729 | .0793079 | 11.99 | 0.000 | .795623, .106513

该非常简单模型的参数估计比使用 `poisson` 命令得到的估计精确得多，且差异显著。这是由于组内相关性的估计值非常高：后估计命令 `estat correlation` 得到 p=0.879。使用 `vce(robust)` 选项会导致报告聚类稳健标准误。在本例中，这种收益是巨大的。

### 9.3 RE 与混合模型

RE 模型允许截距随聚类变化，聚类内观测值的条件密度变为：

```
f(y_{ig}|x_{ig}) = f(α_g + x'_{ig}\beta, \gamma)
```

假设 `$\alpha_g$` 服从正态分布，均值为 0，方差为 `$\sigma_{\alpha}^2$`。在给定聚类特定截距 `$\alpha_g$` 的情况下，聚类内的观测值是独立的。这意味着聚类内所有观测值的联合密度是个体密度的乘积。积分 `$\alpha_g$` 得到：

```
f(y_{1g}, \dots, y_{N_g}|x_{1g}, \dots, x_{N_g}, \beta, \gamma, \sigma_{\alpha}^2)d\alpha_g = \int_{i=1}^{N_g} f(y_{ig}|x_{ig}, \beta, \gamma) \phi(\alpha_g|\sigma^2)d\alpha_g (13.15)
```
