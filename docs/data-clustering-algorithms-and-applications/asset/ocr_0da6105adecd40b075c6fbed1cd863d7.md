# 420 Data Clustering: Algorithms and Applications

inertia. In a convex domain, this axis aligns itself with the shape of the mesh and the spatial extend in the directions orthogonal to the axis is minimized. This usually results in a minimized cut-size.

# 17.5.3 Geometric Partitioning

Miller et al. introduced the method in [115] that for certain graphs, a vertex separator divides the graph into two roughly equal sizes with high probability. The following definitions are necessary in order to state the theorem given in [115].

**Definition 17.5.1** A $k$-ly neighborhood system in $d$ dimensions is a set $D_1, D_2, ..., D_n$ of closed disks in $\mathbb{R}^d$ such that no point of $\mathbb{R}^d$ is strictly inner to more than $k$ disks.

**Definition 17.5.2** An $(\alpha, k)$-overlap graph is defined in terms of a $k$-ly neighborhood system $D_1, D_2, ..., D_n$ and a constant $\alpha \geq 1$. Each closed disk $D_i$ is represented by a vertex and there is an edge between two vertices if expanding the radius of the smaller disks by a factor of $\alpha$ causes the disks to overlap. Mathematically,

```
$E = \{i, j | \alpha D_i \cap D_j \neq \emptyset and \alpha D_j \cap D_i \neq \emptyset\}$
```

A regular $b$-n graph is a (1,1)-overlap graph. The theorem given in [115] is as follows:

**Theorem 1** Given $G = (V', E)$, an $(\alpha, k)$-overlap graph in $d$ dimensions with $n$ nodes, there is a vertex separator $V_s$ such that $V' = V_1 \cup V_s \cup V_2$ with the following properties:

+   1. $V_1$ and $V_2$ each have at most $(n+1)/(d+2)$ vertices,
2. $V_s$ has at most $O(\alpha^k n^{(d-1)/(d-)})$ vertices,

Where $\mathcal{}$ represents union, i.e., $\mathcal{U} \cup \mathcal{V} = \mathcal{U}$ and $\mathcal{U} \cap \mathcal{V} = \emptyset$. The separator size given by the theorem is "asymptotically optimal" for regular meshes in simple geometric shapes.

The proof of the theorem leads to a randomized algorithm running in linear time that will find a d-dimensional sphere defines the separator and the algorithm randomly chooses the separating circle from a distribution that, with high probability, satisfies the conclusions of the theorem. We will now define some terminologies before describing the algorithm.

A *stereo-projection* is a mapping of points in $\mathbb{R}^d$ to the unit-sphere centered at the origin in $\mathbb{R}^{d+1}$.

The *center-point* of given set of points in $\mathbb{R}^d$ is such that every hyperplane through the center-point divides the set into two halves so that the disks divide it by a maximum ratio of $1d$. The algorithm is as follows:

**Algorithm 36** Geometric Bisection
**Project up**: Stereographically project points from $\mathbb{R}^d$ to unit-sphere in $\mathbb{R}^{d+1}$n**Find Centerpoint**: Find centerpoint of the projected points
**Conformal Map**: Map the points on sphere so that the centerpoint lies at the origin; that is, to rotate the sphere around the origin and then dilate so that the new centerpoint lies in the origin
**Find great circle**: Intersect the $S^{d+1}$ with a random $d$-dimensional hyperplane through the origin
**Unmap**: Unmap the great circle to a circle $C$ in $\mathbb{R}^d$ by inverting the dilation, rotation, and stereographic projection
**Find Separator**: A *point separator* is found by choosing all points whose corresponding disk, magnified by a factor of $\alpha$, intersects C

© 2014 by Taylor & Francis Group, LLC