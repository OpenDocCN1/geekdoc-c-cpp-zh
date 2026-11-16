$$ \frac{1}{E_{N_m}(z)} = \sum_k p[k] z^{-k}, \quad |z| = 1. $$ 
 (7.59)

It can be shown that

(7.60) 
 $$ p[k] = u_m \sum_{i=1}^{p_m} \Lambda_i \lambda_i^{k+p_m}, \quad k \ge 0; $$

where

(7.61) 
 $$ \Lambda_i = \frac{1}{\lambda_i \prod_{j=1, j \neq i}^{2p_m} (\lambda_i - \lambda_j)} $$

and $\lambda_i : i = 1, \dots, 2p_m$ are the roots of (7.54) with $|\lambda_i| < 1$ and $\hat{\lambda}_i \hat{\lambda}_{2p_m+1-i} = 1$ for $i = 1, \dots, p_m$. Here $u_m = (2m-1)!$ and $p_m = m-1$. Observe from (7.54) and (7.59) that

(7.62) 
 $$ \sum_k p[k] = \frac{1}{E_{N_m}(1)} = \sum_{k=-m+1}^{m-1} \frac{1}{N_{2m}(m+k)} = 1, $$

where the last equality is a consequence of the partition of unity property of cardinal $B$-splines, described in Chapter 5.

Roots $\lambda_i$ for linear and cubic splines are given below. The coefficients $\{p[k]\}$ are given in Tables 7.1 and 7.2. The