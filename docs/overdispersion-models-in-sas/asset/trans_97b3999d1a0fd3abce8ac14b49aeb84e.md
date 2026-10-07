

# 程序 4.2：拟合度检验——染色体数据

| 标题 |
|------------------------------------------------------------|
| 此宏执行皮尔逊拟合优度检验 |
| Skellam (1948) 染色体数据示例 |
| data = 包含变量 Obs 和 Pred 的数据集 |
| df = 自由度 |
| title = 正在拟合的分布 |

```sas
%macro gof(data,df,title);
proc imml;
  use &data;
  read all(freq) into Observed;
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

# 第 4 章 用于过度离散二项响应的似然模型 93

输出 4.2：Beta 二项分布下的拟合度结果

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

表 4.3 显示了本示例中考虑的五种分布下关联数量的观测频率和期望频率。二项分布并没有很好地拟合数据，因为在 2 个自由度下，$X^2 = 8.11$，对应的 P 值为 0.017。对于零值膨胀二项分布（Zero-inflated Binomial），也可以观察到类似的现象，其在 1 个自由度下，$X^2 = 4.71$，对应的 P 值为 0.030。自由度的计算方法为（类别数减去1）减去（估计的参数个数）。在二项分布的情况下，自由度为 $(4-1)=2$。过度离散分布多额外的参数 $\rho$，这使得它们的自由度变为 $(4-1)-2=1$。二项分布、随机聚类二项分布和具有加性交互作用的广义二项分布能够较好地拟合关联数量的分布，其卡方检验的 P 值 值分别为 0.384、0.347 和 0.439。当存在多个模型且它们都符合拟合度标准，且模型之间互不嵌套时，很难选出一个单一模型作为最终建议。这种情况也发生在回归建模的情况下。因此，建议与领域专家讨论这些选项，并向他们说明每个模型的含义，同时就哪种模型更接近他们研究的现象征求他们的意见。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 表 4.3：染色体数据的皮尔逊卡方拟合度检验

| 关联数量 | 观测频率 | 二项分布 | Beta 二项分布 | 随机聚类二项分布 | 零值膨胀二项分布 | 广义二项分布 |
|---|---|---|---|---|---|---|
| 0 | 32 | 24.86 | 33.97 | 34.08 | 32.00 | 33.91 |
| 1 | 103 | 103.24 | 97.16 | 96.82 | 93.60 | 97.55 |
| 2 | 122 | 142.94 | 127.67 | 128.24 | 140.80 | 126.84 |
| 3 | 80 | 65.96 | 78.20 | 77.85 | 70.60 | 78.70 |
| $\chi^2$ | | 8.11 | 1 | 1 | | 1 |
| P 值 | | 0.017 | 0.384 | 0.347 | 0.030 | 0.439 |

## 染色体数据的皮尔逊卡方拟合度检验

正如我们之前看到的，对于聚类大小 $m$，Beta 二项分布和随机聚类分布几乎是完全相同的。请注意，当 $\rho$ 接近单位1 时，它们之间的差异会变得显著。

[注：OCR 文本包含大量的重复和乱码部分，已根据逻辑流进行了清理。]

