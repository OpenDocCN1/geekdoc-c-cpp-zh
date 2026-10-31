# **Table 3.6**  
Factor Table for the ARMA(2,1) Model in [Equation 3.93](#)

|  | Roots ($r_j$) | $|r_j^{-1}|$ | $f_{0j}$ |
|---|---:|---:|---:|
| *AR factor* |  |  |  |
| $1 - 1.6B + 0.9B^2$ | $0.89 \pm 0.57i$ | 0.95 | 0.09 |
| *MA factor* |  |  |  |
| $1 - 0.8B$ | 1.25 | 0.8 | 0 |

![](bbox=[0.209, 0.279, 0.792, 0.616])

# **FIGURE 3.24**

(a) Realization, (b) autocorrelations, and (c) spectral densities for the ARMA(2,1) model $(1 - 1.6B + 0.9B^2)X_t = (1 - 0.8B)a_t$.

which can be factored as

$$(1 - 1.8B + 0.95B^2)(1 + 1.5B + 0.85B^2)X_t = (1 + 0.9B)(1 + 0.8B^2)a_t. \tag{3.95}$$

The factor table is shown in [Table 3.7](#), and it should be noted that the AR factor is the one previously considered in the AR(4) model in Example 3.13. [Figure 3.25](#) displays a realization of length $n = 200$ from the ARMA(4,3) model in [Equations 3.94 and 3.95](#) with $\sigma_a^2 = 1$.