# Table 13.1 PCA data.

| Data |  | Adjusted data |  | In PCA basis |  |
|---|---|---|---|---|---|
| x | y | x | y | x₁ | x₂ |
| 2.5 | 2.4 | 0.69 | 0.49 | −0.828 | −0.175 |
| 0.5 | 0.7 | −1.31 | −1.21 | 1.78 | 0.143 |
| 2.2 | 2.9 | 0.39 | 0.99 | −0.992 | 0.484 |
| 1.9 | 2.2 | 0.09 | 0.29 | −0.274 | 0.130 |
| 3.1 | 3.0 | 1.29 | 1.09 | −1.68 | −0.209 |
| 2.3 | 2.7 | 0.49 | 0.79 | 0.913 | 0.175 |
| 2 | 1.6 | 0.19 | −0.31 | 0.0991 | −0.350 |
| 1.0 | 1.1 | −0.81 | −0.81 | 1.14 | 0.464 |
| 1.6 | 1.6 | −0.31 | −0.31 | 0.438 | 0.0178 |
| 1.1 | 0.9 | −0.71 | −1.01 | 1.22 | −0.163 |

# 13.7.1
Demonstration of Principal Component Analysis

The derivation of PCA and proofs of its theorems can get quite involved. Instead, as our introduction to the subject we take a purely operational approach and work through a simple PCA analysis following the example of (Smith, 2002). We assume that the data have two dimension, and we call these x and y, but they need not be related to spatial positions.

1. Enter Data We start with a data set, in our case the first two columns of Table 13.1.

2. Subtract the Mean PCA analysis assumes that the data in each dimension has zero mean. Accordingly, as shown in columns two and three in Table 13.1, we calculate the mean for each column, (x̄, ȳ), and then subtract them from the data in each column. The resulting adjusted data are given in the third and fourth columns of the table, and placed here into a data matrix:

```
X = ⎛ 0.69   0.49 ⎞
    ⎜ −1.31 −1.21 ⎟
    ⎜ 0.39   0.99 ⎟
    ⎜ 0.09   0.29 ⎟
    ⎜ 1.29   1.09 ⎟
    ⎜ 0.49   0.79 ⎟
    ⎜ 0.19  −0.31 ⎟
    ⎜ −0.81 −0.81 ⎟
    ⎜ −0.31 −0.31 ⎟
    ⎝ −0.71 −1.01 ⎠ .   (13.42)
```