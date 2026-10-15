```
void GaussSeidel(double **a, double b[], double x[], int n, int init, double &err)
//--------------------------------------------------------------------------------
// Solves linear system a x = b by the Gauss-Seidel method.
// To ensure convergence, the system is left-multiplied with a^T.
// a   - coefficient matrix (n x n)
// b   - vector of constant terms
// x   - initial approximation of solution (input); solution (output)
// n   - order of system
// err - maximum relative error of the solution components
// init - initialization option: 0 - refines initial approximation
//                                 1 - initializes solution
//--------------------------------------------------------------------------------
{
    const double eps = 1e-10;                     // relative precision criterion
    const int itmax = 1000;                       // max no. of iterations
    double del, f, **s, *t;
    int i, j, k;

    s = Matrix(1,n,1,n);                          // matrices of reduced system
    t = Vector(1,n);

    for (i=1; i<=n; i++) {                        // matrices of normal system
        for (j=1; j<=i; j++) {                    // by multiplication with a^T
            s[i][j] = 0e0;                        // store result in s and t
            for (k=1; k<=n; k++) s[i][j] += a[k][i]*a[k][j];
            s[j][i] = s[i][j];
        }
        t[i] = 0e0;
        for (j=1; j<=n; j++) t[i] += a[j][i]*b[j];
    }

    for (i=1; i<=n; i++) {                        // matrices s and t of reduced system
        f = -1e0/s[i][i]; t[i] /= s[i][i];
        for (j=1; j<=n; j++) s[i][j] *= f;
    }

    if (init) for (i=1; i<=n; i++) x[i] = t[i];   // initialize solution

    for (k=1; k<=itmax; k++) {                    // loop of iterations
        err = 0e0;
        for (i=1; i<=n; i++) {
            del = t[i];                           // correction
            for (j=1; j<=n; j++) del += s[i][j]*x[j];
            x[i] += del;                          // new approximation to solution
            if (x[i]) del /= x[i];                // relative error
            if (fabs(del) > err) err = fabs(del); // maximum error
        }
        if (err <= eps) break;                    // check convergence
    }
    if (k > itmax) printf("GaussSeidel: max. no. of iterations exceeded !\n");

    FreeMatrix(s,1,1); FreeVector(t,1);
}

#endif
```