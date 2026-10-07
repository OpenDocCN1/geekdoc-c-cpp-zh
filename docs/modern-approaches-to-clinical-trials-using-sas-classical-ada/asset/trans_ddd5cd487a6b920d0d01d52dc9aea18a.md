

- 51. Hu F, Rosenberger WF & Zhang LX. (2006). Asymptotically best response-adaptive randomization procedures. Journal of Statistical Planning and Inference 136: 1911-1922.
- 52. Gu X & Lee JJ. (2010). A simulation study for comparing testing statistics in response-adaptive randomization. BMC Medical Research Methodology 10: 48.
- 53. Sverdlov O & Rosenberger WF. (2013). On recent advances in optimal allocation designs in clinical trials. Journal of Statistical Theory and Practice 7: 753-773.
- 54. Zhu H & Hu F. (2009). Implementing optimal allocation for sequential continuous responses with multiple treatments. Journal of Statistical Planning and Inference 139: 2420-2430.
- 55. Gwise T, Zhou J & Hu F. (2011). An optimal response biased design with k heteroscedastic treatments. Journal of Statistical Planning and Inference 141: 235-242.
- 56. Wong WK & Zhu W. (2008). Optimal treatment allocation rules under a variance heterogeneity model. Statistics in Medicine 27: 2850-2864.
- 57. Hu F, Zhang LX, Cheung SH & Chan WS. (2008). Doubly biased coin designs with delayed responses. The Canadian Journal of Statistics 36: 541-559.
- 58. Zhang LX, Chan WS, Cheung SH & Hu F. (2007). A generalized drop-the-loser rule for clinical trials with delayed responses. Statistica Sinica 17: 387-409.
- 59. Zhang L & Rosenberger WF. (2007). Response-adaptive randomization for survival trials: the parametric approach. Applied Statistics 56: 153-165.
- 60. Li X & Wang X. (2013). Response-adaptive designs with misclassified responses. Communications in Statistics—Theory and Methods 42: 2071-2083.
- 61. Karrison T, Huo D & Chappell R. (2003). Group sequential, response-adaptive designs for clinical trials. Clinical Trials 24: 506-522.
- 62. Chappell R & Karisson T. (2007). Letter to the editor. Statistics in Medicine 26: 3046-3052.
- 63. Simon R & Simon N. (2011). Using randomization tests to preserve type I error with adaptive randomization. Statistics and Probability Letters 81: 767-772.
- 64. Hu F & Rosenberger WF. (2000). Analysis of time trends in adaptive designs with application to neurophysiology. Statistics in Medicine 19: 2067-2075.
- 65. Rosenberger WF & Sverdlov O. (2008). Handling covariates in the design of clinical trials. Statistical Science 23: 404-419.
- 66. Connor EM, Sperling RS, Gelber R, Kiselev P, Scott G, O'Sullivan MJ, VanDyke R, Bey M, Shearer W, Jacobson RL, Jimenez E, O'Neill E, Bazin B, Culmane M, Coombs R, Elkins M, Moye J, Stratton P (1994). Reduction of maternal-infant transmission of human immunodeficiency virus type 1 with zidovudine. The New England Journal of Medicine 331: 1173-1180.
- 67. Yuan Y & Yin G. (2011). On the usefulness of outcome-adaptive randomization. Journal of Clinical Oncology 29: e390-e402.
- 68. Zhu H & Hu F. (2010). Sequential monitoring of randomized clinical trials. The Annals of Statistics 38: 2218-2241.
- 69. Zhu H & Hu F. (2012). Interim analysis of clinical trials based on urn models. Canadian Journal of Statistics 40: 550-568.
- 70. Lai TL & Liao O. (2012). Efficient adaptive randomization and stopping rules in multiarm clinical trials. Sequential Analysis 31: 441-457.
- 71. Chambaz A & van der Laan MJ. (2014). Inference in group-sequential covariate-adjusted clinical trials. Scandinavian Journal of Statistics 41: 104-140.

## 作者

Oleksandr Sverdlov，生物统计学副总，EMD Serono, Inc.（默克 KgaA 子公司），美国马萨诸州 Rockland。

Zorayr Manukyan，生物统计总监，生物治疗研究部门，Pfizer Inc.,美国马萨诸州 Cambridge。

Gaurav Sharma，统计师，EMMES Corporation，美国马里兰州 Rockville。

## 第 11 章：人群富集设计

### 11.1 引言
### 11.2 经典设计
### 11.3 经典富集设计的效率
### 11.4 适应性富集设计
### 11.5 总结

## 参考文献

## 作者

## 11.1 引言

### 11.1.1 背景

实验性疗法的传统临床开发利用的是“一刀切”的方法，在未选择或未针对的患者人群中测试治疗方案。这种方法假设疾病人群的反应是同质的。随着分子靶向疗法的出现，基因测序和 mRNA 转录谱分析使得疾病的精细化分类成为可能，从而为特定患者群体开发精准诊断、预后和治疗范式，即个性化医疗。因此，这些靶向疗法可能仅对人群的部分受益，而对其他部分没有益甚至产生伤害。另一方面，蛋白质组和基因组生物标志物具有为医疗实践提供巨大价值的潜力。例如，在肿瘤学中，某些生物标志物提供了将有效性准确预测与特定机制治疗相结合，利用肿瘤的遗传组成和每个患者的基因型指导癌症治疗的选择（美国针对分子靶点批准的某些肿瘤药物）。

由于这些新机遇和挑战，不考虑反应异质性的传统药物开发范式可能是次优的。为了开启个性化医疗的任务，超越固定设计的创新统计设计变得越来越具有吸引力，这些设计允许评估由于表型或基因组异质性的治疗效应。

2012 年，FDA 发布了一份关于支持人类药物和生物制品批准的临床试验富集策略草案。在指南中，“富集”一词被定义为“前瞻性使用任何患者特征来选择研究人群，在该人群中检测药物效应（如果确实存在）的可能性比在未选择的人群中更高”。此外，富集策略分为三大类（节选自指南）：

- 减少异质性的策略：包括选择基线测量在窄范围内的患者（减少患者间异质性），并排除疾病自发好转或测量变异大的患者（减少患者内异质性）。这些策略提供的变异性减少增加了统计功效。
- 预后性富集策略：选择更有可能发生疾病相关终点（对于事件驱动的研究）或病情严重恶化的患者（对于连续终点）。这些策略将增加组别之间的绝对效应差异，但不会改变相对效应。
- 预测性富集策略：选择比其他患病患者更容易对药物治疗产生反应的患者。这种选择可以导致更大的效应量（绝对和相对），并允许使用较小的研究人群。

在本章中，我们概述了统计文献中日益增长的人群富集设计，重点关注预测性富集策略的设计，以便提高在临床试验中根据预测生物标志物检测有效疗法的功效和效率。本章的关注点在于感兴趣的疗效终点；不讨论与预测生物标志物安全性相关的设计问题。

