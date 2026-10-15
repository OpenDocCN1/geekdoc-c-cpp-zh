# Solution

Implementations are provided in Listings 5.12 and 5.13, and graphical output, in Figure 5.5.

# Listing 5.13  Plot of a Polynomial and Its Derivative (C/C++ Coding)

```
```cpp
// Plot polynomial and derivative
#include "menallco.h"
#include "elemfunc.h"
#include "graphlib.h"

int main(int argc, wchar_t** argv)
{
    const int np = 5;                                      // degree of polynomial
    double a[] = {63e0/8e0, 0e0, -70e0/8e0, 0e0, 15e0/8e0, 0e0};    // coeffs
    double b[np+1];                                        // work array
    double h, xmin, xmax, *x, *y, *z;
    int i, n;

    xmin = -1e0; xmax = 1e0;                               // plotting domain
    h = 0.01e0;                                             // argument spacing
    n = int((xmax-xmin)/h + 0.5) + 1;                      // number of points

    x = Vector(1,n); y = Vector(1,n); z = Vector(1,n);     // arrays for plots

    PolyDerive(a,b,np);                                    // coefficients of derivative in b

    for (i=1; i<=n; i++) {
        x[i] = xmin + (i-1)*h;                             // argument
        y[i] = Poly(x[i],a,np);                            // polynomial
        z[i] = Poly(x[i],b,np-1);                           // derivative
    }

    PyGraph w(argc, argv);
    w.GraphInit(1200,600);

    w.Plot(x,y,n,"blue",1,0.10,0.45,0.15,0.85,"x","P(x)","Polynomial");
    w.Plot(x,z,n,"red",1,0.60,0.95,0.15,0.85,"x","P'(x)","Derivative");

    w.MainLoop();
}
```
```

# PROBLEM 5.2

Write routines for calculating the functions $\sin x$ and $\arcsin x$ from their power-series expansions:

$$\sin x = \sum_{i=0}^{\infty} \frac{(-1)^i}{(2i+1)!}x^{2i+1} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots, \tag{5.61}$$

$$\arcsin x = \sum_{i=0}^{\infty} \frac{(2i)!}{2^{2i}(i!)^2(2i+1)}x^{2i+1} = x + \frac{1}{6}x^3 + \frac{3}{40}x^5 + \cdots. \tag{5.62}$$