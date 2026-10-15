

## 3.9 汇总分类变量

分类数据通常通过每个分类变量的水平响应频率或相对频率，或分类变量水平组合的频率来汇总。一个变量的频率表可用于检查数据录入的完整性。例如，五种浓度组中应有 10 只动物。以下用于检查数据完整性的代码使用 PROC FREQ，该过程生成了显示 3.23 中的表：

```
proc freq data=nitro_tox;
    table conc;
run;
```

可以看到，五种硝酚浓度水平已正确录入（即 CONC=0、80、160、235 和 310，与预期一致）。每个浓度均记录了 10 个观测值。

### 显示 3.23 各硝酚浓度中的观测值数量

| conc | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|------|-----------|---------|----------------------|--------------------|
| 0    | 10        | 20.00   | 10                   | 20.00              |
| 80   | 10        | 20.00   | 20                   | 40.00              |
| 160  | 10        | 20.00   | 30                   | 60.00              |
| 235  | 10        | 20.00   | 40                   | 80.00              |
| 310  | 10        | 20.00   | 50                   | 100.00             |

个体对两个或多个分类变量的响应通常以列联表形式显示。在两个分类变量的情况下，一个变量标记行。另一个变量标记列。列联表显示行值和列值每种组合下的观测计数。以下代码请求一个列联表，其中硝酚水平显示为行（CONC），第三窝中幼崽的存在情况（CBROOD3）显示为列（二水平分类变量）。表输出被修改为仅显示行百分比。（NOCOL 和 NOPCT 选项分别抑制列百分比和联合百分比的打印。）请求统计检验以查看在第三窝产生幼崽的概率是否对其他窝相同（CHISQ 和 EXACT 选项），以及是否存在浓度相关的趋势（TREND 选项）。以下部分代码生成了显示 3.24 中的输出：

```
```sas
proc freq data=nitro_tox;
  table conc*cbrood3 / noperct nocol chisq trend exact;
run;
```
```

### 显示 3.24 显示氮浓度与第三窝是否产生幼崽的列联表

The FREQ Procedure

Table of conc by cbrood3

conc (Nitrofen concentration)

| Frequency / Row Pct | none | some | Total |
|---|---:|---:|---:|
| 0 | 0<br>0.00 | 10<br>100.00 | 10 |
| 80 | 0<br>0.00 | 10<br>100.00 | 10 |
| 160 | 0<br>0.00 | 10<br>100.00 | 10 |
| 235 | 1<br>10.00 | 9<br>90.00 | 10 |
| 310 | 10<br>100.00 | 0<br>0.00 | 10 |
| Total | 11 | 39 | 50 |

*(continued)*

### 显示 3.24 （续）

Statistics for Table of conc by cbrood3
Statistic	DF	Value	Prob
Chi-Square	4	44.7552	<.0001
Likelihood Ratio Chi-Square	4	46.1891	<.0001
Mantel-Haenszel Chi-Square	1	24.5782	<.0001
Phi Coefficient		0.9461
Contingency Coefficient		0.6873
Cramer's V		0.9461
WARNING: 50% of the cells have expected counts less than 5. Chi-Square may not be a valid test.
Fisher's Exact Test
Table Probability (P)	2.677E-10
Pr <= P	5.354E-09
Cochran-Armitage Trend Test
Statistic (Z)	5.0080
One-sided Pr > Z	<.0001
Two-sided Pr > |Z|	<.0001
Sample Size = 50

在最高硝酚浓度下，第三窝产生幼崽的概率似乎下降。有关本例中统计检验的更多细节，请参阅标准分类数据参考资料（例如 Agresti 2002）。Stokes 等人（2009）很好地总结了 SAS 中的分类数据分析方法。

## 3.10 汇总数值变量

如果你被困在荒岛上，只能使用一个 SAS 过程，PROC UNIVARIATE 可能是你的选择（假设你在荒岛上对描述数值变量感兴趣）。该过程可以生成位置描述统计量（均值、中位数、分位数）和离散度统计量（标准差、方差、范围、四分位距）。它可以识别数据集中的极值。此外，它还可以生成简单的图形，包括直方图、正态分位数图、茎叶图、箱线图等。以下编程语句生成总幼崽数的直方图，并带有非参数密度估计（显示 3.25）。语句还生成数据分位数与正态分位数的图（显示 3.26）：

