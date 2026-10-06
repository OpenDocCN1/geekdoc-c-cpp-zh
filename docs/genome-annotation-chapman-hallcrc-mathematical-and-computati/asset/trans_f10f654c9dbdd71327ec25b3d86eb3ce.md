
参数。下一阶段称为相似性阶段，它对未被目标阶段映射的基因组区域应用相同的比对技术，但参数设置稍不严格。这两个阶段的相对贡献取决于该物种及其近缘物种现有的公共数据量。

结构预测的第二部分是 cDNA 比对。将物种特异性 cDNA（组装）和 EST（单次通过）转录序列与基因组进行比对。如果 cDNA 比对与基于蛋白的阶段预测的基因区域重叠，则 cDNA 比对中的非重叠区域被注释为预测的 5' 或 3' UTR。由于 EST 比对的质量较低，其在注释过程中的支持证据权重低得多。

最后，通过合并来自不同比对蛋白的相同转录本，产生基因的非冗余转录模型。所有的最终转录模型都会在最终界面呈现给用户，其中部分或全部代表真实的生物转录。

## 8.5.3 功能注释

若干后处理步骤过滤并注释预测的基因。Ensembl 积累了来自第 7 章中提到的工具的证据，例如 SignalP 和相关工具 (Emanuelsson et al., 2007) 以及 InterPro (Hunter et al., 2011)。这些数据显示在产品的蛋白质摘要页中，如图 8 所示。

非编码 RNA 注释使用 Rfsam (Gardner et al., 2011)。会检查是否存在起始甲氨酸残基和末尾聚尾腺化信号（见第 2 章）。在真生物中，假基因很难区分。Ensembl 的假基因预测基于匹配以下任一：

![](img/7da802df4d7c0829a4a41adf9acaf30d_163_0.png)

图 8.9 Ensembl 功能证据摘要。（顶部）外子结构，用交替的浅紫色和深紫色显示边界。（中间）两条生化特征和六条结构域同源性证据线。（底部）已知序列变异（可用时）。**（参见彩色插图。）**

- 该转录本具有单个外子，并与地方的多外子转录本匹配。
- RepeatMasker 将该转录本识别为完全重复的。
- 该转录本具有多个移框且无内含子。
- 该转录本具有移框且所有内含子至少 80% 是重复的。

Ensembl 并不合成基因描述，而是交叉来自现有蛋白注释数据源（如 UniProt、NCBI Gene 数据库 www.ncbi.nih.gov/gene）可用信息。可以使用 Apollo (Lewis et al., 2002) 对 Ensembl 基因进行手动结构和功能关联。Ensembl 在基因组注释工具中独特，它结合了第 4 章讨论的几种基因组相关数据类型，以预测基因组调节特征。来自功能基因组学实验的经验数据：

- 染色质免疫沉淀——覆盖芯片 (ChIP-chip)、测序和 DNase 测序
- 表观基因组修饰——组蛋白、转录因子、RNAPolIII、DNA 甲基化，来自 ENCODE 项目的数据
- 调节基序
- 微RNA (miRNA) 靶

## 8.6 总结

功能注释对于理解新出现的基因组至关重要。功能注释建立在良好的结构注释的基础上。基因组注释流程用于处理这两个阶段并自动收集生物信息学证据。存在多种流程实现，以针对原核生物与真核基因组，以及简单与复杂的真核基因组。某些流程是独立的，而另一些旨在与其他组件结合使用，以编辑或查看自动注释结果。第 9 章探讨了这些注释数据显示和编辑环境的示例。

## 参考文献

Altschul, S., Madden, T., Schaffer, A., et al. 1997. Gapped BLAST and PSI-BLAST: A new generation of protein database search programs. Nucleic Acids Res. 25:3389–3402.

Bairoch, A. 2000. The ENZYME database in 2000. Nucleic Acids Res. 28(1):304–305.

Birney, E., Clamp, M., Durbin, R. 2004. GenWise and Genemose. Genome Res. 14:988–995.

Cantarel, B., Korf, I., Robb, S., et al. 2008. MAKER: An easy-to-use annotation pipeline designed for model genomes. Genome Res. 18(1):188–196.

Carver, T., Berkiman, M., Tvey, A., et al. 2008. Artemis and Cluster: annotating and comparing sequences in a relational database. Bioinformatics 24:2672–2676.

Delcher, A., Blatche, K., Powers, E.C., Salzberg, S. 2007. Identifying bacterial genes and endosymbiosis with Glimmer. Bioinformatics 23(6):673–679.

