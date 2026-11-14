It allows for defining vectors, matrices, and higher-order tensors of customizable scalar types.

MTL4 is a template library from the author for vectors and a wide variety of matrices. In addition to standard linear-algebra operations, it provides the latest iterative linear solvers. The basic version is open source. GPU support is provided with CUDA. The Supercomputing edition can run on thousands of processors. MTL5 is under development and will use C++17 features heavily.11

HPR (pronounced “hyper”) are template libraries that provide High-Performance Reproducible computation. They are built on top of MTL and the Universal library and provide algorithmic implementations that leverage the rounding control provided by posit arithmetic to yield reproducible results regardless of the concurrency environment. Two key open-source libraries are HPR-BLAS [48] and HPR-Tensor [49] that provide reproducible basic linear algebra and tensor operators.

# 4.7.4 Ordinary Differential Equations

odeint by Karsten Ahnert and Mario Mulansky solves Ordinary Differential Equations (ODE) numerically. Thanks to its generic design, the library doesn't only work with a variety of standard containers but also cooperates with external libraries. Therefore, the underlying linear algebra can be performed with MKL, the CUDA library Thrust, MTL4, VexCL, and ViennaCL. The advanced techniques used in the library are explained by Mario Mulansky in Section 7.1.

# 4.7.5 Partial Differential Equations

The number of software packages for solving Partial Differential Equations (PDE) is enormous. Here, we only mention two of them which are in our opinion very broadly applicable and make good use of modern programming techniques:

FEniCS is a software collection for solving PDEs by the Finite Element Method (FEM). It provides a user API in Python and C++ in which the