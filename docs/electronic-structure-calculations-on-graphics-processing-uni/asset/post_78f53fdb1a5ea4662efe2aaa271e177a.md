
not saturate the hardware. Streams can be used to batch small, independent operations so as to fully utilize the hardware. This adds an additional tool for the scheduler to hide latency, which can help in maximizing instruction throughput and increasing parallel efficiency.

Batching is a method of bundling together operations to create one larger operation from two or more smaller operations. For example, if one has five matrices, each of size 5 x 5, finding the inverse of each matrix is an O(N^3) problem. This is in the microsecond timescale and will not provide enough work for a GPU to hide the start-up costs of invoking several smaller kernels and fetching data from memory. Batching all the independent, small matrix inverse operations into one larger matrix inverse maximizes GPU utilization so as to yield better performance.

The CUDA Programming Guide [1] and Best Practices Guide [7] are excellent resources for discovering programming and optimization conventions that will improve the performance of a GPU application. The extent by which performance is improved when applying any of the above techniques or concepts is application-dependent. It is worth measuring the performance of a GPU application/kernel in order to deduce the limiting factor, that is, bandwidth-bound or compute-bound. An optimization used to improve memory throughput, for example, moving data to on-chip shared memory, may not service a compute-bound application and can waste time in much programming effort for little performance reward. Tools such as the CUDA Profiler [8] can assist in identifying the bottlenecks in a code and should be used alongside metrics such as theoretical bandwidth and speedup to assess the efficiency of a GPU implementation.

## 2.5 Software Libraries for GPUs

As general-purpose GPU technology matures, an increasing number of GPU-accelerated software libraries and functions are becoming available to the programmer. These are already an optimization to benefit from GPU acceleration by calling functions in the libraries that have already been optimized for the target architecture, reducing the effort for the programmer. Scientific codes that already make use of libraries such as BLAS [9–11] and LAPACK [12] for linear algebra can easily call a GPU-accelerated version of a routine by linking to the accelerated library and modifying the arguments as required. There are dozens of GPU-accelerated libraries available at https://developer.nvidia.com/gpu-accelerated-libraries. Some of the more useful libraries for computational chemistry applications are the following:

- cuBLAS [13] – a completely accelerated, freely available version of the Basic Linear Algebra Subroutines (BLAS) library offering very high performance on Nvidia GPUs. The Nvidia CUDA BLAS library (cuBLAS) supports all data types, that is, single precision, double precision, complex, and double complex, concurrent streams, multiple GPUs, and batching of some operations such as matrix-matrix multiplications. cuBLAS offers batch mode, which enables a programmer to specify that the solutions to multiple small independent matrix operations be provided simultaneously.
- cuFFT [14] – Fast Fourier transforms are frequently used in many scientific applications and are a means of converting a function from real (time) to reciprocal space (frequency) and vice versa. The Nvidia CUDA Fast Fourier Transform library (cuFFT) offers freely available, GPU-accelerated FFT functions capable of performing up to 10x faster through the use of a divide-and-conquer decomposition strategy.
- cuSPARSE [15] – The NVIDIA CUDA Sparse Matrix library (cuSPARSE) offers freely available, GPU-accelerated, sparse matrix, basic linear algebra subroutines capable of improving performance significantly as compared to popular CPU based implementations.
- CULA [16] – CULA is a CUDA-enabled GPU-accelerated linear algebra software library that is distributed as CULA Basic, CULA Premium, or CULA Commercial. Each distribution offers different levels of functionality, features, and support at varying prices starting at free for CULA Basic (limited to single-precision data types). The programmer can choose between using a lower level version of a specific function, offering more control to the programmer at the price of higher programming effort, or a higher level version, whereby the function call takes care of all of the GPU management behind the scenes.
- MAGMA [17] – an open source software library from the developers of LAPACK and ScaLAPACK offering GPU-accelerated linear algebra routines for heterogeneous systems. It is capable of multiple-precision arithmetic and supports hybrid many-/multi-core CPUs and multiple Intel Xeon Phi accelerator cards or GPUs. This library interfaces to current LAPACK and BLAS packages and standards for ease of programming.

