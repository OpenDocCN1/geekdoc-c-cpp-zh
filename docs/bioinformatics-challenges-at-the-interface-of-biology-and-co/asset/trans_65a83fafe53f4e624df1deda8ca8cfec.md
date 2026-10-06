

![](img/1af42ff402ef4720886c50af0bb8e9b5_172_0.png)

**图 5.7**
GPCRs 的不同激活模式：(a) 在 7TM 骨架内结合进入的配体；(b) 在延伸的 N 端区域内捕获配体；(c) 在细胞外环中结合配体；(d) 在 TM 框架内共价价结合配体。

我们的目标不是被此类辩论的细枝节分散注意力；相反，我们想要尝试理解不同的比对输出、应用了哪些间隙罚、间隙是如何建模的、使用了哪些评分矩阵、间隙输出是什么，以及对这些输出的解释充其量也可能是误导性的。脱离这一背景，问题在于，由于比对工具太容易获得，用户会对它们的输出结果产生怀疑。事实上，几乎所有的生物信息学工具（尤其是在线工具）也是如此，因为它们被刻意设计成以尽可能痛苦的方式提供答案——理想情况下，只需点击一下（对于一种有趣的未来愿景，我们推荐阅读*生物信息学历史（2039 年）*³¹，其中 Titus Brown 将这种按按钮式的数据分析称为“易用”工具的灾难）。

¹https://www.youtube.com/watch?v=uwsjwMO-TEA

现在，在接下来的章节中，我们将更仔细地检查在理解比对结果含义时需要考虑的问题。

## 5.8.2 我的序列共享哪些属性？

理解比对含义的任务远深于不同算法产生的间隙数量和位置。正如我们在第 3 章和第 4 章所示，我们比对序列是为了能够有效地比较它们、检测共同的特征或差异、推断它们的祖先以及它们是如何演化以获得特化功能和结构修饰的。那么，图 5.5 中的序列共享哪些特征呢？

尽管这些或多是“标准”输出，但实际上要确定哪些序列具有共同点几乎是不可能的（这比图 5.5 看起来还要困难，因为我们不得不“缝合”一些比对后的区块以便让它们显示在同一行）。困难在于它们的呈现方式——大部分是白背景上的黑字。在实践中，这样的输出由手动编辑工具“消耗”，这些工具通常采用一系列可视化选项——大多数使用颜色。但随后又使用不同的颜色来描述单个氨基酸或氨基基；结果是，比较比对可能具有挑战性，正如图 5.8 所示。

从图 5.8 可以清楚地看到不同颜色方案引起的混乱程度（为了方便比较，每个方案中比对的部分是相同的）。在这里，Kite 和 Zimmermann 是更详细尺度的简化/疏水性表示（回想第 2 章）：每个尺度的一半被涂成白色（疏水性），而另一半被涂成绿色（亲水性）。CINEMA 使用图 2.8 所示的“标准”氨基酸属性组和颜色。ClusterX 是一种混合方案，颜色似乎用于表示一般的氨基酸属性组和保守性：因此，Thr 和 Ser 有时被涂成绿色，但有时 Arg 和 Lys 是红色，有时又不是；有时 Ala、Leu 和 Ile 是蓝色，有时 Asp 和 Glu 是紫色，有时又不是。

由于 CINEMA 和 ClusterX 方案分配给氨基酸组的颜色几乎是完全相反的，情况变得更加混乱：红色在其中一种方案中表示酸性基团，在另一种中表示碱性基；蓝色在一种中表示碱性基，在另一种中表示疏水性；芳香族在一种中表示某种基，在另一种中表示酸性基；黄色在一种中表示含硫氨基酸 Cys，而在另一种中则表示氧（如框 5.3 所示）。具有这种复杂性，根据特征来解释比对含义绝非易事。

为了理解不同的比对结果，用户必须首先理解颜色方案。CINEMA 中实现的“标准”方案是基于我们早期物理和化学课程中学到的颜色，以减少理解比对输出所需的认知努力：结果是，我们直觉上红色是酸性的（负电荷）；蓝色是碱性的（正电荷）；黄色是含氧的；因此，原则上我们不需要像看 ClusterX 那样费力去理解 CINEMA 比对。

