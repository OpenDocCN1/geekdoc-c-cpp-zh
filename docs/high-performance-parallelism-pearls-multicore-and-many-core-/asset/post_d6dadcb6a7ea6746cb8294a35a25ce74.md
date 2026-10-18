
analyze the performance of the Triad kernel from this benchmark, which does a combination of the operations from the Copy, Scale, and Add kernels.

## SMITH-WATERMAN

The Smith-Waterman algorithm performs local sequence alignment for determining similar regions between two strings and is used in genomic applications to find out structural or functional similarities between nucleotides on amino acid sequences.

For this study, we used a highly tuned code that uses intrinsics to fully exploit the vector units of the coprocessor. These intrinsics are specific to 512-bit wide vectors found first on the Intel Xeon Phi coprocessor; our intrinsics should be easily adapted to Intel Xeon Phi processors with AVX-512 support (Knights Landing) and Intel Xeon processors with AVX-512 support (Skylake). The two hot loops for this application are found at approximately lines 134 and 148 in `SmithWatermanMIC()` in SmithWaterman.cpp in the Smith-Waterman source code.

## SHOC MD

The MD benchmark from the SHOC benchmark suite is a molecular dynamics kernel based on the Lennard-Jones potential. It models the interactions between nearby atoms or molecules by iteratively updating all forces in the system.

The kernel for this application is `compute_lj_force()`, found in MD.cpp. An abridged version of this function is shown in Figure 21.4.

Note the three nested loops in this function. The outermost loop (k) runs for the number of iterations required by the simulation parameters. The next inner loop (i) loops over the atoms, and the innermost loop (j) traverses the neighbors of each atom. In the body of this loop, the forces on each atom are computed based on the distance between an atom and its neighbor.

Notice that the values of the neighbors’ positions (`jposx`, `jposy`, `jposz`) come from an *indirect array access*, that is, using the values of a second “index array” (`neighList[]`) as the indices into the `position[]` array. This means that the elements of `position[]` are not necessarily accessed in sequential order; the order that they are accessed depends on the values in the `neighList[]` array. Therefore, it is very difficult for the compiler to predict a pattern of memory accesses to prefetch.

At each iteration, the item at `position[neighList[j + i * maxNeighbors]]` is accessed. This requires two memory accesses, first to get the value of `neighList[]` for the iteration, then a second memory access to the array `position[]` using that value as an index. If the accesses to this array followed a sequential or strided pattern, they would be easy to predict. However, because this code uses an index array, the access pattern is determined by the values in `neighList[]`. A diagram of the index array problem is shown in Figure 21.5. Prefetching these locations manually can help overlap the latency of memory accesses with the computation of previous iterations.

## TUNING PREFETCHING

In the following sections, we demonstrate strategies for tuning prefetching using our three example applications. The first step in tuning an application should be to determine the hot functions or loops that take up the majority of the runtime. This analysis is available for the processor and coprocessor using a tool such as Intel® VTune™ Amplifier.

![](img/16cb41208935c5f22dd1044f03f2e31b_457_0.png)

## FIGURE 21.5

Indirect accesses to an array of data using an index array can lead to unpredictable access patterns.

## PREFETCH DISTANCE TUNING ON THE COPROCESSOR

A critical parameter for success is the prefetching “distance,” which is how many iterations ahead we issue a prefetch instruction prior to using the data. To inspect the prefetch distance used automatically by the compiler, we can use compiler optimization reports. The loop optimizations are generated using the -qopt-report-phase=loop compiler options (Intel C Compiler 2015). To generate the highest level of detail, we use the option -qopt-report=5.

Sometimes it is useful to tune the prefetch distance manually instead of relying on the compiler to determine it. This is done by using the -qopt-prefetch-distance=n1,n2 compiler option. n1 represents the distance for prefetching from memory L2, while n2 represents the distance for prefetching from L2 to L1. To tune the distance for individual loops, the compiler directive #pragma prefetch var: hint:distance can be used.

## RESULTS—PREFETCH TUNING EXAMPLES ON A COPROCESSOR

Using Stream Triad, Smith-Waterman, and MD as examples, we will show how software prefetching can be tuned to improve performance on the coprocessor.

## PREFETCHING METRICS FOR STREAM TRIAD

To show why prefetching affects performance, we can look at the hardware performance counters, which can be collected using Intel VTune Amplifier. We use the values of these counters to develop two low-level metrics of prefetching effectiveness: coverage and efficiency. A useful prefetch is one that takes a miss off the critical path of the program by bringing data into the cache before it is used.

Coverage is a measure of how well prefetches replace demand misses in the execution, which should lead to higher performance. In other words, perfect coverage means that all the data used were prefetched into the cache and the program experienced no misses (other than prefetches). Coverage is calculated as follows:

Coverage = (MissesNoPrefetching − MissesWithPrefetching) / MissesNoPrefetching = SavedMisses / TotalMisses

Efficiency measures how expensive prefetching was. If many useless prefetches are issued, the cost of prefetching might outweigh the benefits. Efficiency also affects the performance because a large
number of useless prefetches may pollute the cache and waste memory bandwidth. We calculate the percent of prefetches that were actually beneficial as follows:

$$\text{Efficiency} = \frac{\text{Misses}_{\text{NoPrefetching}} - \text{Misses}_{\text{WithPrefetching}}}{\text{TotalPrefetches}} = \frac{\text{Good Prefetches}}{\text{TotalPrefetches}}$$

See the section on Useful Coprocessor Hardware Event Counters for more details about how to calculate these metrics using hardware event counters.

We measured the performance of Stream on an Intel Xeon Phi coprocessor and also collected hardware event counters using VTune. To compare the performance of prefetching, we ran the application multiple times with different prefetchers enabled or disabled. Note that software prefetching can only be disabled by recompiling the source code. The total misses and resulting performance with three combinations of prefetching settings are shown in Figure 21.6. Note that “no prefetching” is not a realistic setting because it is difficult to disable hardware prefetching, and disabling all prefetching leads to poor performance for most workloads. Here, we use it for comparison to show the benefits of prefetching. In most systems, hardware prefetching should be left on.

Compared to no prefetching, hardware prefetching improves performance by 6.8×, and the combination of hardware and software prefetching improves performance by nearly 9×. In a more realistic setting where hardware prefetching is always enabled, the combination of hardware and software prefetching improves performance by 1.3× over software alone.

The number of prefetches of each type for the two prefetching-enabled configurations is shown in Figure 21.7. The small number of software prefetches in the hardware-only case comes from prefetches already existing in related code such as libraries, not from the compiler. Notice that in the combined case, even though the hardware prefetcher is enabled, there are much fewer hardware prefetches issued. This is because the hardware prefetcher does not train itself on streams of misses that have been filtered out by the software prefetches.

![](img/16cb41208935c5f22dd1044f03f2e31b_458_0.png)

## FIGURE 21.6

Total number of misses and performance achieved on the coprocessor with three prefetching configurations. The results for each configuration were obtained by running the application multiple times with each type of prefetching enabled or disabled.
