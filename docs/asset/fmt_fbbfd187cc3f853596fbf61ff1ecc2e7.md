
在本章中，我们讨论了分析组间成本效益比较时涉及的主要问题。我们提供了执行 `PSBB` 分析的 `SAS` 代码，并附带了一个基于精神分裂症试验的模拟示例。`PSBB` 方法是一种极具吸引力的分析方法，因为它评估了平均成本、非参数性，并通过广泛接受的倾向评分分层方法评估了基线偏差。`PSBB` 可能并非适用于所有情况——因为缺乏关于方法论的比较研究，以了解各种方法的性能如何。

我们没有完全解决分析或成本数据呈现中涉及的所有问题。首先，我们在这里重点关注统计分析方法论——忽略了如研究设计、资源或成本的选择、成本数据的分配以及成本折现等问题——这些在引用的经济分析指南中已过充分讨论。我们还没有讨论缺失或截断成本数据的影响。这里说明的方法表明，无偏的成本或插补值是有价值的，或者处理数据的方法可以在倾向评分 Bootstrap 分析的结构内使用（例如）。我们的目标是让无偏成本或插补值有价值的，处理缺失数据的方法可以在倾向评分 Bootstrap 分析的结构内使用，包含以下三个部分：

- 1. 对假设的详尽评估；
- 2. 方法的可执行性；
- 3. 结果的透明度。

`Oberchain` 及其同事（1999）以及 `Kereaakis` 等同事（2000）的研究在成本效益方面是两个良好的案例。关于缺失数据的 cost-effectiveness 方法，请见 `Doshi` 和 `Young` (2006)。

# 参考文献

- Bouckaert, A., & Briggs, R. 1997. 成本差异的均值方法。
- Briggs, A. H., & Efron, B. 1996. 统计科学中的置信区间。
- Chennick, J. 1999. 倾向评分。John Wiley。
- DiCaprio, J. T., & Efron, B. 1996. 医疗决策中的 Bootstrap。
- Doshi, A. H., & Polsky, D. 2006. 随机对照试验的成本效益。
- Duan, N. 1983. 涂层估计：一种非参数变换方法。《美国统计学会杂志》。
- Duggan, M. 2005. 没有新药？第二代精神病药物。《药物经济学》。
- Garrison, R. L., Neumann, P. J., Erickson, E., Marshall, S., & Mullins, C. 2007. 使用真实数据进行覆盖和支付：ISOR 数据报告。
- Gianfranco, F., Wang, R., & White, R. 2002. 精神病领域基于索赔的研究方法。《药物经济学》。
- Grimes, D. A., & Schulz, K. 2002. 观察性研究中的偏差与关联。《柳叶刀》。
- Lindsey, J. K., & Jones, B. 1998. 选择应用于医学数据的广义线性模型。《医学统计学》。
- Liu, G. G., Sun, S. X., Christensen, B., & Zhao, Z. 2007. 北卡罗来州医疗补助计划中使用第二代精神病药物治疗精神分裂症的成本分析。《美国药剂协会杂志》。

## 336 使用 SAS 进行观察性健康数据分析

Lumley, T. P. Diehr, S. Emerson, and L. Chen. 2002. “正态假设在大型公共卫生数据集中的重要性。”Annual Review of Public Health 23: 151–169.

Manning, W. G. 1998. “对数因变量、异方差性与重构问题。”Journal of Health Economics 17: 283–295.

Mullahy, J. 1999. “健康经济学中考虑重构和两部分模型时我们所做的工作。”Journal of Health Economics 17(3): 247–281.

Nyhuis, A. W., M. D. Stensland, and D. E. Faries. 2003. “计算成本效益策略的恢复天数。”Schizophrenia Research 60(1): Supplement 1): 341.

Olinch, R. 2003–“ICEprobs: 一个通过倾向评分自助（两个偏倚样本）计算增量成本效益方差的 Windows 应用。”可用 http://members.iquest.net/softrix/ICErefs.htm

Olinch, R., and B. M. Johnstone. 1999. “随机临床试验中退出者成本数据的混合模型插补。”Drug Information 33: 191–209.

Olinch, R., C. A. Meifi, T. W. Croghan, and D. P. Buesching. 1997. “抗抑郁药物药物治疗中成本效益的自助分析。”Pharmacoeeconomics 11(5): 464–472.

