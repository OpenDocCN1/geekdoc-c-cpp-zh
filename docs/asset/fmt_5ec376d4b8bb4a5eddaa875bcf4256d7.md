
Neuschwander, Branson, 和 Gponder (2008) 报告了一项 I 期试验，在该试验中，当规模为 2 的队列中两名患者都发生 DLT 后，单参数 CRM 要求增加剂量。作者推测这种行为归因于单参数幂模型。但有人指出，这种行为更有可能是由于骨架模型（`skeleton`）选择不当（Ianosos 和 O'Quigley, 2014）；一个信息量丰富的先验对高剂量水平成为 MTD 赋予了过多的先验概率（Ianosos 和 O'Quigley, 2012）；或者允许研究者跳过两个剂量的偏离原始设计。关于 CRM 中过度参数化的进一步讨论，请读者参考 Ianosos 等 (2016)。

# 3.4 偏序重评估方法

最近，人们对研究药物组合的潜力产生了增长的兴趣。治疗药物组合的动机源于改善反应。在本节中，将讨论偏序重评估方法（POCRM）。

如前所述，I 期试验的一个关键挑战是识别顺序的组合。例如，考虑概率的偏序。可以假设 $x_5$ 比 $x_6$ 毒性。可能是 $\pi(x_5) < \pi(x_6)$ 或 $\pi(x_6) < \pi(x_5)$。

考虑表 3.3 定义的剂量水平，从 $x_1$ 移动到 $x_5$：

| 治疗 | $x_1$ | $x_2$ | $x_3$ | $x_4$ | $x_5$ |
|---|---|---|---|---|---|
| BMS-2162 | 80 | 80 | 120 | 160 | 160 |
| 聚紫醇 | 135 | 175 | 175 | 175 | 225 |

考虑到这些组合之间已知和未知的关系，我们可以制定两种可能的排序，索引为 $m$：

$m = 1 : \pi(x_1) < \pi(x_2) < \pi(x_3) < \pi(x_4) < \pi(x_5) < \pi(x_6)$，

$m = 2 : \pi(x_1) < \pi(x_2) < \pi(x_3) < \pi(x_4) < \pi(x_6) < \pi(x_5)$。

利用这种方法的方法是 Wages、Conaway 和 O'Quigley (2011) 最初提出的偏序重评估方法。

偏序 CRM 是基于使用一组对应于可能排序的工作模型类。具体来说，假设我们正在考虑 $M$ 种可能的排序。对于特定的排序 $m$，我们通过一组单参数工作模型 $F_m(x_i, m)$ 来对组合 $x_i$ 的真实毒性概率，例如幂模型

```
$F_m(x_i, \beta_m) = x_{mi}^{exp(\beta_m)}, \quad (3.7)$
```

工作模型 $m$。研究已经探索了 CRM 类常用的其他单参数工作模型，例如双曲正切函数或单参数逻辑模型，发现各种模型选择之间的运行特征差异不大。

## 贝叶斯框架

与 CRM 类似，POCRM 的原始公式采用了贝叶斯方法。在这种设定下，我们首先为每个模型的参数 $\beta_m$ 分配先验分布 $g_m(\beta_m)$。我们用一组先验概率来描述所考虑排序的合理性：

$\tau = \{\tau(1), \dots, \tau(M)\}$

其中 $\tau(m) > 0$ 且 $\tau(1) + \dots + \tau(M) = 1$。

假设在试验的某一点，在接受 $x_i$ 治疗的 $n_i$ 名患者中，有 $y_i$ 名患者经历了剂量毒性（DLT）。使用数据 $D=\{(y_i, n_i)\}; i = 1, \dots, k$，在第 $m$ 种排序下的似然函数给出：

$$\mathcal{L}_m(D|\beta_m) \propto \prod_{i=1}^k (F_m(x_i, \beta_m))^{y_i} (1 - F_m(x_i, \beta_m))^{n_i-y_i}. \quad (3.8)$$

其后验密度给出为：

