

这将生成以下随机列表。

| 实验 | 机身宽度 | 机翼长度 |
|---|---|---|
| 1 | 3.25 | 4 |
| 2 | 3.75 | 6 |
| 3 | 4.25 | 4 |
| 4 | 4.25 | 6 |
| 5 | 3.25 | 6 |
| 6 | 3.25 | 5 |
| 7 | 3.75 | 5 |
| 8 | 3.75 | 6 |
| 9 | 3.75 | 4 |
| 10 | 3.25 | 4 |
| 11 | 3.25 | 6 |
| 12 | 4.25 | 4 |
| 13 | 3.25 | 5 |
| 14 | 3.75 | 6 |
| 15 | 4.25 | 6 |
| 16 | 3.25 | 4 |
| 17 | 4.25 | 5 |
| 18 | 3.25 | 6 |

此列表显示，第一个实验包括构建一个机身宽度为 3.25 英寸、机翼长度为 4 英寸的直升机，从固定高度释放并计时其飞行。第二个实验包括构建一个机身宽度为 3.75 英寸、机翼长度为 6 英寸的直升机，从相同的固定高度释放并计时其飞行，以此类推。随机化将有助于防止来自任何潜在变量的偏差，例如气流变化、温度变化或释放或计时直升机的学习曲线。此随机列表可以转换为双行间距的数据收集表，如第 2.2 节中的示例所示。

通过利用 proc factex，可以获得一组更简洁的命令来为因子设计创建随机列表。以下命令将在文件 copter 中生成一个类似于上面所示的随机列表。

```
proc factex;
   factors BW WL/nlev=3;
   model estimate=(BW|WL);
   output out=copter randomized designrep=2
   BW nvals=(3.25 3.75 4.25) WL nvals=(4 5 6) ;
run;
proc print data=copter;
run;
```

factors 语句上的 nlev=3 选项指定机身宽度和机翼长度各有三个水平。proc factex 中默认的水平数为 2。estimate(BW|WL) 指定设计应允许估计机身宽度和机翼长度的主效应及其交互作用。最后，output 语句将列表列在文件中。designrep 选项指定每个因子水平组合有两个重复，randomize 选项随机化列表的顺序，而 `nvals=` 选项指定两个因子水平的数值。如果水平是定性的，例如 (low, mid, high)，则可以使用 `cvals=('low' 'mid' 'high')` 选项代替 `nvals`。对于全因子设计，`proc factex` 本身不产生任何输出。因此，使用 `proc print` 命令来打印随机列表。

## 3.5 SAS 中双因子因子设计的分析

完全随机双因子因子设计的数学模型可以写成：

```
y_{ijk} = \mu_{ij} + \epsilon_{ijk} (3.1)
```

其中 i 表示第一个因子的水平，j 表示第二个因子的水平，k 表示重复次数。此模型称为单元均值模型，\mu_{ij} 表示第 ij 个单元中的预期响应。

表示模型的另一种方法是效应模型

```
y_{ijk} = \mu + \alpha_i + \beta_j + \alpha\beta_{ij} + \epsilon_{ijk} (3.2)
```

在此模型中，\alpha_i 和 \beta_j 是主效应，分别表示第一个因子第 i 个水平的所有实验的边际平均值与总体平均值之间的差异，以及第二个因子第 j 个水平的边际平均值与总体平均值之间的差异。交互效应 \alpha\beta_{ij} 表示单元均值 \mu_{ij} 与 \mu + \alpha_i + \beta_j 之间的差异。

通常假设实验误差相互独立，且 \epsilon_{ijk} \sim N(0, \sigma^2)。如果处理组合被随机分配给实验单位，则独立性假设得到保证；方差齐性和正态性假设可以通过残差对预测值图以及第 2.4 节所述的残差正态概率图进行验证。

如第 2.3.4 节所述的单因子模型，可估计函数是可以表示为数据线性组合的单元均值的线性组合。对于双因子因子设计，单元均值 \mu_{ij} = \mu + \alpha_i + \beta_j + \alpha\beta_{ij} 是可估计函数，但单独的效应 \alpha_i、\beta_j 和 \alpha\beta_{ij} 不是可估计函数。效应之间的对比，例如 \sum_i c_i \alpha_i 和 \sum_j c_j \beta_j（其中 \sum_i c_i = 0、\sum_j c_j = 0）以及 \sum_i \sum_j b_{ij} \alpha\beta_{ij}（其中 \sum_i b_{ij} = 0、\sum_j b_{ij} = 0）是可估计的。这些可估计函数及其标准误可以使用 SAS `proc glm` 中的 `estimate` 命令计算。边际均值 \mu + \alpha_i + \bar{\alpha\beta}_i 和 \mu + \beta_j + \bar{\alpha\beta}_j 是可估计函数，它们及单元均值可以使用 SAS `proc glm` 中的 `means` 或 `lsmeans` 语句计算。

### 3.5.1 模型与分析的矩阵表示

效应模型可以用矩阵表示法表示为

\( y = X\beta + \epsilon = (1 \mid X_A \mid X_B \mid X_{AB}) \begin{pmatrix} \mu \\ \beta_A \\ \beta_B \\ \beta_{AB} \end{pmatrix} + \epsilon \quad (3.3) \)

