
```sas
proc genmod data=yourDataset;
    model cost = arm / dist=normal link=identity;
    output out=c predicted=pred_c;
run;

proc genmod data=yourDataset desc;
    model effectiveness= arm / dist=bin link=identity;
    output out=e predicted=pred_e;
run;
```

```sas
data temp; merge c;
    resid_e = effectiveness - pred_e;
    resid_c = cost - pred_c;
    keep resid_e resid_c;
run;

proc corr data=temp var resid_e resid_c; run;
```

### 程序 15.1 输出

| 参数 | DF | 估计值 | 标准误 | Wald 95% | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 | 1 | 972.479 | 210.9007 | 932.121 | 1013.84 | 2126.50 | <0001 |
| arm | 1 | -805.724 | 279.817 | -1389.44 | -222.008 | 4965.68 | 0.0068 |

$\hat{\Delta}_c = -805.724$; $\hat{V}(\hat{\Delta}_c) = (297.819)^2.$

| 参数 | DF | 估计值 | 标准误 | Wald 95% | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 | 1 | 0.8802 | 0.0125 | 0.8557 | 0.9047 | 4965.68 | <0001 |
| arm | 1 | 0.0507 | 0.0158 | 0.0197 | 0.0817 | 10.26 | 0.0014 |

$\hat{\Delta}_e = 0.0507;$ $\hat{V}(\hat{\Delta}_e) = (0.0158)^2.$

皮逊相关系数，N = 1356

| | resid_e | resid_c |
|---|---|---|

| resid_e | 1.00000 | -0.31306 |
| resid_c | -0.31306 | |

$\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c) = (-0.31306) * (297.819) * (0.0158).$

## 15.5 使用 SAS 分析观察性健康数据

以下 SAS 代码提供了五个所需参数的估计值。输出（未显示）与程序 15.1 的输出相同。

### 程序 15.2 使用伽马分布建模成本

```sas
proc genmod data=yourDataset;
    model cost = arm / dist=gamma link=identity;
    output out=c predicted=pred_c;
run;

proc genmod data=yourDataset desc;
    model effectiveness = arm / dist=bin link=identity;
    output out=e predicted=pred_e;
run;

data temp; merge e c;
    resid_e = effectiveness - pred_e;
    resid_c = cost - pred_c;
    keep resid_e resid_c;
run;

proc corr data=temp; var resid_e resid_c; run;
```

#### 表 15.2 CD 试验的参数估计

| 参数 | 合并 | 正态* | 伽马* |
|---|---|---|---|

| $\hat{\Delta}_e$ | 0.0507 | 0.0507 | 0.0507 |
| $\hat{\Delta}_c$ | -805.72 | -805.72 | -805.72 |
| $\hat{V}(\hat{\Delta}_e)$ | 0.0002506 | 0.0002496 | 0.0002496 |
| $\hat{V}(\hat{\Delta}_c)$ | 88,828 | 88,697 | 65,839 |
| $\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)$ | -1.482 | -1.473 | -1.268 |

* 用于成本的分布

# 第15章 增量净收益 355

**图 15.7** 使用正态分布和伽马分布的 CD 试验的增量净收益及置信区间

![](img/fe9ff008f88baacd415148b0b25dd58c_369_0.png)

**图 15.8** 使用正态分布和伽马分布的 CD 试验的成本效益接受性曲线

![](img/fe9ff008f88baacd415148b0b25dd58c_369_1.png)

## 356 使用 SAS 对观察性健康数据进行分析

对成本使用伽马分布，我们考察了协变量对成本和30天存活率的影响。协变量对30天存活率没有显著影响（$p=0.5843$），但整体效应显著（0.0315），且与治疗组之间存在边际显著的交互作用（0.0630）。最终模型包含了治疗组、$X$以及成本，而30天存活率模型仅包含治疗组，用于提供参数估计。详见程序 15.3。参数估计见表 15.3。由于成本模型中治疗组与 $X$ 之间存在交互作用，$\Delta_{\lambda}$ 及其方差的估计取决于 $X$ 的水平。当 $X=0$ 时，节省的成本更高，且治疗在患者亚组中更具成本效益。增量收益图和 CEAC 见图 15.9 和 15.10。对于 $X=0$，所有 $\lambda$ 值的 CEAC 均超过 0.9；对于 $X=1$，当 $\lambda$ 值大于每节省一个寿命 10,000 美元时，CEAC 超过 0.85。这为 T 的成本效益提供了有力的支持。

