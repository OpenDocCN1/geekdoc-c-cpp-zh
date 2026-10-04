# Nonstationary Time Series Models

the realizations. Which model appears to produce realizations most similar to the log-lyn data given in Figure 3.15b?

+   a. Find and print the factor for $(1-B^o)X_t = a_t$. What are the roots of unity?
b. Generate a realization of length $n = 120$ from the seasonal model in (a). Describe any seasonal behavior you see in the realization.
c. Plot the realization in (b) along with the true autocorrelations and true spectral density (use `plots.true.wge`). Describe the behavior in the autocorrelations and spectral density.
d. Plot the realization in (b) along with the sample autocorrelations, periodogram, and Parzen window spectral density estimates. How do these plots compare with those in (c)?

+   5.8 Generate and plot realizations of length $n = 100$ from the random walk/walk with drift models $X_t = \alpha + X_{t-1} + a_t$, (in all cases $X_0 = 0)

+   a. $\alpha = 0, \sigma_\epsilon^2 = 1$
b. $\alpha = 0, \sigma_a^2 = 10$
c. $\alpha = 0.10, \sigma_\epsilon^2 = 1$
d. $\alpha = 0.25, \sigma_a^2 = 1$
e. $\alpha = 1, \sigma_\epsilon^2 = 1$

Discuss your findings.

# Theoretical Problems

+   5.9 Verify the following from Example 5.7:
a. $(1-B)ho_k^* = 0 \Rightarrow ho_k^* = 1, k=0, \pm1, \pm2, \dots$
b. $(1-B^4)ho_k^* = 0 \Rightarrow ho_k^* = 1, k=4m, m=0, \pm1, \pm2, \dots$
$=0$, otherwise
c. $(1-\sqrt{3B+B^2})ho_k^* = 0 \Rightarrow ho_k^* = \cos\frac{\pi k}{6}$.
d. $(1-B)(1-\sqrt{3B+B^2})ho_k^* = 0 \Rightarrow ho_k^* = 0.65+0.35\cos\frac{\pi k}{6}$.

+   5.10 Consider the following ARUMA($p,d,q$) model:
$(1-B^2)(1-B^3)(1+B)(1-1.6+0.6B^2)(1+0.8B^2)(X_t-10) = (1+0.2B+0.9B^2)q_t$.

+   a. Identify $p, d$, and $q$.
b. Identify $j$ and $\ell$ in Theorem 5.1.
c. What difference equation does $ho_k^*$ satisfy? What is $ho_\infty^*$?