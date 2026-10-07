

通过根据患者的标志物状态，将更多患者分配给更有效的治疗方案，使患者在试验中获益。大多数频率派设计也能实现前两个目标。

BAR 富集设计（BAR enrichment design）可以自然地扩展到多种治疗方案和多种标志物。对于基线特征属于标志物组 $j$ 的患者，假设治疗 $i$ 效应大小的后验估计为 $\delta_{ij}$，则到治疗 $i$ 的随机化比例可以表示为 $\lambda_i / \sum \lambda_j$ ，其中 $\lambda$ 是调节参数。注意，当 $\lambda=0$ 时，对应于等随机化。当它变成“胜者为”（play-the-winner）设计时，根据可用数据将下一个患者分配给当前的获胜治疗，且不涉及随机化。$\lambda$ 越大，随机化的不平衡程度就越严重。

BAR 富集设计已经在几项著名的肿瘤学临床试验中成功实施。一个例子是肺癌消除标志物整合靶向治疗方法（BATTLE）试验 [56]。BATTLE 项目由一个伞型试验和四个并行的 II 期研究组成，这些研究针对此前接受过化疗但随后失败的基于标志物的靶向治疗法。该研究的主要目标是根据患者的标志物谱，估计并测试每种治疗方案在 8 周的疾病控制率。使用贝叶斯Probit 模型（Bayesian probit model）通过自适应随机化来描述每个标志物亚组每种治疗的疾病控制率。另一个著名的例子是针对局部晚期乳腺癌女性的新辅助治疗设置的 I-SPY 2（通过影像和分子分析预测治疗反应的系列研究）II 期试验。其新辅助设计旨在在一个特殊的人群中测试联合标准化疗的调查性药物。通过采用创新的 BAR 设计，该研究旨在用一半的时间、更低的成本和显著更少的参与者来测试新治疗法 [58]。显示贝叶斯预测概率优于标准疗法的方案将带着其相应的标志物特征通过试验。如果方案在任何标志物特征下显示出疗效改善概率较低，则会被剔除。当通过测试的药物毕业或被淘汰时，新药物将进入。

BAR 设计的一个明显局限性是，自适应随机化需要快速反馈，以便从中期数据中学习并调整随机化速率。因此，BAR 设计仅适用于终点可以在较短时间内评估的试验。

Korn 和 Freidlin [59] 在随机双臂设置中，比较了结果自适应随机化设计与固定的 1:1 或 2:1 随机化设计。比较是基于所需的样本量、疗效较差的患者人数和比例进行的。作者发现，结果自适应随机化相对于 1:1 或 2:1 随机化没有优势，因此，当倾向于让更高比例的患者被随机分配到实验治疗时，建议使用固定的 2:1 随机化设计。在性评论论文中，Berry [60] 认为，自适应随机化的最大潜力在于多臂试验（如 BATTLE 和 I-SPY 2 研究），尽管在双臂试验中自适应随机化的获处是有限的。

# 11.4.3.2 针对标志物与治疗相互作用的贝叶斯/频率派设计

在生存终点且仅有 1 个标志物的情况下，Karur 和 Simon [61] 提出了一种两阶段贝叶斯设计，类似于 Freidlin 和 Simon [29] 以及 Wang 等人 [45] 的频率派设计。具体而言，它是 Wang 等人 [45] 自适应设计的贝叶斯版本，其中标志物阳性和标志物阴性分层内治疗效应的后验分布基于中期分析，该第一阶段数据用于对患者招募和试验进展做出决策。这本质上是一种混合贝叶斯/频率派设计，它利用了贝叶斯方法在整合候选预测标志物先验置信度方面的灵活性，同时控制了符合传统频率派 III 期试验标准的 I 型和 II 型错误率。在中期分析时，将后验概率与预设阈值进行比较，并采取 3 种行动之一：

- 1. 停止试验
- 2. 在中期停止招募标志物阴性组
- 3. 继续招募阴性和阳性患者。

Karurui 和 Simon 设计能够在数据表明无获益时，限制接受测试药物的阴性患者数量。还证明了该设计比 Wang 等人 [45] 的频率派版本具有许多优势。

# 11.5 总结

在个性化/精准医学的新时代，临床研究人员面临着日益增长挑战，同时也面临独特的机遇，以满足患者、支付方以及不断增加的健康经济成本的需求。在本章中，我们概述了统计文献中日益增长的人群富集设计，重点关注预测富集策略的设计，以增加临床试验中根据预测性标志物检测有效疗法的效能和效率。我们将现有设计分类为经典设计、频率派自适应设计和贝叶斯自适应设计。我们还讨论了标志物富集设计与传统全人群相比的效率、分析的敏感性/特异性，以及标志物阳性组与标志物阴性组的相对治疗效应。

我们的重点是与感兴趣的临床疗效终点和实验治疗相关的一个或多个预测标志物的设计。与安全结局相关的标志物是一个重要研究领域，但本章未涵盖。此外，预后标志物、药代计量标志物和替代标志物不在本章的范围内。

# 参考文献

- 1. Mandrekar SJ and Sargent D. (2009). 用于预测标志物验证的临床试验设计：理论考虑和实践挑战. Journal of Clinical Oncology 27: 4027-4034.
- 2. Karapetis CS, Khambata-Ford S, Jonker J, O'Callaghan CJ, Tu D, Tebbutt C, Simes RJ, Chalchal H, Shaprio JD, Robitaille S, Price TJ, Shepard L, Au HJ, Langer C, Moore MJ & Zalberg JR. (2008). 晚期结肠癌中 K-ras 突变和西妥单抗的获益. New England Journal of Medicine 359: 1757-1765.
- 3. Bokemeyer C, Makhson A, Hartmann JT, Aparicio J, de Braud F, Donea S, Ludwig H, Lim R, Schuch G, Stroch C, Loos AH, Zubel A & Koralewski P. (2009). 转移性结肠癌一线治疗中使用不含西妥单抗的氟尿嘧啶、白氨酸和奥沙利. Journal of Clinical Oncology 27: 663-671.
- 4. Van Cutset E, Köhne CH, Hitre E, Zaluski J, Chang Bien CR, Makhson A, D'Haens G, Pinter T, Lim R, Bodoky G, Folprecht G, Ruff P, Tejpar S, Schlichting M, Nicholson J & Rogue P. (2009). 西妥单抗和化疗作为转移性结肠癌的初始治疗. New England Journal of Medicine 360: 1408-1417.
- 5. Amado RG, Wolf M, Peeters M, Van Cutset E, Siena S, Freeman DJ, Juan T, Sikorski R, Suggs S, Radinsky R, Patterson SD & Chang DD. (2008). 野生型 KRAS 是转移性结肠癌患者泛舒妥单抗疗效所需的. Journal of Clinical Oncology 26: 1626-1634.
- 6. Freidlin B, McShane LM & Korn EL. (2010). 带有标志物的随机临床试验：设计问题 Journal of the National Cancer Institute 102: 152-160.
- 7. Sargent DJ, Conley BA, Allegra C & Collette L. (2005). Clinical trial

