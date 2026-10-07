

# SAS 中的过度离散模型

$O_s = \sum_{j=1}^{n_s} I\left(\frac{t_j}{m_j} \in A_s\right) \quad (5.5)$

and

$E_s = \sum_{j=1}^{n_s} \text{Pr}(T_j = t) I\left(\frac{t}{m_j} \in A_s\right), \quad (5.6)$

其中 $I(.)$ 表示指示函数，$\text{Pr}(T=t)$ 通过 $\pi$ 和 $\rho$ 的最大似然估计值得出。注意 $\sum_{s=1} O_s = \sum_{s=1} E_s = n$。如果所有簇的大小都相同，可以证明频率派的表达式 (5.6) 简化为：

$E = m \text{Pr}\left(\frac{T}{m} \in A_s\right)$，且卡方统计量将变为普通的 Pearson 拟合优度（GOF）统计量。

这种具有不同 'm' 的综合检验出现在 Neerchel 和 Morel (1998) 中。他们将 Beta-二项分布和随机聚类二项分布拟合到三个诱导突变损伤数据集（称为数据集 I、II 和 III）上，这些数据曾由 Haseman 和 Soares (1976) 分析过。一组雄鼠首先接受一种怀疑的突变剂处理，随后接受一个或多个未处理的雌鼠的处理。雌鼠怀孕后，一段时间后它们被处死，并检查活死植入的频率（植入是胚胎的早期阶段）。由于来自同一母体的植入或胚胎需要产生相似，因此将它们视为自然簇是合理的。表 5.2 详细介绍了数据集 III，它是基于 n=554 只 DBA/23 雌鼠与 CD-1 雄鼠的配种。该表提供了具有“d”植入频率的雌鼠数量，其中雌鼠总数 n=554。注意植入的总数（怀孕鼠中的簇大小在 1 到 18 之间变化）。死亡植入的数量在零到九之间变化。正如 Neerchel 和 Morel (1998) 所报告的，结果表明 Beta-二项和随机聚类二项模型均拟合了数据集 I。另一方面，随机聚类二项分布勉强拟合数据集 II，并充分拟合数据集 III。Beta-二项模型未拟合数据集 II 或 III。

More, Jorge, and Nagaraj Neerchel. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 5 章 过离散二项模型的拟合优度检验

## 表 5.2: 诱导突变数据，Haseman 和 Hogan (1976) 中的数据集 III

| m | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 7 | | | | | | | | | |
| 2 | 7 | | | | | | | | | |
| 3 | 6 | | | | | | | | | |
| 4 | 5 | | 2 | 1 | | | | | | | |
| 5 | 8 | | 2 | | 1 | 1 | | | | | |
| 6 | 8 | | | | | | | | | | |
| 7 | 7 | | 4 | 2 | | | | | | | |
| 8 | 7 | | 7 | 1 | | | | | | | |
| 9 | 8 | | 9 | 7 | 1 | | | | | | |
| 10 | 22 | | 17 | 2 | | 1 | | 1 | | | |
| 11 | 30 | | 18 | 9 | | 1 | | 2 | | | |
| 12 | 54 | | 27 | 12 | | 1 | 1 | | | | |
| 13 | 46 | | 30 | 8 | 4 | 1 | | 1 | | | |
| 14 | 43 | | 21 | 13 | 3 | | | | 1 | | |
| 15 | 22 | | 22 | 5 | 2 | 1 | | | | | | |
| 16 | 6 | | | 6 | 3 | 1 | | | | | | | |
| 18 | 3 | | 3 | 2 | | | | | | | | |

我们首先拟合表 5.2 以获得 $\pi$ 和 $\rho$ 的 MLE。然后，我们计算 (5,4)、(5,5) 和 (5,6) 中描述的综合 GOF 检验。为此，我们使用了由 Pfizer 公司的 Santosh C. Sudradhar 博士提供的 "GOF_GB" 和 "GOF_RCB" 模块。

这些模块分别可以在附录 5.1 和 5.2 中找到。这些模块中的迭代过程基于 Fisher 信息矩阵而不是 Hessian 矩阵（如我们在使用 NLMIXED 的情况 4 中所示）。两种过程在渐近上是等价的。程序 5.3 提供了表 5.2 突变数据所需的统计量。在调用 "GOF_GB" 和 "GOF_RCB" 之前，应根据观测频率期望频率 (5.6) 输出残差到 "Resid_GB" 和 "Resid_RCB" 数据中，并构建残差的 QQ 图。表 5.3 提供了 Beta-二项和随机聚类模型的结果。

## 程序5.3: 诱导突变数据的 MLE 分析和 GOF

```sas
* GOF Test for DataSet III on Neerchel and Morel (1998)
Source: Haseman and Soares (1976)
This program uses "GOF_GB" and "GOF_RCB" Macros
```

```sas
data haseman_soares;
input m t1-t10;
array tt t1-t10;
do over tt;
  1;
freq = tt;
  output;
end;
```

Morel, Jorge, and Nagaraj. Overdispersion models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 服务，请访问 support.sas.com/publishing.

| m | freq |
|---|---|
| 1 | 7 |
| 2 | 7 |
| 3 | 6 |
| 4 | 5 |
| 5 | 5 |
| 6 | 8 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | 22 |
| 11 | 30 |
| 12 | 54 |
| 13 | 46 |
| 14 | 43 |
| 15 | 22 |
| 16 | 6 |
| 18 | 3 |

```sas
data haseman_soares;
  set haseman_soares;
  if freq < 5 then delete;
  do i=1 to
    output;
  end;
  drop freq;
run;
ods html;
ods graphics;
%GOF_BB(inds=haseman_soares,t=t,m,title2=DataSet III -- Haseman and Soares (1976));
%GOF_RCB(inds=haseman_soares,t=t,m,title2=Dataset III -- Haseman and Soares (1976));
* Construct QQ Plots
data Resid_BB_RCB;
  set Resid_BB Resid_RCB;
run;
proc sort data=Resid_BB_RCB;
  by Distribution;
run;
proc rank data=Resid_BB_RCB out=new_qqplots normal= ties=mean;
  by Distribution;
  var Resid;
  ranks Nquant;
run;
proc sg data=new_qqplots autlegend;
  panel Distribution;
  title "Dataset III -- Haseman and Soares (1976)";
  title2 "QQ-Plots of Residuals based on Observed and Expected Frequencies";
  x=Resid y=Nquant;
run;
ods graphics off; ods close;
```

最初，单位区间被分为 R 个互斥区间。对于 s 个区间 $A_s, s=1,2,...,R$，计算所有的 $\frac{t_j}{m_j}$，落在区间 $A_s$ 中的数量即为 $A_s$ 的观测频率。即：

$O_s = \sum_{j=1}^{554} I\left(\frac{t_j}{m_j} \in A_s\right)$

期望频率计算更为密集，且取决于 $t_j$ 的变异性。例如，使用 Beta-二项分布，$A_s$ 的期望频率计算为：

$E_s = \sum_{j=1}^{554} \sum_{t=0}^{m_j} Pr[T_j=t|T_j \sim \text{Beta-binomial}(\hat{\pi}, \hat{\rho}; m_j)] I\left(\frac{t}{m_j} \in A_s\right)$

其中 $\hat{\pi}$ 和 $\hat{\rho}$ 是表 5.3 给出的 $\pi$ 和 $\rho$ 的 MLE。随机聚类二项模型进行了类似的计算。我们从 $R=\max(m_j,j=1,2,...,554)=18$ 个区间开始。我们使用通常的经验法则确保每个区间的期望频率至少为 5。不符合此规则的区间将与上一个合并。使用模块 "GOF_BB" 的结果显示在输出 5.3 中。

## 表 5.3: 诱导突变数据最大似然结果

| | | Beta-binomial | Random-clumped Binomial |
|---|---|---|---|---|
| Parameter | Estimate | Standard Error | Estimate | Standard Error |
| $\pi$ | 0.0739 | 0.0045 | 0.0760 | 0.0046 |
| $\rho$ | 0.2741 | 0.0207 | 0.3235 | 0.0253 |
| -2 Log Likelihood | 1402.66 | | 1378.75 | |

## 输出 5.3: 诱导突变数据的 Beta-二项模型最大似然 GOF 结果

| Goodness-of-fit test under Betaomial distribution DataSet III -- Haseman and Soares (1976) |
|---|---|
| Fit Statistics |
| -2 Log Likelihood | 1402.66 |
| AIC (smaller is better) | 1406.66 |
| AICC (smaller is better) | 1406.68 |
| BIC (smaller is better) | 1415.30 |
| Maximum Likelihood Estimates |
| Estimate | Std-Error | t-Value | DF | p-Value |
| Parameter Pi | 0.07385 | 0.00443 | 16.6704 | 552 | 0.0001 |
| Parameter Rho | 0.27412 | 0.02086 | 13.1409 | 552 | 0.0001 |
| Goodness-of-fit Test under Beta-binomial Distribution |
| Lower | Upper | Observed Frequency | Expected Frequency |
| 0.0000 | 0.0526 | 286 | 298.8466 |
| 0.0526 | 0.1053 | 141 | 113.9468 |

