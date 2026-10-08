
you may need to manipulate the library handle. In still other cases, you may need to manage separate-rate metadata objects.

## Stage 6: Executing

Executing the actual library call is the simplest step! You call the desired library function with the properly configured functions from Stages 1 through 5 and reap the performance benefits of a highly-optimized CUDA library function.

## Stage 7: Retrieving Results from Device Memory

For this step, you retrieve the output from device memory into host memory in a pre-determined format (like configured as Stage 5 or prescribed by the library). You can think of this as the mirror of Stage 4.

## Stage 8: Converting Back to Native Format

In the case that an application's native data format is different from the formats supported by the CUDA library use, you will need to convert back to the application-specific format. You can think of this step as a mirror of Stage 3.

## Stage 9: Releasing CUDA Resources

If the resources allocated by this workflow are no longer necessary, you can release them for use in future computation. Note, there is some overhead in allocating and releasing resources, so it is better to reuse resources across multiple applications of CUDA library when possible. Examples of resources include device memory, library handles, and CUDA streams.

## Stage 10: Continuing with the Application

After you retrieve the output from Stage 7 and (optionally) convert to the application's native representation in Stage 8, you can now continue with any future processing as the prior computation had not been run on the GPU.

Note, these stages are verbose and leave the impression that the conceptual and development overhead for CUDA libraries is high. As subsequent sections will demonstrate, this is far from the truth. In many cases, the entire workflow requires only a few lines of code. These details are provided to help you draw analogies from past knowledge to improve your understanding, and to add insight to the underlying processes.

In the next sections, you will explore in-depth the most commonly used CUDA libraries. For each library you will learn related concepts, review an example, and understand the workflow stages.

## THE CUSPARSE LIBRARY

The cuSPARSE library implements a wide range of general-purpose sparse linear algebra functions. It supports a collection of dense and sparse data formats on which these functions operate.

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

A dense matrix contains primarily non-zero values. When representing dense matrices every value in the matrix is stored in a multi-dimensional array. In contrast, sparse matrices and vectors consist primarily of zero-valued entries and can be more compactly represented by storing only the non-zero values and their coordinates rather than many redundant zero values. There are many ways of representing sparse matrices, eight of which are currently supported by cuSPARSE. This section briefly covers three of the most common storage formats supported for matrices in cuSPARSE.

# Dense

The dense matrix format is the one widely known. This format stores the value for every cell in a matrix regardless of whether it is zero or non-zero. These matrices are stored in memory, memory is inherently one-dimensional, the cells of a dense matrix must be “flattened” and mapped to consecutive, one-dimensional memory addresses. An example mapping from a two-dimensional matrix M to its flattened, dense format T is shown in Figure 8-2.

![](img/506ba3a4c9f4512233692f3f20de1f3a_361_0.png)

# Coordinate (COO)

For each non-zero value in a sparse matrix, the coordinate (COO) sparse matrix format stores the non-zero value with both its row index and column index. When referencing a given row and column in a sparse matrix stored in COO format, the value is found by matching the target location among stored row and column indices. If no match is found, the value must be zero.

The point at which a coordinate-formatted matrix consumes less space than a dense matrix depends on the sparsity of the matrix, the size of the values, and the size of the type used to store their coordinates. For example, given a sparse matrix storing 32-bit floating-point values and a coordinate format that uses 32-bit integers to represent matrix coordinates, space savings are achieved when less than one third of the cells in the matrix contain non-zero values. In this particular coordinate format requires triple the space of storing only the value which is true for storing a non-zero entry in a dense format. An example mapping from a two-dimensional matrix M to its coordinate representation T is shown in Figure 8-3.

![](img/506ba3a4c9f4512233692f3f20de1f3a_361_1.png)

# Compressed Sparse Row (CSR)

Compressed sparse row format (CSR) is similar to coordinate format. The only change is in how the row index for each non-zero value is stored. non-zero value that indicated the row index for that value. Rather than storing the row index for each value explicitly, CSR instead stores an offset to where all of the values belonging to the same row are stored in the value and column arrays.

For example, suppose the non-zero lengths of a sparse matrix $M$ are stored in array $V$ and the column indices for those values are stored in array $C$, as shown in Figure 8-4. This formatting is identical to Coordinate but without the row indices.

![](img/506ba3a4c9f4512233692f3f20de1f3a_362_0.png)

Since all values in the same row are stored adjacent to each other in $V$, finding the values of a row simply requires an offset and length in the $V$ array. For example, if you wanted to know only the non-zero values stored in the third row of $M$, those values could be defined as starting at offset 2 and length 2 in $V$, as shown in Figure 8-5. This is how row indices are stored in CSR format.

![](img/506ba3a4c9f4512233692f3f20de1f3a_362_1.png)

Using that offset and length in the $C$ column array would define the column indices of those values are stored at, and therefore it would be possible to fully define each value's location in the original sparse matrix $M$. When storing large matrices with many elements, representing each row with a simple offset and a length is much more efficient than storing a row index for every value.

Now, how are offsets and lengths stored for each row? The simplest would be to create arrays $R_o$ and $R_l$, each with length $nrows$, and store the offsets of every value in $R_o$ and the lengths in $R_l$. However, if a matrix has many rows this requires two arrays. Instead, it is possible to use a single array $R$ with length $nrows+1$ where the offset of row $i$ in $V$ and $C$ is stored at index $i$ in $R$. The length of row $i$ can be derived from the difference between the offset of row $i$ and $i+1$ in $R$. Essentially, the value at $R[i+1]$ is the total number of non-zero values stored in row $0, 1, \dots$, and $R[nrows]$ is the total number of non-zero values in $M$. Applying these conventions to the matrix $M$ results in the $R$ shown in Figure 8-6.

![](img/506ba3a4c9f4512233692f3f20de1f3a_362_2.png)
