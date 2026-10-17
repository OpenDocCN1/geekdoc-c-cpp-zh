
- Cross, J., Lee, H., Westelinck, A., Nelson, J., Grudzinskas, C., Peck, C. (2002). Postmarketing drug dosage changes of 499 FDA-approved new molecular entities, 1980-1999. *Pharmacoepidemiology and Drug Safety*. 11, 439-446.

- Dmitrienko, A., Fritzsch, K., Hsu, J., Rubberg, S. (2007). Design and analysis of dose-ranging clinical studies. *Pharmaceutical Statistics Using SAS: A Practical Guide*. Dmitrienko, A., Chuang-Stein, C., D’Agostino, R. (editors). Cary, NC: SAS Institute Inc.

- EMA (2014). Qualification opinion of MCP-Mod as an efficient statistical methodology for model-based design and analysis of Phase II finding studies under model uncertainty. Committee for Medicinal Products for Human Use (CHMP). EMA/CHMP/SAWP/75052/2013.

- Genz, A., Bretz, F. (2002). Methods for the computation of multivariate t-probabilities. *Journal of Computational and Graphical Statistics* 11, 950-971.

- Hoeting, J.A., Madigan, D., Raftery, A.E., Volinsky, C.T. (1999). Bayesian model averaging: A tutorial. *Scientific Science* 4, 382-401.

- Kass, R. E., Raftery, A. E. (1995). Bayes factors. *Journal of the American Statistical Association* 90, 773-795.

- Klingenberg, B. (2009). Proof of concept and dose estimation with binary responses under model uncertainty. *Statistics in Medicine* 28, 274-292.

- Mallinckrodt, C., Lipkovich, I. (2016). *Analyzing Longitudinal Clinical Data: A Practical Guide*. New York: Chapman and Hall/CRC.

- Menon, S., Zink, R. (2016). *Clinical Trials Using SAS: Classical, Adaptive and Bayesian Methods*. Cary, NC: SAS Institute Inc.

- Mercier, F., Bornkamp, B., Ohlssen, D., Wallstrom, E. (2015). Characterization of dose-response for count data using a generalized MCP-Mod approach in an adaptive dose-ranging trial. *Pharmaceutical Statistics* 14, 359-367.

- O'Kelly, M., Ratitch, B. (2014). *Clinical Trials with Missing Data: A Guide for Practitioners*. New York: Wiley.

- Pinheiro, J. C., Bornkamp, B., Bretz, F. (2006). Design and analysis of dose finding studies combining multiple comparisons and modeling procedures. *Journal of Biopharmaceutical Statistics* 16, 639-656.

- Pinheiro, J., Bornkamp, B., Bretz, F. (2014). Generalizing the MCP-Mod method beyond normal. *Dose Finding*. Ting, N. (editor). New York: Springer.

- Pinheiro, J., Bornkamp, B., Glimm, E., Bretz, F. (2013). Parametric procedures under model uncertainty. *Statistics in Medicine* 33, 1646-1661.

- Raftery, A.E. (1995). Bayesian model selection in social research. *Sociological Methodology*. Marsden, P. (editor), 111-195. Cambridge, MA: Blackwell.

- Ruberg, S.J. (1989). Contrasts for identifying the minimum dose. *Journal of the American Statistical Association* 84, 816-822.

- Ruberg, S.J. (1995a). Dose response studies. Some design considerations. *Journal of Biopharmaceutical Statistics* 5, 1-14.

- Ruberg, S.J. (1995b). Dose response studies. Analysis and interpretation. *Journal of Biopharmaceutical Statistics* 5, 15-42.

- Scheffe, H. (1959). *The Analysis of Variance*. London, UK: Wiley.

- Stewart, W. H., Ruberg, S. (2000). Detecting dose response with contrasts. *Statistics in Medicine* 19, 913-921.

- Tamhane, A.C., Logan, B.R. (2002). Multiple test procedures identifying the minimum effective and safe doses of a drug. *Journal of the American Statistical Association* 97, 293-301.

- Tukey, J.W., Ciminera, J.L., Heyse, J.F. (1985). Testing the statistical certainty of a response to increasing doses of a drug. *Biometrics* 41, 295-301.

- Williams, D.A. (1971). A test for differences between treatment means when several dose levels are compared with a zero dose control. *Biometrics* 27, 103-117.

- Williams, D.A. (1972). The comparison of several dose levels with a zero dose control. *Biometrics* 28, 519-531.

## 第5章

## 多重调整方法

Thomas Brechenmacher (QuintilesIMS)

Alex Dmitrienko (Mediana)

- 5.1 引言
- 5.2 单步程序
- 5.3 基于数据驱动的假设排序的程序
- 5.4 基于预设假设排序的程序
- 5.5 参数化程序
- 5.6 门控程序
- 5.7 参考文献
- 5.8 附录

