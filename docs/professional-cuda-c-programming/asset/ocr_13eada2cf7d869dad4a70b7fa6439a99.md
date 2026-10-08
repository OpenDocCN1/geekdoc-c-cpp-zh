There are many advantages to using CUDA libraries, compared to building your own hand-coded CUDA implementation or using legacy host-only libraries. For many applications, CUDA libraries offer the best balance of usability and performance. The APIs of many CUDA libraries are easily similar to those in a standard library in the same domain. As a result, you can use CUDA libraries in the same fashion as the host-based versions, and realize speedup with minimal programming effort. The time required to port complex algorithms to CPUs can be reduced from months or weeks to days or hours.

Performance is a key advantage that CUDA libraries have over host-only libraries, and often hand-coded CUDA implementations as well. CUDA library developers are learning to take advantage of their expertise to accelerate new and legacy applications.

CUDA libraries also incur low maintenance overhead for software. By reusing existing and mature implementations, the burden of testing and managing these complex algorithms in CUDA is delegated. These libraries are rigorously tested and managed by NVIDIA and its partners, removing those tasks from the responsibility of a domain expert or CUDA programmer.

Still, there are generally additional steps required to add CUDA libraries to a legacy application, and further optimizations are possible for performance improvement relative to standard host libraries. Please note, there are reference guides freely available online through the NVIDIA Developer Zone. This chapter does not focus on the use of each individual function but higher-level use and optimization of applications. The examples in this section use CUDA libraries based on case studies of particular libraries.

# # Supported Domains for CUDA Libraries

As the writing of this book, there are 19 GPU-accelerated documents and available for download from the NVIDIA Developer Zone. For an up-to-date list, please visit the NVIDIA Developer Zone at developer.nvidia.com. A current list and the domain to which they apply are included in Table 8-1.

TABLE 8-1: A Collection of Supported CUDA Library Domains

| LIBRARY NAME | DOMAIN |
|---|---|
| NVIDIA cuFFT | Fast Fourier Transforms |
| cuBLAS | Linear Algebra (BLAS Library) |
| CULA Tools | Linear Algebra |
| MAGMA | Next generation Linear Algebra |
| IMSL Fortran Numerical Library | Mathematics and Statistics |
| NVIDIA cuSPARSE | Sparse Linear Algebra |
| NVIDIA CUSP | Sparse Linear Algebra and Graph Computations |

continues