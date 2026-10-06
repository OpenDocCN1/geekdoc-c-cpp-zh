

## 基因组相关数据 ■ 63

- 错义/非同义——氨基酸的翻译将与参考基因组不同。
- 无义——SNP（单核苷酸多态性）引入了框内终止密码子。
- 读通（Read through）——SNP 移除了参考序列中的终止密码子。

HGVS 语法也允许在蛋白质水平上描述变异。第 488 位残基从氨酰胺变为精氨酸描述为“p.Gln488Arg”。也可以使用单氨基酸 IUPAC 编码（LiBecq, 1992）。SNP 还可以通过其他方式影响蛋白质翻译。引入提前终止密码子的 SNP 将标记为“p.Gln488Ter”。如果该变化产生了一个半胱氨酸，且下一个框内终止密码在下游 25 个氨基酸（即 75 个碱基），则读通的语法为“p.Ter797Cys*25”。

位于外显子的某些变异可能会产生新的（“隐性”）受体或供体剪接位点（例如 Dunn 等人，2002）。内含子中的 SNP 变异也可能破坏供体或受体位点。在少数情况下，它们还会在通常内含子的区域内部创建一个新的外显子（也称为隐外显子）。在 5’ UTR 中，SNP 可能会破坏转录因子的供体或创建一个新的偏好密码子。在 3’ UTR 中，SNP 可能会破坏基因的聚聚腺化信号，还会破坏微RNA 抑制机制，这些正开始被分类（Bruno 等人，2012）。所有这些可能性都说明了对基因及相关控制元件进行正确注释的重要性。

来自1100 千基因组计划的 VCF 文件以及文献中报道的 SNP 变异和小插入或缺失（indels）可从 NCBI 的 dbSNP 数据库获取（Day, 2010），并带有相关疾病等资源的链接。

## 4.4.3 插入与缺失

### 4.4.3.1 命名法

插入是指个体中存在但参考基因组中不存在的额外碱基（而非碱基替换）。这些可以在 VCF 文件中报告。对于编码序列中第 22 和 23 碱基之间插入 TTG，HGVS 语法为“c.22_23insTTG”。缺失是指相对于参考基因组个体中碱基的移除。对于删除五个（末–起始+1）碱基，HGVS 语法为“c.22_26del”，在单碱基缺失的情况下，允许使用语法“c.22del”。与参考序列相比删除的序列可以附加地在此在此语法（例如 c.11delT）。

## 64 基因组注释

由同时发生的插入和缺失事件组成的复杂变异通常称为 indels。对于用四个碱基 TTTG 替换参考序列中的三个碱基的情况，HGVS 语法为“c.345_347delinsTTTG”。indels 的一种特殊情况是倒位，其中插入序列与缺失序列长度相同，且两个序列为反向互补。这种情况下，六个碱基倒位的 HGVS 语法为“c.665_670inv”。

由于插入和缺失跨越了多个碱基位置，其命名可能非常复杂。例如，“c.344_347+2del”是一个六碱基缺失，移除了四个编码碱基和（推测的）内含子供体 GT。语法“c.89-7*_89delinsGAA”是一个五碱基 indel，位于 3’ UTR 外显子的受体位点之前。插入的一种特殊情况是参考基因组短序列的重复，语法为“c.345_348dup”。

### 4.4.3.2 效应

除了 SNP 的情况外，插入和缺失还可能导致蛋白质区域氨基酸的插入或缺失。如果变异长度不是三的倍数，将会发生翻译移码。例如，如果移码导致氨基酸从半胱氨酸变为色氨酸且框内终止在39个残基之后，HGVS 语法为“p.Cys254Tr”。列出新的终止位置，“p.Cys254ps”也是有效的。

## 4.4.4 拷贝数变异

