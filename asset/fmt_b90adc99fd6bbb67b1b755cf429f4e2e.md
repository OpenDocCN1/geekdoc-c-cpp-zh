
# 第9章 使用边际结构模型进行纵向观察数据分析

其中 `$A(k)$` 代表时间 $k$ 的治疗，$A(1)$ 代表在时间 1 使用的治疗。患者 $i$ 在治疗序列 $a$ 下的反事实结果是指如果该患者（尽管可能与事实相反）接受了 $Y_{i,a}(t)$，那么其结果。

每个患者对于其未接受的每种治疗或观察到的结果都有一个反事实结果。在个体层面，如果对于某些时间点 $t$ 和治疗模式 $a$ 与 $a'$，$Y_{i,a}(t) \neq Y_{i,a'}(t)$，则认为该治疗对患者的结果具有因果效应。也就是说，治疗模式根据所接受的治疗而不同。在群体层面，如果所有患者遵循特定治疗模式（例如 $a$）的平均结果与所有患者遵循另一种治疗模式（例如 $a'$）的平均结果不同（即对于某些时间点和治疗方案，$E[Y_a(t)] \neq E[Y_{a'}(t)]$），则认为该治疗具有因果效应。

Robbins 及其同事（1999）证明，在本文讨论的一系列假设下，MSMs 在存在治疗变化、时间依赖性混杂因素和随机缺失脱落的情况下，能够产生对平均因果治疗效应的一致性估计。在本章中，我们首先描述 MSM 方法（第 9.2 节），然后对一项纵向精神分裂症研究进行 MSM 分析（第 9.3 节）。文中提供了 SAS 代码，并讨论了 SAS 输出，以便读者理解分析的实现并修改代码以供自己使用。Faire 及其同事（2007）还使用多种方法（包括 MSM）总结了该研究的数据。文献中 MSM 的其他应用包括 Hernán 及其同事（2000, 2002）、Ko 和同事（2003）、Brumback 及其同事（2004）以及 Cole 及其同事（2005），他们检查了 HIV 患者的事件时间结果；Bodnar 及其同事（2004）、Yamaguchi 和 Ohashi（2004a 和 2004b）、Mortimer 及其同事（2005）、Suarez 及其同事（2006）、Peterson 及其同事（2007）以及 Vansteeland 及其同事（2009），他们评估了其他应用。

## 9.3 示例：模拟精神分裂症试验的 MSM 分析

### 9.3.1 研究描述

为了说明 MSM 分析的实现，使用了基于一项精神分裂症患者药物有效研究的模拟数据。随后是实际研究设计的简要描述，尽管读者可以参考 Tunis 和同事（2006）获取详细信息。这是一项针对精神分裂症、情感情感障碍或精神分裂样障碍患者的一期研究，他们被随机分配到三种

## 216 使用 SAS 分析观察性健康数据

### 表 9.1（续）

| 变量 | 描述 | 变量 | 描述 |
|---|---|---|---|
| `TRTA` | 访视期间处于 Tr A | | |
| `TRTB` | 访视期间处于 Tr B | | |
| `TRTC` | 访视期间处于 Tr C | | |
| `TRT` | 权重计算期间的治疗 | | |

### 9.3.2.2 推断权重的计算

进行 MSM 分析的第一步是估计选择权重和删失权重 `SW`（使用 9.2 节中的公式）。对于估计治疗选择权重，使用 `PROC LOGISTIC` 配合 `LINK=GLOG` 选项对分子和分母实现了多项模型（见程序 9.1）。治疗是两个模型的因变量，并使用 GLOGIT 链接，是因为每次访视的治疗选择有五个潜在结果（三种个体治疗、无治疗和一种联合治疗）。`LOGISTIC` 过程输出包含治疗选择的预测概率（数据集 `PREDTRT0` 和 `PREDTRT1`）。除了治疗外，此模型还包含了以下时间变化的协变量：

