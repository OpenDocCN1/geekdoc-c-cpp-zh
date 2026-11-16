In C++ Code 6.4 and C++ Code 6.3 we show how to calculate the mean variance optimal portfolio for a given required return. This is the case where there are no constraints on the weight, and we use the analytical solution directly.

```
#include "newmat.h"
using namespace NEWMAT;
ReturnMatrix mv_calculate_portfolio_given_mean_unconstrained(const Matrix& e,
                                 const Matrix& V,
                                 const double& r){
  int no_assets=nRows();
  Matrix ones = Matrix(no_assets,1); for (int i=0;i<no_assets;++i) ones.element(i,0) = 1;
  Matrix Vinv = V.i(); // inverse of V
  Matrix A = (ones.t()*Vinv*e); double a = A.element(0,0);
  Matrix B = e.t()*Vinv*e; double b = B.element(0,0);
  Matrix C = ones.t()*Vinv*ones; double c = C.element(0,0);
  double d = b*c - a*a;
  Matrix Vinv1=Vinv*ones;
  Matrix Vinve=Vinv*e;
  Matrix g = ((Vinv1*b - Vinve*a)*(1.0/d));
  Matrix h = (Vinv*e - Vinv1*a)*(1.0/d);
  Matrix w = r * g + h*r;
  w.Release();
  return w;
};
```

# C++ Code 6.3: Calculating the unconstrained frontier portfolio given an expected return using Newmat

# Example

Mean variance calculations.

\(\mathbf{e} = \left[ \begin{array} { c } { 0 . 0 5 } \\ { 0 . 1 } \\ \end{array} \right]\)

\(\mathbf{V} = \left[ \begin{array} { c c } { 1 . 0 } & { 0 . 0 } \\ { 0 . 0 } & { 1 . 0 } \\ \end{array} \right]\)

Find the optimal minimum variance portfolio with return \(r = 0.075\).

```
C++ program:
cout << "Testing portfolio calculation " << endl;
Matrix e(2,1);
e(1)=0.05; e(2,1)=0.1;
Matrix V(2,2);
V(1,1)=1.0; V(2,1)=0.0;
V(1,2)=0.0; V(2,2)=1.0;
double r=0.075;
Matrix w = mv_calculate_portfolio_given_mean_unconstrained(e,V,r);
cout << "suggested portfolio: ";
cout << " w1 = " << w(1) << " w2 = " << w(2.1) << endl;
Output from C++ program:
Testing portfolio calculation
suggested portfolio: w1 = 0.5 w2 = 0.5
```