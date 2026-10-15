```
// using the recurrence relation
//---------------------------------------------------------------------------
{
    double f, fm1, fm2;
    int i;

    if (n == 0) {
        f = 1e0;
    } else {
        f = 1e0 + k - x; fm1 = 1e0;
        for (i=2; i<=n; i++) {
            fm2 = fm1; fm1 = f;
            f = ((2*i+k-1-x)*fm1 - (i+k-1)*fm2)/i;
        }
    }
    return f;
}

//===========================================================================
double Hermite(int n, double x, double &d)
//---------------------------------------------------------------------------
// Evaluates the n-th order Hermite polynomial and its derivative d in x
// using the recurrence relation
//---------------------------------------------------------------------------
{
    double f, fm1, fm2, x2;
    int i;

    if (n == 0) {
        f = 1e0; d = 0e0;
    } else {
        f = 2*x; fm1 = 1e0; x2 = 2*x;
        for (i=2; i<=n; i++) {
            fm2 = fm1; fm1 = f;
            f = x2*fm1 - 2*(i-1)*fm2;
        }
        d = 2*n*fm1;
    }
    return f;
}

//===========================================================================
void SpherY(int l, int m, double theta, double phi, double &ReY, double &ImY)
//---------------------------------------------------------------------------
// Evaluates the real and imaginary parts (ReY and ImY) of the spherical
// harmonic of orders l and m for arguments theta and phi.
// Calls aLegendre to calculate associated Legendre polynomials.
//---------------------------------------------------------------------------
{
#define pi 3.141592653589793
    double fact;
    int i, mabs;

    mabs = abs(m);

    fact = 1e0;
    for (i=1-mabs+1; i<=1+mabs; i++) fact *= i;  // (1+|m|)!/(1-|m|)!

    fact = sqrt((2*l+1)/(4e0*pi*fact)) * aLegendre(l,mabs,cos(theta));
```