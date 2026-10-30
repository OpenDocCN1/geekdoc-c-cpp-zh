```
> theFit := GenerateEquations(RA, vars);
  theFit := {a[1,0] = -\frac{79000}{1463}, a[1,1] = \frac{71475}{10241}, a[1,2] = \frac{23825}{71687},
  a[2,0] = \frac{511375}{209}, a[2,1] = -\frac{695900}{1463}, a[2,2] = \frac{28275}{931}, a[2,3] = -\frac{40750}{71687}, a[2,4] = -\frac{1525100}{209},
  a[3,1] = \frac{1340575}{1463}, a[3,2] = -\frac{362850}{10241}, a[3,3] = \frac{1825}{3773}, a[4,0] = \frac{3953300}{209}, a[4,1] = -\frac{2768225}{1463},
  a[3,1] = \frac{646350}{10241}, a[4,3] = \frac{7275}{10241}, a[4,4] = -\frac{3553925}{209}, a[5,0] = \frac{389275}{71687}, a[5,1] = -\frac{359275}{1463}, a[5,2] = -\frac{153875}{10241}, a[5,3] = \frac{7175}{71687}};
```

Set the values of the coefficients.

```
> assign(theFit);
```

And plot the results.

```
> SplinePlot := plot(Spline(x), x = X_1..X_N):
  DataPlot := pointplot(Pts, symbol = solidcircle, symbolsize = 18):
  display(SplinePlot, DataPlot);
```

![](bbox=[0.298, 0.395, 0.714, 0.694])

The natural cubic spline fits the data very well. Caution: do not use the spline outside the data! Plot over a larger range to see why.

```
Use Maple’s

CurveFitting:-Spline(Pts, x, 3, endpoints = ’natural’);
```

to verify that we have found the curve.

In general, to connect N knots (data points), we need N − 1 cubic equations. To set up the system of equations, we will need:

+   1. 2(N − 2) equations matching the endpoints of the N − 1 connecting cubic curves,