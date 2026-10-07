Fault Injection and Failure Monitoring

# Table 26.1
Linear Relations

| Measures | Normal | Stress |
|---|---|---|
| Time | $TTF_o$ | $TTF_s = MTTF_o 	imes CF$ |
| CDF | $F_o(t)$ | $F_s(t) = F_o(\frac{t}{CF})$ |
| Density function | $f_o(t)$ | $f_s(t) = \frac{1}{CF} 	imes f_o(\frac{t}{CF})$ |
| Hazard Function | $\lambda_o(t)$ | $\lambda_s(t) = \frac{1}{CF} 	imes \lambda_o(t)$ |
| MTTF | $MTTF_o$ | $MTTF_s = MTTF_o 	imes CF$ |

which is equal to

```
$MTTF_s = MTTF_o 	imes CF$,
```

when CF is constant, let us summarize these results in Table 26.1.

**Example 26.1.1.** Assume a stress experiment was executed and a sample of hundred times to failure collected. The mean time calculated from the sample was $MTTF_s = 548.3h$. If the acceleration factor is $AF=12$, the mean time to failure at normal operation condition may be estimated using Equation 26.1.2. Hence,

```
$MTTF_o = AF 	imes MTTF_s$
$MTTF_o = 12 	imes 548.3h$
$MTTF_o = 6579.6$.
```

There is a subtle assumption when multiplying test lifetime data by a constant factor since it assumes the lifetime distribution of the system under stress conditions is the same as the lifetime distribution of the system in normal operating conditions. Consequently, the two distributions are considered to have the same shape, which may not be the case [469].

# Non-Constant Scaling

For non-constant scaling factors, the failure rate (and the time to failure) parameters represented in the model. Failure rate increases according to the stresses are commonly related to aging, environmental conditions, and operation stress levels. The following general model

```
$AF = \sum_{i=1}^n B_i 	imes A_i^{(D_i - F_i 	imes s_i)^{E_i}} + C_i$,
```