Olinch, R. L. Robinson, and R. W. Swindle. 2005. “基于自助置信水平的成本效益推断：三个主导程度。”Journal of Biopharmaceutical Statistics 15(3): 419–436.

Oostenbrick, J. B., and M. J. Al. 2005. “由于脱落导致不完整成本数据分析。”Health Economics 14(8): 763–776.

Polsky, D. H. A. Glick, R. Willke, and K. Schulman. 1997. “成本效益的置信区间：四方法的比较。”Health Economics 6(3): 243–252.

Polsky, D. J., A. Doshi, M. S. Bauer, and H. A. Glick. 2006. “抗精神药技术的临床试验成本效益分析。”The American Journal of Psychiatry 163: 2047–2056.

Ramsey, S., R. Willke, R. Brown, M. Buxton, A. Chawla, J. Cook, H. Glick, B. Liljas, S. Pettitti, and S. Reed. 2005. “临床试验沿线成本效益分析的良好研究实践：ISPOR RCT-CEA 任务组报告。”Value in Health 8(5): 521–533.

Revicki, D. A., and L. Rubin. 1999. “真实世界中的药物经济学评价：有效性效力研究。”Pharmacoeconomics 15(5): 423–434.

Rosenbaum, P., and D. B. Rubin. 1983. “倾向评分在因果效应观察性研究中的核心作用。”Biometrika 70: 41–55.

Rosenbaum, P., and D. B. Rubin. 1984. “使用倾向评分中的子分类减少观察性研究中的偏倚。”Journal of the American Statistical Association 79: 516–524.

Rosenberg, R., D. Perlick, S. Bingham, W. Liu-Mares, J. Collins, S. Warren, D. Leslie, E. Allan, E. C. Campbell, S. Caroff, J. Corvin, D. Lewis, R. Douillon, L. Dunn, E. Evans, E. Fresca, J. Grabowski, D. Graeber, L. Herz, K. Kwon, W. Lawson, F. Mena, J. Sheikh, D. Smelson, and V. Smith-G. 2005. 奥氮西平对比氟氟啶平治疗分裂症的资源利用和成本：随机试验。”The Journal of Medical Association 290: 2693。

## 第15 章

### 增量效益

Andrew R. Willan

- 摘要 339
- 引言 340
- 成本效益分析 341
- 参数估计 346
- 示例 351
- 观察性研究 359
- 讨论 359
- 致谢 360
- 参考文献 360

# 摘要

自20世纪90年代初，受比较患者组临床研究中患者水平成本数据的推动，研究人员在成本效益数据的统计方法方面取得了快速进展。最初的工作集中在增量成本效益率的推断上，但由于比例统计的问题，兴趣更多地转向了增量。无论采用何种方法，都需要估计五个参数：组间平均有效性和平均成本的差异，以及相应的方差和协方差。通过这些参数估计，分析师可以估计增量成本效益率并计算相应的置信限。由于对比例统计的担忧，分析师可能会选择关注增量效益。采用传统的频率学方法，可以估计增量效益，并用相应的置信限表征其不确定性。或者，采用贝叶斯方法用于显示组间对比幅度并表征其不确定性。本文对这些方法进行了回顾。估计五个参数的特定统计方法取决于：

* 是否存在删
* 是否调整了协变量
* 是否调整了随机效应（例如国家）
* 关于成本分布的假设是什么

在存在这些条件组合的情况下，本文简要回顾了每种情况特定的统计方法。文中还提供了一个随机临床试验的示例。

# 15.1 引言

自20世纪90年代初以来，在临床研究中收集资源利用数据已变得越来越普遍。资源数据结合单位价格权重，除了有效性衡量外，还提供了患者水平总成本的衡量。在患者水平上拥有有效性和成本，允许使用传统的统计推断方法来量化由于抽样和测量误差引起的不确定性。关于成本效益数据的统计分析已发表大量文章。最初的工作集中于为增量成本效益比（`ICER`）提供置信区间，`ICER` 是治疗组间平均成本差异与治疗组间有效性差异的比值。然而，由于对比率统计量的考量，净收益（`INB`）的概念被用作一种替代方案。`INB` 是以货币形式衡量的有效性增加减去成本的增加。本章的目的是对建议的统计成本效益分析（`CEA`）方法进行结构化回顾，重点关注 `INB`。全文使用的背景是双臂临床试验，其中患者被随机分配到治疗组（`R`组）或标准组（`S`组）。然而，这些方法允许比较任何两组，但受限于缺乏随机分组的考虑（进一步讨论请参见第 15.5节）。

