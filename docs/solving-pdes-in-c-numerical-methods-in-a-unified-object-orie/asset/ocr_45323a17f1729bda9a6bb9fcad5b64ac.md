# 17.4 Jacobi Relaxation

In the Gauss–Seidel relaxation, the components are relaxed one by one. The relaxation of the i-th component, $x_i^{(k)}$, uses the already updated components $x_0^{(k+1)}, x_1^{(k+1)}, ..., x_{i-1}^{(k+1)}$. The order in which the relaxation takes place is, thus, important. In the Jacobi relaxation method, on the other hand, all the components are relaxed independently, using only components from $x^{(k)}$, not from $x^{(k+1)}$. This approach, although inferior to the previous one in terms of convergence rate, is more suitable for parallel implementation (see Chapter 18, Section 15).

The Jacobi relaxation method can be written as follows: for every $0 \le i < N$,

$x_i^{(k+1)} \equiv x_i^{(k)} + (A_{i,i})^{-1} \left( f - A x^{(k)} \right)_i$

In fact, the Jacobi iteration can also be written in vector form as follows:

$x^{(k+1)} \equiv x^{(k)} + \operatorname{diag}(A)^{-1} \left( f - A x^{(k)} \right)$

Actually, here $\operatorname{diag}(A)$ (the main diagonal of $A$) serves as a preconditioner.

If we use the arithmetic operations in the "dynamicVector" and "sparseMatrix" classes, the implementation of the Jacobi iteration is particularly straightforward. First, however, we need to define an "operator/" function that takes a vector $v$ and a matrix $A$ as arguments and returns the vector $\operatorname{diag}(A)^{-1} v$:

```
template<class T>
const dynamicVector<T>
operator/(const dynamicVector<T>&v,
        const sparseMatrix<T>&A) {
    dynamicVector<T> result(v);
    for(int i=0; i<v.dim(); i++)
        result(i) /= A(i,i);
    return result;
} // vector divided by the main diagonal of matrix
```

This operator is now used in the Jacobi iteration that computes $x^{(k+1)}$ and places it in the same storage that was occupied by $x^{(k)}$:

```
template<class T>
void Jacobi(const sparseMatrix<T>&A,
        const dynamicVector<T>&f, dynamicVector<T>&x) {
    x += (f - A * x) / A;
} // Jacobi relaxation
```

Note that, since the priority rules of user-defined operators are the same as the priority rules built in C for arithmetic operations, one must use parentheses to form the residual before dividing it by the main diagonal of $A$. Using the above function, one can now use a loop of 100 Jacobi iterations as follows:

```
for(int i=0; i<100; i++)
    Jacobi(A,f,x);
print(x);
```