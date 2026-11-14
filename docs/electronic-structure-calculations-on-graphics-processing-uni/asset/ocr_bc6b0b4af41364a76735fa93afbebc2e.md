The derivatives of the $Q_{ij}$ are computed similarly using its Fourier transform $Q_{ij}(g)$. The last terms are the projections $\langle u_{n\mathbf{k}} | \beta \rangle$ and their derivatives:

\(\left\langle u_{n\mathbf{k}} \left| \frac{\partial \beta_i}{\partial \mathbf{R}_u^\alpha} \right| \right\rangle = \sum_g i g(\beta_i | g) \langle u_{n\mathbf{k}} \rangle.\) (7.47)

Evaluating the derivative terms can be done using the same strategies as those used to compute the projection in Section 7.3.1. Real-space projection will require the Fourier transformation of \(g(\beta|\beta')\) back to real space, but this needs to be computed only once for the entire calculation.

# 7.4 Optimizations

Two key issues in developing high-performance implementations for heterogeneous architectures are

+   1. maximizing the occupancy of the GPU, and
+   2. minimizing the high cost of transferring data between the GPU and CPU node(s).

The first issue boils down to expressing enough parallelism to feed the tens of thousands of GPU threads. The second issue is addressed by keeping data resident on the GPU for as long as possible. This can mean porting many intermediate, non-performance-critical methods to the GPU and carefully choosing and designing low-communication algorithms.

# 7.4.1 GPU Optimization Techniques

As explained in Chapters 1 and 2, the GPU is a massively parallel architecture capable of running several tens of thousands of threads concurrently. In order to use the GPU to its full potential, we need to execute computations as large enough tasks so that every thread has work to do.

Nearly every step in PWDFT involves a loop over bands. The easiest way to generate large, GPU-ready tasks is to group bands together and express computations on those larger groups. We call those groups blocks and this technique blocking. The example kernels given in Section 7.3 all block over a single band index, seen by loops of size nband. Blocking can be especially effective when the constituent calculations share data. For example, the action of the kinetic energy is an element-wise multiplication by the same \(|g + k|^2\) vector for every band. Sharing this data allows the application to read fewer memory and hence have higher arithmetic intensity and higher performance.

Sometimes, blocking over a single index, such as bands, is not enough. This could be because the number of available bands is small or the amount of work per band is small. The projection is a good example of the latter: the number of arithmetic operations per ion per band is 100 and does not scale with the problem size. In order to fully occupy the GPU, multiple ions must be processed concurrently as well.

Each ion requires a different scatter/gather of the band data, so parallelizing is not as simple as adding a band index. The next solution would be to use streaming to concurrently execute multiple kernels, with each kernel working on a single ion. The newest Nvidia GPUs (Kepler at the time of writing) support up to 32 concurrent kernels executing on a device, so this can be an effective source of added parallelism. Kernels issued in the same stream have implicit first-in-first-out (FIFO) dependency ordering, but the ordering between kernels in different streams needs to be enforced through the use of explicit synchronization. In this case, the data dependency is intra-ion, so each ion is assigned to a stream. If starting from unstreamed code, adding streams often requires the expansion of temporary buffers to handle more data in-flight.

GPU kernel launches are not free, and if launching the kernel to the GPU takes more time than the duration of the kernel, streams will offer no acceleration. More generally, the kernel launch latency cuts into stream performance if each streamed kernel is not long-lived. The amount of work per ion