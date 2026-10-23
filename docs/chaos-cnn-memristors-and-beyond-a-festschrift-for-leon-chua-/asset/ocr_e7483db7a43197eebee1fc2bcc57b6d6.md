# 1. Problem Setting and Equation Derivation

# 1.1. *nth order surface of revolution*

In this study, the dynamics are determined by a downward gravity force and a horizontal force rotating around the axis of revolution of the surface. The fundamental behavior of this system is a periodical circular motion, as the total force is balanced by the damping force, externally-applied force, gravitational force, and constraining force.

Let us take the vertical $Z$-axis upward, and generate a curve of the constrained surface by $Z=X^n$, i.e., surface of revolution $Z=\sqrt{X^2+Y^2}^{\,n}$ (from now on, we call the surface nth order surface of revolution). Of course, the $(X,Y)$-plane is horizontal.

# 1.2. *Derivation of motion equation*

A motion of a constrained mass point $m$ is described by the following equation

```
$$\begin{aligned}
m\frac{d^2X}{dt^2}&=-\delta\frac{dX}{dt}+F_x(t)+R_x(t)\\
m\frac{d^2Y}{dt^2}&=-\delta\frac{dY}{dt}+F_y(t)+R_y(t)\\
m\frac{d^2Z}{dt^2}&=-\delta\frac{dZ}{dt}-mg+R_z(t)
\end{aligned}\tag{1}$$
```

where $\delta$ represents the damping coefficient, $mg$ the gravitational force, $F_x(t),F_y(t)$, the $X$- and $Y$-components of the sinusoidal periodic external force, $R_x(t),R_y(t),R_z(t)$ the constrained force by the nth order revolution surface.

# 1.3. *Normalized equations of motion*

In order to carry out a feasible experimental study, a parameter $\ell$ is introduced to regulate the actual size of the nth order constrained surface, via

```
$$Z/\ell=(\sqrt{X^2+Y^2}/\ell)^n \tag{2}$$
```

By replacing variables $X$, $Y$ and $Z$ with $\ell x$, $\ell y$ and $\ell z$, and the constrained force $R_*(t)/m\ell$ with $\Lambda(t)N_*(t)$ ($* = x,y,z$), and using Eq. (2), one can represent Eq. (1) as

```
$$\begin{aligned}
\frac{dx}{dt}&=u, & \frac{du}{dt}&=-ku+f_x(t)+\Lambda(t)N_x(t)\\
\frac{dy}{dt}&=v, & \frac{dv}{dt}&=-kv+f_y(t)+\Lambda(t)N_y(t)\\
\frac{dz}{dt}&=w, & \frac{dw}{dt}&=-kw-\frac{g}{\ell}+\Lambda(t)N_z(t)
\end{aligned}\tag{3}$$
```

where

```
$$k=\frac{\delta}{m},\qquad f_x=\frac{F_x}{m\ell}=F\cos\omega t,\qquad f_y=\frac{F_y}{m\ell}=F\sin\omega t \tag{4}$$
```

Here, $\Lambda(t)$ is an unknown function about the magnitude of the constrained force, $N_x(t),N_y(t),N_z(t)(=R_*(t)/m\ell)$ represent directional components of the constrained force, which are given via partial derivatives of the following constrained condition:

```
$$\varphi=z-r^n=0,\qquad r^2=x^2+y^2 \tag{5}$$
```

that is,

```
$$\begin{aligned}
N_x(t)&=-nxr^{n-2}\\
N_y(t)&=-nyr^{n-2}\\
N_z(t)&=1
\end{aligned}\tag{6}$$
```

# 1.4. *Determination of unknown function $\Lambda(t)$*

Derivatives of constrained Eq. (5) are expressed by

```
$$\frac{d\varphi}{dt}=w-nr^{n-2}(xu+yv)=0 \tag{7}$$
```

```
$$\frac{d^2\varphi}{dt^2}=\frac{dw}{dt}-nr^{n-2}\left(x\frac{du}{dt}+y\frac{dv}{dt}+u^2+v^2\right)-n(n-2)r^{n-4}(xu+yv)^2=0 \tag{8}$$
```