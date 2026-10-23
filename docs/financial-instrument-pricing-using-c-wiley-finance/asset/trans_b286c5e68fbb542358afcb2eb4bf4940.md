
applications because *data races* can occur. These functions access and modify the internal state of objects. This is a general problem when we use random number generators with internal state that can be non-deterministically modified by threads.

## 26.8 CRYPTOGRAPHIC GENERATORS

In the interest of completeness, we give a brief overview of random generators that are used in *cryptography*. This is the study of techniques to ensure data security and secure communications in the presence of eavesdroppers and adversaries. To this end, we need to generate random numbers for key generation, SSL (*Secure Sockets Layer*) and challenge/response algorithms. We note that pseudo-random number generators are not suitable for cryptographic applications because the requirements for *statistical randomness* differ from those for *cryptographic randomness*. A sequence of numbers can be statistically random but cryptographically insecure if an attacker can predict the sequence of the generated numbers by understanding the algorithm and the random seed used. This means that data will not be secure. We need *cryptographic random numbers*. For a sequence of random numbers to be deemed *cryptographically secure* it must be computationally infeasible to regenerate the same sequence of random numbers. In the case of pseudo-random numbers all we need to know is the pseudo-random number generator and the seed. It is intuitively clear that it takes more time to create a cryptographically secure random number than a pseudo-random number. In the case of the C# language, for instance, it can be up to eight times slower.

## 26.9 MATRIX DECOMPOSITION METHODS

The generation of correlated and uncorrelated standard normal variates is important in several areas in finance, such as Monte Carlo option pricing and multidimensional diffusions (Kienitz and Wetterau, 2012). We introduce a number of algorithms that are used in these applications. The algorithms are concerned with operations on matrices whose elements are real valued or complex valued. This is a major area of research (Golub and van Loan, 1996) and we focus on a number of methods that are directly applicable in the current book.

We introduce some notation. The *Hermitian transpose* of a square matrix A of size n with complex elements (denoted by $A^H$) is the complex conjugate transpose of A, that is $A^H = \overline{A}^{T}$ or $(A^H)_{ij}=\overline{A}_{ji}$, $1 \leq i,j \leq n$, where in general $\overline{z}$ denotes the complex conjugate of the complex number z, that is $\overline{z}=x-iy$ where $z=x+iy$.

An example is:

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_838_0.png)

In other words, we mirror the corresponding elements on each side of the main diagonal and then we take the complex conjugate of each mirrored element. A special case is when the elements are real valued and we then speak of the *transpose* of a matrix. An example is:

$$A=\begin{pmatrix}1&0.9&0.7\\0.5&1&0.6\\2.0&-3.0&1\end{pmatrix}$$

$$A^{\mathsf T}=\begin{pmatrix}1&0.5&2.0\\0.9&1&-3.0\\0.7&0.6&1\end{pmatrix}.$$

This is called transposing the matrix.

A matrix $A$ is called *Hermitian* if it is equal to its own Hermitian transpose, that is $A=A^H$. We say that a matrix is *normal* if $AA^H=A^HA$. A matrix is *symmetric* if it is its own transpose, that is $A=A^{\mathsf T}$.

Let $x$ and $y$ be two complex-valued $n$-dimensional vectors $x=(x_1,\ldots,x_n)^{\mathsf T}$, $y=(y_1,\ldots,y_n)^{\mathsf T}$. Then the *Euclidean inner product* is defined as:

$$(x,y)=\sum_{j=1}^{n}x_j\overline{y_j},\quad x_j,y_j\in\mathbb C,\ j=1,\ldots,n$$

where in general $\bar a$ is the complex conjugate of $a\in\mathbb C$. We now say that a Hermitian matrix $A$ is *positive definite* if:

$$(Ax,x)>0$$

for all nonzero $n$-dimensional vectors $x$, where $Ax$ denotes matrix–vector multiplication of $A$ and $x$. Furthermore, the matrix $A$ is called *positive semi-definite* if:

$$(Ax,x)\geq 0.$$

A *lower-triangular matrix* $L$ is one whose elements above the main diagonal are zero while an *upper-triangular matrix* $U$ is one whose elements below the main diagonal are zero. An example is given by:

$$L=\begin{pmatrix}1&0&0\\7&2&0\\8&9&4\end{pmatrix}$$

$$U=\begin{pmatrix}1&7&8\\0&2&9\\0&0&4\end{pmatrix}.$$

A matrix $U$ is called *unitary* if its inverse equals its Hermitian transpose, that is:

$$U^{-1}=U^H=\overline{U}^{\mathsf{T}}.$$  (26.20)

An *orthogonal matrix* $P$ is a unitary matrix whose elements are all real and that satisfies:

$$P^{-1}=P^{\mathsf{T}}.$$  (26.21)

### 26.9.1 Cholesky (Square-Root) Decomposition

This is a method to factor a positive definite matrix $A$ into the product of a lower-triangular matrix $L$ and its Hermitian transpose $L^H$:

$$A=LL^H.$$  (26.22)

