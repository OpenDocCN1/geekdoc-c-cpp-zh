

# 80 基因组注释

Felsenstein, J. 1989. PHYLIP–Phylogeny Inference Package (Version 3.2). Classistics 5:164–166.

Freshman, J., Albermann, K., Hani, J., et al. 2001. 使用 PENDANT 进行功能和结构基因组学. Bioinformatics 19:44–57.

Fuchs, R., Stoehr, P., Rice, P., Omond, R., Cameron, G. 1990. EMBL 数据库的新服务。Nucleic Acids Res. 18:4319–4323.

Gaasterland, T., Tensen, C.W. 1996. 反映需求和偏好的全自动基因组分析。MAGPIE 系统架构的详细介绍。78:302–310.

Gilbert, D. 2003. 使用命令行 readseq 进行序列格式转换。Curr. Prot. Bioinformatics Appendix 1:Appendix 1E.

Gilbert, W., Maxam, A. 1973. lac 操子的核苷酸序列。Nat. Acad. Sci. USA 70:1–4.

Hennikoff, S., Jenkins, J. 1991. 用于数据库搜索的蛋白质块自动组装。Nucleic Acids Res. 19(23):6565–6572.

Kneale, G.G., Kennard, O. 1984. EMBL 核苷酸序列数据库。Biochem. Soc. Trans. 12:1011–1014.

Kolakowski, L.F., Leunissen, A., Smith, J.E. 1992. 使用与蛋白质结构功能相关的正则表达式搜索蛋白质。Bioinformatics 13:919–921.

Lipman, D., Wilbur, W., Smith, T.F., Waterman, M.S. 1984. 关于核酸相似性的统计学意义。Nucleic Acids Res. 11:215–226.

Morgan, J., Engelberg, A., Airoch. 1988. 使用 PC/GENE 进行蛋白质和核酸分析。Bioinformatics 6:566–572.

Mullan, L.J., Bleasley, A.J. 2002. 短 EMBOSS 用户指南。欧洲分子生物学开放软件get。Bioinformatics. 28:92–94.

Notredame, C., Holm, L., Higgins, D.G. 1998. COFFEE：多序列比对的性函数。Bioinformatics 14(5):407–422.

Pearson, R.W., Lipman, D.J. 1988. 改进的生物学序列比较工具。Proc. Natl. Acad. Sci. USA 85:2444–2448.

Pustell, J., Kafatos, F.A. 1984. 一种用于 DNA 和蛋白质序列处理与分析的方便且适应的微型环境。Nucleic Acids Res. 10:479–488.

Roberts, R.J., Maxwell, M. 1993. REBASE—限制酶和甲基化酶。Nucleic Acids Res. 21:3125–3127.

Sanger, F., Donelson, J.E., Coulson, A.R., Kessel, H., Fischer, G. 1973. 利用合成寡核苷酸通过 DNA 聚合酶确定 ph4 DNA 中的核苷酸序列。Proc. Natl. Acad. Sci. USA 70:1209–1213.

Smith, S.W., Overbeek, R., Woese, R., Gilbert, W., Gillet, P.M. 1994. 遗传数据环境：一个用于多序列分析的可扩展 GAP 环境。Comput. Appl. Biol. 10:671–675.

Staden, R. 1980. 一种用于 DNA 基因读段数据存储和处理的新方法。Nucleic Acids Res. 25:3673–3694.

Staden, R. 1986. 我们序列处理软件的现状和可移植性。Nucleic Acids Res. 10:217–213.

Thompson, J.D., Higgins, D.G., Gibson, T.J. 1994. Clustal W：通过序列加权、位置特异性空罚和权重矩阵选择提高渐进式多序列比对的敏感性。Nucleic Acids Res. 11:4673–4680.

# 基因组数据的可视化技术与工具

## 6.1 引言

从测序步骤开始，基因组注释涉及多个阶段，包括基因组组装、序列比对、系统发育分析和基因表达谱分析，在这些阶段，研究人员可能希望对当前处理的基因组数据获得整体且详细的理解。由于人类对以文本形式呈现的任何数据的认知能力相对较小，这一序列-注释流水线中的每个阶段无疑将受益于适当的可视化方法，这使得人们能够在有限的空间内（如屏幕）快速获取丰富的信息。

在讨论特定的可视化工具之前，我们想指出可视化的两个首括性特征。首先，从测序步骤开始，基因组注释涉及多个阶段，包括基因组组装、序列比对、系统发育分析和基因表达谱分析，在这些阶段，研究人员可能希望对当前处理的基因组数据获得整体且详细的理解。由于人类对以文本形式呈现的任何数据的认知能力相对较小，这一序列-注释流水线中的每个阶段无疑将受益于适当的可视化方法，这使得人们能够在有限的空间内（如屏幕）快速获取丰富的信息。

其次，数据的性质发生了巨大变化。

## 6.2 测序数据的可视化

随着代测序（NGS）的出现，主要的 DNA 测序数据分析发生了巨大变化。对于 Illumina Solexa 基因分析仪（www.illumina.com）和 Applied Biosystems SoliD 系统（www.appliedbiosystems.com）生成的测序数据，仅保存图像数据而没有轨迹。传统的读取比对查看器无法显示这些图像，部分原因是由于存储和显示速度的原因。此外，由于 NGS 实验通常具有高度冗余的序列覆盖，检查单个读取轨迹的意义变得较小，因为目标碱基可以与所有比对序列中相同位置的许多碱基进行比较。