| | | | |
|---|---|---|---|
| Without | Q2293 | AEYSLAVAGMAFCTT- | SASQSDSTPRQVAYLLCPFVAS |
| colour | OPSD2 | AIWLSLLLAERYVVVC- | KMNERPF-GENHAIGVMFNTACA |
| gap | ACM1 | ASVMNNLL-IDFRYSYVT- | PLYSRAKRR-TPRAALIGLWFNVA |
| # | OPRM | TIFTCLCT-MSVDYIAVC- | HPKALDFRR-TPRANIKWCNNISAAG |
| | C5AR | ASILLATAT-ISDFLRADY- | KPIQKCNGR-GAGLAWVCAGLLTI |
| | GP13 | ACFTCVTS-LSHHTMWC- | PVYNTLSKN-AKQAHVTIGWFSSELSA |
| | GP162 | ACFTCVAS-LSHHTMWC- | PVYNTLSKN-AKQALHAVGMVWFSST |
| | UL78 | STALFLFL-LIIDLEASYGDLIH-ETRENAGAGVALVSIIAV |
| | Kyte | Q2293 | AEYSLAVAGMAFCTT- | SASQSDSTPRQVAYLLCPFVAS |
| | | OPSD2 | AIWLSLLLAERYVVVC | | KMNERPF-GENHAIGVMFNTACA |
| | | ACM1 | ASVMNNLL-IDFRYSYVT- | PLYSRAKRR-TPRAALIGLWFNVA |
| | | OPRM | TIFTCLCT-MSVDYIAVC- | HPKALDFRR-TPRANIKWCNNISAAG |
| | | C5AR | ASILLATAT-ISDFLRADY- | KPIQKCNGR-GAGLAWVCAGLLTI |
| | | GP13 | ACFTCVTS-LSHHTMWC- | PVYNTLSKN-AKQAHVTIGWFSSELSA |
| | | GP162 | ACFTCVAS-LSHHTMWC- | PVYNTLSKN-AKQALHAVGMVWFSST |
| | | UL78 | STALFLFL-LIIDLEASYGDLIH-ETRENAGAGVALVSIIAV |
| | Zimmermann | Q2293 | AEYSLAVAGMAFCTT- | SASQSDSTPRQVAYLLCPFVAS |
| | | OPSD2 | AIWLSLLLAERYVVVC- | KMNERPF-GENHAIGVMFNTACA |
| | | ACM1 | ASVMNNLL-IDFRYSYVT- | PLYSRAKRR-TPRAALIGLWFNVA |
| | | OPRM | TIFTCLCT-MSVDYIAVC- | HPKALDFRR-TPRANIKWCNNISAAG |
| | | C5AR | ASILLATAT-ISDFLRADY- | KPIQKCNGR-GAGLAWVCAGLLTI |
| | | GP13 | ACFTCVTS-LSHHTMWC- | PVYNTLSKN-AKQAHVTIGWFSSELSA |
| | | GP162 | ACFTCVAS-LSHHTMWC- | PVYNTLSKN-AKQALHAVGMVWFSST |
| | | UL78 | STALFLFL-LIIDLEASYGDLIH-ETRENAGAGVALVSIIAV |
| | CINEMA | Q2293 | AEYSLAVAGMAFCTT- | SASQSDSTPRQVAYLLCPFVAS |
| | | OPSD2 | AIWLSLLLAERYVVVC- | KMNERPF-GENHAIGVMFNTACA |
| | | ACM1 | ASVMNNLL-IDFRYSYVT- | PLYSRAKRR-TPRAALIGLWFNVA |
| | | OPRM | TIFTCLCT-MSVDYIAVC- | HPKALDFRR-TPRANIKWCNNISAAG |
| | | C5AR | ASILLATAT-ISDFLRADY- | KPIQKCNGR-GAGLAWVCAGLLTI |
| | | GP13 | ACFTCVTS-LSHHTMWC- | PVYNTLSKN-AKQAHVTIGWFSSELSA |
| | | GP162 | ACFTCVAS-LSHHTMWC- | PVYNTLSKN-AKQALHAVGMVWFSST |
| | | UL78 | STALFLFL-LIIDLEASYGDLIH-ETRENAGAGVALVSIIAV |
| | ClustX | Q2293 | AEYSLAVAGMAFCTT- | SASQSDSTPRQVAYLLCPFVAS |
| | | UL78 | STALFLFL-LIIDLEASYGDLIH-ETRENAGAGVALVSIIAV |
| | | OPSD2 | AIWLSLLLAERYVVVC- | KMNERPF-GENHAIGVMFNTACA |
| | | ACM1 | ASVMNNLL-IDFRYSYVT- | PLYSRAKRR-TPRAALIGLWFNVA |
| | | OPRM | TIFTCLCT-MSVDYIAVC- | HPKALDFRR-TPRANIKWCNNISAAG |
| | | C5AR | ASILLATAT-ISDFLRADY- | KPIQKCNGR-GAGLAWVCAGLLTI |
| | | GP13 | ACFTCVTS-LSHHTMWC- | PVYNTLSKN-AKQAHVTIGWFSSELSA |
| | | GP162 | ACFTCVAS-LSHHTMWC- | PVYNTLSKN-AKQALHAVGMVWFSST |

