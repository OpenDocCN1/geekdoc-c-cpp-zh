# COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

pairs $p_1$ and $p_2$ in Figure 11.3a are compatible, whereas $p_1$ and $p_3$ have inconsistent splice junctions and are incompatible. Unlike with single-end reads, in this case, the unknown region of the fragment may overlap with two fragments that have different and incompatible sets of splice junctions. For instance, in Figure 11.3a, $p_2$ is compatible with both $p_1$ and $p_3$, but $p_1$ and $p_3$ are incompatible with each other. In such a case, compatibility or incompatibility cannot be assigned to the three pairs of fragments without introducing a conflict.

To avoid conflicts, Cufflinks removes these “uncertain” reads prior to constructing the overlap graph, so that paths in the graph encode pairwise compatible fragments that could form complete isoforms. Figure 11.4 shows an overlap graph that encodes three isoforms.

# 11.3.1.2 Connectivity Graphs and Splicing Graphs Overlap graphs captured connectivity at the level of reads. More recently, two other types of structures, namely connectivity graphs and splicing graphs, have been used in transcript assembly to capture relationships among genomic or transcribed bases.

Connectivity graphs, as used in Scripture (27) and Isoasso (26), represent each genomic position as a vertex. Two vertices are connected by an edge if they are either consecutive on the genome or if they are linked by a spliced alignment. Thus, the graph represents the connectivity of bases along the transcript, whose projection on the genome is interrupted by introns.

By comparison, a splicing graph (28) retains only those portions of the genome covered by reads. Nonambiguous paths in the graph can be collapsed to a single vertex without losing any structural information. Vertices in the splicing graph

![](bbox=[0.208, 0.565, 0.792, 0.814])

**Figure 11.3** Inconsistencies occurring with paired-end reads. Source: Li et al. (2021). Adapted with permission of Mary Ann Lieber. (a) Read pairs $p_1$, $p_2$, as well as $p_2$ and $p_3$, are compatible, whereas $p_1$ and $p_3$ cannot originate from the same isoform. Read pair $p_2$ is uncertain. (b) The splicing graph comprises five exons and four paths (isoforms). Exon combinations ACE and B are infeasible, since the read pair supporting splice site AC includes exon D and the read pair supporting junction BC additionally includes exon E.