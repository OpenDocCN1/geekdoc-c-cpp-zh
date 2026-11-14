$sT = \ln(z)$

We now have the relationship between $s$ and $z$, but we need to deal with taking the natural log of $z$, which doesn't have a closed form solution. If we use the Taylor series expansion for $\ln()$, we get Equation 6.12 for $\text{Re}(z) > 0$:

$$sT = 2 \left[ \frac{z-1}{z+1} + \frac{1}{3} \left( \frac{z-1}{z+1} \right)^3 - \frac{1}{5} \left( \frac{z-1}{z+1} \right)^5 + \frac{1}{7} \left( \frac{z-1}{z+1} \right)^7 - ... \right]$$ Taking the first term only $$s = \frac{2}{T} \frac{z-1}{z+1}$$ (6.12)

This first term *approximation* of the general solution is the bilinear transform. The bilinear transform we use is Equation 6.13:

$$s = \frac{z-1}{z+1}$$ (6.13)

The 2/T term washes out mathematically, so we can neglect it. This equation does the mapping by taking values at the infinite frequencies and mapping them to Nyquist. So, a pole or zero at $-\infty$ or $+\infty$ is mapped to Nyquist. The other frequencies between Nyquist and $-\infty$ or $\infty$ Hz are squeezed into the little region right around Nyquist, just inside the unit circle, as shown in Figure 6.13.

![](bbox=[0.15, 0.45, 0.85, 0.72])

**Figure 6.13:** The bilinear transform maps the area outside the Nyquist zone on the left-hand plane to an area just inside the circle near Nyquist.

The bilinear transform maps analog frequencies to their corresponding digital frequencies nonlinearly via the tan() function (Equation 6.14):

$$\omega_d = \tan \left[ \frac{\omega_a f_s}{2} \right]$$ (6.14)

where $\omega_a$ = the analog frequency $\omega_d$ = the mapped digital frequency $f_s$ = the sample rate