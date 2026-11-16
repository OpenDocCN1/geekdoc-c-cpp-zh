![](bbox=[0.13, 0.08, 0.83, 0.2])

Similar to the case of the Shannon scaling function, here too we get

```
(6.51) g_0[k] = \phi_{M,m} \left( \frac{k}{2} \right).
```

Therefore, for m = 0, we can obtain g_0[k] by simply substituting k/2 for t in (6.50). Table 6.2 gives the two-scale coefficients for m = 1.

Meyer's wavelets can be obtained by using the two-scale relations. Since the scaling functions have compact support in the frequency domain, Meyer wavelets are related to the scaling function in a more direct way as shown below.

```
(6.52)
\hat{\psi}_{M,m}(\omega) = G_1(z) \hat{\phi}_{M,m} \left( \frac{\omega}{2} \right) ; \quad z = \exp(-j\omega/2)
= -z \overline{G_0(-z)} \hat{\phi}_{M,m} \left( \frac{\omega}{2} \right)
= -z \left[ \sum_{k=-\infty}^{\infty} \hat{\phi}_{M,m}(\omega + 2\pi + 4\pi k) \right] \hat{\phi}_{M,m} \left( \frac{\omega}{2} \right)
= -z \left[ \hat{\phi}_{M,m}(\omega + 2\pi) + \hat{\phi}_{M,m}(\omega - 2\pi) \right] \hat{\phi}_{M,m} \left( \frac{\omega}{2} \right).
```