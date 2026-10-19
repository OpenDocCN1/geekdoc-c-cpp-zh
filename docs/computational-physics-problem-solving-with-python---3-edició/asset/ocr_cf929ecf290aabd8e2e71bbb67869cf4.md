![](bbox=[0.141, 0.101, 0.471, 0.235])

**Figure 20.4** Temperature vs. position and time when two bars at differing temperatures are placed in contact at $t=0$. The projected contours show the isotherms.

only a single time value is known, the method uses a *split time step*,<sup>1)</sup> so that time is advanced from time $t$ to $t+\Delta t/2$:

$$\frac{\partial T}{\partial t}\left(x,t+\frac{\Delta t}{2}\right)\simeq \frac{T(x,t+\Delta t)-T(x,t)}{\Delta t}+O(\Delta t^2). \tag{20.27}$$

Yes, we know that this looks just like the forward-difference approximation for the derivative at time $t+\Delta t$, for which it would be a bad approximation; regardless, it is a better approximation for the derivative at time $t+\Delta t/2$, although it makes the computation more complicated. Likewise, in (20.14) we gave the central-difference approximation for the second space derivative for time $t$. For $t=t+\Delta t/2$, that becomes

$$2(\Delta x)^2\frac{\partial^2T}{\partial x^2}\left(x,t+\frac{\Delta t}{2}\right)\simeq [T(x-\Delta x,t)-2T(x,t)+T(x+\Delta x,t)]\\+[T(x-\Delta x,t+\Delta t)-2T(x,t+\Delta t)+T(x+\Delta x,t+\Delta t)]+O(\Delta x^2). \tag{20.28}$$

In terms of these expressions, the heat difference equation is

$$T_{i,j+1}=\frac{\eta}{2}\left[T_{i-1,j+1}-2T_{i,j+1}+T_{i+1,j+1}+T_{i-1,j}-2T_{i,j}+T_{i+1,j}\right],\\x=i\Delta x,\qquad t=j\Delta t,\qquad \eta=\frac{K\Delta t}{C\rho\Delta x^2}. \tag{20.29}$$

We group together terms involving the same temperature to obtain an equation with future times on the LHS and present times on the RHS:

$$-T_{i-1,j+1}+\left(\frac{2}{\eta}+2\right)T_{i,j+1}-T_{i+1,j+1}=T_{i-1,j}+\left(\frac{2}{\eta}-2\right)T_{i,j}+T_{i+1,j}. \tag{20.30}$$

> <sup>1)</sup> In Section 22.2.1 we develop a different split-time algorithm for the solution of the Schrödinger equation. There the real and imaginary parts of the wave function are computed at times that differ by $\Delta t/2$.