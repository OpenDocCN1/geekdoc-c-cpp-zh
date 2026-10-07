294 NUMERICAL OPTIMIZATION

```
//optDriver.cpp
#include <iostream>
#include <stdlib.h>
#include <iomanip>
#include <optim.h>
#include "functor.h"

double fun(double theta) {
    return (-theta*(1. theta));
}

int main(int argc, char** argv) {
    int itMax = atoi(argv[1]);
    double delta = atof(argv[2]);
    Functor f(&fun);
    Optim Opt Opt = Optim(itMax, delta);
    double fMin = Opt.golden(f, 0., 1.);
    std::cout << "The approximate minimizer is " <<
           std::cout << std::setprecision(16) << fMin << std::endl;
}

return 0;
```

This program takes the maximum number of iterations (itMax) and the lower bound for the relative change in the approximate minimizer (delta) as command line arguments and converts them from char to int and double using the atoi and atof functions (by including the c header). The address of the function fun is to be minimized using the user-supplied values of itMax and the golden method is applied to the Functor object. The next step is to print the result to standard output. For reasons that will become clear momentarily, the output is to be printed to 16 decimal places accuracy. For this purpose the C++ standard library function setprecision (see Section 2.5) is accessed via inclusion of the iomanip header.

To carry out the minimization process using the optDriver.cpp program is necessary to provide values for the stopping parameters itMax and delta. As noted, since the computations are aided by double precision there is no reason to choose delta smaller than 10^{-16}. The selection of itMax can be guided by several considerations. If the golden section search over an interval [a,b] then at each step of the recursion the length of the interval that remains to be searched is reduced by the factor r. After the kth iteration the current search interval will have length r^k(b-a). For a=0 and b=1 this gives k = -16/log10(r) ≈ 76 as the number of iterations that will be required to produce changes in the minimizer that are no longer detectable in double precision.

The optim and optDriver.cpp programs are compiled and linked to create an executable title. The opt section method then produced

$ /opt 76 .000000000000001
The approximate minimizer is 0.5000000037252904

The performance of golden section here seems somewhat disappointing. Certainly, the search has placed us in the right location for minimization of the target function. But, there are only eight decimals of accuracy and as may have been expected. The culprit here is off-round error; but, not from the approximation of the minimizer se. The problem is that the objective function f(\theta) = -\theta(1-\theta) behaves like $-\theta^2$ near