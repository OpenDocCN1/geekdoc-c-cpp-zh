
# 132 GENERATION OF PSEUDO-RANDOM NUMBERS

789\Your random numbers are
1.22472 2.50259 0.159843 0.1064

Similar to what was done for the FM2 generator, driverExp was used with seeds 123, 456, 789 to generate a random sample of 500 values from the exponential distribution with unit mean that was imported into R as a numeric vector object eDat. The following information was obtained about the data.

```
> summary(eDat)
Min. 1st Qu. Mean 3rd Qu. Max.
0.001526 0.258000 0.657300 0.980200 1.300000 8.784000
```

- sd(eDat)
[1] 1.06676
- [1] IQR(eDat)
[1] 1.042139
- [1] pnorm(length(eDat))*mean(eDat) - 1)
[1] 0.326831
- ks.test(eDat, pexp)

One-sample Kolmogorov-Smirnov test
data: eDat
D = 0.0402 p-value = 0.3954
alternative hypothesis: two-sided

The R function was invoked in this session to calculate some of the basic statistics for the imported data. Information is augmented with the sample standard deviation (using the sd) and sample inter-quartile range (IQR). As the data was produced using an input value of 1 for λ, both the mean and the variance of the parent population are the mean and inter-quartile range, approximately, 6.93 and 1.1 (Exercise 4.18). As a result, the sample statistics are more or in agreement with what might be expected. Although the outcome is outside, a normalized (multiplication by the square root of the sample size) difference between the sample mean and I computed that behave like a number drawn from the standard normal distribution if the values come from an exponential distribution with λ=1. The p-value obtained using the cumulative distribution pnorm for the normal distribution is not significant and the Kolmogorov-Smirnov goodness-of-fit test detects no significant departure from the exponential model. The histogram of the data in Figure 4.3 shows the J-shape that would be expected from exponentially distributed data.

If F has a closed form, but there is no closed form for F⁻¹, Algorithm 4.1 can still be used with the quantile function evaluated by numerical methods (ec, Exercise 8.26). When there is no closed form for F, as is true for the normal distribution, the cdf itself can be approximated numerically using, eg, numeric integration and the same basic approach can be applied to the approximation. There is an alternative, less involved, strategy that we will now describe.

As before, the problem is that of simulating from a continuous random variable with density f. However, now it is assumed that there is another density g with the property that for all numbers x

```
f(x) \le cg(x)
```

for constant c ≥ 1. The g density is sometimes referred to as the instrumental density with f being the target density. The basic accept-reject algorithm takes the

The justification for the accept-reject approach is provided by Theorem 4.4.

# GENERATION OF PSEUDO-RANDOM NUMBERS

**Theorem 4.4.** *Let $Y$ have density $g$ satisfying (4.13) and let $U$ be conditional on $Y=y$ have a uniform distribution on $[0, cg(y)]$. Then, $X=Y[U < f(Y)]$ has density $f$.*

*Proof.* Theorem 4.4 can be found in Devoye (1986) and Robert and Casella (2004), for example. The idea is that if $A$ is any open interval of the real line

```
$Prob(X \in A) = Prob(Y \in A[u \leq f(Y)])
= \int_A \int_0^{cg(y)} cg(y)du = \int_{-\infty}^{\infty} \int_0^{f(y)} f(y)g(y)dy = \int_A f(y)dy$
```

which proves the theorem.

Note that Theorem 4.4 first to generate a value $y$ from the density $g$ and then generate a uniform number on $[0, cg(y)]$. But, it suffices to generate from the interval $[0, 1]$ and then multiply by $cg(y)$ the quantile function for random variable on $[0, \theta]$, $Q(u)=bu$ for $u \in [0, 1]$ and $b>0$. Thus, the plan is (i) generate $y$ from a distribution with density $g$, (ii) generate $u$ from a uniform distribution on $[0, 1]$ and then take $y$ as the desired value if $cg(y)u \leq f(y)$ or, equivalently, $ru \leq 1$ in our original formulation.

A measure of an accept-reject algorithm is provided by the number of rejections that are required to actually generate a random number from the target distribution. $U$ and $Y$ are in Theorem 4.4. Then, on any given the probability of acceptance is

```
$Prob(U \leq f(Y)) = \int_{-\infty}^{\infty} \frac{f(y)}{cg(y)}g(y)dy = 1/c$
```

and the number of trials before the first acceptance has a geometric distribution with success probability $c^{-1}$. The value of $c$ extends the extent to which $g$ is able to approximate $f$. Consequently, the accept-reject algorithm will benefit from a careful choice of $g$ that allows us to take $c$ close to one.

An illustration of an accept-reject method can be obtained using the Cauchy density to generate standard normal variables. The Cauchy density scale parameter $\sigma>0$ has this

```
$g(x) = \frac{1}{\pi(1+x^2/\sigma^2)}, -\infty < x < \infty, \sigma>0$ (4.14)
```

for which the quantile function is

