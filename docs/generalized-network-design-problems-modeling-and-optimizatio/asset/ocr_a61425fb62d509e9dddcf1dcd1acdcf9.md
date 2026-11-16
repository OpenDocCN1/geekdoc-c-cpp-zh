with respect to the edges and to the nodes, respectively, and, as before, \(W' \subset W^* = \{i \in V | z_i^* \ge \frac{1}{\rho}\}\), such that \(|W'| = m\) and \(W'\) consists of exactly one vertex from every cluster.

For the approximation algorithm proposed in this case, the following holds:

APP = \(L^T(W') + V^T(W') \le \rho \left(2 - \frac{2}{n}\right) L_{OPT} + \rho V_{OPT}\)
\(\le \rho \left(2 - \frac{2}{n}\right) (L_{OPT} + V_{OPT}) = \rho \left(2 - \frac{2}{n}\right) OPT.\)

In the case of the at least generalized minimum spanning tree problem, Femermans et al. [41] considered a geometric case of the problem, where the graph is complete, all vertices are situated in the plane and the Euclidean distance between the vertices defines the edge cost. This special case of the problem, with the clustering structured as specified, is called grid clustering.

For the case of the grid clustering, the same authors proved that the problem is strongly NP-hard, they provided an exact exponential time dynamic programming algorithm, and based on this algorithm, they developed a polynomial time approximation scheme, namely if \(T^{APPX}\) is the generalized spanning tree, constructed in polynomial time, using the dynamic programming algorithm, then the following result holds:

# Theorem 2.17 (Femermans et al. [41]).

\(\frac{c(T^{APPX}) - c(T^{OPT})}{c(T^{OPT})} \le \epsilon.\)

# 2.5 Solving the GMSTP

Myung et al. [128] used a branch and bound procedure in order to solve the GMSTP. Their lower procedure is a heuristic method, which approximates the linear programming relaxation associated with the dual of the multicommodity flow formulation of the GMSTP. They also developed a heuristic algorithm, which finds a primal feasible solution for the GMSTP, using the obtained dual solution and they reported the exact solution of instances with up to 100 vertices. The GMSTP was solved to optimality for nodes up to 200 by Femermans [37], using a branch-and-cut algorithm. More recently, Pop et al. [150] have proposed a new integer programming formulation of the GMSTP, based on a distinction between local and global variables and a solution procedure that finds an optimal solution on instances with up to 240 vertices.

The difficulty of obtaining optimum solutions for the GMSTP has led to the development of several metaheuristics. The first such algorithms were the tabu search (TS) heuristic of Femermans [37] and the simulated annealing (SA) heuristic of Pop [142]. An improved version of the SA was described in [154]. Two variants of the TS