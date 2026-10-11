
请记住，在参数化下，$\rho^2$ 代表一致系数 $\kappa$。以下是使用 `NLMIXED` 过程计算相关多项模型 (7.40) 下 Kappa 系数的编程语句。请注意，原始的 3x3 列联表需要扩展为包含 $n=160$ 个三元响应样本的原始数据。这是使用 `IML` 过程完成的。有 24 个形式为 $(2,0,0)$ 的响应，8 个形式为 $(1,1,0)$，13 个形式为 $(1,0,1)$ 等。

## 问题 6.6：Sissel 和 Ebert 电影评分的 Kappa 系数（续）

```sas
ode html;
proc iml;
  use movie_ratings;
  read all into x;

  n0 = row(x);
  n1 = sum(x[j,3]);
  t1 = j(n1,3,0);
  t2 = j(n1,3,0);

  row = 0;
  do j=1 to n0;
    do t=1 to x[j,3];
      row = row + 1;
      t1[row,x[j,1]] = 1;
      t2[row,x[j,2]] = 1;
    end;
  end;

  t = t1 + t2;
  create new var(t3);
```

Morel, J., and Nagaraj Neeraj. Overdispersion Models in SAS.. © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 需更多 SAS 信息，请访问 support.sas.com/publishing。

```sas
append tm;
quit;
ods output ParameterEstimates=Parms_Estimates
AdditionalEstimates=Estimates;
proc nlmixed a=0 data=new;
parms a=0, b0=0, b02=0;
rho = -1 / (1 + exp(-a0));
etal = exp(b01);
eta2 = exp(b02);
p1 = etal/(1+etal+eta2);
p2 = eta2/(1+etal+eta2);
p3 = 1-p1-p2;
t3 = t1+t2;
c = (1-rho**2)/(1+rho**2);
const = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1);
  loglik = lgamma(c)-lgamma(m+c)+lgamma(t1+c+1)+lgamma(t2+c*p2)
  +lgamma(t3*c+p3)-lgamma(c*p1)+lgamma(c*p2)-lgamma(c*p3);
model t1 ~ general(loglik);
estimate 'Kappa' / 1 / (1 + exp(-a0)) / (1 + exp(-a0));
run;
```

```sas
data Estimates;
set Estimates;
rename Estimate = Kappa;
keep Estimate Lower Upper;
run;
```

```sas
data Parm_Estimates;
set Parm_Estimates;
if Parameter = 'a0';
Estimate = 1 / (1 + exp(-Estimate)) / (1 + exp(-Lower));
Lower = 1 / (1 + exp(-Lower)) / (1 + exp(-Lower));
Upper = 1 / (1 + exp(-Upper)) / (1 + exp(-Upper));
rename Estimate = Kappa;
keep Estimate Lower Upper;
run;
```

```sas
title2 "使用 NLMIXED 中估计值的 Kappa 结果";
proc print data=Estimates;
run;
```

```sas
title2 "使用 NLMIXED 中逆方法的 Kappa 结果";
proc print data=Parms_Estimates;
run;
```

注意，在 `NLMIXED` 中 $\kappa$ 被重参数化为 $\frac{\exp(\hat{\alpha}_0)}{1+\exp(\hat{\alpha}_0)}$。$\hat{\kappa}$ 的估计方差 $\hat{v}(\hat{\kappa})$ 使用泰勒线性计算。因此，$\kappa$ 的近似 95% 置信区间为 $\hat{\kappa}\pm 1.96\sqrt{\hat{v}(\hat{\kappa})}$。为了保证置信区间落在 0-1 之间，需要使用逆方法。如果 $\hat{L}$ 和 $\hat{U}$ 分别对应于 $\alpha_0$ 的 95% 置信区间边界，则通过逆方法得到的 $\kappa$ 的近似 95% 置信区间为：

$$\left\{ \frac{\exp(\hat{L})}{1+\exp(\hat{L})}, \frac{\exp(\hat{U})}{1+\exp(\hat{U})} \right\}$$

