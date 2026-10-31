sponds to $h_0 = z_0 = 0.6$, $\alpha = 0.365$, $\beta = 0.95$, $\delta = 0.84$ (very successful zombies, indeed), $\gamma = 0.44$, and $\zeta = 0.09$. As in most predator-prey-systems it is quite difficult to find a parameter setting which gives oscillatory behaviour with stable minima and maxima amplitudes. Since neither species becomes extinct with this particular parameter set there is plenty of scope for many Zombie movies in years to come.

# 6.12 Rössler attractor

An electronic analog computer is ideally suited to studying continuous-time dynamic systems of which those exhibiting chaotic behaviour are not only fascinating but also yield aesthetically pleasing phase space plots. The following sections describe a number of such systems; the first of these was developed and studied in 1976 by Otto Rössler.⁹⁸ This system is described by the three coupled differential equations

$$\dot{x}=-(y+z),\\
\dot{y}=x+ay,\\
\dot{z}=b+z(x-c)$$

where $a = 1/5$, $b = 1/5$, and $c = 5.7$. A remarkable property of this particular system is that only one of these equations is non-linear.

Since the variables in these equations will exceed the valid range $[-1,1]$ of the machine units, the equations must be scaled before setting up the computer. Due to the non-linear nature of the problem, this scaling process is rather cumbersome and is best done in a multi-step fashion. The final set of scaled coupled DEQs for this problem looks like this:

$$\dot{x}=-0.8y-2.3z\\
\dot{y}=1.25x+a^*y\\
\dot{z}=b^*+15z(x-c^*)$$

with $a^* = 0.2$, $b^* = 0.005$, and $c^* = 0.3796$. The resulting computer setup is shown in figure 6.41 while figure 6.42 shows an $x$-$y$ plot of the attractor, photographed with ISO 100 and a time scale factor $k_0 = 10^3$ set on all three integrators.

A particularly beautiful picture can be obtained with a simple (static) 3d-projection of the attractor. One input of the oscilloscope, which is set to $x$; $y$-mode, is directly fed by $x$ while the other input is fed from a summer yielding

$$y^* = -(y\sin(\varphi)+z\cos(\varphi)),$$