spent on a basic block, several lines of code, or even a single line of the source code inside a function. In this way, we can identify the performance-intensive function (hot-spot function) or lines of code (hot block) in the software algorithm [14].

# 20.3 EXPERIMENTS

In this section, we first present how we set up the experiments. Then we present the results from our experimental data in detail.

# 20.3.1 Experiment Setup

The experiments have been conducted on BEACON, an energy-efficient cluster that utilizes Intel Xeon Phi coprocessors. BEACON is funded by the National Science Foundation (NSF) to port and optimize scientific codes to the coprocessors based on Intel's MIC architecture [15]. By June 2013, BEACON was listed at the no. 3 position among the most energy-efficient supercomputers in the world on the Green500 list [16] and at the no. 397 position among the most powerful supercomputers in the world on the TOP500 List [17]. BEACON currently has 48 compute nodes. Each compute node houses two 8-core Intel Xeon E5-2670 processors, 256 GB of memory, and four Intel Xeon Phi 5110P coprocessors. This specific Xeon Phi model has 60 cores and 8 GB of memory [15]. To compile the code, we use icc version 14.0.2 and OpenMP version 4.0.

To obtain the results, we conducted this experiment using the following steps:

+   1. Write the source code in C code on BEACON and then verify the correctness and validate against the original results obtained from Microsoft Visual Studio 2010.
+   2. Study the workload characterization of the iris matching algorithm by using Intel VTune.
+   3. Based on the results from previous steps, rewrite this program by adding the parallelism and vectorization features.
+   4. Compare all the results; get the optimal number of threads, the influence of different affinities, as well as vectorization on the performance.

# 20.3.2 Workload Characteristics

The workload used in the experiment is from the Quality in Face and Iris Research Ensemble (Q-FIRE) data set [18] and Q-FIRE II Unconstrained data set, where we used a total number of 574 iris samples. The iris matching process is to match every iris sample against the entire data set, resulting in a total of 164,451 comparisons. In this section, we will demonstrate the results of the performance analysis.

In our iris matching algorithm, each sample needs to be compared against all the other samples in the database, so the main function will have a two-level nested loop for comparison. Each iteration will load two samples (both template and mask) for comparison and then calculate the Hamming distance to generate the matching score [14]. VTune