例如，考虑一种情况：第一个因子有两个水平，第二个因子有三个水平，且每个单元有两个重复。则

\(\begin{pmatrix} y_{111} \\ y_{112} \\ y_{211} \\ y_{212} \\ y_{121} \\ y_{122} \\ y_{221} \\ y_{222} \\ y_{131} \\ y_{132} \\ y_{231} \\ y_{232} \end{pmatrix} = \begin{pmatrix} 1 & 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\ 1 & 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} \mu \\ \alpha_1 \\ \alpha_2 \\ \beta_1 \\ \beta_2 \\ \beta_3 \\ \alpha\beta_{11} \\ \alpha\beta_{21} \\ \alpha\beta_{12} \\ \alpha\beta_{22} \\ \alpha\beta_{13} \\ \alpha\beta_{23} \end{pmatrix} + \begin{pmatrix} \epsilon_{111} \\ \epsilon_{112} \\ \epsilon_{211} \\ \epsilon_{212} \\ \epsilon_{121} \\ \epsilon_{122} \\ \epsilon_{221} \\ \epsilon_{222} \\ \epsilon_{131} \\ \epsilon_{132} \\ \epsilon_{231} \\ \epsilon_{232} \end{pmatrix}\)

\( X'X \) 是奇异矩阵，为了求解正规方程，SAS proc glm 使用广义逆 \( (X'X)^- \)，这等同于施加限制 \( \alpha_2 = \beta_3 = \alpha\beta_{22} = \alpha\beta_{32} = 0 \)。这与在第 2.3.1 节和 2.3.2 节中为单因子模型求解所做的相同。误差平方和 \( ssE = y'y - \beta'X'y = y'(I - X(X'X)^-X')y \)，其中 \( \hat{\beta} = (X'X)^-X'y \) 是 proc glm 指定为有偏估计的估计量。为了检验假设 \( H_0: \alpha_1 = \alpha_2 = 0 \)、\( H_0: \beta_1 = \beta_2 = \beta_3 = 0 \) 和 \( H_0: \alpha\beta_{11} = \alpha\beta_{21} = \alpha\beta_{22} = \alpha\beta_{32} = 0 \)，通过计算 ANOVA 均方的比值来获得似然比 F 检验。SAS proc glm 指定的因子 A 的类型 I 平方和为 \( ssA = \hat{\beta}'X'y - (1'y)^2/(1'1) \)，其中模型简化为仅包含第一个因子的效应，即 \( X = (1 \mid X_A) \)。此简化模型的误差平方和为 \( ssE_A \)。因子 A 的类型 I 平方和记为 \( R(\alpha|\mu) \)。因子 B 的类型 I 平方和记为 \( R(\beta|\alpha, \mu) = ssE_A - ssE_B \)，其中 \( ssE_B \) 是简化模型（其中 \( X = (1 \mid X_A) \mid X_B \)）的误差平方和。最后，交互作用 AB 的类型 I 平方和记为 \( R(\alpha, \beta|\alpha, \mu) = ssAB - ssE \)。一般来说，当因子 A 有 a 个水平、因子 B 有 b 个水平且每个单元有 r 个重复时，双因子因子设计的类型 I ANOVA 表可以用符号表示为表 3.2 所示。

### 表 3.2 方差分析表

| 来源 | 自由度 | 平方和 | 均方 | F 比值 |
| :--- | :--- | :--- | :--- | :--- |
| A | a - 1 | R(α|μ) | ssA / (a-1) | F = msA / msE |
| B | b - 1 | R(β|α, μ) | ssB / (b-1) | F = msB / msE |
| AB | (a - 1)(b - 1) | R(α|β, α, μ) | ssAB / ((a-1)(b-1)) | F = msAB / msE |
| 误差 | ab(r - 1) | ssE | ssE / (ab(r-1)) | |

平方和 ssA、ssB 和 ssAB 也可以写成以下形式

```
ssA = (L_A β̂)'(L_A (X'X)^- L_A')^-1 (L_A β̂)
ssB = (L_B β̂)'(L_B (X'X)^- L_B')^-1 (L_B β̂)
ssAB = (L_αβ β̂)'(L_αβ (X'X)^- L_αβ')^-1 (L_αβ β̂)
```

其中 L_A、L_B 和 L_αβ 是由 SAS proc glm 内部计算的对比矩阵，参见 Goodnight (1980)。在原假设下，F 比值 msA/msE、msB/msE 和 msAB/msE 服从表中所示自由度的 F 分布，而在备择假设下，它们服从非中心 F 分布。F = msA/msE 的非中心性参数由表达式 λ_α = (σ²)^-1 (L_A β̂)'(L_A (X'X)^- L_A')^-1 (L_A β̂) 给出。F 比值 msB/msE 和 msAB/msE 的非中心性参数类似给出。当每个单元中有相同数量 r 的重复时，可以证明非中心性参数等于

```
λ_α = br Σ_i α_i² / σ²      (3.4)
λ_β = ar Σ_j β_j² / σ²      (3.5)
```

和

```
λ_αβ = r Σ_i Σ_j α_ij² / σ²   (3.6)
```

为了说明使用 SAS proc glm 进行双因子因子实验分析，请参考表 3.3 中的数据。这些是 Hunter (1989) 给出的双因子实验结果。在此数据中，一个实验包括

