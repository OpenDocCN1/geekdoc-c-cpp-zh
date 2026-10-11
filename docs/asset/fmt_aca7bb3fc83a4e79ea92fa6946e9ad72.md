
## 程序代码

```
2 32.0

2 38.4

ods html;

title "Relative Risk Results";

proc genmod data=adverse_events;

class id treat;

model y = dist=poisson link=log;

repeated subject=id / type=ind;

lsmeans treat;

estimate "Active Vs Placebo" treat 1 -1;

run;

title "Rate Ratio Results";

proc genmod data=adverse_events;

class id treat;

model y = dist=poisson link=log offset=offs;

repeated subject=id / type=ind;

lsmeans treat;

estimate "Active Vs Placebo" treat 1 -1;

run;

ods close;
```

## 输出 9.5：程序 9.5 的选取结果

| 相对风险结果 | | |
| GENMOD 过程 | | |
| 最小二法平均 | | |
| 效应 | 估计值 | 标准误 | DF | 卡方 | Pr > Chi |
| | 平均值 | L'Beta | | | |
| treat | 1 | 0.6000 | -0.5108 | 0.2582 | 1 | 3.91 | 0.0479 |
| treat | 2 | 0.3000 | -1.2040 | 0.4830 | 1 | 6.21 | 0.0127 |
| 差异估计结果 | | | | | | | |
| 标签 | 平均估计值 | 平均 L'Beta 估计值 | 标准误 | Alpha | L'Beta | 卡方 | Pr > Chi |
|---|---|---|---|---|---|---|---|
| | 置信区间 | | | | | | |
| Active Vs Placebo | 2.0000 | 0.6836 | 5.8513 | 0.6931 | 0.5477 | 0.05 | -0.3804 | 1.7667 | 1.60 | 0.2057 |

Morel, Jorge, and Nagaraj Neelhari. Overdispersion Models in SAS®. ©2011, SAS Institute Inc., Cary, North Carolina, USA. 保留所有权利。更多 SAS 资源，请访问 support.sas.com/publishing。

314 SAS 中的过度离散模型

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **风险率结果** | | | | | | | |
| **GENMOD 过程** | | | | | | | |
| **最小二法平均** | | | | | | | |
| 效应 | treat | 估计值 | 标准误 | DF | 卡方 | Pr > Chi | |
| | | 平均值 | L'Beta | | | | |
| treat | 1 | 0.0300 | -3.5066 | 0.3332 | 1 | 110.78 | <0001 |
| treat | 2 | 0.0075 | -4.8929 | 0.5266 | 1 | 86.34 | <0001 |
| **差异估计结果** | | | | | | | | |
| 标签 | 平均估计值 | 平均 L'Beta 估计值 | 标准误 | Alpha | L'Beta | 卡方 | Pr > Chi |
|---|---|---|---|---|---|---|---|
| | | 置信区间 | | | | | | |
| Active Vs Placebo | 4.0000 | 13.5663 | 1.3863 | 0.6231 | 0.05 | 0.1650 | 2.6076 | 4.95 | 0.0261 |

区间 (9,19) 中的相对风险对数为 0.6931。其从 (9,20) 得到的估计标准误为 0.5477。近似 95% 置信区间为 (-0.3804, 1.7667)。估计的相对风险为 `exp [0.6931]=2.0`，近似 95% 置信区间为 (0.638, 5.8513)。如果分析的目的是估计风险率而非相对风险，AE 发生时间的对数就是一个偏移变量。在这种情况下，主要结果如下：活性组和安慰剂组的估计发生率对数分别为 -3.5066 和 -4.8929 (9.14)。使用方程 (9,15)，通过三明治方差估计得到的标准误分别为 0.3332 和 0.5266。活性组和安慰剂组的估计率分别为 0.0300 和 0.0075。在安慰剂组中，预期发生率为 52(0.0075)=0.39 AE/人年。另一方面，活性组的率更高，为 `exp(0.0300)=1.03` AE/人年。估计的风险率为 4.00。近似 95% 置信区间为 (1.1794,35.863)。注意，上述方法是一种计算技巧，可以给出正确的相对风险和风险率及其相应的标准误，因此输出的其他部分可能并不相关。获取与相对风险相关的结果另一种方法如下：

```
title "Relative Risk Results";nproc genmod data=average_events descending;

class id treat;

model y = dist=binomial link=log;

repeated subject=id / type=ind;

ismeans treat;

estimate 'Active Vs Placebo' treat 1 -1;

run;
```

### 第 9 章 边缘模型的广义估计方程技术

然而，无法使用 `dist=binomial` 和 `link=log` 选项获得率比结果，因为偏移变量（offset variables）产生的均值参数对于某些观测值是无效的或处于极限。顺便提到，本节描述的方法也适用于 9.6 节讨论的 Proagide 示例中的重复测量。模型 (9.9) 回归参数的解释如下：

| 治疗组 | 访问次数 | 每周预期发作次数 |
| --- | --- | --- |
| 安慰剂 (Placebo) | 基线 (Baseline) | `exp(β₁)` |
| | 治疗期 (Treatment Phase) | `exp(β₀ + β₁)` |
| Proagide | 基线 | `exp(β₀ + β₂)` |
| | 治疗期 | `exp(β₀ + β₂ + β₃)` |

基线率与 Proagide 率的比例为 `exp(-β₂)`，治疗期安慰剂率与 Proagide 率的比为。注意 `β₁` 是随机化的效应。此外，安慰剂治疗期与基线的比例为 `R₁ = exp(β₁)`，它捕捉了安慰剂效应；而 Proagide 治疗期与基线的比例为 `R₂ = exp(β₂ + β₃)`。

最后，`R₃ = exp(-β₁)` 代表 `R₁` 与 `R₂` 的比例。该比例 `R₃` 可以被看作是在将在每种率与其相关的基线率进行归一化后，安慰剂治疗率与 Proagide 率的比例。这些率、它们的对数及其标准差可以使用上一个示例中解释的方法通过 `GLIMMIX` 过程进行估计。编程语句在程序 9.3 的延续中所示。

## 程序 9.3：延续

```sas
ods html;

*** Rates Proagide Trial ***

proc glimmix data=seizures;

class id;

model cnt = trt xl1*trt dist=poison offset=time covb=none random / subject=typecorr;

estimate 'Rate Placebo Baseline' 1;

estimate 'Rate Placebo Treatment Phase' 1;

estimate 'Rate Proagide Baseline' 1;

estimate 'Rate Placebo TRT Phase' trt-1 xl1*trt 1;

estimate 'Rate Placebo Proagide Baseline' trt-1 xl1*trt -1;

estimate '(R1) Baseline TRT Phase / Placebo Baseline' xl1 1;

estimate '(R2) Proagide TRT Phase / Proagide Baseline' xl1*trt 1;

estimate '(R3) = (R1) / (R2)' xl1*trt -1;

run;

ods html close;
```
