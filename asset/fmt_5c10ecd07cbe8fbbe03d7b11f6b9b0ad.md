
`w = 1 / StandardError**2;`

`west = Estimate*w;`

```sas
PROC MEANS NOPRINT; CLASS Parameter; VAR west;

OUTPUT out=sums sum=sumest;

DATA poolest; set sums; IF _TYPE_EQ 1;

poolest = sumest / sum;

poolse = 1 / sqrt(sum);

poolz = poolest / poolse;

poolp = 2*(1) - probnorm(abs(poolz));
```

```sas
/ 打印 poolest 结果 /

PROC PRINT;

VAR Parameter poolse poolz poolp;

RUN;
```

## 程序 8.4 的输出

| Obs | Parameter | poolest | poolse | poolz | poolp |
|---|---|---|---|---|---|
| 1 | b0 | -3.84229 | 0.23478 | -16.3566 | 0.00000 |
| 2 | b1 | -0.42659 | 0.13324 | -3.2016 | 0.00137 |
| 3 | sd | 0.11333 | 0.13715 | 1.4166 | 0.15974 |
| 4 | t2 | 0.50464 | 0.16553 | 3.6795 | 0.00023 |
| 5 | t3 | 0.89581 | 0.19464 | 5.4118 | 0.00000 |
| 6 | t4 | 1.60004 | 0.22543 | 8.2204 | 0.00000 |
| 7 | t5 | 2.44533 | 0.21645 | 11.6682 | 0.00000 |
| 8 | t6 | 2.86478 | 0.23911 | 13.2354 | 0.00000 |
| 9 | t7 | 4.10759 | 0.17118 | 17.0884 | 0.00000 |

## 程序 8.5 跨所有受试者的治疗效性分析：主效应

```sas
/ 分组时间生存分析 -- 所有受试者 -- 所有分位数主效应 /

/* 带有截断的二值协变量随机截距模型 */

PROC MIXED;

PARMS b0=0 b1=0 b2=0 b3=0 b4=0 b5=0 sd=1

t2=1 t3=1.25 t4=1.5 t5=1.5 t6=2 t7=2.5

z=0+b1*btx+ b2*q1+ b3*q2+ b4*q3+ b5*q4 + sd*u;

..更多 SAS 语句..
```

```sas
like = LOG(p);

MODEL surv ~ GENERAL(like);

RANDOM u ~ NORMAL(0,1) SUBJECT=id;

ESTIMATE 'ICC' sd*sd/(((ATAN(1) **2)/6)+sd*sd);

RUN;
```

## 第8章 用于观察性数据分析的两阶段纵向倾向调整 205

## 程序 8.5 的输出

NOTE: GCON 收敛标准已满足。

| 拟合统计 | |
|---|---|
| -2 Log Likelihood | 3203.7 |
| AIC (越小越好) | 3229.7 |
| AICC (越小越好) | 3230.0 |
| BIC (越小越好) | 3277.2 |

## 程序 8.6 跨所有受试者的治疗效性合并：主效应和交互作用

```sas
* 分组时间生存分析 - 所有受试者 - 所有分位数主效应和交互作用 */

/* 带有截断的二值复杂对数对数随机截距模型 */

PROC NLMIXED;

PARMS b0=0 b1=0 b2=0 b3=0 b4=0 b5=0 b6=0 b7=0 b8=0 b9=0 sd=1

t2=-1 t3=1.25 t4=-1.5 t5=1.75 t6=2 t7=-2.25;

z = b0+b1*tx+b2*q1+b3*q2+b4*q3+b5*q4

b6+tx*q1+b7*tx*q2+b8*tx*q3+b9*tx*q4 + sd*u;

like = LOG(p);

MODEL surv ~ GENERAL(like);

RANDOM u ~ NORMAL(0,1) SUBJECT=id;

ESTIMATE 'ICC' sd*sd/(((ATAN(1) **2)/6)+sd*sd);
```

程序 8.6 的输出

NOTE: GCON 收敛标准已满足。

| 拟合统计 | |
|---|---|
| -2 Log Likelihood | 3197.3 |
| AIC (越小越好) | 3231.3 |
| AICC (越小越好) | 3237.7 |
| BIC (越小越好) | 3293.3 |

跨所有受试者的治疗效性合并：主效应和交互作用

带有截断的二值复杂对数对数随机截距模型

NOTE: GCON 收敛标准已满足。

