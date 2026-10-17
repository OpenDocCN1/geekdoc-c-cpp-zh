
| 性 0 vs 1 | 1.111 | 0.528 2.342 |

| 配偶 是vs否 | 0.875 | 0.471 1.623 |

| 就业 是vs否 | 1.330 | 0.719 2.462 |

| 年龄 | 0.981 | 0.960 1.003 |

| phqnl | 0.919 | 0.868 0.973 |

分析的下一步是根据预先选择的倾向模型评估平衡性，并在评估结局变量之前进行任何必要的调整以改善平衡。然而，由于我们正在演示倾向方法的使用，为了简单起见，我们首先展示使用每种方法的预选模型进行分析。然后进行倾向调整评估和敏感性分析。

要通过倾向评分分层来估计治疗效应，可以为每个五位数估计治疗效应的回归模型，并将五个估计值合并为一个。尽管如此，如果结局是二元的（如缓解），可以使用 Mantel-Haenszel 方法估计合并值。使用 `PROC FRE`（参见程序 2.3）来获得按倾向评分分层的缓解治疗效应差异。

使用了两种方法通过回归调整倾向评分来估计治疗效应。首先，拟合了一个以因变量和倾向评分五位数自变量的逻辑回归模型。拟合了相同的模型，但将倾向评分作为连续变量，而不是倾向评分的分类变量（五位数）。这两个模型是使用 `PROC LOGISTIC`（参见程序 2.3）拟合的。

程序 2.3 的输出显示了未调整的缓解治疗效应比值比 (`ORs`)，以及通过呈现的三种倾向评分方法相应的估计 `OR`。一旦通过倾向评分估计考虑了基线不平衡，未调整分析中治疗 A 优于 B 的明显优势就消失了。如表 2.3 所示，来自不同倾向评分的三个治疗效应估计高度一致。

## 34 使用 SAS 分析观察性护理数据

## 表 2.3 估计比值比摘要

| 比值比 | 95% CI | P 值 |

|---|---|---|

| 未调整 | 1.89 | (1.06, 3.36) | .030 |

| PS 调整 | 1.50 | (0.82, 2.75) | .178 |

| PS 回归（分类） | 1.54 | (0.83, 2.86) | .173 |

| PS 回归（连续） | 1.44 | (0.78, 2.65) | .247 |

每个情况下还评估了治疗与倾向评分之间的交互作用。尽管组间差异存在很大，但这些差异在统计学上并不显著（p 值 > 0.10）。Karth 等同事（2006）提供了当治疗效应随倾向变化时需要考虑的问题的示例。

## 程序 2.3 计算治疗效应

```sas
* 这部分代码计算 1) 未调整的治疗效应，
2) 按倾向评分五位数分层的治疗效应， 3) 通过回归调整倾向评分五位数的治疗效应，以及 4) 通过回归调整将倾向评分作为连续协变量的治疗效应

/* 未调整的治疗效应*/ 
TITLE 'UNJUSTED ESTIMATE',
PROC LOGISTIC DATA-ADOS3;
CLASS TX;
MODEL REMISSION = TX;
RUN;
```

```sas
* 按倾向评分分层计算的治疗效应*/
TITLE 'STRATIFY ON PROPENSITY SCORES ESTIMATE'
PROC FREQ DATA-ADOS3;
TABLE QUINTLES_PS*TX*REMISSION / NOCHH;
RUN;
```

```sas
* 通过回归调整倾向评分五位数的治疗效应*/
TITLE 'REGRESSING FOR QUINTLES OF PROPENSITY SCORES ESTIMATE',
PROC LOGISTIC DATA-ADOS3;
CLASS TX QUINTLES_PS;
MODEL REMISSION = QUINTLES_PS;
RUN;
```

```sas
* 通过回归调整倾向评分作为连续变量的治疗效应*/
TITLE 'REGRESSING FOR PROPENSITY SCORES AS A CONTINUOUS COVARIATE',
PROC LOGISTIC DATA=ADOS3;
CLASS TX;
MODEL REMISSION = TX;
RUN;
```

## 第 2 章 倾向评分分层与回归 35

