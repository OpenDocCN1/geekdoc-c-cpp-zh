
```c
}
    return s;
}

//=============================================================================
void xSimpson(double a, double b, double x[], double w[], int n)
//-----------------------------------------------------------------------------
// Calculates abscissas x[] and weights w[] for Simpson’s rule with n
// integration points on interval [a,b]
//-----------------------------------------------------------------------------
{
    const double c13 = 1e0/3e0, c23 = 2e0/3e0, c43 = 4e0/3e0;
    double h;
    int i;

    if (n % 2 == 0) n++;

    h = (b-a)/(n-1);
    for (i=1; i<=n; i++) {
        x[i] = a + (i-1)*h; w[i] = h * (i % 2 ? c23 : c43);
    }
    w[1] = w[n] = h * c13;
}

//=============================================================================
double qSimpson3D(double Func(double,double,double),
                  double ax, double bx, int nx,
                  double ay, double by, int ny,
                  double az, double bz, int nz)
//-----------------------------------------------------------------------------
// Integrates function Func(x,y,z) in the cuboid [ax,bx] x [ay,by] x [az,bz]
// using Simpson’s rule with (nx x ny x nz) integration points
//-----------------------------------------------------------------------------
{
    double *wx, *wy, *wz, *x, *y, *z;
    double s, sx, sy;
    int i, j, k;

    if (nx % 2 == 0) nx++;
    if (ny % 2 == 0) ny++;
    if (nz % 2 == 0) nz++;

    x = Vector(1,nx); wx = Vector(1,nx);
    y = Vector(1,ny); wy = Vector(1,ny);
    z = Vector(1,nz); wz = Vector(1,nz);

    xSimpson(ax,bx,x,wx,nx);
    xSimpson(ay,by,y,wy,ny);
    xSimpson(az,bz,z,wz,nz);

    s = 0e0;
    for (i=1; i<=nx; i++) {
        sx = 0e0;
        for (j=1; j<=ny; j++) {
            sy = 0e0;
            for (k=1; k<=nz; k++) {
                sy += wz[k] * Func(x[i],y[j],z[k]);
            }
            sx += wy[j] * sy;
        }
        s += wx[i] * sx;
    }
}
    s += wx[i] * sx;
}

FreeVector(x,1); FreeVector(wx,1);
FreeVector(y,1); FreeVector(wy,1);
FreeVector(z,1); FreeVector(wz,1);

return s;
}
//==============================================================================
double qGaussLeg3D(double Func(double,double,double),
    double ax, double bx, int nx,
    double ay, double by, int ny,
    double az, double bz, int nz)
//------------------------------------------------------------------------------
// Integrates function Func(x,y,z) in the cuboid [ax,bx] x [ay,by] x [az,bz]
// using Gauss-Legendre quadratures with (nx x ny x nz) integration points
//------------------------------------------------------------------------------
{
    double *wx, *wy, *wz, *x, *y, *z;
    double s, sx, sy;
    int i, j, k;

    x = Vector(1,nx); wx = Vector(1,nx);
    y = Vector(1,ny); wy = Vector(1,ny);
    z = Vector(1,nz); wz = Vector(1,nz);

    xGaussLeg(ax,bx,x,wx,nx);                 // generate integration points
    xGaussLeg(ay,by,y,wy,ny);
    xGaussLeg(az,bz,z,wz,nz);

    s = 0e0;
    for (i=1; i<=nx; i++) {
        sx = 0e0;
        for (j=1; j<=ny; j++) {
            sy = 0e0;
            for (k=1; k<=nz; k++) {
                sy += wz[k] * Func(x[i],y[j],z[k]);
            }
            sx += wy[j] * sy;
        }
        s += wx[i] * sx;
    }

    FreeVector(x,1); FreeVector(wx,1);
    FreeVector(y,1); FreeVector(wy,1);
    FreeVector(z,1); FreeVector(wz,1);

    return s;
}
//==============================================================================
double qSimpsonAng(double Func(double,double), int nt, int np)
//------------------------------------------------------------------------------
// Integrates function Func(theta,phi) on [0,pi] x [0,2*pi] in spherical
// coordinates using Simpson's rule with (nt x np) points
//------------------------------------------------------------------------------
{
#define pi 3.141592653589793
double *wt, *wp, *t, *p;
double s, st;
int i, j;
if (nt % 2 == 0) nt++; // increment nt if even
if (np % 2 == 0) np++; // increment np if even
t = Vector(1,nt); wt = Vector(1,nt);
p = Vector(1,np); wp = Vector(1,np);
xSimpson(0e0,pi,t,wt,nt); // generate integration points
xSimpson(0e0,2e0*pi,p,wp,np);
for (i=1; i<=nt; i++) {
    wt[i] *= sin(t[i]);
} // volume element
s = 0e0;
for (i=1; i<=nt; i++) {
    st = 0e0;
    for (j=1; j<=np; j++) {
        st += wp[j] * Func(t[i],p[j]);
    }
    s += wt[i] * st;
}
FreeVector(t,1); FreeVector(wt,1);
FreeVector(p,1); FreeVector(wp,1);
return s;
}
//================================================================================
double qSimpsonSph(double Func(double,double,double), double a, int nr, int nt, int np)
//--------------------------------------------------------------------------------
// Integrates function Func(r,theta,phi) on [0,a] x [0,pi] x [0,2*pi]
// in spherical coordinates using Simpson's rule with (nr x nt x np) points
//--------------------------------------------------------------------------------
{
#define pi 3.141592653589793
double *wr, *wt, *wp, *r, *t, *p;
double s, sr, st;
int i, j, k;
if (nr % 2 == 0) nr++; // increment nr if even
if (nt % 2 == 0) nt++; // increment nt if even
if (np % 2 == 0) np++; // increment np if even
r = Vector(1,nr); wr = Vector(1,nr);
t = Vector(1,nt); wt = Vector(1,nt);
p = Vector(1,np); wp = Vector(1,np);
xSimpson(0e0,a,r,wr,nr); // generate integration points
xSimpson(0e0,pi,t,wt,nt);
xSimpson(0e0,2e0*pi,p,wp,np);
for (i=1; i<=nr; i++) {
    wr[i] *= r[i] * r[i];
} // factors from
for (j=1; j<=nt; j++) {
    wt[j] *= sin(t[j]);
} // volume element
s = 0e0;
for (i=1; i<=nr; i++) {
    sr = 0e0;
    for (j=1; j<=nt; j++) {
        st = 0e0;
        for (k=1; k<=np; k++) {
            st += wp[k] * Func(r[i],t[j],p[k]);
        }
        sr += wt[j] * st;
    }
    s += wr[i] * sr;
}

FreeVector(r,1); FreeVector(wr,1);
FreeVector(t,1); FreeVector(wt,1);
FreeVector(p,1); FreeVector(wp,1);

return s;
}

//====================
double qGaussSph(double Func(double,double,double), int nr, int nt, int np)
//-------------------
// Integrates function Func(r,theta,phi) on [0,inf] x [0,pi] x [0,2*pi]
// in spherical coordinates using Gauss-Laguerre and Gauss-Legendre formulas
// with (nr x nt x np) points
//-------------------
{
#define pi 3.141592653589793
    double *wr, *wt, *wp, *r, *t, *p;
    double s, sr, st;
    int i, j, k;

    r = Vector(1,nr); wr = Vector(1,nr);
    t = Vector(1,nt); wt = Vector(1,nt);
    p = Vector(1,np); wp = Vector(1,np);

    xGaussLag(0e0,r,wr,nr);            // Gauss-Laguerre radial quadrature
    xGaussLeg(0e0,pi,t,wt,nt);         // Gauss-Legendre angular quadratures
    xGaussLeg(0e0,2e0*pi,p,wp,np);

    for (i=1; i<=nr; i++) { wr[i] *= r[i] * r[i]; }      // factors from
    for (j=1; j<=nt; j++) { wt[j] *= sin(t[j]); }        // volume element

    s = 0e0;
    for (i=1; i<=nr; i++) {
        sr = 0e0;
        for (j=1; j<=nt; j++) {
            st = 0e0;
            for (k=1; k<=np; k++) {
                st += wp[k] * Func(r[i],t[j],p[k]);
            }
            sr += wt[j] * st;
        }
        s += wr[i] * sr;
    }

    FreeVector(r,1); FreeVector(wr,1);
}

# 10.14 Problems

The Python and C/C++ programs for the following problems may import the functions developed in this chapter from the modules integral.py and, respectively, integral.h, which are available as supplementary material. For creating runtime plots, the graphical routines contained in the libraries graphlib.py and graphlib.h may be employed.

# PROBLEM 10.1

Evaluate the integral

I = ∫₀^π sin x dx = 2,

by using comparatively the composite trapezoidal and Simpson rules (routines qTrapz and qSimpson) for numbers of subintervals doubled in sequence from n = 2 to 1024. For each number of subintervals, evaluate the relative errors with respect to the exact result

δ_T^(n) = |1 − I_T^(n)/I|,   δ_S^(n) = |1 − I_S^(n)/I|,

as well as the error reduction factor between two consecutive estimates of the integral

f_T^(n) = I_T^(n−1)/I_T^(n),   f_S^(n) = I_S^(n−1)/I_S^(n).

Compare the numerical reduction factors with the theoretical values 4 and, respectively, 16, resulting from the orders O(h²) and O(h⁴) of the global errors featured by the trapezoidal and Simpson rules.

# Listing 10.26 Convergence of the Trapezoidal and Simpson Rules (Python Coding)

```
# Convergence of trapezoidal and Simpson quadratures
from math import *
from integral import *

def Func(x): return sin(x)                     # integrand

a = 0e0; b = pi                               # integration domain

I = cos(a) - cos(b)                           # exact result
print("Exact result = ",I)
print("   n        IT        errT    facT        IS        errS    facS")

n = 1
errT0 = 1e0; errS0 = 1e0
for i in range(1,11):
    n = 2*n                                   # number of intervals

    IT = qTrapz(Func,a,b,n+1)                 # trapezoidal rule
    errT = fabs(1e0 - IT/I)                   # relative error
    facT = errT0/errT                         # error reduction

    IS = qSimpson(Func,a,b,n+1)               # Simpson's rule
    errS = fabs(1e0 - IS/I)                   # relative error
    facS = errS0/errS                         # error reduction

    print(("{0:5d}{1:11.6f}{2:10.1e}{3:6.1f}{4:11.6f}{5:10.1e}{6:6.1f}").
          format(n,IT,errT,facT,IS,errS,facS))

    errT0 = errT; errS0 = errS
```
