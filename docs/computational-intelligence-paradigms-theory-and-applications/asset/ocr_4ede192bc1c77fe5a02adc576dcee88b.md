```
End For
Update the trail pheromone intensity for every edge (i, j)

τ_ij(t) = ρτ_ij(t − 1) + Σ_{k=1}^{n} Δτ_ij^k(t) ∀(i, j)

Δτ_ij^k(t) = { Q/L_k(t)  if the edge (i, j) chosen by ant_k
                0          otherwise }

Compare and update the best solution
End For
End While
```

# 15.9 Studies and Applications of Swarm Intelligence

In this section a few illustrations based on scientific and engineering swarm intelligence studies are given.

# 15.9.1 Ant-based Routing

Dorigo et al. and Hewlett Packard during the mid-1990's applied Swarm Intelligence to the field of Telecommunication Networks and referred this as Ant Based Routing. The application involves a probabilistic routing table rewarding or reinforcing the route successfully traversed by each "ant" (a small control packet). Reinforcement of the route in the forward, reverse direction and both simultaneously have been studied and analyzed in their research. A symmetric network is used for backward reinforcement, which couples the network bidirectionally. The forward reinforcement rewards a route before the outcome is known.

# 15.9.2 Clustering Behavior of Ants

The main idea of the clustering algorithm based on swarm intelligence was proposed by Deneubourg. The process of clustering is defined in three stages. In the first stage, the data objects are chosen at random and are projected onto a low dimensional space. During the second phase, simple agents perceive the swarm similarity of the current object with the local region, and compute the probability of pick-up and drop. And