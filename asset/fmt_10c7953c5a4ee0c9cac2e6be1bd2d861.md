
### 4.5.3 `margins`, `dydx(varlist)` 命令

可以使用 `margins`, `dydx(varlist)` 命令获取 MES，其中 `varlist` 是变量列表。`margins`, `dydx(*)` 命令计算所有解释变量的 MES。与基本的 `margins` 命令（见 4.4.2 节）一样，可以在某些或所有解释变量的指定值（`at()`）或所有解释变量的平均值（`atmeans`）处进行评估。默认是在变量的样本值处估计。`margins, dydx()` 命令取代了 Stata 的 `mfx` 命令和社区分发的 `mageeff` 命令。

因此，如果对跨样本的平均响应感兴趣，可以使用简单命令 `margins`, `dydx(*)` 计算 AME。

相反，如果感兴趣的是样本中平均个体的响应，则使用命令 `margins`, `dydx()` `atmeans` 计算 MEM。

默认，使用微积分方法计算所有变量的 MES，但被识别为因子指示变量的变量除外，这些变量使用有限差分法。`continuous` 选项则改为对因子指示变量使用微积分方法。

估计 MES 的默认标准误将回归变量视为固定的。如果需要总体 ME 且在计算 ME 时使用了回归变量的样本值，则 `vce(unconditional)` 选项额外通过采样控制回归变量的变化；见第 13.7.9 节。

如果需要总体 AMES 且提供了总体 margins，则需要计算加权边际。如果在之前的估计命令中使用了权重，则会自动给出加权 ME。如果之前的估计命令没有使用权重（微计量经济学中常见），但需要加权 ME，则随后需要向 `margins, dydx()` 命令添加权重。

### 4.5.4 平均边际效应

如果解释变量是非线性进入（例如二次项或交互项），原始估计命令需要使用因子变量算子引入这些变量。为了完整性，我们使用因子变量算子定义原始 OLS 回归中的所有变量。

以下示例在与上一节相同的回归模型中计算所有回归变量的 AMES。

+ 使用用于定义模型的因子变量计算 AMES
``` 
qui regress totexp 1.suppins 1.phylim 1.actlim c.totochr c.age##c.age 1.female##c, vce(robust) noheader
* margins, dydx(*) novflabel
```
Average marginal effects  Number of obs = 3,064
Model VCE: Robust
Expression: Linear prediction, predict()
d/dx write: 1.suppins 1.phylim 1.actlim totochr 1.female income

| | Delta-method | | | | [95% conf. interval] |
|---|---|---|---|---|---|---|
| | dy/dx | std. err. | t | P|t| | | |
| 1.suppins | 854.581 | 413.6253 | 2.07 | 0.039 | 43.56894 | 1665.593 |
| 1.phylim | 2432.789 | 536.4219 | 4.54 | 0.000 | 138.101 | 3484.573 |
| 1.actlim | 3779.804 | 690.7463 | 5.47 | 0.000 | 2425.429 | 5134.178 |
| totochr | 1921.016 | 180.5999 | 10.64 | 0.000 | 1556.906 | 2275.125 |
| age | -59.8676 | 39.07924 | -1.53 | 0.126 | -136.492 | 16765.258 |
| 1.female | -1226.86 | 415.9167 | -2.95 | 0.003 | -2042.365 | -411.357 |
| income | 11.03041 | 8.42507 | 1.31 | 0.191 | -5.48931 | 27.550

注意：因子水平的 dy/dx 是离散变化。得到的 AMES 与使用 `margins, dydx(*)` 得到的相同。除了简单之外，`margins, dydx(*)` 的优势在于为 AMES 有效的标准误。对于因子指示变量，`margins, dydx(*)` 使用有限差分法。有限差分可以通过 contrast 等效计算。事实上，在上一节中，`contrast (ci)` 计算出的差异为 -1226.86，标准误为 415.9167。`margins, contrast` 允许变量组合，而 `dydx(*)` 仅允许每个变量的独立变化。如果使用 `margins, dydx(*)` 命令会怎样？下面的示例演示了这一点，其中我们需要为回归变量 `age2` 和交互项 `female × income` 生成变量。

