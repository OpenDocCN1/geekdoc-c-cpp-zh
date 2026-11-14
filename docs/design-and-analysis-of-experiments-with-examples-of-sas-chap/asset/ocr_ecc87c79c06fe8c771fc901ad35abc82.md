```
data Process;
input 5 68;
datalines;
1.13 1.25 .97 1.70 1.47 1.28 1.18 .98
.78 1.36 1.85 .62 1.09 1.10 .76 2.1
data soup; merge design process;
```

# Table 6.4 2<sup>-1</sup> Experiment To Determine Which Factors Are Associated with Fill Variation in Random Order

| Batch | (A) Number of Ports | (B) Temperature | (C) Mixing Time (sec) | (D) Batch Weight (lbs) | (E) Delay (days) | Response $\sigma_p$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | Cool Water | 60 | 2000 | 7 | 0.78 |
| 2 | 3 | Cool Water | 80 | 2000 | 7 | 1.10 |
| 3 | 3 | Ambient | 60 | 1500 | 1 | 1.70 |
| 4 | 3 | Cool Water | 80 | 1500 | 1 | 1.28 |
| 5 | 1 | Ambient | 60 | 1500 | 7 | 0.97 |
| 6 | 1 | Cool Water | 80 | 1500 | 7 | 1.47 |
| 7 | 1 | Ambient | 60 | 2000 | 1 | 1.85 |
| 8 | 3 | Ambient | 80 | 2000 | 1 | 2.10 |
| 9 | 1 | Ambient | 80 | 2000 | 7 | 0.76 |
| 10 | 3 | Ambient | 60 | 2000 | 7 | 0.62 |
| 11 | 1 | Cool Water | 80 | 2000 | 1 | 1.09 |
| 12 | 1 | Cool Water | 60 | 1500 | 1 | 1.13 |
| 13 | 3 | Cool Water | 60 | 1500 | 7 | 1.25 |
| 14 | 3 | Ambient | 80 | 1500 | 7 | 0.98 |
| 15 | 3 | Cool Water | 60 | 2000 | 1 | 1.36 |
| 16 | 1 | Ambient | 80 | 1500 | 1 | 1.18 |

The SAS commands to fit the model in the main effects and two-factor interactions and to make a normal probability plot of the regression coefficients, are shown on the next page. This is the same thing that was done in Section 3.7.5, except only 15 terms are included in the model rather than the full model which would contain main effects and interactions up to order 5. Each effect in this model is confounded with one other interaction as shown in the alias pattern on the previous page. Therefore only 15 effects can be estimated.

As can be seen in the normal plot of effects, the main effect E (Delay Time between mixing and packaging), BE (the interaction between Temperature and Delay Time), and DE (the interaction between Batch Weight and Delay Time) appear to be significant. If the hierarchical effect ordering can be as-