- BPRS 总分
- 全局功能评估 `GAF`
- 事件（是否存在至少一次中度或严重的不良事件）
- 住院

选择这些变量是为了涵盖症状严重程度、功能状态、耐受性和资源利用等领域。包含在模型中的与时间不相关变量包括年龄、性别、种族以及每个时间依赖变量的基线值。可以使用宏变量在代码开始处输入所有模型参数；但我们选择通过在 `LOGISTIC` 语句中直接显示模型来简化对过程的理解。此外，为了简化输出，抑制了权重模型的输出。然而，人们可以轻松移除限制，以更详细地评估权重模型。

使用 `PROC GENMOD` 通过逻辑回归计算删失的估计权重（见程序 9.1）。删失权重模型的因变量与治疗选择权重模型相同——由于数据结构的原因，删失是前瞻性的（患者是否返回进行随访访视？），这相对于治疗（上一个阶段分配了什么治疗方案？），因此时间变化的协变量偏移了一个访视。此处使用了 logit 链接函数，因为结果是二项的。在仅评估两个治疗组的研究中，`GENMOD` 方法可用于两种权重的计算。

多项回归和逻辑回归权重模型的部分输出位于程序 9.1 的输出中。先前的治疗是当前治疗最强的预测因子。所有时间变化的协变量都不是治疗变化的强预测因子——这表明数据中随时间变化的治疗选择偏差可能并不特别奇怪。与之前的治疗相比，较高的（时间变化的）症状严重程度被发现是删失的预测因子。症状较多的患者更有可能退出研究。

#### 程序 9.1 计算治疗选择权重和删失权重

* 此部分代码计算治疗选择权重删失权重。这通过 4 个步骤完成：
1) 多项模型计算治疗选择权重的分子；
2) 多项模型计算治疗选择权重的分母；
3) 二项模型计算删失调整权重的分子；
4) 二项模型计算删失调整权重的分母。

```sas
/ 治疗选择权重：分子计算
（仅使用基线协变量进行治疗的概率） /
PROC LOGISTIC DATA = INPSDS;
CLASS VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP BEVNT
MODEL TR = VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP
BEVNT AGERS BGAF BPRPS
/LINK=GLOG;
OUTPUT OUT=PRETRT0(WHERE=(TR_=LEVEL)) PRED=PRETRT0;
```

```sas
/ 治疗选择权重：分母计算
（使用基线协变量和时间依赖协变量进行治疗的概率） /
PROC LOGISTIC DATA = INPSDS;
CLASS VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP BEVNT
PRIEVNT HOSP;
MODEL TR = VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP
BEVNT AGERS BGAF BPRPS HOSP PRIBPRS GIFAGC
/LINK=GLOG;
OUTPUT OUT=PRETRT1(WHERE=(TR_=LEVEL)) PRED=PRETRT1;
```

```sas
/ 删失调整权重：分子计算
（仅使用基线协变量进行删失的概率） /
ODS LISTING EX OBSTATS;
PROC GENMOD DATA = INPSDS;
CLASS PATSC VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
EVNT HOSP;
MODEL CFLAG = VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
AGERS BGAF BPRPS
/DIST = BIN LINK = LOGIT TYPE3 OBSTATS;
REPEATED SUBJECT = EMSC / TYPE = EXCH;
ODS OUTPUT STATS = PRECENO(RENAME=(PRE=PRECENO));
ODS LISTING SELECT ALL;
```

```sas
/ 删失调整权重：分母计算
（使用基线协变量和时间依赖协变量进行删失的概率） /
ODS LISTING EXCLUDE OBSTATS;
PROC GENMOD DATA = INPSDS;
CLASS PATSC VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
EVNT HOSP;
MODEL CFLAG = VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
EVNT HOSP AGERS BGAF BPRPS
/DIST = BIN LINK = LOGIT TYPE3 OBSTATS;
REPEATED SUBJECT = PATSC / TYPE = EXCH;
ODS OUTPUT STATS = PRECENO(RENAME=(PRE=PRECENO));
ODS LISTING SELECT ALL;
```

