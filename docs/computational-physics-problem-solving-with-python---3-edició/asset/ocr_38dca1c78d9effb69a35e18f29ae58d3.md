1/g(E_i) weighting factor. Thus, if by including this weighting factor we produce a flat histogram, then we have perfectly counteracted the actual peaking in g(E_i), which means that we have arrived at the correct g(E_i).

# 17.6

Wang–Landau Algorithm

The steps in WLS are similar to those in the Metropolis algorithm, but now with use of the density-of-states function g(E_i) rather than a Boltzmann factor:

+   1. Start with an arbitrary spin configuration α_k = {s_1, s_2, …, s_N} and with arbitrary values for the density of states g(E_i) = 1, i = 1, …, M, where M = 2^N is the number of states of the system.
+   2. Generate a trial configuration α_{k+1} by
+      a) picking a particle i randomly and
+      b) flipping i’s spin.
+   3. Calculate the energy E_{α_tr} of the trial configuration.
+   4. If g(E_{α_tr}) ≤ g(E_{α_k}), accept the trial, that is, set α_{k+1} = α_tr.
+   5. If g(E_{α_tr}) > g(E_{α_k}), accept the trial with probability P = g(E_{α_k})/g(E_{α_tr}):
+      a) choose a uniform random number 0 ≤ r_i ≤ 1
+      b) set α_{k+1} = { α_tr, if P ≥ r_i (accept); α_k, if P < r_i (reject) }.

This acceptance rule can be expressed succinctly as

$$\mathcal{P}(E_{\alpha_k} \to E_{\alpha_{tr}})=\min\left[1,\frac{g(E_{\alpha_k})}{g(E_{\alpha_{tr}})}\right], \tag{17.24}$$

which manifestly always accepts low-density (improbable) states.

+   6. Once we have a new state, we modify the current density of states g(E_i) via the multiplicative factor f:

$$g(E_{\alpha_{k+1}})\to f g(E_{\alpha_{k+1}}), \tag{17.25}$$

and add 1 to the bin in the histogram corresponding to the new energy:

$$H(E_{\alpha_{k+1}})\to H(E_{\alpha_{k+1}})+1. \tag{17.26}$$

+   7. The value of the multiplier f is empirical. We start with Euler’s number f = e = 2.718 28, which appears to strike a good balance between very large numbers of small steps (small f) and too rapid a set of jumps through energy space (large f). Because the entropy S = k_B ln g(E_i) → k_B[ln g(E_i) + ln f], (17.25) corresponds to a uniform increase by k_B in entropy.
+   8. Even with reasonable values for f, the repeated multiplications in (17.25) lead to exponential growth in the magnitude of g. This may cause floating-point overflows and a concordant loss of information (in the end, the magnitude