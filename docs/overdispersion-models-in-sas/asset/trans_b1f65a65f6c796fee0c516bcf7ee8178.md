

# 第 7 章 过离散多项响应的似然模型 233

| 0 | 0 | -1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 1 | -1 | 0 | 0 | 0 | 0 | 0 |
| 带 C= | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 |

因此，用于检验 (7.37) 的 Wald 统计量为：

```
$$X^2 = (C\hat{\theta})^T C \hat{V}(\hat{\theta}) C^{-1} (C\hat{\theta}) \quad (7.38)$$
```

在原假设下，该统计量渐近服从自由度为五的卡方统计分布。在本例中，矩阵 $\hat{V}(\hat{\theta})$ 是满秩的。因此，自由度由矩阵 $C$ 的秩决定，即五。

程序 7.5 包含了使用链接函数 (7.35) 将狄利克雷-多项（Dirichlet-multinomial）和随机聚类多项（Random-clumped Multinomial）模型拟合表 7.2 缺陷研究数据的编程语句。我们跳过了与数据读取相关的语句，这些可以在程序 7.2 中找到。在本例中，我们使用了 NLMIXED 过程。NLMIXED 中的 CONSTRAINT 语句提供了经过自由度归一化的 (7.38) Wald 。这可以用 F 分布近似。由于我们的模型（DM 和 RCM）是基于似然的，我们还可以计算似然比检验以及与 (7.38) 中 Wald 检验对应的得分检验。注意，在 ODS 语句中，已经列出了特定的表格来计算用于检验平行假设的 Wald 检验和似然比检验。涉及累积对数（cumulative logits）的参数初始估计是通过 LOGISTIC 过程链接的（此处未显示）。编程语句由 Sandia 国家实验室的 John New 博士感谢提供。

## 程序 7.5：在狄利克雷-多项和随机聚类多项模型下优势比例假设的检验——产前钙和锌暴露数据

```
/*
来自 Morel 和 Koehler (1995) 的缺陷示例
拟合广义过离散模型
dichlet-multinomial 和 Random-clumped Multinomial
使用 NLMIXED 过程中的
CONSTRAINT 语句检验比例性假设
*/
\ods html;
Title "Testing Proportionality Assumption -- Dirichlet-multinomial Distribution"
ods output Contrast=Prop_Sum_DM FitStatistics=Fit_DM_full
ParameterEstimates=Betas_DM CovMatParmEst=Cov_DM;
Proc nlmixed data=birth_defects;
parms a1=3.7, a2=-2.4, b11=-0.2, b21=-0.2, b12=3.1, b22=3.1,
b13=5.5, b23=5.5, b14=-1.8, b24=-1.8, b15=-1.7, b25=-1.7,
rho=0;
bounds 1>rho=0;
eta1 = a1*zn2*b12*cd2*cd13*b14*zn2_cd2*b15*zn2_cd3;
eta2 = eta2*b21*zn2*b22*cd2*cd23*b23*b24*zn2_cd2*b25*zn2_cd3;
gamma1 = 1/(1+exp(-eta1))
gamma2 = 1/(1+exp(-eta2))
pl1 = gamma1
pl2 = gamma2
p = pl1 - pl2
m = t1+t2+t3
c = (1-rho2)/(rho2);
loglik = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1)
lgamma(c)-lgamma(m+c)-lgamma(t1+c)*lgamma(t2+c)+lgamma(t2*c)
lgamma(t3+c)-lgamma(t3+c)-lgamma(p1)*lgamma(c*p2)-lgamma(c*p3)
+ const;
todel tl = general(loglik);
contrast = "Proportionality Assumption Test -- DM Distribution"
b11-b21, b12-b22, b13-b23, b14-b24, b15-b25;
```

Title Testing Proportionality — Random-coupled Multinomial Distribution;

ods Outputs Contrast-Assump_Rho_RCM FitStatistics=Fit_Rcm_full Full_Dimensions=Dimensions_1
ParameterEstimates=Betas_RCM CoVarMapEstimate=Cov_RCM;

```
Proc nlmix data=defects cov;
params a1=3.7, a2=2.4, b11=0.2, b21=0.2, b31=3.1, b22=3.1,
b13=3.5, b23=3.5, b14=-1.8, b24=-1.8, b15=-1.7, b25=-1.7,
rho=0.5;
bounds 1>rho=0;
eta1 = a1*zn2*b12*cd2*cd13*b14*zn2_cd2*b15*zn2_cd3;
eta2 = eta2*b21*zn2*b22*cd2*cd23*b23*b24*zn2_cd2*b25*zn2_cd3;
gamma1 = 1/(1+exp(-eta1))
gamma2 = 1/(1+exp(-eta2))
pl1 = gamma1;
pl2 = gamma2;
p = pl1 - pl2
m = t1+t2+t3;
hoc = 1-rho2;
loglik = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1)
+ lgamma(hoc)-lgamma(m+hoc)-lgamma(t1+hoc)*lgamma(t2+hoc) + (p*(p1)**t1)*(p*(p2)**t2)*(p*(p3)**t3)
+ const;
todel tl = general(loglik);
contrast = "Proportionality Assumption Test -- RCM"
b11-b21, b12-b22, b13-b23, b14-b24, b15-b25;
ods html;
```

