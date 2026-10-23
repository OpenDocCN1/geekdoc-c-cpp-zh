This system of equations is called the normal equation. Because Aᵗ A is always SPD, the Gauss–Seidel iteration applied to the normal equation always converges to x.

The Gauss–Seidel iteration applied to the normal equation is known as the Kaczmarz iteration [77]. Although this iteration always converges to the numerical solution x, the convergence may be extremely slow. The Kaczmarz iteration may be useful only when no other iterative method converges, such as for highly indefinite systems. For better-posed systems such as those arising from diffusion equations, more efficient iterative methods should be used.

# 17.7 Incomplete Factorization

In this section, we describe the incomplete LU (ILU) factorization of the sparse matrix A. This factorization is then used in the ILU iterative method for the numerical solution of the linear system Ax = f. The ILU iteration is usually considered much more efficient than the above relaxation methods in terms of convergence rate (that is, it usually requires fewer iterations to converge to x), particularly when it is accelerated by one of the acceleration techniques in Section 17.11 below. However, as we shall see, this is not always the case, and ILU may well be inferior to symmetric Gauss–Seidel for SPD examples.

As discussed in Chapter 2, Section 21, the decomposition (or factorization) of the matrix A as the product

A = LU,

where L is a lower triangular matrix with main-diagonal elements that are all equal to 1 and U is an upper triangular matrix, is computed in Gaussian elimination. This decomposition is then used to give the solution of the linear system as

x = A⁻¹ f = U⁻¹ L⁻¹ f.

Of course, U⁻¹ or L⁻¹ is never calculated explicitly. Instead, x can be calculated in two steps. First, the lower triangular system

L y = f

is solved for the unknown vector y (forward elimination in L). Then, the upper triangular system

U x = y

is solved for the unknown vector x (back substitution in U). This direct method gives the desired numerical solution x.

As discussed in Section 17.1, the direct method for finding x is impractical for large sparse linear systems because of the large amount of fill-in produced in Gaussian elimination. In other words, the L and U factors are no longer sparse and have to be stored as expensive dense matrices. The ILU factorization attempts to avoid this problem by producing approximate L and U matrices (incomplete factors), in which elements that are too small in some sense are dropped [49], [30]. These inexact factors are now used to form the preconditioner

𝒫 = LU.

The iteration that uses this preconditioner is called the ILU iteration.