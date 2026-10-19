the net number of particles pointing in the direction of the magnetic field:

$$M(T) = \mu \times (N_{L} - N_{U}) \tag{7.16}$$

$$= N\mu \tanh\left(\frac{\lambda \mu M(T)}{k_{B} T}\right). \tag{7.17}$$

Note that this expression appears to make sense because as the temperature approaches zero, all spins will be aligned along the direction of $B$ and so $M(T = 0) = N\mu.$

**Solution via Searching** Equation 7.17 relates the magnetization and the temperature. However, it is not really a solution to our problem because $M$ appears on the LHS of the equation as well as within the hyperbolic function on the RHS. Generally, a *transcendental equation* of this sort does not have an analytic solution that would give $M$ as simply a function of the temperature $T$. But by working backward, we can find a numerical solution. To do that we first express (7.17) in terms of the reduced magnetization $m$, the reduced temperature $t$, and the Curie temperature $T_{c}$:

$$m(t) = \tanh\left(\frac{m(t)}{t}\right), \tag{7.18}$$

$$m(T) = \frac{M(T)}{N\mu}, \quad t = \frac{T}{T_{c}}, \quad T_{c} = \frac{N\mu^{2}\lambda}{k_{B}}. \tag{7.19}$$

While it is no easier to find an analytic solution to (7.18) than it was to (7.17), the simpler form of (7.18) makes the programming easier as we search for values of $t$ and $m$ that satisfy (7.18).

![](bbox=[0.115, 0.62, 0.6, 0.835])

**Figure 7.4** A function of the reduced magnetism $m$ at three reduced temperatures $t$. A zero of this function determines the value of the magnetism at a particular value of $t.$