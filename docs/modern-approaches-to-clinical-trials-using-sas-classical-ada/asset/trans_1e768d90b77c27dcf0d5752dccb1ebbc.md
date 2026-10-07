

# 6.4 使用模拟数据进行分析示例

### 6.4.1 Emax 模型简介介绍

本节描述了针对连续终点和二分类终点的两个模拟实际示例。模拟数据假设在 II 期剂量范围试验中有 5 个剂量组，分别为 0mg（安慰剂）、2.5mg、5mg、10mg 和 20mg。每个剂量组的样本量为 60。使用混合过程（mixed procedure）拟合 4 参数模型以分析数据。请注意，SAS 中的 `proc nlin` 也可以用于拟合 4 参数模型，它专门用于非线性回归模型。两种过程产生的估计值和结果非常相似。此外，为了方便连续和二分类终点情况的读者，还包含了用于 PoC 趋势测试的代码，使用使用 `polyorth` 宏生成的对比考虑了等间距或不等剂量间距。

该模型是剂量响应研究中常用的非线性终点模型之一 [24]。模型所示：

```
$y_i = E_0 + E_{max} \tilde{A} - \frac{D_i^h}{ED_{50}^h + D_i^h} + I\mu_i$,
```

其中：

- 1. $i$ 是受试者 ID
- 2. $y_i$ 是第 $th$ 个患者观测到的连续响应变量
- 3. $E_0$ 是基础效应，即剂量为 0 mg 时的响应
- 4. $E_{max}$ 是药物引起的最大效应
- 5. $ED_{50}$ 是产生一半效应的剂量
- 6. $h$ 是 Hill 参数或斜率，用于衡量响应对药物剂量范围的敏感性，决定了剂量-响应曲线的陡峭程度 $(N > 0)$
- 7. $D_i$ 是第 $i$ 个患者的剂量水平
- 8. $\epsilon_i$ 是第 $i$ 个受试者的随机误差。此处采用的一个标准假设是 $\epsilon_i$ 项是独立同分布的，均值为 0，方差为 $\sigma_\epsilon^2$。另一个标准假设是误差项服从正态分布。

图 6.5 Emax 模型剂量响应曲线（重自文献 [24]）显示了基于单调增加假设的典型剂量响应曲线。请注意，模型剂量响应曲线相对于剂量的增加可能是增加的也可能是减少的。如果响应是减少，参数值将为负。

# 图 6.5 Emax 模型剂量响应曲线

![](img/f4ec2665c3484c528370923aeb5cb99f_324_0.png)

上述模型是传统的 4 参数模型（也称为 Sigmoid 模型），常用于剂量响应研究分析。通过 4 个参数（$E_0$、$ED_{50}$ 和 $h$），模型为拟合各种形状的剂量响应关系提供了巨大的灵活性，使其成为流行的剂量响应模型之一。然而，该模型的应用存在一些局限性。首先，由于模型有 4 个参数，至少至少 5 个剂量（可以包含0作为安慰剂），并假设剂量响应曲线是单调的。其次，4 参数模型有时不收敛。在 4 参数模型不收敛或研究仅设计 4 个剂量水平的情况下，通常的做法是移除 Hill 参数，例如通过斜率参数 $h=\uparrow$。此时模型变为 3 参数模型（即所谓的双曲线模型），

```
$y_i = E_0 + E_{max} \tilde{A} - \frac{D_i}{ED_{50}+D_i} + \mu_i$，
```

其中各项的定义与上述 Sigmoid 模型相同。

上述模型假设响应变量是连续的，但有时响应变量可能是二分类的，例如响应率。在这种情况下，可以将模型修改为使用 logit 链接的广义模型：

```
$\log(\frac{\pi}{1-\pi}) = E_0 + E_{max} \tilde{A} - \frac{D^h}{ED_{50}+D^h}$
```

其中 $\pi$ 是观测到的响应率。

在接两个章节中，我们将使用上述模型分析模拟数据，作为应用演示。数据集模拟为 `detcon`（连续连续终点）和 `detbin`（二分类终点）。

### 6.4.2 连续终点

模拟和分析的示例 SAS 代码在示例代码 6.2 中提供，该代码模拟了基于上述模型的数据集。

示例代码 6.2 使用 $Emax$ 模型模拟连续数据的程序

```
data dose;
  input dose@;
  datalines;
0 2.5 10 20
run;

%macro simu(n=, sd=, e0=10, emax=80, ed50=5.5, h=1, outdst=dstcon)
** n 是每个剂量组的样本量；
 proc sql noprint;
  select count(dose)into:ngpr
  from dose;
quit;
%let ngpr=&ngpr;

data data_null;
  set dose;
  mean=&e0.+(&emax.*dose*h)/(ed50.**h);
  call symput("mean"|put(mean, 1));
  call symput("dose"|put(dose, 1));
run;
%do i=1 to &ngpr; %put &i.****mean;
data outdst;
  do i=1 to &ngpr;
  group=&i;
  mean=&mean;
  dose=&dose;
  do n=1 to &n;
  resp=&mean.&sd.*rannor(1500);* 使用种子数1500
  output;
  end;
end;
%mend;
%simu(n=60, sd=10, e0=10, emax=80, ed50=5.5, h=1, outdst=dstcon);
```