通过程序 7.5 得到的 MLE。

表 7.6：链接函数 (7.35) 下狄利克雷-多项和随机聚类多项模型的似然结果——产前镉和锌数据

| 参数 | Dirichlet-multinomial Estimate | Dirichlet-multinomial Std Err | Random-clumped Multinomial Estimate | Random-clumped Multinomial Std Err |
|---|---|---|---|---|
| $\alpha_1$ | -2.8350 | 0.4261 | -3.1780 | 0.4199 |
| $\alpha_2$ | -2.4428 | 0.3598 | -2.6938 | 0.3366 |
| $\eta_{11}$ | 0.5400 | 0.6032 | 0.6959 | 0.5788 |
| $\eta_{21}$ | 0.4565 | 0.5203 | 0.4877 | 0.4894 |
| $\eta_{12}$ | 2.2039 | 0.5333 | 2.5221 | 0.4994 |
| $\eta_{22}$ | 3.6969 | 0.5265 | 3.9455 | 0.4740 |
| $\eta_{13}$ | 4.8780 | 0.6362 | 5.6568 | 0.6694 |
| $\eta_{23}$ | 6.5592 | 1.0840 | 7.1377 | 1.0645 |
| $\eta_{14}$ | -2.2316 | 0.8287 | -2.5301 | 0.7771 |
| $\eta_{24}$ | -2.6706 | 0.7225 | -2.6513 | 0.6524 |
| $\eta_{15}$ | -2.7366 | 0.8173 | -3.1895 | 0.8172 |
| $\eta_{25}$ | -3.4496 | 1.1897 | -3.5442 | 1.1654 |
| $\rho$ | 0.4262 | 0.0419 | 0.4069 | 0.0362 |
| -2*Log-likelihood | 397.9 | | 402.1 | |

NLMIXED CONTRAST 语句提供的检验比例假设的 F 统计量如下。两个统计量都拒绝了平行假设。

| 狄利克雷-多项分布 | | | | |
|---|---|---|---|---|
| 检验 | | | | |
| | | | | F Value | Pr > F |
| 比例假设检验 -- DM 分布 | 5 | 70 | 4.27 | 0.0119 |

| 随机聚类多项分布 | | | | |
|---|---|---|---|---|
| 检验 | | | | |
| | | | F | Pr > F |
| 比例假设检验 -- RCM 分布 | 5 | 70 | 5.66 | 0.0002 |

程序 7.5 的后续部分提供了计算 Wald 统计量的语句。注意使用 IML 过程通过 LINMIXED 的 ODS 输出计算表达式 (7.38)。

## 程序 7.5：使用 Wald 统计量检验平行假设（延续）

```
ods html;
title "Testing Parallelism Assumption using a Wald Statistic";
data Beta_DM;
  set Beta_DM;
  keep estimate;
run;
data Cov_DM;
  set Cov_DM;
  drop row parameter;
run;
data Beta_RCM;
  set Beta_RCM;
  keep estimate;
run;
data Cov_RCM;
  set Cov_RCM;
  drop row parameter;
run;
proc iml;
  use Beta_DM;
  read all int beta;
  use Cov_DM;
read all into cov;

c={0 0 1 -1 0 0 0 0 0 0,
      0 0 0 1 -1 0 0 0 0 0,
      0 0 0 0 0 1 -1 0 0 0,
      0 0 0 0 0 0 0 1 -0 0};
Degrees_of_Freedom
Degrees_of_Freedom = ncov(cov);

Wald_Statistic = beta * c' * inv(c * cov * c') * c * beta;
P_Value = 1 - probchhi(Wald_Statistic,Degrees_of_Freedom,0);
print "Dirichlet-multinomial Distribution";
print Degrees_of_Freedom Wald_Statistic[format=6.2] P_Value[format=p6.4];

use Beta RCM;
read all into rcm;
use Cov RCM;
read all into cov;

Wald_Statistic = beta * c' * inv(c * cov * c') * c * beta;
P_Value = 1 - probchhi(Wald_Statistic,Degrees_of_Freedom,0);
print "Random-clumped Multinomial Distribution";
print Degrees_of_Freedom Wald_Statistic[format=6.2] P_Value[format=p6.4];
quit;
ods html close;
```