在 `http://www.andyllan.com/downloads` 可以获得用于生成 CEAC 和 INB（带置信区间）图表的 Microsoft Excel 工具。所需的唯一输入是五个参数估计、最小值、最大值以及置信水平。

以下代码显示了这些模型。有效性模型将 $\lambda$ 作为唯一的协变量，成本模型包含了组别、$X$ 及其它们的交互作用。

### 程序 15.3 协变量调整

```
proc glm data=yourData
    model cost = arm X*/ dist=gamma link=identity;
    output out=c predicted=pred_c;
run;

proc glm data=yourData desc
    model effectiveness = arm / dist=bin link=identity;
    output out=c predicted=pred_e;
run;

data temp; merge c;
    resid_e = effectiveness - pred_e;
    resid_c = cost - pred_c;
    keep resid_e resid_c;
run;

proc corr data=temp; var resid_e resid_c; run;
```

| 参数 | DF | 估计 | 标准误 | Wald 置信区间 | 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|---|

| 截距 | 1 | 10203.31 | 266.7096 | 9680.51 | 10726.05 | 1463.54 | <.0001 |
| arm | 1 | -1226.95 | 360.0549 | -1932.65 | -521.29 | 11.61 | 0.0007 |
| X | 1 | -1066.06 | 375.9776 | -1802.96 | -329.153 | 8.04 | 0.0046 |
| arm*X | 1 | 949.0657 | 510.5547 | -51.6032 | 1949.735 | 3.46 | 0.063 |

对于 $X=0$：$\hat{A}_{\lambda} =-1226.95$；$\hat{V}(\hat{A}_{\lambda}) = (360.0549)^2$。

## 第15章 增量净收益 357

对于 $X=0: \hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)=(-0.03140)*(360.0549)*(0.0158)$。

$$\hat{\Delta}_e = 0.0507; \hat{V}(\hat{\Delta}_c) = (0.0158).$$

Pearson 相关系数，$N = 1356$

| 参数 | DF | 估计 | 标准误 | Wald 95% 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 arm | 1 | 0.8802 | 0.0125 | 0.8557 | 0.9047 | 4965.68 | <.0001 |
| | | | 0.0158 | 0.0197 | 0.0887 | 10.26 | 0.0014 |
| resid_e | | | | | | |
| resid_c | | | | | | |
| 1.0000 | -0.03140 | | | | | |

对于 $X=1$，$X$ 的值可以反转，得到如下：

| 参数 | DF | 估计 | 标准误 | Wald 95% 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 | 1 | 9137.25 | 265.0003 | 8617.86 | 9656.47 | <.0001 |
| X | 1 | -277.88 | 361.9759 | -329.15 | 10.26 | 0.0014 |
| arm+X | 1 | 1066.05 | 375.9776 | 329.15 | 8.04 | 0.0046 |
| | | | | | | |
| | | -949.06 | 510.5547 | -51.603 | 1949.73 | 3.46 | 0.063 |

对于 $X=0$，$\hat{A}_{\lambda} =-1226.95$；$\hat{V}(\hat{A}_{\lambda}) = (360.0549)^2$。

对于 $X=1$，$X$ 的值可以反转，得到如下：

| 参数 | $X=0$ | $X=1$ |
|---|---|---|

| $\hat{\Delta}_e$ | 0.0507 | 0.0507 |
| $\hat{\Delta}_c$ | -1226.95 | -277.88 |
| $\hat{V}(\hat{\Delta}_e)$ | 0.002496 | 0.002496 |
| $\hat{V}(\hat{\Delta}_c)$ | 0.0158 | 0.0158 |
| $\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)$ | -0.03140 | -0.03140 |