```
proc univariate data=nitro_tox;
    var total;
    histogram / kernel;  * histogram with nonpar. Density est.;
    qqplot;             * quantile-quantile plot vs. normal;
run;
```

### 显示 3.25 五种硝酚浓度条件下 50 个观测值的总幼崽数直方图

![](img/26474180ee55914c13fb9156a7678157_124_0.png)

该显示的多峰模式并不令人惊讶，因为它包含了来自五种不同浓度条件的数据，包括产生幼崽较多的条件（例如 CONC=0、80）和产生幼崽较少的条件（例如 CONC=310）。在显示 3.26 中，Q-Q 图的非线性表明总幼崽数的分布不是正态的。同样，这也不令人惊讶，因为这些数据包含了来自五种不同浓度条件的响应。

### 显示 3.26 五种硝酚浓度条件下 50 个观测值的总幼崽数正态分位数图

![](img/26474180ee55914c13fb9156a7678157_125_0.png)

以下编程语句为每种浓度生成单独的数值汇总：

```
proc univariate data=nitro_tox;
  by conc;
  var total;
run;
```

显示 3.25 中的直方图可由 SGPLOT 过程按显示 3.27 中的代码和显示 3.28 中的输出生成。请注意 ODS RTF 语句中 STYLE=JOURNAL 的指定。该指定生成灰度版本的图形，可能更适合期刊发表。有关样式和图形的更多讨论，请参阅第 6 章。

### 显示 3.27 使用 PROC SGPLOT 生成叠加密度的直方图

```
%let DATA_DIR = C:\Users\baileraj.IT\Desktop;
data nitro_tox;
  infile "&DATA_DIR\ch2-dat.txt"
    firstobs=16 expandtabs missover pad ;
  input @9 animal 2. @17 conc 3. @25 brood1 2.
        @33 brood2 2. @41 brood3 2. @49 total 2.;
run;

*ods rtf style=journal bodytitle
    file="&DATA_DIR\Display-3.27.rtf";  * selecting gray scale style/
B&W;

ods listing image dpi=300 style=journal;
ods graphics / width=4.5in;
proc sgplot data=nitro_tox;          * figure as often used in journal
                                     articles;
  histogram total;
  density total / type=kernel;
  keylegend / location=inside position=topleft;
run;
ods graphics off;
*ods rtf close;
```

### 显示 3.28 由 PROC SGPLOT 生成的叠加密度直方图

![](img/26474180ee55914c13fb9156a7678157_126_0.png)

让我们使用 PROC UNIVARIATE 查看来自 SMSA² 城市数据的 1 月温度数据的数值汇总。（有关更多背景信息，请参阅第 2.2 节。）显示 3.29 包括对 JANTEMP 变量的单变量统计请求以及识别与极端低或高温度相关的城市。（这是一种很好的检查数据集中异常值的方法。）

### 显示 3.29 请求描述 SMSA 数据集中 1 月温度分布的单变量统计

```
options nodate nocenter nonumber;
%let DATA_DIR = C:\Users\baileraj.IT\Desktop;
data SMSA_from_txt;
  infile "C:\Users\baileraj.IT\Desktop\SMSA-DASL-2space-sep.txt"
  firstobs=2;
  length city $ 39;
  input city & JanTemp JulyTemp RelHum Rain Mortality Education PopDensity pct_NonWhite pct_WC pop pop_per_house income HCPot NOxPot SO2Pot NOx;
run;
ods rtf bodytitle file="&DATA_DIR\Display-3.29.rtf";
proc univariate data=SMSA_from_txt;
  var JanTemp;
  id city;
run;
ods rtf close;
```

显示 3.30 中的输出提供了关于观测值数量、中心值和离散度度量的信息。它包括检验均值温度是否为零的统计检验。它显示了 1 月温度数据的分位数和极端观测值（五个最低的 1 月温度和五个最高的 1 月温度）。

### 显示 3.30 描述 SMSA 数据集中 1 月温度的信息

The UNIVARIATE Procedure
Variable: JanTemp

|  | Moments |  |
|---|---|---|
| N | 60 | Sum Weights | 60 |
| Mean | 33.9833333 | Sum Observations | 2039 |
| Std Deviation | 10.1688985 | Variance | 103.406497 |
| Skewness | 0.96071148 | Kurtosis | 1.08782139 |
| Uncorrected SS | 75.393 | Corrected SS | 6100.98333 |
| Coeff Variation | 29.9231933 | Std Error Mean | 1.31279915 |

