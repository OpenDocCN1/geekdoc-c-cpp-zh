techniques apply to problems of sewer systems, freshwater networks, irrigation systems, as well as traffic networks.

We depart from a full space–time formulation of the problem with both discrete and continuous controls. After that we discretize the problem with respect to time using a simple implicit Euler step, for the sake of brevity. The corresponding optimal control problem, which still involves all time-steps is then reduced to what has come to be known as an instantaneous control problem that is defined on a single time-step, thereby decoupling the time history. The resulting optimal control problem can be viewed as a nonlinear (semi-linear or even linear) elliptic optimal control problem on the network. The network, in turn, is then decomposed into small subnetworks even to single links. As a result, at the core of the approach, elementary problems can be solved very effectively.

Clearly, in this chapter, we can only indicate the procedure and refer to mathematically rigorous results from the literature whenever possible and feasible.

To this end, we consider the Euler equations consisting of the continuity equation, the balance of moments, and the energy equation. (cf. [1, 2, 3, 4]) We denote by ρ the density, by v the velocity of the gas, and by p the pressure. We define λ as the friction coefficient of the pipe, D the diameter, a the cross section area. The unknowns of the system are given by ρ and the flux q = aρv. We also denote by c with c² = ∂p/∂ρ (for constant entropy) the speed of sound. For horizontal pipes

```
∂ρ/∂t + ∂/∂x (ρv) = 0
∂/∂t (ρv) + ∂/∂x (p + ρv²) = - λ/(2D) ρv|v|.
(2.1)
```

In the particular case, where we have a constant speed of sound c = √(p/ρ), for small velocities |v| ≪ c, we arrive at the semi-linear model

```
∂ρ/∂t + ∂/∂x (ρv) = 0
∂/∂t (ρv) + ∂p/∂x = - λ/(2D) ρv|v|.
(2.2)
```

# 2.1.2 Network Modeling

Let G = (V, E) denote the graph of the gas network with vertices (nodes) V = {n_j : j ∈ 𝒥, |𝒥| = |V|} and edges E = {e_i : i ∈ ℐ, |ℐ| = |E|}. We associate to each edge a direction. To this end, we introduce the edge-node incidence matrix

```
d_ij = { -1, if node n_j is the left node of the edge e_i,
          +1, if node n_j is the right node of the edge e_i,
          0,  else. }
```

In contrast to the classical notion of discrete graphs, the graphs considered here are known as metric graphs, in the sense that the edges are continuous curves. In fact, we consider here straight edges, along which differential equations hold. The index set of all edges incident