
# 第 12 章：健康与生命科学

- 12.1 引言
- 12.2 森林图
- 12.3 森林图 (9.3)
- 12.4 生存图
- 12.5 不良事件时间线
- 12.6 不良事件时间线 (9.3)
- 12.7 随时间的最大值 (9.3)
- 12.8 随时间的中位数 (9.3)
- 12.9 随基线的趋势 (9.3)
- 12.10 带有“风险”的表格
- 12.11 随基线的变化
- 12.12 统计数据的 LFT
- 12.13 随治疗的概
- 12.14 最频繁的事件
- 12.15 LFT 概
- 12.16 随时间的 LFT
- 12.17 使用 PROC 的分布 (9.3)
- 12.18 使用 PROC 的分布 (9.3)
- 12.19 随治疗的指标
- 12.20 伴随药物
- 12.21 使用 PROC 的 2 图

## 12.1 引言

健康与生命科学行业是图表的理想应用场景。数据用于许多应用，如临床试验、人口统计学、生命体征和不良事件。对这类数据的评估可以通过可视化得到显著增强，而通过表格形式无法观察趋势和相关性。将数据和统计摘要结合在显示图中可以对结果进行分析和解释。

`SG` 过程非常适合使用书中章节介绍的技术来创建此类图表。在本章中，我们将探讨如何创建该行业常用的某些图表。示例见图 12.1。创建此类图表的详细代码见后几页。

![](img/0c09161c0be53934e5708cffbdcc441f_298_0.png)

图 12.1

## 12.2 森林图

该图显示了森林图的一种形式，展示了不同研究的结果和总体观察。数据如下表所示。关键特征包括：
- 图位于 X-Y 轴（数值），限制在 x 轴的下方 65%。
- 数据位于 X2-Y 轴（字符），限制在 X2 轴的上方 30%。
- 使用带有 `MARKERCHAR` 的标记显示统计数据。

![](img/0c09161c0be53934e5708cffbdcc441f_300_0.png)

| 研究 | 优势比 | 下限 | 上限 | Q1 | Q2 | 观察2 | icl2 | OR | LCL | UCL | 权重 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Modano (1967) | 0.590 | 0.096 | 3.634 | 5% | 0.56 | 26 | 0.096 | 3.634 | LCL | UCL | Weight |
| Borodan (1981) | 0.464 | 0.201 | 1.074 | 18% | 0.38 | 5 | | | | | |

## 12.3 森林图 (9.3)

此图显示了 SAS 9.3 中提供的 HighLow 图绘制了图 12.2 中的森林图。数据所示。该图的主要特征是：

- 使用 `TYPE=Bar` 的 `HighLow` 图来显示研究权重。
- 使用 `TYPE=Line`（默认）的 `HighLow` 图来显示置信限。

| 研究 | 优势比 (OddsRatio) | LowerCL | UpperCL | Q1 | Q3 | Odds study2 | lci2 | uci2 | OR | UCL | Weight |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Modano (1967) | 0.590 | 0.236 | 3.634 | 5% | 0.55 | 0.62 | 0.096 | 3.634 | OR | UCL | Weight |
| Borodanov (1981) | 0.460 | 0.201 | 1.074 | 18% | 0.38 | 0.55 | 0.201 | 2.074 | OR | UCL | Weight |
| | | 0.328 | 0.233 | 0.462 | | | | | 16 Overall | OR | UCL | Weight |

### 各研究中治疗对死亡率的影响

优势比和 95% CL

| OR | UCL | Weight |
| :--- | :--- | :--- |
| Modano (1967) | 0.590 | 0.096 | 3.63% |
| Borodanov (1981) | 0.464 | 0.201 | 18% |
| Leighton (1973) | 0.386 | 0.076 | 2.26% |
| Novak (1992) | 0.490 | 0.089 | 2.37% |
| Steaver (1998) | 1.250 | 0.479 | 3.21% |
| Trucek (2002) | 0.521 | 0.057 | 1.65% |
| Feynman (2005) | 0.313 | 0.054 | 1.90% |
| Modano (1969) | 0.429 | 0.070 | 2.60% |
| Solomon (2003) | 0.718 | 0.037 | 2.17% |
| Adams (1999) | 0.143 | 0.082 | 0.20% |
| Fayneve (2002) | 0.313 | 0.054 | 1.90% |
| Mode2 (1969) | 0.429 | 0.070 | 2.60% |
| Solomon (2002) | 0.718 | 0.037 | 2.17% |
| Adams (1999) | 0.143 | 0.082 | 0.20% |
| Overall | | | |