在参数方法中，`CEA` 的核心任务是联合建模有效性和成本以估计五个参数。其中两个参数是治疗组间的平均有效性差异，记为 `$\Delta_e$`，以及治疗组间的平均成本差异记为 `$\Delta_c$`。另外三个参数是 `$\Delta_e$` 估计量的方差记为 `$V(\Delta_e)$`；以及 `$\Delta_e$` 和 `$\Delta_c$` 估计量的协方差记为 `$C(\Delta_e, \Delta_c)$`，其中 `$\hat{\theta}$` 表示 `$\theta$` 的估计量。必须对有效性和成本进行联合建模才能估计协方差。用于估计这五个参数的特定统计程序取决于：

- 是否存在截断
- 是否调整了协变量
- 是否调整了如国家之类的随机效应
- 关于成本分布的假设是什么

利用这五个参数的估计量，可以进行基于增量效益比或增量收益的 `CEA`。在本章的其余部分，假设 `$\Delta_e$` 和 `$\Delta_c$` 的估计量服从正态分布。这一假设基于中心极限定理，该定理认为大量独立变量之和将趋于从正态分布。

在第 15.2 节中说明了基于五个参数估计值显示 `CEA` 的。用于估计参数的统计程序（取决于前述讨论的问题）将在第 15.3 节中回顾。第 15.4 节给出了一个使用随机临床试验的示例。第 15.5 节讨论了针对观察性研究特定的问题。第 15.6 节是本章的总结。

# 15.2 成本效益分析

本节提供了与两组比较相关的成本效益分析概介绍。通常（但并非如此），`CEA` 中的有效性衡量与患者经历的临床事件相关，例如死亡、复发或达到预设的症状缓解水平。与事件相关的三个有效性衡量指标例如：

- 1. 患者在感兴趣期内是否存活
- 2. 在感兴趣期内的生存时间
- 3. 在感兴趣期内的质量调整后生存时间

相应的 `$\Delta_e$` 为：

- 1. 存活概率的治疗组间差异
- 2. 平均生存时间的治疗组间差异
- 3. 平均质量调整后生存时间的治疗组间差异

所有平均值均限于感兴趣期，差异取为 `T-S`。`ICER` 定义为 `$\Delta_c/\Delta_e$`，分别为：

- 1. 使用 `T` 替 `S` 的额外成本
- 2. 使用 `T` 替 `S` 获得额外寿命的成本
- 3. 使用 `T` 替 `S` 获得质量调整寿命（`QALY`）的成本

`ICER` 可以在成本效益平面上所示，如图 15.1 所示，即原点与点 `($\Delta_c$, $\Delta_e$)` 之间的斜率。

在图 15.1 到 15.5 中，我们假设有效性衡量是质量调整生存时间，有效性单位是质量调整年（`QALYs`）。图 15.1 中同样显示的直线称为阈值，其斜率等于单位性的支付意愿（`WTP`），记为 `$\lambda$`。阈值将成本效益平面分为两个区域。对于阈值右侧（阴影部分）的点，`T` 被认为是有成本的，但对于上方和左侧的点，则不是。因为 `$\lambda$` 是正值，`SE` 象限中 `T` 更有效且成本更高的点位于阈值下方，因此对应的比较 `T` 有成本效益。相反，`NW` 象限中 `T` 有效且成本更高的点位于阈值上方，因此对应的比较 `T` 无。在 `NE` 和 `SW` 象限，`WTP` 概念允许有效性和成本之间的权衡。在 `NE` 象限，直线下方任何点的斜率小于 `$\lambda$`（即 `$\Delta_c/\Delta_e < \lambda$`），这意味着 `$\Delta_c < \lambda\Delta_e$`。

# 15.3 使用 SAS 分析观察性数据

