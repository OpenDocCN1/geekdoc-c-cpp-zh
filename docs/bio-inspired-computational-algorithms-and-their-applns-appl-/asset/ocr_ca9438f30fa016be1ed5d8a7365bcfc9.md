```
line-crossover(x,y)
{
  λ ← a random real number in [0,1];
  for i ← 1 to n
    z_i ← λx_i + (1 − λ) y_i;
  return z = (z1,z2,...,zn);
}
```

Fig. 4. Pseudo-code of line crossover

```
extended-line-crossover(x,y)
{
  m ← −∞, M ← ∞;
  for i ← 1 to n
    if x_i ≠ y_i
      t_i ← (l_i − y_i)/(x_i − y_i), t_u ← (u_i − y_i)/(x_i − y_i);
      t_m ← min(t_i,t_u), t_M ← max(t_i,t_u);
      m ← max(m,t_m), M ← min(M,t_M);
  λ ← a random real number in [max(m−α), min(M,1 + α)];
  for i ← 1 to n
    z_i ← λx_i + (1 − λ) y_i;
  return z = (z1,z2,...,zn);
  // α is extension rate.
}
```

Fig. 5. Pseudo-code of extended-line crossover

The most common form of mutation for real-code vectors generates an offspring vector by adding a vector M of random variables with expectation zero to the parent vector. There are two types of mutations bounded and unbounded depending on the fact that the range of the random variable is bounded or unbounded. The most frequently used bounded mutations are the creep mutation and the single-variable mutation and for the unbounded case is the Gaussian mutation. For the creep (or hyper-box) mutation M ∼ U[(-a,a)]^n is a vector of uniform random variables, where a is a parameter defining the limits of the offspring area. This operator yields offspring within a hyper-box centered in the parent vector. For the single-variable mutation M is a vector in which all entries are set to zero except for a random entry which is a uniform random variable ∼ U[(-a,a)]. Bounded mutation operators may get stuck in local optima. In contrast, unbounded mutation operators guarantee asymptotic global convergence. The primary unbounded mutation is the Gaussian mutation for which M is a multivariate Gaussian distribution.

# 2.2 Adopted operators for this study

As crossover operators for our analysis, we adopted four representative crossovers: box, extended-box, line, and extended-line crossovers. Their pseudo-codes are shown in Figures 2, 3, 4, and 5, respectively and the possible range for each crossover is represented in Figure 1.