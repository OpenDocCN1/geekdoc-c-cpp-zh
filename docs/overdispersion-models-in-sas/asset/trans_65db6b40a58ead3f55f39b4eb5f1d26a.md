

# 第6章 针对过度离散计数响应的似然模型 189

```
ods html;
title2 "泊松障碍模型";nproc nlmixed data=Milk Consumption;
parms alpha=0 beta=0;
p1 = 1/(1+exp(-alpha));
mu = exp(beta);
p2 = exp(-mu);
if y=0
else ll = log((1-p1)/(1-p2)) + y * log (mu)
ll -= gamma(y+1)
ll -= freq*ll;
model y = general(1);
predict 1/(1+exp(-alpha)) out=PredMilk_1;
estimate "Mu" = 1/(1+exp(-alpha));
estimate "Mean" = exp(beta);
estimate "Variance" = 1/(1+exp(-alpha))/(1/(1+exp(-alpha)))*exp(beta)*exp(beta);
run;
```

```
title2 "负二项分布障碍模型";nproc nlmixed data=Milk Consumption;
parms alpha=0 beta=0 kappa=0.5;
bounds kappa > 0;
p1 = 1/(1+exp(-alpha));
mu = exp(beta);
a = 1 / (1 + kappa*mu);
p2 = p^a;
if y=0
else ll = log((1-p1)/(1-p2)) + a * log (p) + y * log (1-p)
ll -= gamma(y+a) - gamma(a)
ll -= freq*ll;
model y = general(1);
predict 1/(1+exp(-alpha)) out=PredMilk_2;
estimate 'Pl' = 1/(1+exp(-alpha));
estimate 'Mu' = exp(beta);
estimate 'Kappa' = 1/(1+exp(-alpha))/(1/(1+exp(-alpha)))**(kappa))*exp(beta)*exp(beta);
estimate 'Variance' = 1/(1+exp(-alpha))/(1/(1+exp(-alpha)))**(kappa))*exp(beta) * (1+exp(beta)+kappa*exp(beta);
1/(1+exp(-alpha))/(1/(1+exp(-alpha))**(kappa))*exp(beta)*exp(beta);
1/(1+exp(-alpha))/(1/(1+exp(-alpha))**(kappa))*exp(beta);
run;
```

```
title "牛奶消耗示例 - Mullahy (1986)";
titoc means data=Milk Consumption n mean maxdec=4;
var y;
freq freq;
run;
ods html close;
```

程序 6 结果的选定部分见输出 6。在两种模型中，$\pi_i = Pr(Y, 0)$ 的估计值是相同的，即 $\pi_i = 0.4037$。一旦越过障碍（hurdle），正计数的估计均值为 $(1-\hat{\pi}_1) \frac{\hat{\mu}}{(1-\hat{\pi}_2)}$，其中 $\pi_2 = Pr(Y_2, 0)$。在本例中，两个障碍模型提供了相同的值：1.1095。真实的赤池信息准则 (AIC)、修正信息准则 (AICC) 和施瓦特贝叶斯信息准则 (BIC) 在负二项障碍模型下均较小，这表明该模型可能比泊松障碍模型更优。我们将通过执行与程序 6.2 中计算的类似的皮尔逊拟优度检验来验证这一观察。两种模型下的估计均值（见方程 (6.27) 和 (6.30)）均为 1.1095，这与 MEANS 过程得到的算术均值一致。方差的情况并非如此。泊松障碍模型下的估计方差为 2.28，而负二项障碍模型下的方差（见方程 (6.31)）为 1.568。后者方差更接近 1.564——即 MEANS 过程通常报告的方差。注意，所讨论的两个模型的方差均大于其均值。因此，这些模型表现出过度离散（overdispersion）。此外，在这种情况下泊松分布的估计均值为 1.1095，两个障碍模型相对于泊松分布也表现出过度离散。

# 输出 6.6：拟合两个障碍模型到每日牛奶消耗量的结果 — Mullahy (1986)

| 泊松障碍模型 | 负二项分布障碍模型 |
| :--- | :--- |
| NLMIXED 过程 | NLMIXED 过程 |
| 拟合统计量 | |
| -2 对数似然 | 5470.5 | 5449.9 |
| AIC (越小越好) | 5474.5 | 5455.9 |
| AICC (越小越好) | 5477.5 | 5463.9 |
| BIC (越小越好) | 5474.4 | 5455.8 |
| 其他估计 | |
| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > [t] | Alpha | 下限 | 上界 |
| P1 | 0.4037 | 0.01126 | 7 | 35.86 | <.0001 | 0.05 | 0.3771 | 0.4303 |
| Mu | 0.4037 | 0.01126 | 7 | 35.86 | <.0001 | 0.05 | 0.3771 | 0.4303 |
| Mean | 1.1095 | 0.02749 | 7 | 40.32 | <.0001 | 0.05 | 1.3051 | 1.5013 |
| Variance | 2.28 | 0.0496 | 7 | 29.02 | <.0001 | 0.05 | 1.3184 | 1.5523 |

牛奶奶消耗示例 — Mullahy (1986)

 MEANS 过程

| 分析变量：Y (牛奶数量) | | |
| :--- | :--- | :--- |
| N | 均值 | 方差 |
| 1900 | 1.1095 | 1.5644 |

# 程序 6.7：障碍模型的拟优度检验—每日牛奶消耗数据

```
/*
   牛奶消耗示例 — Mullahy (1986)
*/
%macro gof_test(File,Distribution,DF);
proc iml;
/* 输入：File 包含观测和期望频率
               Distribution 拟合的分布
               DF GOF 检验自由度
   输出：皮尔逊 GOF 统计量及 P 值 */
--- 获取观测和期望频率
use &File var (freq);
read all into obs;
use &File var (pred);
read all into exp_f;
sum1       = obs[,1];
sum2       = exp_f[,1];
exp_f[7,1] = exp_f[7,1] + sum1 - sum2;
sum2       = exp_f[,1];
--- 计算 卡方量和 P 值
chi = 0;
do j = 1 to 7;
  chi = chi + obs[j] * obs[j] / exp_f[j];
end;
chi = round(chi &n, 0.01);
df = &DF;
npval = 1 - probchi(chi,df);
--- 打印结果
print 'Goodness-of-fit Results';
print x0 x1 x2;
print Distribution chi pval;
quit;
%end gof_test;\ods html;
title1 "牛奶消耗示例 — Mullahy (1986)"
title2 "泊松障碍模型";
```

```
%gof_test(Pred_Milk_1,'Poisson Hurdle',7-1-2);
title2 "负二项分布障碍模型";
%gof_test(Pred_Milk_2,'Negative-binomial Hurdle',7-1-3);\ods htm close;
```