示例代码 6.3 下 proc nmixed 使用模拟数据拟合 4 参数模型。

示例代码 6.3 4 参数 $Emax$ 模型拟合 proc nmixed

```
proc nmixed data=dtcn alpha=0.05;
**设置初始值;
parms eo=10 emax=80 edso=5.5 h=1 v=400;
**指定 edso 必须为正;
bounds edso>0;
**定义模型;
if dose=0 then eta=;
else eta= eo + {(emax**h)/(ed50**h)};
model resp= normal(eta, v);
**估计均值差异;
estimate "Diff Means (dose 20mg-placebo)"
  eo+((20**h)/(ed50**h+20**h));
estimate "Diff Means (dose 10mg-placebo)"
  eo+((10**h)/(ed50**h+10**h));
estimate "Diff Means (dose 5 mg-placebo)"
  eo+((5**h)/(ed50**h+5**h));
estimate "Diff Means (dose 2.5mg-placebo)"
  eo+((2.5**h)/(ed50**h+2.5**h));
predict eta=etah;
**输出估计值;
dataset 输出均值差异;
dataset parms 输出参数: e0 emax ed50;
ods output=est ParameterEstimates=parms;
```

使用 proc nmixed 的示例代码 6.3 4 参数 Emax 模型的关键结果在图 6.6 中。图中显示了模型估计剂量的输出以及 95% 置信区间。第一行表示 20mg 剂量与安慰剂之间的均值差异为 60.8，95% 置信区间为 (57.2, 64.4)。

| Label | Estimate | Standard Error | DF | Pr >t | Alpha | Lower | Upper |
|---|---|---|---|---|---|---|
| Diff Means (dose 20mg-placebo) | 60.8246 | 1.8432 | 33.02 | <0001 | 0.05 | 57.1993 | 64.4500 |
| Diff Means (dose 10mg-placebo) | 50.9201 | 1.6521 | 30.89 | <0001 | 0.05 | 47.6761 | 54.1642 |
| Diff Means (dose 5 mg-placebo) | 37.5029 | 1.6567 | 22.84 | <0001 | 0.05 | 34.2428 | 40.7632 |
| Diff Means (dose 2.5mg-placebo) | 23.7832 | 1.7872 | 13.29 | <0001 | 0.05 | 20.2353 | 27.2692 |

图 6.6 示例代码 6.3 输出

如果读者感兴趣使用对比（使用示例代码 6.1 中的 SAS 宏 %poly 生成）练习趋势测试，在下方的示例代码 6.4 中提供了使用模拟数据集生成用于趋势测试的正交多项式的样本代码。多项式的输出显示在图 6.7 中。趋势测试在示例代码 6.5 考虑等间距或不等间距的趋势 POC 中执行，输出显示在图 6.8 中。

# 示例代码 6.4 用于趋势测试的正交多项式程序

```
data dose;
  input dose@;
  datalines;
0 2.5 5 10 20
  run;
  %polyorth(fichin=dose);
```

# 示例 6.7 示例 6.4 输出

| Polynomial degree | level_1 | level_2 | level_3 | level_4 | level_5 |
|---|---|---|---|---|---|
| deg. 1 | -0.47434 | -0.31623 | -0.15811 | 0.15811 | 0.79057 |
| deg. 2 | -0.54598 | -0.33428 | -0.03402 | 0.05163 | 0.40507 |
| deg. 3 | -0.46999 | 0.42226 | 0.51435 | -0.57050 | 0.10388 |
| deg. 4 | -0.23872 | -0.72143 | 0.63125 | -0.15781 | 0.11127 |

# 示例代码 6.5 考虑等间距或不等间距的趋势 POC

```
title "General linear model for PoC hypothesis testing";
proc glm data=dstcon;
  class group;
  model resp = "Trend contrast" group;
  contrast -0.47434 -0.31623 -0.15811 0.15811 0.79057;
```

run;

# 图 6.8 示例 6.5 输出

| Source | DF | Type III | Mean Square | F | Pr > F |
|---|---|---|---|---|---|
| group | 4 | 13867.7035 | 34119.9259 | 328.46 | <0.0001 |

| Contrast | DF | Type III | Mean Square | F | Pr > F |
|---|---|---|---|---|---|
| Trend contrast | 1 | 109819.5017 | 109819.5017 | 1054.98 | <0.0001 |

使用简单的 %polyorth 宏有助于获取实际的

