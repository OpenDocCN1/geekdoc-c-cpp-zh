
**b** = bₓ x̂ + bᵧ ŷ + b_z ẑ

with respect to the body fixed axes xyz. Here, (x̂, ŷ, ẑ) is the unit vector in the rotating frame xyz. Moreover, the vector b can also be decomposed as

**b** = b_X X̂ + b_Y Ŷ + b_Z Ẑ

with respect to the non-rotating axes XYZ. Here, (X̂, Ŷ, Ẑ) is the unit vector in the inertial frame XYZ. We now differentiate b (defined in fixed frame) with respect to time t to get

d**b**/dt = [ dbₓ/dt x̂ + dbᵧ/dt ŷ + db_z/dt ẑ ] + [ bₓ d x̂/dt + bᵧ d ŷ/dt + b_z d ẑ/dt ]   (10.2)

The first part on the right hand side of Equation (10.2) can be interpreted as the instantaneous change of b observed from the body fixed frame xyz since the unit vectors (x̂, ŷ, ẑ) are fixed (do not change) in the body fixed frame. The second part on the right hand side of Equation (10.2) refers to the rate of change of the unit vectors as observed from the inertial frame (non-rotating frame) XYZ. Since the origin of the inertial frame has the same instantaneous velocity as the body-fixed frame, the only way that these unit vectors change with respect to time is by a rotation about some axis passing through the common origin. We denote this rotational velocity as ω and we have

d x̂/dt = ω × x̂,   d ŷ/dt = ω × ŷ,   d ẑ/dt = ω × ẑ.

Hence, the second part in Equation (10.2) becomes (ω × b) and Equation (10.2) reduces to

d**b**/dt = (d**b**/dt)_b + ω × **b**   (10.3)

Equation (10.3) relates the rate of change of the vector b between the translating axis (XYZ) and body fixed rotating axis (xyz). The subscript b indicates that the derivative is with respect to body fixed rotating frame xyz. The LHS is the rate of change of b in the non rotating frame XYZ, which is equal to the rate of change of b with respect to body fixed frame xyz plus omega cross b. Physically, it means that the vector b can increase in magnitude while keeping its direction fixed, and in addition it can change its direction.

Let us now consider the angular momentum L (also called as rotational momentum). The angular momentum is defined as the product of moment of inertia tensor I_m and the angular velocity ω, that is,

**L** = I_m ω,   I_m = [ I_xx  -I_xy  -I_xz ; -I_yx  I_yy  -I_yz ; -I_zx  -I_zy  I_zz ]

Here, I_xx is the moment of inertia of the body about the x-axis defined as

I_xx = ∫_{Ω_S(t)} ρ_s (y² + z²) dx dy dz,

where $\rho_s$ is the density of the solid body. Similarly, $I_{yy}$ and $I_{zz}$ are moment of inertia of the body about the $y$-axis and $z$-axis, respectively, defined analogously. Further, $I_{xy}$, $I_{xz}$ and $I_{yz}$ are the product of inertia, for instance

$$I_{xy}=\int_{\Omega_s(t)}\rho_s\,xy\,dx\,dy\,dz.$$

Note that $I_{xy}=I_{yx}$, $I_{xz}=I_{zx}$ and $I_{yz}=I_{zy}$. These terms can further be simplified if we compute these quantities with respect to the body fixed axes $xyz$, which is also aligned with the principal axes of the rigid body. With such a reference axes (principle axes), the products of inertia $I_{xy}$, $I_{yz}$ and $I_{zx}$ become zero and $I_{xx}$, $I_{yy}$ and $I_{zz}$ become the principle moments of inertia. Hence, we have

$$\mathbf{L}=\mathbf{I}_G\boldsymbol{\omega}_G=I_{xx}\omega_x\hat{x}+I_{yy}\omega_y\hat{y}+I_{zz}\omega_z\hat{z}$$

where,

$$\mathbf{I}_G=\begin{bmatrix}I_{xx}&0&0\\0&I_{yy}&0\\0&0&I_{zz}\end{bmatrix}\qquad\text{and}\qquad \boldsymbol{\omega}_G=\begin{bmatrix}\omega_x\\\omega_y\\\omega_z\end{bmatrix}$$

Similar to Equation (10.3), the time derivative of the angular momentum $\mathbf{L}$ becomes

$$\frac{d\mathbf{L}}{dt}=\left(\frac{d\mathbf{L}}{dt}\right)_b+\boldsymbol{\omega}\times\mathbf{L}.$$

We now write Equation (10.3) in component-wise and in the body-fixed frame $xyz$. For the first term, we get

