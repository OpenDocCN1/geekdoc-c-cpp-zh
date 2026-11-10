```
1/3*x^2 - 7/3*x - 82/9*cos(sqrt(3))*sin(sqrt(3)*x)/sin(sqrt(3))
+ 115/9*sin(sqrt(3)*x)/sin(sqrt(3)) - 82/9*cos(sqrt(3)*x) + 91/9
```

that is

$\frac{1}{3}x^2-\frac{7}{3}x-\frac{82\sin(\sqrt{3}x)\cos(\sqrt{3})}{9\sin(\sqrt{3})}+\frac{115\sin(\sqrt{3}x)}{9\sin(\sqrt{3})}-\frac{82}{9}\cos(\sqrt{3}x)+\frac{91}{9}.$

**How to Solve a PDE: the Heat Equation.** Next we will study the famous heat equation. The temperature $z$ is distributed in a homogeneous rectilinear rod of length $\ell$ according to the equation (where $x$ is the abscissa along the rod, and $t$ the time):

$\frac{\partial^2 z}{\partial x^2}(x,t)=C\frac{\partial z}{\partial t}(x,t).$

This equation will be studied against the following initial conditions:

$\forall t\in\mathbb{R}^+,\quad z(0,t)=0\quad z(\ell,t)=0\quad \forall x\in]0,\ell[,\quad z(x,0)=1.$

We will seek non-zero solutions of the form:

$z(x,t)=f(x)g(t).$

This is the method of separation of variables.

```
sage: x, t = var('x, t'); f = function('f')(x); g = function('g')(t)
sage: z = f*g
sage: eq(x,t) = diff(z,x,2) == diff(z,t); eq(x,t)
g(t)*diff(f(x), x, x) == f(x)*diff(g(t), t)
```

The equation thus becomes:

$g(t)\frac{d^2f(x)}{dx^2}=f(x)\frac{dg(t)}{dt}.$

Let us divide by $f(x)g(t)$, assumed not to be zero:

```
sage: eqn = eq/z; eqn(x,t)
diff(f(x), x, x)/f(x) == diff(g(t), t)/g(t)
```

We then obtain an equation where each side depends only on one variable:

$\frac{1}{f(x)}\frac{d^2f(x)}{dx^2}=\frac{1}{g(t)}\frac{dg(t)}{dt}.$

Each side can therefore only be constant. Let us separate equations and introduce a constant $k$:

```
sage: k = var('k')
sage: eq1(x,t) == eqn(x,t).lhs() == k; eq2(x,t) = eqn(x,t).rhs() == k
```

We solve the equations separately, beginning with the second one:

```
sage: g(t) = desolve(eq2(x,t), g(t)); g(t)
```