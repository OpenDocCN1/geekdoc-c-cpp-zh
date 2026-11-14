# # GPU-Accelerated Sparse Matrix–Matrix Multiplication for Linear Scaling Density Functional Theory

Ole Schütt¹, Peter Messmer²,³, Jürg Hutter⁴ and Joost VandeVondele¹

¹Department of Materials, ETH Zürich, Zürich, Switzerland
²NVIDIA, Zürich, Switzerland
³NVIDIA Co-Design Lab for Hybrid Multicore Computing, Zürich, Switzerland
⁴Institute of Physical Chemistry, University of Zürich, Zürich, Switzerland

This chapter discusses how GPUs can be exploited to accelerate sparse matrix–matrix multiplications as required to solve the self-consistent field equations in linear scaling density functional theory calculations. We present the DBCSR sparse matrix multiplication library and describe the algorithms that are used to achieve maximum performance on distributed multicore and hybrid CPU/GPU architectures. Our numerical results demonstrate the efficiency of this linear scaling GPU-based implementation on supercomputers for very large simulations. This paves the way for scientific applications based on three-dimensional models consisting of 10.000 atoms or more.

# ## 8.1 Introduction

# ### 8.1.1 Linear Scaling Self-Consistent Field

With the steady increase in computer power available, larger and larger systems are simulated using electronic structure methods. These large simulations expose the asymptotic scaling of the traditional algorithms used in electronic structure calculations. Many of the traditional algorithms have a cubic or higher scaling with system size, effectively blocking the path to very large scale simulations.