$$\left(\frac{d\mathbf{L}}{dt}\right)_b=I_{xx}\frac{d\omega_x}{dt}\hat{x}+I_{yy}\frac{d\omega_y}{dt}\hat{y}+I_{zz}\frac{d\omega_z}{dt}\hat{z}.$$

It is true since $I_{xx}$, $I_{yy}$ and $I_{zz}$ are the principal moments of inertia and they do not change with time. Further,

$$\boldsymbol{\omega}\times\mathbf{L}=[(\omega_y\omega_z(I_{zz}-I_{yy}))\hat{x}]+[(\omega_z\omega_x(I_{xx}-I_{zz}))\hat{y}]+[(\omega_x\omega_y(I_{yy}-I_{xx}))\hat{z}].$$

Hence, the angular momentum equation in component-wise can be written as:

$$I_{xx}\frac{d\omega_x}{dt}+(I_{zz}-I_{yy})\omega_y\omega_z=M_x,$$

$$I_{yy}\frac{d\omega_y}{dt}+(I_{xx}-I_{zz})\omega_z\omega_x=M_y,$$

$$I_{zz}\frac{d\omega_z}{dt}+(I_{yy}-I_{xx})\omega_x\omega_y=M_z,$$

where $\mathbf{M}=(M_x,M_y,M_z)$ is the total external moments about the center of mass. Since these equations are defined in the body fixed frame $xyz$, $\frac{d\mathbf{L}}{dt}$ is calculated first and then projected

along the principal axes. Contrarily, we cannot project **L** on the principle axis and then compute the time derivative, since these equations are valid only at an instant of time and the quantities $\boldsymbol{\omega}$ and **M** would change with respect to this axes at the next time instant.

## 10.2.2 Governing Equations of the Fluid Flow

Let $\Omega(t)\subset\mathbb{R}^3$ be the time-dependent domain of the fluid around the ship (floating structure). We consider a free surface flow in a towing tank with a partially submerged ship in the fluid, as shown in Figure 10.2.

Further, the time-dependent boundary is defined by $\partial\Omega(t):=\Gamma_{in}\cup\Gamma_{out}\cup\Gamma_{wall}\cup\Gamma_s\cup\Gamma_{fs}$, where $\Gamma_{in}$ is the inlet boundary, $\Gamma_{out}$ outlet boundary, $\Gamma_{wall}$ container/tank wall, $\Gamma_s$ ship-fluid interface, and $\Gamma_{fs}$ is the free surface as shown in Figure 10.2. The fluid flow around the ship is described by the time-dependent incompressible Navier–Stokes equations [9]

```
$$\frac{\partial\mathbf{u}}{\partial t}+(\mathbf{u}\cdot\nabla)\mathbf{u}-\frac{1}{\rho}\nabla\cdot\mathbf{T}(\mathbf{u},p)=\mathbf{g}e \quad \text{in }\Omega(t)\times[0,I],$$

$$\nabla\cdot\mathbf{u}=0 \quad \text{in }\Omega(t)\times[0,I].$$
```

where $\mathbf{u}$, $p$, and $\rho$ denote the fluid velocity, pressure in the fluid and density of the fluid, respectively. Here, the stress tensor $\mathbf{T}(\mathbf{u},p)$ and the velocity deformation tensor $\mathbf{D}(\mathbf{u})$ are given by

```
$$\mathbf{T}(\mathbf{u},p)=-p\mathbf{I}+2\mu\mathbf{D}(\mathbf{u}),\qquad \mathbf{D}(\mathbf{u})=\frac{1}{2}(\nabla\mathbf{u}+\nabla\mathbf{u}^{T}),$$
```

where $\mathbf{I}$ and $\mu$ denote the identity tensor and the viscosity of the fluid, respectively and the superscript $T$ is used to denote transpose.

## 10.2.3 Coupled Boundary and Initial Conditions

The 6-DOF Equations (10.1) and (10.4), and the Navier–Stokes Equation (10.5) are closed with the boundary and initial conditions. We consider a force-balancing boundary condition on

![](img/81c56bc4b2fca1951aff5e0ab85b66be_176_0.png)

the free surface $\Gamma_{fs}(t)$. Moreover, a traction (surface force per unit area) condition can also be considered, where the traction can be due to wind, and in reality ocean waves are primarily caused by tidal forces. Next, we impose the slip with friction boundary condition at the fluid–solid interface $\Gamma_s(t)$, a free slip with no penetration condition on the side and bottom walls $\Gamma_w$, zero stress on the outlet boundary $\Gamma_{out}$, and a prescribed velocity on the inlet boundary $\Gamma_{in}$. The conditions can be formulated as below:

