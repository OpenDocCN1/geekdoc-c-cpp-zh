# 5.10 Matrices and Vectors*

A matrix is a set of numbers arranged in a rectangular grid with rows and columns. Consider a matrix with four rows and three columns; the size of this matrix is also specified as 4 × 3, as shown:

```
A = [ -1  0  0 ]
    [  1  1  0 ]
    [  1 -2  3 ]
    [  0  2  1 ]
```

Note that the values within a matrix are written within large brackets. A matrix with one row is called a **row vector**, and a matrix with one column is called a **column vector**. The term **vector** by itself does not distinguish between a row vector and a column vector.

In mathematical notation, matrices are usually given names with uppercase boldface letters. To refer to individual elements in the matrix, the row and column number are used, with both the row and column numbers starting with the value 1. In formal mathematical notation, the uppercase name refers to the entire matrix, and the lowercase name with subscripts refers to a specific element. Thus, by using the matrix A, the value of a32 is -2. If a matrix has the same number of rows and columns, it is a **square matrix**.

A two-dimensional array can be used to store a matrix, but we must be careful translating equations in matrix notation into C statements because of the difference in subscripting. Matrix notation assumes that the row and column numbers begin with the value 1, whereas C statements assume that the row and column numbers of a two-dimensional array begin with the value 0. Although a vector could be stored as a two-dimensional array with either one row or one column, vectors are more commonly stored as one-dimensional arrays; thus, they do not usually make the distinction of a row vector or a column vector.

Matrix operations are frequently used in engineering problem solutions, so we now present common operations with matrices and vectors. We will include C statements for performing some of the operations; the problems at the end of the chapter relate to developing C statements for the remaining operations.

# Dot product

The **dot product** is a number computed from two vectors of the same size. This value is the sum of the products of the values in corresponding positions in the vectors, as shown in this summation equation, which assumes that there are n elements in the vectors **A** and **B**:

```
Dot product = A · B = \sum_{k=1}^{n} a_k b_k.
```

To illustrate, assume that A and B are the following vectors:

```
A = [4 -1 3]   B = [-2 5 2].
```

The dot product is then

```
A · B = 4 · (-2) + (-1) · 5 + 3 · 2
= (-8) + (-5) + 6
= -7.
```

The dot product is also called an **inner product**.

*Optional section.