To use $g$ for simulating the standard normal distribution it is necessary to find a value $c \geq 1$ for which $f(y)/g(y) \leq c$

```
$f(x) = \frac{1}{\sqrt{2\pi}}exp\{-x^2/2\}$.
```

Proceeding in Section 3.2 of Devoye (1986) we will find the smallest number that $f(x) \leq cg(x)$. This choice will be the one that, on the average, will lead to few rejections and thereby to faster sample generation.

The ratio $f(x)/g(x)$ will achieve a maximum when $(1+x^2/\sigma^2)exp\{-x^2/2\}$. It is equivalent to maximize the logarithm of this ratio which is tantamount to finding the solutions of $2x=(\sigma^2+x^2)$; namely, $x=0$ and $x=\pm\sqrt{2-\sigma^2}$. The two roots are only applicable when $\sigma\sqrt{2}$ in which case the maxima are at $\pm\sqrt{2-\sigma^2}$ corresponding to

# NONUNIFORM

a maximum value of $c=\sqrt{2\pi}\exp\{\sigma^2/2 - 1\}/\sigma$ for $f/g$. For $f/g$ is $\sigma=\sqrt{2}$.

The code below is the header file for WHCauchy that uses accept-reject method to generate standard normals.

```
// WHCauchy.h
#ifndef WHCAUCHY_H
#define WHCAUCHY_H

class WHCauchy {
    double a1, a2, a3;
    unsigned long m1, m2, m3;
    double g(double x) const;
    double Ginv(double x) const;
    double f(double x) const;

public:
    WHCauchy();
    void range(unsigned long seed1, unsigned long seed2, int n, double* pNorm) const;
};
#endif
```

```
// WHCauchy.cpp
#include <cmath>
#include <iostream>
#include "WHCauchy.h"

using std::cout;
using std::endl;

double pi = acos(-1.0);
double sqrtpi = sqrt(2.*pi);
double c = sqrt(2pi);

WHCauchy::WHCauchy() {
    a1 = pi; a2 = sqrtpi; a3 = 1;
    m1 = 2; m2 = 0; m3 = 0;
}

void WHCauchy::range(unsigned long seed1, unsigned long seed2, int n, double* pNorm) {
    double temp, y;
    double u[2];
    int nFill = 0, iAccept, nReject = 0;

    while(nFill < n){
        iAccept = 0;
        while(iAccept == 0){
            for(int i = 0; i < 2; i++){
                seed1 = a1*seed1; seed2 = a2*seed2; seed3 = a3*seed3;
                temp = ((double)seed1)/((double)m1)
                        + ((double)seed2)/((double)m2)
                        + ((double)seed3)/((double)m3);
                if(temp > 2.) temp -= 2;
                if(temp > 1.) temp -= 1;
            }
            u[i] = temp;
            y = Ginv(u[i]);
            if(c*y < f(y)){
            pNorm[nFill] = y;
            nFill++;
            iAccept++;
        } else nReject += 1;
    }
    }
    cout << "The Number of rejections was " << nReject << endl;
}

double WHCauchy::g(double x) const {
    return 1/(1 + x*x)*pi;
}

double WHCauchy::Ginv(double u) const {
    return tan(pi*(u -.5));
}

double WHCauchy::f(double x) const {
    return exp(-5.*x*x)/sqrtpi);
}
```

![](img/b50973a0535e1d499ab735f151.png)

# 136 GENERATION OF PSEUDO-RANDOM NUMBERS

```cpp
int nFill = 0, iAccept, nReject = 0;

while(nFill < n){
    iAccept = 0;
    while(iAccept == 0){
        for(int i = 0; i < 2; i++){
            seed1 = a1*seed1; seed2 = a2*seed2; seed3 = a3*seed3;
            temp = ((double)seed1)/((double)m1)
                    + ((double)seed2)/((double)m2)
                    + ((double)seed3)/((double)m3;
            if(temp > 2.) temp -= 2;
            if(temp > 1.) temp -= 1;
        }
        u[i] = temp;
        y = Ginv(u[i]);
        if(c*y < f(y])){
            pNorm[nFill] = y;
            nFill++;
            iAccept++;
        } else nReject += 1;
    }
}
cout << "The Number of rejections was " << nReject << endl;
```

There are a few features that merit discussion in this listing. First, at the beginning of the listing three constants are defined: π,√2π and the optimal constant for use with the Cauchy instrument. This allows them with global scope as discussed in Section 3.2. That is, by defining pi, sqrt outside the scope of function in the program they become available to all functions that may need them removing the need to compute more than.

The algorithm works through a while loop that terminates when nFill, the number of samples that have been accepted, coincides with the desired sample size. A variable that counts the number of rejected samples has also been included to assess the efficiency of using the Cauchy distribution for generation of samples from the normal distribution.

It turns out that most of the distributions that use in statistics are tied to the chi-square/or normal distributions. For example, a random variable from the F-distribution can be obtained as the ratio of two independent chi-square random variables by their degrees-of-freedom while a random variable from the t-distribution can be created as the
