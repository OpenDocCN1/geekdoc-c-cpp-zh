# Applied Time Series Analysis with R

test = factor.wge(phi = c(-0.3,0.44,0.29,-0.378,-0.648))
you will see the following output:

| Factor | Roots | Abs Recip | System Freq |
|---|---|---|---||
| 1-1.6000B+0.9000B^2 | 0.8889+-0.5666i | 0.9487 | 0.0903 |
| 1+0.9000 | -1.1111 | 0.9000 | 0.5000 |
| 1+1.0000B+0.8000B^2 | -0.6250+-0.9271i | 0.8944 | 0.3444 |

+   2. mult.wge(fac1,fac2,fac3,fac4,fac5,fac6) The above functions from ARMA processes require the coefficients phi and theta as input. If you only know the model in factored form, for example,

```
(1-1.6B+.9B^2)(1+.9B)(1+B+.8B^2)Xi = (1+.5B)(1+.95B^3)at,
```

then multiplying the associated polynomials you do not know the components of the vectors phi and theta used in the function calls. The tswge mult.wge can be used to multiply to 6 factors to obtain phi or theta.

fac1 through fac6 are vectors specifying the coefficients of the AR or MA part of the model. If you only have 3 factors, then the call statement is mult.wge(fac1,fac2,fac3).

The function outputs the coefficients of the polynomial resulting from the multiplication of the first and second order factors. The output is in the form of a vector and the associated characteristic polynomial. See example below.

NOTE: This function uses the CRAN package PolymF.

Example: Suppose we want to calculate and plot the true spectral of the ARMA(5,3) model above. The following commands will accomplish:

```
arfac1 = c(1.6,.9)
arfac2 = -.9
arfac3 = c(-1,.8)
mafac1 = -.5
mafac2 = c(0,-.95)
ar = mult.wge(arfac1,arfac2,arfac3)
ma = mult.wge(mafac1,mafac2)
```

For this example, the two calls to function mult.wge create the following output:

```
ar$char.poly: 1 + 0.3*x-.44*x^2-0.29*x^3 + 0.378*x^4 + 0.648*x^5
ar$model.coef: [1] -0.300 0.440 0.290 -0.378 -0.648
ma$char.poly: [1] 1+.0.5*x+.95*x^2 0.475*x^3
ma$model.coef: [1] -0.500 -0.950 -0.475
```