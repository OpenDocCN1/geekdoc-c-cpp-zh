# 5.1. Introduction to OpenMP

| Number of Threads | Barrier | for | with nowait |
|---|---|---||}{
| 1 | 26 | 66 | 36 |
| 2 | 1178 | 1401 | 93 |
| 3 | 1250 | 1451 | 101 |
| 4 | 1671 | 1758 | 96 |
| 6 | 2427 | 2555 | 100 |
| 8 | 2710 | 2731 | 99 |
| 10 | 2346 | 2458 | 99 |
| 12 | 2516 | 2415 | 101 |
| 16 (2.2 GHz AVX) | 3262 | 3743 | 371 |

Table 5.2: Overheads of OpenMP constructs reported as number of cycles. All the entries of this table are for a 2.6 GHz SSE2 machine, except the last, which is for a 2.2 GHz AVX machine (see table A.1 for the full names of the machines).

important not to change the number of threads between parallel regions. Doing so will trigger the worst-case cost. The reason for that will also become clearer later.

Thus, assuming all parallel regions use the same number of threads, the cost we have to contend with the median or mean cost, which is in the thousands of cycles. The median cost is much lower for the two-core machine than the 12-core or 16-core machines (see table 5.1). The two-core machine has only one processor package for both. In the other two machines, the cores are split between two processor packages (in figures 3.6 and 4.2b). More processor packages implies greater cost.

The typical cost of around 5000 cycles for a parallel region is not prohibitive. Even a for-loop that iterates 10^5 or 10^6 times may be parallelized effectively. However, an inner loop that iterates 100 or 1000 times cannot be parallelized effectively. The overhead of entering and leaving the parallel region will overwhelm any benefit from parallelization. Thus, OpenMP parallelism is not as fine as the parallelism involved in XMM/YMM/ZMM registers (see table 3.1) or the instruction pipeline.

Table 5.2 reports the overheads of the barrier and constructs. The programs for calculating these overheads are similar to the one we just saw. Therefore, the programs are not listed.

The most striking inference from table 5.2 is that most of the cost of the omp for construct seems to be due to the implicit barrier at the end of the construct. To