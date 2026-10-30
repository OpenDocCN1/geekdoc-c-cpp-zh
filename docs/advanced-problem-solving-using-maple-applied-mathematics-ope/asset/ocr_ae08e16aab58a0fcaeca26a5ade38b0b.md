Enter the augmented coefficient matrix for the system into Maple and row reduce to find the solution.

```
A := Matrix([[354, 96, 30, 400], [96, 30, 10, 190], [30, 10, 5, 171]]):
ReducedRowEchelonForm(A);
```

The output yields \(a=-197/111\), \(b=-326/36\), and \(c=11557/185\). Therefore, the quadratic model for our data is

\[f(x)=-\frac{197}{111}x^2-\frac{326}{37}x+\frac{11557}{185}.\]

Check the fit.

```
with(plots):
f := x -> -197/111*x^2 - 326/37*x + 11557/185:
Pts := zip((x, y) -> [x, y], [0..4], []):
DataPlot := pointplot(Pts, symbol = solidcircle, symbolsize = 18):
fPlot := plot(f, -1..5, -10..70, thickness = 2):
display(DataPlot, fPlot);
```

![](bbox=[0.286, 0.563, 0.72, 0.865])

The plot shows visually that the fit captures the trend of the data.

Our next example of an application of systems of linear equations is a different method of fitting a curve to data: this time, smoothly connecting