因此，价值的增加 `($\lambda\Delta$)` 大于成本的增加，使得 `T` 有成本效益。在 `SW` 象限，直线下方任何点的斜率大于 `$\lambda$`，由于 `$\Delta_c$` 和 `$\Delta_e$` 均为负值，`$|\Delta_c| > |\lambda\Delta|$`，我们得到 `$\frac{\Delta_c}{\Delta_e} > \lambda$`，这意味着 `$|\Delta_c|$` 小于 `T` 节省的金额 `($\lambda\Delta$)`。总而言之，`T` 有成本效益当且仅当：

`A: \frac{\Delta_c}{\Delta_e} < \lambda` 若 `$\Delta_e > 0$`，或者 `$\frac{\Delta_c}{\Delta_e} > \lambda$` 若 `$\Delta_e < 0$`。(1)

方程 1（假设 A）定义了阈值下方的区域，可以认为是零假设 `H` 的备择假设，即：

`H: \frac{\Delta_c}{\Delta_e} \geq \lambda` 若 `$\Delta_e > 0$`，或者 `$\frac{\Delta_c}{\Delta_e} \leq \lambda$` 若 `$\Delta_e < 0$`。(2)

拒绝 `H` 而接受 `A` 将为采用 `T` 提供证据。这些方程有些繁琐，通过引入 `INB` 可以大大简化。

**图 15.1** 成本效益平面

| NW | `$\Delta_c$` | NE |
| :--- | :--- | :--- |
| | | `($\Delta_c$, $\lambda\Delta$)` |
| | 阈值；斜率 = `$\lambda$` | |
| | | 斜率 = `$\Delta_c/\Delta_e$` |
| | `$\Delta_e$` (QALYs) | |
| SW | | SE |

# 15.4 增量净收益

`INB` 是 `$\lambda$` 的函数，定义为 `$b_\lambda \equiv \lambda\Delta - \Delta_c$`；`$b_\lambda$` 是增量收益，因为它是增量价值 `($\lambda\Delta$)` 与增量成本 `($\Delta$)` 之差。无论 `$\lambda$` 的符号如何，`T` 有成本效益当且仅当 `$b_\lambda > 0$`。为了证明这一点，方程 1 中涉及 `ICER` 的两个不等式都可以重组为 `$\lambda\Delta - \Delta_c > 0$`。同样，方程 2 中涉及 `ICER` 的两个不等式都可以重组为 `$\lambda\Delta - \Delta_c \le 0$`。因此，从 `INB` 来说，零假设和备择假设简化为：

`H: b_\lambda \le 0 \quad A: b_\lambda > 0`。(3)

方程 1、2、3 中假设 `H` 和 `A` 的公式说明了 `ICER` 和 `INB` 之间的紧密关系`$b_\lambda$` 是从点 `($\lambda\Delta$, $\Delta_c$)` 到阈值的垂直距离，如果点在直线下方则为正，反之为负。因为它的斜率为 `$\lambda$`，阈值上横坐标等于 `$\Delta_c$` 的点为 `($\Delta_c$, $\lambda\Delta$)`，它与 `($\lambda\Delta$, $\Delta_c$)` 之间的垂直距离为 `$\lambda\Delta - \Delta_c$`（见图 15.2）。

# 图 15.2 成本效益平面上的 INB ($b_\lambda$)

![](img/fe9ff008f88baacd415148b0b25dd58c_357_0.png)

`ICER` 可以通过 `$\hat{\Delta}_c/\hat{\Delta}_\lambda$` 估计，其中 `$\hat{\Delta}_c$` 和 `$\hat{\Delta}_\lambda$` 分别是 `$\Delta_c$` 和 `$\lambda\Delta$` 的估计量。估计量 `$\hat{\Delta}_c/\hat{\Delta}_\lambda$` 是偏的，但如果 `$\hat{\Delta}_c$` 和 `$\hat{\Delta}_\lambda$` 是无偏的，它是一致的，这意味着随着样本量的增加偏差会减小（`Caudhary` and `Stearns`, 1996; `Cochran`, 1997）。`ICER` 的统计推断被限于计算其置信区间。应用 Fieller 定理 [1, 3]，`$(1-2\alpha)100\%$` 置信限为

## 344 使用 SAS 进行观察性健康数据分析