Emanuelsson, O., Brunak, S., von Heje, G., Nielsen, H. 2007. Locating proteins in the cell UsingTarget, SignalP and related tools. Nat. Prot. 2:953–971.

Flick, P., Aken, B., Ballester, B., et al. 2010. Ensembl’s 10th: Nucleic Acids Res. 38(Database issue):D557–D562.

Gaasterland, T., Sensen, C. 1996. MAPPIE: Automated genome interpretation. Trends Gen. 12(2):6–78.

Gardner, P., Bauer, J., Tate, J., et al. 2011. Rfam: Wikipedia, and the “decimal release.” Nucleic Acids Res 39(Database issue):D141–D145.

Hunter, S., Jones, P., Mitchell, A., et al. 2011. InterPro in 2011: New developments in the family and domain database. Nucleic Acids Res. 40:D306–D312.

Iseli, C., Jongeneel, C.V., Bucher, P. 1999. ESTScan: A program for detecting, evaluating, reconstructing potential coding regions in EST sequences. Proc. Int. Conf. Syst. Mol. Biol. 138–148.

Kaneishi, M., Goto, S., Sato, Y., Furumichi, M., Tanabe, M. 2012. KEGG for integration and interpretation of large-scale molecule data sets. Nucleic Acids Res. 40(Database issue):D109–D114.

Kent, W.J., Baertsch, R., Hinrichs, A., Weiss, Haussler, D. 2003. Evolution’s caululdron: duplication, deletion, and rearrangement in the mouse and human genomes. Proc. Nat. Acad. Sci. USA 100:11484–11489.

Korf, I. 2004. Finding gene in novel clusters. BMC Bioinformatics 5:59.

Kumar, K., Desai, V., Cheng, L., et al. 2011. AGES: A software system for microbial genome annotation. Plus One 6(3):e17469.

Lagensen, K., Hallin, P., Rodland, E., Staerfeldt, H.H., Rognes, T., Ussery, D.W. 2007. RNAmmer: Consistent and rapid annotation of ribosomal.

Lewis, S., Searle, S.M., Harris, N., et al. 2002. Apollo: A sequence editor. Genome Biol. 3:002.

Li, H., Haiders, S., Baran, J., et al. 2009. Sequence Alignment/Map-format. Bioinformatics 25:2078–2079.

Lowe, T., Eddy, S. 1997. tRNAscan-SE: A program for improved detection of transfer RNA genes. Nucleic Acids 25:955–964.

Magrane, M., Consortium, U. 2011. BioMart: A data federation framework for large collaborative projects. Database 2011:ba038.

Markowitz, W., Chen, L., Palaniappan, K., et al. 2010. Genome-wide enzyme annotation with precision control: Catalytic families (CatFam) databases. Proteins 74(2):449–460.

Potter, C., Clarke, L., Curwen, W., et al. 2004. The Ensembl pipeline. Genome Res. 14(5):934–941.

Schwartz, S., Kent, W.J., Smith, A., et al. 2003. Human-mouse alignments with BLASTZ. Genome Res. 13(1):103–107.

She, Q., Singh, R.K., Conflonieri, F., et al. 2001. The complete genome of the narchaeon Sulfolobus solarius P2. Nat. Acad. Sci. USA 98:7835–7840.

Stanke, M., Keller, O., Gunduz, I., Hayes, A., Waak, S., Morgenstern, B. 2006. AUGUSTUS: Ab initio prediction of alternative transcripts. Nucleic Acids 34(Web Server issue):W435–W439.

Stein,L.D., Mungal, C., Shu, et al. 2002. The generic genome browser: A building for a model system database. Genome Res. 12:1259–1610.

Stewart, A.C., Osborne, B., Read, T.D. 2009. DIYA: A bacterial annotation pipeline for any genomics lab. Bioinformatics 25(7):962–963.

Yu, C., Zavaljevski, N., Desai, V., Reimman, J. 2009. Genome-wide enzyme annotation with precision control: Catalytic families (CatFam) databases. Proteins 74(2):449–460.

Zhang, J., Haider, S., Baran, J., et al. 2011. BioMart: A data federation framework for large collaborative projects. Database 2011:ba038.

Zhou, P., Emmert, D., Zhang, P. 2006. Using Chado to store genome annotation data. Curr. Prot. Bioinformatics Chapter 9:Unit 9.6.

