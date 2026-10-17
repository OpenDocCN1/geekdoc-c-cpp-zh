
简单加权估计量仅利用了完整观测的数据。因此它不是高效的，特别是在删失严重的情况下。改进它的一种方法是获取来自删失观测的信息或来自删失和未删失观测的可用成本。为了提高简单加权估计量的效率，Bang 和 Tsiatis（2000）提出了分区估计量。它将区间 `[0, L]` 分成更小的区间，然后对所有区间进行求和。后来，Zhao 和 Tian（2001）展示了一种更方便、更高效的估计量，它属于 Bang 和 Tsiatis（2000）针对平均成本的通用估计量类，但它不需要对健康史进行分区。Priefer 和 Bang（2005）为这种改进的估计量建议了一个易于使用的公式，其可以写为：

$$\hat{\mu}_{IMP} = \frac{1}{n} \sum_{i=1}^{n} \frac{\Delta U_i}{\hat{R}(T_i)} + \frac{1}{n} \sum_{i=1}^{n} \frac{(1 - \Delta_i)}{\hat{R}(C_i)} \{U_j - \bar{U}(C_j)\} \quad (3)$$

$$\bar{U}(C_j) = \frac{\sum_{i=1}^{n} U_i(C_i)(X_i \geq C_j)}{\sum_{i=1}^{n}(X_i \geq C_j)}$$

其中 $\bar{U}(C_j)$ 是在时间 $C_j$ 仍在观测状态下的个体的平均成本。Zhao 等同事（2007）已经证明，当分区边界选择在删失时间时，该估计量与 Bang 和 Tsiatis（2000）的分区估计量以及 Lin 等同事（1997）的 A 和 B 估计量等价。

成本改进估计量的方差估计给出：

$$\hat{V}(\hat{\mu}_{IMP}) = \hat{V}(\hat{\mu}_{WT}) \frac{1}{n^2} \sum_{j=1}^{n} \frac{(1 - \Delta_j)^2}{\hat{R}(C_j)\hat{R}(\bar{C})} \sum_{i=1}^{n} \frac{\Delta L_i(X_i)(X_i \geq X_i)}{\hat{R}(T_i)} \{U_i(X_i) - \bar{U}(X_i)\} \quad (4)$$

## 368 使用 SAS 分析观测数据

这种改进估计量并不保证比简单加权估计量高效，但在大多数现实情况下，它的表现会优于简单加权估计量。对于两种估计量，我们假设可以计算个体在删失或死亡某一时刻的总成本。当存在缺失数据时，必须首先采用适当的处理方法（Briggs 等，2003）。Wang 和 Zhao（2006）讨论了某些个体成本删失早于生存删失的特殊情况。

### 16.2 增量成本效益比及其信区间

我们考虑两一组试验的增量成本效益比。对于组 $k(k=0,1)$ $\hat{\mu}_k^U$ 为平均成本，$\hat{\mu}_k^S$ 为限制在 `[0, L]` 窗口内的平均生存时间。ICER 通过下式估计：

$$\frac{\hat{\mu}_1^U - \hat{\mu}_0^U}{\hat{\mu}_1^S - \hat{\mu}_0^S}, \quad (5)$$

其中 $\hat{\mu}_k^U$ 和 $\hat{\mu}_k^S$ 分别是组 $k(k=0,1)$ 的平均成本和平均生存时间估计量。平均生存时间可以使用 `[0, L]` 上生存函数的 Kaplan-Meier 曲线下的面积来估计，这等于 $\hat{\mu}^T = \frac{1}{n}\sum_{i=1}^T \frac{\Delta t_i}{d_i}$，$T$ 在时间 $L$ 截断。

获取 ICER 信区间的方法有。第 14 章提供了自助方法的示例。我们使用 Fieller 定理（Fieller, 1954），因为 (5) 中的分子 $x = \hat{\mu}_1^U - \hat{\mu}_0^U$ 和分母 $y = \hat{\mu}_1^S - \hat{\mu}_0^S$ 渐近服从双正态分布，符合该定理的要求。因此，ICER 的 $100(1-\alpha)$ 百百分比置信限为：

$$xy - z_{\alpha/2}^2S_{xy} \pm \sqrt{f(x,y,S_{xx},S_{yy})(y^2)} \quad (6)$$

其中 $f(x,y,S_{xx},S_{yy}) = S_{xx}y^2 + S_{yy}x^2 - 2S_{xy}xy$。

## 第 16 章 删失数据的成本与成本效益分析 369

### 16.3 示例

#### 16.3.1 研究描述