$f_m(\beta_m|D) = \frac{\mathcal{L}_m(D|\beta_m)g_m(\beta_m)}{\int \mathcal{L}_m(D|\beta_m)g_m(\beta_m)d\beta_m}$

这些信息可以用于建立给定数据下的模型后验概率：

$P(m|D) = \frac{\int_M \mathcal{L}_m(D|\beta_m)g_m(\beta_m)d\beta_m}{\sum_{m=1}^M \int \mathcal{L}_m(D|\beta_m)g_m(\beta_m)d\beta_m}$

POCRM 建议选择具有最大后验模型概率的单一排序（模型）$h$，使得

$h = \arg\max_{m} P(m|\mathcal{D})$

并应用 CRM 的贝叶斯形式。给定排序 $h$ 和工作模型 $F_h(x_p, \beta_h)$，我们在每个组合生成 DLT 概率，使得：

$$\tilde{\pi}(x_i) = F_h(x_i, \beta_h)$$

其中

$$\tilde{\beta}_h = \int f_h(\beta_h|\mathcal{D})d\beta_h$$

分配给试验中下一个患者的组合是其估计 DLT 概率最接近目标 DLT 概率的组合。

## 案例 2 中的 POCRM

回到案例 2，设计了一个剂量递增试验以确定标记为 $x_1, \dots, x_5$ 的治疗的最大耐剂量（MTD）组合（见表 3.3）。PCRRM 的先验设定根据组合的部分序来选择可能的剂量-毒性排序子集。对于每种排序，可能性上述两种排序。我们需要指定一组骨架值 $x_{mi}$。我们只需指定一组间距合理的值，或使用 Lee 和 Cheung (2009) 的算法生成这些值。然后对这些值进行调整以对应每个可能的排序。例如，对于上述定义的 $m = 1$，我们指定 $x_{1i}$ 为：

$m = 1 : 0.05\ 0.15\ 0.25\ 0.35\ 0.45\ 0.55,$

而对于上述定义的 $m = 2$，我们指定 $x_{2i}$ 为：

$m = 2 : 0.05\ 0.15\ 0.25\ 0.35\ 0.55\ 0.45.$

我们先验假设这两种排序的概率相等，并令 $\tau(1) = \tau(2) = 0.5$。对于每种排序，$\beta$ 的先验分布假设为 $g_m(\beta_m) = N(0, 1.34)$。

DLT 概率通过方程 3.7 中定义的幂模型进行建模。

所得基于 POCRM 的算法定义如下：

1. 给第一个患者分配“最低”组合 $x_1$。在试验的任何时候，根据迄为止包含在试验中的患者累计数据，根据上述涉及贝叶斯模型选择的程序，获得所有测试组合的估计毒性概率 $\pi(x_i)$。

2. 将下一个入患者分配到估计毒性概率最接近目标率的剂量组合，使得 $|\pi(x_i) - \theta|$ 最小化，并带有以下限制：在递增时，不允许试验“跳过”未尝试过的组合。如果所有组合都已尝试，允许研究移动到方法推荐的任何组合。

3. MTD 组合定义为总样本量为 $n$ 名患者后使 $|\pi(x_i) - \theta|$ 最小的组合。

在试验 DLT 结果的模拟中，每个患者的耐受性可以被视为区间 $[0, 1]$ 上的均匀分布随机变量。该值被称为患者的潜在毒性耐受性，对于第 $j$ 个患者用 $u_j$ 表示（O’Quigley, Paolaletti, and Maccario, 2002）。在分配给患者 $j$ 的组合 $(x_j)$ 上，如果耐受性小于或等于其真实的 DLT 概率（即 $u_j \le \pi(x_j)$），则患者 $j$ 具有 DLT。否则患者为非 DLT 结果。当然，在真实试验中无法观测患者的潜在耐受性。但它是模拟中非常有用的工具，可用于评估单个试验内剂量寻找方法的运行特征。

在进行此练习时，我们使用程序 3.6 为 $n=30$ 名患者生成了表 3.4 中的潜在耐受性序列。

### 程序 3.6 30 名患者的潜在结果生成

