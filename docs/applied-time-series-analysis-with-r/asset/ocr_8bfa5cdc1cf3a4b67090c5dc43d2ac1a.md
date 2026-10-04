b. Generate and plot four realizations of length $n = 150$ and with white variance 0.01 from the model

$X_i = -0.526 + 0.0044t + Z_i$, where $(1 - 0.0614B + 0.044B^2 - 0.077B^3 - 0.206B^4)Z_i = 0$,

which was fit to the global temperature data in dataset hadley.\ How do these realizations compare with the data in Figure 1.24a?

5.3 Generate realizations of length $n = 200$ from the following models:

+   a. $(1 - 1.2B + 0.8B^2)(1 - B)X_i = a_i$,
b. $(1 - 1.2B + 0.8B^2)(1 - B^2)X_i = a_i$,
c. $(1 - 1.2B + 0.8B^2)(1 - B^4)X_i = a_i$,
d. $(1 - 1.2B + 0.8B^2)(1 - B^4)(1 + B + B^2)X_i = a_i$,

Discuss features of the model that you can observe from the realizations. For each model, specify whether it is

+   i. Stationary
ii. Nonstationary
iii. Seasonal (and nonstationary)

5.4 This problem involves generating realizations from the ARUMA(3, 2, 1) model

$(1 - B)(1 + B - \alpha_1B)(1 + B + 0.5B^2)X_i = a_i$,

where $|\alpha_i| < 1$.

+   a. Generate a realizations of length $n = 500$ for the cases $\alpha_i = 0.01, 0.5, 0.9, 0.999$.
b. For each $a_i$, plot the realization and true autocorrelations (use plots.true). The plots of the true autocorrelations behave in the way suggested by the Finley–Quinn Theorem.
c. For each $\alpha_i$, plot the realization and sample autocorrelations (use plots.sample). Do the sample autocorrelations behave in a manner analogous to that displayed by the true autocorrelations?
d. How is the behavior in the autocorrelations shown in the realizations?

5.5 For each of these ARUMA(p, d, q) models, find $p, d$, and $q$.

+   a. $(1 - 3B + 4.5B^2 - 5B^3 + 4B^4 - 2B^5)X_i = (1 - 1.7B + 0.8B^2)a_i$,
b. $(1 - 0.5B + 0.3B^2 - 0.95B^3 + 0.3B^4 - 0.35B^5 + 0.2B^6)X_i = a_i$,
c. $(1 - 1.5B + 1.3B^2 + 0.35B^3 - B^4 + 1.35B^5 - 0.7B^6 + 0.4B^7)X_i = (1 + 0.9B^2)a_i$,
d. $(1 - 0.5B - 0.5B^2 - B^4 + 0.5B^5 + 0.5B^6)X_i = (1 - 0.81B^2)a_i$.

5.6 Generate four realizations of length $n = 114$ from each model in Example 5.2 for the base (10) index data. Compare and contrast