![](bbox=[0.13, 0.08, 0.95, 0.68])

Figure 15.3 Potential coding gain in a Gaussian channel.

Solving for \( E_b/N_0 \) yields

```
\(\frac{E_b}{N_0} > \frac{2^{2R} - 1}{2R}.\) (15.11)
```

giving the potential coding gain for a code of information rate \( R \).

Notice that if the information transmission rate \( R_t \) is held constant, then by (15.10), when \( W \to \infty, R \to 0 \). Letting \( R \to 0 \) in (15.11), we obtain \( E_b/N_0 > \ln 2 \), agreeing with (15.9) in the case where the channel has unlimited bandwidth. Suppose that we keep the bandwidth fixed when the channel is bandwidth limited. The right-hand side of (15.11) is an increasing function of \( R \). Hence to communicate near the Shannon limit, \( R \) must be close to 0; by (15.10), the information transmission rate \( R_t \) must also be close to 0. The