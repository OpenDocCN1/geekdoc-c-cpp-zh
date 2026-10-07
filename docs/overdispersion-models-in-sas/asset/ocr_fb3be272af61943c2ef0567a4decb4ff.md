# Chapter 10 Generalized Linear Overdispersion Mixed Models 361

| Label | Estimate | Standard Error | DF | t Value | Pr > |t| | Alpha | Lower | Upper |
|---|---|---|---|---|---|---|---||}{
| PI_1 | 0.1108 | 0.007683 | 399 | 14.43 | <0001 | 0.05 | 0.09573 | 0.1259 |
| PI_2 | 0.0720 | 0.005539 | 399 | 13.00 | <0001 | 0.05 | 0.06111 | 0.08289 |
| OR | 1.6065 | 0.09668 | 399 | 16.62 | <0001 | 0.05 | 1.4164 | 1.7966 |
| Rho*Rho | 0.1471 | 0.01835 | 399 | 8.01 | <0001 | 0.05 | 0.1110 | 0.1831 |
| Sigma*Sigma | 1.4715 | 0.01586 | 399 | 9.28 | <0001 | 0.05 | 1.1597 | 1.7883 |

Table 10.5 shows the estimates and standard errors of the Beta-binomial GLOMM of equation (10.5) as obtained from the NLMIXED procedure. The reader can verify that the parameter estimates (for '-2 Log Likelihood obviously') are very close to the underlying parameters.

# #### Table 10:5: Parameters Estimates and Standard Errors of the Beta-binomial GLOMM

| Parameter | Estimate | Standard Error |
|---|---||}{
| -2 Log Likelihood | 3229.6 | -- |
| $\pi_1$ | 0.1108 | 0.0077 |
| $\pi_2$ | 0.0720 | 0.0055 |
| Odds-ratio | 1.6065 | 0.0967 |
| $\rho^2$ | 0.1471 | 0.0184 |
| $\sigma^2$ | 1.4715 | 0.1586 |

We now to the Random-clumped GLOMM

```
$t_{ij} \text{ given } (x_{ij}; u_{ij}) \sim \text{Random-clumped Binomial}(\pi_i; \rho; m_{ij}),\n\log (\pi_{ij}) = \beta_0 + \beta_1,x_{ij} + u_{ij}$ (10.16)
```

with parameters used in the previous BB GLOMM: $\pi_i = 0.12, \pi_2 = 0.08, \rho^2 = 0.15, \sigma = 1.2$ and $m_{ij} = 20$. The programming statements for analyzing the RZ GLOMM data are provided in Program 10.5. As before, we obtain initial estimates of the beta parameters and the variance component using a GLMM model where subjects are treated as random. This is obtained using the GLIMMIX procedure. The Random-clumped GLOMM is then fit via the NLMIXED procedure with initial values defined by a grid based on the GLMM beta estimates. Selected results from Program 1.5 are shown in Output 10.5.