
```
/* 此代码使用加权重复测量方法运行最终分析模型。结果使用 PROC GPLOT 以图形形式展示.*/
/*最终分析模型*/
PROC GENMOD DATA = WEIGHTS;
CLASS PATISC GENDER ORIGIN2 INSC TRIS;
WEIGHT STABWT;
MODEL CAVAR = INVAS BVAR VIS AGERS GENDER ORIGIN2 TRIS VISTRT
/ DIST=NONNORMAL LINK=ID TYPE3;
REPEATED SUBJECT = PATSC / TYPE=EXCH;
LMEANS TRIS*TRT / PDIFF;
ESTIMATE 'A*B VS C';
TRT 0 .5 -1 0;
ESTIMATE 'A*B VS C AT VIS 3'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A*B VS C AT VIS 4'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .5 -1 0;
ESTIMATE 'A*B VS C AT VIS 5'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .50 0;
ESTIMATE 'A*B VS C AT VIS 6'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
;
 'A*B VS C VS VIS 7'
'T 0 5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .5 -1 0;;
ODS OUTPUT LMEANS=LMEANS;
RUN;
```

# 222 使用 SAS 分析观察性健康数据

```
/*最终模型的 LS MEANS2 图绘制*/
DATA LSMEANS;
SET LSMEANS;
WHERE TRIN IN ('A ', 'B');
IF TRIN IN ('A ', 'B') THEN TR2='A+B';
ELSE TR2='C';
RUN;

PROC SQL;
CREATE TABLE LSMEANS AS
SELECT TR2, VIS, MEAN(ESTIMATE) AS ESTIMATE
FROM LSMEANS
GROUP BY TR2, VIS;
QUIT;

ODS RTF FILE="%SYFSUNC(PATHNAME (WORK)) \FIG2.RTF";

FILENAME FIGURE="%SYFSUNC(PATHNAME (WORK)) \SASGRAPH.EMF";

OPTIONS RESET=ALL TARGET=ASEMF DEVICE=ASEMF FTEXT=DUPLEX HEXT=.75
CBACK=WHITE MAX=6IN PIXELS=120 YMAX=5IN PIXELS=1000
GSNAME=FIGURE GSFMODE=REPLACE;

AXIS1 MINOR = NONE COLOR = BLACK LABEL=(ANGLE=90 ROTATE=0 "BPRS 总变化");
SYMBOL I=JOIN W=2 C=SQUARE;
SYMBOL II=JOIN W=2 C=CIRCLE;

PROC DATA=LSMEANS;
PLOT ESTIMATE*VIS=TRT / VAXIS=AXIS1;
TITLE "基线估计均值";
LABEL VIS="访视";
LABEL TRT="治疗";
RUN;
ODS RTF CLOSE;
```

# 第 9 章 使用边际结构模型分析纵观察数据 223

程序 9.3 的输出

| 源 | DF | 卡方 | Pr > ChiSq |
|---|---|---|---|
| INSVC | 19 | 84.25 | <0001 |
| BAVAR | 1 | 71.12 | <0001 |
| VIS | 4 | 37.69 | <0001 |
| AGEYRS | 1 | 0.80 | .3735 |
| GENDER | 1 | 0.09 | .7624 |
| ORIGIN2 | 2 | 0.86 | .6500 |
| TRT | 4 | 11.70 | .0197 |
| VIS*TRT | 16 | 21.57 | .1576 |
| 对比估计 结果 | | 标准误 | Alpha | 置信限 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| A+B VS C | -1.7852 | 0.7321 | 0.05 | -3.2201 | -0.3504 | 5.95 | .0147 |
| A+B VS C AT VIS 3 | -0.7336 | 0.9615 | 0.05 | -2.6181 | 1.1509 | 0.58 | .4455 |
| A+B VS C AT VIS 4 | -1.1225 | 0.9417 | 0.05 | -2.9682 | 0.7232 | 1.42 | .2333 |
| A+B VS C AT VIS 5 | -1.7746 | 1.2532 | 0.05 | -4.2307 | 0.6815 | 2.01 | .1567 |
| A+B VS C AT VIS 6 | -2.1785 | 1.2752 | 0.05 | -4.6778 | 0.3208 | 2.92 | .0876 |
| A+B VS C AT VIS 7 | -3.1169 | 1.3185 | 0.05 | -5.7012 | -0.5327 | 5.59 | .0181 |

![](img/fe9ff008f88baacd415148b0b25dd58c_237_0.png)

# 224 使用 SAS 分析观察性健康数据

## 9.3.2.4 敏感性分析

为了评估发现的稳健性，应当评估因果关系三个假设的合理性（无未测量混杂、阳性、正确模型），并实施基于不同假设的其他统计方法。关于未测量混杂，已努力收集并整合专家和文献的信息，以考虑分析的潜在混杂因素。模型中包含的变量涵盖了症状严重程度、功能、耐受性和资源负担领域。为了评估未测量混杂对结果的潜在影响，我们实现了简单的测量混杂函数（使用基于 Barnett 等人 2004 的常数 alpha）。使用该函数，如果缺失的混杂因素导致 BPRS 量表上发生 0.45（BPRS 总分）的偏移，且有利于处于治疗组患者的潜在结果，将导致统计学上的显著发现。换句话说，我们对显著差异的发现取决于不存在此类混杂因素（或具有相同效应的一组混杂因素）的假设。使用 SAS 代码中的 `ALPHA=c` 常数评估了多个常数（见程序 9）。保留 0.45 的值是因为它是产生约 0.05 p 值的最小值。虽然解释特定 alpha 的含义具有挑战性，但这种影响（BPRS 上的 <1）看起来并不极端。然而，它大于本研究中观察到的相反方向混杂（未加权与加权分析之间的差异）（在未加权与加权分析之间）0.29。无论敏感性分析如何，结果并不意味着可能未未的因素会导致此类分析无法产生因果治疗效应的估计。通过更改提供的 SAS 代码中的变量 `CAVAR_SENS` 和 `SAPT`，可以轻松测试不同的敏感性函数。

