# NUMERICAL LINEAR ALGEBRA

```
fIn1 >> pc[i];
}
for(int i = 0; i < n; i++)
    for(int j = 0; j < m; j++)
        fIn2 >> pA2[m*i + j];

fIn1.close(); fIn2.close();
TNT::Array2D<double> A1(n, pA1);
cout << "The matrix A1" << endl;
cout << A1 << endl;
TNT::Array1D<double> c(n, pc);
cout << "The right-hand side" << endl;
cout << c << endl;
JAMA::olesky<double> Ch(A1);
cout << "The solution by Cholesky" << endl;
cout << Ch.solve(c) << endl;

JAMA::Eigenvalue<double> A1Eg(A1);
TNT::Array2D<double> V1(n, n);
TNT::Array1D<double> lambda(n);
A1Eg.getRealEigenvalues(lambda);
A1Eg.getV(V1);
cout << "The eigenvalues for A1" << endl;
cout << lambda << endl;
cout << "The eigenvectors for A1" << endl;
cout << V1 << endl;

TNT::Array2D<double> A2(n, pA2);
cout << "The matrix A2" << endl;
cout << A2 << endl;

int dmin = min(m, n);
JAMA::SVD<double> A2Svd(A2);
TNT::Array2D<double> V2(n, m);
TNT::Array2D<double> U(n, n);
TNT::Array1D<double> s(dmin);
A2Svd.getSingularValues(s); A2Svd.getU(U); A2Svd.getV(V2);

cout << "The singular values for A2" << endl;
cout << s << endl;
cout << "The left singular vectors for A2" << endl;
cout << U << endl;
cout << "The right singular vectors for A2" << endl;
cout << V2 << endl;
return 0;
}
```

First observe that the headers for the JAMA package classes have been included: namely, jama_cholesky.h, jama_eig.h and jama_svd.h for classes Cholesky, Eigenvalue and SVD, respectively. The solution of our linear system is obtained as a direct application of the solve function using a Cholesky class object. For the eigenvalue and singular-value decompositions different constructors were employed for the TNT Array1D and Array2D classes that require specification of only the array dimensions. Arrays created in this manner are passed as arguments to the functions that return the eigenvalues, eigenvectors, singular values and singular vectors.