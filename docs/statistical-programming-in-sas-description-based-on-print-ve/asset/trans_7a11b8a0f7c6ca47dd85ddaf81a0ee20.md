

## Display 8.16 将日期、时间和货币数据读入 SAS

```
data test;
  input @1 date MMDDYY10. @21 time TIME8. @31 money DOLLAR10.2;
  datalines;
01/01/1960      01:00:00  $100.22
09/29/2003      09:49:59  $12693.79
;
run;

ODS RTF file="C:\Users\baileraj.IT\Desktop\Display-8-16.rtf";
proc print data=test;
title "print of date and time w/o formatting - internal SAS representation";
var date time money;
run;

proc print data=test;
title "print of date and time w/ formatting";
var date time;
format date MMDDYY10. time TIME8. money DOLLAR10.2;
run;
ODS RTF CLOSE;
```

比较有格式和无格式打印此数据的情况如 Display 8.17 所示。

## Display 8.17 包含日期、时间和货币数据的 PROC PRINT 输出

| proc print; var date time money; | proc print; var date time money; format date MMDDYY10. time TIME8. money DOLLAR10.2; |
|---|---|
| Obs | date | time | money | Obs | date | time | money |
| 1 | 0 | 3600 | 100.22 | 1 | 01/01/1960 | 1:00:00 | $100.22 |
| 2 | 15977 | 35399 | 12693.79 | 2 | 09/29/2003 | 9:49:59 | $12,693.79 |

## 8.3 在 DATA 步中重新编码和转换变量

DATA 步是定义、重新定义和转换变量以供后续分析的核心枢纽。常见的转换示例包括对响应变量进行方差稳定化或线性化转换、为多项式回归定义高阶项，以及构建指示变量。以下使用 Display 8.18 中编码的 nitrofen 数据³ 突出了其中两个任务。

## Display 8.18 在拟合多项式回归模型之前的数据转换

```
data nitrofen;
infile 'C:\Users\baileraJ.IT\Desktop\ch2-dat.txt' firstobs=16 expandtabs;
input 017 conc 3. 049 total 2.;
sqrt_total = sqrt(total); * transformed response variable;
cconc = conc - 157; * construct mean-centered concentration;
cconc2 = cconc*cconc; * quadratic term;
run;
ods rtf BODYTITLE file="C:\Users\baileraJ.IT\Desktop\Display-8-18.rtf";
ods graphics on;
proc reg data=nitrofen;
model sqrt_total = cconc cconc2; * fit the polynomial reg. model;
run;
ods graphics off;
ods rtf close;
```

均值中心化的浓度是在不同的程序中确定的，并在此处硬编码。 （使用 PROC STANDARD 构造包含浓度变量均值中心化版本的变量会更简洁，然后将其输出到新的数据集中。你能在家里弄清楚如何做到这一点吗？）对转换进行 DATA 步编程的更令人感兴趣的替代方案还包括以下内容：

- PROC GLM with MODEL SQRT_TOTAL=CONC | CONC;
- PROC TRANSREG with MODEL POWER(TOTAL / PARAMETER=0.5)=PSPLINE(CONC / CENTER DEGREE=2);

与此拟合的多项式回归模型关联的 ODS 图形如 Display 8.19 所示。

> ³ Nitrofen 数据集来自 Bailer, A. John., and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.

## Display 8.19 来自多项式回归模型的输出

![](img/26474180ee55914c13fb9156a7678157_294_0.png)

模型拟合得出了以下预测方程：

```
predicted sqrt(Total)=5.25-0.01×(conc-157)-0.00056×(conc-157)²
```

在此模型中，计数响应进行了平方根转换。 （它进行平方根转换是因为我们假设 Total 为 Poisson 变量，因此应应用方差稳定化转换。）浓度变量进行了中心化。 变量 CCONC2 包含中心化变量的平方。试试看：如果你不将 CONC 预测变量中心化而对其进行平方， collinearity 诊断会改变吗？你将如何解释此模型的參數？

另一个常见的转换涉及根据变量的值构造指示变量。 定义这些指示变量的最简单方法之一是进行布尔比较，其结果被强制转换为数值形式。 在这里，如果语句为真，则分配值 1。 如果语句为假，则分配值 0。 在第 5 章中，构造了一个指示变量，以使恐龙的体重和脑重关系与数据集中其他动物不同。 用于构造指示变量的语句如下：

