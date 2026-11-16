

程序，深入分析的细节超出了本章的范围，就我们的目的而言，你只需要理解SEM可以用来估计变量之间的关系，仿佛它们被完美测量一样。因此，在完美相关下的相关系数估计为r = 0.90（决定系数为0.81），非常接近计算的校正相关效应量。不幸的是，尽管0.80范围内的alpha很常见，但基于可靠性远低于此的数据的已发表研究也不难找到。事实上，找到0.70以下的alpha也不困难，尽管这意味着相当一部分效应量损失了！在21世纪，这应该被视为一种不理想的状态，特别是当通过增加条目数量或使用结构方程建模等现代方法进行分析来改善量表测量相对简单时。

## 应用

## 样本量与Alpha的精确度

如前所述，alpha取决于样本。因此，可以预期样本量会影响我们alpha估计的精确度。当使用较小的样本来估计alpha时，每个观测值对估计都贡献了大量信息。小样本中的异常值或与预期的偏差可能对结果产生深远影响，并导致结果与总体均值不同。然而，在较大的样本中，异常值或偏差可能会被其他观测值平均掉。

让我们使用本书中一直在使用的Marsh SDQ数据来探讨样本量和精确度的问题。让我们首先检查完整数据集中父母子量表的可靠性。父母子量表由五个条目组成：

- (Par1) 我的父母公平对待我。
- (Par2) 我不太喜欢我的父母。
- (Par3) 我与父母相处融洽。
- (Par4) 我的父母通常对我所做的事不高兴或失望。
- (Par5) 我的父母理解我。

显然，Par2和Par4的方向是相反的。如果直接使用这五个条目计算alpha（参见第192页的图11.2），你将得到一个负的alpha（这是不可能的）以及一些负的条目-总分相关（另一个问题的迹象）。

### 图11.2 反向编码条目的输出

### Cronbach系数Alpha

| 变量 | Alpha |
|---|---|
| 原始 | -.338304 |
| 标准化 | -.316077 |

### 删除变量后的Cronbach系数Alpha

| 删除的变量 | 原始变量与总分的相关 | 原始变量Alpha | 标准化变量与总分的相关 | 标准化变量Alpha |
|---|---|---|---|---|
| Par1 | 0.193681 | -.834220 | 0.180020 | -.861766 |
| Par2 | -.417175 | 0.194553 | -.431354 | 0.245049 |
| Par3 | 0.174914 | -.828698 | 0.163839 | -.821268 |
| Par4 | -.406022 | 0.220399 | -.402013 | 0.208550 |
| Par5 | 0.115035 | -.872559 | 0.181588 | -.865728 |

因此，我们必须对两个变量进行重新编码并重新运行。由于我们可能希望保留原始数据的副本，我们将创建一个包含重新编码值的新变量，即Par2_recode和Par4_recode。下面给出了初始运行（如上所述）、重新编码和修订运行的语法，并附有注释。请注意，我们提供了两种重新编码选项——一种是为每个变量单独重新编码值的冗长方法，另一种是使用数组的较短方法。

```
/*Try to compute alpha for parenting items;
proc corr data=sqdata alpha;
Par;

run;

/*Recode and re-run;
*Recode option 1 - the long way;
data sqdata;
set sqdata;

recode Par2;
if Par2=1 then Par2_recode=6;
if Par2=2 then Par2_recode=5;
if Par2=3 then Par2_recode=4;
if Par2=4 then Par2_recode=3;
if Par2=5 then Par2_recode=2;
if Par2=6 then Par2_recode=1;
*recode Par4;
if Par4=1 then Par4_recode=6;
if Par4=2 then Par4_recode=5;
if Par4=3 then Par4_recode=4;
if Par4=4 then Par4_recode=3;
if Par4=5 then Par4_recode=2;
if Par4=6 then Par4_recode=1;
run;
```

```
*Recode option 2 - arrays;
data sqddata (drop=i);
set sqddata;
array old(*) Par2 Par4; *old variables to recode;
array recode(*) Par2_recode Par4_recode; *new versions;
do i=1 to dim(old);
  if old(i)=1 then recode(i)=6;
  if old(i)=2 then recode(i)=5;
  if old(i)=3 then recode(i)=4;
  if old(i)=4 then recode(i)=3;
  if old(i)=5 then recode(i)=2;
  if old(i)=6 then recode(i)=1;
end;
run;
```

