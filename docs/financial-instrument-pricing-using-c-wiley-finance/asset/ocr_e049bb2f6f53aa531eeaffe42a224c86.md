where:

$x_{i-1/2}=x_{i-1}+h_x/2$

$y_{j-1/2}=y_{j-1}+h_y/2$

$z_{k-1/2}=z_{k-1}+h_z/2,\quad 1\leq i\leq NX,\ 1\leq j\leq NY,\ 1\leq k\leq NZ.$

You can create this scheme from first principles as we did in the two-dimensional case by composing divided differences in the $x$, $y$ and $z$ directions. Furthermore, we adopt the heuristic by defining the boundary values (similar to (16.5)):

$U(AL,y,z)=u(x,BL,z)=u(x,y,CL)\quad \forall\ -\infty<x,y,z<\infty$

where $AL$, $BL$, and $CL$ are truncation values (typically $AL=BL=CL=-8$).

Since we are working in three-dimensional space we need a data structure to hold three-dimensional discrete data. To this end, we use the *Boost multi_array* structure (Demming and Duffy, 2010). We define the structure as follows:

```
```cpp
#include <boost/multi_array.hpp>
const int DIM = 3; // 3d matrix
typedef boost::multi_array<double, DIM> Tensor;
typedef Tensor::index Index;
```
```

The code for scheme (16.15) consists of creating three mesh arrays, creating and initialising the *tensor* to hold the values to be generated and then updating the values by mapping scheme (16.15) to C++ code:

```
```cpp
// Call this function once and then do table lookup at a given (x,y)
double IntegralValues(double b1, double b2, double b3,
                      double a21, double a31, double a32,
                      int NX, int NY, int NZ)
{ // Matrix of integral values at mesh points

    double hx = std::abs(b1-a1)/static_cast<double>(NX);
    double hy = std::abs(b2-a2)/static_cast<double>(NY);
    double hz = std::abs(b3-a3)/static_cast<double>(NZ);


    // Tensor to hold results
    Tensor Values;
    Values.resize(boost::extents [NX+1] [NY+1] [NZ+1]);

    // Create arrays of mesh points
    ublas::vector<double> xarr (NX+1, 0.0);
    xarr[0] = a1;
    for (std::size_t i = 1; i < xarr.size(); ++i) xarr[i] = xarr[i-1] + hx;

    ublas::vector<double> yarr (NY+1, 0.0);
    yarr[0] = a2;
    for (std::size_t i = 1; i < yarr.size(); ++i) yarr[i] = yarr[i-1] + hy;
```
```