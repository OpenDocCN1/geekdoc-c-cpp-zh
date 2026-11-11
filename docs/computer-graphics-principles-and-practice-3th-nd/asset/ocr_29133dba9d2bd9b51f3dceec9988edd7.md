This tells us that if we know $n_1$, $n_2$, and $\theta_1$, we can determine $\theta_2$. The index of refraction, $n$, determines a great deal about how light interacts with a medium. For instance, when light arrives at the interface between air and glass at some angle, the refractive index determines not only the amount of bending, but also how much of the light is transmitted through the glass and how much is reflected, as we'll see in Section 26.5. Those interested in physically realistic renderings of glass and other transparent materials must take this fact into account.

Using only the assumption that the electromagnetic field has a sinusoidal form with the same frequency in each medium, and is continuous, we can prove Snell's law. Fortunately, the mathematics of this explanation apply to any kind of wave, not just plane waves in three dimensions, so we can illustrate the idea with linear waves in a plane. Consider the situation shown in Figure 26.12: a shallow tray whose left side is twice as deep as its right side; this makes waves on the left half travel about twice as fast as those on the right half. If we create sinusoidal waves of frequency $f$ on the left side, moving right, when they enter the right side they "bunch up." Because of the slower speed on the right, the same number of waves per second reach the right-hand side of the tray as reached the midline.

![](bbox=[0.719, 0.134, 0.954, 0.268])

*Figure 26.12:* Waves traveling to the right bunch up as they slow down.

When we create waves traveling in an off-axis direction (see Figure 26.13) in the left half of the tank, they arrive at the dividing line between the two sides and continue on as waves in the shallower right-hand side of the tank. The peaks of the waves on the two sides of the tank must match up at the dividing line if the wave height is to be a continuous function; for this to happen, the directions of propagation must differ.

![](bbox=[0.719, 0.347, 0.954, 0.491])

*Figure 26.13:* Off-axis waves change direction “at an interface.”

+   **Inline Exercise 26.6:**
+   
+   - (a) Suppose that the wavelength of the waves in the left half of the tank is $\lambda$, and the direction of propagation in the left side is at angle $\theta_r \ne 0$ to the left-right axis of the tank. Show that along the midline of the tank, the distance between peaks is $\lambda / \sin(\theta_r)$.
+   - (b) For a corresponding statement to be true on the right side of the tank, where the wavelength is about $\lambda/2$, the distance between peaks will be $(\lambda/2)/\sin(\theta_R)$. Setting these equal, show that $\sin(\theta_r)/\sin(\theta_R) = 2$, which is exactly the ratio of the velocities in the two sides of the tank.

A similar phenomenon happens with plane waves that meet at a planar interface between media, from which Snell's law follows as a consequence.

The index of refraction of a medium is not really a constant: It depends on the wavelength of the light. Cauchy developed an empirical approximation for the dependence, showing it was of the form

$$n(\lambda) \approx A + \frac{B}{\lambda^2},$$

where the values of $A$ and $B$ are material-dependent. The exact values are not important, except that $B \ne 0$. This means that light of different wavelengths, arriving at an interface between different media, gets bent by different amounts: The different wavelengths are separated from one another. One instance of this is the rainbows cast by prisms when they are struck by sunlight. Another is that lenses, which are supposed to focus light at a single point, actually focus light of different wavelengths at different points: When red light is in focus, blue light will be blurry, etc. This **chromatic aberration** is a significant problem in lens design, and many lens coatings are designed to minimize it.