+ 如果存在非线性，可能错误地计算平均 ME
``` 
* generate agesq=age2
* generate femybinc=income
* qui regress totexp 1.suppins actin tochr agesq female femybinc, vce(robust)
* margins, dydx(*)
```
Average marginal effects
Number of obs = 3,064
Model VCE: Robust
Expression: Linear prediction, predict(
supplins actin tochr agesq female femybinc

| Delta-method |
| dy/dx | std.err. | t | P|t| | [95% conf. interval] |
|---|---|---|---|---|
| suppins | 854.581 | 413.623 | 2.07 | 0.039 | 43.56894 1665.593 |
| phylim | 2432.789 | 536.421 | 4.54 | 0.000 | 138.101 3484.573 |
| actlin | 3779.804 | 690.743 | 5.47 | 0.000 | 2425.429 5134.178 |
| tochr | 1921.016 | 180.599 | 10.64 | 0.000 | 1566.906 2275.125 |
| age | 1342.275 | 763.421 | 1.76 | 0.079 | -154.5957 2839.146 |
| agesq | -9.45201 | 5.04187 | -1.87 | 0.061 | -19.3745 433.42 |
| female | -1573.508 | 573.318 | -2.74 | 0.000 | -2697.638 -449.3781 |
| income | 2.090179 | 11.27985 | 0.19 | 0.853 | -20.0269 24.20705 |
| femybinc | 15.42391 | 15.81709 | 0.98 | 0.330 | -15.58931 46.3713 |

底层的 OLS 估计被隐藏了，但与之前相同。现在 `age`、`female` 和 `income` 的 AMES 标记方式不同，且回归变量 `agesq` 和 `femybinc` 有额外的 AMES。这是错误的方法。例如，`age` 的 AME 计算时假设 `agesq` 没有变化，尽管 `age` 已经发生了变化。

同时，没有通过二次项或交互项非线性出现的前四个变量的 AMES 保持不变。分类回归变量 `suppins`、`phylum` 和 `actlim` 的这种等性是线性模型的特殊属性，因为有限差分和微积分方法提供了相同的 ME。`logit` 模型等非线性模型会产生不同的 MES。

### 4.5.5 平均值处的边际效应

ME 在概念上不同于 AME，因为通常情况下平均个体的 ME 不等于每个个体 MES 的平均值。

在纯线性模型中，两者相等相等。在这个特定的示例中，由于指定的特定非线性形式，它们也相等。考虑一个具有二次项和交互项的模型：$E(y|x) = \beta_1 + \beta_2x + \beta_3x^2 + \beta_4z + \beta_5z^2 + \beta_6xz$。那么 ME $x = \beta_2 + 2\beta_3\bar{x} + \beta_6\bar{z}$。因此 AME $x = (1/N)\sum_{i=1}^N \beta_2 + 2\beta_3x_i + \beta_6z_i = \beta_2 + 2\beta_3\bar{x} + \hat{\beta}_6\bar{z}$。但最后等于 MEz。同样，AMEz = MESz。

### 4.5.6 代表值处的边际效应

以下示例计算了当所有变量被设置为特定值时（对于一位 70 岁、有补充保险、身体和活动限制、两种慢性疾病且年收入为 20,000 美元的女性），每个变量的 MER。

* 使用因子变量计算的 MER
``` 
qui regress totexp 1.suppins 1.phlym 1.actlim 1.ctochr 1.age##c.age
> 1.female##c.income, vce(robust) noheader

margins, dydx*(at(suppins=1 phlym=1 actlim=1 totchr=2 age=70 female=1 income=20)) noxlabel
```
条件边际效应 观测值 = 3,064
模型 VCE: Robust
表达式: 预测, predict(
dy/dx wrt: 1.suppins 1.phlym 1.actlim tochchr 1.female income

+   在此时: suppins = 1
phlym = 1
actlim = 1
tochr = 2
age = 70
female = 1
income = 20

| dy/dx | 标准误. | t | P>t| | [95% 置信区间] |
|---|---|---|---|---|---|
| 1.suppins | 854.581 | 413.623 | 2.07 | 0.039 | 43.5694 | 1665.593 |
| 1.phlym | 2432.789 | 536.421 | 4.54 | 0.000 | 1381.004 | 3484.573 |
| 1.actlim | 3779.804 | 690.743 | 5.47 | 0.000 | 2425.429 | 5134.178 |
| 1.tochr | 1921.016 | 180.599 | 10.64 | 0.000 | 1566.906 | 2275.125 |
| age | 18.99368 | 67.3056 | 0.28 | 0.778 | -112.971 | 150.9615 |
| 1.female | -1265.03 | 421.603 | -3.00 | 0.003 | -2091.685 | -438.3746 |
| income | 17.5149 | 11.63454 | 1.51 | 0.132 | -5928.229 | 40.32641 |

注：因子水平的 dy/dx 是相对于基准水平的离散变化。

以交互形式进入的 `age`、`female` 和 `income` 变量的 MERS 与呈现的 AMES 不同。对于前四个没有通过二次项或交互项表现出非线性特性的变量，其 MES 等于 AMES。

更一般地说，对于 `logit` 等其他估计命令，MERS 将与该回归中所有变量的 AMES 不同。

## 4.5. 弹性

前面的 MES 估计了当解释变量变化时条件均值的变化。这些 MES 使用的是水平变化。在某些情况下，估计收入变化 1% 导致医疗支出百分比变化的比例或百分比变化的弹性可能会提供更多信息。

弹性和半弹性可以使用 `margins` 命令的 `eyex()`、`dyex()` 和 `eydex()` 选项计算。同样，这些可以在回归变量指定的指定处或每个观测值的样本值处计算，然后取平均值。下文所示，在回归变量的指定值处评估弹性和半弹性更好。

$y$ 对 $x$ 的弹性为 $\partial y/\partial x \times (x/y)$。由于弹性可以重写为 $[\partial y/\partial y]/(\partial x/\partial x)$，它被解释为 $x$ 的比例变化导致 $y$ 的比例变化，或者等价于 $x$ 变化 1% 引起 $y$ 的百分比变化。要计算弹性，我们使用 `margins` 命令的 `eyex()` 选项。

设 $x_i^*$ 表示第 $i$ 个观测值的值。例如，如果所有变量都在样本均值处评估，则 $x_i^* = \bar{x}$；而如果所有变量都在其样本值处评估，则 $x_i^* = x_i$。那么，使用微积分方法，我们看到 `margins` 命令的 `eyex()` 选项计算 $x_j$ 对变量 $x_j$ 的弹性为：

> $$\hat{\epsilon}_j = \frac{1}{N} \sum_{i=1}^N \frac{\partial \hat{y}_i}{\partial x_{ij}} |_{x_i^*} \times \frac{x_{ij}^*}{\hat{y}_i}$$

其中 $\hat{y}_i = \hat{E}(y_i|\mathbf{x}_i=\mathbf{x}^*)$。

以下示例计算了 `totex` 对变量 `income` 的样本平均弹性：

* 关于收入的样本平均弹性
``` 
margins, eyex(income)
```
平均边际效应 观测值 = 3,064
模型 VCE: Robust
表达式: 预测, predict()
ey/ex wrt: income

| | Delta 方法 | [95% 置信区间] |
|---|---|---|
| ey/ex | 标准误. | t | P>t| |
| income | -.0474743 | 1.56076 | -0.997 | -26.6362 | 26.541 |

平均而言，收入变化 1% 医疗支出减少 .047%。该估计值标准误很大，且极不显著。以下代码手动计算相同的弹性。

* 关于收入的样本平均弹性手动计算
``` 
* predict yhat (假设拟合值)
* generate income = (_b[income]+_b[female]) * income / yhat
* sum income
```
| 变量 | 观测值 | 均值 | 标准差 | 最小值 | 最大值 |
|---|---|---|---|---|
| income | 3064 | -.04747 | 3.83905 | -199.9224 | 3.52857 |

再次，平均弹性为 -.04747。但注意波动很大，范围从不合理的 -199.9224 到不合理的 3.529。这很可能是由于 $\hat{y}_i$ 取值接近零。因此，在回归变量的指定值处（无论是代表值还是均值处）计算弹性更好。例如：

* 在代表值处的弹性
``` 
* margins, eyex(income) at(suppins=1 phlym=1 actlim=1 totchr=2 age=70 female=1 income=20)
```
条件边际效应 观测值 = 3,064
模型 VCE: Robust
表达式: 预测, predict()
ey/ex wrt: income
在此时: suppins = 1
phylym = 1
actlim = 2
totchr = 2
age = 70
female = 1
income = 20
```| ey/ex | 标准误. | P>t| | [95% 置信区间] |

|---|---|---|---|

| income | .0294402 | .0197600 | 1.49 | -.0093641, .06824 |

在所有变量指定值处，收入增加 1% 医疗支出增加 .0294%。该估计比之前的平均弹性精确得多，但在 0.05 水平上仍不显著。对于分类变量，弹性没有意义，例如，考虑性别变化 1% 的影响没有意义。因此，因子变量不提供 `eyex()` 选项。

### 4.5.8 半弹性

对于像 `female` 或 `actlim` 这样的指示变量，当指示变量发生单位变化时，考虑医疗支出的比例变化更有意义。这种半弹性可以使用 `eydx()` 选项获得。例如，在变量的指定值处进行操作：

* 半弹性：相对于 x 单位单位变化的 $y$ 比例变化
``` 
margins, eydx(*) at suppins=1 phylim=1 actlm=1 totchr=2 age=70 female=1 income=20label
```
条件边际效应 观测值 = 3,064

模型 VCE: Robust

Expr: 预测, predict(

ey/dx wrt: 1.suppins 1.phylum 1.actlm totchr age 1.female income

At: suppins = 1

phylym = 1

actlm = 2

tochr = 2

nage = 70

female = 1

income = 20

| Delta 方法 |

| ey/dx | 标准误. | t | P>t| | [95% 置信区间] |

|---|---|---|---|---|---|

| 1.suppins | .074535 | .036082 | 2.07 | 0.039 | .003794 | .145206 |

| 1.phylum | .228452 | .056154 | 4.15 | 0.000 | .120582 | .336102 |

| 1.actlm | .382257 | .069224 | 5.52 | 0.000 | .246284 | .517989 |

| totchr | .161458 | .018642 | 8.66 | 0.000 | .124024 | .198001 |