## 程序 2.3 的输出

| 未调整估计 响应分布 | | |

| 有序值 | 缓解 | 总频数 |

|---|---|---|

| 1 | 是 | 105 |

| 2 | 否 | 87 |

建模概率为 remission='Yes'。

类型 3 效应分析

| 效应 | DF | 卡方值 | Pr > ChiSq |

|---|---|---|---|

| tx | 1 | 4.6882 | 0.0304 |

比值比估计

| 效应 | 点估计值 | 95% Wald 置信区间 |

|---|---|---|---|

| tx A vs B | 估计 | 1.889 | 1.062 3.359 |

倾向评分分层估计 ochran-Mantel-Haenszel 统计量（基于评分）

| 统计量 备择假设 DF 值 | 95% 置信 概率 |

|---|---|---|---|

| 1 非零 | 1 | 1.8177 | .1776 |

| 2 行均差异 | 1 | 1.8177 | .1776 |

| 3 关联 | 1 | 1.8177 | .1776 |

共同相对风险估计（行1/行2)

| 研究方法类型 | 值 | 95% 置信 |

|---|---|---|

| 个例对照（比值比） Mantel-Haenszel Logit | 1.5036 | 0.8215 2.7520 |

| | | 1.5187 | 0.8063 2.8660 |

倾向评分五位数回归估计

| 有序值 | 缓解 | 总频数 |

|---|---|---|

| 1 | 是 | 105 |

| 2 | 否 | 87 |

建模概率为 remission='Yes'。

类型 3 效应分析

| 效应 | DF | 卡方值 | Pr > ChiSq |

|---|---|---|---|

| tx | 1 | 1.8561 | 0.1731 |

| quintiles_ps | 4 | 16.3637 | 0.0026 |

（续）

## 36 使用 SAS 分析观察性护理数据

## 程序 2.3 的输出（续）

| | 比值比 | 点估计值 | 95% Wald 置信区间 |

|---|---|---|---|

| tx A vs B | 1.539 | 0.828 2.863 |

| quintiles_0 ps vs 4 | 0.186 | 0.067 0.518 |

| quintiles_1 ps vs 4 | 0.198 | 0.074 0.535 |

| quintiles_2 ps vs 4 | 0.608 | 0.222 1.667 |

| quintiles_3 ps vs 4 | 0.446 | 0.166 1.197 |

## 第2章 倾向性评分分层与回归

在每个倾向性评分分层内。输出中提供了基线 PHQ1 变量的箱线图。

Macro `GEN2` 为未调整的样本（不含倾向性评分）生成标准化差异，并按倾向性评分平均值（调整后）以及每个倾向性评分分层内进行平均处理。标准化差异被输出到数据集中，以便能够方便地创建标准化差异的摘要、列表或箱线图。在五个未调整的标准化差异中，有四个大于 0.10，而所有跨分层平均的标准化差异都很较小。然而，倾向性评分分层显示出大于 0.10 的标准化差异。虽然这些差异并不比随机性产生的差异大（如双向模型所示），但这表明了在每个分层内使用较小样本进行预测和平衡的困难性。倾向性评分的平衡并不意味着每个个体协变量的平衡。由于如此，我们检查了倾向性模型，包括交互作用以及项的删除。一个具有显著双向交互作用以及涉及 PHQ1 的双向交互作用的模型减少了不平衡，尽管在分层 1 和 5 中仍有注意到。最终，PHQ1 以外的变量似乎与结果无关，各种模型并未影响结果。一种敏感性分析是考虑倾向性评分匹配以获得更好的平衡（第 3 章）。

Macro `GEN3` 计算加权标准化差异，用于在倾向性评分回归中评估协变量的平衡。来自 `PROC GENMOD` 的输出数据集用于根据所有协变量的结果来汇总数据。两个 PHQ1 的标准化差异略大于 0.1，表明可能需要进一步评估。再次将这些变量加入回归模型作为敏感性分析，结果并没有对最终结果产生任何影响（`OR=1.47`; p<.235）。

