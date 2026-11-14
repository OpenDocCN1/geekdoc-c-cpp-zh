him. His hastily typed version of CG—which you should only skim over—looks like this:

# Listing A-1: Low-abstraction implementation of CG

Click here to view code image

```
#include <iostream>
#include <cmath>

void diag_prec(int size, double *x, double* y)
{
    y[0] = x[0];

    for (int i= 1; i < size; i++)
        y[i] = 0.5 * x[i];
}

double one_norm(int size, double *vp)
{
    double sum= 0;
    for (int i= 0; i < size; i++)
        sum+= fabs(vp[i]);
    return sum;
}

double dot(int size, double *vp, double *wp)
{
    double sum= 0;
    for (int i= 0; i < size; i++)
        sum+= vp[i] * wp[i];
    return sum;
}

int cg(int size, double *x, double *b,
       void (*prec) (int, double*, double*), double eps)
{
    int i, j, iter= 0;
    double rho, rho_1, alpha;
    double *p= new double[size];
    double *q= new double[size];
    double *r= new double[size];
    double *z= new double[size];

    // r = A*x;
    r[0] = 2.0 * x[0] - x[1];
    for (int i= 1; i < size-1; i++)
        r[i] = 2.0 * x[i] - x[i-1] - x[i+1];
```