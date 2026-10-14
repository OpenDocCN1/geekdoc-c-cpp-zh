
d\mathbf{u}_b / dt = (\rho L^3 / m) \mathbf{F}_{flow} + 1/Fr \mathbf{e}, \quad in (0,I]
I_{xx} d\omega_x / dt + (I_{zz} - I_{yy}) \omega_y \omega_z = \rho / \rho_s M_x, \quad in (0,I]
I_{yy} d\omega_y / dt + (I_{xx} - I_{zz}) \omega_z \omega_x = \rho / \rho_s M_y, \quad in (0,I]
I_{zz} d\omega_z / dt + (I_{yy} - I_{xx}) \omega_x \omega_y = \rho / \rho_s M_z, \quad in (0,I]
\partial \mathbf{u} / \partial t + (\mathbf{u} - \mathbf{w}) \cdot \nabla \mathbf{u} - \nabla \cdot \mathbb{T}(\mathbf{u},p) = 1/Fr \mathbf{e} \quad in \Omega(t) \times (0,I],
\nabla \cdot \mathbf{u} = 0 \quad in \Omega(t) \times (0,I] \quad (10.8)
-\mathbb{T}(\mathbf{u},p) \cdot \nu = \mathscr{K} / We, \quad in \Gamma_{fs}(t) \times [0,T]
\mathbf{u} \cdot \nu = \mathbf{u}_s \cdot \nu; \quad \mathbf{u} \cdot \tau - \eta \mathbf{u}_s \cdot \tau = -1/\beta (\tau \cdot \mathbb{T} \cdot \nu), \quad in \Gamma_s(t) \times [0,T]
\mathbf{u} \cdot \nu = 0; \quad \tau \cdot \mathbb{T} \cdot \nu = 0, \quad in \Gamma_w \times [0,T]
-\mathbb{T}(\mathbf{u},p) \cdot \nu = 0, \quad in \Gamma_{out} \times [0,T]
\mathbf{u} = \mathbf{u}_{in} / U, \quad in \Gamma_{in} \times [0,T]
\mathbf{u}(\mathbf{x},0) = \mathbf{u}_0 / U; \quad \omega_s(\mathbf{x},0) = U / L \omega_{s,0}.

Here, the dimensionless stress tensor, the total body force F_flow from the fluid and the total external moments M are given by
\mathbb{T}(\mathbf{u},p) = 2/Re \mathbb{D}(\mathbf{u}) - p \mathbb{I}; \quad \mathbf{F}_{flow} = -\int_{\Gamma_s} \mathbb{T} \cdot \eta d\Gamma_s; \quad M' = -\int_{\Gamma_s} \mathbf{r} \times (\mathbb{T} \cdot \eta) d\Gamma_s.

Note that a traction forces (if known) can be used instead of surface force on the free surface.

## 10.3 Interface Tracking Methods

Tracking/capturing the moving or deforming interfaces and boundaries is one of the main challenges in moving boundary value problems. Several numerical methods have been proposed to track or capture the moving boundaries. We will recall a few Eulerian and Lagrangian methods briefly.

### 10.3.1 Eulerian Approaches

#### 10.3.1.1 Volume of Fluid Method

In the volume-of-fluid method (VOF), a "volume-of-fluid function" (also called "marker function") is used to identify each fluid phase. The "volume-of-fluid function" gives the

The main challenge lies in the calculation of the local curvature of the interface from the volume fraction. Furthermore, guaranteeing the mass conservation separately for “Liquid A” and “Liquid B” is also very challenging in this method, see [11]. A number of recent developments, including a technique to improve the resolution of the interface with higher-order schemes [10] and local mass preserving schemes [11], have increased applicability of this method.

### 10.3.1.2 Level Set Method

A continuous zero-level set function represents the interface in the level set method. The level set function $\phi(x,t)$ is constructed as signed distance function in such a way that $\phi(x,t)>0$ holds on one side of the interface and $\phi(x,t)<0$ holds on the other side of the interface. Similarly, several interfaces can be represented by the same level set function $\phi(x,t)$.

As an example, let us consider an interface of an unit circle centre at origin at time $t=0$. We assume that the interface inside a square domain $[-2,2]$, which is meshed by a square grid (Figure 10.4). A signed distance level set function, pictures which have positive values inside the circle and negative values outside the circle, at a time $t=0$ is defined by

$$\phi(x,0)=1-\sqrt{x^2+y^2}.$$

