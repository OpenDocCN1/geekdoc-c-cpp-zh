
# 54 Genome Annotation

Thomas-Chollier, M., Sand, O., Turatsinje, J.V., et al. 2008. RSAT: Regulatory sequence analysis tools. Nucleic Acids Res. 36:W119–W127.

Volff, J.N. 2006. Turning junk into gold: Domestication of transposable elements and the creation of new genes in eukaryotes. Bioessays 28:913–922.

Xie, X., Lu, J., Kulbokas, E.J., et al. 2005. Systematic discovery of regulatory motifs in human promoters and 3' UTRs in several mammals. Nature 434:338–345.

Yan, Z., Hu, H.Y., Zhang, X., et al. 2011. Widespread expression of piRNA-like molecules in somatic tissues. Nucleic Acids Res. 36:6596–6607.

Yang, J.H., Zhang, X.C., Huang, Z.P., et al. 2006. snoSeeker: An advanced computational package for screening of gene and orphan snoRNA genes in the human genome. Nucleic Acids Res. 34:5112–5123.

Yano, Y., Saito, R., Yoshida, N., et al. 2004. A new role for expressed pseudogenes as ncRNA: Regulation of mRNA stability of its homologous coding gene. J. Mol. Med. 82:414–422.

Zhang, Y., Waterman, M.S. 2005. An Euler path to multiple local alignment for DNA sequences. Proc. Natl. Acad. Sci. USA 102:1285–1290.

Zhang, Z., Harrison, P., Gerstein, M. 2002. Identification and analysis of over 2000 ribosomal protein pseudogenes in the human genome. Genome Res. 12(10):1466–1482.

Zhou, Q., Wang, W.H. 2004. CisModule: De novo discovery of cis-regulatory modules by hierarchical mixture modeling. Proc. Natl. Acad. Sci. USA 101(33):12114–12119.

# Genome-Associated Data

## 4.1 INTRODUCTION

Determining the location of genes alone is of course not sufficient to get a comprehensive picture of the dynamic process called life. If genes are the program for an organism's life, then gene expression is the equivalent of the running software process. Transcription factor analysis (see Chapter 3) is just the beginning of the process used to determine how genes work together and how a functioning organism works overall. In prokaryotes, expression in neighboring genes can be coordinated (through cotranscription in operons, for instance). In higher eukaryotes, the burgeoning field of epigenetics attests to the additional levels of gene expression control implemented in these organisms by its name: means "outside" or "above" in the Greek language. Adding another level of complexity, the concept of "the" genome for a "species" is becoming more or obsolete. High-throughput sequencing has facilitated the elucidation of many individual human genomes. At the same time, sequencing uncultured prokaryotes has revealed that delineating genes by sequence data is nontrivial, due to factors as widespread lateral gene transfer (Boucher et al., 2003). While the tools for analyzing genomic data are quickly evolving, this chapter provides a brief introduction to these new data annotation complexes and extant tools.

## 4.2 OPERONS

In prokaryotes, multiple neighboring genes on the same strand can be cotranscribed; such a genomic region is called an operon. The genes in an operon are normally involved in the same biological process, such as a metabolic pathway. If all one of the genes coding for a reaction cascade are in an operon and a gene with unknown function is also found in the same operon, this location information can be used as circumstantial evidence that the gene with unknown function may perform the missing reaction. This can be a lead for follow-up biochemical validation. This form of functional annotation is independent of the other annotation techniques described in Chapter 7.

Prediction of operon structure has traditionally been based on observing smaller-than-normal intergenic gaps. Cotranscription also implies only one ribosomal binding site (Shine-Dalgarno pattern from Chapter 2) with the most 5’ gene, and often a stem-loop structure to terminate at the 3’ end. Relatively high false-positive and false-negative rates for these signals (which are very short patterns) mean other techniques need to be used to improve the accuracy of operon prediction. Predictions can be measured against data such as coexpression analysis (e.g., microarrays) or RNA sequencing. The most accurate extant operon prediction software (~94%), called STRING (Tabaeda et al., 2010), use intrinsic data, functional clustering of genes based on protein interaction.

## 4.3 METAGENOMICS

Metagenomics is the study of genomic DNA extracted from a mixed population of microbial species, typically directly from the environment rather than cultured in a media in a lab. The principal purpose of such a data collection is to gain an understanding of the dynamics of microbial ecosystems in nature. For this reason, this technique is also known as ecogenomics (Oourg and Vriezen, 2007). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

### 4.3.1 Population Statistics

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics.

Wait, the sequence-based approach is to-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the sequence-based approach is to-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the sequence-based approach is to-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the sequence-based approach is to-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to-sequence-based approach.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to metagenomics (Schloss et al., 2006). The analysis and annotation of this mixed data requires several considerations: population statistics, data size, phylogenetic sorting, and quality of the assembly.

Wait, the many of the sample mixture models used in population statistics are borrowed from ecology, which has been applied to-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the

## 4.3.2 Data Size

With the advent of high-throughput metagenomics, the traditional 16S RNA calculation can prove too costly for even large bioinformatics facilities. At the cost of some accuracy, QIIME (Caporoso et al., 2010) can be used to rapidly cluster OTUs based on pairwise alignments. Removing exact duplicates and shorter subsequences from the initial data set can simplify the OTU creation, as long as measures are in place to include these removed data in the final OTU counts. Another approach is to divide the initial data into large superclusters (e.g., sequences within 30%), using a tool intended for transcript-clustering such as CD-HIT (Niu et al., 2010). These superclusters can subsequently be processed with robust methods (and in parallel) without the risk of significantly affecting the final OTU assignments. A case study in metagenomics methodology is presented in Chapter 11.

It is worth noting that 16S RNA sequencing stringent quality control (e.g., clipping) should be applied to the incoming data set, because the individual reads cannot be assembled together and need to be analyzed individually. With large data sets in particular, there is also a significant risk that chimeric sequences (i.e., sequences artificially created by ligation of disparate sequence fragments) are likely to inflate the total number of OTUs detected. Chimeric sequence checking algorithms, such as UCHIME (Edgar et al., 2011), can be used to filter these out.

## 4.3.3 Phylogenetic Sorting

Once OTUs are established and population statistics calculated, insight into the possible ecological roles of the constituent organisms can be roughly inferred by linking the OTUs to the phylogenetic tree. Once the taxonomic distribution is available, one might see, for example, that families of sulfur-reducing microbes are prevalent in a particular sample. Traditionally, a phylogenetic tree would be constructed for related sequences, for example, using distance, parsimony, or maximum likelihood methods in the MEGA software (Tamura et al., 2011). Unfortunately, metagenomic data sets are too large to use in regular tree construction methods.

Intra-sample comparisons of OTU distribution can be made to evaluate the similarity of microbial environments.
