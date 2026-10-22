Recently some defuzzification methods have been introduced which considerably simplify calculation of the output value: the rules are aggregated and defuzzification is performed in a single operation, bypassing calculation of the fuzzy output set [23].

Let us see the equations used to calculate the fuzzy inferences in greater detail.

Each rule has I antecedents. For the generic r-th rule, the i-th antecedent, P_ir, has the following form:

```
P_ir = X_i IS FS_ir  (8.6)
```

X_i is the i-th input and is crisp. That is, X_i is the particular fuzzy set that is always null except for a precise numerical value x_i. FS_ir is a fuzzy set. It has a Gaussian membership function μ_FS_ir(x), univocally determined by a centre, c_ir, and a parameter, γ_ir, linked to the variance according to the following equation:

```
μ_FS_ir(x) = e^{-γ_ir^2 (x - c_ir)^2}  (8.7)
```

Considering the crisp nature of the inputs, the degree of truth, α_ir, of the generic antecedent P_ir is:

```
α_ir = e^{-γ_ir^2 (x_i - c_ir)^2}  (8.8)
```

We always used the connector AND, as calculated by Zadeh, between the various antecedents. So the degree of truth, θ_r, of the r-th rule is the lowest of all the degrees of truth, α_ir, of the antecedents belonging to the rule:

```
θ_r = min_{i=1}^I (α_ir)  (8.9)
```

As regards the conclusion of the rules, a numerical output value, C_r, is associated with each rule.

The analytical expression of the defuzzification method adopted, called Weighted Sum (WS) defuzzification [23], is:

```
y = Σ_{r=1}^R C_r θ_r  (8.10)
```

Figure 8.1 shows a practical example of calculation of a fuzzy inference made up of only two rules.