对于此分析，我们假设在三个月的研究期间，协变量值没有缺失数据、没有脱落，且没有治疗方案的变化（从 A 到 B 或从 B 到 A）。第 5 章涵盖了在协变量数据缺失的情况下倾向性评分的计算，第 8 章至第 11 章讨论了处理纵向自然主义数据中发现的问题的方法。

结论是，各种敏感性分析均支持最初的分析结果。因此，虽然未调整的结果提示了治疗差异，但倾向性调整技术揭示了治疗 A 和 B 在缓解率上的差异在统计学上并不显著。

## 程序 2.4 评估倾向性评分产生的平衡

```sas
/ 此部分代码通过以下方式评估倾向性评分产生的平衡：
1) 通过箱线图总结倾向性评分的分布
```

```sas
/ ** 2) 通过箱线图评估不同治疗组和倾向性评分五分位数之间
协变量的平衡 **/
```

## 使用 SAS 进行观察性医疗保健分析

```sas
PROC FORMAT;
VALUE BPF
  1 = 'Q1-A'
  2 = 'Q1-B'
  3 = 'Q2-A'
  4 = 'Q2-B'
  5 = 'Q3-A'
  6 = 'Q3-B'
  7 = 'Q4-A'
  8 = 'Q4-B'
  9 = 'Q5-A'
  10 = 'Q5-B';
RUN;

DATA ADOS4;
  SET ADOS3;
  LABEL BP='QUANTILE-TREATMENT';
  FORMAT BP*;

  IF TX=1 AND QUANTILES=0 THEN BP=1;
  ELSE IF TX=0 AND QUANTILES=1 THEN BP=2;
  ELSE IF TX=1 AND QUANTILES=1 THEN BP=3;
  ELSE IF TX=0 AND QUANTILES=2 THEN BP=4;
  ELSE IF TX=1 AND QUANTILES=2 THEN BP=5;
  ELSE IF TX=0 AND QUANTILES=3 THEN BP=6;
  ELSE IF TX=1 AND QUANTILES=3 THEN BP=7;
  ELSE IF TX=0 AND QUANTILES=4 THEN BP=8;
  ELSE ELSE BP=10;
RUN;

PROC SORT DATA=ADOS4;
  BY BP;
RUN;

TITLE '按五分位数和治疗分布的倾向性评分';
PROC BOXPLOT DATA=ADOS4;
  PLOT PS*BP;
RUN;

TITLE '按五分位数和治疗分布的基线 PHQ1';
PROC BOXPLOT DATA=ADOS4;
  PLOT PHQ1*BP;
RUN;
```

```sas
********************************************************************************************************************************;;
* MACRO GEN1 通过双向模型方法评估倾向性 *;
* 分层调整产生的基线 *;
* (Rosenbaum and Rubin, 1984)。生成一个包含治疗效应 *;
* 测试统计量和 p 值的数据集，按分层的 *;
* 治疗效果。 *;
* 输入变量： *;
  VAR 用于正态分布协变量，BIN 用于二元变量 *;
  DST 用于正态分布 NOR，BIN 用于二元变量 *;
  LNK 用于正态分布的 ID，LOGIT 用于二元变量 *;
********************************************************************************************************************************;
```

```sas
%MACRO GEN1(VAR, DST, LNK);
```

```sas
* 使用 GENMOD 运行主效应和 ps 调整模型，
将参数估计值输出到数据集以进行编译；
PROC GENMOD DATA = ADOS &DESCENDING;
CLASS TX;
MODEL &VAR = TX / &DST LINK = &LNK TYPE3;
ODS OUTPUT TYPE3 = 'TESTING FOR COVARIATE BALANCE: WITHOUT PS';
TITLE3 'VAR:&VAR';
PROC GENMOD DATA = ADOS &DESCENDING;
CLASS TX QUINTILE PS;
MODEL &VAR = TX QUINTILE_PS*QUINTILE_PS / &DST LINK = &LNK TYPE3;
... (此处代码逻辑一致，未翻译以遵循要求)
...
```

