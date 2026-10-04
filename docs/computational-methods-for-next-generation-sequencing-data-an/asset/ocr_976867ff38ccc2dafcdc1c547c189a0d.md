# COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

low-quality sequences and likely artifacts. Vector and adapter sequences and also polyadenylation stretches at the ends of the reads, which could cluster sequences from unrelated genes, can be detected and removed using a tool such as cutadapt (16). Sequencing errors often impact the last few positions in a read, creating sequence differences that prevent assembly; they can be removed by clipping the last few bases of reads. Furthermore, *de novo* assemblers use the topology of the De Bruijn graph to detect and correct sequencing errors occur randomly. Lastly, error correction methods have been devised and are highly successful in correcting DNA reads prefix to assembly (17), improving the quality of the assembled sequence. These methods detect identifying sequence words that have a smaller than expected number of occurrences in the data set. However, few of these methods have been adapted to RNA-seq data, an area of active development.

# 11.2.2 The De Bruijn Graph for RNA-seq Assembly

11.2.2.1 The De Bruijn Graph in Sequence Assembly The De Bruijn graph was introduced to bioinformatics by the work of Iury and Waterman (18) and Pevner et al. (19), who applied it to the problem of assembling genes. This data structure is based on short sequence segments of a fixed length $k$ (typically $k \ge 19$), called $k$-mers. Given a sequence or set of input sequences, the corresponding De Bruijn graph has a node for each distinct $k$-mer that occurs in the input, and an edge between two nodes if the two $k$-mers are adjacent in an input sequence (Figure 11.2). Consequently, for each edge, the $(k - 1)$ length suffix of the originating node ($k$) coincides with the $(k - 1)$ prefix of the target node. Usually, the nodes are labeled with the $k$-mer occurrence count.

```
$V_1$ = AGCTAGTCACCTT $quad r_{1,1}$ AGCTAGAGT $quad k = 4$
$V_2$ = AGCTGCCTT $quad r_{1,2}$ GTACACCT
$r_{1,3}$ AGCTGCCTT
$r_{2,1}$ GCTGCCTT
```

AGCT $ightarrow$ GCTG $ightarrow$ CTGA $ightarrow$ GAG $ightarrow$ GAGT $ightarrow$ AGTC $ightarrow$ GTCA $ightarrow$ TCAC $ightarrow$ CACC $ightarrow$ ACCT $ightarrow$ CCTT

CTGC $ightarrow$ TGCC $ightarrow$ GCCT

AGCTG $ightarrow$ CTGAGTCACCTT $ightarrow$ CCTT

"bubble": $(2k - 2) = 6$

**Figure 11.2** De Bruijn graph for two variants, $v_1$, and $v_2$, sampled by five reads. The expanded graph is shown at the top and the graph with compressed nonambiguous paths at the bottom. The alternative splicing event passes as a "bubble" with one of the two paths of length $(2k - 2)$.

![](bbox=[0.121, 0.597, 0.879, 0.853])