# 246 NUMERICAL LINEAR ALGEBRA

Listing 7.4 linssDriver.cc

```
//linssDriver.cc
#include "R.h"
#include "vector.hh"
#include "linss.hh"

extern "C" {

void linss(int* n, double* lam, double* px, double* py,
    double* pfit, double* GCV){

    Vector y(*n, py);
    Vector x(*n, px);

    Linss S(x, y);
    Vector fit = S.smooth(*lam, GCV);
    for(int i = 0; i < n; i++)
        pfit[i] = fit[i];
}
```

The arguments to the linss function are pointers to variables that use in computing the fit of responses (n), the value of the smoothing parameter for the independent variable (px), the response vector (py), a vector (pfit) being passed from R that will be filled with the fitted values and an empty memory location that will hold the value of the GCV criterion return to the R environment. The shared library linssDriver.so

$ CMD SHLIB linssDriver.cc linss.cc matrix.cc vector.cc

From R inside the library is loaded with
> dyn.load("linssDriver.so")

Linear smoothing splines may be fit in R by using the imported library with the .C function. Rather than do this directly, we will use the mechanics in the wrapper function

Listing 7.5 linss.r

```
#linss.r
function(x, y, lam) {
    fit <- .C("linss", as.integer(length(x)), as.double(lam),
        as.double(x), as.double(y), vector("numeric", length(x)), 0..)
    list(fit[[5]], fit[[6]])
}
```

In calling existing values will be used for x and y that originate in R. The numeric vector that will hold the fitted values and the variable that will hold the value of the GCV criterion need to be initialized of R as well. Upon completion of the C++ program returns control to the .C function that packages the outcome in the form of a list containing the return values for all the variables that were passed to the C++ program. In this particular the result is a length of six with the fitted values and the value of the GCV criterion being the fifth and sixth components, respectively. These quantities are what the user will want and, accordingly, our wrapper returns them in a two component list.

Section 8.3.2 of the next chapter develops an automated procedure for selecting a good