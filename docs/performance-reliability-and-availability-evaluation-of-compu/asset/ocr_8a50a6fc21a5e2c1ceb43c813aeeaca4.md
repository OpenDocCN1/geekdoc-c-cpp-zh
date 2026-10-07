# Performance, Reliability, and Availability Evaluation of Computational Systems

![](bbox=[0.137, 0.103, 0.863, 0.347])

Figure 18.25 System Redundancy and Component Redundancy

which is simplified to

$R_{S2}(t) = (R_a(t)-2)R_a(t)(R_b(t)-2)R_b(t)$.

Let us consider the relation

$R_{S1}(t) = rac{(R_a(t)-2)R_a(t)(R_b(t)-2)R_b(t)}{R_a(t)R_b(t)(2-R_a(t)R_b(t))}$

Applying some algebra yields

$$\frac{(R_a(t)-2)(R_b(t)-2)}{2-R_a(t)R_b(t)} = (18.6.1)$

$$\frac{R_a(t)R_b(t)-2R_a(t)-2R_b(t)+4}{2-R_a(t)R_b(t)} =$

$$\frac{R_a(t)R_b(t)-2(R_a(t)+R_b(t))+4}{2-R_a(t)R_b(t)} =$$

$R_a(t) \times R_b(t)-2\times(R_a(t)+R_b(t))+4-2\times(R_a(t) \times R_b(t))-2+2\times R_a(t) \times R_b(t)+2 = \frac{2}{2-R_a(t) \times R_b(t)}$