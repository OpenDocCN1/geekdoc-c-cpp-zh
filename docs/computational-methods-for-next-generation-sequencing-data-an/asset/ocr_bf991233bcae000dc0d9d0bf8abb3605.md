# SCAFFOLDING ALGORITHMS

# 5.2.5 SCARPA

SCARPA formulates the problem of contig orientation as finding a minimal odd cycle transversal in the scaffolding graph G = (V,E) built as follows: each contig c is represented by two nodes c+ and c- in V (5' and 3' of the contig) and each edge consists of two types of edges, namely connecting the two nodes of contig and the edges between the two nodes of different contigs correspond to read pairs mapping to the corresponding strands.

In addition to removing contigs such that no odd cycles remain in G, SCARPA allows discarding inconsistent edges. For each edge in E, two auxiliary nodes are introduced and in case there is a tie between removing a node in V and removing an auxiliary node, the last option is preferred, resulting in discarding a suspicious link between contigs rather than removing a contig from the node set V.

Although the orientation stage removes odd-length cycles, the directed graph may still have cycles. Contig ordering is obtained after all directed cycles are eliminated by solving the feedback arc set problem.

In the last stage, SCARPA solves a linear program for determining a topological ordering such that the distance between the contigs agrees best with the size of the gaps.

# 5.3 RECENT SCAFFOLDING TOOLS

In this section, we provide a detailed description for two recent scaffolding algorithms, namely SILP2 and ScaffoldMatch.

# 5.3.1 SILP2

Given a set of contigs C and a set of read pairs R, the scaffolding problem asks for the most likely orientation of the contigs along a partition of the contigs into ordered sets connected by read pairs of R. The main steps of the SILP2 algorithm are as follows (see Figure 5.1 for a high-level flowchart). We first map the read onto contigs using bowtie2, disregarding pairing information in the mapping process. Alignments are processed to extract read pairs for which both have unique alignments, and the alignments are onto distinct contigs. A scaffolding graph is then constructed with nodes representing contigs and edges representing extracted read pairs. The scaffolding graph is partitioned into 3-connected components using the SPQR data structure (11, 12) implemented in OGDF (13). The maximum likelihood orientation is formulated as an ILP that is efficiently solved by applying nonlinear dynamic programming based the SPQR tree structure. Next, scaffold chains are extracted from the ILP solution by bipartite matching and breaking remaining cycles. Finally, maximum likelihood estimates for the gap lengths are obtained using quadratic programming. In the following, we detail the key steps of the algorithm, including scaffolding graph construction, the maximum likelihood models used for contig orientation, and mapped read probability estimation, then we briefly overview the orientation, the ILP formulation, and the improved NSDP algorithm for efficiently solving the ILP.