## 使用 SAS 分析观察性数据

### 程序 9.1 权重分母模型输出：治疗权重

Type 3 分析

| 效应 | DF | 卡方 | Pr > ChiSq |
|---|---|---|---|
| VIS | 16 | 124.2473 | .0001 |
| THERAPY | 8 | 11.8349 | .1587 |
| PRTRTA | 4 | 229.7185 | .0001 |
| PRTRTB | 4 | 100.6526 | .0001 |
| PRTRTC | 4 | 269.8819 | .0001 |
| GENDER | 4 | 3.3971 | .4937 |
| ORIGIN2 | 8 | 10.4911 | .2322 |
| BOSP | 4 | 0.4611 | .9972 |
| BEVNT | 4 | 3.0900 | .5429 |
| AGEYRS | 4 | 1.4773 | .8359 |
| BGAF | 4 | 1.9736 | .7406 |
| BBPRS | 4 | 2.2390 | .6919 |
| PRIENT | 4 | 7.5905 | .1078 |
| PR1BSP | 4 | 4.6487 | .3253 |
| PR1BPRS | 4 | 2.5962 | .6275 |
| PR1GAFC | 4 | 2.5983 | .6271 |

### 权重分母模型：删失权重 GEE Type 3 分析

| 来源 | DF | 方 | Pr > ChiSq |
|---|---|---|---|
| VIS | 4 | 13.21 | .0103 |
| THERAPY | 2 | 9.04 | .0109 |
| TRTA | 2 | 3.95 | .0468 |
| TRTB | 2 | 3.74 | .0532 |
| TRTC | 1 | 0.39 | .5356 |
| GENDER | 2 | 0.15 | .6964 |
| ORIGIN2 | 2 | 0.99 | .6087 |
| BOSP | 1 | 0.88 | .3473 |
| BEVNT | 1 | 0.93 | .3338 |
| EVNT | 1 | 0.61 | .4338 |
| ROSS | 1 | 0.05 | .8163 |
| AGEYRS | 1 | 4.89 | .0220 |
| BGAF | 1 | 0.04 | .8431 |
| BPRS | 1 | 0.67 | .4115 |
| BBPRS | 1 | 12.21 | .0005 |
| GAFC | 1 | 0.32 | .5726 |

为了产生此分析中每个观测值（患者访视）的总体权重，根据 SAS 9.2 节（程序 9.2）中的公式，在 DATA 步骤中累积乘以选择和删失的概率权重。在 sas 代码中，SQL 过程从治疗选择和权重模型的四个输出集（`PREDTR0`、`PREDTR1`、`PREDCENS0` 和 `PREDCENS1`）收集数据并产生加权值。变量 `SWAT` 是 `SW` 的最终估计值。程序的输出以箱线图格式显示所有患者访视的最终权重分布。平均值接近 1（平均值=1.002，SD=0.1555），符合权重平均值的预期，且箱线图中没有明显的离群值。

#### 程序 9.2 合并程序 9.1 的输出

* 此部分代码执行必要的步骤，合并权重模型（程序 9.1）的输出，以便计算分析数据集中每个观测值的单个调整值（稳定权重）。随后是生成最终权重摘要的代码。

```sas
PROC SQL;
/* 治疗的概率比 */
CREATE TABLE PREDTTR
SELECT *, PREDTT0/PREDTT1 AS PREDTTR
FROM PREDTT1
NATURAL FULL JOIN
PREDTT0 (KEEP=PATSC VIS PREDTT0)
ORDER PATSC, VIS;
/* 删失的概率比 */
CREATE TABLE PREDCEN
SELECT *, PREDCEN0/PREDCEN1 AS PREDCEN
FROM (SELECT INPUT(PATSC, BEST.) AS PATSC, INPUT(VIS, BEST.) AS VIS,PREDCEN0 FROM PREDCEN0)
NATURAL FULL JOIN
(SELECT INPUT(PATSC, BEST.) AS PATSC, INPUT(VIS, BEST.) AS VIS,PREDCEN1 FROM PREDCEN1)
ORDER PATSC, VIS;
QUIT;
```

