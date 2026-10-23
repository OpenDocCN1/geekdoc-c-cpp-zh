```
Corr(3,2) = Corr(2,3) = 0.30;
std::cout << "Original matrix: " << Corr << std::endl;

u::matrix<double> Backup(Corr);

u::triangular_matrix<double, u::lower> LD(D,D);
u::triangular_matrix<double, u::upper> UD(D,D);

InitLU(Corr, LD, UD);

// Recover original matrix in different ways
Corr = LD * UD;
std::cout << "LD*UD: " << Corr << std::endl;

Corr = UD * LD;
std::cout << "UD*LD: " << Corr << std::endl;

// Look at matrix norms
u::matrix<double> m1 = Backup - UD*LD;
std::cout << "A - U*L max error: " << u::norm_inf(m1) << std::endl;

u::matrix<double> m2 = Backup - LD*UD;
std::cout << "A - L*U max error: " << u::norm_inf(m2) << std::endl;

// Now test Cholesky directly
u::triangular_matrix<double, u::lower> L(D,D);
Cholesky(Backup, L);

u::matrix<double> Product  = L * trans(L);
std::cout << "Cholesky, L*trans(L): " << Product << std::endl;
std::cout << "A - L*trans(L) max error: "
          << u::norm_inf(Backup - Product) << std::endl;

Product  = trans(L)*L;
std::cout << "Cholesky, trans(L)*L: " << Product << std::endl;
std::cout << "A - trans(L)*L max error: "
          << u::norm_inf(Backup - Product) << std::endl;
```

The Cholesky decomposition is also applicable to matrices with complex coefficients; however, we need to introduce a modification to the code (we need to take the complex conjugate of the transposed matrix elements):

```
template <typename T>
    void CholeskyComplex(const u::matrix<std::complex<T>>& A,
                        u::triangular_matrix<std::complex<T>, u::lower>& L)
{ // Cholesky decomposition

    std::complex<T> sum;
    unsigned N = A.size1();
```