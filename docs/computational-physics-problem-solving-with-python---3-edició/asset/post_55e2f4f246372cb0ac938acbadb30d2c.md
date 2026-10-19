
each instruction requires, and “cycle time” is the actual time it takes for one CPU cycle. After thinking about (10.3), we can understand the CISC philosophy that tries to reduce CPU time by reducing the number of instructions, as well as the RISC philosophy, which tries to reduce the CPU time by reducing cycles/instruction (preferably to 1). For RISC to achieve an increase in performance requires a greater decrease in cycle time and cycles/instruction than is the increase in the number of instructions.

In summary, the elements of RISC are the following:

- **Single-cycle execution,** for most machine-level instructions.
- **Small instruction set,** of less than 100 instructions.
- **Register-based instructions,** operating on values in registers, with memory access confined to loading from and storing to registers.
- **Many registers,** usually more than 32.
- **Pipelining,** concurrent preparation of several instructions that are then executed successively.
- **High-level compilers,** to improve performance.

## 10.5 CPU Design: Multiple-Core Processors

The present time is seeing a rapid increase in the inclusion of multicore (up to 128) chips as the computational engine of computers, and we expect that number to keep rising. As seen in Figure 10.5, a dual-core chip has two CPUs in one integrated circuit with a shared interconnect and a shared level-2 cache. This type of configuration with two or more identical processors connected to a single shared main memory is called symmetric multiprocessing, or SMP.

Although multicore chips were originally designed for game playing and single precision, they are finding use in scientific computing as new tools, algorithms, and programming methods are employed. These chips attain more integrated speed with less heat and more energy efficiency than single-core chips, whose heat generation limits them to clock speeds of less than 4 GHz. In contrast to multiple single-core chips, multicore chips use fewer transistors per CPU and are thus simpler to make and cooler to run.

Parallelism is built into a multicore chip because each core can run a different task. However, because the cores usually share the same communication channel and level-2 cache, there is the possibility of a communication bottleneck if both CPUs use the bus at the same time. Usually the user need not worry about this, but the writers of compilers and software must. Modern compilers automatically make use of the multiple cores, with MPI even treating each core as a separate processor.

## Dual CPU Core Chip

![](img/bccda43674e4a93dee81c749eba8d2f7_245_0.png)

(a)

![](img/bccda43674e4a93dee81c749eba8d2f7_245_1.png)

(b)

Figure 10.5 (a) A generic view of the Intel core-2 dual-core processor, with CPU-local level-1 caches and a shared, on-die level-2 cache (courtesy of D. Schmitz). (b) The AMD Athlon 64 X2 3600 dual-core CPU (Wikimedia Commons).

## 10.6 CPU Design: Vector Processors

Often the most demanding part of a scientific computation involves matrix operations. On a classic (von Neumann) scalar computer, the addition of two vectors of physical length 99 to form a third, ultimately requires 99 sequential additions (Table 10.2). There is actually much behind-the-scenes work here. For each element i there is the fetch of a(i) from its location in memory, the fetch of b(i) from its location in memory, the addition of the numerical values of these two elements in a CPU register, and the storage in memory of the sum in c(i). This fetching uses up time and is wasteful in the sense that the computer is being told again and again to do the same thing.

When we speak of a computer doing vector processing, we mean that there are hardware components that perform mathematical operations on entire rows or columns of matrices as opposed to individual elements. (This hardware can also handle single-subscripted matrices, that is, mathematical vectors.) In the vector processing of [A] + [B] = [C], the successive fetching of and addition of the elements A and B are grouped together and overlaid, and Z ≅ 64–256 elements (the section size) are processed with one command, as seen in Table 10.3. Depending on the array size, this method may speedup the processing of vectors by a factor of approximately 10. If all Z elements were truly processed in the same step, then the speedup would be ~ 64–256.

Vector processing probably had its heyday during the time when computer manufacturers produced large mainframe computers designed for the scientific and military communities. These computers had proprietary hardware and software and were often so expensive that only corporate or military laboratories

could afford them. While the Unix and then PC revolutions have nearly eliminated these large vector machines, some do exist, as well as PCs that use vector processing in their video cards. Who is to say what the future holds in store?

### Table 10.2 Computation of matrix [C] = [A] + [B]

