define a set of basic operations that is rich enough to allow us to model high-level algorithms on the one hand and simple enough to allow optimisation on a range of computers on the other hand.

The advantages of using BLAS are its robustness, portability and readability. The BLAS functionality consists of three levels that we now discuss.

# 10.8.3  BLAS Level 1

This level consists of low-level operations such as *inner products* (also known as *dot products*) of vectors and the addition of a multiple of one vector to another vector. These *vector–vector operations* are referred to as Level 1 BLAS, such as:

$y \leftarrow \alpha x + y$  (10.1)

where $x$ and $y$ are vectors and $\alpha$ is a scalar.

These operations involve $O(n)$ floating-point operations in general, where $n$ is the length of the vectors. In equation (10.1) we see that the vector $y$ is being updated and the operation is sometimes called *saxpy* (‘scalar ax plus y’).

# 10.8.4  BLAS Level 2

This level contains matrix–vector operations of the form:

$y \leftarrow \alpha Ax + \beta y$  (10.2)

where $x$ and $y$ are vectors, $A$ is a matrix, $\alpha$ and $\beta$ are scalars.

These *matrix–vector operations* occur during the implementation of many of the most common algorithms in linear algebra. The Level 2 BLAS involve $O(mn)$ scalar operations where $m$ and $n$ are the dimensions of the matrix involved in the operations.

Other operations in BLAS Level 2 are:

+   - Rank-one and rank-two updates:
+   
+     $A = \alpha xy^T + A$ (rank 1 update)
+   
+     $A = \alpha xy^T + \alpha yx^T + A$ (rank 2 update)  (10.3)

where $y^T$ is the transpose of vector $y$.

+   - Solution of triangular equations of the form:
+   
+     $Ty = x$  (10.4)

where $T$ is a non-singular *upper-triangular matrix* (all elements below the main diagonal are zero) or *lower-triangular matrix* (all elements above the main diagonal are zero).