```sas
MEAN B2 = MAX(B2,.05); MEAN B2 = MIN(B2,.95);
IF &BURY = 1 THEN SDP = SQRT((MEAN_A2*(1-A2)) +
MEAN B2*(1-B2)) / 2);
STDDIF_UNADJ = MN_DIFF / SDP;
OVAR = &VAR;
KEEP DUMMY MN_DIFF SDP STDDIF_UNADJ;
```

```sas
* 使用 PROC SUMMARY 为每个倾向分层生成汇总统计量，并使用 STRAT 宏计算每个层的标准化差异 *;
PROC SORT DATA = ADOS3; BY QUINTLES_PS; RUN;
PROC SUMMARY DATA = ADOS3;
BY QUINTLES_PS;
CLASS TX;
VAR &VAR;
OUTPUT OUT=PSSTAT MEAN=MN STD=SD N=NUM;
```

```sas
DATA PSSTAT;
SET PSSTAT;
IF TX = '' THEN DELETE;
%STRAT(PSSTAT,SD0,1); RUN;
%STRAT(PSSTAT,SD1,1); RUN;
%STRAT(PSSTAT,SD2,2); RUN;
%STRAT(PSSTAT,SD3,3); RUN;
%STRAT(PSSTAT,SD4,4); RUN;
```

```sas
DATA MERG;
MERGE SD0 SD1 SD2 SD3 SD4;
BY DUMMY;
ADJ_DIFF = (MN_DIFF_0 + MN_DIFF_1 + MN_DIFF_2 + MN_DIFF_3
+ MN_DIFF_4) / 5;
```

```sas
* 创建包含未调整、调整后以及每个五分位数方法的标准化差异的最终集。这里使用了未调整的 SD，而不是跨层的合并内 SD，以便与未调整的标准化差异进行直接比较。 *;
DATA FINAL &VAR;
MERGE MERG SSSTAT;
BY DUMMY;
STDDIF ADJ = ADJ_DIFF / SDP;
KEEP OVAR STDDIF_UNADJ STDDIF ADJ STDDIF_0 STDDIF_1
STDDIF_2 STDDIF_3 STDDIF_4;
```

```sas
* 通过运行宏和 GEN2 计算每个协变量的标准化差异，并将结果编译到单个数据集中汇总。 *;
%GEN2(GENDER,1); RUN;
%GEN2(SPOUSE,1); RUN;
%GEN2(WORK,1); RUN;
%GEN2(AGE,0); RUN;
%GEN2(PHQ1,0); RUN;
```

## 第 2 章 倾向评分分层与回归

```sas
DATA FINAL;
SET GENDER FINAL SPOUSE FINAL_WORK FINAL_AGE
FINAL_PHQI;
PROC PRINT DATA = FINAL;
VAR OVAR STDDIFF UNADJ STDDIFF_ADJ STDDIFF_0 STDDIFF_1
STDDIFF_2 STDDIFF_3 STDDIFF_4;
TITLE 'PS 调整前的标准化差异
(STAND UNADJ)，PS 调整后的 ';
TITLE 2 '跨层平均值调整
(STAND ADJ)，以及每个 PS 层内的调整 ';
TITLE 3 '五分位数 (STDDIFF_0 ... STDDIFF_4)'; RUN;
```

```sas
****************************************************************
* MACRO GEN3 评估由倾向评分产生的平衡；
* 用于倾向回归分析的评分。
* 产生的加权标准化差异 (Austin, 2007a) 是；
* 为给定的协变量生成的。
* 输入变量：
* 待评估的 DVR
* BNR - 二分类变量输入 1，连续变量输入 0
* DST - 正态分布输入 NOR，二分类变量输入 BIN
* LNK - 正态分布输入 ID，二分类变量输入 LOGIT。
****************************************************************
```

```sas
@MACRO GEN3(VAR, BNR, DST, LNK)
运行双向模型并输出参数估计\PROC GENMOD DATA = ADOS3;
CLASS TX;
MODEL &XVAR = TX PS * PS / DIST = &LNK TYPE3;
LSMEANS TX // DIFF;
ODS OUTPUT MODELFIT = TEST11;
ODS OUTPUT TESTFIT = TEST;
TITLE 2 '协变量平衡性测试：带有 PS'; RUN;
```
