
# DISCOVERING AND GENOTOMIC TWILIGHT ZONE DELETIONS

22. Treangen TJ, Salzberg SL. Repetitive DNA and next-generation computational challenges and solutions. Nat Rev Genet 2012;13:557–567.

23. Emde A-K, Schulz MH, Weese D, Sun R, Vringron M, Kalscheuer VM, Haas SA, Reinert K. Detecting indent variants with exact breakpoints in single-and and paired-end sequencing using PlayerS. Bioinformatics 2012;28(5):619–627.

24. Schroeder J, Hsu A, Boyle SE, Macintyre G, Cmero M, Tothill RW, Johnston RW, Shackleton M, Papenfuss AT. Socrates: identification of genomic rearrangements in tumour genomes by re-aligning clipped reads. 2014. DOI: 10.1093/bioinformatics/ct067.

25. Zhang Z, Du J, Ham L, Abyzov A, Urban AE, Snyder Gerstein M. Identification of genomic indels and structural variations using split reads. BMC Genomics 2011;12:375.

26. Jiang Y, Wang Y, Brudo M. Prism: pair-read input split-read mapping for accurate and efficient calling of base-pair level detection of insertion, and structural variants. Bioinformatics 2012;28(20):2578–2583.

27. Zhang J, Wang J, Wu Y. An improved approach for accurate and efficient calling of structural variations with low-coverage sequence data. BMC Bioinf 2012;13: Suppl 6:S6.

28. Toepfer A, Marschall T, Bull RA, Luciani F, Schönhuth A, Beerenwikel N. Viral quasispecies assembly via maximal clique enumeration. PLoS Comput Biol 2014;10(3):e1003515.

29. Marschall T, Schönhuth A. Sensitive long-indel-aware alignment of sequencing reads. Technical report, 2013. arXiv:1303.3520.

30. Wu TD, Nacu S. Fast and SNP-tolerant alignment of complex variants and splicing in short reads. Bioinformatics 2010;26:873–881.

31. Wu TD, Watanabe CK. GMAP: a genomic mapping and alignment program for mRNA and EST sequences. Bioinformatics 2005;21:1859–1875.

32. Langmead B, Salzberg SL. Fast gained-read alignment with Bowtie 2. Nat Methods 2012;9(4):357–359.

33. Lunter G, Goodman M. Stampy: a statistical algorithm for sensitive and fast mapping of illumina sequence reads. Genome Res 2011;21(6):936–939.

34. Langmead B, Trapnell C, Pop M, Salzberg SL. Ultrafast and memory-efficient alignment of short DNA sequences to the human genome. Genome Biol 2009;10(3):R25.

# 8 COMPUTATIONAL APPROACHES FOR FINDING LONG INSERTIONS AND DELETIONS WITH NGS DATA

JIN ZHANG
McDonnell Genome Institute, Washington University in St. Louis, MO, USA

ONG CHU AND YUFENG WU
Department of Computer Science & Engineering, University of Connecticut, Storrs, CT, USA

## 8.1 BACKGROUND

Structural variation (SV), or genomic structural variation, is the variation in the structure of an organism's genome. When there is a reference genome of a species, a variation is usually defined relative to the reference genome. Among different genomes of one species, there can be many types of SVs, such as deletions, insertions, duplications, copy number variants, inversions, and translocations. While many structural variations affect disease susceptibility, such as cancer. Great efforts have been taken to map and categorize SVs in large-scale projects, such as the 1000 Genome Project (1) and The Cancer Genome Atlas (2). Many computational tools of calling SVs have been developed and applied to these projects.

In this chapter, we will cover some aspects of the computational methods that can call certain types of SVs (namely long insertions and deletions) using next-generation sequencing (NGS). It is known that insertions and deletions are among the most common SVs in the genome. More, long indels may potentially have significant impact on some phenotypes. NGS has become the standard technology in discovering

Computational Methods for Next Generation Sequencing Data Analysis, First Edition.
Edited by Ion I. Mandoiou and Alexander Zelikovsky.
© 2016 John Wiley & Sons, Inc. Published 2016 by John Wiley & Sons, Inc.
Companion website: www.wiley.com/go/Mandoiou/NextGenerationSequencing

# COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

Reference

![](img/46aec008551cecb3bbf3aac2ee69b926_192_0.png)

SVs recently. High-throughput and low-cost NGS technologies make it possible to discover SVs from thousands of samples. On the other hand, there are also challenges for calling SVs using NGS. First, NGS sequence reads are short and may contain sequencing errors and artifacts. Second, these sequence reads be generated not perfectly uniformly and coverage may vary at many regions of the genome. Third, the volume of sequence reads is often very large.

One approach is assembling the sequence reads to obtain the complete donor (or alternative) genome. If the donor genome is well known, one may compare the donor genome with the reference genome (which is available for many species) to find the SVs. Figure 8.1 shows an example of a simulated donor genome which contains one long deletion and one long insertion. The simulated reference genome is 1 million base pairs (bp) long. The donor genome does not have the sequences from 25,001 to 251,000 (the portion marked with light grey), and a segment that does not exist in the reference genome (the portion marked with dark grey). Compared to the reference genome, the donor genome has a long deletion and a long insertion.

In practice, however, it is often difficult to assemble a perfect donor genome using NGS reads. A main issue for assembling NGS reads is the short reads length, the distribution of reads is usually uneven, which may lead to low coverage on some regions of the genome. The noise contained in the reads also present serious challenges for assembly. Moreover, the donor genome itself can be repetitive.

An alternative strategy for finding SVs from sequence reads is calling SVs from the reads without performing assembly. There are many computational tools that use NGS data to call SVs. Most of these tools fail in one of the four categories of methods of calling structural variants, namely: (i) assembly (AS), (ii) read depth (RD), (iii) read pair (RP), and (iv) split read (SP). In the following, we will describe the main idea of each of these methods. We introduce some tools to illustrate these approaches, by primarily considering techniques in calling deletions and insertions (especially deletions). Some of these techniques may be applicable to other types of SVs. We note that certain kinds of SVs may need other techniques not described in this advantage.

Each category of mentioned earlier has its advantages and disadvantages in calling different SVs. It is unlikely that a tool from one would be able to call all the SVs from the sequence reads. One category of method may be intrinsically not able to find certain SVs. Instead of using tools of one, it might be sensible to combine results of tools from different categories in calling SVs, as The 1000 Genomes Project does (3). There are different ways of running multiple tools on the same data with various parameters, and then taking the intersection, union

# COMPUTATIONAL APPROACHES FOR FINDING LONG INSERTIONS AND DELETIONS

some other subsets of the output of these tools as the final result. The overall precision is the percentage of true positives (TPs) in the final list, and the overall sensitivity is the percentage of TPs out of all TPs. For example, running each tool with relatively stringent parameters may lead to good overall accuracy when using the union. Note that the overall accuracy might be lower than using a single tool because different tools share some SVs. By using multiple tools, the overall sensitivity can be much higher than using a single tool, since there be many TPs that are picked up by a small number of tools. Thus, a combined method may have higher accuracy and sensitivity. Also note that the combined approach, if devised properly, can lead to more efficient algorithms. We will introduce such combined method in Section 8.2.4.

In this chapter, we first describe the main approaches from different categories, including the combined approaches. We then introduce ongoing projects that SV calling methods have been applied to. Finally, we provide a conclusion and discussion for future research directions.

## 8.2 METHODS

We now describe the technical ideas of various approaches. Each approach relies on some kind of signal contained in the reads that indicate the occurrence of SVs. We call such signals the signatures of SVs.

### 8.2.1 Signatures of Long Indels in Sequence Reads

In the problem of SV calling, we care more about whether there are some SVs in the donor genome and the coordinates of true SVs. Coordinates are measured according to the positions of the bases of reference genome. For example, the coordinates for the long deletion in Figure 8.1 is reference : 250,001–251,000, and the long insertion between reference : 750,000 and reference : 750,001. Note that the NGS reads are
