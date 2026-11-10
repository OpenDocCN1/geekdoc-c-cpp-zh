Hence $f$ has well-defined directional derivatives in any direction at the point $(0, 0)$. To better visualise the surface corresponding to $f$, we can first look for some level sets; for example the level set of value $\frac{1}{2}$:

```
sage: solve(f(x,y) == 1/2, y)
[y == x^2]
sage: a = var('a'); h = f(x, a*x^2).simplify_rational(); h
a/(a^2 + 1)
```

Along the parabola of equation $y = ax^2$, except at the origin, $f$ has thus a constant value $f(x, ax^2) = \frac{a}{1+a^2}$. We then display the function $h: a \longmapsto \frac{a}{1+a^2}$:

```
sage: plot(h, a, -4, 4)
```

![](bbox=[0.345, 0.326, 0.655, 0.462])

Figure 4.16 – A vertical cut of the surface under study.

The function $h$ has its maximum at $a = 1$ and its minimum at $a = -1$. The restriction of $f$ to the parabola of equation $y = x^2$ corresponds to the level set at “height” $\frac{1}{2}$; conversely, the restriction to the parabola of equation $y = -x^2$ corresponds to the bottom of the “thawleg” at height $-\frac{1}{2}$. In conclusion, arbitrarily close to the point $(0, 0)$, we can find points where $f$ takes as value $\frac{1}{2}$, or respectively $-\frac{1}{2}$. As a consequence, $f$ is not continuous at the origin.

```
sage: p = plot3d(f(x,y),(x,-2,2),(y,-2,2),plot_points=[150,150])
```

We might also draw horizontal planes to display the level sets of this function with:

```
sage: for i in range(1,4):
....:     p += plot3d(-0.5 + i / 4, (x, -2, 2), (y, -2, 2),\
....:               color=hue(i / 10), opacity=.1)
```

Among the other 3D graphical commands, `implicit_plot3d` allows us to display surfaces defined by an implicit equation of the form $f(x,y,z) = 0$. Let us display for example the Cassini surface (Figure 4.18a) defined by the implicit equation: $(a^2 + x^2 + y^2)^2 = 4a^2x^2 + z^4$.

```
sage: x, y, z = var('x, y, z'); a = 1
sage: h = lambda x, y, z: (a^2 + x^2 + y^2)^2 - 4*a^2*x^2-z^4
sage: implicit_plot3d(h, (x,-3,3), (y,-3,3), (z,-2,2),\
....:                 plot_points=100)
```