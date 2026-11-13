```
...
narrowband.insert(DT[n.i][n.j],n);
//Compute one-point feature transform
float dmin = DIST.MAX+DIST.MAX;
for (all Points q neighbors of n)
{
    if (state[q.i][q.j]==Known) continue ;
    Point c = from(FT[q.i][q.j]);
    int d = (c.i-n.i)*(c.i-n.i)+(c.j-n.j)*(c.j-n.j);
    if (d<dmin) continue ;
    dmin=d; FT[n.i][n.j]=FT[c.i][c.j];
}
...
```

# Listing 9.6. One-point feature transform.

a pixel close to or on the skeleton will always have a different feature point than its neighbors. In order to prevent computing a two-pixel-thick skeleton, we only consider the right and lower neighbors \(n_R, n_L\) (or the upper and left ones) instead of all four.

The third and final step in the skeleton computation is to build in a multiscale representation of the shape. For a skeleton pixel \(p\), we notice that the further apart two features \(f_i, f_j \in \{FT(p), FT(n_R), FT(n_L)\}\) are, the more central to the skeleton the position of \(p\) is. Hence, we can define the importance \(\rho(p)\) as
\(\rho(p) = \max [\text{dist}(u(FT(n_R)), u(FT(p))), \text{dist}(u(FT(n_L)), u(FT(p)))] , \quad (9.42)\)

where \(u: \partial\Omega \to \mathbb{R}_+\) is an arc-length boundary parameterization and \(\text{dist}(a,b) = \min(|a-b|, \frac{|\partial\Omega|}{2})\) is the shortest distance along the boundary between two points. Implementing the complete skeletonization method starting from the fast marching code (see Listing 9.5), the one-point feature transform addition (see Listing 9.6) and the skeleton detector and importance measure \(\rho\) (Equation (9.42)) are left as an exercise for the reader.

The measure \(\rho\) in Equation (9.42) defines the importance of a skeleton point as being the maximal shortest distance along the boundary \(\partial\Omega\) between two feature points of \(p\). Note that this importance measure only holds for shapes of genus zero; that is, shapes without holes. For example, the importance of the skeleton point \(p\) in Figure 9.12(a) equals the length of the upper leaf lobe delimited by the boundary points \(q_1\) and \(q_2\). If we want to compare the importances of skeletons of different objects, we can normalize \(\rho\) in the range \([0, 1]\) by dividing it by half the boundary length \(|\partial\Omega|/2\).