```sas
data latent;
do i = 1 to 30;
  u = rand("Uniform");
  output;
end;
run;

proc print data=latent;
run;
```

## 程序 3.6 的输出

| Obs | i | u |
| :--- | :--- | :--- |
| 1 | 1 | 0.978 |
| 2 | 2 | 0.595 |
| 3 | 3 | 0.340 |
| 4 | 4 | 0.055 |
| 5 | 5 | 0.043 |
| 6 | 6 | 0.869 |
| 7 | 7 | 0.478 |
| 8 | 8 | 0.649 |
| 9 | 9 | 0.873 |
| 10 | 10 | 0.539 |
| 11 | 11 | 0.738 |
| 12 | 12 | 0.129 |
| 13 | 13 | 0.495 |
| 14 | 14 | 0.690 |
| 15 | 15 | 0.413 |
| 16 | 16 | 0.787 |
| 17 | 17 | 0.285 |
| 18 | 18 | 0.847 |
| 19 | 19 | 0.905 |
| 20 | 20 | 0.963 |
| 21 | 21 | 0.779 |
| 22 | 22 | 0.223 |
| 23 | 23 | 0.248 |
| 24 | 24 | 0.862 |
| 25 | 25 | 0.534 |
| 26 | 26 | 0.286 |
| 27 | 27 | 0.440 |
| 28 | 28 | 0.237 |
| 29 | 29 | 0.803 |
| 30 | 30 | 0.321 |

* `nsim` 是模拟模式下模拟运行的次数（默认值为 1,000）。如果 `redata=TRUE`，则忽略此参数。
* `seed` 是模拟运行的种子。
* `ncohort` 是每个模拟试验中入组患者队列（`patient cohort`）的数量。
* `startdose` 是模拟模式下的起始剂量（默认值为 1）以及数据分析模式下的当前剂量。
* `cs` 是确定试验是否应因安全原因终止的安全阈值。
* `nstop` 指定了为了停止试验在剂量组合（`combination`）中需要入组的患者人数。
* `csize` 是每个患者队列的大小（默认值为 1）。
* `target` 是目标毒性率（默认值为 0.25）。
* `pl` 是用于生成数据的每个剂量组合的真实毒性率。
* `pskel` 是对应 DLT 概率可能排序的工作模型骨架。
* `redata` 决定宏的运行模式（数据分析模式或模拟模式）。如果 `redata=TRUE`，宏将运行一次并分析 `trialdata` 数据集中的真实临床数据。请注意，在这种情况下，模拟设置将被忽略。

程序 3.7 展示了 `%POCRM` 宏的应用。

## 程序 3.7 POCRM 实现

```sas
* y 是 DLT 的数量，n 是患者数量；
data fdata;
input y n;
cards;
0 1
0 1
0 1
1 1
0 0
0 0
run;

* 在实现 realdata 后（设置 realdata=TRUE），将起始剂量更改为当前组合。如果是模拟，则 realdata=%POCRM(nsim=1000, seed=580, ncohort=30, startdose=4, cs=0.9, csize=1, target=0.25,
pl=%bquote((0.02 0.05 0.08 0.25 0.45 0.55)),
pskel=%bquote((0.05 0.15 0.25 0.35 0.45 0.55),
0.05 0.15 0.25 0.35 0.55 0.45));nrealdata=TRUE, trialdata=fdata);
```

## 程序 3.7 的输出

`mtox_sel`

1

`ptox_hat`

0.1074933 0.2082244 0.296629 0.3826772 0.4692604 0.5577856

`pstop`

0

`pry`

0 0 0 1 0

`prn`

1 1 1 1 0

`pselect`

0 1 0 0 0 0

对于 `fdata` 数据集中包含的示例数据，输出 3.7 提供了估计的排序 (`mtox sel`)、每个剂量组合的估计 DLT 概率 (`ptox hat`)、试验是否应终止 (`pstop`)、每个剂量组合的观察到的 DLT 数量 (`pry`)、每个剂量组合接受治疗的患者人数 (`prn`) 以及基于累积数据推荐的组合 (`pselect`)。

