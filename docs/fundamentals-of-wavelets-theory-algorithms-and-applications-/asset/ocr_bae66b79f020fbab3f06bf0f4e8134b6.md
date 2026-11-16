![](bbox=[0.15, 0.08, 0.82, 0.22])

![](bbox=[0.15, 0.23, 0.82, 0.45])

# 4.10.2 Marginal Properties

Of particular concern to signal processing is the energy conservation. This is expressed by the marginal properties of the distribution

```
(4.72) 
\(\int_{-\infty}^{\infty} \mathbf{W}_f(t, \omega) d\omega = |f(t)|^2\)
```

```
(4.73) 
\(\int_{-\infty}^{\infty} \mathbf{W}_f(t, \omega) dt = |\hat{f}(\omega)|^2\)
```

Marginal (density) expresses the energy density in terms of one of the two variables alone. If we wish to find the energy density in terms of t, we simply integrate (sum up) the distribution with respect to \(\omega\) and vice versa. The total