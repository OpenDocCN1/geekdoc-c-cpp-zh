
The Magnus effect was proposed to build propulsion systems made from large vertical rotating cylinders able to produce a longitudinal thrust when the wind is perpendicular to the ship (this was the case of the Baden-Baden rotor ship built by Anton Flettner, which crossed the Atlantic in 1926).

### 4.1.7 Evolute of a Curve

We now give an example of drawing the evolute of a parametric arc (let us recall that the evolute is the envelope of the normals of a curve, or equivalently, the locus of centres of curvature).

EXAMPLE. (*Evolute of the parabola*) Let us find the equation of the evolute of the parabola $\mathcal{P}$ of equation $y=x^2/4$, and show on the same graph the parabola $\mathcal{P}$, some normals to $\mathcal{P}$ and its evolute.

To determine a system of parametric equations $(x(t),y(t))$ of the evolute of a family of lines $\Delta_t$ defined by cartesian equations of the form $\alpha(t)X+\beta(t)Y=\gamma(t)$, we express the fact that the line $\Delta_t$ is tangent to the envelope at $(x(t),y(t))$:

\[ \alpha(t)x(t)+\beta(t)y(t)=\gamma(t), \quad (4.1) \]
\[ \alpha(t)x'(t)+\beta(t)y'(t)=0. \quad (4.2) \]

The derivative of Equation (4.1), combined with (4.2), yields the system:

\[ \alpha(t)x(t)+\beta(t)y(t)=\gamma(t), \quad (4.1) \]
\[ \alpha'(t)x(t)+\beta'(t)y(t)=\gamma'(t). \quad (4.3) \]

In our case, the normal $(N_t)$ to the parabola $\mathcal{P}$ in $M(t,t^2/4)$ has normal vector $\vec{v}=(1,t/2)$ (which is tangent to the parabola); it thus has for equation:

\[ \begin{pmatrix} x-t \\ y-t^2/4 \end{pmatrix} \cdot \begin{pmatrix} 1 \\ t/2 \end{pmatrix}=0 \quad\Longleftrightarrow\quad x+\frac{t}{2}y=t+\frac{t^3}{8}, \]

in other words, $(\alpha(t),\beta(t),\gamma(t))=(1,t/2,t+t^3/8)$. We can then solve the preceding system with the solve function:

```sage
sage: x, y, t = var('x, y, t')
sage: alpha(t) = 1; beta(t) = t / 2; gamma(t) = t + t^3 / 8
sage: env = solve([alpha(t) * x + beta(t) * y == gamma(t),\
....:     diff(alpha(t), t) * x + diff(beta(t), t) * y == \
....:     diff(gamma(t), t)], [x,y])
```

\[ \boxed{\left[x=-\frac14 t^3,\quad y=\frac34 t^2+2\right]} \]

This gives a parametric representation of the normal envelope:

\[ \begin{cases} x(t)=-\frac14 t^3,\\ y(t)=2+\frac34 t^2. \end{cases} \]

We can then answer the given question, by drawing some normals to the parabola (more precisely, we draw line segment $[M,M+18\vec{n}]$ where $M(u,u^2/4)$ is a point on $\mathcal{P}$ and $\vec{n}=(-u/2,1)$ a normal vector to $\mathcal{P}$):

| Type of drawing | Function |
|---|---|
| Graph of a function | `plot` |
| Parametric curve | `parametric_plot` |
| Curve defined by a polar equation | `polar_plot` |
| Curve defined by an implicit equation | `implicit_plot` |
| Level set of a complex function | `complex_plot` |
| Empty graphical object | `Graphics()` |
| Integral curves of a differential equation | `odeint, desolve_rk4` |
| Bar graph, bar chart | `bar_chart` |
| Histogram of a statistical sequence | `plot_histogram` |
| Polygonal chain | `line` |
| Cloud of points | `points` |
| Circle | `circle` |
| Polygon | `polygon` |
| Text | `text` |

Table 4.1 — Summary of 2D graphical functions.

```sage
sage: T(t) = [df(t)[0] / df(t).norm(), df(t)[1] / df(t).norm()]
sage: N(t) = [-df(t)[1] / df(t).norm(), df(t)[0] / df(t).norm()]
sage: R(t) = (df(t).norm())^3 / (df(t)[0]*d2f(t)[1]-df(t)[1]*d2f(t)[0])
sage: Omega(t) = [f(t)[0] + R(t)*N(t)[0], f(t)[1] + R(t)*N(t)[1]]
sage: g = parametric_plot(f(t), (t,-8,8), color='green',thickness=2)
sage: for u in srange(.4, 4, .2):
....:     g += line([f(t=u), Omega(t=u)], color='red', alpha = .5)
....:     g += circle(Omega(t=u), R(t=u), color='blue')
sage: g.show(aspect_ratio=1,xmin=-12,xmax=7,ymin=-3,ymax=12)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_103_0.png)

Figure 4.14 — Osculating circles of the parabola.

Table 4.1 gives a summary of the functions detailed in this section. It also contains the text command which enables us to add a character string in a graph, and the polygon command to plot polygons.

## 4.2 3D Curves

Sage provides the `plot3d(f(x,y),(x,a,b),(y,c,d))` command to display surfaces in 3 dimensions. The surface obtained may then be visualised via the Jmol application; the Tachyon 3D Ray Tracer or three.js can be used alternatively with the option `viewer='tachyon'` or `viewer='threejs'` of the show command. Here is a first example of parametric surface (Figure 4.15):

```sage
sage: u, v = var('u, v')
sage: h = lambda u,v: u^2 + 2*v^2
sage: plot3d(h, (u,-1,1), (v,-1,1), aspect_ratio=[1,1,1])
```

![](img/99840d73c45ee58b635c4eedc727fd9a_104_0.png)

FIGURE 4.15 The parametric surface $(u, v) \mapsto u^2 + 2v^2$.

Displaying the surface corresponding to a 2-variable function helps us to study that function, as will be seen in the following example.

EXAMPLE. (*A discontinuous function whose directional derivatives exist everywhere!*) Study the existence in $(0,0)$ of the directional derivatives and the continuity of the function $f$ from $\mathbb{R}^2$ to $\mathbb{R}$ defined by:

\[
f(x,y)=
\begin{cases}
\dfrac{x^2y}{x^4+y^2}, & (x,y)\ne(0,0),\\
0, & (x,y)=(0,0).
\end{cases}
\]

For $H=[\cos\theta;\sin\theta]$, the function $\varphi(t)=f(tH)=f(t\cos\theta,t\sin\theta)$ is differentiable in $t=0$ for any value of $\theta$; indeed,

```sage
sage: f(x, y) = x^2 * y / (x^4 + y^2)
sage: t, theta = var('t, theta')
sage: limit(f(t * cos(theta), t * sin(theta)) / t, t=0)
cos(theta)^2/sin(theta)
```

Hence $f$ has well-defined directional derivatives in any direction at the point $(0, 0)$. To better visualise the surface corresponding to $f$, we can first look for some level sets; for example the level set of value $\frac{1}{2}$:

```sage
sage: solve(f(x,y) == 1/2, y)
[y == x^2]
sage: a = var('a'); h = f(x, a*x^2).simplify_rational(); h
a/(a^2 + 1)
```

Along the parabola of equation $y = ax^2$, except at the origin, $f$ has thus a constant value $f(x, ax^2) = \frac{a}{1+a^2}$. We then display the function $h: a \longmapsto \frac{a}{1+a^2}$:

```sage
sage: plot(h, a, -4, 4)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_105_0.png)