以下是使用 `NLMIXED` 的置信区间结果。

![](img/fa69b648c17ad45ebe4ad92f57_0)

![](img/fa69b648c17ad45ebe4ad92f57_1)

`FREQ` 和 `NLMIXED` 过程提供的结果非常一致。注意相关模型 (7.40) 属于广义线性离散模型族，允许对在本章之前讨论的概率向量 $\pi$ 和离散参数 $\rho$ ($\kappa=\rho^2$) 使用连接函数。希望读者注意，Landis 和 Koch (1977) 为解释 Kappa 值提供了以下指南。这些指南并非所有统计学家都接受。

### 7.8 解释 Kappa 的指南

| Kappa | 解释 |
| :--- | :--- |
| < 0 | 无一致 |
| 0 — 0.20 | 极低 |
| 0.21 — 0.40 | 低一致 |
| 0.41 — 0.60 | 中等一致 |
| 0.61 — 0.80 | 完全一致 |
| 0.81 — 1.00 | 完美一致 |

根据这些指南，任何大于 0.60 的 Kappa 值都被视为完全一致或完美一致。由于 Sissel 和 Ebert 评分的 Kappa 点估计值为 0.38，近似 95% 置信区间约为 (0.26, 0.51)，根据上述指南，可以说两个电影之间的一性在低到中等之间。

### 附录 7.1：Dirichlet-多项和随机聚类多项分布的数据生成

在本附录中，我们描述在 Dirichlet-多项或随机聚类多项分布下随机样本 $\mathbf{t}_1, \mathbf{t}_2, \dots, \mathbf{t}_n$ 的生成。

在 Dirichlet-多项模型下，首先从 $(d+1)$ 维 Dirichlet 密度函数生成随机样本 $\mathbf{p}_1, \mathbf{p}_2, \dots, \mathbf{p}_n$：

$$f_D(\mathbf{p}; \alpha_1, \alpha_2, \dots, \alpha_{d+1}) = \frac{\Gamma(\alpha_1 + \alpha_2 + \dots + \alpha_{d+1})}{\prod_{i=1}^{d+1} \Gamma(\alpha_i)} \prod_{i=1}^{d+1} p_i^{\alpha_i-1}$$

其中 $\alpha_i = c\pi, i=1,2,\dots,(d+1), c = \rho^2(1-\rho), 0 < \rho < 1,$ 且 $\Gamma(\cdot)$ 表示 Gamma 函数。然后，给定 $\mathbf{p}_j, j=1,2,n$，从参数为 $\mathbf{p}_j$ 和 $m$ 的多项分布生成 $\mathbf{t}_j$。T$ 的无条件分布是 Dirichlet-多项分布，其概率函数如方程 (7.30)。`IML` 库中的 `RANDDIRICHLET` 函数用于从 Dirichlet 分布生成随机样本。

Dirichlet 变量 $\mathbf{p}_j$ 可以从 Beta 变量获得（Brier, 1979, 定理 4.1; Kotz, Balakrishnan, and Johnson, 2000, p. 448）。在下面的讨论中，为了方便，我们省略了下标 '$j$'。从参数为 $\alpha_1 = c\pi_1, \alpha_2 = c(1-\pi_1)$ 的 Beta 分布生成 $X_i$，则 $p_1 = x_1$。然后从参数为 $\alpha_1 = c\pi_1, \alpha_2 = c(1-\pi_1-\pi_2)$ 的 Beta 分布生成 $x_2$，并计算 $p_2$：

$p_2 = x_2(1-p_1)$。每个 Dirichlet 分布的第 $d$ 个分量获取为：

$p_d = x_d \sum_{i=1}^{d} p_i$，其中 $x_d$ 是从参数为 $\alpha_i = c\pi_d$ 和 $\alpha_2 = c(1-\sum_{i=1}^{d} \pi_i)$ 的 Beta 分布生成的（此处原文公式可能有笔误，通常应为 $1-\text{sum}$，注：原文此处为 $1-\pi_1-\pi_2$）。因此，$p_{d+1} = 1-\sum_{i=1}^{d} p_i$，所以不需要生成 $(d+1)$ 个分量。

