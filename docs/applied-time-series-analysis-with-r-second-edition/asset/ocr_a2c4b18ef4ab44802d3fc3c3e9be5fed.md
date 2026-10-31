$X_t - 0.3 X_{t-1} - 0.9 X_{t-2} - 0.1 X_{t-3} + 0.8 X_{t-4} = a_t,$

whose factor table is given in Table 3.4. In the factor table, it can be seen that the characteristic equation has two pairs of complex conjugate roots, one associated with a system frequency of $f = 0.06$ and the other with a frequency of $f = 0.4$. It can also be seen that the roots associated with $f = 0.06$ are closer to the unit circle. Thus, the realizations should have pseudo-periodic behavior with a more dominant period of about 17 (1/0.06) and a higher frequency component with period of about 2.5 (1/0.4). We also expect two peaks in the spectral density, at about $f = 0.06$ and $f = 0.4$.

In Figure 3.19, we show a realization of length $n = 200$, where $\sigma_a^2 = 1$, the autocorrelations, and the spectral density for the AR(4) model in this example. The realization has the anticipated pseudo-periodic behavior with a period of about 17 and a high-frequency component. There are peaks in the spectral density at about $f = 0.06$ and $f = 0.4$ as expected. The autocorrelation is a damped sinusoidal with a period of about 17 with a slight indication of the higher frequency behavior. Again, we see that the spectral density and the factor table give a much clearer picture of the periodic behavior.

# EXAMPLE 3.14: DOMINANCE OF ROOTS NEAR THE UNIT CIRCLE

In this example, we return to the AR(3) model in Example 3.8. We first consider the AR(3) models

$(1 - 0.95B)(1 - 1.6B - \lambda_2 B^2) X_t = a_t,$

where $\lambda_2 = -0.7$, $-0.9$ (as in Example 3.8), and $-0.98$. We do not show the factor tables for these three models, but it should be noted that $|r_j^{-1}| = 0.95$ for the real root. More completely, for $\lambda_2 = -0.7$, $-0.9$, and $-0.98$ the complex roots have $|r_j^{-1}| = 0.84$, $0.95$, and $0.99$, respectively. Thus, the complex roots and real root are equally close to the unit circle when $\lambda_2 = -0.9$; however, when $\lambda_2 = -0.7$, the real root is closer to the unit circle than are the complex roots, and when $\lambda_2 = -0.98$, the complex roots are closer. So, based on the discussion preceding Example 3.13, we expect the real root to dominate the cyclic