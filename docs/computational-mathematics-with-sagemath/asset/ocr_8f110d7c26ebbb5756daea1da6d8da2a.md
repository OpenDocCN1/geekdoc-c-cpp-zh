![](bbox=[0.207, 0.07, 0.797, 0.331])

FIGURE A.3 Integral curves of x^2 y' - y = 0.

```
~~~sage
sage: g += line(liste_pts(-4, 8), rgbcolor = (.01,0,0))
sage: g += line(liste_pts(1.3, 3), rgbcolor = (.5,0,0))
sage: g += plot(f, -1, 3, rgbcolor = 'blue')
sage: g += plot(x, -1, 3, rgbcolor = 'green')
sage: g.show(aspect_ratio = 1, ymin = -.2, ymax = 3)
~~~
```

# **Exercise 14 page 85.** *(First order differential equation, resolved)*

```
~~~sage
sage: x = var('x'); y = function('y')
sage: DE = x^2 * diff(y(x), x) - y(x) == 0
sage: desolve(DE, y(x))
_C*e^(1/x)
sage: g = plot([c*e^(-1/x) for c in srange(-8, 8, 0.4)], (x, -3, 3))
sage: y = var('y')
sage: g += plot_vector_field((x^2, y), (x,-3,3), (y,-5,5))
sage: g.show()
~~~
```

# **Exercise 15 page 87.** *(Predator-prey model)*

```
~~~sage
sage: from sage.calculus.desolvers import desolve_system_rk4
sage: f = lambda x, y: [a*x-b*x*y,-c*y+d*b*x*y]
sage: x, y, t = var('x', 'y', 't')
sage: a, b, c, d = 1, 0.1, 1.5, 0.75
sage: P = desolve_system_rk4(f(x,y), [x,y],\
....:     ics=[0,10,5], ivar=t, end_points=15)
sage: QL = [[i,j] for i,j in P]; p = line(QL, color='red')
sage: p += text("Rabbits", (12,37), fontsize=10, color='red')
sage: QR = [[i,k] for i,k in P]; p += line(QR, color='blue')
sage: p += text("Foxes", (12,7), fontsize=10, color='blue')
sage: p.axes_labels(["time", "population"])
~~~
```