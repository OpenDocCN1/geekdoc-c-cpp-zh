*diff* & *Diff*: differentiation or partial differentiation and ‘indefinite’ differentiation

*int* & *Int*: definite and indefinite integration

For example, let’s differentiate an expression $y = 2x^2 + 24.1x - 1$, and then find the area under the curve in general and from $x = 1$ to $x = 4$.

```
```text
> y := 2x^2 + 24.1 · x − 1
y := 2x^2 + 24.1x − 1
```
```

```
```text
> Diff(y, x)
\frac{d}{dx}(2x^2 + 24.1x - 1)
```
```

```
```text
> diff(y, x)
4x + 24.1
```
```

```
```text
> Int(y, x)
∫ (2x² + 24.1x − 1) dx
```
```

```
```text
> int(y, x)
0.6666666667x³ + 12.05000000x² − x
```
```

```
```text
> Int(y, x = 1..4)
∫₁⁴ (2x² + 24.1x − 1) dx
```
```

```
```text
> int(y, x = 1..4)
219.7500000
```
```

Note the difference between *diff* and *Diff*. The capital letters indicate the “inert form” of the command.

Often, we want to find critical points of the first derivative (where $y' = 0$). We can use the *solve* command as follows,

```
```text
> solve(diff(y, x) = 0, x);
−6.025000000
```
```

# Plotting and Graphs

Maple has an extremely detailed and developed *plot* command, which provides graphs in both two and three dimensions. For modeling purposes, 2-D plots will typically be used. We suggest loading the plots package, via *with(plots)*, prior to plotting. The syntax for *plot* is *plot(y, hr, vr, options)*, where *y* is the expression to be plotted, *hr* is the horizontal range and *vr* is the vertical range. Additionally, many other options can be added after the vertical range to control a variety of items. Table 1.5 presents a short list of options (defaults