**程序 3.8** 通过模拟十次试验展示了 POCRM 算法：

## 程序 3.8 POCRM 模拟

```sas
%POCRM(nsim=10, seed=580, ncohort=30, startdose=1, cs=0.90,
csize=1, target=0.25,
pl=%bquote({0.02 0.05 0.08 0.25 0.45 0.55}),
pskel=%bquote({0.05 0.15 0.25 0.35 0.45 0.55,
0.05 0.15 0.25 0.35 0.55 0.45});
```

## 程序 3.8 的输出

`pstop`

0

`pry`

0 0.3 0.5 3 1.8 1.1

`prn`

1.6 2.4 7.8 11.8 4.4 2

`pselect`

0 0 0.2 0.6 0.1 0.1

基于十次模拟试验，**输出 3.8** 提供了提前终止的试验百分比 (`pstop`)、每个剂量组合观察到的平均 DLT 数量 (`pry`)、每个剂量组合接受治疗的平均患者人数 (`prn`) 以及每个组合被推荐为最大耐量剂量 MTD 的试验百分比 (`pselect`)。

### 3.5 总结

本章概述了早期剂量爬增试验中的剂量寻找设计，重点讨论了肿瘤学试验。首先对定义剂量分配方法（基于规则的方法）较为直接的方法进行了高级总结。这包括基础算法（如 3+3 算法）以及更灵活的算法（如组上下降设计（`group up-and-down design`）和 mTPI 方法）。本章还详细描述了基于连续重新评估法（CRM）的基于剂量爬增方法。回顾了 CRM 在单药和药物联合剂量爬增试验中的应用。CRM 是传统基于规则方法（如基础 3+3 算法）的替代方法。它已被许多研究人员广泛研究，并证明在确定 MTD 方面更多功能且高效。这类基于模型的方法使用累积数据和灵活的队列大小，允许更好的决策。我们提供了关于如何在 SAS 中实现标准 CRM 算法及其在药物联合试验中扩展（POCRM）的建议。我们希望 SAS 代码的可用性将鼓励这些方法在实践中的广泛使用。

### 3.6 参考文献

Babb, J., Rogatko, A., Zacks, S. (1998). Cancer Phase I clinical trials: efficient dose escalation with overdose control. Statistics in Medicine 17, 1103-1120.

Cheung, Y. K., Chappell, R. (2000). Sequential designs for Phase I clinical trials with late-onset toxicities. Biometrics 56, 1177-1182.

Cheung, Y.K., Chappell, R. (2002). A simple technique to evaluate model sensitivity in the continual reassessment method. Biometrics 58, 671-674.

Cheung, Y.K. (2013). Sample size formulae for the Bayesian continual reassessment method. Clinical Trials 10, 852-861.

Cheung, Y.K. (2011). Dose finding by the Continual Reassessment Method. New York: Chapman and Hall Biostatistics.

Chevret, S. (1993). The continual reassessment method in cancer I trials. Statistics in Medicine 12, 1093-1108.

Dy, G.K., Bruzek, L.M., Croghan, G., et al. (2005). A Phase I trial of the novel farnesyl protein transferase inhibitor, BMS214662 in combination with paclitaxel and carbobatin in patients with advanced cancer. Clinical Cancer Research 11, 1877-1883.

Faries, D. (1984). Practical modifications of the continual reassessment method for phase I trials. Journal of Biopharmaceutical Statistics 4, 147-164.

Gatson, C., Greenhouse, J.B. (1992). Bayesian methods for phase I clinical trials. Statistics in Medicine 11, 1377-1389.

Goodman, S.N., Zahurak, M.L., Piantados, S. (1995). Some practical improvements in the continual reassessment method for phase I studies. Statistics in Medicine 14, 1149-1161.

Guo, W., Wang, S.J., Yang, S., Lin, S., Ji, Y. (2017). A Bayesian interval dose-finding design addressing Ockham’s razor: mTPI-2. In press.