Here, the zero level set function $\phi(x,0)=0$, represents the interface. Given the fluid velocity **u** on the background mesh, the interface is advected by solving the advection equation

$$\frac{\partial \phi(x,t)}{\partial t}+\mathbf{u}\cdot\nabla\phi(x,t)=0,$$

for a new level set function at time $t\geq 0$. The numerical error, which is obtained by discretizing the advection equation, causes a problem to guarantee mass conservation in each fluid phase. In particular, the most losses are significant on coarse meshes [10]. More accurate and robust numerical schemes (for e.g., higher order ENO/WENO) are proposed in the literature to solve this type of advection equation. In the finite element context, the mass loss can be reduced by using finer meshes. However, the computational costs would enormously increase. Alternatively, a mass correction scheme has been used in [12]. Additionally, a stabilization technique such as streamline diffusion (SDFEM) has to be used for advection equation to get a stable system [12, 13].

Moreover, it is essential that $\phi(x,t)$ remains as a signed distance function to guarantee mass conservation. In general, this property is not preserved during the advection and thus a reinitialization technique has been proposed in the literature to overcome this difficulty. Recent advances in the level set method, add the natural ability to handle the topological changes of the interface, make the method attractive.

### 10.3.1.3 Front Tracking Method

The basic idea behind the front tracking method is to use separate front markers for the interface on a fixed mesh and modify the mesh near the front to fit the interface. The method which we discuss here is a hybrid one between the front tracking and the front capturing methods [14]. The main idea is to use stationary meshes for the fluid flow and a separate one-dimensional lower moving mesh to track the interface. The front points (interface mesh points) are advected by the computed velocity, where the velocity at each front is obtained by an interpolation from the fixed background mesh.

![](img/81c56bc4b2fca1951aff5e0ab85b66be_181_0.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_181_1.png)

FIGURE 10.4
The level set function φ(x,0) (left) and their contours (right).

For example, in a two-space dimension, the interface is represented by a one-dimensional moving “front” consisting of connected front points χ_F. In general, smooth function (for e.g., Legendre polynomials or interpolated cubic splines) is constructed from the front points to calculate the curvature, [14, 15]. Once the fluid velocity u on the fixed background meshes is calculated, the velocity is interpolated at the front points. Then, the new position of the interface is obtained by the equation.

```
∂χ_F/∂t = ℐ_XF u(χ_F, t),
```

where ℐ_XF is the interpolated velocity from the background mesh to the front points χ_F. Since front points are moved in a Lagrangian manner, these points may accumulate or the solution becomes inadequate at some part of the interface. It can be addressed by adding and deleting or redistributing the front points. In front tracking method there is no need to solve any additional equation to advect the interface. However, one has to solve some algebraic equations to construct a parametrized curve, calculate the curvature, and redistribute the front points.

Since the interface is tracked explicitly, topological changes such as breaking and merging of interfaces have to be done manually. Furthermore, the interface is not advected by an interpolated velocity and generally this interpolated velocity is not divergence-free at the front points. Therefore, guaranteeing the mass conservation in each phase is a challenge in the front tracking method.

### 10.3.2 Lagrangian Approaches

Even though there are several advantages in computations when using Eulerian approaches, the Lagrangian approach is preferred for flows with rigid bodies. Since the interface is not deforming, interface resolved mesh in the Lagrangian approach can be used to develop efficient and accurate numerical schemes.

#### 10.3.2.1 Arbitrary Lagrangian Eulerian Approach

An early description of the ALE approach was given in [16]. The ALE approach is quite popular for fluid structure interaction and free-surface/two-phase problems. For the application to free-surface flows in the finite element context, we refer to [17, 18, 19, 20, 21, 22, 23]. Here, we recall the ALE approach which is based on the description in [23].

Let us denote the boundary points of all interfaces by χ_F. In the ALE approach, the boundary points χ_F are advected with their corresponding velocity, as

```
dχ_F/dt = u(χ_F, t)
```

and the inner points can be moved arbitrarily to preserve the mesh quality.

Let us define a family of mappings 𝒳_t, which at each time t ∈ [0,1) map a point (namely ALE coordinate) Ŷ ∈ Ω̂ of a reference domain Ω̂ onto a point (namely Eulerian coordinate) X of the current domain Ω_t. That is,

```
𝒳_t : Ω̂ → Ω(t),    𝒳_t(Y) = X(Y, t)
```
