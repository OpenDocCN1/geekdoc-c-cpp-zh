# **Theorem 10.3.** A thrust network $G$ with simply connected top view $\bar{G}$ is in equilibrium if and only if there exists a discrete Airy stress surface $S$ over $\bar{G}$ with

```
-F_i/A_i = 2K_g^S(v_i) H \vec{G}_S^\nabla(v_i) \quad (10.8)
```

at interior vertices $v_i$, with faces of $S$ abutting consecutive pieces of free boundary coplanar.

Here, $F_i/A_i$, like $F/\sqrt{\det g}$ in (10.6), should be interpreted as a load density over the top view rather than the thrust surface itself.

# ## 10.4 OPTIMIZING FOR STABILITY

We now have the theoretical pieces necessary to formulate some algorithms for solving inverse problems related to stable masonry. In its simplest form, the inverse problem asks: given a thrust network $M$, is it in equilibrium? If not, what changes must be made to $M$ so that it is now in equilibrium? Once such a network is found, a masonry structure can be built that is adapted to the shape of the thrust network, as described in Section 10.3.2.

The first question can be answered by looking for non-negative edge weights $w_{ij}$ that satisfy equation (10.1). If such weights do not exist, some modification must be made, either to the combinatorics of $M$, or to its geometric shape, in order for it to become stable.

# ### 10.4.1 Alternating optimization

If a thrust network is not stable, one can still look for weights that satisfy equilibrium as much as possible, in the sense of minimizing the residual force at each node of the thrust network,

```
\(\arg \min_{w_{ij} \ge 0} \sum_i \left\| \mathbf{F}_i - \sum_{j \sim i} w_{ij} (v_i - v_j) \right\|^2, \quad (10.9)\)
```

where the sum is taken over all interior and free boundary vertices of $M$. This optimization amounts to solving a least squares problem with nonnegativity constraints on the variables, for which there exist specialized solvers [234].

One could now fix the weights $w_{ij}$ and solve for displacements of the vertices of the thrust network that minimize the force residual; since this is a square system of linear equations, it usually has a solution. While the resulting thrust network $M'$ would be in equilibrium, there is no guarantee that $M'$ is at all similar in shape to $M$, and in practice it is not, particularly if the initial network $M$ was far from equilibrium. Vouga et al. [405] proposed an *alternating minimization* that repeatedly solves for the $w_{ij}$, while allowing the thrust network to slowly relax away from $M$: