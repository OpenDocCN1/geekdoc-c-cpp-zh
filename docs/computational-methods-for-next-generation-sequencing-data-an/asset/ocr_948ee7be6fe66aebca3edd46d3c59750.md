# SCAFFOLDING ALGORITHMS

# 121

![](bbox=[0.313, 0.101, 0.686, 0.483])

**Figure 5.7** Contigs A, B, and C with connecting bundles of read pairs and the corresponding scaffolding graph. Each contig is split into two nodes connected with a dummy edge. Each bundle of read pairs corresponds to an inter-contig edge connecting respective strands with the two strands.

**5.3.2.2 Scaffolding Graph** ScaffMatch (17) constructs the scaffolding graph in the following way. Each vertex of the scaffolding graph $G = (V, E)$ corresponds to one of the contig strands (SILP2 denotes every contig as a graph node in one of the four states, see Figure 5.2) and *inter-contig* edge corresponds to a bundle of read pairs connecting two strands of different contigs (see Figure 5.7). The weight of an inter-contig edge is equal to the size of the corresponding bundle. Also for each contig we have a dummy edge connecting its two strands.

**5.3.2.3 Matching Scaffolding** Ideally, we expect that the scaffolding graph would consist of a set of paths each corresponding to a different chromosome (see Figure 5.8a). Unfortunately, repeats introduce noisy edges connecting unrelated contigs from different chromosomes. Additionally, the paths corresponding to chromosomes may skip short contigs (especially contigs which are shorter than the insert length). Therefore, any set of paths passing through dummy edges in the scaffolding graph $G$ corresponds to a plausible scaffold (see Figure 5.8b). The most likely scaffold (see Figure 5.8c) would be supported by the largest number of read pairs. Therefore, we can formulate the following