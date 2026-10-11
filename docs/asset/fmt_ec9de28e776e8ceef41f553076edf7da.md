
```sas
  read all(Pred) into Predicted;

  gof = sum(Observed # Predicted) - &n;

  pvalue = 1 - probchi(gof,df,0);

  Summary = j(3,1,0);

  Summary[1,1] = gof;

  Summary[2,1] = &df;

  Summary[3,1] = pvalue;

  label = { 'Pearson's GOF Test',

  'Degrees of Freedom',

  't-value'};

  print &title;

  print Observed Predicted[format=10.4];

  print Summary[label=rowname format=10.4];

quit;

%mend gof;

ods html;

%gof(pred1,1,'Binomial Distribution');

%gof(pred2,1,'Beta-binomial Distribution');

%gof(pred3,1,'Random-connected Binomial Distribution');

%gof(pred4,1,'Zero-correlated Binomial Distribution');

%gof(pred5,1,'Generalized-Binomial Distribution -- Additive Interaction');

ods html close;
```

输出 4.2 仅显示了 Beta 二项分布的拟合度结果。

# 第 4 章 用于过度离散二项响应的似然模型

## 输出 4.2：Beta 二项分布下的拟合度结果

| Beta 二项分布 |
| 观测值 | 预测值 |
| 32 | 33.9692 |
| 103 | 97.1628 |
| 122 | 127.6667 |
| 80 | 78.2014 |

| 总结 |
| 皮尔逊拟合优度检验 | 0.7577 |
| 自由度 | 1.0000 |
| P 值 | 0.3840 |

表 4.3 显示了本示例中考虑的五种分布下关联数量的观测频率和期望频率。二项分布并没有很好地拟合数据，因为在 2 个自由度下，$X^2 = 8.11$，对应的 P 值为 0.017。对于零值膨胀二项分布（Zero-inflated Binomial），也可以观察到类似的现象，其在 1 个自由度下，$X^2 = 4.71$，对应的 P 值为 0.030。自由度的计算方法为（类别数减去1）减去（估计的参数个数）。在二项分布的情况下，自由度为 $(4-1)=2$。过度离散分布多额外的参数 `ρ`，这使得它们的自由度变为 $(4-1)-2=1$。二项分布、随机聚类二项分布和具有加性交互作用的广义二项分布能够较好地拟合关联数量的分布，其卡方检验的 P 值 值分别为 0.384、0.347 和 0.439。当存在多个模型且它们都符合拟合度标准，且模型之间互不嵌套时，很难选出一个单一模型作为最终建议。这种情况也发生在回归建模的情况下。因此，建议与领域专家讨论这些选项，并向他们说明每个模型的含义，同时就哪种模型更接近他们研究的现象征求他们的意见。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

### 表 4.3：染色体数据的皮尔逊卡方拟合度检验

| 关联数量 | 观测频率 | 二项分布 | Beta 二项分布 | 随机聚类二项分布 | 零值膨胀二项分布 | 广义二项分布 |
|---|---|---|---|---|---|---|
| 0 | 32 | 24.86 | 33.97 | 34.08 | 32.00 | 33.91 |
| 1 | 103 | 103.24 | 97.16 | 96.82 | 93.60 | 97.55 |
| 2 | 122 | 142.94 | 127.67 | 128.24 | 140.80 | 126.84 |
| 3 | 80 | 65.96 | 78.20 | 77.85 | 70.60 | 78.70 |
| $\chi^2$ | | 8.11 | 1 | 1 | | 1 |
| P 值 | | 0.017 | 0.384 | 0.347 | 0.030 | 0.439 |

## 染色体数据的皮尔逊卡方拟合度检验

正如我们之前看到的，对于聚类大小 `m`，Beta 二项分布和随机聚类分布几乎是完全相同的。请注意，当 `ρ` 接近单位1 时，它们之间的差异会变得显著。

[注：OCR 文本包含大量的重复和乱码部分，已根据逻辑流进行了清理。]

## 表 4.4: 当 `π=0.3, ρ=0.2,0.7` 且 `m=4,20` 时，Beta二项分布与随机聚集二项分布的偏度