Figure 4.16 – A vertical cut of the surface under study.

The function $h$ has its maximum at $a = 1$ and its minimum at $a = -1$. The restriction of $f$ to the parabola of equation $y = x^2$ corresponds to the level set at “height” $\frac{1}{2}$; conversely, the restriction to the parabola of equation $y = -x^2$ corresponds to the bottom of the “valley” at height $-\frac{1}{2}$. In conclusion, arbitrarily close to the point $(0, 0)$, we can find points where $f$ takes as value $\frac{1}{2}$, or respectively $-\frac{1}{2}$. As a consequence, $f$ is not continuous at the origin.

```sage
sage: p = plot3d(f(x,y),(x,-2,2),(y,-2,2),plot_points=[150,150])
```

We might also draw horizontal planes to display the level sets of this function with:

```sage
sage: for i in range(1,4):
....:     p += plot3d(-0.5 + i / 4, (x, -2, 2), (y, -2, 2),\
....:               color=hue(i / 10), opacity=.1)
```

Among the other 3D graphical commands, `implicit_plot3d` allows us to display surfaces defined by an implicit equation of the form $f(x,y,z) = 0$. Let us display for example the Cassini surface (Figure 4.18a) defined by the implicit equation: $(a^2 + x^2 + y^2)^2 = 4a^2x^2 + z^4$.

```sage
sage: x, y, z = var('x, y, z'); a = 1
sage: h = lambda x, y, z: (a^2 + x^2 + y^2)^2 - 4*a^2*x^2-z^4
sage: implicit_plot3d(h, (x,-3,3), (y,-3,3), (z,-2,2),\
....:                 plot_points=100)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_106_0.png)

FIGURE 4.17 – The surface corresponding to $f : (x,y) \mapsto \frac{x^2 y}{x^4+y^2}$.

Finally, let us give an example of 3-dimensional curve (Figure 4.18b) with the line3d command:

```sage
sage: line3d(([-10*cos(t)-2*cos(5*t)+15*sin(2*t),\
....:       -15*cos(2*t)+10*sin(t)-2*sin(5*t),\
....:       10*cos(3*t)) for t in srange(0,6.4,.1)],radius=.5)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_106_1.png)

(a) The Cassini surface.

(b) A knot in space.

FIGURE 4.18 – Surface and curve in 3D.
