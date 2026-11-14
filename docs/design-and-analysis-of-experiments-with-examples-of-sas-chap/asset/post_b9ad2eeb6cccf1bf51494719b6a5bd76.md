
This results in the following randomized list.

| experiment | BW | WL |
|---|---|---|
| 1 | 3.25 | 4 |
| 2 | 3.75 | 6 |
| 3 | 4.25 | 4 |
| 4 | 4.25 | 6 |
| 5 | 3.25 | 6 |
| 6 | 3.25 | 5 |
| 7 | 3.75 | 5 |
| 8 | 3.75 | 6 |
| 9 | 3.75 | 4 |
| 10 | 3.25 | 4 |
| 11 | 3.25 | 6 |
| 12 | 4.25 | 4 |
| 13 | 3.25 | 5 |
| 14 | 3.75 | 6 |
| 15 | 4.25 | 6 |
| 16 | 3.25 | 4 |
| 17 | 4.25 | 5 |
| 18 | 3.25 | 6 |

This list shows that the first experiment consists of constructing a helicopter with a body width of 3.25” and a wing length of 4”, dropping it from a fixed height and timing its flight. The second experiment consists of constructing a helicopter with a body width of 3.75” and a wing length of 6”, dropping it from the same fixed height and timing its flight, etc. The randomization will help prevent biases from any lurking variables such as changes in air currents, changes in temperature or learning curves in dropping or timing helicopters. This randomized list could be converted to a double spaced data collection form as shown in the example in Section 2.2.

By utilizing proc factex a more compact set of commands can be obtained for creating a randomized list for a factorial design. The commands below will produce a randomized list in the file copter that is similar to that shown above.

```
proc factex;
   factors BW WL/nlev=3;
   model estimate=(BW|WL);
   output out=copter randomized designrep=2
   BW nvals=(3.25 3.75 4.25) WL nvals=(4 5 6) ;
run;
proc print data=copter;
run;
```

The nlev=3 option on the factors statement specifies three levels for body width and wing length. The default number of levels in proc factex is 2. The estimate(BW|WL) specifies that the design should allow estimation of the body width and wing length main effects and their interaction. Finally the output statement lists the list in the file. The designrep option specifies two replicates of each combination of factor levels, the randomize option randomizes the order of the list and the `nvals=` option specifies numerical values for the levels of the two factors. If the levels were qualitative like (low, mid, high), the `cvals=('low' 'mid' 'high')` option could be used instead of `nvals`. For a full factorial `proc factex` produces no output itself. Therefore `proc print` command is used to print the randomized list.

## 3.5 Analysis of a Two-Factor Factorial in SAS

The mathematical model for a completely randomized two-factor factorial design can be written as:

```
y_{ijk} = \mu_{ij} + \epsilon_{ijk} (3.1)
```

where i represents the level of the first factor, j represents the level of the second factor, and k represents the replicate number. This model is called the cell means model and \mu_{ij} represents the expected response in the ijth cell.

Another way of representing the model is the effects model

```
y_{ijk} = \mu + \alpha_i + \beta_j + \alpha\beta_{ij} + \epsilon_{ijk} (3.2)
```

In this model \alpha_i, \beta_j are the main effects and represent the difference between the marginal average of all experiments at the ith level of the first factor and the overall average, and the difference between the marginal average at the jth level of the second factor and the overall average, respectively. The interaction effects, \alpha\beta_{ij}, represent the difference between the cell mean, \mu_{ij} and \mu + \alpha_i + \beta_j.

The usual assumptions are that the experimental errors are independent and \epsilon_{ijk} \sim N(0, \sigma^2). The independence assumption is guaranteed if the treatment combinations are randomly assigned to the experimental units, and the equal variance and normality assumptions can be verified with a residual versus predicted plot and a normal probability plot of the residuals as described in Section 2.4.

Estimable functions, as described for the one-factor model in Section 2.3.4, are linear combinations of the cell means that can be expressed as a linear combination of the data. For the two-factor factorial the cell means, \mu_{ij} = \mu + \alpha_i + \beta_j + \alpha\beta_{ij}, are estimable functions but the individual effects, \alpha_i, \beta_j, and \alpha\beta_{ij} are not estimable functions. Contrasts among the effects such as \sum_i c_i \alpha_i, and \sum_j c_j \beta_j, where \sum_i c_i = 0, \sum_j c_j = 0 and \sum_i \sum_j b_{ij} \alpha\beta_{ij}, where \sum_i b_{ij} = 0, \sum_j b_{ij} = 0 are estimable. These estimable functions and their standard errors can be computed with the `estimate` command in SAS `proc glm`. The marginal means \mu + \alpha_i + \bar{\alpha\beta}_i and \mu + \beta_j + \bar{\alpha\beta}_j are estimable functions and they and the cell means can be computed using the `means` or `lsmeans` statement in SAS `proc glm`.

### 3.5.1 Matrix Representation of Model and Analysis

The effects model can be represented in matrix notation as

\( y = X\beta + \epsilon = (1 \mid X_A \mid X_B \mid X_{AB}) \begin{pmatrix} \mu \\ \beta_A \\ \beta_B \\ \beta_{AB} \end{pmatrix} + \epsilon \quad (3.3) \)

