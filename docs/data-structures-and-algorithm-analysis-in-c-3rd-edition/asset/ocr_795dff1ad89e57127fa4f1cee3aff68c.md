Our next example of reduction concerns the multiplication of two n × n matrices. For this problem, we will assume that the values stored in the matrices are simple integers and that multiplying two simple integers takes constant time (because multiplication of two int variables takes a fixed number of machine instructions). The standard algorithm for multiplying two matrices is to multiply each element of the first matrix’s first row by the corresponding element of the second matrix’s first column, then adding the numbers. This takes Θ(n) time. Each of the n² elements of the solution are computed in similar fashion, requiring a total of Θ(n³) time. Faster algorithms are known (see the discussion of Strassen’s Algorithm in Section 16.3.3), but none are so fast as to be in O(n²).

Now, consider the case of multiplying two symmetric matrices. A symmetric matrix is one in which entry ij is equal to entry ji; that is, the upper-right triangle of the matrix is a mirror image of the lower-left triangle. Is there something about this restricted case that allows us to multiply two symmetric matrices faster than in the general case? The answer is no, as can be seen by the following reduction. Assume that we have been given two n × n matrices A and B. We can construct a 2n × 2n symmetric matrix from an arbitrary matrix A as follows:

[ 0  A ]
[ Aᵀ 0 ]

Here 0 stands for an n × n matrix composed of zero values, A is the original matrix, and Aᵀ stands for the transpose of matrix A.¹ Note that the resulting matrix is now symmetric. We can convert matrix B to a symmetric matrix in a similar manner. If symmetric matrices could be multiplied “quickly” (in particular, if they could be multiplied together in Θ(n²) time), then we could find the result of multiplying two arbitrary n × n matrices in Θ(n²) time by taking advantage of the following observation:

[ 0  A ][ 0  Bᵀ ] = [ AB  0 ]
[ Aᵀ 0 ][ B  0 ]   [ 0  AᵀBᵀ ]

In the above formula, AB is the result of multiplying matrices A and B together.

# 17.2 Hard Problems

There are several ways that a problem could be considered hard. For example, we might have trouble understanding the definition of the problem itself. At the beginning of a large data collection and analysis project, developers and their clients might have only a hazy notion of what their goals actually are, and need to work that out over time. For other types of problems, we might have trouble finding or understanding an algorithm to solve the problem. Understanding spoken English