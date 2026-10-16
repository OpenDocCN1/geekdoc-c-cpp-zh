# 13.4 MATRIX PROCESSING

A two-dimensional numeric array having m rows and n columns is called an m × n matrix. Matrices arise naturally in many problems in engineering and applied mathematics. In this section we describe some of the basic matrix operations that are useful in these applications.

# 13.4.1 Matrix Operations

Several matrix operations such as addition and subtraction are defined elementwise; that is, two matrices of the same shape are added by adding corresponding elements and are subtracted by subtracting corresponding elements. More precisely, the sum of two matrices that have the same number of rows and the same number of columns is defined as follows: If A_ij and B_ij are the entries in the i-th row and j-th column of m × n matrices A and B, respectively, then A_ij + B_ij is the entry in the i-th row and j-th column of the sum A + B, which will also be an m × n matrix. Similarly, the difference A − B is the m × n matrix in which A_ij − B_ij is the entry in the i-th row and j-th column. For example, if

A = [ 1  3  2 ]
    [ -1 4  5 ] and B = [ 3  0  1 ]
                       [ 7  1  3 ]

then

A + B = [ 4  3  3 ]
         [ 6  5  8 ]

and

A − B = [ -2  3  1 ]
         [ -8  3  2 ]

Similarly, a matrix is multiplied by a scalar (number) elementwise. For example,

2A = [ 2  6  4 ]
      [ -2 8 10 ]

One important matrix operation that is not defined elementwise is matrix multiplication. Suppose that A is an m × n matrix and B is an n × p matrix. The product AB is the m × p matrix for which

The entry in row i and column j
= the sum of the products of the entries in row i of A with the entries in column j of B