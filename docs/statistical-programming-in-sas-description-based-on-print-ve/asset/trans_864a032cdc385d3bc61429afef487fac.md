

## 显示 7.6 对说明抛硬币相对频率的图形进行注释

```
data cointoss;
    retain num_heads 0;
    call streaminit(1234567);
    do itoss = 1 to 1200;
        outcome = RAND('Bernoulli', 0.50);
        num_heads = num_heads + (outcome=1);
        probability_heads = num_heads / itoss;
        output;
    end;
run;

goptions reset=global;
symbol interpol=join;
axis1 order=(0.35 to 0.65 by 0.05)
    minor=NONE
    label=(angle=90 "Estimated Pr(HEADS)");
axis2 order=(0 to 500 by 50)
    minor=NONE
    label=("Number of simulated data points");

data myanno;
length function $ 8 text $ 45;
retain xsys "2" ysys "2";
function="move";  x=0;    y=0.50; output;
function="draw";  x=500;  y=0.50; output;
function="label"; x=350; y=0.48;
    text="Long-term relative frequency of HEADS=0.50"; output;
run;

ods rtf bodytitle
    file="C:\Users\baileraj\Desktop\cointoss2-graph.rtf";
proc print data=myanno;
run;

proc gplot data=cointoss;
    plot probability_heads*itoss / annotate=myanno
                                    vaxis=axis1 haxis=axis2;
run;
quit;
ods rtf close;
```

数据集 myanno 包含显示注释的命令。长度声明为 8 确保函数标签不会被截断为四个字符，因为函数的第一个值是四字符值 move，而文本长度的声明允许显示更长的文本字符串。 （长度 8 可容纳任何可能的函数参数。）retain 语句具有双重功能。它保持 xsys 和 ysys 的值不变，用于后续行中定义的所有观测值。并且，它将值 2 分配给这些变量。xsys 和 ysys 变量定义了注释数据集中坐标 (x,y) 对所使用的坐标轴定义。值 2 是与数据值比例对应的绝对比例。XSYS 和 YSYS 值 1 到 6 对应于绝对比例，而 {7, 8, 9, A, B, C} 对应于相对比例。你可能会发现 2 对于统计图形的注释或对于与数据区域百分比相关的注释（1, 7）或与图形输出区域百分比相关的注释（3, 9）是最有用的值。第一个观测值将光标移动到 (0, 0.50) 位置：

```
function="move"; x=0; y=0.50; output;
```

第二个观测值从当前位置 (0, 0.50) 绘制到目标位置 (500, 0.50)：

```
function="draw"; x=500; y=0.50; output;
```

第三个观测值在 (350, 0.48) 处添加居中文本：

```
function="label"; x=350; y=0.48;
    text="Long-term relative frequency of HEADS=0.50"; output;
```

注释数据集 myanno 的内容在显示 7.7 中。

## 显示 7.7 注释数据集的内容

| Obs | function | Text | xsys | ysys | x | y |
|---|---|---|---|---|---|---|
| 1 | move |  | 2 | 2 | 0 | 0.50 |
| 2 | draw |  | 2 | 2 | 500 | 0.50 |
| 3 | label | Long-term relative frequency of HEADS=0.50 | 2 | 2 | 350 | 0.48 |

注释数据集是通过 PLOT 语句的选项作为 PROC GPLOT 的一部分呈现的：

```
plot probability_heads*itoss / annotate=myanno;
```

生成的图形和注释显示在显示 7.8 中。

## 显示 7.8 带注释的硬币正面相对频率散点图

![](img/26474180ee55914c13fb9156a7678157_262_0.png)

许多图形任务由其他函数完成（例如，POLY、POINT、BAR、SYMBOL、DRAW2TXT、PIE 和 FRAME）。

让我们考虑一个更复杂的例子。比值比（OR）是 logistic 回归和流行病学调查中报告的常见汇总指标。并不少见，近似置信区间（CI）是通过对 log[OR] 构造的对称 CI 进行指数化而产生的。假设观察到估计 OR=2 且估计 SE{log[OR]}=0.2。OR 的近似 95% CI 将为 exp[log(2) ± 1.96*0.2]。构造一个显示此内容的图形不是很酷吗？该图形将执行以下操作：

- 说明 (OR, log[OR]) 关系。
- 将 OR=2 映射到其对应的 log[OR] 值。
- 从该值移动 ± 1.96 SE{log[OR]}。
- 移回 OR-log[OR] 轨迹。
- 投影回 OR 轴以获得 CI。

显示 7.9 提供了构造此图形的代码。图形显示在显示 7.10 中。

## 显示 7.9 基于指数化对称 CI 构造 OR 的 CI