## 2.6 Special Features of CUDA-Enabled GPUs

GPU technology is still an emerging field in the world of HPC with a steep growth curve, the benefit of which is fast-paced innovation and improvement of features. Some of the more recent GPU features available at the time of writing are Hyper-Q technology, Multi-Process Service (MPS), Unified Memory, and NVLink.

### 2.6.1 Hyper-Q

Hyper-Q technology allows kernels to be launched on a single GPU from multiple CPU processes at any one time by increasing the number of “connections” to a GPU from 1 (compute capability 2.x and lower) to 32 (compute capability 3.x and above). This feature is designed to enhance the performance of CUDA streams and enable the use of multiple MPI processes. Programs that use streams can often be limited by something called false sharing. False sharing is where the scheduler underestimates the number of independent instructions able to be executed concurrently as a consequence of multiple independent streams being queued into a single pipeline. The multiple “connections” of Hyper-Q aid in reducing the false sharing behavior by allowing streams to remain in separate pipelines so that the scheduler is more likely to recognize independent instructions for concurrent execution.

### 2.6.2 MPS

MPS is a client-server runtime implementation of the CUDA API, which enables multiple MPI processes to execute kernels and carry out data transfers on a single GPU through the use of Hyper-Q technology. The server

- Enables multiple MPI processes to launch kernels on a GPU, reducing idle hardware.
- Reduces storage and scheduling resource usage by allocating a single copy of data on a GPU accessible to all MPI processes.
- Extends the lifetime of scheduling resources of a single MPI process to eliminate the overhead of swapping resources every time a new MPI process is scheduled.

### 2.6.3 Unified Memory

Unified memory is a feature of CUDA 6, which eliminates the need to explicitly allocate data on a GPU and transfer it between the CPU and GPU. A single pointer can be used by the CPU and the GPU to address shared data, as the hardware carries out all the data migration behind the scenes, making GPU programming much simpler, as separate GPU data arrays do not need to be created. This is done through a pool of managed memory shared by a CPU and GPU (Figure 2.7).

### Unified memory

![](img/255d48531d66773aa863436a333dac7d_65_0.png)

Figure 2.7 Visual representation of unified memory. Host and device memory is presented as a single address space. This makes programming easier, but since memory copies still happen behind the scenes, performance can be lower compared to explicitly managed memory. Picture adaptation courtesy of Nvidia Corporation

Unified memory removes some of the complexity from programming and can be as quick as local data accesses on a GPU. It is worth noting, however, that the use of asynchronous memory copies and programming at a lower level is more than likely faster than using unified memory. Unified memory is designed to open up GPU programming to a wider audience by simplifying code development.

### 2.6.4 NVLink

The final special feature to be discussed is NVLink, which is the first interconnect designed specifically for GPUs. At the time of writing, NVLink was not yet available, having been announced only in March 2014. NVLink promises a high-speed interconnect between CPU and GPU, allowing 5–12 times the bandwidth capabilities of the fastest interconnect currently on the market, and enables GPU-GPU connection, making data sharing between multiple GPUs faster and more efficient. One of the largest bottlenecks in a GPU application is the rate at which data can be transferred between the host and the device. This advancement in GPU technology will hopefully reduce the data transfer bottleneck and thus improve data throughput.

## References

- 1. NVIDIA (2014) CUDA C Programming Guide 2007–2014. Available from: http://docs.nvidia.com/cuda/cuda-c-programming-guide (accessed 01 September 2015).
- 2. NVIDIA (2014) CUDA Runtime API: API Reference Manual 2014. Available from: http://docs.nvidia.com/cuda/pdf/CUDA_Runtime_API.pdf (accessed 01 September 2015).
- 3. Khronos (2014) The OpenCL Specification 2014. Available from: https://www.khronos.org/registry/cl/ (accessed 01 September 2015).
- 4. OpenACC (2014) The OpenACC Application Programming Interface 2013. Available from: http://www.openacc.org/sites/default/files/OpenACC.2.0a_1.pdf (accessed 01 September 2015).
