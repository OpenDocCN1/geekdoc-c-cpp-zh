shown here) on the φ_i’s for the YW estimates in Tables 7.6 and 7.8 do not cover the true parameter values, a much better understanding of the nature of and differences among the fitted models is achieved by examining the factor tables in Tables 7.7 and 7.9.

# EXAMPLE 7.10: ESTIMATING PARAMETERS IN AN ARMA(2,1) MODEL

We consider the use of ML estimates of the parameters of an ARMA(2,1) model fit to the realization in Figure 3.24a of length n = 200 from the model (1 − 1.6B + 0.9B)X_t = (1 − 0.8B)a_t. Table 7.10 shows the ML estimates, which can be seen to be good estimates. The factor table (not shown) reveals that for the true model and the fitted model, the AR characteristic function has complex roots with a system frequency of f = 0.09. However, the complex roots associated with the fitted model are somewhat further from the unit circle than are those in the true model.

# TABLE 7.10

Parameter Estimates for the Realization in Figure 3.24a from the ARMA(2,1) Model (1 − 1.6B + 0.9B²)X_t = (1 − 0.8B)a_t

|  | φ₁ | φ₂ | θ₁ | σₐ² |
|---|---|---|---|---|
| True | 1.6 | -0.9 | 0.8 | 1.0 |
| MLE | 1.56 | -0.83 | 0.88 | 1.05 |

# EXAMPLE 7.11: PARAMETER ESTIMATION FOR SELECTED REAL DATA SETS

In this example we consider the estimation of an AR(9) model fit to the sunspot data in Figure 1.23 (tswge data set ss08) and an ARMA(2,3) model for the log-lynx data in Figure 5.2b. Methods for choosing models are discussed in Chapters 8 and 9.

+   1. Sunspot data: Table 7.11 shows the YW, Burg, and ML estimates for an AR(9) fit to the sunspot data in ss08 using tswge function est.ar.wge. As can be seen, the parameter estimates for all three estimates are similar.
+   
+   The first three rows of the factor table for the MLE fit are shown in Table 7.12 where it can be seen that the dominant behavior is associated with frequency 0.09 which is consistent with the 10–11