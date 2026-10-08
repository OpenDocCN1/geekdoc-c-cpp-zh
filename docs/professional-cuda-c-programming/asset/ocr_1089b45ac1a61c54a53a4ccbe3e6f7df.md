TABLE 8-1 (continued)
| LIBRARY NAME | DOMAIN |
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

# # A Common Library Workflow

Many CUDA libraries share concepts, features, and a common workflow when being called from a host application. A common workflow when using NVIDIA libraries is follows:

+   1. Create a library-specific handle that manages contextual information useful for the library’s operation.
2. Allocate memory for inputs and outputs to the library function.
3. If inputs are not already in a library-supported format, convert them to be accessible by the library.
4. Populate the pre-allocated memory with inputs in a supported format.
5. Configure the library computation to be executed.
6. Execute a library call that offloads the desired computation to the GPU.
7. Retrieve the results of computation from device memory, possibly in a library-determined format.
8. If necessary, convert the retrieved data to the application’s native format.
9. Release CUDA resources.
10. Continue with the remainder of the application.

Not every library follows this workflow, and even the ones that might skip certain steps. Still it is important for you to be aware of the behind-the-scenes events at each stage this