
研究人群被分为 k 个子样本。

针对交叉验证自适应特征设计开发了相应的宏（macros），并包含在补充材料的 `cvad.sas` 中。使用这些宏需要指定三个数据集。

- 1. `OutcomeInput`，包含治疗及治疗结果受试者信息的数据集。该数据集的格式应遵循“OutcomeInput 数据集示例”。

表 11.6 OutcomeInput 数据集示例

| subjid | treatment | response |
| :--- | :--- | :--- |
| 1 | 0 | 1 |
| 2 | 0 | 1 |
| 3 | 1 | 1 |
| 4 | 1 | 1 |

- 2. `GeneInput`，一个包含用于开发潜在生物标志物的受试者基因信息的数据集。然后根据生物标志物值将受试者分类为敏感受试者或非敏感受试者。该数据集的格式应遵循下方“GeneInput 数据集示例”中的示例。

表 11.7 GeneInput 数据集示例

| subjid | gene1 | gene2 | gene3 | gene4 | gene5 | gene6 | gene7 | gene8 |
| 1 | 0.359 | 0.490 | 1.085 | 0.174 | -1.471 | -0.207 | -0.375 | -0.5 |
| 2 | 1.371 | 1.570 | 1.541 | -0.141 | 0.121 | 0.555 | 0.094 | -0.0 |
| 3 | 0.809 | 0.362 | 1.279 | -0.134 | -0.678 | -0.216 | 0.183 | -0.3 |
| 4 | 1.960 | 0.531 | 0.508 | -0.529 | -0.191 | 0.293 | 0.153 | 0.11 |

- 3. `TPInput`，一个包含设计中使用的特定调优参数候选的数据集。该数据集的格式应遵循“TPInput 数据集示例”中的示例。

表 11.9 示例

表 11.0 示例 1：输入数据集
| eta | OS_R | gene_G |
| :--- | :--- | :--- |
| 0.2 | 0.8 | 1 |
| 0.25 | 1.5 | 1 |

`@decision` 宏在指定的显著性水平 $\alpha_1$（$\alpha_1$ 通常略低于总体 $\alpha$）下测试靶治疗相对于总体人群的获益。它决定了是否有必要进入设计中的特征部分（示例代码 11.6 决策宏调用）。

## 示例代码 11.6 决策宏调用

```sas
libname perm "directory of sample data";
%macro Decision(outcome, gene, par, alpha, seed);
%global seed;
%let sseed = &seed;

data outcome;
set &outcome;
run;

data gene;
set &gene;
run;

data par;
set &par;
run;

proc freq data=outcome;
table response*treatment/chisq;
out out=chisqtest quisq;
run;

data null;
set chisqtest("chis_value",P_PCHI);
run;
/*如果卡方检验根据预设*
/*alpha 结果显著，则打印结果并终止*/
/*否则，需要进入 CVSD 阶段*/
%if &chisq_value <&alpha %then %do
ntitle "Chi-square Test SIGNIFICANT"
proc print data=chisqtest;
run;
%abort;
%end
%mend Decision;

%Decision(perm.adsl, perm.adgene, perm.par, 0.04,12345);
```

输出（未显示）的卡方 p 值为 0.7877。由于测试在指定的 $\alpha$ 水平下不显著，将实施设计中的特征部分，以选择一个可能具有前景的生物标志物亚组，也称为敏感子集。

替换宏（见补充材料）计算了被最终特征分类为敏感的未来受试者中治疗效应的回复估计量。为了节省计算时间，通过对第一个 CV 子集进行 k 折交叉验证来选择调优参数集。

一个用于交叉验证自适应特征设计的、通过开发的宏以识别敏感受试者预测效应的回复估计量的实现示例，见 [示例代码 11.7 回归估计量]。

## 示例代码 11.7 回归估计量

```sas
libname perm "directory of sample data";
%Decision(perm.ads, perm.agene, perm.par, 0.04,12345);
%Resstitution(10,5);
```

结果显示，测试整个研究人群的治疗反应差异的卡方 p 值为 0.7877（与示例代码 11.6 的输出相似）。对于回复估计量，从 `perm.par` 预先指定的调优参数列表中选择了调优参数 `eta=0.2`、`os_rt=0.8` 和 `gene_G=1`。最后，124 名患者中有 113 名被分类为敏感型，对照组和实验组的反应率分别为 53% 和 47%。

CV 宏（见补充材料）计算了被最终特征分类为敏感的未来受试者中治疗效应的 CV 估计量。最佳调优参数集从整个研究人群中选择。

一个用于交叉验证自适应特征设计的、通过开发的宏以识别敏感受试者预测治疗效应回复估计量的实现示例，见 [示例代码 11.8 CV 估计量]。

## 示例代码 11.8 CV 估计量

```sas
libname perm "directory of sample data";
%Decision(perm.adsl, perm.adgene, perm.par, 0.04, 12345);
%CVest(10, 5);
```

结果显示，测试整个研究人群治疗反应的卡方 p 值为 0.7877（与示例代码 11.6 决策宏调用的输出相似）。对于 CV 估计量，从 `perm.par` 预选调优参数列表中选择了调优参数 `eta=0.25`、`os_R=1.5` 和 `gene_c=1`。最后，124 名患者中有 41 名被分类为敏感型，对照组和实验组的反应率分别为 33% 和 67%。

交叉验证方法可以显著增强自适应设计的性能，用于开发特征，特别是在样本量或信噪比有限的情况下 [29]。Molinar 等人 [37] 证明，交叉验证可以在省略部分病例的情况下提供类似的样本的有效性。Freidlin 等人 [6] 认为，这并不意味着分类是不稳定的。在基因组分析中，良好的特征通常不是唯一的。然而，它们通常是相关的。

## 11.4.2.4 自适应无缝/III 设计

无缝设计将传统上独立试验中的目标合并到一个试验中。这种类型的设计消除了试验之间的时间，并可能在总患者数方面提供额外的效率。自适应无缝设计是使用自适应前后数据进行分析的组合。

