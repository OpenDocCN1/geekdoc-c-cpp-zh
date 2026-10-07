# 574 Performance, Reliability, and Availability Evaluation of Computational Systems

Using the time to failure sample, obtain the first two data moments about the origin

```
$m_1 = \frac{\sum_{i=1}^{n} x_i}{n}$
```

and

```
$m_2 = \frac{\sum_{i=1}^{n} x_i^2}{n}$
```

As

```
$$\mu_1 = \frac{a+b}{2} = m_1$
```

and

```
$$\mu_2 = \frac{1}{3}(a^2+ab+b^2) = m_2$,
```

we get

```
$$\hat{a} = \hat{m}_1 - \sqrt{3\hat{m}_2-\hat{m}_1^2} \quad (25.3.14)$
```

and

```
$$\hat{b} = \hat{m}_1 + \sqrt{3\hat{m}_2-\hat{m}_1^2} \quad (25.3.15)$
```

**Example 25.3.6.** Consider one hundred hard disks ($n=100$) were observed in an accelerated lifetime test. The test finished when all hard disks failed. The times each device failed is depicted in Columns ($X_i$) of Table 25.18. The exploratory analysis did not reject the uniform distribution (not shown here). Then, we can estimate the uniform distribution parameters, $a$ and $b$, adopting the method of moments presented. From Columns $X_i$ and $X_i^2$ of Table 25.18, we get

```
$$\m_1 = \frac{\sum_{i=1}^{100} X_i}{100} = \frac{201284.46}{100} = 2012.84h$.
```

and

```
$$\m_2 = \frac{\sum_{i=1}^{100} X_i^2}{100} = \frac{443259330.98}{100} = 4432593.31h^2$.
```

Adopting Equation 25.3.1 and 25.3.15, the uniform distribution parameters are estimated:

```
$$\hat{a} = \hat{m}_1 - \sqrt{3\hat{m}_2-\hat{m}_1^2} = 943.66h$,
```

and

```
$$\hat{b} = \hat{m}_1 + \sqrt{3\hat{m}_2-\hat{m}_1^2} = 3082.03h$.
```