

# SAS 中的过离散模型

| 使用 PROC PROBIT 的二项分布和 Probit 链接的 GLM |
| 最大似然参数估计分析 |

| 参数 | DF | 估计值 | 标准误 | 95% 置信限 | 卡方 | Pr > ChiSq |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 1 | -5.9139 | 0.1875 | -6.2815 | -5.5464 | 994.63 | <0001 |
| Ln(dose) | 1 | 1.4090 | 0.0402 | 1.3303 | 1.4877 | 1230.23 | <0001 |

| Ln(dose) 上的 Probit 分析 |

| 概率 | Ln(dose) | 95% Fiducial Limits |
| :--- | :--- | :--- | :--- |
| 0.50 | 4.1973 | 4.1574 | 4.2344 |

| dose 上的 Probit 分析 |

| 概率 | dose | 95% Fiducial Limits |
| :--- | :--- | :--- | :--- |
| 0.50 | 66.5040 | 63.90220 | 69.0298 |

似乎没有明确的标准来选择这两种分析（Probit 与 Logit）之间。它们可以被视为由正态分布或逻辑分布触发的潜变量建模。Cox 和 Snell（1989，第 21-22 页）指出，对于大多数目的，逻辑分布和正态分布非常接近，除了当关注极值时，成功概率非常小或非常接近时。累积正态曲线比累积逻辑曲线更快地接近其极限，表明后者比前者具有更长的尾部。程序 2.4 中的编程语句提供了估计概率函数与观察比例的图。（70 多年前，Bliss 和 Berkinson 必须手工绘制这些图！）观察比例 $\hat{P}_j = \frac{t_j}{m}, j=1,2,...,11$ 是 m.，叠加了估计函数。我们首先生成数据集“temp”，剂量值在 38 到 301 范围内，以 10 为增量。变量“$x” 是剂量的自然对数。此数据与数据“pyrethrins”连接。然后拟合两个 GLM：一个使用 Probit 链接，另一个使用 Logit。数据集“temp”未用于计算变量“$t” 和 “$m” 的 MLE 的任何计算中，它们缺失。然而，像许多其他过程一样，GLIMMIX 为缺失数据提供概率估计。它们用于构建平滑的累积概率函数。

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## 第 2 章 广义线性模型

## 程序 2.4：估计正态和逻辑累积分布函数——拟除虫菊酯的剂量-死亡率数据

```
-- Plotting
1)Estimated Logistic Curve and Observed Proportions
2)Estimated Probit Curve and Observed Proportions
temp:
    do dose=38 to 301 by 0.1; -- Dose range in increments of 0.1;
    x = log(dose);
    output;
end;
drop dose;
run;
data new;
    set pyrethrins temp;
run;
proc glimmix data=new;
    model t/m = x / link=probit;
    output=pred_out1(xlink)=pi_hat;
run;
proc glimmix data=new;
    model t/m = x;
    output=pred_out2(xlink)=pi_hat;
run;
data pred_out1;
    set pred_out1;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
data pred_out2;
    set pred_out2;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
html;
ods graphics data=pred_out1;
proc sgplot;
    title "Estimated Probit Curve"
    title2 "Dosage-Mortality of Pyrethrins on Male Flies, Murray (1938)";
    scatter x=x y=pi_hat;
    series x=x y=pi_hat / y2axis;
run;
proc sgplot data=pred_out2;
    title "Estimated Logistic Curve";
```

More, Jorge, and Nagaraj Neelchal. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

```
title2 "Dosage-Mortality of Pyrethrins on Male Flies, Murray (1938)";
scatter x=x y=obs_pi;
series x=x y=pi_hat / y2axis;
run;
ods graphics off;
ods close;
```

SGPLOT 过程用于创建最终绘图（需要 SAS 9 或更高版本）。图 2.4 和 2.5 提供了所讨论的绘图。两幅图之间的差异可能很微妙。读者可以看到累积正态曲线比逻辑曲线更快地接近其极限。在此示例中，逻辑曲线拟合更好，这可以从图中看出。

### 图 2.4：拟除虫菊酯剂量-死亡率数据的估计累积正态函数
img/fa69b48c17ad45ebeb4d92ffb_50.png

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