为了说明讨论的方法，我们使用多中心自动除颤试验（MADIT）的数据。MADIT 是一项随机临床试验，检查了植入式除颤器（ICD）预防猝死的有效性（Moss 等，1996）。从 36 个中心共募了 181 名患者，89 人分配到治疗组接受 ICD，92 人分配到控制组接受常规治疗。第一个入组患者随访了 61 个月，最后一个少于 1 个月。原始成本分析限制在 4 年期间，并使用与 Lin 等同事（1997）提出的类似的方法进行。数据被严重删失，ICD 组删失率为 70%，常规治疗组删失率为 48%。改进估计量允许我们获取来自删失观测的信息。对于成本效益分析，ICER 也使用估计成本的改进方法进行计算。正如成本效益分析中常见的，成本和生存时间都按 3% 的年利率折现。

#### 16.3.2 数据分析

每个治疗组的数据来自单独的文件，一个包含生存信息，另一个包含成本。生存数据包含三个变量：个体 ID、生存时间（天）和生存状态（1=死亡；0=删失）。由于许多成本（如住院费用）在特定时期内积累，因此它们通过开始时间、停止时间和期间内的总成本（美元）进行记录。这些成本已按 3% 的年利率折现。以下是检查 ICD 组两个文件前 10 个观测值的 SAS 代码和输出。

### 程序 16.1 查看生存文件的 SAS 代码

```
filename local "C:\Documents and Settings\My Documents\Example";
nproc print data=local.survl (obs=10);
run;
```

## 370 使用 SAS 对观察性健康数据的分析

程序 16.1 的输出

| Obs | id | delta | surv |
|---||--|--|--|
| 1 | 1 | 0 | 167 |
| 2 | 2 | 0 | 1582 |
| 3 | 3 | 0 | 1792 |
| 4 | 4 | 0 | 1303 |
| 5 | 5 | 0 | 1204 |
| 6 | 6 | 0 | 763 |
| 7 | 7 | 0 | 453 |
| 8 | 8 | 0 | 1644 |
| 9 | 9 | 0 | 1818 |
| 10 | 10 | 10 | 804 |

程序 16.2 查看成本文件的 SAS 代码 (obs=10)

```
proc print data=local.cost1;
run;
```

程序 16.2 的输出

| Obs | cid | start | stop | cost |
|---|---|---|---|---|
| 1 | 1 | 1 | 29 | 133.12 |
| 2 | 1 | 1 | 29 | 16.44 |
| 3 | 1 | 1 | 158 | 421.75 |
| 4 | 1 | 1 | 158 | 28.94 |
| 5 | 1 | 1 | 158 | 25.28 |
| 6 | 1 | 1 | 158 | 29.80 |
| 7 | 1 | 1 | 158 | 2.79 |
| 8 | 1 | 5 | 7 | 32764.22 |
| 9 | 1 | 29 | 158 | 79.48 |
| 10 | 1 | 30 | 120 | 150.99 |

分析过程中使用了 SAS/IML 软件。由于我们的公式涉及 Kaplan-Meier 估计器，我们需要在 SAS Stat Studio (SAS/IML Studio) 中调用 SAS LIFETEST 程序，这使我们能够完成此任务。以下程序在环境中运行。对于每组生存和成本数据、用户定义的时间限制 `L` 以及折现率 `r`，程序会计算并打印成本估计值（简单加权和改进型）、平均（折现）生存时间以及估计的方差和协方差。

### 程序 16.3 成本分析的 SAS 代码

```
libname local "C:\Data and Settings\hongweiMy\Documents\Home\SASBook\Example";
```

```
/* 读取生存数据 */
use local.surv;
read all var {id delta surv};
/* 受者 ID、死亡指示和生存时间; */
close local.surv;
```

```
/* 读取成本数据 */
use local.cost;
read all var {cid start stop cost};
/* 受者 ID、成本开始日期、停止日期、产生的成本 */
show names;
close local.cost;
```

