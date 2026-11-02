
need to be highly parallel and vectorial in order to optimize the performance on this platform. The developers can maximize parallel performance on Xeon Phi in four ways:

- Increasing concurrency in parallel regions
- Reduction of serial code
- Minimizing the number of critical sections
- Improvement of load balance

They should also vectorize applications to maximize single instruction multiple data (SIMD) parallelism by including vectorial directives and applying loop transformations as needed, in case the code cannot be automatically vectorized by the compiler [5].

Xeon Phi can be used in two different modes: native and offload. In our experiments, we focused on the offload mode. There are two problems we need to handle in the offload mode: One is managing the data transfer between the host and the coprocessor; the other is launching the execution of functions (or loops) on the coprocessor. For the offload mode, all the data transfer between the host and the coprocessor goes through the PCIe bus. Therefore, an attempt should be made to exploit data reuse. This is also a consideration for applications written using OpenMP that span both the host and the coprocessor. Getting the benefit from both the host and Xeon Phi is our goal.

## 20.2.2 Iris Matching Algorithm

An iris matching algorithm has been recognized as one of the most reliable methods for biometric identification. The algorithm we used in this study is based on Daugman's iris matching algorithm [8], the most representative iris matching method. The procedure of an iris matching algorithm can be summarized as follows:

- 1. Generate a template along with a mask for the iris sample.
- 2. Compare two iris templates using Hamming distances.
- 3. Shift Hamming distance calculation to counter rotational inconsistencies.
- 4. Get the sample pair with the lowest Hamming distance reading.

After sampling the iris region (pupil and limbus), the iris sample is transformed into a two-dimensional (2-D) image. Then Gabor filtering will extract the most discriminating information from the iris pattern as a biometric template. Each iris sample is represented with two 2-D matrices of bits (20 rows by 480 columns). The first one is the template matrix representing the iris pattern. The second one is the mask matrix, representing aspects such as eyelid, eyelash, and noise (e.g., specular reflections), which may occlude parts of the iris. Two iris samples are compared based on the Hamming distance calculation, with both matrices from each sample being used. The calculated matching score is normalized between 0 and 1, where a lower score indicates that the two samples are more similar.

The main body of the algorithm is a 17-round for-loop structure with the indexing shifting from –8 to 8, performing bit-wise logical operations (AND, OR, XOR) on the matrices. We suppose that the matrices of the first iris sample are named as *template1* and *mask1* and the matrices of the second iris sample are named as *template2* and *mask2*. In each round, three steps are needed to finish the procedure. Firstly, *template1* and *mask1* are rotated for 2 × |shift| columns to form two intermediate matrices, named *template1s* and *mask1s*. They will be left-rotated if shift is less than 0 or right-rotated if shift is larger than 0. Secondly, we will XOR *template1s* with *template2* into *temp* and OR *mask1s* with *mask2* into *mask*. Finally, Matrix *temp* will be ANDed with Matrix *mask* to form Matrix *result*. So the Hamming distance from this round is calculated by dividing the number of 1s of Matrix *result* by the total number of the 2-D matrix entries (which is 20 × 480) minus the number of 1s in Matrix *temp* [9]. The minimum-valued Hamming distance of all 17 iterations shows the two samples' similarity, which is returned as the matching score of the two samples.

### 20.2.3 OpenMP

OpenMP [10] is an application programming interface (API) that supports multiplatform shared-memory parallel programming in FORTRAN, C, and C++. It consists of a set of compiler directives and library routines, in which runtime behavior can be controlled by environment variables [11]. Annotating loop bodies and sections of the codes, compiler directives are used for parallel execution and marking variables as local or shared (global). Certain constructs exist for critical sections, completely independent tasks, or reductions on variables [12].

When a for loop is declared to be parallel, the iterations of the loop are executed concurrently. The iterations of the loop can be allocated to the working threads according to three scheduling policies: static, dynamic, and guided. In static scheduling, the iterations are either partitioned in as many intervals as the number of threads or partitioned in chunks that are allocated to the threads in a round-robin fashion. Dynamic scheduling partitions the iterations in chunks. Those chunks are dynamically allocated to the threads using a first-come first-served policy. Finally, the guided scheduling policy tries to reduce the scheduling overhead by allocating first a large amount of work to each thread. It geometrically decreases the amount of work allocated to the thread (up to a given minimum chunk size) in order to optimize the load balance [12]. In this study, we use the default static scheduling policy. In addition, the `#pragma omp parallel` directive can be used to mark the parallel section, and the `#pragma simd` directive can be used to perform the vectorization. In this study, we employed both.

### 20.2.4 Intel VTune Amplifier

In order to get an insight into the software behavior, we employed the Intel VTune Amplifier XE 2013 [13] (in short, VTune) to perform the workload characterization of the iris matching algorithm. VTune analyzes the software performance on IA-32- and Intel 64-based machines, and the performance data are displayed in an interactive view. At the granularity-of-function level, VTune breaks down the total execution time and shows the time spent on each function, so the function consuming most of the execution time is identified as the “hot-spot function.” At a finer granularity level, it can also show the time spent on a basic block, several lines of code, or even a single line of the source code inside a function. In this way, we can identify the performance-intensive function (hot-spot function) or lines of code (hot block) in the software algorithm [14].

## 20.3 EXPERIMENTS

In this section, we first present how we set up the experiments. Then we present the results from our experimental data in detail.

### 20.3.1 Experiment Setup

The experiments have been conducted on BEACON, an energy-efficient cluster that utilizes Intel Xeon Phi coprocessors. BEACON is funded by the National Science Foundation (NSF) to port and optimize scientific codes to the coprocessors based on Intel's MIC architecture [15]. By June 2013, BEACON was listed at the no. 3 position among the most energy-efficient supercomputers in the world on the Green500 list [16] and at the no. 397 position among the most powerful supercomputers in the world on the TOP500 List [17]. BEACON currently has 48 compute nodes. Each compute node houses two 8-core Intel Xeon E5-2670 processors, 256 GB of memory, and four Intel Xeon Phi 5110P coprocessors. This specific Xeon Phi model has 60 cores and 8 GB of memory [15]. To compile the code, we use icc version 14.0.2 and OpenMP version 4.0.

To obtain the results, we conducted this experiment using the following steps:

- 1. Write the source code in C code on BEACON and then verify the correctness and validate against the original results obtained from Microsoft Visual Studio 2010.
- 2. Study the workload characterization of the iris matching algorithm by using Intel VTune.
- 3. Based on the results from previous steps, rewrite this program by adding the parallelism and vectorization features.
- 4. Compare all the results; get the optimal number of threads, the influence of different affinities, as well as vectorization on the performance.

### 20.3.2 Workload Characteristics

The workload used in the experiment is from the Quality in Face and Iris Research Ensemble (Q-FIRE) data set [18] and Q-FIRE II Unconstrained data set, where we used a total number of 574 iris samples. The iris matching process is to match every iris sample against the entire data set, resulting in a total of 164,451 comparisons. In this section, we will demonstrate the results of the performance analysis.

In our iris matching algorithm, each sample needs to be compared against all the other samples in the database, so the main function will have a two-level nested loop for comparison. Each iteration will load two samples (both template and mask) for comparison and then calculate the Hamming distance to generate the matching score [14]. VTune
