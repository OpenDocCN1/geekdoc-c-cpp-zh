

# 第10章 广义线性过度散混合模型 349

# 程序 10.2：拟合泊松 GLMM——法利核电站1号机的泵可靠性数据

```sas
/*
压水反应堆核电站的泵可靠性
Gaver and O'Muirchheartaigh (1987)
Draper (1996) */

data pump;
  pump = _n;
  input group y;
  logstd = log(t) - 2.5469400;
  datalines;
  1 1 94.320
  1 5 62.880
  1 14 127.560
  1 19 31.440
  2 1 15.720
  2 3 3.240
  2 1 1.048
  2 2 1.048
  2 4 2.096
  2 22 10.480;
;
```

```sas
ods html;
title "压水反应堆核电站的泵可靠性";
proc glimmix data=pump method=quad;
  class group;
  model y = group logstd*group / noint dist=poisson link=log
    solution ddfm=residual;
  random it / subject=pump;
  estimate "Difference Y-intercepts" group 1 -1;
  estimate "Difference Slopes" group 1 -1;
run;
ods html close;
```

在协方差分析（ANCOVA）中，对于响应变量 Y 和协变变量 X，“MODEL Y = X GROUP X*GROUP” 提供了组间直线平行性的检验（即斜率相等性）。将之前的 ANCOVA 模型重新参数化为“MODEL Y = X*GROUP / NOINT”，可以获得回归线 y 截距和斜率的无偏估计。程序 10.2 通过 GLIMMIX 针对 (10.13) 中描述的泊松 GLMM 请求了后一种重新参数化方法。输出 10.2 提供了程序 10.2 输出的节选。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 support.sas.com/publishing。

# 输出 10.2：程序 10.2 的部分结果——法利核电站1 号机的泵可靠性数据

| 压水反应堆核电站的泵可靠性 |
| :--- |
| GLIMMIX 过程 |
| 拟合统计量 | |
| -2 Log Likelihood | 56.07 |
| AIC (越小越好) | 66.07 |
| AICC (越小越好) | 81.07 |
| BIC (越小越好) | 67.58 |
| CAIC (越小越好) | 72.58 |
| HQIC (越小越好) | 64.41 |
| 协方差参数估计 | |
| Cov Parm | Subject | Estimate | Standard Error |
| Intercept | pump | 0.5314 | 0.3415 |
| 固定效应解 | | |
| Effect | Group | Estimate | Standard Error | DF | t Value | Pr >t| |
| group | 1 | 2.9644 | 1.3826 | 6 | 2.14 | 0.075 |
| group | 2 | 1.7992 | 0.5492 | 6 | | 0.0169 |
| logstd*group | 1 | -0.4256 | 0.7473 | 6 | -0.57 | 0.5896 |
| logstd*group | 2 | 0.6097 | 0.3814 | 6 | 1.60 | 0.1610 |
| 固定效应的 III 型检验 | | |
| Effect | Num DF | Den DF | F Value | Pr > F |
| Group | 2 | 6 | 7.63 | 0.0224 |
| logstd*group | 2 | 6 | 1.44 | 0.3083 |

表 10.3：GLMM–法利核电站1 号机泵可靠性数据主要结果

| 泵类型 | 参数 | 估计 | 标准误差 | P 值 |
| :--- | :--- | :--- | :--- | :--- |
| 连续 | Intercept | 2.9644 | 1.3826 | 0.0757 |
| | Slope | -0.4256 | 0.7473 | 0.5896 |
| 间歇 | Intercept | 1.7992 | 0.5492 | 0.0169 |
| | Slope | 0.6097 | 0.3814 | 0.1610 |
| | Difference Y-intercepts | 1.1653 | 1.4855 | 0.4626 |
| | Difference Slopes | -1.0354 | 0.8389 | 0.2633 |
| | σ² | 0.5314 | 0.3415 | |
| | -2log-likelihood | 56.07 | | |

表 10.3 提供了每条线的参数估计值、标准误差和 P 值。没有证据表明 y 截距存在显著差异（P 值=0.4626）。此外，斜率在统计学上没有差异（P 值=0.2633）。使用 NLMIXED 过程拟合泊松 GLMM (10.13) 的编程语句如下所示。对于自由度，在 GLMIX 中由于使用了“residual”选项自由度为 6，而在 NLMIXED 中，结果是相同的。

```sas
proc nlmixed data=pump;
  parms logstd 0 beta1 beta2 1 alpha1 alpha2 1;
  if (group = 1) alpha = alpha1+ beta1*logstd;
  else alpha = alpha2+ beta2*logstd;
  lambda = exp(alpha);
  y = poisson(lambda);
  random = normal(0,exp(2*logstd)) subject=pump;
  estimate 'alpha-alpha2' alpha-alpha2;
  estimate 'beta-beta2' beta-beta2;
  estimate 'Sigma*' exp(2*logstd);
run;
```

# 10.4 效应模型

本节将利用 9.9 中的肩痛研究演示多项分布模型的拟合。在该研究中，有 22 名实验组（有抽吸），19 名对照组（无抽吸）。回想腹腔镜手术后，患者被要求在术后三天内每天上午和下午对视觉模拟评分进行评分。响应是定序的，其中“1”表示“低疼痛”，“5”表示“高疼痛”。协变量是性别、年龄和时间，所有时间都是个体特异的。令 $y_{ij}$ 表示第 $i$ 组第 $j$ 个受者在 $t$ 个时刻的响应，$i=1, 2, j=1, 2, \dots$ （$n_i=22, n_j=19, t=1, 2, \dots$），其中

$$E(y_{ij}) = \frac{\pi_{1ij}}{\pi_{1ij} + \pi_{2ij} + \pi_{3ij} + \pi_{4ij}}$$

注意，具有重复测量值的个体构成了一个簇。我们考虑以下 Logit GLMM：

$$\ln(\pi_{1ij} / (\pi_{2ij} + \pi_{3ij} + \pi_{4ij})) = \alpha_1 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$
$$\ln(\pi_{2ij} / (\pi_{1ij} + \pi_{3ij} + \pi_{4ij})) = \alpha_2 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$
$$\ln(\pi_{3ij} / (\pi_{1ij} + \pi_{2ij} + \pi_{4ij})) = \alpha_3 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$
$$\ln(\pi_{4ij} / (\pi_{1ij} + \pi_{2ij} + \pi_{3ij})) = \alpha_4 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$

其中 $u_{ij}$ 是独立同分布的 $N(0, \sigma^2)$。