| -2 Log Likelihood | 3197.3 |
| AIC (越小越好) | 3231.3 |
| AICC (越小越好) | 3237.7 |
| BIC (越小越好) | 3293.3 |

跨所有受试者的治疗效性合并：主效应和交互作用

带有截断的二值复杂对数对数随机截距模型

由于提供的原始文本中存在部分重复和格式错乱，译文已根据逻辑进行了清理和对齐，以确保内容通顺。

# 致谢

国家心理健康研究所合作抑郁症研究由以下研究人员目前参与：M.B. Keller, M.D.（主席，普罗维登斯）；W. Coryell（共同主席，爱荷华市）；D.A. Solomon, M.D.（普罗维登斯）；W.A. Schenfler, M.D.（芝加哥）；W. Coryell, M.D.（爱荷华市）；J. Endicot, P.D., A.C. Leon, P.D., J. Long, M.S.W.（纽约）；以及 J. Rice, P.D.（圣路易斯）。其他贡献者包括：H.S. Akiskal, M.D.;J. Fawcett, M.D.;L.J. Jung, P.D.;P.W. Lavori, P.D.;J.D. Maser; T.I. Mueller, M.D.。本手稿已通过合作抑郁症研究出版委员会审查，并获得其认可。本手稿的数据来自国家心理健康研究所（NIMH）抑郁症心理学协作计划——临床研究（Katz and Kramer, 1979）。该计划于1975年启动，旨在调查情绪障碍的社会、遗传、家族和预后方面，是一项关于情绪及相关情感障碍病程的持续、长期的多学科调查。最初的首席专家和首席研究员来自五个学术中心，包括 Gerald Kramer, M.D.（共同主席），Martin Keller, M.D. 和 Robert Shapiro, M.D.（马萨诸塞州总医院，哈佛医学院）；Eli Robins, M.D.;Paul Clayton, M.D.;Theodore Reed 和 Amos Weller, M.D.（华盛顿大学医学院）；Nancy Andreasen, M.D., P.D., 以及 William Coryell, M.D.以及 George Winokur, M.D.（爱荷华大学）；以及 Jan Fawcett, M.D. 和 William Sheftner, M.D.（拉什-普斯比得-圣路加医学中心）。NIMH临床研究分支是协作计划起源和发展的活跃合作者，其中部门主任 Martin M. Katz, P.D. 担任共同主席，Robert Hirschfeld, M.D. 担任计划协调。其他贡献者包括：Crough, M.D.;M.T. Shea, P.D.;R. Gibbons, P.D.;M.A. Young, P.D.以及 D.C. Clark, P.D.。

本研究部分由 NIH 资助项目 MH60447 和 MH49762 支持。

# 参考文献

- Cochran, W. G. 1968. "The effectiveness of adjustment by subclassification in removing bias in observational studies." Biometrics 24: 295–313.
- Drake, C. 1993. "Effects of misspec of the propensity score on estimators of the treatment effect." Biometrics 49: 1231–1236.
- Fleiss, J. L. 1981. *Statistical Methods for Rates and Proportions.* New York: John Wiley & Sons. Hedeker, D., O. Siddigki, and F. B. Hu. 2000. "Random-effects regression analysis of correlated grouped-time survival data." *Statistical Methods in Medical Research* 9: 161–179.
- Katz, M. M., and G. L. Kramer. 1979. "Introduction: overview of the clinical studies program." *The American Journal of Psychiatry* 136(1): 49–51.
- Keller, M. B. 1988. "Undertreatment of depression." *Psychopharmacology Bulletin* 24(1): 75–80.
- Keller, M. B., P. W. Lavori, T. I. Mueller, J. Endicot, W. Coryell, R M. Hirschfeld, T. Shea. 1992. "To recovery, chóng, and levels of psychopathology in depression: A five-year prospective follow-up of 43 subjects." *Archives of General Psychiatry* 49(10):809–816.
- Leon, A. C., and D. Hedeker. 2005. "A mixed-effects quantile-stratified propensity adjustment for effectiveness of.

## 使用 SAS 对观察性健康数据进行分析

意向性治疗分析 (ITT) 最后观察结转法 (LOCF) 或重复测量可能并不适用。

ITT 分析仅根据患者的治疗分配对患者进行分组，并忽略所有关于其他处方或服用的药物的信息。此类研究中，患者的脱落通常通过利用 LOCF 方法来处理。显然，当治疗方案之间存在大量切换时，这种技术并不能直接解决治疗效果的问题。ITT 分析在纵向观察性研究中具有其地位，例如比较政策或治疗策略的研究，在这些研究中，人们主要感兴趣的单个药物的效果（Tunis et al., 2006）。

