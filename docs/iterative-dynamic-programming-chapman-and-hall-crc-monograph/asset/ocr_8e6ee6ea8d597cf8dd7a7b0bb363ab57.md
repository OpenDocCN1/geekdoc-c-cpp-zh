![](bbox=[0.35, 0.07, 0.64, 0.36])

Figure 11.10: Convergence profile for Example 5, showing ||x(t_f)|| as a function of pass number with penalty function factor θ = 2000

# 11.2.3 Absolute value penalty function

Although for steady state optimization difficult equality constraints are handled very well by the use of quadratic penalty function with shifting terms [13], Luus and Wyrwicz [20] showed that absolute penalty functions can also be used effectively to get accurate optimum results for high-dimensional systems in the presence of difficult equality constraints.

Dadebo and McAuley [3] reported successful results in using in IDP an absolute value penalty function. Therefore, in this section, we consider the augmented performance index in the form

```
J = I + Σ_{i=1}^{k} θ_i |x_i(t_f) - x_i^d| . (11.93)
```

There are k positive weighting factors θ_i, which must be provided by the user, or must be determined during the course of the calculations. One effective method of getting good values for these weighting factors during the course of the calculations is to use the suggestion of Mekarapiruk and Luus [22] where the weighting factors are adjusted after every pass of IDP, being increased in magnitude if the tolerance is not met, and decreased in value if the final state constraint is satisfied within the given tolerance. Thus, after starting with some reasonable values for each θ_i, these penalty function factors are changed after every pass by

```
θ_i^{q+1} = (1 + δ)θ_i^{q}  if  |x_i(t_f) - x_i^d| > ε_i (11.94)
```

```
θ_i^{q+1} = (1 - δ)θ_i^{q}  if  |x_i(t_f) - x_i^d| ≤ ε_i (11.95)
```