在多倍体基因组中，染色体片段的数量发生在个体中（Freeman 等人，2006）。这些拷贝数变异（CNVs）可能通过基因剂量效应影响基因并导致疾病（Alman 和 Path, 2012）。高通量测序 CNV 检测尚处于起阶段，使用比较基因组杂交（CGH）生成相对拷贝数估计（例如 -1 或 1）。在可用高分辨率数据的情况下，Wiggle 文件格式（Kent 等人，2010）适用于存储并在 UCSC 基因组浏览器中绘图（见第 9 章）。当 CNV 数据为粗粒度时，BedGraph 文件格式（Kent 等人，2010）可以简洁地表示这些信息并被许多浏览器接受。用于 CNVs、大插入和缺失以及易位（即结构变异）的公共存储库 dVAR，现在由一个国际联盟协调（Church 等人，2010）。癌症通常是特定基因中新发突变的产物。对于关注癌症相关结构变化的，一个优秀的公共资源是 Progenetix（Baudis, 2006）。

## 参考文献

Alkan, C., Poe, B., Eichler, E.E. 2011. 基因组结构变异发现与基因分型。Nat. Rev. Genet. 12(5):366–376.

Almal, S.H., Padh, H. 2012. 健康与疾病中的基因拷贝数变异。Hum. Gen. 57(1):6–13.

 Babu, A., Verma, R.S. 1987. 染色体结构：常染色质与异染色质。Int. Rev. Cytol. 108:1–60.

Bartreff, T., Troop, D.B., Wilhite, S.E., 等 al. 2011. NCBI GEO: 功能基因组数据集存档。Nucleic Acids. 39:D1005–D1010.

Baudis, M. 2006. 支持癌症细胞遗传学的在线数据库和生物信息学工具。Biotechniques 40:296–272.

Boucher, Y., Douadycy, C., Papke, R.T., 等 al. 2003. 水平基因转移与原核基因的起源。Annu. Rev. Genet. 37:283–328.

Bruno, A.E., Li, K., Kalabas, J., Hu, Z. 2012. miRSNP: 疾病相关 SNP 和人类基因 3' UTR 上的 miRNA 靶点数据库。BMC Genomics 13(1):44.

Caporoso, J.G., Kuczynski, J., Stombaugh, J., 等 al. 2010. 高通量测序数据的 QIIME 分析。Nat. Methods 7(5):335–336.

Church, D.M., Lappalainen, I., Sneddon, T.P. 2010. 基因组变异的公共数据存档。Nat. Genet. 42(10):813–814.

Daneck, P., Anton, A., Abecasis, G., 等 al. 2001. 变异检测格式与 VCFools。Bioinformatics 17(15):2156–2158.

Day, I.N. 2000b. 详细的 SNP 与拷贝数复杂性。Hum. Mutat. 31(1):2–4.

den Juden, T.J., Antonarakis, S.E. 2000. 突变编号扩展与描述复杂突变的建议。Hum. Mutat. 15(1):7–12.

DeSantis, T.J., Holzloft, P., Larsen, N., 等 al. 2006. Greengens，一种基于变异的基因组分析工具。Appl. Environ. Microbiol. 72(7):506–512.

Dunn, D., Ishigami, J., 2002. 全基因组隐性剪接位点的鉴定。J. Mol. Biol. 319(2):363–374.

Edgar, R., Haas, B., Clemente, J., 等 al. 2011. ENCODE 用户指南。PLoS Biol. 9(4):e1001.

Felsenstein, J. 2004. 从 DNA 序列推推系统发育树。牛津大学出版社。

Freeman, S.L., 等 al. 2006. 人体的拷贝数变异。Cell 122(4):90–100.

Harbison, C.T., Levine, S., 等 al. 2005. 酵母核小体乙酰化和甲基化的全基因组图谱。Wait, I. Kent, W.J., 等 al. 2010. UCSC 基因组浏览器的 Wiggle 文件格式。Bioinformatics 26(17):2204–2210.

Kwan, C., 1992. 生化学命名。London: Portland Press.

Ludwig, J. 1991. 基于香农熵的测量。IEEE T. Inform. Theory 37(1):145–155.

Markowitz, V., 等 al. 2008. IMG/M: 一种数据管理系统。Nucleic Acids Res. 36:D534–D538.

