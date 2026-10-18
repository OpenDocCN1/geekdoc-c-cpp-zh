
![](img/16cb41208935c5f22dd1044f03f2e31b_339_0.png)

Users provide their own source and sink-side application code and can freely link to dynamic libraries.

de-marshalling operands from the hStreams remote invocation interface, and implementing the user-defined functionality. Helper functions that make marshalling easier are envisioned for future product releases. The hStreams runtime manages the dependencies, the remote signaling, the passing of parameters, and the memory operand address translation.

hStreams executables have multiple parts: an executable for the source, for example, a Xeon host, and a dynamic library for the sink, for example, a coprocessor, as shown in Figure 15.14. Each side is separately compiled and has its own references to dynamically loaded libraries, as usual. If users follow the convention that the sink-side dynamic library has the same name as the source-side executable, but with a _mic extension, then the sink-side dynamic library name need not be specified.

## RELATED WORK

hStreams is most similar to CUDA Streams from NVidia. While CUDA Streams uses FIFO semantics within each stream, hStreams’ ability for actions to execute and complete out of order creates greater performance opportunities. hStreams’ event interfaces are designed to be easier to use, and to allow greater concurrency. First, each action has an associated event; events do not need to be created separately after actions are enqueued. Events do not need to be explicitly created, registered, and destroyed. It is possible to wait for a set of events, for example, within a stream.

The hStreams interface does not need the boilerplate code that OpenCL does. Unlike tasks in SyCL, MPI, OmpSs, Qualcomm MARE, CnC, and others, task dependencies need not be explicitly specified. Unlike SyCL, Phalanx, CnC, UPC++, CHARM++, and Chapel, there is no current dependence on C++ or other language mechanisms. As a library, hStreams does not depend on users to stay current with the latest versions of compilers, as is the case for the Offload Streams feature of the Intel compiler (under development as of this writing). The current hStreams interfaces are at a lower level than related systems such as Trilinos and Legion. Other frameworks that deal with distributed environments, like Global Arrays and TIDA or simple offloading, like OpenMP TR3 do not offer the FIFO stream

## FIGURE 15.16

4 × 4 tiling of matrix for tiled Cholesky factorization. The tiles are colored according to the BLAS operations that are applied to them in the first pass of the outer-loop for the algorithm in Figure 15.17.

two operations. For the inner most loop, this requires: 2 * (i − (k + 1) + 1) or 2 * (i − k) operations. Thus total complexity is written as:

```
∑_{k=1}^m ∑_{i=k+1}^m 2(i − k) = 2∑_{k=1}^m (m − k + 1)(m − k)/2 ≈ ∑_{k=1}^m k² ≈ m³/3. (15.4)
```

To make use of the high-performance BLAS level-3 functions of the MKL library, we next show a tiled version of the Cholesky factorization algorithm. For this, the matrix is divided into square tiles as shown in Figure 15.16. The algorithm is given in Figure 15.17. The matrix is divided into T tiles for each side.

In Figure 15.16, each tile color corresponds to an MKL BLAS operation, namely, dpotrf, dtrsm, dsyrk, and dgemm. The actual MKL function names for the C-interface for these functions are LAPACKE_dpotrf, cblas_dtrsm, cblas_dsyrk, and cblas_dgemm, respectively. For details on these MKL functions, the reader is referred to the MKL reference manual. The colored tiles in the figure are the ones which are processed in the first iteration of the outer k-loop of the algorithm. In a right-looking algorithm, these colors (and corresponding BLAS operations) move to the right for each outer-loop iteration. The tiles in

```
1: for k = 1, T do
2:   A_{k,k} ← LAPACKE_dpotrf(A_{k,k})
3:   for m = k + 1, T do
4:     A_{m,k} ← cblas_dtrsm(A_{k,k}, A_{m,k})
5:   end for
6:   for n = k + 1, T do
7:     A_{n,n} ← cblas_dsyrk(A_{n,k}, A_{n,n})
8:     for m = n + 1, T do
9:       A_{m,n} ← cblas_dgemm(A_{m,k}, A_{n,k}, A_{m,n})
10:    end for
11:  end for
12: end for
```

## FIGURE 15.17

Tiled Cholesky factorization algorithm.

each column get finalized (contain factored data) as we move through the outer loop. Note that only the lower triangular half of the matrix (including the diagonal tiles) are operated on. The white tiles are not operated on. The overall compute is dominated by the `cblas_dgemm` operation at the inner most loop which executes on the matrix tile of size `tile_size`. The cost of this dgemm on the tile is `2 * (tile_size)^3`. The total computational cost for the tiled algorithm is also `m^3/3` (not derived), which is the same as the elemental algorithm, where `m` is the matrix size, with `m = T * tile_size`.