* 此部分代码通过寻找消除观察到的治疗差异的混杂水平，检查结果对未测量混杂的敏感性。*

## 第 9 章 使用边际结构模型分析纵向运营数据 225

```
ESTIMATE 'A+B VS C'
TRT 0 .5 .5 -1 0
ESTIMATE 'A+B VS C AT VIS 3'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 4'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 5'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 6'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 7'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .5 -1 0;
RUN;
```

MSM 敏感性分析：`ALPHA = 0.45`

## 对比估计结果

| | 标准估计误差 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| A+B VS C | -1.3991 | 0.7303 | 0.05 | -2.8224 | 0.0402 | 3.63 | 0.0568 |
| A+B VS C AT VIS 3 | -0.0620 | 0.9615 | 0.05 | -2.5048 | 1.2642 | 0.42 | 0.5188 |
| A+B VS C AT VIS 4 | -0.8879 | 0.9417 | 0.05 | -2.7335 | 0.9577 | 0.89 | 0.3457 |
| A+B VS C AT VIS 5 | -1.3184 | 1.2534 | 0.05 | -3.7750 | 1.1383 | 1.11 | 0.2922 |
| A+B VS C AT VIS 6 | -1.6479 | 1.2726 | 0.05 | -4.1422 | 0.8464 | 1.68 | 0.1954 |
| A+B VS C AT VIS 7 | -2.4810 | 1.3135 | 0.05 | -5.0569 | 0.9950 | 3.56 | 0.0991 |

为了评估这种可能性，我们根据 Mortner 等人 (2005) 在所有随访中所有可能的协变量，对五种治疗中的每种进行了选择。这里使用的 `CATMOD` 模型用于为所有可能的治疗方案生成预测概率。虽然本研究在概率假设上没有问题（所有患者都有切换的机会，且可以是任何治疗组合），但目标是评估任何观测协变量集是否为这组数据产生了 0 或 1 的预测概率。这是通过 SAS 程序 9 完成的，我们计算了每个观测协变量集的预测概率，然后对预测概率进行了汇总（使用 `PROC MEANS` 进行汇总统计）。我们发现，最小的概率（非零 < 0.0015）出现在早期随访中从无治疗切换到 A 和 C 治疗组合的理论切换，正如根据其观测频率预期的那样。随后，在排除最极端记录的情况下进行了敏感性分析，并将组合治疗重新分配给初始单一治疗（例如，被随机分配到治疗 A 但接受 C 治疗的患者将仅接受治疗 A）。从这些敏感性分析中没有观察到推断发生重大变化，结果未显示。

## 226 使用 SAS 分析观察性健康数据

## 程序 9.5 检查因果推断的充分性假设

```
* 此部分代码通过检查所有可能的治疗变更的预测值，来检查因果推断的充分性假设。显示了汇总统计数据，并列出了列表以便检查离群值。*
```

```
*充分性检查 Mortimer (2005) - 生成预测概率*/
ODS LISTING CLOSE;
PROC CATMOD DATA = INDPS;
DIRECT AGEYRS BGAF BEYPRS PRBPRS PRIGAFC;
MODEL TRT = VIS THERAPY PRTRTA1 PRTRTC GENDER ORIGIN2 BHOSP
BEVNT AGEYRS BGAF BEYPRS PRWNT PRBPRS PRIGAFC
/PRED;
ODS OUTPUT PREDICTED=PREDTRT1 (KEE=VIS THERAPY PRTRTA
PRTRTC GENDER ORIGIN2 BHOSP BEVNT AGEYRS BGAF
BBPRS PRWNT PRBPRS PRIGAFC
RENAME=(PREDICTION-PREDTRT1));
RUN;
ODS LISTING;
ODS RTF FILESYSFUN(PATHNAME(WORK))SASGF.RTF";
FILENAME="%SYSFUN(PATHNAME(WORK))SASGF.EMF";
OPTIONS RESET=ALL TARGET=ASEMF DEVICE=ASEMF TEXT=DUPLEX HEXT=75 CBACK=WHITE XMAX=6 INXELS=1200 YMAX=5 INXELS=1000 GSFNAME=REPLACE;
PROC UNIVATE DATA = PREDTPOS
VAR PREDTRT1;
HISTOGRAM BLPLOT;
TITLE 'SUMMARY STATS ON PREDICTED VALUES';
RUN;
```

```
OPTIONS RESET=ALL;
ODS RTF CLOSE;
```

```
PROC MEANS DATA = PREDTPOS
CLASS TRT;
VAR PREDTRT1;
TITLE 'Positivity Check: Summary Stats on Predicted Values by Observed Treatment';
RUN;
```

```
PROC SORT DATA = PREDTPOS;
BY PREDTRT1;
RUN;
```