### 图 2.5：拟除虫菊酯剂量-死亡率数据的估计累积逻辑函数
img/fa69b48c17ad45ebeb4d92ffb_51.png

## 2.8 优势比和逻辑回归

逻辑回归的主要优点之一是其参数可以用优势比来清晰解释，并且能够以多种不同的研究形式实现。考虑一个假设的例子，其中受试者根据风险因素的存在与否以及某种疾病的存在与否进行交叉分类。暴露/疾病的真实且未知的联合概率可以用 2x2 列联表表示

| 暴露因素 | 是 | 否 | 总计 |
| :--- | :--- | :--- | :--- |
| 存在 | $\pi_{11}$ | $\pi_{12}$ | $\pi_{+}$ |
| 不存在 | $\pi_{21}$ | $\pi_{22}$ | $\pi_{++}$ |
| 总计 | $\pi_{+1}$ | $\pi_{+2}$ | 1 |

More, Jorge, and Nagaraj Neerchal. *Overdispersion Models in SAS*. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

其中 $\pi_i = \sum_{j=1}^{2} \pi_{ij}, i=1,2$ 且 $\pi_{\cdot j} = \sum_{i=1}^{2} \pi_{ij}, j=1,2$。在 **前瞻性研究** 中，选择了两个独立的组。来自一组受试者暴露于风险因素，另一组的受试者未暴露。来自两组的受试者随后被随访，研究结束时根据是否患病进行分类。前瞻性研究中疾病的真实且未知的条件概率，给定受试者相对于暴露的状态如下

| 暴露因素 | 是 | 否 | 总计 |
| :--- | :--- | :--- | :--- |
| 存在 | $\pi_{11} / \pi_{++}$ | $\pi_{12} / \pi_{++}$ | 1 |
| 不存在 | $\pi_{21} / \pi_{++}$ | $\pi_{22} / \pi_{++}$ | 1 |

一个常见的风险度量是 **优势比（OR）**，它基于两个优势的比率，即暴露因素存在时患病的优势，以及暴露因素不存在时患病的优势。这些优势定义为

> $\text{Odds(Having the disease when the Exposure Factor is Present)} = \frac{\pi_{11} / \pi_{12}}{\pi_{21} / \pi_{22}}$

和

> $\text{Odds(Having the disease when the Exposure Factor is Absent)} = \frac{\pi_{21} / \pi_{22}}{\pi_{11} / \pi_{12}}$

因此，优势比为

> $OR = \frac{\text{Odds(Having the disease when the Exposure Factor is Present)}}{\text{Odds(Having the disease when the Exposure Factor is Absent)}} = \frac{\pi_{11} / \pi_{12}}{\pi_{21} / \pi_{22}}$

现在考虑一个分类变量 X，如果暴露因素存在则取值为 1，否则取值为 0。令 $\pi(X)$ 表示给定暴露因素 X 时患病的概率。现在，我们对 $\pi(X)$ 提出逻辑回归模型如下：

```
logit(\pi(X)) = \ln\left(\frac{\pi(X)}{1-\pi(X)}\right) = \beta_0 + \beta_1 X .
```

当暴露因素存在时，患病的概率为

```
\pi(X=1) = \frac{e^{\beta_0+\beta_1}}{1+e^{\beta_0+\beta_1}} .
```

同样，暴露因素不存在时患病的概率

```
\pi(X=0) = \frac{e^{\beta_0}}{1+e^{\beta_0}} .
```

因此，可以证明优势比为

```
OR = \frac{\pi(X=1)}{1-\pi(X=1)}}{\frac{\pi(X=0)}{1-\pi(X=0)}} = e^{\beta_1} .
```

该结果是基础的：逻辑回归模型的斜率参数可以用优势比的对数来解释。在之前的设置中，$\beta_1=\ln(OR)$。逻辑回归的主题已被许多作者介绍。我们建议读者参考 Hosner 和 Lemhow（2000）以获取关于逻辑回归的全面文本。

一般来说，如果暴露因素存在，分类变量取 $X=x_1$，如果暴露因素不存在则取 $X=x_2$。优势比由 $OR=e^{(x_1-x_2)\beta_1}$ 给出。特别地，如果使用 $\pm1$ 编码 $OR=e^{\pm\beta_1}$。编码为分析人员提供了直接估计给定研究中影响量的灵活性。

