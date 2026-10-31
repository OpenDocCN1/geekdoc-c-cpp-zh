$$(1 - 0.95B)(1 + 0.7B)X_t = a_t.$$

+   4. **Characteristic equation has complex roots:** Figure 3.12 shows autocorrelations for the AR(2) processes

$$(1 - 1.6B - \phi_2B^2)X_t = a_t, \tag{3.70}$$

for $\phi_2 = -0.7$, $-0.9$, and $-0.98$, for which the associated characteristic equation is $1 - 1.6z - \phi_2z^2 = 0$. This equation has complex roots for all $\phi_2 < -0.64$. By Equation 3.63, the system frequency associated with the operator $1 - 1.6B - \phi_2B^2$ is

![](bbox=[0.207, 0.397, 0.794, 0.731])

**FIGURE 3.12**  
Autocorrelations for the AR(2) models $X_t - 1.6X_{t-1} - \phi_2X_{t-2} = a_t$, $(a = c)\phi_2 = -0.7,\ -0.9,\ -0.98$.

$$f_0 = \frac{1}{2\pi}\cos^{-1}\left(\frac{1.6}{2\sqrt{-\phi_2}}\right). \tag{3.71}$$