# Table 5.12 Pesticide Residue on Cotton Plants

| Formulation | Application Technique | Plot | Sample 1 | Sample 2 |
|---|---|---|---|---|
| A | 1 | 1 | 0.237 | 0.252 |
| A | 1 | 2 | 0.281 | 0.274 |
| B | 1 | 1 | 0.247 | 0.294 |
| B | 1 | 2 | 0.321 | 0.267 |
| A | 2 | 1 | 0.392 | 0.378 |
| A | 2 | 2 | 0.381 | 0.346 |
| B | 2 | 1 | 0.351 | 0.362 |
| B | 2 | 2 | 0.334 | 0.348 |

where \( y_{ijkl} \) is the pesticide residue found on the \( l \)th sample taken from the \( k \)th plot, treated with formulation level \( i \) and application technique \( j \). In general \( i = 1, ..., a, j = 1, ..., b, k = 1, ..., r \), and \( l = 1, ..., s \). In this specific example, \( a = 2, b = 2, r = 2 \), and \( s = 2 \), \( \alpha_i \) is the formulation effect, \( \beta_j \) is the application effect, \( \alpha\beta_{ij} \) is the interaction effect, \( \rho_{(ij)k} \) is the random plot effect, and \( \epsilon_{ijkl} \) is the random sample effect.

The model can be written in matrix notation as:

```
\(\boldsymbol{y} = \boldsymbol{X}\boldsymbol{\beta} + \boldsymbol{Z}\boldsymbol{\gamma} + \boldsymbol{\epsilon}, \quad (5.14)\)
```

where

```
\(\boldsymbol{y} = \begin{pmatrix} y_{1111} \\ y_{1112} \\ y_{1121} \\ y_{1122} \\ y_{2111} \\ y_{2112} \\ y_{2121} \\ y_{2122} \\ y_{1211} \\ y_{1212} \\ y_{1221} \\ y_{1222} \\ y_{2121} \\ y_{2122} \\ y_{2211} \\ y_{2212} \\ y_{2221} \\ y_{2222} \end{pmatrix}, \quad \boldsymbol{X} = \begin{pmatrix} 1 & 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 0 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \\ 1 & 0 & 1 & 0 & 1 & 0 & 0 & 0 & 1 \end{pmatrix}, \quad \boldsymbol{\beta} = \begin{pmatrix} \mu \\ \alpha_1 \\ \alpha_2 \\ \beta_1 \\ \beta_2 \\ \alpha\beta_{11} \\ \alpha\beta_{12} \\ \alpha\beta_{21} \\ \alpha\beta_{22} \end{pmatrix}\)
```