# 10.4.2 Dual formulation as vertex weights

Instead of examining equilibrium through the lens of edge weights, one may instead attack the problem from the perspective of the discrete Airy stress surface S. Here we can make an important observation: when a thrust network top view M is simply connected and has purely triangular faces, then all discrete convex functions S on M are valid discrete Airy stress surfaces on M, since S automatically has planar faces. To each such S must be associated a reciprocal diagram, which in this case is the power diagram [19] (see Section 9.2.1) with vertex weight $r_i$ at $\bar{\mathbf{v}}_i$ given by

$$r_i = \frac{1}{2} \| \mathbf{v}_j \|^2 - \frac{1}{2} s_i.$$

Some sets of edge weights do not correspond to valid reciprocal diagrams, and hence Airy stress surfaces (if they do not satisfy (10.2)) and many sets of edge weights can give the same Airy stress surface. On the other hand, the vertex weights $s_i$ form a reduced basis for the valid Airy stress surfaces, an observation that de Goes et al. [113] and Liu et al. [255] leveraged into efficient algorithms for finding equilibrium thrust networks $M'$ approximating a designed network M.

Given M, the algorithm seeks $S_i$ and heights $z_i$ satisfying the vertical equilibrium condition (10.3) while keeping the $z_i$ as close as possible to their designed values; de Goes et al. [113] propose to penalize displacements of $z_i$ more for vertices initially closer to equilibrium. The compression-only constraint, that S is convex, becomes a set of linear inequality constraints encoding that every edge of S is a convex edge. The algorithm can be easily modified to handle the more general case where M has holes, and S exists only locally. It can also be augmented to allow sliding of the top view vertices, using edge flips to keep M a regular triangulation [255].

# 10.4.3 Perfect Laplacian optimization

Recall that equilibrium of M is equivalent to the existence of a perfect Laplacian (10.2) on the top view $\bar{M}$ for which vertical heights of the network vertices satisfy a Poisson equation (10.3). Herholz et al. [187] studied perfect Laplacians on polygonal meshes and developed a different approach to finding an equilibrium thrust network $M'$ given a guess M. The key insight is that a current guess for the weights $w_{ij}$, together with the specified supported boundary vertex positions and the external loads, uniquely determine heights $z_i$ of a thrust network $M'$ in equilibrium, with $\bar{M} = \bar{M}'$, via (10.3). Comparing edge lengths of $M'$ to M suggests that the edge weights should be updated as

$$u_{ij}^{k+1} = u_{ij}^k \frac{\| \mathbf{v}_i^k - \mathbf{v}_j^k \|}{\| \mathbf{v}_i - \mathbf{v}_j \|},$$

where $u_{ij}^k$ and $\mathbf{v}_i^k$ are the edge weights and vertex positions at the k-th iteration of the algorithm. This process is repeated until convergence of $M'$.