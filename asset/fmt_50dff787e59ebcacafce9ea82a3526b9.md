
# 高保真测序协议在 RNA 病毒中的应用

## 4.8 基于高保真测序读段的纠错工具评估

高保真测序协议的另一个应用是针对二代测序（`NGS`）读段的纠错方法评估。该协议为基因组的每个片段连接一个单独的条形码。测序后，属于原始片段的`reads`通过条形码进行聚类。只有当任何位置上最常见的碱基超过簇内`reads`数的 `90%`时，该簇的一致`read`才被认为是错误`read`。否则，整个条形码簇将被忽略。因此，在测序步骤之后，我们获得了带有测序误差的原始`reads`。在去复用步骤之后，我们获得了属于基因组片段的错误`reads`。我们建议使用某些纠错工具修正原始`reads`，并将结果与条形码纠正后获得的原始`reads`进行比较。具体而言，我们将属于某个簇的每个错误`reads`与分配到同一簇并经过修正的`reads`进行比较。

在我们的工作中，评估了 `BLESS` (39) 和 `Fiona` (40) 纠错工具。我们将它们应用于 `15M` 双端`reads`。纠错之前，我们删除了部分中的所有条形码，使`reads`的长度变为 `87bps`。纠错后，两种方法改变的`reads`均不超过所有`reads`的 `5%`。为了简单起见，我们忽略了这些`reads`。我们将每个修正后的 `87bps` `reads` 分配到其之前识别出的错误一致`read`所在的条形码簇中。我们统计了原始`reads`和纠错后`reads`与错误`reads`相同的百分比。结果显示，两种方法都导致了原始`reads`过度修正；因此，在纠错前，约 `90%` 的簇中，所有分配的原始`reads`实际上等同于对应的错误一致`read`。在经过 `BLESS` 纠错后，只有在 `78%` 的簇中所有`reads`才对应对应的`read`。`Fiona` 对正向和反向端的处理方式不同。在 `78.5%` 的簇中，所有修正`reads`的正向端与对应的错误`reads`的正向端相等。尽管在 `99.1%` 的簇中，反向端与对应的一致`read`的反向端不同。

## 致谢

作者感谢 `UCLA` 临床微阵核心实验室执行高通量测序实验。

`S.M.` 和 `E.E.` 的资金来自美国科学基金会项目 `0513612`, `0731455`, `0729049`, `0916676`, `1065276`, `1302448` 和 `1320589`，以及美国国立卫生基金会项目 `K25-HL08007`, `U01-DA02417`, `P01-HL30568`, `P01-HL28481`, `R01-GM083198`, `R01-MH101782` 和 `R01-ES022282`。`S.M.` 部分获得 `UCLA` 定量与定量生物科学研究奖学金支持。`N.C.W.` 获得 `UCLA` 分子生物学博士读前奖学金支持。`A.Z.` 部分获得美国农业部食品与农业研究倡议竞争性资助（项目号 `201167016-30331`）以及美国科学基金会奖励 `IIS-0916401`。`N.M.` 部分获得佐治亚州立大学第二世纪计划支持。

利益冲突：未声明。

## 参考文献

- 1. Lauring AS, Andino R. 准物种类型和 RNA 病毒的行为。PLoS Pathog 2010;6(7):e101005.
- 2. Tbisris AM, Korber B, Armonaut R, Russ C, Lo C-C, Leitner T, Gaschen B, Theiler J, Paresdes R, Su Z et al. 定量深测序揭示了体内 CCR5 拮抗剂导致的 HIV-1 逃逸和群体转变。PLoS ONE 2009;4(5):e5683.
- 3. Henn MR, Boutwell CL Charlebois P, Lennon NJ, Power KA, Macalalad AR, Berlin AM, Malboef CM, Ryan S et al. HIV-1 基因组深测序揭示了急性感染免疫识别期间微变异株的早期重要性。PLoS Pathog 2012;8(3):e100259.
- 4. Metzker ML. 测序技术——下一代。Nat Gen 2009;11(1):31–46.
- 5. Mangul S, Wu Mancuso N, Zelikosky A, Sun R, Eskin E. 来自超深测序数据的准确病毒种群估计。Bioinformatics 2014;30(12):i1329–i337.
- 6. Astroskaya I, Tok B, Mangul S, Westbooks C, Mandoiu I, Balfe P, Zelikosky A. 从 454 焦序测序读段中推断病毒准物种谱。BMC bioinformatics 2012;11:Suppl6.
- 7. Zagordi O, Bhattacharya A, Eriksson N, Beerwinkel N, ShoRAH: 从下一代测序数据估算混合样本的遗传多样性。BMC Bioinformatics 2012;11(1):119.
