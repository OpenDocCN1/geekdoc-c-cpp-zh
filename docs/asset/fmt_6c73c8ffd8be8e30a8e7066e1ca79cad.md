
```sas
/* Bacteria in meat under 4 different conditions */
options ls = 75;
data meat;
    input condition $ logcount @@;
datalines;
Plastic    7.66    Plastic    6.98    Plastic    7.80
Vacuum     5.26    Vacuum     5.44    Vacuum     5.80
Mixed      7.41    Mixed      7.33    Mixed      7.04
Co2        3.51    Co2        2.91    Co2        3.66
;
run;

title "bacteria growth under 4 packaging conditions";

ODS RTF file='C:\Users\baileraj.IT\Desktop\oneway-output.rtf';
ods listing image dpi=300;
ods graphics on / width=4.5in;
proc sgplot data=meat;          * graphical comparisons;
    vbox logcount / category=condition;
run;

proc glm data=meat order=data plot(unpack)=diagnostics;
    title2 "fitting the one-way anova model via GLM";
    class condition;
    model logcount = condition;
    means condition / bon tukey scheffe cldiff lines;
    lsmeans condition / cl pdiff;
    lsmeans condition / cl pdiff adjust=Tukey;
    contrast 'plastic vs. rest' condition 3 -1 -1 -1;
    output out=new p=yhat r=resid stdr=eresid;
run;

proc sgplot data=new;          * plots for model checking;
    title2 "residual analyses";
    scatter x=yhat y=resid;
    refline 0 / axis=y;
run;

proc univariate data=new noprint;
    histogram resid / normal;
    qqplot resid / normal;
run;
ods graphics off;

ODS RTF CLOSE;
```

³ 肉类数据集使用基于 Kuehl, R. O. Statistical Principles of Research Design and Analysis. 1st Ed. © 1994. Brooks/Cole, a part of Cengage Learning, Inc. ISBN: 9780534188047(0534188044) 的“肉类细菌生长”数据集。

在示例中，使用 `PROC SGPLOT` 的 `VBOX` 语句生成的并排箱线图创建了四个组中响应的图形显示。`VBOX` 语句标识响应变量 `LOGCOUNT` 和标识不同组的变量 `CONDITION`。

#### Display 5.17 不同包装条件下 `log`-细菌生长的并排箱线图

![](img/26474180ee55914c13fb9156a7678157_194_0.png)

从该显示中，`log`-细菌生长在 CO₂ 包装条件下最低，其次是真空，塑料和混合最差。可以说，箱线图在每组仅有三个观测值时不是很有信息量。然而，该箱线图对于提供适用于重复次数更大的实验的示例非常有用。

`PROC GLM` 请求对四个组之间的均值相等性进行检验，并请求一系列相关分析。`GLM` 是广义线性模型的缩写，其中包括先前描述的回归分析和 ANOVA 模型。广义线性模型通常简称为线性模型。如果您期望的是广义线性模型，`GLM` 可能是令人困惑的过程名称，该模型在 SAS 中使用 `PROC GENMOD` 实现。作为 `PROC GLM` 语句的一部分，使用 `plot(unpack)=diagnostics` 包含诊断图请求。这将在下一章中更详细地讨论。然而，值得一提的是，因为 ANOVA 模型的拟合

```
plot(unpack)=diagnostics
```

#### Display 5.18B 细菌生长 ANOVA 模型拟合的残差直方图，叠加正态密度和核密度

![](img/26474180ee55914c13fb9156a7678157_196_0.png)

单因素方差分析模型的两个必需语句在 `PROC GLM` 语句之后。`CLASS` 语句标识包含组变量水平的变量。`GLM` 的 `MODEL` 语句类似于 `REG` 的 `MODEL` 语句（特别是语句的形式为：`响应变量 = 预测变量或组变量`）。在 `PROC GLM` 中分析的数据描述如 Display 5.19 所示。

#### Display 5.19 ANOVA 模型结果的包装汇总

| Class Level Information |  |  |
|---|---|---|
| Class | Levels | Values |
| `condition` | 4 | Plastic Vacuum Mixed Co2 |

Number of observations: 12

此信息描述了组变量的水平。这是一个很好的地方来查看输入数据集中的印刷错误。水平条目的拼写错误将导致超过 `g=4` 个水平。例如，如果 `C02`（C-零-二）被输入一个观测值，而 `Co2`（C-oh-two）也被输入两个案例，则表中会有 `g=5` 个水平。观测总数已注明。`PROC FREQ` 的 `CONDITION` 水平表也可以用于检查这一点。