| Step 1 | Step 2 | ... | Step 99 |
|---|---|---|---|
| c(1) = a(1) + b(1) | c(2) = a(2) + b(2) | ... | c(99) = a(99) + b(99) |

### Table 10.3 Vector processing of matrix [A] + [B] = [C]

| Step 1 | Step 2 | ... | Step Z |
|---|---|---|---|
| c(1) = a(1) + b(1) |  |  |  |
|  | c(2) = a(2) + b(2) |  |  |
|  |  | ... |  |
|  |  |  | c(Z) = a(Z) + b(Z) |

## 10.7 Introduction to Parallel Computing

There is a little question that advances in the hardware for parallel computing are impressive. Unfortunately, the software that accompanies the hardware often seems stuck in the 1960s. In our view, message passing and GPU programming have too many details for application scientists to worry about and (unfortunately) requires coding at an elementary level reminiscent of the early days of computing. However, the increasing occurrence of clusters in which the nodes are symmetric multiprocessors has led to the development of sophisticated compilers that follow simpler programming models; for example, partitioned global address space compilers such as CoArray Fortran, Unified Parallel C, and Titanium. In these approaches, the programmer views a global array of data and then manipulates these data as if they were contiguous. Of course, the data really are distributed, but the software takes care of that outside the programmer’s view. Although such a program may make use of processors less efficiently than would a hand-coded program, it is a lot easier than redesigning your program. Whether it is worth your time to make a program more efficient depends on the problem at hand, the number of times the program will be run, and the resources available for the task. In any case, if each node of the computer has a number of processors with a shared memory and there are a number of nodes, then some type of a hybrid programming model will be needed.

## 10.8 Parallel Semantics (Theory)

We saw earlier that many of the tasks undertaken by a high-performance computer are run in parallel by making use of internal structures such as pipelined and segmented CPUs, hierarchical memory, and separate I/O processors. While these tasks are run “in parallel,” the modern use of *parallel computing* or *parallelism* denotes applying multiple processors to a single problem (Quinn, 2004). It is a computing environment in which some number of CPUs are running asynchronously and communicating with each other in order to exchange intermediate results and coordinate their activities.

For an instance, consider the matrix multiplication:

$$[B] = [A][B]. \tag{10.4}$$

Mathematically, this equation makes no sense unless [A] equals the identity matrix [I]. However, it does make sense as an algorithm that produces new value of $B$ on the LHS in terms of old values of $B$ on the RHS:

$$[B^{\mathrm{new}}] = [A][B^{\mathrm{old}}]. \tag{10.5}$$

$$\Rightarrow\quad B_{i,j}^{\mathrm{new}} = \sum_{k=1}^{N} A_{i,k}B_{k,j}^{\mathrm{old}}. \tag{10.6}$$

Because the computation of $B_{i,j}^{\mathrm{new}}$ for specific values of $i$ and $j$ is independent of the computation of all the other values of $B_{i,j}^{\mathrm{new}}$, each $B_{i,j}^{\mathrm{new}}$ can be computed in parallel, or each row or column of $[B^{\mathrm{new}}]$ can be computed in parallel. If $B$ were not a matrix, then we could just calculate $B = AB$ with no further ado. However, if we try to perform the calculation using just matrix elements of $[B]$ by replacing the old values with the new values as they are computed, then we must somehow establish that the $B_{k,j}$ on the RHS of (10.6) are the values of $[B]$ that existed before the matrix multiplication.

This is an example of *data dependency*, in which the data elements used in the computation depend on the order in which they are used. A way to account for this dependency is to use a temporary matrix for $[B^{\mathrm{new}}]$, and then to assign $[B]$ to the temporary matrix after all multiplications are complete:

$$[\mathrm{Temp}] = [A][B], \tag{10.7}$$

$$[B] = [\mathrm{Temp}]. \tag{10.8}$$

In contrast, the matrix multiplication $[C] = [A][B]$ is a *data parallel* operation in which the data can be used in any order. So already we see the importance of communication, synchronization, and understanding of the mathematics behind an algorithm for parallel computation.

The processors in a parallel computer are placed at the *nodes* of a communication network. Each node may contain one CPU or a small number of CPUs, and
