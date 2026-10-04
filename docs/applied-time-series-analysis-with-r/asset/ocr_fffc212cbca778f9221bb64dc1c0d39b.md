# Other Stationary Time Series Models

# 197

![](bbox=[0.14, 0.123, 0.851, 0.23])

![](bbox=[0.14, 0.237, 0.851, 0.344])

![](bbox=[0.14, 0.352, 0.851, 0.459])

![](bbox=[0.14, 0.467, 0.851, 0.574])

**FIGURE 4.12**nConditional standard deviations for the ARCH(1) realizations in Figure 4.10. (a) $a_1 = 0$. (b) $a_1 = 0.4$. (c) $a_1 = 0.7$, (d) $a_1 = 0.9$.

```
$$\sigma_a^2 = \frac{\alpha_0}{1 - \alpha_1 - \dots - \alpha_{q_0}} \quad (4.25)$
```

# 4.2.2 The GARCH($p_0, q_0$) Process

The ARCH($q_0$) model in Equation 4.23 has been generalized by Brockwell and Davis (1991) and Taylor (1986) to the GARCH($p_0, q_0$) model to include lagged terms of the conditional variance in the model. Specifically, for the GARCH($p_0, q_0$) model, Equation 4.23 is generalized to

```
$a_t = \sigma_{t-1}\epsilon_t , \quad (4.26)$
```