| 倾向于治疗 | 倾向于安慰剂 |
| :--- | :--- |
| 0.01 | 1 | 10 |

![](img/0c09161c0be53934e5708cffbdcc441f_301_0.png)

```
title="各研究中治疗对死亡率的影响":
title2="优势比和 95% CL":
proc sgplot data=forestbook var=neolecogand nycletog;
highlow y=lowlcf2 type=line;
highlow y=highlow type=segment;
scatter y=xor marker=symbol(shape=filled);
scatter y=x1 marker=lower x2axis;
scatter y=x2 marker=survivor x2axis;
scatter y=weight marker=weight x2axis;
refine 100 0.01 0 10 axisline(pattern=shortdash) transparency=0.5;
inset *
inset "Favors Place" position=bottomleft;
axis-type=log(offset=-0.5 min=0.1 max=100 minor display=(no label));
x2axis offset=0.7 display=(noticks label);
yaxis display=(noticks label) offsetmin=-0.1 offsetmax=0.2 reverse;
run;
```

## 12.4 生存图

此图显示了根据疾病严重程度划分的多组患者的生存估计。数据是通过使用 `LIFETEST` 过程示例 49.2.1 中 "`SurvivalPlot`" 对象的 "`ods output`" 获取的，如下所示。图的主要特征是：

- 在 X-Y 轴（数值型）上绘制曲线，限制在 Y 轴的上 75% 区域。
- 在 X-Y2 轴（字符型）上绘制风险数据，限制在 Y2 轴上。
- 生存曲线使用标签进行标记。

| 观测值 | 时间 | 风险 | 事件 | 分层 | 分层数 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 10000 | 38 | ALL | 1 |
| 2 | 0 | 38 | 0 | ALL | 1 |

![](img/0c09161c0be53934e5708cffbdcc441f_302_0.png)

```
ods survivalplot=sgbook.SurvivalPlot49_2;
proc LIFETEST data=test survival(atrisk=0 to 250);
  title=;
  strata Group adjust=id;
proc format value1="Low" 2="High";
title1="积限生存估计";
title2="风险人数";
proc sgplot data=sgbook.SurvivalPlot49_2;
  stratum=all;
  step y=censored lineattrs=(pattern=solid);
  scatter x=atrisk markerattrs=(plus) name="censored";
  scatter x=atrisk y=stratum markerattrs(cross) group=stratum;
  keylegend "censored" location=topright;
  refine 0;
  yaxis offsetmin=0.2;
  yaxis offsetmax=0.8 display=(nolabel) value=(size=8);
run;
```

## 12.5 不良事件时间

此图显示了随时间和严重程度变化的不良事件。数据提取自临床数据并在表中所示。图的主要特征是：

- 使用向量图显示事件。
- 使用散点图显示开始和结束事件。
- 使用带有标记的散点图显示事件名称。
- 注意：的 X 位置 (`xc`) 需要计算。

| 观测值 | 开始日期 | 结束日期 | 计数 | 变量 | 严重程度 | 开始天 | 结束天 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 06MAR13 | 06MAR13 | 1 | DUMMY | MILD | -100 | -4.4 |
| 2 | 06MAR13 | 06MAR13 | 1 | DUMMY | MODERATE | -100 | -4.4 |
| 3 | 06MAR13 | 06MAR13 | 1 | SEVERE | -100 | -4.4 |
| 4 | 06MAR13 | 06MAR13 | 1 | DIZZINESS | MODERATE | -1 | -6.6 |
| 5 | 20MAR13 | | 2 | COUGH | MILD | 2 | 9.57 | 14 |

```
title "患者 ID = xx-xxx-xxxx 的不良事件"
proc sgplot data=sgbook.acat nootelaage nocycleattr;
refine(axis=(thickness=1)color=black);
vector xendesy ysy / markerchartay vertgny noarrowheads
lineatrs=(thickness=9)
/* 示例 */
vector xendesy ysy / markerchartay vertgny group=aesev noarrowheads
lineatrs=(thickness=9)pattern(transparency=0)name='sev';
scatter xendesy ysy / markerchar=(size=5px) symbol=triangledfilled group=aesev;
scatter xendesy ysy / markerchar=(size=5px) symbol=triangledfilled group=aesev;
lineatrs=(thickness=9)pattern;
scatter xendesy ysy / markerchar=(size=5px) symbol=triangledfilled group=aesev;
scatter xsc xcy / markerchar=none;
scatter xasteate ysy / markerchar=(size=0) x2axis;
axis display=(label Study days novabels) min=0;
axis grid label="Days" offsetsmin=0.02 offsetmax=0.02;
values(from=0 by 22);
x2axis notetimes display=(nolabel) offsetmin=0.02 offsetmax=0.02;
keylegend "sev" title="";
run;
```

