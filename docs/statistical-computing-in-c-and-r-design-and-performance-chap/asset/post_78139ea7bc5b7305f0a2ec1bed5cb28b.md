
![](img/b50973a0535e1d41c799ab78355b19f6_157_0.png)

Figure 4.4 Histogram for simulated data

```
> summary(nDat)
Min. 1st Qu. Median Mean 3rd Qu. Max.
-2.60400 -0.71500 -0.01388 -0.05790 0.63210 2.82700
> sd(nDat)
[1] 0.9918201
> IQR(nDat)
[1] 1.347105
> pnorm(sqrt(length(nDat))*mean(nDat)/sd(nDat))
[1] 0.09588755
> ks.test(nDat, pnorm)
```

One-sample Kolmogorov-Smirnov test

```
data: nDat
D = 0.0346, p-value = 0.5865
alternative hypothesis: two-sided
```

```
> shapiro.test(nDat)
```

Shapiro-Wilk normality test

```
data: nDat
W = 0.9967, p-value = 0.4145
```

Since the data is used to have come from a normal distribution, the Shapiro-Wilk tests statistic was computed as well as the Kolmogorov-Smirnov statistic. On the basis of these two measures the hypothesis of normality cannot be rejected at any reasonable significance level.

# 142 GENERATION OF PSEUDO-RANDOM NUMBERS

### 4.8 Generating random numbers in R

As described in Appendix B, the R language provides the facility for obtaining random deviates from most of the standard distributions used in statistics. Random numbers for a distribution are produced with syntax such

```
rnorm(n, ...)
```

with n being the desired sample size and ... indicating other arguments that might be needed for a particular distribution of interest. The type of random number generator that is used in the rnorm functions can be determined and set using RNGkind. Entering RNG() will return two values: the generator used to generate uniforms and the generator used to generate normals. The default generator is the Mersenne Twister. There are other options, including the VH generator, which are listed in the R help for RNGkind. The default method for generating random deviates is direct inversion. There are four other options which is the Box-Muller method. A user-specified method can also be employed for generating either uniforms or normals.

To choose one of the other options for generating uniforms or normals, simply specify a value for one or both of RNGkind and determine the uniform and normal generator, respectively. The ensuing code segments for the current generator and changing them to the Wichmann-Hill and Box-Muller methods are

```
> RNGkind()
[1] MersenneTwister "Inversion"
> RNGkind(kind = "Wichmann-Hill", kind = "Box-Muller")
> RNGkind()
[1] Wichmann-Hill "Box-Muller"
```

Although the RNG generator discussed in Section 4.5 is not one of the options that can be chosen with RNGkind, it can be accessed through the rstream package. After loading the package, the random number generator for the R session can be set as follows

```
> library("rstream")
> rstream.RNG(seed = c(1, 2, 3, 4, 5, 6))
> runif(1)
[1] 0.0010948
```

The seed argument chosen to be the same as the one that was used in the generator from Section 4.5. The output indicates that the RNG generator with this seed is now being used to generate uniforms in R. In order to recreate data that has been previously produced by a random number generator, we need to know the seed or seeds that were used in the generator. The function setseed is an integer variable that is used to set whatever seeds are required for the chosen generator method. In the example shown below seed is first set to 123. Then two sets of five random normals are generated. The second set of five is different from the first as be expected. Then seed is reset to 123 and the rnorm(5) command produces the values that were originally obtained

```
> setseed(123)
> rnorm(5)
[1] -0.4542997 0.1593962 0.8977403 1.1607478 -0.4748856
> rnorm(5)
[1] -1.5673634 0.6444441 1.0574895 0.1692509 0.6725876
> setseed(123)
> rnorm(5)
[1] -0.4542997 0.1593962 0.8977403 1.1607478 -0.4748856
```

Note that this exercise was carried out using the RNG generator for the uniforms required for the Box-Muller method. This generator requires three seeds. The setseed function uses its single argument to create the three seeds that are needed for this particular generator and performs similar tasks for the other generator options that require multiple and/or choices for these seeds.

### 4.9 Using the R Standalone Math Library

R language is largely implemented in C. One consequence of this is that it is possible to create a code library that contains the C implementations of the standard functions that are used in R. These include the quantile functions, densities and distribution functions for the standard probability distributions as well as the associated number generators. To obtain this library the following steps are required:

1. Download the R source code from http://cran.r-project.org and save it in a direct directory, e.g., Rsc.
2. From Rsc enter ./config on the shell command line.
3. If there are no errors from the previous step, enter make on the shell command line.
4. Move to the subdirectory src/math/standalone and enter again to make the command.

If things have gone smoothly, you will now have the library libR.h in the standalone directory. The corresponding header file Rmath.h is located in the src/directory where the R source code was downloaded. The library should be placed in the /user/local/lib directory of your unity tree and the header file should be placed in the /user/local/include directory.

# 4.10 USING THE R STANDONE LIBRARY GENERATION OF PSEUDO-RANDOM NUMBERS

The next code uses the R library to evaluate the distribution functions with one degree-of-freedom.

```cpp
//RmathEx1.cpp
#define MATHLIB_STANDONE
#include <iostream>
#include "Rmath.h"

using std::cout;
using std::cin;
using std::endl;

int main() {
    double x1, x2;
    cout << "Enter an argument for the normal cdf:" << endl;
    cin >> x1;
    cout << "Enter an argument for the chi-square cdf:" << endl;
    cin >> x2;

    cout << "Prob(Z <= " << x1 << ") = " << pnorm(x1, 0, 1, 0) << endl;
    cout << "Prob(Chi-2 <= " << x2 << ") = " << pchisq(x2, 1, 0) << endl;
    return 0;
}
```

The primary ingredient in Listing 4.10 is the use of #define MATHLIB_STANDONE at the top of the file. This needs to be placed before the #include statement for Rmath.h because it determines what definitions will be set in the header file.

There is a question of how to determine the arguments for the pnorm and pchisq functions for evaluating the two distribution functions. To accomplish this we look at the two function prototypes in Rmath.h and find them to

double pnorm(double, double, double, int, int);

and

double pchisq(double, double, double, int, int);

By comparing these prototypes to the descriptions on the help pages for the R functions pnorm and pchisq, it can be discerned that

- the double arguments for pnorm are the evaluation point, mean and standard deviation. The two integer arguments are interpreted as logical variables. The first one is 1 or 0 depending on whether a lower or upper tail is evaluated and the second is 1 or 0 depending on whether or not the return value will be the natural log of the probability.
- the double arguments for pchisq are the evaluation point and degrees-of-freedom. The two integer arguments are, logical variables with a value of 1 for the first meaning that lower tail probabilities will be returned and a choice of 0 for the second producing probabilities as the return values.
