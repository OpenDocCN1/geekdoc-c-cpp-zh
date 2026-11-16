# Chapter 22

# Term Structure Models

# Contents

| Section | Page |
|---|---|
| 22.1 The Nelson Siegel term structure approximation | 198 |
| 22.2 Extended Nelson Siegel models | 200 |
| 22.3 Cubic spline. | 202 |
| 22.4 Cox Ingersoll Ross. | 205 |
| 22.5 Vasicek | 208 |
| 22.6 Readings | 210 |

We now expand on the analysis of the term structure in chapter 5. As shown there, the term structure is best viewed as an abstract class providing, as functions of term to maturity, the prices of zero coupon bonds (discount factors), yield on zero coupon bonds (spot rates) or forward rates. In the earlier case we considered two particular implementations of the term structure. A flat term structure or a term structure estimated by linear interpolations of spot rates. We now consider a number of alternative term structure models. The focus of this chapter is empirical. we consider ways in which one can specify a term structure in a lower dimensional way. Essentially we are looking at ways of doing curve-fitting, of estimating a nonlinear relationship between time and discount factors, or between time and spot rates. Since the relationship is nonlinear, this is a nontrivial problem. One has to choose a functional form to estimate, which allows enough flexibility to “fit” the term structure, but not so flexible that it violates the economic restrictions on the term structure. Here are some considerations.

+   - Discount factors must be positive. \( (d_t > 0) \). This is because they are prices, negative prices allow for arbitrage.
+   - Discount factors must be a nonincreasing function of time. \( (d_t \ge d_{t+k} \forall k > 0) \). Again, this is to avoid arbitrage.
+   - Nominal interest rates can not be negative. \( (r_t \ge 0 \forall t) \) This is another implication of the absence of arbitrage opportunities.
+   - Both discount factors and interest rates must be smooth functions of time.
+   - The value of a payment today is the payment today. \( d_0 = 1 \).

A number of alternative ways of estimating the term structure has been considered. Some are purely used as interpolation functions, while others are fully specified, dynamic term structure models. Of the models that follow, the approximating function proposed in Nelson and Siegel (1987) and the cubic spline used by e.g. McCulloch (1971) are examples of the first kind, and the term structure models of Cox, Ingersoll, and Ross (1985) and Vasicek (1977) are examples of the second kind.