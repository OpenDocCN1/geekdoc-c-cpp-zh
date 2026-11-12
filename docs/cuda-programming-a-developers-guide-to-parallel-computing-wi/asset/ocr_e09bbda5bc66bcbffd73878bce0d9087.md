| Device Name | Function Name | Start Time | Duration | Occupancy | Registers/Thread | Grid Size | Block Size | Threads | Cache Configuration | Shared Memory Configuration |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| GeForce GTX 470 | count_gmem_768_kernel | 4,801,264 | 4,340.76 | 0.24 | 10 | (634, 1, 1) | (64, 1, 1) | 1048576 | PREFER_L1 | PREFER_L1_NONE |
| GeForce GTX 470 | count_gmem_768_kernel | 8,213,646 | 1323.28 | 0.17 | 14 | (4, 1, 1) | (64, 1, 1) | 256 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 1,056,920 | 4796 | 0.02 | 8 | (16, 1, 1) | (64, 1, 1) | 1024 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 1,056,920 | 3117.204 | 0.23 | 11 | (256, 1, 1) | (64, 1, 1) | 16384 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 10,068,726 | 3117.204 | 0.23 | 11 | (1034, 1, 1) | (64, 1, 1) | 14080 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 70,840,965 | 4264.0246 | 0.22 | 22 | (256, 1, 1) | (64, 1, 1) | 16384 | PREFER_L1 | PREFER_L1_L1 |

![](bbox=[0.13, 0.23, 0.89, 0.56])

FIGURE 9.45 Parallel Nsight occupancy.

The next experiment to look at is the “Instruction Statistics” (Figure 9.46). Here we see a few issues. There is a very high level of instructions that are being issued but not executed. This is indicative of the SM having to serialize and thus reissue the same instructions. We also see a huge spike of activity on SM 2. This is in fact very bad, as it means one of the blocks that we were allocated to this SM performed a huge amount of additional work compared with the other blocks. This indicates the blocks are not equally distributed in terms of work per block, and this is something we need to solve at the algorithm level. Some balancing of the work per block is needed.

The next experiment is the “Branch Statistics,” which tells us how much the execution within a warp diverges (Figure 9.47). We ideally want a very small if not zero value for branch divergence. Here we see 16% of the branches diverge, which contributes to the reissuing of instructions we saw in the “Instruction Statistics” experiment. This too originates from the algorithm in that the amount of work per thread varies. It points to the need to balance the workload between the work blocks.

The next experiment looks at the ability of the SM to issue and execute instructions. We’d expect to see a roughly equal distribute in terms of the “Active Warps per Cycle” chart. It shows that despite SM