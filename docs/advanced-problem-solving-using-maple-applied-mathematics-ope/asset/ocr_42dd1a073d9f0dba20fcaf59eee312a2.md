matrices. Find the dominant eigenvector of each matrix. The power method is often used to calculate eigenvectors; see, e.g., [BurdenFairies2005]. The goal, in AHP, is to obtain a set of eigenvectors of the system that measure the importance of alternatives with respect to the criteria.

**TABLE 8.10: Saaty’s Nine-Point Scale**

| Importance level | Definition |
|---|---|
| 1 | Equal importance |
| 3 | Moderate importance |
| 5 | Strong importance |
| 7 | Very Strong importance |
| 9 | Extreme importance |

**TABLE NOTES:** Even numbers represent intermediate importance levels which should only be used as compromises. If the importance level of A to B is 3, then that of B to A is 1/3, the reciprocal.

Saaty’s *consistency ratio* $CR$ measures the consistency of the pairwise assessments of relative importance. The value of $CR$ must be less than or equal to 0.1 to be considered valid. To compute $CR$, start by approximating the largest eigenvalue $\lambda$ of the comparison matrix. Then calculate the consistency index $CI$ with

$$CI = \frac{\lambda - n}{n - 1}.$$

Finally, $CR = CI/RI$, where $RI$ is the *random index* (from [Saaty1980]) found from

| $n$ | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| $RI$ | 0.0 | 0.0 | 0.58 | 0.90 | 1.12 | 1.24 | 1.32 | 1.41 | 1.45 | 1.49 |

If $CR > 0.1$, we must go back to our pairwise comparisons and repair the inconsistencies. In general, consistency ensures that if $A > B$ and $B > C$, then $A > C$ for all $A$, $B$, and $C$.

**STEP 3.** Combine all the alternative comparison eigenvectors into a matrix, then multiply by the criteria matrix’s eigenvector to obtain an overall comparative ranking.

**STEP 4.** After the $m$ criterion weights are combined into an $n \times m$ normalized matrix (for $n$ alternatives by $m$ criteria), multiply by the criteria ranking vector to obtain the final rankings.

**STEP 5.** Interpret the order presented by the final ranking.