`PROC GLM` 包含两个选项：一个标识输入数据集的选项和 `order=data` 选项。包装按塑料、真空、混合和 CO₂ 的顺序输入。如果没有 `ORDER` 选项，SAS 会在 `PROC GLM` 中进行内部字母排序，这将对 `CONTRAST` 等语句产生影响。特别是，内部字母排序会将 CO₂（编码为 `Co2`）分配为第一个水平，`Mixed` 为第二个水平，`Plastic` 为第三个水平，`Vacuum` 为第四个水平。

Display 5.20 显示了 `g=4` 组均值相等的检验。在分析中，四个包装条件下平均 `log`-细菌计数相同的原假设被拒绝，适用于任何通常选择的显著性水平（F(3,8)=94.58, P<0.0001）。该检验及其相关 p 值连同 ANOVA 表、描述性统计（总体均值、变异系数）和两个额外的检验表一起呈现。Type I 和 Type III 表在不平衡数据的多因素 ANOVA 模型背景下更有意义。

#### Display 5.20 ANOVA 表结果：比较不同包装的平均对数细菌生长

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---:|---:|---:|---:|
| Model | 3 | 32.87280000 | 10.95760000 | 94.58 | <.0001 |
| Error | 8 | 0.92680000 | 0.11585000 |  |  |
| Corrected Total | 11 | 33.79960000 |  |  |  |

| R-Square | Coeff Var | Root MSE | `logcount` Mean |
|---:|---:|---:|---:|
| 0.972580 | 5.768940 | 0.340367 | 5.900000 |

| Source | DF | Type I SS | Mean Square | F Value | Pr > F |
|---|---:|---:|---:|---:|---:|
| `condition` | 3 | 32.87280000 | 10.95760000 | 94.58 | <.0001 |

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
|---|---:|---:|---:|---:|---:|
| `condition` | 3 | 32.87280000 | 10.95760000 | 94.58 | <.0001 |

`MODEL` 语句之后紧跟的语句（`means condition / bon tukey scheffe cldiff lines`）请求对包装条件进行成对比较。虽然 SAS 提供了许多多重比较程序，但本例中仅调用了三种程序——Bonferroni（`bon`）、Tukey（`tukey`）和 Scheffe（`scheffe`）。`cldiff` 请求包装条件之间成对差异的置信区间。`lines` 请求比较所有均值差异结果的图形显示。对于 `tukey`，`cldiff` 生成 Display 5.21。

#### Display 5.21 Tukey ANOVA 表结果，指定 `CLDIFF`

NOTE: This test controls the Type I experimentwise error rate.

- Alpha: 0.05
- Error Degrees of Freedom: 8
- Error Mean Square: 0.11585
- Critical Value of Studentized Range: 4.52880
- Minimum Significant Difference: 0.89

Comparisons significant at the 0.05 level are indicated by `***`

| condition Comparison | Difference Between Means | Simultaneous 95% Confidence Limits | Significance |
|---|---|---:|---:|---:|
| Plastic - Mixed | 0.2200 | -0.6700, 1.1100 |  |
| Plastic - Vacuum | 1.9800 | 1.0900, 2.8700 | `***` |
| Plastic - Co2 | 4.1200 | 3.2300, 5.0100 | `***` |
| Mixed - Plastic | -0.2200 | -1.1100, 0.6700 |  |
| Mixed - Vacuum | 1.7600 | 0.8700, 2.6500 | `***` |
| Mixed - Co2 | 3.9000 | 3.0100, 4.7900 | `***` |
| Vacuum - Plastic | -1.9800 | -2.8700, -1.0900 | `***` |
| Vacuum - Mixed | -1.7600 | -2.6500, -0.8700 | `***` |
| Vacuum - Co2 | 2.1400 | 1.2500, 3.0300 | `***` |
| Co2 - Plastic | -4.1200 | -5.0100, -3.2300 | `***` |
| Co2 - Mixed | -3.9000 | -4.7900, -3.0100 | `***` |
| Co2 - Vacuum | -2.1400 | -3.0300, -1.2500 | `***` |

Tukey 多重比较程序的 `LINES` 语句产生了 Display 5.22 所示的输出。

#### Display 5.22 Tukey ANOVA 表结果，指定 `LINES`

Means with the same letter are not significantly different

| Tukey Grouping | Mean | N | `condition` |
|---|---:|---:|---|
| A | 7.4800 | 3 | Plastic |
| A | 7.2600 | 3 | Mixed |
| B | 5.5000 | 3 | Vacuum |
| C | 3.3600 | 3 | Co2 |

