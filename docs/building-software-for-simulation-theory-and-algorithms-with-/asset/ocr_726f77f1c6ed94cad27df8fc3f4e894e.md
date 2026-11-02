Now consider a simpler model that ignores the transient current. By assuming that $i$ is an instantaneous function of $\omega$, we can set $\dot i = 0$ and obtain the algebraic relationship

$$i = \frac{\epsilon - \alpha\omega}{R_m} \tag{5.22}$$

Substituting this into Equations 5.18–5.21 gives the three-variable model

$$\dot v = \frac{1}{m_t}\left(2F - B_t v\right) \tag{5.23}$$

$$\dot \omega = \frac{1}{J_g}\left(\frac{\alpha\epsilon - \alpha^2\omega}{R_m} - \omega B_g - \frac{r}{g}F\right) \tag{5.24}$$

$$\dot F = \frac{1}{K_t}\left(\frac{r}{g}\omega - v\right) \tag{5.25}$$

This eliminates the large ratio for $\dot i$ and changes the ratios governing the acceleration $\dot \omega$ of the gears to

$$\frac{\alpha^2/R_m + B_g}{J_g} = 0.827$$

$$\frac{(r/g)}{J_g} = 61.27$$

The magnitudes of the largest and smallest eigenvalues of this reduced model are 50 and 0.8, respectively. This is a considerable reduction in the maximum rate of the system and gives a correspondingly larger step size.

Figure 5.12 shows the trajectory of this simplified model. It is very similar to the plot that includes the motor because the inrush of current occurs so quickly that its long-term effects are negligible. The step sizes chosen by the integrator confirm the expected advantage; with an error tolerance of $10^{-2}$, the timesteps during the initial transients are on the order of $10^{-5}$ and are $10^{-2}$ once the tank has gotten up to speed.

This reformulation of the model works well if the motors are at full power, but it is inadequate for operating at a smaller duty ratio. Figure 5.13 shows why; at a 50% duty ratio, the electric current in the more accurate model remains positive. This is because the motor controller switches fast enough for inductance to maintain the current when the batteries are disconnected. The reformulated model has no inductance, and the current actually reverses if the switches are opened while the tank is moving. This problem is corrected by using in Equation 5.22 the average voltage over an interrupt period rather than the instantaneous voltage. The correction requires a small change to the internal transition function of the *InterruptHandler*, which now computes $e_l$ as

$$e_l = 7.2(\text{left motorontime}/255) \tag{5.26}$$