```
/* 定义全局变量 */
n=nrow(id); /* 受者数量 */
nobs=nrow(cid); /* 成本数据的总观测数 */
L=1461; /* 时间限制 */
r=0.03; /* 年度折现率 */

/* 将生存时间截断到 L，命名新变量 tsur 和 tdelta */
run TranSurv(delta, surv, tdelta, tsur);

/* 将最大的观测值视为失效 */
do i = 1 to n;
if (tsur[i] == L) then tdelta[i]=1;
end;

/* 计算删失数据的百分比 */
percens=CalCenter(tdelta);
print , "Percent of censoring = %%%"

/* 计算 K(t)=Pr(C>t) 的 Kaplan Meier 估计器，命名为 kc */
run KmCal(tsur,tdelta,kc);

/* 计算 S(t)=Pr(C>t) 的 Kaplan Meier 估计器，命名为 s */
censor=j(n,1,0);
do i = 1 to n;
censor[i]=1-tdelta[i];
end;
run KmCal(tsur,census,s);

/* 计算每个受者的总成本，简单加权估计器需要此项 */
run CalCost(cid,start,stop, cost, id, tsur, tcost);

/* 使用加权估计器计算平均值 */
mean sw=CalourMean(tdelta, kc, cost);
print , "Weighted estimator for mean cost = mean_sw"

/* 计算简单加权估计器的标准误 */
var sw=CalourVar(tsur, tdelta, s, kc, mean_sw);
se sw=sqrt(var);
print , "Standard error for the simple weighted estimator = se_sw"

/* 计算平均生存时间及其标准误 */
dsurv=j(n,1,0);
do i = 1 to n;
dsurv[i] = 365.25/r * (1.0-exp(-r*tsur[i]/365.25));
end;
mean T=CalourMean(tdelta, kc, cost);
var T=CalourVar(tsur, tdelta, s,,, mean_sw);
se T=sqrt(var);
print , "Mean survival time = T"
print , "Standard error for mean survival time =_T"

/* 每个删失时间的累积成本，改进估计器需要此项 */
run CalCost(cid,start, stop, id, id, tdelta);

/* 计算平均成本的改进估计器及其标准误 */
CalMeanAdd(tsur, tdelta, kc, s, tcost,
meanimp = meanimp;
impimp =varsubub
, "imp estimator for mean cost = mean_imp;
print, "Standard of of estimator = imp;

/* 计算平均生存时间与简单加权估计器之间的协方差 */
cov_sw = CalCov(tdelta, tsur, s,,,, mean_ T;
print, "Covariance between mean time and simple weighted estimator = cov_sw;

/* 计算平均生存时间与改进估计器之间的协方差 */
cov_imp=CalCovSub(td,, t,, s,,,,,,,,,,,,imp;
print, "Covariance between mean time and improved estimator = cov_imp;

/* 截断生存时间到 L 的子程序 */
start TrSunv(delta, tsur, tdelta) global
(L,n);
tsurv=delta;
tdelta=delta;
do i = 1 to n;
  if (tsurv[i]>L then
    tsurv[i]=L;
    tdelta[i]=1;
  end;
finish TrSunv;
```

```
/* 计算删失百分比的子程序 */
start CalCensor(tdelta) global (L,n);
cens=sum(cens)/n;
finish CalCensor;
```

```
/* 计算 K(t)=Pr(C>t) 的 Kaplan Meier 估计器的子程序 */
start KmSur(surv, delta,kc);
create InputDataSet{var delta};
append;
close InputDataSet;
```

```
use Out;
read all (tsur tpdelta);
run ChangeKmv(tsurv, tpdelta, survival, kc);
close Out;
finish KmCal;
```

```
/* 向前传递生存函数估计值的子程序 */
start ChangeKmv(tsurv, tdelta, survival, kc) global
(L,n)
minkc=1000;
nrow=n(tsurv);
kc=j(n,1,0);

do j=1 to nn;
if (survival[j]>0 & survival[j]<minkc) then do
minkc=survival[j];
maxtime=tpsur[j];
end;

do i=1 to n;
if (sur[i]>maxtime) then kc[i]=minkc;
elelse do
 j=1 to nn;
if (sur[i]=tpsur[j]) then kc[i]=survival[j];
end;
end;
finish ChangeKmv;
```

```
/* 计算总成本的子程序 */
/* 与计算累积成本的程序相比，此子程序运行时间更短 */
start CalCost(cid, start, stop, cost, id, tsurv, tcost) global (n, nobs);
tcost=j(n,1,0);
do i=1 to n;
do k=1 to nn;
if (cid[k]=id[i] & start[k]<= tsurv[i]) then do
if (stop[k]>tsurv[i]) then
tcost[i]=tcost[i]+cost[k]*(tsurv[i]-start[k]+1.0)/(stop[k]-start[k]+1.0);
else tcost[i]=tcost[i]+cost[k];
end;
end;
finish CalCost;
```

```
/* 计算平均成本的简单加权估计器的子程序 */
start CalMean(tdelta, kc, tcost) global (n);
mymean=0;
do i=1 to n;
if (tdelta[i]=1) then mymean = mymean + tcost[i]/kc[i];
end;
mymean=mymean/n;
return(mymean);
finish CalMean;
```

## 374 使用 SAS 对观察性医疗数据的分析