Display 5.21 和 5.22 都显示，CO₂ 包装条件的平均对数细菌生长显著低于真空包装，而真空包装又显著低于塑料或混合包装。这一事实在 Display 5.21 中得以体现，因为用于成对差异的均值比较的置信区间不包含零。在 Display 5.22 中，这一事实通过不同组别关联的不同字母（A、B 和 C）得以体现。

`MEANS` 语句之后有两个语句，`lsmeans condition / cl pdiff` 和 `lsmeans condition / cl pdiff adjust=Tukey`。这些语句请求不同组的均值，请求每个组中均值响应的置信区间（使用合并方差估计）和均值差异的置信区间，并请求均值相等成对检验的 p 值矩阵。第二个 `LSMEANS` 语句对比较应用了 Tukey 多重比较调整。这两个语句的输出显示在 Display 5.23 中。毫不奇怪，Tukey 调整后的 p 值更大，与未调整的对应值相比，同时置信区间更宽。也可以指定其他调整，例如 Bonferroni。在分析一个处理时，`MEANS` 和 `LSMEANS` 会得到相同的结果。然而，在多因素研究中，如果处理（因子水平的组合）复制不相等，则会出现差异。这在第 5.4 节“ANOVA 模型——具有两个或多个因子的 ANOVA 模型的 `PROC GLM`”中进行了讨论。

#### Display 5.23 通过 `LSMEANS` 进行成对比较（编辑后）

| `condition` | `logcount` `LSMEANS` | `LSMEANS` Number | 95% Confidence Limits |
|---|---:|---:|---|
| Plastic | 7.48000000 | 1 | 7.026844, 7.933156 |
| Vacuum | 5.50000000 | 2 | 5.046844, 5.953156 |
| Mixed | 7.26000000 | 3 | 6.806844, 7.713156 |
| Co2 | 3.36000000 | 4 | 2.906844, 3.813156 |

Least Squares Means for Effect Condition

Pr > |t| for H0: `LSMeans(i)=LSMeans(j)`

Dependent Variable: `logcount`

| i/j | 1 | 2 | 3 | 4 |
|---|---:|---:|---:|---:|
| 1 |  | <.0001 | 0.4514 | <.0001 |
| 2 | <.0001 |  | 0.0002 | <.0001 |
| 3 | 0.4514 | 0.0002 |  | <.0001 |
| 4 | <.0001 | <.0001 | <.0001 |  |

Least Squares Means for Effect Condition

| i | j | Difference Between Means | 95% Confidence Limits for `LSMeans(i)-LSMeans(j)` |
|---|---:|---:|---|
| 1 | 2 | 1.980000 | 1.339141, 2.620859 |
| 1 | 3 | 0.220000 | -0.420859, 0.860859 |
| 1 | 4 | 4.120000 | 3.479141, 4.760859 |
| 2 | 3 | -1.760000 | -2.400859, -1.119141 |
| 2 | 4 | 2.140000 | 1.499141, 2.780859 |
| 3 | 4 | 3.900000 | 3.259141, 4.540859 |

NOTE: To ensure overall protection level, only probabilities associated with preplanned comparisons should be used.

#### Display 5.23 （续）

Adjustment for Multiple Comparisons: Tukey

| `condition` | `logcount` `LSMEANS` | `LSMEANS` Number |
|---|---:|---:|
| Plastic | 7.48000000 | 1 |
| Vacuum | 5.50000000 | 2 |
| Mixed | 7.26000000 | 3 |
| Co2 | 3.36000000 | 4 |

Least Squares Means for Effect Condition

Pr > |t| for H0: `LSMeans(i)=LSMeans(j)`

Dependent Variable: `logcount`

| i/j | 1 | 2 | 3 | 4 |
|---|---:|---:|---:|---:|
| 1 |  | 0.0005 | 0.8564 | <.0001 |
| 2 | 0.0005 |  | 0.0010 | 0.0003 |
| 3 | 0.8564 | 0.0010 |  | <.0001 |
| 4 | <.0001 | 0.0003 | <.0001 |  |

两包装结论之间平均对数细菌计数差异的置信限与基于合并方差 t 检验的置信区间相似。均方误差被用作合并方差的估计值，且自由度相应调整。试一试：在家使用 `PROC TTEST` 比较两种包装条件。均值差异的置信区间与（未调整的）`LSMEANS` 比较相比，与 `PROC TTEST` 相比有何不同？