In this section we use the *Boost uBLAS* library that supports vectors and matrices. We mention that this library does not have operations for numerical linear algebra. We already discussed this library in Chapter 10. See also Demming and Duffy (2012).

For symmetric positive definite matrices the Cholesky decomposition algorithm takes on a particularly simple form:

$$A=LL^{\mathsf{T}}.$$

The algorithm to compute the matrix $L$ is given by (see Dahlquist and Björck, 1974):

$$l_{jj}=\left(a_{jj}-\sum_{k=1}^{j-1}l_{jk}^{2}\right)^{1/2},\qquad 1\leq j\leq n$$

$$l_{ij}=\left(a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk}\right)/l_{jj},\qquad i=j+1,\ldots,n.$$

The C++ code that implements this algorithm is:

```cpp
// Cholesky decomposition.
void Cholesky(const ublas::matrix<double>& A,
              ublas::triangular_matrix<double, ublas::lower>& L)
{
    double sum;
    size_t N = A.size();

    for (size_t j = 0; j < N; ++j)    // Loop over columns.
    {
        sum = 0.0;
        for (size_t k = 0; k < j; ++k)
        {
            sum += L(j,k)*L(j,k);
        }
        L(j,j) = sqrt(A(j,j) - sum);

        for (size_t i = j+1; i < N; ++i) // Rows.
        {
            sum = 0.0;
            for (size_t k = 0; k < j; ++k)
            {
                sum += L(i,k)*L(j,k);
            }
            L(i,j) = (A(i,j) - sum) / L(j,j);
        }
    }
}
```

Finally, an example of how to use the Cholesky algorithm (notice we used a dense matrix in Boost uBLAS) is:

```cpp
// Correlation matrix.
unsigned D = 4;
u::matrix<double> Corr(D,D);
Corr(0,0) = Corr(1,1) = Corr(2,2) = Corr(3,3) = 1.0;
Corr(0,1) = Corr(1,0) = 0.5;
Corr(0,2) = Corr(2,0) = 0.2;
Corr(0,3) = Corr(3,0) = 0.01;
Corr(1,2) = Corr(2,1) = 0.01;
Corr(1,3) = Corr(3,1) = 0.30;
Corr(3,2) = Corr(2,3) = 0.30;
cout << "Original matrix:" << endl << Corr << endl << endl;
```

A test case is:

```cpp
// Cholesky decomposition.
cout << endl << "--- Do Cholesky decomposition ---" << endl << endl;
ublas::triangular_matrix<double, ublas::lower> L(D,D);
Cholesky(Corr, L);
cout << "L:" << endl << L << endl << endl;
```

Now we remark on testing the Cholesky method. In particular, we wish to double-check our algorithm while at the same time using some of the functionality of uBLAS. We try to recover the original matrix that we used in the algorithm by multiplying the constructed lower-triangular matrix by its transpose:

```cpp
// Recover the original matrix; a kind of check.
ublas::triangular_matrix<double, ublas::upper> U = LowerToUpper(L);
cout << "U:" << endl << U << endl << endl;
cout << "L*U (same as original matrix):" << endl << L*U << endl << endl;
```

where LowerToUpper() is a user-defined free function that converts a lower-triangular matrix to an upper-triangular matrix:

```cpp
// Transpose a lower triangular matrix to form an upper triangular matrix.
ublas::triangular_matrix<double, ublas::upper> LowerToUpper
    (const ublas::triangular_matrix<double, ublas::lower>& L)
{
    ublas::triangular_matrix<double, ublas::upper> U(L.size2(), L.size1());
    for (size_t i = 0; i < U.size1(); ++i)
    {
        for (size_t j = i; j < U.size2(); ++j)
        {
            U(i,j) = L(j,i);
        }
    }
    return U;
}
```

We conclude this section by showing how to recover the original matrix by multiplying the upper- and lower-triangular matrices:

```cpp
// Create LU matrices.
cout << "--- Recover original matrix from LD & LD ---" << endl << endl;
ublas::triangular_matrix<double, ublas::lower> LD(D,D);
ublas::triangular_matrix<double, ublas::upper> UD(D,D);
InitLU(Corr, LD, UD);      // Documented in section 26.9.2 This factor
                           // decomposes the
                           // matrix Corr into product of LD and UD
cout << "LD: " << endl << LD << endl << endl;
cout << "UD: " << endl << UD << endl << endl;

// Recover original matrix in different ways.
cout << "LD*UD (same as original matrix): " << endl << LD*UD << endl;
cout << "UD*LD (same as original matrix): " << endl << UD*LD << endl;
```

where we have created user-defined operators for multiplying lower- and upper-triangular matrices:

```cpp
// Compute Lower*Upper.
ublas::matrix<double> operator * (
    const ublas::triangular_matrix<double, ublas::lower>& L,
    const ublas::triangular_matrix<double, ublas::upper>& U)
{
    ublas::matrix<double> result(L.size1(), L.size2());
    double sum; size_t r;
    for (size_t i = 0; i < result.size1(); ++i)
    {
        for (size_t j = 0; j < result.size2(); ++j)
        {
            sum = 0.0;
            r = std::min(i,j);
            for (size_t p = 0; p <= r; ++p)
```

