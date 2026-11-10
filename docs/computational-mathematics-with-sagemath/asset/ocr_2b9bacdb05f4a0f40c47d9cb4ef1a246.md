# 4.1.2　Parametric Curve

Parametric curves \((x = f(t),\ y = g(t))\) may be visualised using the command `parametric_plot((f(t), g(t)), (t, a, b))`, where \([a, b]\) is the interval over which the parameter \(t\) ranges.

Let us show the parametric curve defined by the equations:

\[
\begin{cases}
x(t)=\cos(t)+\frac{1}{2}\cos(7t)+\frac{1}{3}\sin(17t),\\
y(t)=\sin(t)+\frac{1}{2}\sin(7t)+\frac{1}{3}\cos(17t).
\end{cases}
\]

```
```sage
sage: t = var('t')
sage: x = cos(t) + cos(7*t)/2 + sin(17*t)/3
sage: y = sin(t) + sin(7*t)/2 + cos(17*t)/3
sage: g = parametric_plot((x, y), (t, 0, 2*pi))
sage: g.show(aspect_ratio=1)
```
```

![](bbox=[0.305, 0.416, 0.693, 0.676])

Figure 4.4 – Parametric curve of equation \(x(t)=\cos(t)+\frac{1}{2}\cos(7t)+\frac{1}{3}\sin(17t)\), \(y(t)=\sin(t)+\frac{1}{2}\sin(7t)+\frac{1}{3}\cos(17t)\).

# 4.1.3　Curve in Polar Coordinates

Curves in polar coordinates \(\rho = f(\theta)\), where the parameter \(\theta\) spans the interval \([a, b]\), may be drawn by the command `polar_plot(rho(theta), (theta,a,b))`. For example, let us see graphically the rose-curves with polar equation \(\rho(\theta)=1+e\cdot\cos(n\theta)\) when \(n=20/19\) and \(e\in\{2,1/3\}\).

```
```sage
sage: t = var('t'); n = 20/19
sage: g1 = polar_plot(1+2*cos(n*t),(t,0,n*36*pi),plot_points=5000)
sage: g2 = polar_plot(1+1/3*cos(n*t),(t,0,n*36*pi),plot_points=5000)
```
```