
APIs with standardized data formats to facilitate their ability to plug in existing applications (pluggability). CUDA libraries sit on top of the CUDA runtime, providing a simple, familiar, and domain-specific interface for both host applications and third-party libraries (depicted in Figure 8-1).

![](img/506ba3a4c9f4512233692f3f20de1f3a_355_0.png)

FIGURE 8-1

Another tool that provides a layer of abstraction over CUDA is OpenACC. OpenACC uses compilers to annotate regions of code and data for offload from the host to an accelerator device. The compiler arranges those regions to be executed on the device by auto-generating necessary memory copies, kernel launches, and other CUDA API calls. OpenACC will look familiar to you: its usage is similar to that of OpenMP, the directive-based hosting model described in Chapter 6. OpenACC can be integrated with CUDA libraries and hand-coded CUDA kernels. It allows programmers to implement their own kernel code, but dissociates many of the more mundane CUDA programming tasks.

The sections and examples that follow your existing knowledge of CUDA, to help you understand these tools and how to integrate them into your applications. You will start learning about the CUDA libraries listed below, and explore more on OpenACC.

- cuSPARSE includes a range of general-purpose sparse linear algebra routines.
- cuBLAS includes CUDA ports of all functions in the standard Basic Linear Algebra Subprograms (BLAS) library for Levels 1, 2, and 3.
- cuFFT includes methods for performing fast Fourier transforms (FFTs) and their inverse.
- cuRAND includes methods for random number generation using the GPU.

# INTRODUCING THE CUDA LIBRARIES

CUDA libraries are no different than system libraries or user-built libraries. They are a collection of function definitions whose signatures are exposed through header files. The CUDA libraries are special in that all computation implemented in the library is accelerated using a GPU, as opposed to a CPU.

There are many advantages to using CUDA libraries, compared to building your own hand-coded CUDA implementation or using legacy host-only libraries. For many applications, CUDA libraries offer the best balance of usability and performance. The APIs of many CUDA libraries are easily similar to those in a standard library in the same domain. As a result, you can use CUDA libraries in the same fashion as the host-based versions, and realize speedup with minimal programming effort. The time required to port complex algorithms to CPUs can be reduced from months or weeks to days or hours.

Performance is a key advantage that CUDA libraries have over host-only libraries, and often hand-coded CUDA implementations as well. CUDA library developers are learning to take advantage of their expertise to accelerate new and legacy applications.

CUDA libraries also incur low maintenance overhead for software. By reusing existing and mature implementations, the burden of testing and managing these complex algorithms in CUDA is delegated. These libraries are rigorously tested and managed by NVIDIA and its partners, removing those tasks from the responsibility of a domain expert or CUDA programmer.

Still, there are generally additional steps required to add CUDA libraries to a legacy application, and further optimizations are possible for performance improvement relative to standard host libraries. Please note, there are reference guides freely available online through the NVIDIA Developer Zone. This chapter does not focus on the use of each individual function but higher-level use and optimization of applications. The examples in this section use CUDA libraries based on case studies of particular libraries.

# Supported Domains for CUDA Libraries

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

TABLE 8-1 (continued)
| LIBRARY NAME | DOMAIN |
|---|---|
| AccelerEyes ArrayFire | Mathematics, Signal and Image Processing, and Statistics |
| NVIDIA cuRAND | Random Number Generation |
| NVIDIA NPP | Image and Signal Processing |
| NVIDIA CUDA Math Library | Mathematics |
| Thrust | Parallel Algorithms and Data Structures |
| HiPLAR | Linear Algebra in R |
| Geometry Performance Primitives | Computational Geometry |
| Paralution | Sparse Iterative Methods |
| AmX | Core Solvers |

If your application fits any of these domains, it is strongly recommended that you explore the online documentation for the provided libraries.

# A Common Library Workflow

Many CUDA libraries share concepts, features, and a common workflow when being called from a host application. A common workflow when using NVIDIA libraries is follows:

1. Create a library-specific handle that manages contextual information useful for the library’s operation.
2. Allocate memory for inputs and outputs to the library function.
3. If inputs are not already in a library-supported format, convert them to be accessible by the library.
4. Populate the pre-allocated memory with inputs in a supported format.
5. Configure the library computation to be executed.
6. Execute a library call that offloads the desired computation to the GPU.
7. Retrieve the results of computation from device memory, possibly in a library-determined format.
8. If necessary, convert the retrieved data to the application’s native format.
9. Release CUDA resources.
10. Continue with the remainder of the application.

Not every library follows this workflow, and even the ones that might skip certain steps. Still it is important for you to be aware of the behind-the-scenes events at each stage this understanding may help you with performance tuning or simplify the debugging process. Each of the libraries covered in the subsequent sections of this chapter follow this workflow to some extent. The remainder of this section briefly covers each stage of the workflow, including any new concepts or vocabulary.

# Stage 1: Creating a Library Handle

CUDA libraries share the concept of a handle, which contains contextual library information as the format of data structures used, the devices used for computation, and other environmental data. For those library methods that accept a handle, you must allocate and initialize the handle before making any library calls. In general, you can think of the handle as an object on the host that contains information which each library function may access. For example, you might want all library operations to run in a particular CUDA stream. Although libraries use different function names, many offer a function that forces all library operations to occur in a certain stream (for example, cuSPARS uses cusSetStream, cuBLAS uses cublasSetStream, and cuFFT cuffStream). This stream information would be stored in the library handle. The handle provides a way for library information to be stored, but places the responsibility of managing concurrent access to the handle to the programmer.

# Stage 2: Allocating Device Memory

For the libraries covered in this section, device memory is either allocated by the programmer using cudaMalloc. Only multi-GPU libraries require the use of an API other than cudaMalloc to allocate device memory.

# Stage 3: Converting Inputs to a Library-Supported Format

If the format of your application's data is not supported by the CUDA library you are using, it must be reformatted. For instance, if an application uses 2D arrays in row-major order, but CUDA only accepts in column-major order, you will need to perform some transformations. For optimal performance, every effort should be made to avoid data transformations and to conform to CUDA data formats.

# Stage 4: Populating Device Memory with Inputs

Given the global memory allocated in Stage 2 and the properly formatted data from Stage 3, the next task in Stage 4 makes that data available to the library function on the CUDA device by transferring it to device memory. You can think of this as analogous to cudaMemcpy, in many cases a library-specific function is used. For instance, when transferring a vector from the host to the device in a cuBLAS-based application, cublasSetVector should be used. Internally, it uses properly ordered and strided calls cudaMemcpy (or some equivalent function) to transfer the input data to device memory.

# Stage 5: Configuring the Library

Often, the library being called must be aware of data formatting, dimensionality, or configurable parameters. In Stage 5, you manage this configuration process. In some cases, these configurables are simply parameters passed to a computational library function. In other cases,
