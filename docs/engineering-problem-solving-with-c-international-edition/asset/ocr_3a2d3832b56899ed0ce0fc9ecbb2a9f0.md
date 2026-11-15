# 1. PROBLEM STATEMENT

Use the least-squares technique to determine a linear model for estimating the ozone-mixing ratio at a specified altitude.

# 2. INPUT/OUTPUT DESCRIPTION

The following I/O diagram shows that the input is the data file zone1.txt, and the output is the range of altitudes and the linear model:

![](bbox=[0.28, 0.3, 0.9, 0.38])

# 3. HAND EXAMPLE

Assume that the data consist of the four data points in the following table.

| Altitude (km) | Ozone Mixing Ratio (ppmv) |
|---|---|
| 20 | 3 |
| 24 | 4 |
| 26 | 5 |
| 28 | 6 |

We now need to evaluate Equations (3.1) and (3.2), which are repeated here for convenience:

```
m = \frac{\sum_{k=1}^n x_k \cdot \sum_{k=1}^n y_k - n \cdot \sum_{k=1}^n x_k y_k}{(\sum_{k=1}^n x_k)^2 - n \cdot \sum_{k=1}^n x_k^2},

b = \frac{\sum_{k=1}^n x_k \cdot \sum_{k=1}^n x_k y_k - \sum_{k=1}^n x_k^2 \cdot \sum_{k=1}^n y_k}{(\sum_{k=1}^n x_k)^2 - n \cdot \sum_{k=1}^n x_k^2}.
```

To evaluate these equations using the data from the hand example, we need to compute the following group of sums:

```
\sum_{k=1}^4 x_k = 20 + 24 + 26 + 28 = 98,
```