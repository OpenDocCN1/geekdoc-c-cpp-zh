# 5 SCAFFOLDING ALGORITHMS

IGOR MANDRIC

Department of Computer Science, Georgia State University, Atlanta, GA, USA

JAMES LINDSAY AND ION I. MĀNDOI

Department of Computer Science and Engineering, University of Connecticut, Storrs, CT, USA

ALEXANDER ZELIKOVSKY

Department of Computer Science, Georgia State University, Atlanta, GA, USA

# 5.1 SCAFFOLDING

Due to rapid advances in high-throughput sequencing (HTS) technologies, the interest in the problem of novo genome assembly has been renewed. These technologies, also referred to as next-generation sequencing (NGS), can produce millions of short paired-reads covering whole genome; thus, the throughput is a magnitude higher than the classic Sanger sequencing. It is worth noting that the cost of producing keeps a decreasing trend, making NGS a very attractive tool for a high range of applications. For example, Illumina HiSeq platform is to produce billions of reads in a single run at a cost of cents per megabase. The number of reads (shotgun reads) is significant due to their short length, genome assembly still represents a challenging problem.

Current assemblers (Velvet (1), ALLPATHS-LG (2)) output a set of contiguous DNA chunks, usually referred to as contigs. Contig length can vary from hundreds to hundreds of thousands base pairs. As genomes generally constitute millions of base pairs, the resulting assemblies are highly fragmented

> Computational Methods for Next Generation Sequencing Data Analysis, First Edition.
Edited by Ion I. Mandoiu and Alexander Zelikovsky.
© 2016 John Wiley & Sons, Inc. Published 2016 by John Wiley & Sons, Inc.
Companion website: www.wiley.com/go/Mandoiu/NextGenerationSequencing