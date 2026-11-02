
```
gnuplot> fit f(x) "sg_e0_L.dat" via e,a,b
```

Then gnuplot writes log information to the output describing the fitting process. After the fit has converged it prints for the given example:

```
After 8 iterations the fit converged.
final sum of squares of residuals : 7.55104e-06
rel. change during last iteration : -2.54894e-10

degrees of freedom      (FIT_NDF)          : 5
rms of residuals        (FIT_STDFIT) = sqrt(WSSR/ndf) : 0.00122891
variance of residuals   (reduced chisquare) = WSSR/ndf : 1.51021e-06
```

| Parameter | Final set of parameters | Asymptotic Standard Error |
|---|---|---|
| e | = -1.78786 | +/- 0.0008548 (0.04781%) |
| a | = 2.54248 | +/- 0.2282 (8.976%) |
| b | = -2.80103 | +/- 0.08264 (2.951%) |

correlation matrix of the fit parameters:

|  | e | a | b |
|---|---|---|---|
| e | 1.000 |  |  |
| a | 0.708 | 1.000 |  |
| b | -0.766 | -0.991 | 1.000 |

The most interesting lines are those where the results θ̂ for your parameters along with the standard error bar are printed.23 Additionally, the quality of the fit can be estimated by the information provided in the three lines beginning with "degree of freedom". The first of these lines states the number of degrees of freedom, which is just n − n_p. As visible in the brackets, within gnuplot this is available in the variable FIT_NDF:

```
gnuplot> print FIT_NDF
5
```

The mean-squared difference χ²_N is denoted as WSSR in the gnuplot output. The root of this mean-squared difference per degree of freedom is stored in the gnuplot variable FIT_STDFIT.

> 23 "These "error bars" are calculated in a way which is in fact correct only when fitting linear functions; hence, they have to be taken with care.

A measure of quality of the fit is the probability Q that the value of the mean-squared difference is equal or larger compared to the value from the current fit, given the assumption that the data points are distributed as in Eq. (8.97) [Press et al. (1995)]. The larger the value of Q, the better is the quality of the fit. As mentioned above, Q can be evaluated from a chi-squared distribution with n − n_p degrees of freedom. Since the cumulative chi-squared distribution is related to the normalized incomplete gamma function, which is available in gnuplot, one can evaluate Q directly in gnuplot:

```
gnuplot> Q = 1 - igamma(0.5 * FIT_NDF, 0.5 * FIT_NDF*FIT_STDFIT**2)
```

Note that in this case we obtain Q = 1, which is so large, because σ_r = 1 was used, see below.

To watch the result of the fit along with the original data, just enter

```
gnuplot> plot "sg_e0_L.dat" w e, f(x)
```

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_388_0.png)

Fig. 8.48 Gnuplot window showing the result of a fit command along with the input data.

The result is displayed in Fig. 8.48. Please note that the convergence depends on the initial choice of the parameters. The algorithm may be trapped into a local minimum in case the parameters are too far away from the best values. Try the initial values e=1, a=-3 and b=1! Furthermore, not all function parameters have to be subjected to the fitting. Alternatively, you can set some parameters to fixed values and omit them from the via list at the end of the fit command. Remember that in the above example all data points enter into the result with the same weight, i.e. σi = 1 ∀i is assumed. You can tell the algorithm to consider the error bars, for example supplied in the third column, by typing

```
gnuplot> fit f(x) "sg_e0_L.dat" using 1:2:3 via e,a,b
```

Then, data points with larger error bars have less influence on the results. In this case a different result with smaller value of Q will arise (try it !). You can also restrict the data points which are considered for the fit, which is applicable if only a subset of the sample follows the function law you are considering. This can be done in the same way as restricting the range of plotted values, for instance using

```
gnuplot> fit [5:12] f(x) "sg_e0_L.dat" using 1:2:3 via e,a,b
```

In some cases, it is clear that some parameters to be fitted fall into a certain range, e.g. a parameter must be larger than zero. Within gnuplot, one cannot explicitly state constraints to fitting parameters. Instead, this can be achieved via using suitable functions.

| GET SOURCE CODE |
|---|
| DIR: randomness |
| FILE(S): parabola.dat |
| fit_restricted.gp |

