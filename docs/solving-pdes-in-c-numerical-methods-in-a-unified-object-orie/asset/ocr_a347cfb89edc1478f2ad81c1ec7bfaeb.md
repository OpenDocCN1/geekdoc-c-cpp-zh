![](bbox=[0.115, 0.162, 0.933, 0.908])

**Figure 9.9.** *The characteristic line (along which $F$ is integrated to contribute to $u_{i+1/2,j+1/2}$ at the half time step) has slope $dx/dt=u_{i,j}>0$ if the state $u_{i,j}$ on the left travels to the right (a), $dx/dt=u_{i,j+1}<0$ if the state $u_{i,j+1}$ on the right travels to the left (b), or $dx/dt=0$ if $u_{i,j}<0<u_{i,j+1}$ (c).*

from the $i$th time step toward the point $((i+1/2)\Delta t,(j+1/2)h)$. In the inhomogeneous case, however, $u$ is no longer constant along this line. Indeed, it follows from the chain rule (Sections 10.11, 12.5, 28.5, and 30.10) that

```
$$\frac{du(t,x(t))}{dt}=u_t(t,x(t))+u_x(t,x(t))\frac{dx(t)}{dt}$$
$$\qquad =u_t(t,x(t))+u_x(t,x(t))u_x(t,x(t))$$
$$\qquad =F(t,x(t)).$$
```

Thus, one should also add the contribution from the integral of $F(t,x(t))$ over the characteristic line $x(t)$ issuing from time $t=i\Delta t$ toward the point $((i+1/2)\Delta t,(j+1/2)h)$. (See Chapter 6, Section 6, and set $S=0$ there.) This contribution can be approximated