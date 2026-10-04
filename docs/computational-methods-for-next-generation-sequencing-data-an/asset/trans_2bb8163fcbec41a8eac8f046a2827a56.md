
## 发现与基因型鉴定暮昏地带缺失

NGS 缺失的暮昏地带。简而言之，虽然一些先进的基于片段大小的方法从“上方”处理这一暮昏地带（其中包括 7–9），但基于比对的方法（无论是常规的还是针对拆分读取（split-read）的，见参考文献 14, 18, 34）都是从“下方”处理这一暮昏地带。基于内部片段大小的方法的一个通用缺点是预测的断裂点相当不准确（参见松弛和严格精确率统计的差异）。混合方法解决了这一问题，因此兼顾了基于片段大小的方法在检测更大缺失方面的优势，以及基于比对的方法在高度准确的断裂点预测方面的优势。

## 7.7.1 HiSeq

在所有评估的方法中，只有 CLEVER (10) 及其混合版本 MATE-CLEVER 提供了跨越暮昏地带范围（30–150 bp）的完整缺失集。在基于内部片段大小的检测中，VariationHunter 对至少 50 bp 的缺失提供了良好的检测集，Breakander 对至少 70 bp 的缺失提供了检测集。然而，召回率是以牺牲断裂点准确性为代价的，这在两种情况下都可以显著提高。在这种情况下，CLEVER 在基于内部片段大小的方法中领先，因为它的严格精确率明显优于其他方法。

在混合方法中，只有 MATE-CLEVER 对暮昏地带做出了贡献。DELLY 专注于缺失，并对大于 200 bp 的缺失实现了非常理想的性能率（数据未显示）。

在基于拆分比对（split-alignment-based）的方法中，PINDEL 在综合评估方面表现最好，对 50 bp 以内的检测实现了卓越的性能率，并在 50 bp 之外发现了不可忽视的缺失。GSNAP 和 Stampy 提供了大量的优秀预测，然而，这两种工具对于 40–50 bp 及更长缺失的召回率仍需改进。

## 7.7.11 30–50 bp 杂合缺失

处理 HiSeq 数据时一直存在的一个挑战是长度为 30–50 bp 的杂合缺失。在这种情况下，CLEVER 的召回率最高（61%）。尽管如此，基于 HiSeq 的此类检测尚未开发出新的解决方案。杂合性与尺寸范围的结合似乎（部分）仍然是所有类发现方法的弱点，在仅使用 HiSeq 实验时无法（完全）克服。

总结来说，可以为 30 bp 以内的缺失推荐 GSNAP-(UG/HC)，为所有大于 30 bp 的缺失推荐 MATE-CLEVER，基于 GSNAP 的基因型鉴定流水线在 30–50 bp 的纯合缺失方面也达到了具有竞争力的性能率。由于通常对杂合和纯合缺失的相对比例信息很少，MATE-CLEVER 是大于 30 bp 缺失的优越整体选择，它是支持 30+ 缺失的唯一工具，其整体基因型精确率超过 90%。

## 7.7.2 MiSeq

MiSeq 是一种最近测序技术，允许长度为 250 bp 及更长的读取。因此，它在基于拆分比对的方法检测更长缺失方面具有巨大潜力。事实上，MiSeq 实验不受 30–50 bp 杂合缺失“盲点”的影响，而这仍然适用于 HiSeq 实验。部分 BWA-MEM (18) 和部分 GSNAP (30) 都受益于测序技术的进步，在可靠的精确率实现了超过 80% 的召回率（BWA-MEM 为 85.7%，BWA-MEM：86.2/279.1% 松弛/严格精确率）。如果 MiSeq 技术可用且吞吐量满足当前应用，显然这些是首选方法。

对于 50bp 及以上的缺失，CLEVER 和 MATE-CLEVER 再次是首选方法，在范围内实现了最高性能率，而 VariationHunter 的检测非常不准确（Variation 严格精确率 <10%）。

使用 MiSeq 数据会导致基于片段的方法以及混合方法的损失，这很可能是由于片段长度的增加。对于基于拆分比对的方法，这通常会导致召回率的大幅增加。

总结，在考虑 30–50 bp 长度的杂合缺失时，使用 MiSeq 数据具有明显优势。在所有其他类型的检测中，当与拆分比对方法结合时，它会导致更“激进”的暮昏地带检测，而基于 HiSeq 数据的检测往往包含更少的假阳性。

## 7.7.2.1 基因型鉴定

在基因型鉴定方法中，MiSeq 通常会导致召回率，但提高了 MATE-CLEVER 的精确率。解释是 MATE-CLEVER 是一种混合方法。虽然 MATE-CLEVER 通常具有最佳的基因型精确率，但对于大于 30 bp 的缺失，基于 HC 的工具会导致更“激进”的基因型，其精确率较低，并且对于 30-50 bp 的缺失，“可鉴定型”检测明显增加。

