
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

均值中心化的浓度是在不同的程序中确定的，并在此处硬编码。 （使用 `PROC STANDARD` 构造包含浓度变量均值中心化版本的变量会更简洁，然后将其输出到新的数据集中。你能在家里弄清楚如何做到这一点吗？）对转换进行 `DATA` 步编程的更令人感兴趣的替代方案还包括以下内容：

- `PROC GLM` with `MODEL SQRT_TOTAL=CONC | CONC;`

- `PROC TRANSREG` with `MODEL POWER(TOTAL / PARAMETER=0.5)=PSPLINE(CONC / CENTER DEGREE=2);`

与此拟合的多项式回归模型关联的 `ODS` 图形如 Display 8.19 所示。

> ³ `Nitrofen` 数据集来自 Bailer, A. John., and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.

## Display 8.19 来自多项式回归模型的输出

![](img/26474180ee55914c13fb9156a7678157_294_0.png)

模型拟合得出了以下预测方程：

```
predicted sqrt(Total)=5.25-0.01×(conc-157)-0.00056×(conc-157)²
```

在此模型中，计数响应进行了平方根转换。 （它进行平方根转换是因为我们假设 `Total` 为 Poisson 变量，因此应应用方差稳定化转换。）浓度变量进行了中心化。 变量 `CCONC2` 包含中心化变量的平方。试试看：如果你不将 `CONC` 预测变量中心化而对其进行平方， collinearity 诊断会改变吗？你将如何解释此模型的參數？

另一个常见的转换涉及根据变量的值构造指示变量。 定义这些指示变量的最简单方法之一是进行布尔比较，其结果被强制转换为数值形式。 在这里，如果语句为真，则分配值 1。 如果语句为假，则分配值 0。 在第 5 章中，构造了一个指示变量，以使恐龙的体重和脑重关系与数据集中其他动物不同。 用于构造指示变量的语句如下：

```
idino = 0;                * define the indicator of dinosaurs;
if (species="diplodoc" or species="tricerat" or
    species="brachios") then
idino=1;
```

指示变量 `idino` 首先对所有观测值初始化为 0，如果条件 `(species="diplodoc" or species="tricerat" or species="brachios")` 为真，则重新分配为 1。 这里有一个避免初始化和条件检查的替代语句：

```
idino = (species="diplodoc" or species="tricerat" or
    species="brachios");
```

此语句在条件为假时将 `idino` 分配为 0，在条件为真时将 `idino` 分配为 1。 必须认识到这些比较中大小写很重要。 如果 `species` 的值为 `Diplodoc`，则 `idino` 为 0，因为 `Diplodoc` 与 `diplodoc` 不同。

对于下一个指示变量示例，使用了包装和对数细菌生长数据⁴。 假设你想使用指示变量的线性回归作为单向方差分析模型的替代方案。 数据中存在四种不同的包装条件。 Display 8.20 中的代码为每种条件定义了一个指示变量。 `PROC GLM` 中的 `CLASS` 语句会自动为方差分析模型生成指示变量。

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

Display 8.21 包含 Display 8.20 中 `PROC PRINT` 的输出。 此输出可让你检查重新编码是否按预期工作。 （其他过程的输出被省略）。

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

打印数据集证实指示变量已正确构造。 （重新编码变量后打印数据始终是一个好主意。）顺便说一下，`PROC REG` 和 `PROC GLM` 输出中 `F_obs=94.58`，均未显示。 不妨自己试试这段代码。

你可以在 `DATA` 步中使用“布尔技巧”来构造更复杂的变量。 让我们重新审视具有变量 `LITERACY` 的数据，该变量记录为百分比。 你想重新编码此变量。 你决定根据变量值所在的区间对观测值进行标记（例如，≤53%、53% 至 76%、76% 至 90% 或 >90%）。 你想将类别标签 1、2、3 和 4 分配给这些区间。 数据包含位于区间内的观测值、一些值超出有效范围（0 到 100）的观测值，以及一个缺失观测值。 Display 8.22 中为类别定义了四个不同的指示变量。

### Display 8.22 定义识字类别的指示变量

