Table 8-2 summarizes the set of linear algebra operations supported by cuSPARSE. For more detailed information on any of the following functions, refer to the cuSPARSE User Guide. Note that cuSPARSE separates functions into levels. All Level 1 functions operate exclusively on dense and sparse vectors. All Level 2 functions operate on sparse matrices and dense vectors. All Level 3 functions operate on sparse matrices and dense matrices.

# TABLE 8-2: Sparse Linear Algebra Operations Supported by cuSPARSE

| FUNCTION NAME | DESCRIPTION |
| --- | --- |
| Level 1 Functions | |
| axpy | y = y + ax |
| doti | z = yᵀx |
| dotci | z = yᵀx |
| gthr | Gathers a set of values from a vector y into a vector x based on indices stored in a third vector z |
| ghrz | Performs the same operation as gthr, but zeroes the locations read from in y |
| roti | Applies the Givens rotation to x and y |
| sctr | Scatters selected elements from a vector x into a vector y based on the indices stored in a third vector z |
| Level 2 Functions | |
| mv | At most basic, mv performs the calculation y = aAx + by, though more advanced options provide for additional manipulations |
| sv | Solves a sparse triangular linear system |
| Level 3 Functions | |
| mm | C = aAB + bC |
| sm | Solves a sparse triangular linear system |

In the descriptions of each sparse linear algebra operation, lowercase letters represent vectors, uppercase letters represent matrices, and italicized lowercase letters indicate scalars.

In the next section you will learn about the data formats supported by cuSPARSE, including format conversion.

# cuSPARSE Data Storage Formats

A dense matrix contains primarily non-zero values. When representing dense matrices every value in the matrix is stored in a multi-dimensional array. In contrast, sparse matrices and vectors consist primarily of zero-valued entries and can be more compactly represented by storing only