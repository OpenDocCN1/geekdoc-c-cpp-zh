This is the Capital Allocation Line (CAL)—see Section 3.1.1.7.

The slope of this line is the Sharpe Ratio (SR)—see Section 3.1.1.6. It is a measure of the risk premium on the asset per unit risk—as measured by the standard deviation of the asset.

6) Characteristics of a two-asset portfolio with one asset taking short positions to appreciate the economic characteristics of a two-asset portfolio; one may consider the effects of combining two assets to form a portfolio. One can extend the analysis to cases in which short positions may be taken.

First, assume that one may either go long on the risk-free asset lend) or take a short position in it borrow) at the same interest rate, e1.

Let x_A and x_B be the proportions invested in assets A and B, respectively, and let e_A and e_B be their respective returns.

Then, the Expected Return of the whole portfolio, e_p, will be given by

e_p = x_A e_A + x_B e_B

(3.52)

and since

x_A + x_B = 1,

namely,

x_A = 1 - x_B

(3.52) may be written as

e_p = (1 - x_B) e_A + x_B e_B

namely,

e_p = e_A + x_B (e_B - e_A)

(3.53)

The variance of the portfolio, var_p, will be a function of

+   - a) the proportions, x_A and x_B, invested in these assets,
+   - b) their return variances: var_A and var_B and
+   - c) the covariance between their returns: covar_{A-B}.

covar_{A-B} = x_A^2 var_A + x_B^2 var_B + 2 x_A x_B covar_{A-B}

Upon substituting (1 - x_B) for x_A to derive an expression relating the variance of the portfolio to the amount invested in asset B:

var_{A-B} = (1 - x_B)^2 var_A + x_B^2 var_B + 2(1 - x_B) x_B covar_{A-B}
= (1 - 2x_B + x_B^2) var_A + x_B^2 var_B + 2x_B covar_{A-B} - 2x_B^2 covar_{A-B}
= var_A - 2x_B var_A + x_B^2 var_A + x_B^2 var_B + 2x_B covar_{A-B} - 2x_B^2 covar_{A-B}