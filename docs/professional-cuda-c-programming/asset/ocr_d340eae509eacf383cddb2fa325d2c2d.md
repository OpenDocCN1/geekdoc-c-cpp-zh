# CUDA: A Platform for Heterogeneous Computing

CUDA is a general-purpose parallel computing platform and programming model that leverages the parallel compute engine in NVIDIA GPUs to solve many complex computational problems in a more efficient way. Using CUDA, you can access the GPU for computation, as has been traditionally done on the CPU.

The CUDA platform is accessible through CUDA-accelerated libraries, compiler directives, application interfaces, and extensions to industry-standard programming languages, including C, C++, Fortran, and Python (as illustrated by Figure 1-12). This book focuses on CUDA C programming.

GPU Computing Applications

| CUFT CUBLAS CURAND CUSPARSE | CULA MAGMA | Thrust NPP | VSIPL SVM OpenCurrent | PhysX Opti | iray | MATLAB Mathematica |

Programming Languages

| C | C++ | Fortran | Python | DirectCompute | Direct (e.g. OpenACC) |

FIGURE 1-12

CUDA is an extension of standard ANSI C with a handful of language extensions to enable heterogeneous programming, and also straightforward APIs to manage devices, memory, and other tasks. CUDA is also a scalable programming model that enables programs to truly scale parallelism

CUDA is also a scalable programming model that enables programs to truly scale their parallelism to GPUs with varying numbers of cores, while maintaining a shallow learning curve for programmers familiar with the C programming language.

CUDA provides two API levels for managing the GPU device and organizing threads, as shown in Figure 1-13.

+   * CUDA Driver API
"* CUDA Runtime API"

The driver API is a low-level API and relatively hard to program, but it provides more control over how the GPU device is used. The runtime API is a higher-level API implemented on top of the