总结来说，在 MiSeq 数据上，MATE-CLEVER 是唯一在所有范围内可靠鉴定暮昏地带缺失的方法。对于暮昏地带较低范围的缺失，基于比对的方法结合 UG 或或 HC 有助于生成“更高敏感性”的检测集。

## 7.7.3 结论

### 7.7.3.1 HiSeq

对于 HiSeq 数据，可以将 PINDEL 作为检测 10-30 bp 缺失的最强方法。对于中间范围的检测，推荐结合 PINDEL、CLEVER 和/或 MATE-CLEVER，它们应该共同为纯合缺失产生完整的检测集，但为杂合缺失留下了改进空间。从 50 bp 开始，当关注单一工具时，MATE-/CLEVER 是首选方法。

对于基因型鉴定，可以推荐使用基于比对的方法（如 BWA-MEM 或 GSNAP）结合 UG 和或 HC 来检测 10–30 bp（以及更短的，未显示），而 MATE-CLEVER 是大于 30 bp 缺失的首选方法。

顺带一提，这些见解导致了荷兰基因组计划（Genome of the Netherlands Project (1)）中这些工具的选择，它提供了该尺寸范围内缺失检测集，比其他项目（如 1000 基因组计划 (2)）全面得多。

### 7.7.3 MiSeq

对于 MiSeq 数据的通用建议是，当与拆分比对方法结合时，使用更“激进”的暮昏地带检测。对于基因型鉴定，再次 BWA-MEM 和/或 GSNAP（经 UG 和或 HC 后处理）是大于 30 bp 缺失的首选方法，而 MATE-CLEVER 是 30+ bp 缺失的首选方法。对于 10–50 bp 的缺失，将 GSNAP 与 MATE-CLEVER 结合可以做出价值贡献。

## 7.8 可用性

访问 http://homepages.cern.ch/twilightzone/

## 7.9 致谢

A. Schonuth 感谢荷兰科学组织（NWO）的资助 639。

## 7.10 参考文献

- 1. The Genome of the Netherlands Consortium. 人口结构和人口历史。Nature 2009;460:623–635.
- 2. The 1000 Genomes Project. 人类变异图。Science 2009;326(5955):773–778.
- 3. The International Cancer Genome Project. 从头测序数据。Nature 2010;467(7291):993–998.
- 4. The Cancer Genome Project. 人口规模测序。Bioinformatics 2011;27(12):1297–1303.
- 5. The Cancer Genome Project. 人口变异。Nature Rev. Genet 2012;13(5):363–376.
- 6. The Cancer Genome Project. 从测序数据中识别变异。Nat Methods 2009;6(7):473–474.
- 7. The Cancer Genome Project. 基于人口的发现。Nat Methods 2009;9(6):677–681.
- 8. The Cancer Genome Project. 从双端测序检测结构变异。Genome Res 2009;19(11):1270–1278.
- 9. The Cancer Genome Project. 从头组装方法。Bioinformatics 2009;25(14):1754–1760.
- 10. The Cancer Genome Project. 变异发现与基因型鉴定。Bioinformatics 2013;28(13):2828–2839.
- 11. The Cancer Genome Project. 结构变异分类。Bioinformatics 2009;25(12):i222–i230.
- 12. The Cancer Genome Project. 识别基因变异的整合模型。Genome Biol 2012;13(2):R23.
- 13. The Cancer Genome Project. 检测缺失和中等尺寸插入。Bioinformatics 2009;25(21):2865–2871.
- 14. The Cancer Genome Project. 使用 Burrows-Wheeler 变换映射短 DNA 读取。Bioinformatics 2009;25(14):1754–1760.
- 15. The Cancer Genome Project. 使用质量评分映射测序读取并检测变异。Genome Res 2008;18(11):1851–1858.
- 16. The Cancer Genome Project. 组装人类基因组序列。PLoS Biol 2007;5(e120).
- 17. The Cancer Genome Project. 对从头短读取组装方法的竞争评估。Genome Res 2011;21:2224–2224.
- 18. The Cancer Genome Project. 使用 Burrows-Wheeler 变换映射短 DNA 读取并检测变异。Bioinformatics 2009;25(14):1754–1760.
- 19. The Cancer Genome Project. 使用质量评分映射测序读取并检测变异。Genome Res 2008;18(11):1851–1858.
- 20. The Cancer Genome Project. 一种基于模拟误差从双端测序数据识别基因变异的计算框架。Genome Biol 2009;10(2):R23.
- 21. The Cancer Genome Project. 小鼠基因组中结构断裂点的映射和分析。Genome Res 2010;20(5):623–635.
