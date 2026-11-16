(5.28) 
\(\hat{\phi}(\omega) = G_0(z) \hat{\phi}\left(\frac{\omega}{2}\right)\)

(5.29) 
\(\hat{\psi}(\omega) = G_1(z) \hat{\phi}\left(\frac{\omega}{2}\right)\)

where

(5.30) 
\(G_0(z) := \frac{1}{2} \sum_k g_0[k] z^k\)

(5.31) 
\(G_1(z) := \frac{1}{2} \sum_k g_1[k] z^k\)

with \(z = e^{-j\omega/2}\). Observe that the definitions in (5.30) and (5.31) are slightly different from those used in Chapter 2 for z-transform. An example of a two-scale relation for the Haar case (\(H\)) is shown in Figure 5.3. Using (5.28) and (5.29) recursively, we have

(5.32) 
\(\hat{\phi}(\omega) = \prod_{\ell=1}^{\infty} G_0\left(\exp\left[-j\frac{\omega}{2^\ell}\right]\right)\)

(5.33) 
\(\hat{\psi}(\omega) = G_1\left(\exp\left[-j\frac{\omega}{2}\right]\right) \prod_{\ell=2}^{\infty} G_0\left(\exp\left[-j\frac{\omega}{2^\ell}\right]\right)\)