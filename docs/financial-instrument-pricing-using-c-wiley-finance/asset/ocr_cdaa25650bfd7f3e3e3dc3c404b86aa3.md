```
*Drezner 1978 Quantlib 1.8     : 0.003199150046013107
*FDM approx                   : 0.003186916800067802
FDM approx extrap             : 0.00319914563772

Max error West/QL: 1.11022302463e-16
Max error Fdm/West: 0.00055286738894
Max error Fdm Extrap/West: 3.32514473067e-07
```

We notice that the finite difference method gives between four and six digits accuracy even when NX = NY = 50.

We can draw the following conclusions based on our experiments:

+   - The West and Quantlib implementations of the Genz algorithms give the same accuracy up to machine precision. We used the finite difference method to check them to ensure that they do not give the same incorrect output for certain values of the parameters.
+   - The added value of the finite difference approach is that it can be tuned to suit our accuracy requirements. The scheme is second-order accurate and we can use Richardson extrapolation to achieve fourth-order accuracy. Furthermore, these schemes deliver a matrix as output which saves recomputing for certain classes of applications.
+   - The finite difference approach can be applied to a wide range of bivariate and trivariate distributions, for example the bivariate-t distribution and the trivariate normal distribution.
+   - The Drezner (1978) algorithm is less accurate than the other schemes and it degrades when ρ = ±1.

We now discuss two more algorithms to compute (16.1) for completeness.

# 16.5 ABRAMOWITZ AND STEGUN APPROXIMATION

A number of methods to compute (16.1) are given in Abramowitz and Stegun (1965). We focus on the specific cases (‘AS 26.3.3’) defined by the nested integral:

```
M(a, b; ρ) = ∫_{-∞}^{a} Z(x)dx ∫_{-∞}^{w(x)} Z(t)dt    (16.7)
```

where:

```
Z(x) = 1/√(2π) e^{-x²/2}
```

and

```
w(x) = (b - ρx)/√(1 - ρ²).
```

We conjecture that this formulation might be easier to compute than other methods. To this end, we write (16.7) in the form:

```
M(a, b; ρ) = ∫_{-∞}^{a} Z(x) N(w(x)) dx    (16.8)
```