本章讨论了处理具有多个临床目标的临床试验中多重性问题的统计策略。它定义了常用的多重调整，包括基础的单步检验方法，以及依赖于数据驱动或预设假设排序的更高级的步进方法。本章还回顾了在高级设置下使用的门控检验策略——例如在支持对新型治疗药物多个剂量下同时评估多个临床终点的试验中。本章介绍的多重调整将通过确认性 III 期临床试验进行说明。

### 5.1 引言

多重性问题在几乎所有后期临床试验中都会出现，因为试验赞助者通常希望基于多个终点的评估来研究多个临床目标，例如，多个剂量-对照比较、在两个或多个患者人群中评估治疗效果等。在这些情况下，试验的总体成功标准是基于多项显著性检验定义的。因此，在名义水平上控制错误地得出新治疗法有效的结论概率（第一类错误率）至关重要，例如，单侧 $\alpha = 0.025$ 或双侧 $\alpha = 0.05$。

以下是临床试验中遇到的多重性问题示例：

1. **多重治疗比较。** 在涉及多个治疗组的临床试验中，经常遇到多重检验。此类情况的示例包括：II 期试验，其目的是评估实验性药物的几个剂量与安慰剂或活性对照组相比的疗效和安全性特征。将实验性药物的不同剂量水平与对照组进行多重比较会导致多重性问题。

2. **多个主要终点。** 多重性也源于用于评估实验性药物有效性或安全性的多个标准。需要这些多个标准来准确描述预期治疗获益的各个方面。例如，心血管药物的疗效特征通常使用多个结局变量进行评估，如全因死亡、非致命性心肌梗死或顽治性心绞痛/紧急血管重建。

3. **多个次要终点。** 公认认为，所有确认性临床试验都必须处理主要分析中的多重性问题。在现代临床试验中，基于关键次要终点做出正式声明越来越理想。因此，还需要对次要统计检验进行适当的多重性调整，以控制总体第一类错误率。例如，在肿瘤临床试验中，通常希望结合无进展生存期和总生存期来描述临床获益。

4. **多个患者人群。** 临床试验的主要分析可以在普通患者人群中进行，也可以在预设的目标亚组中进行。与普通人群患者相比，该亚组中的患者预计可能会获得更大的治疗获益，或更有可能产生反应。这种多人群设计出现在肿瘤临床试验和其他治疗领域。

这些临床试验示例处理的是单一多重性来源或导致第一类错误率膨胀的单一设计特征。在确认性临床试验中，遇到具有多个多重性来源的问题日益常见。这些问题的特征是：考虑了多个导致第一类错误率膨胀的特征。其示例包括在多个剂量或多个患者人群中评估多个终点效果的临床试验。

几份监管指导文件强调了在确认性临床试验中保护第一类错误率的重要性。欧洲药品管理局（EMA）发布了关于临床试验中多重性问题的指南（EMA, 2002）。最近，美国食品药品监督管理局（FDA, 2017）和欧洲药品管理局（EMA, 2017）发布了关于这一通用主题的草案指导文件。这些指南，特别是 FDA 指南，对临床试验中出现的多重性问题以及解决这些问题的统计方法提供了全面的讨论。

### 概述

本章讨论了用于确认性 III 期试验中以解决多重性问题的一大类方法。文献中提出了多种多重性调整方法，以便在具有一个或多个多重性来源的环境中保护第一类错误率。本章描述了常用的多重检验程序（MTPs）及其在 SAS 中的实现。第 5.2 节和 5.3 节讨论了单步 MTP（例如 Bonferroni 程序）以及其改进为数据驱动的步进 MTP（例如 Holm、Hochberg 和 Hommel 程序）。第 5.4 节涵盖了依赖预设假设检验排序的方法，例如固定序列、回退程序和链式程序。第 5.5 节简要回顾了用于多重性调整的参数方法，即 Dunnett 过程及其步进版本。最后，第 5.6 节引入了一类门控程序，这些程序旨在在具有两个或多个多重性来源的临床试验中进行多重性调整，例如在具有多个排序终点和多个剂量-安慰剂比较的试验中。

最近的几篇综述和书籍章节提供了临床试验应用中常用的多重性调整调查。参见 Hochberg and Tamhane (1987)、Hsu (1996)、Dmitrienko et al. (2009)、Bretz et al. (2009)、Westfall and Bretz (2010) 以及 Tamhane (2011)，以获得关于多重比较通用理论和不同类 MTP 的更详细讨论。Westfall et al. (2011) 以及 Dmitrienko and D'Agostino (2013) 提供了带有 SAS 实现示例的 MTP 概述。

