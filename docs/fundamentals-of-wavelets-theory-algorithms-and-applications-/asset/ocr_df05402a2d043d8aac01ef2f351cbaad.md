amount—16 in this case—from the value that is over the threshold for this pass. For example, the coefficient 58 has 58 – 32 – 16 = 10 yet to be refined by the next iteration. In addition, one should also remember that the coded values are now replaced by zero in the coefficient map and will not be coded from later iterations.

# 3. We repeat step 1 with the second dominant pass with a threshold T₁ = 16. We have the following codes from this pass.

| Coefficient Value | Symbol | Reconstructed Value | Coefficient Value | Symbol | Reconstructed Value |
|---|---|---|---|---|---|
| 29 | P | 24 | -11 | Z | 0 |
| -17 | N | -24 | -3 | Z | 0 |
| -13 | ZTR | 0 | 6 | Z | 0 |
| 22 | P | 24 | -13 | Z | 0 |
| -14 | ZTR | 0 | 2 | Z | 0 |
| -9 | IZ | 0 | 10 | Z | 0 |
| -11 | ZTR | 0 | -5 | Z | 0 |
| 25 | P | 24 | -22 | N | -24 |
| -9 | ZTR | 0 | 4 | Z | 0 |
| -16 | N | -24 | 9 | Z | 0 |
| 12 | ZTR | 0 | -1 | Z | 0 |
| -8 | Z | 0 | 0 | Z | 0 |
| 13 | Z | 0 | -30 | N | -24 |
| 3 | Z | 0 | -7 | Z | 0 |
| 4 | Z | 0 | -1 | Z | 0 |
| 5 | Z | 0 | 6 | Z | 0 |
| 8 | Z | 0 | -8 | Z | 0 |
| -1 | Z | 0 | 2 | Z | 0 |
| 10 | Z | 0 | 5 | Z | 0 |

4. The second subordinate pass will separate the intervals more finely by dividing all intervals at their midpoints. Hence we have intervals (64,56), (56,48), (40,32), (32,24), and (24,16). This pass also updates all