```
**Re-run;
proc corr data=sqddata alpha;
var Par1 Par2_recode Par3 Par4_recode Par5;
run;
```

使用重新编码的Par2和Par4运行后的更新结果显示在第194页的图11.3中。由于我们输入的是原始数据而非变量的标准化版本，我们解释所呈现的原始系数。我们现在有一个看起来正常（相当不错）的alpha为0.834，N = 15661。此外，条目-总分相关系数均在0.569到0.733之间，这是合理的。

### 图11.3 重新编码条目的更新输出

| 变量 | Alpha |
|---|---|
| 原始 | 0.834427 |
| 标准化 | 0.838161 |

| 删除的变量 | 原始变量与总分的相关 | 原始变量Alpha | 标准化变量与总分的相关 | 标准化变量Alpha |
|---|---|---|---|---|
| Par1 | 0.643062 | 0.800653 | 0.644466 | 0.804390 |
| Par2_recode | 0.595988 | 0.811647 | 0.597524 | 0.817244 |
| Par3 | 0.732967 | 0.775705 | 0.733190 | 0.779291 |
| Par4_recode | 0.568660 | 0.820491 | 0.568433 | 0.825066 |
| Par5 | 0.658999 | 0.796445 | 0.661981 | 0.799518 |

让我们将此视为我们的黄金标准“总体”统计量，并看看小样本对alpha估计有何影响。使用PROC SURVEYSELECT，我们从数据集中通过有放回的简单随机抽样抽取了1000个N=50的子样本、1000个N=100的子样本和1000个N=250的子样本。执行此操作的语法如下所示。

```
/*Take 1000 subsamples of N=50;
proc surveysselect data=sasdqta method=SRS n=50 out=sasdqta_sub50
seed=5092 reps=1000;
run;
/*Take 1000 subsamples of N=100;
proc surveysselect data=sasdqta method=SRS n=100 out=sasdqta_sub100
seed=821 reps=1000;
run;
/*Take 1000 subsamples of N=250;
proc surveysselect data=sasdqta method=SRS n=250 out=sasdqta_sub250
seed=291 reps=1000;
run;
```

然后，我们计算了每个子样本中父母量表的alpha，并按样本量绘制了alpha分布，以了解估计值的范围。针对1000个N=50的子样本执行此步骤的语法如下所示。另外两组子样本的语法与此相同，只是输入（以及通常输出）数据集的名称不同（如果你遵循最佳实践并更改重要输出数据集的名称）。在此语法中，我们使用ODS输出包含alpha的数据集，然后使用ODS图形和SGPLOT过程绘制直方图。

```
*Estimate alpha in each subsample;
ods output CronbachAlpha=alphaS50;
*noprint option used to suppress printing and outp used to output data set
with alphas;
proc corr data=sqdata_sub50 alpha nosimple nocorr noprob;
by Replicate;
var Par1 Par2_recode Par3 Par4_recode Par5;
run;
ods output close;

**Print histogram of alphas;
ods graphics on /height=3in width=3in;
proc sgplot data = alpha50 nautolegend;
title "Sample Size = 50";
where Variables="Raw";
histogram Alpha / binwidth=.025 FILLATTRS=(COLOR=cx5E5EAF2) ;
xaxis label = 'Alpha' grid values = (.55 to 1 by .1);
run;

ods graphics off;
```

一般来说，子样本alpha越接近我们的“总体”alpha 0.83，就可以认为越精确。然而，越远离的就越不精确。如在第196页的图11.4所示，在较小的样本中alpha变得有些不稳定。在最小的样本（N=50）中，观察到的alpha范围从低至α = 0.56到高至α = 0.94。在N=100的样本中，范围进一步缩小，低至α = 0.70，高至α = 0.92。最后，N=250的样本具有最窄的alpha范围，低至α = 0.74，高至α = 0.89。因此，随着样本量的增加，alpha的精确度得到了提高。这表明，即使在具有相当强心理测量特性的量表中（如本例），小样本也往往存在相当大的波动性。