$$\begin{aligned}
-\boldsymbol{\Pi}(\mathbf{u},p)\cdot\boldsymbol{\nu} &= \sigma\,\mathcal{K}\,\boldsymbol{\nu} && \text{on }\Gamma_{fs}(t)\times[0,T]\\
\mathbf{u}\cdot\boldsymbol{\nu} &= \mathbf{u}_s\cdot\boldsymbol{\nu};\quad \mathbf{u}\cdot\boldsymbol{\tau}=-\varepsilon_\mu(\boldsymbol{\tau}\cdot\mathbf{T}\cdot\boldsymbol{\nu})+\eta\mathbf{u}_s\cdot\boldsymbol{\tau} && \text{on }\Gamma_s(t)\times[0,T]\\
\mathbf{u}\cdot\boldsymbol{\nu} &= 0;\quad \boldsymbol{\tau}\cdot\mathbf{T}\cdot\boldsymbol{\nu}=0 && \text{on }\Gamma_w\times[0,T]\\
-\boldsymbol{\Pi}(\mathbf{u},p)\cdot\boldsymbol{\nu} &= 0 && \text{on }\Gamma_{out}\times[0,T]\\
\mathbf{u} &= \mathbf{u}_{in} && \text{on }\Gamma_{in}\times[0,T].
\end{aligned}$$

Next, the initial conditions are given by

$$\mathbf{u}(x,0)=\mathbf{u}_0,\quad \mathbf{u}_b(x,0)=\mathbf{u}_{b,0},\quad \boldsymbol{\omega}(x,0)=\boldsymbol{\omega}_0;\quad \mathbf{u}_s( s,0)=\mathbf{u}_{b,0}+(\boldsymbol{\omega}_0\times\mathbf{r}).$$

Here, $\sigma$, $\mathcal{K}$, $\mathbf{u}_s$, $\varepsilon_\mu$, $\eta$, $\mathbf{u}_0$, $\mathbf{u}_{b,0}$, $\boldsymbol{\omega}_0$, $\mathbf{r}$, $\boldsymbol{\tau}=(\tau_1,\tau_2)$ and $\boldsymbol{\nu}$ are the surface tension, curvature, total velocity (combination of translation and rotation) of the rigid body, slip coefficient, friction coefficient at the fluid-solid interface, initial fluid velocity, initial translational velocity, initial rotational velocity, position vector from the center of mass in the solid, unit tangential, and outward normal with respect to fluid phase, respectively. Further, the total body force $\mathbf{F}_{flow}$ from the fluid and the total external moments $\mathbf{M}$ are given by

$$\mathbf{F}_{flow}=-\int_{\Gamma_s}\mathbf{T}\cdot\boldsymbol{\nu}\,d\Gamma_s,\qquad \mathbf{M}'=-\int_{\Gamma_s}\mathbf{r}\times(\mathbf{T}\cdot\boldsymbol{\nu})\,d\Gamma_s,\tag{10.7}$$

Here, the prime on $\mathbf{M}$ indicates that the computed moment has to be projected back to principal axes $xyz$ since we have considered rotation equations with respect to principal axes.

### 10.2.3.1 Dimensionless Form

To rewrite the 6-DOF Equations (10.1) and (10.4), and the Navier–Stokes Equation (10.5) in a dimensionless form, we introduce the scaling factors L and U as the characteristic length and velocity, respectively. Further, we define the non-dimensional variables

$$\tilde{x}=\frac{x}{L},\quad \tilde{\mathbf{u}}=\frac{\mathbf{u}}{U},\quad \tilde{\mathbf{u}}_b=\frac{\mathbf{u}_b}{U},\quad \tilde{\mathbf{w}}=\frac{\mathbf{w}}{U},\quad \tilde{t}=\frac{tU}{L},\quad \tilde{p}=\frac{p}{\rho U^2},\quad \tilde{\mathbf{I}}=\frac{I U}{L}$$

and the dimensionless numbers (Reynolds, Weber, Froude, and slip, respectively)

$$\mathrm{Re}=\frac{\rho UL}{\mu_0},\qquad \mathrm{We}=\frac{\rho U^2L}{\sigma},\qquad \mathrm{Fr}=\frac{U^2}{Lg},\qquad \beta=\frac{1}{\varepsilon_\mu\rho U}.$$

Using these dimensionless parameters in the governing equations and omitting the tilde afterwards, we obtain the dimensionless form of the coupled 6-DOF and Navier–Stokes model in ALE form as
