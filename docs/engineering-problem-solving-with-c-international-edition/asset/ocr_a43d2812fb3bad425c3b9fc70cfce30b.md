# Matrix Addition and Subtraction

The addition (or subtraction) of two matrices is performed by adding (or subtracting) the elements in corresponding positions in the matrices. Therefore, matrices that are added (or subtracted) must be the same size; the result of the operation is another matrix of the same size.

Consider the following matrices:

```
A = [2 5 1; 0 3 -1], B = [1 0 2; -1 4 -2]
```

Several matrix sums and differences follow:

```
A + B = [-3 5 3; 1 7 -3], A - B = [1 5 -1; 1 -1 1],
B - A = [-1 -5 1; -1 1 -1]
```

# Matrix Multiplication

Matrix multiplication

Matrix multiplication is not computed by multiplying corresponding elements of the two matrices. The value in position $c_{i,j}$ of the product C of two matrices A and B is the dot product of row $i$ of the first matrix and column $j$ of the second matrix, as shown in this summation equation:

```
c_{i,j} = \sum_{k=1}^{n} a_{i,k} b_{k,j}
```

Since the dot product requires that the vectors have the same number of elements, the first matrix (A) must have the same number of elements in each row as the second matrix (B) has in each column. Thus, if A and B both have five rows and five columns, their product has five rows and five columns. Furthermore, for these matrices, we can compute both AB and BA, but, in general, they will not be equal.

If A has two rows and three columns, and B has three rows and three columns, the product AB will have two rows and three columns. To illustrate, consider the following matrices:

```
A = [2 5 1; 0 3 -1], B = [1 0 2; -1 4 -2; 5 2 1]
```

The first element in the product C = AB is

```
C_{1,1} = \sum_{k=1}^{3} a_{1,k} b_{k,1}
= a_{1,1}b_{1,1} + a_{1,2}b_{2,1} + a_{1,3}b_{3,1}
= 2 \cdot 1 + 5 \cdot (-1) + 1 \cdot 5
= 2.
```