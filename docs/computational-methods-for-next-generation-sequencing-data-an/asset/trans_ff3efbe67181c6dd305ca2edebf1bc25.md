

242

NGS 数据分析的计算方法

- 11. Hogges, E, Molaro A, Dos Santos CO, Thekat P, Song Q, Uren PJ, Park J, Butler J, Rafii S, McCombie WR, Smith AD, Hannon G. Directional DNA methylation changes and complex intermediate states lineage specificity in the adult hematopoietic compartment. Mol Cell 2011;44(1):1–12.
- 12. Fang F, Edges E, Molaro A, Dean MD, Hannon G, Smith AD. The genetic landscape of human-epigenetic DNA methylation. Nat Acad Sci U S A 2012;109(9):7332–7337.
- 13. Li Y, Zhi J, Jian G, Li N, Qi Y, Meng Z, Hu J, Wu H, Sun J, Zhang Q, Chen R et al. The DNA methylation of human fetal blood mononuclear cells. PLoS Biol 2010;8(11):e100053.
- 14. Wang RR, Taouf C, Nagarajan RP, Hong D, Downey SL, Johnson BE, Fuse Delaney D, Ahmed Y, Olshehen A, Ballinger T, Zhou X, Forsberg KJ, Gu Echaire, O'Green H, Lister R, Pizzola M Y, Epstein CB, Bernstein BE, Hawkins RD, Farm PJ, Gu Y, Bu C, Garker A, Smith MQ, Decker ER, Li, Farm M, Milosavlvic J. Comparison of sequencing-based methods for profile DNA methylation and identification of monoallelic modifications. Nat Biotechnol 2010;28(10):1097–1150.
- 15. Kruger F, Buerke F, Andrews SR. DNA methylation analysis using short bisulfite data. Nat Methods 2019(2):145–151.
- 16. Burrows M, Wheeler D. A block sortless dictionary data compression algorithm. Technical Report #14. Palo Alto (CA): Digital Equipment Corporation;1994.
- 17. Zeschnik M, Martin M, Betz G, Kalbe A, Srisch C, Biting S, Gross F, Fritz, Elias F, Rahmann A, Rosshmann S. Massive parallel bisulfite sequencing of CG-rich DNA fragments reveals methylation of X-chromosomal CpG sites in female DNA is incomplete. Hum Mol Gen 2009;18(8):1439–1448.
- 18. Xi Y, Li W, BSMAP: whole genome bisulfite sequencing mapping. BMC Bioinformatics 2009;10(1):232–240.
- 19. Coarca C, Yu F, Miller CA, Chen Z, Harris RA, Milosavlvic A. Pash 3.0: A versatile software for read mapping and integrative analysis of genomic and epigenomic variation using massively parallel DNA sequencing. BMC Bioinformatics 2010;11(1):572.
- 20. Din QH, Dublin M, Sedbrack J, Lettner N, Mittelteidcheid O, van Haesler A. Advanced methylation analysis after bisulfite sequencing: an example in Arabidopsis. PLOS ONE 2012;7(7):e41528.
- 21. Smith AD, Chung WY, Hodges E, Kendall J, Hannon G, Hicks J, Xuan Z, Zhang MQ. Methods using the RMAP short-read methylation sequencing. Bioinformatics 2009;25(2):2841–2842.
- 22. Harris EY, Ponts N, Lechuk A, Lech R, Lonardi S. BRAT: bisulfite-treated reads analysis tool. Bioinformatics 2010;26(4):572–573.
- 23. Chen PY, Soks J, Pleijberg M B Seeker: precise mapping for bisulfite sequencing. BMC Bioinformatics 2010;11(1):203.
- 24. Kruger F, Andrews S. Bismark: a flexible linker and methylation springer for Bisulfite-Seq applications. Bioinformatics 2011;27(11):1571–1572.
- 25. Harris EY, Ponts N, Lech KG, Lonardi S. BRAT-BW: efficient and accurate methylation of bisulfite-treated reads. Bioinformatics 2012;28(13):1795–1796.
- 26. Smith TF, Waterman MS. Identification of molecular sequences. J Mol Biol 1981;147:195–197.
- 27. Langmead B, Trapnell C, Pop M, Salz S. Ultrafast and memory-efficient alignment of short DNA sequences to the human genome. Genome Biol 2009;10(3):R25.

# 基于亚硫酸盐转化的 DNA 甲基化测序方法

- 28. Xi Y, Bock C, Müller F, Sun D, Meissner A, Li W. RRBSMAP: a fast, accurate and user-friendly alignment tool for reduced representation bisulfite sequencing. Bioinformatics 2012;28(3):430–432.
- 29. Guo W, Fiziev P, Yan W, Cokus S, Sun X, Zhang MQ, Chen PY, Pellegrini M. BS-Seeker2: a versatile aligning pipeline for bisulfite sequencing data. BMC Genomics 2013;14(1):774.

## 引言

转录组分析的主要目标是鉴定和表征基因，因为 RNA-seq 已证明能够捕捉跨越五个数量级的表达范围。然而，由于文库制和测序的偏差，即使在同一转录本内的覆盖度也不均匀。此外，每个读可能会被分配给具有相似序列的多个家族基因，或者同一个基因的多个异构体。重叠基因、嵌套基因以及反剪接等生物现象增加了组装的难度。最后，RNA-seq 实验产生的海量数据需要具有扩展性和高效性的工具。

转录本组装分为两类：从头（*de novo*），仅基于序列重叠进行组装；以及基于基因组，先将读比对到参考基因组，然后对重叠的比对结果进行组装。基于基因的方法通常更准确。然而，在缺乏基因组或基因组高度碎片化的情况下，从头组装可以有效地确定代表性转录本集，尽管组装过程更为复杂且容易出错。我们将在接下来的章节中介绍这两种方法、具体方法及其设计原则。

## 11.2 从头组装

这类方法根据序列的重叠进行组装。直观地说，如果一个读的末端序列与另一个读的开头相似，这种关系就确定了这两个读在原始序列中的顺序。

