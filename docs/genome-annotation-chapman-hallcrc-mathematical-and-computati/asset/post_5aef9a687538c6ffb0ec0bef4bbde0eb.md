
# Genome-Associated Data 67

Pruesse, E., Quast, C., Knittel, K., et al. 2007. SILVA: A comprehensive online resource for quality checked and aligned ribosomal RNA sequence compatible with ARB. Nucleic Acids Res. 35(2):7188–7196.

Pusharev, D., Neeff, N.F., Quake, S.R. 2009. Single-molecule sequencing of an individual human genome. Nat. Biotechnol. 27(9):847–850.

Röhe, C., Zhang, Y., Jurkowski, T.P., Stamerjanns, H., Reinhardt, R., Jeltsch, A. 2008. Bisulfite sequencing Data Presentation and Compilation (BPC) Web server—a useful tool for DNA methylation analysis. Nucleic Acids Res. 36(5):e234.

Schloss, P.D., Westcott, S.L., Ryabin, T., et al. 2009. Introducing mothur: Open-source, platform-independent, community-supported software for describing and comparing microbial communities. Appl. Microbiol. 75(23):7537–7541.

Real, R., Gordon, S.M., Lush, M.J., Wright, M.W., Bruford, E.A. 2011. Genomics: The NCBI resources in 2011. Nucleic Acids Res. 39(Database issue): D514–D519.

Segal, E., Fondufe-Mittendorf, Y., Chen, L., et al. 2006. A genomic code for some positioning. Nature 442(7014):772–278.

Sun, Y., Cai, Y., Liu, L., et al. 2009. ESPR: Estimating species richness using large collections of 16S rRNA sequences. Nucleic Acids Res. 37(10):e76.

Taboida, B., Verde, C., Merino, E. 2010. High accuracy operon prediction method based on STRING database searches. Nucleic Acids Res. 38(12):e130.

Tamura, K., Peterson, D., Peterson, N., Stecher, G., Nei, M., Kumar, S. 2011. MEGA5: Molecular evolutionary genetics analysis using maximum likelihood, evolutionary distance, and maximum parsimony methods. Mol. Biol. Evol. 28(10):2731–2739.

Wang, Q., Garrity, G.M., Tiedje, J.M., Cole, J.R. 2007. Naive Bayesian classifier for rapid assignment of rRNA sequences into the new bacterial taxonomy. Appl. Environ. Microat. 73(16):5261–5267.

Wples, R.S., Gaggiotti, O. 2006. What is a population? An empirical evaluation of some genetic methods for identifying the number of gene pools and their degree of connectivity. Mol. Ecol. 15:1419–1439.

Westberger, S.J., Cui, L., Dharia, N., Winzeler, E., Cui, L. 2009. Genome-wide nucleosome mapping of Plasmodium falciparum reveals histone-coding and histone-poor intergenic regions and chromatin remodeling of core and subtelomeric genes. BMC Genomics 10:610.

# Characterization of Gene Function through Bioinformatics

The Early Days

## 5.1 OVERVIEW

The characterization of gene sequences began with the invention of protein sequencing techniques (Edman, 1949) and intensified after DNA sequencing became a reality (Gilbert and Maxam, 1973; Sanger et al., 1973). In the early days of sequence production, computation was in its infancy, with punch cards and primitive mainframe computers as the only means to perform bioinformatics tasks. Despite these rudimentary environments, researchers began to develop tools that allowed the comparison of sequences (Doolittle, 1981). The next phase of computer development introduced the command line terminals and large-scale data storage on disk drives. Still, the Web did not exist and computing was only accessible to a select minority. With the creation of early personal computers, especially the IBM PC, the Apple II, and the Atari 520, this changed dramatically, as all of a sudden access to computers became a possibility for most scientists. At the same time, the programming tools evolved rapidly, that it was possible for many to create scripts and programs to assist in the analysis of sequence information. To this day, some of the bioinformatics tools developed early on are still in use and students at the university level are still learning how to use a command line interface (now of course on UNIX machines).

# 70 Genome Annotation

It was recognized early on that the newly created protein and DNA sequences needed to be stored in a public repository, similar to books and other works in libraries; therefore GenBank, the European Molecular Biology Laboratory (EMBL) Data library, and Japanese International Protein Information Database (JIPID) were founded (Benson et al., 1993; Kneale and Kennard, 1984). As the Internet really not yet exist as a commodity in these early days, the data were initially distributed on tapes and floppy disks at a cost. Smith and Waterman created the original exhaustive search algorithm for sequence data in 1984 (Lipman et al., 1984). It turned out that the exhaustive search was too slow, so heuristic methods were developed. FASTA (Pearson and Moldatos, 1988) and BLAST (Altschul et al., 1990) were the first tools to allow rapid searches of databases. These tools were used to identify motifs within proteins (Durbin et al., 1992) and restriction sites (Roberts and Edelman, 1993). Hydrophobicity plots can also be used (Whiteley et al., 1967).

Many early tools were bundled into suites, which grew over time. For example, Clustal (Thompson et al., 1994) and T-Coffee (Notredame et al., 1998) were used for multiple sequence alignment. However, many early tools were limited to 100,000 amino acids or base pairs, a restriction that was eventually broken by the advent of complete genomes. When the first microbial genomes were presented in the year 1995, the only tools to handle complete sequence were word processors, such as Microsoft Word or Wordstar.

Characterization of Gene Function through Bioinformatics ■ 71

Initially, the sequences created in the laboratories were only a few acids long. One should not forget that it took several months to create even 1000 bp sequence in the early days of DNA sequencing. As the main memory on personal computers, and even mainframes, were very limited (640 kilobytes was considered very large), the bioinformatics tool developers universally restricted the maximum size of a sequence that could be handled at once. One problem, which began to haunt researchers early on, was the large number of different file formats, which were developed without coordination.

## 5.2 STAND-ALONE TOOLS FOR THE INTERNET

Bioinformatics began with the creation of individual tools and evolved into the provision of complete packages, which could be used to analyze DNA and protein sequences. Several of the original stand-alone tools were so essential in bioinformatics that they are still used as individual tools today. We cannot make any attempt to list all of them, some, which were important for the creation of genome analysis pipelines, are discussed next.

The FASTA and BLAST tools really opened up the ability to efficiently search the databases to almost anyone, as these tools allowed rapid searches on benign hardware and gave reasonable approximate answers within a short period of time.

Two alignment tools really shine, and both were created by Des Higgins: Clustal (in its various incarnations up to the most recent ClustX) (Thompson et al., 1994) and T-Coffee (Notredame et al., 1998). The original publication describing Clustal remains one of the most cited bioinformatics publications of all time and both tools are still in use in many laboratories. Figure 5.1 shows an example of using Clustal to perform multiple sequence alignment.