```
idino = 0;                * define the indicator of dinosaurs;
if (species="diplodoc" or species="tricerat" or
    species="brachios") then
idino=1;
```

指示变量 idino 首先对所有观测值初始化为 0，如果条件 (species="diplodoc" or species="tricerat" or species="brachios") 为真，则重新分配为 1。 这里有一个避免初始化和条件检查的替代语句：

```
idino = (species="diplodoc" or species="tricerat" or
    species="brachios");
```

此语句在条件为假时将 idino 分配为 0，在条件为真时将 idino 分配为 1。 必须认识到这些比较中大小写很重要。 如果 species 的值为 Diplodoc，则 idino 为 0，因为 Diplodoc 与 diplodoc 不同。

对于下一个指示变量示例，使用了包装和对数细菌生长数据⁴。 假设你想使用指示变量的线性回归作为单向方差分析模型的替代方案。 数据中存在四种不同的包装条件。 Display 8.20 中的代码为每种条件定义了一个指示变量。 PROC GLM 中的 CLASS 语句会自动为方差分析模型生成指示变量。

## Display 8.20 为拟合方差分析模型定义不同条件的指示变量

```
options nodate formdlim="-";
data meat;
    input condition $ logcount @@;
    iPlastic = (condition ="Plastic");
    iVacuum = (condition="Vacuum");
    iMixed  = (condition="Mixed");
    iCO2    = (condition="Co2");
    datalines;
Plastic    7.66  Plastic    6.98  Plastic    7.80
Vacuum     5.26  Vacuum     5.44  Vacuum     5.80
Mixed      7.41  Mixed      7.33  Mixed      7.04
Co2        3.51  Co2        2.91  Co2        3.66
;
run;

title "bacteria growth under 4 packaging conditions";

ODS RTF bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-20.rtf";

proc print data=meat;
title "Print to check indicator variable construction";
run;

proc reg data=meat;
title "Regression with indicator variables: alt. to one-way anova model";
    model logcount = iPlastic iVacuum iMixed;
run;

proc glm data=meat;
title "One-way ANOVA model";
    class condition;
    model logcount = condition;
run;

ods rtf close;
```

Display 8.21 包含 Display 8.20 中 PROC PRINT 的输出。 此输出可让你检查重新编码是否按预期工作。 （其他过程的输出被省略）。

## Display 8.21 PROC PRINT 输出

| condition | logcount | iPlastic | iVacuum | iMixed | iCO2 |
|-----------|----------|----------|---------|--------|------|
| Plastic   | 7.66     | 1        | 0       | 0      | 0    |
| Plastic   | 6.98     | 1        | 0       | 0      | 0    |
| Plastic   | 7.80     | 1        | 0       | 0      | 0    |

(continued)

## Display 8.21 (continued)

| condition | logcount | iPlastic | iVacuum | iMixed | iCO2 |
|-----------|----------|----------|---------|--------|------|
| Vacuum | 5.26 | 0 | 1 | 0 | 0 |
| Vacuum | 5.44 | 0 | 1 | 0 | 0 |
| Vacuum | 5.80 | 0 | 1 | 0 | 0 |
| Mixed | 7.41 | 0 | 0 | 1 | 0 |
| Mixed | 7.33 | 0 | 0 | 1 | 0 |
| Mixed | 7.04 | 0 | 0 | 1 | 0 |
| Co2 | 3.51 | 0 | 0 | 0 | 1 |
| Co2 | 2.91 | 0 | 0 | 0 | 1 |
| Co2 | 3.66 | 0 | 0 | 0 | 1 |

打印数据集证实指示变量已正确构造。 （重新编码变量后打印数据始终是一个好主意。）顺便说一下，PROC REG 和 PROC GLM 输出中 F_obs=94.58，均未显示。 不妨自己试试这段代码。

你可以在 DATA 步中使用“布尔技巧”来构造更复杂的变量。 让我们重新审视具有变量 LITERACY 的数据，该变量记录为百分比。 你想重新编码此变量。 你决定根据变量值所在的区间对观测值进行标记（例如，≤53%、53% 至 76%、76% 至 90% 或 >90%）。 你想将类别标签 1、2、3 和 4 分配给这些区间。 数据包含位于区间内的观测值、一些值超出有效范围（0 到 100）的观测值，以及一个缺失观测值。 Display 8.22 中为类别定义了四个不同的指示变量。