For example, consider a case where the first factor has two levels, the second factor has three levels, and there are two replicates per cell. Then

\(\begin{pmatrix} y_{111} \\ y_{112} \\ y_{211} \\ y_{212} \\ y_{121} \\ y_{122} \\ y_{221} \\ y_{222} \\ y_{131} \\ y_{132} \\ y_{231} \\ y_{232} \end{pmatrix} = \begin{pmatrix} 1 & 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\ 1 & 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} \mu \\ \alpha_1 \\ \alpha_2 \\ \beta_1 \\ \beta_2 \\ \beta_3 \\ \alpha\beta_{11} \\ \alpha\beta_{21} \\ \alpha\beta_{12} \\ \alpha\beta_{22} \\ \alpha\beta_{13} \\ \alpha\beta_{23} \end{pmatrix} + \begin{pmatrix} \epsilon_{111} \\ \epsilon_{112} \\ \epsilon_{211} \\ \epsilon_{212} \\ \epsilon_{121} \\ \epsilon_{122} \\ \epsilon_{221} \\ \epsilon_{222} \\ \epsilon_{131} \\ \epsilon_{132} \\ \epsilon_{231} \\ \epsilon_{232} \end{pmatrix}\)

The \( X'X \) is singular and to solve the normal equations SAS proc glm uses a generalized inverse, \( (X'X)^- \) which is equivalent to placing the restriction \( \alpha_2 = \beta_3 = \alpha\beta_{22} = \alpha\beta_{32} = 0 \). This is the same thing that was done to get a solution for the one-factor model in Sections 2.3.1 and 2.3.2. The error sum of squares \( ssE = y'y - \beta'X'y = y'(I - X(X'X)^-X')y \), where \( \hat{\beta} = (X'X)^-X'y \) are the estimates that proc glm designates as biased. To test the hypothesis \( H_0: \alpha_1 = \alpha_2 = 0 \), \( H_0: \beta_1 = \beta_2 = \beta_3 = 0 \) and \( H_0: \alpha\beta_{11} = \alpha\beta_{21} = \alpha\beta_{22} = \alpha\beta_{32} = 0 \), the likelihood ratio F-tests are obtained by calculating ratios of the ANOVA means squares. What SAS proc glm designates as the type I sums of squares for factor A is \( ssA = \hat{\beta}'X'y - (1'y)^2/(1'1) \), where the model is simplified to include only the effects for the first factor, i.e., \( X = (1 \mid X_A) \). The error sums of squares for this simplified model is \( ssE_A \). The type I sums of squares for factor A is denoted \( R(\alpha|\mu) \). The type I sums of squares for factor B is denoted R(β|α, μ)=ssE_A - ssE_B where ssE_B is the error sums of squares from the reduced model where X = ( 1 | X_A ) | X_B . Finally, the type I sums of squares for the interaction AB is denoted R(α, β|α, μ) = ssAB - ssE . In general when there are a levels of factor A, b levels of factor B, and r replicates per cell, the type I ANOVA Table for the two-factor factorial design can be represented symbolically as shown in Table 3.2.

### Table 3.2 Analysis of Variance Table

| Source | df | Sum of Squares | Mean Squares | F-ratio |
| :--- | :--- | :--- | :--- | :--- |
| A | a - 1 | R(α|μ) | ssA / (a-1) | F = msA / msE |
| B | b - 1 | R(β|α, μ) | ssB / (b-1) | F = msB / msE |
| AB | (a - 1)(b - 1) | R(α|β, α, μ) | ssAB / ((a-1)(b-1)) | F = msAB / msE |
| Error | ab(r - 1) | ssE | ssE / (ab(r-1)) | |

The sums of squares ssA, ssB, and ssAB can also be written in the form

```
ssA = (L_A β̂)'(L_A (X'X)^- L_A')^-1 (L_A β̂)
ssB = (L_B β̂)'(L_B (X'X)^- L_B')^-1 (L_B β̂)
ssAB = (L_αβ β̂)'(L_αβ (X'X)^- L_αβ')^-1 (L_αβ β̂)
```

where L_A, L_B and L_αβ are contrast matrices computed internally by SAS proc glm, see Goodnight (1980). Under the null hypotheses the F-ratios msA/msE, msB/msE and msAB/msE follow the F-distribution with the degrees of freedom shown in the table, and under the alternative they follow the noncentral F-distribution. The noncentrality parameter for F = msA/msE is given by the expression λ_α = (σ²)^-1 (L_A β̂)'(L_A (X'X)^- L_A')^-1 (L_A β̂). The non-centrality parameters for the F-ratios msB/msE and msAB/msE are similarly given. When there is an equal number, r, of replicates in each cell, the noncentrality parameters can be shown to be equal to

```
λ_α = br Σ_i α_i² / σ²      (3.4)
λ_β = ar Σ_j β_j² / σ²      (3.5)
```

and

```
λ_αβ = r Σ_i Σ_j α_ij² / σ²   (3.6)
```

To illustrate the analysis of a two-factor factorial experiment in using SAS proc glm consider the data in Table 3.3. These are results of a two-factor experiment given by Hunter (1989). In this data, an experiment consisted
