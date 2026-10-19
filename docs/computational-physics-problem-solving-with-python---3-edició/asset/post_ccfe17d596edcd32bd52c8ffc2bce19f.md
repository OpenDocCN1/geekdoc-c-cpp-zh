
![](img/bccda43674e4a93dee81c749eba8d2f7_591_0.png)

**Figure 24.4** A 1D chain of pendulums coupled with a torsion bar on top. The pendulums swing in planes perpendicular to the length of the bar.

together. As shown in Figure 24.4, we take as our model a 1D chain of identical, equally spaced pendulums connected by a torsion bar that twists as the pendulums swing. The angle θᵢ measures the displacement of pendulum i from its equilibrium position, and a is the distance between pivot points. If all the pendulums are set off swinging together, θᵢ ≡ θⱼ, the coupling torques would vanish and we would have our old friend, the equation for a realistic pendulum. We assume that three torques act on each pendulum, a gravitational torque trying to return the pendulum to its equilibrium position, and the two torques from the twisting of the bar to the right and to the left of the pendulum. The equation of motion for pendulum j follows from Newton's law for rotational motion:

$$
\sum \tau_j = I \frac{d^2\theta_j(t)}{dt^2}, \tag{24.38}
$$

$$
-\kappa(\theta_j - \theta_{j-1}) - \kappa(\theta_j - \theta_{j+1}) - mgL \sin\theta_j = I \frac{d^2\theta_j(t)}{dt^2}, \tag{24.39}
$$

$$
\Rightarrow \kappa(\theta_{j+1} - 2\theta_j + \theta_{j-1}) - mgL \sin\theta_j = I \frac{d^2\theta_j(t)}{dt^2}, \tag{24.40}
$$

where I is the moment of inertia of each pendulum, L is the length of the pendulum, and κ is the torque constant of the bar. The nonlinearity in (24.40) arises from the sin θ ≈ θ − θ³/6 + ... dependence of the gravitational torque. As it stands, (24.40) is a set of coupled nonlinear equations, with the number of equations equal to the number of oscillators, which would be large for a realistic solid.

### 24.6.1 Including Dispersion

Consider a surfer remaining on the crest of a wave. Since he/she does not see the wave form change with time, his/her position is given by a function of the form f(kx − ωt). Consequently, to him/her, the wave has a constant phase

$$
kx - \omega t = \text{constant} \quad \Rightarrow \quad x = \frac{\omega t}{k} = \text{constant}. \tag{24.41}
$$

The surfer's (phase) velocity is the rate of change of x with respect to time,

$$
v_p = \frac{dx}{dt} = \frac{\omega}{k}, \tag{24.42}
$$

which is constant. In general, the frequency ω may be a nonlinear function of k, in which case the phase velocity varies with frequency and we have dispersion. If the wave contained just one frequency, then you would not observe any dispersion, but if the wave was a pulse composed of a range of Fourier components, then it would broaden and change shape in time as each frequency moved with a differing phase velocity. So although dispersion does not lead to an energy loss, it may well lead to a loss of information content as pulses broaden and overlap.

The functional relation between frequency ω and the wave vector k is called a dispersion relation. If the Fourier components in a wave packet are centered around a mean frequency ω₀, then the pulse's information travels, not with the phase velocity, but with the group velocity

$$
v_g = \left.\frac{\partial\omega}{\partial k}\right|_{\omega_0}. \tag{24.43}
$$

A comparison of (24.42) and (24.43) makes it clear that when there is dispersion the group and phase velocities may well differ.

To isolate the dispersive aspect of (24.40), we examine its linear version

$$
\frac{d^2\theta_j(t)}{dt^2} + \omega_0^2 \theta_j(t) = \frac{\kappa}{I} (\theta_{j+1} - 2\theta_j + \theta_{j-1}), \tag{24.44}
$$

where ω₀ = √(mgL/I) is the natural frequency for any one pendulum. Because we want to determine if a wave with a single frequency propagates on this chain, we start with a traveling wave with frequency ω and wavelength λ,

$$
\theta_j(t) = A e^{i(\omega t - k x_j)}, \quad k = \frac{2\pi}{\lambda}, \tag{24.45}
$$

and then test if it is a solution. Substitution of (24.45) into the wave equation (24.44) produces the dispersion relation (Figure 24.5):

$$
\omega^2 = \omega_0^2 - \frac{2\kappa}{I} (1 - \cos ka) \quad \text{(dispersion relation)}. \tag{24.46}
$$

To have dispersionless propagation (all frequencies propagate with the same velocity), we need a linear relation between ω and k:

$$
\lambda = c \frac{2\pi}{\omega} \quad \Rightarrow \quad \omega = ck \quad \text{(dispersionless propagation)}. \tag{24.47}
$$

This will be true for the chain only if ka is small, because then cos ka ≈ 1 and ω ≈ ω₀.

Not only does the dispersion relation (24.46) change the speed of waves, but it also limits which frequencies can propagate on the chain. In order to have real k solutions, ω must lie in the range

$$
\omega_0 \le \omega \le \omega^* \quad \text{(wave propagation)}. \tag{24.48}
$$

![](img/bccda43674e4a93dee81c749eba8d2f7_593_0.png)