Using this tiled algorithm as baseline, we next describe an offload algorithm for tiled Cholesky factorization. The offload algorithm uses both the host CPU and coprocessor using the `Streams` framework. Before describing the algorithm, it is important to understand the data and compute dependences in a tiled Cholesky program as described above. For this, we construct a task-graph for the tiled Cholesky program. Figure 15.18 shows this task-graph for a 4 × 4 tiling. For each outer-loop iteration, the compute

![](img/16cb41208935c5f22dd1044f03f2e31b_342_0.png)

## FIGURE 15.18

Task dependence graph for 4 × 4-tiled Cholesky factorization. Solid connections indicate dependences within the same outer-loop iteration of algorithm in Figure 15.17, and dashed connections indicate dependences between the current and subsequent outer-loop iteration. The rectangles indicate compute operations and parallelograms indicate input matrix data.

dependences are as follows: dpotrf is computed first on the “hot” diagonal tile (hot tiles are tiles that contain the final factored data after the current iteration of the outer-loop), dtrsm operations are conducted next on the tiles in the hot column, dgemm and dsyrk operations are finally conducted on all the remaining tiles on the right of hot column, but only for the lower-triangular part of the matrix. Note that dpotrf requires only the data for its own tile, dtrsm requires two input tiles—its own tile and the diagonal tile directly above its own tile on which dpotrf was executed. dsyrk also requires two input tiles—its own tile and the hot tile on which dtrsm was executed in the same block row as itself. Lastly, dgemm requires three input parameters—its own tile, and two hot tiles on which dtrsm was executed, one corresponding to the row-index and other corresponding to the column-index of its own tile. Also note, that dgemm and dsyrk operations do not depend on each other and can be concurrently executed. Thus, the concurrency (i.e., how many BLAS operations can be executed in parallel) for a 4×4 tiled matrix, changes dynamically within the same outer loop iteration: first 1 dpotrf operation, then 3 dtrsm operations, and finally 3 dgemm and 3 dsyrk operations together for k = 1. So the maximum concurrency of 6 comes from the concurrent execution of dsyrk and dgemm operations. One can follow the dependence graph as we move to the next iteration of outer-loop. In general, the concurrency can be written as (T − k) + ½(T − k − 1) * (T − k) for T tiles at kth outer-loop iteration. Understanding of concurrency is very important for optimal scheduling of compute and data transfers to the streams. It is important that the number of streams be smaller than the maximum concurrency so that we do not under-subscribe the coprocessor, at least for the first few outer-loop iterations. The load balancing will be better if the concurrency is an integer multiple of number of streams for as many outer-loop iterations as possible.

For the offload tiled Cholesky algorithm using the hStreams library (hereafter called “tiled hStreams Cholesky”), we first define an important concept called “function-specific targeting,” which means executing functions on architectures for which they are best suited. For example, executing a function which does not have much parallelism on the host processor (which has good serial performance) and a function which as a great deal of intrinsic parallelism on the coprocessor. For this algorithm, we execute the dpotrf on the diagonal hot tile on the processor as dpotrf does not have a lot of parallelism because of task dependences. All the other functions (i.e., dtrsm, dsyrk, and dgemm) are executed on the coprocessor. At the time of writing this chapter, running streams with the host processor as sink is not implemented in the hStreams library so we execute the dpotrf using the host thread and MKL library takes care of spawning multiple host threads to parallelize the dpotrf. There is ongoing work to extend the hStreams capability so that one can concurrently run streams on both host processor and the coprocessor. With that capability, seamless function-specific targeting of kernels of the application will be possible.

**NOTE**
Use function-specific targeting to execute kernels of an application on either the host or the coprocessor depending on the kernel characteristics such as inherent parallelism.

The algorithm for tiled hStreams Cholesky is given in Figure 15.19. The entries of the input matrix A are overwritten with those of the Cholesky factored matrix as the algorithm proceeds. The algorithm details steps for the first iteration of the outer-loop (k = 1) for brevity. For the other outer-loop iterations, one also needs to add extra synchronization steps between each outer-loop iteration by following the task-graph in Figure 15.18. Note also that all the data transfers for the input matrix required for the coprocessor are completed by the end of the first iteration of outer-loop. The algorithm starts by
