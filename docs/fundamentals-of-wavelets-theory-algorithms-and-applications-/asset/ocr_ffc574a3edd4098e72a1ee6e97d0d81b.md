![](bbox=[0.156, 0.086, 0.818, 0.326])

# Linear Spline (m = 2)

```
(7.63) 
\(\lambda_1 = -2 + \sqrt{3} = \frac{1}{\lambda_2}.\)
```

```
(7.64) 
\(p[k] = (-1)^{|k|} \sqrt{3} (2 - \sqrt{3})^{|k|}.\)
```

# Cubic Spline (m = 4)

```
(7.65) 
\(\left\{\begin{array}{l} \lambda_1 = -9.1486946 \times 10^{-3} = 1/\lambda_6 \\ \lambda_2 = -0.1225546 = 1/\lambda_5 \\ \lambda_3 = -0.5352805 = 1/\lambda_4. \end{array}\right.\)
```

# 7.6.2 Change of Basis for Spline Wavelets

Here our objective is to write

```
(7.66) 
\(r(t) = \sum_k \tilde{w}_k \tilde{\psi}_m(t-k) = \sum_k w_k \psi_m(t-k).\)
```