## 248 SAS 中的过度离散模型

```sas
do j=1 to n;
  p = RANDDIRICHLET(1, shape);
  p = p ||/ (1-sum(p));
  t = RANDOMMULTOMIAL(1,m,p);
  t_dm[j] = t[1:d];
end;

* 在随机聚类多项分布下生成数据
do j=1 to n;
  y = RANDOMMULTOMIAL(1,1,pi);
  call randgen(n,"BINOM",m,rho);
  t = y*nn; * 数据的随机聚类;
  if nc < m then t = t + RANDOMMULTOMIAL(1,m-n,pi);
  t_cm[j] = t[1:d];
end;

start mean_var(t,n,d);
  SampleMean = t[::];
  SampleCov = (t*t - SampleMean*SampleMean) / (n-d);
  print SampleCov[format=8.4],];
finish mean_var;
print 'Sample Mean and Covariance -- Dirichlet-multinomial Model';
call mean_var(t,dm,n);
print 'Sample Mean and Covariance -- Random-clumped Multinomial Model';
call mean_var(t_cm,n,d);
quit;
ods html close;
```

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_260_0.png)

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。 如需更多 SAS 资源，请访问 support.sas.com/publishing。

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_261_0.png)

### 附录 7.2: 模块 "DirMult_RCMult"

```sas
Proc IML;
/************************************************************************/
/* MLE 函数                                                              */
/************************************************************************/
/**********************************************************************/
/* Module: MLEDM(m,T)                                                              *
/* 此模块使用费舍信息 *
/* Matrix和费舍评分算法从狄利克特 *                               
/* 多项分布中计算极大似然估计 (MLE) *
/* m - 聚类大小                                                              *
/* T - nxk 计数矩阵 (t1,t2,...,tk)，其中 ti 是 *                               
/* nxl1 向量，表示类别 i 中的观测计数 *                                     /
/**********************************************************************/
Start MLEDM(m, T);
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersed Models in SAS.. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

## 250 SAS 中的过度离散模型

```sas
*** 费舍评分法 -- 狄利克特多项分布 ***;

pi0 = QLEpi(m,T);
rho0 = QLErho(m,T,pi0);
k = ncol(T);
n = nrow(T);
theta = j(k,1,0);
theta[1:k-1] = pi0;
theta[k] = rho0;

eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);

    iter = iter + 1;
    pi = theta[1:k-1];
    rho = theta[k];
    INVNFIM = Inv(n*FIMDM(m, pi, rho));
    Old = 0;
    Scores = j(k,1,0);
    Do j = 1 to n;
        tj = T[j,1:k-1];
        Scores = Scores + gradDM(m, pi, rho, tj);
        Old = Old + log(ProbDM(m, pi, rho, tj));
    End;

    si = 0;
    Lnew = Old - 1;
    Do Until (Lnew > Old);
    thetaNew = theta + {0.5*si}INVNFIM*Scores;
    pi = thetaNew[1:k-1];
    rho = thetaNew[k];
    Lnew = 0;
        Do j = 1 to n;
            tj = T[j,1:k-1];
            Lnew = Lnew + log(ProbDM(m, pi, rho, tj));
        End;

        si = si + 1;
        if si > 20 then;
            print "NOTE: 步长减了二十次，假设收敛";
            Lnew = Old + 0.000001;
        end;
    End;

    theta = thetaNew;
    conv = abs(Lnew)/(abs(Lnew)+1E-6);
    conv_0 = conv;

    if si > 20 then conv = eps - 0.000001;
    if iter > 100 then;
        print "NOTE: 迭代 100 次后，尚未满足收敛";
        conv = eps - 0.000001;
    end;

End;

if conv_0 < eps then;
    print "NOTE: 收敛标准 (EPSILON-1E-8) 已满足";
end;
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersed Models in SAS.. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 7 章 过度离散多项响应的似然模型
