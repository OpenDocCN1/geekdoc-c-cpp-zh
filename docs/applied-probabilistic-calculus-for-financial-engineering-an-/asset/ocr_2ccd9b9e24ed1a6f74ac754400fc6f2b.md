View (2): INTC will outperform AMZN by 1.75% per month.

+   - The difference in implied excess returns is 0.18% per month.
+   - We would expect that incorporating our view would increase our holdings of INTC and reduce our holdings of AMZN.

The views expressed above are relative views of assets.

# *Incorporating Our Views:*

To link our views to implied excess returns, we need a link matrix, P.

Matrix P is constructed in the following way:

Each row represents a view, each column represents a company

| | INTC | AEP | AMZN | MRK | XOM |
|---|---|---|---|---|---|
| View 1 | 0 | 1 | 0 | 0 | -1 |
| P = | [ | | | | | ] |
| View 2 | 1 | 0 | -1 | 0 | 0 |
| View 3 | 0.5 | 0 | 0.5 | -0.5 | -0.5 |

# *The View Vector and Uncertainty*

What do Q and Ω look like?

Q + ε = [ |Q₁| ; |Qₖ| ] + [ |ε₁| ; |εₖ| ] → Q + ε = [ 0.01 ; 0.0175 ] + [ ε₁ ; ε₂ ]
View 1 ↓
View 2 ↑

where
[ε₁]   ([0] [ω₁₁ … ω₁ₖ])
[ : ] ~ N ([ : ] ; [ : ] … ; [ : ])
[εₖ]   ([0] [ωₖ₁ … ωₖₖ])
Ω

# **Calculating Ω**

There is no best way to calculate Ω. It will depend on how confident you are of your predictions.

Black and Litterman recommend
Base ⇒ Ω = τ P S Pᵀ , where P = Link matrix and S = variance—covariance matrix