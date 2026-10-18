![](bbox=[0.203, 0.122, 0.812, 0.485])

**FIGURE 5.10**  
Performance of *eFindSite* using parallel processor threads. The speed is measured by the number of RMSD calculations per second (mean ± standard deviation) for 2, 4, 8, and 16 threads across the benchmarking dataset of 501 proteins. Solid triangles and open squares correspond to the total time and the time spent calculating structure alignments, respectively.

`OMP_STACKSIZE=64M`. In Figure 5.10, we plot the performance of the multi-threaded version of *eFindSite* on the Intel® Xeon® E5-2680 processor. Using the total simulation time, the serial (1 thread) and parallel (16 threads) versions have an average performance across the benchmarking dataset of 1.06 × 10⁵ and 6.16 × 10⁵ RMSD calculations per second, respectively. When considering the time spent calculating structure alignments, the average performance increases to 1.24 × 10⁵ and 1.85 × 10⁶ RMSD calculations per second. A good linear scaling is achieved with a speedup over the serial execution of 15 when 16 processor threads are utilized. The performance reaches a plateau at a speedup of 5.8 for the total wall time; we note that according to Amdahl’s law, the maximum theoretical speedup of a code that is 90% parallelized using 16 threads is 6.4.

# TASK-LEVEL SCHEDULING FOR PROCESSOR AND COPROCESSOR

Computing nodes equipped with Intel Xeon Phi coprocessor cards provide massively parallel capabilities through multicore processors and many-core coprocessors. Therefore, our ultimate goal was to develop a production code of *eFindSite* that takes full advantage of both resources. The production scheme