虽然在治疗中利用重复测量可能提供一种简单的解决方案，但 Hernán 及其同事（2004, 2005）解释说，在存在时间依赖性混杂因素（结果的预测因子和随后的治疗）且这些因素受到先前治疗的影响的情况下，这种方法无法提供具有因果解释的估计（见下文）。例如，任何疾病严重程度的纵向测量可能存在问题，因为它与结果指标相关，可以预测随后的治疗，并可能受到先前治疗的影响。即使治疗在研究基线时是随机的，随时间变化的因果治疗结果最终会导致关键患者特征的失衡。为了处理治疗切换，药物切换忽略了在纵向分析中证明非常有用的标准重复测量（Verbek and Molenbergh, 2000; Mallinckhardt et al., 2003）。这种方法将切换后的数据视为缺失，但显然没有利用药物切换后获得的信息。

在本章中，我们考察边际结构模型 (MSMs) 在纵向观察性数据中的应用。为了解释 MSM 方法的潜在优势，我们必须简要回顾反事实结果和因果效应的概念。我们将遵循 Hernán 及其同事（2002）提供的符号表示。令 `$a$` 表示患者在一段时间内的治疗历史（例如，`$a = \{a(1), a(2), ...,a(t)\}$`，其中 `a(1)` 表示在时间 1 使用的治疗）。患者 `i` 在治疗序列 `a` 下的反事实结果是指如果该患者（尽管可能与事实相反）接受了 `Y_{i,a}(t)`，那么其结果。

每个患者对于其未接受的每种治疗或观察到的结果都有一个反事实结果。在个体层面，如果对于某些时间点 `t` 和治疗模式 `a` 与 `a'`，`Y_{i,a}(t) != Y_{i,a'}(t)`，则认为该治疗对患者的结果具有因果效应。也就是说，治疗模式根据所接受的治疗而不同。在群体层面，如果所有患者遵循特定治疗模式（例如 `a`）的平均结果与所有患者遵循另一种治疗模式（例如 `a'`）的平均结果不同（即对于某些时间点和治疗方案，`E[Y_a(t)] != E[Y_{a'}(t)]`），则认为该治疗具有因果效应。

Robbins 及其同事（1999）证明，在本文讨论的一系列假设下，MSMs 在存在治疗变化、时间依赖性混杂因素和随机缺失脱落的情况下，能够产生对平均因果治疗效应的一致性估计。在本章中，我们首先描述 MSM 方法（第 9.2 节），然后对一项纵向精神分裂症研究进行 MSM 分析（第 9.3 节）。文中提供了 SAS 代码，并讨论了 SAS 输出，以便读者理解分析的实现并修改代码以供自己使用。Faire 及其同事（2007）还使用多种方法（包括 MSM）总结了该研究的数据。文献中 MSM 的其他应用包括 Hernán 及其同事（2000, 2002）、Ko 和同事（2003）、Brumback 及其同事（2004）以及 Cole 及其同事（2005），他们检查了 HIV 患者的事件时间结果；Bodnar 及其同事（2004）、Yamaguchi 和 Ohashi（2004a 和 2004b）、Mortimer 及其同事（2005）、Suarez 及其同事（2006）、Peterson 及其同事（2007）以及 Vansteeland 及其同事（2009），他们评估了其他应用。

## 9.2 MSM 方法论

MSM 分析是一种加权重复测量方法——将治疗作为随变化的协变量。基于逆概率治疗加权控制了时间依赖性混杂因素，并本质上建立了一个在时间不变量和随变化协变量上达到平衡的伪群体，允许使用标准的重复测量模型进行因果比较。权重也可以调整以包含对缺失数据的更新——在随机缺失（MAR；缺失数据可能依赖于已观测但未观测的指标）和完全随机缺失（MCAR；缺失数据不依赖于已观测或未观测的指标）下有效。

进行 MSM 分析是一个两的过程。首先，为每个观测值（患者就诊）估计两个权重：一个用于治疗选择，另一个用于调整中断。这些估计权重的完成可以包含时间独立和时间依赖的因素。Hernán（2002）建议使用稳定权重（stabilized weight），我们使用稿中的符号（此处用于治疗选择）：

```
$SW = \prod_{k=0}^{t} \frac{f[A(k-1),V]}{f[A(k)|A(k-1),L(k)]}$
```