| `ρ` | m | Beta-二项分布 (Beta-binomial) | 随机聚集二项分布 (Random-clumped Binomial) |
|---|---|---|---|
| 0.2 | 4 | 0.5076 | 0.5184 |
| | 20 | 0.3621 | 0.5029 |
| 0.7 | 4 | 0.8256 | 0.8396 |
| | 20 | 0.8204 | 0.8622 |

当 `ρ=0` 时，这两个分布的峰度系数 (4.25) 和 (4.26) 变为 `{1+6ρ(1-π)}/mπ(1-π)+3`，这正是二项分布的峰度系数。对于退化情况 `ρ=1`，Beta-二项分布和随机聚集二项分布的峰度系数为 `1/{π(1-π)}`。为了对 Beta-二项分布和随机聚集二项分布的峰度进行有意义的比较，我们考虑 `π=0.5` 的情况，此时两种分布都是对称的。也就是说偏度系数为零。对于 `π=0.5`，Beta-二项分布和随机聚集分布的峰度系数变为：

```
Kurtosis(Beta-binomial when π=0.5) = \frac{(3m-2)+\{3m(m-1)+2\}\rho^2}{m[1+(m-1)\rho^2]^2}$ (4.27)
```

以及

```
Kurtosis(Random-clumped when π=0.5) = \frac{(3m-2)+\{2(m-1)(3m-4)\rho^2+(m-1)(m-2)(m-4)\rho^4}{m[1+(m-1)\rho^2]^2}$ (4.28)
```

可以证明，对于 `π=0.5`，当 `ρ<1` 时，随机聚集二项分布的峰度系数小于 Beta-二项分布。任何对称 Beta-二项分布的尾部都比对应的随机聚集二项分布尾部更厚。表 4.5 展示了 `π=0.5, ρ=0.2,0.7` 且 `m=5,20` 时峰度系数 (4.27) 和 (4.28) 的值。对于任何给定的 `ρ` (`0<ρ<1`)，随着簇大小 `m` 的增加，两种分布的峰度趋于相互发散。对于固定的 `m`，随着 `ρ` 趋于 1，两种分布的峰度都会减小。

## 第4章 针对过度离散二项响应的似然模型

**表 4.5：** Beta-二项分布与随机聚集二项分布的峰度
`π=0.5, ρ=0.2,0.7` 且 `m=4,20`

| | m | Beta-二项分布 | 随机聚集二项分布 |
|---|---|---|---|
| `ρ` | | | |
| 0.2 | 4 | 2.3810 | 2.3776 |
| | 20 | 2.7273 | 2.4603 |
| 0.7 | 4 | 1.4630 | 1.4326 |
| | 20 | 1.5127 | 1.1744 |

我们继续对概率函数进行视觉评估。程序 4.3 提供了为给定的 `π, ρ` 和 `m` 生成 Beta-二项分布和随机聚集二项分布概率函数的编程语句。

### 程序 4.3：Beta-二项分布与随机聚集二项分布的概率函数图

```sas
/*

Plots of Probability Functions of

the Beta-binomial and Random-clumped Binomial Distributions

*/

%macro plots_bb_rcb(pi,rho,m);

data bb rcb;

format Distribution $14;

label Prob = "Probability";nlabel t = "Number of Successes (t)";

pi = &pi;

rho = &rho;

m = &m;

c = 1 - rho / (rho - 1);

p1 = 1 - pi;

pl1 = (1 - rho)*pi + rho;

lc1 = 1 - p1;

p2 = pi - rho;

c2 = 1 - p2;

do t=0 to m;

Z = exp(z + gamma(c) + gamma(t+c*pi) + gamma(m-t+c*pi));

Prob = gamma(m-c) - gamma(c*pi) - gamma(c*pi);

Distribution = 'Beta-binomial';

output;

Prob = exp(z) * (pi*p1**t*pl1**(m-t) + pi*p2**t*c2**(m-t));

Distribution = 'Random-clumped Binomial';

output;

end;

keep t Prob Distribution;

run;

title1 "Probability Functions Beta-binomial and Random-clumped Binomial Distributions";

ntitle2 "with Pi=&pi Rho=&rho and m=&m";

proc sgpanel data=bb rcb;

panelby / spacing=8;

var t / response=Prob group=Distribution;

run;

%mend plots_bb_rcb;

%plots_bb_rcb(0.3, 0.7, 20);

%plots_bb_rcb(0.5, 0.5, 20);

%plots_bb_rcb(0.5, 0.8, 20);
```
