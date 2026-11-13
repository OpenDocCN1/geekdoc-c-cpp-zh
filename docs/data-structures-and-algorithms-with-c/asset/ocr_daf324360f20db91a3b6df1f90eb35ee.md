Consider the following polynomials:
10x^3 + 15x^2 - 7x^2 - x
Here (10, 15, -7, -1) are coefficients and (5, 3, 2, 1) are exponents.

# Representation of Polynomials using Array

All the terms of a polynomial can be represented using array in two different ways:

+   i) Linear array representation
+   ii) Array of structure representation

# Linear array representation

In this representation, the exponent/degree of a term can be treated as an index of the linear array and the coefficient of the term stored in that index of the array.

For Example, polynomial 10x^3 + 15x^3 - 7x^2 - x can be represented as follows:

| [0] | [1] | [2] | [3] | [4] | [5] |
|---|---|---|---|---|---|
| 0 | -1 | -7 | 15 | 0 | 10 |

Figure 3.9: Polynomial representation using linear array

The drawback of this representation is most of the entries of the linear array may be remains zero for higher order polynomials.

# Array of Structure representation

In this representation, each term defined as structure variable to store degree and coefficient of the corresponding term and polynomial can be represented by an array of structures as follows:

```
typedef struct poly
{
    int deg;
    int coef;
}poly;
poly term[100];
```

Now, if we represent the polynomials using an array, then we have to define the size of the array in advance. Therefore, there is a possibility of wastage of computer memory. However, this representation is simple enough.

The polynomial can also be represented by using linked list. We have discussed polynomial representation using a linked list in Chapter 5 in this book.

# SPARSE MATRIX

One of the most important developments in scientific computing is a sparse matrix. This includes the data structures to represent the matrices, the techniques for manipulating them, the algorithms used and efficient mapping of the data structures and algorithms for high performance.

_Definition_: A matrix is said to be Sparse Matrix if most of its elements are zero (near more than 2/3 elements are zero), having a relatively small number of non-zero elements. A matrix that is not sparse is called Dense Matrix.

A sparse matrix is a two-dimensional array in which most of the elements have a null value or zero. However, for sparse matrices, this invokes wastage of a lot of memory space.