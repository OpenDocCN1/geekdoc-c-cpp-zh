![](bbox=[0.08, 0.13, 0.77, 0.41])

Figure 6.22. Stream tubes in a 3D vector field (a). Corresponding stream surface (b) and zoomed-in surface detail showing tears in the stream surface (c).

from each point $x$ of the discretization of $\Omega$, a streamline $S$ is traced backwards in the vector field. If $S$ hits $\partial\Omega$ at some point $y$ after a given amount of time, the value $f(y)$ is assigned to all points along it in $\Omega$. After all points of $\Omega$ have been thus visited, we obtain a scalar field $f_\Omega : \Omega \rightarrow \mathbb{R}$. Next, the desired stream surface corresponding to $\Gamma$ can be easily extracted as an isosurface of $f_\Omega$ corresponding to the value that $\Gamma$ takes over $\partial\Omega$, using for example the marching cubes algorithm (Section 5.3.2). Although this method is simple to implement, and delivers at once a family of stream surfaces for different isovalues rather than a single such surface, it cannot extract stream surfaces which do not pass through the boundary of the dataset.

# 6.5.6 Streak Surfaces

For time-dependent vector fields, streak surfaces generalize the notion of streaklines in the same way that stream surfaces generalize the notion of streamlines. Given a seed curve $\Gamma$, a streak surface $S_\Gamma$ is a surface that contains all massless particles that pass through $\Gamma$ at different time moments, or, in other words, the (time-dependent) locus of dye advected in the flow that originates at $\Gamma$.

Conceptually, streak surfaces can be computed using a similar approach to stream surfaces: Streaklines are traced in the flow starting from a densely sam-