```sas
/*计算稳定权重 */
PROC SORT DATA=INPADS OUT=WEIGHTS;
BY PATSC VIS;
RUN;
```

```sas
DATA WEIGHTS;
MERGE WEIGHTS PREDTTR PREDCEN;
BY PATSC VIS;
VWT=PREDTTR*PREDCEN;
IF FIRST.PATSC THEN STABWT=VWT;
ELSE STABWT=VWT*;
RETAIN DUM;
DROP DUM;
DUM=STABWT;
RUN;
```

```sas
/*权重诊断图*/
DATA GRPH;
SET WEIGHTS;
IF VIS = 3 THEN MONTH = 0.5;
IF VIS = 4 THEN MONTH = 2;
IF VIS = 5 THEN MONTH = 5;
IF VIS = 6 THEN MONTH = 8;
IF VIS = 7 THEN MONTH = 12;
IF MONTH = 0.5 DELETE;
```
```sas
PROC SORT DATA = GRPH;
BY MONTH;
RUN;
```

# 220 使用 SAS 分析观察性数据

```sas
ODS RTF FILE="%SYFSUNC(PATHNAME (WORK)) \FIG1.RTF";
FILENAME FIGURE="%SYFSUNC(PATHNAME (WORK)) \SASGRAPH.EMF";
OPTIONS RESET=ALL TARGET=ASEMF DEVICE=ASEMF FTEXT=DUPLEX HEXT=.75
CBACK=WHITE MAX=6IN PIXELS=120 YMAX=5IN PIXELS=1000
GSNAME=FIGURE GSFMODE=REPLACE;
SYMBOL1 COLOR=BLACK INTERPOL=JOIN
WIDTH=2 VALUE=SQUARE
HEIGHT=1;
AXIS1 MINOR = NONE COLOR = BLACK LABEL=("稳定后体重") ANGLE=90
ROTATE=0;
PROC BOXPLOT DATA=GRPH;
PLOT STWAB*MONTH / CFRAME=WHITE
CBOXES=DAG
CBFILL=WHITE
VAXIS=AXIS1;
TITLE "访视权重体重值摘要";
TITLE2 "箱线图：最小值、第一四分位数、中位数、第三四分位数、最大值；
方块：均值)";
RUN;
GOPTIONS RESET=ALL;
ODS RTF CLOSE;
```

# 程序 9.2 的输出

![](img/fe9ff008f88baacd415148b0b25dd58c_234_0.png)

# 第 9 章 使用边际结构模型分析纵向观察性数据 221

### 9.3.2.3 治疗效应分析模型

MSM 分析的最后一步是使用广义估计方程（`PROC GENMOD`——见程序 9.3）和可交换相关矩阵的加权重复测量模型来估计因果治疗效应。基线 BPRS 总分是分析模型中的因变量。分析模型中的自变量为研究中心、年龄、性别、种族、基线 BPRS、访视、随时间治疗以及治疗与访视的交互。`PROC GENMOD` 中的 `WEIGHT` 语句结合了概率加权以估计因果治疗效应。`PROC GENMOD` 中使用的 `ESTIMATE` 语句将个体治疗合并，并生成了不同组的估计均值（而非复合个体组）。这部分代码在许多应用中并非必要。程序 9.3 的输出显示了最终模型结果的摘要，以及一个显示最小二均值的图，图中显示治疗组（合并后的治疗 A 和 B）相对于对照组具有统计学上的显著差异，在 1 年后 BPRS 变化的平均差异为 .1 [0.4, 3.2]，p=.015。尽管差异在数值上有所增加，但治疗与访视的交互在统计学上并不显著（p=.158）。

#### 程序 9.3 运行最终分析模型
