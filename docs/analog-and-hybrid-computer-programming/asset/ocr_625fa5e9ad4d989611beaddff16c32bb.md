The corresponding computer setup is shown in figures 6.21 and 6.22. The upper and lower halves of the circuit are symmetric except for the input for the gravitational acceleration to the lower left integrator which gives $\dot{y}$. The velocities $\dot{x}$ and $\dot{y}$ are fed to multipliers to give their respective squares, which are then summed and square rooted to get $v$ since $\delta(v)/v = r v$ according to (6.17).

The parameters $\alpha_1$ and $\alpha_2$ are scaling parameters that are set to give a suitably scaled picture on the oscilloscope set to $x,y$-mode. Table 6.23 shows the parameter set yielding the result shown in figure 6.23. The initial conditions satisfy $\dot{x}_0 = \cos(\varphi_0)$ and $\dot{y}_0 = \sin(\varphi_0)$ with $\varphi$ denoting the elevation of the cannon. In the screenshot shown $\varphi_0$ was set to $60^\circ$.

# 6.7 Charged particle in a magnetic field

This example uses an analog computer to simulate the path of a charged particle traversing a magnetic field.$^{88}$ Basically, a particle with charge $q$ moving in a magnetic field $\vec{B}$ is subjected to a force $\vec{F}_{Lorentz}$ which is perpendicular to both, the magnetic field $\vec{B}$ and the direction in which the particle moves, yielding $\vec{F}_{Lorentz} = q\left(\vec{v} \times \vec{B}\right) = q\left(\dot{\vec{r}} \times \vec{B}\right)$.

$\vec{v}$ denotes the velocity and $\vec{r}$ the position of the particle under consideration. Also, $\vec{F}_{particle} = m\ddot{\vec{r}}$ holds. In addition to this, some form of friction exerting a force $\vec{F}_{friction} = -\mu\dot{\vec{r}}$ is assumed to act on the particle.

Combining these three equations finally yields $m\ddot{\vec{r}} = \vec{F}_{Lorentz} + \vec{F}_{friction} = q\left(\dot{\vec{r}} \times \vec{B}\right) - \mu\dot{\vec{r}}.$ (6.20)

88 This is based on [Telefunken/Particle], which was probably written by Ms. INGE BORCHARDT who did the trajectory simulations at DESY for the high-energy particle accelerators - initially on an EAI 231RV analog computer and subsequently on a Telefunken RA770 hybrid computer.