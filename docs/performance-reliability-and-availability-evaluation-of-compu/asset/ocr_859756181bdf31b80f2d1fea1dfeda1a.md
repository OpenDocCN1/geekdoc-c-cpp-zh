# Fault Injection and Failure Monitoring

There are numerous accelerated stress models. Most of these models are either statistical or physics-based models [124, 269, 469].

Environmental stresses are generally related to (1) natural stress, circumscribed by the geographic area, meteorological conditions, and (2) induced stress situations. The latter may be directly or indirectly induced to mimic stress exposures due to environmental conditions. These environmental stimuli bait the creation of harsh circumstances that lead to changes in failure or lifetime under a normal state. The most common scenarios of interest are that represent failure factors. For example, if corrosion failures occur at typical temperatures and humidities, then identical correlation is likely to arise much faster in a humid laboratory at high temperatures. The testing activity that accelerates the fault phenomenon is called fault acceleration. It is worth noting that physical models may be appealing choices for representing well-known failure phenomena. However, the relations between accelerating factors and the actual failure are usually complex. In practical cases, simpler models may suffice when plausible constraints are adopted. On the other hand, empirical models may be an attractive modeling approach when the chemical or physical failing processes are not well known. However, the analyst should be careful when adopting models for extrapolation.

Scaling factors (usually called acceleration factors AF) or its inverse, time scaling factors (usually called CF = 1/AF), are functions that assign to faults' events which represent primary parameters to accelerated life testing. The acceleration factors speed up systems' or devices' degradation and allow one to estimate the failure rate - λ - (or the time to failure - TTF) under stress circumstances due to temperature, voltage, humidity, mechanical wear-out, memory leaking, etc. A suitable choice of such factors, AF or CF, supports extrapolating the failure rate (or the time to failure) to a given specific operation. The acceleration factor is defined as the ratio between the average failure rate at state condition 1 - stress (λ₁ or λ₂) and the average failure rate at state condition 2 - possibly normal operation condition (λ₂ or λ₀); hence

```
AF = \frac{\lambda_2}{\lambda_1} = \frac{\lambda_s}{\lambda_o}, \quad (26.1.1)
```

which is equivalent to

```
AF = \frac{TTF_1}{TTF_2} = \frac{TTF_o}{TTF_s}, \quad (26.1.2)
```

where TTF₁ (TTFo) and TTF₂ (TTFs) are time to failure at condition 1 (possibly normal operation condition) and the time to failure at condition 2 (stress), respectively.