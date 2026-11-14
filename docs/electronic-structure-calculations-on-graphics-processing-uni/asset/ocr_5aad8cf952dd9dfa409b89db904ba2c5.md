the time required for data transfers across the PCI-Express bus. These can be measured using CUDA events on the GPU. Based on the measurements, we can calculate the average computational and transfer time per output unit. From these we can solve the optimal split value so that the GPU gemm time equals the sum of the transfer times and the CPU gemm time.

Each time the hybrid gemm routine is called, we calculate new values for the average times per unit and use those to update previously calculated and stored values. Approximately similar matrix sizes get grouped together. A small benchmark matrix multiplication is run when the routine is called for the first time to get initial values. During the SCF iteration, the split ratio should converge to an optimal value. Alternatively to splitting A and C row-wise as in Eq. (9.20), it is also possible to split B and C matrices column-wise. In the hybrid gemm routine, we choose either the row-wise or column-wise split, based on which we minimize the total transfer cost.

For the nsyrk2x BLAS routine (zher2k in the complex case), we can perform the decomposition as follows:

```
[C] = [C1] + [C2] = a [A1] [B1^T] + a [B1] [A1^T] + beta [C]. (9.21)
```

Now we can calculate C1 on the GPU:

```
C1 = a (A1 B1^H + B1 A1^H) + beta C. (9.22)
```

At the same time, we transfer A2 and B2, asynchronously to the host and then compute on the CPU:

```
C2 = a (A2 B2^H + B2 A2^H). (9.23)
```

We then transfer the resulting matrix C2 to the device and calculate C. As before, we can estimate and update the optimal decomposition parameters. The hybrid nsyrk and zherk functions can be thought of as simplified versions of this.

# 9.3.3 Parallelization for Multiple GPUs

In GPAW, the high-level parallelization of the code is done with the MPI (message passing interface). Multiple GPUs can be used by domain decomposition of the real-space grid or by parallelizing over k-points or spins. Domain decomposition for the finite-difference stencils, restriction, and interpolation as well as PAW integration operations involves communication with the nearest neighbor domains. A robust way that is compatible with all MPI libraries is to do the data transfers between the host and the device manually. This means that we move the data from the device memory to the main memory, then transfer the data using MPI, and then move the data from the main memory to the device memory in the destination node. On an individual GPU card, the sends in boundary exchange are done in order, one boundary region at a time. This is to ensure the correctness of results. The receives can happen in any order, but they have to be done for the previous boundary regions before we can send data from the current boundary. The MPI transfers are always done asynchronously. The memory copies between host and device are done either synchronously or asynchronously depending on the size of the boundary regions. With asynchronous transfers, we can overlap sends and receives but the individual transfers have a larger initial overhead.

On large grids we overlap computation with communications. This means that we perform stencil calculations in the middle part of the grid, and at the same time exchange boundary regions with neighboring nodes. We also use batching to combine several small transfers into a few large ones. We also support using CUDA-aware MPI implementations where all the transfers are handled by the MPI library.