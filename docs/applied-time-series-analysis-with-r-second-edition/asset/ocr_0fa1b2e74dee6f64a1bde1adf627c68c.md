# ### 3.18 Using the formula in [Equation 3.63](#) (not an R routine)

+   a. Find the system frequency $f_0$ associated with the AR(2) process
+   
+   $$X_t - 1.3X_{t-1} + 0.85X_{t-2} = a_t.$$

+   b. Find $φ_1$, so that the AR(2) model
+   
+   $$X_t - φ_1X_{t-1} + 0.9X_{t-2} = a_t$$
+   
+   has system frequency $f_0 = 0.4$.

### 3.19

Consider the AR(2) model $X_t - φ_1X_{t-1} - φ_2X_{t-2} = a_t$ for which the roots, $r_1, r_2$, of the characteristic equation are complex conjugates whose reciprocals are $a \pm bi$. Show that $φ_2 = -1/|r_i|^2$ and $φ_1 = 2a$.

# ### 3.20

+   a. Let $X_t$ satisfy the AR(2) model $X_t - φ_1X_{t-1} - φ_2X_{t-2} = a_t$ for which the roots of the characteristic equation are complex conjugates. Show that:

+   i. If $|\phi_1| \le -4\phi_2/(1-\phi_2)$, then the peak in the AR(2) spectral density occurs at
+   
+   $$f_s = \frac{1}{2\pi}\cos^{-1}\left(\frac{\phi_1(\phi_2-1)}{4\phi_2}\right).$$

+   ii. If $φ_1 > -4φ_2/(1-φ_2)$, then the peak in the spectral density occurs at frequency 0.

+   iii. If $φ_1 < 4φ_2/(1-φ_2)$, then the peak in the spectral density occurs at frequency 0.5.

+   b. Suppose $|\phi_1| \le -4\phi_2/(1-\phi_2)$ for a given $φ_1$ and $φ_2$. Then if $φ_1$ stays fixed as $|\phi_2| \to 1$, show $f_s \to f_0$ approaches $f_0$, the system frequency.

+   c. For the AR(2) model $X_t - 1.42X_{t-1} + 0.73X_{t-2} = a_t$, fit to the sunspot data, find $f_s$ and $f_0$.

# ### 3.21 Consider the AR(2) model given in factored form by

$$(1 - 0.8B)(1 + 0.5B)(X_t - 50) = a_t,$$

where $σ_a^2 = 5$.

+   a. Use the Yule–Walker equations to find $ρ_1$ and $ρ_2$.

+   b. Find $C_1$ and $C_2$ in the general expression for $ρ_k$.

$$\rho_k = C_1(r_1)^{-k} + C_2(r_2)^{-k}.$$