```
/* generate a profile of [OR, log(OR)] values */
data or_stuff;
   do or=0.01 to 5 by .01;
      logor = log(or);
      output;
   end;
run;

goptions reset=global; * often a good idea, especially if doing a lot of graphs;

/* interpolate btwn [OR, log(OR)] values and set up axes */
symbol interpol=join c=black; * always specify color in symbol stmt;
axis1 label=("Odds Ratio");
axis2 label=(angle=90 "Log(Odds Ratio)");

/* set up annotate data set with arrows and text to illustrate the CI idea */
data myanno;
length function $ 8 text $ 7; * good habit b/c max fcn length=8;
retain xsys "2" ysys "2" function SE;
SE = .2;
function="move"; x=2; y=-5; output;
function="arrow"; x=2; y=log(2); output; * from OR to logOR;
function="arrow"; x=.01; y=log(2); output; * back to y-axis;

function="draw"; x=.01; y=log(2) + 1.96*SE; line=2; output; * upper CI;
function="arrow"; x=exp(log(2) + 1.96*SE); y=log(2) + 1.96*SE; output;
function="arrow"; x=exp(log(2) + 1.96*SE); y=-4.5; output;

function="move"; x=.01; y=log(2); output; * lower CI;
function="draw"; x=.01; y=log(2) - 1.96*SE; output;
function="arrow"; x=exp(log(2) - 1.96*SE); y=log(2) - 1.96*SE; output;
function="arrow"; x=exp(log(2) - 1.96*SE); y=-4.5; output;
function="label";
        x=exp(log(2) - 1.96*SE); y=-4.75; text="LCL OR"; output;
        x=exp(log(2) + 1.96*SE); y=-4.5; text="UCL OR"; output;
        x=2.2; y=-2; text="Step 1"; output;
        x=1; y=log(2) + .25; text="Step 2"; output;
        x=0.5; y=log(2) - 1.96*SE; text="Step 3a"; output;
        x=0.5; y=log(2) + 1.96*SE + .25; text="Step 3b"; output;
        x=3.2; y=-2; text="Step 4a"; output;
        x=1.2; y=-2; text="Step 4b"; position="<"; output; * right justify text;
run;

/* produce the graph with annotation */
ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\fig7p9.rtf";
proc gplot data=or_stuff;
   plot logor * or / annotate=myanno haxis=axis1 vaxis=axis2;
run;
quit;
ods rtf close;
```

注释数据集的新元素包括：

- 使用 `arrow` 函数。
- 使用 `line=2` 在 `draw` 函数中请求虚线。
- 使用 `position="<"` 请求标签中的文本右对齐。
- 使用 `retain` 将 `label` 函数分配给其后所有注释观测值。

## 显示 7.10 基于指数化对称 CI 构造 OR 的 CI 的概念步骤

![](img/26474180ee55914c13fb9156a7678157_264_0.png)

你怎么看？能够制作这样的显示来解释 CI 构造不是很酷吗？

专业的 SAS 程序员经常使用这些方法来构造非常专门的显示。然而，对于想要创建自定义图形的统计用户来说，学习如何使用图形模板语言（GTL）和 PROC SGRENDER 比学习如何使用注释数据集更值得投入时间。GTL 是一种功能强大的语言，具有内置的统计计算功能，而注释数据集是原始的。

## 7.4 案例研究：比较响应分布

在本节中，先前描述的许多想法应用于图形，以帮助你了解实验条件之间响应分布的差异。你将使用 nitrophen 数据集，该数据集包含暴露于不同浓度硝基酚的水蚤（Ceriodaphnia dubia）的硝基酚浓度-生殖响应数据。²（嘿，你可能对这些数据厌倦了，但你现在应该足够熟悉数据，可以专注于代码！）该数据集在每种浓度下包含 10 个观测值。你想要构造图形以显示响应分布如何随浓度条件变化。你想要呈现数据值和适当的汇总统计量。在第一个图形中，你生成响应与浓度变量的散点图，并在平均响应处设置参考线段。在第二个图形中，你生成散点图，并在每个浓度的响应上叠加箱线图。

显示 7.11 中适用于两个散点图的代码的一些关键操作包括以下内容：

- 定义抖动，以便可以观察到所有观测值。
- 使用 AXIS 语句旋转 y 轴标签。
- 定义 x 轴的标签和 x 轴值范围（AXIS2 语句的 LABEL 和 ORDER 部分）。
- 抑制 x 轴上的刻度标记和比例值（AXIS2 语句中的 MINOR=NONE、MAJOR=NONE 和 V=NONE）。

在第一个散点图中，使用注释数据集在 x 轴上方标记浓度值，并绘制并叠加平均响应值的线段。在第二个散点图中，SYMBOL1 选择散点图的绘图字符，SYMBOL2 选择箱线图插值并指定箱子的宽度（bwidth=8）。同样，使用注释数据集在 x 轴上方标记浓度值。由于使用了抖动来修改值，因此在这两个散点图中，使用注释数据集来定义 x 轴值。试试看：AXIS 语句能否生成这些散点图？

> ² Nitrophen 数据集来自 Bailer, A. John, and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.