```
data toyexample;
    input literacy @@;

/* method 1-2:
    Boolean trick to assign category labels 1-4;
    If a logical comparison is TRUE (FALSE), it evaluates to 1 (0)
    e.g. if literacy=54, (53<literacy<=76)=TRUE while
        (0<literacy<=53)=(76<literacy<=90)=(90<literacy<=100)=FALSE
        And so cat_literacy1 = 1*0 + 2*1 + 3*0 + 4*0 = 2
*/

cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
    + 3*(76<literacy<=90) + 4*(90<literacy<=100);

cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
    + 3*(76<literacy<=90) + 4*(90<literacy<=100);

/*
    method 3:
    First check for nonmissing and valid ranges before Boolean trick
*/

if ( (literacy NE .) AND (0<=literacy<=100) ) then
    cat_literacy3 = 1*(literacy<=53) + 2*(53<literacy<=76)
        + 3*(76<literacy<=90) + 4*(90<literacy<=100);

/* method 4:
    IF-THEN-ELSE blocks to assign category labels
*/

if ( (literacy EQ .) OR (100<literacy)
        OR (literacy<0) ) then cat_literacy4=.;
else if (literacy <=53) then cat_literacy4=1;
else if (literacy <=76) then cat_literacy4=2;
else if (literacy <=90) then cat_literacy4=3;
else cat_literacy4=4;
datalines;
-99 25.55 73.7 83   99.9 107 .
;
run;
ods rtf file="C:\Users\baileraj.IT\Desktop\Display-8-22.rtf";
proc print data=toyexample;
run;
ods rtf close;
```

四个不同的指示变量显示在 Display 8.23 中。

### Display 8.23 不同指示变量的 PROC PRINT 输出

| Obs | literacy | cat_literacy1 | cat_literacy2 | cat_literacy3 | cat_literacy4 |
|---|---|---|---|---|---|
| 1 | -99.00 | 0 | 1 | . | . |
| 2 | 25.55 | 1 | 1 | 1 | 1 |
| 3 | 73.70 | 2 | 2 | 2 | 2 |
| 4 | 83.00 | 3 | 3 | 3 | 3 |
| 5 | 99.90 | 4 | 4 | 4 | 4 |
| 6 | 107.00 | 0 | 0 | . | . |
| 7 | . | 0 | 1 | . | . |

观察定义变量 `cat_literacy1` 的第一种方法。当 `literacy=54` 时，第一个条件 `(0<literacy<=53)` 为 FALSE。第二个条件 `(53<literacy<=76)` 为 TRUE。第三个条件 `(76<literacy<=90)` 为 FALSE。第四个条件 `(90<literacy<=100)` 为 FALSE。考虑以下表达式：

```
cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

如果 `TRUE =1` 且 `FALSE =0`，则该表达式求值为以下内容：

```
cat_literacy1 = 1*(0) + 2*(1) + 3*(0) + 4*(0) = 2
```

如果你希望保留 `LITERACY` 的缺失值，或者希望将有效范围之外的取值赋为缺失值，则此代码不会按预期行为运行。如果 `LITERACY` 缺失 `(.)`，或其取值超出所测试的范围 `(-99` 到 `107)`，则没有任何条件为 TRUE，且 `cat_literacy1=0`。

第二种方法导致了值得注意的其他行为。考虑以下表达式：

```
cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

此方法在 `LITERACY` 为 `-99` 或缺失时将 `cat_literacy2=1`。此赋值发生是因为条件 `(literacy<=53)` 对 `-99` 为 TRUE（不出所料，因为 `-99≤53`），且缺失观测为 TRUE（可能令人惊讶，因为你可能不知道缺失 `(.)≤53`）。

第三种和第四种方法的行为符合预期。首先进行非缺失值和有效范围的 `IF` 检查。如果该值通过此检查，则类别的分配遵循前两种方法分配类别的方式。第四种方法使用 `IF–THEN–ELSE` 构造。代码稍长，但可能更容易理解。关键是始终使用边界、无效和缺失案例测试你的代码，以确保你得到想要的结果。

## 8.4 任务执行的顺序

在开始为问题实现编程解决方案之前，你需要知道计算执行的顺序（所谓的运算顺序或运算优先级）。让我们快速看一下初学者程序员常见的头痛来源。（如果你已经知道这些内容，则跳过。）计算机做你所说的，而不是你所想的。因此，你应仔细编写程序，尤其是方程。当编码方程时，请记住计算机以特定顺序执行方程的各部分。如果没有括号，则先进行指数运算。然后，第二步进行乘法和除法（同等优先级）。最后进行加法和减法（同等优先级）。括号内的表达式先于其他表达式处理。处理方程时从左到右求值。`AND` 运算符在 `OR` 运算符之前执行，这在复杂的表达式中如果程序未包含括号时可能会产生差异。

让我们从抽象转向具体。下一个示例说明了粗心编码的一些危险。在示例中，请特别注意计算对：

```
x1a=3×2² versus x1b=(3×2)²
x2a=3−2/2 versus x2b=(3−2)/2
x3a=−2² versus x3b=(−2)²
```

你可能期望由于括号的分组，这对会产生不同的值。然而，当你查看代码时，这并不完全清晰。例如，如果你天真地认为代码不考虑运算顺序而从左到右处理，那么你可能会期望 `x2a=3−2/2` 和 `x2b=(3−2)/2` 产生相同的答案。Display 8.24 包含测试代码，证明情况并非如此。

## Display 8.24 运算顺序的测试代码