本章包含的 SAS 代码和数据集可以在书籍网站获取：`http://support.sas.com/publishing/authors/dmitrienko.html`。

### 族误差率的弱控制和强控制

第一类错误率的概念源于单一假设检验问题。它被定义为假设为真时拒绝该假设的概率。当正在检验多个假设时，第一类错误率的概念可以广义为族误差（FWER），即在所测试假设族中错误地拒绝至少一个真假设的概率。FWER 控制有两种定义：弱控制和强控制。理解意图执行的推断对于选择正确的 FWER 定义和适当的 MTP 至关重要。为了说明，请考虑贯穿第 5.2、5.3 和 5.4 节的以下示例。

### 示例：案例研究 1（高血压剂量试验）

假设进行了一项剂量试验，以比较低剂量、中剂量和高剂量抗高血压药物（标记为 L、M 和 H）与安慰剂（标记为 P）的效果。主要效效变量是收缩压。具有临床意义的收缩压平均下降的剂量将被判定有效。

令 $\mu_P$ 表示安慰剂组收缩压的平均下降。同样，$\mu_L$、$\mu_M$ 和 $\mu_H$ 分别表示低剂量、中剂量和高剂量组收缩压的平均下降。试验中检验以下零假设：

$H_L = {\mu_P - \mu_L \leq \delta\}, H_M = {\mu_P - \mu_M \leq \delta\}, H_H = {\mu_P - \mu_H \leq \delta}$。

其中 $\delta$ 代表相对于安慰剂的临床意义。在优性检验框架下，临床意义设置为 0。

为了测试单个剂量对舒张期血压的影响，我们需要控制无论何种零假设为真、其数量如何，都错误地拒绝任何真实零假设的概率。这被称为族整体错误率（FWER）的**强力控制**。例如，Dunnett (1955) 提出的程序可以用于检验全局零假设，同时提供关于单个剂量与安慰剂比较的信息，即它可以用于检验零假设 $H_L$、$H_M$ 和 $H_H$。Dunnett 过程在预定义的 $\alpha$ 水平下（例如在双侧 $\alpha = 0.05$ 处）从强意义上控制 FWER。假设 $H_L$ 和 $H_M$ 均真实（这意味着 $\mu_P \le \mu_L$ 且 $\mu_P \le \mu_M$），而 $H_H$ 是虚假的（因此 $\mu_P > \mu_H$）。在这种情况下，对 FWER 的强力控制意味着通过 Dunnett 程序错误地拒绝 $H_L$ 或 $H_M$ 的概率将不超过 $\alpha$。

FDA 关于临床试验中多个终点的草案指南（FDA, 2017）强调了 FWER 强力控制在确认性临床试验中的重要性，本章将仅关注在强意义上保持 FWER 的方法。

值得注意的是，文献中还提出了错误决策概率的其他定义。这包括错误发现比例、错误发现率和广义族整体错误率。有关这些定义的更多详尽信息，请参阅 Dmitrienko 等人 (2009)。控制错误发现率或广义族整体错误率的多重检验程序比设计用于保护强意义下 FWER 的程序更具效力，同时也更“宽松”。这些程序仅适用于具有大量零假设的多重性问题，例如大规模遗传学研究。

# 多重检验程序

在过去的 20 到 30 年里，开发了几类多重检验程序（MTPs），它们在临床试验中得到了广泛应用。在特定设定下选择处理多重性的合适方法通常由若干因素驱动，例如可用的临床信息（即关于多重性问题中假设之间的逻辑限制或依赖关系的信息）和统计信息（关于假设检验统计量联合分布的信息）。为了方便审查可用的多重性调整选项，表 5.1 根据临床试验中出现的多重性问题的相关逻辑限制和可用的分布信息，定义了一个基于九类的简单分类方案。

# 表 5.1 常用多重检验程序分类

| 逻辑限制 | 单步法程序 | 数据驱动排序 | 预设排序 |
|---|---|---|---|
| 非参数程序 | Bonferroni | Holm | 固定序列回退 |
| | | | 基于 Bonferroni 的比较 |
| | Simes | Hochberg | NA |
| | Šidák | Hommel | |
| 半参数程序 | | | |
| 参数程序 | Dunnett | 步减式 Dunnett | 参数回退 |

# 逻辑限制

为了提供更多关于临床信息如何在多重性问题中使用的更多信息，表 5.1 显示可以根据逻辑限制定义三类 MTP：依赖于数据驱动排序的单步法程序，以及依赖于预设排序的步进式程序。单步法程序（如 Bonferroni 程序）独立于其他假设检验每个假设。这意味着检验假设的顺序并不重要。相比之下，步进式程序（如 Holm 程序）一次检验一个。结果是，某些假设可能根本不会被检验。步进式程序优于单步法程序的地方在于，它们不会膨胀 FWER。
