![](bbox=[0.18, 0.11, 0.82, 0.61])

Figure 12.12 For loading condition (i), displaying pure shear with average deformation gradient $(F) = \lambda e_1 \otimes e_1 + \lambda^{-1} e_2 \otimes e_2, \lambda \ge 1$, the figure illustrates the final deformed configuration reached by (a) $\mathcal{M}_2 - \mathcal{M}_1$ elements, (b) $\mathcal{M}_2 - \mathcal{P}_1$ elements, (c) $\mathcal{M}_1 - \mathcal{P}_0$ elements, and (d) CPE6HM elements (solved in ABAQUS). This figure is adapted from [100]. See color insert.

following stored-energy function [259]

```
W(F) = \begin{cases} \frac{3^{1-\alpha_1}}{2\alpha_1} \mu_1 [I_1^{\alpha_1} - 3^{\alpha_1}] + \frac{3^{1-\alpha_2}}{2\alpha_2} \mu_2 [I_2^{\alpha_2} - 3^{\alpha_2}], & \text{if } \det F = 1, \\ +\infty, & \text{otherwise,} \end{cases}
```

with $I_1 = F_{ij}F_{ij}, \mu_1 = 0.032$ MPa, $\mu_2 = 0.3$ MPa, $\alpha_1 = 3.837, \alpha_2 = 0.559$. Thus, the initial shear modulus of the matrix is $\mu_m = \mu_1 + \mu_2 = 0.332$ MPa, and that of the interphase is $\mu_i = 3.32$ MPa. Again, both loading conditions (i) and (ii) are considered.