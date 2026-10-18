![](bbox=[0.21, 0.11, 0.73, 0.38])

# FIGURE 6.11

Speedup of Cellulose NVE (408,609 atoms) on two configurations using optimized code: two processors, two processors, and one coprocessor.

Figure 6.11 shows the speedup of the offload implementation when scaling across multiple nodes in comparison to using the parallel implementation of Amber’s pmemd engine. Runs were carried out on two different platforms:

+   1. Processor-only platform whereby a node is comprised of two Intel Xeon E5 2697 processors (24 cores) on a dual socket platform (IVT).
+   2. Processor and coprocessor platform whereby the node is comprised of two Intel Xeon E5 2697 processors (24 cores) plus one Intel Xeon Phi 7120P coprocessor (61 cores) on a dual socket platform.

The total number of MPI tasks are shown in the X-axis for various numbers of nodes. For the offload runs, atom distribution was modified so, that in each node, only the middle 4 MPI ranks offload direct space sum work to the coprocessor. Each offloading MPI rank uses a quarter of the coprocessor’s cores (15 cores). The same network switches (Single-Rail FDR Mellanox IB) are used for both platforms. The original Amber MD code does not scale well beyond about 96 MPI ranks because of all-to-all MPI communications used to distribute atom coordinates, force arrays, and FFT arrays. Thus performance results are only shown for up to 4 nodes (4 × 24 MPI ranks/node = 96 MPI ranks). As seen from the figure, the coprocessor offload code consistently out-performs the processor-only code. It also shows that the offload implementation has similar scaling to the processor-only code.

# CONCLUSIONS

In this chapter, version 14 of the pmemd MD (MD) engine in the Amber MD software package was extended to support offloading to an Intel Xeon Phi coprocessor. Work involved the implementation of a two-fold decomposition strategy that employs spatial decomposition of the system using MPI