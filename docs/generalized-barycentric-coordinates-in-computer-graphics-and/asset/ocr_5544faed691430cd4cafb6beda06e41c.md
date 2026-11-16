![](bbox=[0.16, 0.11, 0.83, 0.3])

Figure 7.4 Blending edge-to-edge affine maps. A source cage of a pants shape in (a) is deformed identically in (b) and (c) to create an effect of legs stretching. In (b) the edge-to-edge affine maps are chosen to be similarities. The map from (a) to (b) is the holomorphic Cauchy barycentric map. In (c) the edge-to-edge affine maps stretch only in the direction of the edges but not in the orthogonal direction, resulting in a non-holomorphic map with a more natural look that better approximates the target cage. See color insert.

Planar affine maps $A(z) = az + b\bar{z} + c$ have three complex degrees of freedom $a, b, c \in \mathbb{C}$. Two are nailed down by the requirement to map the source edge endpoints to the target ones, $A(z_i) = f_i$ and $A(z_{(i+1)}) = f_{(i+1)}$. The third degree of freedom controls the behavior of the map in the direction orthogonal to the edge. Let $e_i = z_{i+1} - z_i$ and $\hat{e}_i = f_{i+1} - f_i$, then the (unnormalized) normals to the source and target edges are $n_i = ie_i$, and $\hat{n}_i = i\hat{e}_i$. We require that $A_i$ transforms the vector $n_i$ to the vector $\rho \hat{n}_i$, where $\rho_i \in \mathbb{C}$, and it turns out that the edge-to-edge affine maps can be expressed as

```
$A_i(z) = f_i - \frac{(\rho_i + 1)\hat{e}_i B_i(z)}{2e_i} + \frac{(\rho_i - 1)\hat{e}_i \overline{B_i}(z)}{2\hat{e}_i}$.
```

If $\rho_i = 1$, then the anti-holomorphic term on the right-hand side above vanishes and $A_i(z) = S_i(z)$. An alternative choice is to use $\rho_i = |c_i|/|\hat{e}_i|$, which maps the source normal to a vector that is orthogonal to the target edge while maintaining its length. This encourages the map to allow stretch only in the direction tangential to the boundary. Figure 7.4 shows a comparison between two types of maps having $\gamma_i = \text{Log}(\frac{\rho \hat{e}_i}{e_i})$. The first map uses $\rho_i = 1$, and is hence identical to Cauchy's coordinates, while the second map uses $\rho_i = |e_i|/|\hat{e}_i|$.

# 7.2.3 Magic coordinates

In the previous section we showed how to construct complex barycentric coordinates based on arbitrary weight functions $\gamma_i$. Since the similarity transformations $S_i$ are holomorphic functions, it is clear that if $\gamma_i$ are holomorphic, then the complex barycentric map (7.17) is also holomorphic. Obviously, there exist complex