Consider for example that you measure in a simulation the magnetization m of a metal as function of an applied field B. Clearly, the magnetization can on average only increase with the field. But due to statistical fluctuations, for very small fields, you may sometimes actually measure a small decrease, as visible in the example data file parabola.dat. Now, you want to extract the so-called susceptibility χ = dm/dB|B→0 via fitting a parabola m(B) = m0 + b B + c B²:

```
gnuplot> m(x)=m0+b*x+c*x*x
gnuplot> m0=1
gnuplot> b=1
gnuplot> c=1
gnuplot> fit m(x) "parabola.dat" u 1:2:3 via m0,b,c
```

This will result in a negative value for the susceptibility χ =b:

Final set of parameters
Asymptotic Standard Error

m0 = 1.20905 +/- 0.03342 (2.765%)
b = -0.0576451 +/- 0.25 (433.6%)
c = 3.0935 +/- 0.3017 (9.753%)

Notice the large error bar given for b which is compatible with zero. One can restrict the coefficient of the linear term via using the exponential function, which can only take positive values:

```
m2(x)=m2+exp(b2)*x+c2*x*x
m2=1
b2=-10
c2=1
fit m2(x) "parabola.dat" u 1:2:3 via m2,b2,c2
```

resulting in

Final set of parameters          Asymptotic Standard Error
m2 = 1.20357 +/- 0.03354 (2.786%)
b2 = -10.5721 +/- 9840 (9.308e+04%)
c2 = 3.02815 +/- 0.3027 (9.996%)

Thus, the resulting value of b2 will be negative, i.e., the effective value of the linear coefficient is close to zero but positive: b = exp(b2) = 2.6 × 10⁻⁵. Note that here the effect is rather small, the resulting function m2(B) cannot be distinguished from m(B). But for other cases, in particular when the fit converges to something completely off the data, which sometimes happens, restricting the values of fitting parameters as shown above can help a lot. For stronger restrictions, e.g. within an interval [b0, b1], the application of other functions may help. For example, the tanh(), which is available in gnuplot as well, is limited to the range [-1,1]. Therefore, identifying b ≡ (b0 + (b1 - b0)) tanh(b̃)+1)/2) and fitting b̃ will give the desired restriction for b.

Finally, we discuss multi-branch fitting. This means that several function sharing one or more parameters, possibly having also individual parameters in addition, are fitted to several independent data sets.

| GET SOURCE CODE |
|---|
| DIR: randomness |
| FILE(S): exp1.dat |
| multi_fit.gp |

As an example, we consider the case of three exponential functions f_i(x) = a_i exp(-x/μ) (i = 1,2,3), which have different prefactors but share the same parameter μ. We want to fit the three functions, i.e., determine

the values of the parameters a0, a1, a2, and μ, to three sets of data generated from exponential distributions with three different values of a lower cutoff, but all exhibiting the parameter μ = 1. To make this multi-branch fitting work within gnuplot, all three data sets have to be contained in one single file, exp1.dat here, separated by blank lines. First, we define the three functions:

```
gnuplot> f0(x)=a0*exp(-x/mu)
gnuplot> f1(x)=a1*exp(-x/mu)
gnuplot> f2(x)=a2*exp(-x/mu)
```

Next, we have to combine these three functions into a single function, f(x,s) where the first argument is the same argument as to the functions f0(x), f1(x), f2(x). The second argument s is used to select among the three functions. For this purpose, we first define an auxiliary function delta(a,b), which returns 1 if a=b and 0 else. The definition of the function uses the conditional operator (see page 20) as known from the programming language C. This delta(a,b) is used for the actual definition of f(x,s):

```
gnuplot> delta(a,b) = (a==b) ? 1 : 0
gnuplot> f(x,s) = delta(s,0)*f0(x)+delta(s,1)*f1(x)+delta(s,2)*f2(x)
```

From gnuplot 4.4 onwards, you can use as an alternative the value command, which takes any string as the name of a variable and returns the value assigned currently to the variable. For our example the command can be used in the following way:

```
gnuplot> f(x,s) = value(sprintf("a%d",s))*exp(-x/mu)
```

Note that all given gnuplot commands are collected in multi_fit.gp and can be executed using gnuplot multi_fit.gp. The fit is performed such that the first column is used as x argument. The argument s is the index of the current data file exp1.dat. This can be taken automatically from the data file via stating the "column number" -2 in the second column of the using part of the fit command, stating the function value at the third column, and the error bars as fourth column

```
gnuplot> fit f(x,s) "exp1.dat" using 1:-2:2:3 via a0,a1,a2,mu
```
