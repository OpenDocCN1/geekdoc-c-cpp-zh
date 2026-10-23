![](bbox=[0.22, 0.14, 0.75, 0.42])

# Figure 17.3. The domain decomposition. The bullets denote nodes in the coarse grid c.

![](bbox=[0.25, 0.51, 0.78, 0.78])

# Figure 17.4. The first prolongation step, in which the known values at the bullets are prolonged to the line connecting them by solving a homogeneous subproblem in the strip that contains this line.

In the domain-decomposition approach, the original domain is viewed as the union of disjoint subdomains. The vertices of these subdomains form the coarse grid c (Figure 17.3). The prolongation operator P consists of two steps: the first step extends a vector defined on c to the nodes that lie on the edges of subdomains, and the second extends it further to the interiors of the subdomains.

For a given coarse-grid vector v, the first prolongation step produces the values of the extended vector Pv at nodes that lie on the edges of the subdomains (between coarse-grid nodes). The second prolongation step uses these values as Dirichlet data to solve a homogeneous PDE in each individual subdomain (Figure 17.5). The numerical solution of these subproblems produces Pv in the interiors of the subdomains as well. Because these subproblems are independent of each other, they can be solved simultaneously in parallel.

The first prolongation step, which extends v to the edges in Figure 17.3, is trickier than the second one. Clearly, it should use the original values of v at the endpoints of each edge as Dirichlet data for a one-dimensional equation in this edge. However, it is not clear how this one-dimensional equation should be defined.