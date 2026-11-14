

```
data plt; set sol;
estimate;
if _n_=1 then drop Stderr tValue Probt ;
* proc rank calculates normal scores for parameter estimates ;
proc rank data=plt out=plots normal=blom; var estimate;
ranks zscore;
data nplots; set plots;
if zscore=. then parameter=' ' ;
proc sgplot data=nplots;
scatter x=zscore y=estimate/datalabel=parameter;
xaxis label="Normal Scores";
run;
```

## 图 3.15 回归系数的正态概率图

![](img/878b651cdbe9da3d6d22e64d64b8a54f_113_0.png)

直接计算半正态分数，\(|\hat{\beta}_{(i)}|\) 的半正态分数可由公式 \(\Phi^{-1}(((i - 1/2) + 1)/2)\) 近似，其中 \(\Phi^{-1}()\) 是标准正态分布的逆累积分布函数，\(i\) 是 \(|\hat{\beta}_{(i)}|\) 的秩次。在 SAS 中，probit 函数计算 \(\Phi^{-1}()\)，创建半正态图的代码如下一页所示。

图 3.16 所示的半正态图左下角有一条从原点出发的参考线，以及一条上预测限界线。效应 A、B 以及 A×B 交互作用位于上限线之上，且明显显著。图 3.16 中的参考线和上限是由 Lawson (2008a) 描述的 SAS 宏按照概述的程序自动添加的。

```
data hmplot; set sol;
estimate;
if _n_=1 then drop StdErr tValue Probt;
* proc rank calculates ranks for parameter estimates ;
proc rank data=hmplot out=hnplots; var estimate; ranks rnk;
* data step calculates half normal scores for estimates;
data hnplots; set hnplots;
z=probit((rnk-0.375)/(n+1)/2);
if abs(z)<1.0 then parameter=' ' ;
proc sgplot data=hnplots;
scatter x=z y=estimate/datalabel=parameter;
xaxis label="Half Normal Scores";
run;
```

## 图 3.16 绝对回归系数的半正态图

![](img/878b651cdbe9da3d6d22e64d64b8a54f_114_0.png)

由 Lawson 等人 (1998) 描述。在图上手动绘制参考线时，使用半正态图比使用正态图更容易，因为从左下角开始的前一半到三分之二的点几乎总是会形成一条直线。然而，在半正态图中，系数的符号会丢失。例如，在 proc glm 输出和正态图中，可以清楚地看出主效应 A（反应物 A 的过量）具有负效应，并且平均而言，增加反应物 A 的过量会导致转化率下降。在半正态图中，可以看出主效应 A 是显著的，但必须返回系数表来查看它是正效应还是负效应。

当然，在本例中存在显著的交互作用，因此无法单独解释主效应。为了帮助解释交互作用，应创建交互图。下面显示了创建和标记因子 A（反应物 A 的过量）与因子 B（催化剂浓度）之间交互图的 SAS 命令，生成的图表如图 3.17 所示。

```
proc format;
   value levels -1='Low Level' 0=' ' 1='High Level';
   run;
   ***** table of means;
   proc sort data=chem; by A B;
   run;
   proc means data=chem noprint; var y; by A B;
   output out=output mean=yhat;
   run;
   proc print; run;
   ***** plot of interaction;
   proc sgplot data=output;
   series x=A y=yhat /group=B markers;
   xaxis label='Excess of Reactant A' type=discrete;
   yaxis label='Percent Conversion';
   format B levels. A levels.;
   run;
```

## 图 3.17 催化剂与过量 A 的交互图

![](img/878b651cdbe9da3d6d22e64d64b8a54f_115_0.png)

从中可以看出，增加催化剂水平会提高转化率。当使用低水平催化剂时，增加反应物 A 的过量对转化率影响甚微。然而，如果使用高水平催化剂，增加反应物 A 的过量会使转化率下降超过 20%。因此，为了达到最高转化率，应使用高水平催化剂和低水平过量反应物 A。

## 3.8 验证模型假设

当因子模型中每个单元都有重复实验单位，或者当交互项可被假设为可忽略并从模型中移除（例如根据第 3.5.4 节或 3.7.5 节描述的初步检验结果），则可按照第 2.4 节所述，使用残差图来验证因子模型的正态性和常方差假设。

然而，在每个单元只有一个重复的 2^k 设计中，检查正态性假设会稍微困难一些。正态性假设最常因存在一个异常值或非典型值而被违反。在两水平因子设计中，计算出的主效应和交互作用始终可以表示为两个平均值之差，\(\bar{y}_+ - \bar{y}_-\)。当实验误差服从正态分布时，对响应影响可忽略的因子和交互作用的计算效应应服从均值为零的正态分布。潜在有影响因子的显著性是根据其与由可忽略因子形成的效应正态图或半正态图上的参考线点的关系来判断的。然而，一个非典型值会使每个计算出的效应向正或向负方向偏离零。非有影响因子和交互作用的计算效应的变异性会大得多，这使得判断效应的显著性变得更加困难，更不用说检查残差的正态性假设了。

Daniel (1960) 提出了一种手动方法，用于检测和纠正未重复 2^k 设计中的异常值或非典型值。该方法包含三个步骤。首先，通过效应正态图中心的间隙来检测异常值的存在。其次，通过将不显著效应的符号与每个观测值的编码因子水平和交互作用的符号相匹配来识别异常值。第三步是估计差异的大小并纠正非典型值。

例如，考虑 Box (1991) 描述的未重复 2^k 实验的效应正态图（图 3.18）。在此图中，主效应 B 和 C 可能显著，但不显著效应线中存在一个垂直间隙，这表明可能存在异常值。

Lawson 和 Gathin (2006) 实现了 Daniel 识别和纠正非典型值的过程的自动化，Lawson (2008a) 提供了执行此过程的 SAS 宏。下一页的 SAS 命令说明了如何将此宏与 Box (1991) 描述的数据一起使用。第一个数据步骤创建一个 2^k 设计并将其存储在名为 xmatrix16 的数据集中。下一个数据步骤将响应数据读入名为 box 的数据集。接下来定义宏变量 %nobs 和 %vname1。%nobs 是设计中的运行次数，%vname1 是 X 矩阵中列名的列表。宏需要这些宏变量。最后，表示 X 矩阵的数据集被复制到名为 x1 的数据集，表示响应变量的数据集被复制到名为 y 的数据集。这些是宏所需的名称。最后，通过语句 %gapmth 调用宏。宏的输出包括回归系数表及其显著性检验、正态图中间隙的显著性检验，以及当间隙被判定为显著时，生成经校正的响应表和使用经校正数据计算的回归系数表。经校正的响应表显示在生成它的 SAS 命令下方的下一页。

![](img/878b651cdbe9da3d6d22e64d64b8a54f_117_0.png)

该方法检测到第 13 次运行存在异常值，并通过将 59.15 改为 52.15 来校正响应。对经校正数据的重新分析得出了经校正数据表之后页面所示的表格。

该宏还生成基于原始数据和经校正数据计算的回归系数的半正态图。图 3.19 显示了使用经校正数据计算的系数的半正态图。在此图中，除了在图 3.18 中识别的主效应 B 和 C 之外，可以清楚地看出 AC 交互作用也是显著的。它们在图 3.18 中无法被检测到，因为异常值夸大了不显著效应的估计，而 AC 效应被淹没在噪声中。

每当使用此方法或残差图发现异常值，并且在移除或校正异常值时分析结论发生变化，实验者应谨慎行事。当存在超过两个