## 358 使用 SAS 对观察性健康数据进行分析

图 15.9 使用正态分布和伽马分布的 CD 试验的增量收益（INB（$）

![](img/fe9ff008f88baacd415148b0b25dd58c_369_0.png)

图 15.10 使用正态分布和伽马分布的 CD 试验的成本效益接受性曲线

![](img/fe9ff008f88baacd415148b0b25dd58c_369_1.png)

## 15.5 观察性研究

虽然许多成本效益分析是在随机试验中进行的，但这些方法也适用于观察性研究，尽管存在由于缺乏随机分配可能带来的偏差。通常，基于观察性研究数据的分析需要调整偏差。通用的方法包括：倾向评分和回归分析。如果数据量足够，倾向匹配是一个可能的选项。如果倾向匹配来自 RCT，则可以进行分析。倾向分层也是一个选项。对于倾向分层数据，需要进行回归分析，将有效性和成本对治疗指示变量以及倾向分层的虚拟指示变量（分层数减一）进行回归。对于非截断数据，分析师可以使用 `PROC GENMOD` 执行回归，如15.4节所示。这样不需要创建虚拟指示变量。对于截断数据，参考 Willan、Lin 和 Manca (2005) 使用的方法。

## 15.6 讨论

本文概述了使用增量净收益比较两组的成本效益。分析师根据支付意愿（WTP）估计 INB 并确定其相应的置信区间，并在贝叶斯方法绘制成本效益接受性曲线。CEAC 的优势在于它既显示了组间对比估计的幅度，又描述了其不确定性。INB 相比于 ICER 避免了与比率统计相关的所有问题。关于信息方法（参见 Willan 和 Pinto, 2006 以及“参考文献”中的其他来源）。

# 致谢

作者的资金助来自加拿大自然科学与工程研究委员会的发现资助（资助号：44868-03）。

# 参考文献

- Bang, H., and A. A. Tsiatis. 2000. “Estimating medical costs with censored data.” *Biometrika* 87(2): 329–343.

- Briggs, A. H., and A. M. Gray. 1998. “The distribution of health care costs and their statistical analysis for economic evaluation.” *Journal of Health Services Research & Policy* 3(4): 235–345.

- Briggs, A. H., D. E. Wonderling, and C. Z. Mooney. 1997. “Pulling cost-effectiveness analysis by its bootstraps, a non-parametric approach to confidence interval estimation.” *Health Economics* 60(4): 327–340.

- Briggs, A., R. Nixon, S. Dixon, and S. Thompson. 2005. “Health economics: parametric modeling of data cost: some simulation evaluation.” *Health Economics* 14: 421–428.

- Chaudhary, M. A., and S. C. Stearns. 1996. “Estimating confidence intervals for cost-effectiveness: an example from a randomized trial.” *Statistics in Medicine* 15: 1447–558.

- Cochran, W. G. 1997. *Sampling Techniques*. New York: John Wiley & Sons, Inc.

- Cook, J. R., M. Drummond, H. Glic, and J. F. Heysse. 2003. “Assessing the appropriateness of combining economic data from multinational trials.” *Statistics in Medicine* 22: 1955–576.

- Eckmann, S., and A. R. Witten. 2007. “Expected value of information and decision making in HTA.” *Health Economics* 16: 195–209.

- Eckmann, S., and A. R. Witten. 2008. “The option of delay in health technology assessment.” *Medical Decision Making* 28(3): 300–305.

- Eckmann, S., and A. R. Witten. 2008. “Time and expected value of sample information wait for no patient.” *Value in Health* 11(3): 522–526.

- Eckmann, S., and A. R. Witten. 2009. “Globally optimal trial design for local decision making.” *Health Economics* 18:203–216.

- Efron, R. B., and B. R. J. Tibshirani. 1993. *Introduction to the Bootstrap*. New York: Chapman & Hall

- Fenwick, E. J. O’Brien, and A. H. Briggs. 2004. “Cost-effectiveness acceptability curves—fallacies, and frequently asked questions.” *Health Economics* 13: 405–415.
