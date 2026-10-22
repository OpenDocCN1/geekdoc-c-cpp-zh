![](bbox=[0.05, 0.14, 0.95, 0.46])

Figure 2.10: Rule Block.

translinear principle does not hold, the circuit is found to realize the following nonlinear transformation:

w*_ks = (β_N4t / β_N4b) w_ks [1 + η(w_s) / sqrt(w_ks) ]^2  (2.12)

where function η(w_s) is

η(w_s) = ( Σ_k sqrt(w_ks) / N ) ( sqrt( 1 + ( N I'_SS - Σ_k w_ks ) / ( Σ_k sqrt(w_ks) )^2 ) - 1 )  (2.13)
(I'_SS = (β_N4b / β_N4t) I_SS)

and

w*_k = w*_ks - I*_OS      I*_OS = w*_ks(I_OS)  (2.14)

The offset current I_OS is added to improve the dynamic behavior. Note from Fig.2.10 that it is related to the bias currents in the rule antecedent by