Matange, Sanjay and Heath, Dan. *Statistical Procedures by Example: Effective Graphs using SAS®*. 版权所有 2011, SAS Institute Inc., Cary, North Carolina, USA. 保留所有权利。欲更多 SAS 资源，请访问 support.sas.com/publishing。

## 12.6 不良事件时间 (9.3)

此图显示了随时间和严重程度变化的不良事件。数据提取自 CDISC 数据并如下表所示。图的主要特征是：

- 使用 HighLow 选项显示事件。
- 使用 LOWABEL 选项显示事件名称。
- 使用低高端帽显示持续中的事件。

| 开始日期 | 结束日期 | 序列 | 代码 | y | 严重程度 | 结束天 | 高端帽 | x位置 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 06MAR13 | 06MAR13 | | MILD | -100 | -4.4 | 0 | | |
| 06MAR13 | 06MAR13 | | MODERATE | -100 | -4.4 | 0 | | |
| 06MAR13 | 06MAR13 | | SEVERE | -100 | -4.4 | 0 | | |
| 06MAR13 | 06MAR13 | | DIZZINESS | MODERATE | -1 | -6.6 | 0 | | |
| 20MAR13 | | | COUGH | 2 | 9.57 | 14 | 104 |

![](img/0c09161c0be53934e5708cffbdcc441f_304_0.png)

## 12.8 各治疗组随时间变化的脂质概况中位数 (9.3)

在此图中，我们展示了不同治疗组随时间变化的脂质概况。在这里我们再次使用了“Y-Y2 分割”技术将分组区域分为两部分：

- 上部区域用于显示图表。
- 下部区域用于显示统计数据。
- 值使用簇分组散点图。
- 折线图使用簇分组系列图。
- 缩小了簇宽度以使簇看起来更轻盈。
- 使用带有 `y-Drug` 和 `MARKERCHAR` 选项的散点图显示统计数据。
- Y2 轴上带有 `DISCRETEOFFSET` 的参考线用于区分两个区域。

| X | 药物 | 中位数 | Lcl | Ucl |
|---|---|---|---|---|
| 基线 | 药物 A | 5.21 | 5.04 | 5.52 |
| 基线 | 药物 B | 5.17 | 4.94 | 5.47 |
| 基线 | 药物 C | 5.24 | 4.97 | 5.53 |
| 基线 | 安安慰剂 | 5.23 | 4.95 | 5.50 |
| 第 14 天 | 药物 A | 4.90 | 4.60 | 5.79 |
| 第 14 天 | 药物 B | 6.65 | 4.81 | 7.51 |

![](img/0c09161c0be53934e5708cffbdcc441f_306_0.png)

```
title "Median of Lipid Profile over Time by Treatment";
proc sgplot datagroup.lipid_grp;
where by test=1;
scatter x=y /group=drug yrorupper=ucl yrorlower=lcl
groupdisplay=cluster clusterswidth=0.5 markerattrs=(size=9);
series x=y /group=markerchar groupdisplay=cluster clusterswidth=0.5;
scatter x=y /group=marker-median y2axis;
refine "Placebo" /discreteoffset=0.5 axis=y2;
axis grid off offsetmin=0.30;
y2axis offsetmax=0.8 display=(noticks nolabel)
run;
```

## 12.9 各治疗组随时间变化的较基线 QTc 变化 (9.3)

此图显示了心跳校正 QT (`QTc`) 间期的变化。访视间隔不均匀，开始阶段频率较高，因此对时间使用线性轴是比较理想的。该图具有以下特征：

- 数据使用了两个 `VBOX` 语句的重叠。
- x 轴值对每个治疗组进行了 0.25 的抖动（jittered），以获得相邻的叠加层。
- 使用用户定义的格式将最后一个值标记为“Max”。
- 添加了参考线以分离最后一个值。
- 理想情况下，我们希望显示研究中每周的“风险人数”（atRisk）值。为此，我们将使用如图 12.10 所示的 SGPLOT 注释功能。

| 周 | 2 | atRisk | atRisk | valueB |
|---|---|---|---|---|
| 1 | 0.75 | 209 | 72.1929 |
