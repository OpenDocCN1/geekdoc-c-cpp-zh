```
```text
> myOptions := (scaling = constrained, axes = framed, thickness = 2) :
  plot([sin(x), x^0.5], x = 0..5, myOptions);
```
```

![](bbox=[0.3, 0.2, 0.73, 0.41])

```
```text
> with(plots) :
> curve := plot(30 · sin(x), x = 0..30) :
> points := pointplot(agewt, symbol = diamond, symbolsize = 14) :
> display(curve, points);
```
```

![](bbox=[0.29, 0.58, 0.72, 0.87])