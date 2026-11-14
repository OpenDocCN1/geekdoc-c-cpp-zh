model for the one-factor sampling experiment is given by Equation (5.1), and the analysis of variance table is identical to Table 2.2 in Chapter 2. The $F$-test in the analysis of variance table can be used to test the null hypothesis $H_0 : \sigma_T^2 = 0$ against the alternative $H_a : \sigma_T^2 > 0$.

To estimate the variance components from the ANOVA, the mean squares are equated to their expected values and the simultaneous equations are solved. When the treatment factor is a random factor, as in model (5.1), and there are an equal number of replicates in each level, the $msT$ term in the ANOVA table follows a distribution that is a multiple of the central chi-square distribution. This is different than the model with a fixed effect treatment factor. In that case, described in Section 2.3.5, the distribution of $msT$ was a non-central chi-square. In either case, the $msT$ from the ANOVA can be represented as the quadratic form $\mathbf{y}'\mathbf{Ay}$; and in the random effects model (5.1), Hartley (1967) has shown that its expected value can be written as $\sigma^2 + c\sigma_T^2$, where $c = \sum \mathbf{x}'_i \mathbf{A}\mathbf{x}_i$, and $\mathbf{x}_i$ is an indicator of the $i$th level of $t_i$ (that is the $(i+1)$th column in the $\mathbf{X}$ matrix as shown in Equation (2.6). When there is an equal number of replicates, $r$, in each level of the random factor, the coefficient in the expected mean square simplifies to $c = r$. The method of moments estimators for the variance components can be used when there are equal number replicates in each level of the random factor as shown in Table 5.2, or an unequal number as shown in Table 5.1. For the equal replicates case, the estimates turn out to be uniformly best unbiased estimators, but for the unequal case estimators that are uniformly best do not exist (see Searle et al., 1992).

To illustrate the estimation of the variance components using SAS, the commands to read in the data from the apo measurement sampling experiment, shown in Table 5.1, along with the proc glm commands to produce the ANOVA are shown below.

```
```
data labs;
   input lab $ conc;
   datalines;
   A 1.195
   .
   .
   .
proc glm data=labs; class lab;
   model conc=lab;
   random lab;
run;
```
```

The output is shown at the top of the next page.

The statement random lab tells proc glm that the lab factor is a random factor. By adding this statement the proc glm output includes the additional

table shown below that contains the expected value of $msT$ calculated by Hartley's method.

As shown in Section 2.3.3 the expected value of the $msE$ in the ANOVA Table is $\sigma^2$, therefore two simultaneous equations, in the two unknown vari-