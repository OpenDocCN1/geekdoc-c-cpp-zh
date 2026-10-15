
```python
x = [0]*(nx+1)                                      # spatial mesh

for i in range(1,nx+1): x[i] = (i-nx2-1)*hx          # spatial mesh

Init(u0,u1,x,nx,c,dk,hx,ht)                          # initial wave packet

GraphInit(1200,600)

for it in range(1,nt+1):                             # time loop
    t = it*ht
    PropagWave(u0,u1,u,nx,c,hx,ht)                   # propagate solution

    for i in range(1,nx): u0[i] = u1[i];  u1[i] = u[i]      # shift solutions

    if (it % nout == 0 or it == nt):                 # output every nout steps
        fname = "wave_{0:4.2f}.txt".format(t)
        out = open(fname,"w")
        out.write("t = {0:4.2f}\n".format(t))
        out.write("      x           u\n")
        for i in range(1,nx+1):
            out.write("{0:10.5f}{1:10.5f}\n".format(x[i],u[i]))
        out.close()

GraphClear()
title = "Wave propagation  t = {0:4.2f}".format(t)
Plot(x,u,nx,"blue",1,0.15,0.95,0.15,0.90,"x","u",title)
GraphUpdate()

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_604_0.png)

FIGURE 13.22 Numerical solution of problem 13.163–13.165 for the classical wave equation, yielded by Program 13.25 with Δk = 0.5 (for Problem 13.8).

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_605_0.png)

FIGURE 13.23 Numerical solution of problem 13.163–13.165 for the classical wave equation, yielded by Program 13.25 with Δk = 5 (for Problem 13.8).

## References and Suggested Further Reading

- Ames, W. F. 1992. Numerical Methods for Partial Differential Equations (3rd ed.). Computer Science and Scientific Computing. San Diego, New York: Academic Press.
- Beu, T. A. 2004. Numerical Calculus in C (3rd ed., in Romanian). Cluj-Napoca: MicroInformatica.
- Beu, T. A. 2007. Numerical solutions of the diffusion equation. In O.-G. Piringer and A. Baner (eds.), Plastic Packaging Materials for Food: Barrier Function, Mass Transport, Quality Assurance, and Legislation. Weinheim: Wiley-VCH.
- Burden, R. and J. Faires. 2010. Numerical Analysis (9th ed.). Boston: Brooks/Cole, Cengage Learning.
- Crank, J. 1975. The Mathematics of Diffusion (2nd ed.). Oxford: Clarendon Press.
- Goldberg, A., H. M. Schey, and J. L. Schwartz. 1967. Computer-generated motion pictures of one-dimensional quantum-mechanical transmission and reflection phenomena. American Journal of Physics 35(3), 177–186.
- Golub, G. H. and J. M. Ortega. 1992. Scientific Computing and Differential Equations: An Introduction to Numerical Methods. San Diego, New York, Boston, London, Sydney, Tokyo, Toronto: Academic Press.
- Hoffman, J. D. 2001. Numerical Methods for Engineers and Scientists (2nd ed.). New York, Basel: Marcel Dekker.
- Koonin, S. E. and D. C. Meredith. 1990. Computational Physics: Fortran Version. Redwood City, CA: Addison-Wesley.
- Landau, R. H., M. J. Páez, and C. C. Bordeianu. 2007. Computational Physics: Problem Solving with Computers (2nd ed.). Weinheim: Wiley-VCH.
- Press, W. H., S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery. 2007. Numerical Recipes: The Art of Scientific Computing (3rd ed.). Cambridge: Cambridge University Press.
- von Neumann, J. 1950. Numerical integration of the barotropic vorticity equation. Tellus 2(4), 237–254.

## Appendix A: Dynamic Array Allocation in C/C++

Listing A.1 shows the content of the header file memalloc.h, which is included in all the C/C++ programs developed in this book for performing dynamic memory allocation for vectors and matrices of types double, int, and complex. The overall concepts are similar to those developed in Press et al. (2002) (for details, see Chapter 2).

### Listing A.1 Functions for Dynamic Allocation of Vectors and Matrices (memalloc.h)

```cpp
//----------------------------------------- memalloc.h -----------------------------------------
// Functions for dynamic memory allocation of vectors and matrices.
// Part of the numxlib numerics library. Author: Titus Beu, 2013
//-----------------------------------------------------------------------------------------------

#ifndef __MEMALLOC_
#define __MEMALLOC_

#include <stdlib.h>
#include <stdio.h>
#include <complex>

using namespace std;
typedef complex<double> dcmplx;

//===============================================================================================
double *Vector(int imin, int imax)
//-----------------------------------------------------------------------------------------------
// Allocates a double vector with indices in the range [imin,imax]
//-----------------------------------------------------------------------------------------------
{
    double *p;
    p = (double*) malloc((size_t) ((imax-imin+1)*sizeof(double)));      // assign block start to array pointer
    if (!p) {
        printf("Vector: allocation error !\n");
        exit(1);
    }
    return p - imin;                                                     // adjust for offset
}

//===============================================================================================
void FreeVector(double *p, int imin)
//-----------------------------------------------------------------------------------------------
// Deallocates a double vector allocated with Vector, with offset imin
//-----------------------------------------------------------------------------------------------
{
    free((void*) (p+imin));                                             // compensate for offset
}
//===============================================================================================

double **Matrix(int imin, int imax, int jmin, int jmax)
//---------------------------------------------------------------------
// Allocates a double matrix, with row and column indices in the range
// [imin,imax] x [jmin,jmax]
//---------------------------------------------------------------------
{
    int i, ni = imax-imin+1, nj = jmax-jmin+1;    // numbers of rows and columns
    double **p;
                                    // allocate array of row pointers
    p = (double**) malloc((size_t) (ni*sizeof(double*)));
    if (!p) {
        printf("Matrix: level 1 allocation error !\n");
        exit(1);
    }
    p -= imin;                                    // adjust for row offset
                                    // assign block start to 1st row pointer
    p[imin] = (double*) malloc((size_t) (ni*nj*sizeof(double)));
    if (!p[imin]) {
        printf("Matrix: level 2 allocation error !\n");
        exit(2);
    }
    p[imin] -= jmin;                // adjust 1st row pointer for column offset
                                    // define row pointers spaced by row length
    for (i=imin+1; i<=imax; i++) p[i] = p[i-1] + nj;

    return p;
}

//=====================================================================
void FreeMatrix(double **p, int imin, int jmin)
//---------------------------------------------------------------------
// Deallocates a double matrix allocated with Matrix, with row and column
// offsets imin and jmin
//---------------------------------------------------------------------
{
    free((void*) (p[imin]+jmin));                        // deallocate block
    free((void*) (p+imin));                // deallocate array of row pointers
}

//=====================================================================
int *IVector(int imin, int imax)
//---------------------------------------------------------------------
// Allocates an int vector with indices in the range [imin,imax]
//---------------------------------------------------------------------
{
    int *p;
                                    // assign block start to array pointer
    p = (int*) malloc((size_t) ((imax-imin+1)*sizeof(int)));
    if (!p) {
        printf("IVector: allocation error !\n");
        exit(1);
    }
    return p - imin;                                // adjust for offset
}

//=====================================================================
void FreeIVector(int *p, int imin)
//---------------------------------------------------------------------
// Deallocates an int vector allocated with IVector, with offset imin
```
