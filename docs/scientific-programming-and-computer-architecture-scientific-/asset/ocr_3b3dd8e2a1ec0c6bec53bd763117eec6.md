# 416 Chapter 6. Special Topic: Networks and Message Passing

| | nprocs = 2 | nprocs = 10 | nprocs = 20 | nprocs = 50 | nprocs = 100 |
|---|---|---|---|---||}{
| $10^5$ | 0.66 | 0.627 | 0.64 | 0.43 | 0.50 |
| $10^5$ | 1.92 | 1.58 | 1.49 | 1.63 | 1.62 |
| $10^5$ | 1.71 | 1.56 | 1.59 | 1.69 | 1.59 |

Table 6.3: Bandwidths in bytes/cycle for cyclic data exchange on QDR Infiniband. All hosts are 3.33 GHz SSE2 machines (see table A.1). The number of double-precision numbers in each message is $n$.

on each MPI process. The $post()$ is immediately followed by $wait()$, although in general program may perform some computations before it waits for the posted requests to be complete.

Table 6.3 shows the network bandwidth holds up quite well as the number of communicating agents increases from 2 to 100. The bandwidth is measured by each host as the number of bytes transferred into or of it in a single cycle. The reported numbers are medians of a large number of trials and correspond to the process of rank 0. For this simple pattern of communication, the bandwidth realized are often in the advertised QDR Infiniband port bandwidth of 5 GB/s, which corresponds to 1.5 bytes/cycle.

# 6.3.2 Jacobi iteration

The Jacobi iteration is a technique for solving linear systems that arise when partial differential equations are discretized. Jacobi is an iterative method. Successive iterations improve the guess with each iteration, reducing the error by a factor greater than 1. The iterations are stopped when the error is deigned to be low enough.

Poisson's equation $u_{xx} + u_{yy} = \mathit}{}= f$ is amenable to the Jacobi iteration once the equation is discretized using finite differences or finite elements. The Jacobi iteration by itself is not a particularly effective method for solving such differential equations. However, the Jacobi iteration can be supplemented by other ideas, such as multigrid, and turned into a powerful method.

The data in the Jacobi iteration is laid out as a matrix $a_{ij}$, $0 \le i < m$ and $0 \le j < n$. The matrix is split between MPI processes by column. Each MPI process