**Figure 24.5** The dispersion relation for a linearized chain of pendulums.

The minimum frequency ω₀ and the maximum frequency ω* are related through the limits of cos ka in (24.46),

$$
(\omega^*)^2 = \omega_0^2 + \frac{4\kappa}{I}. \tag{24.49}
$$

Waves with ω < ω₀ do not propagate, while those with ω > ω* are nonphysical because they correspond to wavelengths λ < 2a, that is, oscillations where there are no particles. These high and low ω cutoffs change the shape of a propagating pulse, that is, cause dispersion.

### 24.6.2 Continuum Limit, the Sine-Gordon Equation

If the wavelengths in a pulse are much longer than the pendulum–pendulum repeat distance a, that is, if ka ≪ 1, the chain can be approximated as a continuous medium. In this limit, a becomes the continuous variable x, and the system of coupled ordinary differential equations becomes a single, partial differential equation:

$$
\theta_{j+1} \simeq \theta_j + \left(\frac{\partial\theta}{\partial x}\right)\Delta x \tag{24.50}
$$

$$
\Rightarrow (\theta_{j+1} - 2\theta_j + \theta_{j-1}) \simeq \left(\frac{\partial^2\theta}{\partial x^2}\right)\Delta x^2 \to \left(\frac{\partial^2\theta}{\partial x^2}\right)a^2 \tag{24.51}
$$

$$
\Rightarrow \frac{\partial^2\theta}{\partial t^2} - \frac{\kappa a^2}{I}\frac{\partial^2\theta}{\partial x^2} = \frac{mgL}{I}\sin\theta . \tag{24.52}
$$

If we measure time in units of √(I/mgL) and distances in units of √(κa²/(mgL)), we obtain the standard form of the sine-Gordon equation (SGE)¹:

$$
\frac{1}{c^2}\frac{\partial^2\theta}{\partial t^2} - \frac{\partial^2\theta}{\partial x^2} = \sin\theta \quad \text{(SGE)}, \tag{24.53}
$$

where the sin θ on the RHS introduces the nonlinear effects.

> 1) The name “sine-Gordon” is either a reminder that the SGE is like the Klein–Gordon equation of relativistic quantum mechanics with a sin u added to the RHS, or a reminder of how clever one can be in thinking up names.

### 24.6.3 Analytic SGE Solution

The nonlinearity of the SGE (24.53) makes it hard to solve analytically. There is, however, a trick. Guess a functional form of a traveling wave, substitute it into (24.53) and thereby convert the PDE into a solvable ODE:

$$
\theta(x,t) \stackrel{?}{=} \theta(\xi = t \pm x/v) \quad \Rightarrow \quad \frac{d^2\theta}{d\xi^2} = \frac{v^2}{v^2 - 1}\sin\theta . \tag{24.54}
$$

You should recognize (24.54), the equation of motion for the realistic pendulum with no driving force and no friction, as our old friend. The constant v is a velocity in natural units, and separates different regimes of the motion:

$$
\begin{cases}
v < 1 : \ \text{pendulums initially down} \ \downarrow\downarrow\downarrow\downarrow \ \text{(stable)},\\[4pt]
v > 1 : \ \text{pendulums initially up} \ \uparrow\uparrow\uparrow\uparrow \ \text{(unstable)}.
\end{cases} \tag{24.55}
$$

Although the equation is familiar, it does not mean that an analytic solution exists. However, for an energy E = ±1, we have motion along the separatrix, and have a solution with the characteristic soliton form,

$$
\theta(x - vt) = \begin{cases}
4\tan^{-1}\left(\exp\left[\displaystyle\frac{+(x-vt)}{\sqrt{1-v^2}}\right]\right), & \text{for } E = 1,\\[6pt]
4\tan^{-1}\left(\exp\left[\displaystyle\frac{-(x-vt)}{\sqrt{1-v^2}}\right]\right) + \pi, & \text{for } E = -1.
\end{cases} \tag{24.56}
$$

This soliton corresponds to a solitary kink traveling with velocity \(v\) that flips the pendulums around by 2π as it moves down the chain. There is also an antikink in which the initial θ = π values are flipped to final θ = −π.

### 24.6.4 Numeric Solution: 2D SGE Solitons

We have already solved for 1D solitons arising from the KdeV equation. The elastic-wave solitons that arise from the SGE can be easily generalized to two dimensions, as we do here with the 2D generalization of the SGE equation (24.53):

$$
\frac{1}{c^2}\frac{\partial^2 u}{\partial t^2} - \frac{\partial^2 u}{\partial x^2} - \frac{\partial^2 u}{\partial y^2} = \sin u \quad \text{(2D SGE)}. \tag{24.57}
$$

Whereas the 1D SGE describes wave propagation along a chain of connected pendulums, the 2D form might describe wave propagation in nonlinear elastic media. Interestingly enough, the same 2D SGE also occurs in quantum field theory, where the soliton solutions have been suggested as models for elementary particles (Christiansen and Lomdahl, 1981; Christiansen and Olsen, 1978; Argyris, 1991). The idea is that, like elementary particles, the solutions are confined to a region of space for a long period of time by nonlinear forces, and do not radiate.
